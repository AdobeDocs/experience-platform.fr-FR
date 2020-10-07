---
keywords: Experience Platform;home;popular topics;DULE;dule
solution: Experience Platform
title: Gouvernance des données d’Adobe Experience Platform
topic: overview
description: La gouvernance des données d’Adobe Experience Platform vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux stratégies applicables à l’utilisation des données. Elle joue un rôle clé dans Experience Platform à différents niveaux, notamment dans le catalogage, la traçabilité des données, l’étiquetage de l’utilisation des données, les politiques d’utilisation des données et le contrôle de l’utilisation des données lors d’activités marketing
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 70%

---


# [!DNL Data Governance]aperçu

L’une des principales fonctionnalités d’Adobe Experience Platform est de rassembler des données issues de plusieurs systèmes d’entreprise afin de permettre aux professionnels du marketing d’identifier, de comprendre et d’impliquer les clients avec plus d’efficacité. Ces données peuvent être soumises à des restrictions d’utilisation définies par votre organisation ou par des réglementations juridiques. It is therefore important to ensure that your data operations within [!DNL Platform] are compliant with data usage policies.

Adobe Experience Platform [!DNL Data Governance] allows you to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data use. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data usage policies, and controlling usage of data for marketing actions.

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

The [!DNL Data Governance] framework simplifies and streamlines the process of categorizing data and creating data usage policies. Une fois les libellés de données appliqués et les stratégies d’utilisation des données en place, vous pouvez évaluer les actions marketing permettant d’assurer la bonne utilisation des données.

There are three key elements to the [!DNL Data Governance] framework: Labels, Policies, and Enforcement.

1. **Libellés :** classent les données en fonction des considérations liées à la confidentialité et aux conditions contractuelles afin qu’elles soient conformes aux réglementations et aux politiques de l’organisation.
1. **Stratégies :** décrivent le ou les types d’actions marketing que vous êtes autorisé à effectuer ou non sur certaines données.
1. **Application :** utilise le cadre de la politique pour conseiller et appliquer les stratégies sur différents modèles d’accès aux données.

## Libellés d’utilisation des données

[!DNL Data Governance] permet aux responsables de données d’appliquer des étiquettes d’utilisation au niveau du jeu de données et des champs afin de classer les données en fonction du type de stratégies appliquées.

The [!DNL Data Governance] framework includes predefined data usage labels that can be used to categorize data in three ways:

![Catégorie des libellés d’utilisation des données](./images/overview/label-categories.png)

* **Étiquettes de données Contrat « C » :** étiquetez et catégorisez les données soumises à des obligations contractuelles ou associées à des politiques de gouvernance des données clients.
* **Étiquettes de données Identité « I » :** étiquetez et catégorisez des données pouvant identifier ou contacter une personne en particulier.
* **Étiquettes de données Sensibles « S » :** étiquetez et catégorisez les données associées aux données sensibles, telles que les données géographiques.

>[!NOTE]
>
>Consultez le guide sur les [libellés d’utilisation des données pris en charge](labels/reference.md) pour obtenir la liste complète des libellés disponibles ainsi que des définitions de chaque type de libellé.

Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. Best practice encourages labeling data as soon as it is ingested into [!DNL Experience Platform], or as soon as data becomes available in [!DNL Platform].

Pour plus d’informations, voir la présentation des étiquettes [d’utilisation des](./labels/overview.md) données.

## Stratégies d’utilisation des données

Des stratégies d’utilisation des données doivent être mises en œuvre pour que les libellés d’utilisation des données prennent en charge efficacement la conformité des données. Data usage policies are rules that describe the kinds of marketing actions that you are allowed to, or restricted from, performing on data within [!DNL Experience Platform].

Un exemple d’action marketing peut être le souhait d’exporter un jeu de données vers un service tiers. If there is a policy in place saying that specific types of data, such as Personally Identifiable Information (PII), cannot be exported and an &quot;I&quot; label (Identity data) has been applied to the dataset, you will receive a response from the [!DNL Policy Service] telling you that a data usage policy has been violated.

Once data usage labels have been applied, data stewards can create policies using the [!DNL Policy Service] API or the [!DNL Experience Platform] user interface.

>[!IMPORTANT]
>
>Toutes les stratégies d’utilisation des données (y compris les stratégies de base fournies par l’Adobe) sont désactivées par défaut. Pour qu’une stratégie individuelle soit prise en compte pour l’application de la loi, vous devez l’activer manuellement.

Pour plus d’informations sur les stratégies d’utilisation des données et les actions marketing, voir l’aperçu [des](./policies/overview.md)stratégies.

## Étapes suivantes

This document provided a high-level introduction to [!DNL Data Governance] and the[!DNL Data Governance] framework. Vous pouvez désormais poursuivre en consultant le [guide d’utilisation des libellés d’utilisation des données](labels/user-guide.md) et commencer à ajouter des libellés d’utilisation à vos données d’expérience.

## Annexe

The following section provides additional information regarding [!DNL Data Governance].

### [!DNL Data Governance] terminologie

The following table outlines key terms related to [!DNL Data Governance] and the[!DNL Data Governance] framework.

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
| **Action marketing** | A marketing action, in the context of the data governance framework, is an action that an [!DNL Experience Platform] data consumer takes, for which there is a need to check for violations of data usage policies |
| **Stratégie** | Dans le cadre de la gouvernance des données, une stratégie est une règle qui décrit le type d’actions marketing que vous pouvez effectuer ou non sur des données spécifiques. |
| **Étiquettes Sensibles** | Les étiquettes Sensibles « S » sont utilisées pour catégoriser les données que vous et votre entreprise considérez comme sensibles. |

## Ressources supplémentaires

La vidéo suivante est destinée à vous aider à comprendre la [!DNL Data Governance] structure.

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

La vidéo suivante présente diverses [!DNL Data Governance] fonctionnalités de l’Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/36653?quality=12&enable10seconds=on&speedcontrol=on)