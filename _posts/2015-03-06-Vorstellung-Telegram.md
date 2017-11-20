---
layout: post
title: Telegram Vorstellung - ein Messenger wie er sein sollte
description: Vor- und Nachteile des Messengers Telegram im Vergleich zu Whtasapp
categories:
- Technik
date: 2015-03-06 13:22:00.000000000 +02:00
---

Ich war schon lange auf der Suche nach einem bequemen, aber vorallem auch zuverlässigen und offenen Messenger fürs Handy/Smartphone. Damit das auch was wird, muss der Messenger auch DAU-freundlich sein. Nach einer Empfehlung eines Kumpels fiel die Wahl auf [Telegram](https://www.telegram.org/). Bei Telegram handelt es sich um ein Instant Messaging Dienst mit offenen Client [(GPL-2.0)](https://de.wikipedia.org/wiki/Telegram_Messenger) und proprietären Server mit öffentlich dokumentiertem [Protokoll](https://core.telegram.org/mtproto) und [API](https://core.telegram.org/api). Das Protokoll implementiert asymmetrische Verschlüsselung durch ein [public/private Key Verfahren](https://core.telegram.org/api/end-to-end). Außerdem beherrscht der Telegram die Funktion, Nachrichten mit Selbstzerstörungmechanismus zu verschicken.

Das tolle an Telegram sind zum einen die Features in Kombination mit der Einfachheit, die sonst nur Whatsapp hat. Kontakte werden über die Handynummer verwaltet. Beim ersten einloggen/erstellen des Users wird die Handynummer angegeben, die auch gleichzeitig der Username ist. Anschließend bekommt man eine SMS mit dem Verifikationscode. Nun werden die Telefonnummern abgegleicht und alle bekannten User in die Kontaktliste aufgenommen. Bei zusätzlichen Anmeldungen auf anderen Geräten, wird einfach die Handynummer wiederholt eingegeben und per SMS authorisiert.

Zu den Hauptfeatures gehören folgende:

* einfache Kontaktverwaltung durch Zuordnung per Handynummer
* bei Bedarf asymmetrisch verschlüsselte Kommunikation
* Gruppenkonversationen
* GIF und allgemein Bilder Support
* Audio und Video Nachrichten
* offenes Protokoll, API und Client
* Multidevice fähig

Leider hat Telegram auch Nachteile. Dazu gehören folgende:

* Server proprietär
* Gruppenchat nicht asymmetrisch verschlüsselt
* Datensammlung durch Handynummern (Verwertung in den AGBs nicht geprüft)
* standardmäßig wird der unsichere Chat (nur SSL gesichert) gestartet

Dank offener API und offenem Protokoll haben 3rd Party Implementierungen nicht lange auf sich warten lassen. So gibt es bereits neben den [offiziellen Desktop Clients](https://desktop.telegram.org/) ein [Pidgin/libpurple Plugin](https://github.com/majn/telegram-purple), welches Telegram nahezu vollständig unterstützt. Gruppenchat inklusive Bilder können geführt werden, verschlüsselte Chats kann man nutzen und alle anderen notwendingen Features wurden bereits eingebaut. Somit kann man auch auf dem Desktop mit Freunden in Kontakt bleiben.

Somit ist Telegram neben Jabber (für Technikinteressierte) die beste Lösung um vernünftig verschlüsselt mit seinen Freunden in Kontakt zu bleiben. Also wenn sich jemand in eurem Freundeskreis nach einer Whatsapp Alternative erkundigt, empfehlt der Person Telegram.
