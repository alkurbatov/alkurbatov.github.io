---
title: "Создание загрузочной флешки на базе CentOs 6+"
date: 2013-01-17 13:33:00 +0300
tags: linux centos
---
Существует несколько способов создания загрузочных флешек на базе CentOs, однако все они весьма трудоемки. Наиболее простой и быстрый способ - использование скрипта livecd-iso-to-disk, идущего в комплекте с образами CentOs 6.3 (для CentOs 5.+ этот способ не подходит).
<!--more-->

1. Достать скрипт из образа *.iso CentOs 6.+
2. Отформатировать флешку в FAT32 (на флешке должен быть один раздел).
3. Проверить, что флешка не примонтирована.
4. Установить extlinux, isomd5sum (опционально).
5. Выполнить команду:
{% highlight bash %}
# CentOS-6.3-i386-minimal.iso - образ CentOs
# /dev/sdb1 - наша флешка
$ ./livecd-iso-to-disk --format --reset-mbr CentOS-6.3-i386-minimal.iso /dev/sdb1
{% endhighlight %}

Подробнее о других способах создания загрузочной флешки можно прочитать [здесь](http://wiki.centos.org/HowTos/InstallFromUSBkey)