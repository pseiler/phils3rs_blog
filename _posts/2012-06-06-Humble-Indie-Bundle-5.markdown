---
layout: post
title: Humble Indie Bundle #5
description: Linux Hilfe um die Spiele aus dem Humble Indie Bunlde #5 zum laufen zu bringen
categories:
- Gaming
date: 2012-06-06 16:34:00.000000000 +02:00
---
Ich habs mir natürlich nicht nehmen lassen, diesmal nicht auch beim [Humble Indie Bundle #5](https://www.humblebundle.com/) mitzumachen. Diesmal sind echt grandiose Games mit bei. Das wären:

* **Psychonauts**
* **Bastion**
* **Superbrothers: Swords and Sorcery EP**
* **Amnesia: The Dark Descent**

Weil das Ding so gut eingeschlagen ist, kamen auch drei neue Spiele hinzu:

* **Super Meat Boy**
* **Lone Survivor**
* **Braid**

Limbo ist auch dabei, nur bin ich von diesem Spiel maßlos enttäucht. Hab mir das vor einiger Zeit mal ausm Netz gezogen und unter Wine nicht zum laufen gebracht. Mit Psychonauts war das der Titel auf den ich mich am meisten gefreut hatte, und was bekomm ich jetzt da? Ein Windows Spiel mit wine draufgepackt, das beim starten schon eine Windows/Wine Meldung auslöst.
Eine Code Portierung hätte schon drin sein müssen, anstatt diesem ekligen "workaround". Ansonsten schaffen es doch alle anderen Indie Spiele Firmen ihre Spiele auf Linux zu portieren.

Aber genug gegen den Entwicklern hinter Limbo geflamed, ich will euch noch nen weiteren Aspekt des Humble Bundle unter Linux erzählen.
Ich hab einen Laptop mit Intel Grafikkarte und einem openSUSE 12.1. Funktioniert alles wunderbar. Nur macht die Grafikkarte und der Treiber bei openGL öfters zicken. 
Ich lade mir also das erste Spiel "Bastion" runter installier es, samt schöner RPM und will nun starten. Fehlanzeige zuerst kommt das "WB" logo und die Entwicklerfirma, dann das ganze Display ist schwarz. Naja erst Mal egal.
Probierst ein anderes Spiel. Psychonauts bricht mit folgender Fehlermeldung auf der Kommandozeile ab.
{% highlight bash %}
ERROR: Missing required OpenGL extensions:
- GL_EXT_texture_compression_s3tc
{% endhighlight %}
Bei Amnesia ähnliches Spiel. Beim Laden der Engine ein segfault.

So läuft erst Mal nur Superbrothers: Swords and Sorcery EP out of the box.
Das wirkt aber auf dem ersten Blick nur mäßig interessant.

Nach ein bisschen googlen, finde ich raus das es bei allen Spielen am selben Problem liegt. Eine openGL Bibliothek fehlt, da diese patentgeschützt ist. Anscheinend kann man diese mit boardmitteln erzwingen, wenn man eine Umgebungsvariable beim start setzt.
Das funktioniert in den Fällen Psychonauts und Bastion so.
{% highlight bash %}
force_s3tc_enable=true /usr/local/games/psychonauts/Psychonauts
{% endhighlight %}

Für Bastion muss man natürlich den Pfad zur Binary austauschen. 
Amnesia startet trotzdem nicht verfünftig.
Die fehlende patentgeschützte GL Library wird anscheinend auch als open-source entwickelt und ist für openSUSE hier zu finden.
[Packman 1-Click Link](http://packman.links2linux.de/package/libtxc_dxtn)

Für andere Linuxdistributionen müsst ihr einfach mal nach "libtxc" suchen. Da findet sich auf jeden Fall was, oder ihr kompiliert euch die Library selbst.
[Libtxc_dxtn Projekt Seite](http://cgit.freedesktop.org/~mareko/libtxc_dxtn/)
Nachdem die Library installiert wurde, hab ich allle Spiele nochmal gestartet und seitdem funktionieren jedes Spiel mit Intel Grafik und Mesa, auch wen die Performance aufgrund der Grafikhardware nur mäßig ist.

Die drei neuen Spiele laufen auch alle out-of-the-box. Somit hat sich der Kauf des Humble Indie Bundle #5 wirklich gelohnt. Die meisten Spiele werde ich dann nur auf dem Tower genießen können, aber für 12.50€ war es den Kauf mehr als wert.
