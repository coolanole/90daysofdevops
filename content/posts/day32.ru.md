---
title: 32. Модели хранилища Microsoft Azure
description: Модели хранилища Microsoft Azure
toc: true
authors:
tags: [devops]
categories:
series: 
date: "2022-05-22"
lastMod: "2022-05-22"
featuredImage:
draft: false
id: 1048775
weight: 32
---
## Модели хранилища

### Службы хранилища

- Службы хранилища Azure предоставляются учетными записями хранения.
- Доступ к учетным записям хранения в основном осуществляется через REST API.
- Учетная запись хранения должна иметь уникальное имя, являющееся частью DNS-имени `<Storage Account name>.core.windows.net`.
- Различные варианты репликации и шифрования.
- Находится в группе ресурсов

Мы можем создать нашу группу хранения, просто выполнив поиск группы хранения в строке поиска в верхней части портала Azure.

![](../images/Day32_Cloud1.ru.png?v1)
Затем мы можем выполнить шаги по созданию нашей учетной записи хранения, помня, что это имя должно быть уникальным, а также оно должно быть написано строчными буквами, без пробелов, но может включать цифры.

![](../images/Day32_Cloud2.ru.png?v1)
Мы также можем выбрать уровень избыточности, который мы хотели бы использовать для нашей учетной записи хранения и всего, что мы здесь храним. Чем дальше по списку, тем дороже вариант, но также и распространение ваших данных.

Даже опция избыточности по умолчанию дает нам 3 копии наших данных.

