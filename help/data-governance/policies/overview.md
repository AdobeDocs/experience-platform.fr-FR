---
keywords: Experience Platform ; accueil ; rubriques populaires ; calendrier ; DUL
solution: Experience Platform
title: Présentation des stratégies d’utilisation des données
topic-legacy: policies
description: Des stratégies d’utilisation des données doivent être mises en œuvre pour que les libellés d’utilisation des données prennent en charge efficacement la conformité des données. Les stratégies d’utilisation des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé ou non à effectuer sur des données d’Experience Platform.
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 17%

---

# Présentation des stratégies d’utilisation des données

Des stratégies d’utilisation des données doivent être mises en œuvre pour que les libellés d’utilisation des données prennent en charge efficacement la conformité des données. Les stratégies d’utilisation des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé à exécuter, ou dont vous êtes limité à l’exécution, sur les données dans [!DNL Experience Platform].

Ce document fournit un aperçu général des stratégies d’utilisation des données et fournit des liens vers d’autres documents sur l’utilisation des stratégies dans l’interface utilisateur ou l’API.

## Actions marketing {#marketing-actions}

Les actions marketing (également appelées cas d’utilisation marketing) dans le cadre de la gouvernance des données sont des actions qu’un utilisateur de données [!DNL Experience Platform] peut entreprendre, pour lesquelles votre entreprise souhaite limiter l’utilisation des données. Ainsi, une stratégie d’utilisation des données est définie par les éléments suivants :

1. Une action marketing spécifique
2. Étiquette(s) d&#39;utilisation des données pour laquelle l&#39;action est limitée ne peut pas être exécutée

