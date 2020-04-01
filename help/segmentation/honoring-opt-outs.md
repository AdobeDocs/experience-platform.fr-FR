---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Respect des exclusions
topic: overview
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Traitement des demandes d’exclusion dans les segments

Experience Platform permet à vos clients d’envoyer des demandes d’exclusion concernant l’utilisation et l’  de leurs données dans le cadre de l’client en temps réel. Ces demandes d’exclusion font partie de la Loi sur la protection des renseignements personnels des consommateurs (LPCPC) de la Californie, qui accorde aux résidents de la Californie le droit d’accéder à leurs données personnelles et de les supprimer, et de savoir si leurs données personnelles sont vendues ou divulguées (et à qui).

Une fois qu’un client s’est désabonné, il est important que votre entreprise honore ces exclusions lors de la génération de   pour les de  marketing. Ce décrit des détails importants concernant le traitement des demandes d’exclusion.

## Prise en main

Le respect des demandes d’exclusion nécessite une compréhension des différents services Adobe Experience Platform impliqués. Avant de traiter les demandes d’exclusion, consultez la documentation relative aux services suivants :

- [](../profile/home.md)du client en temps réel : Fournit un client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
- [Adobe Experience Platform Segmentation Service](./home.md): Permet de créer  segments  à partir de données de client en temps réel.
- [Modèle de données d’expérience (XDM)](../xdm/home.md): Cadre normalisé selon lequel la plateforme organise les données d’expérience client.
- [Service](../privacy-service/home.md)de confidentialité d’Adobe Experience Platform : Aide les entreprises à automatiser la conformité aux réglementations de confidentialité des données impliquant les données client dans Platform. Ces règlements comprennent :
   - California Consumer Privacy Act (CCPA) : Droits à la confidentialité des données pour les résidents de Californie, y compris le droit d&#39;accéder et de supprimer des données personnelles et de savoir si des données personnelles sont vendues ou divulguées (et à qui).
   - Règlement général sur la protection des données: Les droits à la confidentialité des données pour les membres de la  européenne , y compris le &quot;droit d&#39;accès&quot; et le &quot;droit à l&#39;oubli&quot;.

## Mélins d’exclusion

Afin d’honorer les demandes d’exclusion de l’ACCP, l’un des qui fait partie de la  de l’de l’doit contenir les champs d’exclusion du modèle de données d’expérience (XDM) nécessaires. Il existe deux mixins qui peuvent être utilisés pour ajouter des champs d’exclusion à un. Chacun d’eux est traité plus en détail dans les sections suivantes :

