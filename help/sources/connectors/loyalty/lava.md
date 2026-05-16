---
title: LAVE
description: En savoir plus sur la source LAVA sur Adobe Experience Platform
badge: Beta
hide: true
source-git-commit: 04601673ca9c158c183469cdc6d704e859d057b4
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 2%

---

# [!DNL LAVA]

>[!AVAILABILITY]
>
>La source [!DNL LAVA] est en version Beta. Lisez les [termes et conditions](../../home.md#terms-and-conditions) dans la présentation des sources pour plus d’informations sur l’utilisation de sources étiquetées bêta.

[[!DNL LAVA]](https://lava.ai/) est une plateforme d’engagement client. [!DNL LAVA] s&#39;intègre à vos billetteries, points de vente, applications mobiles et autres points de contact et crée des moments qui comptent avec nos solutions d&#39;automatisation, de fidélité et de laissez-passer mobile.

Le connecteur source [!DNL LAVA] peut être utilisé pour plusieurs jeux différents de données et d’événements de profil. Vous pouvez décider lesquelles sont pertinentes pour vous. Pour chaque type de données que vous souhaitez diffuser de [!DNL LAVA] à Adobe, répétez les étapes de « Connexion à votre compte LAVA ».

## Conditions préalables

Avant de pouvoir utiliser ce connecteur source, vérifiez les points suivants :

* Vous êtes déjà client [!DNL LAVA] et des droits d’exportation Adobe vous ont été accordés.
* Vous disposez d’un compte [Console LAVA](https://app.lava.ai/) avec un accès « Administrateur » ou « Gestionnaire d’exportation ».
* (Recommandé) Vous disposez des autorisations de gestionnaire de sandbox dans Adobe Experience Cloud.


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

### Charger le package [!DNL LAVA]

[!DNL LAVA] fournit un package qui inclut nos groupes de champs, schémas, espaces de noms d’identité et jeux de données recommandés pour l’utilisation de [!DNL LAVA] dans Experience Platform. L’utilisation de ces packages est recommandée, mais pas obligatoire.

Pour charger ces packages, dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sandboxes]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sandboxes]. L’écran [!UICONTROL Packages] affiche les packages disponibles. Sélectionnez **[!UICONTROL Create package]** et **[!UICONTROL Paste package payload]**, puis collez les éléments suivants.

```json
{
  "imsOrgId": "1EF71E43679AAD1E0A495C77@AdobeOrg",
  "packageId": "416a0c2a32794092aa1a957cbe9a6698"
}
```

Pour plus d’informations sur le chargement du package, consultez le tutoriel [partage de packages](../../../sandboxes/ui/sharing-packages-across-orgs.md#create-a-new-package-using-a-package-payload).

Une fois le package créé, sélectionnez les points de suspension (`...`) pour ouvrir le menu, puis sélectionnez **[!UICONTROL Import Package]** pour importer le package. Pour plus d’informations sur l’importation d’un package, consultez le [guide d’utilisation des sandbox](../../../sandboxes/ui/sandbox-tooling.md#import-a-package-to-a-target-sandbox).

## Étapes suivantes

Le connecteur source [!DNL LAVA] ingère des profils de membres, des soldes de récompenses et des événements d’analyse de ticket dans Experience Platform. Planifiez les conditions préalables répertoriées, mappez et étendez les schémas à l’aide des tables de référence de champ et des fichiers d’exemple JSON, et importez éventuellement le package recommandé de [!DNL LAVA] dans un sandbox avant de créer des connexions et des flux de données.

Pour une configuration pas à pas :

* [Créer une connexion source et un flux de données pour diffuser  [!DNL LAVA]  données à l’aide de l’API  [!DNL Flow Service] &#x200B;](../../tutorials/api/create/loyalty/lava.md)
* [Créer une connexion source et un flux de données pour diffuser  [!DNL LAVA]  données à l’aide de l’interface utilisateur](../../tutorials/ui/create/loyalty/lava.md)
