---
keywords: Experience Platform;accueil;rubriques populaires;dule;DULE
solution: Experience Platform
title: Présentation de la gouvernance des données
description: La gouvernance des données d’Adobe Experience Platform vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Elle joue un rôle clé dans Experience Platform à différents niveaux, notamment dans le catalogage, la traçabilité des données, l’étiquetage de l’utilisation des données, les politiques d’utilisation des données et le contrôle de l’utilisation des données lors d’actions marketing.
exl-id: 00ca6bc2-1c58-4ea2-8bb5-30fd3fa5944a
source-git-commit: 1a050cfb41a28053606f07931c7c97d15989ac3e
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 66%

---

# Présentation de la gouvernance des données {#data-governance-overview}

>[!CONTEXTUALHELP]
>id="platform_datagovernance_framework"
>title="Obligation de gouvernance des données"
>abstract="N’oubliez pas qu’il vous incombe, à vous uniquement, de respecter les politiques de gouvernance des données de votre organisation et de satisfaire vos exigences réglementaires. Experience Platform fournit des outils de gouvernance des données qui vous permettent de gérer vos obligations en matière d’utilisation des données. Appliquez les libellés d’utilisation des données appropriés avant d’interroger ou de traiter des données. Consultez la documentation pour en savoir plus sur les outils de gouvernance des données et les bonnes pratiques."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=fr" text="Présentation de la gouvernance des données"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=fr" text="Vue d’ensemble des libellés de gouvernance des données"

L’une des principales fonctionnalités d’Adobe Experience Platform est de rassembler des données issues de plusieurs systèmes d’entreprise afin de permettre aux spécialistes marketing d’identifier, de comprendre et d’impliquer les clients avec plus d’efficacité. Ces données peuvent être soumises à des restrictions d’utilisation définies par votre organisation ou par des réglementations juridiques. Il est donc important de s’assurer que vos opérations de données au sein de [!DNL Platform] sont conformes aux politiques d’utilisation des données.

Gérez les données client et assurez-vous de la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données avec la gouvernance des données de Adobe Experience Platform. La gouvernance des données joue un rôle clé au sein de l’Experience Platform à différents niveaux, notamment le catalogage, la traçabilité des données, l’étiquetage de l’utilisation des données, les stratégies d’utilisation des données et le contrôle de l’utilisation des données pour les actions marketing.

>[!NOTE]
>
>Dans Experience Platform, la gouvernance des données ne concerne que la manière dont les données sont utilisées ou activées, peu importe l’utilisateur ou l’utilisatrice qui effectue l’action. Pour plus d’informations sur le contrôle de l’accès à des champs de données spécifiques pour certains utilisateurs et utilisatrices de Platform au sein de votre organisation, consultez plutôt la documentation sur le [contrôle d’accès basé sur les attributs](../access-control/abac/overview.md).

## Rôles de la gouvernance des données {#data-governance-roles}

En tant que concept, la gouvernance des données n’est pas automatique, mais ne vient pas non plus de nulle part. Ce qui a débuté comme étant le rôle d’une personne, portant généralement le titre de gestionnaire de données, a évolué considérablement à mesure que l’écosystème de gouvernance des données s’est élargi. Aujourd&#39;hui, la gouvernance des données nécessite une gestion et un suivi continus pour réussir. Pour garantir une gouvernance efficace des données, les gestionnaires de données doivent disposer d’outils avec lesquels les données peuvent être correctement étiquetées, de stratégies d’utilisation pouvant être créées et la conformité à ces politiques peut être appliquée.

Bien que la gouvernance des données doive être la responsabilité de chacun des membres de l’organisation, voici quelques-uns des rôles essentiels qui régissent les cycles de gouvernance des données :

![Graphique pour transmettre les quatre rôles de gouvernance des données, avec des citations sur les devoirs de chaque rôle.](./images/overview/roles.png)

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

Le cadre de gouvernance des données simplifie et rationalise le processus de catégorisation des données et de création des politiques d’utilisation des données. Une fois les étiquettes de données appliquées et les politiques d’utilisation des données en place, vous pouvez évaluer les actions marketing permettant d’assurer la bonne utilisation des données. 

