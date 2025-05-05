---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Configuration d’un jeu de données pour capturer les données de consentement et de préférence
description: Découvrez comment configurer un schéma et un jeu de données de modèle de données d’expérience (XDM) pour capturer les données de consentement et de préférence dans Adobe Experience Platform.
role: Developer
feature: Consent, Schemas, Datasets
exl-id: 61ceaa2a-c5ac-43f5-b118-502bdc432234
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 4%

---

# Configuration d’un jeu de données pour capturer les données de consentement et de préférence

Pour que Adobe Experience Platform puisse traiter vos données de consentement/préférence client, ces données doivent être envoyées à un jeu de données dont le schéma contient des champs liés aux consentements et à d’autres autorisations. Plus précisément, ce jeu de données doit être basé sur la classe [!DNL XDM Individual Profile] et activé pour une utilisation dans [!DNL Real-Time Customer Profile].

Ce document décrit les étapes de configuration d’un jeu de données pour traiter les données de consentement dans Experience Platform. Pour une présentation complète du workflow de traitement des données de consentement/préférence dans Experience Platform, reportez-vous à la section [présentation du traitement du consentement](./overview.md).

>[!IMPORTANT]
>
>Les exemples de ce guide utilisent un ensemble normalisé de champs pour représenter les valeurs de consentement du client, telles que définies par le groupe de champs de schéma [[!UICONTROL &#x200B; Détails du consentement et des préférences &#x200B;]](../../../../xdm/field-groups/profile/consents.md). La structure de ces champs est destinée à fournir un modèle de données efficace pour couvrir de nombreux cas d’utilisation courants de la collecte de consentement.
>
>Cependant, vous pouvez également définir vos propres groupes de champs pour représenter le consentement en fonction de vos propres modèles de données. Consultez votre équipe juridique pour obtenir l’approbation d’un modèle de données de consentement adapté aux besoins de votre entreprise, en fonction des options suivantes :
>
>* Groupe de champs de consentement normalisé
>* Un groupe de champs de consentement personnalisé créé par votre organisation
>* Combinaison du groupe de champs de consentement normalisé et des champs supplémentaires fournis par un groupe de champs de consentement personnalisé

## Conditions préalables

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Modèle de données d’expérience (XDM)](../../../../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données d’expérience client.
   * [Notions de base de la composition du schéma](../../../../xdm/schema/composition.md) : en savoir plus sur les blocs de création de base des schémas XDM.
* [Real-Time Customer Profile](../../../../profile/home.md) : consolide les données client provenant de sources disparates en une vue complète et unifiée tout en offrant un compte horodaté et exploitable de chaque interaction client.

>[!IMPORTANT]
>
>Ce tutoriel suppose que vous connaissez le schéma de [!DNL Profile] dans Experience Platform que vous souhaitez utiliser pour capturer les informations d’attributs du client. Quelle que soit la méthode que vous utilisez pour collecter les données de consentement, ce schéma doit être [activé pour le profil client en temps réel](../../../../xdm/ui/resources/schemas.md#profile). En outre, l’identité principale du schéma ne peut pas être un champ directement identifiable qui est interdit d’utilisation dans la publicité en fonction des intérêts, telle qu’une adresse e-mail. Consultez votre service juridique si vous n’êtes pas sûr des champs restreints.

## Structure du groupe de champs [!UICONTROL Détails du consentement et des préférences] {#structure}

Le groupe de champs [!UICONTROL &#x200B; Détails du consentement et des préférences &#x200B;] fournit des champs de consentement normalisés à un schéma. Actuellement, ce groupe de champs n’est compatible qu’avec les schémas basés sur la classe [!DNL XDM Individual Profile].

Le groupe de champs fournit un champ de type objet unique, `consents`, dont les sous-propriétés capturent un ensemble de champs de consentement normalisés. Le fichier JSON suivant est un exemple du type de données attendu par `consents` lors de l’ingestion de données :

```json
{
  "consents": {
    "collect": {
      "val": "y",
    },
    "share": {
      "val": "y",
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "y"
      },
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
      }
    },
    "idSpecific": {
      "email": {
        "jdoe@example.com": {
          "marketing": {
            "email": {
              "val": "n"
            }
          }
        }
      }
    }
  },
  "metadata": {
    "time": "2019-01-01T15:52:25+00:00"
  }
}
```

>[!NOTE]
>
>Pour plus d’informations sur la structure et la signification des sous-propriétés dans `consents`, consultez la présentation du groupe de champs [[!UICONTROL Détails du consentement et des préférences] ](../../../../xdm/field-groups/profile/consents.md).

## Ajouter les groupes de champs obligatoires à votre schéma de [!DNL Profile] {#add-field-group}

Pour collecter des données de consentement à l’aide de la norme Adobe, vous devez disposer d’un schéma activé pour Profile contenant les deux groupes de champs suivants :

* [[!UICONTROL Détails relatifs au consentement et aux préférences]](../../../../xdm/field-groups/profile/consents.md)
* [[!UICONTROL IdentityMap]](../../../../xdm/field-groups/profile/identitymap.md) (obligatoire si vous utilisez Experience Platform Web ou Mobile SDK pour envoyer des signaux de consentement)

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Parcourir]** pour afficher la liste des schémas existants. À partir de là, sélectionnez le nom du schéma [!DNL Profile] auquel vous souhaitez ajouter des champs de consentement. Les captures d’écran de cette section utilisent le schéma « Membres du programme de fidélité » créé dans le [ tutoriel sur la création de schémas ](../../../../xdm/tutorials/create-schema-ui.md) à titre d’exemple.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-schema.png)

>[!TIP]
>
>Vous pouvez utiliser les fonctionnalités de recherche et de filtrage de l’espace de travail pour faciliter la recherche de votre schéma. Pour plus d’informations, consultez le guide sur l’[exploration des ressources XDM](../../../../xdm/ui/explore.md).

La [!DNL Schema Editor] s’affiche et indique la structure du schéma dans la zone de travail. Sur le côté gauche de la zone de travail, sélectionnez **[!UICONTROL Ajouter]** sous la section **[!UICONTROL Groupes de champs]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-field-group.png)

La boîte de dialogue **[!UICONTROL Ajouter un groupe de champs]** s’affiche. À partir de là, sélectionnez **[!UICONTROL Détails du consentement et des préférences]** dans la liste. Vous pouvez éventuellement utiliser la barre de recherche pour affiner les résultats afin de localiser plus facilement le groupe de champs.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-group-dialog.png)

