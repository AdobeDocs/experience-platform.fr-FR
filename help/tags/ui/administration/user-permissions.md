---
title: Autorisations d’utilisateur relatives aux balises
description: Découvrez les différents types d’autorisations relatives aux balises disponibles et quelques stratégies d’implémentation de base pour différents cas d’utilisation commerciale.
exl-id: 9b48847a-6133-4dbd-b17d-e7b88152ad7d
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 91%

---

# Autorisations d’utilisateur relatives aux balises

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Les autorisations d’utilisateur relatives aux balises dans Adobe Experience Platform sont attribuées aux utilisateurs via Adobe Admin Console. Plutôt que d’être attribuées à chaque utilisateur, les autorisations sont configurées séparément en différents jeux, sous forme de profils de produit. Les utilisateurs sont ensuite affectés à ces profils de produit afin d’obtenir les autorisations pour lesquelles ces derniers ont été configurés.

Ce guide présente un aperçu des différents types d’autorisations relatives aux balises disponibles, des fonctionnalités auxquelles elles donnent accès et de quelques stratégies d’implémentation de base pour différents cas d’utilisation commerciale.

>[!NOTE]
>
>Pour savoir comment configurer les autorisations pour les utilisateurs qui utilisent Admin Console, reportez-vous au tutoriel sur la [gestion des autorisations pour la collecte de données](../../../collection/permissions.md).

## Types d’autorisations

Dans un profil de produit, les autorisations relatives aux balises sont réparties en quatre catégories :

1. Plateformes
1. Propriétés
1. Droits de propriété
1. Droits d’entreprise

### Plateformes

Chaque propriété de balise possède une plateforme. Vous pouvez actuellement utiliser deux plateformes pour les balises : Web et Mobile. Vous pouvez utiliser ce type d’autorisation pour restreindre ou accorder l’accès à un type particulier de propriété. Cela peut s’avérer utile lorsque l’équipe qui gère vos applications mobiles diffère de celle qui gère vos sites web.

### Propriétés

Par défaut, les profils de produit octroient l’accès à toutes les propriétés qui existent au sein de votre société, actuellement et à l’avenir. Avec ce type d’autorisation, vous pouvez restreindre ou octroyer l’accès à des propriétés existantes spécifiques par nom.

### Droits de propriété {#property-rights}

Toute propriété de balise que vous créez dans l’interface utilisateur est disponible dans Admin Console, ce qui vous permet de regrouper la propriété avec des droits de propriété spécifiques dans le même profil de produit.

Si, par exemple, un profil de produit donné n’a pas accès à Propriété A1, les utilisateurs qui appartiennent à ce profil ne peuvent ni consulter ni modifier les paramètres dans Propriété A1.

Si un utilisateur appartient à un profil qui a accès à Propriété A1, les actions qu’il peut effectuer dans Propriété A1 sont déterminées par les droits qui lui ont été octroyés à partir de ce profil. Si un utilisateur dispose d’autorisations pour Propriété A1 mais ne dispose pas de droits attribués, il dispose alors d’un accès en lecture seule pour cette propriété.

Le tableau suivant décrit les droits de propriété disponibles et les fonctionnalités auxquelles ils donnent accès :

| Droit de propriété | Description |
| --- | --- |
| **Développer** | Ce droit autorise les actions suivantes :<ul><li>Création de règles et d’éléments de données</li><li>Création de bibliothèques et intégration dans des environnements de développement existants</li><li>Envoi de bibliothèque pour approbation</li></ul>La plupart des tâches quotidiennes dans l’interface utilisateur exigent ce droit. |
| **Approuver** | Cela vous permet de prendre une bibliothèque envoyée et de l’intégrer dans l’environnement d’évaluation. Vous pouvez également approuver une bibliothèque en vue de la publier une fois le test terminé. |
| **Publier** | Cela vous permet de publier des bibliothèques approuvées dans l’environnement de production. |
| **Gérer les extensions** | Ce droit autorise les actions suivantes : <ul><li>Installation de nouvelles extensions sur une propriété</li><li>Modification de la configuration d’une extension déjà installée</li><li>Suppression d’une extension</li></ul>Consultez la documentation de présentation des extensions pour [plus dʼinformations sur les extensions](../managing-resources/extensions/overview.md). Ce rôle appartient généralement au service informatique ou au marketing, selon votre organisation. |
| **Gérer les environnements** | Permet de créer et de modifier des environnements. Pour plus dʼinformations, consultez la [documentation sur les environnements](../publishing/environments.md). Ce rôle appartient généralement au groupe informatique. |

{style="table-layout:auto"}

### Droits d’entreprise

Les droits d’entreprise s’appliquent aux autorisations qui s’appliquent à plusieurs propriétés. Ces informations sont présentées dans le tableau ci-dessous :

| Droit de la société | Description |
| --- | --- |
| **Gérer les propriétés** | Ce droit autorise les actions suivantes :<ul><li>Création de propriétés</li><li>Modification des métadonnées et des paramètres au niveau de la propriété</li><li>Suppression des propriétés</li></ul>Les administrateurs assument généralement ce rôle. Pour plus dʼinformations, voir la [documentation sur les propriétés](companies-and-properties.md). |
| **Développer des extensions** | Permet de créer et de modifier des packages dʼextensions dont lʼentreprise dispose, y compris les versions privées et les demandes de version publique. |
| **Gérer les configurations d&#39;application** | Cette option n’est disponible que si vous disposez d’une licence pour Adobe Journey Optimizer ou d’une autre solution qui accorde l’accès à la messagerie intégrée (in-app) mobile et push.  Cela permet de gérer les applications dont Experience Cloud a connaissance, ainsi que les informations d’identification push nécessaires pour communiquer avec le service Firebase Cloud Messaging et le service de notification push Apple. |

