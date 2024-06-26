---
title: 50. Выбор платформы Kubernetes для проекта
description: 
toc: true
authors:
tags: [devops]
categories:
series: 
date: "2022-06-09"
lastMod: "2022-06-09"
featuredImage:
draft: false
id: 1049046
weight: 50
---
## Выбор платформы Kubernetes

Я хотел бы использовать эту сессию для разбора некоторых платформ или, может быть, дистрибутивов - более подходящий термин для этого, одна вещь, которая была проблемой в мире Kubernetes - это устранение сложности.

Kubernetes the hard way рассказывает о том, как построить из ничего полноценный функциональный кластер Kubernetes, очевидно, что это крайность, но все больше и больше людей, по крайней мере, тех, с кем я общаюсь, хотят устранить эту сложность и запустить управляемый кластер Kubernetes. Проблема в том, что это стоит больше денег, но преимущества могут быть следующими: если вы используете управляемый сервис, действительно ли вам нужно знать архитектуру узлов и то, что происходит с точки зрения плоскости управления узлов, когда обычно у вас нет к этому доступа.

Затем у нас есть локальные дистрибутивы для разработки, которые позволяют нам использовать наши собственные системы и запускать локальную версию Kubernetes, чтобы разработчики могли иметь полную рабочую среду для запуска своих приложений на платформе, для которой они предназначены.

Общая основа всех этих концепций заключается в том, что все они являются разновидностью Kubernetes, что означает, что мы должны иметь возможность свободно мигрировать и перемещать наши рабочие нагрузки туда, куда нам нужно, в соответствии с нашими требованиями.

Во многом наш выбор будет зависеть от того, какие инвестиции были сделаны. Я уже упоминал об опыте разработчиков, но некоторые из локальных сред Kubernetes, в которых работают наши ноутбуки, отлично подходят для ознакомления с технологией без затрат денег.

### Bare-Metal Clusters

Вариантом для многих может быть запуск ОС Linux прямо на нескольких физических серверах для создания кластера, это также может быть Windows, но я не слышал о темпах внедрения Windows, контейнеров и Kubernetes. Очевидно, что если вы - компания, и вы приняли решение о покупке физических серверов, то это может быть способом создания кластера Kubernetes, но управление и администрирование здесь означает, что вам придется создавать и управлять всем с нуля.

### Виртуализация

Независимо от тестовых и учебных сред или готовых корпоративных кластеров Kubernetes виртуализация является отличным способом продвижения, обычно это возможность запускать виртуальные машины в качестве узлов и затем объединять их в кластер. Вы получаете базовую архитектуру, эффективность и скорость виртуализации, а также возможность эффективно использовать существующие затраты. Например, VMware предлагает отличное решение для виртуальных машин и Kubernetes в различных вариантах.

Мой первый кластер Kubernetes был создан на основе виртуализации с использованием Microsoft Hyper-V на старом сервере, который был способен запускать несколько виртуальных машин в качестве узлов.

### Варианты локального рабочего стола

Существует несколько вариантов запуска локального кластера Kubernetes на вашем настольном компьютере или ноутбуке. Как уже говорилось ранее, это дает разработчикам возможность увидеть, как будет выглядеть их приложение, без необходимости создавать несколько дорогостоящих или сложных кластеров. Лично я часто использую этот кластер, в частности, я использую minikube. Он обладает отличной функциональностью и дополнениями, которые меняют способ создания и запуска приложений.

### Kubernetes Managed Services

Я уже упоминал о виртуализации, и это может быть достигнуто с помощью гипервизоров локально, но мы знаем из предыдущих разделов, что мы также можем использовать виртуальные машины в публичном облаке в качестве узлов. Я говорю об управляемых сервисах Kubernetes - это предложения, которые мы видим у крупных гипермасштабирующих компаний, а также у MSP, которые убирают уровни управления и контроля от конечного пользователя; это может быть удаление плоскости управления от конечного пользователя, что происходит с Amazon EKS, Microsoft AKS и Google Kubernetes Engine. (GKE)

### Непреодолимый выбор  

Выбор - это здорово, но есть момент, когда он становится чрезмерным, и это не глубокий обзор всех вариантов в каждой из перечисленных выше категорий. В дополнение к вышеперечисленному у нас есть OpenShift от Red Hat, и этот вариант действительно может быть использован во всех вышеперечисленных вариантах у всех основных облачных провайдеров и, вероятно, сегодня обеспечивает наилучшее общее удобство для администраторов независимо от того, где развернуты кластеры.

Итак, с чего вы начнете свое обучение, как я уже сказал, я начал с пути виртуализации, но это было потому, что у меня был доступ к физическому серверу, который я мог использовать для этой цели, я ценю и фактически с тех пор у меня больше нет такой возможности.

Сейчас я бы посоветовал использовать Minikube в качестве первого варианта или Kind (Kubernetes в Docker), но Minikube дает нам некоторые дополнительные преимущества, которые почти абстрагируют сложность, так как мы можем просто использовать дополнительные модули и быстро создавать вещи, а затем разрушать их, когда мы закончим, мы можем запускать несколько кластеров, мы можем запускать их почти везде, кросс-платформенные и аппаратно-агностические.

Я проделал небольшой путь в изучении Kubernetes, поэтому я собираюсь оставить выбор платформы и конкретику здесь, чтобы перечислить варианты, которые я пробовал, чтобы дать мне лучшее понимание платформы Kubernetes и того, где она может работать. Что я мог бы сделать с нижеприведенными записями в блоге, так это еще раз взглянуть на них, обновить их и перенести сюда, вместо того, чтобы они были ссылками на записи в блоге.

## Ресурсы

- [Kubernetes playground – How to choose your platform](https://vzilla.co.uk/vzilla-blog/building-the-home-lab-kubernetes-playground-part-1)
- [Kubernetes playground – Setting up your cluster](https://vzilla.co.uk/vzilla-blog/building-the-home-lab-kubernetes-playground-part-2)
- [Getting started with Amazon Elastic Kubernetes Service (Amazon EKS)](https://vzilla.co.uk/vzilla-blog/getting-started-with-amazon-elastic-kubernetes-service-amazon-eks)
- [Getting started with Microsoft Azure Kubernetes Service (AKS)](https://vzilla.co.uk/vzilla-blog/getting-started-with-microsoft-azure-kubernetes-service-aks)
- [Getting Started with Microsoft AKS – Azure PowerShell Edition](https://vzilla.co.uk/vzilla-blog/getting-started-with-microsoft-aks-azure-powershell-edition)
- [Getting started with Google Kubernetes Service (GKE)](https://vzilla.co.uk/vzilla-blog/getting-started-with-google-kubernetes-service-gke)
- [Kubernetes, How to – AWS Bottlerocket + Amazon EKS](https://vzilla.co.uk/vzilla-blog/kubernetes-how-to-aws-bottlerocket-amazon-eks)
- [Getting started with CIVO Cloud](https://vzilla.co.uk/vzilla-blog/getting-started-with-civo-cloud)
- [Minikube - Kubernetes Demo Environment For Everyone](https://vzilla.co.uk/vzilla-blog/project_pace-kasten-k10-demo-environment-for-everyone)
