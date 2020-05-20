---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Gouvernance des données de la plateforme Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 42efd7295dd8002869694a146ea166ad21bd14bb
workflow-type: tm+mt
source-wordcount: '1508'
ht-degree: 3%

---


# Présentation de la gouvernance des données

L’une des principales fonctionnalités d’Adobe Experience Platform consiste à rassembler les données issues de plusieurs systèmes d’entreprise afin de permettre aux spécialistes du marketing d’identifier, de comprendre et d’impliquer davantage les clients. Ces données peuvent être soumises à des restrictions d’utilisation définies par votre organisation ou par des réglementations juridiques. Il est donc important de s’assurer que vos opérations de données dans Platform sont conformes aux règles d’utilisation des données.

La gouvernance des données dans Adobe Experience Platform vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Il joue un rôle clé dans la plate-forme d’expérience à divers niveaux, notamment le catalogage, le lignage des données, l’étiquetage de l’utilisation des données, les stratégies d’utilisation des données et le contrôle de l’utilisation des données pour les actions marketing.

## Rôles de gouvernance des données

En tant que concept, la gouvernance des données n&#39;est ni automatique, ni ne se fait dans le vide. Ce qui a commencé comme un rôle pour un individu, généralement reconnu comme un gestionnaire **de** données, s&#39;est considérablement développé avec l&#39;expansion de l&#39;écosystème de gouvernance des données. Aujourd&#39;hui, la gouvernance des données nécessite une gestion et un contrôle continus afin d&#39;être efficace et repose sur des gestionnaires de données disposant d&#39;outils avec lesquels les données peuvent être correctement étiquetées, des stratégies d&#39;utilisation peuvent être créées et la conformité à ces stratégies peut être mise en oeuvre.

Bien que la gouvernance des données doive relever de la responsabilité de chaque individu de l&#39;organisation, voici quelques-uns des rôles essentiels du cycle de gouvernance des données :

![Rôles de gouvernance des données](./images/overview/roles.png)

### Responsable de données

Les gestionnaires de données sont au coeur de la gouvernance des données. Ce rôle est chargé d&#39;interpréter les règlements, les restrictions contractuelles et les politiques, et de les appliquer directement aux données. Informé par leur compréhension de ces règlements, restrictions et politiques, le rôle d&#39;un gestionnaire de données comprend :

* Vérification des données, des jeux de données et des exemples de données pour appliquer et gérer l’étiquetage d’utilisation des métadonnées.
* Création de stratégies de données et application de ces stratégies aux jeux de données et aux champs.
* Communication des stratégies de données à l’entreprise.

### Marketer

Les marketeurs sont le point final de la gouvernance des données. Ils demandent des données à l&#39;infrastructure de gouvernance des données créée par les gestionnaires de données, les scientifiques et les ingénieurs. Les spécialistes du marketing comprennent un certain nombre de spécialités différentes sous l’égide marketing, dont les suivantes :

* Les analystes marketing demandent des données pour permettre la compréhension des clients, en tant qu’individus et dans des groupes (également appelés segments).
* Les spécialistes du marketing et les concepteurs d’expérience utilisent les données pour concevoir de nouvelles expériences client.


## Structure DULE

L’étiquetage et l’application de l’utilisation des données (DULE) constituent le cadre de base de la gouvernance des données de la plateforme d’expérience. DULE simplifie et rationalise le processus de catégorisation des données et de création de stratégies d&#39;utilisation des données. Une fois les étiquettes de données appliquées et les stratégies d’utilisation des données mises en place, les actions marketing peuvent être évaluées afin de garantir une utilisation correcte des données.

Le cadre de DULE comporte trois éléments clés : Étiquettes, politiques et application de la loi.

1. **Étiquettes :** Classer les données qui reflètent les considérations liées à la vie privée et les conditions contractuelles pour les rendre conformes aux règlements et aux politiques de l&#39;organisation.
1. **Stratégies :** Décrivez le ou les types d’actions marketing autorisées ou non sur des données spécifiques.
1. **Application :** Utilise le cadre de stratégie pour conseiller et appliquer les stratégies selon différents modèles d’accès aux données.

## Étiquettes d’utilisation des données

