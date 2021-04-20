---
keywords: Experience Platform ; accueil ; rubriques populaires ; identité ; identité ; graphiques XDM ; service d'identité ; service d'identité
solution: Experience Platform
title: Présentation du service d’identité
topic: overview
description: Adobe Experience Platform Identity Service vous permet d'obtenir une meilleure vue de vos clients et de leur comportement en rapprochant les identités entre les périphériques et les systèmes, ce qui vous permet de fournir des expériences numériques personnelles et impactées en temps réel.
translation-type: tm+mt
source-git-commit: bb218fc0cca6fe74693e99747963058bd0dc962a
workflow-type: tm+mt
source-wordcount: '1718'
ht-degree: 73%

---


# [!DNL Identity Service] présentation

Proposer des expériences numériques pertinentes nécessite une compréhension complète de votre client. Cela devient plus difficile lorsque les données de vos clients sont fragmentées entre plusieurs systèmes, chaque client semble donc posséder plusieurs « identités ». Adobe Experience Platform [!DNL Identity Service] vous aide à mieux vue de votre client et de son comportement en rapprochant les identités entre les périphériques et les systèmes, ce qui vous permet de fournir des expériences numériques personnelles et impactées en temps réel.

## Présentation de [!DNL Identity Service]

Chaque jour, les clients interagissent avec votre entreprise et établissent une relation en constante évolution avec votre marque. Un client type peut être actif dans un certain nombre de systèmes au sein de l’infrastructure de données de votre organisation, comme vos systèmes d’e-commerce, de fidélité et de service d’assistance. Ce même client peut également utiliser un nombre illimité d’appareils de manière anonyme. [!DNL Identity Service] vous permet de dresser le portrait complet de votre client, en agrégeant des données connexes qui pourraient autrement être réparties dans différents systèmes.

Prenons un exemple courant de relation entre un consommateur et votre marque :

Marie possède un compte sur votre site d’e-commerce sur lequel elle a déjà passé quelques commandes. En général, elle utilise son ordinateur portable personnel pour se connecter lorsqu’elle fait des achats. Cependant, lors d’une de ses visites, elle a utilisé sa tablette pour chercher des sandales, mais n’a pas passé de commande et ne s’est pas connectée.

À ce stade, l’activité de Marie apparaît sous la forme deux profils distincts : son nom d’utilisateur d’e-commerce et sa tablette, peut-être identifiée par l’identifiant de l’appareil.

Plus tard, Marie relance la session sur sa tablette et fournit son adresse électronique en s’abonnant à votre newsletter. Ce faisant, l’ingestion par flux ajoute une nouvelle identité en tant que données d’enregistrement dans son profil. Par conséquent, [!DNL Identity Service] fait maintenant le lien entre l&#39;activité des tablettes de Mary et son historique de compte de commerce électronique.

La prochaine fois qu’elle utilisera sa tablette, votre contenu ciblé pourrait refléter le profil et l’histoire complets de Marie, plutôt qu’une simple tablette utilisée par un client inconnu.

Les relations d&#39;identité que [!DNL Identity Service] définit et entretient sont exploitées par [!DNL Real-time Customer Profile] pour obtenir une image complète d&#39;un client et de ses interactions avec votre marque. Pour plus d’informations, consultez la [présentation de Real-time Customer Profile](../profile/home.md).

### Identités

Une identité correspond à des données propres à une entité, généralement une personne individuelle. Une identité telle qu’un identifiant de connexion, un ECID ou un identifiant de fidélité correspond à une identité connue.

Les PII telles que l’adresse électronique et le numéro de téléphone permettent d’identifier directement un client. Par conséquent, les PII sont utilisées pour faire correspondre les identités multiples d’un client sur plusieurs systèmes.

Les identités inconnues ou anonymes distinguent un appareil sans identifier la personne qui l’utilise. Cette catégorie comprend des informations telles que l’adresse IP et l’identifiant de cookie d’un visiteur. Bien que les données comportementales puissent être collectées à partir d’un appareil à l’aide d’identités inconnues, l’association de ces identités sur plusieurs appareils ou supports est limitée jusqu’à ce que votre client fournisse des PII lors de son parcours.

