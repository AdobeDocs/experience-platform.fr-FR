---
keywords: Experience Platform;accueil;rubriques populaires;environnement de test;environnement de test;test
solution: Experience Platform
title: Présentation des environnements de test
description: Les environnements de test constituent des partitions virtuelles au sein d’une instance d’Experience Platform unique, ce qui permet une intégration transparente au processus de développement de vos applications d’expérience numérique.
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 86%

---

# Présentation des environnements de test

Adobe Experience Platform est conçu pour enrichir les applications d’expérience numérique à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience numérique en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle.

Pour répondre à ce besoin, Experience Platform fournit des environnements de test qui divisent une instance unique de Platform en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Ce document présente de manière générale les environnements de test dans Experience Platform.

## Fonctionnement des environnements de test

Les environnements de test constituent des partitions virtuelles au sein d’une instance d’Experience Platform unique, ce qui permet une intégration transparente au processus de développement de vos applications d’expérience numérique. Tout le contenu et les actions réalisés dans une sandbox sont limités à celle-ci et n’en affectent aucun autre. Deux types d’environnements de test sont pris en charge sur Experience Platform :

* **Sandbox de production** : une sandbox de production est conçue pour être utilisée avec des profils dans votre environnement de production. Platform vous permet de créer plusieurs sandbox de production afin de fournir les fonctionnalités appropriées aux données tout en maintenant l’isolation opérationnelle. Cette fonctionnalité vous permet de dédier des sandbox de production spécifiques à des secteurs d’activité, des marques, des projets ou des régions distincts. Les sandbox de production prennent en charge un volume de profils de production allant jusqu’à votre engagement sous licence de [!DNL Profile] (mesuré de manière cumulée sur toutes vos sandbox de production autorisées). Vous avez le droit d’utiliser un profil moyen sous licence par [!DNL Profile] autorisé (mesuré de manière cumulée sur toutes vos sandbox de production autorisées).
* **Sandbox de développement** : une sandbox de développement est une sandbox qui peut être utilisée exclusivement à des fins de développement et de test avec des profils hors production. Les sandbox de développement prennent en charge un volume de profils hors production pouvant atteindre 10 % de votre engagement sous licence de [!DNL Profile] (mesuré de manière cumulée sur toutes vos sandbox de développement autorisées). Vos droits incluent jusqu’à :
   * une richesse moyenne de profil hors production de 75 kilo-octets par profil hors production autorisé (mesurée de manière cumulative sur toutes vos sandbox de développement autorisées) ;
   * une tâche de segmentation par lots par jour, par sandbox de développement ;
   * une moyenne de 120 appels API [!DNL Profile], par [!DNL Profile], par an (mesurée de manière cumulée sur toutes vos sandbox de développement autorisées).

Une instance Experience Platform prend en charge plusieurs environnements de test de production et de développement, chaque environnement de test conservant sa propre bibliothèque indépendante de ressources Platform (y compris les schémas, les jeux de données, les profils, etc.). En outre, les environnements de test de production et de développement disposent d’une fonctionnalité de réinitialisation qui supprime de l’environnement de test toutes les ressources créées par les clients. Les environnements de test de développement ne peuvent pas être convertis en environnements de test de production.

Une licence Experience Platform par défaut vous accorde un total de cinq sandbox que vous pouvez classer en tant que production ou développement. Vous pouvez ajouter des packs de 10 sandbox jusquʼà un maximum de 75 sandbox au total. Ces environnements de test supplémentaires peuvent être utilisés pour créer des environnements de test de production et de développement. Contactez votre administrateur dʼorganisation IMS ou votre représentant commercial Adobe pour plus de détails.

Enfin, l’environnement de test de production par défaut est le premier environnement de test de production créé lors de la première création d’une organisation IMS. La sandbox de production par défaut vous permet d’ingérer ou d’utiliser des données de Platform, ainsi que d’accepter des requêtes qui n’incluent pas de valeurs pour un nom de sandbox ou un identifiant de sandbox.

