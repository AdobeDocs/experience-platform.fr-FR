---
keywords: Experience Platform;accueil;rubriques populaires;dule;DULE
solution: Experience Platform
title: Présentation de la gouvernance des données
description: La gouvernance des données d’Adobe Experience Platform vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Elle joue un rôle clé dans Experience Platform à différents niveaux, notamment dans le catalogage, la traçabilité des données, l’étiquetage de l’utilisation des données, les politiques d’utilisation des données et le contrôle de l’utilisation des données lors d’actions marketing.
exl-id: 00ca6bc2-1c58-4ea2-8bb5-30fd3fa5944a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 63%

---

# Présentation de la gouvernance des données {#data-governance-overview}

>[!CONTEXTUALHELP]
>id="platform_datagovernance_framework"
>title="Obligation de gouvernance des données"
>abstract="N’oubliez pas qu’il vous incombe, à vous uniquement, de respecter les politiques de gouvernance des données de votre organisation et de satisfaire vos exigences réglementaires. Experience Platform fournit des outils de gouvernance des données qui vous permettent de gérer vos obligations en matière d’utilisation des données. Appliquez les libellés d’utilisation des données appropriés avant d’interroger ou de traiter des données. Consultez la documentation pour en savoir plus sur les outils de gouvernance des données et les bonnes pratiques."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=fr" text="Présentation de la gouvernance des données"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=fr" text="Vue d’ensemble des étiquettes de gouvernance des données"

L’une des principales fonctionnalités d’Adobe Experience Platform est de rassembler des données issues de plusieurs systèmes d’entreprise afin de permettre aux spécialistes marketing d’identifier, de comprendre et d’impliquer les clients avec plus d’efficacité. Ces données peuvent être soumises à des restrictions d’utilisation définies par votre organisation ou par des réglementations juridiques. Il est donc important de s’assurer que vos opérations de données au sein de [!DNL Experience Platform] sont conformes aux politiques d’utilisation des données.

Gérez les données clients et assurez-vous de la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données avec la gouvernance des données de Adobe Experience Platform. La gouvernance des données joue un rôle essentiel dans Experience Platform à différents niveaux, notamment dans le catalogage, la traçabilité des données, l’étiquetage d’utilisation des données, les politiques d’utilisation des données et le contrôle de l’utilisation des données lors d’actions marketing.

>[!NOTE]
>
>Dans Experience Platform, la gouvernance des données ne concerne que la manière dont les données sont utilisées ou activées, peu importe l’utilisateur ou l’utilisatrice qui effectue l’action. Pour plus d’informations sur le contrôle de l’accès à des champs de données spécifiques pour certains utilisateurs et utilisatrices d’Experience Platform au sein de votre organisation, consultez plutôt la documentation sur le [contrôle d’accès basé sur les attributs](../access-control/abac/overview.md).

## Rôles de la gouvernance des données {#data-governance-roles}

En tant que concept, la gouvernance des données n’est pas automatique, mais ne vient pas non plus de nulle part. Ce qui a débuté comme étant le rôle d’une personne, portant généralement le titre de gestionnaire de données, a évolué considérablement à mesure que l’écosystème de gouvernance des données s’est élargi. Aujourd’hui, la gouvernance des données nécessite une gestion et une surveillance continues pour réussir. Une gouvernance efficace des données repose sur le fait que les gestionnaires de données disposent d’outils permettant d’étiqueter correctement les données, de créer des politiques d’utilisation et d’appliquer la conformité à ces politiques.

Bien que la gouvernance des données doive être la responsabilité de chacun des membres de l’organisation, voici quelques-uns des rôles essentiels qui régissent les cycles de gouvernance des données :

![Graphique pour transmettre les quatre rôles de gouvernance des données, avec des citations sur les tâches de chaque rôle.](./images/overview/roles.png)

### Gestionnaire de données {#data-steward}

Les gestionnaires de données sont au cœur de la gouvernance des données. Ce rôle consiste à interpréter les réglementations, les restrictions et les politiques contractuelles et à les appliquer directement aux données. Grâce à sa compréhension de ces réglementations, restrictions et politiques, le rôle d’un gestionnaire de données inclut notamment :

* la vérification des données, des jeux de données et des exemples de données pour appliquer et gérer l’étiquetage d’utilisation des métadonnées ;
* la création des politiques de données et l’application de ces politiques aux jeux de données et aux champs ;
* la communication des politiques de données à l’organisation.

### Spécialiste marketing {#marketer}

