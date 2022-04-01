---
keywords: Experience Platform;accueil;rubriques populaires;dule;DULE
solution: Experience Platform
title: Présentation des stratégies dʼutilisation des données
topic-legacy: policies
description: Des stratégies d’utilisation des données doivent être mises en œuvre pour que les libellés d’utilisation des données prennent en charge efficacement la conformité des données. Les stratégies d’utilisation des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé ou non à effectuer sur des données d’Experience Platform.
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: 6e4a3ff03a551069efb8dc96f21b82de06cc47d8
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 92%

---

# Présentation des stratégies d’utilisation des données

Des stratégies d’utilisation des données doivent être mises en œuvre pour que les libellés d’utilisation des données prennent en charge efficacement la conformité des données. Les stratégies d’utilisation des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé ou non à effectuer sur des données d’[!DNL Experience Platform].

Deux types de stratégies sont disponibles :

* **[!UICONTROL Politique de gouvernance des données]**: Restreindre l’activation des données en fonction de l’action marketing en cours et des libellés d’utilisation des données transportés par les données en question.
* **[!UICONTROL Stratégie de consentement] (Version bêta)**: Filtrer les profils pouvant être activés sur [destinations](../../destinations/home.md) en fonction du consentement ou des préférences de vos clients

Ce document fournit une présentation de haut niveau des stratégies dʼutilisation des données et fournit des liens vers la documentation supplémentaire sur lʼutilisation des stratégies dans lʼUI ou lʼAPI.

## Actions marketing {#marketing-actions}

Les actions marketing (également appelées cas dʼutilisation marketing), dans le contexte du cadre de gouvernance des données, sont des actions quʼun utilisateur de données [!DNL Experience Platform] peut entreprendre et pour lesquelles votre entreprise souhaite restreindre lʼutilisation des données. En tant que telle, une stratégie dʼutilisation des données est définie par les éléments suivants :

1. Une action marketing spécifique
2. Les conditions dans lesquelles cette action n’est pas exécutée

Un exemple d’action marketing peut être le souhait d’exporter un jeu de données vers un service tiers. S’il existe une stratégie en place indiquant que des types de données spécifiques (comme les informations d’identification personnelle ou PII) ne peuvent pas être exportés et que vous tentez d’exporter un jeu de données contenant un libellé « I » (données d’identité), vous recevez une réponse de [!DNL Policy Service] vous informant qu’une stratégie d’utilisation des données a été enfreinte.

>[!NOTE]
>
>En tant que telles, les actions marketing ne limitent pas l’utilisation des données. Elles doivent être incluses dans les stratégies d’utilisation des données activées afin que ces actions soient évaluées en cas de violation des stratégies.