Le cadre de gouvernance des données comporte trois éléments clés : les libellés, les politiques et l’application. 

1. **Libellés :** classent les données en fonction des considérations liées à la confidentialité et aux conditions contractuelles afin qu’elles soient conformes aux réglementations et aux politiques de l’organisation.
1. **Stratégies :** Décrivez les types d’actions marketing qui peuvent ou non être effectuées sur des données spécifiques.
1. **Application :** utilise le cadre de la politique pour conseiller et appliquer les stratégies sur différents modèles d’accès aux données.

## Libellés d’utilisation des données {#data-usage-labels}

La gouvernance des données permet aux gestionnaires de données d’appliquer des libellés d’utilisation au niveau du champ de schéma pour classer les données en fonction du type de stratégies qui s’appliquent.

Le cadre de gouvernance des données inclut des libellés d’utilisation des données prédéfinis pouvant être utilisés pour catégoriser les données de trois manières différentes :

![Les trois catégories d’étiquettes d’utilisation des données.](./images/overview/label-categories.png)

* **Étiquettes de données Contrat « C » :** étiquetez et catégorisez les données soumises à des obligations contractuelles ou associées à des politiques de gouvernance des données clients.
* **Étiquettes de données Identité « I » :** étiquetez et catégorisez des données pouvant identifier ou contacter une personne en particulier.
* **Étiquettes de données Sensibles « S » :** étiquetez et catégorisez les données associées aux données sensibles, telles que les données géographiques.

>[!NOTE]
>
>Consultez le guide sur les [libellés d’utilisation des données pris en charge](labels/reference.md) pour obtenir la liste complète des libellés disponibles et des définitions pour chaque type d’étiquette.

Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. La bonne pratique encourage à étiqueter les données lorsqu’elles sont ingérées dans Experience Platform ou dès que les données sont disponibles dans [!DNL Platform].

Pour plus d’informations sur l’utilisation des libellés d’utilisation des données pour renforcer la conformité de la gouvernance des données, consultez la présentation sur les [libellés d’utilisation des données](./labels/overview.md) .

## Politiques d’utilisation des données {#data-usage-policies}

Pour que les libellés d’utilisation des données prennent en charge efficacement la conformité des données, les stratégies d’utilisation des données doivent être mises en oeuvre. Les politiques d’utilisation des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé ou non à effectuer sur des données d’Experience Platform.

Un exemple d’action marketing peut être le souhait d’exporter un jeu de données vers un service tiers. Si une stratégie a été mise en place pour déclarer que les informations d’identification personnelle (PII) ne peuvent pas être exportées et qu’une étiquette &quot;I&quot; (données d’identité) a été appliquée au niveau du champ à partir de son schéma. Policy Service empêche alors toute action qui exporterait ce jeu de données vers une destination tierce. Si l’une de ces tentatives d’action se produit, Policy Service envoie un message vous informant qu’une violation de politique d’utilisation des données s’est passée.


Deux types de politiques sont disponibles :

* **[!UICONTROL Politique de gouvernance des données]** : permet de restreindre l’activation des données en fonction de l’action marketing en cours et des étiquettes d’utilisation des données associées aux données en question.
* **[!UICONTROL Stratégie de consentement]** : filtrez les profils qui peuvent être activés vers [destinations](../destinations/home.md) en fonction du consentement ou des préférences de vos clients.

Une fois les libellés d’utilisation des données appliqués, les gestionnaires de données peuvent créer des stratégies à l’aide de l’API Policy Service ou de l’interface utilisateur de l’Experience Platform. Pour plus d’informations sur les politiques d’utilisation des données et les actions marketing, consultez la [présentation des politiques](./policies/overview.md).

>[!IMPORTANT]
>
>Toutes les politiques d’utilisation des données (y compris les politiques de base fournies par Adobe) sont désactivées par défaut. Pour qu’une stratégie individuelle soit prise en compte pour l’application, vous devez l’activer manuellement.

## Étapes suivantes

