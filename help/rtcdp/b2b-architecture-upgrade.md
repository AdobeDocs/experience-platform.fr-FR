---
title: Mises à niveau de l’architecture vers Real-Time CDP B2B edition
description: Lisez ce document pour en savoir plus sur les mises à niveau complètes de l’architecture vers Real-Time CDP B2B edition.
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: d958a947-e195-4dd4-a04c-63ad82829728
source-git-commit: a48196d369cec9e9927d9320475e06457e575691
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 1%

---

# Mises à niveau de l’architecture vers Real-Time CDP B2B edition

>[!IMPORTANT]
>
>Ce document décrit les mises à niveau architecturales apportées aux éditions B2B et B2P de Real-Time CDP. Les mises à niveau ne nécessitent aucune action de la part de la plupart des clients. Cependant, certaines audiences ne peuvent pas être mises à niveau automatiquement. Adobe travaillera directement avec vous pour résoudre ces scénarios. Reportez-vous à ce document pour plus d’informations sur l’impact des mises à niveau sur les fonctionnalités existantes de Adobe Experience Platform. Pour toute question, contactez l’équipe chargée de votre compte Adobe.

Adobe a repensé les éditions B2B et B2P de Real-Time CDP afin d’améliorer l’évolutivité, les performances et la fiabilité, tout en prenant en charge des cas d’utilisation B2B plus avancés. Pour que tous les clients bénéficient de ces améliorations, Adobe mettra à niveau tous les clients B2B et B2P existants vers la nouvelle architecture.

Utilisez l’architecture améliorée pour bénéficier des avantages suivants :

* **Évolutivité de l’ingestion des données** : prise en charge améliorée des relations B2B à cardinalité élevée, telles que les comptes connectés à des milliers de personnes.
* **Évaluation d’audience performante et fiable** : segmentation plus rapide et plus résiliente pour les audiences B2B complexes.
* **résolution d’entité** : résolution d’identité améliorée pour les entités B2B, qualité des données améliorée et duplication réduite pour permettre une segmentation et une agrégation plus précises.

## Nouvelles fonctionnalités

Lisez ce qui suit pour connaître les principales améliorations incluses dans la mise à niveau architecturale.

### Instantanés de compte pour l’appartenance à une audience

Avec la nouvelle architecture B2B, les détails d’appartenance à l’audience sont désormais inclus pour les entités de compte dans les exportations d’instantanés. Cette fonctionnalité vous permet d’accéder au statut de l’audience, aux horodatages et aux indicateurs d’appartenance au niveau du compte.

Grâce à cette mise à niveau, vous pouvez désormais :

* Permettre aux équipes marketing et opérationnelles de valider directement l’appartenance à une audience de compte.
* Parité des fonctionnalités entre vos modèles de segmentation de profil (personne) et de compte, ce qui garantit une expérience cohérente entre les entités.

Pour plus d’informations, consultez la documentation sur les [audiences de compte](../segmentation/types/account-audiences.md).

### Nombres de profils des audiences pour les audiences qui incluent des entités B2B

Les estimations de taille d’audience pour les audiences avec des entités B2B sont désormais calculées avec précision. Ces estimations sont disponibles lors de la prévisualisation et fournissent des informations plus précises et plus fiables pour les audiences qui impliquent des relations B2B complexes.

Grâce à cette mise à niveau, vous pouvez désormais :

* Utilisez les informations provenant d’estimations précises de la taille de l’audience pour améliorer la planification et la prise de décision pendant le processus de création d’audience.
* Concevez des audiences B2B complexes en toute confiance, avec la connaissance d’une estimation d’audience plus précise.
* Permettre une planification de campagne plus intelligente, un ciblage plus précis et une meilleure allocation des ressources.

Pour plus d’informations, consultez la documentation sur les [audiences de compte](../segmentation/types/account-audiences.md).

## Mises à niveau vers les fonctionnalités existantes

Les fonctionnalités suivantes ont été mises à jour dans le cadre des mises à niveau de l’architecture B2B.

### Mises à jour de l’audience à entités multiples avec des attributs B2B et des événements d’expérience

Dans le cadre de la nouvelle mise à niveau de l’architecture, les filtres d’événement d’expérience ne peuvent plus être utilisés dans une audience unique à entités multiples qui inclut des attributs B2B.

