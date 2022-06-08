---
title: Suppression d’enregistrements de clients
description: Découvrez comment supprimer des enregistrements de consommateurs dans l’interface utilisateur de Adobe Experience Platform.
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
hide: true
hidefromtoc: true
source-git-commit: 95d75292b7697ef4f98e3ebd34c04724019ac37f
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 3%

---

# Suppression des enregistrements de consommateurs

>[!IMPORTANT]
>
>Actuellement, les fonctionnalités d’hygiène des données de Adobe Experience Platform ne sont disponibles que pour les organisations qui ont acheté Adobe Shield pour les soins de santé.

Le [[!UICONTROL Hygiène des données] workspace](./overview.md) Dans l’interface utilisateur de Adobe Experience Platform, vous pouvez supprimer les enregistrements de consommateurs qui participent à Identity Service et à Real-time Customer Profile.

## Conditions préalables

La suppression des enregistrements de consommateurs nécessite une compréhension pratique du fonctionnement des champs d’identité dans Experience Platform. Plus précisément, vous devez connaître les Principales valeurs d’identité des consommateurs dont vous souhaitez supprimer les enregistrements, en fonction du jeu de données (ou des jeux de données) duquel vous les supprimez.

Pour plus d’informations sur les identités dans Platform, consultez la documentation suivante :

* [Adobe Experience Platform Identity Service](../../identity-service/home.md) : associe les identités des appareils et des systèmes, en liant les jeux de données en fonction des champs d’identité définis par les schémas XDM auxquels ils se conforment.
   * [Espaces de noms d’identité](../../identity-service/namespaces.md): Les espaces de noms d’identité définissent les différents types d’informations d’identité qui peuvent être associés à une seule personne et qui sont un composant requis pour chaque champ d’identité.
* [Real-time Customer Profile](../../profile/home.md): tire parti des graphiques d’identités des consommateurs pour fournir des profils consommateurs unifiés basés sur des données agrégées provenant de plusieurs sources, mis à jour en temps quasi réel.
* [Modèle de données d’expérience (XDM)](../../xdm/home.md): Fournit des définitions et des structures standard pour les données de Platform grâce à l’utilisation de schémas. Tous les jeux de données Platform sont conformes à un schéma XDM spécifique et le schéma définit les champs qui sont des identités.
   * [Champs d’identité](../../xdm/ui/fields/identity.md): Découvrez comment un champ d’identité est défini dans un schéma XDM.

## Création d’une requête

Pour lancer le processus, sélectionnez **[!UICONTROL Créer une requête]** de la page principale de l’espace de travail.

![Image montrant le [!UICONTROL Créer une requête] bouton sélectionné](../images/ui/delete-consumer/create-request-button.png)

La boîte de dialogue de création de requête s’affiche. Par défaut, la variable **[!UICONTROL Consommateur]** est sélectionnée sous la propriété **[!UICONTROL Action]** . Laissez cette option sélectionnée.

![Image montrant l’option consommateur sélectionnée dans la boîte de dialogue de création](../images/ui/delete-consumer/consumer-action.png)

## Sélectionner des jeux de données

Sous , **[!UICONTROL Détails du client]** , l’étape suivante consiste à déterminer si vous souhaitez supprimer des données clients d’un seul jeu de données ou de tous les jeux de données.

