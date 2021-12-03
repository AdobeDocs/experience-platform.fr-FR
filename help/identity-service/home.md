---
keywords: Experience Platform;accueil;rubriques populaires;identité;Identité;graphiques XDM;identity service;Identity service
solution: Experience Platform
title: Présentation dʼIdentity Service
topic-legacy: overview
description: Adobe Experience Platform Identity Service vous permet de mieux connaître vos clients et leurs comportements, en établissant un lien entre les identités des différents appareils et systèmes, ce qui vous permet de proposer des expériences numériques personnelles et percutantes en temps réel.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: eb0fe2267416c5053cb589cc6d147324cc31c985
workflow-type: ht
source-wordcount: '1747'
ht-degree: 100%

---

# Présentation d’[!DNL Identity Service]

Proposer des expériences numériques pertinentes nécessite une compréhension complète de votre client. Cela devient plus difficile lorsque les données de vos clients sont fragmentées entre plusieurs systèmes ; chaque client semble alors posséder plusieurs « identités ».

Adobe Experience Platform Identity Service vous offre la possibilité de mieux connaître vos clients et leur comportement en établissant un lien entre les identités des différents appareils et systèmes, ce qui vous permet de proposer des expériences numériques personnelles et percutantes en temps réel.

Avec [!DNL Identity Service], vous pouvez réaliser les actions suivantes :

- Veiller à ce que vos clients bénéficient d’une expérience cohérente, personnalisée et pertinente lors de chaque interaction.
- Combiner plusieurs identités différentes à partir de sources disparates et créer une vue d’ensemble complète de vos clients.
- Utiliser un graphique d’identités pour mapper différents espaces de noms d’identité, ce qui vous permet d’avoir une représentation visuelle de la manière dont vos clients interagissent avec votre marque sur différents canaux.

## Prise en main

Avant de rentrer dans les détails de [!DNL Identity Service], voici un résumé des termes clés :

| Terme | Définition |
| --- | --- |
| Identité | Une identité correspond à des données propres à une entité, généralement une personne individuelle. Une identité telle qu’un identifiant de connexion, un ECID ou un identifiant de fidélité correspond à une « identité connue ». |
| ECID | L’identifiant Experience Cloud ID (ECID) est un espace de noms d’identité partagé utilisé dans les applications Experience Platform et Adobe Experience Cloud. ECID fournit une base pour l’identité du client et est utilisé comme ID principal pour les appareils et comme nœud de base pour les graphiques d’identités. Pour plus d’informations, consultez la [présentation ECID](./ecid.md). |
| Espace de noms d’identité | Un espace de noms d’identité sert à distinguer le contexte ou le type d’une identité. Par exemple, une identité identifie « name<span>@email.com » comme adresse e-mail ou « 443522 » comme identifiant CRM numérique. Les espaces de noms d’identité sont utilisés pour rechercher des identités individuelles et fournir le contexte des valeurs d’identité. Cela vous permet de déterminer que deux fragments [!DNL Profile] contenant des identifiants principaux différents mais partageant la même valeur pour l’espace de noms d’identité `email` sont en fait la même personne. Pour plus d’informations, voir [Présentation des espaces de noms d’identité](./namespaces.md). |
| Graphique d’identités | Un graphique d’identités est une carte des relations entre différentes identités, ce qui vous permet de visualiser et de mieux comprendre les identités de client qui sont regroupées et comment. Pour plus d’informations, consultez le tutoriel sur [à l’aide de la visionneuse de graphiques d’identités](./ui/identity-graph-viewer.md). |
| Informations d’identification personnelle (PII) | Les PII sont des informations qui permettent d’identifier directement un client, telles qu’une adresse e-mail ou un numéro de téléphone. Les valeurs des PII sont souvent utilisées pour faire correspondre. les identités multiples d’un client sur différents systèmes. |
| Identités inconnues ou anonymes | Les identités inconnues ou anonymes sont des indicateurs qui isolent les appareils sans identifier la personne qui utilise l’appareil. Les identités inconnues et anonymes incluent des informations telles que l’adresse IP et l’ID de cookie d’un visiteur. Bien que les identités inconnues et anonymes puissent fournir des données comportementales, elles sont limitées jusqu’à ce qu’un client fournisse ses informations d’identification personnelle. |

## Qu’est-ce que [!DNL Identity Service] ?

Chaque jour, les clients interagissent avec votre entreprise et établissent une relation en constante évolution avec votre marque. Un client type peut être actif dans un certain nombre de systèmes au sein de l’infrastructure de données de votre organisation, comme vos systèmes d’e-commerce, de fidélité et de service d’assistance. Ce même client peut également utiliser un nombre illimité d’appareils de manière anonyme. [!DNL Identity Service] vous permet de dresser le portrait complet de votre client, en agrégeant des données connexes qui pourraient autrement être réparties dans différents systèmes.

