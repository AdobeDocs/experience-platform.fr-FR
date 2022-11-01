---
keywords: Experience Platform;activation;dépannage;barrières de sécurité;instructions;limite
title: Barrières de sécurité par défaut pour les données d’activation
solution: Experience Platform
product: experience platform
type: Documentation
description: En savoir plus sur l’utilisation par défaut de l’activation des données et les limites de débit.
source-git-commit: 69496d2e00ce866413786160d4524cabd03ae350
workflow-type: ht
source-wordcount: '1198'
ht-degree: 100%

---

# Barrières de sécurité pour les données d’activation

Cette page fournit les limites d’utilisation et de débit par défaut en ce qui concerne le comportement d’activation. Lors de la révision des barrières de sécurité suivantes, on suppose que vous avez correctement [connecté aux destinations](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* La plupart des clients ne dépassent pas ces limites par défaut. Si vous souhaitez en savoir plus sur les limites personnalisées, contactez votre représentant de l’assistance clientèle.
>* Les limites décrites dans ce document sont constamment améliorées. Consultez régulièrement les mises à jour.
>* Selon les limites individuelles en aval, certaines destinations peuvent avoir des barrières de sécurité plus strictes que celles documentées sur cette page. Veillez également à vérifier la page du [catalogue](/help/destinations/catalog/overview.md) de la destination à laquelle vous vous connectez et activez les données.


## Types de limite {#limit-types}

Ce document comprend deux types de limites par défaut :

* **Limite soft :** il est possible d’aller au-delà d’une limite soft, cependant ces limites fournissent une orientation recommandée pour les performances du système.
* **Limite Hard :** une limite Hard fournit un maximum absolu. L’interface utilisateur ou l’API d’Experience Platform ne vous permet pas de franchir cette limite. Une erreur sera renvoyée si vous la dépassez.


## Limites d’activation {#activation-limits}

Les barrières de sécurité suivantes fournissent des limites recommandées lors de l’activation des données Real-time Customer Profile vers les destinations.

### Barrières de sécurité générales de l’activation {#general-activation-guardrails}

Les barrières de sécurité ci-dessous s’appliquent généralement à l’activation par le biais de [tous les types de destination](/help/destinations/destination-types.md#destination-types).

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre maximal de segments vers une seule destination | 250 | Soft | Il est recommandé de mapper un maximum de 250 segments vers une seule destination dans un flux de données. <br><br> Si vous devez activer plus de 250 segments vers une destination, vous pouvez effectuer l’une des opérations suivantes : <ul><li> Annuler le mappage des segments que vous ne souhaitez plus activer, ou</li><li>Créer un nouveau flux de données vers la destination souhaitée et mapper les segments vers ce nouveau flux de données.</li></ul> <br> Notez que dans le cas de certaines destinations, vous pouvez être limité à moins de 250 segments mappés vers la destination. Ces destinations sont répertoriées plus bas sur la page, dans leurs sections respectives. |
| Nombre maximal de destinations | 100 | Soft | Il est recommandé de créer un maximum de 100 destinations auxquelles vous pouvez connecter et activer des données *par sandbox*. Les [destinations de personnalisation Edge (personnalisation personnalisée)](#edge-destinations-activation) peuvent représenter un maximum de 10 sur les 100 destinations recommandées. |
| Nombre maximal d’attributs mappés vers une destination | 50 | Soft | Dans le cas de plusieurs destinations et types de destination, vous pouvez sélectionner des attributs de profil et des identités à mapper pour l’exportation. Pour des performances optimales, un maximum de 50 attributs doit être mappé dans un flux de données vers une destination. |
| Type de données activées vers les destinations | Données de profil, y compris les identités et le mappage d’identités | Hard | Actuellement, il n’est possible d’exporter que des *attributs d’enregistrement de profil* vers les destinations. Pour l’instant, les attributs XDM qui décrivent les données d’événement ne sont pas pris en charge pour l’exportation. |
| Type de données activées vers les destinations : prise en charge des attributs de tableau et de mappage | Non disponible | Hard | À l’heure actuelle, il n’est **pas** possible d’exporter des *attributs de tableau ou de mappage* vers des destinations. L’exception à cette règle est le [mappage d’identités](/help/xdm/field-groups/profile/identitymap.md), qui est exporté à la fois dans les activations par flux et basées sur des fichiers. |

{style=&quot;table-layout:auto&quot;}

### Activation de la diffusion en continu {#streaming-activation}

Les barrières de sécurité ci-dessous s’appliquent à l’activation par le biais de [destinations de diffusion en continu](/help/destinations/ui/activate-segment-streaming-destinations.md).

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre d’activations (messages HTTP avec export de profils) par seconde | S/O | - | Il n’existe actuellement aucune limite au nombre de messages par seconde envoyés par Experience Platform aux points d’entrée de l’API des destinations partenaires. <br> Toute limite ou latence est déterminée par le point d’entrée où Experience Platform envoie des données. Veillez également à vérifier la page [catalogue](/help/destinations/catalog/overview.md) de la destination à laquelle vous vous connectez et vers laquelle vous activez les données. |

{style=&quot;table-layout:auto&quot;}

### Activation par lot (basée sur des fichiers) {#batch-file-based-activation}

Les barrières de sécurité ci-dessous s’appliquent à l’activation par le biais de [destinations par lot (basées sur des fichiers)](/help/destinations/ui/activate-batch-profile-destinations.md).

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Fréquence d’activation | Exportation complète quotidienne ou exportation incrémentielle plus fréquente toutes les 3, 6, 8 ou 12 heures. | Hard | Consultez les sections de documentation [Exporter des fichiers complets](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) et [Exporter des fichiers incrémentiels](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) pour plus d’informations sur les incréments de fréquence pour les exportations par lots. |
| Nombre maximal de segments pouvant être exportés à une heure donnée | 100 | Soft | La recommandation est d’ajouter un maximum de 100 segments aux flux de données de destination par lot. |
| Nombre maximum de lignes (enregistrements) par fichier à activer | 5 million | Hard | Adobe Experience Platform fractionne automatiquement les fichiers exportés à raison de 5 millions d’enregistrements (lignes) par fichier. Chaque ligne représente un profil. Les noms de fichiers fractionnés sont ajoutés avec un nombre indiquant que le fichier fait partie d’une exportation plus importante, comme : `filename.csv`, `filename_2.csv`, `filename_3.csv`. Pour plus d’informations, reportez-vous à la [section de planification](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) du tutoriel d’activation des destinations par lot. |

{style=&quot;table-layout:auto&quot;}

### Activation ad hoc {#ad-hoc-activation}

Les barrières de sécurité ci-dessous s’appliquent à la méthode d’[activation ad hoc](/help/destinations/api/ad-hoc-activation-api.md).

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Segments activés par traitement d’activation ad hoc | 80 | Hard | Actuellement, chaque traitement d’activation ad hoc peut activer jusqu’à 80 segments. Si vous tentez d’activer plus de 80 segments par traitement, celui-ci échouera. Ce comportement peut faire l’objet de modifications dans les prochaines versions. |
| Traitements d’activation ad hoc simultanés par segment | 1 | Hard | N’exécutez pas plusieurs traitements d’activation ad hoc simultanés par segment. |

{style=&quot;table-layout:auto&quot;}

### Activation des destinations de personnalisation Edge {#edge-destinations-activation}

Les barrières de sécurité ci-dessous s’appliquent à l’activation par le biais des [Destinations de personnalisation Edge](/help/destinations/destination-types.md#streaming-profile-export).

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre maximal de destinations de [Personnalisation personnalisée](/help/destinations/catalog/personalization/custom-personalization.md) | 10 | Soft | Vous pouvez configurer des flux de données vers 10 destinations de personnalisation personnalisée par sandbox. |
| Nombre maximal d’attributs mappés à une destination de personnalisation par sandbox | 20 | Hard | Un maximum de 20 attributs peuvent être mappés dans un flux de données à une destination de personnalisation, par sandbox. |
| Nombre maximal de segments mappés à une seule destination [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) | 50 | Soft | Vous pouvez activer un maximum de 50 segments dans un flux d’activation vers une seule destination Adobe Target. |

{style=&quot;table-layout:auto&quot;}

### Barrières de sécurité Destination SDK {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) est une suite dʼAPI de configuration permettant de configurer des modèles dʼintégration de destination, afin quʼExperience Platform puisse envoyer des données dʼaudience et de profil à votre point dʼentrée, selon les formats de données et dʼauthentification choisis. Les barrières de sécurité ci-dessous s’appliquent aux destinations que vous configurez à l’aide de Destination SDK.

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre maximal de [destinations personnalisées privées](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Soft | Vous pouvez créer un maximum de 5 destinations de diffusion en continu ou par lots privées à l’aide de Destination SDK. Contactez un représentant de l’assistance clientèle si vous devez créer plus de 5 destinations de ce type. |
| Politique d’exportation de profils pour Destination SDK | <ul><li>`maxBatchAgeInSecs` (1 800 au minimum et 3 600 au maximum)</li><li>`maxNumEventsInBatch` (1 000 au minimum, 10 000 au maximum)</li></ul> | Hard | Lors de l’utilisation de l’option [agrégation configurable](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation) pour votre destination, gardez à l’esprit les valeurs minimale et maximale qui déterminent la fréquence d’envoi des messages HTTP vers votre destination basée sur l’API et le nombre de profils que les messages doivent inclure. |

{style=&quot;table-layout:auto&quot;}

### Politique de limitation et de reprise des destinations {#destination-throttling-and-retry-policy}

Détails sur les seuils de limitations ou les limites pour des destinations données. Cette section fournit également des informations sur la politique de reprise pour les destinations.

| Type de destination | Description |
| --- | --- |
| Destinations Grands comptes (API HTTP, Kinesis Amazon, Azure EventHubs) | Dans 95 % des cas, Experience Platform tente d’offrir une latence de débit inférieure à 10 minutes pour les messages envoyés avec succès, avec un taux de moins de 10 000 demandes par seconde pour chaque flux de données vers une destination Grands comptes. <br> En cas d’échec des requêtes vers la destination de votre entreprise, Experience Platform stocke les requêtes ayant échoué et tente à deux reprises d’envoyer les requêtes à votre point d’entrée. |

{style=&quot;table-layout:auto&quot;}

## Barrières de sécurité pour les autres services Experience Platform {#guardrails-other-services}

Consultez les informations sur les barrières de sécurité pour d’autres services Experience Platform :

* Barrières de sécurité pour l’[ingestion des données](/help/ingestion/guardrails.md)
* Barrières de sécurité pour les [[!DNL Identity Service] données](/help/identity-service/guardrails.md)
* Barrières de sécurité pour les [[!DNL Real-time Customer Profile] données](/help/profile/guardrails.md)
* Barrières de sécurité pour les [[!DNL Query Service] données](/help/query-service/guardrails.md)