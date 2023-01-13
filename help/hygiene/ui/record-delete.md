---
title: Suppression d’enregistrements
description: Découvrez comment supprimer des enregistrements dans l’interface utilisateur de Adobe Experience Platform.
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
hide: true
hidefromtoc: true
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 56%

---

# Suppression d’enregistrements

Le [[!UICONTROL Hygiène des données] workspace](./overview.md) dans l’interface utilisateur de Adobe Experience Platform vous permet de supprimer les enregistrements qui participent à Identity Service et à Real-Time Customer Profile. Ces enregistrements peuvent être liés à des consommateurs individuels ou à toute autre entité incluse dans le graphique d’identités.

>[!IMPORTANT]
>
>Les demandes de suppression d’enregistrement ne sont disponibles que pour les organisations qui ont acheté **Adobe Health Care Shield**.
>
>
>Les suppressions d’enregistrements sont destinées à être utilisées pour la normalisation des données, la suppression des données anonymes ou la minimisation des données. Ils sont **not** à utiliser pour les demandes de droits des titulaires de données (conformité) en ce qui concerne les réglementations de confidentialité comme le Règlement général sur la protection des données (RGPD). Pour tous les cas d’utilisation de conformité, utilisez [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) au lieu de .

## Conditions préalables

La suppression d’enregistrements nécessite une compréhension pratique du fonctionnement des champs d’identité dans Experience Platform. Plus précisément, vous devez connaître les Principales valeurs d’identité des entités dont vous souhaitez supprimer les enregistrements, en fonction du jeu de données (ou des jeux de données) duquel vous les supprimez.

Pour plus d’informations sur les identités dans Platform, consultez la documentation suivante :

* [Adobe Experience Platform Identity Service](../../identity-service/home.md) : associe les identités des appareils et des systèmes, en liant les jeux de données en fonction des champs d’identité définis par les schémas XDM auxquels ils se conforment.
   * [Espaces de noms d’identité](../../identity-service/namespaces.md) : définissent les différents types d’informations d’identité qui peuvent être associés à une seule personne et constituent un composant obligatoire pour chaque champ d’identité.
* [Profil client en temps réel](../../profile/home.md): tire parti des graphiques d’identités pour fournir des profils consommateurs unifiés basés sur des données agrégées provenant de plusieurs sources, mises à jour en temps quasi réel.
* [Modèle de données d’expérience (XDM)](../../xdm/home.md) : fournit des structures et des définitions standard pour les données de Platform à l’aide de schémas. Tous les jeux de données de Platform sont conformes à un schéma XDM spécifique et le schéma définit les champs qui sont des identités.
   * [Champs d’identité](../../xdm/ui/fields/identity.md) : découvrez la définition d’un champ d’identité dans un schéma XDM.

## Créer une requête

Pour lancer le processus, sélectionnez **[!UICONTROL Créer une requête]** dans la page principale de l’espace de travail.

![Image illustrant le bouton [!UICONTROL Créer une requête] sélectionné](../images/ui/record-delete/create-request-button.png)

La boîte de dialogue de création de requête s’affiche. Par défaut, la variable **[!UICONTROL Supprimer un client]** est sélectionnée sous la propriété **[!UICONTROL Action requise]** . Conservez la sélection de cette option.

![Image montrant l’option de suppression du consommateur sélectionnée dans la boîte de dialogue de création](../images/ui/record-delete/consumer-action.png)

## Sélectionner des jeux de données

Sous , **[!UICONTROL Détails du client]** , l’étape suivante consiste à déterminer si vous souhaitez supprimer des enregistrements d’un seul jeu de données ou de tous les jeux de données.

Si vous choisissez **[!UICONTROL Sélectionner un jeu de données]**, sélectionnez l’icône de base de données (![image de l’icône de base de données](../images/ui/record-delete/database-icon.png)). Une boîte de dialogue s’affiche et vous permet de sélectionner le jeu de données souhaité dans la liste.

![Image illustrant la boîte de dialogue de sélection du jeu de données](../images/ui/record-delete/select-dataset.png)

Si vous souhaitez supprimer des enregistrements de tous les jeux de données, sélectionnez **[!UICONTROL Tous les jeux de données]**.

