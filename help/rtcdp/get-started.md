---
keywords: RTCDP;CDP;Real-Time Customer Data Platform;real time customer data platform;real time cdp;cdp;rtcdp
title: Prise en main de Real-Time Customer Data Platform
description: Utilisez cet exemple de scénario comme exemple lors de la configuration de votre implémentation d’Adobe Real-Time Customer Data Platform.
feature: Get Started, Use Cases
exl-id: 9f775d33-27a1-4a49-a4c5-6300726a531b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2326'
ht-degree: 62%

---

# Prise en main de Real-Time Customer Data Platform

Ce guide de prise en main vous guide tout au long d’un exemple d’implémentation de Real-Time Customer Data Platform (Real-Time CDP). Vous pouvez l’utiliser comme exemple lors de la configuration de votre propre implémentation. Bien que ce guide présente des exemples spécifiques, il fournit des liens vers des informations supplémentaires que vous pouvez utiliser lors de la création de votre configuration.

Cet exemple illustre la puissance de Real-Time Customer Data Platform, optimisé par Adobe Experience Platform, pour :

* ingérer des données à partir de plusieurs sources ;
* Les fusionner en un seul [!DNL real-time customer profile]
* diffuser une expérience cohérente, pertinente et personnalisée sur tous les appareils.

## Cas d’utilisation

Luma, une entreprise de vêtements de sport, cherche constamment à améliorer son expérience client. L’entreprise a lancé une nouvelle initiative pour augmenter les ventes de cadeaux. Elle souhaite également réduire la surexposition, notamment les publicités intempestives que les clients reçoivent en permanence.

Actuellement, ils dépensent trop pour les médias qui reciblent des articles que le visiteur ne va pas acheter à l&#39;avenir. Par exemple, Luma ne souhaite pas recibler une personne avec un article conçu comme un achat unique pour quelqu’un d’autre.

Actuellement, les données de Luma sont dispersées dans plusieurs sources. Elle fait donc face à des défis importants :

* Le service marketing doit collaborer avec différentes équipes possédant chacune une source de données, notamment un site web, une application mobile, des systèmes de fidélité, un système CRM, etc.
* Au moment où l’équipe marketing accède aux données, elles sont souvent obsolètes et ne sont plus pertinentes pour les campagnes où le temps joue un rôle important.
* Elle doit unifier les données pour cibler une personne, et non les canaux.

Par conséquent, Luma a adopté les objectifs suivants :

* Créer une vue unique en temps réel des clients à partir de ses sources de données disparates
* Personnaliser les campagnes marketing avec des messages pertinents sur différents canaux et appareils

Pour atteindre ces objectifs, l’équipe marketing doit être en mesure de gérer les données clients à l’échelle.

Avec Real-Time CDP, optimisé par Adobe Experience Platform, le service marketing de Luma peut :

1. collecter des données à partir de plateformes disparates et s’assurer qu’elles sont disponibles en aval pour d’autres activités marketing ;
1. créer une vue unique en temps réel des consommateurs, indépendamment de l’origine des données ;
1. offrir une expérience cohérente, pertinente et personnalisée sur chaque point de contact.

## Étapes

Ce tutoriel comprend les étapes suivantes :

