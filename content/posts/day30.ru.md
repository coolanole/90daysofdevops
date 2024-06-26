---
title: 30. Модули безопасности Microsoft Azure
description: Модули безопасности Microsoft Azure
toc: true
authors:
tags: [devops]
categories:
series:
date: "2022-05-20"
lastMod: "2022-05-20"
featuredImage:
draft: false
id: 1049039
weight: 30
---

## Microsoft Azure Security Models

Следуя обзору Microsoft Azure, мы начнем с безопасности Azure и посмотрим, как это может помочь в наши дни. По большей части я обнаружил, что встроенных ролей было достаточно, и зная это, мы можем создавать и работать со многими различными областями аутентификации и конфигураций. Я обнаружил, что Microsoft Azure довольно продвинута с ее инструментом [Active Directory](https://docs.microsoft.com/ru-ru/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview) по сравнению с другими общедоступными облаками.

Это одна из областей, в которой Microsoft Azure, по-видимому, работает иначе, чем другие поставщики общедоступных облаков, в Azure ВСЕГДА есть Azure AD.

### Службы каталогов (Directory Services )

- Azure Active Directory содержит принципы безопасности, используемые Microsoft Azure и другими облачными службами Microsoft.
- Аутентификация осуществляется с помощью таких протоколов, как SAML, WS-Federation, OpenID Connect и OAuth2.
- Запросы выполняются через REST API, который называется Microsoft Graph API.
- У арендаторов по умолчанию есть имя tenant.onmicrosoft.com, но они также могут иметь собственные доменные имена.
- Подписки связаны с арендатором Azure Active Directory.

Если мы сравним с AWS, эквивалентным предложением будет [AWS IAM](https://aws.amazon.com/iam/) (управление идентификацией и доступом), хотя все еще очень разные

Azure AD Connect предоставляет возможность репликации учетных записей из AD в Azure AD. Сюда также могут входить группы и иногда объекты. Это может быть гранулировано и отфильтровано. Поддерживает несколько лесов и доменов.

В Microsoft Azure Active Directory (AD) можно создавать облачные учетные записи, но большинство организаций уже учли своих пользователей в собственной локальной Active Directory.

Azure AD Connect также позволяет вам видеть не только серверы Windows AD, но и другие Azure AD, Google и другие. Это также дает возможность сотрудничать с внешними людьми и организациями, что называется Azure B2B.

Варианты аутентификации между доменными службами Active Directory и Microsoft Azure Active Directory возможны с синхронизацией удостоверений с хэшем пароля.

![](../images/Day30_Cloud1.ru.png?v1)
Передача хэша пароля необязательна, если он не используется, требуется сквозная аутентификация.

Ниже приведено видео, в котором подробно рассказывается о сквозной аутентификации.

[User sign-in with Azure Active Directory Pass-through Authentication](https://docs.microsoft.com/ru-ru/azure/active-directory/hybrid/how-to-connect-pta)

![](../images/Day30_Cloud2.ru.png?v1)

### Федерации (Federation)

Справедливости ради стоит сказать, что если вы используете Microsoft 365, Microsoft Dynamics и локальную Active Directory, их довольно легко понять и интегрировать в Azure AD для федерации. Однако вы можете использовать другие службы за пределами экосистемы Microsoft.

Azure AD может выступать в качестве посредника федерации для этих других приложений сторонних производителей и других служб каталогов.

Это будет отображаться на портале Azure как корпоративные приложения, для которых существует большое количество вариантов.

![](../images/Day30_Cloud3.ru.png?v1)

Если вы прокрутите вниз страницу корпоративного приложения, вы увидите длинный список рекомендуемых приложений.

![](../images/Day30_Cloud4.ru.png?v1)

Эта опция также позволяет «принести свою» интеграцию, приложение, которое вы разрабатываете, или приложение, не являющееся галереей.

Я не изучал это раньше, но вижу, что это вполне подходящий набор функций по сравнению с другими облачными провайдерами и возможностями.

### Управление доступом на основе ролей

Мы уже рассмотрели в [День 29](../day29) области, которые мы собираемся охватить здесь, мы можем настроить управление доступом на основе ролей в соответствии с одной из этих областей.

- Subscriptions
- Management Group
- Resource Group
- Resources

Роли можно разделить на три, в Microsoft Azure много встроенных ролей. Эти три:

- Owner
- Contributor
- Reader

Владелец и участник очень похожи по своим границам, однако владелец может изменять разрешения.

Другие роли относятся к определенным типам ресурсов Azure, а также к пользовательским ролям.

Мы должны сосредоточиться на назначении разрешений группам и пользователям.

Разрешения наследуются.

Если мы вернемся назад и посмотрим на группу ресурсов «90DaysOfDevOps», которую мы создали, и проверим контроль доступа (IAM) внутри, вы увидите, что у нас есть список участников и администратор доступа пользователей клиента, и у нас есть список владельцев (но Я не могу это показать)

![](../images/Day30_Cloud5.ru.png?v1)

Мы также можем проверить роли, которые мы назначили здесь, являются ли они встроенными ролями и к какой категории они относятся.

![](../images/Day30_Cloud6.ru.png?v1)

Мы также можем использовать вкладку проверки доступа, если мы хотим проверить учетную запись по этой группе ресурсов и убедиться, что учетная запись, к которой мы хотим иметь этот доступ, имеет правильные разрешения, или, может быть, мы хотим проверить, не имеет ли пользователь слишком много доступа.

![](../images/Day30_Cloud7.ru.png?v1)

### Microsoft Defender for Cloud

- Microsoft Defender for Cloud (ранее известный как Azure Security Center) предоставляет информацию о безопасности всей среды Azure.

- Единая панель мониторинга для просмотра общего состояния безопасности всех ресурсов Azure и других ресурсов (через Azure Arc) и рекомендации по усилению безопасности.

- Уровень бесплатного пользования включает постоянную оценку и рекомендации по безопасности.

- Платные планы для защищенных типов ресурсов (например, серверы, AppService, SQL, хранилище, контейнеры, KeyVault).

Я перешел на другую подписку для просмотра Центра безопасности Azure, и вы можете увидеть здесь, основываясь на очень небольшом количестве ресурсов, что у меня есть некоторые рекомендации в одном месте.

![](../images/Day30_Cloud8.ru.png?v1)

### Azure Policy

- Azure Policy — это собственная служба Azure, которая помогает применять организационные стандарты и оценивать соответствие в масштабе.

- Интегрирован в Microsoft Defender для облака. Azure Policy проверяет несоответствующие ресурсы и применяет исправления.

- Обычно используется для управления согласованностью ресурсов, соблюдением нормативных требований, безопасностью, стоимостью и стандартами управления.

- Использует формат JSON для хранения логики оценки и определения того, соответствует ли ресурс требованиям или нет, а также любых действий, которые необходимо предпринять в случае несоответствия (например, аудит, аудит, если не существует, запретить, изменить, развернуть, если не существует).

- Бесплатно для использования. Исключение составляют подключенные ресурсы Azure Arc, взимаемые за сервер в месяц за использование гостевой конфигурации политики Azure.

### Практика

Я купил домен и хотел бы добавить этот на свой портал Azure Active Directory, [Add your custom domain name using the Azure Active Directory Portal](https://docs.microsoft.com/ru-ru/azure/active-directory/fundamentals/add-custom-domain)

![](../images/Day30_Cloud9.ru.png?v1)

Теперь мы можем создать нового пользователя в нашем новом домене Active Directory.

![](../images/Day30_Cloud10.ru.png?v1)

Теперь мы хотим создать группу для всех наших новых пользователей 90DaysOfDevOps в одной группе. Мы можем создать группу, как показано ниже, обратите внимание, что я использую «Динамический пользователь», это означает, что Azure AD будет запрашивать учетные записи пользователей и добавлять их динамически по сравнению с назначенными, когда вы вручную добавляете пользователя в свою группу.

![](../images/Day30_Cloud11.ru.png?v1)

Существует множество вариантов создания вашего запроса, мой план состоит в том, чтобы просто найти основное имя и убедиться, что оно содержит мой запрос.

![](../images/Day30_Cloud12.ru.png?v1)

Теперь, поскольку мы уже создали нашу учетную запись пользователя, мы можем проверить, работают ли правила. Для сравнения я также добавил здесь еще одну учетную запись, связанную с другим доменом, и вы можете видеть, что из-за этого правила наш пользователь не попадет в эту группу.

![](../images/Day30_Cloud13.ru.png?v1)

С тех пор я добавил нового пользователя, и если мы пойдем и проверим группу, мы увидим наших участников.

![](../images/Day30_Cloud14.ru.png?v1)

Если у нас есть это требование x100, то мы не собираемся делать все это в консоли, мы собираемся воспользоваться либо массовыми параметрами для создания, приглашения, удаления пользователей, либо вы захотите изучить [PowerShell](https://docs.microsoft.com/ru-ru/powershell/) для достичь этого автоматизированного подхода к масштабированию.

Теперь мы можем перейти к нашей группе ресурсов и указать, что в группе ресурсов 90DaysOfDevOps мы хотим, чтобы владельцем была группа, которую мы только что создали.

![](../images/Day30_Cloud15.ru.png?v1)

Мы также можем войти сюда и запретить доступ назначений к нашей группе ресурсов.

Теперь, если мы войдем на портал Azure с нашей новой учетной записью пользователя, вы увидите, что у нас есть доступ только к нашей группе ресурсов 90DaysOfDevOps, а не к другим, показанным на предыдущих рисунках, потому что у нас нет доступа.

![](../images/Day30_Cloud16.ru.png?v1)

Вышеприведенное замечательно, если это пользователь, имеющий доступ к ресурсам внутри вашего портала Azure, но не каждый пользователь должен знать о портале, но для проверки доступа мы можем использовать [Портал приложений](https://myapps.microsoft.com/) Это портал единого входа, который мы тестируем.

![](../images/Day30_Cloud17.ru.png?v1)

Вы можете настроить этот портал под своим собственным брендом, и мы, возможно, вернемся к этому позже.

## Ресурсы

- [Hybrid Cloud and MultiCloud](https://www.youtube.com/watch?v=qkj5W98Xdvw)
- [Microsoft Azure Fundamentals](https://www.youtube.com/watch?v=NKEFWyqJ5XA&list=WL&index=130&t=12s)
- [Google Cloud Digital Leader Certification Course](https://www.youtube.com/watch?v=UGRDM86MBIQ&list=WL&index=131&t=10s)
- [AWS Basics for Beginners - Full Course](https://www.youtube.com/watch?v=ulprqHHWlng&t=5352s)
