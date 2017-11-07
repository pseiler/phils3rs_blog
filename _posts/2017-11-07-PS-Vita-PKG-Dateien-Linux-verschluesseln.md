---
layout: post
title: PS Vita PkgDecrypt unter Linux kompilieren

categories:
- Technik
- Linux
date: 2017-11-07 14:45:00.000000000 +02:00
---

Man glaubt es kaum, aber mein Blog lebt tatsächlich noch. Diesmal geht es ums kompilieren des Programms [PkgDecrypt](https://github.com/weaknespase/PkgDecrypt), welches PS Vita Software entschlüsseln kann, die man von der Sony Seite heruntergeladen hat. Um die Software kompilieren zu können, lädt man sich zunächst den letzten Software Release herunter [[Source Code (tar.gz)]](https://github.com/weaknespase/PkgDecrypt/archive/v1.3.2.tar.gz) und entpackt ihn. Die benötigten Abhängigkeiten, die man zum kompilieren der Software benötigt, wären **cmake**, **make**, **zlib-devel**, **gcc** und **gcc-c++**
Unter openSUSE führt man zum installieren der Abhängigkeiten folgenden Befehl aus:

{% highlight bash %}
user$ sudo zypper install gcc gcc-c++ cmake make zlib-devel
{% endhighlight %}

Nun wechselt man in das Softwareverzeichnis und lädt folgenden Patch herunter [add\_c\_version.patch](https://phils3r.de/add_c_version.patch).
{% highlight bash %}
user$ wget -c 'https://phils3r.de/add_c_version.patch'
{% endhighlight %}

Dieser Patch forciert den C Standard, der zum kompilieren genutzt wird. Neuere C Standards erlauben eine Progrmamierung, wie sie in diesem Programm genutzt wird, nicht mehr. 

Anschließend spielt man den Patch ein und führt die gängigen Befehle zum komplilieren der Software aus:

{% highlight bash %}
user$ patch -p1 < add_c_version.patch
user$ mkdir build
user$ cd build
user$ cmake ..
user$ make
user$ sudo make install
{% endhighlight %}

Damit sollten die beiden notwendigen Binärdateien (*make_key*, *pkg_dec*) unter */usr/local/bin/* zu finden sein.
Natürlich kann man die Software auch paketieren, was ich für openSUSE auch getan habe. Dieses findet man [hier](https://software.opensuse.org/package/pkgdecrypt).