>[!NOTE]
>
>Lorsqu’un environnement de test est créé pour la première fois, il ne contient aucune donnée. Puisque chaque environnement de test conserve sa propre banque de données isolée, ils doivent également tous ingérer leurs données de manière indépendante.

Pour résumer, les environnements de test offrent les avantages suivants :

* **Gestion du cycle de vie des applications** : créez des environnements virtuels distincts pour développer et faire évoluer des applications d’expérience numérique.
* **Gestion de projet et de marque** : permet à plusieurs projets de fonctionner en parallèle au sein de la même organisation IMS, tout en maintenant l’isolement et le contrôle d’accès. Les prochaines versions prendront en charge l’assistance au déploiement dans plusieurs régions.
* **Écosystème de développement flexible** : proposez des environnements de test de manière transparente, évolutive et économique pour l’exploration, l’activation et la démonstration.

## Contrôle d’accès pour les environnements de test

Par défaut, tous les utilisateurs d’une organisation ont accès à un environnement de test de production. L’accès aux environnements de test hors production doit être autorisé par un administrateur système, un administrateur de produit ou un administrateur de profil de produit au moyen d’[Adobe Admin Console](https://adminconsole.adobe.com).

Pour pouvoir visualiser, créer, mettre à jour ou supprimer des environnements de test hors production, les utilisateurs doivent également disposer de droits d’administration pour les environnements de test.

Pour plus d’informations sur la gestion des rôles et des autorisations pour les environnements de test, reportez-vous à la [présentation du contrôle d’accès](../access-control/home.md).

## Environnements de test dans l’interface utilisateur d’Experience Platform

Dans l’[interface utilisateur d’Experience Platform](https://platform.adobe.com), les utilisateurs peuvent basculer entre les environnements de test auxquels ils ont accès en utilisant le **sélecteur d’environnement de test** en haut à gauche de l’écran.  Les utilisateurs disposant de droits d’administration pour les environnements de test ont également accès à l’onglet **[!UICONTROL Environnements de test]** dans le volet de navigation de gauche, où ils peuvent visualiser et gérer des environnements de test pour leur organisation. Pour plus d’informations sur l’utilisation des environnements de test dans l’interface utilisateur, voir le [guide d’utilisation de l’environnement de test](ui/overview.md).

## Environnements de test dans les API Experience Platform

Lors d’appels aux API Experience Platform, un nom d’environnement de test doit être renseigné sous l’en-tête `x-sandbox-name`. Par exemple, lors d’un appel à la fonction [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) pour afficher tous les jeux de données dans l’environnement de test de production, le nom de l’environnement de test (&quot;prod&quot;) est fourni en tant qu’en-tête dans la requête API :

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: prod'
```

Si `x-sandbox-name` n’est pas inclus dans un appel API, le système utilisera un environnement de test par défaut à la place. Toutefois, la bonne pratique consiste à inclure systématiquement cet en-tête dans tous les appels API, même lorsque vous utilisez l’environnement de test par défaut. C’est pourquoi la documentation de l’API pour Experience Platform considère `x-sandbox-name` comme un en-tête obligatoire.

### API Sandbox

L’API Sandbox vous permet de gérer les environnements de test à l’aide des opérations de l’API RESTful. Consultez le [guide de développement des environnements de test](api/overview.md) pour obtenir des informations détaillées sur l’utilisation de l’API, notamment des requêtes correctement formatées et des exemples de réponses.

## Étapes suivantes

En lisant ce document, vous avez pris connaissance des concepts fondamentaux concernant les environnements de test dans Experience Platform. Pour obtenir des instructions détaillées sur la gestion des environnements de test, reportez-vous au [guide d’utilisation](ui/overview.md) pour l’interface utilisateur ou au [guide de développement](./api/getting-started.md) pour l’API.

Bien que les environnements de test constituent un outil précieux servant à isoler les environnements Platform pour votre équipe de développement, vous pouvez également gérer un contrôle d’accès plus granulaire à l’aide d’Adobe Admin Console. Pour plus d’informations, consultez la [présentation du contrôle d’accès](../access-control/home.md).
