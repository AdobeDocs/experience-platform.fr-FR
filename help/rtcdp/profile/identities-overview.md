---
keywords: identités rtcdp;identités rtcdp;identités cdp en temps réel
title: Identités dans Real-time Customer Data Platform
description: Identity Service d’Adobe Experience Platform vous permet de mieux connaître vos clients et leurs comportements en rapprochant des identités entre appareils et systèmes.
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
source-git-commit: 5611a5abc7d1ed7781108b6f263e7550092b715d
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 72%

---

# Présentation des identités

Adobe Experience Platform [!DNL Identity Service] vous aide à mieux connaître vos clients et leur comportement en rapprochant des identités entre appareils et systèmes. En règle générale, vos clients interagissent avec votre marque via plusieurs canaux, par exemple en naviguant sur votre site web, en effectuant un achat en magasin, en rejoignant votre programme de fidélité ou en appelant un centre d’assistance pour obtenir de l’aide. Sur ces systèmes multiples, une identité est créée pour ce client, et [!DNL Identity Service] permet de rassembler ces identités pour obtenir une vue d’ensemble.

Désormais, plutôt que d’avoir cinq clients distincts interagissant avec votre marque sur cinq canaux différents, vous pouvez vous assurer qu’il s’agit du même client et que celui-ci bénéficie d’une expérience cohérente, personnalisée et pertinente lors de chaque interaction. Les informations acquises sur votre client (par exemple, un navigateur anonyme de votre site web décide de s’abonner à un compte et de se connecter) sont combinées et l’image de votre client devient de plus en plus précise.

## Espaces de noms d’identité

Les espaces de noms d’identité sont un composant de [!DNL Identity Service] et servent d’indicateurs fournissant un contexte supplémentaire aux identités client. Un exemple d’espace de noms d’ID couramment utilisé serait « Email », l’utilisation d’une même adresse e-mail sur plusieurs sites web permettant de rassembler plusieurs identités, chacune associée à un ID client unique, comme appartenant au même client. [!DNL Experience Platform] permet d’utiliser des espaces de noms d’ID pour rechercher des profils individuels dans l’interface utilisateur. Pour plus d’informations sur l’affichage des profils, reportez-vous à la section [présentation de la navigation dans les profils](profile-browse.md). Pour en savoir plus les espaces de noms d’identité, consultez la [présentation des espaces de noms d’identité](../../identity-service/namespaces.md).

## Graphiques d’identités

Un graphique d’identités est une carte des relations entre différents espaces de noms d’identité. Il permet de visualiser la façon dont un client interagit avec votre marque sur différents canaux. Tous les graphiques dʼidentité clients sont gérés et mis à jour collectivement par [!DNL Identity Service] en temps quasi réel, en réponse à lʼactivité du client.

[!DNL Identity Service] gère un graphique d’identité visible par votre entreprise uniquement et basé sur vos données. Il est appelé graphique privé. [!DNL Identity Service] augmente le graphique privé lorsqu’un enregistrement de données ingérées contient plusieurs identités, ajoutant ainsi une relation entre les identités trouvées.

## Étapes suivantes

Les identités et les relations entre elles sont définies et gérées par [!DNL Identity Service] et utilisés par [!DNL Real-time Customer Profile] pour obtenir une vue d’ensemble complète de chaque client et de ses interactions. Pour en savoir plus, consultez la [documentation sur Identity Service](../../identity-service/home.md).
