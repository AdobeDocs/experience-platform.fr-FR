---
keywords: Experience Platform;accueil;rubriques les plus consultées;dépannage des environnements de test
solution: Experience Platform
title: Guide de dépannage des environnements de test
topic-legacy: troubleshooting guide
description: Ce document apporte des réponses aux questions fréquentes sur les environnements de test dans Adobe Experience Platform.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: 2a7b2040c221ff039f17f78d9ca712032d9fc02c
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 44%

---

# Guide de dépannage des environnements de test

Ce document apporte des réponses aux questions fréquentes sur les environnements de test dans Adobe Experience Platform. Pour les questions et le dépannage relatifs aux autres services Platform, consultez le [guide de dépannage d’Experience Platform](../landing/troubleshooting.md).

Les environnements de test divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique. Pour plus d’informations, consultez la [Présentation des environnements de test](home.md).

## Qu’est-ce qu’un environnement de test ?

Les environnements de test sont des partitions virtuelles au sein d’une instance unique d’Experience Platform. Chaque environnement de test conserve sa propre bibliothèque indépendante de ressources Platform (qui comprend des schémas, des jeux de données, des profils, etc.). Tout le contenu et les actions réalisés dans un environnement de test sont limités à celui-ci et n’en affectent aucun autre. Pour plus d’informations, consultez la [Présentation des environnements de test](home.md).

## Quels sont les types d’environnements de test disponibles et quelles sont leurs différences ?

Deux types d’environnements de test sont disponibles dans Experience Platform :

* **Environnement de test de production**: Un environnement de test de production est conçu pour être utilisé avec des profils dans votre environnement de production. Platform vous permet de créer plusieurs environnements de test de production afin de fournir les fonctionnalités appropriées aux données tout en maintenant l’isolation opérationnelle. Cette fonctionnalité vous permet de dédier des environnements de test de production spécifiques à des secteurs d’activité, des marques, des projets ou des régions distincts. Les environnements de test de production prennent en charge un volume de profils de production allant jusqu’à votre licence [!DNL Profile] engagement (mesuré de manière cumulée sur tous vos environnements de test de production autorisés). Vous avez le droit d’utiliser un profil de moyenne sous licence par autorisé [!DNL Profile] (mesuré de manière cumulée sur tous vos environnements de test de production autorisés).
* **Environnement de test de développement**: Un environnement de test de développement est un environnement de test qui peut être utilisé exclusivement à des fins de développement et de test avec des profils hors production. Les environnements de test de développement prennent en charge un volume de profils hors production pouvant atteindre 10 % de votre licence [!DNL Profile] engagement (mesuré de manière cumulée sur tous vos environnements de test de développement autorisés). Vous avez le droit de :
   * une richesse moyenne de profil hors production de 75 kilo-octets par profil hors production autorisé (mesurée de manière cumulative sur tous vos environnements de test de développement autorisés) ;
   * une tâche de segmentation par lots par jour, par environnement de test de développement ;
   * Une moyenne de 120 [!DNL Profile] appels API, par [!DNL Profile], par an (mesuré de manière cumulée sur tous vos environnements de développement autorisés).

Pour plus d’informations, consultez la [Présentation des environnements de test](./home.md).

## Puis-je accéder à une ressource depuis plusieurs environnements de test ?

Les environnements de test sont des partitions isolées d’une instance Platform unique pour laquelle chaque environnement de test conserve sa propre bibliothèque indépendante de ressources. Il n’est pas possible d’accéder à une ressource qui existe dans un environnement de test depuis un autre environnement de test, quel que soit le type d’environnement de test (production ou hors production).

## Quel est l’environnement de test de production par défaut ?

L’environnement de test de production par défaut est le premier environnement de test de production créé lorsqu’une organisation IMS est configurée pour la première fois. L’environnement de test de production par défaut vous permet d’ingérer ou d’utiliser des données de Platform, ainsi que d’accepter des requêtes qui n’incluent pas de valeurs pour un nom d’environnement de test ou un ID d’environnement de test. L’environnement de test de production par défaut peut être réinitialisé, mais pas supprimé.

## De combien d’environnements de test de production puis-je disposer ?

Une instance Experience Platform prend en charge plusieurs environnements de test de production et de développement, chaque environnement de test conservant sa propre bibliothèque indépendante de ressources Platform (y compris les schémas, les jeux de données et les profils).

Une licence d’Experience Platform par défaut vous accorde un total de cinq environnements de test que vous pouvez classer en tant que production ou développement. Vous pouvez attribuer une licence à des modules supplémentaires de 10 environnements de test, jusqu’à 75 environnements de test au total.

Les environnements de test de production peuvent être réinitialisés ou supprimés, à l’exception des environnements de test de production également utilisés par Adobe Analytics pour la variable [Analyses entre appareils (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=fr) ou si le graphique d’identités hébergé dans est également utilisé par Adobe Audience Manager pour la variable [Destinations basées sur les personnes (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=fr) fonction .

Vous pouvez mettre à jour le titre d’un environnement de test de production. Cependant, un environnement de test de production ne peut pas être renommé.

>[!NOTE]
>
>Le nom de l’environnement de test est utilisé à des fins de recherche dans les appels API, tandis que le titre de l’environnement de test est utilisé comme nom d’affichage.

## Combien d’environnements de test de développement puis-je avoir ?

Experience Platform permet actuellement à un maximum de 75 environnements de test (production et développement) d’être principaux au sein d’une seule organisation IMS.

Les environnements de test de développement prennent en charge les fonctionnalités de réinitialisation et de suppression.

## Je viens de créer un environnement de test. Comment puis-je définir des autorisations pour les utilisateurs qui travailleront avec cet environnement de test ?

Adobe Admin Console lie les utilisateurs aux environnements de test et aux autorisations via l’utilisation de profils de produits. Après avoir créé un nouvel environnement de test, rendez-vous dans l’onglet **Autorisations** du profil de produits auquel vous souhaitez accorder l’accès, puis cliquez sur **Environnements de test**. De là, vous pouvez ajouter ou supprimer l’accès au nouvel environnement de test de la même manière que pour les autres autorisations.

Si vous souhaitez ajouter des autorisations uniques aux utilisateurs d’un environnement de test spécifique, vous pouvez avoir besoin de créer un nouveau profil de produits pour lequel vous aurez appliqué les environnements de test et les autorisations appropriées et attribuez ces utilisateurs à ce profil.

Pour plus d’informations sur la gestion des environnements de test et des autorisations dans Admin Console, consultez le [guide d’utilisation du contrôle d’accès](../access-control/ui/overview.md).
