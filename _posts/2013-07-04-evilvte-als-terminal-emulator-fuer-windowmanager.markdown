---
layout: post
title: evilvte als Terminal Emulator für Windowmanager
categories:
- Linux
permalink: /archives/29-evilvte-als-terminal-emulator-fuer-windowmanager.html
s9y_link: http://blog.phils3r.de/index.php?/archives/29-evilvte-als-terminal-emulator-fuer-windowmanager.html
date: 2013-07-04 23:18:43.000000000 +02:00
---
Ich meld mich mal wieder für einen kleinen Tech Post zurück.
Ich benutze ja einen schlanken windowmanager ([i3](http://i3wm.org/)) um meine Programme und vorallem koammdozeilen tools zu starten.
Eine gut konfigurierte shell (bash,zsh oder wie auch immer) ist wichtig.  Aber viel wichtiger ist eigentlch der Terminal Emulator, weil er die Schnittstelle zwischen GUI und der shell ist. Man muss vernünftig kopieren und einfügen können, Die Steuerungstasten (DEL,POS1,END,...) sollten alle funktionieren. Mir persönlich ist ja diese STRG + Pfeiltasten Kombination, um ans Ende von Strings zu springen, ans Herz gewachsen. Die wollt ich nicht missen. Die bin ich von xterm gewöhnt gewesen. Somit fällt auch der unkonfigurierte urxvt als Terminal Emuator raus.

Meine Wahl ist durch meine Kriterien oben auf [evilvte](http://www.calno.com/evilvte/) gefallen. In der Standard Konfiguration ist das eher ein besserer xterm für schlichte Desktop Environments. Aber mit der richtigen Konfiguration passt er sich wunderbar meinen Windowmanagerbedürfnissen an.

[Patch für die Baukonfiguration.](https://build.opensuse.org/package/view_file/home:seilerphilipp/evilvte?expand=1&file=customization.patch)

Leider kompiliert man das Programm hardcoded mit einer bestimmten Konfiguration.
Deswegen kann man den evilvte auch nicht so einfach für die Allgemeinheit paketieren.

NIchtsdestotrotz hab ich mit evilvte den besten Terminal Emulator für meinen windowmanager i3 gefunden. Unter anderem auch deswegen weil er pseudo und echte Transparenz beherrscht.

Kann man sich mal aufjeden Fall anschauen. Für openSUSE hab ich meine Konfiguration [paketiert](http://software.opensuse.org/package/evilvte">paketiert)
