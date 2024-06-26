---
title: 39. Просмотр, удаление, отмена и восстановление
description: Просмотр, удаление, отмена и восстановление версий в Git
toc: true
authors:
tags: [devops]
categories:
series: 
date: "2022-05-29"
lastMod: "2022-05-29"
featuredImage:
draft: false
id: 1048827
weight: 39
---
## GIT - Просмотр, удаление, отмена и восстановление

### Просмотр файлов в Stagig area и Working area

Если некоторые файлы/папки уже добавлены в `staging area`, то можно просмотреть их рахницу по отношению в главной ветке комадой:  `git diff --staged`

![](../images/Day39_Git1.ru.png?v1)

Это покажет нам все внесенные изменения и все новые файлы, которые мы добавили или удалили.

Изменения в измененных файлах обозначаются символами `---` или `+++` Вы можете видеть ниже, что мы только что добавили `+add some text`, что означает, что это новые строки.

![](../images/Day39_Git2.ru.png?v1)

Мы также можем запустить `git diff`, чтобы сравнить наш staging area с нашим рабочим каталогом. Если мы внесем некоторые изменения в наш только что добавленный файл code.txt и добавим несколько строк текста.

![](../images/Day39_Git3.ru.png?v1)

![](../images/Day39_Git4.ru.png?v1)

### Инструменты для визуального отображения

Вот несколько инструментов для визуального сравнения коммитов и веток:

- KDiff3
- P4Merge
- WinMerge (только для Windows)
- VSCode

Если запустим `git difftool` то запустится визуальный инструмент сравнения по умолчанию.
![](../images/Day39_Git7.ru.png?v1)
Проверить текущие настройки `git config --global -e`
![](../images/Day39_Git6.ru.png?v1)
Чтобы установить инструмент в git, выполним следующую команду `git config --global diff.tool vscode`.
![](../images/Day39_Git5.ru.png?v1)
Теперь при запуске `git difftool` откроется vscode
После этого открывается редактор VScode на странице diff и сравнивает их, мы изменили только один файл, добавив строку кода с правой стороны.
![](../images/Day39_Git8.ru.png?v1)
Можем использовать `git difftool --staged` для сравнения файлов в `staging area` с "прокомиченными" файлами.
![](../images/Day39_Git9.ru.png?v1)
VScode, как и большинство IDE, имеют встроенную функциональность, поэтому очень редко вам понадобится запускать эти команды из терминала, хотя это полезно, если у вас по какой-то причине не установлена IDE.

### Просмотр истории изменений

Просмотреть историю изменений в Git можно командой `git log`

![](../images/Day39_Git11.ru.png?v1)
Каждый коммит имеет свою шестнадцатеричную строку, уникальную для репозитория. Здесь вы можете увидеть, над какой веткой мы работаем, а также автора, дату и комментарий коммита.

У нас также есть `git log --oneline`, и это даёт нам гораздо меньшую версию шестнадцатеричной строки, которую мы можем использовать в других командах `diff`.

![](../images/Day39_Git12.ru.png?v1)
Чтобы просмотреть коммиты с самого первого, а не послденего, как по умолчанию, запустим   `git log --oneline --reverse`, и теперь мы видим наш первый коммит в верхней части страницы.

![](../images/Day39_Git13.ru.png?v1)

### Просмотр коммита

Можно просмотреть данные ко конкретном коммите более детально: `git show` или `git show <commit ID>`

![](../images/Day39_Git14.ru.png?v1)

![](../images/Day39_Git15.ru.png?v1)

Мы также можем использовать `git show HEAD~1`, где 1 - это количество шагов назад от текущей версии, к которой мы хотим вернуться.

Это отличный вариант, если вам нужна подробная информация о файлах, но если мы хотим получить список всех файлов в дереве для всего каталога снимков. Мы можем добиться этого, используя команду `git ls-tree HEAD~1`, снова вернувшись на один снимок назад от последнего коммита. Ниже мы видим два пятна, которые обозначают файлы, в то время как дерево обозначает каталог. В этой информации вы также можете увидеть коммиты и теги.

![](../images/Day39_Git16.ru.png?v1)

Проверим коммит

![](../images/Day39_Git17.ru.png?v1)

![](../images/Day39_Git18.ru.png?v1)

### Unstaging

Бывают случаи, когда вы, возможно, использовали `git add .`, но на самом деле есть файлы, которые вы пока не хотите фиксировать в этом снапшоте. В этом примере ниже я добавил newfile.txt в область staging, но я не готов зафиксировать этот файл, поэтому я собираюсь использовать `git restore --staged newfile.txt`, чтобы отменить шаг `git add`.

![](../images/Day39_Git19.ru.png?v1)

Мы также можем сделать то же самое с изменёнными файлами, такими как main.js, и снять фиксацию, см. выше у нас есть greem M для modified, а ниже мы снимаем фиксацию этих изменений.

![](../images/Day39_Git20.ru.png?v1)

Я нашел эту команду весьма полезной во время 90DaysOfDevOps, поскольку иногда я работаю заранее, когда чувствую, что хочу сделать заметки для следующего дня, но не хочу фиксировать и выкладывать в публичный репозиторий GitHub.

### Отмена локальных изменений

