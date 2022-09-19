---
keywords: Experience Platform;Zendesk;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK;zendesk;Zendesk
title: Création d’une connexion source Zendesk dans l’interface utilisateur
description: Découvrez comment créer une connexion source Zendesk à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 75d303b0-2dcd-4202-987c-fe3400398d90
source-git-commit: 795c98fb555f79afd7a7035a23a9989cc734a1e1
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 32%

---

# (Version bêta) Créez un [!DNL Zendesk] connexion source dans l’interface utilisateur

>[!NOTE]
>
>Le [!DNL Zendesk] La source est en version bêta. Voir [présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Zendesk] connexion source à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

### Collecter les informations d’identification requises

Pour accéder à [!DNL Zendesk] sur Platform, vous devez fournir des valeurs pour les informations d’identification suivantes :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| Sous-domaine | Domaine unique spécifique à votre compte créé lors du processus d’enregistrement. | `yoursubdomain` |
| Jeton d’accès | Jeton d’API Zendesk. | `0lZnClEvkJSTQ7olGLl7PMhVq99gu26GTbJtf` |

Pour plus d’informations sur l’authentification [!DNL Zendesk] source, voir [[!DNL Zendesk] présentation de la source](../../../../connectors/customer-success/zendesk.md).

![Jeton d’API Zendesk](../../../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

### Création d’un schéma Platform pour [!DNL Zendesk]

Avant de créer un [!DNL Zendesk] connexion source, vous devez également vous assurer de créer au préalable un schéma Platform à utiliser pour votre source. Voir le tutoriel sur [création d’un schéma Platform](../../../../../xdm/schema/composition.md) pour obtenir des instructions complètes sur la création d’un schéma.

Pour plus d’informations sur votre [!DNL Zendesk] schéma requis pour la [!DNL Zendesk Search API], reportez-vous à la section [limites](#limits) ci-dessous.

![Création d’un schéma](../../../../images/tutorials/create/zendesk/schema.png)

## Connecter votre compte [!DNL Zendesk]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , *Succès des clients* catégorie, sélectionnez **[!UICONTROL Zendesk]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/zendesk/catalog.png)

Le **[!UICONTROL Connexion au compte Zendesk]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez la variable *Zendesk* compte avec lequel vous souhaitez créer un nouveau flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/zendesk/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom, une description facultative et vos informations d’identification . Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]**, puis patientez quelques instants le temps que la nouvelle connexion sʼétablisse.

![new](../../../../images/tutorials/create/zendesk/new.png)

### Sélectionner les données

Une fois votre source authentifiée, la page se met à jour dans une arborescence de schémas interactifs qui vous permet d’explorer et d’inspecter la hiérarchie de vos données. Sélectionnez **[!UICONTROL Suivant]** pour continuer.

![select-data](../../../../images/tutorials/create/zendesk/select-data.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez authentifié et créé une connexion source entre vos [!DNL Zendesk] compte et plateforme. Vous pouvez maintenant passer au tutoriel suivant et [créer un flux de données pour importer les données de succès client dans Platform ;](../../dataflow/customer-success.md).

## Ressources supplémentaires

Les sections ci-dessous contiennent des ressources supplémentaires auxquelles vous pouvez vous référer lors de l’utilisation de la variable [!DNL Zendesk] source.

### Validation {#validation}

La section suivante décrit les étapes que vous pouvez suivre pour vérifier que vous avez bien connecté votre [!DNL Zendesk] source et [!DNL Zendesk] les profils sont ingérés dans Platform.

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Jeux de données]** dans le volet de navigation de gauche pour accéder à la fonction [!UICONTROL Jeux de données] workspace. Le [!UICONTROL Activité du jeu de données] affiche les détails des exécutions.

![Page d’activité](../../../../images/tutorials/create/zendesk/dataset-activity.png)

Sélectionnez ensuite l’identifiant d’exécution du flux de données que vous souhaitez afficher pour afficher des détails spécifiques sur cette exécution.

![Page Flux de données](../../../../images/tutorials/create/zendesk/dataflow-monitoring.png)

Enfin, sélectionnez **[!UICONTROL Prévisualisation d’un jeu de données]** pour afficher les données qui ont été ingérées.

![Jeu de données Zendesk](../../../../images/tutorials/create/zendesk/preview-dataset.png)

Vous pouvez également vérifier vos données Platform par rapport aux données de votre [!DNL Zendesk] > [!DNL Customers] page.

![zendesk-customers](../../../../images/tutorials/create/zendesk/zendesk-customers.png)

### Schéma Zendesk

Le tableau ci-dessous répertorie les mappages pris en charge qui doivent être configurés pour Zendesk.

>[!TIP]
>
>Voir [API de recherche Zendesk > Exporter les résultats de recherche](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) pour plus d’informations sur l’API.

| Source | Type |
|---|---|
| `results.active` | Booléen |
| `results.alias` | Chaîne |
| `results.created_at` | Chaîne |
| `results.custom_role_id` | Nombre entier |
| `results.default_group_id` | Nombre entier |
| `results.details` | Chaîne |
| `results.email` | Chaîne |
| `results.external_id` | Entier |
| `results.iana_time_zone` | Chaîne |
| `results.id` | Entier |
| `results.last_login_at` | Chaîne |
| `results.locale` | Chaîne |
| `results.locale_id` | Entier |
| `results.moderator` | Booléen |
| `results.name` | Chaîne |
| `results.notes` | Chaîne |
| `results.only_private_comments` | Booléen |
| `results.organization_id` | Nombre entier |
| `results.phone` | Chaîne |
| `results.photo` | Chaîne |
| `results.report_csv` | Booléen |
| `results.restricted_agent` | Booléen |
| `results.result_type` | Chaîne |
| `results.role` | Chaîne |
| `results.role_type` | Entier |
| `results.shared` | Booléen |
| `results.shared_agent` | Booléen |
| `results.shared_phone_number` | Booléen |
| `results.signature` | Chaîne |
| `results.suspended` | Booléen |
| `results.ticket_restriction` | Chaîne |
| `results.time_zone` | Chaîne |
| `results.two_factor_auth_enabled` | Booléen |
| `results.updated_at` | Chaîne |
| `results.url` | Chaîne |
| `results.verified` | Booléen |

{style=&quot;table-layout:auto&quot;}

### Limites {#limits}

* Le [API de recherche Zendesk > Exporter les résultats de recherche](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) renvoie un maximum de 1 000 enregistrements par page.
   * La valeur de la variable ``filter[type]`` est défini sur ``user`` et par conséquent, la connexion Zendesk renvoie uniquement les utilisateurs.
   * Le nombre de résultats par page est géré par la variable ``page[size]`` . La valeur est définie sur ``100``. Cela permet de réduire l&#39;impact des contraintes de réduction de vitesse définies par Zendesk.
   * Voir [Limites](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#limits) et [Pagination](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#pagination-1).
   * Vous pouvez également consulter [Pagination des listes à l’aide de la pagination du curseur](https://developer.zendesk.com/documentation/developer-tools/pagination/paginating-through-lists-using-cursor-pagination/).
