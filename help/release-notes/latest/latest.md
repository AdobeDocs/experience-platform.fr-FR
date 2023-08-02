---
title: Notes de mise à jour d’Adobe Experience Platform
description: Les notes de mise à jour de juillet 2023 pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: d639b0830b88307b249e7da232b3f48b142ad37b
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 45%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 26 juillet 2023**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Service de catalogue](#catalog-service)
- [Collecte de données](#data-collection)
- [Préparation des données](#data-prep)
- [Destinations](#destinations)
- [Query Service](#query-service)
- [Segmentation Service](#segmentation)
- [Sources](#sources)
- [Modèle de données d’expérience (XDM)](#xdm)

## Service de catalogue {#catalog-service}

Le Catalog Service est le système d’enregistrement pour l’emplacement et la parenté des données au sein d’Adobe Experience Platform. Bien que toutes les données ingérées dans Experience Platform soient stockées dans le lac de données sous forme de fichiers et de répertoires, le catalogue renferme les métadonnées et la description de ces fichiers et répertoires à des fins de recherche et de surveillance.

| Fonctionnalité | Description |
| --- | --- |
| Gestion des stocks de jeux de données | L’interface utilisateur des jeux de données propose désormais un ensemble d’actions intégrées pour mieux gérer vos jeux de données. La gestion avancée des jeux de données améliore votre efficacité par la création et l’affectation de dossiers et de balises à vos jeux de données, ce qui permet de filtrer et d’améliorer la visibilité. Pour plus d’informations sur la [actions intégrées](../../catalog/datasets/user-guide.md#inline-actions), comment [recherche et filtrage de jeux de données](../../catalog/datasets/user-guide.md#search-and-filter), et [déplacer des jeux de données vers des dossiers ;](../../catalog/datasets/user-guide.md#move-to-folders). |

{style="table-layout:auto"}

Pour plus d’informations sur le service de catalogue, reportez-vous au [Présentation du service de catalogue](../../catalog/home.md).

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Type | Fonctionnalité | Description |
| --- | --- | --- |
| Balises et transfert d’événement | Journaux d’audit de la collecte de données | Vous pouvez maintenant savoir quand une action a été effectuée et qui a effectué cette action sur les balises et le transfert d’événement. Cela facilite la résolution des problèmes liés aux produits, la bonne gouvernance et les activités d’audit interne. Ces données d’audit s’affichent par le biais de menus de diapositives contextuels qui incluent également des actions rapides et des mises à jour de l’état des ressources. Ces données sont visibles dans l’interface utilisateur Balises et Transfert d’événement dans les écrans suivants :<br><ul><li>[Présentation de la propriété](../../tags/ui/event-forwarding/overview.md#properties)</li><li>[Règles](../../tags/ui/event-forwarding/overview.md#rules)</li><li>[Éléments de données](../../tags/ui/event-forwarding/overview.md#data-elements)</li><li>[Extensions](../../tags/ui/event-forwarding/overview.md#extensions)</li><li>[Révision de bibliothèque](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li><li>[Dernière version et publication de la bibliothèque](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li></ul> |
| Flux de données | [Recherche géographique](../../datastreams/configure.md#advanced-options) | Vous pouvez désormais configurer la géolocalisation et la recherche réseau pour les flux de données afin d’inclure des informations telles que : <ul><li>Pays</li><li>Code postal</li><li>Etat/Province</li><li>DMA</li><li>Ville</li><li>Latitude </li><li>Longitude</li><li>Opérateur</li><li>Domaine</li><li>Fournisseur de services Internet</li></ul> Il vous incombe de vous assurer que vous avez obtenu toutes les autorisations, consentements, autorisations et autorisations nécessaires en vertu des lois et réglementations applicables pour collecter, traiter et transmettre des données personnelles, y compris des informations de géolocalisation précises. <br> Votre sélection de l’obscurcissement des adresses IP n’a aucune incidence sur le niveau des informations de géolocalisation qui seront dérivées de l’adresse IP et envoyées à vos solutions d’Adobe configurées. Les recherches de géolocalisation doivent être limitées ou désactivées séparément. <br> Voir [documentation sur les datastreams](../../datastreams/configure.md#advanced-options) pour plus d’informations. |

{style="table-layout:auto"}

Pour plus d’informations sur la collecte de données, veuillez lire la section [présentation des collections de données](../../tags/home.md).

## Préparation des données {#data-prep}

La préparation des données permet aux personnes travaillant dans l’ingénierie de données de mapper, de transformer et de valider les données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouvelles fonctions de mappeur | Vous pouvez désormais utiliser les fonctions suivantes lors du mappage d’objets dans Data Prep : <ul><li>`map_get_values`</li><li>`map_has_keys`</li><li>`add_to_map`</li></ul> Pour plus d’informations sur ces fonctions, consultez la section [Guide des fonctions de préparation de données](../../data-prep/functions.md#hierarchies---objects). |

{style="table-layout:auto"}

Pour plus d’informations sur la préparation des données, consultez la [présentation de la préparation des données](../../data-prep/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour** {#new-updated-destinations}

| Destination | Nouvelle ou mise à jour | Description |
| ----------- |----------------|----------- |
| [[!DNL LiveRamp - Onboarding]](../../destinations/catalog/advertising/liveramp-onboarding.md) | Nouveau  | Identités intégrées de Adobe Experience Platform vers [!DNL LiveRamp Connect] afin de cibler les utilisateurs sur mobile, ouvrir le web, les réseaux sociaux et [!DNL CTV] plateformes, à l’aide de [!DNL Ramp ID] identifiant. |
| [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Nouveau  | Créez une connexion sortante active vers [!DNL Azure Data Lake Storage Gen2] pour exporter régulièrement des fichiers de données d’Adobe Experience Platform vers votre propre emplacement de stockage. Cette nouvelle destination offre une fonctionnalité d’exportation de fichiers améliorée et prend en charge [!BADGE Beta]{type=Informative} |
| [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | Nouveau  | [!DNL Data Landing Zone] est une interface de stockage [!DNL Azure Blob] fournie par Adobe Experience Platform et qui vous permet d’accéder à une fonctionnalité de stockage de fichiers sécurisée basée sur le cloud pour exporter des fichiers hors de Platform. Cette nouvelle destination offre une fonctionnalité d’exportation de fichiers améliorée et prend en charge [!BADGE Beta]{type=Informative} |
| [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Nouveau  | Créez une connexion sortante active vers [!DNL Google Cloud Storage] pour exporter régulièrement des fichiers de données d’Adobe Experience Platform dans vos propres compartiments. Cette nouvelle destination offre une fonctionnalité d’exportation de fichiers améliorée et prend en charge [!BADGE Beta]{type=Informative} |
| [[!DNL Amazon S3] mettre à jour](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Mise à jour des lots   | Grâce à cette mise à jour, la destination offre des fonctionnalités d’exportation de fichiers améliorées et prend en charge [!BADGE Beta]{type=Informative} |
| [[!DNL Azure Blob] mettre à jour](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Mise à jour des lots   | Grâce à cette mise à jour, la destination offre des fonctionnalités d’exportation de fichiers améliorées et prend en charge [!BADGE Beta]{type=Informative} |
| [[!DNL SFTP] mettre à jour](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Mise à jour des lots   | Grâce à cette mise à jour, la destination offre des fonctionnalités d’exportation de fichiers améliorées et prend en charge [!BADGE Beta]{type=Informative} |
| Connexion [[!DNL Adobe Campaign Managed Services] ](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Mise à jour des lots   | La variable [!DNL Adobe Campaign Managed Services] l’intégration à Adobe Experience Platform prend désormais en charge différents types de synchronisation d’audience. Utilisez le contrôle Sélectionner le type de synchronisation pour déterminer si vous devez exporter des audiences vers Adobe Campaign ou des audiences et leurs attributs de profil. <br> ![Nouveau sélecteur de type de synchronisation sélectionné en surbrillance.](/help/release-notes/2023/assets/acms-destination-export-type.png "Nouveau sélecteur de type de synchronisation sélectionné en surbrillance."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

La mise à jour et la mise à jour générale des six destinations de stockage dans le cloud ci-dessus fournissent les fonctionnalités suivantes :

- [Options de dénomination de fichier](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) supplémentaires.
- Possibilité de définir des en-têtes de fichier personnalisés dans vos fichiers exportés via l’[étape de mappage améliorée](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
- Possibilité de personnaliser les [formatage des fichiers de données CSV exportés](/help/destinations/ui/batch-destinations-file-formatting-options.md).
- [!BADGE Version bêta]{type=Informative}[Prise en charge de l’exportation des jeux de données](/help/destinations/ui/export-datasets.md).


**Correctifs et améliorations** {#destinations-fixes-and-enhancements}

- Correction d’un problème avec la destination de Marketing Cloud Salesforce (API) en raison duquel, à l’étape de mappage, tous les attributs de cible disponibles n’étaient pas renvoyés par Salesforce. Il existe maintenant une [limite supérieure de 2 000 attributs cibles](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md#mapping-considerations-example) de Salesforce qui peut être affiché.
- Correction d’un problème avec la destination Microsoft Dynamics 365. La destination prend désormais en charge le routage régional des données via le [Sélecteur de région](/help/destinations/catalog/crm/microsoft-dynamics-365.md#authenticate), afin que vous puissiez acheminer vos exportations de données en fonction de la région dans laquelle votre entreprise est configurée dans l’écosystème Microsoft. <br> ![Nouveau sélecteur de région mis en surbrillance.](/help/release-notes/2023/assets/region-parameter-microsoft-dynamics-365.png "Nouveau sélecteur de région mis en surbrillance."){width="100" zoomable="yes"}

Pour des informations plus générales sur les destinations, reportez-vous à la [présentation des destinations](../../destinations/home.md).

## Query Service {#query-service}

Query Service vous permet d’utiliser le langage SQL standard pour interroger les données dans le lac de données d’Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du lac de données et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans l’espace de travail de science des données ou à ingérer en tant que profil client en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Bascule de l’éditeur de requêtes amélioré | Le bouton bascule amélioré de l’éditeur de requêtes offre une meilleure accessibilité et une prise en charge multi-thème. Les paramètres d’éditeur améliorés vous permettent d’activer les thèmes foncés ou clairs. Pour plus d’informations, consultez la [documentation](../../query-service/ui/user-guide.md#enhanced-editor-toggle). |
| Nom d’alias pour les statistiques calculées | Vous pouvez maintenant fournir un nom d’alias pour référencer de manière descriptive les résultats de votre dans vos statistiques calculées dans les requêtes SQL. Consultez la documentation pour plus d’informations à ce sujet et sur d’autres mises à jour de la commande CALCULER les STATISTIQUES . Pour plus d’informations, consultez la [documentation](../../query-service/essential-concepts/dataset-statistics.md#alias-name). |

{style="table-layout:auto"}

Pour plus d’informations sur Query Service, consultez la [vue d’ensemble de Query Service](../../query-service/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] vous permet de segmenter les données stockées dans [!DNL Experience Platform] qui se rapporte aux individus (tels que les clients, les prospects, les utilisateurs ou les organisations) dans des audiences. Vous pouvez créer des audiences par le biais de définitions de segment ou d’autres sources à partir de vos [!DNL Real-Time Customer Profile] data. Ces audiences sont configurées et gérées de manière centralisée sur [!DNL Platform], et sont facilement accessibles par toute solution d’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Audience    Portail | Audience Portal offre une nouvelle expérience de navigation pour accéder aux audiences, les créer et les gérer dans Adobe Experience Platform. Dans Audience Portal, vous pouvez afficher les audiences générées par Platform et générées de l’extérieur, améliorer l’efficacité de votre travail grâce au filtrage, aux dossiers et aux balises, créer des audiences générées par Platform et importer des audiences générées de l’extérieur au moyen de fichiers CSV. Pour plus d’informations sur Audience Portal, veuillez lire le [Guide de l’interface utilisateur de Segmentation Service](../../segmentation/ui/overview.md). |
| Composition de l’audience | La composition d’audiences offre un espace de travail convivial pour créer et modifier des audiences à l’aide de blocs utilisés pour représenter différentes actions. Pour plus d’informations sur la composition de l’audience, veuillez lire le [Guide de l’interface utilisateur de composition d’audience](../../segmentation/ui/audience-composition.md). |

Pour plus d’informations sur [!DNL Segmentation Service], veuillez lire la [Présentation de la segmentation](../../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| [!BADGE Version bêta]{type=Informative}[!DNL SAP Commerce] | Vous pouvez désormais utiliser la variable [[!DNL SAP Commerce] source](../../sources/connectors/ecommerce/sap-commerce.md) pour importer les données de facturation d’abonnement de votre [!DNL SAP Commerce] compte à Experience Platform. |
| Prise en charge de [!DNL Phoenix] | Vous pouvez désormais utiliser la variable [[!DNL Phoenix] source](../../sources/connectors/databases/phoenix.md) pour importer des données de [!DNL Phoenix] base de données vers Experience Platform. |
| Mises à jour d’authentification vers [!DNL Salesforce] et [!DNL Salesforce Service Cloud] | Vous pouvez maintenant spécifier la version d’API de votre [[!DNL Salesforce]](../../sources/connectors/crm/salesforce.md) et [[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md) source lors de l’authentification d’un nouveau compte avec l’interface utilisateur de l’Experience Platform ou le [!DNL Flow Service] API. |

{style="table-layout:auto"}

Pour plus d’informations sur les sources, consultez la [vue d’ensemble des sources](../../sources/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouveaux composants XDM**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Classe | [[!UICONTROL XDM Individual Prospect Profile]](https://github.com/adobe/xdm/pull/1758/files) | Utilisez cette classe pour importer les profils de prospect provenant des cas d’utilisation d’acquisition client les plus récents des fournisseurs de données. |
| Groupe de champs | [[!UICONTROL Détails du segment d’événement enrichi]](https://github.com/adobe/xdm/pull/1754/files) | Liste des audiences auxquelles le profil est admissible au moment de la collecte de l’événement. |

{style="table-layout:auto"}

**Composants XDM mis à jour**

| Type de composant | Nom | Description de la mise à jour |
| --- | --- | --- |
| Groupe de champs | [[!UICONTROL Détails de l’interaction MediaAnalytics]](https://github.com/adobe/xdm/pull/1756/files) | La variable `meta:status` a été mis à jour d’ expérimental en `stable`. |
| Groupe de champs | [[!UICONTROL Détails de l’interaction multimédia]](https://github.com/adobe/xdm/pull/1756/files) | La variable `meta:status` a été mis à jour à partir de `stable` to `deprecated`. |
| Type de données | [[!UICONTROL Informations détaillées sur la session]](https://github.com/adobe/xdm/pull/1756/files) | La variable `meta:status` a été mis à jour à partir de `experimental` to `stable`. |
| Type de données | [[!UICONTROL Informations détaillées sur les données de la QoE]](https://github.com/adobe/xdm/pull/1756/files) | La variable `meta:status` a été mis à jour à partir de `experimental` to `stable`. |
| Type de données | [[!UICONTROL Informations sur l’état du lecteur]](https://github.com/adobe/xdm/pull/1756/files) | La variable `meta:status` a été mis à jour à partir de `experimental`to `stable`. |
| Type de données | [[!UICONTROL Informations sur les événements multimédia]](https://github.com/adobe/xdm/pull/1756/files) | La variable `meta:status` a été mis à jour à partir de `experimental` to `stable`. |
| Type de données | [[!UICONTROL Informations détaillées sur les médias]](https://github.com/adobe/xdm/pull/1756/files) | La variable `meta:status` a été mis à jour à partir de `experimental` to `stable`. |
| Type de données | [[!UICONTROL Informations détaillés sur les erreurs]](https://github.com/adobe/xdm/pull/1756/files) | La variable `meta:status` a été mis à jour à partir de `experimental` to `stable`. |
| Type de données | [[!UICONTROL Informations détaillés sur les erreurs]](https://github.com/adobe/xdm/pull/1756/files) | La variable `meta:status` a été mis à jour à partir de `stable` to `deprecated`. |
| Type de données | [[!UICONTROL Informations détaillées sur les métadonnées personnalisées]](https://github.com/adobe/xdm/pull/1756/files) | La variable `meta:status` a été mis à jour à partir de `experimental` to `stable`. |
| Type de données | [[!UICONTROL Informations détaillées sur le chapitre]](https://github.com/adobe/xdm/pull/1756/files) | La variable `meta:status` a été mis à jour à partir de `experimental` to `stable`. |
| Type de données | [[!UICONTROL Informations détaillées sur le pod publicitaire]](https://github.com/adobe/xdm/pull/1756/files) | La variable `meta:status` a été mis à jour à partir de `experimental` to `stable`. |
| Type de données | [[!UICONTROL Informations détaillées sur la publicité]](https://github.com/adobe/xdm/pull/1756/files) | La variable `meta:status` a été mis à jour à partir de `experimental` to `stable`. |
| Extension (gestion des Parcours client) | [[!UICONTROL Domaine]](https://github.com/adobe/xdm/pull/1756/files) | `Domain` champ ajouté à [!UICONTROL Adobe CJM ExperienceEvent - Détails du profil du message] pour enregistrer le domaine de l&#39;adresse email du destinataire. |
| Extension (gestion des Parcours client) | [[!UICONTROL Nom de variante du canal]](https://github.com/adobe/xdm/pull/1753/files) | Ce champ a été ajouté à [!UICONTROL Champs d’entité AJO] pour représenter le nom de la variante du canal. |
| Extension (Adobe Analytics) | [[!UICONTROL Valeur contextuelle]](https://github.com/adobe/xdm/pull/1761/files) | `Context value` a été ajouté à [!UICONTROL `Adobe Analytics ExperienceEvent Full Extension`]. |

{style="table-layout:auto"}

Pour plus d’informations sur XDM dans Platform, consultez la [présentation du système XDM](../../xdm/home.md)