Les spécialistes marketing sont le point de terminaison de la gouvernance des données. Ils ont besoin des données des infrastructures de gouvernance des données créées par des gestionnaires, des analystes et des ingénieurs des données. Les spécialistes marketing englobent plusieurs spécialistés différentes au sein du secteur marketing, notamment les suivantes :

* Les analystes marketing demandent des données pour permettre la compréhension des clients, aussi bien en tant que personnes que groupes (également connus sous le nom de segments).
* Les spécialistes marketing et les concepteurs/conceptrices d’expériences utilisent des données pour concevoir de nouvelles expériences clients.

## Cadre de gouvernance des données {#data-governance-framework}

Le cadre de gouvernance des données simplifie et rationalise le processus de catégorisation des données et de création des politiques d’utilisation des données. Une fois les libellés de données appliqués et les politiques d’utilisation des données en place, vous pouvez évaluer les actions marketing permettant d’assurer la bonne utilisation des données. 

Le cadre de gouvernance des données comporte trois éléments clés : les libellés, les politiques et l’application. 

1. **Libellés :** classent les données en fonction des considérations liées à la confidentialité et aux conditions contractuelles afin qu’elles soient conformes aux réglementations et aux politiques de l’organisation.
1. **Politiques :** décrivez les types d’actions marketing qu’il est autorisé ou non d’effectuer sur des données spécifiques.
1. **Application :** utilise le cadre de la politique pour conseiller et appliquer les stratégies sur différents modèles d’accès aux données.

## Libellés d’utilisation des données {#data-usage-labels}

La gouvernance des données permet aux gestionnaires de données d’appliquer des libellés d’utilisation au niveau du champ du schéma pour classer les données en fonction du type de politiques qui s’applique.

Le cadre de gouvernance des données inclut des libellés d’utilisation des données prédéfinis pouvant être utilisés pour catégoriser les données de trois manières différentes :

![Les trois catégories de libellés d’utilisation des données.](./images/overview/label-categories.png)

* **Étiquettes de données Contrat « C » :** étiquetez et catégorisez les données soumises à des obligations contractuelles ou associées à des politiques de gouvernance des données clients.
* **Libellés de données Identité « I » :** étiquetez et catégorisez des données pouvant identifier ou contacter une personne en particulier.
* **Libellés de données Sensibles « S » :** étiquetez et catégorisez les données associées aux données sensibles, telles que les données géographiques.

>[!NOTE]
>
>Consultez le guide sur les [libellés d’utilisation des données pris en charge](labels/reference.md) pour obtenir la liste complète des libellés disponibles et des définitions de chaque type de libellé.

Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. La bonne pratique encourage à libeller les données lorsqu’elles sont ingérées dans Experience Platform ou dès que les données sont disponibles dans [!DNL Experience Platform].

Consultez la présentation des [libellés d’utilisation des données](./labels/overview.md) pour plus d’informations sur l’utilisation des libellés d’utilisation des données pour appliquer la conformité en matière de gouvernance des données.

## Politiques d’utilisation des données {#data-usage-policies}

Pour que les libellés d’utilisation des données prennent en charge efficacement la conformité des données, des politiques d’utilisation des données doivent être implémentées. Les politiques d’utilisation des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé ou non à effectuer sur des données d’Experience Platform.

Un exemple d’action marketing peut être le souhait d’exporter un jeu de données vers un service tiers. Si une politique est en place indiquant que les informations d’identification personnelle (PII) ne peuvent pas être exportées et qu’un libellé « I » (données d’identité) a été appliqué au niveau du champ à partir de son schéma. Policy Service empêche ensuite toute action qui exporterait ce jeu de données vers une destination tierce. Si l’une de ces tentatives d’action se produit, Policy Service envoie un message vous informant qu’une violation de politique d’utilisation des données s’est passée.


Deux types de politiques sont disponibles :

* **[!UICONTROL Data governance policy]** : permet de restreindre l’activation des données en fonction de l’action marketing en cours et des libellés d’utilisation des données associés aux données en question.
* **[!UICONTROL Consent policy]** : filtrez les profils pouvant être activés sur [destinations](../destinations/home.md) en fonction du consentement ou des préférences de vos clients.

Une fois les libellés d’utilisation des données appliqués, les gestionnaires de données peuvent créer des politiques à l’aide de l’API Policy Service ou de l’interface utilisateur d’Experience Platform. Pour plus d’informations sur les politiques d’utilisation des données et les actions marketing, consultez la [présentation des politiques](./policies/overview.md).

>[!IMPORTANT]
>
>Toutes les politiques d’utilisation des données (y compris les politiques de base fournies par Adobe) sont désactivées par défaut. Pour qu’une politique individuelle soit prise en compte pour l’application, vous devez l’activer manuellement.