Ce document a fourni une introduction de haut niveau à la gouvernance des données et au cadre de gouvernance des données. Vous pouvez désormais poursuivre en consultant le [guide d’utilisation des libellés d’utilisation des données](labels/user-guide.md) et commencer à ajouter des libellés d’utilisation à vos données d’expérience.

## Annexe

La section suivante fournit des informations supplémentaires concernant la gouvernance des données.

### Terminologie de la gouvernance des données {#data-governance-terminology}

Le tableau suivant présente les termes clés liés à la gouvernance des données ainsi qu’au cadre de gouvernance des données. 

| Terme | Définition |
|---|---|
| **Étiquettes Contrat** | Les étiquettes Contrat « C » sont utilisées pour catégoriser des données qui possèdent des obligations contractuelles ou qui sont liées aux politiques de gouvernance des données de votre organisation. |
| **Données intersites** | Les données intersites sont la combinaison de données provenant de plusieurs sites. Les données intersites comprennent des données sur site et hors site, ou une combinaison de données provenant de plusieurs sources hors site. |
| **Gouvernance des données** | La gouvernance des données englobe les stratégies et les technologies utilisées pour s’assurer que les données sont conformes aux réglementations et aux politiques d’entreprise en matière d’utilisation des données. |
| **Gestionnaire de données** | Le/la gestionnaire de données est la personne responsable de la gestion, de la supervision et de l’application des ressources de données d’une organisation. Un gestionnaire de données veille également à ce que les politiques de gouvernance des données soient préservées et conservées pour être conformes aux réglementations gouvernementales et aux politiques de l’organisation. |
| **Libellés d’utilisation des données** | Les libellés d’utilisation des données permettent aux utilisateurs de catégoriser les données en fonction des considérations liées à la confidentialité et des conditions contractuelles afin qu’elles soient conformes aux réglementations et aux politiques d’entreprise. |
| **Libellés de jeux de données** | Les libellés peuvent être ajoutés à un schéma. Tous les champs d’un jeu de données héritent des libellés du schéma. |
| **Libellés de champ** | Les libellés du champ sont des libellés de gouvernance des données qui sont hérités d’un schéma ou appliqués directement à un champ. Les libellés de gouvernance des données appliqués à un champ ne sont pas hérités jusqu’au niveau du schéma. |
| **Géobarrière** | Une géobarrière est une limite géographique virtuelle, définie par les technologies GPS ou RFID qui permet à un logiciel de déclencher une réponse lorsqu’un appareil mobile entre ou quitte une zone particulière. |
| **Étiquettes Identité** | Les étiquettes Identité « I » sont utilisées pour catégoriser des données pouvant identifier ou contacter une personne en particulier. |
| **Ciblage en fonction des intérêts** | Le ciblage en fonction des intérêts, également appelé personnalisation, se produit si les trois conditions suivantes sont remplies :<br>Les données collectées sur site sont,<br><ul><li>Utilisé pour établir des inférences sur l’intérêt d’un utilisateur,</li><li>Utilisé dans un autre contexte, tel que sur un autre site ou une autre application (hors site)</li><li>Utilisé pour sélectionner le contenu ou les publicités diffusés en fonction de ces inférences.</li></ul> |
| **Action marketing** | Dans le cadre de la gouvernance des données, une action marketing est une action entreprise par un utilisateur de données Experience Platform pour laquelle il est nécessaire de vérifier les violations des politiques d’utilisation des données |
| **Politique** | Dans le cadre de la gouvernance des données, une stratégie est une règle qui décrit les types d’actions marketing que vous pouvez ou non entreprendre sur des données spécifiques. |
| **Libellés de schéma** | Gérez les libellés liés à la gouvernance des données, au consentement et au contrôle d’accès au niveau du schéma. Cela propage les libellés à chaque jeu de données qui utilise ce schéma. |
| **Libellés Sensibles** | Les libellés sensibles « S » sont utilisés pour classer les données que vous et votre entreprise considérez comme sensibles. |

## Ressources supplémentaires

La vidéo suivante a pour but de vous aider à comprendre le cadre de gouvernance des données. 

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

La vidéo suivante explique comment appliquer des libellés d’utilisation des données à vos schémas ou à l’ensemble d’un jeu de données dans Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29709/?learn=on)
