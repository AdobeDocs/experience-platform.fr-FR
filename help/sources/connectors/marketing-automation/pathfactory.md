---
title: Présentation de la source PathFactory
description: Découvrez comment connecter PathFactory à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.
last-substantial-update: 2024-04-30T00:00:00Z
hide: true
hidefromtoc: true
badge: Version Beta
source-git-commit: 18f6c253aec6815cf84272cbce340a9aa7ed8ab9
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 16%

---

# [!DNL PathFactory]

>[!NOTE]
>
>La source [!DNL PathFactory] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

[[!DNL PathFactory]](https://www.pathfactory.com/) offre une plateforme cloud qui aide les entreprises à gérer les parcours de contenu et à stimuler l’engagement par le biais d’insights sur le contenu intelligent. Ce guide explique comment intégrer des données de PathFactory dans Experience Platform à l’aide des connecteurs de PathFactory pour une ingestion optimale des données.

Vous pouvez ingérer des données à partir de [[!DNL PathFactory]](https://www.pathfactory.com/) l’utilisation de trois sources principales :

* **[!DNL Visitors]**: ingérez des données client et contact en tant qu’enregistrements pour mieux comprendre votre audience.
* **[!DNL Sessions]**: événements de série temporelle qui effectuent le suivi des activités de session utilisateur individuelles sur votre plateforme.
* **[!DNL Page Views]**: événements de série temporelle qui fournissent des informations sur les pages consultées, ce qui vous permet d’analyser les performances du contenu.

Pour plus d’informations sur la configuration de votre [!DNL PathFactory] compte source.

## Liste autorisée d’adresses IP {#ip-allow-list}

Il peut être nécessaire d’ajouter une liste d’adresses IP à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Conditions préalables {#prerequisites}

Avant de commencer l’intégration [[!DNL PathFactory]](https://www.pathfactory.com/) connecteurs avec Experience Platform, assurez-vous de respecter les conditions préalables suivantes :

* **A [Compte PathFactory]**.
   * Contact [[!DNL PathFactory]](https://www.pathfactory.com/portal/company/contactus.shtml) si vous ne disposez pas déjà d’un compte valide.
* **Un abonnement actif** à tout [!DNL PathFactory] produit.
* **Nom d’utilisateur, mot de passe et domaine**.
   * Ces informations d’identification sont requises pour accéder à vos [!DNL PathFactory] et ses données.
* **Jeton d’accès** et **Points de terminaison API**.
   * Ces informations sont nécessaires pour la connexion à [!DNL PathFactory] API.

### Comment obtenir des informations d’identification et des jetons d’accès {#gather-credentials}

Pour se connecter [!DNL PathFactory] pour Experience Platform, vous devez fournir les informations d’identification suivantes :

| Informations d’identification | Description | Point d’entrée |
| --- | --- | --- |
| Nom d’utilisateur | Votre [!DNL PathFactory] nom d’utilisateur du compte. | Non applicable |
| Mot de passe | Votre [!DNL PathFactory] mot de passe du compte. | Non applicable |
| Domaine | Le domaine associé à votre [!DNL PathFactory] compte . | Non applicable |
| Jeton d’accès | Jeton unique utilisé pour l’authentification API. | Non applicable |
| Point de terminaison Visiteurs | Point d’entrée de l’API pour les données du visiteur. | `/api/public/v3/data_lake_apis/visitors.json` |
| Point de terminaison des sessions | Point de terminaison de l’API pour les données de session. | `/api/public/v3/data_lake_apis/sessions.json` |
| Point de terminaison des pages vues | Point de terminaison de l’API pour les données de pages vues. | `/api/public/v3/data_lake_apis/page_views.json` |

Pour obtenir des instructions détaillées sur la manière d’obtenir votre nom d’utilisateur, votre mot de passe, votre domaine et votre jeton d’accès, consultez la page [[!DNL PathFactory] Centre d’assistance](https://support.pathfactory.com/categories/adobe/). Cette ressource fournit des guides complets sur la récupération et la gestion de vos informations d’identification.

### Configuration des autorisations sur Experience Platform

Vous devez disposer des deux **[!UICONTROL Afficher les sources]** et **[!UICONTROL Gérer les sources]** autorisations activées pour votre compte afin de connecter [!DNL PathFactory] compte à Experience Platform. Contactez votre administrateur de produit pour obtenir les autorisations nécessaires. Pour plus d’informations, consultez la section [guide de l’interface utilisateur du contrôle d’accès](../../../access-control/ui/overview.md).

## Connecter [!DNL PathFactory] à Platform {#pathfactory-connect}

La documentation ci-dessous fournit des informations sur la connexion de [!DNL PathFactory] à Platform à l’aide d’API ou de l’interface utilisateur :

* [Créer une connexion source et un flux de données à importer [!DNL PathFactory] données vers Platform à l’aide d’API](../../tutorials/api/create/marketing-automation/pathfactory.md).
* [Connectez-vous à [!DNL PathFactory] compte à Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/marketing-automation/pathfactory.md).
* [Créer un flux de données pour une connexion source à l’aide de l’interface utilisateur](../../tutorials/ui/dataflow/marketing-automation.md).
