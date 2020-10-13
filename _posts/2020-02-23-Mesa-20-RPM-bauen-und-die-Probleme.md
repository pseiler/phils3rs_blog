---
layout: post
title: AMD Radeon RX 5600 XT unter openSUSE mit Mesa 20 und aktuellem Kernel betreiben
description: Möchte man eine AMD Grafikkarte betreiben, welche gerade erst erschienen ist, steht man vor so manchen Problemen. Diese werden hier behandelt
categories:
- Linux
date: 2020-02-24 09:50:00.000000000 +02:00
---

Ich habe mir vor kurzem ein neues Gaming PC Setup zusammengestellt, welches unter anderem die Grafikkarte AMD Radeon RX 5600 XT beinhaltet. Da diese erst vor ein paar Wochen erschienen ist, ist die Unterstützung unter Linux nur mit den neuesten Systemkomponenten möglich. Diese beinhalten:

## Komponenten für eine optimale Unterstützung
* aktueller [Linux Kernel](https://www.kernel.org/) mit Kernel Modul **amdgpu**
* aktuelles [Mesa 20.0.0+](https://mesa3d.org/)
* aktuelles [libdrm](https://dri.freedesktop.org/wiki/) aus dem aktuellsten git Stand kompiliert (gültig bis eine neuere Version als 2.4.100 erscheint)

## Details
### Mesa selbst
Das zusammenspiel aller Komponenten herauszufinden war gar nicht so einfach. Ich selbst nutze ja openSUSE (aktuell 15.1). Den Kernel konnte ich einfach über das Zusatzrepository ***Kernel:Stable*** aktualisieren. Um Mesa musste ich mich leider komplett selbst kümmern, da es zum initialen Zeitpunkt nur einen Release Candidate gab. Gesagt getan. Beim Paketbau der neuen Version bin ich über ein paar selbstverschuldete Fehler gestoßen, die ich nicht weiter erläutern möchte. Allerdings gibt es ein paar Dinge zu beachten. Ich habe die Pakete aktualisiert und alle direkten Abhängigkeiten. Mein erster Fehler, der mich leider wesentlich mehr Zeit gekostet hat als erwartet, war die fehlende Aktualisierung von der Komponente **libgbm**. Diese gehört zur Mesa, hat aber an sich keine direkte Abhängigkeit. Bevor ich diese aktualisiert hatte, startete der XServer nicht, da ***libGLX\_mesa.so*** den Fehler ***undefined symbol: gbm_format_get_name*** zurückgegeben hatte. Erster Fehler beseitigt.

### libdrm
Der zweite Fehler war weitaus kniffliger zu identifizieren. Die Bibliothek ***/usr/lib64/libdrm_amdgpu.so.1*** war zu alt, und hat meine Grafikkarte nicht identifizieren können, da die Vendor ID noch nicht hinterlegt war. Dies hat sich darin geäußert, dass der XServer DRI (Direct Rendering Interface), 3D und 2D Beschleunigung abgeschalten hat, und demnach u.A. kein openGL und Vulkan auf dem System möglich war. Aufgefallen ist mir das durch den Aufruf des Programs **glxinfo**, welches aber eine sehr missverständliche Fehlermeldung ausgab.

{% highlight bash %}
libGL error: MESA-LOADER: failed to open swrast (search paths /usr/lib64/dri/)
libGL error: failed to load driver: swrast
{% endhighlight %}

Dadurch habe ich einen anderen Fehler vermutet, dass er **swrast** nicht laden konnte. Was ich nicht wusste ist, dass **swrast** der Software Renderer ist, welcher nur zum Einsatz kommt, wenn keine Hardware für Hardwarebeschleunigung zur Verfügung steht. Die **swrast** Bibliotheken unter ***/usr/lib64/dri/*** waren nämlich vorhanden. Den Tip bzgl. Software Rendering hat mir ein netter Helfer aus der IRC Community um Mesa gegeben. Darüber und zusätzlich ein wenig auf der Suchmaschine der Wahl suchen, brachte mich auf das Ergebnis, dass es ggf. an libdrm liegen könnte. Dieser [git Commit](https://gitlab.freedesktop.org/mesa/drm/commit/5c8ff5773298bd88b4133ebee2ceeaf193228b52) im Gitlab Projekt hat mich dann auch stutzig gemacht. Leider wurde seit vier Monaten keine neue Version mehr veröffentlicht, daher musste ich den aktuellen git Stand kompilieren. Am Kompilierprozess hat sich nichts geändert, weswegen das bauen eines aktualisierten RPMS kein Problem war. Nach dem Update des Pakets ***libdrm_amdgpu1*** funktionierte dann das Testprogramm ***glxinfo*** auch wieder und meine Grafikkarte ist einsatzbereitt.

Das fertige Repository findet man [hier](https://download.opensuse.org/repositories/home:/seilerphilipp:/mesa/)

Hinzufügen kann man es mit den folgenden Befehlen:

#### openSUSE Leap 15.1
{% highlight bash %}
zypper addrepo -f https://download.opensuse.org/repositories/home:seilerphilipp:mesa/openSUSE_Leap_15.1/ home_seilerphilipp_mesa
{% endhighlight %}

#### openSUSE Leap 15.2
{% highlight bash %}
zypper addrepo -f https://download.opensuse.org/repositories/home:seilerphilipp:mesa/openSUSE_Leap_15.2/ home_seilerphilipp_mesa
{% endhighlight %}

#### openSUSE Tumbleweed
{% highlight bash %}
zypper addrepo -f https://download.opensuse.org/repositories/home:seilerphilipp:mesa/openSUSE_Tumbleweed/ home_seilerphilipp_mesa
{% endhighlight %}

Anschließend kann man mit folgenden Befehlen Mesa und alle relevanten Komponenten aktualisieren
{% highlight bash %}
zypper install --from home_seilerphilipp_mesa Mesa Mesa-libGLESv1_CM1 Mesa-dri Mesa-libGLESv2-2 libOSMesa8 Mesa-libva Mesa-gallium Mesa-libEGL1 Mesa-libOpenCL Mesa-libGL1 Mesa-libglapi0 libgbm1 libdrm_amdgpu1
{% endhighlight %}

Bei Fragen zur Abhängigkeitsauflösung wechselt man den Vendor natürlich auf **home\_seilerphilipp\_mesa**.

Bei Bedarf aktualisiert man die gleichen Pakete mit ***-32bit*** Suffix.
