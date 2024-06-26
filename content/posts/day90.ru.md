---
title: 90. Мобильность данных и приложений
description: 
toc: true
authors:
tags: [devops]
categories:
series: 
date: "2022-07-01"
lastMod: "2022-07-01"
featuredImage:
draft: false
id: 1048748
weight: 90
---
## Мобильность данных и приложений

День 90 из #90DaysOfDevOps Challenge! В этой заключительной сессии я собираюсь рассказать о мобильности наших данных и приложений. Я сосредоточусь конкретно на Kubernetes, но потребность в мобильности между платформами и между платформами - это то, что является постоянно растущей потребностью и встречается на практике.

Сценарий использования таков: "Я хочу переместить рабочую нагрузку, приложение и данные из одного места в другое" по разным причинам, будь то стоимость, риск или предоставление бизнесу более качественных услуг.

На этом занятии мы возьмем нашу рабочую нагрузку и рассмотрим перемещение рабочей нагрузки Kubernetes с одного кластера на другой, но при этом мы изменим то, как наше приложение находится в целевом месте.

Фактически, здесь используются многие характеристики, которые мы рассмотрели в статье [Аварийное восстановление](.../day89)

### **Требование**

Наш текущий кластер Kubernetes не справляется со спросом, а наши затраты стремительно растут, поэтому мы хотим переместить наш производственный кластер Kubernetes в место аварийного восстановления, расположенное в другом публичном облаке, которое обеспечит возможность расширения, но при этом будет дешевле. Мы также сможем воспользоваться некоторыми собственными облачными сервисами, доступными в целевом облаке.

Наше текущее критически важное приложение (Pac-Man) имеет базу данных (MongoDB) и работает на медленном хранилище, мы хотели бы перейти на новый более быстрый уровень хранения.

Текущий фронтенд Pac-Man (NodeJS) не очень хорошо масштабируется, и мы хотели бы увеличить количество доступных стручков в новом месте.

### Приступаем к ИТ

У нас есть бриф, и на самом деле мы уже импортировали наши импорты в кластер Disaster Recovery Kubernetes.

Первое, что нам нужно сделать, это удалить операцию восстановления, которую мы выполнили в день 89 для тестирования Disaster Recovery.

Мы можем сделать это с помощью команды `kubectl delete ns pacman` на "резервном" кластере minikube.

![](../images/Day90_Data1.ru.png?v1)

Чтобы начать работу, зайдите в Kasten K10 Dashboard, выберите карточку Applications. Из выпадающего списка выберите "Удаленные"

![](../images/Day90_Data2.ru.png?v1)

Затем мы получим список доступных точек восстановления. Мы выберем ту, которая доступна, так как она содержит важные данные. (В этом примере у нас только одна точка восстановления).

![](../images/Day90_Data3.ru.png?v1)

Когда мы работали над процессом аварийного восстановления, мы оставили все по умолчанию. Однако эти дополнительные опции восстановления существуют, если у вас есть процесс Disaster Recovery, который требует преобразования вашего приложения. В данном случае нам требуется изменить хранилище и количество реплик.
![](../images/Day90_Data4.ru.png?v1)

Выберите опцию "Применить преобразования к восстановленным ресурсам".

![](../images/Day90_Data5.ru.png?v1)

Так получилось, что два встроенных примера преобразования, которые мы хотим выполнить, соответствуют нашим требованиям.

![](../images/Day90_Data6.ru.png?v1)

Первое требование заключается в том, что на нашем основном кластере мы использовали класс хранения под названием `csi-hostpath-sc`, а в нашем новом кластере мы хотим использовать `standard`, поэтому мы можем сделать это изменение здесь.

![](../images/Day90_Data7.ru.png?v1)

Выглядит хорошо, нажимаем кнопку create transform внизу.

![](../images/Day90_Data8.ru.png?v1)

Следующее требование заключается в том, что мы хотим масштабировать развертывание нашего фронтенда Pac-Man до "5"

![](../images/Day90_Data9.ru.png?v1)

Если вы следите за развитием событий, вы должны увидеть оба наших преобразования, как показано ниже.

![](../images/Day90_Data10.ru.png?v1)

Теперь вы можете видеть на изображении ниже, что мы собираемся восстановить все артефакты, перечисленные ниже, если бы мы захотели, мы могли бы также детализировать то, что мы хотим восстановить. Нажмите кнопку "Восстановить"

![](../images/Day90_Data11.ru.png?v1)

Снова нам будет предложено подтвердить действия.

![](../images/Day90_Data12.ru.png?v1)

И последнее, что мы покажем, если мы вернемся в терминал и посмотрим на наш кластер, вы увидите, что у нас теперь 5 стручков для стручков pacman и наш класс хранения теперь установлен на стандартный, а не на csi-hostpath-sc

![](../images/Day90_Data13.ru.png?v1)

Существует множество различных вариантов, которые могут быть достигнуты с помощью трансформации. Это может охватывать не только миграцию, но и аварийное восстановление, скрипты типа тестирования и разработки и т.д.

### API и автоматизация

Я не говорил о возможности использовать API и автоматизировать некоторые из этих задач, но эти опции присутствуют, и во всем пользовательском интерфейсе есть хлебные крошки, которые предоставляют наборы команд для использования API для задач автоматизации.

Важно отметить, что при развертывании Kasten K10 развертывается внутри кластера Kubernetes и затем может быть вызван через API Kubernetes.

На этом мы завершаем раздел о хранении и защите данных.

## Ресурсы

- [Kubernetes Backup and Restore made easy!](https://www.youtube.com/watch?v=01qcYSck1c4&t=217s)
- [Kubernetes Backups, Upgrades, Migrations - with Velero](https://www.youtube.com/watch?v=zybLTQER0yY)
- [7 Database Paradigms](https://www.youtube.com/watch?v=W2Z7fbCLSTw&t=520s)
- [Disaster Recovery vs. Backup: What's the difference?](https://www.youtube.com/watch?v=07EHsPuKXc0)
- [Veeam Portability & Cloud Mobility](https://www.youtube.com/watch?v=hDBlTdzE6Us&t=3s)

### **Закрытие**

Заканчивая эту задачу, я хочу продолжить просить об обратной связи, чтобы убедиться, что информация всегда актуальна.

Я также ценю, что есть много тем, которые я не смог охватить или не смог глубже погрузиться в тему DevOps.

Это означает, что мы всегда можем предпринять еще одну попытку в следующем году и найти еще 90 дней контента и прохождений для работы.

### Что дальше?

Во-первых, немного отдохнем от писанины, я начал этот вызов 1 января 2022 года и закончил 31 марта 2022 года в 19:50 BST! Это был тяжелый труд. Но, как я говорю и говорил уже давно, если этот контент поможет одному человеку, то всегда стоит учиться публично!
У меня есть несколько идей, куда двигаться дальше, и я надеюсь, что у него будет жизнь за пределами репозитория GitHub, и мы сможем рассмотреть возможность создания электронной книги и, возможно, даже физической книги.

Я также знаю, что нам нужно пересмотреть каждый пост и убедиться, что все грамматически правильно, прежде чем делать что-то подобное. Если кто-то знает о том, как использовать формат markdown для печати или создания электронной книги, я буду очень признателен за ответ.

Как всегда, продолжайте обсуждать вопросы и PR.

Спасибо!
