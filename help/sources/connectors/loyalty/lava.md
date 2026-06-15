---
title: LAVE
description: En savoir plus sur la source LAVA sur Adobe Experience Platform
source-git-commit: b1810a83a3eda5674d91a8c122f3ad858ef94aa1
workflow-type: tm+mt
source-wordcount: '1584'
ht-degree: 1%

---

# [!DNL LAVA]

[[!DNL LAVA]](https://lava.ai/) est une plateforme d’engagement client. [!DNL LAVA] s&#39;intègre à vos billetteries, points de vente, applications mobiles et autres points de contact et crée des moments qui comptent avec nos solutions d&#39;automatisation, de fidélité et de laissez-passer mobile.

## Conditions préalables

Avant de pouvoir utiliser ce connecteur source, vérifiez les points suivants :

* Vous êtes déjà client [!DNL LAVA] et des droits d’exportation Adobe vous ont été accordés.
* Vous disposez d’un compte [Console LAVA](https://app.lava.ai/) avec un accès « Administrateur » ou « Gestionnaire d’exportation ».
* (Recommandé) Vous disposez des autorisations de gestionnaire de sandbox dans Adobe Experience Cloud.

## Flux de données

Le connecteur source [!DNL LAVA] peut être utilisé pour plusieurs jeux différents de données et d’événements de profil. Vous pouvez décider lesquels sont pertinents pour vous, en diffusant uniquement ces enregistrements vers Adobe.

### Profils de membre

Le profil de membre répertorie les attributs de profil clés que LAVA stocke sur un membre. En utilisant `email` comme champ d’identité, [!DNL Adobe Real-time Customer Profiles] pouvez grouper des enregistrements [!DNL LAVA] avec d’autres profils Adobe.

Téléchargez le fichier de données [exemples de profils de membres ici.](../../assets/lava/lava_profile_sample.json)

| Champ [!DNL LAVA] connecteur Source | Exemple de valeur | Description |
| --- | --- | --- |
| `lavaId` | c448e091-af0f-4eab-98ff-2c758c149051 | ID de [!DNL LAVA] de l’utilisateur. |
| `firstName` | John | Prénom de l’utilisateur. |
| `lastName` | Doe | Nom de l’utilisateur. |
| `email` | jdoe@example.com | Adresse e-mail de l’utilisateur. |
| `phone` | +12223334444 | Numéro de téléphone de l’utilisateur. |
| `type` | profil | Indicateur du type d’enregistrement concerné. |
| `id` | c448e091-af0f-4eab-98ff-2c758c149051 | ID unique pour l’enregistrement. |
| `timestamp` | 2025-10-:51:04.317084Z | Lorsque ces attributs ont été définis pour le profil. |

{style="table-layout:auto"}

### Soldes des membres

L&#39;origine du solde du membre répertorie les soldes des récompenses de vos membres. `balances` est un tableau. Lorsque vous les utilisez pour les audiences, la personnalisation du contenu, les conditions et d’autres emplacements de ce type, vous devez souvent sélectionner une entrée particulière, répéter quelque chose pour toutes les entrées ou agréger plusieurs entrées.

Téléchargez le fichier de données [exemples de soldes de membres ici.](../../assets/lava/lava_balance_sample.json)


| Champ [!DNL LAVA] connecteur Source | Exemple de valeur | Description |
| --- | --- | --- |
| `lavaId` | `c448e091-af0f-4eab-98ff-2c758c149051` | ID de [!DNL LAVA] de l’utilisateur. |
| `balances[]` | - | Liste des soldes de récompense en LAVA. Un solde est une instance d’une récompense avec une expiration spécifique. Si un membre possède un montant de récompense expirant à la date A et un montant de la même récompense expirant à la date B, ils seront enregistrés comme soldes distincts. Voir balanceSummary pour une agrégation. |
| `balances[].amount` | 500 | Montant des éléments de récompense dans ce solde. Pour la valeur stockée, il s’agit de l’unité de dénomination la plus basse (centimes). |
| `balances[].expiresAt` | `2025-10-22T12:51:04.317084Z` | À l’expiration de ce solde. |
| `balances[].rewardId` | 123 | ID d’une récompense [!DNL LAVA]. Cela ne change jamais pour une récompense donnée. |
| `balances[].rewardName` | Crédit F&amp;B | Nom de la récompense configurée dans la console Activation du moment [!DNL LAVA]. Cela peut être modifié. |
| `balances[].rewardSlug` | Crédit | Slogan principal de la récompense configurée dans la console d’activation du moment [!DNL LAVA]. Cela peut être modifié. |
| `balances[].rewardType` | stocké | Le type de récompense (accès, offre, points, stocké ou bon). |
| `type` | récompenses | Indicateur du type d’enregistrement concerné. |
| `id` | `8fefe232-0375-4d56-a24c-d009e9d351e8` | ID unique pour l’enregistrement. |
| `timestamp` | `2025-10-22T12:51:04.317084Z` | Date à laquelle ces données ont été enregistrées. |

{style="table-layout:auto"}

### Événements d’analyse des tickets

La source d&#39;événement d&#39;analyse du ticket fournit des informations détaillées chaque fois qu&#39;un membre analyse un ticket lors d&#39;un événement. Ces données peuvent être utilisées pour comprendre les schémas d’assiduité, d’engagement et de comportement dans des lieux ou activités spécifiques. En diffusant des événements d’analyse de ticket vers Adobe Experience Platform, vous pouvez augmenter les profils des membres et activer la personnalisation ou l’analyse pilotée par les événements. Chaque enregistrement d’événement de balayage comprend des métadonnées sur l’événement, le lieu, ainsi que le lieu et la date du balayage.

Téléchargez le fichier de données [exemple d’événement d’analyse de ticket ici.](../../assets/lava/lava_ticketscan_sample.json)

| Champ [!DNL LAVA] connecteur Source | Exemple de valeur | Description |
| --- | --- | --- |
| `lavaId` | `aff0ee5f-da62-4054-8cdb-076f5b60bfc3` | ID de [!DNL LAVA] de l’utilisateur qui a analysé le ticket. |
| `eventId` | 1234 | Identifiant d’un événement fourni par un service de ticket. |
| `eventName` | GRE1234A | Nom d’événement fourni par le service de ticket. |
| `eventLabel` | Vert Et Bleu | Description d’un événement fournie par le fournisseur de billets. |
| `venue` | ABC | Code de lieu utilisé par le fournisseur de billets. |
| `venueLabel` | Stade ABC | Description du lieu fournie par le billetterie. |
| `section` | GA4 | Section des places sur le ticket analysé. |
| `sectionLabel` | Général | Libellé de la section fournie par le fournisseur de tickets. |
| `row` | GA3 | Ligne sur le ticket analysé. |
| `seat` | 13 | Place sur le ticket scanné. |
| `gate` | ÉQUIPE ST1 | Porte sur le ticket scanné. |
| `gateLabel` | Général | Libellé du point de contrôle fourni par le fournisseur de billets. |
| `type` | event-ticketscan | Indicateur du type d’enregistrement concerné. |
| `id` | `1234567/GRE1234A/GA4/GA3/13/0` | Identifiant unique de l’événement d’analyse du ticket. |
| `timestamp` | `2025-11-03T01:41:00Z` | Le moment où l&#39;analyse du ticket a eu lieu. |

{style="table-layout:auto"}

### Événements de transaction

La source d&#39;événement de transaction fournit des informations détaillées chaque fois qu&#39;un achat est effectué dans un système de point de vente par un utilisateur identifié comme [!DNL LAVA]. Ces données peuvent être utilisées pour évaluer le taux d’utilisation des promotions, comprendre les préférences des clients et évaluer le rendement des ventes. En diffusant des événements d’analyse de ticket vers Experience Platform, vous pouvez augmenter les profils des membres et activer la personnalisation ou l’analyse pilotée par les événements. Chaque enregistrement d’événement de transaction comprend des métadonnées sur l’achat, [!DNL LAVA] récompenses utilisées et les articles achetés. Notez que certains fournisseurs ne fournissent ces données que lorsqu&#39;une récompense a été appliquée.

Téléchargez le fichier de données [exemple d’événement de transaction ici.](../../assets/lava/lava_transaction_sample.json)

| Champ [!DNL LAVA] connecteur Source | Exemple de valeur | Description |
| --- | --- | --- |
| `lavaId` | `52b6a289-f5a0-47f5-b5b5-da3e08aaedb9` | ID de [!DNL LAVA] de l’utilisateur qui a effectué un achat. |
| `transactionId` | `8d515630-eb0f-43bc-a9f6-221f3813f438` | ID [!DNL LAVA] pour la transaction. |
| `referenceId` | `2aed9e2c-77a4-496c-81cc-e9772d128c0e` | ID créé au point de vente pour la transaction. |
| `subtotal` | `974` | Sous-total de la transaction dans l&#39;unité de dénomination la plus basse (centimes). |
| `total` | `974` | Total de la transaction dans l&#39;unité de dénomination la plus basse (centimes). |
| `location` | `64312` | Emplacement où la transaction a eu lieu. |
| `items[]` | - | Liste des articles achetés dans cette transaction. Ce champ est absent (liste non vide) lorsque les données au niveau de l&#39;article ne sont pas fournies par le fournisseur. |
| `items[].sku` | `1083947` | SKU de l’élément. |
| `items[].amount` | `1949` | Prix unitaire de l’article dans l’unité de dénomination la plus basse (centimes). |
| `items[].quantity` | `1` | Quantité de cet article achetée. |
| `items[].adjustedTotal` | `1949` | Prix total de cet élément de ligne après application de toute récompense au niveau de l’élément, dans l’unité de dénomination la plus basse (centimes). |
| `items[].rewardsApplied[]` | - | Liste des récompenses appliquées à cet élément. |
| `items[].rewardsApplied[].amount` | `975` | Montant de la remise appliquée par cette récompense, dans l’unité de dénomination la plus basse (centimes). |
| `items[].rewardsApplied[].rewardId` | `5` | Identifiant [!DNL LAVA] de la récompense appliquée. |
| `redeemedAmount` | `0` | Montant de la valeur stockée remboursée dans cette transaction, dans l&#39;unité de dénomination la plus basse (centimes). |
| `rewardsApplied[]` | - | Liste des récompenses appliquées à cette transaction. |
| `rewardsApplied[].amount` | `975` | Montant de la remise appliquée par cette récompense, dans l’unité de dénomination la plus basse (centimes). |
| `rewardsApplied[].rewardId` | `5` | Identifiant [!DNL LAVA] de la récompense appliquée. |
| `type` | `transaction` | Indicateur du type d’enregistrement concerné. |
| `id` | `8aa43866-173f-4c6e-bfa1-f231e34d6d71` | ID unique pour l’enregistrement. |
| `timestamp` | `2026-05-09T22:24:43.951Z` | Lorsque la transaction a été effectuée. |

{style="table-layout:auto"}

### Événements comptables

La source d&#39;événement comptable fournit un enregistrement de chaque modification des soldes d&#39;un membre, y compris les allocations dans un moment, les allocations provenant du remplissage d&#39;un formulaire, les rachats effectués dans le cadre d&#39;un achat ou par l&#39;intermédiaire de l&#39;application [!DNL LAVA], et les transferts. Une `amount` positive indique que des récompenses ont été ajoutées au solde ; une `amount` négative indique que des récompenses ont été échangées ou supprimées. Les événements de transfert produisent deux enregistrements : l&#39;un pour le membre qui perd le solde et l&#39;autre pour le membre qui le reçoit. Les paiements et les transactions peuvent utiliser plusieurs soldes, chacun d&#39;eux étant présenté comme un événement distinct.

Téléchargez le fichier [exemple de données d’événements comptables ici.](../../assets/lava/lava_ledger_sample.json)

| Champ [!DNL LAVA] connecteur Source | Exemple de valeur | Description |
| --- | --- | --- |
| `lavaId` | `292c367c-19ee-4d56-8d33-b2ab2c8fd553` | ID de [!DNL LAVA] du membre dont le solde a changé. |
| `amount` | `-100` | Le changement du solde de récompense. Les valeurs positives indiquent des subventions ; les valeurs négatives indiquent des remboursements ou des déductions. Pour la valeur stockée, il s’agit de l’unité de dénomination la plus basse (centimes). |
| `expiresAt` | `2026-05-31T22:40:43.109Z` | À l’expiration du solde concerné. |
| `rewardId` | `1` | ID d’une récompense [!DNL LAVA]. Cela ne change jamais pour une récompense donnée. |
| `rewardName` | `F&B Credit` | Nom de la récompense configurée dans la console Activation du moment [!DNL LAVA]. Cela peut être modifié. |
| `rewardSlug` | `Credit` | Slogan principal de la récompense configurée dans la console d’activation du moment [!DNL LAVA]. Cela peut être modifié. |
| `rewardType` | `stored` | Le type de récompense (accès, offre, points, stocké ou bon). |
| `type` | `ledger` | Indicateur du type d’enregistrement concerné. |
| `id` | `8aa43866-173f-4c6e-bfa1-f231e34d6d71` | ID unique pour l’enregistrement. |
| `timestamp` | `2026-05-21T22:40:43.109Z` | Lorsque le solde a été modifié. |

{style="table-layout:auto"}

### Événements combinés

Utilisez ce [fichier d’exemple de données d’événement combiné](../../assets/lava/lava_transaction_sample.json) pour configurer un flux de données unique qui ingère tous les types d’événements.

## Considérations relatives au déploiement

1. Créez un flux de données pour les données de profil de membre si vous avez besoin de données de base sur [!DNL LAVA] membres et/ou si vous souhaitez que [!DNL LAVA] données soient regroupées dans d’autres profils par adresse e-mail.
2. Si vous utilisez les données de soldes de membres, elles doivent être stockées dans un jeu de données distinct de celui du profil de membres.
3. Les événements peuvent être stockés dans un ou plusieurs jeux de données. Pour stocker dans un seul jeu de données, créez un flux de données à l’aide du fichier/mappage de données d’événement « combiné », puis configurez plusieurs exportations dans le [!DNL LAVA MAC] vers la même URL d’ingestion et le même ID de flux. Pour stocker chaque type d’événement dans un jeu de données différent, créez un flux de données pour chaque jeu de données, puis configurez chaque exportation du [!DNL LAVA MAC] vers l’URL d’ingestion et l’ID de flux pour le flux de données approprié.

## Charger le package [!DNL LAVA]

[!DNL LAVA] fournit un package qui inclut nos groupes de champs, schémas, espaces de noms d’identité et jeux de données recommandés pour l’utilisation de [!DNL LAVA] dans Experience Platform. L’utilisation de ces packages est recommandée, mais pas obligatoire.

Pour charger ces packages, dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sandbox]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sandbox]. L’écran [!UICONTROL Packages] affiche les packages disponibles. Sélectionnez **[!UICONTROL Créer un package]** et **[!UICONTROL Coller la payload du package]** et collez les éléments suivants.

