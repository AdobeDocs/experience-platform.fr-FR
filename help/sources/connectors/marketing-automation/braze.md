---
title: Présentation de la source des courants de braquage
description: Découvrez comment diffuser des données de Braze Currents vers Experience Platform.
badge: Version Beta
source-git-commit: 64975ccb6a44730489427cef745f3dbce5bcedf1
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 18%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>La source [!DNL Braze Currents] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données à partir d’applications de diffusion en continu. La prise en charge des fournisseurs de diffusion en continu inclut [!DNL Braze Currents].

[!DNL Braze] alimente en temps réel les interactions centrées sur les clients entre les consommateurs et les marques. [!DNL Braze Currents] est un flux de données en temps réel d’événements d’engagement de la plateforme Braze, qui constitue l’exportation la plus robuste mais la plus granulaire de la [!DNL Braze] plateforme.

## Conditions préalables

Pour suivre les étapes de ce guide, vous aurez besoin des éléments suivants :

* Une connexion à [Adobe Experience Platform](https://platform.adobe.com) et l’autorisation de créer une nouvelle connexion source en continu.
* Une connexion à [[!DNL Braze] tableau de bord](https://dashboard.braze.com/sign_in), une valeur inutilisée [Licence currents Connector](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)et les autorisations pour créer un connecteur. Pour plus d’informations, consultez la section [conditions requises pour configurer [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

### Collecter les informations d’identification requises

Pour envoyer votre [!DNL Braze Currents] pour les données d’Experience Platform, vous devez saisir les informations d’identification d’Experience Platform suivantes dans la variable [!DNL Braze] Tableau de bord de l’interface utilisateur.

| Champ | Description |
| --- | --- |
| Identifiant client | ID client associé à la source de votre Experience Platform. |
| Secret client | Le secret client associé à la source de votre Experience Platform. |
| Identifiant du client | Identifiant du tenant associé à la source de votre Experience Platform. |
| Nom du sandbox | Environnement de test associé à la source de votre Experience Platform. |
| Identifiant de flux de données | Identifiant de flux de données associé à la source de votre Experience Platform. |
| Point de terminaison de diffusion en continu | Point de terminaison de diffusion en continu associé à votre source Experience Platform. **Remarque**: [!DNL Braze] convertit automatiquement ce paramètre au point de terminaison de la diffusion par lots. |

Pour plus d’informations sur la manière de récupérer ces valeurs, consultez le guide sur [Prise en main des API Platform](../../../landing/api-authentication.md). Pour plus d’informations sur l’utilisation de la variable [!DNL Braze] tableau de bord, lisez la [!DNL Braze] guide sur la manière de procéder [Accéder aux courants](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

## Étapes suivantes

En lisant ce document, vous avez terminé la configuration préalable nécessaire pour diffuser des données à partir de votre [!DNL Braze Currents] compte à Experience Platform. Vous pouvez maintenant passer au guide sur la [connexion [!DNL Braze Currents] Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/marketing-automation/braze.md).