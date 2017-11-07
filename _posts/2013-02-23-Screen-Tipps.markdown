---
layout: post
title: Screen Tipps
categories:
- Linux
date: 2013-02-23 18:02:00.000000000 +01:00
---
Seit ich auf einen Tiling Windowmanager umgestiegen bin, hab ich auch [screen](http://www.gnu.org/software/screen/) zu schätzen gelernt. Screen ist ein Windowmanager auf Kommandozeilenebene. Man kann von verschiedenen Shells auf die screen Session zugreifen, da screen eine serielle Konsole öffnet. Somit ist das Arbeiten auf einem Terminal mit zwei oder mehreren Personen möglich. So hab ich screen auch kennengelernt.
Aber es kann noch mehr. Man kann innerhalb der screen Session mehrere Shells öffnen und zwischen diesen hin- und herwechseln. Das ist momentan das Feature, welches ich am meisten gebrauche. Oft ist der Einstieg in komplexe Programme wie [VIM](http://www.vim.org/) oder screen nicht ganz einfach. Deswegen will ich euch hier ein paar Tastenkombinationen zeigen, die ich ständig nutze:

Als erstes müsst ihr screen installieren. Das macht ihr mit der Paketverwaltung eurer Distribution. 

Unter openSUSE sieht das so aus:
{% highlight bash %}
user$ sudo zypper install screen
{% endhighlight %}

Starten könnt ihr die screen Session folgendermaßen. Es wird zwischen Groß- und Kleinschreibung unterschieden. Daher muss ein großes S als Parameter eingetippt werden. Anschließend befindet man sich bereits in der screen Session.

{% highlight bash %}
user$ screen -S $SESSIONNAME
{% endhighlight %}
Um einer bestehenden Session beizutreten nutzt man folgendes Kommando:

{% highlight bash %}
user$ screen -x $SESSIONNAME
{% endhighlight %}

Wie gesagt. Das funktioniert von unterschiedlichen Shells und Maschinen aus. Zum Beispiel von zwei verschiedenen SSH Verbindungen.

Um die screen Session wieder zu verlassen müsst ihr folgende Tastenkombination drücken:

**STRG** + **a** &#124; **d**

Ein neues Fenster in der Session öffnet ihr folgendermaßen:

**STRG** + **a** &#124; **c**

Das funktioniert beliebig oft. Um zwischen dem letzten und dem aktuellen Fenster hin und her zu schalten verinnerlicht folgende Tastenkombination: 

**STRG** + **a** &#124; **STRG** + **a**

Um immer zum nächsten Fenster zu schalten müsst ihr das drücken:

**STRG** + **a** &#124;  **n**

*n* steht wahrscheinlich für *next*.  Natürlich gibt es auch eine Kombination für das vorherige Fenster. Für was *p* steht, dürft ihr selbst raten.

**STRG** + **a** &#124;  **p**

Eine Alternative um zum nächsten Fenster zu welchseln ist folgende:

**STRG** + **a** &#124;  **Leertaste**

Meiner Meinung nacht ist diese Kombination besser zu drücken, als mit *n* Taste.
Um ein Fenster in der Session umzubennen drück folgendes:

**STRG** + **a** &#124; **Shift** + **a**

Anschließend kommt unten eine Leiste wo ihr den Fenstertitel umbenennen könnt.
Um einen Überblick zu bekommen, welche Fenster in der Session offen sind, drückt ihr folgendes

**STRG** + **a** &#124;  **w**

Dazu gibt es noch eine Alternative Anzeige mit interaktiver Fensterauswahl. Wirklich nützlich ist diese aber nur, wenn man seinen screen Fenstern vernünftige Namen verpasst hat.

**STRG** + **a** &#124; **Shift** + **2**

Installiert euch screen und probiert es einfach aus. Um screen grundlegend zu bedienen werden die Befehle ausreichen. Um tiefer einzusteigen hab ich leider keinen speziellen Tipp. Ich denke aber im Internet gibt bestimmt HowTos und Anleitungen die tiefer aufs Thema eingehen. Außerdem gibt es ja noch die guten alten Manpages.
