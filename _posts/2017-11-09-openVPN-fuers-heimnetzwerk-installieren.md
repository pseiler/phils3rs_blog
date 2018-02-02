---
layout: post
title: openVPN mit DynDNS für Zugriff aufs Heimnetzwerk installieren
description: Mit Linux einen openVPN Server aufsetzen, um sich ins eigene Heimnetz zu verbinden
categories:
- Technik
- Linux
date: 2017-11-09 21:11:00.000000000 +02:00
---

Und gleich der nächste Artikel hinterher. Mein letztes kurzes persönliches Projekt war das aufsetzen eines [openVPN](https://openvpn.net/) für das persönliche Heimnetzwerk mitsamt Routing und Vollzugriff fürs Netzwerk und das erreichen per DynDNS Adresse. Hierfür wird folgendes benötigt.

+ Ein Account bei einem DynDNS Anbieter. Oder eine selbst gebaute Lösung. Ich benutze [goip.de](http://www.goip.de/).
+ Einen Router, welcher selbst eingetragene DynDNS Update URLS unterstützt (ich habe eine Fritzbox verwendet)
+ einen Linux Rechner, welcher 24/7 betrieben werden kann. (z.B. einen [Raspberry Pi](https://www.raspberrypi.org/))
+ openVPN auf sowohl auf dem Client, als auch auf dem Server

Zuallererst konfigurieren wir unseren DynDNS Dienst. Im Falle von [goip.de](http://www.goip.de/) brauchen wir zuallererst einen Account. Den erstellen wir uns auf der Homepage. Eine genau Anleitung dazu finden wir hier: ([klick mich](http://www.goip.de/install.html))

Die genaue update URL die wir für die Fritzbox brauchen, ist diese:
{% highlight html %}
https://www.goip.de/setip?username=<username>&password=<pass>&subdomain=<domain>&ip=<ipaddr>
{% endhighlight %}

Als nächstes setzt man den Server auf, der später der VPN Server werden soll. Man kann dazu jede beliebige Linux Distribution nehmen. In meinem Fall war es ein [Raspbian](http://www.raspbian.org/). Anschließend installiert man die Software **openvpn**.

{% highlight bash %}
user$ sudo apt-get install openvpn
{% endhighlight %}

Nun erstellt man die benötigten Zertifikate die zu einem fehlerfreien Betrieb notwendig sind. 
Man kopiert das RSA Skripte Verzeichnis nach /etc/openvpn/
{% highlight bash %}
root# cp /usr/share/doc/openvpn/examples/easy-rsa/2.0/ /etc/openvpn/easy-rsa
{% endhighlight %}
Falls das Verzeichnis nicht hier liegt, kann man es innerhalb des Pakets suchen.
Dazu führt man je nach Distribution einen der folgenden Befehle aus:
Für Debian basierte Systeme
{% highlight bash %}
root# dpkg -L openvpn
{% endhighlight %}
oder für RPM basierte Systeme
{% highlight bash %}
root# rpm -ql openvpn
{% endhighlight %}

Nun geht es ans generieren der Zertifikate. Zuerst editiert man die Variablen die man für das generieren des Zertifikats nutzt.
Wichtig sind folgende Parameter: *KEY_COUNTRY*, *KEY_PROVINCE*, *KEY_CITY*, *KEY_ORG*, and *KEY_EMAIL*. Möchte man die Sicherheit bzw. den Paranoialevel erhöhen, so kann man die Schlüssellänge beim Parameter *KEY_SIZE* auf *2048* ändern.

{% highlight bash %}
root# vim /etc/openvpn/easy-rsa/vars
{% endhighlight %}

Hat man die **vars** Datei erfolgreich editiert, sourced man sie.
{% highlight bash %}
root# cd /etc/openvpn/easy-rsa/
root# . ./vars
root# ./clean-all
{% endhighlight %}

Nun erstellt man die Zertifikate nach der Reihe und ändert die Felder ggf. ab. 
{% highlight bash %}
root# ./build-ca
Generating a 1024 bit RSA private key
............++++++
...........++++++
writing new private key to 'ca.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [KG]:
State or Province Name (full name) [NA]:
Locality Name (eg, city) [BISHKEK]:
Organization Name (eg, company) [OpenVPN-TEST]:
Organizational Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) []:OpenVPN-CA
Email Address [me@myhost.mydomain]:
{% endhighlight %}

Als nächstes erstellen wir das Server Zertifikat. Die Fragen beantwortet man natürlich mit ja, damit sie erfolreich in die Datenbank aufgenommen werden.

{% highlight bash %}
./build-key-server server
{% endhighlight %}

Jetzt erstellt man das Client Zertifikat. $CLIENTNAME steht für den tatsächlichen Namen des Zertifikats. Diesen Schritt kann man beliebig oft wiederholen, um mehreren Clients Zugriff aufs VPN zu geben
{% highlight bash %}
./build-key $CLIENTNAME
{% endhighlight %}

Als letzten Schritt erstellt man noch das [Diffie Hellmann](http://www.rsasecurity.com/rsalabs/node.asp?id=2248) Zertifikat. Je nach System und Schlüssellänge kann das sehr lange dauern.
{% highlight bash %}
./build-dh
Generating DH parameters, 1024 bit long safe prime, generator 2
This is going to take a long time
.................+...........................................
...................+.............+.................+.........
......................................
{% endhighlight %}

{% highlight ini %}
# der zu verwendende Port
port 1194

# Die lokale Adresse, auf welcher der Dienst hört
# Das kann man weg lassen, falls der beim Systemstart
# z.B. erst die Adresse per DHCP vergeben wird und der Dienst 
# den Start verweigert, da er die Adresse noch nicht kennt
#local 192.168.100.80

# Das Protokoll, welches verwendet wird (tcp oder udp)
proto udp

# Die Wahl zwischen tun oder tap Device.
# tun verwendet routing, tap verwendet bridging
# in diesem Tutorial wird nur die Variante
# mit routing beschrieben
dev tun

# Die Zertifikate, welche der Server verwendet
ca /etc/openvpn/easy-rsa/keys/ca.crt
cert /etc/openvpn/easy-rsa/keys/server.crt
key /etc/openvpn/easy-rsa/keys/server.key # Diese Datei sollte geheim
# bleiben

dh /etc/openvpn/easy-rsa/keys/dh2048.pem

# Das Netzsegment, für die IP Adressen innerhalb des VPNs
server 10.12.0.0 255.255.255.0
# Die Route die im Client gesetzt werden kann.
# "192.168.10.0" muss durch das eigentliche
# Netzsegment ersetzt werden. 
push "route 192.168.10.0 255.255.255.0"

# Dieser Parameter erlaubt es, das VPN Clients untereinander
# eine Verbindung aufbauen können.
client-to-client

# Erlaubt es die Verbindung auch ohne Probleme
# im idle State aufrecht zu erhalten.
keepalive 10 120

# Paketkompression mit LZO
comp-lzo

# Anzahl der maximalen VPN Clients
max-clients 15

#user nobody
#group nobody

persist-key
persist-tun

# Status Logging
status /var/log/openvpn-status.log

# Info und Fehler Logging
log-append  /var/log/openvpn.log

# Client spezifische Konfigurationen (dazu komme ich später noch)
client-config-dir /etc/openvpn/client-config

# Ausführlichkeitslevel des Logs
verb 4

;mute 20

# Pfad für ausgeschlossene Zertifikate
#crl-verify crl.pem
{% endhighlight %}

Für einzelne Clients kann man eine zusätzliche spezifische Konfiguration pflegen. Das ist nützlich, da man hier z.B. die VPN IP festlegen kann, oder ob z.B. das Gateway umgestellt wird.
Dazu erstellt man wie oben in der Konfiguration eingetragen das Verzeichnis

{% highlight bash %}
root# mkdir /etc/openvpn/client-config
{% endhighlight %}

Die Datei für den Client benennt man wie das Zertifikat. Hat man mit `./build-key client1` Die Zertifikate für *client1* generiert, so heißt die Datei auch im *client-config* Verzeichnis auch *client1*

{% highlight bash %}
vim /etc/openvpn/client-config/client1
{% endhighlight %}
{% highlight ini %}
# Die IP Adresse, die der Client "client1"
# zugewiesen bekommen soll
ifconfig-push 10.12.0.10 10.12.0.1

# Ändert das Standard Gateway ab.
#push "redirect-gateway"
#push "dhcp-option DNS 213.73.91.35"
{% endhighlight %}

Serverseitig fehlt noch der Kernelparameter, um Routing zu aktivieren. Hierzu editiert man für eine persistente Änderung die Datei `/etc/sysctl.conf` und fügt folgende Zeile hinzu. Ggf. gibt es ein Template, bei dem man die Zeile auch einfach einkommentieren kann.
{% highlight ini %}
net.ipv4.ip_forward=1
{% endhighlight %}

Allerdings wird die Konfigurationsdatei erst beim nächsten Boot gesetzt. Um Routing im Live Betrieb zu aktivieren, muss folgender Befehl ausgeführt werden.
{% highlight bash %}
root# echo "1" > /proc/sys/net/ipv4/ip_forward
{% endhighlight %}

Außerdem fehlt die Route zurück ins VPN Netz vom Standard Gateway (der Router im Heimnetz).
In unserem Fall ist es das Netz 10.12.0.0.
Die Route sieht dann wie folgt aus

![FritzBox Routing](/images/fritzbox_route.png)

Für die einfache Zertifikats- und Client Konfigurationsverteilung habe ich mir eine Kombination aus Template und Skript zum verpacken der VPN Zertifikate ausgedacht.
Das Template legt man unter `/etc/openvpn_client.in` an.

Der Inhalt ist folgender

{% highlight ini %}
# Anweisung, dass diese Konfiguration für einen openVPN Client ist
client
# Die VPN Variante
dev tun
# das Protokoll
proto udp
# Der DynDNS Hostaname und der zugehörige Port von oben
remote $HOSTNAME.goip.de 1194
#compression
comp-lzo
resolv-retry infinite
nobind
persist-key
persist-tun
mute-replay-warnings
ns-cert-type server
verb 3
mute 20

ca keys/ca.crt
{% endhighlight %}

Ich habe mir ein Konzept ausgedacht, um einfach Zertifikate gepackt als Tarball zum direkten Nutzen, zu erstellen.
Dafür habe ich folgendes Skript geschrieben, welches man unter `/etc/openvpn/easy-rsa/keys/maketar.sh` ablegt. Auch wird
eine Konfiguration mit den richtigen relativen Pfaden generiert.

{% highlight bash %}
#!/bin/bash

if [ -z $1 ]
then
 echo "no user indicated"
 exit 1
fi

if [ ! -d $1 ];
then
  mkdir $1;
  chmod 700 $1;
  mkdir $1/keys;
  chmod 700 $1/keys;
fi;
if [ ! -f $1/keys/$1.key ] && [ ! -f $1/keys/$1.crt ]
then
  mv $1.key $1.crt $1/keys/;
fi
if [ ! -f $1/keys/ca.crt ]
then
  cp ca.crt $1/keys/ca.crt
  chmod 600 $1/keys/ca.crt
fi
cp /etc/openvpn/openvpn_client.in $1/$1.conf
echo "cert keys/$1.crt" >> $1/$1.conf
echo "key keys/$1.key" >> $1/$1.conf
chmod 600 $1/$1.conf
tar czf $1.tar.gz $1
{% endhighlight %}
Dem Skript gibt man dann noch Ausführrechte
{% highlight bash %}
root# chmod +x /etc/openvpn/easy-rsa/keys/maketar.sh
{% endhighlight %}
Nun kann man einfach in zwei Schritten ein Client Zertifikat erstellen, welches man dem Client direkt übergeben kann, damit er es direkt ready-to-run auf seinem Client benutzen kann.

{% highlight bash %}
root# ./build-key client2
root# cd keys/
root# ./maketar.sh client2
{% endhighlight %}

Jetzt befindet sich ein Tarball im **keys/** Verzeichnis mit dem Namen **client2.tar.gz**. Diesen Tarball muss der Client nur dann nach Zustellung nur noch entpacken.

Auf dem Server startet man noch den Dienst und aktiviert ihn beim Systemstart. Je nach Distribution und Init System geht das wie folgt:
{% highlight bash %}
root# systemctl start openvpn@server.service
root# systemctl enable openvpn@server.service
{% endhighlight %}
oder für SysVinit basierte Systeme
{% highlight bash %}
root# update-rc.d openvpn defaults
root# /etc/init.d/openvpn start
{% endhighlight %}

Auf dem Client entpackt man den Tarball und führt folgende Befehle aus, um eine Verbindung mit dem Server aufzubauen.

{% highlight bash %}
user$ tar xf client2.tar.gz
user$ cd client2
user$ sudo openvpn client2.conf
{% endhighlight %}

Eine weiterführende Dokumentation zur openVPN Einrichtung findet man hier: ([klick mich](https://openvpn.net/index.php/open-source/documentation/howto.html))
