---
layout: post
title: SrcDS unter openSUSE
categories:
- Gaming
date: 2014-01-27 18:30:00.000000000 +01:00
---
Zeit mal wieder was zu posten.
ist ja schon so lang her.
Diesmal geht es darum wie man einen Counter-Strike:Global Offensive Linux Server mit SrcDS (Source Dedicated Server) und der steamcmd aufsetzt.

Als erstes wird der Tarball benötigt.

[steamcmd_linux.tar.gz](http://media.steampowered.com/installer/steamcmd_linux.tar.gz)

Man erstellt am besten ein Verzeichnis namens steamcmd und verschiebt den Tarball in das Verzeichnis.
Anschließend entpackt man den Tarball.

{% highlight bash %}
tar xfz steamcmd_linux.tar.gz
{% endhighlight %}

Hier findet man eine Datei namens **steamcmd.sh**
Diese führt man direkt aus und es wird ein update heruntergeladen.

{% highlight bash %}
./steamcmd.sh
{% endhighlight %}

Jetzt kann man sich ohne Account einloggen und die Dedicated Server Dateien runterladen. Das funktioniert beispielsweiße bei CS:GO aber nicht bei jedem Spiel (hier wird ein steam User, Passwort und gültige Spielelizenz benötigt.
{% highlight bash %}
Steam> login anonymous
{% endhighlight %}

Man wählt noch den Pfad in welches Verzeichnis der Dedicated Server heruntergeladen werden soll und schon gehts los.
Die passende AppID für CS:GO ist die **740**.

{% highlight bash %}
Steam> force_install_dir ./csgo-server/
Steam> app_update 740 validate
{% endhighlight %}

Das kann jetzt eine Weile dauern, aber anschließend kann man schon ins oben konfigurierte Verzeichnis wechseln um den Server zu starten.

Eine passende Kommandozeile für den Serverstart gibts noch hier (startet ein Public Community Casual Map Modus:
{% highlight bash %}
./srcds_run -game csgo -console -usercon +ip$SERVERIP +game_type 0 +game_mode 0 +mapgroup mg_bomb +map de_inferno
{% endhighlight %}

Hierbei ist wichtig das ihr unbedingt die IP angebt auf dem der Server lauschen soll. Ich persönlich hatte das Problem, das ich mich ansonsten nicht auf den Server verbinden konnte, obwohl er erreichbar war und funktioniert hat.

Zusätzlich hatte ich noch Probleme dass das Serverbinary bei jedem Startversuch gecrasht ist. Ich habe aber nach langem Suchen eine Lösung für das Problem gefunden.
Das Problem war das Paket **aaa_base-malloccheck** welches ich dann deinstalliert habe. Anschließend crasht das binary auch nicht mehr.

{% highlight bash %}
sudo zypper rm aaa_base-malloccheck
{% endhighlight %}

Auf der openSUSE Mailing Liste hab ich die Lösung gefunden. Ich würde die Seite hier auch gern verlinken, leider finde ich sie nicht mehr.
/e: Gefunden. Unten bei links die #5

Anschließend kann man noch diverse Konfigurationen mit der **server.cfg** überschreiben.

Diese liegt unter

{% highlight bash %}
./csgo-server/csgo/cfg/server.cfg
{% endhighlight %}

Hier dazu ein paar Beispiele:
{% highlight bash %}
// Set Region and Internet Activity
sv_lan 0 // erzwingt die Anmeldung an die Master Server
sv_region 3 // Setzt die Region auf Europa
writeid // loggt die Benutzer die sich verbinden
writeip // loggt die IPs die sich verbinden
exec banned_user.cfg // lädt gebannte User beim Start
exec banned_ip.cfg // lädt gebannte IPs beim Start
log on // loggt die Server Aktivität

// Set Basic Information
hostname "Phils3r.de 5on5" // Setzt den Servernamen
rcon_password "$PRIVATES_PW" // Setzt das RCON (Remote login) Passwort
sv_password "kaugummi" // Setzt ein Server Password


// configurate Bots
bot_difficulty 2
bot_chatter "off"
bot_join_after_player 0 // Bots verbinden sich nach dem User
bot_quota "0" // maximale Anzahl an Bots
bot_quota_mode "0" // Stellt ein Bot Gleichgewicht her
//**The following commands manage kicks and bans

//performance configuration
fps_max "600" // konifguriert den Server das er mit der maximal möglichen FPS Leistung läuft.
{% endhighlight %}

Weiter Konfigurationsvariablen und Startoptionen können hier nachgelesen werden.

* [Alle CS:GO Konsolenbefehle für die Serverkonfiguration](http://cs-go-download.blogspot.de/2012/08/cs-go-konsolenbefehle.html)
* [Ausführlicheres SteamCMD Tutorial](https://developer.valvesoftware.com/wiki/SteamCMD)
* [Valves CS:GO DS Anleitung](https://developer.valvesoftware.com/wiki/Counter-Strike:_Global_Offensive_Dedicated_Servers)
* [SrcDS Startoptionen](https://developer.valvesoftware.com/wiki/Command_Line_Options#Source_Dedicated_Server)
* [openSUSE Mailinglisten Archiv](http://lists.opensuse.org/opensuse-bugs/2011-11/msg04945.html)

Viel Spass beim zocken auf dem eigenen Server wünsch ich euch

Philipp

