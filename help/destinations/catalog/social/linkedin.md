---
keywords: linkedin;connexion linkedin;destinations linkedin;linkedin;
title: Connexion des audiences correspondantes LinkedIn
description: Activez les profils de vos campagnes LinkedIn pour le ciblage, la personnalisation et la suppression des audiences, en fonction des e-mails hachés.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: c8eedc1f020b8605c9565015461cb1dfd47bba1f
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 33%

---

# Connexion [!DNL LinkedIn Matched Audiences]

## Présentation {#overview}

Activez les profils de vos campagnes [!DNL LinkedIn] pour le ciblage, la personnalisation et la suppression des audiences, en fonction des e-mails hachés et des identifiants mobiles.

![ Destination LinkedIn dans l’interface utilisateur de Adobe Experience Platform ](../../assets/catalog/social/linkedin/catalog.png)

## Cas d’utilisation

Pour mieux comprendre quand et comment utiliser la destination [!DNL LinkedIn Matched Audiences], consultez le cas d’utilisation ci-dessous que la clientèle Adobe Experience Platform peut résoudre à l’aide de cette fonctionnalité.

Une société de logiciels organise une conférence et souhaite rester en contact avec les participants et leur présenter des offres personnalisées en fonction de leur statut de participation à la conférence. L’entreprise peut ingérer des adresses e-mail ou des identifiants d’appareil mobile de ses propres [!DNL CRM] dans Adobe Experience Platform. Ensuite, ils peuvent créer des audiences à partir de leurs propres données hors ligne et les envoyer à la plateforme sociale [!DNL LinkedIn], ce qui optimise leurs dépenses publicitaires.

## Identités prises en charge {#supported-identities}