Recherchez ensuite le groupe de champs **[!UICONTROL IdentityMap]** dans la liste et sélectionnez-le également. Une fois que les deux groupes de champs sont répertoriés dans le rail de droite, sélectionnez **[!UICONTROL Ajouter des groupes de champs]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/identitymap.png)

La zone de travail réapparaît, indiquant que les champs `consents` et `identityMap` ont été ajoutés à la structure du schéma. Si vous avez besoin de champs de consentement et de préférence supplémentaires, non capturés par le groupe de champs standard, reportez-vous à la section de l’annexe sur [l’ajout de champs de consentement et de préférence personnalisés au schéma](#custom-consent). Sinon, sélectionnez **[!UICONTROL Enregistrer]** pour finaliser les modifications apportées au schéma.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/save-schema.png)

>[!IMPORTANT]
>
>Si vous créez un schéma ou modifiez un schéma existant qui n’a pas été activé pour Profil, vous devez [activer le schéma pour Profil](../../../../xdm/ui/resources/schemas.md#profile) avant d’enregistrer.

Si le schéma que vous avez modifié est utilisé par le [!UICONTROL jeu de données de profil] spécifié dans votre flux de données Experience Platform Web SDK, ce jeu de données inclut désormais les nouveaux champs de consentement. Vous pouvez maintenant revenir au [guide de traitement du consentement](./overview.md#merge-policies) pour poursuivre le processus de configuration d’Experience Platform afin de traiter les données de consentement. Si vous n’avez pas créé de jeu de données pour ce schéma, suivez les étapes de la section suivante.

## Créer un jeu de données en fonction de votre schéma de consentement {#dataset}

Une fois que vous avez créé un schéma avec des champs de consentement, vous devez créer un jeu de données qui ingérera à terme les données de consentement de vos clients. Ce jeu de données doit être activé pour [!DNL Real-Time Customer Profile].

Pour commencer, sélectionnez **[!UICONTROL Jeux de données]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Créer un jeu de données]** dans le coin supérieur droit.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/create-dataset.png)

Sur la page suivante, sélectionnez **[!UICONTROL Créer un jeu de données à partir d’un schéma]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/from-schema.png)

Le workflow **[!UICONTROL Créer un jeu de données à partir d’un schéma]** s’affiche, en commençant par l’étape **[!UICONTROL Sélectionner un schéma]**. Dans la liste fournie, recherchez l’un des schémas de consentement que vous avez créés précédemment. Vous pouvez éventuellement utiliser la barre de recherche pour affiner les résultats et localiser plus facilement votre schéma. Sélectionnez le bouton radio en regard du schéma souhaité, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-dataset-schema.png)

L’étape **[!UICONTROL Configurer le jeu de données]** apparaît. Fournissez un nom et une description uniques et facilement identifiables pour le jeu de données avant de sélectionner **[!UICONTROL Terminer]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/dataset-details.png)

La page de détails du jeu de données nouvellement créé s’affiche. Si le jeu de données est basé sur votre schéma de série temporelle, le processus est terminé. Si le jeu de données est basé sur votre schéma d’enregistrement, l’étape finale du processus consiste à activer le jeu de données pour une utilisation dans [!DNL Real-Time Customer Profile].

Dans le rail de droite, sélectionnez le bouton (bascule) **[!UICONTROL Profil]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/profile-toggle.png)

