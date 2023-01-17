---
keywords: Experience Platform;accueil;rubriques populaires;dépannage sandbox
solution: Experience Platform
title: Guide de dépannage des sandbox
description: Ce document apporte des réponses aux questions fréquentes sur les sandbox dans Adobe Experience Platform.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: ht
source-wordcount: '857'
ht-degree: 100%

---

# Guide de dépannage des sandbox

Ce document apporte des réponses aux questions fréquentes sur les sandbox dans Adobe Experience Platform. Pour les questions et le dépannage relatifs aux autres services Platform, consultez le [guide de dépannage d’Experience Platform](../landing/troubleshooting.md).

Les sandbox divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique. Pour plus d’informations, consultez la [Présentation des sandbox](home.md).

## Qu’est-ce qu’une sandbox ?

Les sandbox sont des partitions virtuelles au sein d’une instance unique d’Experience Platform. Chaque sandbox conserve sa propre bibliothèque indépendante de ressources Platform (qui comprend des schémas, des jeux de données, des profils, etc.). Tout le contenu et les actions réalisés dans une sandbox sont limités à celle-ci et n’en affectent aucun autre. Pour plus d’informations, consultez la [Présentation des sandbox](home.md).

## Quels sont les types de sandbox disponibles et quelles sont leurs différences ? {#sandbox-types}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtypes"
>title="Type de sandbox"
>abstract="Le type de sandbox indique s’il s’agit d’une sandbox de production ou de développement. Les sandbox de production incluent des données actives et les sandbox de développement sont utilisées pour les tests et le développement."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html?lang=fr#create" text="Création de sandbox dans l’interface utilisateur"

Deux types de sandbox sont disponibles dans Experience Platform :

* **Sandbox de production** : une sandbox de production est conçue pour être utilisée avec des profils dans votre environnement de production. Platform vous permet de créer plusieurs sandbox de production afin de fournir les fonctionnalités appropriées aux données tout en maintenant l’isolation opérationnelle. Cette fonctionnalité vous permet de dédier des sandbox de production spécifiques à des secteurs d’activité, des marques, des projets ou des régions distincts. Les sandbox de production prennent en charge un volume de profils de production allant jusqu’à votre engagement sous licence de [!DNL Profile] (mesuré de manière cumulée sur toutes vos sandbox de production autorisées). Vous avez le droit d’utiliser un profil moyen sous licence par [!DNL Profile] autorisé (mesuré de manière cumulée sur toutes vos sandbox de production autorisées).
* **Sandbox de développement** : une sandbox de développement est une sandbox qui peut être utilisée exclusivement à des fins de développement et de test avec des profils hors production. Les sandbox de développement prennent en charge un volume de profils hors production pouvant atteindre 10 % de votre engagement sous licence de [!DNL Profile] (mesuré de manière cumulée sur toutes vos sandbox de développement autorisées). Vos droits incluent jusqu’à :
   * une richesse moyenne de profil hors production de 75 kilo-octets par profil hors production autorisé (mesurée de manière cumulative sur toutes vos sandbox de développement autorisées) ;
   * une tâche de segmentation par lots par jour, par sandbox de développement ;
   * une moyenne de 120 appels API [!DNL Profile], par [!DNL Profile], par an (mesurée de manière cumulée sur toutes vos sandbox de développement autorisées).

Pour plus d’informations, consultez la [Présentation des sandbox](./home.md).

## Puis-je accéder à une ressource depuis plusieurs sandbox ?

Les environnements de test sont des partitions isolées d’une instance Platform unique pour laquelle chaque sandbox conserve sa propre bibliothèque indépendante de ressources. Il n’est pas possible d’accéder à une ressource qui existe dans un environnement de test depuis une autre sandbox, quel que soit le type de sandbox (production ou hors production).

## Quelle est la sandbox de production par défaut ?

La sandbox de production par défaut est la première sandbox de production créée lorsqu’une organisation IMS est configurée pour la première fois. La sandbox de production par défaut vous permet d’ingérer ou d’utiliser des données de Platform, ainsi que d’accepter des requêtes qui n’incluent pas de valeurs pour un nom de sandbox ou un identifiant de sandbox. La sandbox de production par défaut peut être réinitialisée, mais pas supprimée.

## De combien de sandbox de production puis-je disposer ?

Une instance Experience Platform prend en charge plusieurs sandbox de production et de développement. Chaque sandbox conserve sa propre bibliothèque indépendante de ressources Platform (y compris les schémas, les jeux de données et les profils).

Une licence Experience Platform par défaut vous accorde un total de cinq sandbox que vous pouvez classer en tant que production ou développement. Vous pouvez ajouter des packs de 10 sandbox jusquʼà un maximum de 75 sandbox au total.

Les sandbox de production peuvent être réinitialisées ou supprimées, à l’exception des sandbox de production également utilisées par Adobe Analytics pour la fonctionnalité [Analytics sur l’ensemble des appareils (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=fr), ou si le graphique d’identité qui y est hébergé est également utilisé par Adobe Audience Manager pour la fonctionnalité [Destinations basées sur les personnes (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=fr).

Vous pouvez mettre à jour le titre d’une sandbox de production. Cependant, une sandbox de production ne peut pas être renommée.

>[!NOTE]
>
>Le nom de la sandbox est utilisé à des fins de recherche dans les appels API, tandis que le titre de la sandbox est utilisé comme nom d’affichage.

## De combien de sandbox de développement puis-je disposer ?

Experience Platform autorise actuellement un maximum de 75 sandbox au total (de production et de développement) à être actives au sein d’une seule organisation IMS.

Les sandbox de développement prennent en charge les fonctionnalités de réinitialisation et de suppression.

## Je viens de créer une sandbox. Comment puis-je définir des autorisations pour les utilisateurs qui travailleront avec cette sandbox ?

Adobe Admin Console lie les utilisateurs et utilisatrices aux sandbox et aux autorisations via l’utilisation de profils de produits. Après avoir créé une nouvelle sandbox, rendez-vous dans l’onglet **Autorisations** du profil de produits auquel vous souhaitez accorder l’accès, puis cliquez sur **Sandbox**. De là, vous pouvez ajouter ou supprimer l’accès à la nouvelle sandbox de la même manière que pour les autres autorisations.

Si vous souhaitez ajouter des autorisations uniques aux utilisateurs d’une sandbox spécifique, vous pouvez avoir besoin de créer un nouveau profil de produits pour lequel vous aurez appliqué les sandbox et les autorisations appropriées et attribuez ces utilisateurs à ce profil.

Pour plus d’informations sur la gestion des sandbox et des autorisations dans Admin Console, consultez le [guide d’utilisation du contrôle d’accès](../access-control/ui/overview.md). 
