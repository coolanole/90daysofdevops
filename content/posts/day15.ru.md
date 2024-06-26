---
title: 15. Команды Linux в DevOps
description: Команды Linux в DevOps
toc: true
authors:
tags: [devops, linux]
categories:
series: 
date: "2022-05-05"
lastMod: "2022-05-05"
featuredImage:
draft: false
id: 1048834
weight: 15
---

## Команды Linux для DevOps

Я упомянул [вчера](../day14), что мы собираемся провести много времени в терминале с некоторыми командами, чтобы что-то сделать.

Я также упомянул, что с нашей виртуальной машиной, подготовленной  с помощью vagrant, мы можем использовать `vagrant ssh` и получить доступ к нашей машине. Вам нужно будет находиться в том же каталоге, из которого мы его предоставили.

Для SSH нам не понадобятся имя пользователя и пароль, они понадобятся нам только в том случае, если решим войти в консоль Virtual Box.

Вот где мы хотим быть, как показано ниже:

![](../images/Day15_Linux1.ru.png?v1)

## Команды

Очевидно, что я не могу охватить здесь все команды. Есть тонны документации, которые охватывают их, но также, если вы находитесь в своем терминале, и вам просто нужно понять параметры конкретной команды, у нас есть команда `man`, сокращенная от manual. Мы можем использовать это, чтобы просмотреть каждую из команд, которые мы коснемся в этом посте, чтобы узнать больше вариантов для каждой из них. Мы можем запустить `man man`, который поможет вам со страницами руководства. Чтобы выйти из справочных страниц, вы должны нажать `q` для выхода.

Примеры:

```
man ls
man whoami
...
```

![](../images/Day15_Linux2.ru.png?v1)
![](../images/Day15_Linux3.ru.png?v1)

`sudo` Если вы знакомы с Windows и щелкаете правой кнопкой мыши по `запустить от имени администратора`, мы можем думать о `sudo` как об этом. Когда вы запускаете команду с помощью этой команды, вы будете запускать ее как «root», она запросит у вас пароль перед запуском команды.

![](../images/Day15_Linux4.ru.png?v1)

Для разовых работ, таких как установка приложений или служб, вам может понадобиться эта команда sudo, но что, если у вас есть несколько задач, и вы хотите какое-то время пожить как sudo? Здесь вы можете снова использовать `sudo su` так же, как `sudo`, после ввода вам будет предложено ввести пароль `root`. В тестовой виртуальной машине, такой как наша, это нормально, но мне было бы очень сложно работать как «root» в течение длительного времени, могут произойти плохие вещи. Чтобы выйти из этого возвышенного положения, вы просто набираете «exit».

![](../images/Day15_Linux5.ru.png?v1)

Я ловлю себя на том, что все время использую `clear`. Команда `clear` делает именно то, о чем говорит: она очищает экран от всех предыдущих команд, помещая курсор наверх и предоставляя вам красивое чистое рабочее пространство. Windows, это «cls» в .mdprompt.

![](../images/Day15_Linux6.ru.png?v1)

Давайте теперь посмотрим на некоторые команды, с помощью которых мы можем создавать вещи в нашей системе, а затем визуализировать их в нашем терминале. Прежде всего, у нас есть `mkdir`, это позволит нам создать папку в нашей системе. С помощью следующей команды мы можем создать папку в нашем домашнем каталоге с именем Day15 `mkdir Day15`

![](../images/Day15_Linux7.ru.png?v1)

С помощью `cd` это позволяет нам изменить каталог, поэтому для перехода в наш вновь созданный каталог мы можем сделать это с помощью вкладки `cd Day15`, которая также может использоваться для автозаполнения доступного каталога. Если мы хотим вернуться к тому, с чего начали, мы можем использовать `cd ..`

![](../images/Day15_Linux8.ru.png?v1)

`rmdir` позволяет нам удалить каталог, если мы запустим `rmdir Day15`, тогда папка будет удалена (обратите внимание, что это будет работать, только если у вас ничего нет в папке)

![](../images/Day15_Linux9.ru.png?v1)

Я уверен, что все мы делали это, когда мы переходили в глубины нашей файловой системы в каталог и не знали, где мы находимся. `pwd` дает нам распечатку рабочего каталога, pwd, насколько это похоже на пароль, означает печать рабочего каталога.

![](../images/Day15_Linux10.ru.png?v1)

Мы знаем, как создавать папки и каталоги, но как мы создаем файлы? Мы можем создавать файлы с помощью команды «touch», если бы мы запускали «touch Day15», это создало бы файл. Игнорируйте `mkdir`, мы еще увидим это позже.

![](../images/Day15_Linux11.ru.png?v1)

`ls` Я могу поставить на это свой дом, вы будете использовать эту команду так много раз, что она выведет список всех файлов и папок в текущем каталоге. Давайте посмотрим, сможем ли мы увидеть тот файл, который мы только что создали.