```json
{
  "imsOrgId": "1EF71E43679AAD1E0A495C77@AdobeOrg",
  "packageId": "7ec94330c1ca43a09266a9a3b85f3727"
}
```

Pour plus d’informations sur le chargement du package, consultez le tutoriel [partage de packages](../../../sandboxes/ui/sharing-packages-across-orgs.md#create-a-new-package-using-a-package-payload).

Une fois le package créé, sélectionnez les points de suspension (`...`) pour ouvrir le menu, puis sélectionnez **[!UICONTROL Importer le package]** pour importer le package. Pour plus d’informations sur l’importation d’un package, consultez le [guide d’utilisation des sandbox](../../../sandboxes/ui/sandbox-tooling.md#import-a-package-to-a-target-sandbox).

Le package [!DNL LAVA] comprend trois jeux de données : [!DNL LAVA Profiles], [!DNL LAVA Balances] et [!DNL LAVA Events]. Bien que les profils et soldes utilisent le même schéma, ils doivent être des jeux de données distincts afin que les mises à jour des soldes ne remplacent pas les mises à jour des profils, et vice versa.

## Étapes suivantes

Le connecteur source [!DNL LAVA] ingère des profils de membres, des soldes de récompenses, des événements d’analyse de ticket, des événements de transaction et des événements comptables dans Experience Platform. Planifiez les conditions préalables répertoriées, mappez et étendez les schémas à l’aide des tables de référence de champ et des fichiers d’exemple JSON, et importez éventuellement le package recommandé de [!DNL LAVA] dans un sandbox avant de créer des connexions et des flux de données.

Pour une configuration pas à pas :

* [Créer une connexion source et un flux de données pour diffuser  [!DNL LAVA]  données à l’aide de l’API  [!DNL Flow Service] &#x200B;](../../tutorials/api/create/loyalty/lava.md)
* [Créer une connexion source et un flux de données pour diffuser  [!DNL LAVA]  données à l’aide de l’interface utilisateur](../../tutorials/ui/create/loyalty/lava.md)
