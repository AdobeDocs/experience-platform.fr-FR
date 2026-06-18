---
title: Modèles de configuration de flux de données dynamiques
description: Découvrez  [!DNL Dynamic Datastream Configuration]  modèles et quand utiliser en premier lieu les stratégies de jeu de données Exploitable par rapport à Analytics pour Experience Platform.
source-git-commit: 738597c837440cb66aa80b24f1f877c9c4cb758b
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 0%

---


# Modèles de configuration de trains de données dynamiques

Deux catégories de modèles s’appliquent à [!DNL Dynamic Datastream Configuration] conception de règle : les modèles généraux d’écriture de règles qui s’appliquent à tous les services et les modèles de stratégie de jeu de données spécifiques à [!DNL Adobe Experience Platform]. Chaque catégorie répond à une décision de conception différente et peut être appliquée indépendamment.

Avant de lire cette page, passez en revue la [taxonomie des valeurs d’événement](/help/datastreams/dynamic-configurations/overview.md#event-taxonomy) dans la présentation de la [!DNL Dynamic Datastream Configuration]. Classer vos événements en tant que **Consommable**, **Analytique** ou **Exploitable** est une condition préalable pour choisir le bon modèle.

## Modèles généraux {#general-patterns}

Les modèles suivants s’appliquent à tous les services : [!DNL Adobe Analytics], [!DNL Adobe Target], [!DNL Adobe Audience Manager], transfert d’événement et [!DNL Adobe Experience Platform].

### Règles spécifiques avant règles générales {#granular-before-generic}

Comme Edge Network utilise une évaluation premier match-gagnant, définissez des règles plus spécifiques avant des règles plus larges. Une règle générique placée avant une règle spécifique correspond en premier et Edge Network n’évalue jamais la règle spécifique.

**Exemple :** commencez par placer la règle la plus spécifique, puis la règle plus large :

- Règle 1 (spécifique) : _`eventType`est égal `commerce.purchases` [!DNL AND] `web.webPageDetails.URL` contient`/checkout/confirmation`_
- Règle 2 (large) : _`eventType`égale`commerce.purchases`_

### Règles d’écriture uniquement pour les exceptions {#override-rules}

Comme les événements non correspondants reviennent à la configuration de train de données statique par défaut, vous n’avez pas besoin de règles pour le chemin d’accès à l’événement le plus courant. Définissez des règles uniquement pour le sous-ensemble d’événements qui doit s’écarter de la valeur par défaut.

**Exemple :** un flux de données avec un jeu de données principal non activé pour le profil (`Web Events - Analytics`) et un jeu de données secondaire activé pour le profil (`Web Events - Profile`). Au lieu d’écrire des règles pour tous les types d’événements, écrivez une seule règle pour acheminer les événements **exploitables** vers `Web Events - Profile`. Tous les autres événements sont automatiquement renvoyés au jeu de données principal.

## Modèles de jeux de données Experience Platform {#aep-patterns}

Lors du routage d’événements vers des [!DNL Adobe Experience Platform], choisissez une stratégie de jeu de données principale avant de créer des règles. La stratégie détermine l’emplacement des événements sans correspondance, ce qui est le cas de la majorité des événements dans la plupart des mises en œuvre.

Les deux modèles prennent en charge les mêmes services Edge Network : [!UICONTROL Gestion des décisions], [!UICONTROL Segmentation Edge], [!UICONTROL Destinations Personalization] et [!DNL Adobe Journey Optimizer]. Voir [Paramètres ](/help/datastreams/configure.md#aep) pour les activer dans votre flux de données.

>[!NOTE]
>
>Vous pouvez avoir jusqu’à 5 règles pour [!DNL Adobe Experience Platform], 5 pour [!DNL Adobe Analytics], 5 pour [!DNL Adobe Target], 5 pour [!DNL Adobe Audience Manager] et 5 pour le transfert d’événement, toutes sur le même flux de données. Les limites s’appliquent indépendamment par service.

### Actionnable en premier {#actionable-first}

**Exploitable en premier** signifie que vous donnez la priorité à l’ingestion, à la segmentation et à l’activation des profils en vous assurant que chaque événement va au [!DNL Real-Time Customer Profile] et à tous les services Edge activés, sauf si une règle l’achemine explicitement ailleurs.

Définissez le jeu de données principal (par défaut) sur un jeu de données activé pour le profil. Activez les services Edge [!DNL Adobe Experience Platform] dont vous avez besoin.

Tous les événements se rapportent au lac de données, au [!DNL Real-Time Customer Profile] et à tous les services Edge activés. Écrivez des règles pour acheminer les événements **Analytics** en dehors du profil et pour désactiver les services Edge pour ces événements.

### Analytique en premier {#analytical-first}

**Analytique en premier** signifie que vous donnez la priorité au lac de données par rapport au [!DNL Real-Time Customer Profile] en vous assurant que chaque événement arrive dans un jeu de données ne concernant pas les profils, sauf si une règle le promeut explicitement auprès des services [!DNL Real-Time Customer Profile] et Edge.

Définissez le jeu de données principal (par défaut) sur un jeu de données non activé pour le profil. Activez les services Edge [!DNL Adobe Experience Platform] dont vous avez besoin.

Tous les événements accèdent uniquement au lac de données. Écrivez des règles pour acheminer les événements **exploitables** vers un jeu de données activé pour un profil et activer les services Edge appropriés pour ces événements. Ajoutez des règles pour désactiver les services Edge pour les événements **Analytics** si nécessaire.

## Quand choisir entre utilisable en premier et analytique en premier {#which-pattern}

Choisissez en fonction du type d’événement qui constitue la majorité de votre trafic.

| Considération | Actionnable en premier | Analytique en premier |
|---|---|---|
| **Idéal lorsque** | La plupart de vos événements sont **exploitables** (par exemple, applications transactionnelles, plateformes de fidélité). | La plupart de vos événements sont **Analytiques** (par exemple, les sites web riches en contenu avec un volume de pages vues élevé). |
| **comportement par défaut** | Tous les événements sont redirigés vers le profil. Les règles acheminent les événements **analytiques** loin du profil. | Tous les événements accèdent uniquement au lac de données. Les règles acheminent les événements **exploitables** vers le profil. |
| **Efficacité des règles** | Moins de règles sont nécessaires lorsque les types d’événements **Analytics** sont petits | Moins de règles sont nécessaires lorsque les types d’événement **Exploitables** sont petits |
| **Lorsque les choses tournent mal** | Des événements inattendus apparaissent dans Profile (coût plus élevé, mais aucune perte d’opportunité pour la personnalisation) | Les événements inattendus restent hors de Profile (coût inférieur, mais peuvent manquer les opportunités de personnalisation) |

**Règle de base :** permet d’écrire des règles pour la minorité de vos types d’événements. Si vous disposez de 3 types d’événement **Exploitables** et de 15 types d’événement **Analytiques**, utilisez Analytics en premier et écrivez 3 règles pour promouvoir les événements **Exploitables** au profil. Cela permet de maintenir le nombre de règles dans la limite de 5 règles par service.

## Étapes suivantes

- Voir [Cas d’utilisation de configuration de train de données dynamique](/help/datastreams/dynamic-configurations/use-cases.md) pour des configurations de règles concrètes basées sur ces modèles.
- Consultez l’[exemple complet](/help/datastreams/dynamic-configurations/example.md) pour voir si les deux modèles sont appliqués ensemble dans un scénario de production.
- Suivez les instructions de l’interface utilisateur dans [Créer des configurations de flux de données dynamiques](/help/datastreams/configure-dynamic-datastream.md) pour créer vos règles.