Lorsque des données sont utilisées dans le service de votre organisation, les actions marketing appropriées doivent être indiquées afin que toute violation de stratégie puisse être identifiée. Vous pouvez ensuite utiliser l’[API Policy Service](https://www.adobe.io/experience-platform-apis/references/policy-service/) pour vérifier les violations de stratégie dans votre intégration.

>[!NOTE]
>
>Vous pouvez configurer des cas d’utilisation marketing sur des destinations afin d’automatiser l’application des stratégies. Voir [documentation sur les destinations](../../destinations/home.md) pour plus d’informations sur les options de configuration de votre destination spécifique.

Voir l’annexe du présent document pour obtenir une liste des [actions marketing définies par Adobe disponibles](#core-actions). Vous pouvez également définir vos propres actions marketing personnalisées à l’aide de l’API [!DNL Policy Service] ou de l’interface utilisateur d’[!DNL Experience Platform]. Vous trouverez plus d’informations sur l’utilisation des actions marketing et des stratégies dans la section suivante.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## Gestion des stratégies d’utilisation des données {#manage}

Une fois les libellés d’utilisation des données appliqués, les gestionnaires de données peuvent utiliser l’API [!DNL Policy Service] ou l’interface utilisateur d’[!DNL Experience Platform] pour gérer et évaluer les stratégies liées aux actions marketing effectuées sur les données contenant des libellés d’utilisation des données. Vous pouvez créer et mettre à jour des stratégies, déterminer l’état d’une stratégie et utiliser des actions marketing pour évaluer si une action spécifique enfreint une stratégie d’utilisation des données.

>[!IMPORTANT]
>
>Toutes les stratégies d’utilisation des données (y compris les stratégies de base fournies par Adobe) sont désactivées par défaut. Pour qu’une stratégie individuelle soit prise en compte pour l’application, vous devez l’activer manuellement par le biais de l’API ou de l’interface utilisateur.

Pour obtenir des instructions détaillées sur l’utilisation des actions marketing et des stratégies d’utilisation des données dans l’API, consultez le tutoriel sur la [création et l’évaluation des stratégies d’utilisation des données](create.md). Pour plus d’informations sur les opérations clés fournies par l’API [!DNL Policy Service], consultez le [guide de développement de Policy Service](../api/getting-started.md).

Pour plus d’informations sur l’utilisation des actions marketing et des stratégies dans l’interface utilisateur de [!DNL Platform], consultez le [guide d’utilisation des stratégies d’utilisation des données](./user-guide.md).

## Étapes suivantes

Ce document est une introduction aux stratégies d’utilisation des données dans le cadre de la gouvernance des données. Vous pouvez maintenant poursuivre votre lecture en consultant la documentation relative au processus référencée tout au long de ce guide pour en savoir plus sur l’utilisation des stratégies dans l’API et l’interface utilisateur.

## Annexe

La section suivante fournit des informations supplémentaires sur les stratégies d’utilisation des données.

### Actions marketing définies par Adobe {#core-actions}

Le tableau ci-dessous décrit les principales actions marketing prêtes à l’emploi fournies par Adobe.

>[!NOTE]
>
>Les principales actions marketing doivent être considérées comme un point de départ pour vous aider à identifier les stratégies d’utilisation à créer et à vérifier en cas de violation. Les définitions et leur interprétation dépendent des besoins et des stratégies de votre organisation.

| Action marketing | Description |
| --- | --- |
| Intégration | Action qui utilise des données à des fins d’analyse, telles que la mesure, l’analyse et le compte rendu des performances de l’utilisation par les clients des sites ou applications de votre organisation. |
| Combinaison avec des données directement identifiables | Action qui combine des informations d’identification personnelle (PII) avec des données anonymes. Les contrats relatifs aux données provenant de réseaux publicitaires, de serveurs de publicités et de fournisseurs de données tiers comportent souvent des interdictions contractuelles spécifiques concernant l’utilisation de ces données avec des données directement identifiables. |
| Ciblage intersite | Action qui utilise des données pour le ciblage publicitaire intersite. La combinaison de données provenant de plusieurs sites, y compris une combinaison de données sur site et de données hors site ou une combinaison de données provenant de plusieurs sources hors site, est appelée données intersites. Les données intersites sont généralement collectées et traitées afin d’établir des inférences sur les intérêts des utilisateurs. |
| Science des données | Action qui utilise les données pour les workflows relatifs à la science des données. Certains contrats prévoient des interdictions explicites sur l’utilisation des données pour la science des données. Parfois, elles sont formulées en des termes qui interdisent l’utilisation de données pour l’intelligence artificielle (AI), l’apprentissage automatique (ML) ou la modélisation. |
| Ciblage e-mail | Action qui utilise les données dans les campagnes de ciblage e-mail. |
| Exportation vers un tiers | Action qui exporte des données vers des responsables du traitement et des entités qui n’ont pas de relations directes avec les clients. De nombreux fournisseurs de données ont des clauses dans leurs contrats qui interdisent l’exportation de données à partir de l’endroit où elles ont été collectées à l’origine. Par exemple, les contrats de réseau social limitent souvent le transfert des données que vous recevez de leur part. |
| Publicités sur site | Action qui utilise des données pour les publicités sur site, notamment la sélection et la diffusion des publicités sur les sites web ou applications de votre organisation, ou pour mesurer la diffusion et l’efficacité de ces publicités. |
| Personnalisation sur site | Action qui utilise des données pour la personnalisation du contenu sur site. La personnalisation sur site correspond à toutes les données utilisées pour faire des inférences sur les intérêts des utilisateurs et qui servent à sélectionner le contenu ou les publicités diffusés en fonction de ces inférences. |
| Correspondance de segments | Action qui utilise des données pour le service Correspondance de segments dʼAdobe Experience Platform et qui permet à deux ou plusieurs utilisateurs Platform dʼéchanger des données de segments. En activant les stratégies qui font référence à cette action, vous pouvez limiter les données utilisées pour la Correspondance de segments. Par exemple, si la stratégie de base « Limiter le partage des données » est activée, les données avec un [libellé C11](../labels/reference.md#c11) ne peuvent pas être utilisées pour la correspondance de segments. |
| Personnalisation d’identité unique | Action qui nécessite l’utilisation d’une identité unique à des fins de personnalisation au lieu de regrouper des identités provenant de plusieurs sources. |
