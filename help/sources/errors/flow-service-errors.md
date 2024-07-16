---
title: Messages d’erreur du service de flux
description: Prenez connaissance des messages d’erreur que vous pouvez rencontrer lors de l’utilisation du service de flux pour les sources.
exl-id: af79c547-25d0-459a-8de7-eb14206a8694
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 100%

---

# Messages d’erreur du service de flux

Le service de flux est utilisé pour collecter et centraliser les données client provenant de diverses sources dans Platform. Le service fournit une interface utilisateur et une API RESTful qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent d’authentifier vos systèmes tiers, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Ce document fournit une liste des messages d’erreur dans le service de flux, avec leur description et les résolutions possibles.

## Erreurs de validation internes dans le service de flux

Le tableau suivant décrit les erreurs de validation interne dans le service de flux.

| Code d’erreur | Titre | Message détaillé |
| --- | --- | --- |
| `1100-400` | Requête non valide | La requête n’a pas pu être traitée. Erreur du fournisseur de flux : cette opération n’est pas autorisée. |
| `1101-404` | Ressource introuvable | La ressource demandée est introuvable. Erreur du fournisseur de flux : la ressource avec l’ID donné n’existe pas. |
| `1102-500` | Erreur interne | Une erreur interne sʼest produite. Veuillez réessayer. Si le problème persiste, contactez l’assistance clientèle. |
| `1103-503` | Service indisponible | Le service est temporairement indisponible. Veuillez réessayer. Si le problème persiste, contactez l’assistance clientèle. |
| `1104-504` | Délai d’expiration de la passerelle | Un délai d’expiration de passerelle s’est produit. Veuillez réessayer. Si le problème persiste, contactez l’assistance clientèle. |
| `1400-500` | Erreur interne | Une erreur interne sʼest produite. Veuillez réessayer. Si le problème persiste, contactez l’assistance clientèle. |
| `1401-400` | Requête non valide | Les paramètres de limite et de nombre ne peuvent pas être présents au sein d’une même requête. Indiquez uniquement le paramètre de limite ou de nombre et réessayez. |
| `1402-400` | Requête non valide | L’action « finalize » n’est prise en charge que pour les requêtes de fournisseurs. |
| `1403-400` | En-tête manquant | L’en-tête « If-Match » est manquant dans la requête. Indiquez l’en-tête et réessayez. |
| `1404-412` | La version ne correspond pas | La version fournie « v1 » ne correspond pas à la version actuelle de l’entité « cc01fc2c-0000-0200 ». Assurez-vous que la version fournie correspond à la version actuelle de l’entité et réessayez. |
| `1405-400` | Requête non valide | Le corps de la requête ne peut pas être nul ou vide. Indiquez un corps de requête et réessayez. |
| `1406-400` | Requête non valide | La sous-opération « progress » ne peut pas être appliquée avec d’autres sous-opérations. Mettez à jour la liste des sous-opérations et réessayez. |
| `1407-400` | Requête non valide | Le statut d’échec ne peut pas être utilisé avec la sous-opération `progress`. Supprimez la sous-opération `progress` ou utilisez le statut « inProgress » et réessayez. |
| `1408-400` | Requête non valide | Le pourcentage d’achèvement doit être de 100 pour les statuts terminés ou en échec. Mettez à jour le pourcentage d’achèvement et réessayez. |
| `1409-400` | Requête non valide | L’opération « finalize » ne peut pas être appliquée au statut actuel « enabled-finalizing ». Mettez à jour l’opération et réessayez. |
| `1410-400` | Requête non valide | `State` n’est pas autorisé dans la requête de flux de création. |
| `1411-400` | Requête non valide | Impossible de récupérer « entityId ». Requête non valide reçue avec le chemin « baseConnections/123 ». |
| `1412-400` | Requête non valide | Version de mappage non valide dans la requête. Indiquez une version de mappage correcte. |
| `1413-400` | Requête non valide | L’identifiant de spécification fourni n’est pas valide. Indiquez un identifiant de spécification valide et réessayez. |
| `1414-400` | Requête non valide | Impossible de mettre à jour la spécification de connexion d’une connexion. |
| `1415-400` | Requête non valide | La spécification d’authentification « authConnection » est introuvable pour l’ID de spécification de connexion « ba6e206f-f233-ab16 ». |
| `1416-400` | Requête non valide | La suppression ou la mise à jour ne peuvent être appliquées que pour une connexion ayant l’état « enabled », « disabled » ou « initializing ». |
| `1417-400` | Requête non valide | La suppression ou mise à jour des connexions ayant l’état `initializing` ne sont pas autorisées avec UserToken. |
| `1418-400` | Requête non valide | La connexion de base avec l’ID « 35dcaad3-122a-4278 » ne peut pas être supprimée, car elle est utilisée dans un ou plusieurs flux. Assurez-vous que les flux correspondants sont supprimés avant de supprimer une connexion de base. |
| `1419-400` | Requête non valide | Erreur lors de la validation du mappage avec l’ID 45d90285d2d249acb87a72a2f12f7401, version 0. Cela peut être dû à des autorisations inadéquates sur les champs mappés. Vérifiez le mappage ou contactez l’administration. |
| `1420-400` | Requête non valide | L’état actuel « disabling » ne peut pas être mis à jour. |
| `1421-400` | Requête non valide | L’état actuel « updating » ne peut pas faire l’objet d’une transition. |
| `1422-400` | Requête non valide | L’action « disable » ne peut pas être appliquée à l’état actuel {state}. Mettez à jour l’action et réessayez. |
| `1423-400` | Requête non valide | Un champ baseSpec non géré a été fourni dans ConnectionSpecFiltering. Mettez à jour le champ {field} et réessayez. |
| `1424-400` | Requête non valide | OrderBy n’est pas pris en charge dans les requêtes entre sandbox. |
| `1425-400` | Requête non valide | Erreur lors de la correspondance entre le schéma du jeu de données cible 64ef1a3c0ef et le schéma du mappage 91ac5a2c0eb. Le schéma avec le même ID et la même version doit être utilisé dans le jeu de données de mappage et le jeu de données cible. |
| `1426-400` | Requête non valide | Le jeton utilisateur n’est pas autorisé à créer ou mettre à jour la spécification de connexion. Vérifiez que le jeton utilisateur dispose des autorisations nécessaires et réessayez. |
| `1427-400` | Requête non valide | Le jeton utilisateur n’est pas autorisé à créer ou mettre à jour les exécutions de flux. Vérifiez que le jeton utilisateur dispose des autorisations nécessaires et réessayez. |
| `1428-400` | Requête non valide | L’exécution du flux prédécesseur est introuvable avec l’identifiant aa6a206f-f233-4c2d. |
| `1429-400` | Requête non valide | Le flux prédécesseur est introuvable avec l’identifiant aa6a206f-f233-4c2d. |
| `1430-400` | Requête non valide | Le flux est introuvable avec l’identifiant aa6a206f-f233-4c2d. |
| `1431-400` | Requête non valide | Le tableau vide « fields » n’est pas autorisé dans la politique. |
| `1432-400` | Requête non valide | L’ordre de tri spécifié n’est pas correct. Ajoutez « + » pour l’ordre croissant et « - » pour l’ordre décroissant dans le champ Nom. |
| `1433-400` | Requête non valide | Champ incorrect= #id transmis dans orderBy. Les exemples sont +name, -name, name. |
| `1434-400` | Requête non valide | Opération « move » non prise en charge reçue. Utilisez l’un des types d’opérations pris en charge et réessayez. |
| `1435-400` | Requête non valide | Sous-action « reverse » non prise en charge reçue. Utilisez l’un des types de sous-actions pris en charge et réessayez. |
| `1436-400` | Requête non valide | Sous-opération « progress » non prise en charge reçue pour l’opération « enable ». |
| `1437-400` | Requête non valide | Valeur de statut « started » non prise en charge reçue. Mettez à jour la valeur de statut et réessayez. |
| `1438-400` | Requête non valide | Opération d’agrégat « average » non prise en charge reçue. |
| `1439-400` | Ressource introuvable | La ressource de flux demandée 3f4ae131-b384-4e73 est introuvable. Vérifiez l’ID de la ressource avant de réessayer. |
| `1440-400` | Requête non valide | L’opérateur « ~ » n’est pas implémenté. |
| `1441-400` | Requête non valide | La fonction d’agrégat « average » n’est pas implémentée. |
| `1442-400` | Requête non valide | L’agrégation n’est pas autorisée sur le champ id. |
| `1443-400` | Requête non valide | L’opérateur « &lt;= » n’est pas autorisé pour les valeurs multiples. |
| `1444-400` | Requête non valide | Le flux 3f4ae131-b384-4e73 n’est pas dans l’état prévu en attente. |
| `1445-400` | Requête non valide | Fonctionnalité de connexion PATCH non activée. |
| `1446-400` | Requête non valide | L’ID de flux ne peut pas être nul ou vide. Mettez à jour l’ID de flux et réessayez. |
| `1447-400` | Requête non valide | Flux actifs trouvés contenant l’ID aa6a206f-f233-4c2d. |
| `1448-400` | Requête non valide | Opérateur >= non pris en charge pour l’ID de champ. |
| `1449-400` | Requête non valide | Connexions de champs non valides dans les paramètres de filtre. |
| `1450-400` | Requête non valide | Opérateur non valide.> dans les paramètres de filtre. |
| `1451-400` | Requête non valide | Paramètres testParam non valides fournis dans les paramètres de requête. |
| `1452-400` | Requête non valide | Valeur non valide 1676643256,1676643210 pour le champ createdAt. |
| `1453-400` | Requête non valide | Valeur de requête non valide createdAt== fournie dans le paramètre de requête. |
| `1454-400` | Requête non valide | Type de valeur de filtre non géré fourni. |
| `1455-400` | Requête non valide | Une erreur s’est produite lors de la validation des instructions du correctif : champ manquant « keyWhichDoesNotExist ». |
| `1456-400` | Requête non valide | L’état supprimer-finalisation n’est pas une valeur valide. Les valeurs autorisées sont [activé, désactivé, initialisation]. |
| `1457-400` | Requête non valide | L’opération « Mettre à jour » ne peut pas être appliquée avec l’état supprimer-finalisation. |
| `1458-400` | Requête non valide | L’opération « Supprimer » ne peut pas être appliquée avec l’état supprimer-finalisation. |

