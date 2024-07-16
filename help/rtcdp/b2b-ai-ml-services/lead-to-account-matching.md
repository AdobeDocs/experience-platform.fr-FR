---
title: Conduire à la correspondance de comptes dans Real-Time CDP B2B
type: Documentation
description: Présentation et informations supplémentaires sur la fonctionnalité de correspondance de comptes dans la plateforme CDP B2B Experience Platform.
feature: Get Started, Profiles, B2B
badgeB2B: label="Édition B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 5%

---

# Conduire à la correspondance de comptes dans Real-Time CDP B2B

## Vue d’ensemble {#overview}

Le marketing basé sur les comptes est une stratégie de plus en plus importante pour le marketing B2B. Le marketing basé sur les comptes offre les avantages clés suivants pour acquérir des clients à forte valeur ajoutée spécifiques :

- Effacer le ROI
- Alignement commercial et marketing
- Une approche personnalisée
- Moins de ressources gaspillées
- Un cycle de vente plus court

Le marketing basé sur les comptes permet de lier des personnes connues et des visiteurs web anonymes à des comptes de ventes. Cela permet aux équipes marketing d’interagir avec les prospects potentiels des comptes cibles dès le début du parcours client afin d’augmenter leurs chances de conversion. Un enregistrement de personne connue comprend généralement une partie ou l’ensemble des informations suivantes :

- Nom de la personne
- Adresse e-mail
- Numéro de contact
- Nom de la société
- Site Web de la société
- Intitulé du poste
- Emplacement

La correspondance des prospects et des comptes permet d’associer des profils de personnes connus à des profils de compte. Vous pouvez ensuite segmenter et cibler des données dans un contexte B2B tel que des comptes, des opportunités, etc. Les profils de personnes peuvent être classés dans les trois catégories suivantes :

- **Profil de personne du compte :** Le profil de personne est déjà associé à au moins un profil de compte par le biais de la relation à partir d’une source de données. Cela signifie qu’il existe au moins un fragment de contact.

>[!NOTE]
>
> Les profils de personne de compte ne correspondent pas lors de l’exécution d’un prospect pour les tâches de correspondance de compte.

- **Profil de personne connue :** Le profil de personne n’est associé à aucun profil de compte et au moins un des attributs de profil de personne suivants a une valeur :

   - Adresse e-mail
   - Nom de la société
   - Site Web de la société

- **Profil de personne anonyme :** Le profil de personne n’est associé à aucun profil de compte et aucun des attributs de profil de personne suivants n’a de valeur :

   - Adresse e-mail
   - Nom de la société
   - Site Web de la société

>[!NOTE]
>
> Un profil de personne peut être associé à plusieurs profils de compte. Cependant, le processus de correspondance de comptes de piste ne correspondra qu’à la meilleure correspondance. Si un plus grand nombre de correspondances est requis, associez l’prospect à la fonction de correspondance de compte associée.

## Fonctionnement {#how-it-works}

Les tâches exécutées quotidiennement utilisent des facteurs déterministes et probabilistes pour faire correspondre des profils de prospect connus sans aucune association de compte existante. L’un des attributs suivants est disponible pour les profils de prospect connus :

- b2b.companyName
- b2b.companyWebsite
- workEmail

>[!NOTE]
>
> L’attribut b2b.personKey.sourceKey doit exister.

Les attributs b2b.companyName, b2b.companyWebsite et b2b.personKey.sourceKey peuvent se trouver dans le groupe de champs b2b du schéma de personne B2B.

![Schéma de personne B2B présentant les attributs](/help/rtcdp/accounts/images/b2b-person-schema.png)

L’attribut workEmail se trouve en tant que groupe de champs de niveau supérieur dans le schéma de personne B2B.

![ Schéma de personne B2B affichant workEmail](/help/rtcdp/accounts/images/b2b-person-workemail.png)

Les profils ne seront mieux mis en correspondance que si le score de correspondance est supérieur à un seuil de confiance interne. Les résultats sont enregistrés dans un nouveau jeu de données système de la relation de personne de compte existante XDM.

Le service de correspondance de compte est exécuté lorsqu’un nouvel instantané de profil de personne est disponible, une fois toutes les 24 heures. Consultez la documentation pour plus d’informations sur la [configuration de la correspondance de pistes vers comptes](/help/rtcdp/accounts/account-profile-ui-guide.md).

## Comment afficher le résultat de la correspondance de comptes {#how-to-view}

Après l’exécution de la tâche, les résultats sont enregistrés dans un nouveau jeu de données de la relation de personne de compte existante XDM.

Pour prévisualiser le jeu de données, sélectionnez **[!UICONTROL Prévisualiser le jeu de données]** en haut à droite.

![Nouveau jeu de données](/help/rtcdp/accounts/images/b2b-dataset-output.png)

Le jeu de données inclut les informations de compte correspondantes ainsi que le score de correspondance du jeu de données sélectionné. Le champ **[!UICONTROL Relationship Source]** indique s’il provient du processus de correspondance de piste vers compte.

![Prévisualiser les scores de confiance du jeu de données et la sortie](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## Surveillance des traitements de correspondance de comptes {#monitoring-jobs}

Vous pouvez surveiller l’état de la tâche et les mesures associées pour toute piste permettant d’effectuer des tâches correspondantes à partir du tableau de bord.

Consultez la documentation pour plus d’informations sur les [tâches de surveillance pour obtenir la correspondance de comptes](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
