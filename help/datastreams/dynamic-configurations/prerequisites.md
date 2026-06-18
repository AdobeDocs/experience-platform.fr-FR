---
title: Conditions Préalables De Configuration Des Flux De Données Dynamiques
description: Découvrez comment préparer votre flux de données, vos schémas, vos jeux de données et votre inventaire des événements avant de configurer  [!DNL Dynamic Datastream Configuration]  règles afin d’éviter les erreurs de configuration.
source-git-commit: 738597c837440cb66aa80b24f1f877c9c4cb758b
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---


# Prérequis et liste de contrôle de planification

Procédez comme suit avant de configurer des règles [!DNL Dynamic Datastream Configuration]. Il s’agit des sources les plus courantes de règles mal configurées et de comportement de routage inattendu.

## Configuration du flux de données {#datastream-setup}

Votre flux de données doit exister et tous les services requis doivent être activés avant d’ajouter des règles. Voir [Configurer un flux de données](/help/datastreams/configure.md) et [Ajouter des services à un flux de données](/help/datastreams/configure.md#add-services) pour obtenir des instructions de configuration.

Selon les services que vous prévoyez d’utiliser :

- **[!DNL Adobe Analytics]:** configurer au moins une suite de rapports. Vous pouvez ajouter d’autres suites de rapports sous **[!UICONTROL Options avancées]** comme [&#x200B; remplacements de suites de rapports](/help/datastreams/configure.md#analytics).
- **[!DNL Adobe Target]:** Configurez au moins un jeton de propriété. Vous pouvez ajouter d’autres jetons de propriété sous **[!UICONTROL Options avancées]** comme [remplacements de jeton de propriété](/help/datastreams/configure.md#target).
- **[!DNL Adobe Audience Manager]:** Aucune configuration supplémentaire n’est requise. Voir [Paramètres &#x200B;](/help/datastreams/configure.md#audience-manager).
- **[!DNL Event Forwarding]:** permet de configurer une propriété. Voir [Paramètres Transfert d’événement](/help/datastreams/configure.md#event-forwarding).
- **[!DNL Adobe Experience Platform]:**
   - [Configurez un jeu de données d’événement principal](/help/datastreams/configure.md#aep). Ce jeu de données reçoit tous les événements qui ne correspondent à aucune règle (solution de secours par défaut).
   - Configurez des jeux de données d’événement secondaires supplémentaires vers lesquels vos règles achemineront les événements. Si ces jeux de données n’existent pas encore, effectuez l’étape [Préparation du schéma et du jeu de données](#schema-dataset) avant de configurer des règles.
   - Activez les [!DNL Adobe Experience Platform] services Edge dont vous avez besoin, notamment **[!UICONTROL Gestion des décisions]**, **[!UICONTROL Segmentation Edge]**, **[!UICONTROL Destinations Personalization]** ou **[!UICONTROL Adobe Journey Optimizer]**. Voir [Paramètres &#x200B;](/help/datastreams/configure.md#aep).

## Préparation des schémas et des jeux de données {#schema-dataset}

Préparez vos schémas et jeux de données avant de configurer des règles. Les jeux de données doivent exister avant de pouvoir les référencer dans les configurations de routage.

- Définissez le schéma XDM pour [!DNL Dynamic Datastream Configuration] conditions dans la section **[!UICONTROL Schéma de mappage]** du flux de données (voir [Créer un flux de données](/help/datastreams/configure.md#create)).
- Vérifiez que votre schéma XDM inclut tous les champs que vous prévoyez d’utiliser comme conditions de règle, par exemple les champs `eventType`, les champs personnalisés de la couche de données ou les champs géographiques.
- Si vous prévoyez d’utiliser des règles de filtrage de robots, ajoutez le groupe de champs **[!UICONTROL Informations sur la détection des robots]** à votre schéma XDM et activez [détection des robots](/help/datastreams/bot-detection.md) sur le flux de données. Patientez jusqu’à 15 minutes pour que les règles de détection des robots se propagent avant le test.
- [Créez tous les jeux de données cibles](/help/catalog/datasets/user-guide.md#schema) avant de configurer des règles, en utilisant le schéma et la convention d’affectation de nom appropriés. Après avoir validé vos règles, vous pouvez activer le profil, configurer la conservation des données et activer les connexions [!DNL Customer Journey Analytics].

Pour plus d’informations sur la configuration des fenêtres de conservation des jeux de données, consultez le [Guide de conservation des jeux de données Experience Event](/help/catalog/datasets/experience-event-dataset-retention-ttl-guide.md).

>[!TIP]
>
>Créez d’abord des jeux de données sans activer de profil. Vérifiez que les événements sont acheminés vers les jeux de données corrects à l’aide de [&#128279;](/help/assurance/home.md), puis activez les paramètres de profil et de conservation des données. Cela empêche d’abord l’ingestion d’événements inutiles dans le [!DNL Real-Time Customer Profile].

## Inventaire des événements {#event-inventory}

Cataloguez chaque type d’événement envoyé par votre implémentation et classez chacun d’eux avant de créer une règle unique.

1. **Répertorier tous les types d’événements.** Les exemples courants incluent `web.webpagedetails.pageViews`, `commerce.purchases`, `commerce.productViews`, `commerce.productListAdds`, `decisioning.propositionFetch` et `personalization.request`.

2. **Classez chaque événement** à l’aide de la [taxonomie des valeurs d’événement](/help/datastreams/dynamic-configurations/overview.md#event-taxonomy) :
   - **Consommable :** aucune valeur analytique ou exploitable (trafic de robots, événements système)
   - **Analytique :** nécessaire pour les rapports d’analyse uniquement, et non pour l’enrichissement ou la segmentation des profils
   - **Exploitable :** nécessaire pour l’enrichissement, la segmentation et l’activation des profils. Également disponible pour la création de rapports Analytics

3. **Identifier les événements dépendants de l’audience.** Passez en revue les définitions d’audience et notez les types d’événement auxquels ces audiences font référence. Le routage de ces événements en dehors d’un jeu de données activé pour le profil empêche l’[!DNL Real-Time Customer Profile] de les ingérer, ce qui entraîne l’arrêt de l’évaluation correcte des audiences.

4. **Identifier les champs de condition fiables.** Choisissez des champs qui sont renseignés de manière cohérente et qui disposent d’un petit ensemble de valeurs prévisibles. `eventType` est le champ de condition principal recommandé pour la plupart des règles. Les autres champs utiles sont les champs `botDetection.score`, `web.webPageDetails.URL` et de couche de données personnalisés mappés via [Préparation des données pour la collecte de données](/help/datastreams/data-prep.md).

## Supprimer les remplacements côté client en conflit {#remove-overrides}

[Remplacements de la configuration des trains de données](/help/datastreams/overrides.md) ont priorité sur les règles de [!DNL Dynamic Datastream Configuration]. Tout événement qui comporte un remplacement côté client contourne vos règles de manière silencieuse, sans erreur ni avertissement.

Avant d’activer les règles :

- Vérifiez que votre implémentation de SDK web ou de Mobile SDK n’envoie pas de [`edgeConfigOverrides`](/help/collection/js/commands/sendevent/edgeconfigoverrides.md) dans les appels [`sendEvent`](/help/collection/js/commands/sendevent/overview.md) ou [`configure`](/help/collection/js/commands/configure/overview.md) pour les événements que vos règles doivent gérer.
- Pour chaque type d’événement que vous déplacez vers [!DNL Dynamic Datastream Configuration] règles, supprimez la `edgeConfigOverrides` correspondante de votre code SDK avant d’activer la règle.

## Étapes suivantes

Après avoir terminé cette liste de contrôle, vous êtes prêt à concevoir vos règles :

- Lisez [Modèles de configuration de train de données dynamique](/help/datastreams/dynamic-configurations/configuration-patterns.md) pour choisir la bonne stratégie de jeu de données.
- Voir [Cas d’utilisation de la configuration dynamique des trains de données](/help/datastreams/dynamic-configurations/use-cases.md) pour obtenir des configurations de règles détaillées.
- Suivez les instructions de l’interface utilisateur dans [Créer des configurations de flux de données dynamiques](/help/datastreams/configure-dynamic-datastream.md) pour créer et enregistrer vos règles.