{style="table-layout:auto"}


## Erreurs de vérification du jeton utilisateur pour autorisation

Le tableau suivant répertorie les erreurs concernant la vérification du jeton utilisateur pour autorisation.

| Code d’erreur | Titre | Message détaillé |
| --- | --- | --- |
| `2000-401` | Jeton d’autorisation non valide | Le jeton d’autorisation n’a pas accès à cette organisation ou l’organisation n’existe pas. Assurez-vous que l’organisation existe ou contactez votre administration pour y accéder. |
| `2001-401` | En-tête manquant ou vide | L’en-tête x-gw-ims-org-id est manquant ou vide. Mettez à jour la valeur de l’en-tête et réessayez. |
| `2002-401` | En-tête manquant | L’en-tête x-gw-ims-org-id est absent de la requête. Mettez à jour la valeur de l’en-tête et réessayez. |
| `2100-404` | Sandbox introuvable | La sandbox nommée « dev » est introuvable. Assurez-vous que le nom de la sandbox est correct et réessayez. |
| `2101-404` | Sandbox introuvable | La sandbox nommée « dev » est introuvable. Erreur provenant de l’API Sandbox Management : sandbox nommée « Dev » non présente. Vérifiez si la ressource existe. |
| `2102-500` | Erreur lors de l’obtention de la sandbox par nom | Un problème s’est produit lors de la récupération d’une sandbox nommée « Dev ». Erreur provenant de l’API Sandbox Management : une erreur s’est produite. Veuillez réessayer. |
| `2103-404` | Sandbox introuvable | La sandbox dont l’ID est 8da3ef09-b469-404a et le nom « dev » est introuvable. Assurez-vous que l’ID et le nom de la sandbox sont corrects, puis réessayez. |
| `2104-500` | Erreur lors de l’obtention de la sandbox par identifiant | Un problème s’est produit lors de la récupération d’une sandbox dont l’identifiant est « 8da3ef09-b469-404a » et le nom « dev ». Erreur provenant de l’API Sandbox Management : une erreur s’est produite. Veuillez réessayer. |
| `2105-400` | En-tête manquant | L’en-tête x-sandbox-name est absent de la requête. Ajoutez l’en-tête dans la requête et réessayez. |
| `2106-404` | Erreur lors de l’obtention de la sandbox par défaut | Les informations de la sandbox par défaut sont introuvables. |
| `2107-500` | Erreur lors de l’obtention de la sandbox par défaut | Un problème s’est produit lors de la récupération d’une sandbox par défaut. Erreur provenant de l’API Sandbox Management : une erreur s’est produite. Veuillez réessayer. |
| `2108-500` | Erreur lors de l’obtention des sandbox actives | Un problème s’est produit lors de la récupération d’une sandbox active. Erreur provenant de l’API Sandbox Management : une erreur s’est produite. Veuillez réessayer. |
| `2110-400` | En-têtes non autorisés | L’en-tête x-sandbox-id n’est pas autorisé avec le jeton utilisateur. Mettez à jour l’en-tête et réessayez. |
| `2111-403` | En-têtes avec valeur restreints | L’en-tête x-sandbox-name avec la valeur * est restreint au jeton utilisateur. Mettez à jour l’en-tête et la valeur, puis réessayez. |
| `2112-400` | En-têtes avec une valeur différente non autorisés | Les en-têtes x-sandbox-name et x-sandbox-id doivent tous deux avoir la valeur * pour la requête entre sandbox. Mettez à jour les en-têtes et réessayez. |
| `2113-400` | En-têtes avec valeur non autorisés | Les en-têtes x-sandbox-id et x-sandbox-name avec la valeur * ne sont pas autorisés pour la requête. Mettez à jour les en-têtes et réessayez. |
| `2114-400` | Jeton vide | Jeton vide fourni. Veuillez fournir un jeton et réessayer. |
| `2115-400` | Jeton non valide | Jeton non valide fourni. Veuillez fournir un jeton valide et réessayer. |
| `2116-500` | Erreur interne | Une erreur interne s’est produite lors du décodage hors ligne du jeton porteur pour la résolution de la portée. |
| `2117-500` | Erreur interne | Une erreur interne s’est produite lors de la vérification des autorisations de l’utilisateur ou de l’utilisatrice. Veuillez réessayer. Si le problème persiste, contactez l’assistance clientèle. |
| `2118-403` | Autorisation manquante | L’autorisation d’écriture est manquante. Contactez votre administration pour résoudre les problèmes d’autorisations et réessayez. |
| `2119-400` | Paramètre de requête manquant | Le contexte de requête ne contient pas le paramètre de requête requis specId. Indiquez le paramètre de requête manquant et réessayez. |
| `2120-403` | Interdit | Vous ne disposez pas des autorisations suffisantes pour effectuer l’opération. Contactez votre administration pour résoudre les problèmes d’autorisations et réessayez. |
| `2121-403` | Interdit | La gestion des autorisations est refusée sur la ressource Enterprise Source. Contactez votre administration pour résoudre les problèmes d’autorisations et réessayez. |
| `2200-500` | Erreur de requête de service externe | Un problème s’est produit lors de l’appel du Service de catalogue pour valider le schéma. |
| `2250-500` | Erreur de requête de service externe | Un problème s’est produit lors de l’appel du Service de préparation des données pour la validation du mappage. |

{style="table-layout:auto"}
