---
keywords: connexion linkedin;connexion linkedin;destinations linkedin;linkedin;
title: Connexion à des audiences mises en correspondance Linkedin
description: Activez les profils de vos campagnes LinkedIn pour le ciblage, la personnalisation et la suppression des audiences, en fonction des courriers électroniques hachés.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 10%

---

# Connexion [!DNL LinkedIn Matched Audiences]

## Présentation {#overview}

Activez les profils pour votre [!DNL LinkedIn] campagnes pour le ciblage, la personnalisation et la suppression des audiences, basées sur des emails hachés et des identifiants mobiles.

![Destination linkedIn dans l’interface utilisateur de Adobe Experience Platform](../../assets/catalog/social/linkedin/catalog.png)

## Cas dʼutilisation

Pour vous aider à mieux comprendre comment et à quel moment utiliser la variable [!DNL LinkedIn Matched Audiences] destination : voici un cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette fonctionnalité.

Une société de logiciels organise une conférence et souhaite rester en contact avec les participants et leur présenter des offres personnalisées en fonction de leur statut de participation à la conférence. L’entreprise peut ingérer des adresses électroniques ou des identifiants d’appareil mobile à partir de ses propres adresses. [!DNL CRM] dans Adobe Experience Platform. Ils peuvent ensuite créer des segments à partir de leurs propres données hors ligne et les envoyer à la variable [!DNL LinkedIn] plateforme sociale, optimisant leurs dépenses publicitaires.

## Identités prises en charge {#supported-identities}

[!DNL LinkedIn Matched Audiences] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur [identités](/help/identity-service/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | Google Advertising ID | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms IDFA. |
| email_lc_sha256 | Adresses électroniques hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses électroniques hachées SHA256. Suivez les instructions de la section [Exigences de correspondance des identifiants](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de noms appropriés pour le texte brut et les courriers électroniques hachés, respectivement. Lorsque votre champ source contient des attributs non hachés, vérifiez la variable **[!UICONTROL Appliquer la transformation]** option, pour avoir [!DNL Platform] hachage automatique des données lors de l’activation. |

{style=&quot;table-layout:auto&quot;}

## Type et fréquence d&#39;export {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Exportation des segments]** | Vous exportez tous les membres d’un segment (audience) avec les identifiants (nom, numéro de téléphone et autres) utilisés dans la variable [!DNL LinkedIn Matched Audiences] destination. |
| Fréquence des exports | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont &quot;toujours sur&quot; des connexions basées sur l’API. Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Conditions préalables au compte linkedIn {#LinkedIn-account-prerequisites}

Avant d’utiliser la variable [!UICONTROL Audience mise en correspondance linkedIn] destination, assurez-vous que [!DNL LinkedIn Campaign Manager] Le compte a la variable [!DNL Creative Manager] niveau d’autorisation ou supérieur.

Pour savoir comment modifier votre [!DNL LinkedIn Campaign Manager] autorisations utilisateur, voir [Ajout, modification et suppression des autorisations d’utilisateur sur les comptes Advertising](https://www.linkedin.com/help/lms/answer/5753) dans la documentation de LinkedIn.

## Exigences de correspondance des identifiants {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] exige qu’aucune information d’identification personnelle (PII) ne soit envoyée clairement. Par conséquent, les audiences sont activées vers [!DNL LinkedIn Matched Audiences] peut être désactivé *haché* identifiants, tels que les adresses électroniques ou les identifiants d’appareil mobile.

Selon le type d’ID que vous ingérez dans Adobe Experience Platform, vous devez respecter les exigences correspondantes.

## Exigences en matière de hachage des emails {#email-hashing-requirements}

Vous pouvez hacher les adresses électroniques avant de les ingérer dans Adobe Experience Platform ou utiliser les adresses électroniques en clair dans Experience Platform et disposer des [!DNL Platform] hachez-les lors de l’activation.

Pour en savoir plus sur l’ingestion d’adresses électroniques dans Experience Platform, voir [Présentation de l’ingestion par lots](/help/ingestion/batch-ingestion/overview.md) et le [présentation de l’ingestion par flux](/help/ingestion/streaming-ingestion/overview.md).

Si vous choisissez de hacher vous-même les adresses électroniques, veillez à respecter les exigences suivantes :

* Corrigez tous les espaces de début et de fin de la chaîne de courrier électronique. Par exemple : `johndoe@example.com`, not `<space>johndoe@example.com<space>`;
* Lors du hachage des chaînes d’email, veillez à mettre la chaîne en minuscules par hachage.
   * Exemple : `example@email.com`, not `EXAMPLE@EMAIL.COM`;
* Assurez-vous que la chaîne hachée est entièrement en minuscules.
   * Exemple : `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, not `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Ne salez pas la chaîne.

>[!NOTE]
>
>Les données des espaces de noms non hachés sont automatiquement hachées par [!DNL Platform] lors de l’activation.
> Les données de la source d’attributs ne sont pas automatiquement hachées.
> 
> Durant : [Mappage des identités](../../ui/activate-segment-streaming-destinations.md#mapping) lorsque votre champ source contient des attributs non hachés, vérifiez la variable **[!UICONTROL Appliquer la transformation]** option, pour avoir [!DNL Platform] hachage automatique des données lors de l’activation.
> 
> Le **[!UICONTROL Appliquer la transformation]** ne s’affiche que lorsque vous sélectionnez des attributs comme champs source. Il ne s’affiche pas lorsque vous choisissez des espaces de noms.

![Transformation du mapping des identités](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

La vidéo ci-dessous présente également les étapes de configuration d’une [!DNL LinkedIn Matched Audiences] destination et activation des segments.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>L’interface utilisateur d’Experience Platform est fréquemment mise à jour et peut avoir changé depuis l’enregistrement de cette vidéo. Pour obtenir les informations les plus récentes, reportez-vous à la section [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Authentification à la destination {#authenticate}

1. Recherchez le [!DNL LinkedIn Matched Audiences] destination dans le catalogue des destinations et sélectionnez **[!UICONTROL Configuration]**.
2. Sélectionner **[!UICONTROL Se connecter à la destination]**.
   ![Authentification à LinkedIn](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. Saisissez vos informations d’identification LinkedIn et sélectionnez **Connexion**.

### Renseignement des détails de destination {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="Identifiant de compte"
>abstract="Identifiant de compte du gestionnaire de campagne LinkedIn. Vous pouvez trouver cet identifiant dans votre compte LinkedIn Campaign Manager."

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]**: Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]**: Description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL Identifiant de compte]**: Votre [!DNL LinkedIn Campaign Manager Account ID]. Vous pouvez trouver cet identifiant dans votre [!DNL LinkedIn Campaign Manager] compte .

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur l’état du flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur les [abonnement aux alertes de destinations à l’aide de l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de fournir des détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Voir [Activation des données d’audience vers des destinations d’exportation de segments par flux](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Données exportées {#exported-data}

Une activation réussie signifie qu’une [!DNL LinkedIn] une audience personnalisée serait créée par programmation dans [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). L’adhésion au segment dans l’audience est ajoutée ou supprimée selon que les utilisateurs sont qualifiés ou disqualifiés pour les segments activés.

>[!TIP]
>
>L’intégration entre Adobe Experience Platform et [!DNL LinkedIn Matched Audiences] prend en charge les renvois d’audience historique. Toutes les qualifications de segments historiques sont envoyées à [!DNL LinkedIn] lorsque vous activez les segments vers la destination.
