---
keywords: identités rtcdp ; identités rtcdp ; identités cdp en temps réel
title: Identités sur la plateforme CDP en temps réel
description: Adobe Experience Platform Identity Service vous permet de mieux connaître vos clients et leurs comportements en rapprochant des identités entre appareils et systèmes.
translation-type: tm+mt
source-git-commit: 15323134f0c626cad2c4e90b3e1c0662cf7e57dd
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 72%

---


# Identités sur la plateforme CDP en temps réel

Adobe Experience Platform [!DNL Identity Service] vous aide à mieux vue de vos clients et de leur comportement en rapprochant les identités entre les périphériques et les systèmes. En règle générale, vos clients interagissent avec votre marque via plusieurs canaux, par exemple en naviguant sur votre site web, en effectuant un achat en magasin, en rejoignant votre programme de fidélité ou en appelant un centre d’assistance pour obtenir de l’aide. Dans ces systèmes multiples, il y a une identité créée pour ce client, et [!DNL Identity Service] permet de rassembler ces identités pour voir le tableau complet.

Désormais, plutôt que d’avoir cinq clients distincts interagissant avec votre marque sur cinq canaux différents, vous pouvez vous assurer qu’il s’agit du même client et que celui-ci bénéficie d’une expérience cohérente, personnalisée et pertinente lors de chaque interaction. Les informations acquises sur votre client (par exemple, un navigateur anonyme de votre site web décide de s’abonner à un compte et de se connecter) sont combinées et l’image de votre client devient de plus en plus précise.

## Espaces de noms d’identité

Les espaces de nommage d&#39;identité sont un composant de [!DNL Identity Service] et servent d&#39;indicateurs qui fournissent un contexte supplémentaire aux identités des clients. Un exemple d’espace de noms d’ID couramment utilisé serait « Email », l’utilisation d’une même adresse électronique sur plusieurs sites web permettant de rassembler plusieurs identités, chacune associée à un ID client unique, comme appartenant au même client. [!DNL Experience Platform] permet d’utiliser des espaces de noms d’ID pour rechercher des profils individuels dans l’interface utilisateur. Pour plus d’informations sur l’affichage des profils, consultez la [présentation de la visionneuse de profils](/help/rtcdp/profile/profile-viewer.md). Pour en savoir plus les espaces de noms d’identité, consultez la [présentation des espaces de noms d’identité](../../identity-service/namespaces.md).

## Graphiques d’identités

Un graphique d’identités est une carte des relations entre différents espaces de noms d’identité. Il permet de visualiser la façon dont un client interagit avec votre marque sur différents canaux. Tous les graphiques d&#39;identité des clients sont gérés et mis à jour collectivement par [!DNL Identity Service] en temps quasi réel, en réponse à l&#39;activité des clients.

[!DNL Identity Service] gère un graphique d’identité visible par votre entreprise uniquement et basé sur vos données. Il est appelé graphique privé. [!DNL Identity Service] augmente le graphique privé lorsqu’un enregistrement de données ingérées contient plusieurs identités, ajoutant ainsi une relation entre les identités trouvées.

## Étapes suivantes

Les identités et les relations entre elles sont définies et conservées par [!DNL Identity Service] et exploitées par [!DNL Real-time Customer Profile] pour obtenir une image complète de chaque client et de ses interactions. Pour en savoir plus, consultez la [documentation sur Identity Service](../../identity-service/home.md).