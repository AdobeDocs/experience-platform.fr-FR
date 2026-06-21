---
title: Chronologies du traitement du cycle de vie des données
description: Découvrez comment les demandes de suppression d’enregistrements sont mises en file d’attente et traitées dans Adobe Experience Platform, y compris les engagements SLA pour les droits standard et Shield.
keywords: cycle de vie des données
solution: Experience Platform
source-git-commit: d715686601e700492cabfc2bfabcc3951eb9a958
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# Chronologies du traitement du cycle de vie des données {#data-lifecycle-processing-timelines}

Utilisez ce document pour comprendre à quel moment une demande de suppression d’enregistrement se termine et ce qui affecte cette chronologie. Les délais diffèrent selon le niveau de droits, qu’il s’agisse du standard (SLA de 30 jours), de Privacy and Security Shield ou de Healthcare Shield (SLA de 15 jours). Si vous ne savez pas quel niveau s’applique à votre organisation, vérifiez votre [utilisation des quotas](./api/quota.md) ou contactez votre représentant Adobe. Pour les délais d’expiration des jeux de données, consultez le [guide d’expiration des jeux de données](./ui/dataset-expiration.md).

## Traitement des demandes de suppression d’enregistrements {#how-record-delete-timelines-work}

Après avoir envoyé une [demande de suppression d’enregistrement](./ui/record-delete.md), celle-ci passe par trois phases : mise en file d’attente et traitement par lots, traitement en aval et achèvement. Tous les niveaux de droits suivent le même flux ; votre SLA détermine la durée de chaque phase. Votre SLA dure 30 jours pour les droits standard et 15 jours pour les organisations qui disposent d’un module complémentaire Privacy and Security Shield ou Healthcare Shield.

