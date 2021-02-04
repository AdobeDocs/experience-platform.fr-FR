---
keywords: Experience Platform;accueil;rubriques populaires;DULE;dule
solution: Experience Platform
title: Gouvernance des données d’Adobe Experience Platform
topic: overview
description: La gouvernance des données d’Adobe Experience Platform vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux stratégies applicables à l’utilisation des données. Elle joue un rôle clé dans Experience Platform à différents niveaux, notamment dans le catalogage, la traçabilité des données, l’étiquetage de l’utilisation des données, les politiques d’utilisation des données et le contrôle de l’utilisation des données lors d’activités marketing
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 70%

---


# [!DNL Data Governance] présentation

L’une des principales fonctionnalités d’Adobe Experience Platform est de rassembler des données issues de plusieurs systèmes d’entreprise afin de permettre aux professionnels du marketing d’identifier, de comprendre et d’impliquer les clients avec plus d’efficacité. Ces données peuvent être soumises à des restrictions d’utilisation définies par votre organisation ou par des réglementations juridiques. Il est donc important de s&#39;assurer que vos opérations de données dans [!DNL Platform] sont conformes aux règles d&#39;utilisation des données.

Adobe Experience Platform [!DNL Data Governance] vous permet de gérer les données client et de veiller au respect des réglementations, restrictions et stratégies applicables à l’utilisation des données. Il joue un rôle clé dans [!DNL Experience Platform] à divers niveaux, notamment le catalogage, le lignage des données, l&#39;étiquetage de l&#39;utilisation des données, les stratégies d&#39;utilisation des données et le contrôle de l&#39;utilisation des données pour les actions marketing.

## Rôles de la gouvernance des données

En tant que concept, la gouvernance des données n’est pas automatique, mais ne vient pas non plus de nulle part. Ce qui a débuté comme étant le rôle d’une personne, portant généralement le titre de gestionnaire de données, a évolué considérablement à mesure que l’écosystème de gouvernance des données s’est élargi. Aujourd’hui, la gouvernance des données nécessite une gestion et une surveillance continue pour réussir et compte sur des gestionnaires de données qui possèdent des outils permettant d’étiqueter correctement les données, d’appliquer des politiques d’utilisation et de s’assurer que ces politiques sont conformes.

Bien que la gouvernance des données doive être la responsabilité de chacun des membres de l’organisation, voici quelques-uns des rôles essentiels qui régissent les cycles de gouvernance des données :

![Rôles de la gouvernance des données](./images/overview/roles.png)

### Gestionnaire de données

Les gestionnaires de données sont au cœur de la gouvernance des données. Ce rôle consiste à interpréter les réglementations, les restrictions et les politiques contractuelles et à les appliquer directement aux données. Grâce à sa compréhension de ces réglementations, restrictions et politiques, le rôle d’un gestionnaire de données inclut notamment :

* la vérification des données, des jeux de données et des exemples de données pour appliquer et gérer l’étiquetage d’utilisation des métadonnées ;
* la création des stratégies de données et l’application de ces stratégies aux jeux de données et aux champs ;
* la communication des stratégies de données à l’organisation.

### Professionnel du marketing

Les professionnels du marketing sont le point de terminaison de la gouvernance des données. Ils ont besoin des données des infrastructures de gouvernance des données créées par des gestionnaires, des analystes et des ingénieurs des données. Les professionnels du marketing englobent plusieurs spécialistes différents au sein du secteur marketing, notamment les suivants :

* Les analystes marketing demandent des données pour permettre la compréhension des clients, aussi bien en tant que personnes que groupes (également connus sous le nom de segments).
* Les spécialistes du marketing et les concepteurs dans Experience utilisent des données pour concevoir de nouvelles expériences client.


## [!DNL Data Governance] cadre

La structure [!DNL Data Governance] simplifie et rationalise le processus de catégorisation des données et de création de stratégies d&#39;utilisation des données. Une fois les libellés de données appliqués et les stratégies d’utilisation des données en place, vous pouvez évaluer les actions marketing permettant d’assurer la bonne utilisation des données.

La structure [!DNL Data Governance] comporte trois éléments clés : Étiquettes, politiques et application de la loi.

1. **Libellés :** classent les données en fonction des considérations liées à la confidentialité et aux conditions contractuelles afin qu’elles soient conformes aux réglementations et aux politiques de l’organisation.
1. **Stratégies :** décrivent le ou les types d’actions marketing que vous êtes autorisé à effectuer ou non sur certaines données.
1. **Application :** utilise le cadre de la politique pour conseiller et appliquer les stratégies sur différents modèles d’accès aux données.

## Libellés d’utilisation des données

[!DNL Data Governance] permet aux responsables de données d’appliquer des étiquettes d’utilisation au niveau du jeu de données et des champs afin de classer les données en fonction du type de stratégies appliquées.

La structure [!DNL Data Governance] comprend des étiquettes d&#39;utilisation de données prédéfinies qui peuvent être utilisées pour classer les données de trois manières :

![Catégorie des libellés d’utilisation des données](./images/overview/label-categories.png)

* **Étiquettes de données Contrat « C » :** étiquetez et catégorisez les données soumises à des obligations contractuelles ou associées à des politiques de gouvernance des données clients.
* **Étiquettes de données Identité « I » :** étiquetez et catégorisez des données pouvant identifier ou contacter une personne en particulier.
* **Étiquettes de données Sensibles « S » :** étiquetez et catégorisez les données associées aux données sensibles, telles que les données géographiques.

>[!NOTE]
>
>Consultez le guide sur les [libellés d’utilisation des données pris en charge](labels/reference.md) pour obtenir la liste complète des libellés disponibles ainsi que des définitions de chaque type de libellé.

Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. Il est recommandé d’étiqueter les données dès qu’elles sont ingérées dans [!DNL Experience Platform] ou dès que les données sont disponibles dans [!DNL Platform].

