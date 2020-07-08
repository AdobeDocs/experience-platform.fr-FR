---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: FAQ CCPA
topic: troubleshooting
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---


# FAQ CCPA

Ce document répond aux questions les plus fréquentes sur la loi California Consumer Protection Act (CCPA) et son implémentation dans Adobe Experience Cloud.

## Qu&#39;est-ce que l&#39;ACFPC ?

La California Consumer Privacy Act (CCPA) est la nouvelle loi californienne sur la protection des renseignements personnels qui accorde à ses résidents de nouveaux droits sur leurs renseignements personnels et impose des responsabilités en matière de protection des données à certaines entités qui font des affaires en Californie.

>[!NOTE]
>
>Bien que techniquement efficace en janvier 2020, l&#39;ACCP est encore en voie d&#39;être affinée par les législateurs. En outre, d&#39;importants détails de mise en oeuvre et d&#39;autres directives figurent dans des règles qui n&#39;ont pas encore été rédigées par l&#39;autorité de réglementation californienne.

Bien que l’ACCP partage certains concepts énoncés dans le Règlement général sur la protection des données (RGPD) de l’Union européenne, tels que le droit d’une personne d’accéder à des renseignements personnels et de les supprimer, il existe plusieurs façons fondamentales pour l’ACCP de s’écarter du RGPD. Par exemple, l&#39;ACFPC accorde aux consommateurs un droit d&#39;exclusion de certaines activités de partage de données qui sont admissibles à la &quot;vente&quot; de renseignements personnels à un tiers, plutôt que d&#39;exiger un consentement préalable.

## Quelle est la définition des renseignements personnels en vertu de la LPCA ?

Les renseignements personnels sont des renseignements &quot;qui identifient, se rapportent, décrivent, peuvent être associés à un consommateur ou à un ménage, ou qui pourraient raisonnablement être liés, directement ou indirectement, avec lui&quot;.

## Quels types d’informations personnelles ou d’identifiants utilisés dans Adobe Experience Cloud sont soumis à ces nouvelles exigences ?

Les identifiants suivants sont couramment utilisés dans les applications Experience Cloud et pourraient être assujettis aux exigences de l&#39;ACFPC :

- Nom
- Postal address
- Identifiant personnel unique
- Identificateur en ligne
- Adresse IP
- Adresse électronique
- Nom du compte

Les renseignements personnels peuvent aussi inclure Internet ou d&#39;autres renseignements sur l&#39;activité de réseau électronique. Cela comprend, entre autres :

- Historique de navigation
- Historique des recherches
- Informations relatives à l’interaction d’un consommateur avec un site Web, une application ou une publicité

Même si l’ACFPC couvre un vaste ensemble de renseignements personnels, les clauses contractuelles types de Adobe stipulent que les renseignements personnels sensibles (tels que le numéro d’identification unique, les renseignements sur le permis de conduire, les renseignements sur les comptes financiers et les données biométriques) sont généralement interdits d’importation et d’utilisation dans les applications Experience Cloud.

## Comment les différents rôles et responsabilités de l&#39;ACCP s&#39;appliquent-ils à l&#39;Experience Cloud ?

Selon la définition de l&#39;ACPCS, les rôles suivants s&#39;appliquent à Adobe et à ses clients :

- Les clients Adobe (la partie demandant la collecte et l&#39;utilisation de renseignements personnels auprès des résidents de Californie) seraient considérés comme des **entreprises**.
- Adobe, dans son rôle de fournisseur de services, serait considéré comme un **Prestataire**.

Compte tenu de cette relation et du langage contractuel Adobe, les divulgations à Adobe ne seraient probablement pas considérées comme une &quot;vente&quot; pour laquelle les entreprises devraient fournir un avis et l&#39;offre et une exclusion.

Toutefois, les services Adobe peuvent être utilisés pour permettre certains échanges de données et transferts à des tiers. Ces transferts de tiers pourraient être considérés comme une &quot;vente&quot; et nécessiter légalement la divulgation et l&#39;exclusion.  Les clients devraient collaborer avec leur conseiller juridique pour évaluer des cas d&#39;utilisation spécifiques afin d&#39;évaluer les exigences applicables.

## Combien de jours une entreprise doit-elle répondre à une demande du consommateur pour accéder ou supprimer des renseignements personnels ?

En supposant que l&#39;entreprise ait recueilli des renseignements personnels et qu&#39;elle puisse s&#39;authentifier ou vérifier l&#39;identité d&#39;un consommateur californien particulier, l&#39;ACCP permet que les demandes des consommateurs soient satisfaites dans les 45 jours (à quelques exceptions près).

## Quel est le rôle de l&#39;Adobe dans le cadre de l&#39;ACCP ?

En tant que Prestataire, Adobe recueille et traite des renseignements personnels pour le compte de l&#39;Entreprise et est contractuellement tenu d&#39;utiliser ces renseignements uniquement aux fins précises énoncées dans l&#39;entente.

Compte tenu de cette relation et du langage contractuel de l’Adobe, les divulgations à Adobe relèvent des dispositions de la loi pour les Prestataires, et ne seraient probablement pas considérées comme une &quot;vente&quot; pour laquelle les entreprises devraient fournir un avis et l’offre et une exclusion.

Les services Adobe peuvent être utilisés pour permettre certains échanges de données et transferts à des tiers. Ces transferts de tiers pourraient être considérés comme une &quot;vente&quot; et nécessiter légalement la divulgation et l&#39;exclusion.  Les clients devraient collaborer avec leur conseiller juridique pour évaluer des cas d&#39;utilisation spécifiques afin d&#39;évaluer les exigences applicables.

## Comment puis-je appuyer les exigences de protection de la vie privée des consommateurs en vertu de l&#39;ACFPC si je conserve certains types de données qui sont couvertes par ces exigences ?

Une fois que vous avez pris les mesures nécessaires pour authentifier les consommateurs de CA, l&#39;Adobe Experience Platform Privacy Service vous permet de soumettre des demandes de confidentialité de consommateur à des applications Experience Cloud compatibles. See the [Privacy Service overview](../home.md) for more information. Pour plus d&#39;informations sur la façon dont vos applications Experience Cloud particulières peuvent respecter les demandes de confidentialité, consultez le guide sur les applications [](../experience-cloud-apps.md)Privacy Service et Experience Cloud.

>[!NOTE]
>
>L&#39;autorité de réglementation de la Californie continue de fournir des indications supplémentaires sur les types de données admissibles aux demandes de protection des renseignements personnels des consommateurs.

## L&#39;Adobe offre-t-elle d&#39;autres outils qui pourraient être utiles pour répondre aux exigences de l&#39;ACCP ?

Les applications Adobe Experience Cloud offrent des fonctions de data Management et de gouvernance qui peuvent être utiles pour les besoins de confidentialité des sociétés. Parmi ces outils figurent l’étiquetage de l’utilisation des données, les contrôles d&#39;accès basés sur les rôles, l’obscurcissement d’IP et les capacités de hachage.

Adobe a reçu diverses certifications de ses pratiques de confidentialité et de sécurité, comme une certification ISO 27001 et une validation TrustArc GDPR.