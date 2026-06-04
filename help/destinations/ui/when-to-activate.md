---
title: Quand activer
description: Découvrez la fonctionnalité Quand activer pour les destinations de diffusion en streaming et comment l’utiliser pour contrôler quelles modifications de profil déclenchent des exportations vers vos destinations.
badgeBeta: label="Beta" type="Informative"
source-git-commit: c7a0556e47b5440ffeb7f3770b577584e73ee204
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 3%

---


# Quand activer

>[!IMPORTANT]
>
>Cette fonctionnalité est actuellement en version bêta. Les fonctionnalités et la documentation sont susceptibles d’être modifiées. Cette fonctionnalité est également disponible uniquement à la demande. Contactez votre représentant Adobe pour obtenir l’accès.

Par défaut, Adobe Experience Platform exporte des données vers une destination chaque fois qu’une modification se produit sur un profil : une mise à jour d’attribut, une qualification ou une disqualification d’audience ou un changement d’identité. Cela peut générer un grand volume d&#39;exportations, dont un grand nombre ne comporte aucun changement significatif pour les systèmes en aval.

**[!UICONTROL Quand activer]** permet un contrôle précis des types de modifications de profil qui déclenchent des exportations pour un flux de données de destination donné. Vous pouvez activer ou désactiver chaque type de déclencheur indépendamment. La désactivation d’un type de déclencheur supprime les exportations causées uniquement par ce type de modification.

## Types de destination pris en charge {#supported-destinations}

La fonction **[!UICONTROL Quand activer]** est prise en charge pour les types de destination suivants :

- Destinations basées sur les API de streaming
- Destinations d’entreprise : [[!DNL HTTP API]](/help/destinations/catalog/streaming/http-destination.md), [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md) et [[!DNL Snowflake Streaming]](/help/destinations/catalog/warehouses/snowflake.md).

## Types de déclencheurs d’activation {#trigger-types}

>[!CONTEXTUALHELP]
>id="platform_destinations_activation_triggers"
>title="Quand activer"
>abstract="Sélectionnez les types de modifications de profil qui déclenchent des exportations vers cette destination. Les trois déclencheurs sont activés par défaut. <ul><li><b>Modifications d’attribut :</b> les attributs de profil sont mis à jour à partir de toute source de données en amont.</li><li><b>Modifications de segmentation </b> le profil entre ou sort d’une audience évaluée par le service de segmentation d’Experience Platform.</li><li><b>Modifications d’identité :</b> graphique d’identité de profil est mis à jour, par exemple lorsqu’une nouvelle identité est ajoutée.</li></ul>"

Le tableau ci-dessous décrit chaque type de déclencheur. Les Triggers sont répertoriés dans l&#39;ordre du volume d&#39;exportation attendu, du plus élevé au plus bas.

![Le panneau Quand activer affiche quatre cases à cocher : modifications des attributs, modifications de la segmentation, modifications de la segmentation externe et modifications des identités, toutes activées.](../assets/ui/when-to-activate/when-to-activate.png)

>[!NOTE]
>
>Les quatre types de déclencheur sont activés par défaut. Si vous disposiez de flux de données existants avant la publication de cette fonctionnalité, leur comportement reste inchangé, sauf si vous mettez explicitement à jour les paramètres.

| Type de déclencheur | Qu’est-ce qui le déclenche ? | Quand le désactiver |
| --- | --- | --- |
| **[!UICONTROL Modifications d’attribut]** | Tous les attributs mappés du profil sont mis à jour. | Vous souhaitez supprimer les mises à jour d’attributs haute fréquence déclenchant des exportations vers une API partenaire. |
| **[!UICONTROL Modifications de segmentation]** | Un profil entre ou sort d’une audience évaluée par [!DNL Experience Platform] Segmentation Service. |  |
| **[!UICONTROL Modifications d’identité]** | Le graphique d’identités d’un profil change, par exemple lorsqu’une nouvelle identité est ajoutée ou qu’une identité existante est mise à jour. | Une nouvelle identité, telle qu’un ECID provenant d’une visite sur le site web, est ajoutée à un profil, et vous ne souhaitez pas que cela déclenche une communication ou une exportation vers la destination. |

{style="table-layout:auto"}

## Comportement par défaut {#default-behavior}

Les trois types de déclencheur sont activés sur chaque flux de données nouveau et existant. Lorsque vous désactivez un ou plusieurs déclencheurs, les exportations provoquées par ce type de déclencheur sont supprimées. Les exportations qui résultent d’une combinaison de types de déclencheur se déclenchent toujours si au moins un déclencheur activé a provoqué la modification.

## Bonnes pratiques {#best-practices}

La meilleure configuration de déclenchement dépend de votre cas d’utilisation. Utilisez les conseils suivants comme point de départ.

**Désactivez d’abord les modifications d’identité.** La désactivation du déclencheur de changements d’identité est la première étape la moins risquée pour réduire le volume d’exportation. De nouvelles identités, telles que les ECID provenant de visites sur le site web, sont fréquemment ajoutées aux profils et représentent rarement des modifications significatives pour votre système en aval.

**Désactivez les modifications d’attribut pour la plus grande réduction de volume.** L’attribut change se déclenche chaque fois qu’un attribut mappé est mis à jour, y compris lors de l’ingestion par lots quotidienne qui redéfinit les valeurs inchangées. La désactivation de ce déclencheur entraîne la réduction la plus importante du volume d’exportation pour la plupart des organisations.

**Gardez les modifications de segmentation activées.** Les événements d’entrée et de sortie d’audience sont généralement les signaux les plus significatifs pour les systèmes en aval tels que les CRM et les plateformes publicitaires. La plupart des entreprises gardent ce déclencheur activé.

Chaque organisation possède différents cas d’utilisation, de sorte que différentes combinaisons de déclencheurs peuvent s’appliquer. Contactez votre gestionnaire de compte Adobe ou l’assistance clientèle pour obtenir des conseils adaptés à votre configuration d’activation.

## Configurer le moment d’activation {#configure}

Vous pouvez configurer les paramètres **[!UICONTROL Quand activer]** à deux endroits :

- **Lors de la configuration de l’activation :** l’étape **[!UICONTROL Quand activer]** apparaît dans le workflow d’activation lorsque vous configurez une destination basée sur une API de streaming ou une destination d’entreprise. Voir [Activer les audiences vers des destinations de diffusion en continu](/help/destinations/ui/activate-segment-streaming-destinations.md#when-to-activate) et [Activer les audiences vers des destinations d’exportation de profils de diffusion en continu](/help/destinations/ui/activate-streaming-profile-destinations.md#when-to-activate).
- **Sur les flux de données existants :** utilisez le contrôle **[!UICONTROL Modifier la destination]** sur un flux de données pour modifier les paramètres à tout moment. Voir [Modifier les flux de données d’activation](/help/destinations/ui/edit-activation.md#edit-when-to-activate).

## Afficher la configuration du déclencheur dans l’onglet Parcourir {#browse-tab}

L’onglet **[!UICONTROL Parcourir]** de l’espace de travail [Destinations](/help/destinations/ui/destinations-workspace.md#browse) affiche une colonne **[!UICONTROL Déclencheur d’activation]**. La colonne affiche les déclencheurs actuellement configurés pour chaque flux de données. Utilisez cette colonne pour passer rapidement en revue les types de modification de profil qui activent chacune de vos connexions de destination.

![L’onglet Parcourir dans l’espace de travail Destinations affichant la colonne Déclencheur d’activation avec les types de déclencheur répertoriés pour chaque flux de données.](../assets/ui/when-to-activate/activation-triggers-browse.png)