---
keywords: Experience Platform ; accueil ; IAB ; IAB 2.0 ; consentement ; consentement
solution: Experience Platform
title: Création de jeux de données pour la capture de données de consentement IAB TCF 2.0
topic-legacy: privacy events
description: Ce document décrit les étapes à suivre pour configurer les deux jeux de données nécessaires à la collecte des données de consentement IAB TCF 2.0.
exl-id: 36b2924d-7893-4c55-bc33-2c0234f1120e
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 4%

---

# Créer des jeux de données pour capturer les données de consentement IAB TCF 2.0

Pour que Adobe Experience Platform puisse traiter les données de consentement des clients conformément à l&#39;IAB [!DNL Transparency & Consent Framework] (TCF) 2.0, ces données doivent être envoyées à des jeux de données dont les schémas contiennent des champs de consentement TCF 2.0.

Plus précisément, deux jeux de données sont nécessaires pour capturer les données de consentement TCF 2.0 :

* Jeu de données basé sur la classe [!DNL XDM Individual Profile], activé pour une utilisation dans [!DNL Real-time Customer Profile].
* Jeu de données basé sur la classe [!DNL XDM ExperienceEvent].

Ce document décrit les étapes à suivre pour configurer ces deux ensembles de données afin de collecter les données de consentement IAB TCF 2.0. Pour un aperçu du flux de travail complet de configuration des opérations de données de votre plateforme pour TCF 2.0, consultez la [présentation de la conformité à la norme TCF 2.0 de l&#39;IAB ](./overview.md).

## Conditions préalables  

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Modèle de données d’expérience (XDM)](../../../../xdm/home.md)[!DNL Experience Platform] : cadre normalisé selon lequel Experience organise les données d’expérience client.
   * [Notions de base de la composition du schéma](../../../../xdm/schema/composition.md) : en savoir plus sur les blocs de création de base des schémas XDM.
* [Service](../../../../identity-service/home.md) d&#39;identité Adobe Experience Platform : Vous permet de relier les identités des clients à partir de vos sources de données disparates entre différents périphériques et systèmes.
   * [Espaces de nommage](../../../../identity-service/namespaces.md) d&#39;identité : Les données d&#39;identité du client doivent être fournies sous un espace de nommage d&#39;identité spécifique reconnu par Identity Service.
* [Profil](../../../../profile/home.md) client en temps réel : Exploite  [!DNL Identity Service] cette fonction pour vous permettre de créer des profils clients détaillés à partir de vos jeux de données en temps réel. [!DNL Real-time Customer Profile] Profile extrait les données du lac de données et conserve les profils clients dans sa propre banque de données distincte.

## [!UICONTROL Structure du groupe ] Détails de la confidentialité  {#structure}

Le groupe de champs [!UICONTROL Détails de la confidentialité] schéma fournit les champs de consentement client requis pour la prise en charge de TCF 2.0. Il existe deux versions de ce groupe de champs : l&#39;une est compatible avec la classe [!DNL XDM Individual Profile] et l&#39;autre avec la classe [!DNL XDM ExperienceEvent].

Les sections ci-dessous expliquent la structure de chacun de ces groupes de champs, y compris les données attendues lors de l&#39;assimilation.

### Groupe de champs de profil {#profile-field-group}

Pour les schémas basés sur [!DNL XDM Individual Profile], le groupe de champs [!UICONTROL Détails de la confidentialité] fournit un champ de type de carte unique, `xdm:identityPrivacyInfo`, qui mappe les identités des clients à leurs préférences de consentement TCF. Le fichier JSON suivant est un exemple du type de données `xdm:identityPrivacyInfo` attendu lors de l’assimilation des données :

```json
{
  "xdm:identityPrivacyInfo": {
      "ECID": {
        "13782522493631189": {
          "xdm:identityIABConsent": {
            "xdm:consentTimestamp": "2020-04-11T05:05:05Z",
            "xdm:consentString": {
              "xdm:consentStandard": "IAB TCF",
              "xdm:consentStandardVersion": "2.0",
              "xdm:consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
              "xdm:gdprApplies": true,
              "xdm:containsPersonalData": false
            }
          }
        }
      }
    }
}
```