Un exemple d’action marketing peut être le souhait d’exporter un jeu de données vers un service tiers. Si une stratégie indique que des types de données spécifiques (tels que les informations d&#39;identification personnelle) ne peuvent pas être exportés et que vous tentez d&#39;exporter un jeu de données contenant une étiquette &quot;I&quot; (données d&#39;identité), vous recevrez une réponse de la part de [!DNL Policy Service] vous informant qu&#39;une stratégie d&#39;utilisation des données a été violée.

>[!NOTE]
>
>Les actions marketing ne limitent pas l’utilisation des données. Ils doivent être inclus dans les stratégies d’utilisation des données activées pour que ces actions soient évaluées en cas de violation des stratégies.

Lorsque des données sont utilisées dans le service de votre entreprise, les actions marketing appropriées doivent être indiquées afin que toute violation de stratégie puisse être identifiée. Vous pouvez ensuite utiliser l&#39;[API de service de stratégie](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) pour vérifier les violations de stratégie dans votre intégration.

>[!NOTE]
>
>Si vous utilisez [!DNL Real-time Customer Data Platform], vous pouvez configurer des cas d’utilisation marketing sur des destinations afin d’automatiser l’application des stratégies. Pour plus d&#39;informations, consultez le document sur la [gouvernance des données dans le CDP en temps réel](../../rtcdp/privacy/data-governance-overview.md).

Voir l&#39;annexe du présent document pour obtenir une liste des [actions marketing définies par l&#39;Adobe ](#core-actions) disponibles. Vous pouvez également définir vos propres actions marketing personnalisées à l’aide de l’API [!DNL Policy Service] ou de l’interface utilisateur [!DNL Experience Platform ]. Vous trouverez plus d’informations sur l’utilisation des actions et stratégies marketing dans la section suivante.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## Gestion des stratégies d&#39;utilisation des données {#manage}

Une fois les libellés d’utilisation des données appliqués, les responsables de données peuvent utiliser l’API [!DNL Policy Service] ou l’interface utilisateur [!DNL Experience Platform] pour gérer et évaluer les stratégies liées aux actions marketing effectuées sur les données contenant des libellés d’utilisation des données. Vous pouvez créer et mettre à jour des stratégies, déterminer l’état d’une stratégie et travailler avec des actions marketing pour évaluer si une action spécifique viole une stratégie d’utilisation des données.

>[!IMPORTANT]
>
>Toutes les stratégies d’utilisation des données (y compris les stratégies de base fournies par l’Adobe) sont désactivées par défaut. Pour qu’une stratégie individuelle soit prise en compte pour l’application, vous devez l’activer manuellement par le biais de l’API ou de l’interface utilisateur.

Pour obtenir des instructions détaillées sur l’utilisation des actions marketing et des stratégies d’utilisation des données dans l’API, consultez le didacticiel [Création et évaluation des stratégies d’utilisation des données](create.md). Pour plus d&#39;informations sur les opérations clés fournies par l&#39;API [!DNL Policy Service], consultez le [Guide du développeur de Policy Service](../api/getting-started.md).

Pour plus d&#39;informations sur la manière d&#39;utiliser les actions et stratégies marketing dans l&#39;[!DNL Platform] interface utilisateur, consultez le [guide d&#39;utilisateur des stratégies d&#39;utilisation des données](./user-guide.md).

## Étapes suivantes

Ce document présente les politiques d&#39;utilisation des données dans la structure [!DNL Data Governance]. Vous pouvez maintenant continuer à lire la documentation de processus liée à tout au long de ce guide pour en savoir plus sur l’utilisation des stratégies dans l’API et l’interface utilisateur.

## Annexe

La section suivante fournit des informations supplémentaires sur les stratégies d’utilisation des données.

### Actions marketing définies par Adobe {#core-actions}

Le tableau ci-dessous décrit les principales actions marketing fournies par Adobe.

>[!NOTE]
>
>Les actions marketing de base doivent être considérées comme un point de départ pour vous aider à identifier les stratégies d’utilisation à créer et à vérifier les violations. Les définitions et leur interprétation dépendent des besoins et des stratégies de votre entreprise.

| Action marketing | Description |
| --- | --- |
| Intégration    | Action qui utilise les données à des fins d’analyse, telles que la mesure, l’analyse et le rapports de l’utilisation par les clients des sites ou applications de votre entreprise. |
| Combiner avec les informations d’identification personnelle | Action qui combine des informations d’identification personnelle (informations d’identification personnelle) avec des données anonymes. Les contrats portant sur des données provenant de réseaux publicitaires, de serveurs d’annonces et de fournisseurs de données tiers comportent souvent des interdictions contractuelles spécifiques concernant l’utilisation de ces données à l’aide de données directement identifiables. |
| Ciblage sur plusieurs sites | Action qui utilise les données pour le ciblage publicitaire sur plusieurs sites. La combinaison de données provenant de plusieurs sites, y compris une combinaison de données sur site et de données hors site ou une combinaison de données provenant de plusieurs sources hors site, est appelée données intersites. Les données intersites sont généralement collectées et traitées afin d’en déduire les intérêts des utilisateurs. |
| Science des données | Action qui utilise les données pour les workflows de science de données. Certains contrats prévoient des interdictions explicites sur l’utilisation des données pour la science des données. Parfois, elles sont formulées en des termes qui interdisent l’utilisation de données pour l’intelligence artificielle (AI), l’apprentissage automatique (ML) ou la modélisation. |
| Ciblage des e-mails | Action qui utilise les données dans les campagnes de ciblage par courriel. |
| Exportation vers un tiers | Action qui exporte des données vers des processeurs et des entités qui n’ont pas de relations directes avec les clients. De nombreux fournisseurs de données ont des clauses dans les contrats qui interdisent l&#39;exportation de données d&#39;où elles ont été collectées à l&#39;origine. Par exemple, les contrats de réseau social limitent souvent le transfert des données que vous recevez de leur part. |
| Publicité sur site | Action qui utilise des données pour les publicités sur site, y compris la sélection et la diffusion des publicités sur les sites Web ou les applications de votre entreprise, ou pour mesurer la diffusion et l’efficacité de ces publicités. |
| Personnalisation sur site | Action qui utilise les données pour la personnalisation du contenu sur site. La personnalisation sur site est toute donnée utilisée pour faire des inférences sur les intérêts des utilisateurs et sert à sélectionner le contenu ou les publicités qui sont diffusés en fonction de ces inférences. |
| Personnalisation d’identité unique | Action qui nécessite l’utilisation d’une identité unique à des fins de personnalisation au lieu d’assembler des identités provenant de plusieurs sources. |