[!DNL LinkedIn Matched Audiences] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms IDFA. |
| email_lc_sha256 | Adresses e-mail hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. Suivez les instructions de la section [Exigences de correspondance des identifiants](#id-matching-requirements-id-matching-requirements) et utilisez les espaces de noms appropriés pour le texte brut et les e-mails hachés, respectivement. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience avec les identifiants (nom, numéro de téléphone et autres) utilisés dans la destination [!DNL LinkedIn Matched Audiences]. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conditions préalables relatives au compte LinkedIn {#LinkedIn-account-prerequisites}

Avant de pouvoir utiliser la destination [!UICONTROL Audience appariée LinkedIn], assurez-vous que votre compte [!DNL LinkedIn Campaign Manager] dispose du niveau d’autorisation [!DNL Creative Manager] ou supérieur.

Pour savoir comment modifier vos autorisations d’utilisateur [!DNL LinkedIn Campaign Manager], voir [Ajouter, modifier et supprimer des autorisations d’utilisateur sur les comptes Advertising](https://www.linkedin.com/help/lms/answer/5753) dans la documentation LinkedIn.

## Exigences de correspondance des identifiants {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] nécessite qu’aucune information d’identification personnelle (PII) ne soit envoyée en clair. Par conséquent, les audiences activées pour [!DNL LinkedIn Matched Audiences] peuvent être désactivées à partir d’identifiants *hachés* tels que des adresses e-mail ou des identifiants d’appareil mobile.

Selon le type d’identifiants ingérés dans Adobe Experience Platform, vous devez respecter les exigences correspondantes.

## Exigences en matière de hachage des e-mails {#email-hashing-requirements}

Vous pouvez hacher les adresses e-mail avant de les ingérer dans Adobe Experience Platform ou les utiliser en clair dans Experience Platform et demander à [!DNL Experience Platform] de les hacher lors de l’activation.

Pour en savoir plus sur l’ingestion d’adresses e-mail dans Experience Platform, consultez la [présentation de l’ingestion par lots](/help/ingestion/batch-ingestion/overview.md) et la [présentation de l’ingestion par flux](/help/ingestion/streaming-ingestion/overview.md).

Si vous choisissez de hacher les adresses e-mail vous-même, veillez à respecter les exigences suivantes :

* Supprimez tous les espaces de début et de fin de la chaîne de l’e-mail. Par exemple : `johndoe@example.com`, pas `<space>johndoe@example.com<space>` ;
* Lors du hachage des chaînes de l’e-mail, veillez à hacher la chaîne en minuscules ;
   * Exemple : `example@email.com`, pas `EXAMPLE@EMAIL.COM` ;
* Vérifiez que la chaîne hachée est en minuscules
   * Exemple : `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, pas `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149` ;
* Ne salez pas la chaîne.

>[!NOTE]
>
>Les données des espaces de noms non hachés sont automatiquement hachées par [!DNL Experience Platform] lors de l’activation.
>&#x200B;> Les données source des attributs ne sont pas automatiquement hachées.
> 
> Lors de l’étape [ Mappage d’identité ](../../ui/activate-segment-streaming-destinations.md#mapping), lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation.
> 
> L’option **[!UICONTROL Appliquer la transformation]** ne s’affiche que lorsque vous sélectionnez des attributs comme champs source. Elle ne s’affiche pas lorsque vous choisissez des espaces de noms.

![Transformation du mapping d’identités](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]** et **[!UICONTROL Gérer les destinations]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

La vidéo ci-dessous montre également les étapes à suivre pour configurer une destination [!DNL LinkedIn Matched Audiences] et activer des audiences.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>L’interface utilisateur d’Experience Platform est fréquemment mise à jour et peut avoir changé depuis l’enregistrement de cette vidéo. Pour obtenir les informations les plus récentes, reportez-vous au tutoriel [configuration de destination](../../ui/connect-destination.md).

### S’authentifier auprès de la destination {#authenticate}

1. Recherchez la destination [!DNL LinkedIn Matched Audiences] dans le catalogue de destinations et sélectionnez **[!UICONTROL Configurer]**.
2. Sélectionnez **[!UICONTROL Se connecter à la destination]**.
   ![S’authentifier sur LinkedIn](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. Saisissez vos identifiants LinkedIn et sélectionnez **Connexion**.

### Actualiser les informations d’identification d’authentification {#refresh-authentication-credentials}

Les jetons LinkedIn expirent tous les 60 jours. Vous pouvez surveiller les dates d’expiration de votre jeton à partir de la colonne **[!UICONTROL Date d’expiration du compte]** dans les onglets **[[!UICONTROL Comptes]](../../ui/destinations-workspace.md#accounts)** ou **[[!UICONTROL Parcourir]](../../ui/destinations-workspace.md#browse)**.

Une fois le jeton expiré, les exportations de données vers la destination cessent de fonctionner. Pour éviter cette situation, réauthentifiez-vous en procédant comme suit :

1. Accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Comptes]**
2. (Facultatif) Utilisez les filtres disponibles sur la page pour afficher uniquement les comptes LinkedIn.
   ![Filtrer pour afficher uniquement les comptes LinkedIn](/help/destinations/assets/catalog/social/linkedin/refresh-oauth-filters.png)
3. Sélectionnez le compte à actualiser, puis les points de suspension et sélectionnez **[!UICONTROL Modifier les détails]**.
   ![Sélectionnez Modifier les détails](/help/destinations/assets/catalog/social/linkedin/refresh-oauth-edit-details.png)
4. Dans la fenêtre modale, sélectionnez **[!UICONTROL Reconnecter OAuth]** et réauthentifier à l’aide de vos informations d’identification LinkedIn.
   ![Fenêtre modale avec l’option Reconnecter OAuth ](/help/destinations/assets/catalog/social/linkedin/reconnect-oauth-control.png)

>[!SUCCESS]
> 
>Vos informations d’authentification sont actualisées et leur délai d’expiration est réinitialisé à 60 jours.

### Renseigner les détails de la destination {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="Identifiant de compte"
>abstract="Identifiant de votre compte LinkedIn Campaign Manager. Vous pouvez trouver cet identifiant sur votre compte LinkedIn Campaign Manager."

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Identifiant de compte]** : votre [!DNL LinkedIn Campaign Manager Account ID]. Cet identifiant se trouve dans votre compte [!DNL LinkedIn Campaign Manager].

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le graphique d’identités]** [&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Voir [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

## Données exportées {#exported-data}

Une activation réussie signifie qu’une audience personnalisée [!DNL LinkedIn] est créée par programmation dans [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). L’appartenance à l’audience est ajustée à mesure que les utilisateurs sont qualifiés ou disqualifiés pour les audiences activées.

>[!TIP]
>
>L’intégration entre Adobe Experience Platform et [!DNL LinkedIn Matched Audiences] prend en charge les renvois d’audience historiques. Toutes les qualifications d’audience historiques sont envoyées à [!DNL LinkedIn] lorsque vous activez les audiences vers la destination.
