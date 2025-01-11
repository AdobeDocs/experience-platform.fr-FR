---
title: Correspondance des prospects et des comptes dans Real-Time CDP B2B
type: Documentation
description: Présentation et plus d’informations sur la fonctionnalité de correspondance des prospects et des comptes dans le B2B de CDP Experience Platform.
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: 4ba609e777716b1b38f5b143587e5476d851e344
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 3%

---

# Correspondance des prospects et des comptes dans Real-Time CDP B2B

## Vue d’ensemble {#overview}

Le marketing basé sur les comptes est une stratégie de plus en plus importante pour le marketing B2B. Le marketing basé sur les comptes offre les avantages clés suivants pour acquérir des clients spécifiques à forte valeur ajoutée :

- Effacer le RSI
- Alignement commercial et marketing
- Une approche personnalisée
- Moins de ressources gaspillées
- Un cycle de vente plus court

Le marketing basé sur les comptes permet de lier des clients connus à des comptes de vente. Cela permet aux équipes marketing d’interagir avec les prospects potentiels des comptes cibles dès le début du parcours client afin d’augmenter leurs chances de conversion. Un enregistrement de personne connu comprend généralement une partie ou la totalité des informations suivantes :

- Nom de la personne
- Adresse e-mail
- Numéro de contact
- Nom de la société
- Site web de la société
- Intitulé du poste
- Emplacement

## Fonctionnement {#how-it-works}

Les tâches exécutées quotidiennement utilisent des facteurs déterministes et probabilistes pour faire correspondre les profils de prospect connus sans associations de comptes existantes. Les profils de prospect connus disposent de l’un des attributs suivants :

- b2b.companyName
- b2b.companyWebsite
- workEmail

>[!NOTE]
>
> L’attribut b2b.personKey.sourceKey doit exister.

Les attributs b2b.companyName, b2b.companyWebsite et b2b.personKey.sourceKey peuvent être situés dans le groupe de champs b2b du schéma de personne B2B.

![Schéma de personne B2B présentant les attributs](/help/rtcdp/accounts/images/b2b-person-schema.png)

L’attribut workEmail se trouve en tant que groupe de champs de niveau supérieur dans le schéma de personne B2B.

![Schéma de personne B2B affichant workEmail](/help/rtcdp/accounts/images/b2b-person-workemail.png)

Les profils ne seront mieux associés que si le score de correspondance est supérieur à un seuil de confiance interne. Les résultats sont enregistrés dans un nouveau jeu de données système du XDM relation compte/personne existant.

Le service de correspondance des prospects et des comptes s’exécute lorsqu’un nouvel instantané de profil de personne est disponible, toutes les 24 heures. Pour plus d’informations sur la [configuration de la correspondance des prospects et des comptes](/help/rtcdp/accounts/account-profile-ui-guide.md), consultez la documentation.

## Comment afficher la sortie de correspondance du prospect et du compte {#how-to-view}

Après l’exécution de la tâche, les résultats sont enregistrés dans un nouveau jeu de données du XDM relation compte/personne existant.

Pour prévisualiser le jeu de données, sélectionnez **[!UICONTROL Prévisualiser le jeu de données]** en haut à droite.

![Nouveau jeu de données](/help/rtcdp/accounts/images/b2b-dataset-output.png)

Le jeu de données comprend les informations de compte correspondantes ainsi que le score de correspondance pour le jeu de données sélectionné. Le champ **[!UICONTROL Source de relation]** indique s’il provient du processus de correspondance entre le prospect et le compte.

![Prévisualiser les scores de confiance et la sortie du jeu de données](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## Surveillance des tâches de correspondance des prospects et des comptes {#monitoring-jobs}

Vous pouvez surveiller le statut de la tâche et les mesures associées pour toutes les tâches de correspondance des prospects et des comptes via le tableau de bord.

Pour plus d’informations sur la [surveillance des tâches pour la correspondance des prospects et des comptes](/help/dataflows/ui/b2b/monitor-profile-enrichment.md), consultez la documentation.
