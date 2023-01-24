---
title: Notes de mise à jour de Adobe Experience Platform, janvier 2023
description: Notes de mise à jour de janvier 2023 pour Adobe Experience Platform.
source-git-commit: 3fd3e96d5db6b1e63df338efe383d209690eb1f6
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 43%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 25 janvier 2023**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Collecte de données](#data-collection)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Sources](#sources)

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouvel écran d’accueil | La page d’accueil de l’interface utilisateur de collecte de données a été mise à jour afin d’inclure des informations d’intégration et des liens utiles pour rationaliser la productivité. Cela inclut :<ol><li>Documentation et workflows recommandés pour commencer</li><li>Propriétés, règles et éléments de données récents</li><li>Extensions populaires</li><li>Nouvelles mises à jour d’extension avec une fonction d’installation rapide</li></ol> |
| Envoi de données à [!DNL Google Ads] utilisation du transfert d’événement | Vous pouvez désormais utiliser la variable [[!DNL Google Ads Enhanced Conversions] Extension d’API](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) pour le transfert d’événement, combiné avec [Google Oauth 2 secrets](../../tags/ui/event-forwarding/secrets.md#google-oauth2), pour envoyer en toute sécurité des données côté serveur à [!DNL Google Ads] en temps réel. |

{style=&quot;table-layout:auto&quot;}

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Désactivation des valeurs suggérées pour les champs de chaîne | Vous pouvez désormais [désactiver les valeurs suggérées individuelles pour les champs de chaîne](../../xdm/ui/fields/enum.md) dans le [!UICONTROL Schémas] workspace, y compris ceux des composants standard. Cette fonctionnalité est disponible uniquement pour les champs avec des valeurs suggérées et n’est pas prise en charge pour les contraintes d’énumération. |

**Nouveaux composants XDM**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Classe | [[!UICONTROL Conversion]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | Classe permettant d’effectuer le suivi des données de conversion telles que les conversions de devise. |
| Groupe de champs | [[!UICONTROL Détails sur le taux de conversion de devise]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | Un groupe de champs pour la variable [!UICONTROL Conversion] , capturant des détails supplémentaires liés à la conversion de devise. |
| Groupe de champs | [[!UICONTROL Mappage des résultats d’évaluation des stratégies de consentement avec les métadonnées]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.jsonn) | Capture les détails du résultat de l’évaluation de plusieurs stratégies de consentement, y compris les informations de métadonnées sur les entrées de stratégie de consentement et qui existent. |

**Composants XDM mis à jour**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Type de données | [[!UICONTROL Informations détaillées sur la publicité]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | Le `ID` a été renommé `name`, et le précédent `name` est maintenant `friendlyName`. |
| Type de données | [[!UICONTROL Détails de la proposition de décision]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | Ajout d’une `selectionStrategy` qui capture les détails d’une stratégie de sélection. |
| Groupe de champs | [[!UICONTROL Événement d’expérience - Interactions de propositions]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | Le groupe de champs est désormais compatible avec la variable [!UICONTROL Événement d’étape de parcours] classe . |
| Type de données | [[!UICONTROL Informations détaillés sur les erreurs]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | Le `ID` a été renommé `name`. |
| Type de données | [[!UICONTROL Informations sur les médias]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | Annulation d’une modification du modèle de la propriété de segment vidéo. |
| Type de données | [[!UICONTROL Informations détaillées sur les données de la QoE]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Suppression de la fonction `droppedFrameCount` champ . |
| Type de données | [[!UICONTROL Informations détaillées sur la session]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Renommé `isAuthorized` champ à `authorized`, et mise à jour de ses `type` à une chaîne lorsqu’il s’agissait auparavant d’une valeur booléenne. |
| Type de données | [[!UICONTROL Expédition]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Ajout de plusieurs nouveaux champs : `shipDate`, `trackingNumber`, et `trackingURL`. |
| Groupe de champs | [[!UICONTROL Champs d’entité AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | Ajout de plusieurs nouveaux champs : `journeyNodeID`, `journeyNodeName`, et `journeyModeType`. |
| Groupe de champs | [[!UICONTROL Événement d’expérience client]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | Le groupe de champs est désormais également compatible avec la variable [!UICONTROL Mesures récapitulatives] classe . |
| Groupe de champs | [[!UICONTROL Déclencheurs de produits]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | Le `productTriggers` est maintenant imbriqué sous un `weather` . |
| Groupe de champs | [[!UICONTROL Déclencheurs relatifs]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | Le `relativeTriggers` est maintenant imbriqué sous un `weather` . |
| Groupe de champs | [[!UICONTROL Déclencheurs Conditions extrêmes]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | Le `severeTriggers` est maintenant imbriqué sous un `weather` . |
| Groupe de champs | [[!UICONTROL Déclencheurs météo]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | Le `weatherTriggers` est maintenant imbriqué sous un `weather` . |
| Groupe de champs | [[!UICONTROL Comptes professionnels associés XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | Le groupe de champs est maintenant stable. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur XDM dans Platform, consultez la [présentation du système XDM](../../xdm/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes et vous permet de structurer, d’étiqueter et d’améliorer ces données à l’aide des services Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| --- | --- |
| Autoriser l’accès des utilisateurs aux sous-dossiers des sources de stockage dans le cloud | Vous pouvez désormais définir l’accès à un sous-dossier spécifique de votre source de stockage dans le cloud lors de la création d’un compte. Une fois créés, les utilisateurs ne pourront accéder qu’aux données du sous-dossier autorisé. Cette fonctionnalité est disponible pour les sources de stockage dans le cloud suivantes : [Stockage Azure Blob](../../sources/connectors/cloud-storage/blob.md), [Stockage dans le cloud Google](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md), et [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Disponibilité bêta de [!DNL SugarCRM] | [!DNL SugarCRM] Les sources sont désormais disponibles en version bêta. Utilisez la variable [!DNL SugarCRM Accounts & Contacts] et le [!DNL SugarCRM Events] sources pour importer des données à partir de vos [!DNL SugarCRM] compte à Experience Platform. Pour plus d’informations, reportez-vous à la section [[!DNL SugarCRM] aperçu](../../sources/connectors/crm/sugarcrm.md). |
