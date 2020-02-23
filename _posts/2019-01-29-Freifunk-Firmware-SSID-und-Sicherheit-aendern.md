---
layout: post
title: Freifunk Firmware - SSID, MAC Adresse und Verschlüsselung / Sicherheit ändern
description: Möchte man die openwrt / Freifunk Firmware so ändern, dass sie eine andere SSID nutzt, findet man hier die richtigen Befehle
categories:
- Linux
date: 2019-01-29 17:15:00.000000000 +02:00
---
Nutzt man die modifizierte Version der [openWRT](https://openwrt.org/) Firmware, um einen [Freifunk](https://freifunk.net/) Knoten zu betreiben, wird man unter Umständen vor ein paar Probleme gesetzt. Gegebenfalls möchte man die SSID des WLANs ändern, die Verschlüsselung aktivieren oder die genutzten MAC Adressen ändern. In meinem Fall wurde nicht die reale Hardware Adresse genommen, was dazu führte, dass mein Freifunk Knoten nicht die richtige IP Adresse bekommen hatte, die für den Zugriff aufs Internet freigeschaltet wurde.
In den folgenden Schritten beschreibe ich, welche Schritte nötig sind, um Konfigurationsparameter zu ändern, die die Weboberfläche der Freifunk Firmware verbirgt. Im Übrigen funktioniert das leicht verändert auch mit der normalen openWRT Firmware.

## Folgendes wird vorausgesetzt:
* ein Freifunk Router (in meinem Fall ein TP-Link WR841N V9)
* die installierte Freifunk Firmware (zu finden auf der [Freifunk Seite](https://freifunk.net/wie-mache-ich-mit/community-finden/) deiner Umgebung)
* einen SSH Client auf dem Client Rechner
* ein RJ45 Netzwerkkabel, um sich direkt mit dem Router zu verbinden

## Folgende vorbereitende Schritte sind nötig:

1. Zu allererst muss ein SSH Schlüssel auf dem Client erzeugt werden. Wie das geht, findet man für alle gängigen Plattformen auf der Suchmaschine der Wahl.
1. Anschließend bootet man in den Wartungsmodus des Routers (Je nach Gerät anders. In der Regel hält man drei Sekunden lang den Reset Button gedrückt.).
1. Man verbindet seinen Client per Kabel mit dem Freifunk Router auf eine der LAN Schnittstellen.
1. Jetzt sollte man eine IP Adresse aus dem Bereich 192.168.1.0/24 bekommen.
1. Nun surft man die Webschnittstelle des Routers mit der Adresse 192.168.1.1 an und wechselt oben rechts in den "Expert Mode" bzw. in die "Erweiterten Einstellungen".
1. In dem Tab "Remotezugriff" trägt man den öffentlichen Schlüssel des generierten SSH Schlüsselpaars ein.
1. Nun wechseln wir auf die Kommandozeile, da es nicht vorgesehen ist, andere, die von uns gewollten, Einstellungen in der Weboberfläche vorzunehmen.

## Konfigurationsänderung auf der Kommandozeile
Als Erstes verbinden wir uns per SSH auf den Router (in der Anleitung gehe ich von einem Linux Client aus).
{% highlight bash %}
ssh root@192.168.1.1
{% endhighlight %}
Die Authentifizierung erfolgt mittels dem vorher abgelegten öffentlichen Schlüssel.
Man kann sich die openWRT spezifische Konfiguration mittels folgendem Befehl ansehen.
{% highlight bash %}
root@freifunk# uci show
{% endhighlight %}

Möchte man die MAC Adresse des WAN Interfaces ändern, sucht man den Parameter und ändert ihn anschließend.
{% highlight bash %}
root@freifunk# uci show | grep wan.macaddr
network.wan.macaddr='aa:bb:cc:dd:ee:11'

root@freifunk# uci set network.wan.macaddr='12:23:34:45:ef'
{% endhighlight %}

Nach dem Speichern der Konfiguration und einem Neustart, wird die MAC Adresse auf die Eingegebene geändert.
Selbstverständlich funktioniert das auch mit der LAN- oder jeder beliebigen Schnittstelle.
Wenn man weiß, was man tut, kann man natürlich auch jeden anderen Parameter manipulieren. Die [openWRT Dokumentation](https://openwrt.org/docs/start) liefert die nötigen Informationen.
</br>
</br>
Möchte man die SSID ändern, geht das genauso (Ich weiß, dass das Ändern der SSID des Freifunk Knotens nicht gewünscht ist, aber die Möglichkeit möchte ich trotzdem dokumentieren. Es gibt für alles einen Anwendungszweck. Tut mir Leid Freifunk Projekt.).

{% highlight bash %}
root@freifunk# wireless.client_radio0.ssid='NEUE_SSID'
{% endhighlight %}

Möchte man eine Verschlüsselung aktivieren, geht das mit folgenden beiden Befehlen.
In unserem Beispiel nutzen wir den aktuell weit verbreitesten Verschlüsselungsalgorithmus.
Selbstverständlich sollte man den Schlüssel/Key durch seinen eigenen austauschen.
{% highlight bash %}
root@freifunk# wireless.client_radio0.encryption='psk2'
root@freifunk# wireless.client_radio0.key='n3U3s_P4SSw0R7'
{% endhighlight %}

Möchte man die Einstellungen aktivieren, so stellt man sie dem System mit folgendem Kommando zur Verfügung.
{% highlight bash %}
root@freifunk# uci commit
{% endhighlight %}

Anschließend startet man den Router mit folgendem Kommando neu
{% highlight bash %}
root@freifunk# reboot
{% endhighlight %}