Prenons un exemple courant de relation entre un consommateur et votre marque :

- Marie possède un compte sur votre site d’e-commerce sur lequel elle a déjà passé quelques commandes. En général, elle utilise son ordinateur portable personnel pour se connecter lorsqu’elle fait des achats. Cependant, lors d’une de ses visites, elle a utilisé sa tablette pour chercher des sandales, mais n’a pas passé de commande et ne s’est pas connectée.
- À ce stade, l’activité de Marie apparaît sous la forme de deux profils distincts :
   - Son nom d’utilisateur e-commerce
   - Sa tablette, peut-être identifiée au moyen de l’identifiant de l’appareil
- Plus tard, Marie relance la session sur sa tablette et fournit son adresse e-mail en s’abonnant à votre newsletter. Ce faisant, l’ingestion par flux ajoute une nouvelle identité en tant que données d’enregistrement dans son profil. [!DNL Identity Service] associe désormais lʼactivité sur la tablette de Marie à lʼhistorique de son compte dʼe-commerce.
- La prochaine fois qu’elle utilisera sa tablette, votre contenu ciblé pourra refléter le profil et l’historique complets de Marie, plutôt qu’une simple tablette utilisée par un client inconnu.

![Combinaison d’identités sur Platform](./images/identity-service-stitching.png)

Pour résumer, [!DNL Identity Service] vous permet de dresser le portrait complet de votre client en agrégeant des données connexes qui pourraient autrement être éparpillées sur différents systèmes. Les relations d’identité définies et maintenues par [!DNL Identity Service] sont exploitées par le profil client en temps réel pour dresser le portrait complet d’un client et de ses interactions avec votre marque. Pour plus d’informations, consultez la [présentation de Real-time Customer Profile](../profile/home.md).

### Cas d’utilisation

Voici quelques exemples de mise en œuvre dʼ[!DNL Identity Service] :

- Une société de télécommunications peut se baser sur la valeur « numéro de téléphone », où un numéro de téléphone correspond à la même personne dans les jeux de données hors ligne et en ligne.
- Une société de vente au détail peut utiliser la valeur « adresse e-mail » dans des jeux de données hors ligne et un ECID dans des jeux de données en ligne en raison du pourcentage élevé de visiteurs anonymes.
- Une banque peut préférer la valeur « numéro de compte » dans les jeux de données hors ligne, comme les transactions des succursales. Il se peut qu’elle dépende de la valeur « identifiant de connexion » dans les jeux de données en ligne, car la plupart des visiteurs sont authentifiés au cours de leur visite.
- Vos clients peuvent également disposer d’identifiants propriétaires uniques, comme un GUID ou d’autres identifiants universels uniques.

## Espaces de noms d’identité

Si vous demandez à une personne : « Quel est votre identifiant ? » sans autre précision, il lui sera difficile de fournir une réponse utile. Dans la même logique, une valeur de chaîne représentant une valeur d’identité, qu’il s’agisse d’un identifiant généré par le système ou d’une adresse e-mail, n’est complète que lorsqu’elle est accompagnée d’un qualificateur qui fournit le contexte de la valeur de chaîne : l’espace de noms d’identité.


Vos clients peuvent interagir avec votre marque par le biais d’une combinaison de canaux en ligne et hors ligne, ce qui crée une difficulté lorsqu’il s’agit de rassembler ces interactions fragmentées en une seule identité client.

Pour comprendre votre client sur plusieurs appareils et canaux, vous devez commencer par le reconnaître dans chaque canal. Pour ce faire, Platform utilise les espaces de noms d’identité. Un espace de noms d’identité est un identifiant, tel que E-mail ou Téléphone, utilisé pour fournir un contexte supplémentaire aux identités du client. Les espaces de noms d’identité sont utilisés pour rechercher ou lier des identités individuelles et fournir un contexte pour les valeurs d’identité. Pour plus d’informations, voir [Présentation des espaces de noms d’identité](./namespaces.md).

## Graphiques d’identités

Un graphique d’identités est une carte des relations entre différents espaces de noms d’identité, ce qui vous permet de visualiser et de mieux comprendre les identités de client qui sont regroupées, ainsi que la manière dont elles sont regroupées. Pour plus d’informations, consultez le tutoriel sur [l’utilisation de la visionneuse de graphiques d’identités](./ui/identity-graph-viewer.md).

La vidéo suivante est destinée à étayer votre compréhension des identités et des graphiques dʼidentité.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## Fourniture de données dʼidentité à [!DNL Identity Service]

Cette section décrit le traitement des données fournies à Adobe Experience Platform avant quʼelles ne soient utilisées par [!DNL Identity Service] pour créer un graphique dʼidentité pour chaque client.

### Choix des champs d’identité

En fonction de la stratégie de collecte de données de votre entreprise, les champs de données que vous désignez comme identités déterminent les données qui sont incluses dans votre carte d’identité. Pour tirer le meilleur parti d’Adobe Experience Platform et obtenir les identités de clients les plus complètes possible, vous devez charger des données en ligne et hors ligne.

