---
keywords: Experience Platform;accueil;rubriques populaires;sandbox;Sandbox;test;Test
solution: Experience Platform
title: Présentation des sandbox
description: Les sandbox constituent des partitions virtuelles au sein d’une instance d’Experience Platform unique, ce qui permet une intégration transparente au processus de développement de vos applications d’expérience digitale.
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 81%

---

# Présentation des sandbox

Adobe Experience Platform est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle.

Pour répondre à ce besoin, Experience Platform fournit des sandbox qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Ce document présente de manière générale les sandbox dans Experience Platform.

## Fonctionnement des sandbox

Les sandbox constituent des partitions virtuelles au sein d’une instance d’Experience Platform unique, ce qui permet une intégration transparente au processus de développement de vos applications d’expérience digitale. Tout le contenu et les actions réalisés dans un sandbox sont limités à celui-ci et n’en affectent aucun autre. Deux types de sandbox sont pris en charge sur Experience Platform :

* **Sandbox de production** : un sandbox de production est conçu pour être utilisé avec des profils dans votre environnement de production. Experience Platform vous permet de créer plusieurs sandbox de production afin de fournir les fonctionnalités appropriées aux données tout en maintenant l’isolation opérationnelle. Cette fonctionnalité vous permet de dédier des sandbox de production spécifiques à des secteurs d’activité, des marques, des projets ou des régions distincts. Les sandbox de production prennent en charge un volume de profils de production allant jusqu’à votre engagement sous licence de [!DNL Profile] (mesuré de manière cumulée sur tous vos sandbox de production autorisés). Vous avez le droit d’utiliser l’intégralité du volume total de données sous licence (mesuré de manière cumulée sur tous vos sandbox de production autorisés).

* **Sandbox de développement** : un sandbox de développement est un sandbox qui peut être utilisé exclusivement à des fins de développement et de test avec des profils hors production. Les sandbox de développement prennent en charge un volume de profils hors production pouvant atteindre 10 % de votre engagement sous licence de [!DNL Profile] (mesuré de manière cumulée sur tous vos sandbox de développement autorisés). Vos droits incluent jusqu’à :
   * une tâche de segmentation par lots par jour, par sandbox de développement ;
   * une moyenne de 120 appels API [!DNL Profile], par [!DNL Profile], par an (mesurée de manière cumulée sur tous vos sandbox de développement autorisés).

Une instance Experience Platform prend en charge plusieurs sandbox de production et de développement. Chaque sandbox conserve sa propre bibliothèque indépendante de ressources Experience Platform (y compris les schémas, les jeux de données, les profils, etc.). En outre, les sandbox de production et de développement disposent tous d’une fonctionnalité de réinitialisation supprimant toutes les ressources créées par les clients du sandbox. Les sandbox de développement ne peuvent pas être convertis en sandbox de production.

Une licence Experience Platform par défaut vous accorde un total de cinq sandbox que vous pouvez classer en tant que production ou développement. Vous pouvez ajouter des packs de 10 sandbox jusquʼà 75 sandbox maximum au total. Ces sandbox supplémentaires peuvent être utilisés pour créer des sandbox de production et de développement. Veuillez contacter l’administration de votre organisation ou le service commercial d’Adobe pour plus de détails.

Enfin, la sandbox de production par défaut est la première sandbox de production créée lorsqu’une organisation est configurée pour la première fois. Le sandbox de production par défaut vous permet d’ingérer ou d’utiliser des données d’Experience Platform, ainsi que d’accepter des requêtes qui n’incluent pas de valeurs pour un nom de sandbox ou un identifiant de sandbox.

>[!NOTE]
>
>Lorsqu’un sandbox est créé pour la première fois, il ne contient aucune donnée. Puisque chaque sandbox conserve sa propre banque de données isolée, ils doivent également tous ingérer leurs données de manière indépendante.

Pour résumer, les sandbox offrent les avantages suivants :

* **Gestion du cycle de vie des applications** : créez des environnements virtuels distincts pour développer et faire évoluer des applications d’expérience digitale.
* **Gestion de projet et de marque** : permet à plusieurs projets de fonctionner en parallèle au sein de la même organisation, tout en maintenant l’isolement et le contrôle d’accès.
* **Écosystème de développement flexible** : proposez des sandbox de manière transparente, évolutive et économique pour l’exploration, l’activation et la démonstration.

## Contrôle d’accès pour les sandbox

Par défaut, tous les utilisateurs d’une organisation ont accès à un sandbox de production. L’accès aux sandbox hors production doit être autorisé par un administrateur système, un administrateur de produit ou un administrateur de profil de produit au moyen d’[Adobe Admin Console](https://adminconsole.adobe.com).

Pour pouvoir visualiser, créer, mettre à jour ou supprimer des sandbox hors production, les utilisateurs doivent également disposer de droits d’administration pour les sandbox.

Pour plus d’informations sur la gestion des rôles et des autorisations pour les sandbox, reportez-vous à la [présentation du contrôle d’accès](../access-control/home.md).

## Sandbox dans l’interface utilisateur d’Experience Platform

Dans l’[interface utilisateur d’Experience Platform](https://platform.adobe.com), les utilisateurs peuvent basculer entre les sandbox auxquels ils ont accès en utilisant le **sélecteur de sandbox** en haut à gauche de l’écran.  Les utilisateurs disposant de droits d’administration pour les sandbox ont également accès à l’onglet **[!UICONTROL Sandbox]** dans le volet de navigation de gauche, où ils peuvent visualiser et gérer des sandbox pour leur organisation. Pour plus d’informations sur l’utilisation des sandbox dans l’interface utilisateur, voir le [guide d’utilisation du sandbox](ui/overview.md).

## Sandbox dans les API Experience Platform

Lors d’appels aux API Experience Platform, un nom de sandbox doit être renseigné sous l’en-tête `x-sandbox-name`. Par exemple, lors d’un appel à l’[[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) pour visualiser tous les jeux de données dans le sandbox de production, le nom du sandbox (« prod ») est renseigné comme en-tête dans la requête API :

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: prod'
```

Si `x-sandbox-name` n’est pas inclus dans un appel API, le système utilisera un sandbox par défaut à la place. Toutefois, la bonne pratique consiste à inclure systématiquement cet en-tête dans tous les appels API, même lorsque vous utilisez le sandbox par défaut. C’est pourquoi la documentation de l’API pour Experience Platform considère `x-sandbox-name` comme un en-tête obligatoire.

### API Sandbox

L’API Sandbox vous permet de gérer les sandbox à l’aide des opérations de l’API RESTful. Consultez le [guide de développement des sandbox](api/overview.md) pour obtenir des informations détaillées sur l’utilisation de l’API, notamment des requêtes correctement formatées et des exemples de réponses.

## Étapes suivantes

En lisant ce document, vous avez pris connaissance des concepts fondamentaux concernant les sandbox dans Experience Platform. Pour obtenir des instructions détaillées sur la gestion des sandbox, reportez-vous au [guide d’utilisation](ui/overview.md) pour l’interface utilisateur ou au [guide de développement](./api/getting-started.md) pour l’API.

Bien que les sandbox constituent un outil précieux permettant d’isoler les environnements Experience Platform pour votre équipe de développement, vous pouvez également gérer un contrôle d’accès plus granulaire à l’aide de Adobe Admin Console. Pour plus d’informations, consultez la [présentation du contrôle d’accès](../access-control/home.md).