Comme illustré ci-dessous, les identités connues et anonymes sont deux composants importants des [graphiques d’identités](#identity-graphs), qui sont abordés plus loin dans ce document.

![Combinaison d’identités sur Platform](./images/identity-service-stitching.png)

Voici quelques exemples d&#39;implémentations de [!DNL Identity Service] :

- Une société de télécommunications peut se baser sur la valeur « numéro de téléphone », où un numéro de téléphone correspond à la même personne dans les jeux de données hors ligne et en ligne.
- Une société de vente au détail peut utiliser la valeur « adresse électronique » dans des jeux de données hors ligne et un ECID dans des jeux de données en ligne en raison du pourcentage élevé de visiteurs anonymes.
- Une banque peut préférer la valeur « numéro de compte » dans les jeux de données hors ligne, comme les transactions des succursales. Il se peut qu’elle dépende de la valeur « identifiant de connexion » dans les jeux de données en ligne, car la plupart des visiteurs sont authentifiés au cours de leur visite.
- Vos clients peuvent également disposer d’identifiants propriétaires uniques, comme un GUID ou d’autres identifiants universels uniques.

### Données d’identité

Si vous demandez à une personne : « Quel est votre identifiant ? » sans autre précision, il lui sera difficile de fournir une réponse utile. Dans la même logique, une valeur de chaîne représentant une valeur d’identité, qu’il s’agisse d’un identifiant généré par le système ou d’une adresse électronique, n’est complète que lorsqu’elle est accompagnée d’un qualificateur qui fournit le contexte de la valeur de chaîne : l’espace de noms d’identité.

## Espaces de noms d’identité et graphiques d’identités

Vos clients peuvent interagir avec votre marque par le biais d’une combinaison de canaux en ligne et hors ligne, ce qui entraîne le défi consistant à rassembler ces interactions fragmentées en une seule identité client.

[!DNL Experience Platform] relève ce défi grâce à deux concepts : [espaces de noms d’identité](#identity-namespaces) et [graphiques d’identités](#identity-graphs).

La vidéo suivante est destinée à vous aider à comprendre les identités et les graphiques d&#39;identité. La vidéo suivante couvre les trois fonctionnalités de la collecte d’identité, des graphiques d’identité et des API. Il décrit également comment les algorithmes déterministes et probabilistes sont utilisés pour construire des graphiques d&#39;identité privés et traite du rôle des graphiques d&#39;identité privés, des graphiques Co-op du service d&#39;identité de Adobe Experience Platform et des graphiques tiers.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

### Espaces de noms d’identité

Lorsque votre client interagit avec votre marque sur plusieurs canaux, y compris le Web, l’application mobile, le centre d’appel ou une vitrine, il peut s’avérer difficile de le comprendre et de le satisfaire si vous ne pouvez pas observer et suivre son activité sur l’ensemble des canaux.

Pour comprendre votre client sur plusieurs appareils et canaux, vous devez commencer par le reconnaître dans chaque canal. Pour ce faire, Adobe Experience Platform utilise les espaces de noms d’identité.
Un espace de noms d’identité est un identifiant tel que l’identifiant de l’appareil ou l’identifiant de courrier électronique utilisé pour fournir le contexte d’origine des données. Les espaces de noms d’identité sont utilisés pour rechercher ou lier des identités individuelles et fournir un contexte pour les valeurs d’identité afin d’éviter les collisions de données. Par exemple, l’identifiant « 123456 » peut faire référence à une personne dans votre système d’e-commerce et à une autre personne dans votre système de service d’assistance. Pour plus d’informations, consultez la [présentation des espaces de noms d’identité](./namespaces.md).

### Graphiques d’identités

Un graphique d’identités est une carte des relations entre différents espaces de noms d’identité. Il permet de visualiser la façon dont un client interagit avec votre marque sur différents canaux.

Tous les graphiques d&#39;identité des clients sont gérés et mis à jour collectivement par [!DNL Identity Service] en temps quasi réel, en réponse à l&#39;activité des clients.

[!DNL Identity Service] gère un graphique d’identité visible par votre entreprise uniquement et basé sur vos données. Il est appelé graphique privé. [!DNL Identity Service] augmente le graphique privé lorsqu’un enregistrement de données ingérées contient plusieurs identités, ajoutant ainsi une relation entre les identités trouvées.

Pour illustrer les types de facteurs potentiels à prendre en compte lors de la fourniture des données d’identité et de l’application de libellés sur celles-ci, l’utilisation de numéros de téléphone tels que « téléphone professionnel » peut générer davantage de relations que prévu dans le graphique d’identités. Vous constaterez peut-être que de nombreux employés indiquent le même numéro professionnel, et que les numéros « personnels » et « mobiles » sont mieux adaptés pour des relations aussi précises que possible.

Pour plus d&#39;informations, consultez le didacticiel sur l&#39;[accès à la visionneuse de graphiques d&#39;identité](./ui/identity-graph-viewer.md).

## Fourniture de données d&#39;identité à [!DNL Identity Service]

Cette section décrit comment les données fournies à Adobe Experience Platform sont traitées avant d&#39;être utilisées par [!DNL Identity Service] pour créer un graphique d&#39;identité pour chaque client.

### Choix des champs d’identité

En fonction de la stratégie de collecte de données de votre entreprise, les champs de données que vous désignez comme identités déterminent les données qui sont incluses dans votre carte d’identité. Pour tirer le meilleur parti d’Adobe Experience Platform et obtenir les identités de clients les plus complètes possible, vous devez charger des données en ligne et hors ligne.

- Les données en ligne décrivent la présence et le comportement en ligne, comme les noms d’utilisateur et les adresses électroniques.

- Les données hors ligne ne sont pas directement liées à la présence en ligne, comme les identifiants des systèmes CRM. Ce type de données renforce vos identités et favorise la cohésion des données entre vos systèmes disparates.

### Création d’espaces de noms d’identité supplémentaires

Bien que [!DNL Experience Platform] offre divers espaces de nommage standard, vous devrez peut-être créer d&#39;autres espaces de nommage pour classer correctement vos identités. Pour plus d’informations, consultez la section sur la [consultation et création d’espaces de noms pour votre organisation](./namespaces.md) dans la présentation des espaces de noms d’identité.

>[!NOTE]
>
>Les espaces de noms d’identité sont des qualificateurs d’identités. Par conséquent, une fois qu’un espace de noms a été créé, il ne peut pas être supprimé.

### Inclure les données d&#39;identité dans [!DNL Experience Data Model] (XDM)

Comme cadre normalisé selon lequel [!DNL Platform] organise les données client, [!DNL Experience Data Model] (XDM) permet de partager et de comprendre les données dans [!DNL Experience Platform] et d&#39;autres services interagissant avec [!DNL Platform]. Pour plus d’informations, consultez la [présentation du système XDM](../xdm/home.md).

Les schémas d’enregistrement et de série temporelle permettent d’inclure des données d’identité. À mesure que les données sont ingérées, le graphique d’identités crée de nouvelles relations entre les fragments de données provenant de différents espaces de noms s’il s’avère qu’ils partagent des données d’identité communes.

### Désignation des champs XDM comme identité

Les champs de type `string` dans les schémas qui mettent en œuvre des classes XDM d’enregistrement ou de série temporelle peuvent être qualifiés de champs d’identité. Par conséquent, toutes les données ingérées dans ces champs seraient considérées comme des données d’identité.

Les champs d’identité permettent également de lier des identités si elles partagent des données PII communes.
Par exemple, en étiquetant les champs de numéro de téléphone comme champs d&#39;identité, [!DNL Identity Service] montre automatiquement les relations avec les autres personnes qui utilisent le même numéro de téléphone.

>[!NOTE]
>
>L’espace de noms des identités résultantes est fourni au moment où le champ est libellé.

### Configurer un jeu de données pour [!DNL Identity Service]

Au cours du processus d’assimilation en flux continu, [!DNL Identity Service ]extrait automatiquement les données d’identité des données d’enregistrement et de série chronologique. Toutefois, avant de pouvoir ingérer des données, elles doivent être activées pour [!DNL Identity Service]. Pour plus d’informations, consultez le tutoriel sur la [configuration d’un jeu de données pour Real-time Customer Profile et Identity Service à l’aide des API](../profile/tutorials/dataset-configuration.md).

### Envoi de données à [!DNL Identity Service]

[!DNL Identity Service] consomme des données conformes XDM envoyées  [!DNL Experience Platform] soit par  [assimilation par ](../ingestion/batch-ingestion/overview.md) lot, soit par assimilation [ en ](../ingestion/streaming-ingestion/overview.md)flux continu.

La vidéo suivante est destinée à vous aider à comprendre Identity Service. Cette vidéo vous montre comment étiqueter les champs de données comme identités, assimiler des données d&#39;identité, puis vérifier que les données ont été envoyées au graphique privé Adobe Experience Platform Identity Service.

>[!WARNING]
>
>L&#39;interface utilisateur [!DNL Platform] affichée dans la vidéo suivante est obsolète. Reportez-vous à la documentation pour obtenir les dernières captures d&#39;écran et fonctionnalités de l&#39;interface utilisateur.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Gouvernance des données

Adobe Experience Platform a été conçue dans une optique de confidentialité et comprend une structure de gouvernance des données pour protéger les données PII de vos clients. Les données d’identité sous l’espace de noms « e-mail » ou « téléphone » sont chiffrées par défaut. Toutefois, pour s’assurer que les données sensibles sont chiffrées avant qu’elles ne soient conservées, des libellés d’utilisation des données peuvent être appliqués aux données lors de leur ingestion ou lorsqu’elles arrivent dans [!DNL Platform]. Pour plus d’informations, consultez la [présentation de la gouvernance des données](../data-governance/home.md).

## Étapes suivantes

Maintenant que vous comprenez les concepts clés de [!DNL Identity Service] et son rôle dans [!DNL Experience Platform], vous pouvez commencer à apprendre à utiliser votre graphique d&#39;identité en utilisant [[!DNL Identity Service API]](./api/getting-started.md).