- [Confidentialité](#profile-privacy)des  : Utilisé pour capturer différents types d’exclusion (généraux ou ventes/partage).
- [Détails](#profile-preferences-details)des préférences de  : Utilisé pour capturer des demandes d’exclusion pour des  XDM spécifiques.

Pour obtenir des instructions détaillées sur la manière d’ajouter un mixin à un, reportez-vous à la section &quot;Ajouter un mixin&quot; de la documentation XDM suivante :
- [Didacticiel](../xdm/api/getting-started.md)sur l&#39;API de registre des.: Création d’un  d’à l’aide de l’API de Registre .
- [Didacticiel](../xdm/tutorials/create-schema-ui.md)de l’éditeur de  : Création d’un  à l’aide de l’interface utilisateur de la plateforme.

Voici un exemple d’image montrant les mixins d’exclusion ajoutés à un  d’dans l’interface utilisateur :

![](images/opt-outs/opt-out-mixins-user-interface.png)

La structure de chaque mixin, ainsi qu’une description des champs qu’ils contribuent au  du, sont décrites plus en détail dans les sections suivantes.

### Confidentialité des 

Le mixin Confidentialité  vous permet de capturer deux types de demandes d’exclusion de l’ACCP de la part des clients :

1. Exclusion générale
2. Exclusion de vente/partage

![](images/opt-outs/profile-privacy.png)

Le mixin Confidentialité  contient les champs suivants :

- Exclusions de confidentialité (`privacyOptOuts`) : Tableau contenant un d’objets d’exclusion.
- Type d’exclusion (`optOutType`) : Type d’exclusion. Ce champ est un enum avec deux valeurs possibles :
   - Exclusion générale (`general_opt_out`)
   - Exclusion du partage des ventes (`sales_sharing_opt_out`)
- Valeur d’exclusion (`optOutValue`) : État actif de l’exclusion, également appelé valeur du signal d’exclusion, en fonction du type d’exclusion spécifié. Ce champ est un enum avec quatre valeurs possibles :
   - Non fourni (`not_provided`) : Aucune demande d’exclusion n’a été fournie.
   - Vérification en attente (`pending`) : La demande d’exclusion est en attente de vérification.
   - Exclusion (`out`) : Le client s&#39;est désabonné.
   - Exclusion (`in`) : Le client s&#39;est inscrit.
- Horodatage d’exclusion (`timestamp`) : Horodatage du signal d’exclusion reçu.

Pour  la structure complète du mixin de confidentialité , reportez-vous au référentiel [GitHub public](https://github.com/adobe/xdm/blob/master/schemas/context/profile-privacy.schema.json) XDM ou autableau de bord à l’aide de l’interface utilisateur de la plate-forme.

### Détails des préférences 

Le  de mixage Détails des préférences de l’fournit plusieurs champs qui représentent les préférences pour les  du client (par exemple, le , la langue préférée et le fuseau horaire). L’un des champs inclus dans ce mixin, OptInOut (`optInOut`), permet de définir des valeurs d’exclusion pour les  individuels.

![](images/opt-outs/profile-preferences-details.png)

Le mixage Détails des préférences de l’ contient les champs suivants relatifs aux exclusions :

- OptInOut (`optInOut`) : Objet où chaque clé représente un URI valide et connu pour un  de communication et l’état actif de l’exclusion pour chaque  de. Chaque  peut avoir l’une des quatre valeurs possibles :
   - Non fourni (`not_provided`) : Aucune demande d’exclusion n’a été fournie pour cette  de.
   - Vérification en attente (`pending`) : La demande d’exclusion pour ce est en attente de vérification.
   - Exclusion (`out`) : Le client s&#39;est désabonné de cette .
   - Exclusion (`in`) : Le client s’est connecté à ce.
- Exclusion globale (`globalOptout`) : Valeur booléenne qui, lorsqu’elle est définie sur true, définit un remplacement d’exclusion global pour le  de. La valeur par défaut de ce champ est false.

L’exemple JSON ci-dessous montre comment l’objet OptInOut peut capturer plusieurs signaux d’exclusion pour différents de communication :

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

Pour la structure complète du mixin des détails des préférences de l&#39;, veuillez visiter le référentiel [GitHub public](https://github.com/adobe/xdm/blob/master/schemas/context/profile-preferences-details.schema.json) XDM ou bien lemixin à l&#39;aide de l&#39;interface utilisateur de la plate-forme.

## Gestion des exclusions dans la segmentation

Afin de s’assurer que les  marqués avec des indicateurs d’exclusion CCPA ne sont pas inclus dans les segments, des champs spéciaux doivent être ajoutés aux segments existants ou inclus lors de la création de segments.

Les sections ci-dessous montrent comment ajouter les champs appropriés pour les deux types d’indicateurs d’exclusion :
1. Exclusion générale
2. Exclusion de vente/partage

### Exclusion générale

La segmentation respecte automatiquement tous les  contenant l’indicateur &quot;Exclusion générale&quot;, ce qui signifie que ces  de ne seront pas incluses par défaut dans leou les exportations. Toutefois, il est recommandé d’ajouter les champs appropriés afin de s’assurer que les  de désabonné ne sont pas incluses dans   et dans lede marketing.

Pour ce faire, vous pouvez utiliser l’interface utilisateur du créateur de segments en ajoutant des attributs d’exclusion **de la** confidentialité. Dans ce cas, le segment est défini de manière à inclure uniquement les personnes qui ont opté pour l’exclusion (ce qui signifie qu’elles n’ont pas d’indicateur d’exclusion général sur leur . Pour ce faire, déclarez que le &quot;Type d’exclusion&quot; est égal à &quot;Exclusion générale&quot; et que la &quot;Valeur d’exclusion&quot; est égale à &quot;Exclusion&quot;.

![](images/opt-outs/segment-general-opt-out.png)

### Exclusion de vente/partage

Si un indicateur d’exclusion de vente/partage est défini sur leur  de, ce  de ne doit plus être utilisé pour la création de segments ou le marketing del’. Pour s’assurer que cet indicateur est respecté, le &quot;Type d’exclusion&quot; doit être égal à &quot;Exclusion du partage des ventes&quot; et la &quot;Valeur d’exclusion&quot; doit être égale à &quot;Exclusion&quot;.

![](images/opt-outs/segment-sales-sharing-opt-out.png)

<!-- ### Overriding default exclusions

In some instances, such as building a segment of people who have opted out, it may be necessary to override the default exclusion of opted-out profiles. This override can be done via the API or in the Segment Builder user interface. -->

## Étapes suivantes

Pour plus d’informations sur la segmentation, y compris l’utilisation des définitions de segment et des  de  par le biais de l’API et de l’interface utilisateur, veuillez commencer par lire la présentation [de la](./home.md)segmentation.

Pour en savoir plus sur la confidentialité des données au sein de Platform, y compris sur la manière dont Privacy Service aide à faciliter la conformité automatisée aux réglementations légales et organisationnelles en matière de confidentialité, veuillez consulter la documentation [](../privacy-service/home.md)Privacy Service.
