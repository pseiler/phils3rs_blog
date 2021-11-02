---
layout: post
title: xlock mit Signatur
categories:
- Linux
permalink: /archives/18-xlock-mit-Signatur.html
s9y_link: http://blog.phils3r.de/index.php?/archives/18-xlock-mit-Signatur.html
date: 2013-01-16 13:03:00.000000000 +01:00
---
Ich hab vor längerer Zeit ein tolles Feature für xlock unter Linux gefunden. xlock ist ein sehr minimalistischer Screenlocker, geeignet für xfce4 oder kleine Windowmanager wie z.B. i3.
In der Manpage ist dieses Feature zwar beschrieben, aber ohne Zufall hätte ich dieses Feature wahrscheinlich nie gefunden.

Wenn man in seinem Home Verzeichnis eine Datei namens **.xlocktext**, **.plan** oder wie in meinem Fall **.signature** legt, zeigt er diesen Text untem bein sperren des Bildschirms mit xlock an. Bei mir ist das z.B die Signatur, welche bei mir auch in den Mails verwendet wird. Mein Laptop ist mein Primärarbeitsrechner, dadurch steht das Ding auch mal gesperrt beim Kunden rum. Der kann bei gesperrtem Bildschirm auch sofort anhand der Signatur erkennen wem das Gerät gehört.

Hier nochmal der konkrete Pfad anhand des Beispiels meines Home Verzeichnisses
{% highlight bash %}
/home/philipp/.signature
{% endhighlight %}
