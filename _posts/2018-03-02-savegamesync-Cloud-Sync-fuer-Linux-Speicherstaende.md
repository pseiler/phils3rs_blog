---
layout: post
title: savegamesync - Cloud Sync für Linux Speicherstände
description: Skript um Speicherstände für Linux Spiele mit OwnCloud/Nextcloud zu syncen
categories:
- Linux
date: 2018-03-02 16:12:00.000000000 +02:00
---
Ich habe mich mal wieder ans Python programmieren/skripten gewagt. Dabei ist ein recht ordentliches Programm rausgekommen, welches Speicherstände/savestates von allen unterstützten Linux Spielen in ein *\*.tar.gz* einpackt und an einen konfigurierbaren Ort in der OwnCloud/Nextcloud Instanz hochlädt. Die unterstützten Spiele sind einfach über die mitgelieferte *\*.xml* Datei erweiterbar.

Wer schon immer nach einer simplen Lösung für das synchronisieren seiner Speicherstände gesucht hat, wird bei [savegamesync](https://github.com/pseiler/savegamesync) fündig.

Eine Beschreibung inklusive Installation, Nutzung und Tipps gibt es in der README auf github.com.

Gestartet habe ich dieses kleine Projekt als Bash Skript. Als ich dann alle Funktionalitäten fertig hatte, und möglichst alles in Funktionen auslagern wollte und Daten nicht doppelt pflegen wollte, ist mir aufgefallen, das *bash* nicht mehr reicht. Ich habe mir überlegt, stattdessen einfach *python* zu benutzen um eben die oben genannte *\*.xml* Datei zu parsen. Somit muss man das Skript nicht erweitern, wenn man ein neues Spiel hinzufügen möchte. Der Hintergrund ist auch, dass die Community nach und nach die Spieleliste erweitert um möglichst, alle unter Linux verfügbaren Spiele mit dem Skript zu sichern. Der für mich als Python Einsteiger schwierigste Part war, die korrekte Benutzung von *pyCurl* bzw. *libcurl*. Einen korrekten Aufruf um ein *\*.tar.gz* hochzuladen und zusammen zu stellen, war gar nicht so leicht. Nach viel lesen und rumprobieren hat es dann anschließend doch noch geklappt. Der Rest wurde dann nach und nach hinzugefügt.

Wenn das Skript gut ankommt, werde ich es erweitern und meine neugewonnen Fertigkeiten natürlich in den bestehenden Code einfließen lassen. Ein erster Hinweis ["argparse"](https://docs.python.org/2/library/argparse.html) zu verwenden, werde ich gleich nachgehen. Vllt ist der Code schon umgeschrieben, bis ihr das hier lest. 
