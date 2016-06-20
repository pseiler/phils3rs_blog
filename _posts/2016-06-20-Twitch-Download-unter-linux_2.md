---
layout: post
title: Twitch Video Download die zweite (viel einfacher)

categories:
- Technik
- Linux
date: 2016-06-07 17:45:00.000000000 +02:00
---
Nachdem ich ja letzten Blogeintrag geschrieben habe, bin über einen Kumpel auf das Programm [*livestreamer*](http://docs.livestreamer.io/) aufmerksam gemacht worden. Dieses Programm ist viel einfacher zu nutzen und erfüllt einem fast alle Wünsche. Das Python3 Progrmamm sollte unter jeden Windows, Mac OSX und Linux laufen. Unter openSUSE findet man es z.B. im openSUSE Build Service.

Mit *livestreamer* kann man VODs und Streams runterladen und ansehen. Das ist vorallem angenehm, wenn man den Stream nicht im Browser schauen möchte, sondern direkt im Media Player. Als netten Nebeneffekt, kann der Stream oder eben der VOD runtergeladen werden.


Ich habe hier ein paar Beispiele vorbereitet:

Stream von "hardedgeofficial" mit dem Standard Video Player wiedergeben
{% highlight bash %}
user$ livestreamer twitch.tv/hardedgeofficial best
{% endhighlight %}

Ein bestimmtes VOD mit dem Standard Video Player wiedergeben
{% highlight bash %}
user$ livestreamer twitch.tv/hardedgeofficial/v/69074205 best
{% endhighlight %}

Ein bestimmtes VOD in der Bildauflösung *480p* wiedergeben
{% highlight bash %}
user$ livestreamer twitch.tv/hardedgeofficial/v/69074205 480p
{% endhighlight %}

Ein VOD in der Qualität *480p* runterladen und in die Datei *download.mpg* schreiben
{% highlight bash %}
user$ livestreamer twitch.tv/hardedgeofficial/v/69074205 480p -o download.mpg
{% endhighlight %}


Die Datei *download.mpg* kann dann für die weitere Bearbeitung genutzt werden. Ich empfehle für einfache Schneidearbeiten OpenShot, wie schon im letzten Post. Dieses Videoschnitt- und Bearbeitungsprogramm hat sich bei mir unter Linux bewährt. 
Ich hoffe ich konnte jemand mit dieser neuen Anleitung ebenfalls Leuten helfen. 