![](../images/Day15_Linux12.ru.png?v1)

Как мы можем найти файлы в нашей системе Linux? `locate` позволит нам искать в нашей файловой системе. Если мы используем `locate Day15`, он сообщит о местонахождении файла. Бонусом является то, что если вы знаете, что файл существует, но вы получаете пустой результат, запустите `sudo updatedb`, который проиндексирует все файлы в файловой системе, а затем снова запустите `locate`. Если у вас нет `locate`, вы можете установить его с помощью этой команды `sudo apt install mlocate`

![](../images/Day15_Linux13.ru.png?v1)

Как насчет перемещения файлов из одного места в другое? `mv` позволит вам перемещать ваши файлы. Пример `mv Day15 90DaysOfDevOps` переместит ваш файл в папку 90DaysOfDevOps.

![](../images/Day15_Linux14.ru.png?v1)

Мы переместили наш файл, но что, если мы хотим переименовать его сейчас во что-то другое? Мы можем сделать это снова с помощью команды `mv`. Мы можем просто использовать `mv Day15 day15`, чтобы перейти к верхнему регистру, или мы могли бы использовать `mv day15 AnotherDay`, чтобы полностью изменить его, теперь используйте `ls` для проверки файла.

![](../images/Day15_Linux15.ru.png?v1)

Хватит, теперь давайте избавимся (удалим) от нашего файла и, возможно, даже от нашего каталога, если он у нас есть. `rm` просто `rm AnotherDay` удалит наш файл. Мы также будем использовать `rm -R`, который будет рекурсивно работать через папку или местоположение. Мы также можем использовать `rm -R -f`, чтобы принудительно удалить все эти файлы. Спойлер, если вы запустите `rm -R -f /`, добавьте к нему sudo, и вы можете попрощаться со своей системой ....!

![](../images/Day15_Linux16.ru.png?v1)

Мы рассмотрели перемещение файлов, но что, если я просто хочу скопировать файлы из одной папки в другую, просто скажу, что это очень похоже на команду `mv`, но мы используем `cp`, чтобы теперь мы могли сказать `cp Day15 Desktop`

![](../images/Day15_Linux17.ru.png?v1)

Мы создали папки и файлы, но на самом деле мы не поместили никакого содержимого в нашу папку, мы можем добавить содержимое несколькими способами, но самый простой способ - это `echo`, мы также можем использовать `echo`, чтобы распечатать много вещей в нашей папке. терминал, я лично часто использую эхо для вывода системных переменных, чтобы узнать, установлены они или нет. мы можем использовать `echo "Hello #90DaysOfDevOps" > Day15`, и это добавит это в наш файл. Мы также можем добавить к нашему файлу, используя `echo "Commands are fun!" >> День15`

![](../images/Day15_Linux18.ru.png?v1)

Еще одна из тех команд, которые вы будете часто использовать! `кошка` сокращение от конкатенации. Мы можем использовать `cat Day15`, чтобы увидеть содержимое внутри файла. Отлично подходит для быстрого чтения этих файлов конфигурации.

![](../images/Day15_Linux19.ru.png?v1)

Если у вас есть длинный сложный файл конфигурации, и вы хотите или вам нужно найти что-то быстрое в этом файле, а не читать каждую строку, тогда `grep` вам в помощь, это позволит нам искать в вашем файле определенное слово, используя `cat Day15 | grep "#90DaysOfDevOps"`

![](../images/Day15_Linux20.ru.png?v1)

Если вы похожи на меня и часто используете эту команду `clear`, то вы можете пропустить некоторые из ранее запущенных команд, мы можем использовать «историю», чтобы узнать все те команды, которые мы запускали ранее. `history -c` удалит историю.

Когда вы запускаете `history` и хотите выбрать конкретную команду, вы можете использовать `!3`, чтобы выбрать 3-ю команду в списке.

Вы также можете использовать `history | grep "Команда"` для поиска чего-то определенного.

На серверах для отслеживания времени выполнения команды может быть полезно добавлять дату и время к каждой команде в файле истории.

Следующая системная переменная управляет этим поведением:

```
HISTTIMEFORMAT="%d-%m-%Y %T "
```

Вы можете легко добавить ее в свой bash_profile:

```
echo 'export HISTTIMEFORMAT="%d-%m-%Y %T "' >> ~/.bash_profile
```

Можем увеличить размер файла для хранения истории:

```
echo 'export HISTSIZE=100000' >> ~/.bash_profile
echo 'export HISTFILESIZE=10000000' >> ~/.bash_profile
```

![](../images/Day15_Linux21.ru.png?v1)

Нужно сменить пароль? `passwd` позволит нам изменить наш пароль. Обратите внимание, что когда вы добавляете свой пароль таким образом, когда он скрыт, он не будет отображаться в `history`, однако, если ваша команда имеет `-p ПАРОЛЬ`, тогда он будет виден в вашей `history`.

