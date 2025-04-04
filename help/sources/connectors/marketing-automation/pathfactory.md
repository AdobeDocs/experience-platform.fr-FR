---
title: Présentation du Source PathFactory
description: Découvrez comment connecter PathFactory à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
last-substantial-update: 2024-04-30T00:00:00Z
badge: Beta
exl-id: befb73c4-fd6a-4512-9124-d23a1c27e0e0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 12%

---

# [!DNL PathFactory]

>[!NOTE]
>
>La source [!DNL PathFactory] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

[[!DNL PathFactory]](https://www.pathfactory.com/) propose une plateforme cloud qui aide les entreprises à gérer des parcours de contenu et à stimuler l’engagement grâce à des informations de contenu intelligentes. Ce guide explique comment intégrer des données de PathFactory dans Experience Platform, à l’aide des connecteurs de PathFactory pour une ingestion de données optimale.

Vous pouvez ingérer des données à partir de [[!DNL PathFactory]](https://www.pathfactory.com/) à l’aide de trois sources principales :

* **[!DNL Visitors]** : ingérez les données de client et de contact sous forme d’enregistrements pour mieux comprendre votre audience.
* **[!DNL Sessions]** : événements de série temporelle qui effectuent le suivi des activités de session des utilisateurs individuels sur votre plateforme.
* **[!DNL Page Views]** : événements de série temporelle qui fournissent des informations sur les pages consultées et vous aident à analyser les performances du contenu.

Lisez le document ci-dessous pour plus d’informations sur la configuration de votre compte source [!DNL PathFactory].

## Liste autorisée d’adresses IP {#ip-allow-list}

Il peut être nécessaire d’ajouter une liste d’adresses IP à une liste autorisée de données avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Conditions préalables {#prerequisites}

Avant de commencer l’intégration des connecteurs [[!DNL PathFactory]](https://www.pathfactory.com/) à Experience Platform, veillez à respecter les conditions préalables suivantes :

* **Compte [PathFactory]**.
   * Contactez [[!DNL PathFactory]](https://www.pathfactory.com/portal/company/contactus.shtml) si vous ne disposez pas déjà d’un compte valide.
* **Un abonnement actif** à n’importe quel produit [!DNL PathFactory].
* **Nom d’utilisateur, mot de passe et domaine**.
   * Ces informations d’identification sont requises pour accéder à votre compte [!DNL PathFactory] et à ses données.
* **Jeton d’accès** et **points d’entrée API**.
   * Ils sont nécessaires pour se connecter aux API [!DNL PathFactory].

### Obtention d’informations d’identification et de jetons d’accès {#gather-credentials}

Pour connecter [!DNL PathFactory] à Experience Platform, vous devez fournir les informations d’identification suivantes :

| Informations d’identification | Description | Point d’entrée |
| --- | --- | --- |
| Nom d’utilisateur | Nom d’utilisateur de votre compte [!DNL PathFactory]. | Non applicable |
| Mot de passe | Mot de passe de votre compte [!DNL PathFactory]. | Non applicable |
| Domaine | Domaine associé à votre compte [!DNL PathFactory]. | Non applicable |
| Jeton d’accès | Jeton unique utilisé pour l’authentification API. | Non applicable |
| Point d’entrée des visiteurs | Point d’entrée de l’API pour les données du visiteur. | `/api/public/v3/data_lake_apis/visitors.json` |
| Point d’entrée Sessions | Point d’entrée de l’API pour les données de session. | `/api/public/v3/data_lake_apis/sessions.json` |
| Point d’entrée Pages vues | Point d’entrée de l’API pour les données de pages vues. | `/api/public/v3/data_lake_apis/page_views.json` |

Pour obtenir des instructions détaillées sur la manière d’obtenir votre nom d’utilisateur, mot de passe, domaine et jeton d’accès, consultez le [[!DNL PathFactory] Centre d’assistance](https://support.pathfactory.com/categories/adobe/). Cette ressource fournit des guides complets sur la récupération et la gestion de vos informations d’identification.

### Configuration des autorisations sur Experience Platform

Pour connecter votre compte [!DNL PathFactory] à Experience Platform ]**les autorisations**[!UICONTROL  Afficher les sources et **[!UICONTROL Gérer les sources]** doivent être activées. Contactez votre administrateur de produit pour obtenir les autorisations nécessaires. Pour plus d’informations, consultez le [guide de l’interface utilisateur du contrôle d’accès](../../../access-control/ui/overview.md).

## Connexion de [!DNL PathFactory] à Experience Platform {#pathfactory-connect}

La documentation ci-dessous fournit des informations sur la connexion de [!DNL PathFactory] à Experience Platform à l’aide d’API ou de l’interface utilisateur :

* [Créez une connexion source et un flux de données pour importer  [!DNL PathFactory]  données dans Experience Platform à l’aide d’API](../../tutorials/api/create/marketing-automation/pathfactory.md).
* [Connectez votre compte  [!DNL PathFactory]  Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/marketing-automation/pathfactory.md).
* [Créez un flux de données pour une connexion source à l’aide de l’interface utilisateur](../../tutorials/ui/dataflow/marketing-automation.md).
