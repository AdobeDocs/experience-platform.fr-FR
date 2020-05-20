---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide du développeur de l'API DULE Policy Service
topic: developer guide
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---


# Guide du développeur de l&#39;API DULE Policy Service

L’étiquetage et l’application de l’utilisation des données (DULE) constituent le mécanisme de base de la gouvernance des données de la plate-forme Adobe Experience. Le service de stratégie DULE fournit une API RESTful qui vous permet de créer et de gérer des stratégies d’utilisation des données afin de déterminer quelles actions marketing peuvent être entreprises par rapport aux données qui ont été étiquetées avec certains libellés d’utilisation des données.

Ce document fournit des instructions sur l’exécution des opérations clés disponibles dans l’API Policy Service. Si vous ne l&#39;avez pas encore fait, veuillez commencer par examiner l&#39;aperçu [de la gouvernance des](../home.md) données afin de vous familiariser avec le cadre de DULE. Pour obtenir des instructions détaillées sur la création et l&#39;application de stratégies DULE, consultez le didacticiel [sur les stratégies](../policies/create.md)DULE.

Ce document présente les concepts de base que vous devez connaître avant de tenter d’appeler l’API de service de stratégie.

## Prise en main de DULE Policy Service

Avant de commencer à travailler avec Policy Service, les données de la plate-forme d’expérience doivent être associées à des libellés DULE appropriés. Vous trouverez des instructions détaillées complètes pour appliquer des étiquettes d’utilisation de données aux jeux de données et aux champs dans le guide [d’utilisation des étiquettes](../labels/user-guide.md)DULE.

## Conditions préalables

Ce guide nécessite une bonne compréhension des composants suivants d’Adobe Experience Platform :

* [Gouvernance](../home.md)des données : Cadre selon lequel la plate-forme d’expérience applique la conformité à l’utilisation des données.
   * [Étiquettes](../labels/overview.md)DULE : Les libellés d’utilisation des données sont appliqués aux champs de données du modèle de données d’expérience (XDM), en spécifiant les restrictions d’accès à ces données.
* [Système](../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
* [Profil](../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

## Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

## Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience, y compris celles appartenant à la gouvernance des données, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

* Content-Type : application/json

## Ressources de base et personnalisées

Dans l’API de service de stratégie, toutes les stratégies et actions marketing sont référencées comme des ressources `core` ou `custom` des ressources.

Les `core` ressources sont définies et gérées par Adobe, tandis que `custom` les ressources sont créées et gérées par des clients individuels et sont donc uniques et visibles uniquement par l’organisation IMS qui les a créées. Ainsi, les opérations d&#39;énumération et de recherche (`GET`) sont les seules opérations autorisées sur `core` les ressources, tandis que les opérations d&#39;énumération, de recherche et de mise à jour (`POST`, `PUT`, `PATCH`et `DELETE`) sont disponibles pour les `custom` ressources.

## Statut de la stratégie

Les stratégies d’utilisation des données peuvent avoir l’un des trois états possibles : `DRAFT`, `ENABLED`ou `DISABLED`.

Par défaut, seules les stratégies &quot;ACTIVÉES&quot; participent à l’évaluation des stratégies.

Les stratégies &quot;BROUILLON&quot; peuvent également être prises en compte dans l’évaluation des stratégies, mais uniquement en définissant le paramètre de requête `?includeDraft=true`. On trouvera de plus amples renseignements sur l&#39;évaluation des politiques dans la section du document sur l&#39;application [des](../enforcement/overview.md) politiques à la fin de ce document.

## Noms des actions marketing {#marketing-actions}

Les noms d’action marketing sont des identifiants uniques pour les actions marketing. Chaque action `core` marketing porte un nom unique qui s’applique à toutes les organisations IMS. Ces noms sont définis et conservés par Adobe. En attendant, toutes les actions marketing définies par le client (`custom` ressources) sont uniques au sein de votre organisation et ne sont ni visibles ni partagées avec d&#39;autres organisations IMS.

La procédure d’utilisation des actions marketing dans l’API de service de stratégie est décrite dans la section Actions [](#marketing-actions) marketing de la suite de ce document.

## Étapes suivantes

Maintenant que vous disposez des connaissances et des informations d’identification requises, vous pouvez continuer à lire les exemples d’appels d’API fournis dans ce guide du développeur :

* [Actions marketing](marketing-actions.md)
* [Stratégies](policies.md)