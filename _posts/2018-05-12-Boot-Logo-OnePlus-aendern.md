---
layout: post
title: Boot Logo bei einem OnePlus Smartphone unter Linux ändern
description: ein HowTo wie man das logo.bin von einem OnePlus Smartphone extrahiert
categories:
- Linux
date: 2018-05-12 19:12:00.000000000 +02:00
---
Nachdem ich das jetzt schon zum zweiten Mal mache, schreib ich das mal für die Allgemeinheit nieder.

Mit den folgenden Schritten, kann das Splash Screen Boot Logo von [OnePlus](https://www.oneplus.com/) Smartphones geändert werden-
Folgende Vorraussetzungen sind nötig:

## Vorraussetungen
* Den [gcc](https://gcc.gnu.org/) (um LogoInjector zu kompilieren). Der GCC sollte in jeder Linux Distribution im Paketmanager zu finden sein.
* die neueste Version des [LogoInjectors](https://forum.xda-developers.com/oneplus-one/themes-apps/mod-cm12-logo-bin-image-injector-v1-0-t3161139/)
    * eine kurze Anleitung, wie man den logoinjector unter Linux kompiliert habe ich [hier](https://forum.xda-developers.com/showpost.php?p=75303080&postcount=49) beschrieben. Alternativ hier eine kurze Anleitung
        1. Runterladen der [**lodepng.cpp**](https://raw.githubusercontent.com/lvandeve/lodepng/master/lodepng.cpp) und umbenennen in **lodepng.c**. Die folgende Zeile lädt die Datei automatisch als **lodepng.c** herunter.{% highlight bash %}wget -O lodepng.c -c 'https://raw.githubusercontent.com/lvandeve/lodepng/master/lodepng.cpp'{% endhighlight %}<br>
        1. Nun kopiert man sich den Sourcecode aus dem Forenpost der oben verlinkt ist und speichert ihn in eine Datei mit dem Namen **logoinjector.c**. Diese Datei legt man im selben Verzeichnis ab, wie die **lodepng.c**.
        1. Anschließend führt man folgende Befehle aus, um den *LogoInjector* zu kompilieren{% highlight bash %}gcc -c lodepng.c
gcc -fPIC lodepng.o logoinjector.c -o logoinjector{% endhighlight %}<br>
* ein OnePlus Smartphone mit Root Zugriff
* [adb](https://developer.android.com/studio/command-line/adb)

## Extrahieren der Logo Partition vom Smartphone
Um das Boot Logo (oder ein beliebig anderes Bild aus der Systempartition) zu tauschen, muss man dieses erst aus der Partition extrahieren.
Das geht mit folgendem Befehl über die Android shell (mit einem lokalen Terminal oder bequemer mit adb shell
{% highlight bash %}
user$ dd if=/dev/block/platform/msm_sdcc.1/by-name/LOGO of=/sdcard/logo.bin
{% endhighlight %}

## Extrahieren der Bilddateien der Logo Partition
Anschließend können die einzelnen Bilddateien mit dem logoinjector auf der Linux Kommandozeile extrahiert werden.
{% highlight bash %}
user$ logoinjector -i logo.bin -d
{% endhighlight %}

Jetzt sucht man sich aus den extrahierten PNG Dateien die richtige aus, und tauscht das Bild durch das zu ersetzende aus.
Wichtig ist, dass die Pixel weiterhin 1080x1920 sind.

## Importieren der eigenen Bilddatei in das Partitionsimage

Im nächsten Schritt injeziert man die Bilddatei in Binärdatei.
Wichtig ist, das man die Endung .png weglässt. Das liegt wahrscheinlich an der Programmierung des Programms.

{% highlight bash %}
logoinjector -i logo.bin -j /pfad/zum/png_ohne_Endung
{% endhighlight %}

Hat es geklappt, gibt einem das Programm eine kleine Rückmeldung.
</br>
## Verändertes Logo Partitionsimage zurück auf die Partition des OnePlus Smartphone schreiben
Im letzten Schritt schreibt man die Partition wieder aufs Handy
Dazu nutzen wir wieder die lokale Shell oder adb. Wichtig ist, dass euer Handy gerootet bzw. root Zugriff hat.
Ansonsten kann die Datei nicht auf den Flash Speicher geschrieben werden.

{% highlight bash %}
user$ su -
{% endhighlight %}
Ggf. kommt ein Dialog, wo ihr dem Terminal Root Zugriffe gewähren müsst. Falls ihr adb nutzt, muss vorher der Root Zugriff per ADB in den Entwicklereinstellungen gewährt werden.
Stellt sicher, dass der Zielpfad existiert, bevor ihr die Partition des Flashspeichers mit dd überschreibt.
{% highlight bash %}
root# ls -l /dev/block/platform/msm_sdcc.1/by-name/LOGO
{% endhighlight %}

Hat "ls" sich erfolgreich zurückgemeldet, kann die Partition überschrieben werden.
{% highlight bash %}
root# dd if=/sdcard/logo.bin of=/dev/block/platform/msm_sdcc.1/by-name/LOGO
{% endhighlight %}

Anschließend starten wir das Handy neu, um das Ergebnis zu sehen.
Das geht wahlweise auf dem Terminal mit dem Befehl "reboot" oder ganz normal über das Power Menü des Smartphones.