- Les données en ligne décrivent la présence et le comportement en ligne, comme les noms d’utilisateur et les adresses électroniques.

- Les données hors ligne ne sont pas directement liées à la présence en ligne, comme les identifiants des systèmes CRM. Ce type de données renforce vos identités et favorise la cohésion des données entre vos systèmes disparates.

### Création d’espaces de noms d’identité supplémentaires

Bien qu’Experience Platform offre de nombreux espaces de noms standard, vous devrez peut-être créer des espaces de noms supplémentaires pour classer correctement vos identités. Pour plus d’informations, consultez la section sur la [consultation et création d’espaces de noms pour votre organisation](./namespaces.md) dans la présentation des espaces de noms d’identité.

>[!NOTE]
>
>Les espaces de noms d’identité sont des qualificateurs d’identités. Par conséquent, une fois qu’un espace de noms a été créé, il ne peut pas être supprimé.

### Inclusion des données dʼidentité dans [!DNL Experience Data Model] (XDM)

En tant que cadre normalisé selon lequel [!DNL Platform] organise les données clients, [!DNL Experience Data Model] (XDM) permet de partager et de comprendre les données utilisées sur Experience Platform et d’autres services interagissant avec [!DNL Platform]. Pour plus d’informations, consultez la [présentation du système XDM](../xdm/home.md).

Les schémas d’enregistrement et de série temporelle permettent d’inclure des données d’identité. À mesure que les données sont ingérées, le graphique d’identités crée de nouvelles relations entre les fragments de données provenant de différents espaces de noms s’il s’avère qu’ils partagent des données d’identité communes.

### Désignation des champs XDM comme identité

Les champs de type `string` dans les schémas qui mettent en œuvre des classes XDM d’enregistrement ou de série temporelle peuvent être qualifiés de champs d’identité. Par conséquent, toutes les données ingérées dans ces champs seraient considérées comme des données d’identité.

>[!NOTE]
>
>Les champs de type tableau et mappage ne sont pas pris en charge et ne peuvent pas être marqués et libellés comme des champs dʼidentité.

Les champs d’identité permettent également de lier des identités si elles partagent des données PII communes.
Par exemple, en désignant les champs de numéro de téléphone comme des champs dʼidentité, [!DNL Identity Service] crée automatiquement un graphique des relations avec les autres personnes qui utilisent le même numéro de téléphone.

>[!NOTE]
>
>L’espace de noms des identités résultantes est fourni au moment où le champ est libellé.

### Configuration dʼun jeu de données pour [!DNL Identity Service]

Pendant le processus dʼingestion par flux, [!DNL Identity Service ]extrait automatiquement les données dʼidentité des données dʼenregistrement et de série temporelle. Cependant, les données doivent être activées pour [!DNL Identity Service] avant de pouvoir être ingérées. Pour plus d’informations, consultez le tutoriel sur la [configuration d’un jeu de données pour Real-time Customer Profile et Identity Service à l’aide des API](../profile/tutorials/dataset-configuration.md).

### Envoi de données à [!DNL Identity Service]

[!DNL Identity Service] consomme des données conformes à XDM envoyées à Experience Platform par [ingestion par lots](../ingestion/batch-ingestion/overview.md) ou [ingestion par flux](../ingestion/streaming-ingestion/overview.md).

La vidéo suivante est destinée à vous aider à comprendre Identity Service. Cette vidéo explique comment libeller les champs de données comme des identités, ingérer les données dʼidentité, puis vérifier que les données ont été enregistrées dans le graphique Privé dʼAdobe Experience Platform Identity Service.

>[!WARNING]
>
>Lʼinterface utilisateur de [!DNL Platform] affichée dans la vidéo suivante est obsolète. Reportez-vous à la documentation pour obtenir les dernières captures dʼécran et fonctionnalités de lʼinterface utilisateur.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Gouvernance des données

Adobe Experience Platform a été conçue dans une optique de confidentialité et comprend une structure de gouvernance des données pour protéger les données PII de vos clients. Les données d’identité sous l’espace de noms « e-mail » ou « téléphone » sont chiffrées par défaut. Toutefois, pour s’assurer que les données sensibles sont chiffrées avant qu’elles ne soient conservées, des libellés d’utilisation des données peuvent être appliqués aux données lors de leur ingestion ou lorsqu’elles arrivent dans [!DNL Platform]. Pour plus d’informations, consultez la [présentation de la gouvernance des données](../data-governance/home.md).

## Étapes suivantes

Maintenant que vous comprenez les concepts clés du [!DNL Identity Service] et son rôle au sein d’Experience Platform, vous pouvez commencer à apprendre à travailler avec votre graphique d’identités à l’aide de l’[[!DNL Identity Service API]](./api/getting-started.md).
