---
title: Messages d’erreur du service de flux
description: Découvrez les messages d’erreur que vous pouvez rencontrer lors de l’utilisation du service de flux pour les sources.
source-git-commit: 10edb5dfd9ce99b69cf5bb014f4903942c9bff3e
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 5%

---

# Messages d’erreur du service de flux

Le service de flux est utilisé pour collecter et centraliser des données client à partir de diverses sources disparates dans Platform. Le service fournit une interface utilisateur et une API RESTful qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent d’authentifier vos systèmes tiers, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Ce document fournit un catalogue de messages d’erreur, de descriptions et de suggestions de résolutions concernant le service de flux.

## Erreurs de validation internes dans le service de flux

Le tableau suivant décrit les erreurs concernant la validation interne dans le service de flux.

| Code d’erreur | Titre | Message détaillé |
| --- | --- | --- |
| `1100-400` | Requête non valide | La requête n’a pas pu être traitée. Erreur du fournisseur de flux : Non autorisé à cette opération. |
| `1101-404` | Ressource introuvable | La ressource demandée est introuvable. Erreur du fournisseur de flux : La ressource avec l’ID donné n’existe pas. |
| `1102-500` | Erreur interne | Une erreur interne s’est produite. Veuillez réessayer. Si le problème persiste, contactez le service clientèle. |
| `1103-503` | Service indisponible | Le service est temporairement indisponible. Veuillez réessayer. Si le problème persiste, contactez le service clientèle. |
| `1104-504` | Délai d’expiration de la passerelle | Un délai d’expiration de passerelle s’est produit. Veuillez réessayer. Si le problème persiste, contactez le service clientèle. |
| `1400-500` | Erreur interne | Une erreur interne s’est produite. Veuillez réessayer. Si le problème persiste, contactez le service clientèle. |
| `1401-400` | Requête non valide | Les paramètres limite et nombre ne peuvent pas être combinés dans une même requête. Indiquez uniquement la limite ou le paramètre count et réessayez. |
| `1402-400` | Requête non valide | L’action &quot;finalize&quot; est prise en charge uniquement pour les requêtes de fournisseur. |
| `1403-400` | En-tête manquant | L’en-tête &quot;If-Match&quot; est absent de la requête. Veuillez fournir l’en-tête et réessayer. |
| `1404-412` | La version ne correspond pas | La version fournie &#39;v1&#39; ne correspond pas à la version actuelle sur l’entité &#39;cc01fc2c-0000-0200&#39;. Assurez-vous que la version fournie correspond à la version actuelle de l’entité et réessayez. |
| `1405-400` | Requête non valide | Le corps de la requête ne peut pas être nul ou vide. Veuillez fournir un corps de requête et réessayer. |
| `1406-400` | Requête non valide | La sous-opération &quot;progress&quot; ne peut pas être appliquée à d&#39;autres sous-opérations. Mettez à jour la liste des sous-opérations et réessayez. |
| `1407-400` | Requête non valide | L’état d’échec ne peut pas être utilisé avec la variable `progress` subOp. Supprimez la variable `progress` subOp ou utilisez status=&#39;inProgress&#39; et réessayez. |
| `1408-400` | Requête non valide | Le pourcentage d’achèvement doit être de 100 pour les états terminés ou non. Veuillez mettre à jour le pourcentage de données terminées et réessayer. |
| `1409-400` | Requête non valide | L’opération &quot;finalize&quot; ne peut pas être appliquée à l’état actuel activé-finalizing. Mettez à jour l’opération et réessayez. |
| `1410-400` | Requête non valide | `State` n’est pas autorisé dans la requête de flux de création. |
| `1411-400` | Requête non valide | Impossible de récupérer entityId. Requête non valide reçue avec le chemin &#39;baseConnections/123&#39;. |
| `1412-400` | Requête non valide | Version de mappage non valide dans la requête. Veuillez fournir une version de mappage correcte. |
| `1413-400` | Requête non valide | L’identifiant de spécification fourni n’est pas valide. Indiquez un identifiant de spécification valide et réessayez. |
| `1414-400` | Requête non valide | La spécification de connexion d’une connexion ne peut pas être mise à jour. |
| `1415-400` | Requête non valide | La spécification d’authentification &quot;authConnection&quot; est introuvable pour l’ID de spécification de connexion ba6e206f-f233-ab16. |
| `1416-400` | Requête non valide | La suppression ou la mise à jour ne peuvent être appliquées que pour une connexion avec l’état activé, désactivé ou initialisé. |
| `1417-400` | Requête non valide | Suppression ou mise à jour des connexions dans `initializing` Les états ne sont pas autorisés avec UserToken. |
| `1418-400` | Requête non valide | La connexion de base avec l’ID 35dcaad3-122a-4278 ne peut pas être supprimée, car la connexion de base est utilisée dans un ou plusieurs flux. Assurez-vous que les flux correspondants sont supprimés avant de supprimer une connexion de base. |
| `1419-400` | Requête non valide | Erreur lors de la validation du mapping avec l’id 45d90285d2d249acb87a72a2f12f7401, version 0. Cela peut être dû à des autorisations inadéquates sur les champs mappés. Vérifiez votre mapping ou contactez votre administrateur. |
| `1420-400` | Requête non valide | La désactivation de l’état actuel ne peut pas être mise à jour. |
| `1421-400` | Requête non valide | La mise à jour de l’état actuel ne peut pas être transitoire. |
| `1422-400` | Requête non valide | L’action disable ne peut pas être appliquée à l’état actuel {state}. Mettez à jour l’action et réessayez. |
| `1423-400` | Requête non valide | Un champ baseSpec non géré a été fourni dans ConnectionSpecFiltering. Mettez à jour le champ {field} et réessayez. |
| `1424-400` | Requête non valide | OrderBy n’est pas pris en charge avec la requête cross-sandbox. |
| `1425-400` | Requête non valide | Erreur lors de la correspondance du schéma dans le jeu de données cible 64ef1a3c0ef avec le schéma dans le mappage 91ac5a2c0eb. Le schéma avec le même ID et la même version doit être utilisé dans le mappage et le jeu de données cible. |
| `1426-400` | Requête non valide | Le jeton utilisateur n’est pas autorisé à créer/mettre à jour la spécification de connexion. Vérifiez que le jeton utilisateur est autorisé et réessayez. |
| `1427-400` | Requête non valide | Le jeton utilisateur n’est pas autorisé à créer/mettre à jour des exécutions de flux. Vérifiez que le jeton utilisateur est autorisé et réessayez. |
| `1428-400` | Requête non valide | L’exécution du flux du prédécesseur est introuvable avec l’identifiant aa6a206f-f233-4c2d. |
| `1429-400` | Requête non valide | Flux de prédécesseur introuvable avec l’identifiant aa6a206f-f233-4c2d. |
| `1430-400` | Requête non valide | Flux introuvable avec l’identifiant aa6a206f-f233-4c2d. |
| `1431-400` | Requête non valide | Les &quot;champs&quot; de tableau vide ne sont pas autorisés dans la stratégie. |
| `1432-400` | Requête non valide | L’ordre de tri spécifié n’est pas correct, ajoutez + pour l’ordre croissant et - pour l’ordre décroissant dans le champName. |
| `1433-400` | Requête non valide | Champ incorrect= #id transmis dans orderBy, par exemple sont +name, -name, name. |
| `1434-400` | Requête non valide | Opération &quot;move&quot; non prise en charge reçue. Utilisez l’un des types d’opérations pris en charge et réessayez. |
| `1435-400` | Requête non valide | La sous-action &quot;reverse&quot; non prise en charge a été reçue. Utilisez l’un des types de sous-actions pris en charge et réessayez. |
| `1436-400` | Requête non valide | Activation de la sous-opération non prise en charge PROGRESS reçue pour l’opération. |
| `1437-400` | Requête non valide | La valeur d’état &quot;started&quot; non prise en charge a été reçue. Mettez à jour la valeur d’état et réessayez. |
| `1438-400` | Requête non valide | Opération d’agrégat non prise en charge &#39;average&#39; reçue. |
| `1439-400` | Ressource introuvable | La ressource de flux demandée 3f4ae131-b384-4e73 est introuvable. Vérifiez l’ID de la ressource avant de réessayer. |
| `1440-400` | Requête non valide | L’opérateur &#39;~&#39; n’est pas implémenté. |
| `1441-400` | Requête non valide | Fonction d’agrégation &#39;average&#39; non implémentée. |
| `1442-400` | Requête non valide | Agrégation non autorisée sur l’identifiant du champ. |
| `1443-400` | Requête non valide | L’opérateur &#39;&lt;=&#39; n’est pas autorisé pour les valeurs multiples. |
| `1444-400` | Requête non valide | Le flux 3f4ae131-b384-4e73 n’est pas dans l’état prévu en attente. |
| `1445-400` | Requête non valide | Fonctionnalité de connexion du PATCH non activée. |
| `1446-400` | Requête non valide | L’ID de flux ne peut pas être nul ou vide. Mettez à jour l’ID de flux et réessayez. |
| `1447-400` | Requête non valide | Flux principal trouvé contenant l’identifiant aa6a206f-f233-4c2d. |
| `1448-400` | Requête non valide | Opérateur >= non pris en charge pour l’identifiant de champ. |
| `1449-400` | Requête non valide | Connexions de champs non valides dans les paramètres de filtre. |
| `1450-400` | Requête non valide | Opérateur non valide !> dans les paramètres de filtre. |
| `1451-400` | Requête non valide | Params testParam non valide fourni dans les paramètres de requête. |
| `1452-400` | Requête non valide | Valeur non valide 1676643256,1676643210 pour le champ createdAt. |
| `1453-400` | Requête non valide | Valeur de requête non valide createdAt== fournie dans le paramètre de requête. |
| `1454-400` | Requête non valide | Type de valeur de filtre non géré fourni. |
| `1455-400` | Requête non valide | Une erreur s’est produite lors de la validation des instructions de correctif : Champ manquant &quot;keyWhatDoesNotExist&quot;. |
| `1456-400` | Requête non valide | La suppression d’état-finalisation n’est pas une valeur valide. Les valeurs autorisées sont [activé, désactivé, initialisation]. |
| `1457-400` | Requête non valide | La mise à jour de l’opération ne peut pas être appliquée lors de la suppression et de la finalisation de l’état. |
| `1458-400` | Requête non valide | La suppression de l’opération ne peut pas être appliquée dans la finalisation de la suppression de l’état. |

