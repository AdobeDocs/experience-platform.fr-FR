---
title: Reciblage hors site des visiteurs non authentifiés
description: Découvrez comment recibler des utilisateurs non authentifiés à l’aide d’identifiants de prospect pour créer un attribut calculé qui peut être utilisé pour créer une audience d’utilisateurs non authentifiés.
feature: Use Cases, Customer Acquisition
exl-id: cffa3873-d713-445a-a3e1-1edf1aa8eebb
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 1%

---

# Reciblage hors site des visiteurs non authentifiés

>[!AVAILABILITY]
>
>Cette fonctionnalité est disponible pour les clients qui disposent d’une licence Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Consultez la [description des produits](https://helpx.adobe.com/fr/legal/product-descriptions.html) pour en savoir plus sur ces packages et contactez votre représentant ou représentante Adobe pour obtenir plus d’informations.

Découvrez comment créer une audience de visiteurs non authentifiés et la recibler à l’aide d’identifiants durables fournis par les partenaires.

![Infographie qui montre le flux de données de partenaire de l’ingestion vers Adobe Experience Platform pour la sortie via les audiences vers une destination en aval.](../assets/offsite-retargeting/header.png)

## Pourquoi tenir compte de ce cas pratique ? {#why-use-case}

Avec l’élimination progressive des cookies tiers, les spécialistes du marketing numérique doivent réinventer leurs stratégies de réengagement avec les visiteurs anonymes. Les marques qui choisissent de s’intégrer aux fournisseurs d’identité pour la reconnaissance des visiteurs en temps réel peuvent également tirer parti des identifiants de partenaire fournis pour le reciblage de médias payants hors site.

Malgré un volume élevé de trafic, de nombreuses marques enregistrent une baisse significative à l’étape de conversion. Les visiteurs interagissent avec le contenu et les démonstrations de produits, mais partent sans s’inscrire ou effectuer un achat.

Non seulement vous pouvez créer des audiences basées sur l’engagement sur site pour personnaliser les messages marketing, mais vous pouvez également utiliser la prise en charge par l’Adobe des identifiants de partenaire pour réengager les visiteurs sur les destinations de médias payants.

## Prérequis et planification {#prerequisites-and-planning}

Lors de la planification du reciblage des visiteurs non authentifiés, tenez compte des conditions préalables suivantes lors de votre processus de planification :

- Ai-je configuré les identifiants des partenaires avec les espaces de noms d’identité appropriés ?

En outre, pour mettre en oeuvre le cas d’utilisation, vous utiliserez les fonctionnalités et éléments d’interface utilisateur de Real-Time CDP suivants. Assurez-vous de disposer des autorisations de contrôle d’accès en fonction des attributs nécessaires pour toutes ces zones ou demandez à votre administrateur système de vous accorder les autorisations nécessaires.

- [Audiences](../../segmentation/home.md)
- [Attributs calculés](../../profile/computed-attributes/overview.md)
- [Destinations](../../destinations/home.md)
- [SDK Web](../../web-sdk/home.md)

## Obtention de données de partenaire dans Real-Time CDP {#get-data-in}

Pour créer une audience de visiteurs non authentifiés, vous devez d’abord obtenir les données de vos partenaires dans Real-Time CDP.

Pour savoir comment importer au mieux des données dans Real-Time CDP à l’aide du SDK Web, consultez les [ sections sur la gestion des données et la collecte de données d’événement](./onsite-personalization.md#data-management) du cas d’utilisation de la personnalisation sur site.

## Transfert des identifiants fournis par les partenaires {#bring-partner-ids-forward}

Après avoir importé les identifiants fournis par le partenaire dans un jeu de données d’événement, vous devrez intégrer ces données aux enregistrements de profil. Vous pouvez le faire en utilisant des attributs calculés.

Les attributs calculés vous permettent de convertir rapidement les données comportementales de profil en valeurs agrégées au niveau du profil. Par conséquent, vous pouvez utiliser ces expressions, telles que &quot;total d’achat sur toute la durée de vie&quot;, dans le profil, ce qui vous permet d’utiliser facilement l’attribut calculé dans vos audiences. Vous trouverez plus d’informations sur les attributs calculés dans la [présentation des attributs calculés](../../profile/computed-attributes/overview.md).

Pour accéder aux attributs calculés, sélectionnez **[!UICONTROL Profils]** suivi de **[!UICONTROL Attributs calculés]** et **[!UICONTROL Créer un attribut calculé]**.

![Le bouton [!UICONTROL Créer des attributs calculés] est mis en surbrillance en plus de l’onglet [!UICONTROL Attributs calculés] dans l’espace de travail [!UICONTROL Profils].](../assets/offsite-retargeting/create-ca.png)

La page **[!UICONTROL Créer un attribut calculé]** s’affiche. Sur cette page, vous pouvez utiliser les composants pour créer votre attribut calculé.

![ L&#39;espace de travail Créer un attribut calculé s&#39;affiche.](../assets/offsite-retargeting/ca-page.png)

>[!NOTE]
>
>Pour plus d’informations sur la création d’attributs calculés, consultez le [guide de l’interface utilisateur des attributs calculés](../../profile/computed-attributes/ui.md).

Pour ce cas d’utilisation, vous pouvez créer un attribut calculé qui, si l’ID de partenaire existe, obtient la valeur la plus récente de l’ID de partenaire au cours des dernières 24 heures.

À l’aide de la barre de recherche, vous pouvez rechercher et ajouter l’événement &quot;Identifiant de partenaire&quot; que [vous avez créé pendant le cas d’utilisation de la personnalisation sur site](#get-data-in) au canevas d’attribut calculé.

![L’onglet [!UICONTROL Événements] et la barre de recherche sont mis en surbrillance.](../assets/offsite-retargeting/ca-add-partner-id.png)

Après avoir ajouté l’événement &quot;Identifiant de partenaire&quot; à la définition, définissez la condition de filtrage des événements sur **[!UICONTROL Exists]**, définissez la condition de filtrage des événements sur la valeur **[!UICONTROL Le plus récent]** de l’identifiant de partenaire ajouté, avec une période de recherche arrière de 24 heures.

![La définition de l’attribut calculé que vous souhaitez créer est mise en surbrillance.](../assets/offsite-retargeting/ca-add-definition.png)

Donnez à l’attribut calculé un nom approprié (par exemple &quot;Identifiant de partenaire&quot;) et une description, puis sélectionnez **[!UICONTROL Publish]** pour terminer le processus de création d’attributs calculé.

![Les informations de base de l’attribut calculé que vous souhaitez créer sont mises en surbrillance.](../assets/offsite-retargeting/ca-publish.png)

## Création d’une audience à l’aide de l’attribut calculé {#create-audience}

Maintenant que vous avez créé l’attribut calculé, vous pouvez utiliser cet attribut calculé pour créer une audience. Dans cet exemple, vous allez créer une audience composée des visiteurs qui ont consulté votre site web plus de 5 fois ce mois-ci, mais qui ne se sont pas encore inscrits.

Pour créer une audience, sélectionnez **[!UICONTROL Audiences]**, puis **[!UICONTROL Créer une audience]**.

![Le bouton [!UICONTROL Créer une audience] est mis en surbrillance.](../assets/offsite-retargeting/create-audience.png)

Une boîte de dialogue s’affiche, vous demandant de choisir entre [!UICONTROL Composer l’audience] et [!UICONTROL Créer la règle]. Sélectionnez **[!UICONTROL Créer la règle]** suivi de **[!UICONTROL Créer]**.

![Le bouton [!UICONTROL Créer une règle] est mis en surbrillance.](../assets/offsite-retargeting/select-build-rule.png)

La page Créateur de segments s’affiche. Sur cette page, vous pouvez utiliser les composants pour créer votre audience.

![Le créateur de segments s’affiche.](../assets/offsite-retargeting/segment-builder.png)

>[!NOTE]
>
>Pour plus d’informations sur l’utilisation du créateur de segments, consultez le [guide de l’interface utilisateur du créateur de segments](../../segmentation/ui/segment-builder.md).

Pour atteindre l’objectif de recherche de ces visiteurs, vous devez d’abord ajouter un événement **[!UICONTROL Page vue]** à votre audience. Sélectionnez l’onglet **[!UICONTROL Événements]** sous **[!UICONTROL Champs]**, puis faites glisser et déposez l’événement **[!UICONTROL Page vue]** et ajoutez-le au canevas de la section des événements.

![L’onglet [!UICONTROL Événements] de la section [!UICONTROL Champs] est mis en surbrillance, tout en affichant l’événement [!UICONTROL Page vue].](../assets/offsite-retargeting/add-page-view.png)

Sélectionnez l’événement **[!UICONTROL Page vue]** nouvellement ajouté. Remplacez la période de recherche arrière de **[!UICONTROL Any time]** par **[!UICONTROL This month]** et remplacez la règle d’événement par **Au moins 5**.

![Les détails de l’événement [!UICONTROL Page vue] ajouté s’affichent.](../assets/offsite-retargeting/edit-event.png)

Après avoir ajouté votre événement, vous devez ajouter un attribut . Puisque vous travaillez avec des visiteurs non authentifiés, vous pouvez ajouter l’attribut calculé que vous venez de créer. Cet attribut calculé nouvellement créé vous permet de lier des identifiants de partenaire à une audience.

Pour ajouter l’attribut calculé, sous **[!UICONTROL Attributs]**, sélectionnez **[!UICONTROL XDM Individual Profile]**, suivi de **[l’identifiant du client de votre organisation](../../xdm/api/getting-started.md#know-your-tenant-id).**, **[!UICONTROL SystemComputedAttributes]** et **[!UICONTROL PartnerID]**. Maintenant, ajoutez la **[!UICONTROL valeur]** de l’attribut calculé à la section des attributs du canevas.

![Le cheminement de dossier pour accéder à l’attribut calculé s’affiche.](../assets/offsite-retargeting/access-computed-attribute.png)

De plus, recherchez **[!UICONTROL Personal Email]** et ajoutez l’attribut **[!UICONTROL Address]** sous **[!UICONTROL PartnerID]** à la section des attributs du canevas.

![L’attribut calculé [!UICONTROL PartnerID] et l’attribut [!UICONTROL Personal Email Address] sont mis en surbrillance sur le canevas du créateur de segments.](../assets/offsite-retargeting/added-attributes.png)

Maintenant que vous avez ajouté vos attributs, vous devez définir leurs critères d’évaluation. Pour **[!UICONTROL PartnerID]**, définissez le critère sur **[!UICONTROL exists]**, et pour **[!UICONTROL Address]**, définissez le critère sur **[!UICONTROL n’existe pas]**.

![Les valeurs appropriées des attributs sont mises en surbrillance.](../assets/offsite-retargeting/set-attribute-values.png)

Vous avez maintenant créé avec succès une audience qui recherche les visiteurs de haute intensité qui ont un identifiant fourni par un partenaire, mais qui ne se sont pas encore inscrits pour votre site. Nommez votre audience &quot;Reciblage Unauthenticated Users&quot; et sélectionnez **[!UICONTROL Enregistrer]** pour terminer la création de votre audience.

![Les propriétés de l’audience sont mises en surbrillance.](../assets/offsite-retargeting/save-audience-properties.png)

## Activer votre audience {#activate-audience}

Une fois votre audience créée, vous pouvez désormais l’activer vers les destinations en aval. Sélectionnez **[!UICONTROL Audiences]** sur le rail de navigation de gauche, recherchez l’audience que vous venez de créer, sélectionnez l’icône représentant des points de suspension, puis sélectionnez **[!UICONTROL Activer à la destination]**.

![ Le bouton [!UICONTROL Activer à la destination] est mis en surbrillance.](../assets/offsite-retargeting/activate-to-destination.png)

>[!NOTE]
>
>Tous les types de destinations, y compris les destinations basées sur des fichiers, prennent en charge l’activation de l’audience avec les identifiants de partenaire.
>
>Pour plus d’informations sur l’activation des audiences vers une destination, consultez la [présentation de l’activation](../../destinations/ui/activation-overview.md).

La page **[!UICONTROL Activer la destination]** s’affiche. Sur cette page, vous pouvez sélectionner la destination vers laquelle vous souhaitez activer votre destination. Après avoir sélectionné la destination de votre choix, sélectionnez **[!UICONTROL Suivant]**.

![La destination vers laquelle vous souhaitez activer l’audience est mise en surbrillance.](../assets/offsite-retargeting/select-destination.png)

La page **[!UICONTROL Planification]** s’affiche. Sur cette page, vous pouvez créer un planning qui détermine la fréquence d’activation de l’audience. Sélectionnez **[!UICONTROL Créer une planification]** pour créer une planification pour l’activation de l’audience.

![ Le bouton [!UICONTROL Créer un planning] est mis en surbrillance.](../assets/offsite-retargeting/select-create-schedule.png)

La fenêtre contextuelle [!UICONTROL Planification] s’affiche. Sur cette page, vous pouvez créer le planning de l’activation de votre audience. Après avoir configuré la planification, sélectionnez **[!UICONTROL Créer]** pour continuer.

![ La fenêtre contextuelle de configuration du planning s&#39;affiche.](../assets/offsite-retargeting/configure-schedule.png)

Après avoir confirmé les détails de la planification, sélectionnez **[!UICONTROL Suivant]**.

![Les détails du planning sont affichés.](../assets/offsite-retargeting/created-schedule.png)

La page **[!UICONTROL Select attributes]** s’affiche. Sur cette page, vous pouvez sélectionner les attributs à exporter avec l’audience activée. Vous souhaitez inclure au minimum l’ID de partenaire, car cela vous permet d’identifier les visiteurs que vous prévoyez de recibler. Sélectionnez **[!UICONTROL Ajouter un nouveau mapping]** et recherchez l’attribut calculé. Après avoir ajouté les attributs nécessaires, sélectionnez **[!UICONTROL Suivant]**.

![Le bouton [!UICONTROL Ajouter un nouveau mapping] et l&#39;attribut calculé sont mis en surbrillance.](../assets/offsite-retargeting/add-new-mapping.png)

La page **[!UICONTROL Review]** s’affiche. Sur cette page, vous pouvez consulter les détails de l’activation de votre audience. Si vous êtes satisfait des détails fournis, sélectionnez **[!UICONTROL Terminer]**.

![La page [!UICONTROL Révision] s’affiche, indiquant les détails de l’activation de l’audience.](../assets/offsite-retargeting/review-destination-activation.png)

Vous avez maintenant activé une audience d’utilisateurs non authentifiés vers une destination en aval pour un reciblage supplémentaire.

## Autres cas d’utilisation {#other-use-cases}

Vous pouvez explorer d’autres cas d’utilisation activés grâce à la prise en charge des données des partenaires dans Real-Time CDP :

- [Interagir et acquérir de nouveaux clients](./prospecting.md) à l’aide de données de partenaire.
- [Personnalisez des expériences sur site](./offsite-retargeting.md) avec la reconnaissance de visiteurs assistée par un partenaire.
- [Compléter les profils propriétaires](./supplement-first-party-profiles.md) avec les attributs fournis par le partenaire.
