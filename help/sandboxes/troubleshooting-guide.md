---
keywords: Experience Platform;accueil;rubriques populaires;dépannage sandbox
solution: Experience Platform
title: Guide de dépannage des sandbox
description: Ce document apporte des réponses aux questions fréquentes sur les sandbox dans Adobe Experience Platform.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: 7ee472294e8f255d9de3c15982a6f5d2d3654755
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 97%

---

# Guide de dépannage des sandbox

Ce document apporte des réponses aux questions fréquentes sur les sandbox dans Adobe Experience Platform. Pour les questions et le dépannage relatifs aux autres services Platform, consultez le [guide de dépannage d’Experience Platform](../landing/troubleshooting.md).

Les sandbox divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale. Pour plus d’informations, consultez la [Présentation des sandbox](home.md).

## Qu’est-ce qu’un sandbox ?

Les sandbox sont des partitions virtuelles au sein d’une instance unique d’Experience Platform. Chaque sandbox conserve sa propre bibliothèque indépendante de ressources Platform (qui comprend des schémas, des jeux de données, des profils, etc.). Tout le contenu et les actions réalisés dans un sandbox sont limités à celui-ci et n’en affectent aucun autre. Pour plus d’informations, consultez la [Présentation des sandbox](home.md).

## Quels sont les types de sandbox disponibles et quelles sont leurs différences ? {#sandbox-types}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtypes"
>title="Type de sandbox"
>abstract="Le type de sandbox indique s’il s’agit d’un sandbox de production ou de développement. Les sandbox de production incluent des données actives et les sandbox de développement sont utilisés pour les tests et le développement."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html?lang=fr#create" text="Création de sandbox dans l’interface utilisateur"

Deux types de sandbox sont disponibles dans Experience Platform :

* **Sandbox de production** : un sandbox de production est conçu pour être utilisé avec des profils dans votre environnement de production. Platform vous permet de créer plusieurs sandbox de production afin de fournir les fonctionnalités appropriées aux données tout en maintenant l’isolation opérationnelle. Cette fonctionnalité vous permet de dédier des sandbox de production spécifiques à des secteurs d’activité, des marques, des projets ou des régions distincts. Les sandbox de production prennent en charge un volume de profils de production allant jusqu’à votre engagement sous licence de [!DNL Profile] (mesuré de manière cumulée sur tous vos sandbox de production autorisés). Vous êtes autorisé à utiliser l’intégralité de votre volume de données total sous licence (mesuré de manière cumulée sur tous vos environnements de test de production autorisés).

* **Sandbox de développement** : un sandbox de développement est un sandbox qui peut être utilisé exclusivement à des fins de développement et de test avec des profils hors production. Les sandbox de développement prennent en charge un volume de profils hors production pouvant atteindre 10 % de votre engagement sous licence de [!DNL Profile] (mesuré de manière cumulée sur tous vos sandbox de développement autorisés). Vos droits incluent jusqu’à :
   * une tâche de segmentation par lots par jour, par sandbox de développement ;
   * une moyenne de 120 appels API [!DNL Profile], par [!DNL Profile], par an (mesurée de manière cumulée sur tous vos sandbox de développement autorisés).

Pour plus d’informations, consultez la [Présentation des sandbox](./home.md).

## Puis-je accéder à une ressource depuis plusieurs sandbox ?

Les sandbox sont des partitions isolées d’une instance Platform unique pour laquelle chaque sandbox conserve sa propre bibliothèque indépendante de ressources. Il n’est pas possible d’accéder à une ressource qui existe dans un sandbox depuis un autre sandbox, quel que soit le type de sandbox (production ou hors production).

## Quel est le sandbox de production par défaut ?

La sandbox de production par défaut est la première sandbox de production créée lorsqu’une organisation est configurée pour la première fois. Le sandbox de production par défaut vous permet d’ingérer ou d’utiliser des données de Platform, ainsi que d’accepter des requêtes qui n’incluent pas de valeurs pour un nom de sandbox ou un identifiant de sandbox. Le sandbox de production par défaut peut être réinitialisé, mais pas supprimé.

## De combien de sandbox de production puis-je disposer ?

Une instance Experience Platform prend en charge plusieurs sandbox de production et de développement. Chaque sandbox conserve sa propre bibliothèque indépendante de ressources Platform (y compris les schémas, les jeux de données et les profils).

Une licence Experience Platform par défaut vous accorde un total de cinq sandbox que vous pouvez classer en tant que production ou développement. Vous pouvez ajouter des packs de 10 sandbox jusquʼà 75 sandbox maximum au total.

Les sandbox de production peuvent être réinitialisés ou supprimés, à l’exception des sandbox de production également utilisés par Adobe Analytics pour la fonctionnalité [Analytics sur l’ensemble des appareils (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=fr), ou si le graphique d’identité qui y est hébergé est également utilisé par Adobe Audience Manager pour la fonctionnalité [Destinations basées sur les personnes (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=fr).

Vous pouvez mettre à jour le titre d’un sandbox de production. Cependant, un sandbox de production ne peut pas être renommé.

>[!NOTE]
>
>Le nom du sandbox est utilisé à des fins de recherche dans les appels API, tandis que le titre du sandbox est utilisé comme nom d’affichage.

## De combien de sandbox de développement puis-je disposer ?

Experience Platform autorise actuellement un maximum de 75 sandbox au total (de production et de développement) à être actives au sein d’une seule organisation.

Les sandbox de développement prennent en charge les fonctionnalités de réinitialisation et de suppression.

## Je viens de créer un sandbox. Comment puis-je définir des autorisations pour les utilisateurs qui travailleront avec ce sandbox ?

Adobe Admin Console lie les utilisateurs et utilisatrices aux sandbox et aux autorisations via l’utilisation de profils de produits. Après avoir créé un nouveau sandbox, rendez-vous dans l’onglet **Autorisations** du profil de produits auquel vous souhaitez accorder l’accès, puis cliquez sur **Sandbox**. De là, vous pouvez ajouter ou supprimer l’accès au nouveau sandbox de la même manière que pour les autres autorisations.

Si vous souhaitez ajouter des autorisations uniques aux utilisateurs d’un sandbox spécifique, vous pouvez avoir besoin de créer un nouveau profil de produits pour lequel vous aurez appliqué les sandbox et les autorisations appropriées et attribuez ces utilisateurs à ce profil.

Pour plus d’informations sur la gestion des sandbox et des autorisations dans Admin Console, consultez le [guide d’utilisation du contrôle d’accès](../access-control/ui/overview.md).
