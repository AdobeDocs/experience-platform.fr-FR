---
audience: user
user-guide-title: Guide des destinations
user-guide-description: Activez vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par email, la publicité ciblée et de nombreux autres cas d’utilisation.
description: Ce document répertorie la table des matières pour les destinations Adobe Experience Platform
feature: Destinations
source-git-commit: a7c36f1a157b6020fede53e5c1074d966f26cf3d
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 46%

---


# Destinations  {#destinations}

* [Présentation des destinations](./home.md)
* [Types et catégories de destination](./destination-types.md)
* Tutoriels sur les API {#api}
   * [Connexion à des destinations de diffusion en continu et activation de données à l’aide de l’API Flow Service](./api/streaming-destinations.md)
   * [Connexion à des destinations de marketing par e-mail et activation de données à l’aide de l’API Flow Service](./api/email-marketing.md)
* Guides d’interface utilisateur {#ui}
   * [Espace de travail des destinations](./ui/destinations-workspace.md)
   * [Créer une connexion de destination](./ui/connect-destination.md)
   * Activer les données d’audience vers les destinations{#activate}
      * [Présentation de l’Activation](./ui/activation-overview.md)
      * [Activation des données d’audience vers des destinations d’exportation de segments de diffusion](./ui/activate-segment-streaming-destinations.md)
      * [Activer les données d’audience vers les destinations d’exportation de profil de diffusion en continu](./ui/activate-streaming-profile-destinations.md)
      * [Activer les données d’audience vers des destinations d’exportation de profil de lot](./ui/activate-batch-profile-destinations.md)
      * [Activer les données d’audience vers des destinations de demande de profil (bêta)](./ui/activate-profile-request-destinations.md)
   * [Afficher les détails de destination](./ui/destination-details-page.md)
   * [Mettre à jour les comptes de destination](./ui/update-accounts.md)
   * [Modification des flux d’activation](./ui/edit-activation.md)
   * [Suppression de destinations](./ui/delete-destinations.md)
   * [Surveillance des flux de données](./ui/monitor-dataflows.md)
* Catalogue des destinations {#catalog}
   * [Présentation du catalogue des destinations](./catalog/overview.md)
   * [ (Alpha) Connexion HTTP](./catalog/http-destination.md)
   * Destinations Adobe {#adobe}
      * [Présentation des destinations Adobe](./catalog/adobe/overview.md)
      * [(Bêta) Connexion Marketo Engage](./catalog/adobe/marketo-engage.md)
      * [Partage de segments Experience Platform](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=fr)
   * Destinations publicitaires {#advertising}
      * [Présentation des destinations publicitaires](./catalog/advertising/overview.md)
      * [Extension Adobe Advertising Cloud](./catalog/advertising/adobe-advertising-cloud.md)
      * [Extension Awin Advertiser Conversion Tag](./catalog/advertising/awin-conversiontag.md)
      * [Extension Awin Advertiser Mastertag](./catalog/advertising/awin-mastertag.md)
      * [Extension Bing Ads Universal Event Tracking (UET)](./catalog/advertising/bing-ads.md)
      * [Extension Branch](./catalog/advertising/branch.md)
      * [Extension DoubleClick Floodlight (bêta)](./catalog/advertising/doubleclick-floodlight.md)
      * [Extension Pixel Facebook](./catalog/advertising/facebook-pixel.md)
      * [Extension Flashtalking OneTag](./catalog/advertising/flashtalking.md)
      * [Connexion Google Ads](./catalog/advertising/google-ads-destination.md)
      * [Extension Google Ads](./catalog/advertising/google-ads-extension.md)
      * [Connexion à Google Ad Manager](./catalog/advertising/google-ad-manager.md)
      * [Connexion de correspondance client Google](./catalog/advertising/google-customer-match.md)
      * [Connexion Google Display &amp; Video 360](./catalog/advertising/google-dv360.md)
      * [Extension Google gtag](./catalog/advertising/gtag-advertising.md)
      * [Extension LinkedIn Insight Tag](./catalog/advertising/linkedin.md)
      * [Connexion à Microsoft Bing](./catalog/advertising/bing.md)
      * [Extension Pinterest Conversion Tracking](./catalog/advertising/pinterest-extension.md)
      * [Connexion à la liste des clients pinterest](./catalog/advertising/pinterest.md)
      * [Connexion au bureau de commerce](./catalog/advertising/tradedesk.md)
      * [Extension Twitter Universal Website Tag](./catalog/advertising/twitter-uwt.md)
      * [Connexion à Yahoo/Verizon DataX](./catalog/advertising/datax.md)
   * Destinations d’analyse {#analytics}
      * [Présentation des destinations d’analyse](./catalog/analytics/overview.md)
      * [Extension Adform Website Tracking](./catalog/analytics/adform.md)
      * [Extension Adobe Analytics](./catalog/analytics/adobe-analytics.md)
      * [Extension Adobe Media Analytics for Audio and Video](./catalog/analytics/adobe-video-analytics.md)
      * [Extension Clicktale](./catalog/analytics/clicktale.md)
      * [Extension Contentsquare](./catalog/analytics/contentsquare.md)
      * [Extension Decibel](./catalog/analytics/decibel.md)
      * [Extension Demandbase](./catalog/analytics/demandbase.md)
      * [Extension DialogTech](./catalog/analytics/dialogtech.md)
      * [Extension Google Global Site Tag](./catalog/analytics/gtag-analytics.md)
      * [Extension Google Universal Analytics](./catalog/analytics/google-universal-analytics.md)
      * [Extension JW Player Analytics (Beta)](./catalog/analytics/jw-player-analytics.md)
      * [Extension Nielsen BSDK](./catalog/analytics/nielsen-bsdk.md)
      * [Extension Nielsen IMA Handler](./catalog/analytics/nielsen-ima.md)
      * [Extension Nielsen VideoJS Player Handler](./catalog/analytics/nielsen-videojs.md)
      * [Extension Parse.ly Analytics](./catalog/analytics/parsely.md)
      * [Extension Quantum Metric](./catalog/analytics/quantum-metric.md)
      * [Extension SessionCam](./catalog/analytics/sessioncam.md)
      * [Extension TMMData](./catalog/analytics/tmmdata.md)
      * [Extension Yext Conversion Tracking](./catalog/analytics/yext.md)
   * Destinations de stockage dans le cloud {#cloud-storage}
      * [Présentation des destinations de stockage dans le cloud](./catalog/cloud-storage/overview.md)
      * [(Bêta) Connexion Amazon Kinesis](./catalog/cloud-storage/amazon-kinesis.md)
      * [Connexion à Amazon S3](./catalog/cloud-storage/amazon-s3.md)
      * [Connexion à Azure Blob](./catalog/cloud-storage/azure-blob.md)
      * [(Bêta) Connexion à Azure Event Hubs](./catalog/cloud-storage/azure-event-hubs.md)
      * [Connexion SFTP](./catalog/cloud-storage/sftp.md)
      * [Liste d&#39;autorisations d&#39;adresses IP](./catalog/cloud-storage/ip-address-allow-list.md)
   * Destinations de la plate-forme de gestion des données {#data-management}
      * [Présentation des destinations DMP (Data Management Platform)](./catalog/data-management/overview.md)
      * [Extension Audience Manager DIL](./catalog/data-management/aam-dil-extension.md)
   * Destinations de messagerie {#email}
      * [Extension Bizible](./catalog/email/bizible.md)
      * [Extension Marketo](./catalog/email/marketo.md)
      * [Extension Marketo Munchkin](./catalog/email/marketo-munchkin.md)
      * [Extension PebblePost](./catalog/email/pebblepost.md)
   * Destinations de marketing par e-mail {#email-marketing}
      * [Présentation des destinations du marketing par email](./catalog/email-marketing/overview.md)
      * [Connexion Adobe Campaign](./catalog/email-marketing/adobe-campaign.md)
      * [Oracle de connexion Eloqua](./catalog/email-marketing/oracle-eloqua.md)
      * [Oracle Connexion Responsys](./catalog/email-marketing/oracle-responsys.md)
      * [Connexion au Marketing Cloud Salesforce](./catalog/email-marketing/salesforce-marketing-cloud.md)
   * Extensions de balises {#launch-extensions}
      * [Présentation de l’extension de balise](./catalog/launch-extensions/overview.md)
   * Destinations d’engagement mobile {#mobile-engagement}
      * [Présentation des destinations d’engagement mobile](./catalog/mobile-engagement/overview.md)
      * [Connexion Attributs de navire](./catalog/mobile-engagement/airship-attributes.md)
      * [Connexion aux balises de navigation](./catalog/mobile-engagement/airship-tags.md)
      * [Connexion au frein](./catalog/mobile-engagement/braze.md)
   * Destinations de personnalisation {#personalization}
      * [Présentation des destinations de personnalisation](./catalog/personalization/overview.md)
      * [Connexion Adobe Target (Bêta)](./catalog/personalization/adobe-target-connection.md)
      * [Extension Adobe Target](./catalog/personalization/adobe-target.md)
      * [Extension Adobe Target v2](./catalog/personalization/adobe-target-v2.md)
      * [Extension Beemray](./catalog/personalization/beemray.md)
      * [Connexion personnalisée personnalisée (bêta)](./catalog/personalization/custom-personalization.md)
      * [Extension D&amp;B Visitor Intelligence](./catalog/personalization/dnb.md)
      * [Extension du service Experience Cloud ID](./catalog/personalization/adobe-ecid.md)
      * [Extension Gainsight](./catalog/personalization/gainsight.md)
      * [Extension KickFire](./catalog/personalization/kickfire.md)
      * [Extension Marketo Web Personalization](./catalog/personalization/marketo-web-personalization.md)
   * Destinations sociales{#social}
      * [Présentation des destinations sociales](./catalog/social/overview.md)
      * [Extension Adobe Livefyre](./catalog/social/adobe-livefyre.md)
      * [Connexion facebook](./catalog/social/facebook.md)
      * [Connexion d’auditoires correspondants linkedIn](./catalog/social/linkedin.md)
      * [[!DNL Twitter Custom Audiences] connexion](./catalog/social/twitter.md)
   * Destinations d’enquête {#survey}
      * [Présentation des destinations d’enquête](./catalog/survey/overview.md)
      * [Destination de l’extension Foresee](./catalog/survey/foresee.md)
      * [Extension InMoment](./catalog/survey/inmoment.md)
      * [Extension Website Feedback de Qualtrics](./catalog/survey/qualtrics.md)
      * [Extension Intercept Surveys de QuestionPro](./catalog/survey/web-intercept-surveys.md)
   * Destinations de voix du client {#voice}
      * [Présentation de la voix des destinations client](./catalog/voice/overview.md)
      * [Extension Confirmit Digital Feedback](./catalog/voice/confirmit-digital-feedback.md)
      * [Extension Invoca Tags](./catalog/voice/invoca.md)
      * [Extension Medallia](./catalog/voice/medallia.md)
      * [Extension Talk URL Inbox](./catalog/voice/talkurl.md)
* SDK de destination {#destination-sdk}
   * [Présentation](./destination-sdk/overview.md)
   * [Conditions préalables à l’intégration](./destination-sdk/integration-prerequisites.md)
   * [Prise en main](./destination-sdk/getting-started.md)
   * Fonctionnalité du SDK de destination {#functionality}
      * [Options de configuration](./destination-sdk/configuration-options.md)
      * [Configuration de destination](./destination-sdk/destination-configuration.md)
      * [Spécifications relatives aux serveurs et aux modèles](./destination-sdk/server-and-template-configuration.md)
      * [Format du message](./destination-sdk/message-format.md)
      * [Gestion des métadonnées du public](./destination-sdk/audience-metadata-management.md)
      * [Configuration de l’authentification](./destination-sdk/credentials-configuration.md)
      * [Authentification OAuth 2](./destination-sdk/oauth2-authentication.md)
      * Outils de développement {#developer-tools}
         * [Création et test d’un modèle de transformation de message](./destination-sdk/create-template.md)
         * [Test de votre configuration de destination](./destination-sdk/test-destination.md)
   * Référence d’API {#api-reference}
      * [Opérations de l’API de point de terminaison Destinations](./destination-sdk/destination-configuration-api.md)
      * [Opérations d’API de point de terminaison du serveur de destination](./destination-sdk/destination-server-api.md)
      * [Opérations de l’API de point de terminaison des métadonnées d’audience](./destination-sdk/audience-metadata-api.md)
      * [Opérations de l&#39;API de point de terminaison des informations d&#39;identification](./destination-sdk/credentials-configuration-api.md)
      * [Publication des opérations de l’API de point de terminaison](./destination-sdk/destination-publish-api.md)
      * Référence des outils de développement {#developer-tools-reference}
         * [Obtention d’exemples d’opérations d’API de modèle](./destination-sdk/sample-template-api.md)
         * [Opérations d’API de modèle de rendu](./destination-sdk/render-template-api.md)
         * [Opérations de l’API de test de destination](./destination-sdk/destination-testing-api.md)
         * [Exemples d’opérations d’API de génération de profils](./destination-sdk/sample-profile-generation-api.md)
   * Guides {#guides}
      * [Utiliser le SDK de destination pour configurer une destination de diffusion en continu](./destination-sdk/configure-destination-instructions.md)
   * Document de destination {#document-destination}
      * [Document de destination dans Adobe Experience Platform](./destination-sdk/docs-framework/documentation-instructions.md)
      * [Utilisation de l’interface Web GitHub pour créer une page de documentation de destination](./destination-sdk/docs-framework/use-github-interface-to-create-documentation.md)
      * [Utilisation d’un éditeur de texte dans votre environnement local pour créer une page de documentation de destination](./destination-sdk/docs-framework/work-in-local-environment.md)
      * [Modèle de libre-service de documentation](./destination-sdk/docs-framework/self-service-template.md)
* [Questions fréquentes](./destinations-faq.md)
* [Notes de mise à jour de Platform](https://docs.adobe.com/content/help/fr-FR/experience-platform/release-notes/latest.html)
