---
layout: post
title: Elko-Liste für die Xbox Classic Mainboard Revision v1.4
description: eine ausführliche Liste über alle Elkos der Microsoft Xbox Classic Mainboard Revision v1.4
categories:
- Technik
date: 2022-12-06 21:00:00.000000000 +02:00
---

Das die klassische Xbox (OG Xbox) ein Problem mit den Kondensatoren bzw. den Elektrolytkondensatoren (kurz Elkos) haben, dürfte Enthusiasten längst bekannt sein. Allen voran der sogenannte "Clock Capacitor" (Zeit-Kondensator). Dieser läuft bei den meisten Revisionen als erstes aus, ist aber nicht der einzige Problemfall. Meine Xbox Mainboard Revision 1.4 ist hiervon auch betroffen und benötigt daher neue.

Sogleich hab ich mich auf die Suche nach Informationen begeben. Die erste Anlaufstelle für Enthusiasten ist bekanntermaßen das [Wiki von Console5](https://wiki.console5.com/wiki/Microsoft_Xbox#v1.4). Hier werden alle Elkos gelistet, nur fehlen entscheidende Angabe wie z.B. die Höhe, das Rastermaß und der Durchmesser.

Diese Angaben hab ich selbst gemessen und ergänzt.
Im Folgenden findet ihr eine Tabelle mit allen Elkos, ihren Größen, Rastermaßen und Mainboardbeschriftungen.

| **Menge** | **Typ** | **Kapazität** | **Spannung** | **Rastermaß** | **Höhe** | **Durchmesser** | **Mainboard Positionen** |
|-----------|---------|---------------|--------------|---------------|----------|-----------------|--------------------------|
| 2         | Radial  | 3300 μF       | 10V          | 5mm           | 25mm     | 12,5mm          | C1G1, C7G1               |
| 3         | Radial  | 3300 μF       | 6.3V         | 5mm           | 25mm     | 9mm             | C1E1, C2E4, C3E2         |
| 3         | Radial  | 1500 μF       | 6.3V         | 5mm           | 20mm     | 10mm            | C4F9, C7E2, C7F1         |
| 1         | Radial  | 680 μF        | 16V          | 3mm           | 15mm     | 8mm             | C5A4                     |
| 7         | Radial  | 100 μF        | 25V          | 2.5mm         | 12mm     | 6.3mm           | C1E1, C2E4, C3E2         |
| 13        | Radial  | 22 μF         | 25V          | 2.5mm         | 12mm     | 5mm             | C1G3, C1G6, C2G2, C3F6, C3G1, C4G4, C4G8, C5F5, C6G1, C7B5, C7G6, C8C2, C8E3 (gerne mal ein SMD Elko) |
| 5         | SMD     | 10 μF         | 16V          | -             | 5.8mm    | 4mm             | C6A10, C6A11, C6A4, C6B4, C6B6 |
| 1         | SMD     | 47 μF         | 16V          | -             | 5.8mm    | 6.5mm           | C7B2                     |
| 1         | Radial  | 1F            | 2.5V         | 3mm           | 12.5mm   | 7.7mm           | C7G2 (Clock Cap)         |

Bei einer Sache bin ich mir noch nicht sicher, was genau sie zu bedeuten hat. Die 1500 μF Elkos sind komplett grau und unterscheiden sich farblich komplett von den anderen. Ob die eine zusätzliche Funktion haben, ist mir bisher nicht bekannt. Sollte ich hierzu ein Erkenntnisgewinn haben, editier ich die Informationen selbstverständlich.
