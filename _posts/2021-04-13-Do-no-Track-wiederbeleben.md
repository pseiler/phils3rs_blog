---
layout: post
title: Do-not-Track wiederbeleben
description: Eine spannende Idee wie man das Konzept hinter der Browsereinstellung Do-Not-Track wieder nutzen könnte.
categories:
- Linux
date: 2021-04-13 03:00:00.000000000 +02:00
---


Nach über einem Jahr Pause melde ich mich wieder zurück mit einem eher politischen, aber auch technischen Thema.

Heutzutage ist das Internet ja ein sehr schlimmer Ort. Man besucht eine Webseite, möchte vielleicht auf einem Online Shop etwas einkaufen, oder man möchte sich so über das aktuelle Tagesgeschehen informieren. Nichtsahnend landet man auf einer Seite und das Spektakel beginnt. Surft man ohne Adblocker hat man heutzutage eh schon verloren. Dann wird erst mal eine Menge Javascript ausgeführt. Hier Berechnungen zum Endlosscrolling, dort werden Bilder nachgeladen. Full Responsiveness. Man bekommt das volle Paket ab. Nebenbei fängt die CPU schon an, warm zu laufen, weil man bereits den fünfzehnten Tab offen hat. Aber kein Problem. Für was hat man denn die 32 GB Arbeitsspeicher und den Octacore CPU. Nach erfolgreichem Laden der Seite schiebt man dir noch ganz heimlich ein paar Cookies zu. In den letzten Jahren hat sich das ja auch noch etwas verschlimmbessert. Diese miesen Cookiebanner wollen einen, immer mit fiesen Tricks zur Usermanipulation, dazu bringen, stillschweigend alles abzunicken. Siehe dieses Bild bei spieletipps.de. Hier wird zwischen Einwillung und berechtigem Interesse unterschieden. Bei dem berechtigten Interesse wird natürlich standardmäßig alles zugelassen. Auch gibt es keinen Knopf, um Allem zu widersprechen. Alles auszuschalten, hat mich über fünf Minuten gekostet.

Einwillung:
![Spieletipps Cookie Einwilligung](/images/spieletipps/einwillung.png)

Berechtigtes Interesse:
![Spieletipps Cookie Berechtigtes Interesse](/images/spieletipps/einwillung.png)

Auch eine spannende Methode, was diverse Nachrichtenseiten machen. Ein generelles Erlauben der Cookies erzwingen und wenn man mit der Verarbeitung nicht einverstanden ist, kann man sie am Ende wieder widerrufen. Das scheint auf den ersten Blick ganz nett, ist aber leider unzumutbar. Man muss manuell einen Link aufrufen und auf einen Button klicken. Allein das macht schon niemand mehr (mich eingeschlossen).
Findige Nutzer klicken sich durch absichtlich schwer gestaltete Dialoge und stellen ihren Browser maximal paranoid ein. Hardcoredatenschützer konfigurieren ihren Browser (Firefox) so, dass bei allen Top-Level-Domains selbst entschieden wird, wer einen Cookie setzen darf. 

Ein viel besseres System wäre da einfach [Do-Not-Track](https://browserleaks.com/donottrack). Das ist ein simpel zu implementierendes System, das checkt, ob der Benutzer der Datenverarbeitung zustimmt oder nicht. Leider hat sich das nicht wirklich durchgesetzt. Kein Wunder. Keine Firma hat da freiwillig Interesse daran. Sowas sollte durch den Gesetzgeber geregelt und forciert werden.

Ich kenne genau eine Seite, die das Do-Not-Track Thema sauber aufgreift. Es ist [geizhals.de](https://geizhals.de/). Hier wurde das Setzen des Cookies löblich umgesetzt (Stand 2021-04-13). Es wird ein kurzer Dialog per Javascript (das sieht zumindest mal nach einer halbwegs sinnvollen Verwendung aus) eingeblendet, welcher einem kurz anzeigt, dass er Do-Not-Track berücksichtigt und nur die notwendigen Cookies setzt. Hätte das jede Seite so implementiert, wäre alles viel unkomplizierter. Man könnte auch nicht so leicht reingelegt werden. Das Internet könnte zur Abwechslung mal ein wenig Ehrlichkeit gebrauchen. Auch wenn es vom Gesetzgeber kommen muss. Es hätte aber den starken Vorteil, dass die Benutzererfahrung wesentlich besser ist. Meiner Ansicht nach könnte es sogar bei einem [Opt-Out](https://de.wikipedia.org/wiki/Opt-out_(Permission_Marketing)) bleiben. Solange sichergestellt ist, dass es auch berücksichtigt wird, wenn man Do-Not-Track setzt. Alles ist besser als diese Cookie Banner.

Zum Teil ist das auch nur die Vorstellung einer idealeren Welt im Internet, aber meiner Ansicht nach hat es das Potential, Realität zu werden. Auch wenn viele Leute sagen, Do-Not-Track sei bereits gescheitert.

Die Probleme, dass unsere Webseiten viel zu viel Skripte ausführen und Resourcen verschwenden, sind damit aber leider auch nicht gelöst.
Aber auch dafür gibt es ja auch Add-Ons wie [No-Script](https://noscript.net/) und Konsorten. Das hilft viel gegen Tracking und verhindert die Ausführbarkeit von unerlaubtem Javascript. Es gibt ein paar Alternativen, aber die technisch einwandfreiste Lösung stellt meiner Ansicht nach definitiv No-Script dar.