{style="table-layout:auto"}

## Autorisations utilisateur totales

Les autorisations totales dʼun utilisateur individuel sont déterminées par son nombre total dʼabonnements dans différents profils de produit. Si un utilisateur appartient à plusieurs profils de produit, les autorisations de chaque profil sont additionnées et non multipliées.

Par exemple, le profil de produit A vous accorde le droit de développement pour Propriété 1. Le profil de produit B vous accorde le droit de publication pour Propriété 2. Dans cette situation, vous pouvez développer dans Propriété 1 et publier dans Propriété 2, mais vous ne pouvez pas publier dans Propriété 1 ou développer dans Propriété 2, car vous nʼavez pas reçu de droits explicites à cet effet.

## Scénarios de droits

Toutes les sociétés nʼont pas les mêmes besoins lorsquʼil sʼagit de créer des profils de produit. Ces besoins varient en fonction de la taille de la société, de la structure de lʼorganisation, du nombre de sites, du nombre de personnes impliquées dans la gestion des balises, etc.

Vous trouverez ci-dessous quelques scénarios courants et un point de départ recommandé lorsque vous envisagez de créer des profils de produit et dʼy ajouter des utilisateurs.

### Affichage unique

Si vous dirigez une petite société comptant une personne responsable de tout, accordez-lui les autorisations dʼaccès à toutes les propriétés et attribuez-lui tous les droits répertoriés ci-dessus.

### Séparation des tâches

Supposons que de nombreuses personnes au sein de votre organisation soient concernées par le balisage. Vous disposez dʼun groupe de personnes (un consultant externe, par exemple) qui créent des règles et des éléments de données, mais vous ne souhaitez pas quʼelles aient accès à lʼenvironnement de production. Dans cette situation, assurez-vous que personne nʼeffectue de déploiement pour Production, à lʼexception de lʼéquipe informatique.

Voici comment faire :

1. Créez un compte pour vos consultants et ne leur accordez que le droit de développement.
1. Le consultant crée et teste dans les limites que vous avez définies.
1. Si le consultant souhaite une nouvelle extension ou est prêt à publier son application, un représentant de votre organisation (disposant des droits appropriés) effectue ces actions.

### Entreprise

Une entreprise peut avoir plusieurs sites divisés géographiquement, avec différentes équipes responsables de chaque région. Au sein de ces équipes, différentes personnes se chargent du développement et de la publication.

Cela se rapproche de la section « Séparation des tâches » ci-dessus, à l’exception de l’organisation par zone géographique. Par exemple, vous pouvez créer un profil « Développement » et un profil « Publication » pour lʼAmérique du Nord, et créer des groupes « Développement » et « Publication » distincts pour lʼEurope.

## Exemples de rôles

Le tableau suivant fournit quelques exemples des types de rôles que vous pouvez avoir dans votre organisation et des autorisations que vous devez leur attribuer :

| Rôle | Description | Propriétés | Droits de propriété | Droits d’entreprise |
| --- | --- | --- | --- | --- |
| Le gestionnaire | souhaite voir ce qui se passe dans le système, mais ne peut pas y apporter de modifications. | Inclusion automatique | (Aucun) | (Aucun) |
| Le spécialiste marketing | peut installer des extensions et configurer de nouvelles balises pour des propriétés existantes, mais ne peut pas publier dans les environnements dʼévaluation ou de production. | Inclusion automatique | <ul><li>Développer</li><li>Gérer les extensions</li></ul> | <ul><li>Gérer les propriétés</li></ul> |
| Le développeur d’applications mobiles | est responsable de la mise en œuvre de solutions Adobe et tierces dans une application mobile native. | Inclusion automatique | <ul><li>Développer</li><li>Gérer les extensions</li></ul> | <li>Gérer les propriétés</li><li>Gérer les configurations d’application</li> |
| L’équipe informatique | ne modifie aucune balise, mais contrôle totalement les environnements dʼévaluation et de production, et ce quʼils contiennent. | Inclusion automatique | (Aucun) | <ul><li>Approuver</li><li>Publier</li><li>Gérer les environnements</li></ul> |
| Le développeur d’extensions | développe des extensions et peut les soumettre pour approbation, mais ne peut pas les publier ni les ajouter aux propriétés existantes. | Inclusion automatique | <ul><li>Développer</li></ul> | <ul><li>Gérer les propriétés</li><li>Développement dʼextensions</li></ul> |
| Le super utilisateur | fait tout. | Inclusion automatique | <ul><li>Développer</li><li>Approuver</li><li>Publier</li><li>Gérer les extensions</li><li>Gérer les environnements</li></ul> | <ul><li>Gérer les propriétés</li></ul> |

{style="table-layout:auto"}

## Étapes suivantes

Ce document fournit un aperçu des autorisations disponibles pour les balises dans Experience Platform. Pour obtenir des instructions sur la configuration des profils de produit pour les balises dans Adobe Admin Console, consultez le guide sur la [gestion des autorisations d’utilisateur pour la collecte de données](../../../collection/permissions.md).
