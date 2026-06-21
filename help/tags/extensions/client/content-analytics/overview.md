---
title: Présentation de l’extension Adobe Content Analytics
description: Découvrez l’extension de balise Adobe Content Analytics dans Adobe Experience Platform.
exl-id: fcc46c86-e765-4bc7-bfdf-b8b10e8afacc
TQID: https://experienceleague.adobe.com/eLhCUjeJrOFPTS7rWLqRPPYUFYTgYvj-nGlpUusHuOA
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: e98b7246-966c-4318-9e95-cad2f7a17dc7
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 561
ht-degree: 0%

---

# Présentation de l’extension Adobe Content Analytics

L’extension de balise [!DNL Adobe Content Analytics] permet le suivi des événements liés au contenu sur un site web. L’extension envoie des données de contenu (expériences et ressources) à un flux de données dans Adobe Experience Cloud à partir de propriétés web via Experience Platform Edge Network.

L’extension vous permet de diffuser des données d’événement spécifiques liées au contenu dans Experience Platform afin que vous puissiez utiliser ces données dans vos rapports d’analyse de contenu dans Customer Journey Analytics.

Ce document explique comment configurer l’extension de balise dans l’interface utilisateur des balises.

## Installation de l’extension de balise Adobe Content Analytics {#install}

L’extension de balise Adobe Content Analytics est automatiquement installée dans le cadre de la propriété de balise automatiquement créée lors de l’utilisation de l’assistant de configuration guidé [Content Analytics](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/content-analytics/configuration/guided).

<!--
### Manual installation

In case of a manual configuration, the Adobe Content Analytics tag extension needs a property to be installed on. If you have not done so already, see the documentation on [creating a tag property](https://experienceleague.adobe.com/fr/docs/platform-learn/implement-in-websites/configure-tags/create-a-property).

After you have created a property or when you select the property created using the [Content Analytics guided configuration wizard](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/content-analytics/configuration/guided), open the property and select the **[!UICONTROL Extensions]** tab on the left side bar.

Select the **[!UICONTROL Catalog]** tab. From the list of available extensions, find the **[!DNL Adobe Content Analytics]** extension and select **[!UICONTROL Install]**.

![Image showing the Tags UI with the Web SDK extension selected](assets/aca-tag-install.png)

After selecting **[!UICONTROL Install]**, you must configure the Adobe Content Analytics tag extension and save the configuration.
-->

<!--
## Configure schema

The [Content Analytics guided configuration wizard](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/content-analytics/configuration/guided) automatically populates the proper value for the **[!UICONTROL Tenant Schema Name]**. 

![Image that shows the Schema configuration of the Adobe Content Analytics tag extension in the Tags UI](assets/aca-tag-schema.png)

>[!WARNING]
>
>Do not modify the value for **[!UICONTROL Tenant Schema Name]**.

-->

## Configurer les flux de données

L’assistant de configuration guidée de [&#128279;](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/content-analytics/configuration/guided) sélectionne automatiquement la valeur appropriée pour le **[!UICONTROL Sandbox]** et le **[!UICONTROL Flux de données de production]**. Vous pouvez éventuellement configurer un **[!UICONTROL Flux de données d’évaluation]** et un **[!UICONTROL Flux de données de développement]** supplémentaires.

![Image illustrant la configuration des flux de données de l’extension de balise Adobe Content Analytics dans l’interface utilisateur des balises](assets/aca-tag-datastreams.png)

Vous pouvez remplacer les valeurs automatiques sélectionnées pour **[!UICONTROL Sandbox]** et **[!UICONTROL Flux de données de production]** si vous souhaitez utiliser Content Analytics sur un autre sandbox et avec différents flux de données. Ce faisant, vous pouvez sélectionner un sandbox et des flux de données à partir des menus déroulants disponibles, ou sélectionner **[!UICONTROL Saisir des valeurs]** et saisir un identifiant de flux de données personnalisé pour chaque environnement.

>[!IMPORTANT]
>
>Lorsque vous configurez un autre sandbox et des flux de données, assurez-vous que les éléments suivants sont présents :
>
>* le sandbox sélectionné n’est pas déjà associé à une autre configuration Content Analytics, et
>* le service Experience Platform est configuré pour un flux de données sélectionné avec un jeu de données d’événement d’expérience Content Analytics activé.

Consultez le guide sur [les flux de données](../../../../datastreams/overview.md) pour savoir comment configurer un flux de données.

## Configurer la capture et la définition de l’expérience

Dans la section **[!UICONTROL Capture et définition d’expérience]**, vous pouvez activer l’option **[!UICONTROL Inclure des expériences]** pour inclure des expériences lors de la collecte de données pour Content Analytics.

![Image illustrant la section Capture et définition d’expérience dans l’extension](assets/aca-tag-experiencecapture.png)

1. Activez **[!UICONTROL Inclure des expériences]**.
1. Facultatif. spécifiez les paramètres de rendu du contenu sur votre site web. Les paramètres consistent en zéro ou plusieurs combinaisons d’une **[!UICONTROL Expression régulière du domaine]** et **[!UICONTROL Paramètres de requête]**.
   1. Saisissez une **[!UICONTROL Expression régulière du domaine]** par exemple `^(?!.*\b(store|help|admin)\b)`.
   1. Spécifiez une liste de **[!UICONTROL paramètres de requête]** séparés par des virgules, par exemple `outdoors, patio, kitchen`.
Utilisez ![Fermer](./assets/CrossSize300.svg) pour supprimer des paramètres individuels, ou **[!UICONTROL Effacer tout]** pour supprimer tous les paramètres.
1. Sélectionnez **[!UICONTROL Supprimer]** si vous souhaitez supprimer une combinaison de paramètres d’expression régulière de domaine et de requête.
1. Sélectionnez **[!UICONTROL Ajouter une expression régulière]** si vous souhaitez ajouter une autre combinaison d’une expression régulière et de paramètres de requête.

## Configuration du filtrage des événements

Dans la section **[!UICONTROL Filtrage des événements]** , vous pouvez modifier les expressions régulières pour filtrer **[!UICONTROL URL de page]** et **[!UICONTROL URL d’Assets]** lors de la collecte de données pour Content Analytics. Les expressions régulières que vous avez définies dans l&#39;assistant de configuration guidée de [&#128279;](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/content-analytics/configuration/guided) sont automatiquement renseignées.

![Image montrant les paramètres de filtrage d’événement de l’extension de balise Adobe Content Analytics dans l’interface utilisateur des balises](assets/aca-tag-eventfiltering.png)


### Exemples

* Vous souhaitez exclure toutes les pages de documentation de Content Analytics.<br/>Utilisez l’expression régulière suivante : `^(?!.*documentation).*`
* Vous souhaitez exclure toutes les images JPEG de logo de Content Analytics.<br/>Utilisez l’expression régulière suivante : `^(?!.*(logo\.jpg|)).*$`

Vous pouvez utiliser **[!UICONTROL Tester l’expression régulière]** pour tester votre expression régulière dans le **[!UICONTROL Testeur d’expression régulière]**.

![Image montrant le testeur d’expression régulière de l’extension de balise Adobe Content Analytics dans l’interface utilisateur des balises](assets/aca-tag-regextester.png)

