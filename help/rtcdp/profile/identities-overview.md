---
title: Identités et espaces de noms d’identité
seo-title: Service Adobe Experience Platform Identity
description: description
seo-description: description du seo
translation-type: tm+mt
source-git-commit: 5cba5a1e8139dd85f23250d42a1cd8d2318eb916

---


# Identités dans le CDP en temps réel

Le service d’identité Adobe Experience Platform vous permet de mieux connaître vos clients et leur comportement en rapprochant les identités entre les périphériques et les systèmes. En règle générale, vos clients interagissent avec votre marque sur plusieurs canaux, notamment en naviguant sur votre site Web, en faisant un achat en magasin, en rejoignant votre programme de fidélité ou en appelant un service d’assistance pour obtenir de l’aide, pour n’en citer que quelques-uns. Sur ces systèmes multiples, il existe une identité créée pour ce client, et Identity Service permet de rassembler ces identités pour voir le tableau complet.

Maintenant, au lieu de cinq clients distincts interagissant avec votre marque sur cinq canaux différents, vous pouvez voir qu&#39;il s&#39;agit du même client, et vous pouvez vous assurer qu&#39;ils reçoivent une expérience cohérente, personnalisée et pertinente à travers chaque interaction. À mesure que davantage d’informations sur votre client sont connues (par exemple, un navigateur anonyme de votre site Web décide de s’inscrire à un compte et de se connecter), ces informations sont rassemblées et l’image de votre client devient de plus en plus claire.

## Espaces de noms d’identité

Les espaces de noms d’identité sont un composant d’Identity Service et servent d’indicateurs fournissant un contexte supplémentaire aux identités des clients. Un exemple d’espace de noms d’ID couramment utilisé serait &quot;Courrier électronique&quot;, où l’utilisation d’une même adresse électronique sur plusieurs sites Web vous permet de réunir plusieurs identités différentes, chacune avec un ID de client unique, comme appartenant au même client. Experience Platform vous permet d’utiliser des espaces de noms d’ID pour rechercher des profils individuels dans l’interface utilisateur. Pour plus d’informations sur l’affichage des profils, consultez la présentation [du lecteur de](/help/rtcdp/profile/profile-viewer.md)profils. Pour en savoir plus sur les espaces de noms d’identité, consultez la présentation de l’espace de noms [d’identité sur les E/S](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md)Adobe.

## Graphiques d’identité

Un graphique d’identité est une carte des relations entre différents espaces de noms d’identité, qui vous permet de visualiser la manière dont votre client interagit avec votre marque sur différents canaux. Tous les graphiques d’identité du client sont gérés et mis à jour collectivement par Identity Service en temps quasi réel, en réponse à l’activité du client.

Identity Service gère un graphique d’identité visible uniquement par votre entreprise et basé sur vos données, appelées graphique privé. Identity Service augmente le graphique privé lorsqu’un enregistrement de données assimilées contient plusieurs identités, ajoutant ainsi une relation entre les identités trouvées.

## Étapes suivantes

Les identités et les relations entre elles sont définies et conservées par Identity Service et exploitées par le profil du client en temps réel pour obtenir une image complète de chaque client et de ses interactions. Pour en savoir plus, consultez la documentation [Identity Service sur les E/S](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_services_architectural_overview/identity_services_architectural_overview.md)Adobe.