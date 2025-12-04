---
title: Utilisation et capacité des licences
description: Découvrez les limites d’utilisation et de capacité de votre licence dans Adobe Experience Platform.
exl-id: 38dad2f1-bd0f-4cc3-a3a6-5105ea866ea4
source-git-commit: 5520e449b4cbe45eb9664ce3c913dd5d544e088c
workflow-type: tm+mt
source-wordcount: '1603'
ht-degree: 7%

---


# Utilisation des licences et capacités

>[!AVAILABILITY]
>
>Pour utiliser cette fonctionnalité, vous devez disposer des autorisations suivantes :
>
>- **Afficher le tableau de bord d’utilisation des licences**
>   - Cette autorisation vous permet de **afficher** la page de départ Capacité.
>- **Gestion des sandbox**
>   - Cette autorisation vous permet de **modifier** vos allocations de capacité.
>   - En outre, vous **devez** avoir accès à tous les sandbox pour modifier la capacité de **n’importe quel** sandbox.
>
>Vous trouverez plus d’informations sur les autorisations dans Experience Platform dans la [&#x200B; présentation du contrôle d’accès &#x200B;](/help/access-control/home.md#permissions)
>
>De plus, si vous avez acheté Segmentation par flux à haut débit, vous **ne pourrez pas** allouer vos capacités à l’aide de la capacité. Pour mettre à jour vos capacités, contactez l’Assistance clientèle d’Adobe.

Dans Adobe Experience Platform, les capacités vous permettent de savoir si votre organisation a dépassé l’un de vos mécanismes de sécurisation et vous donnent des informations sur la manière de résoudre ces problèmes.

Pour plus d’informations sur les mécanismes de sécurisation dans Experience Platform, consultez la présentation des mécanismes de sécurisation de [Real-Time CDP](../../rtcdp/guardrails/overview.md).

## Comportement de capacité {#behavior}

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingthroughput"
>title="Débit de streaming"
>abstract="La valeur de débit de streaming mesure le pic combiné d’événements entrants par seconde pour l’ingestion en flux continu dans le service Profil, sur vos sandbox de production et de développement."

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingaudiences"
>title="Nombre d’audiences en streaming"
>abstract="Nombre maximal d’audiences en streaming par sandbox. Ce nombre inclut le nombre d’audiences Edge que vous avez dans votre sandbox."

>[!CONTEXTUALHELP]
>id="platform_capacity_edgeaudiences"
>title="Audiences Edge"
>abstract="Nombre maximal d’audiences Edge par sandbox."

Actuellement, Capacity prend en charge les services suivants :

- Segmentation par streaming
- Ingestion en flux continu

Dans ces services, les mécanismes de sécurisation suivants sont suivis :

- Le nombre maximal d’audiences de diffusion en continu est de 500
   - Sur ces 500 audiences de diffusion en continu, le nombre maximal d’audiences Edge est de 150
- Le débit combiné initial pour l’ingestion en flux continu est de 1 500 enregistrements par seconde (rps)
   - Ce débit de diffusion en continu combiné mesure le pic combiné d’événements entrants par seconde pour l’ingestion en flux continu dans le profil client en temps réel sur vos sandbox de production et de développement.
   - Vous pouvez acheter une prise en charge supplémentaire de la segmentation en flux continu pour un maximum de 13 500 enregistrements par seconde. Vous trouverez plus d’informations sur l’achat de droits supplémentaires dans la description du produit [Real-Time CDP](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

La capacité de l’audience se situe au niveau **sandbox**. Cela signifie que, pour chaque sandbox de votre organisation, vous pouvez avoir 500 audiences en flux continu, dont 150 peuvent être des audiences Edge.

La capacité de débit de diffusion en continu se situe au niveau de l’**organisation** et peut être distribuée à vos sandbox individuels. Par exemple, avec le débit d’ingestion en flux continu de 1 500 i/s, vous pouvez définir votre sandbox de production sur 1 300 i/s et votre sandbox de développement sur 200 i/s.

Experience Platform calcule le débit du sandbox par intervalles de 15 minutes consécutifs. Ce débit est mesuré en temps réel, avec une actualisation des données toutes les 60 secondes.

Si votre utilisation atteint 80 % et 90 % de votre capacité sous licence, Experience Platform émet une alerte pour vous informer que vous atteignez la capacité maximale spécifiée. Vous pouvez modifier les paramètres pour personnaliser le pourcentage de capacité à recevoir l’alerte ou supprimer entièrement l’alerte.

Si votre utilisation dépasse 100 % de votre capacité sous licence, vous serez considéré comme en violation de votre capacité. À ce stade, vous ferez l’expérience d’une latence de performances et vos cibles de niveau de service (SLT) ne seront **pas** garanties.

## Accès {#access}

Pour accéder à la présentation de la capacité, sélectionnez **[!UICONTROL License usage]** suivi de **[!UICONTROL Capacity]**.

![La méthode d’accès à la section Capacité est mise en surbrillance.](/help/landing/images/capacity/access-capacity.png)

La page Aperçu de la capacité s’affiche, avec des informations, notamment un historique des alertes, ainsi que des détails sur les capacités de votre entreprise.

![La page Aperçu de la capacité s’affiche en entier, présentant l’historique des alertes et les sections de détails de la capacité.](/help/landing/images/capacity/capacity-overview.png) {zoomable="yes" width="80%"}

### Historique des alertes {#alert-history}

La section **[!UICONTROL Alert history]** affiche une liste des violations de capacité les plus récentes au sein de votre organisation.

![La section Historique des alertes s’affiche.](/help/landing/images/capacity/alert-history.png)

| Nom de la colonne | Description |
| ----------- | ----------- |
| Sandbox | Nom du sandbox où la violation de capacité s’est produite. |
| Alerte | Capacité qui a été dépassée dans le sandbox. |
| Date et heure | Données et heure auxquelles la violation s’est produite. |

Pour afficher un historique complet des alertes de votre organisation, sélectionnez l’icône ![des trois petits points](/help/images/icons/more.png), puis **[!UICONTROL View all]**.

![L’historique complet des alertes s’affiche pour une organisation.](/help/landing/images/capacity/full-alert-history.png)

### Détails de capacité {#capacity-details}

La section Détails de la capacité fournit des informations sur les capacités de votre organisation. Dans cette section, vous pouvez filtrer par sandbox et modifier la période de recherche en amont.

![Le sélecteur de sandbox et le sélecteur de date pour la période de recherche en amont sont mis en surbrillance.](/help/landing/images/capacity/filter-sandbox-and-date.png)

Actuellement, il affiche des informations de capacité sur le débit de diffusion en continu, les audiences de diffusion en continu et les audiences Edge.

#### Débit de streaming {#streaming-throughput}

La section Débit de diffusion en continu affiche des informations sur le débit de diffusion en continu dans les sandbox de votre organisation. La valeur de débit de diffusion mesure le pic combiné d’événements entrants par seconde pour l’ingestion en flux continu dans le service Profil.

![La section Débit de diffusion en continu de la page des détails de la capacité s’affiche.](/help/landing/images/capacity/streaming-throughput-section.png)

| Nom de la colonne | Description |
| ----------- | ----------- |
| Sandbox | Nom du sandbox. |
| Services | Service utilisé par le sandbox. Actuellement, la seule valeur prise en charge est Profil. |
| Utilisation (pic) | Débit de diffusion en continu maximal des données dans le sandbox au cours de la période de recherche en amont sélectionnée. |
| Capacité | Débit de diffusion en continu maximal pour le sandbox. |
| Violation | Si une violation s’est produite, type de violation pour le débit de diffusion en continu. |
| Actions recommandées | Colonne décrivant l’action recommandée pour remédier à la violation. |

Vous pouvez sélectionner le sandbox individuel pour afficher une vue plus détaillée du débit de diffusion en continu du sandbox.

![Un sandbox est mis en surbrillance dans la section relative au débit de diffusion.](/help/landing/images/capacity/select-sandbox.png)

La page Détails du débit de diffusion en continu s’affiche. Vous pouvez voir un graphique qui affiche le débit des requêtes par rapport à la limite de capacité, une liste des sandbox et leurs débits, ainsi qu’un bouton pour allouer les capacités de votre organisation.

![La page Débit de diffusion en continu s’affiche, affichant des informations détaillées sur le débit de diffusion en continu pour le sandbox sélectionné.](/help/landing/images/capacity/streaming-capacity-allocation.png)

Pour mettre à jour les capacités de débit de diffusion en continu de l’organisation, sélectionnez **[!UICONTROL Allocate capacities]**.

![Le bouton Allouer des capacités est mis en surbrillance dans la page des détails du débit de diffusion en continu.](/help/landing/images/capacity/select-allocate.png)

La page d’attribution s’affiche. Sur cette page, vous pouvez définir vos capacités pour vos différents sandbox. La somme de toutes les capacités **doit** égale au total des capacités de l&#39;organisation.

![La page d’allocation de capacité s’affiche.](/help/landing/images/capacity/allocate-capacity.png)

>[!NOTE]
>
>Vous ne pouvez définir la nouvelle capacité que dans des ordres de **100**. Par exemple, vous pouvez définir la valeur de la nouvelle capacité du sandbox sur 300 ou 500, mais vous **pouvez pas** cette valeur sur 450.
>
>Si la valeur n’est pas de l’ordre de 100, elle sera arrondie à l’unité supérieure ou inférieure en conséquence.

Après avoir mis à jour les allocations de capacité, sélectionnez **[!UICONTROL Save]** pour terminer les mises à jour. Notez que la prise en compte des modifications dans votre organisation peut prendre jusqu’à 10 minutes.

#### Taille de l’audience {#audience-count}

Les sections **[!UICONTROL Streaming audience count]** et **[!UICONTROL Edge audience count]** indiquent le nombre d’audiences de diffusion en continu et Edge dans le sandbox, ainsi que le nombre maximal d’audiences de diffusion en continu et Edge autorisées dans le sandbox.

![Les sections Nombre d’audiences s’affichent.](/help/landing/images/capacity/audience-count.png)

| Nom de la colonne | Description |
| ----------- | ----------- |
| Sandbox | Nom du sandbox. |
| Services | Service utilisé pour le sandbox. |
| Utilisation | Nombre d’audiences du type répertorié qui se trouvent dans le sandbox. |
| Capacité | Nombre maximal d’audiences du type répertorié qui sont autorisées dans le sandbox. |

## Bonnes pratiques relatives au débit en flux continu {#suggestions}

Vous pouvez résoudre vos violations de débit de diffusion en continu en adoptant l’une des recommandations suivantes :

1. Augmentez la capacité allouée pour le sandbox.
2. Identifiez les flux de données à débit élevé dans le [tableau de bord de surveillance](/help/dataflows/ui/monitor-streaming-profile.md) et appliquez une limitation ou un filtrage sur ces flux de données, si nécessaire.
3. Optimisez votre ingestion en utilisant l’ingestion par lots pour des cas d’utilisation de latence plus faible.

En outre, vous pouvez consulter vos flux de données et voir si vous pouvez optimiser votre stratégie de données.

| Facteur contributif | Ce que c&#39;est | Impact sur les cas d’utilisation | Bonnes pratiques |
| --- | --- | --- | --- |
| Conversion par lots en flux continu | Les charges de travail par lots converties en flux continu peuvent augmenter considérablement le débit et affecter les performances et l’allocation des ressources. Par exemple, l’exécution d’une mise à jour de profil en bloc après un événement sans limites de débit. | Les stratégies de diffusion en continu sont inutiles pour les cas d’utilisation par lots lorsqu’un traitement à faible latence n’est pas nécessaire. | Évaluez les exigences du cas d’utilisation. Pour le marketing sortant par lots, pensez à utiliser l’[ingestion par lots](/help/ingestion/batch-ingestion/overview.md) plutôt que la diffusion en continu pour gérer plus efficacement l’ingestion des données. |
| Ingestion de données inutile | L’ingestion de données non requises pour la personnalisation augmente le débit sans valeur ajoutée, ce qui entraîne une perte de ressources. Par exemple, l’ingestion de tout le trafic d’analyse dans des profils quelle que soit la pertinence. | L’excès de données non pertinentes crée du bruit, ce qui rend plus difficile l’identification des points de données pertinents. Cela peut également entraîner des frictions lors de la définition et de la gestion des audiences et des profils. | Ingérez uniquement les données requises pour vos cas d’utilisation. Veillez à filtrer les données inutiles.<ul><li>**Adobe Analytics** : utilisez le [filtrage au niveau des lignes](/help/sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-real-time-customer-profile) pour optimiser la saisie des données.</li><li>**Sources** : utilisez l’API [[!DNL Flow Service] API pour filtrer les données au niveau des lignes](/help/sources/tutorials/api/filter.md) pour les sources prises en charge telles que [!DNL Snowflake] et [!DNL Google BigQuery].</li></li>**Flux de données Edge** : configurez [flux de données dynamiques](/help/datastreams/configure-dynamic-datastream.md) pour effectuer un filtrage au niveau des lignes du trafic provenant du SDK Web.</li></ul> |

## Vue d’ensemble des vidéos {#video}

La vidéo suivante présente un aperçu de la capacité.

>[!VIDEO](https://video.tv.adobe.com/v/3475272/?learn=on&enablevpops)

## Questions fréquentes {#faq}

La section suivante présente les questions fréquentes sur les fonctionnalités de Capacity.

### Puis-je avoir une limite de débit combiné maximale qui s’additionne à moins que mon maximum cible ?

+++ Réponse

Non. La limite maximale de débit combiné **doit** s’élève au niveau du mécanisme de sécurisation de votre organisation.

+++

### Que se passe-t-il si je dépasse mes capacités maximales ?

+++ Réponse

Cela dépend de la capacité qui est dépassée.

Actuellement, si vous dépassez le nombre maximal d’audiences autorisées, vos audiences excessives ne seront pas affectées. Cependant, la possibilité de créer de nouvelles audiences peut être limitée à l’avenir.

Si vous dépassez votre débit de diffusion en continu, vous constaterez une latence des performances dans votre ingestion et votre segmentation.

+++

### Pourquoi dois-je respecter mes capacités maximales ?

+++ Réponse

Le fait de travailler dans les limites de vos capacités garantit la cohérence de vos données et le maintien de leur intégrité.

Vous garantissez des performances cohérentes pendant les pics d’activité, en évitant les problèmes techniques susceptibles de nuire aux performances du système et d’avoir une incidence sur vos expériences client en aval, ce qui améliore finalement l’hygiène des données et les performances globales du système.

+++

### Quelles sont les bonnes pratiques pour gérer le débit d’ingestion en flux continu ?

+++ Réponse

Pour gérer au mieux le débit d’ingestion en flux continu, vous devez évaluer vos jeux de données pour vous assurer qu’ils donnent la priorité aux données nécessaires à la personnalisation.


Si le traitement en temps réel n’est pas requis, vous devez utiliser l’ingestion par lots au lieu de l’ingestion par flux.

+++
