---
title: 14. DevOps и Linux
description: DevOps и Linux
toc: true
authors:
tags: [devops, linux, virtualbox, vagrant]
categories:
series: 
date: "2022-05-04"
lastMod: "2022-05-04"
featuredImage:
draft: false
id: 1049033
weight: 14
---

## Общая картина: DevOps и Linux

Linux и DevOps имеют очень схожие культуры и взгляды; оба ориентированы на настройку и масштабируемость. Оба эти аспекта Linux имеют особое значение для DevOps.

Многие технологии начинаются с Linux, особенно если они связаны с разработкой программного обеспечения или управлением инфраструктурой.

Кроме того, многие проекты с открытым исходным кодом, особенно инструменты DevOps, с самого начала разрабатывались для работы в Linux.

С точки зрения DevOps или фактически с точки зрения какой-либо операционной роли вы столкнетесь с Linux, я бы сказал, в основном. Есть место для WinOps, но большую часть времени вы будете администрировать и развертывать серверы Linux.

Я использую Linux ежедневно в течение нескольких лет, но мой настольный компьютер всегда был либо macOS, либо Windows. Однако, когда я перешел на роль Cloud Native, в которой я сейчас нахожусь, я сделал решительный шаг, чтобы убедиться, что мой ноутбук полностью основан на Linux и является моим ежедневным драйвером, в то время как мне по-прежнему нужна была Windows для рабочих приложений и многих моих аудио и видеоаппаратура не работает в Linux Я заставлял себя постоянно работать на рабочем столе Linux, чтобы лучше понять многие вещи, которые мы собираемся затронуть в течение следующих 7 дней.

## Начало

Я не предлагаю вам делать то же самое, что и я, в любом случае, поскольку есть более простые варианты и менее разрушительные, но я скажу, что этот полный рабочий день заставит вас быстрее научиться тому, как заставить все работать в Linux.

В течение большей части этих 7 дней я фактически собираюсь развернуть виртуальную машину в Virtual Box на моей машине с Windows. Я также собираюсь развернуть настольную версию дистрибутива Linux, в то время как многие серверы Linux, которыми вы будете администрировать, скорее всего, будут серверами без графического интерфейса и полностью основанными на оболочке. Однако, как я сказал в начале, многие инструменты, которые мы рассмотрели в течение всех этих 90 дней, начинались с Linux, я также настоятельно рекомендую вам погрузиться в работу этого рабочего стола Linux для этого обучения.

