---
title: Bonnes pratiques relatives aux configurations de flux de données dynamiques
description: Découvrez les bonnes pratiques de conception, d’organisation et d’exploitation  [!DNL Dynamic Datastream Configuration]  règles pour garantir un routage d’événement et des performances système fiables.
source-git-commit: 19e297602d67a360a3b6bcdd6d5403fb6090de7f
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---


# Bonnes pratiques pour [!DNL Dynamic Datastream Configurations]

Utilisez ces pratiques lorsque vous concevez et utilisez des règles [!DNL Dynamic Datastream Configuration]. Ils vous aident à gérer les [mécanismes de sécurisation système](/help/datastreams/dynamic-configurations/configure.md#guardrails), à éviter les erreurs courantes et à maintenir des configurations faciles à comprendre et à résoudre les problèmes.

## Conception de règle {#rule-design}

**Utiliser des flux de données distincts par source d’événement.** Pensez à créer un flux de données pour Web SDK, un pour Mobile SDK et un pour l’API Server. Si vos données proviennent d’une autre source ou utilisent un autre schéma XDM, créez un flux de données distinct. Un flux de données dédié avec ses propres jeux de données correspondants améliore la traçabilité et simplifie la résolution des problèmes. Les règles de configuration des trains de données dynamiques gèrent ensuite le routage dans chaque train de données.

**Simplifiez et aplatissez les règles.** Les configurations de train de données dynamiques ne prennent pas en charge les expressions logiques imbriquées. Si votre logique nécessite l’imbrication, divisez-la en plusieurs règles aplaties. Des règles plus simples sont plus rapides à évaluer, plus faciles à auditer et moins susceptibles de produire des correspondances inattendues.

**Utilisez `eventType` comme condition principale.** `eventType` est le discriminateur le plus fiable et le plus performant pour les décisions de routage. Il est systématiquement renseigné sur les implémentations de Web SDK, Mobile SDK et de l’API du serveur et possède un ensemble de valeurs bien défini. Pratiquement tous les cas d’utilisation doivent commencer par une condition basée sur `eventType`, éventuellement combinée à des conditions secondaires.

**Classer les règles par priorité : Consommable en premier, puis Exploitable, puis Analytique.** Comme Edge Network utilise une évaluation first-match-wins, l’ordre de vos règles détermine le résultat pour les événements qui peuvent correspondre à plusieurs conditions.

Ordre recommandé :

1. Trafic de robots : **Consommable** ou quarantaine
2. Événements système (`decisioning.propositionFetch`, `personalization.request`) : mise en quarantaine
3. Événements **exploitables** : acheminer vers un jeu de données activé pour un profil
4. Événements **analytiques** : acheminer vers un jeu de données ne concernant pas les profils

Placer des règles **consommables** permet de s’assurer que Edge Network intercepte le trafic nuisible ou opérationnel avant de prendre des décisions de routage coûteuses telles que l’ingestion de profils ou la personnalisation entrante.

**Concevez votre itinéraire par défaut de manière prudente.** Configurez le jeu de données d’événement de [!DNL Adobe Experience Platform] par défaut du flux de données en un jeu de données non activé pour le profil. Les événements inattendus ou non classés arrivent ensuite dans le lac de données au lieu de gonfler votre banque de profils. Vous pouvez toujours ajouter une règle spécifique pour promouvoir un type d’événement récemment découvert dans le profil une fois que vous l’avez classé.

## Stratégie du jeu de données {#dataset-strategy}

**Créer des jeux de données avant de configurer des règles.** Tous les jeux de données cibles doivent exister avec le schéma correct avant de les référencer dans les configurations de routage. Après avoir validé vos règles à l’aide d’Assurance, activez le profil, configurez la conservation des données et mettez à jour votre connexion [!DNL Customer Journey Analytics].

Pour obtenir des conseils sur la configuration de la conservation des données, consultez le [&#x200B; Guide de conservation des jeux de données des événements Experience &#x200B;](/help/catalog/datasets/experience-event-dataset-retention-ttl-guide.md).

**Utilisez une convention de nommage cohérente.** Des noms de jeux de données clairs facilitent l’identification de l’objectif de chaque jeu de données lors de la révision de votre configuration ou de la surveillance de l’ingestion. Un modèle recommandé :

- `[Brand] Web Events - Profile (90d)`
- `[Brand] Web Events - Analytics (12mo)`
- `[Brand] Bot Traffic - Quarantine (30d)`
- `[Brand] System Events - Quarantine (30d)`

**Aligner votre connexion [!DNL Customer Journey Analytics] sur votre stratégie de jeu de données.** Après avoir configuré [!DNL Dynamic Datastream Configuration] routage des règles et des événements vers des jeux de données distincts, mettez à jour votre connexion [!DNL Customer Journey Analytics] pour inclure uniquement les jeux de données qui doivent être utilisés dans les rapports. Excluez les jeux de données de quarantaine pour le trafic de robots et les événements système. Pour plus d’informations, consultez la documentation sur les connexions [&#128279;](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview){target="_blank"}.

## Pratiques opérationnelles {#operational}

**Compter 15 minutes pour que les modifications se propagent.** Les modifications apportées à la configuration des flux de données, y compris les règles de [!DNL Dynamic Datastream Configuration] nouvelles ou mises à jour, prennent jusqu’à 15 minutes pour se propager dans Edge Network. Ne pas tester immédiatement après avoir enregistré les modifications. Patientez dans la fenêtre de propagation complète avant d’exécuter les sessions Assurance ou de comparer les volumes d’ingestion du jeu de données.

**Supprimez les remplacements côté client avant d’activer les règles.** [Remplacements de la configuration des trains de données](/help/datastreams/overrides.md) ont priorité sur les règles de [!DNL Dynamic Datastream Configuration]. Tout événement qui comporte un remplacement côté client contourne vos règles de manière silencieuse, sans erreur ni avertissement. Avant d’activer les règles, vérifiez l’implémentation de votre SDK web ou de Mobile SDK pour supprimer les `edgeConfigOverrides` des appels [`sendEvent`](/help/collection/js/commands/sendevent/overview.md) et [`configure`](/help/collection/js/commands/configure/overview.md) pour les événements que [!DNL Dynamic Datastream Configurations] devez gérer.

**Surveiller après le déploiement.** Après avoir activé les règles en production, surveillez les éléments suivants pour confirmer un comportement correct :

- **Volumes d’ingestion des jeux de données** dans [!DNL Adobe Experience Platform] > **[!UICONTROL Jeux de données]** : vérifiez que les événements se trouvent dans les jeux de données attendus et que les volumes correspondent à vos projections.
- **Débit d’ingestion en flux continu et volume total de données** : vérifiez l’impact dans les volumes d’ingestion en flux continu proportionnel aux événements désormais acheminés loin des jeux de données activés pour le profil. Vérifiez l’impact sur le volume total de données en tenant compte des fenêtres d’expiration de rétention.
- **[!DNL Customer Journey Analytics]workspace** : si vous avez exclu des jeux de données ou supprimé des types d’événements, confirmez que ces événements n’apparaissent plus dans vos rapports.

## Étapes suivantes

- Consultez [Tester et valider [!DNL Dynamic Datastream Configurations]](/help/datastreams/dynamic-configurations/testing.md) pour obtenir une liste de contrôle de test détaillée.
- Consultez [Cas d’utilisation de configuration de train de données dynamique](/help/datastreams/dynamic-configurations/use-cases.md) pour des configurations de règle de référence.
- Consultez le [FAQ](/help/datastreams/dynamic-configurations/faq.md) pour obtenir des réponses aux questions courantes sur le comportement des règles et les interactions système.
