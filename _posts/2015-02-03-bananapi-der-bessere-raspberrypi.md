---
layout: post
title: Banana Pi - der bessere Raspberry Pi?
categories:
- Technik
date: 2015-02-03 18:26:00.000000000 +02:00
---

Vor kurzem hab ich mir einen [Banana Pi](http://www.bananapi.org/p/product.html) (Specs im Link) als Basis für einen Arcadeautomat besorgt. Der erste Eindruck war sehr positiv, da man beim Banana Pi einen Gigabit Ethernet Port + SATA Anschluss (Kabel dafür gibt es [hier](http://www.pollin.de/shop/dt/NzI3NzkyOTk-/Bausaetze_Module/Entwicklerboards/Banana_Pi_SATA_Kabel.html)) hat. Auch der Dualcore Prozessor und der doppelte Arbeitsspeicher konnten erst mal überzeugen. Die GPIO Pins sollten wohl auch cool sein, was dieses [Beispiel](https://www.youtube.com/watch?v=hdYEvDbW6FY) zeigt.

Für Serveranwendungen wie z.B. einen Webserver der ein wenig stemmen sollte, würd ich den Banana Pi dem Raspberry Pi definitv vorziehen. Der größere Dualcore 1Ghz Prozessor in der Kombination mit den beiden oben genannten Zusatzfeatures (Festplatte per SATA + Gigabit Ethernet) sorgt dafür, das der Banana Pi ganz klar die Nase vorn hat. Hier sprechen einfach schnellere Verarbeitung, Zugriffzeiten und Netzwerkübertragen klar für sich. Selbst der neue [Raspberry Pi 2](http://www.heise.de/newsticker/meldung/Raspberry-Pi-2-4-Kerne-1-GByte-RAM-und-Windows-10-2534719.html) dürfte da mit seinem Quadcore mangels SATA und Gigabit Ethernet immer noch nicht dran kommen. Benchmarksvergleiche zu neuen Modell hab ich aber leider noch keine gefunden.

Aber nun zum wesentlichen Nachteil des Raspberry Pi Klons und der Grund warum ich diesen Blogpost überhaupt schreibe. Mein Plan war mit dem Banana Pi einen Arcade Automaten zu bauen, da er wesentlich mehr Leistung bietet als der alte Raspberry Pi. Das hat sich aber als weitaus schwieriger erwiesen als gedacht. Es gibt genügend [arm-optimierte](http://blog.petrockblock.com/retropie/arcade-systems-game-consoles-and-home-computers-in-retropie/) Emulatoren, die aber meist für den Broadcom Grafikchip des Raspberrys angepasst wurden. Das ist erst Mal nicht schlimm, da man das ja wiederum auf den Banana Pi anpassen könnte. Fehlanzeige. Es gibt wohl keinen vom Hersteller unterstützten Grafikkartentreiber für das Gerät. So wie ich das verstehe, gibt es nur einen Binärblob für Android. Ich habe ein Projekt gefunden, das einen OSS Treiber für den Mali-400MP2 [entwickelt](http://limadriver.org), das scheint aber nur mühselig voranzukommen und das letzte Update ist von 2013. Damit ist der Banana Pi für grafisch beschleunigte Emulatoron bzw. generell 3D beschleunigte Projekte äußerst ungeeignet. Hier macht sich der Raspberry Pi mit seinem inzwischen [OSS Treiber](http://www.heise.de/open/meldung/Freier-Grafiktreiber-fuer-den-Raspberry-Pi-2158533.html) wohl weit besser. Und durch die neue Version 2 wird auch das Problem mit mangelnder CPU Power und RAM besser. Bin gespannt wie sich der als Arcade Emulator schlagen wird.

Fakt ist auch einfach, das es auf den Anwendungszweck des Nutzers ankommt, welches Minicomputer geeigneter ist. Beide Geräte haben Vor- und Nachteile. Der Banana Pi verrichtet als Serverrechenknecht wohl besser seine Arbeit, während der Raspberry Pi wiederum als Client für XBMC oder eben als Arcade Emulator besser geeignet ist. Für kleine Mikrocontrolleraufgaben taugen beide in etwa gleich gut. Somit haben beide ihre Daseinsberechtigung und sollten nicht direkt als Konkurrenz angesehen werden. Eher als Hardware für verschiedene Aufgaben. 