---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Identity Service d’Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Présentation du service Identity Service

La diffusion d’expériences numériques pertinentes nécessite une compréhension complète de votre client. Cela est rendu plus difficile lorsque les données de vos clients sont fragmentées entre des systèmes disparates, ce qui donne à chaque client l’impression d’avoir plusieurs &quot;identités&quot;. Le service d’identité Adobe Experience Platform vous permet de mieux  de vos clients et de leur comportement en rapprochant les identités entre les périphériques et les systèmes, ce qui vous permet de diffuser en temps réel des expériences numériques personnelles et impactées.

## Présentation du service d’identité

Chaque jour, les clients interagissent avec votre entreprise et établissent une relation sans cesse croissante avec votre marque. Un client type peut être actif dans un certain nombre de systèmes au sein de l’infrastructure de données de votre entreprise, tels que votre commerce électronique, votre fidélité et vos systèmes d’assistance. Ce même client peut également s&#39;engager anonymement sur un nombre indéfini d&#39;appareils. Identity Service vous permet de rassembler une image complète de votre client, en agrégeant des données connexes qui pourraient autrement être réparties sur des systèmes différents.

Prenons un exemple quotidien de la relation d’un consommateur avec votre marque :

Mary a un compte sur votre site de commerce électronique où elle a passé quelques commandes. Elle utilise généralement son ordinateur portable pour faire ses achats, où elle se connecte à chaque fois. Cependant, lors de l&#39;une de ses visites, elle utilise sa tablette pour acheter des sandales, mais ne passe pas de commande et ne se connecte pas.

À ce stade, le  de Mary  apparaît comme deux distincts  : son identifiant de connexion eCommerce et son appareil à tablette, peut-être identifié par l’identifiant du périphérique.

Marie reprend ensuite sa session sur tablette et fournit son adresse électronique lors de l’abonnement à votre bulletin d’information. Ce faisant, l’ingestion en flux continu ajoute une nouvelle identité en tant que données d’enregistrement dans son . En conséquence, Identity Service associe désormais le périphérique de tablette de Mary  le  de son compte eCommerce.

D&#39;ici le clic suivant sur sa tablette, votre contenu ciblé pourrait refléter l&#39;histoire et la  de Mary, plutôt qu&#39;une tablette utilisée par un acheteur inconnu.

Les relations d&#39;identité définies et maintenues par Identity Service sont exploitées par les clients en temps réel pour obtenir une image complète d&#39;un client et de ses interactions avec votre marque. Pour plus d’informations, reportez-vous à la présentation [du de clients en temps](../profile/home.md)réel.

### Identités

Une identité est une donnée propre à une entité, généralement une personne individuelle. Une identité telle qu’un identifiant de connexion, un identifiant ECID ou un identifiant de fidélité est appelée identité **** connue.

Les informations d’identification personnelle, telles que l’adresse électronique et le numéro de téléphone, permettent d’identifier directement un client. En conséquence, les informations d’identification personnelle sont utilisées pour faire correspondre les identités multiples d’un client sur plusieurs systèmes.

**Des identités** inconnues ou anonymes distinguent un appareil sans identifier la personne qui l&#39;utilise. Ce comprend des informations telles qu’une adresse IP et un ID de cookie . Bien que les données comportementales puissent être collectées à partir d’un périphérique à l’aide d’identités inconnues, l’association de ces identités entre des périphériques ou des supports est limitée jusqu’à ce que votre client fournisse des informations d’identification personnelle pendant son voyage.

Comme le montre l&#39;illustration ci-dessous, les identités connues et anonymes sont deux composantes importantes des graphiques [d&#39;](#identity-graphs)identité, qui sont abordées plus loin dans ce .