## Étapes suivantes

Ce document fournit une présentation détaillée de la gouvernance des données et du cadre de gouvernance des données. Vous pouvez désormais poursuivre en consultant le [guide d’utilisation des libellés d’utilisation des données](labels/user-guide.md) et commencer à ajouter des libellés d’utilisation à vos données d’expérience.

## Annexe

La section suivante fournit des informations supplémentaires concernant la gouvernance des données.

### Terminologie de la gouvernance des données {#data-governance-terminology}

Le tableau suivant présente les termes clés liés à la gouvernance des données ainsi qu’au cadre de gouvernance des données. 

| Terme | Définition |
|---|---|
| **Étiquettes Contrat** | Les étiquettes Contrat « C » sont utilisées pour catégoriser des données qui possèdent des obligations contractuelles ou qui sont liées aux politiques de gouvernance des données de votre organisation. |
| **Données intersites** | Les données intersites sont la combinaison de données provenant de plusieurs sites. Les données intersites comprennent des données sur site et hors site, ou une combinaison de données provenant de plusieurs sources hors site. |
| **Gouvernance des données** | La gouvernance des données englobe les stratégies et technologies utilisées pour s’assurer que les données sont conformes aux réglementations et aux politiques d’entreprise en matière d’utilisation des données. |
| **Gestionnaire de données** | Le/la gestionnaire de données est la personne responsable de la gestion, de la supervision et de l’application des ressources de données d’une organisation. Un gestionnaire de données s’assure également que les politiques de gouvernance des données sont protégées et conservées conformément aux réglementations gouvernementales et aux politiques de l’organisation. |
| **Libellés d’utilisation des données** | Les libellés d’utilisation des données permettent aux utilisateurs de catégoriser les données en fonction des considérations liées à la confidentialité et des conditions contractuelles afin qu’elles soient conformes aux réglementations et aux politiques d’entreprise. |
| **Libellés de jeux de données** | Les libellés peuvent être ajoutés à un schéma. Tous les champs d’un jeu de données héritent des libellés du schéma. |
| **Libellés de champ** | Les libellés de champ sont des étiquettes de gouvernance des données qui sont héritées d’un schéma ou appliquées directement à un champ. Les étiquettes de gouvernance des données appliquées à un champ ne sont pas héritées jusqu’au niveau du schéma. |
| **Géobarrière** | Une géobarrière est une limite géographique virtuelle, définie par les technologies GPS ou RFID qui permet à un logiciel de déclencher une réponse lorsqu’un appareil mobile entre ou quitte une zone particulière. |
| **Libellés Identité** | Les libellés Identité « I » sont utilisés pour catégoriser des données pouvant identifier ou contacter une personne en particulier. |
| **Ciblage en fonction des intérêts** | Le ciblage en fonction des intérêts, également appelé personnalisation, se produit si les trois conditions suivantes sont remplies : <br>Les données collectées sur site sont <br><ul><li>Utilisé pour établir des inférences sur les intérêts d’un utilisateur ou d’une utilisatrice,</li><li>Utilisé dans un autre contexte, par exemple sur un autre site ou sur une autre application (hors site)</li><li>Permet de sélectionner le contenu ou les annonces à diffuser en fonction de ces inférences.</li></ul> |
| **Action marketing** | Dans le cadre de la gouvernance des données, une action marketing est une action entreprise par un utilisateur de données Experience Platform pour laquelle il est nécessaire de vérifier les violations des politiques d’utilisation des données |
| **Politique** | Dans le cadre de la gouvernance des données, une politique est une règle qui décrit les types d’actions marketing autorisées ou non sur des données spécifiques. |
| **Libellés de schéma** | Gérez les libellés liés à la gouvernance des données, au consentement et au contrôle d’accès au niveau du schéma. Cela propage les libellés à chaque jeu de données qui utilise ce schéma. |
| **Libellés Sensibles** | Les libellés sensibles « S » sont utilisés pour classer les données que vous et votre entreprise considérez comme sensibles. |

## Ressources supplémentaires

La vidéo suivante a pour but de vous aider à comprendre le cadre de gouvernance des données. 

>[!VIDEO](https://video.tv.adobe.com/v/33154?captions=fre_fr&quality=12&enable10seconds=on&speedcontrol=on)

La vidéo suivante explique comment appliquer des libellés d’utilisation des données à vos schémas ou à l’intégralité d’un jeu de données dans Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/3422795/?captions=fre_fr&learn=on)
