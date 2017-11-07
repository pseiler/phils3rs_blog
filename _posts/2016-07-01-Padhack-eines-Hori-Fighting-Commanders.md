---
layout: post
title: Padhack eines Hori Fighting Commanders

categories:
- Technik
- Linux
date: 2016-07-01 17:45:00.000000000 +02:00
---

Aktuell hab ich wieder eine größere Motivation meinen Blog zu betreiben.
Habe für einen Kumpel einen Padhack für seinen aktuellen Arcade Stick installiert.
Mit Padhack ist die Schaltplatine (PCB) eines Gamepads gemeint, welche modifiziert wurde, um sie mit Arcade Hardware zu nutzen. 
Prinzipiell unterscheidet sich das Modding nicht von gewöhnlichen Arcade Stick Umbauten. Der einzige Unterschied besteht darin, dass die Lötstellen für den Kabelbaum im Vorfeld präpariert werden müssen. Außerdem sind die Lötstellen nicht immer perfekt fürs Löten ausgelegt.

Im Falle des hier gewählten [Hori Fighting Commander](https://www.amazon.de/Fighting-Commander-PS4-PS3-PC/dp/B017QORK8W)s muss zuallerst die Plastikschicht der Buttons jeweils abgekratzt werden.
Erfahrungsgemäß geht das am besten mit einem mittelgroßen Schlitzschraubenzieher. Beim abkratzen der (in dem Falle schwarzen) Plastikschicht kann man ruhig etwas fester drücken. Umso heller
und glänzender es wird, umso besser. Sobald das Kupfer sichtbar ist merkt man es schon. Anschließend können die freigekratzten Stellen, mithilfe eines Lötkolbens und Lötzinn, für den eigentlichen
Lötvorgang vorbereitet werden. Wie bei solchen Lötarbeiten üblich, erwärmt man mit dem Lötkolben die zu lötende Stelle ein Weilchen, und fügt dann vorsichtig Lötzinn in Form eines Drahtes hinzu.
Generelle Lötinfos gibt es bei [Slagcoin](http://www.slagcoin.com/joystick/pcb_wiring.html) und mithilfe von Tutorials auf Google und YouTube. 

Hier mal ein Bild der Schaltplatine des aktuellen Hori Fighting Commanders:

![Fighting_Commander_vorbereitet](/images/fighting_commander/fc_teils_vorbereitet.jpg)

Die Schaltplatine funktioniert mit einer gemeinsamen Masse (common Ground). Das heißt, dass jede Datenader mit nur einer gemeinsamen Masselitze auf der Platine den Stromkreis schließt.
Das erleichtert das verkabeln mit einer vorgefertigten Daisy-Chain wie [hier](http://www.arcadeworlduk.com/products/insulated-daisy-chain-harness-with-32-crimp-connections.html) z.B.

Im folgenden Bild seht ihr nochmal die genauen Lötstellen für die Buttons visualisiert in rot und pink.
Rot steht für die Datenlitze des jeweiligen Buttons und pink für eine Lötstelle, an der man Masse/Ground anlöten kann.

Außerdem haben wir noch Schultertasten, von denen wir nur die linken benötigen. 
R1/2 sind bereits als Buttons auf dem Pad verfügbar. Das Kabel entfernt man, indem man die Lötpunkte erhitzt, und nach und nach an den Kabeln zieht.
Am einfachsten tut man sich mit einer [Entlötpumpe](https://de.wikipedia.org/wiki/Entl%C3%B6tpumpe). Bevor man die Kabel jedoch erhitzt, sollte man auch Acht geben, ob evtl. auf der Unterseite noch Heißkleber zur Befestigung abgebracht wurde. Diesen kann man einfach vorsichtig mit der Hand abnehmen.

Bei den drei kleinen Buttons in der Mitte gäbe es jeweils auch noch ein Gegenstück mit einer Lötstelle für Ground, diese ist aber sehr klein und ist deshalb nicht empfehlenswert. Es gibt ja genügend andere
Stellen auf der Schaltplatine, an der Ground angelötet werden kann.
Im folgenden Bild seht ihr alle Lötstellen visualisiert.
![Fighting_Commander_Pin_Layout](/images/fighting_commander/fc_pin_layout.png)

Wurde alles vorbereitet (Schulterbuttons abgenommen, Lötstellen abgekratzt und mit Lötzinn vorbehandelt), kann ganz normal an die Kontakte gelötet werden. Bei den drei mittleren Buttons (PS, Option und Share), muss man anschließend etwas vorsichtig sein, da sonst die Verbindung samt Lötstelle abreißen können(so bei einem PS1 Padhack passiert). Die drei kleinen Lötpunkte kann man bei Bedarf (und nach vorherigem Test) auch mit einer Heißklebepistole zusätzlich fixieren, um das abreissen zu verhinden. Bei allen anderen Lötstellen ist das nicht nötig, da hier die Kontaktstellen groß genug sind.
![Fighting_Commander_geloetet](/images/fighting_commander/fc_geloetet.jpg)

Nicht wundern bei den L Tasten auf dem Bild. Die Äußere (L2) ist falsch gelötet und gehört auf die andere Seite. Leider ist mir das erst aufgefallen, nachdem ich das Foto gemacht hatte. Die Pin Belegung im Bild davor ist aber definitiv richtig. 


Eine generelle Info zu Padhacks findet ihr auf [www.slagcoin.com](http://www.slagcoin.com/joystick/pcb_wiring.html#PCB_DIAGRAMS), sowie deutschsprachig sehr viel im Forum von [Hardedge.org](https://www.hardedge.org) im [Hardware Bereich](https://forum.hardedge.org/index.php?board/11-hardware-technik/) (wird von mir moderiert und gepflegt).
Prinzipiell hab ich den Blogpost geschrieben, weil noch kein Bild vom neuen Fighting Commander verfügbar war.
Viel Spass damit.