La gouvernance des données permet aux responsables de la gestion des données d’appliquer des étiquettes d’utilisation au niveau du jeu de données et du champ afin de classer les données en fonction du type de stratégies appliquées.

La structure DULE comprend des étiquettes d’utilisation de données prédéfinies qui peuvent être utilisées pour classer les données de quatre manières :

![Catégories d’étiquettes d’utilisation des données](./images/overview/label-categories.png)

* **Étiquettes de données du contrat &quot;C&quot; :** Étiqueter et classer les données qui ont des obligations contractuelles ou qui sont liées aux stratégies de gouvernance des données client.
* **Étiquettes de données &quot;I&quot; d&#39;identité :** Étiqueter et classer les données qui peuvent identifier ou contacter une personne spécifique.
* **Étiquettes de données sensibles &quot;S&quot; :** Étiqueter et classer les données liées à des données sensibles telles que les données géographiques.
* **Étiquettes des données du RGPD :** Étiqueter et classer les données susceptibles de contenir des identifiants personnels à utiliser dans le RGPD et/ou supprimer des requêtes.

>[!NOTE] Consultez le guide sur les étiquettes [d’utilisation des données](labels/reference.md) prises en charge pour obtenir une liste complète des étiquettes disponibles, ainsi que des définitions pour chaque type d’étiquette.

Les étiquettes peuvent être appliquées à tout moment, ce qui vous permet de gérer les données avec souplesse. Il est recommandé d’étiqueter les données dès qu’elles sont incorporées dans la plate-forme d’expérience ou dès que les données sont disponibles dans la plate-forme.

Pour obtenir des instructions détaillées sur l’application d’étiquettes [aux jeux de données et aux champs à l’aide de l’interface utilisateur, reportez-vous à la présentation des étiquettes d’utilisation des](./labels/overview.md) données.

## Stratégies d’utilisation des données

Pour que les étiquettes d’utilisation des données prennent efficacement en charge la conformité des données, des stratégies d’utilisation des données doivent être mises en oeuvre. Les stratégies d’utilisation des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé à exécuter sur les données dans la plate-forme d’expérience, ou dont vous êtes limité à l’exécution.

Un exemple d’action marketing peut être le désir d’exporter un jeu de données vers un service tiers. Si une stratégie indique que des types spécifiques de données, tels que les informations d’identification personnelle (informations d’identification personnelle), ne peuvent pas être exportés et qu’une étiquette &quot;I&quot; (données d’identité) a été appliquée au jeu de données, vous recevrez une réponse du service de stratégie vous indiquant qu’une stratégie d’utilisation des données a été enfreinte.

Une fois les étiquettes d’utilisation des données appliquées, les responsables de données peuvent créer des stratégies à l’aide de l’API DULE Policy Service ou de l’interface utilisateur de la plateforme d’expérience.

Pour plus d&#39;informations sur l&#39;exécution des opérations clés fournies par l&#39;API DULE Policy Service, consultez le guide [du développeur](api/getting-started.md)Policy Service. Pour obtenir des instructions détaillées sur l’utilisation des stratégies DULE, consultez le didacticiel sur la [création et l’évaluation des stratégies DULE à l’aide de l’API](policies/create.md).

Pour plus d’informations sur la gestion des stratégies dans l’interface utilisateur de la plate-forme d’expérience, voir le guide [d’utilisation des](policies/user-guide.md)stratégies.

## Versions ultérieures

La gouvernance des données prend actuellement en charge l’étiquetage DULE à deux niveaux (jeu de données et champ). La gouvernance des données prend également en charge la création et la gestion de stratégies d’utilisation des données et d’actions marketing via l’API DULE Policy Service.

Les versions suivantes offrent les fonctionnalités suivantes :

* Libellés d’utilisation des données personnalisées : Créez de nouvelles étiquettes et définitions en fonction des besoins de votre entreprise.
* Application des politiques : Utilisez le cadre de stratégie pour conseiller et appliquer des stratégies selon différents modèles d’accès aux données.
* Audit : Surveiller les activités d&#39;accès aux données et identifier et signaler les problèmes de conformité.

## Étapes suivantes

Ce document a fourni une introduction de haut niveau à la gouvernance des données et au cadre DULE. Vous pouvez maintenant continuer à ajouter des étiquettes d’utilisation des [données au guide](labels/user-guide.md) d’utilisation et au début d’utilisation en ajoutant des étiquettes d’utilisation à vos données d’expérience.

