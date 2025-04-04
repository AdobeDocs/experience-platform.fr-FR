---
title: Vue d’ensemble de Braze Current Source
description: Découvrez comment diffuser des données de Braze Currents vers Experience Platform.
badge: Beta
exl-id: dd304e10-26e5-4586-ab39-8fe3294b19c9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 12%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>La source [!DNL Braze Currents] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données à partir d’applications de diffusion en continu. La prise en charge des fournisseurs de streaming inclut [!DNL Braze Currents].

[!DNL Braze] alimente en temps réel les interactions axées sur les clients entre les consommateurs et les marques. [!DNL Braze Currents] est un flux de données en temps réel d’événements d’engagement de la plateforme Braze qui est l’exportation la plus robuste, mais granulaire, de la plateforme [!DNL Braze].

## Conditions préalables

Pour suivre les étapes de ce guide, vous devez :

* Une connexion à [Adobe Experience Platform](https://platform.adobe.com) et l’autorisation de créer une connexion source en continu.
* Une connexion à votre [[!DNL Braze] tableau de bord](https://dashboard.braze.com/sign_in), une [licence actuelle du connecteur](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents) inutilisée et des autorisations pour créer un connecteur. Pour plus d’informations, consultez la [configuration requise [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

### Collecter les informations d’identification requises

Pour envoyer correctement vos données [!DNL Braze Currents] à Experience Platform, vous devez saisir les informations d’identification Experience Platform suivantes dans le tableau de bord de l’interface utilisateur [!DNL Braze].

| Champ | Description |
| --- | --- |
| Identifiant client | Identifiant client associé à votre source Experience Platform. |
| Secret client | Secret client associé à votre source Experience Platform. |
| ID du client | Identifiant client associé à votre source Experience Platform. |
| Nom du sandbox | Sandbox associé à votre source Experience Platform. |
| ID du flux de données | Identifiant du flux de données associé à votre source Experience Platform. |
| Point de terminaison de diffusion en continu | Point d’entrée de diffusion en continu associé à votre source Experience Platform. **Remarque** : [!DNL Braze] le convertit automatiquement en point d’entrée de diffusion en continu par lots. |

Pour plus d’informations sur la manière de récupérer ces valeurs, consultez le guide sur [la prise en main des API d’Experience Platform](../../../landing/api-authentication.md). Pour plus d’informations sur l’utilisation du tableau de bord [!DNL Braze], consultez le guide [!DNL Braze] sur la [Accès aux courants](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

## Étapes suivantes

En lisant ce document, vous avez terminé la configuration requise pour diffuser des données de votre compte [!DNL Braze Currents] vers Experience Platform. Vous pouvez maintenant passer au guide sur la [connexion [!DNL Braze Currents] à Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/marketing-automation/braze.md).