В оставшейся части этого поста мы сосредоточимся на настройке и запуске виртуальной машины Ubuntu Desktop в нашей среде Virtual Box. Теперь мы можем просто загрузить [Virtual Box](https://www.virtualbox.org/) и получить последний [Ubuntu ISO](https://ubuntu.com/download) с сайтов, на которые даны ссылки, и продолжить сборку. нашу среду рабочего стола, но это не было бы очень DevOps с нашей стороны, не так ли?

Еще одна веская причина использовать большинство дистрибутивов Linux заключается в том, что они бесплатны и имеют открытый исходный код. Мы также выбираем Ubuntu, поскольку это, вероятно, наиболее широко используемый дистрибутив, не думая о мобильных устройствах и корпоративных серверах RedHat Enterprise. Я могу ошибаться, но с CentOS и ее историей я уверен, что Ubuntu занимает первое место в списке, и это очень просто.

## HashiCorp Vagrant

Vagrant — это утилита CLI, которая управляет жизненным циклом ваших виртуальных машин. Мы можем использовать vagrant для запуска и отключения виртуальных машин на разных платформах, включая vSphere, Hyper-v, Virtual Box, а также Docker. У него есть другие провайдеры, но мы будем придерживаться того, что здесь мы используем Virtual Box, так что все готово.

Vagrant — свободное и открытое программное обеспечение для создания и конфигурирования виртуальной среды разработки. Является обёрткой для программного обеспечения виртуализации, например VirtualBox, и средств управления конфигурациями, таких как Chef, Salt и Puppet.

Первое, что нам нужно сделать, это установить Vagrant на нашу машину, когда вы перейдете на страницу загрузок, вы увидите все операционные системы, перечисленные на ваш выбор. [HashiCorp Vagrant](https://www.vagrantup.com/downloads) Я использую Windows, поэтому я взял двоичный файл для своей системы и установил его в свою систему.

Далее нам также нужно установить [Virtual Box](https://www.virtualbox.org/wiki/Downloads). Опять же, это также может быть установлено на многих разных операционных системах.

## Файл VAGRANTFILE

VAGRANTFILE описывает тип машины, которую мы хотим развернуть. Он также определяет, как мы хотим, чтобы конфигурация и подготовка этой машины выглядели.

Когда дело доходит до их сохранения и организации ваших VAGRANTFILE, я стараюсь помещать их в отдельные папки в своем рабочем пространстве. Ниже вы можете увидеть, как это выглядит в моей системе. Надеюсь, после этого вы поиграете с Vagrant и увидите легкость запуска разных систем, это также отлично подходит для этой кроличьей норы, известной как скачок дистрибутива для Linux Desktops.

![](../images/Day14_Linux1.ru.png?v1)

Давайте взглянем на этот VAGRANTFILE и посмотрим, что мы строим.

```
Vagrant.configure("2") do |config|
  config.vm.box = "chenhan/ubuntu-desktop-20.04"
  config.vm.provider :virtualbox do |v|
   v.memory  = 8096
   v.cpus    = 4
   v.customize ["modifyvm", :id, "--vram", "128mb"]
  end
end
```

Это очень простой VAGRANTFILE. В целом, мы говорим, что нам нужна конкретная «сборка». Сборка, возможно, является либо общедоступным образом, либо частной сборкой системы, которую вы ищете. Вы можете найти длинный список здесь, в [общедоступном каталоге Vagrant](https://app.vagrantup.com/boxes/search)

Далее мы говорим, что хотим использовать определенного провайдера, в данном случае это «VirtualBox», а затем мы хотим определить память нашей машины как «8 ГБ, а количество процессоров — как «4». Мой опыт также говорит мне, что вы можете также добавить следующую строку, если у вас возникли проблемы с отображением. Это установит видеопамять на то, что вы хотите, я бы увеличил ее до 128 МБ, но зависит от вашей системы.

```

v.customize ["modifyvm", :id, "--vram", ""]

```

## Инициализация нашего рабочего стола Linux

Теперь мы готовы запустить нашу первую машину в терминале нашего ПК. В моем случае я использую PowerShell на своем компьютере с Windows, перейдите в папку своих проектов и там, где вы найдете свой VAGRANTFILE. Оказавшись там, вы можете ввести команду `vagrant up`, и если все правильно, вы увидите что-то вроде того, что показано ниже.

![](../images/Day14_Linux2.ru.png?v1)

Еще одна вещь, которую следует добавить, это то, что сеть будет настроена на `NAT` на вашей виртуальной машине, на данном этапе нам действительно не нужно знать о NAT, и я планирую провести целую сессию в следующем разделе о сети. Но знайте, что это просто кнопка, когда дело доходит до включения машины в вашу домашнюю сеть, это также сетевой режим по умолчанию в Virtual Box. Вы можете узнать больше в [документации Virtual Box](https://www.virtualbox.org/manual/ch06.html#network_nat)

Как только `vagrant up` завершен, мы можем использовать `vagrant ssh`, чтобы перейти прямо в терминал нашей новой виртуальной машины.

![](../images/Day14_Linux3.ru.png?v1)

Именно здесь мы будем проводить большую часть наших исследований в течение следующих нескольких дней, но я также хочу погрузиться в некоторые настройки для вашей рабочей станции разработчика, которые я сделал, и это значительно упрощает вашу жизнь при использовании этого в качестве ежедневного драйвера, и, конечно же, а ты реально в DevOps разве что у тебя крутой нестандартный терминал?

Но просто для подтверждения в Virtual Box вы должны увидеть приглашение для входа в систему при выборе виртуальной машины.

![](../images/Day14_Linux4.ru.png?v1)

О, и если вы зашли так далеко и спрашивали: «ЧТО ТАКОЕ ИМЯ ПОЛЬЗОВАТЕЛЯ И ПАРОЛЬ?»

- Username = vagrant
- Password = vagrant

Завтра мы рассмотрим некоторые команды и то, что они делают. Терминал станет местом, где все произойдет.

## Ресурсы

- [Learn the Linux Fundamentals - Part 1](https://www.youtube.com/watch?v=kPylihJRG70)
- [Linux for hackers (don't worry you don't need be a hacker!)](https://www.youtube.com/watch?v=VbEx7B_PTOE)
- [Vargant tutorial](https://learn.hashicorp.com/vagrant)

Как я уже упоминал, далее мы рассмотрим команды, которые мы можем использовать ежедневно в наших средах Linux.
