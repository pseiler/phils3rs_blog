---
layout: post
title: Twitch Video Download / mit Linux und FFmpeg "MPEG Streams" verbinden
description: Toolchain um Videos von Twitch herunterzuladen, um sie anschließend zu konvertieren.
categories:
- Technik
- Linux
date: 2016-06-07 17:45:00.000000000 +02:00
---
Desöfteren stand ich schon vor dem Problem, dass ich einen Twitch Stream herunterladen wollte. Leider hab ich keine Möglichkeit gefunden, das bequem per Webseite zu erledigen. Twitch hat das Streaming Backend geändert (HLS VoD system), um Downloads oder sonstige Manipulation zu erschweren. Ich habe dennoch eine Lösung gefunden, um ein Stream Archiv (VoD) runterzuladen und zu schneiden. 

Es wird eine Kombination aus drei Komponenten verwendet:

* die Webseite [VODcutter](http://twitch.center/vodcutter) - generiert Download Links der einzelnen 15 Minuten Stücke
* *wget* - um die Dateien herunterzuladen
* *ffmpeg* - um die einzelnen Stücke aneinanderzuheften
* optional: ein Schneideprogramm wie [OpenShot](http://openshot.org/) umd die Datei anschließend zu bearbeiten
* optional: *mediainfo* - um Codecinformationen der Dateien auszulesen (z.B. um Audio und Videoqualität zu ermitteln)


Zuerst besucht man die Seite [VODcutter](http://twitch.center/vodcutter) um die Downloadliste zu generien. Dazu sucht ihr die ID oder den ganzen Link zum VoD/Video raus und fügt sie ins erste Feld der Seite.

Die Felder Start- und Endzeit müssen richtig ausgefüllt werden. Um das ganze Video abzudecken, sollte bei Startzeit 0:00:00h eingegeben werden, und bei der Endzeit ein beliebiger Wert, der länger als das Video ist. Bei einem 4:45:12h langen Video entweder genau den Wert, oder irgendwas höheres. Beispielsweise 10:00:00h.
Nun wählt man noch die Qualität für den Download (in der Regel möchte man "Source" Qualität).
Anschließend klickt man auf "Generate" und eine Liste von Dateien und eine Export Möglichkeit erscheint. Wir möchten die einzelnen Stücke als Liste von Links, also wählen wir direkt unter *Export* *"URLs"*

Eine URL Liste erscheint, die wir kopieren und per Editor in eine Datei schreiben. Die Liste wird benutzt, um alle Links mit *wget* nacheinander in das aktuelle Verzeichnis herunterzuladen.
{% highlight bash %}
wget -c -i /pfad/zur/download_liste
{% endhighlight %}

Anschließend benennen wir die Datein noch um:
{% highlight bash %}
x=1; for i in *.ts*; do echo "$i -> ${x}.ts"; mv $i ${x}.ts; x=$(($x+1)); done
{% endhighlight %}
Im Detail passiert folgendes:
Zuerst wird die Variable "x" und deren Wert "1" definiert. Anschließend wird eine For-Schleife genutzt, um um alle Dateien im aktuellen Verzeichnis, die den String "*.ts*" enthält, anzusprechen. Die Datein werden mithilfe des Befehls "mv" in den Wert von "x" + einer Dateiendung umbenannt. Beim ersten Durchlauf ist es der Wert "1". Anschließend wird der Wert von "x" um eins erhöht. Beim zweiten Durchlauf wird die zweite Datei angesprochen und der Wert beträgt "2".
Die Zieldateien sehen dann so aus:
{% highlight bash %}
1.ts
2.ts
[...]
{% endhighlight %}

Nun ist es an der Reihe, aus den einzelnen Dateien, eine große ganze zu machen. Dazu benötigen wir "FFmpeg". FFmpeg ist ein Video und Audio De- und Encoder. Mit FFmpeg kann nahezu jede Audio oder Video Datei in ein anderes Format convertiert werden. Auch beherrscht es das aneinanderreihen von MPEG Streams, was wir für unser aktuelles Projekt benötigen. Beim Aneinanderheften der einzelnen Dateien, wird im Falle der Videospur nichts konvertiert, sondern nur wirklich aneinandergeheftet. Das ist durch den MPEG Codec möglich. Da dieser aus dem Fernsehbereich stammt und somit beim abspielen nicht wissen muss, an welcher Stelle der Datei es sich gerade befindet. Das ist widerum auch für Streaming interessant. Eigentlich müsste das auch mit Audio funktionieren, nur fehlt der Ton in der aneinandergehefteten Datei dann. Das umgehen wir, indem wir beim einanderheften die Audiospur neu als MP3 convertieren. Vorher ist es interessant, welche maximale Audioqualität die Quelldateien enhalten. An der Stelle kommt "mediainfo" zum Einsatz. Das sollte sich in allen gängigen Linuxdistributionen in der Paketverwaltung befinden. 

{% highlight bash %}
mediainfo /pfad/zu/einem/Videostueck
{% endhighlight %}

Für uns interessant ist hier der Audio Codec.
Hier erkennt man die Bitrate, die man in der Zieldatei so beibehalten kann (oder ggf. verringern).
Hat man die Audio Bitrate herausgefunden, können die Dateien zusammengefügt werden. Falls die Bitrate variabel ist, wählt man im Zweifel mittlere Qualität. 

Bevor wir die Dateien zusammenfügen, benötigen wir zuerst den richtigen String für den späteren FFmpeg Befehl um die Dateien anzugeben.
Dazu hab ich folgendes Script geschrieben:
(Da gibt es bestimmt eine bessere Lösung. Wenn jemand was weiß, schreibt mir ne E-Mail.)

{% highlight bash %}
#!/bin/bash
STRING="1.ts"
for i in $(seq 2 $1)
do
    STRING=${STRING}$(printf "|${i}.ts");
done

echo $STRING
{% endhighlight %}

Das erste Argument ist die letzte angewählte Datei in der Sequenz. Also die Datei mit der letzten Nummer.
Beispielsweise:

{% highlight bash %}
user$ bash string_generator.sh 100
{% endhighlight %}
 
In meinem Fall ist die letzte Datei 100.ts.

Folgender Befehl wird genutzt um die Datei zusammenzufügen. Dazu wird ein installiertes FFmpeg benötigt. Gut wäre es, wenn FFmpeg mit patentierten Codecs gebaut wurde. In Europa stellt das kein Problem dar. In der folgenden Zeile gehört der Output des oben benutzen Scripts für dei Dateiangabe nach dem *"concat:"* hin.

{% highlight bash %}
ffmpeg -i "concat:1.ts|2.ts|3.ts" -c copy -acodec libmp3lame -ab 192k -ar 44100 output.mpg
{% endhighlight %}

Als Output Audio Codec kann gerne etwas anderes genutzt werden. Ich habe hier der Einfachheit halber mp3 genutzt.
Die Datei output.mpg kann dann für die weitere Bearbeitung genutzt werden. Ich empfehle für einfache Schneidearbeiten OpenShot. Dieses Videoschnitt- und Bearbeitungsprogramm hat sich bei mir unter Linux bewährt. 
Ich hoffe ich konnte jemand mit meiner Anleitung helfen. 
Mal sehen ob ich wieder öfter zum schreiben komme.
