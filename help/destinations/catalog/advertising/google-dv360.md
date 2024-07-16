---
title: Connexion Google Display & Video 360
description: Display & Video 360, anciennement appelé DoubleClick Bid Manager, est un outil utilisé pour exécuter le reciblage et des campagnes numériques ciblées dans des sources d’inventaire Display, Video et Mobile.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 55%

---

# Connexion [!DNL Google Display & Video 360]

>[!IMPORTANT]
>
> Google publie des modifications sur l’ [API Google Ads](https://developers.google.com/google-ads/api/docs/start), la [correspondance client](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) et l’ [API Display &amp; Video 360](https://developers.google.com/display-video/api/guides/getting-started/overview) afin de prendre en charge les exigences de conformité et de consentement définies en vertu de la [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) dans l’Union européenne ([Stratégie de consentement de l’utilisateur de l’UE](https://www.google.com/about/company/user-consent-policy/)). L’application de ces modifications aux exigences de consentement est en ligne depuis le 6 mars 2024.
><br/>
>Pour respecter la politique de consentement des utilisateurs de l’UE et continuer à créer des listes d’audiences pour les utilisateurs de l’Espace économique européen (EEE), les publicitaires et les partenaires doivent s’assurer qu’ils transmettent le consentement de l’utilisateur final lors du transfert des données d’audience. En tant que partenaire Google, Adobe vous fournit les outils nécessaires pour vous conformer à ces exigences de consentement en vertu de la DMA dans l’Union européenne.
><br/>
>Les clients qui ont acheté Adobe Privacy &amp; Security Shield et qui ont configuré une [politique de consentement](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) pour filtrer les profils non autorisés n’ont pas besoin d’agir.
><br/>
>Les clients qui n’ont pas acheté Adobe Privacy &amp; Security Shield doivent utiliser les fonctionnalités [définition de segment](../../../segmentation/home.md#segment-definitions) du [créateur de segments](../../../segmentation/ui/segment-builder.md) pour filtrer les profils non autorisés, afin de continuer à utiliser sans interruption les destinations Real-Time CDP Google existantes.

[!DNL Display & Video 360], anciennement appelé [!DNL DoubleClick Bid Manager], est un outil utilisé pour exécuter le reciblage et l’audience de campagnes numériques ciblées dans des sources d’inventaire Display, Video et Mobile.

## Spécificités de la destination {#specifics}

Notez les détails suivants qui sont spécifiques aux destinations [!DNL Google Display & Video 360] :

* Les audiences activées sont créées par programmation dans la plateforme Google.
* L’activation des renvoi d’audience vers la destination [!DNL Google Display & Video 360] est planifiée 24 à 48 heures après le premier mappage d’une audience à une connexion de destination. Cette mise à jour répond à la stratégie de Google consistant à attendre 24 heures avant d’ingérer des données et est destinée à améliorer les taux de correspondance entre Real-Time CDP et [!DNL Google Display & Video 360]. Il s’agit d’une configuration de serveur principal applicable uniquement à cette destination et qui n’est liée à aucune option de planification configurable par le client dans l’interface utilisateur.

>[!IMPORTANT]
>
>Si vous souhaitez créer votre première destination avec Google Display &amp; Video 360 et que vous n’avez pas activé la [fonctionnalité de synchronisation des identifiants](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=fr) dans le service d’ID Experience Cloud par le passé (avec Adobe Audience Manager ou d’autres applications), contactez Adobe Consulting ou l’assistance clientèle pour activer la synchronisation des identifiants. Si vous avez configuré précédemment des intégrations Google dans Audience Manager, les synchronisations d’identifiant que vous aviez configurées sont transférées vers Platform.

## Identités prises en charge {#supported-identities}

[!DNL Google Display & Video 360] prend en charge l’activation des audiences en fonction des identités affichées dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité | Description | Considérations |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| UUID AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=fr), également appelé [!DNL Device ID]. Identifiant numérique à 38 chiffres associé par Audience Manager à chaque appareil avec lequel il interagit. | Google utilise [UUID AAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=fr) pour cibler les utilisateurs en Californie et l’ID de cookie Google pour tous les autres utilisateurs. |
| ID de cookie [!DNL Google] | ID de cookie [!DNL Google] | [!DNL Google] utilise cet identifiant pour cibler les utilisateurs situés en dehors de la Californie. |
| RIDA | ID Roku pour la publicité. Cet identifiant identifie de manière unique les appareils Roku. |  |
| MAID | ID Microsoft Advertising. Cet identifiant identifie de manière unique les appareils exécutant Windows 10. |  |
| ID Amazon Fire TV | Cet identifiant identifie de manière unique les téléviseurs Amazon Fire. |  |

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez toutes les personnes membres d’une audience vers la destination Google. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

## Conditions préalables {#prerequisites}

### Liste autorisée {#allow-listing}

>[!NOTE]
>
>La liste autorisée est obligatoire avant de configurer votre première destination [!DNL Google Display & Video 360] dans Platform. Assurez-vous que le processus de mise en liste autorisée décrit ci-dessous a été terminé par [!DNL Google] avant de créer une destination.
>Une exception à cette règle s’applique aux clients d’[Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=fr). Si vous avez déjà créé une connexion à cette destination Google dans Audience Manager, il n’est pas nécessaire de passer à nouveau par le processus de liste autorisée et vous pouvez passer directement aux étapes suivantes.

Avant de créer la destination [!DNL Google Display & Video 360] dans Platform, vous devez contacter Google pour demander que l’Adobe soit placé sur la liste des fournisseurs de données autorisés et que votre compte soit ajouté à la liste autorisée. Contactez Google et fournissez les informations suivantes :

* **Identifiant de compte** : l’identifiant du compte Adobe avec Google. Identifiant de compte : 87933855.
* **Identifiant client** : l’identifiant client d’Adobe avec Google. Identifiant client : 89690775.
* **Votre type de compte** : utilisez **[!DNL Invite advertiser]** pour ne partager les audiences que vers une marque spécifique de votre compte Display &amp; Video 360 ou utilisez **[!DNL Invite partner]** pour partager les audiences vers toutes les marques de votre compte Display &amp; Video 360.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Type de compte]** : sélectionnez une option, en fonction de votre compte avec Google :
   * Utilisez `Invite Advertiser` pour ne partager les audiences que vers une marque spécifique de votre compte Display &amp; Video 360.
   * Utilisez `Invite Partner` pour partager les audiences vers toutes les marques de votre compte Display &amp; Video 360.
* **[!UICONTROL Identifiant de compte]** : renseignez votre identifiant de compte **[!DNL Invite partner]** ou **[!DNL Invite advertiser]** avec Google. En règle générale, il s’agit d’un identifiant à six ou sept chiffres.

>[!NOTE]
>
>Lors de la configuration d’une destination [!DNL Google Display & Video 360], demandez à votre représentant d’Adobe ou [!DNL Google Account Manager] de déterminer le type de compte dont vous disposez.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Voir [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

## Données exportées

Pour vérifier si les données ont bien été exportées vers la destination [!DNL Google Display & Video 360], vérifiez votre compte [!DNL Google Display & Video 360]. Si l’activation a réussi, les audiences sont renseignées dans votre compte.

## Dépannage {#troubleshooting}

### Message d’erreur 400 Requête incorrecte {#bad-request}

Lors de la configuration de cette destination, vous risquez de recevoir l’erreur suivante :

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Cette erreur se produit lorsque les comptes clients ne respectent pas les [conditions préalables](#prerequisites). Pour résoudre ce problème, contactez Google et assurez-vous que votre compte est sur liste autorisée.