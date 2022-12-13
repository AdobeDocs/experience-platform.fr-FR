---
keywords: Experience Platform;accueil;rubriques populaires;DULE;dule
solution: Experience Platform
title: Présentation de la gouvernance des données
topic-legacy: overview
description: La gouvernance des données d’Adobe Experience Platform vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux stratégies applicables à l’utilisation des données. Elle joue un rôle clé dans Experience Platform à différents niveaux, notamment dans le catalogage, la traçabilité des données, l’étiquetage de l’utilisation des données, les politiques d’utilisation des données et le contrôle de l’utilisation des données lors d’activités marketing
exl-id: 00ca6bc2-1c58-4ea2-8bb5-30fd3fa5944a
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '1479'
ht-degree: 84%

---

# Présentation de la gouvernance des données

L’une des principales fonctionnalités d’Adobe Experience Platform est de rassembler des données issues de plusieurs systèmes d’entreprise afin de permettre aux professionnels du marketing d’identifier, de comprendre et d’impliquer les clients avec plus d’efficacité. Ces données peuvent être soumises à des restrictions d’utilisation définies par votre organisation ou par des réglementations juridiques. Il est donc important de s’assurer que vos opérations de données au sein de [!DNL Platform] sont conformes aux stratégies d’utilisation des données.

La gouvernance des données d’Adobe Experience Platform vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux stratégies applicables à l’utilisation des données. Elle joue un rôle clé dans [!DNL Experience Platform], et ce, à différents niveaux, notamment dans le catalogage, la traçabilité des données, l’étiquetage d’utilisation des données, les stratégies d’utilisation des données et le contrôle de l’utilisation des données lors d’actions marketing.

>[!NOTE]
>
>Dans Experience Platform, la gouvernance des données ne concerne que la manière dont les données sont utilisées ou activées, quel que soit l’utilisateur qui effectue l’action. Pour plus d’informations sur le contrôle de l’accès à des champs de données spécifiques pour certains utilisateurs de Platform au sein de votre entreprise, consultez la documentation sur [contrôle d’accès basé sur les attributs](../access-control/abac/overview.md) au lieu de .

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


## Cadre de gouvernance des données

Le cadre de gouvernance des données simplifie et rationalise le processus de catégorisation des données et de création des stratégies d’utilisation des données. Une fois les libellés de données appliqués et les stratégies d’utilisation des données en place, vous pouvez évaluer les actions marketing permettant d’assurer la bonne utilisation des données. 

Le cadre de gouvernance des données comporte trois éléments clés : les libellés, les stratégies et l’application. 

1. **Libellés :** classent les données en fonction des considérations liées à la confidentialité et aux conditions contractuelles afin qu’elles soient conformes aux réglementations et aux politiques de l’organisation.
1. **Stratégies :** décrivent le ou les types d’actions marketing que vous êtes autorisé à effectuer ou non sur certaines données.
1. **Application :** utilise le cadre de la politique pour conseiller et appliquer les stratégies sur différents modèles d’accès aux données.

## Libellés d’utilisation des données

La gouvernance des données permet aux gestionnaires de données d’appliquer des libellés au niveau du jeu de données et du champ pour catégoriser les données en fonction du type de politiques qui s’applique.

Le cadre de gouvernance des données inclut des libellés d’utilisation des données prédéfinis pouvant être utilisés pour catégoriser les données de trois manières différentes :

![Catégorie des libellés d’utilisation des données](./images/overview/label-categories.png)

* **Étiquettes de données Contrat « C » :** étiquetez et catégorisez les données soumises à des obligations contractuelles ou associées à des politiques de gouvernance des données clients.
* **Étiquettes de données Identité « I » :** étiquetez et catégorisez des données pouvant identifier ou contacter une personne en particulier.
* **Étiquettes de données Sensibles « S » :** étiquetez et catégorisez les données associées aux données sensibles, telles que les données géographiques.

>[!NOTE]
>
>Consultez le guide sur les [libellés d’utilisation des données pris en charge](labels/reference.md) pour obtenir la liste complète des libellés disponibles ainsi que des définitions de chaque type de libellé.

Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. La bonne pratique encourage à libeller les données dès qu’elles sont ingérées dans [!DNL Experience Platform] ou dès qu’elles sont disponibles dans [!DNL Platform].

