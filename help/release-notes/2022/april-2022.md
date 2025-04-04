---
title: Notes de mise à jour d’Adobe Experience Platform - Avril 2022
description: Les notes de mise à jour d’avril 2022 pour Adobe Experience Platform.
exl-id: 39233787-3089-4469-8363-b006ae41ae21
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2679'
ht-degree: 92%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 27 avril 2022**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [[!DNL Dashboards]](#dashboards)
- [Flux de données](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [Destinations](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Édition B2B de Real-Time Customer Data Platform](#B2B)
- [Sources](#sources)

## [!DNL Dashboards] {#dashboards}

Experience Platform propose plusieurs tableaux de bord grâce auxquels vous pouvez afficher des informations importantes sur les données de votre organisation. Celles-ci sont présentées telles qu’elles sont capturées lors d’instantanés quotidiens.

Les tableaux de bord proposent des options de rapports préconfigurés sur les données de votre entreprise. Ils sont directement intégrés au workflow du spécialiste marketing dans Experience Platform. La mise à disposition de ces tableaux de bord ne nécessite pas d’assistance informatique supplémentaire. En outre, ils offrent un gain de temps et d’effort en évitant de recourir à l’exportation et au traitement des données avec une conception et une implémentation d’entreposage de données supplémentaires.

Les widgets suivants sont disponibles via la bibliothèque de widgets dans leurs tableaux de bord respectifs. Pour plus d’informations, consultez la documentation sur l’[ajout de widgets via la bibliothèque de widgets](../../dashboards/customize/widget-library.md).

**Nouveaux widgets**

| Widget | Tableau de bord | Description |
| ------ | --------- | ----------- |
| [!UICONTROL Tendance des profils ajoutés] | Profils | Ce widget utilise un graphique linéaire pour illustrer le nombre total de profils fusionnés qui ont été ajoutés quotidiennement à la banque de profils au cours des 30 derniers jours, des 90 derniers jours, ou des 12 derniers mois. |
| [!UICONTROL Audiences mappées au statut de destination] | Profils | Ce widget affiche le nombre total d’audiences mappées et non mappées dans une seule mesure et utilise un graphique en anneau pour illustrer la différence proportionnelle entre les totaux. |
| [!UICONTROL Taille des audiences] | Profils | Ce widget fournit un tableau à deux colonnes qui répertorie jusqu’à 20 segments et le nombre total d’audiences contenues dans chaque segment. La liste dépend de la politique de fusion appliquée et le nombre total d’audiences est classé par ordre décroissant. |
| [!UICONTROL Tendance du nombre de profils] | Profils | Ce widget utilise un graphique linéaire pour illustrer la tendance du nombre total de profils contenus dans le système au fil du temps. Les données peuvent être consultées sur des périodes de 30 jours, 90 jours et 12 mois. |
| [!UICONTROL Profils d’identité uniques par identité] | Profils | Ce widget utilise un graphique à barres pour illustrer le nombre total de profils qui sont identifiés à l’aide d’un identifiant unique. Le widget prend en charge jusqu’à cinq des identités les plus courantes. |
| [!UICONTROL Statut de destination] | Destinations | Ce widget affiche le nombre total de destinations activées sous la forme d’une mesure unique et utilise un graphique en anneau pour illustrer la différence proportionnelle entre les destinations activées et désactivées. |
| [!UICONTROL Destinations actives par plateforme de destination] | Destinations | Ce widget utilise un tableau à deux colonnes pour afficher la liste des plateformes de destination actives et le nombre total de destinations actives pour chaque plateforme de destination. |
| [!UICONTROL Audiences activées sur toutes les destinations] | Destinations | Ce widget fournit le nombre total d’audiences activées sur toutes les destinations dans une seule mesure. |
| [!UICONTROL Ordre d’activation de l’audience] | Segments | Ce widget fournit un tableau à trois colonnes qui répertorie le nom de destination, la plateforme et la date d’activation de l’audience. |
| [!UICONTROL Tendance de la taille de l’audience] | Segments | Ce widget fournit un graphique linéaire qui illustre le nombre total de profils qui répondent aux critères d’une définition de segment sur des périodes de 30 jours, 90 jours et 12 mois. |
| [!UICONTROL Tendance de changement de la taille de l’audience] | Segments | Ce widget fournit un graphique linéaire qui illustre la différence entre le nombre total de profils qualifiés pour un segment donné et les aperçus quotidiens les plus récents. La période d’analyse des tendances peut être consultée sur des périodes de 30 jours, 90 jours et 12 mois. |
| [!UICONTROL Tendance de la taille de l’audience par identité] | Segments | Ce widget illustre la tendance de la taille de l’audience d’un segment particulier en fonction d’un type d’identité sélectionné. La période d’analyse des tendances peut être consultée sur des périodes de 30 jours, 90 jours et 12 mois. |

**Nouvelles fonctionnalités** {#new-features}

| Fonctionnalité | Tableau de bord | Description |
| ------- | --------- | ----------- |
| Nettoyage de l’appartenance aux segments de profils orphelins | Profils et utilisation de la licence | Le service de profil supprime désormais tous les jours les membres de segments restants, ce qui permet d’obtenir une représentation plus précise de vos profils dans votre système. Ce nettoyage intervient après la suppression de tous les fragments de profil d’un profil donné. En conséquence, les deux mesures suivantes peuvent afficher des chiffres inférieurs : « Audience adressable » dans le tableau de bord de l’utilisation des licences et « Nombre de profils » dans le tableau de bord des profils. En effet, ces mesures incluaient des fragments de segment restants avant la publication de cette version. |

{style="table-layout:auto"}

Consultez la documentation pour plus d’informations sur les tableaux de bord [[!DNL Profiles]](../../dashboards/guides/profiles.md), [[!DNL Destinations]](../../dashboards/guides/destinations.md) et [[!DNL Segments]](../../dashboards/guides/audiences.md).

## Flux de données {#dataflows}

Dans Experience Platform, les données sont ingérées à partir de nombreuses sources différentes, analysées dans le système et activées vers un large éventail de destinations. Experience Platform facilite le processus de suivi de ce flux de données potentiellement non linéaire en offrant de la transparence aux flux de données.

Les flux de données sont une représentation des tâches qui déplacent des données dans Experience Platform. Ces flux de données sont configurés sur différents services, ce qui permet de déplacer les données des connecteurs sources vers les jeux de données cibles, où elles sont ensuite utilisées par le service d’identités et le profil client en temps réel avant d’être finalement activées vers les destinations.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Tableau de bord des segments | Vous pouvez désormais utiliser le tableau de bord de surveillance pour surveiller les flux de données des segments. Pour en savoir plus, consultez le guide sur la [surveillance des segments dans lʼinterface utilisateur](../../dataflows/ui/monitor-audiences.md). |

Pour des informations plus générales sur les flux de données, consultez la [présentation des flux de données](../../dataflows/home.md). Pour en savoir plus sur la segmentation, consultez la [présentation de la segmentation](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de la source Adobe Analytics | La source Adobe Analytics prend désormais en charge les fonctionnalités de préparation de données. Celles-ci vous permettent de mapper vos données de suite de rapports Analytics à un schéma XDM cible lors de la création d’un flux de données. Pour plus d’informations, consultez le tutoriel sur la [création d’une connexion source Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| Prise en charge de l’importation de règles de mappage existantes | Vous pouvez désormais importer des règles de mappage à partir d’un flux de données existant afin d’accélérer vos configurations de flux de données et de limiter les erreurs. Pour plus d’informations, consultez le tutoriel sur l’[importation de règles de mappage existantes](../../data-prep/ui/mapping.md). |

Pour plus d’informations sur Query Service [!DNL Data Prep], consultez la [[!DNL Data Prep] présentation](../../data-prep/home.md) de Query Service.

## [!DNL Destinations] {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ----------- | ----------- |
| Connecteurs de destination d’entreprise avancés | Trois connecteurs de destination d’entreprise sont désormais disponibles : [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md), [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md) et [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md). <br> La disponibilité générale des connecteurs de destination d’entreprise comprend toutes les fonctionnalités proposées précédemment dans la phase Beta, et bien plus encore : <ul><li>Nouvelles fonctionnalités d’authentification, notamment la [Signature d’accès partagé dans Azure Event Hubs](../../destinations/catalog/cloud-storage/azure-event-hubs.md#sas-authentication) et d’autres [types d’authentification](../../destinations/catalog/streaming/http-destination.md#authentication-information) (jetons du porteur, OAuth 2) dans la destination de l’API HTTP</li><li>[Renvoi de données de profil historiques](../../destinations/catalog/streaming/http-destination.md#historical-data-backfill) (envoi de profils historiques qualifiés pour le segment lors de sa première activation)</li><li>Les mesures de l’exécution du flux de données sont désormais prises en charge pour ces destinations</li><li>[Métadonnées de segment supplémentaires](../../destinations/catalog/streaming/http-destination.md#destination-details) incluses dans la charge utile de données, y compris les noms de segment et les dates et heures de segment</li><li>Prise en charge d’[adresses IP statiques](/help/destinations/catalog/streaming/ip-address-allow-list.md) pour les clients qui doivent placer Experience Platform sur la liste autorisée</li></ul> |
| Alertes dans le contexte pour les flux de données de destination | Vous pouvez désormais vous [abonner aux alertes](../../destinations/ui/alerts.md) lors de la création d’un flux de données de destination, pour recevoir des messages d’alerte concernant le statut, le succès ou l’échec de l’exécution du flux de données. Vous pouvez choisir de recevoir des alertes dans l’interface utilisateur d’Experience Platform ou par e-mail. |

### Processus de publication des connecteurs de destination d’entreprise avancés {#release-process-enterprise-destinations}

Pour les destinations Amazon Kinesis, Azure Event Hubs et de l’API HTTP, au cours du processus de publication (à compter du 27 avril), le catalogue des destinations affiche à la fois l’ancienne carte de destination Beta, ainsi que la nouvelle carte de destination mise à disposition générale. Les flux de données configurés par les clients utilisant les destinations Beta sont migrés au cours des deux prochains jours vers la version mise à disposition générale de la même destination. Cette migration doit être terminée d’ici la fin de la journée du vendredi 29 avril. Les destinations Beta restent visibles pendant cette courte période et sont libellées comme **Obsolètes**.

Si vous avez utilisé ces destinations dans la phase Beta, notez les points suivants :

- Si vous avez déjà utilisé la phase Beta pour l’une de ces trois destinations, aucune action n’est nécessaire. Tous les flux de données configurés dans le cadre de la phase Beta restent fonctionnels et sont migrés vers la version mise à disposition générale.
- Si vous souhaitez configurer ces destinations à partir du 27 avril, utilisez la nouvelle version mise à disposition générale des destinations.
- Les cartes Beta marquées comme obsolètes sont supprimées une fois l’opération de publication terminée, prévue pour la fin de la journée du vendredi 29 avril. L’équipe d’ingénieurs d’Experience Platform surveille de près la réussite de l’opération de publication.

**Nouvelles destinations**

| Destination | Description |
| ----------- | ----------- |
| [!DNL Criteo] | Connectez-vous et activez les données sur la plateforme publicitaire [[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md). |
| [!DNL Sendgrid] | Connectez-vous et activez les données sur la plateforme [[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md) pour accéder aux e-mails transactionnels et marketing. |

Pour des informations plus générales sur les destinations, consultez la [présentation des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Ajout ou suppression de champs standard individuels d’un schéma | L’interface utilisateur de l’éditeur de schéma vous permet désormais d’ajouter des parties de groupes de champs standard à vos schémas, offrant ainsi une plus grande flexibilité pour les champs que vous choisissez d’inclure sans avoir à créer intégralement des ressources personnalisées.<br><br>Vous pouvez désormais également définir des champs personnalisés ad hoc directement dans la structure du schéma et les affecter à un groupe de champs personnalisés existant ou nouveau, sans devoir créer ou modifier le groupe de champs au préalable.<br><br>Consultez le guide sur la [création et modification de schémas dans l’interface utilisateur](../../xdm/ui/resources/schemas.md) pour plus d’informations sur ces nouveaux processus. |

{style="table-layout:auto"}

**Nouveaux composants XDM**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Schéma global | [[!UICONTROL Demande d’opération de nettoyage de données]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | Capture les détails d’une demande de nettoyage des données pour supprimer ou modifier des enregistrements dans un jeu de données ou un sandbox spécifié. |
| Descripteur | [[!UICONTROL Descripteur de granularité de série temporelle]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | Indique la granularité des données récapitulatives et de série temporelle. Lorsqu’il est appliqué à un schéma, le champ `timestamp` du schéma est la première date et heure d’une période de cette granularité. |
| Classe | [[!UICONTROL Mesures récapitulatives XDM]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | Fournit des mesures préalablement résumées avec des dimensions de regroupement, telles que les résultats d’une instruction SQL SELECT avec GROUP BY. |
| Groupe de champs | [[!UICONTROL Mappage des résultats d’évaluation des politiques de consentement]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResults.schema.json) | Capture le résultat de l’évaluation de la politique de consentement pour un individu. |
| Groupe de champs | [[!UICONTROL Recherche de site]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Capture les informations relatives à la recherche de site, telles que la requête, le filtrage et le classement. |
| Groupe de champs | [[!UICONTROL Fusion des pistes]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | Capture les détails d’un événement pendant lequel plusieurs pistes sont fusionnées. |
| Groupe de champs | [[!UICONTROL E-mails envoyés]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | Capture les détails d’un événement pendant lequel un e-mail est envoyé à un destinataire. |
| Groupe de champs | [[!UICONTROL Combinaison de champs]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | Capture les valeurs calculées via le processus de combinaison d’identités pour un événement. |
| Groupe de champs | [[!UICONTROL Détails du destinataire secondaire pour un audit]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | Groupe de champs Adobe Journey Optimizer capturant les détails d’un destinataire secondaire pour un audit. |
| Groupe de champs | [[!UICONTROL Détails d’une relation avec la personne du compte d’entreprise XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Capture les détails liés à une relation compte-personne. |
| Groupe de champs | [[!UICONTROL Détails de la personne du compte]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Capture les détails liés à une relation compte-personne. |
| Type de données | [[!UICONTROL Panier]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | Capture les informations sur un panier de commerce électronique. |
| Type de données | [[!UICONTROL Expédition]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Capture les informations d’expédition pour un ou plusieurs produits. |
| Type de données | [[!UICONTROL Recherche de site]](https://github.com/adobe/xdm/blob/master/components/datatypes/sitesearch.schema.json) | Capture des informations sur l’activité de recherche de site. |
| Extension (Workfront) | [[!UICONTROL Attributs de tâche opérationnelle]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | Capture les détails relatifs à une tâche opérationnelle. |
| Extension (Workfront) | [[!UICONTROL Attributs de portfolio de travail]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | Capture les détails liés à un portfolio de travail. |
| Extension (Workfront) | [[!UICONTROL Attributs du programme de travail]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | Capture les détails liés à un programme de travail. |
| Extension (Workfront) | [[!UICONTROL Attributs de projet de travail]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | Capture les détails liés à un projet de travail. |

{style="table-layout:auto"}

**Composants XDM mis à jour**

| Type de composant | Nom | Description de la mise à jour |
| --- | --- | --- |
| Schéma global | [[!UICONTROL Destinations]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | Nouvelles valeurs d’énumération de `destinationCategory`. |
| Descripteur | [[!UICONTROL Descripteur de nom convivial]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | Prise en charge ajoutée pour la suppression des valeurs suggérées (`meta:enum`) qui ne sont pas nécessaires dans les champs standard. |
| Groupe de champs | [[!UICONTROL Processus de connexion de l’utilisateur]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | Champ `createProfile` ajouté. |
| Type de données | [[!UICONTROL Commerce]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | Plusieurs champs liés au panier ont été ajoutés. |
| Type de données | [[!UICONTROL Élément de liste de produits]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Nouveaux champs ajoutés pour les options sélectionnées et le montant de la remise. |
| Extension (Intelligent Services) | [[!UICONTROL Optimisation du temps d’envoi d’Intelligent Services JourneyAI]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | Optimisez le format de stockage pour les scores de temps d’envoi. |
| Extension (Workfront) | [[!UICONTROL Événement de changement de Workfront]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Plusieurs champs remplacés par un champ `workfront:customData` pour les champs de formulaire personnalisé. |
| Extension (Workfront) | [[!UICONTROL Attributs de tâche de travail]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | Plusieurs champs ont été ajoutés. |
| Extension (Workfront) | [[!UICONTROL Objet de travail]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | Nouveaux champs pour le type d’objet parent et les champs de formulaire personnalisé. |

{style="table-layout:auto"}

Pour plus d’informations sur XDM dans Experience Platform, consultez la [ Présentation du système XDM ](../../xdm/home.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai/ml-services}

Les services d’IA/ML permettent aux analystes et spécialistes du marketing d’exploiter la puissance de l’intelligence artificielle et du machine learning dans les cas d’utilisation de l’expérience client. Les analystes marketing peuvent obtenir des prédictions spécifiques aux besoins d’une entreprise en utilisant des configurations au niveau de l’entreprise sans avoir besoin d’expertise en sciences des données.

### IA dédiée à l’attribution

L’IA dédiée à l’attribution est utilisée pour attribuer des crédits aux points de contact qui génèrent des événements de conversion. Il peut aider les spécialistes du marketing à quantifier l’impact publicitaire de chaque point de contact marketing sur le parcours client.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge de jeux de données multiples | La fonctionnalité de jeux de données multiples prend désormais en charge tous les jeux de données d’événement d’expérience, ainsi que la sélection du mappage d’identité comme identité. Les clients peuvent sélectionner le mappage d’identité et les ID associés, à condition que les jeux de données disposent d’un espace de noms d’identité commun. L’IA dédiée à l’attribution prend en charge les schémas suivants : Adobe Analytics, événement d’expérience, événement d’expérience de client. Pour plus d’informations sur la prise en charge de jeux de données multiples dans l’IA dédiée à l’attribution, consultez le [guide d’utilisation de l’IA dédiée à l’attribution](../../intelligent-services/attribution-ai/user-guide.md). |

Pour plus d’informations sur Query Service [!DNL Intelligent Services], consultez la [[!DNL Intelligent Services] présentation](../../intelligent-services/home.md) de Query Service.

### IA dédiée aux clients

L’IA dédiée aux clients disponible dans Real-time Customer Data Platform est utilisée pour générer des scores de propension personnalisés tels que l’attrition et la conversion pour des profils individuels à grande échelle. Cette opération s’effectue sans qu’il soit nécessaire de transformer les besoins professionnels en un problème de machine learning ou d’avoir recours à un algorithme, à une formation ou à un déploiement.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge de jeux de données multiples | La fonctionnalité de jeux de données multiples prend désormais en charge tous les jeux de données d’événement d’expérience, ainsi que la sélection du mappage d’identité comme identité. Les clients peuvent sélectionner le mappage d’identité et les ID associés, à condition que les jeux de données disposent d’un espace de noms d’identité commun. L’IA dédiée aux clients prend en charge les schémas suivants : Adobe Analytics, Événement d’experience, Événement d’experience consommateur et le schéma Adobe Audience Manager. Pour plus d’informations sur la prise en charge de jeux de données multiples dans l’IA dédiée aux clients, consultez le [guide d’utilisation de l’IA dédiée aux clients](../../intelligent-services/customer-ai/user-guide/configure.md). |
| Nouvelles mesures d’évaluation de modèle dans l’IA dédiée aux clients | Les nouveaux graphiques de gains dans l’IA dédiée aux clients permettent aux spécialistes marketing de déterminer la taille du groupe à cibler en fonction de leur budget et de leurs objectifs de retour sur investissement. Les nouveaux graphiques de courbe d’élévation évaluent la qualité du modèle, offrant ainsi une meilleure visibilité sur la courbe d’élévation obtenue par rapport à un ciblage aléatoire. Pour plus d’informations, consultez le document [découvrir des informations avec l’IA dédiée aux clients](../../intelligent-services/customer-ai/user-guide/discover-insights.md). |

Pour plus d’informations sur Query Service [!DNL Intelligent Services], consultez la [[!DNL Intelligent Services] présentation](../../intelligent-services/home.md) de Query Service.

## Édition B2B de Real-Time Customer Data Platform {#B2B}

Basée sur Real-time Customer Data Platform (Real-time CDP), l’édition B2B de Real-time CDP a été conçue pour les professionnels du marketing travaillant dans un modèle de service business-to-business. Elle rassemble des données provenant de sources multiples et les combine en une vue unique des profils de comptes et d’utilisateurs. Ces données unifiées permettent aux spécialistes marketing de cibler précisément des audiences spécifiques afin de stimuler leur engagement sur tous les canaux disponibles.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de la fonctionnalité `isDeleted` | Tous les jeux de données [!DNL Marketo], sauf `Activities` prennent désormais en charge le mappage `isDeleted`. Le nouveau mappage est automatiquement ajouté à vos flux de données B2B existants. Vous pouvez utiliser le mappage `isDeleted` pour filtrer les enregistrements supprimés afin que les données dans le [!DNL Data Lake] soient cohérentes avec les données sources. Consultez le [[!DNL Marketo] guide du mappage des champs](../../sources/connectors/adobe-applications/mapping/marketo.md) pour plus d’informations sur `isDeleted`. |

Pour en savoir plus sur l’édition B2B de Real-time Customer Data Platform, consultez la [présentation B2B](../../rtcdp/b2b-overview.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services d’Experience Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de [!DNL OneTrust Integration] | Vous pouvez désormais utiliser la source de [!DNL OneTrust Integration] pour ingérer les données de consentement et de préférences du compte [!DNL OneTrust] vers Experience Platform. Pour plus d’informations, consultez la documentation sur la [création d’une [!DNL OneTrust Integration] connexion source](../../sources/connectors/consent-and-preferences/onetrust.md). |
| Prise en charge de [!DNL Square] | Vous pouvez désormais utiliser la source de [!DNL Square] pour ingérer les données de paiements à partir du compte [!DNL Square] vers Experience Platform. |
| Prise en charge de la suppression des flux de données d’attributs du client | Vous pouvez désormais supprimer les flux de données créés à l’aide du connecteur source d’attributs du client. |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