Pour appliquer la même logique d’audience, vous pouvez utiliser le créateur de segments pour [ ajouter des audiences et des audiences de référence ](../segmentation/ui/segment-builder.md#adding-audiences)

Par exemple :

* Création d’une audience d’événement d’expérience
   * Définissez la condition comportementale séparément. Par exemple : « Personnes qui ont visité la page de tarification au cours des trois derniers jours ».
* Créez une audience à entités multiples avec des attributs B2B.
   * À partir de là, vous pouvez référencer l’audience Événement d’expérience dans le cadre des critères de cette audience. Par exemple : « Personnes qui sont un décideur **»** de toute opportunité où le compte se trouve dans le secteur de la finance **et membre de l’audience des personnes qui ont visité la page** tarification au cours des trois derniers jours.

Une fois la mise à niveau terminée, toute nouvelle audience d’entités multiples avec des attributs B2B et des événements d’expérience doit être créée à l’aide de l’approche [segment-de-segment](../segmentation/methods/edge-segmentation.md#edge-segmentation-query-types).

>[!TIP]
>
>Un **segment de segments** est toute définition de segment contenant un ou plusieurs segments par lots ou Edge. **Remarque** : si vous utilisez un segment de segments, la disqualification du profil se produit **toutes les 24 heures**.

### Résolution d’entité et fusion de la priorité temporelle dans les audiences B2B

Dans le cadre de la mise à niveau de l’architecture, Adobe introduit la résolution d’entité pour les comptes et les opportunités. La résolution de l’entité est basée sur la correspondance d’identifiants déterministe et sur les données les plus récentes. Le traitement de résolution d’entité s’exécute quotidiennement pendant la segmentation par lots, avant d’évaluer les audiences à entités multiples avec des attributs B2B.

>[!BEGINSHADEBOX]

#### Comment fonctionne la résolution d’entité ?

* **Auparavant** : si un numéro DUNS (Data Universal Numbering System) était utilisé comme identité supplémentaire et que le numéro DUNS du compte était mis à jour dans un système source tel que CRM, l’identifiant de compte est lié à la fois aux anciens et aux nouveaux numéros DUNS.
* **Après** : si le numéro DUNS a été utilisé comme identité supplémentaire et que le numéro DUNS du compte a été mis à jour dans un système source tel qu’un CRM, l’identifiant de compte n’est lié qu’au nouveau numéro DUNS, reflétant ainsi plus précisément l’état actuel du compte.

>[!ENDSHADEBOX]

Grâce à cette mise à niveau, vous pouvez désormais :

* Utilisez les API [!DNL Profile Access] pour afficher les derniers profils de fusion une fois les tâches de résolution d’entité quotidiennes terminées.
* Utilisez l’amélioration de la précision et de la cohérence des données de votre compte et de votre opportunité pour la segmentation, l’activation et l’analyse.

Lisez la [[!DNL Profile Access] API](../profile/api/entities.md) pour plus d’informations.

### Prise en charge des politiques de fusion dans les audiences B2B multientités

Les audiences d’entités multiples avec des attributs B2B prennent désormais en charge une seule politique de fusion (la politique de fusion par défaut que vous configurez) au lieu de plusieurs politiques de fusion.

Pour plus d’informations, consultez le [guide de cas d’utilisation de la segmentation pour Real-Time CDP B2B edition](./segmentation/b2b.md).

### Obsolescence de la recherche et de la suppression d’entités B2B dans l’API [!DNL Profile Access]

Les fonctionnalités de recherche suivantes pour les entités B2B à l’aide de l’API [!DNL Profile Access] sont en train d’être abandonnées :

* Relation Compte-Personne
* Relation Opportunité-Personne
* Campagne
* Membre de la campagne
* Liste marketing
* Membres de la liste marketing

Les requêtes de suppression pour les entités B2B suivantes utilisant l’API [!DNL Profile Access] sont en cours d’obsolescence :

* Compte
* Relation Compte-Personne
* Opportunité
* Relation Opportunité-Personne
* Campagne
* Membre de la campagne
* Liste marketing
* Membres de la liste marketing

Lisez la [[!DNL Profile Access] API](../profile/api/entities.md) pour plus d’informations.

### Obsolescence de l’API de tâche de segmentation

Dans la nouvelle architecture, le point d’entrée « créer une tâche de segmentation » et l’évaluation d’audience flexible ne sont *pas pris en charge.

### Recherches de profils de compte et d’opportunité

Vous pouvez désormais récupérer les schémas de compte et d’opportunité en tant qu’entités de dimension de recherche uniquement après qu’ils ont terminé le processus de résolution quotidienne des entités. Les enregistrements nouvellement ingérés ne seront pas disponibles pour l’enrichissement de profil ou les définitions de segment tant que le cycle de résolution d’entité suivant ne sera pas terminé (généralement toutes les 24 heures).

<!-- ### Deprecation of audience creation via API for B2B entities

Creation of audiences using B2B entities via API is being deprecated. The list of affected B2B entities include:

* Account
* Opportunity
* Account-Person Relation
* Opportunity-Person Relation
* Campaign
* Campaign Member
* Marketing List
* Marketing List Member

Read the [segment definitions endpoint API guide](../segmentation/api/segment-definitions.md) for more information. -->

### Modifications des importations d’audiences à entités multiples dans l’outil Sandbox

Avec les mises à niveau de l’architecture, vous ne pourrez plus importer d’audiences à entités multiples avec des attributs B2B et des événements d’expérience si un package qui incluait ces audiences a été publié avant la mise à niveau. L’importation de ces audiences échouera et ne pourront pas être automatiquement converties dans la nouvelle architecture. Pour contourner cette limitation, vous devez créer un nouveau package avec les audiences mises à jour, puis les importer dans leurs sandbox cibles respectifs à l’aide de l’outil sandbox .

Les sandbox de développement seront mis à niveau vers la nouvelle architecture. Les audiences pouvant être mises à jour automatiquement seront mises à niveau et celles qui ne le peuvent pas seront désactivées. Les audiences désactivées doivent être recréées après la mise à niveau.

Pour plus d’informations, consultez le [guide d’utilisation des sandbox](../sandboxes/ui/sandbox-tooling.md) .
