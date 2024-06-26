---
title: 10. Окружение Go
description: Окружение Go
toc: true
authors:
tags: [devops, golang]
categories:
series: 
date: "2022-04-30"
lastMod: "2022-05-01"
featuredImage:
draft: false
id: 1048701
weight: 10
---

### Окружение Go

В [8-м дне](../day08) мы кратко рассмотрели рабочее пространство Go, чтобы запустить его и перейти к демонстрации «Hello #90DaysOfDevOps». Но мы должны немного рассказать о рабочем пространстве Go.

Помните, что мы выбрали значения по умолчанию, а затем прошли и создали нашу папку Go в GOPATH, который уже был определен, но на самом деле этот GOPATH можно изменить, чтобы он находился там, где вы хотите.

Если вы запустите

```
echo $GOPATH
```

Вывод должен быть похож на мой (может быть с другим именем пользователя), а именно:

```
/home/michael/projects/go
```

Затем здесь мы создали 3 директории. **src**, **pkg** и **bin**

![](../images/Day10_Go1.ru.png?v1)

**src** is where all of your Go programs and projects are stored. This handles namespacing package management for all your Go repositories. This is where you will see on our workstation we have our Hello folder for the Hello #90DaysOfDevOps project.

![](../images/Day10_Go2.ru.png?v1)

**pkg** — это место, где хранятся ваши заархивированные файлы пакетов, которые установлены или были установлены в программах. Это помогает ускорить процесс компиляции в зависимости от того, были ли изменены используемые пакеты.
![](../images/Day10_Go3.ru.png?v1)

**bin** — это место, где хранятся все ваши скомпилированные двоичные файлы.

![](../images/Day10_Go4.ru.png?v1)

Наш Hello #90DaysOfDevOps не является сложной программой, поэтому вот пример более сложной программы Go, взятой из другого замечательного ресурса, на который стоит обратить внимание [GoChronicles](https://gochronicles.com/)
![](../images/Day10_Go5.ru.png?v1)

### Компиляция и запуск кода

На [9-й день](../day09) мы также рассмотрели краткое введение в компиляцию кода, но здесь мы можем пойти немного глубже.

Чтобы запустить наш код, мы сначала должны его **скомпилировать**. В Go это можно сделать тремя способами.

- go build
- go install
- go run

Прежде чем мы перейдем к описанному выше этапу компиляции, нам нужно взглянуть на то, что мы получаем при установке Go.

Когда мы установили Go на 8-й день, мы установили что-то, известное как инструменты Go, которые состоят из нескольких программ, которые позволяют нам создавать и обрабатывать наши исходные файлы Go. Одним из инструментов является «Go».

Стоит отметить, что вы можете установить дополнительные инструменты, которых нет в стандартной установке Go.

Если вы откроете командную строку и наберете «go», вы должны увидеть что-то вроде изображения ниже, а затем вы увидите «Дополнительные разделы справки» ниже, и пока нам не нужно беспокоиться об этом.

![](../images/Day10_Go6.ru.png?v1)

Возможно, вы также помните, что мы уже использовали как минимум два из этих инструментов в День 8.
![](../images/Day10_Go7.ru.png?v1)

Мы хотим узнать больше о сборке, установке и запуске.

![](../images/Day10_Go8.ru.png?v1)

- `go run` - Эта команда компилирует и запускает основной пакет, состоящий из файлов .go, указанных в командной строке. Команда компилируется во временную папку.
- `go build` - чтобы скомпилировать пакеты и зависимости, скомпилируйте пакет в текущем каталоге. Если пакет «main», поместит исполняемый файл в текущий каталог, если нет, то он поместит исполняемый файл в папку «pkg». `go build` также позволяет вам создать исполняемый файл для любой платформы ОС, поддерживаемой Go.
- `go install` - то же самое, что и go build, но помещает исполняемый файл в папку `bin`

Мы прошли через `go build` и `go run`, но не стесняйтесь запускать их снова здесь, если хотите, `go install`, как указано выше, помещает исполняемый файл в нашу папку bin.
![](../images/Day10_Go9.ru.png?v1)

Надеюсь, что вы следите за мной и смотрите один из плейлистов или видеороликов ниже. Я беру их по кусочкам и перевожу в свои заметки, чтобы понять основы языка Голанг. Приведенные ниже ресурсы, вероятно, дадут вам гораздо лучшее понимание многих областей, которые вам нужны в целом, но я пытаюсь задокументировать 7 дней или 7 часов путешествия с интересными вещами, которые я нашел.

## Источники

- [StackOverflow 2021 Developer Survey](https://insights.stackoverflow.com/survey/2021)
- [Why we are choosing Golang to learn](https://www.youtube.com/watch?v=7pLqIIAqZD4&t=9s)
- [Jake Wright - Learn Go in 12 minutes](https://www.youtube.com/watch?v=C8LgvuEBraI&t=312s)
- [Techworld with Nana - Golang full course - 3 hours 24 mins](https://www.youtube.com/watch?v=yyUHQIec83I)
- [**NOT FREE** Nigel Poulton Pluralsight - Go Fundamentals - 3 hours 26 mins](https://www.pluralsight.com/courses/go-fundamentals)
- [FreeCodeCamp -  Learn Go Programming - Golang Tutorial for Beginners](https://www.youtube.com/watch?v=YS4e4q9oBaU&t=1025s)
- [Hitesh Choudhary - Complete playlist](https://www.youtube.com/playlist?list=PLRAV69dS1uWSR89FRQGZ6q9BR2b44Tr9N)

Увидимся на [11-й день](../day11)
