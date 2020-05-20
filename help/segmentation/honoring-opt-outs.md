---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Respect des exclusions
topic: overview
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 0%

---


# Respect des demandes d’exclusion dans les segments

Experience Platform permet à vos clients d’envoyer des demandes d’exclusion concernant l’utilisation et l’enregistrement de leurs données dans le Profil client en temps réel. Ces demandes d&#39;exclusion font partie de la California Consumer Privacy Act (CCPA), qui donne aux résidents de Californie le droit d&#39;accéder et de supprimer leurs données personnelles et de savoir si leurs données personnelles sont vendues ou divulguées (et à qui).

Une fois qu’un client s’est désabonné, il est important que votre entreprise respecte ces exclusions lors de la génération d’audiences pour les activités marketing. Ce document décrit des détails importants concernant le traitement des demandes d’exclusion.

## Prise en main

Le respect des demandes d’exclusion nécessite une bonne compréhension des différents services Adobe Experience Platform impliqués. Avant de traiter les demandes d’exclusion, consultez la documentation relative aux services suivants :

- [Profil](../profile/home.md)client en temps réel : Fournit un profil client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
- [Adobe Experience Platform Segmentation Service](./home.md): Permet de créer des segments d’audience à partir des données du Profil client en temps réel.
- [Modèle de données d’expérience (XDM)](../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.
- [Service](../privacy-service/home.md)de confidentialité d’Adobe Experience Platform : Aide les entreprises à automatiser la conformité aux règles de confidentialité des données impliquant les données client dans Platform. Ces règlements comprennent :
   - California Consumer Privacy Act (CCPA) : Droits à la confidentialité des données pour les résidents de Californie, y compris le droit d&#39;accéder et de supprimer des données personnelles et de savoir si des données personnelles sont vendues ou divulguées (et à qui).
   - Règlement général sur la protection des données : Droits à la vie privée des données pour les membres de l&#39;Union européenne, y compris le &quot;droit à l&#39;accès&quot; et le &quot;droit à l&#39;oubli&quot;.

## Mélins d’exclusion

Afin d’honorer les demandes d’exclusion de l’ACCP, l’un des schémas qui fait partie du schéma d’union doit contenir les champs d’exclusion du modèle de données d’expérience (XDM) nécessaires. Deux mixins peuvent être utilisés pour ajouter des champs d’exclusion à un schéma. Chacun d’eux est traité plus en détail dans les sections suivantes :

- [Confidentialité](#profile-privacy)du Profil : Utilisé pour capturer différents types d’exclusion (généraux ou ventes/partage).
- [Détails](#profile-preferences-details)des préférences de Profil : Utilisé pour capturer des demandes d’exclusion pour des canaux XDM spécifiques.

Pour obtenir des instructions détaillées sur la façon d’ajouter un mixin à un schéma, reportez-vous à la section &quot;Ajouter un mixin&quot; de la documentation XDM suivante :
- [Didacticiel](../xdm/api/getting-started.md)sur l’API de registre de Schéma.: Création d’un schéma à l’aide de l’API de registre du Schéma.
- [Didacticiel](../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Création d’un schéma à l’aide de l’interface utilisateur de la plateforme.

Voici un exemple d’image présentant les mixins d’exclusion ajoutés à un schéma dans l’interface utilisateur :

![](images/opt-outs/opt-out-mixins-user-interface.png)

La structure de chaque mixin, ainsi qu&#39;une description des champs qu&#39;ils contribuent au schéma, sont décrits plus en détail dans les sections suivantes.

### Confidentialité du Profil

Le mixin Confidentialité Profil vous permet de capturer deux types de demandes d’exclusion CCPA de la part de clients :

1. Exclusion générale
2. Exclusion de vente/partage

![](images/opt-outs/profile-privacy.png)

Le mixin Confidentialité des Profils contient les champs suivants :

- Exclusions de confidentialité (`privacyOptOuts`) : Tableau contenant une liste d’objets d’exclusion.
- Type d’exclusion (`optOutType`) : Type d’exclusion. Ce champ est un enum avec deux valeurs possibles :
   - Exclusion générale (`general_opt_out`)
   - Exclusion du partage des ventes (`sales_sharing_opt_out`)
- Valeur d’exclusion (`optOutValue`) : État actif de l’exclusion, également appelé valeur du signal d’exclusion, en fonction du type d’exclusion spécifié. Ce champ est un enum avec quatre valeurs possibles :
   - Non fourni (`not_provided`) : Aucune demande d’exclusion n’a été fournie.
   - Vérification en attente (`pending`) : La demande d’exclusion est en attente de vérification.
   - Exclusion (`out`) : Le client s&#39;est désabonné.
   - Inscription (`in`) : Le client a opté pour.
- Horodatage d’exclusion (`timestamp`) : Horodatage du signal d’exclusion reçu.

Pour vue la structure complète du mixin Confidentialité du Profil, veuillez vous référer au référentiel [GitHub public](https://github.com/adobe/xdm/blob/master/schemas/context/profile-privacy.schema.json) XDM ou à la prévisualisation du mixin à l&#39;aide de l&#39;interface utilisateur de la plate-forme.

### Détails des préférences de Profil

Le mixin Détails des préférences de Profil fournit plusieurs champs qui représentent les préférences des profils clients (par exemple, format d&#39;un email, langue préférée et fuseau horaire). L’un des champs inclus dans ce mixin, OptInOut (`optInOut`), permet de définir des valeurs d’exclusion pour des canaux individuels.

![](images/opt-outs/profile-preferences-details.png)

Le mixin Détails des préférences de Profil contient les champs suivants relatifs aux exclusions :

- OptInOut (`optInOut`) : Objet dans lequel chaque clé représente un URI valide et connu pour un canal de communication et l’état actif de l’exclusion pour chaque canal. Chaque canal peut avoir l’une des quatre valeurs possibles :
   - Non fourni (`not_provided`) : Aucune demande d’exclusion n’a été fournie pour ce canal.
   - Vérification en attente (`pending`) : La demande d’exclusion pour ce canal est en attente de vérification.
   - Exclusion (`out`) : Le client s&#39;est retiré de ce canal.
   - Inscription (`in`) : Le client a opté pour ce canal.
- Exclusion globale (`globalOptout`) : Valeur booléenne qui, lorsqu’elle est définie sur true, définit un remplacement d’exclusion global pour le profil. La valeur par défaut de ce champ est false.

L’exemple JSON ci-dessous illustre comment l’objet OptInOut peut capturer plusieurs signaux d’exclusion pour différents canaux de communication :

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

Pour vue la structure complète du mixin Détails des préférences de Profil, veuillez visiter le référentiel [GitHub public](https://github.com/adobe/xdm/blob/master/schemas/context/profile-preferences-details.schema.json) XDM ou prévisualisation du mixin à l&#39;aide de l&#39;interface utilisateur de la plate-forme.

## Gestion des exclusions dans la segmentation

Afin de s’assurer que les profils marqués avec des indicateurs d’exclusion CCPA ne sont pas inclus dans les segments, des champs spéciaux doivent être ajoutés aux segments existants ou inclus lors de la création de segments.

Les sections ci-dessous montrent comment ajouter les champs appropriés pour les deux types d’indicateurs d’exclusion :
1. Exclusion générale
2. Exclusion de vente/partage

### Exclusion générale

La segmentation respecte automatiquement tous les profils contenant l’indicateur &quot;Exclusion générale&quot;, ce qui signifie que ces profils ne seront pas inclus par défaut dans les audiences ou les exportations. Toutefois, il est recommandé d’ajouter les champs appropriés pour s’assurer que les profils désactivés ne sont pas inclus dans les audiences et les activités marketing.

Pour ce faire, vous pouvez utiliser l’interface utilisateur du créateur de segments en ajoutant des attributs d’exclusion **de la** confidentialité. Dans ce cas, le segment est défini pour inclure uniquement les personnes qui ont opté pour l’exclusion (ce qui signifie qu’elles n’ont pas d’indicateur général d’exclusion sur leur profil. Pour ce faire, il faut déclarer que le &quot;Type d’exclusion&quot; est égal à &quot;Exclusion générale&quot; et que la &quot;Valeur d’exclusion&quot; est égale à &quot;Exclusion&quot;.

![](images/opt-outs/segment-general-opt-out.png)

### Exclusion de vente/partage

Si un indicateur d’exclusion de vente/partage est défini sur leur profil pour un utilisateur, ce profil ne doit plus être utilisé pour la création de segments ou les activités marketing. Pour s&#39;assurer que cet indicateur est respecté, le &quot;Type d&#39;exclusion&quot; doit être égal à &quot;Exclusion du partage des ventes&quot; et la &quot;Valeur d&#39;exclusion&quot; doit être égale à &quot;Exclusion&quot;.

![](images/opt-outs/segment-sales-sharing-opt-out.png)

<!-- ### Overriding default exclusions

In some instances, such as building a segment of people who have opted out, it may be necessary to override the default exclusion of opted-out profiles. This override can be done via the API or in the Segment Builder user interface. -->

## Étapes suivantes

Pour plus d’informations sur la segmentation, y compris l’utilisation de définitions et d’audiences de segment via l’API et l’interface utilisateur, veuillez commencer par lire la présentation [de la](./home.md)segmentation.

Pour en savoir plus sur la confidentialité des données au sein de Platform, y compris sur la façon dont Privacy Service aide à faciliter la conformité automatisée aux réglementations légales et organisationnelles en matière de confidentialité, consultez la documentation [](../privacy-service/home.md)Privacy Service.