Comme le montre l&#39;exemple, chaque clé de niveau racine de `xdm:identityPrivacyInfo` correspond à un espace de nommage d&#39;identité reconnu par Identity Service. En retour, chaque propriété d&#39;espace de nommage doit comporter au moins une sous-propriété dont la clé correspond à la valeur d&#39;identité correspondante du client pour cet espace de nommage. Dans cet exemple, le client est identifié avec un ID d’Experience Cloud (`ECID`) de la valeur `13782522493631189`.

>[!NOTE]
>
>Bien que l&#39;exemple ci-dessus utilise une paire espace de nommage/valeur unique pour représenter l&#39;identité du client, vous pouvez ajouter des clés supplémentaires pour d&#39;autres espaces de nommage et chaque espace de nommage peut avoir plusieurs valeurs d&#39;identité, chacune avec son propre jeu de préférences de consentement TCF.

L&#39;objet de valeur d&#39;identité contient un seul champ, `xdm:identityIABConsent`. Cet objet capture les valeurs de consentement TCF du client pour l&#39;espace de nommage et la valeur d&#39;identité spécifiés. Les sous-propriétés contenues dans ce champ sont répertoriées ci-dessous :

| Propriété | Description |
| --- | --- |
| `xdm:consentTimestamp` | Un horodatage [ISO 8601](https://www.ietf.org/rfc/rfc3339.txt) de la modification des valeurs de consentement TCF. |
| `xdm:consentString` | Objet contenant les données de consentement mises à jour du client et d’autres informations contextuelles. Pour en savoir plus sur les sous-propriétés requises de cet objet, consultez la section [propriétés de chaîne de consentement](#consent-string). |

### Groupe de champs de événement {#event-field-group}

Pour les schémas basés sur [!DNL XDM ExperienceEvent], le groupe de champs [!UICONTROL Détails de confidentialité] fournit un champ de type tableau unique : `xdm:consentStrings`. Chaque élément de ce tableau doit être un objet qui contient les propriétés nécessaires pour une chaîne de consentement TCF, similaire au champ `xdm:consentString` du groupe de champs de profil. Pour plus d’informations sur ces sous-propriétés, voir la section [suivante](#consent-string).

```json
{
  "xdm:consentStrings": [
    {
      "xdm:consentStandard": "IAB TCF",
      "xdm:consentStandardVersion": "2.0",
      "xdm:consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
      "xdm:gdprApplies": true,
      "xdm:containsPersonalData": false
    }
  ]
}
```

### Propriétés de chaîne de consentement {#consent-string}

Les deux versions du groupe de champs [!UICONTROL Détails de la confidentialité] nécessitent au moins un objet qui capture les champs nécessaires qui décrivent la chaîne de consentement TCF pour le client. Ces propriétés sont expliquées ci-dessous :

| Propriété | Description |
| --- | --- |
| `xdm:consentStandard` | Cadre de consentement auquel s’appliquent les données. Pour la conformité TCF, la valeur doit être `IAB TCF`. |
| `xdm:consentStandardVersion` | Numéro de version du cadre de consentement indiqué par `xdm:consentStandard`. Pour la conformité à la norme TCF 2.0, la valeur doit être `2.0`. |
| `xdm:consentStringValue` | Chaîne de consentement générée par la plateforme de gestion des autorisations (CMP) en fonction des paramètres sélectionnés par le client. |
| `xdm:gdprApplies` | Valeur booléenne indiquant si le RGPD s’applique ou non à ce client. La valeur doit être définie sur `true` pour que l’application de TCF 2.0 se produise. La valeur par défaut est `true` si elle n’est pas incluse. |
| `xdm:containsPersonalData` | Valeur booléenne indiquant si la mise à jour du consentement contient ou non des données personnelles. La valeur par défaut est `false` si elle n’est pas incluse. |

## Créer des schémas de consentement client {#create-schemas}

Pour créer des jeux de données qui capturent les données de consentement, vous devez d&#39;abord créer des schémas XDM pour les baser sur ces jeux de données.

Dans l’interface utilisateur de la plate-forme, sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche pour ouvrir l’espace de travail [!UICONTROL Schémas]. À partir de là, suivez les étapes décrites dans les sections ci-dessous pour créer chaque schéma requis.

>[!NOTE]
>
>Si vous souhaitez utiliser des schémas XDM existants pour capturer des données de consentement, vous pouvez modifier ces schémas au lieu de les créer. Cependant, si un schéma existant a été activé pour une utilisation dans le Profil client en temps réel, son identité Principale ne peut pas être un champ directement identifiable qui est interdit d&#39;utilisation dans la publicité basée sur des intérêts, telle qu&#39;une adresse électronique. Consultez votre conseiller juridique si vous ne savez pas quels champs sont restreints.
>
>De plus, lors de la modification de schémas existants, seules des modifications (non-break) peuvent être apportées. Voir la section sur les [principes de l&#39;évolution des schémas](../../../../xdm/schema/composition.md#evolution) pour plus d&#39;informations.

### Créer un schéma de consentement basé sur les enregistrements {#profile-schema}

Dans l&#39;espace de travail **[!UICONTROL Schémas]**, sélectionnez **[!UICONTROL Créer un schéma]**, puis **[!UICONTROL Profil individuel XDM]** dans la liste déroulante.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

Le [!DNL Schema Editor] apparaît, indiquant la structure du schéma dans la trame. Utilisez le rail de droite pour fournir un nom et une description pour le schéma, puis sélectionnez **[!UICONTROL Ajouter]** sous la section **[!UICONTROL Groupes de champs]** sur le côté gauche du canevas.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-profile.png)

La boîte de dialogue **[!UICONTROL Ajouter les groupes de champs]** s&#39;affiche. À partir de là, sélectionnez **[!UICONTROL Détails de la confidentialité]** dans la liste. Vous pouvez éventuellement utiliser la barre de recherche pour restreindre les résultats afin de faciliter la localisation du groupe de champs. Une fois le groupe de champs sélectionné, sélectionnez **[!UICONTROL Ajouter les groupes de champs]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

Le canevas réapparaît, indiquant que le champ `identityPrivacyInfo` a été ajouté à la structure du schéma.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

À partir de là, répétez les étapes ci-dessus pour ajouter les groupes de champs supplémentaires suivants au schéma :

* [!UICONTROL IdentityMap]
* [!UICONTROL Zone de capture de données pour le Profil]
* [!UICONTROL Détails démographiques]
* [!UICONTROL Coordonnées personnelles]

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-all-field-groups.png)

Si vous modifiez un schéma existant qui a déjà été activé pour une utilisation dans [!DNL Real-time Customer Profile], sélectionnez **[!UICONTROL Enregistrer]** pour confirmer vos modifications avant de passer à la section [en créant un jeu de données basé sur votre schéma de consentement](#dataset). Si vous créez un nouveau schéma, suivez les étapes décrites dans la sous-section ci-dessous.

#### Activez le schéma à utiliser dans [!DNL Real-time Customer Profile]

Pour que Plateforme associe les données de consentement qu&#39;elle reçoit à des profils clients spécifiques, le schéma de consentement doit être activé pour une utilisation dans [!DNL Real-time Customer Profile].

>[!NOTE]
>
>L&#39;exemple de schéma illustré dans cette section utilise son champ `identityMap` comme Principale identité. Si vous souhaitez définir un autre champ en tant qu’identité Principale, veillez à utiliser un identifiant indirect, tel qu’un identifiant de cookie, et non un champ directement identifiable qui est interdit d’utilisation dans les publicités basées sur des intérêts, comme une adresse électronique. Consultez votre conseiller juridique si vous ne savez pas quels champs sont restreints.
>
>Pour savoir comment définir un champ d&#39;identité Principal pour un schéma, consultez le [didacticiel de création de schéma](../../../../xdm/tutorials/create-schema-ui.md#identity-field).

Pour activer le schéma pour [!DNL Profile], sélectionnez le nom du schéma dans le rail de gauche pour ouvrir la boîte de dialogue **[!UICONTROL propriétés du Schéma]** dans le rail de droite. À partir de là, sélectionnez le bouton bascule **[!UICONTROL Profil]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

Une fenêtre contextuelle s’affiche, indiquant une identité Principale manquante. Cochez la case pour utiliser une autre identité Principale, car l&#39;identité Principale sera contenue dans le champ `identityMap`.

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

Enfin, sélectionnez **[!UICONTROL Enregistrer]** pour confirmer vos modifications.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### Créer un schéma de consentement basé sur une série chronologique {#event-schema}

Dans l&#39;espace de travail **[!UICONTROL Schémas]**, sélectionnez **[!UICONTROL Créer un schéma]**, puis **[!UICONTROL XDM ExperienceEvent]** dans la liste déroulante.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

Le [!DNL Schema Editor] apparaît, indiquant la structure du schéma dans la trame. Utilisez le rail de droite pour fournir un nom et une description pour le schéma, puis sélectionnez **[!UICONTROL Ajouter]** sous la section **[!UICONTROL Groupes de champs]** sur le côté gauche du canevas.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-event.png)

La boîte de dialogue **[!UICONTROL Ajouter les groupes de champs]** s&#39;affiche. À partir de là, sélectionnez **[!UICONTROL Détails de la confidentialité]** dans la liste. Vous pouvez éventuellement utiliser la barre de recherche pour restreindre les résultats afin de faciliter la localisation du groupe de champs. Une fois que vous avez choisi un groupe de champs, sélectionnez **[!UICONTROL Ajouter des groupes de champs]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

Le canevas réapparaît, indiquant que le tableau `consentStrings` a été ajouté à la structure du schéma.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

À partir de là, répétez les étapes ci-dessus pour ajouter les groupes de champs supplémentaires suivants au schéma :

* [!UICONTROL IdentityMap]
* [!UICONTROL Détails de l&#39;Environnement]
* [!UICONTROL Détails Web]
* [!UICONTROL Détails de mise en œuvre]

Une fois les groupes de champs ajoutés, terminez en sélectionnant **[!UICONTROL Enregistrer]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-field-groups.png)

## Créer des jeux de données basés sur vos schémas de consentement {#datasets}

Pour chacun des schémas requis décrits ci-dessus, vous devez créer un jeu de données qui, en fin de compte, assimilera les données de consentement de vos clients. Le jeu de données basé sur le schéma d&#39;enregistrement doit être activé pour [!DNL Real-time Customer Profile], tandis que le jeu de données basé sur le schéma de série chronologique **ne doit pas être** activé [!DNL Profile].

Pour commencer, sélectionnez **[!UICONTROL Datasets]** dans le volet de navigation de gauche, puis **[!UICONTROL Créer un dataset]** dans le coin supérieur droit.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create.png)

Sur la page suivante, sélectionnez **[!UICONTROL Créer un jeu de données à partir du schéma]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create-from-schema.png)