Pour plus d&#39;informations, consultez l&#39;aperçu des [étiquettes d&#39;utilisation des données](./labels/overview.md).

## Stratégies d’utilisation des données

Des stratégies d’utilisation des données doivent être mises en œuvre pour que les libellés d’utilisation des données prennent en charge efficacement la conformité des données. Les stratégies d’utilisation des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé à exécuter, ou dont vous êtes limité à l’exécution, sur les données dans [!DNL Experience Platform].

Un exemple d’action marketing peut être le souhait d’exporter un jeu de données vers un service tiers. Si une stratégie indique que des types spécifiques de données, tels que les informations d’identification personnelle (PII), ne peuvent pas être exportés et qu’une étiquette &quot;I&quot; (données d’identité) a été appliquée au jeu de données, vous recevrez une réponse de la part de [!DNL Policy Service] vous indiquant qu’une stratégie d’utilisation des données a été violée.

Une fois les étiquettes d’utilisation des données appliquées, les responsables de données peuvent créer des stratégies à l’aide de l’API [!DNL Policy Service] ou de l’interface utilisateur [!DNL Experience Platform].

>[!IMPORTANT]
>
>Toutes les stratégies d’utilisation des données (y compris les stratégies de base fournies par l’Adobe) sont désactivées par défaut. Pour qu’une stratégie individuelle soit prise en compte pour l’application de la loi, vous devez l’activer manuellement.

Pour plus d&#39;informations sur les stratégies d&#39;utilisation des données et les actions marketing, consultez la [présentation des stratégies](./policies/overview.md).

## Étapes suivantes

Ce document a fourni une introduction de haut niveau à [!DNL Data Governance] et au cadre[!DNL Data Governance]. Vous pouvez désormais poursuivre en consultant le [guide d’utilisation des libellés d’utilisation des données](labels/user-guide.md) et commencer à ajouter des libellés d’utilisation à vos données d’expérience.

## Annexe

La section suivante fournit des informations supplémentaires sur [!DNL Data Governance].

### [!DNL Data Governance] terminologie

Le tableau suivant décrit les termes clés liés à [!DNL Data Governance] et à la structure [!DNL Data Governance].

| Terme | Définition |
|---|---|
| **Étiquettes Contrat** | Les étiquettes Contrat « C » sont utilisées pour catégoriser des données qui possèdent des obligations contractuelles ou qui sont liées aux politiques de gouvernance des données de votre organisation. |
| **Données intersites** | Les données intersites sont une combinaison de données de plusieurs sites, y compris une combinaison de données sur site et de données hors site ou une combinaison de données provenant de plusieurs sources hors site. |
| **Gouvernance des données** | La gouvernance des données englobe les stratégies et les technologies utilisées pour s’assurer que les données sont conformes aux réglementations et aux politiques d’entreprise en matière d’utilisation des données. |
| **Gestionnaire de données** | Le gestionnaire de données est la personne responsable de la gestion, de la supervision et de l’application des ressources de données d’une organisation. Un gestionnaire de données assure également la protection et la conservation des politiques de gouvernance des données afin qu’elles soient conformes aux réglementations gouvernementales et aux politiques de l’organisation. |
| **Libellés d’utilisation des données** | Les libellés d’utilisation des données permettent aux utilisateurs de catégoriser les données en fonction des considérations liées à la confidentialité et des conditions contractuelles afin qu’elles soient conformes aux réglementations et aux politiques d’entreprise. |
| **Libellés de jeux de données** | Les libellés peuvent être ajoutés à un jeu de données. Tous les champs d’un jeu de données héritent des libellés du jeu de données. |
| **Libellés de champ** | Les libellés de champ sont des libellés de gouvernance des données qui sont soit hérités d’un jeu de données soit appliqués directement à un champ.  Les libellés de gouvernance des données appliquées à un champ ne sont pas hérités d’un jeu de données. |
| **Géobarrière** | Une géobarrière est une limite géographique virtuelle, définie par les technologies GPS ou RFID qui permet à un logiciel de déclencher une réponse lorsqu’un appareil mobile entre ou quitte une zone particulière. |
| **Étiquettes Identité** | Les étiquettes Identité « I » sont utilisées pour catégoriser des données pouvant identifier ou contacter une personne en particulier. |
| **Ciblage en fonction des intérêts** | Le ciblage en fonction des intérêts, également connu sous le nom de personnalisation, se produit si les trois conditions suivantes sont rassemblées : les données collectées sur site sont utilisées pour établir des inférences sur les intérêts d’un utilisateur, elles sont utilisées dans un autre contexte, par exemple sur un autre site ou sur une autre application (hors site) ou elles sont utilisées pour sélectionner le contenu ou les publicités diffusées en fonction de ces inférences. |
| **Action marketing** | Une action marketing, dans le cadre de la gouvernance des données, est une action entreprise par un [!DNL Experience Platform] utilisateur de données, pour laquelle il est nécessaire de vérifier les violations des stratégies d&#39;utilisation des données. |
| **Stratégie** | Dans le cadre de la gouvernance des données, une stratégie est une règle qui décrit le type d’actions marketing que vous pouvez effectuer ou non sur des données spécifiques. |
| **Étiquettes Sensibles** | Les étiquettes Sensibles « S » sont utilisées pour catégoriser les données que vous et votre entreprise considérez comme sensibles. |

## Ressources supplémentaires

La vidéo suivante est destinée à vous aider à comprendre la structure [!DNL Data Governance].

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

La vidéo suivante présente diverses fonctionnalités [!DNL Data Governance] de l&#39;Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/36653?quality=12&enable10seconds=on&speedcontrol=on)