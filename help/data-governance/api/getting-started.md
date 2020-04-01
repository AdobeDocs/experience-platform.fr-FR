---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide du développeur de l’API du service de stratégie DULE
topic: developer guide
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3

---


# Guide du développeur de l’API du service de stratégie DULE

L’étiquetage et l’application de l’utilisation des données (DULE) constituent le mécanisme de base de la gouvernance des données d’Adobe Experience Platform. Le service de stratégie DULE fournit une API RESTful qui vous permet de créer et de gérer des stratégies d’utilisation des données afin de déterminer quelles actions marketing peuvent être entreprises par rapport aux données qui ont été étiquetées avec certaines étiquettes d’utilisation des données.

Ce fournit des instructions sur l’exécution des opérations clés disponibles dans l’API du service de stratégie. Si vous ne l&#39;avez pas encore fait, veuillez commencer par passer en revue l&#39;aperçu [de la gouvernance des](../home.md) données afin de vous familiariser avec le cadre de DULE. Pour obtenir des instructions détaillées sur la création et l’application des stratégies DULE, consultez le didacticiel [sur les stratégies](../policies/create.md)DULE.

Ce présente les concepts de base que vous devez connaître avant d’effectuer des appels à l’API du service de stratégie.

## Prise en main de DULE Policy Service

Avant de commencer à travailler avec le service de stratégie, les données de la plateforme d’expérience doivent avoir des libellés DULE appropriés appliqués. Vous trouverez des instructions détaillées complètes pour appliquer des libellés d’utilisation des données aux jeux de données et aux champs dans le guide [d’utilisation des libellés](../labels/user-guide.md)DULE.

## Conditions préalables

Ce guide nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Gouvernance](../home.md)des données : Structure par laquelle la plateforme d’expérience applique la conformité à l’utilisation des données.
   * [Étiquettes](../labels/overview.md)DULE : Les libellés d’utilisation des données sont appliqués aux champs de données du modèle de données d’expérience (XDM), en spécifiant les restrictions d’accès à ces données.
* [Système](../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
* [](../../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.
* [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

## Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

## Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience, y compris celles qui appartiennent à la gouvernance des données, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

* Content-Type : application/json

## Ressources de base et personnalisées

Dans l’API du service de stratégie, toutes les stratégies et actions marketing sont appelées `core` ou `custom` ressources.

Les `core` ressources sont définies et gérées par Adobe, tandis que `custom` les ressources sont créées et gérées par des clients individuels. Elles sont donc uniques et visibles uniquement par l’organisation IMS qui les a créées. Ainsi, les opérations de liste et de recherche (`GET`) sont les seules opérations autorisées sur `core` les ressources, tandis que les opérations de liste, de recherche et de mise à jour (`POST`, `PUT`, `PATCH`et `DELETE`) sont disponibles pour `custom` les ressources.

## Statut de la stratégie

Les stratégies d’utilisation des données peuvent avoir l’un des trois états possibles : `DRAFT`, `ENABLED`ou `DISABLED`.

Par défaut, seules les stratégies &quot;ACTIVÉES&quot; participent à l’évaluation des stratégies.

Les stratégies &quot;BROUILLON&quot; peuvent également être prises en compte dans l’évaluation des stratégies, mais uniquement en définissant le paramètre  `?includeDraft=true`. Vous trouverez de plus amples renseignements sur l&#39;évaluation des politiques dans la section  sur l&#39;application [des](../enforcement/overview.md) politiques à la fin de cette .

## Noms des actions marketing {#marketing-actions}

Les noms d’action marketing sont des identifiants uniques pour les actions marketing. Chaque action `core` marketing a un nom unique qui s’applique à toutes les organisations IMS. Ces noms sont définis et maintenus par Adobe. En attendant, toutes les actions marketing définies par le client (`custom` ressources) sont uniques au sein de votre entreprise et ne sont ni visibles ni partagées avec d&#39;autres organisations IMS.

Les étapes de l’utilisation des actions marketing dans l’API de service de stratégie sont décrites dans la section Actions [](#marketing-actions) marketing de la suite de ce .

## Étapes suivantes

Maintenant que vous disposez des connaissances et des informations d’identification requises, vous pouvez continuer à lire les exemples d’appels d’API fournis dans ce guide du développeur :

* [Actions marketing](marketing-actions.md)
* [Stratégies](policies.md)