Si vous choisissez **[!UICONTROL Sélectionner un jeu de données]**, sélectionnez l’icône de base de données (![Image de l&#39;icône de la base de données](../images/ui/delete-consumer/database-icon.png)) et une boîte de dialogue s’affiche, vous permettant de sélectionner le jeu de données souhaité dans la liste.

![Image montrant la boîte de dialogue de sélection du jeu de données](../images/ui/delete-consumer/select-dataset.png)

Si vous souhaitez supprimer des données de consommateur de tous les jeux de données, sélectionnez **[!UICONTROL Tous les jeux de données]**.

![Image montrant le [!UICONTROL Tous les jeux de données] option sélectionnée](../images/ui/delete-consumer/all-datasets.png)

>[!NOTE]
>
>En sélectionnant le **[!UICONTROL Tous les jeux de données]** peut entraîner un temps de suppression plus long et ne pas entraîner une suppression d’enregistrement exacte.

## Fournir des identités aux consommateurs {#provide-consumer-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Identité Principal"
>abstract="Une identité Principale est un attribut qui lie un enregistrement au profil d’un consommateur dans Experience Platform. Le champ d’identité Principal d’un jeu de données est défini par le schéma sur lequel le jeu de données est basé. Dans cette colonne, vous devez indiquer le type (ou l’espace de noms) de l’identité Principale du consommateur, par exemple &quot;email&quot; pour les adresses électroniques et &quot;ecid&quot; pour les identifiants Experience Cloud. Pour en savoir plus, consultez le guide de l’interface utilisateur de l’hygiène des données."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Valeur d’identité"
>abstract="Dans cette colonne, vous devez indiquer la valeur de l’identité Principale du consommateur, qui doit correspondre au type d’identité fourni dans la colonne de gauche. Si le type d’identité Principal est &quot;email&quot;, la valeur doit correspondre à l’adresse électronique du consommateur. Pour en savoir plus, consultez le guide de l’interface utilisateur de l’hygiène des données."

Lors de la suppression de données de consommateurs, vous devez fournir des informations d’identité afin que le système puisse déterminer les enregistrements à supprimer. Pour tout jeu de données de Platform, les enregistrements sont supprimés en fonction de la variable **Principale identité** champ défini par le schéma du jeu de données.

Comme tous les champs d’identité de Platform, une identité Principale se compose de deux éléments : a **type** (parfois appelé espace de noms d’identité) et un **value**. Le type d’identité fournit un contexte sur la manière dont le champ identifie un consommateur (une adresse électronique, par exemple) et la valeur représente l’identité spécifique d’un consommateur pour ce type (par exemple, `jdoe@example.com` pour le `email` type d’identité).  Les champs courants utilisés comme identités comprennent les informations de compte, les identifiants d’appareil et les identifiants de cookie.

>[!TIP]
>
>Si vous ne connaissez pas l’identité Principale d’un jeu de données spécifique, vous pouvez la trouver dans l’interface utilisateur de Platform. Dans le **[!UICONTROL Jeux de données]** workspace, sélectionnez le jeu de données en question dans la liste. Sur la page des détails du jeu de données, passez la souris sur le nom du schéma du jeu de données dans le rail de droite. L’identité Principale s’affiche avec le nom et la description du schéma.
>
>![Image montrant l’identité Principale d’un jeu de données surligné dans l’interface utilisateur](../images/ui/delete-consumer/dataset-primary-identity.png)

Si vous supprimez des enregistrements de consommateur d’un seul jeu de données, toutes les identités que vous fournissez doivent avoir le même type, car un jeu de données ne peut avoir qu’une seule identité Principale. Si vous supprimez de tous les jeux de données, vous pouvez inclure plusieurs types d’identité, car différents jeux de données peuvent avoir différentes identités Principales.

Deux options permettent de fournir des identités de consommateur lors de la suppression d’enregistrements de consommateur :

* [Chargement d’un fichier JSON](#upload-json)
* [Saisie manuelle des valeurs d’identité](#manual-identity)

### Chargement d’un fichier JSON {#upload-json}

Pour charger un fichier JSON, vous pouvez le faire glisser et le déposer dans la zone prévue à cet effet ou sélectionner **[!UICONTROL Sélection de fichiers]** pour parcourir et sélectionner dans votre répertoire local.

![Image montrant les méthodes de chargement de JSON dans l’interface utilisateur](../images/ui/delete-consumer/upload-json.png)

Le fichier JSON doit être formaté sous la forme d’un tableau d’objets, chaque objet représentant une identité du consommateur.

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
| `value` | L’identité du consommateur telle qu’elle est identifiée par le type. |

Une fois le fichier chargé, vous pouvez continuer à [envoyer la requête ;](#submit).

### Saisie manuelle des identités {#manual-identity}

Pour saisir les identités manuellement, sélectionnez **[!UICONTROL Ajout d’une identité]**.

![Image montrant le [!UICONTROL Ajout d’une identité] bouton sélectionné](../images/ui/delete-consumer/add-identity.png)

Des contrôles s’affichent pour vous permettre de saisir les identités des consommateurs un par un. Sous **[!UICONTROL Identité Principal]**, utilisez le menu déroulant pour sélectionner le type d’identité. Sous **[!UICONTROL Valeur d’identité]**, fournissez la valeur d’identité Principale pour le consommateur.

![Image montrant un champ d’identité ajouté manuellement](../images/ui/delete-consumer/identity-added.png)

Pour ajouter d’autres identités, cliquez sur l’icône plus (![Image de l’icône plus](../images/ui/delete-consumer/plus-icon.png)) en regard de l’une des lignes, ou sélectionnez **[!UICONTROL Ajout d’une identité]**.

![Image montrant comment ajouter d’autres identités à la requête](../images/ui/delete-consumer/more-identities.png)

## Envoyer la demande (#submit)

Une fois que vous avez terminé d’ajouter des identités à la requête, sélectionnez **[!UICONTROL Envoyer]**.

![Image montrant le [!UICONTROL Envoyer] bouton sélectionné](../images/ui/delete-consumer/submit.png)

Vous êtes invité à confirmer la liste des identités dont vous souhaitez supprimer les données. Sélectionner **[!UICONTROL Envoyer]** pour confirmer votre sélection.

![Image de la boîte de dialogue de confirmation](../images/ui/delete-consumer/confirm-request.png)

Une fois la demande envoyée, un ordre de travail est créé et s’affiche sur la page [!UICONTROL Consommateur] de l’onglet [!UICONTROL Hygiène des données] workspace. À partir de là, vous pouvez surveiller l’état de l’ordre de travail lors du traitement de la requête. La plupart des commandes de travail de suppression des clients prennent plusieurs jours.

## Étapes suivantes

Ce document explique comment supprimer des enregistrements de consommateurs dans l’interface utilisateur de l’Experience Platform. Pour plus d’informations sur l’exécution d’autres tâches d’hygiène des données dans l’interface utilisateur, reportez-vous à la section [Présentation de l’interface utilisateur de l’hygiène des données](./overview.md).

Pour savoir comment supprimer des enregistrements de consommateurs à l’aide de l’API Data Hygiene, reportez-vous à la section [guide de point de terminaison des commandes de travail](../api/workorder.md).