{style="table-layout:auto"}


## Erreurs de vérification du jeton utilisateur pour l’autorisation

Le tableau suivant répertorie les erreurs concernant la vérification du jeton utilisateur pour autorisation.

| Code d’erreur | Titre | Message détaillé |
| --- | --- | --- |
| `2000-401` | Jeton d’autorisation non valide | Le jeton d’autorisation n’a pas accès à cette organisation ou l’organisation n’existe pas. Assurez-vous que l’organisation existe ou contactez votre administrateur pour y accéder. |
| `2001-401` | En-tête manquant ou vide | L’en-tête x-gw-ims-org-id est manquant ou vide. Mettez à jour la valeur de l’en-tête et réessayez. |
| `2002-401` | En-tête manquant | L’en-tête x-gw-ims-org-id est absent de la requête. Mettez à jour la valeur de l’en-tête et réessayez. |
| `2100-404` | Sandbox introuvable | L’environnement de test nommé &quot;dev&quot; est introuvable. Assurez-vous que le nom de l’environnement de test est correct et réessayez. |
| `2101-404` | Sandbox introuvable | L’environnement de test nommé &quot;dev&quot; est introuvable. Erreur provenant de l’API Sandbox Management : Environnement de test nommé &quot;dev&quot; non présent. Vérifiez si la ressource existe. |
| `2102-500` | Obtenir l’environnement de test par nom | Un problème s’est produit lors de la récupération d’un environnement de test nommé &quot;dev&quot;. Erreur provenant de l’API Sandbox Management : Quelque chose s&#39;est mal passé. Veuillez réessayer. |
| `2103-404` | Sandbox introuvable | L’environnement de test avec l’ID 8da3ef09-b469-404a et le nom dev est introuvable. Assurez-vous que les valeurs d’ID et de nom de l’environnement de test sont correctes, puis réessayez. |
| `2104-500` | Obtention d’un environnement de test par erreur d’identifiant | Un problème s’est produit lors de la récupération d’un environnement de test avec l’identifiant &quot;8da3ef09-b469-404a&quot; et le nom &quot;dev&quot;. Erreur provenant de l’API Sandbox Management : Quelque chose s&#39;est mal passé. Veuillez réessayer. |
| `2105-400` | En-tête manquant | L’en-tête x-sandbox-name est absent de la requête. Ajoutez l’en-tête dans la requête et réessayez. |
| `2106-404` | Obtention de l’erreur sandbox par défaut | Les informations de l’environnement de test par défaut sont introuvables. |
| `2107-500` | Obtention de l’erreur sandbox par défaut | Un problème s’est produit lors de la récupération d’un environnement de test par défaut. Erreur provenant de l’API Sandbox Management : Quelque chose s&#39;est mal passé. Veuillez réessayer. |
| `2108-500` | Obtention de l’erreur principal des environnements de test | Un problème s’est produit lors de la récupération d’un principal environnement de test. Erreur provenant de l’API Sandbox Management : Quelque chose s&#39;est mal passé. Veuillez réessayer. |
| `2110-400` | En-têtes non autorisés | L’en-tête x-sandbox-id n’est pas autorisé avec le jeton utilisateur. Mettez à jour l’en-tête et réessayez. |
| `2111-403` | En-têtes avec valeur limitée | L’en-tête x-sandbox-name avec la valeur * est limité au jeton utilisateur. Mettez à jour l’en-tête et la valeur, puis réessayez. |
| `2112-400` | En-têtes avec une valeur différente non autorisés | Les en-têtes x-sandbox-name et x-sandbox-id doivent tous deux avoir la valeur * pour la requête cross sandbox. Mettez à jour les en-têtes et réessayez. |
| `2113-400` | En-têtes avec valeur non autorisés | Les en-têtes x-sandbox-id et x-sandbox-name avec la valeur * ne sont pas autorisés pour la requête. Mettez à jour les en-têtes et réessayez. |
| `2114-400` | Jeton vide | Jeton vide fourni. Veuillez fournir un jeton et réessayer. |
| `2115-400` | Jeton non valide | Jeton non valide fourni. Veuillez fournir un jeton valide et réessayer. |
| `2116-500` | Erreur interne | Une erreur interne s’est produite lors du décodage hors ligne du jeton porteur pour la résolution de la portée. |
| `2117-500` | Erreur interne | Une erreur interne s’est produite lors de la vérification des autorisations de l’utilisateur. Veuillez réessayer. Si le problème persiste, contactez le service clientèle. |
| `2118-403` | Permission manquante | L&#39;écriture de permission est manquante. Contactez votre administrateur pour résoudre les problèmes d’autorisations et réessayez. |
| `2119-400` | Paramètre de requête manquant | Le contexte de requête ne contient pas le paramètre de requête requis specId. Indiquez le paramètre de requête manquant et réessayez. |
| `2120-403` | Interdit | Vous ne disposez pas des autorisations suffisantes pour effectuer l’opération. Contactez votre administrateur pour résoudre les problèmes d’autorisations et réessayez. |
| `2121-403` | Interdit | La gestion des autorisations est refusée sur la ressource Enterprise Source. Contactez votre administrateur pour résoudre les problèmes d’autorisations et réessayez. |
| `2200-500` | Erreur de demande de service externe | Un problème s’est produit lors de l’appel du service Catalog pour valider le schéma. |
| `2250-500` | Erreur de demande de service externe | Un problème s’est produit lors de l’appel du service Data Prep pour valider le mappage. |

{style="table-layout:auto"}
