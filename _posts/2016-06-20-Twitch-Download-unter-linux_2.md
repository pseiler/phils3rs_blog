---
layout: post
title: Twitch Video Download die zweite (viel einfacher)

categories:
- Technik
- Linux
date: 2016-06-07 17:45:00.000000000 +02:00
---
Nachdem ich ja letztens einen Blogeintrag geschrieben habe, bin ich über einen Kumpel auf das Programm [*livestreamer*](http://docs.livestreamer.io/) aufmerksam gemacht worden. Dieses Programm ist viel einfacher zu nutzen und erfüllt einem fast alle Wünsche. Das Python3 Progrmamm sollte unter jedem Windows, Mac OSX und Linux laufen. Unter openSUSE findet man es z.B. im openSUSE Build Service.

*/e*: Mittlerweile ist das eigentliche Projekt eingeschlafen. Ein anderes Team hat das Projekt geforkt und unter dem Namen [*streamlink](https://streamlink.github.io/) weiterentwickelt.

Mit *streamlink* kann man VODs und Streams runterladen und/oder ansehen. Das ist vorallem angenehm, wenn man den Stream nicht im Browser schauen möchte, sondern direkt im Media Player. Als netten Nebeneffekt, kann der Stream oder eben das VOD runtergeladen werden.

Ich habe hier ein paar Beispiele vorbereitet:

Stream von "hardedgeofficial" mit dem Standard Video Player wiedergeben
{% highlight bash %}
user$ streamlink twitch.tv/hardedgeofficial best
{% endhighlight %}

Ein bestimmtes VOD mit dem Standard Video Player wiedergeben
{% highlight bash %}
user$ streamlink twitch.tv/hardedgeofficial/v/69074205 best
{% endhighlight %}

Ein bestimmtes VOD in der Bildauflösung *480p* wiedergeben
{% highlight bash %}
user$ streamlink twitch.tv/hardedgeofficial/v/69074205 480p
{% endhighlight %}

Ein VOD in der Qualität *480p* runterladen und in die Datei *download.mp4* schreiben
{% highlight bash %}
user$ streamlink twitch.tv/hardedgeofficial/v/69074205 480p -o download.mp4
{% endhighlight %}

Die Datei *download.mp4* kann dann für die weitere Bearbeitung genutzt werden. Wie schon im letzten Blogpost, empfehle ich für einfache Schneidearbeiten OpenShot. Dieses Videoschnitt- und Bearbeitungsprogramm hat sich bei mir unter Linux bewährt. 