![Image illustrant l’option [!UICONTROL Tous les jeux de données] sélectionnée](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>La sélection de l’option **[!UICONTROL Tous les jeux de données]** peut entraîner un temps de suppression plus long et une suppression imprécise des enregistrements.

## Fournir des identités {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Identité principale"
>abstract="Une identité principale est un attribut qui lie un enregistrement au profil d’un client dans Experience Platform. Le champ d’identité principale d’un jeu de données est défini par le schéma sur lequel le jeu de données est basé. Dans cette colonne, vous devez indiquer le type (ou l’espace de noms) de l’identité Principale de l’enregistrement, telle que `email` pour les adresses électroniques et `ecid` pour les identifiants Experience Cloud. Pour en savoir plus, consultez le guide de l’interface utilisateur de l’hygiène des données ."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Valeur de l’identité"
>abstract="Dans cette colonne, vous devez indiquer la valeur de l’identité Principale de l’enregistrement, qui doit correspondre au type d’identité fourni dans la colonne de gauche. Si le type d’identité Principal est `email`, la valeur doit correspondre à l’adresse électronique de l’enregistrement. Pour en savoir plus, consultez le guide de l’interface utilisateur de l’hygiène de données."

Lors de la suppression d’enregistrements, vous devez fournir des informations d’identité afin que le système puisse déterminer les enregistrements à supprimer. Pour les jeux de données de Platform, les enregistrements sont supprimés en fonction du champ **Identité principale** défini par le schéma du jeu de données.

Comme tous les champs d’identité de Platform, une identité principale se compose de deux éléments : un **type** (parfois appelé espace de noms d’identité) et une **valeur**. Le type d’identité fournit un contexte sur la manière dont le champ identifie un enregistrement (une adresse électronique, par exemple) et la valeur représente l’identité spécifique d’un enregistrement pour ce type (par exemple, `jdoe@example.com` pour le `email` type d’identité). Les champs courants utilisés comme identités comprennent les informations de compte, les identifiants d’appareil et les identifiants de cookie.

>[!TIP]
>
>Si vous ne connaissez pas l’identité principale d’un jeu de données spécifique, vous pouvez la trouver dans l’interface utilisateur de Platform. Dans l’espace de travail **[!UICONTROL Jeux de données]**, sélectionnez le jeu de données en question dans la liste. Sur la page des détails du jeu de données, passez la souris sur le nom du schéma du jeu de données dans le rail de droite. L’identité principale s’affiche avec le nom et la description du schéma.
>
>![Image illustrant l’identité principale d’un jeu de données surligné dans l’interface utilisateur](../images/ui/record-delete/dataset-primary-identity.png)

Si vous supprimez des enregistrements d’un seul jeu de données, toutes les identités que vous fournissez doivent avoir le même type, car un jeu de données ne peut avoir qu’une seule identité Principale. Si vous effectuez une suppression dans tous les jeux de données, vous pouvez inclure plusieurs types d’identité, car différents jeux de données peuvent avoir différentes identités principales.

Deux options permettent de fournir des identités lors de la suppression d’enregistrements :

* [Charger un fichier JSON](#upload-json)
* [Saisir des valeurs d’identité manuellement](#manual-identity)

### Charger un fichier JSON {#upload-json}

Pour charger un fichier JSON, vous pouvez le faire glisser et le déposer dans la zone prévue à cet effet ou sélectionner **[!UICONTROL Choisir les fichiers]** pour parcourir et sélectionner les fichiers dans votre répertoire local.

![Image illustrant les méthodes de chargement de fichiers JSON dans l’interface utilisateur](../images/ui/record-delete/upload-json.png)

Le fichier JSON doit être formaté sous la forme d’un tableau d’objets, chaque objet représentant une identité.

```json
[
  {
    "namespaceCode": "email",
    "value": "jdoe@example.com"
  },
  {
    "namespaceCode": "email",
    "value": "san.gray@example.com"
  }
]
```

| Propriété | Description |
| --- | --- |
| `namespaceCode` | Type d’identité. |
| `value` | La valeur d’identité telle qu’elle est indiquée par le type. |

Une fois le fichier chargé, vous pouvez continuer à [envoyer la requête](#submit).

### Saisir des identités manuellement {#manual-identity}

Pour saisir les identités manuellement, sélectionnez **[!UICONTROL Ajouter une identité]**.

![Image illustrant le bouton [!UICONTROL Ajouter une identité] sélectionné](../images/ui/record-delete/add-identity.png)

Les commandes qui s’affichent vous permettent de saisir des identités une par une. Sous **[!UICONTROL Identité principale]**, utilisez le menu déroulant pour sélectionner le type d’identité. Sous **[!UICONTROL Valeur d’identité]**, indiquez la valeur d’identité Principale de l’enregistrement.

![Image illustrant un champ d’identité ajouté manuellement](../images/ui/record-delete/identity-added.png)

Pour ajouter d’autres identités, cliquez sur l’icône plus (![image de l’icône plus](../images/ui/record-delete/plus-icon.png)) en regard de l’une des lignes ou sélectionnez **[!UICONTROL Ajouter une identité]**.

![Image illustrant comment ajouter d’autres identités à la requête](../images/ui/record-delete/more-identities.png)

## Envoyer la requête (#submit)

Une fois que vous avez terminé d’ajouter des identités à la requête, sous **[!UICONTROL Paramètres de requête]**, attribuez un nom et une description facultative à la requête avant de sélectionner **[!UICONTROL Envoyer]**.

![Image illustrant le bouton [!UICONTROL Envoyer] sélectionné](../images/ui/record-delete/submit.png)

Vous êtes invité à confirmer la liste des identités dont vous souhaitez supprimer les données. Sélectionnez **[!UICONTROL Envoyer]** pour confirmer votre sélection.

![Image illustrant la boîte de dialogue de confirmation](../images/ui/record-delete/confirm-request.png)

Une fois la requête soumise, un ordre de travail est créé et s’affiche dans l’onglet [!UICONTROL Consommateur] de l’espace de travail [!UICONTROL Nettoyage de données]. Ensuite, vous pouvez surveiller le statut de l’ordre de travail lors du traitement de la requête.

>[!NOTE]
>
>Consultez la section de présentation sur [calendrier et transparence](../home.md#record-delete-transparency) pour plus d’informations sur le traitement des suppressions d’enregistrement une fois qu’elles sont exécutées.

## Étapes suivantes

Ce document explique comment supprimer des enregistrements dans l’interface utilisateur de l’Experience Platform. Pour plus d’informations sur l’exécution d’autres tâches d’hygiène de données dans l’interface utilisateur, consultez la [Présentation de l’interface utilisateur de l’hygiène de données](./overview.md).

Pour savoir comment supprimer des enregistrements à l’aide de l’API Data Hygiene, reportez-vous à la section [guide de point de terminaison des commandes de travail](../api/workorder.md).
