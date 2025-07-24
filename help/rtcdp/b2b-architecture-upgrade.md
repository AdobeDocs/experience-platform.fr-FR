---
title: Mises à niveau de l’architecture vers Real-Time CDP B2B edition
description: Lisez ce document pour en savoir plus sur les mises à niveau complètes de l’architecture vers Real-Time CDP B2B edition.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
hide: true
hidefromtoc: true
source-git-commit: 78444555178773a8305ba27aaaf7998fe279a71d
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 0%

---

# Mises à niveau de l’architecture vers Real-Time CDP B2B edition

>[!IMPORTANT]
>
>Ce document décrit les mises à niveau architecturales apportées aux éditions B2B et B2P de Real-Time CDP. **Aucune action n’est requise de votre part** à ce stade. Reportez-vous à ce document pour plus d’informations sur l’impact des mises à niveau sur les fonctionnalités existantes de Adobe Experience Platform. Pour toute question, contactez l’équipe chargée de votre compte Adobe.

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

### Nombre d’audiences pour les audiences qui incluent des entités B2B

Les estimations de taille d’audience pour les audiences avec des entités B2B sont désormais calculées avec précision. Ces estimations sont disponibles lors de la prévisualisation et fournissent des informations plus précises et plus fiables pour les audiences qui impliquent des relations B2B complexes.

Grâce à cette mise à niveau, vous pouvez désormais :

* Utilisez les informations provenant d’estimations précises de la taille de l’audience pour améliorer la planification et la prise de décision pendant le processus de création d’audience.
* Concevez des audiences B2B complexes en toute confiance, avec la connaissance d’une estimation d’audience plus précise.
* Permettre une planification de campagne plus intelligente, un ciblage plus précis et une meilleure allocation des ressources.

Pour plus d’informations, consultez la documentation sur les [audiences de compte](../segmentation/types/account-audiences.md).

### Recherche en amont complète des événements au niveau de la personne dans les audiences de compte

Les audiences de compte peuvent désormais exploiter l’historique complet des événements au niveau de la personne, dépassant l’intervalle de recherche en amont de 30 jours précédent.

Grâce à cette mise à niveau, vous pouvez désormais :

* Créez des audiences plus complètes en fonction de l’historique complet des événements au niveau de la personne associés.
* Définissez des audiences plus riches et plus précises en exploitant des données comportementales à long terme.
* Identifiez les comptes à forte valeur ajoutée en fonction de schémas d’engagement plus précis au fil du temps.
* Prend en charge les cas d’utilisation qui nécessitent des informations sur les actions historiques, comme celles impliquant de longs cycles de vente ou des signaux d’achat retardé.

Pour plus d’informations, consultez la documentation sur les [audiences de compte](../segmentation/types/account-audiences.md).

## Mises à niveau vers les fonctionnalités existantes

Les fonctionnalités suivantes ont été mises à jour dans le cadre des mises à niveau de l’architecture B2B.

### Mises à jour de l’audience à entités multiples avec des attributs B2B et des événements d’expérience

Dans le cadre de la nouvelle mise à niveau de l’architecture, les filtres d’événement d’expérience ne peuvent plus être utilisés dans une audience unique à entités multiples qui inclut des attributs B2B.

Pour obtenir la même logique d’audience, utilisez l’approche segment par segment :

1. Créer une audience d’événement d’expérience : définissez la condition comportementale séparément. Par exemple : « Personnes qui ont visité la page de tarification au cours des trois derniers jours ».
2. Créer une audience à entités multiples avec des attributs B2B : référencez l’audience d’événement d’expérience dans le cadre des critères de cette audience. Par exemple : « Personnes qui sont un décideur **»** de toute opportunité où le compte se trouve dans le secteur de la finance **et membre de l’audience des personnes qui ont visité la page** tarification au cours des trois derniers jours.

Une fois la mise à niveau terminée, toute nouvelle audience d’entités multiples avec des attributs B2B et des événements d’expérience doit être créée à l’aide de l’approche segment-par-segment. De plus, vous devez valider l’appartenance à l’audience pour garantir le comportement attendu.

### Résolution d’entité et fusion de la priorité temporelle dans les audiences B2B

Dans le cadre de la mise à niveau de l’architecture, Adobe a introduit la résolution d’entité pour les comptes et les opportunités, qui s’exécute tous les jours. Cette amélioration permet à Experience Platform d’identifier et de consolider plusieurs enregistrements représentant la même entité réelle, améliorant ainsi la cohérence des données et permettant une segmentation d’audience plus précise.

Grâce à cette mise à niveau, vous pouvez désormais :

* Utilisez les API [!DNL Profile Access] pour afficher les derniers profils de fusion une fois les tâches de résolution d’entité quotidiennes terminées.
* Utilisez l’amélioration de la précision et de la cohérence des données de votre compte et de votre opportunité pour la segmentation, l’activation et l’analyse.

Lisez la [[!DNL Profile Access] API](../profile/api/entities.md) pour plus d’informations.

### Prise en charge des politiques de fusion dans les audiences B2B multientités

Les audiences d’entités multiples avec des attributs B2B prennent désormais en charge une seule politique de fusion (la politique de fusion par défaut que vous configurez) au lieu de plusieurs politiques de fusion.

Les audiences qui dépendaient auparavant d’une politique de fusion autre que la politique par défaut peuvent produire des résultats différents. Pour comprendre les changements potentiels dans la composition de l’audience, passez en revue et testez toutes vos audiences qui reposent sur une politique de fusion autre que celle par défaut. En outre, surveillez les résultats de l’activation pour détecter tout changement dans la composition de l’audience en raison du changement de la politique de fusion.

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

### Recherches de profils de compte et d’opportunité

Vous pouvez désormais récupérer les schémas de compte et d’opportunité en tant qu’entités de dimension de recherche uniquement après qu’ils ont terminé le processus de résolution quotidienne des entités. Les enregistrements nouvellement ingérés ne seront pas disponibles pour l’enrichissement de profil ou les définitions de segment tant que le cycle de résolution d’entité suivant ne sera pas terminé (généralement toutes les 24 heures).

Nous vous recommandons de passer en revue tous les cas d’utilisation qui nécessitent un accès en temps réel aux données du compte et de l’opportunité. En outre, il est recommandé de planifier une période de latence de 24 heures maximum lors de la conception ou de la mise à jour des workflows qui dépendent de la segmentation ou de la personnalisation basée sur la recherche avec les entités de compte et d’opportunité.

### Obsolescence de la création d’audiences via l’API pour les entités B2B

La création d’audiences à l’aide d’entités B2B via l’API est obsolète. La liste des entités B2B affectées comprend :

* Compte
* Opportunité
* Relation Compte-Personne
* Relation Opportunité-Personne
* Campagne
* Membre de la campagne
* Liste marketing
* Membre de la liste marketing

Pour plus d’informations, consultez le [guide de l’API de point d’entrée des définitions de segment](../segmentation/api/segment-definitions.md).

### Modifications des importations d’audiences à entités multiples dans l’outil Sandbox

Avec les mises à niveau de l’architecture, vous ne pourrez plus importer d’audiences à entités multiples avec des attributs B2B et des événements d’expérience s’ils ont été exportés avant la mise à niveau. L’importation de ces audiences échouera et ne pourront pas être automatiquement converties dans la nouvelle architecture. Pour contourner cette limitation, vous devez réexporter ces audiences, puis les importer dans leurs sandbox cibles respectifs à l’aide de l’outil Sandbox .

Pour plus d’informations, consultez le [guide d’utilisation des sandbox](../sandboxes/ui/sandbox-tooling.md) .