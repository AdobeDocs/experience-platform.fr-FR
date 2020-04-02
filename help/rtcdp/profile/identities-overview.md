---
title: Identités et espaces de noms d’identité
seo-title: Identity Service d’Adobe Experience Platform
description: description
seo-description: description seo
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Identités sur la plateforme CDP en temps réel

Identity Service d’Adobe Experience Platform vous permet de mieux connaître vos clients et leurs comportements en rapprochant des identités entre appareils et systèmes. En règle générale, vos clients interagissent avec votre marque via plusieurs canaux, par exemple en naviguant sur votre site web, en effectuant un achat en magasin, en rejoignant votre programme de fidélité ou en appelant un centre d’assistance pour obtenir de l’aide. Il existe une identité pour ce client sur ces multiples systèmes, et Identity Service permet de rassembler ces identités pour obtenir une vue d’ensemble.

Désormais, plutôt que d’avoir cinq clients distincts interagissant avec votre marque sur cinq canaux différents, vous pouvez vous assurer qu’il s’agit du même client et que celui-ci bénéficie d’une expérience cohérente, personnalisée et pertinente lors de chaque interaction. Les informations acquises sur votre client (par exemple, un navigateur anonyme de votre site web décide de s’abonner à un compte et de se connecter) sont combinées et l’image de votre client devient de plus en plus précise.

## Espaces de noms d’identité

Les espaces de noms d’identité sont des composants d’Identity Service et servent d’indicateurs fournissant un contexte supplémentaire aux identités client. Un exemple d’espace de noms d’ID couramment utilisé serait « Email », l’utilisation d’une même adresse électronique sur plusieurs sites web permettant de rassembler plusieurs identités, chacune associée à un ID client unique, comme appartenant au même client. Experience Platform permet d’utiliser des espaces de noms d’ID pour rechercher des profils individuels dans l’interface utilisateur. Pour plus d’informations sur l’affichage des profils, consultez la [présentation de la visionneuse de profils](/help/rtcdp/profile/profile-viewer.md). Pour en savoir plus sur les  d&#39;identité  , consultez la présentation [de l&#39;](../../identity-service/namespaces.md)identité .

## Graphiques d’identité

Un graphique d’identité est une carte des relations entre différents espaces de noms d’identité. Il permet de visualiser la façon dont un client interagit avec votre marque sur différents canaux. Tous les graphiques d’identité client sont gérés et mis à jour collectivement par Identity Service en temps quasi réel, en réponse à l’activité du client.

Identity Service gère un graphique d’identité visible par votre entreprise uniquement et basé sur vos données. Il est appelé graphique privé. Identity Service augmente le graphique privé lorsqu’un enregistrement de données ingérées contient plusieurs identités, ajoutant ainsi une relation entre les identités trouvées.

## Étapes suivantes

Les identités et les relations entre elles sont définies et conservées par Identity Service et utilisées par le profil client en temps réel pour obtenir une vue d’ensemble de chaque client et de ses interactions. Pour en savoir plus, consultez la documentation [du service](../../identity-service/home.md)d&#39;identité.