Иногда мы можем вносить изменения, но эти изменения нас не устраивают, и мы хотим их отбросить. Мы снова воспользуемся командой `git restore` и сможем восстановить файлы из наших снимков или предыдущих версий. Мы можем запустить команду `git restore .` для нашего каталога, и мы восстановим все из нашего снимка, но обратите внимание, что наш неотслеживаемый файл все еще присутствует. Нет предыдущего отслеживаемого файла под названием newfile.txt.

![](../images/Day39_Git21.ru.png?v1)

Теперь, чтобы удалить newfile.txt или любой другой неотслеживаемый файл. Мы можем использовать `git clean`, но получим только предупреждение.

![](../images/Day39_Git22.ru.png?v1)

Или, если мы знаем о последствиях, мы можем запустить `git clean -fd`, чтобы принудительно удалить все каталоги.

![](../images/Day39_Git23.ru.png?v1)

### Восстановление файла до более ранней версии

Как мы уже упоминали, большая часть того, чем может помочь Git, - это возможность восстановления копий файлов из снимков (это не резервное копирование, но это очень быстрая точка восстановления). Я советую вам также сохранять копии вашего кода в других местах, используя для этого решение для резервного копирования.

В качестве примера давайте удалим наш самый важный файл в каталоге, обратите внимание, что мы используем команды на базе unix для удаления этого файла из каталога, а не команды git.

![](../images/Day39_Git24.ru.png?v1)

Теперь у нас нет readme.mdin в нашей рабочей директории. Мы могли бы использовать `git rm readme.md` и тогда это было бы отражено в нашей базе данных git. Давайте также удалим его отсюда, чтобы имитировать его полное удаление.

![](../images/Day39_Git25.ru.png?v1)

Теперь зафиксируем это с сообщением и докажем, что у нас больше нет ничего в рабочем каталоге или в области постановки.

![](../images/Day39_Git26.ru.png?v1)

Была допущена ошибка, и теперь нам нужно вернуть этот файл!

Мы можем использовать команду `git undo`, которая отменит последний коммит, но что если это было давно? Мы можем использовать команду `git log`, чтобы найти наши коммиты, и тогда мы обнаружим, что наш файл находится в последнем коммите, но мы не хотим, чтобы все эти коммиты были отменены, поэтому мы можем использовать эту команду `git restore --source=HEAD~1 README.md`, чтобы найти файл и восстановить его из нашего снимка.

Вы можете видеть, что с помощью этого процесса мы вернули файл в наш рабочий каталог.

![](../images/Day39_Git27.ru.png?v1)

Теперь у нас есть новый неотслеживаемый файл, и мы можем использовать наши команды, упомянутые ранее, для отслеживания, этапа и фиксации наших файлов и изменений.

### Rebase / Merge

Это, кажется, самая большая головная боль, когда речь заходит о Git и о том, когда использовать rebase, а когда использовать merge в ваших git-репозиториях.

Прежде всего, нужно знать, что и `git rebase`, и `git merge` решают одну и ту же задачу. Оба они интегрируют изменения из одной ветки в другую. Однако они делают это по-разному.

Давайте начнем с новой функции в новой выделенной ветке. Основная ветку продолжает работу с новыми коммитами.

![](../images/Day39_Git28.ru.png?v1)

Простой вариант здесь - использовать `git merge feature main`, который объединит основную ветку с веткую feature.

![](../images/Day39_Git29.ru.png?v1)

Слияние простое, потому что оно неразрушающее. Существующие ветви никак не изменяются. Однако это также означает, что функциональная ветку будет иметь неактуальный коммит слияния каждый раз, когда вам нужно будет включить изменения, внесённые выше по течению. Если main очень занят или активен, это может привести к загрязнению истории функциональной ветви.

В качестве альтернативного варианта мы можем перебазировать функциональную ветку на основную ветку с помощью команды

```
git checkout feature
git rebase main
```

Это перемещает ветку feature (всю ветку feature), эффективно включая все новые коммиты в main. Но вместо использования коммита слияния, rebasing переписывает историю проекта, создавая совершенно новые коммиты для каждого коммита в исходной ветке.

![](../images/Day39_Git30.ru.png?v1)

Самым большим преимуществом ребасинга является гораздо более чистая история проекта. Это также устраняет ненужные коммиты слияния. и если сравнить последние два изображения, то можно увидеть, что история проекта намного чище.

Хотя это еще не окончательный вывод, потому что выбор более чистой истории также связан с компромиссами. Если вы не будете следовать [The Golden rule of rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing#the-golden-rule-of-rebasing), переписывание истории проекта может стать потенциально катастрофой для вашего рабочего процесса совместной работы. И, что менее важно, при пересборке теряется контекст, предоставляемый коммитом слияния - вы не можете увидеть, когда изменения, внесенные выше по течению, были включены в функцию.  

## Ссылки

- [What is Version Control?](https://www.youtube.com/watch?v=Yc8sCSeMhi4)
- [Types of Version Control System](https://www.youtube.com/watch?v=kr62e_n6QuQ)
- [Git Tutorial for Beginners](https://www.youtube.com/watch?v=8JJ101D3knE&t=52s)
- [Git for Professionals Tutorial](https://www.youtube.com/watch?v=Uszj_k0DGsg)
- [Git and GitHub for Beginners - Crash Course](https://www.youtube.com/watch?v=RGOj5yH7evk&t=8s)
- [Complete Git and GitHub Tutorial](https://www.youtube.com/watch?v=apGV9Kg7ics)
- [Git cheatsheet](https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet)
- [Exploring the Git command line – A getting started guide](https://veducate.co.uk/exploring-the-git-command-line/)