Enfin, sélectionnez **[!UICONTROL Activer]** dans la fenêtre contextuelle de confirmation pour activer le schéma à [!DNL Profile].

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/enable-dataset.png)

Le jeu de données est maintenant enregistré et activé pour une utilisation dans [!DNL Profile]. Si vous prévoyez d’utiliser Experience Platform Web SDK pour envoyer des données de consentement au profil, vous devez sélectionner ce jeu de données comme [!UICONTROL jeu de données de profil] lors de la configuration de votre [flux de données](../../../../datastreams/overview.md).

## Étapes suivantes

En suivant ce tutoriel, vous avez ajouté des champs de consentement à un schéma activé pour [!DNL Profile], dont le jeu de données sera utilisé pour ingérer des données de consentement à l’aide du SDK Web Experience Platform ou de l’ingestion XDM directe.

Vous pouvez maintenant revenir à la [présentation du traitement du consentement](./overview.md#merge-policies) pour continuer à configurer Experience Platform pour traiter les données de consentement.

## Annexe

La section suivante contient des informations supplémentaires sur la création d’un jeu de données pour ingérer les données de consentement et de préférence du client.

### Ajout de champs de préférence et de consentement personnalisés au schéma {#custom-consent}

Si vous devez capturer des signaux de consentement supplémentaires en dehors de ceux représentés par le groupe de champs standard [!UICONTROL Détails du consentement et des préférences], vous pouvez utiliser des composants XDM personnalisés pour améliorer votre schéma de consentement en fonction des besoins spécifiques de votre entreprise. Cette section décrit les principes de base de la personnalisation de votre schéma de consentement afin d’ingérer ces signaux dans Profile.

>[!IMPORTANT]
>
>Les SDK web et mobile d’Experience Platform ne prennent pas en charge les champs personnalisés dans leurs commandes de modification du consentement. Actuellement, la seule façon d’ingérer des champs de consentement personnalisés dans le profil consiste à utiliser [ingestion par lots](../../../../ingestion/batch-ingestion/overview.md) ou une [connexion source](../../../../sources/home.md).

Il est vivement recommandé d’utiliser le groupe de champs [!UICONTROL Détails du consentement et des préférences] comme référence pour la structure de vos données de consentement et d’ajouter des champs supplémentaires si nécessaire, plutôt que d’essayer de créer l’ensemble de la structure à partir de zéro.

Pour ajouter des champs personnalisés à la structure d’un groupe de champs standard, vous devez d’abord créer un groupe de champs personnalisé. Après avoir ajouté le groupe de champs [!UICONTROL Détails du consentement et des préférences] au schéma, sélectionnez l’icône **plus (+)** dans la section **[!UICONTROL Groupes de champs]**, puis sélectionnez **[!UICONTROL Créer un groupe de champs]**. Attribuez un nom et une description facultative au groupe de champs, puis sélectionnez **[!UICONTROL Ajouter un groupe de champs]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field-group.png)

Le [!DNL Schema Editor] réapparaît avec le nouveau groupe de champs personnalisés sélectionné dans le rail de gauche. Dans la zone de travail, des contrôles s’affichent pour vous permettre d’ajouter des champs personnalisés à la structure du schéma. Pour ajouter un nouveau champ de consentement ou de préférence, sélectionnez l’icône **plus (+)** à côté de l’objet `consents`.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field.png)

Un nouveau champ apparaît dans l’objet `consents`. Puisque vous ajoutez un champ personnalisé à un objet XDM standard, le nouveau champ est créé sous un objet d’espace de noms associé à votre identifiant client.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/nested-tenantId.png)

Dans le rail de droite sous **[!UICONTROL Propriétés du champ]**, indiquez un nom et une description pour le champ. Lors de la sélection du **[!UICONTROL Type]** du champ, vous devez utiliser le type de données standard approprié pour un champ de préférence ou de consentement personnalisé :

* [[!UICONTROL Champ de consentement générique]](../../../../xdm/data-types/consent-field.md)
* [[!UICONTROL Champ générique de préférences marketing]](../../../../xdm/data-types/marketing-field.md)
* [[!UICONTROL Champ générique de préférences marketing avec abonnements]](../../../../xdm/data-types/marketing-field-subscriptions.md)
* [[!UICONTROL Champ de préférence Personalization générique]](../../../../xdm/data-types/personalization-field.md)

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Appliquer]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-properties.png)

Le champ de consentement ou de préférence est ajouté à la structure du schéma. Notez que le [!UICONTROL Chemin] affiché dans le rail de droite contient l’espace de noms `_tenantId`. Cet espace de noms doit être inclus chaque fois que vous référencez le chemin d’accès à ce champ dans vos opérations de données.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-added.png)

Suivez les étapes ci-dessus pour continuer à ajouter les champs de consentement et de préférence dont vous avez besoin. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]** pour confirmer vos modifications.

Si vous n’avez pas créé de jeu de données pour ce schéma, passez à la section sur la [création d’un jeu de données](#dataset).
