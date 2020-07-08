---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Identity Service d’Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 5%

---


# [!DNL Identity Service] de la validation

La diffusion d’expériences numériques pertinentes nécessite une compréhension complète de votre client. Cela est rendu plus difficile lorsque les données de vos clients sont fragmentées entre des systèmes disparates, ce qui donne à chaque client l’impression d’avoir plusieurs &quot;identités&quot;. L’Adobe Experience Platform [!DNL Identity Service] vous aide à mieux vue de votre client et de son comportement en rapprochant les identités entre les périphériques et les systèmes, ce qui vous permet de fournir des expériences numériques personnelles et impactées en temps réel.

## Understanding [!DNL Identity Service]

Chaque jour, les clients interagissent avec votre entreprise et établissent une relation sans cesse croissante avec votre marque. Un client type peut être actif dans un certain nombre de systèmes de l’infrastructure de données de votre entreprise, tels que votre commerce électronique, votre fidélité et vos systèmes d’assistance. Ce même client peut également s&#39;engager anonymement sur un nombre quelconque d&#39;appareils. [!DNL Identity Service] vous permet de rassembler une image complète de votre client, en agrégeant des données connexes qui pourraient autrement être réparties sur des systèmes disparates.

Prenons l&#39;exemple quotidien de la relation d&#39;un consommateur avec votre marque :

Mary a un compte sur votre site de commerce électronique où elle a passé quelques commandes. Elle utilise généralement son ordinateur portable pour faire ses achats, où elle se connecte à chaque fois. Cependant, lors d&#39;une de ses visites, elle utilise sa tablette pour acheter des sandales, mais ne passe pas de commande et ne se connecte pas.

À ce stade, l&#39;activité de Mary apparaît comme deux profils distincts : son identifiant de connexion eCommerce et son tablette, peut-être identifié par l’identifiant de l’appareil.

Marie reprend ensuite sa session sur tablette et fournit son adresse électronique lors de son abonnement à votre bulletin d’information. Ce faisant, l’assimilation en flux continu ajoute une nouvelle identité en tant que données d’enregistrement dans son profil. En conséquence, [!DNL Identity Service] maintenant fait référence à l&#39;activité de Mary sur les tablettes avec son historique de compte eCommerce.

D&#39;ici le clic suivant sur sa tablette, votre contenu ciblé pourrait refléter l&#39;profil et l&#39;histoire de Marie, plutôt qu&#39;une simple tablette utilisée par un acheteur inconnu.

Les relations d&#39;identité qui [!DNL Identity Service] définissent et maintiennent sont exploitées [!DNL Real-time Customer Profile] pour obtenir une image complète d&#39;un client et de ses interactions avec votre marque. Pour plus d’informations, voir la présentation [du Profil client en temps](../profile/home.md)réel.

### Identités

Une identité est une donnée propre à une entité, généralement une personne individuelle. Une identité telle qu’un identifiant de connexion, un identifiant ECID ou un identifiant de fidélité est appelée identité **** connue.

Les informations d’identification personnelle, telles que l’adresse électronique et le numéro de téléphone, permettent d’identifier directement un client. En conséquence, les informations d’identification personnelle sont utilisées pour faire correspondre les identités multiples d’un client entre les systèmes.

**Des identités** inconnues ou anonymes distinguent un dispositif sans identifier la personne qui l&#39;utilise. Cette catégorie comprend des informations telles que l’adresse IP d’un visiteur et l’ID de cookie. Bien que les données comportementales puissent être collectées à partir d’un périphérique utilisant des identités inconnues, l’association de ces identités entre des périphériques ou des supports est limitée jusqu’à ce que votre client fournisse des informations d’identification personnelle au cours de son voyage.

Comme le montre l&#39;illustration ci-dessous, les identités connues et anonymes sont deux composantes importantes des graphiques [](#identity-graphs)identitaires, qui sont discutées plus loin dans ce document.

