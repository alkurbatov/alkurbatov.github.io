---
title: "Smplayer и полочки в стиле Mac"
date: 2011-01-02 13:33:00 +0300
tags: cairo-dock linux smplayer
---
Поставил я себе интерфейс в виде полочек как у Mac OS и было мне счастье (использую Cairo-Dock), но не долго. В целом все хорошо, но вот картинка в smplayer стала полностью прозрачной и никакими плясками с настройками не лечится. Замена видеопригрывателя на totem не самый лучший вариант в силу низкого функционала. Но решение все-таки есть (за что большое спасибо официальному форуму ubuntu).
<!--more-->

1. Открываем терминал и становимся root'ом.
2. Выполняем следующую последовательность команд:
{% highlight bash %}
$ bash -c "cat > /usr/bin/smplayer.helper" <<EOF
export XLIB_SKIP_ARGB_VISUALS=1
exec smplayer.real "\$@"
EOF
{% endhighlight %}
Таким образом мы создали файл, изменяющий переменную окружения перед запуском smplayer. Далее идет вызов самого проигрывателя.
3. Теперь необходимо дать файлу права на запуск и подменить вызовы smplayer запуском нашего нового файла (при помощи создания ссылки). Для этого пишем следующее:
{% highlight bash %}
$ chmod 755 /usr/bin/smplayer.helper
$ mv /usr/bin/smplayer{,.real}
$ ln -sf smplayer.helper /usr/bin/smplayer
{% endhighlight %}

После этого глюки с прозрачностью пропадают и настает нам минисчастье)