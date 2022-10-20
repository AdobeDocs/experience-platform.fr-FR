---
keywords: Experience Platform;activation;dépannage;garde-fous;conseils;limite
title: Barrières de sécurité par défaut pour les données d’activation
solution: Experience Platform
product: experience platform
type: Documentation
description: En savoir plus sur l’utilisation par défaut de l’activation des données et les limites de taux.
source-git-commit: 69496d2e00ce866413786160d4524cabd03ae350
workflow-type: tm+mt
source-wordcount: '1198'
ht-degree: 18%

---

# Barrières de sécurité pour les données d’activation

Cette page fournit les limites d’utilisation et de taux par défaut en ce qui concerne le comportement d’activation. Lors de la révision des barrières de sécurité suivantes, on suppose que vous avez correctement [connecté aux destinations](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* La plupart des clients ne dépassent pas ces limites par défaut. Si vous souhaitez en savoir plus sur les limites personnalisées, contactez votre représentant de l’assistance clientèle.
>* Les limites décrites dans ce document sont constamment améliorées. Consultez régulièrement les mises à jour.
>* Selon les limites individuelles en aval, certaines destinations peuvent avoir des barrières de sécurité plus strictes que celles documentées sur cette page. Veillez également à vérifier la variable [catalogue](/help/destinations/catalog/overview.md) de la destination à laquelle vous vous connectez et à laquelle vous activez des données.


## Types de limite {#limit-types}

Ce document comprend deux types de limites par défaut :

* **Limite soft :** il est possible d’aller au-delà d’une limite soft, cependant ces limites fournissent une orientation recommandée pour les performances du système.
* **Limite Hard :** une limite Hard fournit un maximum absolu. L’interface utilisateur ou l’API de l’Experience Platform ne vous permet pas d’aller au-delà de cette limite ou une erreur est renvoyée si vous dépassez cette limite.


## Limites d’activation {#activation-limits}

Les barrières de sécurité suivantes fournissent des limites recommandées lors de l’activation des données Real-time Customer Profile vers les destinations.

### Protections générales de l’activation {#general-activation-guardrails}

Les barrières de sécurité ci-dessous s’appliquent généralement à l’activation par le biais de [tous les types de destination](/help/destinations/destination-types.md#destination-types).

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre maximal de segments vers une seule destination | 250 | Soft | Il est recommandé de mapper un maximum de 250 segments à une seule destination dans un flux de données. <br><br> Si vous devez activer plus de 250 segments vers une destination, vous pouvez effectuer l’une des opérations suivantes : <ul><li> Annuler le mappage des segments que vous ne souhaitez plus activer ou</li><li>Créez un nouveau flux de données vers la destination souhaitée et mappez les segments à ce nouveau flux de données.</li></ul> <br> Notez que dans le cas de certaines destinations, vous pouvez être limité à moins de 250 segments mappés à la destination. Ces destinations sont répertoriées plus bas sur la page, dans leurs sections respectives. |
| Nombre maximal de destinations | 100 | Soft | Il est recommandé de créer un maximum de 100 destinations auxquelles vous pouvez vous connecter et activer des données. *par environnement de test*. [Destinations de personnalisation Edge (personnalisation personnalisée)](#edge-destinations-activation) peut représenter un maximum de 10 des 100 destinations recommandées. |
| Nombre maximal d’attributs mappés à une destination | 50 | Soft | Dans le cas de plusieurs destinations et types de destination, vous pouvez sélectionner des attributs de profil et des identités à mapper pour l’exportation. Pour des performances optimales, un maximum de 50 attributs doit être mappé dans un flux de données à une destination. |
| Type de données activées vers les destinations | Données de profil, y compris les identités et la carte des identités | Hard | Actuellement, il n&#39;est possible d&#39;exporter que *attributs d’enregistrement de profil* vers les destinations. Pour l’instant, les attributs XDM qui décrivent les données d’événement ne sont pas pris en charge pour l’exportation. |
| Type de données activées vers les destinations : prise en charge des attributs de tableau et de mappage | Non disponible | Hard | À l’heure actuelle, la variable **not** possible à exporter *Attributs de tableau ou de mappage* vers les destinations. L’exception à cette règle est la suivante : [identity map](/help/xdm/field-groups/profile/identitymap.md), qui est exporté à la fois dans les activations par flux et basées sur des fichiers. |

{style=&quot;table-layout:auto&quot;}

### Activation de la diffusion en continu {#streaming-activation}

Les barrières de sécurité ci-dessous s’appliquent à l’activation par le biais de [destinations de diffusion en continu](/help/destinations/ui/activate-segment-streaming-destinations.md).

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre d’activations (messages HTTP avec export de profils) par seconde | S/O | - | Il n’existe actuellement aucune limite au nombre de messages par seconde envoyés par Experience Platform aux points de terminaison de l’API des destinations partenaires. <br> Toutes les limites ou latences sont dictées par le point de terminaison où l’Experience Platform envoie des données. Veillez également à vérifier la variable [catalogue](/help/destinations/catalog/overview.md) de la destination à laquelle vous vous connectez et à laquelle vous activez des données. |

{style=&quot;table-layout:auto&quot;}

### Activation du lot (basé sur les fichiers) {#batch-file-based-activation}

Les barrières de sécurité ci-dessous s’appliquent à l’activation par le biais de [destinations par lot (basées sur des fichiers)](/help/destinations/ui/activate-batch-profile-destinations.md).

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Fréquence d&#39;activation | Exportation complète quotidienne ou exportation incrémentielle plus fréquente toutes les 3, 6, 8 ou 12 heures. | Hard | Lisez le [export des fichiers complets](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) et [export de fichiers incrémentiels](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) sections de documentation pour plus d’informations sur les incréments de fréquence pour les exportations par lots. |
| Nombre maximal de segments pouvant être exportés à une heure donnée | 100 | Soft | Il est recommandé d’ajouter un maximum de 100 segments aux flux de données de destination par lot. |
| Nombre maximum de lignes (enregistrements) par fichier à activer | 5 million | Hard | Adobe Experience Platform divise automatiquement les fichiers exportés à 5 millions d’enregistrements (lignes) par fichier. Chaque ligne représente un profil. Les noms de fichiers fractionnés sont ajoutés avec un nombre indiquant que le fichier fait partie d’une exportation plus importante, comme : `filename.csv`, `filename_2.csv`, `filename_3.csv`. Pour plus d’informations, reportez-vous à la section [section de planification](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) du tutoriel Activation des destinations par lot . |

{style=&quot;table-layout:auto&quot;}

### Activation ad hoc {#ad-hoc-activation}

Les barrières de sécurité ci-dessous s’appliquent au [activation ad hoc](/help/destinations/api/ad-hoc-activation-api.md) .

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Segments activés par tâche d’activation ad hoc | 80 | Hard | Actuellement, chaque tâche d’activation ad hoc peut activer jusqu’à 80 segments. Si vous tentez d’activer plus de 80 segments par tâche, la tâche échouera. Ce comportement peut être modifié dans les prochaines versions. |
| Tâches d’activation ad hoc simultanées par segment | 1 | Hard | N’exécutez pas plusieurs tâches d’activation ad hoc simultanées par segment. |

{style=&quot;table-layout:auto&quot;}

### Activation des destinations de personnalisation Edge {#edge-destinations-activation}

Les barrières de sécurité ci-dessous s’appliquent à l’activation par le biais de [Destinations de personnalisation de périphérie](/help/destinations/destination-types.md#streaming-profile-export).

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre maximal de [Personnalisation personnalisée](/help/destinations/catalog/personalization/custom-personalization.md) destinations | 10 | Soft | Vous pouvez configurer des flux de données vers 10 destinations de personnalisation personnalisées par environnement de test. |
| Nombre maximal d’attributs mappés à une destination de personnalisation par environnement de test | 20 | Hard | Un maximum de 20 attributs peuvent être mappés dans un flux de données à une destination de personnalisation, par environnement de test. |
| Nombre maximal de segments mappés à une seule [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) destination | 50 | Soft | Vous pouvez activer un maximum de 50 segments dans un flux d’activation vers une seule destination Adobe Target. |

{style=&quot;table-layout:auto&quot;}

### Barrières de sécurité de Destination SDK {#destination-sdk-guardrails}

[Le SDK Destination est un ensemble dʼAPI de configuration permettant de configurer des modèles dʼintégration de destination, afin quʼExperience Platform puisse envoyer des données dʼaudience et de profil à votre point dʼentrée, selon les formats de données et dʼauthentification choisis. ](/help/destinations/destination-sdk/overview.md) Les barrières de sécurité ci-dessous s’appliquent aux destinations que vous configurez à l’aide de Destination SDK.

| Barrière de sécurité | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre maximal de [destinations personnalisées privées](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Soft | Vous pouvez créer un maximum de 5 destinations de diffusion en continu ou par lots personnalisées à l’aide de Destination SDK. Contactez un représentant de l’assistance personnalisée si vous devez créer plus de 5 destinations de ce type. |
| Stratégie d’exportation de profils pour Destination SDK | <ul><li>`maxBatchAgeInSecs` (1 800 au minimum et 3 600 au maximum)</li><li>`maxNumEventsInBatch` (minimum 1 000, maximum 10 000)</li></ul> | Hard | Lors de l’utilisation de la variable [agrégation configurable](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation) pour votre destination, gardez à l’esprit les valeurs minimale et maximale qui déterminent la fréquence d’envoi des messages HTTP vers votre destination basée sur l’API et le nombre de profils que les messages doivent inclure. |

{style=&quot;table-layout:auto&quot;}

### Stratégie de ralentissement et de reprise des destinations {#destination-throttling-and-retry-policy}

Détails sur les seuils de ralentissement ou les limites pour des destinations données. Cette section fournit également des informations sur la stratégie de reprise pour les destinations.

| Type de destination | Description |
| --- | --- |
| Destinations d’entreprise (API HTTP, Kinesis Amazon, Azure EventHubs) | Dans 95 % des cas, l’Experience Platform tente d’offrir une latence de débit inférieure à 10 minutes pour les messages envoyés avec succès, avec un taux de moins de 10 000 demandes par seconde pour chaque flux de données vers une destination d’entreprise. <br> En cas d’échec des requêtes vers la destination de votre entreprise, Experience Platform stocke les requêtes ayant échoué et tente à deux reprises d’envoyer les requêtes à votre point de terminaison . |

{style=&quot;table-layout:auto&quot;}

## Barrières de sécurité pour les autres services Experience Platform {#guardrails-other-services}

Affichage des informations sur les barrières de sécurité pour d’autres services Experience Platform :

* Barrières de sécurité pour [ingestion de données](/help/ingestion/guardrails.md)
* Barrières de sécurité pour [[!DNL Identity Service] data](/help/identity-service/guardrails.md)
* Barrières de sécurité pour [[!DNL Real-time Customer Profile] data](/help/profile/guardrails.md)
* Barrières de sécurité pour [[!DNL Query Service] data](/help/query-service/guardrails.md)