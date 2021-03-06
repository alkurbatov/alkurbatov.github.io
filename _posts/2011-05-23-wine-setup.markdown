---
title: "Настройка wine"
date: 2011-05-23 13:33:00 +0300
tags: linux wine
---
Для корректной работы Windows-программ необходимы различные дополнения, не входящий в базовый комплект wine . Какие именно - зависит от конкретной программы. Здесь я постараюсь описать основные действия, необходимые для запуска большинства программ в wine.
<!--more-->

## Получение winetricks
Winetricks — это небольшой скрипт для установки некоторых основных компонентов (как правило, библиотек DLL и шрифтов), необходимых для некоторых приложений для правильной работы под wine. Проект wine принимает сообщения об ошибках для пользователей winetricks, в отличие от большинства сторонних приложений.

1. Скачать сам скрипт:
{% highlight bash %}
$ wget http://winetricks.org/winetricks
{% endhighlight %}
3. Устанавливаем скаченному файлу права на запуск.
4. Поместим скрипт в каталог ~/.wine просто для порядка :)


## Установка directx9
DirectX — это набор API, разработанных для решения задач, связанных с программированием под Windows. Наиболее широко используется при написании компьютерных игр. Для корректной работы большинства игр наличие в системе directx является одним из обязательных условий.

1. Открываем консоль и переходим в каталог, содержащий скрипт winetricks.
2. Установить directx:
{% highlight bash %}
$ ./winetricks directx9
{% endhighlight %}


## Установка шрифтов Windows
По понятным причинам в моем дистрибутиве (Fedora) отсутствуют шрифты Windows. К несчастью некоторым программам они нужны, поэтому будем их доустанавливать.

1. Убедиться в наличии в системе пакета cabextract и установить его при необходимости.
2. Открываем консоль и переходим в каталог, содержащий скрипт winetricks.
3. Загрузить и установить шрифты Windows в систему:
{% highlight bash %}
$ ./winetricks corefonts
{% endhighlight %}


## Запуск Starcraft 2
1. Обязательно установить directx9.
2. Для повышения производительности подключить OpenGL, добавив к команде запуска программы параметр -opengl:
{% highlight bash %}
$ wine StarCraft\ II.exe -opengl
{% endhighlight %}
3. Для корректного определения звуковых устройств нужно запустить winecfg и на закладке “Библиотеки” добавить mmdevapi с настройкой “блокировать”.
4. Для корректной работы установщика обновлений необходимо установить ie6.
5. Для улучшения качества картинки необходимо выполнить следующую серию команд:
{% highlight bash %}
$ winetricks ddr=opengl
$ winetricks multisampling=disabled
$ winetricks glsl-disable
{% endhighlight %}


## Запуск приложений в виртуальном рабочем столе wine
Многие старые программы windows не поддерживают огромные разрешения современных мониторов, поэтому выходом может стать запуск их в специальном виртуальном рабочем столе, который эмулируется wine . Кроме того, если запускаемая программа часто "падает", использовать её в полноэкранном режиме, как минимум, не безопасно, так как это может привести к зависанию графической консоли. Рабочий стол задается в настройках wine (вызов winecfg) и автоматически создается для каждого запускаемого приложения. Однако, что делать, если одни программы нам нужны в полноэкранном режиме, а другие - на виртуальном столе?

1. Открываем winecfg и убираем галочку из строки "Эмулировать виртуальный рабочий стол". Теперь все наши windows-программы будут запускаться автоматически в полноэкранном режиме.
2. Для запуска приложения в виртуальном рабочем столе необходимо набрать в консоли (или отредактировать соответствующую строку в меню приложений) следующую команду:
{% highlight bash %}
# 1024х768 - разрешение виртуального рабочего стола
# Program.exe - исполняемый файл программы, которую мы хотим запустить
wine explorer /desktop=name,1024x768 Program.exe
{% endhighlight %}


## Полезные ссылки
* [Требования для запуска игр](http://appdb.winehq.org/)
