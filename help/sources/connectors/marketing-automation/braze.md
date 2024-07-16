---
title: Présentation du module Braze Current Source
description: Découvrez comment diffuser des données de Braze Currents vers Experience Platform.
badge: Version bêta
exl-id: dd304e10-26e5-4586-ab39-8fe3294b19c9
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 19%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>La source [!DNL Braze Currents] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données à partir d’applications de diffusion en continu. [!DNL Braze Currents] est compatible avec les fournisseurs de diffusion en continu.

[!DNL Braze] alimente en temps réel les interactions centrées sur les clients entre les consommateurs et les marques. [!DNL Braze Currents] est un flux de données en temps réel d’événements d’engagement de la plateforme Braze, qui est l’exportation la plus robuste mais la plus granulaire de la plateforme [!DNL Braze].

## Conditions préalables

Pour suivre les étapes de ce guide, vous aurez besoin des éléments suivants :

* Connexion à [Adobe Experience Platform](https://platform.adobe.com) et autorisation de créer une connexion source en continu.
* Connectez-vous à votre [[!DNL Braze] tableau de bord](https://dashboard.braze.com/sign_in), une [licence Currents Connector](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents) inutilisée et des autorisations pour créer un connecteur. Pour plus d’informations, consultez les [exigences de configuration [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

### Collecter les informations d’identification requises

Pour envoyer correctement vos données [!DNL Braze Currents] à l’Experience Platform, vous devez saisir les informations d’identification d’Experience Platform suivantes dans le tableau de bord de l’interface utilisateur [!DNL Braze].

| Champ | Description |
| --- | --- |
| Identifiant client | ID client associé à la source de votre Experience Platform. |
| Secret client | Le secret client associé à la source de votre Experience Platform. |
| Identifiant du client | Identifiant du tenant associé à la source de votre Experience Platform. |
| Nom du sandbox | Environnement de test associé à la source de votre Experience Platform. |
| ID du flux de données | Identifiant de flux de données associé à la source de votre Experience Platform. |
| Point de terminaison de diffusion en continu | Point de terminaison de diffusion en continu associé à votre source Experience Platform. **Remarque** : [!DNL Braze] la convertit automatiquement en point de terminaison de la diffusion par lots. |

Pour plus d’informations sur la manière de récupérer ces valeurs, consultez le guide de [prise en main des API Platform](../../../landing/api-authentication.md). Pour plus d’informations sur l’utilisation du tableau de bord [!DNL Braze], consultez le guide [!DNL Braze] sur la façon de [ accéder aux courants](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

## Étapes suivantes

En lisant ce document, vous avez terminé la configuration préalable nécessaire pour diffuser les données de votre compte [!DNL Braze Currents] vers Experience Platform. Vous pouvez maintenant passer au guide sur la [connexion [!DNL Braze Currents] à l’Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/marketing-automation/braze.md).
