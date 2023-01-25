---
title: Notes de mise à jour d’Adobe Experience Platform
description: Dernières notes de mise à jour pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 5657473ad10880b907a5b010fa99e08a5e45e174
workflow-type: tm+mt
source-wordcount: '1993'
ht-degree: 31%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 25 janvier 2023**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Assurance](#assurance)
- [Collecte de données](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Profil client en temps réel](#profile)
- [Segmentation Service](#segmentation)
- [Sources](#sources)

## Assurance {#assurance}

Adobe Assurance vous permet d’inspecter, de tester, de simuler et de valider la manière dont vous collectez des données ou diffusez des expériences dans votre application mobile.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Éditeur de validation | De nouvelles améliorations ont été apportées à l’éditeur de validation. Ces améliorations incluent des colonnes de validation, de nouveaux outils de création de code et des vues améliorées. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur Assurance, veuillez lire la section [Documentation d’assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouvel écran d’accueil | La page d’accueil de l’interface utilisateur de collecte de données a été mise à jour afin d’inclure des informations d’intégration et des liens utiles pour rationaliser la productivité. Cela inclut :<ol><li>Documentation et workflows recommandés pour commencer</li><li>Propriétés, règles et éléments de données récents</li><li>Extensions populaires</li><li>Nouvelles mises à jour d’extension avec une fonction d’installation rapide</li></ol> |
| Envoi de données à [!DNL Google Ads] utilisation du transfert d’événement | Vous pouvez désormais utiliser la variable [[!DNL Google Ads Enhanced Conversions] Extension d’API](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) pour le transfert d’événement, combiné avec [Google Oauth 2 secrets](../../tags/ui/event-forwarding/secrets.md#google-oauth2), pour envoyer en toute sécurité des données côté serveur à [!DNL Google Ads] en temps réel. |

{style=&quot;table-layout:auto&quot;}

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Nouvelles destinations**

| Destination | Description |
| ----------- | ----------- |
| [(Version bêta) Connexion à Adobe Experience Cloud Audiences](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Utilisez la variable [!UICONTROL (Version bêta) Audiences Adobe Experience Cloud] connexion pour partager des segments d’Experience Platform vers différentes solutions d’Experience Platform, telles qu’Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target ou Marketo. |
| [Connexion à un profil Pega](../../destinations/catalog/personalization/pega-profile.md) | Utilisez la variable [!DNL Pega Profile Connector] dans Adobe Experience Platform pour créer une connexion sortante active à votre [!DNL Amazon] Stockage S3 pour exporter périodiquement des données de profil vers des fichiers CSV à partir de Adobe Experience Platform dans vos propres compartiments S3. Dans [!DNL Pega Customer Decision Hub], vous pouvez planifier des tâches de données pour importer ces données de profil à partir du stockage S3 afin de mettre à jour la variable [!DNL Pega Customer Decision Hub] profile. |
| [(Version bêta) Connexion européenne du bureau de commerce CRM](../../destinations/catalog/advertising/tradedesk-emails.md) | Avec la publication de l’EUID (European Unified ID), deux [!DNL The Trade Desk - CRM] destinations dans [destinations](/help/destinations/catalog/overview.md). <ul><li> Si vous source des données dans l’UE, utilisez la variable **[!DNL The Trade Desk - CRM (EU)]** destination.</li><li> Si vous sources des données dans les régions APAC ou NAMER, utilisez la variable **[!DNL The Trade Desk - CRM (NAMER & APAC)]** destination. </li></ul> |

**Nouvelle fonctionnalité ou mise à jour**

| Fonction | Description |
| ----------- | ----------- |
| Nouvelles options de délimiteur pour les connecteurs de destination de stockage dans le cloud bêta | Trois nouvelles options de délimiteur (deux points) `:`, Pipe `|`, point-virgule `;`) sont désormais disponibles pour les nouvelles destinations de stockage dans le cloud bêta - [(Version bêta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Version bêta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Version bêta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(Version bêta) Zone d’entrée des données](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Version bêta) Stockage dans le cloud Google](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(Version bêta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md). <br> En savoir plus sur la prise en charge [options de formatage de fichier](/help/destinations/ui/batch-destinations-file-formatting-options.md) pour les destinations basées sur des fichiers. |
| Nouveau paramètre facultatif disponible dans [Champs de données client](/help/destinations/destination-sdk/destination-configuration.md#customer-data-fields) configurations dans [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique`: Utilisez-le lorsque vous devez créer un champ de données client dont la valeur doit être unique dans tous les flux de données de destination configurés par l’organisation d’un utilisateur. <br> Par exemple, la variable **[!UICONTROL Alias d’intégration]** dans le champ [[!UICONTROL Personnalisation personnalisée]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) destination doit être unique, ce qui signifie que deux flux de données distincts vers cette destination ne peuvent pas avoir la même valeur pour ce champ. |

**Correctifs et améliorations** {#fixes-and-enhancements}

<!--

| Fix or enhancement | Description |
| ----------- | ----------- |
| UI and API validation for required mappings and duplicate mappings (PLAT-123316) | Validation is now enforced as follows in the UI and API when [mapping fields](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) in the activate destinations workflow:<ul><li>**Required mappings**: If the destination has been set up by the destination developer with required mappings (for example, the [Google Ad Manager 360](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#activate) destination), then these required mappings need to be added by the user when activating data to the destination. </li><li>**Duplicate mappings**: expand on allowed and forbidden source-to-target mappings.</li></ul> |
| Updated profile export behavior to cloud storage destinations (PLAT-123316) | We fixed an issue in the behavior of [mandatory attributes](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) when exporting data files to batch destinations. <br> Previously, every record in the output files was verified to contain both: <ol><li>A non-null value of the `mandatoryField` column and</li><li>also contain a non-null value on at least one of the other non-mandatory fields.</li></ol> The second condition has been removed. As a result, you might be seeing more output rows in your exported data files. |

-->

<table>
    <tr>
        <td><b>Correctif ou amélioration</b></td>
        <td><b>Description</b></td>
    </tr>
    <tr>
        <td>Validation de l’interface utilisateur et de l’API pour les mappages requis et les mappages en double (PLAT-123316)</td>
        <td>La validation est désormais appliquée comme suit dans l’interface utilisateur et l’API lors de la <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mapping">champs de mappage</a> dans le workflow d’activation des destinations :<ul><li><b>Mappings requis</b>: Si la destination a été configurée par le développeur de destination avec les mappages requis (par exemple, la variable <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html?lang=en">Google Ad Manager 360</a> destination), ces mappages requis doivent être ajoutés par l’utilisateur lors de l’activation des données vers la destination. </li><li><b>Duplication des mappages</b>: Dans l'étape de mapping du workflow d'activation, vous pouvez ajouter des valeurs en double dans les champs sources, mais pas dans les champs cibles. Consultez le tableau ci-dessous pour obtenir un exemple de combinaisons de mappage autorisées et interdites. <br><table><thead><tr><th>Autorisé/interdit</th><th>Champ source</th><th>Champ cible</th></tr></thead><tbody><tr><td>Autorisée</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>email alias2</li></ul></td></tr><tr><td>Interdit</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>
    <tr>
        <td>Mise à jour du comportement d’exportation vers des destinations basées sur des fichiers (PLAT-123316)</td>
        <td>Nous avons corrigé un problème dans le comportement de <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mandatory-attributes">attributs obligatoires</a> lors de l’exportation de fichiers de données vers des destinations par lot. <br> Auparavant, chaque enregistrement des fichiers de sortie était vérifié pour contenir les deux : <ol><li>Une valeur non nulle de la variable <code>mandatoryField</code> column et</li><li>Une valeur non nulle sur au moins un des autres champs non obligatoires.</li></ol> La deuxième condition a été supprimée. Par conséquent, il se peut que davantage de lignes de sortie s’affichent dans vos fichiers de données exportés, comme illustré dans l’exemple ci-dessous :<br> <b> Exemple de comportement avant la version de janvier 2023 </b> <br> Champ obligatoire : <code>emailAddress</code> <br> <b>Données de saisie à activer</b> <br><table><thead><tr><th>Prénom</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>Sortie d’activation</b> <br><table><thead><tr><th>Prénom</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> Exemple de comportement après la version de janvier 2023 </b> <br> <b>Sortie d’activation</b> <br> <table><thead><tr><th>Prénom</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
</table>

Pour des informations plus générales sur les destinations, consultez la [présentation des destinations](../../destinations/home.md).

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

## Profil client en temps réel {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Real-Time Customer Profile offre une vue d’ensemble de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le Profil vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

**Dépréciation à venir** {#deprecation}

Pour supprimer la redondance dans le cycle de vie de l’adhésion au segment, la variable `Existing` est obsolète de la [carte d’appartenance aux segments](../../xdm/field-groups/profile/segmentation.md) fin mars 2023. Une annonce de suivi contiendra la date exacte d’obsolescence.

Les profils qualifiés dans un segment sont représentés comme suit : `Realized` et les profils disqualifiés continueront à être représentés comme `Exited`. Cela permettra d’obtenir la parité avec les destinations basées sur des fichiers avec `Active` et `Expired` états des segments.

Cette modification peut avoir un impact sur vous si vous utilisez [destinations d’entreprise](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hubs, API HTTP) et ont mis en place des processus en aval automatisés, en fonction des `Existing` statut. Vérifiez vos intégrations en aval si c’est le cas pour vous. Si vous souhaitez identifier les profils nouvellement qualifiés au-delà d’un certain temps, envisagez d’utiliser une combinaison de la variable `Realized` et le `lastQualificationTime` dans votre carte d’appartenance aux segments. Pour plus d’informations, contactez votre représentant Adobe.

Pour en savoir plus sur Real-time Customer Profile, notamment des tutoriels et des bonnes pratiques concernant l’utilisation des données de profil, commencez par lire la section [Présentation de Real-Time Customer Profile](../../profile/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Expiration de l’appartenance à un segment généré par Platform | Toute adhésion au segment qui figure dans la variable `Exited` d’un état de plus de 30 jours, en fonction de la variable `lastQualificationTime` sera sujette à suppression. |
| Expiration de l’appartenance à une audience externe | Par défaut, les appartenances aux audiences externes sont conservées pendant 30 jours. Pour les conserver plus longtemps, utilisez le `validUntil` lors de l’ingestion des données d’audience. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [présentation de la segmentation](../../segmentation/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes et vous permet de structurer, d’étiqueter et d’améliorer ces données à l’aide des services Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| --- | --- |
| Autoriser l’accès des utilisateurs aux sous-dossiers des sources de stockage dans le cloud | Vous pouvez désormais définir l’accès à un sous-dossier spécifique de votre source de stockage dans le cloud lors de la création d’un compte. Une fois créés, les utilisateurs ne pourront accéder qu’aux données du sous-dossier autorisé. Cette fonctionnalité est disponible pour les sources de stockage dans le cloud suivantes : [Stockage Azure Blob](../../sources/connectors/cloud-storage/blob.md), [Stockage dans le cloud Google](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md), et [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Disponibilité bêta de [!DNL SugarCRM] | [!DNL SugarCRM] Les sources sont désormais disponibles en version bêta. Utilisez la variable [!DNL SugarCRM Accounts & Contacts] et le [!DNL SugarCRM Events] sources pour importer des données à partir de vos [!DNL SugarCRM] compte à Experience Platform. Pour plus d’informations, reportez-vous à la section [[!DNL SugarCRM] aperçu](../../sources/connectors/crm/sugarcrm.md). |