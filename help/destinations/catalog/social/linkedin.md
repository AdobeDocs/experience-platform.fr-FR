---
keywords: linkedin connection;linkedin connection;linkedin destinations;linkedin;
title: Connexion des Audiences mises en correspondance Linkedin
description: Activez des profils pour vos campagnes LinkedIn pour le ciblage, la personnalisation et la suppression des audiences, en fonction des courriers électroniques hachés.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
translation-type: tm+mt
source-git-commit: 95ca7112d1f2655bf33e8a1c549e886ced244a5d
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 5%

---

# [!DNL LinkedIn Matched Audiences] connexion

## Présentation {#overview}

Activez des profils pour vos campagnes [!DNL LinkedIn] pour le ciblage, la personnalisation et la suppression des audiences, en fonction des courriers électroniques hachés et des identifiants mobiles.

![Destination linkedIn dans l’interface utilisateur Adobe Experience Platform](../../assets/catalog/social/linkedin/catalog.png)

## Cas d’utilisation

Pour vous aider à mieux comprendre comment et quand utiliser la destination [!DNL LinkedIn Matched Audiences], voici un cas d&#39;utilisation que les clients de Adobe Experience Platform peuvent résoudre en utilisant cette fonctionnalité.

Une société logicielle organise une conférence et veut garder le contact avec les participants et leur montrer des offres personnalisées en fonction de leur statut de présence à la conférence. La société peut assimiler des adresses électroniques ou des ID de périphérique mobile de leur propre [!DNL CRM] à Adobe Experience Platform. Ils peuvent ensuite créer des segments à partir de leurs propres données hors ligne et les envoyer vers la [!DNL LinkedIn] plate-forme sociale, en optimisant leurs dépenses publicitaires.

## Identités prises en charge {#supported-identities}

[!DNL LinkedIn Matched Audiences] prend en charge l&#39;activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/namespaces.md).

| Identité de cible | Description | Considérations |
|---|---|---|
| GAID | Identifiant Google Advertising | Sélectionnez cette identité de cible lorsque votre identité source est un espace de nommage GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez cette identité de cible lorsque votre identité source est un espace de nommage IDFA. |
| email_lc_sha256 | Adresses électroniques hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses électroniques hachées SHA256. Suivez les instructions de la section [Exigences de correspondance d&#39;ID](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de nommage appropriés pour le texte brut et les courriers électroniques hachés, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hachage automatiquement les données sur l’activation. |


## Type d&#39;exportation {#export-type}

**Exportation**  de segment : vous exportez tous les membres d’un segment (audience) avec les identifiants (nom, numéro de téléphone et autres) utilisés dans la  [!DNL LinkedIn Matched Audiences] destination.

## Configuration requise pour le compte linkedIn {#LinkedIn-account-prerequisites}

Avant d’utiliser la destination [!UICONTROL Audience LinkedIn Matched], assurez-vous que votre compte [!DNL LinkedIn Campaign Manager] a le niveau d’autorisation [!DNL Creative Manager] ou supérieur.

Pour savoir comment modifier vos [!DNL LinkedIn Campaign Manager] autorisations d&#39;utilisateur, voir [Ajouter, modifier et supprimer des autorisations d&#39;utilisateur sur des comptes de publicité](https://www.linkedin.com/help/lms/answer/5753) dans la documentation LinkedIn.

## Exigences de correspondance d&#39;ID {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] exige qu’aucune information d’identification personnelle (identification personnelle) ne soit envoyée en clair. Par conséquent, les audiences activées pour [!DNL LinkedIn Matched Audiences] peuvent être masquées par des identifiants *hachés*, tels que des adresses électroniques ou des identifiants de périphérique mobile.

En fonction du type d’ID que vous saisissez dans Adobe Experience Platform, vous devez respecter les exigences correspondantes.

## Conditions requises pour le hachage des courriels {#email-hashing-requirements}

Vous pouvez hacher des adresses électroniques avant de les importer dans Adobe Experience Platform ou utiliser des adresses électroniques en clair dans l’Experience Platform et les faire [!DNL Platform] hacher sur l’activation.

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

Pour vous connecter à la destination [!DNL LinkedIn Matched Audiences], voir le [Processus d’authentification des destinations de réseau social](./workflow.md).

La vidéo ci-dessous présente également les étapes de configuration d&#39;une destination [!DNL LinkedIn Matched Audiences] et d&#39;activation de segments.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## Activer les segments dans [!DNL LinkedIn Matched Audiences] {#activate-segments}

Pour savoir comment activer des segments dans [!DNL LinkedIn Matched Audiences], voir [Activer les données vers les destinations](../../ui/activate-destinations.md).

## Données exportées {#exported-data}

Une activation réussie signifie qu’une audience personnalisée [!DNL LinkedIn] serait créée par programmation dans [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). L’adhésion au segment dans l’audience est ajoutée ou supprimée selon que les utilisateurs sont qualifiés ou disqualifiés pour les segments activés.

>[!TIP]
>
>L’intégration entre Adobe Experience Platform et [!DNL LinkedIn Matched Audiences] prend en charge les remplissages d’audiences historiques. Toutes les qualifications des segments historiques sont envoyées à [!DNL LinkedIn] lorsque vous activez les segments vers la destination.
