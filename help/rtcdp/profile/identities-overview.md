---
keywords: identités rtcdp;identités rtcdp;identités real-time cdp
title: Identités dans Real-time Customer Data Platform
description: Le service d’identités d’Adobe Experience Platform vous permet de mieux connaître vos clients et leurs comportements en rapprochant des identités entre appareils et systèmes.
feature: Get Started, Identities
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
TQID: https://experienceleague.adobe.com/vWzqLV70suJEq7OEoiPI4E3LEcswBPwKqK7ToKFuzf4
product_v2: id: fdddec33-c9cb-4459-b8b6-2664395a6f10
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 426
ht-degree: 81%

---

# Vue d’ensemble des identités

Adobe Experience Platform [!DNL Identity Service] vous permet de mieux connaître vos clients et leurs comportements en reliant les identités entre les appareils et les systèmes. En règle générale, vos clients interagissent avec votre marque via plusieurs canaux, par exemple en naviguant sur votre site web, en effectuant un achat en magasin, en rejoignant votre programme de fidélité ou en appelant un centre d’assistance pour obtenir de l’aide. Dans ces multiples systèmes, il existe une identité créée pour ce client ou cette cliente, et [!DNL Identity Service] permet de rassembler ces identités pour obtenir une vue d’ensemble.

Désormais, plutôt que d’avoir cinq clients distincts interagissant avec votre marque sur cinq canaux différents, vous pouvez vous assurer qu’il s’agit du même client et que celui-ci bénéficie d’une expérience cohérente, personnalisée et pertinente lors de chaque interaction. Les informations acquises sur votre client (par exemple, un navigateur anonyme de votre site web décide de s’abonner à un compte et de se connecter) sont combinées et l’image de votre client devient de plus en plus précise.

## Espaces de noms d’identité

Les espaces de noms d’identité sont des composants d’[!DNL Identity Service] et servent d’indicateurs pour donner un contexte supplémentaire aux identités des clientes et des clients. Un exemple d’espace de noms d’ID couramment utilisé serait « E-mail », l’utilisation d’une même adresse e-mail sur plusieurs sites web permettant de rassembler plusieurs identités, chacune associée à un ID client unique, comme appartenant au même client. [!DNL Experience Platform] permet d’utiliser des espaces de noms d’ID pour rechercher des profils individuels dans l’interface d’utilisation. Pour plus d’informations sur l’affichage des profils, consultez la [présentation de la vue d’ensemble des profils](profile-browse.md). Pour en savoir plus les espaces de noms d’identité, consultez la [présentation des espaces de noms d’identité](../../identity-service/features/namespaces.md).

## Graphiques d’identités

Un graphique d’identités est une carte des relations entre différentes identités. Il permet de visualiser la manière dont un client interagit avec votre marque sur différents canaux. Tous les graphiques d’identités client sont gérés et mis à jour collectivement par Identity Service, en réponse à l’activité du client.

[!DNL Identity Service] gère un graphique d’identité visible uniquement par votre organisation et basé sur vos données. [!DNL Identity Service] augmente le graphique lorsqu’un enregistrement de données ingérées contient plusieurs identités, ajoutant ainsi une relation entre les identités trouvées.

## Étapes suivantes

Les identités et les relations qui les constituent sont définies et conservées par [!DNL Identity Service] et utilisées par [!DNL Real-Time Customer Profile] pour créer une vue d’ensemble de chaque client/cliente et de ses interactions. Pour en savoir plus, consultez la [documentation sur le service d’identités](../../identity-service/home.md).
