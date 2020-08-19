---
keywords: identities rtcdp;rtcdp identities;real-time cdp identities
title: Identités sur la plateforme CDP en temps réel
description: Adobe Experience Platform Identity Service vous permet de mieux connaître vos clients et leurs comportements en rapprochant des identités entre appareils et systèmes.
translation-type: tm+mt
source-git-commit: 15323134f0c626cad2c4e90b3e1c0662cf7e57dd
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 74%

---


# Identités sur la plateforme CDP en temps réel

Adobe Experience Platform [!DNL Identity Service] helps you to gain a better view of your customers and their behavior by bridging together identities across devices and systems. En règle générale, vos clients interagissent avec votre marque via plusieurs canaux, par exemple en naviguant sur votre site web, en effectuant un achat en magasin, en rejoignant votre programme de fidélité ou en appelant un centre d’assistance pour obtenir de l’aide. Across these multiple systems, there is an identity created for that customer, and [!DNL Identity Service] makes it possible to bring those identities together to see the complete picture.

Désormais, plutôt que d’avoir cinq clients distincts interagissant avec votre marque sur cinq canaux différents, vous pouvez vous assurer qu’il s’agit du même client et que celui-ci bénéficie d’une expérience cohérente, personnalisée et pertinente lors de chaque interaction. Les informations acquises sur votre client (par exemple, un navigateur anonyme de votre site web décide de s’abonner à un compte et de se connecter) sont combinées et l’image de votre client devient de plus en plus précise.

## Espaces de noms d’identité

Identity namespaces are a component of [!DNL Identity Service] and serve as indicators providing additional context to customer identities. Un exemple d’espace de noms d’ID couramment utilisé serait « Email », l’utilisation d’une même adresse électronique sur plusieurs sites web permettant de rassembler plusieurs identités, chacune associée à un ID client unique, comme appartenant au même client. [!DNL Experience Platform] permet d’utiliser des espaces de noms d’ID pour rechercher des profils individuels dans l’interface utilisateur. Pour plus d’informations sur l’affichage des profils, consultez la [présentation de la visionneuse de profils](/help/rtcdp/profile/profile-viewer.md). Pour en savoir plus les espaces de noms d’identité, consultez la [présentation des espaces de noms d’identité](../../identity-service/namespaces.md).

## Graphiques d’identités

Un graphique d’identités est une carte des relations entre différents espaces de noms d’identité. Il permet de visualiser la façon dont un client interagit avec votre marque sur différents canaux. All customer identity graphs are collectively managed and updated by [!DNL Identity Service] in near real-time, in response to customer activity.

[!DNL Identity Service] gère un graphique d’identité visible par votre entreprise uniquement et basé sur vos données. Il est appelé graphique privé. [!DNL Identity Service] augmente le graphique privé lorsqu’un enregistrement de données ingérées contient plusieurs identités, ajoutant ainsi une relation entre les identités trouvées.

## Étapes suivantes

Identities, and the relationships between them, are defined and maintained by [!DNL Identity Service] and leveraged by [!DNL Real-time Customer Profile] to build a complete picture of each individual customer and their interactions. Pour en savoir plus, consultez la [documentation sur Identity Service](../../identity-service/home.md).