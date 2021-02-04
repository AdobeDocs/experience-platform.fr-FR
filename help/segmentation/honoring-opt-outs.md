---
keywords: Experience Platform ; accueil ; rubriques populaires ; exclusion ; Segmentation ; service de segmentation ; service de segmentation ; exclusions d’abonnement ; opt-out ; exclusions ;
solution: Experience Platform
title: Respect du droit d’opposition
topic: overview
description: 'Experience Platform permet à vos clients d’envoyer des demandes d’opposition concernant l’utilisation et le stockage de leurs données au sein de Real-time Customer Profile]. Ces demandes d’opposition entrent dans le cadre du California Consumer Privacy Act (CCPA) qui donne aux personnes résidant en Californie le droit d’accéder à leurs données personnelles et de les supprimer, mais aussi de savoir si celles-ci sont vendues ou divulguées (et si oui, à qui). '
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 66%

---


# Respect des demandes d’opposition dans les segments

[!DNL Experience Platform] permet à vos clients d’envoyer des demandes d’exclusion concernant l’utilisation et l’enregistrement de leurs données dans  [!DNL Real-time Customer Profile]. Ces demandes d&#39;exclusion font partie de l&#39;[!DNL California Consumer Privacy Act] (CCPA), qui donne aux résidents de Californie le droit d&#39;accéder et de supprimer leurs données personnelles et de savoir si leurs données personnelles sont vendues ou divulguées (et à qui).

Lorsqu’un client fait valoir son droit d’opposition, il est important que votre organisation respecte ce droit lorsqu’elle génère des audiences à des fins marketing. Ce document décrit des détails importants concernant le respect des demandes d’opposition.

## Prise en main

Le respect des demandes d&#39;exclusion nécessite une compréhension des différents services [!DNL Adobe Experience Platform] impliqués. Avant de travailler sur les demandes d’opposition, consultez la documentation des services suivants :