1. Création du [profil client](#customer-profile)
1. [Personnalisation](#personalizing-the-user-experience) de l’expérience utilisateur
1. Utilisation de [plusieurs sources de données](#using-multiple-data-sources)
1. [Configuration d’une source de données](#configuring-a-data-source)
1. [Collecte des données](#bringing-the-data-together-for-a-specific-customer) pour un client spécifique
1. Configurer des [audiences](#audiences).
1. Configuration des [destinations](#destinations)
1. [Ajout du profil sur plusieurs appareils](#cross-device-identity-stitching)
1. [Analyse du profil](#analyzing-the-profile)

## Profil client

Lorsque les clients consultent votre site pour la première fois, vous ignorez tout d’eux.

![image](assets/luma-site.png)

Lors de leur navigation, les données sont capturées en temps réel et envoyées non seulement à une suite de rapports dans Adobe Analytics, mais également directement à Adobe Experience Platform. À mesure que les données sont collectées, vous commencez à former une vue unique du consommateur, basée sur les données comportementales dans [!DNL Experience Platform's real-time customer profile].

De nombreux visiteurs du site web sont probablement des clients réguliers qui ont déjà effectué des achats chez Luma.  Il est important que Luma personnalise les messages et les offres pour s’adresser aux nouveaux visiteurs, aux visiteurs réguliers, ainsi qu’aux clients connus.

### Première visite d’un nouveau client

Par exemple, un visiteur non identifié accède à la section pour hommes sur le site Luma et consulte deux sweats en cours d’exécution.

![Image](assets/luma-sweatshirts.png)

Lorsque le client navigue pour en savoir plus sur ces produits, ces consultations des produits sont collectées dans Adobe Analytics et envoyées à [!DNL Experience Platform].

<!--![image](assets/luma-shirt-detail.png)-->

Luma peut faire correspondre le comportement du visiteur à un profil utilisateur sur Adobe Experience Platform et commencer à obtenir un aperçu plus riche du comportement de ce consommateur.

### Obtention d’une vue plus détaillée du client

Plus le client interagit avec le site web, plus la vue devient précise. Supposons, par exemple, que le visiteur ajoute un produit au panier et qu’il se connecte.

Lorsqu’il se connecte, il s’identifie sous le nom de Sarah Rose.

![image](assets/luma-login.png)

Deux identités sont fusionnées :

* Les données de navigation anonymes
* Les données existantes associées au compte de Sarah Rose

Les deux identités sont combinées en un seul profil dans [!DNL Experience Platform]. Luma dispose désormais d’une vue unifiée de ce consommateur.

Le comportement de navigation du visiteur anonyme dans la section Hommes du site pouvait laisser penser que le client était un homme. Maintenant qu’elle est connectée, Luma reconnaît Sarah Rose. Luma utilise la puissance du [!DNL Real-Time Customer Profile] pour affiner les messages qui lui sont diffusés sur l’ensemble des canaux.

## Personnalisation de l’expérience utilisateur

Sarah reçoit un message qui la remercie de son statut de membre Bronze et lui offre des informations supplémentaires sur les avantages de son statut et la façon de l’améliorer en augmentant son nombre de points.

Elle accède à la page d’accueil pour en parcourir d’autres.

![Image](assets/luma-personal.png)

Sarah bénéficie d’une expérience de page d’accueil personnalisée diffusée dynamiquement, en fonction de son [!DNL Real-Time Customer Profile] dans Adobe Experience Platform.

Elle voit le contenu pertinent, grâce à la personnalisation optimisée par Adobe Sensei dans Adobe Target, qui prend en compte ses achats précédents et son intérêt pour les vêtements et l’équipement de course à pied. Luma adapte également le contenu du catalogue pour hommes en fonction de l’équipement de course à pied masculin en fonction de sa dernière navigation.

Plus bas sur la page, Sarah découvre les produits phares, ainsi que de nouvelles suggestions basées sur les derniers articles consultés.

Ce contenu personnalisé permet à Sarah de trouver les articles qui l’intéressent rapidement. Cela augmente les conversions et offre une expérience client plus agréable.

### Récupération du client

Sarah change d’activité et quitte le site, mettant fin à sa session. Luma peut utiliser ses données dans Adobe Experience Platform pour l’inciter à revenir sur le site.

Real-Time Customer Data Platform, optimisé par Adobe Experience Platform, est conçu pour la gestion de l’expérience client. Elle permet aux entreprises :

* de simplifier l’intégration et l’activation des données ;
* de gérer l’utilisation des données connues et inconnues ;
* d’accélérer les cas d’utilisation marketing à l’échelle.

## Utilisation de plusieurs sources de données

L’équipe de Luma dispose de toutes les données comportementales et clients à un seul et même endroit.

![image](assets/luma-dash.png)

Elle peut ingérer des données à partir de toutes les sources suivantes :

* Données des solutions Adobe Experience Cloud existantes
* Sources autres qu’Adobe, comme le programme de fidélité de Luma, le centre d’appels et les données du système de point de vente
* Données de flux en temps réel à partir de sources de données Luma
* Données en temps réel provenant des solutions Adobe (aucune nouvelle balise n’est requise)

Toutes ces données provenant de sources disparates sont fusionnées dans un profil client unique et unifié.

## Configuration d’une source de données

Utilisez [!DNL Real-Time Customer Data Platform] pour importer de nouvelles sources de données dans Experience Platform. Real-Time CDP comprend un catalogue de sources de données qui peuvent être ajoutées rapidement et facilement au profil.

![Image](assets/luma-source-cat.png)

Par exemple, pour ingérer les données CRM de Luma, filtrez le catalogue par *CRM*. Tous les connecteurs prêts à l’emploi contenant *CRM* sont répertoriés. Pour ajouter des données [!DNL Microsoft Dynamics CRM] :

1. Autorisez la connexion.

   ![image](assets/luma-source-auth.png)

1. Choisissez ce que vous souhaitez importer depuis une liste recommandée de tables XDM mappées au préalable.

   <!--    ![image](assets/luma-source-import.png) -->

   Par exemple, sélectionnez **[!UICONTROL Contacts]**. Un aperçu des données de contacts est automatiquement chargé afin que vous puissiez vous assurer que tout fonctionne comme prévu.

   Real-Time CDP élimine une grande partie du travail manuel de ce processus en mappant automatiquement les champs standard au schéma de profil [!DNL Experience Data Model] (XDM).

1. Examinez les mappages des champs.

   <!--    ![image](assets/luma-source-mapping.png) -->

   Par exemple, revérifiez que le champ d’adresse e-mail des contacts est correctement mappé.\
   Vous pouvez prévisualiser les données et effectuer un mappage avancé.

1. Définissez un planning.

   ![image](assets/luma-source-sched.png)

C’est fait. Vous venez d’ajouter [!DNL Microsoft CRM] en tant que source de données dans [!DNL Experience Platform].

### Étiquetage des données ingérées pour les politiques d’utilisation

Luma dispose de nombreuses politiques internes qui limitent l’utilisation de certains types d’informations collectées et doit également prendre en compte les questions juridiques et de confidentialité liées à l’utilisation des données. Grâce à la gouvernance des données Adobe Experience Platform, des libellés d’utilisation de données prédéfinis peuvent être appliqués aux jeux de données (et à des champs spécifiques de ces jeux de données), ce qui permet à Luma de classer ses données en fonction de restrictions d’utilisation spécifiques.

![](assets/governance-labels.png)

Une fois les libellés d’utilisation des données appliquées, Luma peut alors utiliser la gouvernance des données pour créer des politiques d’utilisation des données. Les politiques d’utilisation des données sont des règles qui décrivent les types d’actions que vous êtes autorisé à effectuer sur les données qui contiennent certains libellés. Lorsque vous tentez d’effectuer dans Real-Time CDP une action qui constitue une violation de la politique, l’action est bloquée et une alerte est émise pour indiquer quelle politique a été violée et pourquoi.

En outre, Real-Time CDP

## Regroupement des données pour un client spécifique

Dans ce scénario, parcourez les profils à la recherche de Sarah Rose. Son profil s’affiche, avec l’adresse e-mail qu’elle a utilisée pour se connecter.

<!-- ![image](assets/luma-find-profile.png) -->

Toutes les informations que Luma possède sur le profil de Sarah s’affichent. Cela inclut ses informations personnelles telles que l’adresse et le numéro de téléphone, les préférences de communication et les audiences pour lesquelles elle est admissible.

| Catégorie | Description |
|---|---|
| Identités | Affiche les identités qui ont été liées entre elles dans [!DNL Experience Platform] des interactions de Sarah avec Luma sur plusieurs canaux et appareils. Son ECID du site web s’affiche. Son identité comprend également l’ECID de son application mobile, son ID d’e-mail, un ID CRM du jeu de données [!DNL Microsoft Dynamics] récemment ajouté et un ID de fidélité transmis à Adobe Experience Platform par le système de fidélité de Luma. |
| Événements | Affiche toutes les données d’interaction de Sarah avec la marque Luma. Ces données comprennent l’article qu’elle vient de consulter, l’historique de ses consultations, les e-mails qu’elle a reçus, ses interactions avec le centre d’appels, ainsi que le canal et l’appareil utilisés pour chacune de ces interactions. |

Le profil Real-Time CDP réduit le workflow de l’équipe marketing de Luma de quelques semaines à quelques minutes et ouvre la voie à des possibilités de personnalisation basées sur cette vue à 360 degrés du client. Le profil fusionne les données comportementales recueillies lors de sa navigation sur le site avant qu’elle ne se connecte, avec son profil client existant, créant ainsi une vue complète de Sarah.

L’équipe marketing peut utiliser cette [!DNL Real-Time Customer Profile] améliorée pour mieux personnaliser l’expérience de Sarah et accroître sa fidélité à la marque avec Luma.

## Audiences

Les puissantes fonctionnalités de segmentation de Adobe Experience Platform permettent aux spécialistes marketing de combiner des attributs, des événements et des audiences existantes, en fonction des données capturées dans le [!DNL Real-Time Customer Profile].

<!-- ![image](assets/luma-segments.png) -->

Dans ce scénario, les interactions récentes de Sarah sur le site montrent un comportement différent de ses actions passées. Elle achète habituellement des vêtements pour femmes. Cependant, l&#39;article dans son panier est un gros sweat pour homme.

L’équipe de science des données de Luma a créé des modèles autour de la propension à acheter. Un modèle indique un changement soudain de catégorie de vêtements (hommes/femmes, par exemple) ou de taille pour le consommateur existant. Le changement de comportement de Sarah en matière d’achat suggère qu’elle n’achète pas pour elle-même.

<!-- ![image](assets/luma-gift.png) -->

### Définition d’une audience

Utilisez les différentes options de composition visuelle ou d’éditeur d’expression basé sur le code de l’espace de travail des audiences pour modifier ou créer une audience représentant les personnes ayant abandonné leur panier qui semblent être en train d’acheter un cadeau :

```sql
Profile: Category != Preferred Category 
AND 
Product Size != Preferred Size 
in last 7 days.  
AND 
Abandoned Cart 
AND 
Loyalty member 
```

<!-- ![image](assets/luma-abandon.png)-->

Comme Sarah a ajouté un article qui semble être un cadeau dans le panier et l’a abandonné, Luma peut lui proposer un emballage cadeau gratuit.

## Destinations

Lorsque vous avez ajouté l’audience « Abandonnés d’un panier de cadeaux », vous pouvez voir à peu près combien de personnes font partie de cette audience. Vous pouvez prendre des mesures et proposer une personnalisation par le biais de différents canaux.

Sélectionnez **[!UICONTROL Envoyer aux destinations]**.

Dans Real-Time CDP, Luma peut agir de manière transparente sur ses audiences pour la personnalisation.\
Nous voyons ici toutes les destinations disponibles auxquelles Luma peut envoyer cette destination, qu’il s’agisse de solutions Adobe ou de solutions autres qu’Adobe.

![image](assets/luma-dest.png)

### Sélection des destinations

Dans ce scénario, Luma souhaite recibler cette audience avec personnalisation sur ces destinations :

* Google, pour le display
  <!--* Facebook -->
* Adobe Campaign, pour le courrier électronique

<!-- ![image](assets/luma-sched-dest.png) -->

### Planification des destinations

Vous pouvez également planifier l’exportation de l’audience pour qu’elle commence ou se termine à une heure spécifique. L’audience sera publiée et automatiquement mise à jour dans les plateformes configurées aux dates planifiées.

>[!NOTE]
>
>Si vous sélectionnez le champ de date, la planification est automatique pour les 90 jours suivants.

Sélectionnez **[!UICONTROL Enregistrer]** pour accéder à la page suivante.

Lorsqu’un client ou une cliente de cette audience effectue un achat, son adhésion à cette audience est supprimée en temps réel. Ils ne sont plus admissibles parce que leur statut a changé.

Le responsable de l’équipe des médias de Luma peut ainsi économiser des centaines de milliers d’euros en n’utilisant pas l’inventaire pour une audience qui n’est pas qualifiée.

### Application des politiques d’utilisation des données pour les destinations

Adobe Experience Platform comprend des contrôles de confidentialité et de sécurité pour déterminer si une audience peut être activée vers une destination particulière. L’activation est possible ou restreinte en fonction de des objectifs marketing affectés à la destination au moment de sa création, ainsi que des politiques d’utilisation des données définies par votre organisation.

Si votre activité enfreint la politique, un avertissement s’affiche. Cet avertissement contient des informations de lignage de données qui peuvent vous aider à identifier la raison de la violation de la politique et ce que vous pouvez faire pour résoudre la violation.

Grâce à ces contrôles, [!DNL Experience Platform] aide Luma à se conformer aux réglementations et à réaliser un marketing responsable. Ces contrôles sont flexibles et peuvent être modifiés pour répondre aux exigences des équipes de sécurité et de gouvernance de Luma, ce qui leur permet de répondre en toute confiance aux exigences régionales et organisationnelles de gestion des données client connues et inconnues.

<!--

### Data flow canvas

When you save, a visual data flow canvas shows the segment mapped from the unified profile to the three destinations you selected.

![image](assets/luma-flow.png)

-->

## Ajout d’identités sur plusieurs appareils

Sarah consulte un site de médias sociaux sur son appareil mobile et voit une publicité Luma. Celle-ci lui rappelle l’article qu’elle a laissé dans son panier.

Plus tard dans la journée, elle ouvre sa messagerie et découvre les e-mails reciblés. Elle sélectionne un lien vers Luma dans un e-mail.

Ce lien la dirige sur la page d’accueil mobile de Luma, où elle bénéficie d’une expérience hautement personnalisée optimisée par Adobe Target.

* Elle est accueillie en tant que membre Bronze.
* Elle voit le message « Cadeau ».
* Elle voit également le message « Emballage cadeau gratuit », qui fait partie de ses avantages d&#39;adhésion au bronze.
* Elle est toujours ciblée sur l’image à forte identification en raison de son intérêt pour la course à pied.

Elle achète le sweat, ajoute un emballage cadeau et rédige un message pour accompagner le cadeau. Elle peut aussi choisir de recevoir un rappel l’année prochaine pour se souvenir d’acheter un cadeau à l’occasion de cet événement. Elle choisit d’activer cette option et une campagne par e-mail est prévue l’année suivante pour lui rappeler d’acheter un autre cadeau.

Grâce aux possibilités de suppression d’audience, Sarah ne sera plus ciblée avec ce sweat pour hommes.

## Analyse du profil

Les spécialistes marketing de Luma utilisent Adobe Experience Platform pour consulter l’audience des offrants de cadeaux sur le tableau de bord de Real-Time CDP. Ils observent les résultats de cette initiative au fil du temps et constatent qu’elle se développe. Les clients réagissent aux offres et dépensent plus d’argent.

Ces informations permettent aux professionnels du marketing d’agir sur ce signal, qui a été alimenté par la disponibilité de ces données dans CDP et par l’association de clients comme Sarah à l’audience.

Luma utilise les données de cette plateforme pour accroître la fidélité et la satisfaction de ses clients.