## Annexe

La section suivante fournit des informations supplémentaires sur la gouvernance des données.

### Terminologie de la gouvernance des données

Le tableau suivant décrit les termes clés liés à la gouvernance des données et au cadre de DULE.

| Terme | Définition |
|---|---|
| **Libellés de contrat** | Les étiquettes de contrat &quot;C&quot; sont utilisées pour classer les données qui ont des obligations contractuelles ou qui sont liées aux politiques de gouvernance des données de votre entreprise. |
| **Données intersites** | Les données intersites sont la combinaison de données provenant de plusieurs sites, y compris une combinaison de données sur site et de données hors site ou une combinaison de données provenant de plusieurs sources hors site. |
| **Gouvernance des données** | La gouvernance des données englobe les stratégies et les technologies utilisées pour s&#39;assurer que les données sont conformes aux règlements et aux politiques de l&#39;entreprise en matière d&#39;utilisation des données. |
| **Responsable de données** | Le responsable de l&#39;intendance des données est la personne responsable de la gestion, de la surveillance et de l&#39;application des ressources de données d&#39;une organisation. Un gestionnaire de données veille également à ce que les politiques de gouvernance des données soient préservées et maintenues pour être conformes aux règlements et aux politiques organisationnelles du gouvernement. |
| **Étiquettes d’utilisation des données** | Les étiquettes d’utilisation des données permettent aux utilisateurs de classer les données en catégories qui reflètent les considérations liées à la vie privée et les conditions contractuelles afin de se conformer aux réglementations et aux politiques de l’entreprise. |
| **Étiquettes de jeux de données** | Les étiquettes peuvent être ajoutées à un jeu de données. Tous les champs d’un jeu de données héritent des étiquettes du jeu de données. |
| **DULE** | DULE est l’acronyme de &quot;Data Usage Labeling and Enforcement&quot; (Étiquetage et application de l’utilisation des données). Un élément clé de la gouvernance des données, DULE est un ensemble de fonctionnalités qui permet d&#39;étiqueter et d&#39;appliquer des politiques d&#39;accès aux données pour répondre aux besoins de gouvernance au sein d&#39;une organisation. |
| **Libellés de champ** | Les libellés de champ sont des libellés de gouvernance des données hérités d’un jeu de données ou appliqués directement à un champ.  Les étiquettes de gouvernance des données appliquées à un champ ne sont pas héritées jusqu’à un jeu de données. |
| **Géofence** | Une géofence est une limite géographique virtuelle, définie par un GPS ou la technologie RFID, qui permet au logiciel de déclencher une réponse lorsqu&#39;un dispositif portable entre dans une zone particulière ou en sort. |
| **Libellés d’identité** | Les étiquettes &quot;I&quot; d’identité sont utilisées pour classer les données qui peuvent identifier ou contacter une personne spécifique. |
| **Ciblage axé sur l’intérêt** | Le ciblage basé sur l’intérêt, également appelé personnalisation, se produit si les trois conditions suivantes sont remplies : les données collectées sur site servent à faire des inférences sur l’intérêt des utilisateurs, sont utilisées dans un autre contexte, tel que sur un autre site ou une autre application (hors site) et servent à sélectionner le contenu ou les publicités qui sont diffusés en fonction de ces inférences. |
| **Action marketing** | Une action marketing, dans le cadre de la gouvernance des données, est une action entreprise par un utilisateur de données de la plateforme d’expérience, pour laquelle il est nécessaire de vérifier les violations des stratégies d’utilisation des données. |
| **Stratégie** | Dans le cadre de la gouvernance des données, une stratégie est une règle qui décrit le type d’actions marketing autorisées ou non pour des données spécifiques. |
| **Étiquettes sensibles** | Les étiquettes &quot;S&quot; sensibles sont utilisées pour classer les données que vous, et votre entreprise, considérez comme sensibles. |

## Ressources supplémentaires

La vidéo suivante vise à vous aider à comprendre la gouvernance des données et présente les principaux aspects de la structure d&#39;étiquetage et d&#39;application de l&#39;utilisation des données (DULE).

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)