Pour plus d’informations, consultez la présentation des [libellés d’utilisation des données](./labels/overview.md).

## Stratégies d’utilisation des données

Des stratégies d’utilisation des données doivent être mises en œuvre pour que les libellés d’utilisation des données prennent en charge efficacement la conformité des données. Les stratégies d’utilisation des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé ou non à effectuer sur des données d’[!DNL Experience Platform].

Un exemple d’action marketing peut être le souhait d’exporter un jeu de données vers un service tiers. Si une stratégie est en place indiquant que les informations d’identification personnelle (PII) ne peuvent pas être exportées et qu’une étiquette &quot;I&quot; (données d’identité) a été appliquée au jeu de données, [!DNL Policy Service] empêche toute action qui exporterait ce jeu de données vers une destination tierce. Si l’une de ces tentatives d’action se produit, Policy Service envoie un message vous informant qu’une stratégie d’utilisation des données a été enfreinte.

Deux types de stratégies sont disponibles :

* **[!UICONTROL Politique de gouvernance des données]**: Restreindre l’activation des données en fonction de l’action marketing en cours et des libellés d’utilisation des données transportés par les données en question.
* **[!UICONTROL Stratégie de consentement]**: Filtrer les profils pouvant être activés sur [destinations](../destinations/home.md) selon le consentement ou les préférences de vos clients.

Une fois que les libellés d’utilisation des données ont été appliqués, les gestionnaires de données peuvent créer des stratégies à l’aide de l’API [!DNL Policy Service] ou de l’interface utilisateur d’[!DNL Experience Platform]. Pour plus d’informations sur les stratégies d’utilisation des données et les actions marketing, consultez la [présentation des stratégies](./policies/overview.md).

>[!IMPORTANT]
>
>Toutes les stratégies d’utilisation des données (y compris les stratégies de base fournies par Adobe) sont désactivées par défaut. Pour qu’une stratégie individuelle soit prise en compte pour l’application, vous devez l’activer manuellement.

## Étapes suivantes

Ce document fournit une présentation détaillée de la gouvernance des données ainsi que du cadre de gouvernance des données. Vous pouvez désormais poursuivre en consultant le [guide d’utilisation des libellés d’utilisation des données](labels/user-guide.md) et commencer à ajouter des libellés d’utilisation à vos données d’expérience.

## Annexe

La section suivante fournit des informations supplémentaires concernant la gouvernance des données.

### Terminologie de la gouvernance des données

Le tableau suivant présente les termes clés liés à la gouvernance des données ainsi qu’au cadre de gouvernance des données. 

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
| **Ciblage en fonction des intérêts** | Le ciblage en fonction des intérêts, également appelé personnalisation, se produit si les trois conditions suivantes sont remplies : Les données collectées sur site sont utilisées pour établir des inférences sur l’intérêt d’un utilisateur, dans un autre contexte, comme sur un autre site ou une autre application (hors site), et sont utilisées pour sélectionner le contenu ou les publicités diffusés en fonction de ces inférences. |
| **Action marketing** | Dans le cadre de la gouvernance des données, une action marketing est une action entreprise par un utilisateur de données [!DNL Experience Platform] pour laquelle il est nécessaire de vérifier les violations des stratégies d’utilisation des données. |
| **Stratégie** | Dans le cadre de la gouvernance des données, une stratégie est une règle qui décrit le type d’actions marketing que vous pouvez effectuer ou non sur des données spécifiques. |
| **Étiquettes Sensibles** | Les étiquettes Sensibles &quot;S&quot; sont utilisées pour catégoriser les données que vous et votre organisation considérez comme sensibles. |

## Ressources supplémentaires

La vidéo suivante a pour but de vous aider à comprendre le cadre de gouvernance des données. 

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

La vidéo suivante présente une introduction aux diverses fonctionnalités de gouvernance des données dans Experience Platform. 

>[!VIDEO](https://video.tv.adobe.com/v/36653?quality=12&enable10seconds=on&speedcontrol=on)
