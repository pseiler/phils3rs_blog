---
layout: post
title: Automatisiertes Paketbauen mit dem Open Build Service 2.3
categories:
- Linux
date: 2012-05-03 09:21:00.000000000 +02:00
---
Heute habe ich auf Heise etwas erfreuliches gelesen. Open Build Service wurde vom openSUSE Projekt heute in der Version 2.3 released. Für alle Linuxer die das Ding noch nicht kennen. Es handelt sich hierbei um eine Client/Server Lösung um Programmpakete auf/für so ziemlich allen gängigen LinuxDistributionen zu bauen. Es kommt mit RPM, DEB und PKGBUILDs (Archlinux) klar. Distributionen die bereits verfügbar sind, wären

* **openSUSE**
* **SUSE Linux Enterprise Server**
* **Fedora**
* **Red Hat Enterprise Linux**
* **CentOS**
* **Mandriva**
* **Debian**
* **Ubuntu**
* **Archlinux**

Prinzipiell dürft es auch kein Problem sein anderes RPM oder Deb basierte Distributionen einzupflegen. Schwieriger wirds bei eigenen Paketformaten.

Der OBS funktioniert ähnlich zu einer Versionsverwaltung auf dem alle Versionen der Paketbauanleitungen (spec files, tarballs mit dem sourcecode, debian control files usw.) behalten werden, und bei Veränderungen jeweils neu gebaut werden. Der eigentliche Bauvorgang inklusive kompilieren kann auf weitere sogenannte Worker ausgelagert werden um ein bauen vieler Paketer parallel zu gewährleisten. Somit müssen Paketmaintainer ihre Pakete nicht mehr lokal auf ihrer Entwicklermaschine bauen, sondern können das bequem über den OBS regeln. Eine automatische Repositorygenerierung wurde natürlich auch implementiert.

Vom Aufbau her, werden Projekte angelegt innerhalb dieser dann die Pakete erstellt werden. Zum Beispiel kann man auch eine komplett eigene Distribution auf dem OBS erstellen. Oder man erstellt für den Anfang sein eigenes Home Projekt um z.B. eigene Pakete erstellen zu können auf denen man dann seine Distributionen wählt, für die das Paket gebaut werden soll. Natürlich muss man für RPM und Deb basierten Distributionen zwei verschieden Baunleitungen pflegen. Auch kann man dann das fertige Paket an ein anderes Projekt schicken kann. Ähnlich zu Git Pull Requests. Somit wurde auch an die  Community gedacht.

Der OBS bietet eine Weboberfläche in der man Einsicht auf alle öffentlichen Pakete und Projekte hat und theoretisch auch darüber seine Dateien bearbeiten kann. Für die meisten wird das aber wohl zu mühselig sein, daher wird auch ein Kommandozeilenclient bereitgestellt, der mit dem Server über eine Ruby API kommuniziert. Das fühlt sich dann wie Subversion an. Man ändert seine Spec File z.B. lokal und commitet dann die Änderungen samt commit log an den Server zurück.

Zur detaillierten Benutzung hau ich dann auch mal einen zusätzlichen Post raus, damit ihr auf meinem Blog auch mal lernt. vom openSUSE Wiki gibts auch einen Artikel der die Benutzung des "osc" genannten tools erklärt. Google sollte da weiterhelfen. Natürlich hat der cli Client auch eine Manpage.

Zu den Neuerungen des OBS in der Version 2.3 gehören eine verbesserte Weboberfläche, eine verbesserte Koordination für Updates und eine verbesserte Crossbuild Unterstützung für die ARM Architektur.

Alles in allem ein sehr gelungerer Release.

Wenn ihr Fragen habt, könnt ihr die in den Kommentaren stellen, oder ihr schreibt mir eine E-Mail.

Projekt Homepage:
[www.open-build-service.org](http://www.open-build-service.org/">http://www.open-build-service.org/)
Laufende Instanz:
[build.opensuse.org](https://build.opensuse.org/)

Quellen:

* [build.opensuse.org](https://build.opensuse.org/)
* [Open Build Service 2.3 verbessert Update-Handling](http://www.heise.de/open/meldung/Open-Build-Service-2-3-verbessert-Update-Handling-1566188.html)
* Eigene Erfahrungen
