---
layout: post
title: LightDM Windowmanager startet nicht beim Boot
description: Lösung zum Problem, dass Lightdm nicht beim Boot startet (unter openSUSE). gdm deinstalliert hilft.
categories:
- Technik
- Linux
date: 2017-11-23 17:11:00.000000000 +02:00
---

Heute habe ich ein schon lange existierendes Problem gelöst, welches mich tierisch aufgeregt hat. Unter openSUSE nutze ich schon eine gefühlte Ewigkeit den [i3wm](https://i3wm.org/) zusammen mit [LightDM](https://www.freedesktop.org/wiki/Software/LightDM/) als Displaymanager. Das hat bisher auch tadellos funktioniert, nur hat er gefühlt seit der Installation auf openSUSE Leap 42.1 nicht mehr zuverlässig funktioniert. Das hat sich so geäußert, dass LightDM manchmal nicht startet, manchmal aber schon. Manchmal startet LightDM, aber er will den Windowmanager nach dem einloggen nicht starten.

Wie ich soeben herausgefunden habe, funkt der [gdm](https://wiki.gnome.org/Projects/GDM) (welcher noch installiert war) dazwischen. Manchmal bekommt man diese Fehlermeldung in */var/log/lightdm/seat0-greeter.log*.

{% highlight bash %}
Invalid MIT-MAGIC-COOKIE-1 keyUnable to init server: Could not connect: Connection refused
(lightdm-gtk-greeter:3332): Gtk-WARNING **: cannot open display: :0
{% endhighlight %}

Die einfache Lösung war, alles was mit dem **gdm** zu tun hat, zu deinstallieren. 

{% highlight bash %}
user$ sudo zypper rm gdm gdm-branding-openSUSE typelib-1_0-Gdm-1_0
{% endhighlight %}
Auf die Idee hat mich folgender Link [(klick mich)](https://askubuntu.com/questions/74551/lightdm-not-starting-on-boot#84485) gebracht, der den passenden Hinweis geliefert hat. Das googlen nach der Fehlermeldung weiter oben, hat mich immer zu ganz anderen Fehlerursachen geführt. Entweder wurde LightDM falsch Konfiguriert, oder es war eine falschen X-Server Konfiguration.