- [[!DNL Real-time Customer Profile]](../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Permet de créer des segments d’audience à partir de  [!DNL Real-time Customer Profile] données.
- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.
- [[!DNL Adobe Experience Platform Privacy Service]](../privacy-service/home.md): Aide les entreprises à automatiser la conformité aux règles de confidentialité des données impliquant les données des clients au sein  [!DNL Platform]de.

## Mixins d’exclusion

Afin d’honorer les demandes d’exclusion de l’ACCP, l’un des schémas qui fait partie du schéma d’union doit contenir les champs d’exclusion [!DNL Experience Data Model] (XDM) nécessaires. Deux mixins sont mis à votre disposition pour ajouter des champs d’opposition à un schéma. Ces deux mixins sont présentés en détail dans les sections qui suivent :

- [Confidentialité du profil](#profile-privacy) : utilisé pour capturer différents types d’opposition (générale ou ventes/partage).
- [Détails des préférences du profil](#profile-preferences-details) : utilisé pour capturer des demandes d’opposition pour des canaux XDM spécifiques.

Pour obtenir des instructions détaillées sur la manière dont ajouter un mixin au schéma, reportez-vous à la section « Ajout d’un mixin » dans la documentation XDM suivante :
- [Tutoriel sur l’API Schema Registry](../xdm/api/getting-started.md): création d’un schéma à l’aide de l’API Schema Registry.
- [Tutoriel de l’éditeur de schéma](../xdm/tutorials/create-schema-ui.md) : création d’un schéma à l’aide de l’interface utilisateur de Platform.

Voici un exemple d’image montant les mixins d’opposition ajoutés à un schéma dans l’interface utilisateur :

![](images/opt-outs/opt-out-mixins-user-interface.png)

La structure de chaque mixin, ainsi qu’une description des champs auxquels ils contribuent au schéma, est présentée plus en détail dans les sections suivantes.

### [!DNL Profile Privacy] {#profile-privacy}

Le mixin [!DNL Profile Privacy] permet de capturer deux types de demandes d’exclusion de l’ACCP de la part des clients :

1. Opposition générale
2. Opposition de vente/partage

![](images/opt-outs/profile-privacy.png)

Le mixin [!DNL Profile Privacy] contient les champs suivants :

- Oppositions de confidentialité (`privacyOptOuts`) : un tableau contenant une liste d’objets d’opposition.
- Type d’opposition (`optOutType`) : le type d’opposition. Ce champ est une énumération de deux valeurs possibles :
   - Opposition générale (`general_opt_out`)
   - Opposition du partage des ventes (`sales_sharing_opt_out`)
- Valeur d’opposition (`optOutValue`) : l’état actif de l’opposition, également connu comme étant la valeur du signal d’opposition et basé sur le type d’opposition spécifié. Ce champ est une énumération de quatre valeurs possibles :
   - Non fourni (`not_provided`) : aucune demande d’opposition n’a été fournie.
   - En attente de vérification (`pending`) : la demande d’opposition est en attente de vérification.
   - Opposition (`out`) : le client a demandé son opposition.
   - Accord préalable (`in`) : le client a donné son accord préalable.
- Date et heure de l’opposition (`timestamp`) : date et heure du signal d’opposition reçu.

Pour vue la structure complète du mixin [!DNL Profile Privacy], veuillez vous référer au [référentiel GitHub public XDM](https://github.com/adobe/xdm/blob/master/schemas/context/profile-privacy.schema.json) ou à la prévisualisation du mixin à l&#39;aide de l&#39;interface utilisateur de la plate-forme.

### [!DNL Profile Preferences Details] {#profile-preferences-details}

Le mixin [!DNL Profile Preferences Details] fournit plusieurs champs qui représentent les préférences des profils clients (format d&#39;un email, langue préférée et fuseau horaire, par exemple). L’un des champs inclus dans ce mixin, OptInOut (`optInOut`), permet de définir des valeurs d’opposition pour chaque canal individuel.

![](images/opt-outs/profile-preferences-details.png)

Le mixin [!DNL Profile Preferences Details] contient les champs suivants relatifs aux exclusions :

- OptInOut (`optInOut`) : un objet sur lequel chaque clé représente un URI valide et connu pour un canal de communication et l’état actif d’opposition pour chaque canal. Chaque canal peut avoir l’une des quatre valeurs possibles :
   - Non fourni (`not_provided`) : aucune demande d’opposition n’a été fournie pour ce canal.
   - En attente de vérification (`pending`) : la demande d’opposition pour ce canal est en attente de vérification.
   - Opposition (`out`) : le client a fait valoir son droit d’opposition pour ce canal.
   - Accord préalable (`in`) : le client a donné son accord préalable pour ce canal.
- Opposition globale (`globalOptout`) : une valeur booléenne, qui, lorsqu’elle est définie sur « true », envoie un remplacement d’opposition global pour ce profil. La valeur par défaut de champ est « false ».

L’exemple JSON ci-dessous souligne la manière dont l’objet OptInOut peut capturer plusieurs signaux d’opposition pour des canaux de communication différents :

```json
{
  "xdm:optInOut": {
    "https://ns.adobe.com/xdm/channels/email": "pending",
    "https://ns.adobe.com/xdm/channels/phone": "out",
    "https://ns.adobe.com/xdm/channels/sms": "in",
    "https://ns.adobe.com/xdm/channels/fax": "not_provided",
    "https://ns.adobe.com/xdm/channels/direct-mail": "not_provided",
    "https://ns.adobe.com/xdm/channels/apns": "not_provided",
    "xdm:globalOptout": false
  }
}
```

Pour consulter la structure complète du mixin Détails sur les préférences du profil, reportez-vous au [référentiel XDM GitHub public](https://github.com/adobe/xdm/blob/master/schemas/context/profile-preferences-details.schema.json) ou prévisualisez le mixin à l’aide de l’interface utilisateur de [!DNL Platform]

## Gestion des oppositions dans la segmentation

Afin de vous assurer que les profils marqués des indicateurs d’opposition CCPA ne sont pas inclus dans les segments, des champs spéciaux doivent être ajoutés aux segments existants ou inclus lors de la création du segment.

Les sections ci-dessous montrent comment ajouter les champs appropriés aux deux types d’indicateurs d’opposition :
1. Opposition générale
2. Opposition de vente/partage

### Opposition générale

[!DNL Segmentation] honore automatiquement tous les profils contenant l&#39;indicateur &quot;Exclusiongénérale&quot;, ce qui signifie que ces profils ne seront pas inclus par défaut dans les audiences ou exportations. Toutefois, il est recommandé d’ajouter les champs appropriés pour vous assurer que les profils d’opposition ne sont pas inclus dans les audiences et les activités marketing.

Pour ce faire, vous pouvez utiliser l’interface utilisateur en ajoutant des attributs d’**[!UICONTROL exclusion de la confidentialité]**. Dans ce cas, le segment est défini pour inclure uniquement ceux qui ont opté pour (ce qui signifie qu’ils n’ont pas d’indicateur général d’exclusion sur leur profil. Pour ce faire, il faut déclarer que &quot;[!UICONTROL Type d&#39;exclusion]&quot; est égal à &quot;[!UICONTROL Exclusion générale]&quot; et que &quot;[!UICONTROL Valeur d&#39;exclusion]&quot; est égal à &quot;[!UICONTROL Exclusion]&quot;.

![](images/opt-outs/segment-general-opt-out.png)

### Opposition de vente/partage

Si un utilisateur possède un indicateur Opposition de vente/partage sur son profil, ce profil ne doit plus être utilisé pour toute création de segments ou d’activités marketing. Pour que cet indicateur soit respecté, le &quot;[!UICONTROL Type d&#39;exclusion]&quot; doit être égal à &quot;[!UICONTROL Exclusion du partage des ventes]&quot; et la &quot;[!UICONTROL Valeur d&#39;exclusion]&quot; doit être égale à &quot;[!UICONTROL Exclusion]&quot;.

![](images/opt-outs/segment-sales-sharing-opt-out.png)

<!-- ### Overriding default exclusions

In some instances, such as building a segment of people who have opted out, it may be necessary to override the default exclusion of opted-out profiles. This override can be done via the API or in the Segment Builder user interface. -->

## Étapes suivantes

Pour plus d’informations sur la segmentation et notamment sur la manière dont travailler avec les définitions de segment et les audiences dans l’API et l’interface utilisateur, veuillez commencer par lire la [présentation de la segmentation](./home.md).

Pour en savoir plus sur la confidentialité des données dans [!DNL Platform], y compris sur la façon dont [!DNL Privacy Service] aide à faciliter la conformité automatisée aux règlements juridiques et organisationnels en matière de confidentialité, consultez la documentation sur [[!DNL Privacy Service]](../privacy-service/home.md).