Si vous avez déjà soumis une demande et souhaitez confirmer qu’elle progresse normalement, utilisez la section [Délais de traitement par droit](#processing-timelines-by-entitlement) pour déterminer où votre demande doit se fonder sur le temps écoulé.

### Phase 1 : mise en file d’attente et traitement par lots {#queuing-and-batching}

Après l’envoi, un ordre de travail est créé et votre demande entre dans une file d’attente de traitement. Les demandes sont conservées dans la file d’attente et regroupées par lots avant le début du traitement. Le traitement par lots, et non une erreur système, est la principale raison pour laquelle la suppression ne se produit pas immédiatement après l’envoi.

La durée de la file d’attente varie en fonction du niveau de droit. Les demandes standard peuvent rester dans la file d’attente pendant 14 jours au maximum. Les requêtes sous Privacy and Security Shield ou Healthcare Shield sont généralement traitées par lots dans les 24 heures environ, bien que les requêtes volumineuses puissent être promues plus tôt en fonction des seuils de volume.

### Phase 2 : traitement en aval {#downstream-processing}

Une fois qu’un lot quitte la file d’attente, les services en aval traitent la suppression dans vos entrepôts de données Experience Platform. Le statut de l’ordre de travail ne se met pas à jour au cours de cette phase ; il reflète le résultat global une fois le traitement confirmé. Pour vérifier le statut actuel de votre requête, voir [Surveillance du statut de la requête](#monitoring-request-status). La durée du traitement varie en fonction de la charge du système et du niveau de droits et se produit dans la fenêtre SLA opérationnelle pour votre niveau de droits.

### Phase 3 : Achèvement {#completion}

Le statut de l’ordre de travail est mis à jour sur `completed` une fois que tous les systèmes confirment la suppression. Vous pouvez vérifier le statut d’achèvement dans l’espace de travail [Cycle de vie des données](./ui/browse.md).

## Chronologies de traitement par droit {#processing-timelines-by-entitlement}

Les trois phases ci-dessus s’appliquent à tous les niveaux de droits. Les tableaux suivants indiquent la durée approximative de chaque phase en fonction de vos droits. Identifiez votre niveau avant de vous fier à un calendrier spécifique. Les durées des phases sont approximatives et varient en fonction de la charge du système et de la planification des lots. Le SLA de bout en bout indiqué est l’engagement opérationnel.

### Droit standard {#standard-entitlement}

La chronologie suivante s’applique aux organisations **sans** un module complémentaire Privacy and Security Shield ou Healthcare Shield.

>[!IMPORTANT]
>
>Le SLA de bout en bout de 30 jours **est l’engagement opérationnel.**

| Phase | Planning approximatif | Description |
|---|---|---|
| Demande envoyée et groupée | Jusqu’à 14 jours | Un ordre de travail est créé et entre dans la file d’attente de traitement. Les demandes sont traitées par lots avant le début du traitement. Le traitement par lots est la principale raison pour laquelle la suppression n’est pas immédiate. |
| Traitement en aval | Jour 15-25 | Les services en aval reçoivent et exécutent la requête de suppression d’enregistrement. La durée varie en fonction de la charge du système. |
| Achèvement | Jour 25-30 | Les étapes finales de traitement et de validation sont terminées avant la mise à jour du statut de l’ordre de travail sur `completed`. |

{style="table-layout:auto"}

### Privacy and Security Shield / Healthcare Shield {#shield-entitlement}

La chronologie accélérée ci-dessous s’applique uniquement aux organisations qui ont acheté le module complémentaire Privacy and Security Shield ou Healthcare Shield. Pour vérifier le niveau de droits, contactez votre représentant Adobe ou passez en revue votre [utilisation du quota](./api/quota.md).

>[!IMPORTANT]
>
>Le SLA de bout en bout de 15 jours **est l’engagement opérationnel.**

| Phase | Planning approximatif | Description |
|---|---|---|
| Demande envoyée et groupée | Généralement ~24 heures | Un ordre de travail est créé et mis en file d’attente. Les demandes sont regroupées par lots avant le début du traitement, c’est pourquoi la suppression n’est pas immédiate. |
| Traitement et achèvement en aval | Dans un SLA de 15 jours | Les services en aval reçoivent et exécutent la requête de suppression d’enregistrement. Le statut de l’ordre de travail est mis à jour sur `completed` une fois que tous les systèmes confirment la suppression. |

{style="table-layout:auto"}

## Quota et limites de soumission {#quota-and-submission-limits}

Les délais de traitement s’appliquent une fois la demande acceptée. Les demandes de suppression d’enregistrements sont également soumises à des quotas d’envoi d’identifiants mensuels et quotidiens distincts et indépendants des contrats de niveau de service de traitement. Si une demande soumise ne semble pas être en cours d’exécution, [confirmez qu’elle a été acceptée](./ui/browse.md) avant d’attribuer le retard au traitement par lots. Une requête bloquée par l’épuisement du quota requiert une action et ne pénètre pas dans la file d’attente de traitement. Le dépassement de votre quota empêche l’acceptation de nouvelles demandes, quel que soit votre niveau SLA.

Pour les niveaux de quota, les limites mensuelles et les limites basées sur les droits, voir :

- [Quotas d’envoi des identifiants (interface utilisateur)](./ui/record-delete.md#quotas)
- [Quotas d’envoi des identifiants (API)](./api/workorder.md#quotas)

## Surveillance du statut des demandes {#monitoring-request-status}

Pour vérifier le statut d’une demande de suppression d’enregistrement envoyée, accédez à l’espace de travail **[!UICONTROL Cycle de vie des données]** dans l’interface utilisateur d’Experience Platform et sélectionnez l’onglet **[!UICONTROL Enregistrement]**. Une liste des demandes de suppression d’enregistrements envoyées et leur statut actuel s’affiche. Pour les vérifications d’état par programmation, utilisez l’API [work order](./api/workorder.md).

Pour obtenir des instructions détaillées, voir [Parcourir les ordres de travail relatifs au cycle de vie des données](./ui/browse.md) ou le [Guide de point d’entrée des ordres de travail](./api/workorder.md).

## Étapes suivantes {#next-steps}

Pour continuer à travailler avec les demandes de suppression d’enregistrements, consultez les ressources suivantes.

- [Créer une requête de suppression d’enregistrement dans l’interface utilisateur](./ui/record-delete.md)
- [Créer une requête de suppression d’enregistrement à l’aide de l’API](./api/workorder.md)
- [Surveillance de l’utilisation des quotas](./api/quota.md)
