---
title: Connecter AWS Redshift à Experience Platform à l’aide de l’interface utilisateur
description: Découvrez comment connecter un compte AWS Redshift à Experience Platform à l’aide de l’interface utilisateur des sources.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
TQID: https://experienceleague.adobe.com/FPdemGIDPy-gOInJNktinBaP8PD9e7BmXxtiGR1Fwy8
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
subfeature_v2:
  - id: b572b7ff-a413-4173-b2b4-d7d3874f1b9b
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 717
ht-degree: 21%

---

# Connexion d’[!DNL AWS Redshift] à Experience Platform à l’aide de l’interface utilisateur

>[!IMPORTANT]
>
>La source [!DNL AWS Redshift] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Lisez ce guide pour savoir comment connecter votre compte [!DNL AWS Redshift] à Adobe Experience Platform à l’aide de l’espace de travail des sources dans l’interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL AWS Redshift] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/databases.md).

## Parcourir le catalogue des sources

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sélectionnez **[!DNL AWS Redshift]** sous la catégorie *[!UICONTROL Databases]*, puis sélectionnez **[!UICONTROL Set up]**.

>[!TIP]
>
>Les sources du catalogue affichent l’option **[!UICONTROL Set up]** lorsqu’une source donnée ne dispose pas encore d’un compte authentifié. Une fois qu’un compte authentifié existe, cette option devient **[!UICONTROL Add data]**.

![Le catalogue des sources avec la carte source AWS Redshift sélectionnée.](../../../../images/tutorials/create/redshift/catalog.png)

## Utiliser un compte existant {#existing}

Ensuite, vous passez à l’étape d’authentification du workflow des sources. Ici, vous pouvez utiliser un compte existant ou en créer un nouveau.

Pour utiliser un compte existant, sélectionnez le compte [!DNL AWS Redshift] dans le répertoire des comptes, puis sélectionnez **[!UICONTROL Next]** pour continuer.

![Répertoire des comptes dans le workflow des sources où les comptes existants sont répertoriés.](../../../../images/tutorials/create/redshift/existing.png)

## Créer un nouveau compte {#create}

Si vous ne disposez pas d’un compte existant, vous devez créer un compte en fournissant les informations d’authentification nécessaires qui correspondent à votre source.

Pour créer un compte, sélectionnez **[!UICONTROL New account]**, puis fournissez un nom et éventuellement une description pour votre compte.

### Connexion à Experience Platform sur Azure {#azure}

Pour connecter votre compte [!DNL AWS Redshift] à Experience Platform sur Azure, saisissez vos informations d’authentification dans le formulaire de saisie, puis sélectionnez **([!UICONTROL Connect to source])**.

![Nouvelle interface de compte pour connecter AWS Redshift à Experience Platform sur Azure.](../../../../images/tutorials/create/redshift/new.png)

| Informations d’identification | Description |
| --- | --- |
| Serveur | Nom du serveur de votre instance [!DNL AWS Redshift]. |
| Port | Port TCP utilisé par un serveur [!DNL AWS Redshift] pour écouter les connexions client. |
| Nom d’utilisateur | Nom d’utilisateur du compte auquel vous souhaitez donner accès. |
| Mot de passe | Mot de passe correspondant au compte utilisateur. |
| Base de données | Base de données [!DNL AWS Redshift] à partir de laquelle les données doivent être récupérées. |

Pour plus d’informations sur la prise en main, consultez [ce [!DNL AWS Redshift] document](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html).

### Connexion à Experience Platform sur AWS {#aws}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur AWS Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../../../landing/multi-cloud.md).

Pour créer un compte [!DNL AWS Redshift] et vous connecter à Experience Platform sur AWS, vérifiez que vous êtes dans un sandbox VA6, fournissez les informations d’identification nécessaires pour l’authentification, puis sélectionnez **[!UICONTROL Connect to source]**.

![Nouvelle interface de compte pour connecter AWS Redshift à Experience Platform sur AWS.](../../../../images/tutorials/create/redshift/aws-auth.png)

| Informations d’identification | Description |
| --- | --- |
| Serveur | Nom du serveur de votre instance [!DNL AWS Redshift]. |
| Port | Port TCP utilisé par un serveur [!DNL AWS Redshift] pour écouter les connexions client. |
| Nom d’utilisateur | Nom d’utilisateur du compte auquel vous souhaitez donner accès. |
| Mot de passe | Mot de passe correspondant au compte utilisateur. |
| Base de données | Base de données [!DNL AWS Redshift] à partir de laquelle les données doivent être récupérées. |
| Schéma | Nom du schéma associé à votre base de données [!DNL AWS Redshift]. Vous devez vous assurer que l’utilisateur auquel vous souhaitez accorder l’accès à la base de données a également accès à ce schéma. |

Pour plus d’informations sur la prise en main, consultez [ce [!DNL AWS Redshift] document](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html).

## Étapes suivantes

Ce tutoriel vous a permis d’établir une connexion entre votre base de données [!DNL AWS Redshift] et Experience Platform. Vous pouvez maintenant passer au tutoriel suivant et [créer un flux de données pour ingérer des données de votre base de données vers Experience Platform](../../dataflow/databases.md).