![](../images/Day15_Linux22.ru.png?v1)

Мы также можем добавить новых пользователей в нашу систему, мы можем сделать это с помощью `useradd`, мы должны добавить пользователя с помощью нашей команды `sudo`, мы можем добавить нового пользователя с помощью `sudo useradd NewUser`

![](../images/Day15_Linux23.ru.png?v1)

Для повторного создания группы требуется `sudo`, и мы можем использовать `sudo groupadd DevOps`, тогда, если мы хотим добавить нашего нового пользователя в эту группу, мы можем сделать это, запустив `sudo usermod -a -G DevOps` `-a` is add а `-G` это имя группы.

![](../images/Day15_Linux24.ru.png?v1)

Как добавить пользователей в группу `sudo`? Это было бы очень редким случаем но для того, чтобы сделать это, выполним: `usermod -a -G sudo NewUser`

### Права / Permissions

read, write and execute - — это права доступа ко всем нашим файлам и папкам в нашей системе Linux.

Полный список:

- 0 = None `---`
- 1 = Execute only `--X`
- 2 = Write only `-W-`
- 3 = Write & Exectute `-WX`
- 4 = Read Only `R--`
- 5 = Read & Execute `R-X`
- 6 = Read & Write `RW-`
- 7 = Read, Write & Execute `RWX`

Вы также увидите «777» или «775», и они представляют те же числа, что и в приведенном выше списке, но каждый из них представляет **User - Group - Everyone***

Давайте посмотрим на наш файл. `ls -al Day15` вы можете увидеть 3 группы, упомянутые выше, пользователь и группа могут читать и изменять (write), но все остальыне только читать (read).

![](../images/Day15_Linux25.ru.png?v1)

Мы можем изменить это с помощью `chmod`, вы можете сделать это, если вы также создаете двоичные файлы в своих системах, и вам нужно дать возможность запускать эти двоичные файлы. `chmod 750 Day15` теперь запустите `ls -la Day15`, если вы хотите запустить это для всей папки, вы можете использовать `-R`, чтобы сделать это рекурсивно.

![](../images/Day15_Linux26.ru.png?v1)

Как насчет смены владельца файла? Мы можем использовать «chown» для этой операции, если мы хотим изменить владельца нашего «Day15» с пользователя «vagrant» на «NewUser», мы можем запустить «sudo chown NewUser Day15» снова, можно использовать «-R».

![](../images/Day15_Linux27.ru.png?v1)

Команда, с которой вы столкнетесь, это `awk`, где она реально используется, когда у вас есть выходные данные, из которых вам нужны только определенные данные. например, запуская who, мы получаем строки с информацией, но, возможно, нам нужны только имена. Мы можем запустить `кто | awk '{print $1}'`, чтобы получить только список этого первого столбца.

![](../images/Day15_Linux28.ru.png?v1)

Если вы хотите читать потоки данных из стандартного ввода, то генерирует и выполняет командные строки; это означает, что он может принимать вывод команды и передавать его в качестве аргумента другой команды. `xargs` — полезный инструмент для этого случая использования. Если, например, мне нужен список всех учетных записей пользователей Linux в системе, которую я могу запустить. `cut -d: -f1 < /etc/passwd` и получите длинный список, который мы видим ниже.

![](../images/Day15_Linux29.ru.png?v1)

Если я хочу заархивировать этот список, я могу сделать это, используя `xargs` в команде вроде этой `cut -d: -f1 < /etc/passwd | sort | xargs`

![](../images/Day15_Linux30.ru.png?v1)

Я также не упомянул команду `cut`, которая позволяет нам удалять разделы из каждой строки файла. Его можно использовать для вырезания частей строки по положению байта, символу и полю. Команда `cut -d " " -f 2 list.txt` позволяет нам удалить первую букву, которая у нас есть, и просто отобразить наши числа. Есть так много комбинаций, которые можно использовать здесь с этой командой, я уверен, что потратил слишком много времени, пытаясь использовать эту команду, когда я мог бы быстрее извлечь данные вручную.

![](../images/Day15_Linux31.ru.png?v1)

Также обратите внимание, если вы вводите команду, и вы больше не довольны ею, и вы хотите начать снова, просто нажмите Ctrl + c, и это отменит эту строку и начнет все заново.

## Ресурсы

- [Learn the Linux Fundamentals - Part 1](https://www.youtube.com/watch?v=kPylihJRG70)
- [Linux for hackers (don't worry you don't need be a hacker!)](https://www.youtube.com/watch?v=VbEx7B_PTOE)

Это уже довольно большой список, но я могу с уверенностью сказать, что я использую все эти команды в своей повседневной жизни, будь то администрирование серверов Linux или мой рабочий стол Linux, это очень легко, когда вы находитесь в Windows или macOS для навигации по пользовательскому интерфейсу, но в Linux Servers их нет, все делается через терминал.
