---
layout: post
title: Android - Clockwork Recovery und  "Test Keys"
description: Android ohne Tasten mit adb im Recovery Mode neu starten
categories:
- Android
date: 2013-02-23 17:43:00.000000000 +01:00
---
Ich bin gerade dabei Ubuntu Touch auf mein Nexus 7 zu bespielen um das mal anzuschauen. Dabei bin ich ausversehen im Custom Recovery von Clockwork im *Advanced* Menu auf *Test Keys* gekommen. Da das Nexus 7 keine Hardwaretasten außer **Lauter/Leiser** und den **Einschaltknopf**, hab ich zuerst keinen Weg gefunden, aus dem Testmode wieder rauszukommen.

Die Lösung war: Einfach USB Kabel rein und auf dem Terminal
{% highlight bash %}
sudo adb start-server
adb reboot
{% endhighlight %}
einzugeben.
(Den  adb Server muss man nicht als Root starten, wenn man Udev Regeln für die Geräte erstellt hat. Wird hier nur der Vollständigkeit halber erwähnt)
Dazu benötigt man aber das Android SDK mit den platform-tools. Darin enthalten ist das Kommandozeilenprogramm **adb** (Android Debugging Bridge).
Gibt es für Linux, Windows und MacOSX.

Anleitungen für die Installation des SDK gibt es zahlreich im Internet für alle genannten Plattformen.
