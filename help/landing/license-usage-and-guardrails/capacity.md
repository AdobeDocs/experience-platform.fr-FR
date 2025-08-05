---
title: Utilisation et capacité des licences
description: Découvrez les limites d’utilisation et de capacité de votre licence dans Adobe Experience Platform.
exl-id: 38dad2f1-bd0f-4cc3-a3a6-5105ea866ea4
source-git-commit: 326710e48ea9d6eb16f62b9f288311a1d255b287
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 12%

---

# Utilisation des licences et capacités

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
- Le débit combiné maximal pour la segmentation en flux continu est de 1 500 enregistrements par seconde (rps)

La capacité de l’audience se situe au niveau **sandbox**. Cela signifie que, pour chaque sandbox de votre organisation, vous pouvez avoir 500 audiences en flux continu, dont 150 peuvent être des audiences Edge.

La capacité de débit se situe au niveau de l’**organisation** et peut être distribuée à vos sandbox individuels. Par exemple, avec le débit de segmentation en flux continu de 1 500 tr/s, vous pouvez définir votre sandbox de production sur 1 500 tr/s et votre sandbox de développement sur 150 tr/s.

Experience Platform calcule le débit du sandbox par intervalles de 15 minutes consécutifs. Ce débit est mesuré en temps réel, avec une actualisation des données toutes les 60 secondes.

Si votre utilisation atteint 80 % et 90 % de votre capacité sous licence, Experience Platform émet une alerte pour vous informer que vous atteignez la capacité maximale spécifiée. Vous pouvez modifier les paramètres pour personnaliser le pourcentage de capacité à recevoir l’alerte ou supprimer entièrement l’alerte.

Si votre utilisation dépasse 100 % de votre capacité sous licence, vous serez considéré comme en violation de votre capacité. À ce stade, vous ferez l’expérience d’une latence de performances et vos cibles de niveau de service (SLT) ne seront **pas** garanties.

## Questions fréquentes

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

### Quelles sont les bonnes pratiques pour gérer le débit de segmentation en flux continu ?

+++ Réponse

Pour gérer au mieux le débit de segmentation de votre diffusion en continu, vous devez évaluer vos jeux de données pour vous assurer qu’ils donnent la priorité aux données nécessaires à la personnalisation.


Si le traitement en temps réel n’est pas requis, vous devez utiliser l’ingestion par lots au lieu de l’ingestion par flux.

+++
