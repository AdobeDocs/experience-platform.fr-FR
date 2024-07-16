---
title: Présentation de PathFactory Source
description: Découvrez comment connecter PathFactory à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.
last-substantial-update: 2024-04-30T00:00:00Z
badge: Version bêta
exl-id: befb73c4-fd6a-4512-9124-d23a1c27e0e0
source-git-commit: ca17854830edabaf2bd74265258d6f0096f2888e
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 16%

---

# [!DNL PathFactory]

>[!NOTE]
>
>La source [!DNL PathFactory] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

[[!DNL PathFactory]](https://www.pathfactory.com/) offre une plate-forme cloud qui aide les entreprises à gérer les parcours de contenu et à stimuler l’engagement par le biais d’informations sur le contenu intelligent. Ce guide explique comment intégrer des données de PathFactory dans Experience Platform à l’aide des connecteurs de PathFactory pour une ingestion optimale des données.

Vous pouvez ingérer des données à partir de [[!DNL PathFactory]](https://www.pathfactory.com/) à l’aide de trois sources principales :

* **[!DNL Visitors]** : ingérez des données client et contact en tant qu’enregistrements pour mieux comprendre votre audience.
* **[!DNL Sessions]** : événements de série temporelle qui effectuent le suivi des activités de session utilisateur individuelles sur votre plateforme.
* **[!DNL Page Views]** : événements de série temporelle qui fournissent des informations sur les pages consultées, ce qui vous permet d’analyser les performances du contenu.

Lisez le document ci-dessous pour plus d’informations sur la configuration de votre compte source [!DNL PathFactory].

## Liste autorisée d’adresses IP {#ip-allow-list}

Il peut être nécessaire d’ajouter une liste d’adresses IP à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Conditions préalables {#prerequisites}

Avant d’intégrer des connecteurs [[!DNL PathFactory]](https://www.pathfactory.com/) à Experience Platform, assurez-vous de respecter les conditions préalables suivantes :

* **Un [compte PathFactory]**.
   * Contactez [[!DNL PathFactory]](https://www.pathfactory.com/portal/company/contactus.shtml) si vous n&#39;avez pas encore de compte valide.
* **Un abonnement actif** à n’importe quel produit [!DNL PathFactory].
* **Nom d’utilisateur, mot de passe et domaine**.
   * Ces informations d’identification sont requises pour accéder à votre compte [!DNL PathFactory] et à ses données.
* **Jeton d’accès** et **Points de terminaison API**.
   * Elles sont nécessaires pour la connexion aux API [!DNL PathFactory].

### Comment obtenir des informations d’identification et des jetons d’accès {#gather-credentials}

Pour connecter [!DNL PathFactory] à Experience Platform, vous devez fournir les informations d’identification suivantes :

| Informations d’identification | Description | Point d’entrée |
| --- | --- | --- |
| Nom d’utilisateur | Votre nom d&#39;utilisateur de compte [!DNL PathFactory]. | Non applicable |
| Mot de passe | Votre mot de passe de compte [!DNL PathFactory]. | Non applicable |
| Domaine | Domaine associé à votre compte [!DNL PathFactory]. | Non applicable |
| Jeton d’accès | Jeton unique utilisé pour l’authentification API. | Non applicable |
| Point de terminaison Visiteurs | Point d’entrée de l’API pour les données du visiteur. | `/api/public/v3/data_lake_apis/visitors.json` |
| Point de terminaison des sessions | Point de terminaison de l’API pour les données de session. | `/api/public/v3/data_lake_apis/sessions.json` |
| Point de terminaison des pages vues | Point de terminaison de l’API pour les données de pages vues. | `/api/public/v3/data_lake_apis/page_views.json` |

Pour obtenir des instructions détaillées sur la manière d’obtenir votre nom d’utilisateur, votre mot de passe, votre domaine et votre jeton d’accès, consultez le [[!DNL PathFactory] centre d’assistance](https://support.pathfactory.com/categories/adobe/). Cette ressource fournit des guides complets sur la récupération et la gestion de vos informations d’identification.

### Configuration des autorisations sur Experience Platform

Les autorisations **[!UICONTROL Afficher les sources]** et **[!UICONTROL Gérer les sources]** doivent être activées pour votre compte pour connecter votre compte [!DNL PathFactory] à un Experience Platform. Contactez votre administrateur de produit pour obtenir les autorisations nécessaires. Pour plus d’informations, consultez le [guide de l’interface utilisateur du contrôle d’accès](../../../access-control/ui/overview.md).

## Connecter [!DNL PathFactory] à Platform {#pathfactory-connect}

La documentation ci-dessous fournit des informations sur la connexion de [!DNL PathFactory] à Platform à l’aide d’API ou de l’interface utilisateur :

* [Créez une connexion source et un flux de données pour importer [!DNL PathFactory] des données vers Platform à l’aide d’API](../../tutorials/api/create/marketing-automation/pathfactory.md).
* [Connectez votre compte  [!DNL PathFactory] à l’Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/marketing-automation/pathfactory.md).
* [Créez un flux de données pour une connexion source à l’aide de l’interface utilisateur ](../../tutorials/ui/dataflow/marketing-automation.md).