![Collage d&#39;identité sur la plateforme](./images/identity-service-stitching.png)

Voici quelques exemples d’implémentation de Identity Service :

- Un de télécommunications peut se fier à la valeur du &quot;numéro de téléphone&quot;, où un numéro de téléphone se rapporte à la même personne intéressée dans les ensembles de données hors ligne et en ligne.
- Un de vente au détail peut utiliser &quot;adresse électronique&quot; dans des jeux de données hors ligne et ECID dans des jeux de données en ligne en raison du pourcentage élevé de anonymes.
- Une banque peut préférer le &quot;numéro de compte&quot; dans les jeux de données hors ligne, comme les transactions de succursale. Ils peuvent dépendre de l’&quot;identifiant de connexion&quot; dans les jeux de données en ligne, car la plupart des seront authentifiés au cours de leur visite.
- Vos clients peuvent également disposer d’ID propriétaires uniques, tels que GUID ou d’autres identifiants universellement uniques.

### Données d’identité

Si vous demandiez à quelqu&#39;un : &quot;Quel est votre numéro d&#39;identification ?&quot; sans autre contexte, il serait difficile pour eux de fournir une réponse utile. Dans la même logique, une valeur de chaîne représentant une valeur d’identité, qu’il s’agisse d’un ID généré par le système ou d’une adresse électronique, n’est terminée que lorsqu’elle est fournie avec un qualificateur qui fournit le contexte de la valeur de chaîne : l&#39;identité  .

## Graphiques d&#39;identité   et d&#39;identité

Vos clients peuvent interagir avec votre marque par le biais d’une combinaison de  en ligne et hors ligne, ce qui pose le problème de la manière de concilier ces interactions fragmentées en une seule identité de client.

La plateforme d’expérience aborde ce défi à l’aide de deux concepts :  [identité](#identity-namespaces) et graphiques [](#identity-graphs)identitaires.

### Espaces de noms d’identité

Lorsque votre client interagit avec votre marque sur plusieurs , y compris sur le Web, l’application mobile, le centre d’appels ou une vitrine, il peut s’avérer difficile de les comprendre et de les servir si vous ne pouvez pas observer et suivre leur  sur l’ensemble du.

Comprendre votre client sur plusieurs périphériques et  en les reconnaissant dans chaque . Pour ce faire, Adobe Experience Platform utilise l’ d’identité .
Un  d’identité est un identifiant tel que l’ID de périphérique ou l’ID de courrier électronique utilisé pour fournir le contexte d’origine des données. Les d&#39;identité  sont utilisés pour rechercher ou lier des identités individuelles et fournir un contexte pour les valeurs d&#39;identité afin d&#39;éviter les collisions de données. Par exemple, l’ID &quot;123456&quot; peut faire référence à une personne dans votre système de commerce électronique et à une autre personne dans votre système de support technique. Pour plus d&#39;informations, reportez-vous à la [présentation](./namespaces.md)des d&#39;identité.

### Graphiques d’identité

Un graphique d’identité est une carte des relations entre différents espaces de noms d’identité. Il permet de visualiser la façon dont un client interagit avec votre marque sur différents canaux.

Tous les graphiques d’identité client sont gérés et mis à jour collectivement par Identity Service en temps quasi réel, en réponse à l’activité du client.

Identity Service gère un graphique d’identité visible par votre entreprise uniquement et basé sur vos données. Il est appelé graphique privé. Identity Service augmente le graphique privé lorsqu’un enregistrement de données ingérées contient plusieurs identités, ajoutant ainsi une relation entre les identités trouvées.

À titre d&#39;exemple des types de facteurs potentiels à prendre en compte lors de la fourniture et de l&#39;étiquetage des données d&#39;identité, l&#39;utilisation de numéros de téléphone tels que &quot;téléphone de travail&quot; peut générer plus de relations que ce que vous prévoyez dans le graphique d&#39;identité. Vous trouverez peut-être que beaucoup d&#39;employés se réfèrent au même nombre pour le travail, et que &quot;maison&quot; et &quot;mobile&quot; servent mieux à garder les relations aussi précises que possible.

## Fourniture de données d&#39;identité au service Identity Service

Cette section explique comment les données fournies à Adobe Experience Platform sont traitées avant d’être utilisées par Identity Service pour créer un graphique d’identité pour chaque client.

### Déterminer les champs d’identité

En fonction de la stratégie de collecte de données de votre entreprise, les champs de données que vous étiquetez comme identités déterminent quelles données sont incluses dans votre carte d’identité. Pour tirer le meilleur parti d’Adobe Experience Platform et des identités des clients les plus complètes possible, vous devez télécharger des données en ligne et hors ligne.

- Les données en ligne décrivent la présence et le comportement en ligne, tels que les noms d’utilisateur et les adresses électroniques.

- Les données hors ligne font référence à des données qui ne sont pas directement liées à la présence en ligne, telles que les identifiants des systèmes CRM. Ce type de données rend vos identités plus robustes et prend en charge la cohésion des données dans vos systèmes disparates.

### Créer une identité supplémentaire  

Bien que la plate-forme d’ d’expérience  un large éventail de de  standard, vous devrez peut-être créer des supplémentaires pour classer correctement vos identités. Pour plus d&#39;informations, reportez-vous à la section sur l&#39; [affichage et la création de   pour votre organisation](./namespaces.md) dans l&#39;aperçu des  de d&#39;identité.

>[!NOTE] Les d&#39;identité  sont un qualificatif pour les identités. Par conséquent, une fois qu’un   a été créé, il ne peut plus être supprimé.

### Inclure les données d’identité dans le modèle de données d’expérience (XDM)

Le modèle de données d’expérience (XDM), qui constitue le cadre normalisé selon lequel la plate-forme organise les données client, permet de partager et de comprendre les données entre la plate-forme d’expérience et d’autres services interagissant avec la plate-forme. Pour plus d&#39;informations, consultez la présentation [du système](../xdm/home.md)XDM.

Les d&#39;enregistrements et de séries chronologiques  permettent d&#39;inclure des données d&#39;identité. Au fur et à mesure que les données sont ingérées, le graphique d’identité crée de nouvelles relations entre les fragments de données provenant de différents  de  s’ils se révèlent partager des données d’identité communes.

### Marquage des champs XDM en tant qu’identité

Tout champ de type `string` dans les  de qui met en oeuvre des classes XDM d’enregistrement ou de série chronologique peut être étiqueté comme champ d’identité. Par conséquent, toutes les données saisies dans ce champ seraient considérées comme des données d’identité.

Les champs d’identité permettent également de lier des identités s’ils partagent des données d’identification personnelle communes.
Par exemple, en étiquetant les champs de numéro de téléphone comme champs d’identité, Identity Service crée automatiquement un graphique des relations avec les autres personnes qui utilisent le même numéro de téléphone.

>[!NOTE] Le   des identités résultantes est fourni au moment où le champ est libellé.

### Configuration d’un jeu de données pour Identity Service

Pendant le processus d’assimilation en flux continu, Identity Service extrait automatiquement les données d’identité des données d’enregistrement et de série chronologique. Toutefois, avant de pouvoir assimiler des données, celles-ci doivent être activées pour Identity Service. Pour plus d’informations, consultez le didacticiel sur la [configuration d’un jeu de données pour les  de clients en temps réel et le service d’identité à l’aide des API](../profile/tutorials/dataset-configuration.md) .

### Envoi de données au service Identity Service

Identity Service consomme des données conformes XDM envoyées à la plateforme Experience Platform par ingestion [](../ingestion/batch-ingestion/overview.md) par lot ou par ingestion [en](../ingestion/streaming-ingestion/overview.md)flux continu.

## Gouvernance des données

La plateforme Adobe Experience Platform a été créée en tenant compte de la confidentialité et comprend une structure de gouvernance des données pour protéger les données d’identification personnelle de vos clients. Les données d’identité sous le &quot;email&quot; ou &quot;phone&quot;  sont chiffrées par défaut, mais pour s’assurer que les données sensibles sont chiffrées avant qu’elles ne soient conservées, des libellés d’utilisation des données peuvent être appliqués aux données lors de leur assimilation ou lorsqu’elles arrivent dans Platform. Pour plus d&#39;informations, veuillez lire la présentation [sur la gouvernance des](../data-governance/home.md)données.

## Étapes suivantes

Maintenant que vous connaissez les concepts clés d’Identity Service et de son rôle dans Experience Platform, vous pouvez commencer à apprendre à utiliser votre graphique d’identité à l’aide de l’API [](./api/getting-started.md)Identity Service.