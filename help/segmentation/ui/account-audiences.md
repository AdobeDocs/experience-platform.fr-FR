---
title: Audiences du compte
description: Découvrez comment créer et utiliser des audiences de compte pour cibler des profils de compte dans des destinations en aval.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="Édition B2P" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 047930d6-939f-4418-bbcb-8aafd2cf43ba
source-git-commit: fd0a495d68d6a09ccca66c400993d2e72673321c
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 22%

---

# Audiences de compte

>[!AVAILABILITY]
>
>Les audiences de compte ne sont disponibles que dans [B2B edition of Real-Time Customer Data Platform](../../rtcdp/overview.md#rtcdp-b2b) et l’ [édition B2P de Real-Time Customer Data Platform](../../rtcdp/overview.md#rtcdp-b2p).

Grâce à la segmentation des comptes, Adobe Experience Platform vous permet d’offrir une expérience de segmentation marketing simplifiée et conviviale, allant des audiences basées sur les personnes aux audiences basées sur les comptes.

Les audiences de compte peuvent être utilisées comme entrée pour les destinations basées sur un compte, ce qui vous permet de cibler les personnes contenues dans ces comptes dans les services en aval. Par exemple, vous pouvez utiliser des audiences basées sur un compte pour récupérer les enregistrements de tous les comptes qui n’ont **pas** ayant des informations de contact pour toute personne ayant le titre de chef des opérations (COO) ou chef du marketing (CMO).

## Terminologie {#terminology}

Avant de commencer à utiliser les audiences de compte, veuillez examiner les différences entre les différents types d’audience :

- **Audiences du compte** : une audience de compte est une audience créée à l’aide des données de profil **account**. Les données de profil de compte peuvent être utilisées pour créer des audiences qui ciblent les personnes dans les comptes en aval. Pour plus d’informations sur les profils de compte, consultez la [présentation des profils de compte](../../rtcdp/accounts/account-profile-overview.md).
- **Audiences de personnes** : une audience de personnes est une audience créée à l’aide des données de profil **customer**. Les données de profil client peuvent être utilisées pour créer des audiences qui ciblent la clientèle de votre entreprise. Pour plus d’informations sur les profils client, consultez la [présentation de Real-Time Customer Profile](../../profile/home.md).
- **Audiences de prospects** : une audience de prospects est une audience qui est créée à l’aide des données de profil **prospect**. Les données de profil de prospects peuvent être utilisées pour créer des audiences à partir d’utilisateurs non authentifiés. Pour plus d’informations sur les profils de prospects, consultez la [présentation des profils de prospects](../../profile/ui/prospect-profile.md).

## Accès {#access}

Pour accéder aux audiences du compte, sélectionnez **[!UICONTROL Audiences]** dans la section **[!UICONTROL Comptes]** .

![Le bouton Audiences est mis en surbrillance dans la section Comptes.](../images/ui/account-audiences/select.png)

La page [!UICONTROL Parcourir] s’affiche, affichant la liste de toutes les audiences de compte pour l’organisation.

![Les audiences du compte appartenant à l&#39;organisation sont affichées.](../images/ui/account-audiences/browse.png)

Cette vue répertorie des informations sur l’audience, notamment le nom, le nombre de profils, l’origine, l’état du cycle de vie, la date de création et la date de dernière mise à jour.

Vous pouvez également utiliser la fonctionnalité de recherche et de filtrage pour rechercher et trier rapidement des audiences de compte spécifiques. Vous trouverez plus d’informations sur cette fonctionnalité dans la [présentation d’Audience Portal](./audience-portal.md#manage-audiences).

## Créer une audience {#create}

>[!NOTE]
>
>Les audiences de compte sont évaluées à l’aide de la segmentation **batch** et seront évaluées toutes les 24 heures.

Pour créer une audience de compte, sélectionnez **[!UICONTROL Créer une audience]** sur la page [!UICONTROL Parcourir].

![Le bouton [!UICONTROL Créer une audience] est mis en surbrillance sur la page de navigation de l&#39;audience du compte.](../images/ui/account-audiences/select-create-audience.png)

Le créateur de segments s’affiche. Les attributs de compte et les audiences s’affichent dans la barre de navigation de gauche. Sous l’onglet [!UICONTROL Attributs], vous pouvez ajouter des attributs personnalisés et créés par Platform.

![Le créateur de segments s’affiche. Notez que seuls les attributs et les audiences sont affichés.](../images/ui/account-audiences/segment-builder.png)

Lors de la création d’audiences de compte, notez que les événements sont répertoriés sous **[!UICONTROL Personnes]**, plutôt que d’être leur propre onglet, car ces attributs sont associés à des personnes.

![L&#39;emplacement de recherche d&#39;événements, qui se trouve dans le dossier [!UICONTROL People], est mis en surbrillance.](../images/ui/account-audiences/attributes.png)

Sous l’onglet [!UICONTROL Audiences] , vous pouvez ajouter des audiences basées sur des personnes créées précédemment à partir desquelles créer une audience de compte lors de la création de votre propre audience.

![L’onglet Audiences du créateur de segments est mis en surbrillance.](../images/ui/account-audiences/audiences.png)

Pour plus d’informations sur l’utilisation du créateur de segments, consultez le [Guide de l’interface utilisateur du créateur de segments](./segment-builder.md).

### Établissement de relations {#relationships}

Par défaut, pour les audiences de compte, l’interface utilisateur du créateur de segments affiche la relation directe entre un compte et une personne. Cependant, d’autres types de relations sont disponibles pour les audiences de compte.

Pour utiliser d’autres types de relations, sélectionnez ![l’icône de paramètres](../../images/icons/settings.png).

![L&#39;icône des paramètres est mise en surbrillance dans la section Champs.](../images/ui/account-audiences/select-settings.png)

Sur l’onglet [!UICONTROL Paramètres], sélectionnez **[!UICONTROL Afficher les sélecteurs de relation]** dans la section **[!UICONTROL Relation des champs]** .

![ Le bouton d’activation/désactivation Afficher les sélecteurs de relation est sélectionné dans la section Relation des champs de l’onglet Paramètres.](../images/ui/account-audiences/show-relation-selectors.png)

Sélectionnez à nouveau ![l’icône de paramètres](../../images/icons/settings.png) pour revenir à l’onglet [!UICONTROL Champs]. Vous pouvez maintenant consulter la section **[!UICONTROL Établissement de relations]** , qui vous permet de déterminer comment le compte est connecté à la personne et comment la personne est connectée à l’opportunité.

![La section Créer des relations est mise en évidence. Elle affiche les options permettant de connecter un compte à une personne et de connecter une personne à une opportunité.](../images/ui/account-audiences/establish-relationships.png)

Lors de la connexion du compte à la personne, vous pouvez choisir parmi les options suivantes :

| Option | Description |
| ------ | ----------- |
| Relation directe | La connexion directe entre le compte et la personne. Cela spécifie les comptes auxquels chaque personne est liée via le tableau de valeurs `accountID` dans le tableau `personComponents` du schéma de personne. Ce chemin est le plus fréquemment utilisé. |
| Relation entre les comptes et les personnes | La relation entre le compte et la personne, définie par l’objet `accountPersonRelation`. Ce chemin permet également à chaque personne d’être connectée à plusieurs comptes. Elle est utilisée lorsque votre organisation a défini un tableau de relation explicite à partir des données source. |
| Relation opportunités-personnes | La relation entre l’opportunité et la personne, définie par l’objet `opportunityPersonRelation`. Cela permet de connecter la personne à un compte en passant de l’opportunité à l’opportunité d’accéder au compte. Vous pouvez ainsi décrire les entreprises auxquelles la personne est associée à des opportunités à l’adresse . |

Lors de la connexion de l&#39;opportunité à la personne, vous pouvez choisir parmi les options suivantes :

| Option | Description |
| ------ | ----------- |
| Compte | La connexion directe entre le compte et l’opportunité. Lorsque vous l’utilisez dans une audience de compte, ce chemin connecte toutes les personnes de l’entreprise à l’opportunité. |
| Relation opportunités-personnes | La relation entre l’opportunité et la personne, qui est basée sur l’objet personne-opportunité. Ce chemin ne connecte que les personnes qui ont été spécifiquement identifiées comme impliquées dans une opportunité à cette opportunité. |

Après avoir établi la relation souhaitée, vous pouvez ajouter les personnes-audiences requises à votre définition de segment.

## Activer l&#39;audience {#activate}

>[!NOTE]
>
>Seul un nombre limité de destinations prennent en charge les audiences du compte. Assurez-vous que la destination que vous souhaitez activer prend en charge les audiences de compte avant de poursuivre ce processus.

Après avoir créé l’audience de votre compte, vous pouvez activer l’audience vers d’autres services en aval.

Sélectionnez l’audience que vous souhaitez activer, suivie de **[!UICONTROL Activer à la destination]**.

![Le bouton [!UICONTROL Activer la destination] est mis en surbrillance dans le menu des actions rapides pour l’audience sélectionnée.](../images/ui/account-audiences/activate.png)

La page [!UICONTROL Activer la destination] s’affiche. Pour plus d’informations sur le processus d’activation, y compris les destinations prises en charge et les détails sur les mappages de champs, consultez le tutoriel [Activer les audiences de compte](/help/destinations/ui/activate-account-audiences.md) .

## Étapes suivantes {#next-steps}

Après avoir lu ce guide, vous comprenez mieux comment créer et utiliser les audiences de votre compte dans Adobe Experience Platform. Pour savoir comment utiliser d’autres types d’audiences dans Platform, consultez le [guide de l’interface utilisateur de Segmentation Service](./overview.md).

## Annexe {#appendix}

La section suivante fournit des informations supplémentaires sur les audiences de compte.

### Validation de la segmentation du compte {#validation}

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_eventLookbackWindow"
>title="Erreur de période de recherche rétroactive maximale"
>abstract="La période de recherche rétroactive maximale pour les événements d’expérience est de 30 jours."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxDepth"
>title="Erreur de profondeur maximale des conteneurs imbriqués"
>abstract="La profondeur maximale des conteneurs imbriqués est de **5**. Cela signifie qu’il est **impossible** d’avoir plus de cinq conteneurs imbriqués lors de la création de votre audience."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxBreadth"
>title="Erreur de quantité maximale de règles"
>abstract="Le nombre maximal de règles dans un seul conteneur est de **5**. Cela signifie qu’il est **impossible** d’avoir plus de cinq règles dans un seul conteneur lors de la création de votre audience."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_crossEntityMaxDepth"
>title="Erreur de nombre maximal d’entités croisées"
>abstract="Le nombre maximal d’entités croisées pouvant être utilisées dans une seule audience est de **5**. « Entité croisée » désigne le fait de changer d’entités au sein de votre audience. Vous pouvez notamment passer d’un compte à une personne et d’une personne à une liste marketing."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowCustomEntity"
>title="Erreur d’entité personnalisée"
>abstract="Les entités personnalisés **ne sont pas** autorisées."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_b2bBuiltInEntities"
>title="Erreur d’entité B2B non valide"
>abstract="Seules les entités B2B suivantes sont autorisées : `_xdm.context.account`, `_xdm.content.opportunity`, `_xdm.context.profile`, `_xdm.context.experienceevent`, `_xdm.context.account-person`, `_xdm.classes.opportunity-person`, `_xdm.classes.marketing-list-member`, `_xdm.classes.marketing-list`, `_xdm.context.campaign-member` et `_xdm.classes.campaign`."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_rhsMaxOptions"
>title="Erreur de nombre maximal de valeurs"
>abstract="Le nombre maximal de valeurs pouvant être cochées pour un champ est de **50**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByReference"
>title="Erreur d’événement inSegment"
>abstract="Les événements inSegment **ne sont pas** autorisés."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByValue"
>title="Erreur d’événement inSegment"
>abstract="Les événements inSegment **ne sont pas** autorisés."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowSequentialEvents"
>title="Erreur d’événement séquentiel"
>abstract="Les événements séquentiels **ne sont pas** autorisés."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowMaps"
>title="Erreur de propriété de type Map"
>abstract="Les propriétés de type Map **ne sont pas** autorisées."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxNestedAggregationDepth"
>title="Erreur de profondeur maximale d’entité imbriquée"
>abstract="La profondeur maximale des tableaux imbriqués est de **5**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxObjectNestingLevel"
>title="Erreur de nombre maximal d’objets imbriqués"
>abstract="Le nombre maximal d’objets imbriqués autorisés est de **10**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_generic"
>title="Violation de contrainte"
>abstract="L’audience enfreint une contrainte. Lisez le document lié pour plus de détails."

Lors de l’utilisation d’audiences de compte, l’audience **doit** respecter les contraintes suivantes :

>[!NOTE]
>
>La liste suivante présente les contraintes **default** pour les audiences de compte. Ces valeurs **peuvent** changer, selon les paramètres implémentés par l’administrateur de votre entreprise.

- La période de recherche arrière maximale pour les événements d’expérience est de **30 jours**.
- La profondeur maximale des conteneurs imbriqués est **5**.
   - Cela signifie qu’il est **impossible** d’avoir plus de cinq conteneurs imbriqués lors de la création de votre audience.
- Le nombre maximal de règles dans un seul conteneur est **5**.
   - Cela signifie que votre audience **ne peut pas** comporter plus de cinq règles qui composent votre audience.
- Le nombre maximal d’entités croisées pouvant être utilisées est **5**.
   - « Entité croisée » désigne le fait de changer d’entités au sein de votre audience. Vous pouvez notamment passer d’un compte à une personne et d’une personne à une liste marketing.
- Les entités personnalisées **ne peuvent pas** être utilisées.
- Le nombre maximal de valeurs pouvant être cochées pour un champ est de **50**.
   - Par exemple, si vous avez un champ &quot;Nom de ville&quot;, vous pouvez comparer cette valeur à 50 noms de ville.
- Les audiences de compte **ne peuvent pas** utiliser les événements `inSegment`.
- Les audiences de compte **ne peuvent pas** utiliser des événements séquentiels.
- Les audiences de compte **ne peuvent pas** utiliser de mappages.
- La profondeur maximale des tableaux imbriqués est de **5**.
- Le nombre maximal d’objets imbriqués est **10**.