[Azure Storage Redundancy](https://docs.microsoft.com/ru-ru/azure/storage/common/storage-redundancy)

Концепции из ссылки выше:

- **Локально-избыточное хранилище** — трижды реплицирует ваши данные в пределах одного центра обработки данных в основном регионе.
  
- **Геоизбыточное хранилище** — трижды синхронно копирует ваши данные в одном физическом расположении в основном регионе с помощью LRS.
  
- **Хранилище с избыточностью в пределах зоны** — синхронно реплицирует данные службы хранилища Azure в трех зонах доступности Azure в основном регионе.
  
- **Хранилище с избыточностью в геозонах** — сочетает в себе высокую доступность, обеспечиваемую избыточностью в зонах доступности, с защитой от региональных сбоев, обеспечиваемой георепликацией. Данные в учетной записи хранения GZRS копируются в три зоны доступности Azure в основном регионе, а также реплицируются во второй географический регион для защиты от региональных аварий.

![](../images/Day32_Cloud3.ru.png?v1)

Просто возвращаюсь к параметрам производительности. У нас есть Стандарт и Премиум на выбор. В нашем пошаговом руководстве мы выбрали «Стандартный», но «Премиум» дает вам некоторые специфические опции.
![](../images/Day32_Cloud4.ru.png?v1)

Затем в раскрывающемся списке вы можете увидеть, что у нас есть эти три варианта на выбор.
![](../images/Day32_Cloud5.ru.png?v1)

Для учетной записи хранения доступно множество дополнительных параметров, но пока нам не нужно вдаваться в это. Эти параметры связаны с шифрованием и защитой данных.

### Управляемые диски

Доступ к хранилищу можно получить несколькими способами.

Аутентифицированный доступ через:

- Общий ключ для полного контроля.
- Shared Access Signature для делегированного, детализированного доступа.
- Azure Active Directory (где доступно)

Публичный доступ:

- Общий доступ также может быть предоставлен для включения анонимного доступа, в том числе через HTTP.
— Примером этого может быть размещение базового контента и файлов в блочном BLOB-объекте, чтобы браузер мог просматривать и скачивать эти данные.

Если вы получаете доступ к своему хранилищу из другой службы Azure, трафик остается в Azure.

Когда дело доходит до производительности хранилища, у нас есть два разных типа:

- **Standard** - Максимальное количество операций ввода-вывода в секунду
- **Premium** - Гарантированное количество операций ввода-вывода в секунду

Существует также разница между неуправляемыми и управляемыми дисками, которую следует учитывать при выборе правильного хранилища для поставленной задачи.

### Хранилище виртуальной машины

- Диски ОС виртуальной машины обычно хранятся в постоянном хранилище.
- Некоторым рабочим нагрузкам без сохранения состояния не требуется постоянное хранилище, и уменьшение задержки является большим преимуществом.
- Существуют виртуальные машины, поддерживающие эфемерные управляемые диски ОС, созданные в локальном хранилище узла.
  - Их также можно использовать с масштабируемыми наборами виртуальных машин.

Управляемые диски — это надежное блочное хранилище, которое можно использовать с виртуальными машинами Azure. Вы можете иметь Ultra Disk Storage, Premium SSD, Standard SSD, Standard HDD. Они также несут некоторые характеристики.

- Поддержка снимков и изображений
- Простое перемещение между SKU
- Лучшая доступность в сочетании с наборами доступности
- Плата взимается в зависимости от размера диска, а не от использованного хранилища.

## Хранилище архивов

- **Cool Tier** — доступен классный уровень хранилища для блокировки и добавления больших двоичных объектов.
  - Более низкая стоимость хранения
  - Более высокая стоимость сделки.
- **Archive Tier*** — Архивное хранилище доступно для блочных больших двоичных объектов.
  - Это настраивается для каждого BLOB-объекта.
  - Более низкая стоимость, более длительная задержка поиска данных.
  - Такая же надежность данных, как и в обычном хранилище Azure.
  - Пользовательские уровни данных могут быть включены по мере необходимости.

### Общий доступ к файлам

Из вышеописанного создания нашей учетной записи хранения теперь мы можем создавать общие файловые ресурсы.

![](../images/Day32_Cloud6.ru.png?v1)

Это обеспечит файловые ресурсы SMB2.1 и 3.0 в Azure.

Можно использовать в Azure и извне через SMB3 и порт 445, открытый для Интернета.

Предоставляет общее хранилище файлов в Azure.

Можно сопоставить с помощью стандартных клиентов SMB в дополнение к REST API.

Вы также можете почитать [Azure NetApp Files](https://vzilla.co.uk/vzilla-blog/azure-netapp-files-how) (SMB и NFS)

### Службы кэширования и мультимедиа

Сеть доставки содержимого Azure предоставляет кэш статического веб-содержимого с местоположениями по всему миру.

Службы мультимедиа Azure предоставляют технологии транскодирования мультимедиа в дополнение к службам воспроизведения.

## Модели баз данных Microsoft Azure

Еще в [День 28](../day28) мы рассмотрели различные варианты обслуживания. Одним из них была PaaS (Platform as a Service) (платформа как услуга), где вы абстрагируете большую часть инфраструктуры и операционной системы, и вам остается контролировать приложение или, в данном случае, модели базы данных.

### Реляционные базы данных

База данных SQL Azure предоставляет реляционную базу данных как службу на основе Microsoft SQL Server.

Это SQL, работающий с последней веткой SQL с доступным уровнем совместимости базы данных, где требуется конкретная версия функциональности.

Есть несколько вариантов того, как это можно настроить: мы можем предоставить единую базу данных, которая предоставляет одну базу данных в экземпляре, в то время как эластичный пул позволяет использовать несколько баз данных, которые совместно используют пул емкости и совместно масштабируются.

Доступ к этим экземплярам базы данных можно получить как к обычным экземплярам SQL.

Дополнительные управляемые предложения для MySQL, PostgreSQL и MariaDB.

![](../images/Day32_Cloud7.ru.png?v1)

### Решения NoSQL

Azure Cosmos DB — это реализация NoSQL, не зависящая от схемы.

99,99% SLA

Глобально распределенная база данных с однозначными задержками на 99-м процентиле в любой точке мира с автоматическим возвратом в исходное положение.

Ключ раздела, используемый для разделения/разбиения/распределения данных.

Поддерживает различные модели данных (документы, ключ-значение, график, удобный для столбцов)

Поддерживает различные API (DocumentDB SQL, MongoDB, Azure Table Storage и Gremlin).

![](../images/Day32_Cloud9.ru.png?v1)

Доступны различные модели согласованности, основанные на [теореме CAP](https://en.wikipedia.org/wiki/CAP_theorem).

![](../images/Day32_Cloud8.ru.png?v1)

### Кэширование

Не вдаваясь в подробности о системах кэширования, таких как Redis, я хотел добавить, что у Microsoft Azure есть служба под названием [Azure Cache for Redis](https://azure.microsoft.com/ru-ru/services/cache/).

Кэш Azure для Redis предоставляет хранилище данных в памяти на основе программного обеспечения Redis.

- Это реализация Redis Cache с открытым исходным кодом.
  - Размещенный безопасный экземпляр кэша Redis.
  - Доступны разные уровни
  - Приложение должно быть обновлено, чтобы использовать кеш.
  - Предназначен для приложения, которое имеет высокие требования к чтению по сравнению с записью.
  - На основе хранилища ключей-значений.

![](../images/Day32_Cloud10.ru.png?v1)

Я ценю, что за последние несколько дней было много заметок и теории о Microsoft Azure, но я хотел охватить строительные блоки, прежде чем мы перейдем к практическим аспектам того, как эти компоненты объединяются и работают.

У нас есть еще немного теории, связанной с сетью, прежде чем мы сможем запустить и запустить некоторые основанные на сценариях развертывания сервисов. Мы также хотим взглянуть на некоторые различные способы взаимодействия с Microsoft Azure по сравнению с порталом, который мы использовали до сих пор.

## Ресурсы

- [Hybrid Cloud and MultiCloud](https://www.youtube.com/watch?v=qkj5W98Xdvw)
- [Microsoft Azure Fundamentals](https://www.youtube.com/watch?v=NKEFWyqJ5XA&list=WL&index=130&t=12s)
- [Google Cloud Digital Leader Certification Course](https://www.youtube.com/watch?v=UGRDM86MBIQ&list=WL&index=131&t=10s)