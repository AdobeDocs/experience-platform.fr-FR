---
keywords: linkedin connection;linkedin connection;linkedin destinations;linkedin;
title: Connexion d’Audience mise en correspondance LinkedIn
description: Activez des profils pour vos campagnes LinkedIn pour le ciblage, la personnalisation et la suppression des audiences, en fonction des courriers électroniques hachés.
translation-type: tm+mt
source-git-commit: d51de1ab4b2d4e91232166657466e597093f22ef
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 4%

---


# [!DNL LinkedIn Matched Audience] connexion

Activez des profils pour vos campagnes [!DNL LinkedIn] pour le ciblage, la personnalisation et la suppression des audiences, en fonction des courriers électroniques hachés et des identifiants mobiles.

![Destination LinkedIn dans l’interface utilisateur Adobe Experience Platform](../../assets/catalog/social/linkedin/catalog.png)

## Cas d’utilisation

Pour vous aider à mieux comprendre comment et quand utiliser la destination [!DNL LinkedIn Matched Audience], voici un cas d&#39;utilisation que les clients de Adobe Experience Platform peuvent résoudre en utilisant cette fonctionnalité.

Une société logicielle organise une conférence et veut garder le contact avec les participants et leur montrer des offres personnalisées en fonction de leur statut de présence à la conférence. La société peut assimiler des adresses électroniques ou des identifiants de périphérique mobile de leur propre [!DNL CRM] à Adobe Experience Platform, créer des segments à partir de leurs propres données hors ligne et envoyer ces segments à la plateforme sociale [!DNL LinkedIn], optimisant ainsi leurs dépenses publicitaires.

## Caractéristiques de la destination {#destination-specs}

[!DNL LinkedIn Matched Audience] prend en charge l’activation des identités suivantes : courriers électroniques hachés,  [!DNL GAID]et  [!DNL IDFA].

### Type d&#39;exportation {#export-type}

**Exportation**  de segment : vous exportez tous les membres d’un segment (audience) avec les identifiants (nom, numéro de téléphone, etc.) utilisé dans la destination [!DNL LinkedIn Matched Audience].

### Conditions préalables du compte LinkedIn {#LinkedIn-account-prerequisites}

Avant d’utiliser la destination [!UICONTROL Audience à correspondance LinkedIn], assurez-vous que votre compte [!DNL LinkedIn Campaign Manager] a le niveau d’autorisation [!DNL Creative Manager] ou supérieur.

Pour savoir comment modifier vos [!DNL LinkedIn Campaign Manager] autorisations d’utilisateur, voir [Ajouter, modifier et supprimer des autorisations d’utilisateur sur des comptes de publicité](https://www.linkedin.com/help/lms/answer/5753) dans la documentation LinkedIn.

### Exigences de correspondance d&#39;ID {#id-matching-requirements}

[!DNL LinkedIn Matched Audience] exige qu’aucune information d’identification personnelle (identification personnelle) ne soit envoyée en clair. Par conséquent, les audiences activées pour [!DNL LinkedIn Matched Audience] peuvent être masquées par des identifiants *hachés*, tels que des adresses électroniques ou des identifiants de périphérique mobile.

En fonction du type d’ID que vous saisissez dans Adobe Experience Platform, vous devez respecter les exigences correspondantes.

#### Conditions requises pour le hachage des courriels {#email-hashing-requirements}

Vous pouvez choisir de hacher les adresses électroniques avant de les importer dans Adobe Experience Platform, ou vous pouvez choisir de travailler avec les adresses électroniques en clair dans l&#39;Experience Platform et de faire en sorte que notre algorithme les hache sur l&#39;activation.

Pour en savoir plus sur l’assimilation d’adresses électroniques dans l’Experience Platform, consultez les sections [présentation de l’assimilation par lots](/help/ingestion/batch-ingestion/overview.md) et [présentation de l’assimilation en flux continu](/help/ingestion/streaming-ingestion/overview.md).

Si vous choisissez de hacher vous-même les adresses électroniques, veillez à respecter les exigences suivantes :

- Rogner tous les espaces de début et de fin de la chaîne de courriel. Par exemple : `johndoe@example.com`, et non `<space>johndoe@example.com<space>`;
- Lors du hachage des chaînes de courrier électronique, veillez à mettre la chaîne en minuscules en hachage ;
   - Exemple : `example@email.com`, et non `EXAMPLE@EMAIL.COM`;
- Assurez-vous que la chaîne hachée est en minuscules.
   - Exemple : `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, et non `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- Ne salez pas la chaîne.

>[!NOTE]
>
>Les données des espaces de nommage non hachés sont automatiquement hachées par [!DNL Platform] à l&#39;activation.
> Les données de la source d’attributs ne sont pas automatiquement hachées.
> 
> Au cours de l&#39;étape [Mappage d&#39;identité](../../ui/activate-destinations.md#identity-mapping), lorsque votre champ source contient des attributs non hachés, cochez l&#39;option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hachage automatiquement les données sur l&#39;activation.
> 
> L&#39;option **[!UICONTROL Appliquer la transformation]** s&#39;affiche uniquement lorsque vous sélectionnez des attributs comme champs source. Elle ne s’affiche pas lorsque vous choisissez des espaces de nommage.

![Transformation du mappage des identités](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Se connecter à la destination {#connect-destination}

Pour vous connecter à la destination [!DNL LinkedIn Matched Audience], voir le [Processus d’authentification des destinations de réseau social](./workflow.md).

## Activer les segments dans [!DNL LinkedIn Matched Audience] {#activate-segments}

Pour savoir comment activer des segments dans [!DNL LinkedIn Matched Audience], voir [Activer les données vers les destinations](../../ui/activate-destinations.md).

## Données exportées {#exported-data}

Une activation réussie signifie qu’une audience personnalisée [!DNL LinkedIn] serait créée par programmation dans [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). L’adhésion au segment dans l’audience est ajoutée ou supprimée selon que les utilisateurs sont qualifiés ou disqualifiés pour les segments activés.

>[!TIP]
>
>L’intégration entre Adobe Experience Platform et [!DNL LinkedIn Matched Audience] prend en charge les remplissages d’audiences historiques. Toutes les qualifications des segments historiques sont envoyées à [!DNL LinkedIn] lorsque vous activez les segments vers la destination.