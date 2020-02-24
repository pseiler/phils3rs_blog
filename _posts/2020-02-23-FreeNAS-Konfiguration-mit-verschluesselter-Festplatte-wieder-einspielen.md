---
layout: post
title: FreeNAS Konfiguration mit verschlüsselter Festplatte wieder einspielen
description: Beim Zurücksichern der FreeNAS Konfiguration können Probleme bei einer verschlüsselten Festplatte auftreten. Hier wird erklärt was
categories:
- Linux
date: 2020-02-23 13:15:00.000000000 +02:00
---

Nach einer Pause von mehr als einem Jahr melde ich mich mal wieder zurück. Dieses Mal geht es um [FreeNAS](https://www.freenas.org/).
Die System SSD mit 60 GiB hat letztens den Geist aufgegeben, daher musste schnell ein Ersatz her. Einen fast aktuellen Konfigurationsstand hatte ich gesichert, deshalb hatte ich keine Bedenken mein System wieder in einen lauffähigen Zustand zu bekommen. Als Ersatz für die SSD habe ich mir eine ältere 5400RPM Festplatte ausgesucht.

## Voraussetzungen
* frische FreeNAS Installation
* Backup Tarball einer FreeNAS Installation
* Geli Schlüssel für den verschlüsselten ZPool

Platte im Gehäuse getauscht und schon kann es losgehen. FreeNAS wurde auf der neuen alten Festplatte installiert und das Backup eingespielt. Dazu muss man sich nur auf die Weboberfläche anmelden und den Backup Tarball hochladen. Der Klickpfad ist folgender. Zuerst klickt man in der Seiteleiste links auf **System** -> **General**, dann scrollt man runter und wählt den Punkt **Upload Config**. Anschließend dauert das zurückspielen eine ganze Weile und am Ende wird man aufgefordert, das System neu zu starten. Abschließend sollte man das System wieder so vorfinden, wie es zum Zeitpunkt der Backups war.

Das hat bei mir auch wunderbar geklappt, nur den verschlüsselten ZPool aka. Storage Pool wollte das System unter keinen Umständen entschlüsseln und einhängen. Ich habe dann direkt gegooglet, was das Problem sein könnte, aber nichts brauchbares gefunden. Leider nur sehr veraltete Beiträge wie das Vorgehen ggf. früher war. Viel wurde auf der Kommandozeile erklärt, was in diesem Fall der völlig falsche Ansatz ist. Wenn man z.B. einen verschlüsselten Pool auf der Kommandozeile entschlüsselt, weiß die Weboberfläche davon nichts. Generell wird immer geraten, persistente Änderungen nur auf der Weboberfläche vorzunehmen. Am Ende hab ich mir die FreeNAS [Dokumentation](https://www.ixsystems.com/documentation/freenas/11.2/) durchgelesen und bin zu einer Lösung gekommen. Diese wiederum ist sehr einfach. In der Oberfläche muss der verschlüsselte Pool exportiert werden, um ihn anschließend wieder neu zu importieren.

## Pool ex- und importieren
Zuerst klickt man in der Seitenleiste auf **Storage** -> **Pools** und sucht nach dem betroffenen Storage Pool. Anschließend klickt man auf die drei Punkte und wählt **Export/Disconnect** um FreeNAS diesen Storage Pool vergessen zu lassen. Damit könnte man den Storage Pool jetzt auch auf einem anderen System mit Support für das Dateisystem ZFS importieren. Wir wollen diesen aber natürlich weiterhin mit diesem FreeNAS verwenden und klicken nach erfolgreichem Export in der Oberfläche oben rechts auf **Add**. Jetzt taucht ein neuer Dialog auf, der einen frägt, ob man einen neuen Pool erzeugen oder einen importieren möchte. Wir wählen **import an existing pool** und drücken **Next**. Als nächstes frägt einem der Dialog ob der Pool verschlüsselt ist. Wir wählen bei der Frage natürlich **Yes, decrypt the disks**, wählen alle relevanten Festplatten aus, geben den Geli Schlüssel an, und das Entschlüsselungspasswort. Dann drücken wir **Next**. Im nächsten Dialog wird der der Pool angezeigt, den die entschlüsselten Festplatten anbieten. Diesen wählt man zum importieren und drückt dann wieder auf **Next**. Hier werden einem nochmal alle gesetzten Optionen etc. angezeigt und man bestätigt den Dialog ein letztes Mal. Nun sollte der Pool wieder wie gewohnt funktionieren. Nach einem Neustart sollte man das Entschlüsseln mit Passwort nochmal ausprobieren. Bei mir klappt es seitdem wieder anstandslos.