![Correspondance d&#39;identité sur Platform](./images/identity-service-stitching.png)

Voici quelques exemples d’ [!DNL Identity Service] implémentations :

- Une société de télécommunications peut se baser sur la valeur du &quot;numéro de téléphone&quot;, où un numéro de téléphone renvoie à la même personne intéressée par les jeux de données en ligne et hors ligne.
- Une société de vente au détail peut utiliser &quot;adresse électronique&quot; dans les jeux de données hors ligne et ECID dans les jeux de données en ligne en raison du pourcentage élevé de visiteurs anonymes.
- Une banque peut préférer le &quot;numéro de compte&quot; dans les jeux de données hors ligne, tels que les transactions de succursale. Ils peuvent dépendre de l&#39;&quot;identifiant de connexion&quot; dans les jeux de données en ligne, car la plupart des visiteurs seront authentifiés au cours de leur visite.
- Vos clients peuvent également disposer d’identifiants propriétaires uniques, tels que GUID ou d’autres identifiants universellement uniques.

### Données d’identité

Si vous demandiez à une personne &quot;Quel est votre identifiant ?&quot; sans autre contexte, il leur serait difficile de fournir une réponse utile. Selon la même logique, une valeur de chaîne représentant une valeur d’identité, qu’il s’agisse d’un identifiant généré par le système ou d’une adresse électronique, n’est complète que lorsqu’elle est fournie avec un qualificateur qui fournit le contexte de la valeur de chaîne : l&#39;espace de nommage d&#39;identité.

## espaces de nommage d’identité et graphiques d’identité

Vos clients peuvent interagir avec votre marque par le biais d’une combinaison de canaux en ligne et hors ligne, ce qui complique la manière de concilier ces interactions fragmentées en une seule identité de client.

[!DNL Experience Platform] relève ce défi en adoptant deux concepts : [espaces de nommage](#identity-namespaces) d&#39;identité et graphiques [](#identity-graphs)d&#39;identité.

### Espaces de noms d’identité

Lorsque votre client interagit avec votre marque sur plusieurs canaux, y compris sur le Web, l’application mobile, le centre d’appels ou une vitrine, il peut être difficile de les comprendre et de les servir si vous ne pouvez pas observer et suivre leur activité sur plusieurs canaux.

Comprendre votre client sur plusieurs périphériques et débuts de canaux en le reconnaissant dans chaque canal. L&#39;Adobe Experience Platform y parvient en utilisant des espaces de nommage d&#39;identité.
Un espace de nommage d&#39;identité est un identifiant tel que l&#39;ID de périphérique ou l&#39;ID de courrier électronique utilisé pour fournir le contexte d&#39;où proviennent les données. Les espaces de nommage d’identité servent à rechercher ou à lier des identités individuelles et à fournir un contexte aux valeurs d’identité afin d’éviter les collisions de données. Par exemple, l’ID &quot;123456&quot; peut faire référence à une personne de votre système de commerce électronique et à une autre personne de votre système de service d’assistance. Pour plus d&#39;informations, consultez la présentation [de l&#39;espace de nommage](./namespaces.md)d&#39;identité.

### Graphiques d’identité

Un graphique d’identité est une carte des relations entre différents espaces de noms d’identité. Il permet de visualiser la façon dont un client interagit avec votre marque sur différents canaux.

All customer identity graphs are collectively managed and updated by [!DNL Identity Service] in near real-time, in response to customer activity.

[!DNL Identity Service] gère un graphique d’identité visible par votre entreprise uniquement et basé sur vos données. Il est appelé graphique privé. [!DNL Identity Service] augmente le graphique privé lorsqu’un enregistrement de données ingérées contient plusieurs identités, ajoutant ainsi une relation entre les identités trouvées.

À titre d&#39;exemple des types de facteurs potentiels à prendre en compte lors de la fourniture et de l&#39;étiquetage des données d&#39;identité, l&#39;utilisation de numéros de téléphone tels que &quot;téléphone de travail&quot; peut entraîner plus de relations que vous ne l&#39;entendez dans le graphique d&#39;identité. Il se peut que de nombreux employés se réfèrent au même nombre pour le travail, et que &quot;domicile&quot; et &quot;mobile&quot; servent mieux à maintenir les relations aussi précises que possible.

## Fourniture de données d&#39;identité à [!DNL Identity Service]

Cette section décrit comment les données fournies à l&#39;Adobe Experience Platform sont traitées avant d&#39;être utilisées par [!DNL Identity Service] pour créer un graphique d&#39;identité pour chaque client.

### Détermination des champs d&#39;identité

En fonction de votre stratégie de collecte de données d’entreprise, les champs de données que vous étiquetez comme identités déterminent quelles données sont incluses dans votre carte d’identité. Pour tirer le meilleur parti de l’Adobe Experience Platform et des identités de clients les plus complètes possible, vous devez télécharger des données en ligne et hors ligne.

- Les données en ligne sont des données qui décrivent la présence et le comportement en ligne, tels que les noms d’utilisateur et les adresses électroniques.

- Les données hors ligne désignent les données qui ne sont pas directement liées à la présence en ligne, telles que les identifiants des systèmes de gestion de la relation client. Ce type de données rend vos identités plus robustes et prend en charge la cohésion des données dans vos systèmes disparates.

### Créer des espaces de nommage d&#39;identité supplémentaires

Bien que [!DNL Experience Platform] les offres présentent divers espaces de nommage standard, vous devrez peut-être créer d’autres espaces de nommage pour classer correctement vos identités. Pour plus d&#39;informations, reportez-vous à la section relative à l&#39; [affichage et à la création d&#39;espaces de nommage pour votre organisation](./namespaces.md) dans la présentation de l&#39;espace de nommage d&#39;identité.

>[!NOTE]
>
>Les espaces de nommage d&#39;identité sont un qualificatif pour les identités. Par conséquent, une fois un espace de nommage créé, il ne peut plus être supprimé.

### Inclure les données d&#39;identité dans [!DNL Experience Data Model] (XDM)

En tant que cadre normalisé d&#39; [!DNL Platform] organisation des données client, [!DNL Experience Data Model] (XDM) permet de partager et de comprendre les données entre [!DNL Experience Platform] et d&#39;autres services interagissant avec [!DNL Platform]. Pour plus d&#39;informations, consultez la présentation [du système](../xdm/home.md)XDM.

Les schémas d&#39;enregistrement et de série chronologique permettent d&#39;inclure des données d&#39;identité. Au fur et à mesure que les données sont ingérées, le graphique d&#39;identité crée de nouvelles relations entre les fragments de données provenant de différents espaces de nommage s&#39;ils se révèlent partager des données d&#39;identité communes.

### Marquage des champs XDM en tant qu’identité

Tout champ de type `string` dans les schémas qui implémentent des classes XDM d&#39;enregistrement ou de série chronologique peut être étiqueté comme champ d&#39;identité. Par conséquent, toutes les données saisies dans ce champ sont considérées comme des données d’identité.

Les champs d’identité permettent également la liaison d’identités s’ils partagent des données d’identification personnelle communes.
Par exemple, en étiquetant les champs de numéro de téléphone comme champs d’identité, [!DNL Identity Service] affiche automatiquement les relations avec les autres personnes qui utilisent le même numéro de téléphone.

>[!NOTE]
>
>L’espace de nommage des identités résultantes est fourni au moment où le champ est libellé.

### Configuration d’un jeu de données pour [!DNL Identity Service]

Pendant le processus d’assimilation en flux continu, extrait [!DNL Identity Service ]automatiquement les données d’identité des données d’enregistrement et de série chronologique. Toutefois, avant de pouvoir ingérer des données, celles-ci doivent être activées pour [!DNL Identity Service]. Pour plus d’informations, consultez le didacticiel sur la [configuration d’un jeu de données pour le service d’Profil et d’identité client en temps réel à l’aide d’API](../profile/tutorials/dataset-configuration.md) .

### Envoi de données à [!DNL Identity Service]

[!DNL Identity Service] consomme les données conformes XDM envoyées à [!DNL Experience Platform] l’unité par assimilation [](../ingestion/batch-ingestion/overview.md) par lot ou par assimilation [](../ingestion/streaming-ingestion/overview.md)en flux continu.

## Gouvernance des données

L’Adobe Experience Platform a été conçu en tenant compte de la confidentialité et comprend un cadre de gouvernance des données pour protéger vos données d’identification personnelle des clients. Les données d’identité sous l’espace de nommage &quot;courriel&quot; ou &quot;téléphone&quot; sont chiffrées par défaut, mais afin de s’assurer que les données sensibles sont chiffrées avant qu’elles ne soient conservées, des étiquettes d’utilisation des données peuvent être appliquées aux données lorsqu’elles sont ingérées ou lorsqu’elles arrivent dans [!DNL Platform]l’. Pour plus d&#39;informations, veuillez lire la présentation [de la gouvernance des](../data-governance/home.md)données.

## Étapes suivantes

Maintenant que vous comprenez les concepts clés de [!DNL Identity Service] et son rôle dans [!DNL Experience Platform]l&#39;environnement, vous pouvez commencer à apprendre à utiliser votre graphique d&#39;identité en utilisant le [!DNL Identity Service API](./api/getting-started.md).