Le workflow **[!UICONTROL Créer un jeu de données à partir du schéma]** s&#39;affiche, en commençant à l&#39;étape **[!UICONTROL Sélectionner le schéma]**. Dans la liste fournie, recherchez l’un des schémas de consentement que vous avez créés précédemment. Vous pouvez également utiliser la barre de recherche pour restreindre les résultats et faciliter la localisation de votre schéma. Sélectionnez le bouton radio en regard du schéma souhaité, puis **[!UICONTROL Suivant]** pour continuer.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-select-schema.png)

L’étape **[!UICONTROL Configurer le jeu de données]** apparaît. Fournissez un nom et une description uniques et facilement identifiables pour le jeu de données avant de sélectionner **[!UICONTROL Terminer]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-configure.png)

La page de détails du jeu de données nouvellement créé s&#39;affiche. Si le jeu de données est basé sur votre schéma de série chronologique, le processus est terminé. Si le jeu de données est basé sur votre schéma d&#39;enregistrement, la dernière étape du processus consiste à activer le jeu de données pour l&#39;utiliser dans [!DNL Real-time Customer Profile].

Dans le rail de droite, sélectionnez la bascule **[!UICONTROL Profil]**, puis **[!UICONTROL Activer]** dans la fenêtre contextuelle de confirmation pour activer le schéma pour [!DNL Profile].

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

Suivez à nouveau les étapes ci-dessus pour créer un autre jeu de données requis pour la conformité à la norme TCF 2.0.

## Étapes suivantes

En suivant ce didacticiel, vous avez créé deux jeux de données qui peuvent maintenant être utilisés pour collecter les données de consentement des clients :

* Jeu de données basé sur des enregistrements qui peut être utilisé dans le Profil client en temps réel.
* Jeu de données basé sur les séries chronologiques qui n&#39;est pas activé pour [!DNL Profile].

Vous pouvez maintenant revenir à l&#39;[aperçu de l&#39;IAB TCF 2.0](./overview.md#merge-policies) pour poursuivre le processus de configuration de la conformité de Platform pour TCF 2.0.
