---
audience: user
user-guide-title: Guide des destinations
user-guide-description: Activez vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.
description: Ce document répertorie la table des matières des destinations Adobe Experience Platform
feature: Destinations
source-git-commit: 69bf43f86ab3369ad0c7febcb69ec41d3bcac8bb
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 85%

---


# Destinations {#destinations}

* [Présentation des destinations](./home.md)
* [Types et catégories de destination](./destination-types.md)
* Tutoriels sur les API {#api}
   * [Se connecter aux destinations de diffusion en continu et activer les données à l’aide de l’API Flow Service](./api/streaming-destinations.md)
   * [Se connecter à l’espace de stockage par lots et aux destinations de marketing par e-mail et activer les données à l’aide de l’API Flow Service](./api/connect-activate-batch-destinations.md)
   * [(Version Beta) Activer les segments d’audience vers des destinations par lots via l’API d’activation ad hoc](./api/ad-hoc-activation-api.md)
   * [Mettre à jour les flux de données de destination](./api/update-destination-dataflows.md)
   * [Supprimer les comptes de destination](./api/delete-destination-account.md)
   * [Supprimer les flux de données de destination](./api/delete-destination-dataflow.md)
* Guides d’interface utilisateur {#ui}
   * [Espace de travail des destinations](./ui/destinations-workspace.md)
   * [Créer une connexion de destination](./ui/connect-destination.md)
   * Activer les données d’audience vers les destinations {#activate}
      * [Présentation de l’activation](./ui/activation-overview.md)
      * [Activer les données d’audience vers des destinations d’exportation de segments de diffusion en continu](./ui/activate-segment-streaming-destinations.md)
      * [Activer les données d’audience vers des destinations d’exportation de segments de diffusion en continu](./ui/activate-streaming-profile-destinations.md)
      * [Activer les données d’audience vers des destinations d’exportation de profils par lots](./ui/activate-batch-profile-destinations.md)
      * [Activer les données d’audience vers les destinations de requête de profil](./ui/activate-profile-request-destinations.md)
      * [Configurez des destinations de personnalisation pour la personnalisation de la même page et de la page suivante.](./ui/configure-personalization-destinations.md)
      * [(Version bêta) Exportation de fichiers à la demande vers des destinations par lots à l’aide de l’interface utilisateur de l’Experience Platform](./ui/export-file-now.md)
   * [Afficher les détails de la destination](./ui/destination-details-page.md)
   * [Mettre à jour les comptes de destination](./ui/update-accounts.md)
   * [Supprimer les comptes de destination](./ui/delete-destination-account.md)
   * [Modification des flux de données d’activation](./ui/edit-activation.md)
   * [Supprimer les destinations](./ui/delete-destinations.md)
   * [Surveiller les flux de données](./ui/monitor-dataflows.md)
   * [Abonner aux alertes de destination contextuelles](ui/alerts.md)
* Catalogue des destinations {#catalog}
   * [Présentation du catalogue des destinations](./catalog/overview.md)
   * Destinations Adobe {#adobe}
      * [Présentation des destinations Adobe](./catalog/adobe/overview.md)
      * [Connexion Marketo Engage](./catalog/adobe/marketo-engage.md)
      * [Partage de segments Experience Platform](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=fr)
   * Destinations publicitaires {#advertising}
      * [Présentation des destinations publicitaires](./catalog/advertising/overview.md)
      * [Connexion Adobe Advertising Cloud](./catalog/advertising/adobe-advertising-cloud-connection.md)
      * [Extension Adobe Advertising Cloud](./catalog/advertising/adobe-advertising-cloud.md)
      * [Extension Awin Advertiser Conversion Tag](./catalog/advertising/awin-conversiontag.md)
      * [Extension Awin Advertiser Mastertag](./catalog/advertising/awin-mastertag.md)
      * [Extension Bing Ads Universal Event Tracking (UET)](./catalog/advertising/bing-ads.md)
      * [Extension Branch](./catalog/advertising/branch.md)
      * [(Version bêta) Connexion aux critères](./catalog/advertising/criteo.md)
      * [Extension DoubleClick Floodlight (Version Beta)](./catalog/advertising/doubleclick-floodlight.md)
      * [Extension Pixel Facebook](./catalog/advertising/facebook-pixel.md)
      * [Extension Flashtalking OneTag](./catalog/advertising/flashtalking.md)
      * [Connexion Google Ads](./catalog/advertising/google-ads-destination.md)
      * [Extension Google Ads](./catalog/advertising/google-ads-extension.md)
      * [Connexion Google Ad Manager](./catalog/advertising/google-ad-manager.md)
      * [(Version bêta) Connexion à Google Ad Manager 360](./catalog/advertising/google-ad-manager-360-connection.md)
      * [Connexion à Google Customer Match](./catalog/advertising/google-customer-match.md)
      * [Connexion Google Display &amp; Video 360](./catalog/advertising/google-dv360.md)
      * [Extension Google gtag](./catalog/advertising/gtag-advertising.md)
      * [Extension LinkedIn Insight Tag](./catalog/advertising/linkedin.md)
      * [Connexion Microsoft Bing](./catalog/advertising/bing.md)
      * [Extension Pinterest Conversion Tracking](./catalog/advertising/pinterest-extension.md)
      * [Connexion Liste des Clients Pinterest](./catalog/advertising/pinterest.md)
      * [(Version bêta) Connexion à Snapchat Ads](./catalog/advertising/snap-inc.md)
      * [Connexion Trade Desk](./catalog/advertising/tradedesk.md)
      * [La connexion CRM du centre commercial](./catalog/advertising/tradedesk-emails.md)
      * [Extension Twitter Universal Website Tag](./catalog/advertising/twitter-uwt.md)
      * [Connexion Yahoo/Verizon DataX](./catalog/advertising/datax.md)
   * Destinations Analytics {#analytics}
      * [Présentation des destinations Analytics](./catalog/analytics/overview.md)
      * [Extension Adform Website Tracking](./catalog/analytics/adform.md)
      * [Extension Adobe Analytics](./catalog/analytics/adobe-analytics.md)
      * [Extension Adobe Media Analytics for Audio and Video](./catalog/analytics/adobe-video-analytics.md)
      * [Extension Clicktale](./catalog/analytics/clicktale.md)
      * [Extension Contentsquare](./catalog/analytics/contentsquare.md)
      * [Extension Decibel](./catalog/analytics/decibel.md)
      * [Extension Demandbase](./catalog/analytics/demandbase.md)
      * [Extension DialogTech](./catalog/analytics/dialogtech.md)
      * [Extension Google Global Site Tag](./catalog/analytics/gtag-analytics.md)
      * [Extension Google Universal Analytics](./catalog/analytics/google-universal-analytics.md)
      * [Extension JW Player Analytics (version Beta)](./catalog/analytics/jw-player-analytics.md)
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
      * [Connexion à Amazon Kinesis](./catalog/cloud-storage/amazon-kinesis.md)
      * [Connexion Amazon S3](./catalog/cloud-storage/amazon-s3.md)
      * [Connexion Azure Blob](./catalog/cloud-storage/azure-blob.md)
      * [Connexion à Azure Event Hubs](./catalog/cloud-storage/azure-event-hubs.md)
      * [Connexion SFTP](./catalog/cloud-storage/sftp.md)
      * [LISTE AUTORISÉE des adresses IP pour les destinations de stockage dans le cloud](./catalog/cloud-storage/ip-address-allow-list.md)
   * Destinations Data Management Platform {#data-management}
      * [Destinations Data Management Platform (DMP)](./catalog/data-management/overview.md)
      * [Extension Audience Manager DIL](./catalog/data-management/aam-dil-extension.md)
   * Destinations dʼe-mail {#email}
      * [Extension Bizible](./catalog/email/bizible.md)
      * [Extension Marketo](./catalog/email/marketo.md)
      * [Extension Marketo Munchkin](./catalog/email/marketo-munchkin.md)
      * [Extension PebblePost](./catalog/email/pebblepost.md)
   * Destinations du marketing par e-mail {#email-marketing}
      * [Présentation des destinations du marketing par e-mail](./catalog/email-marketing/overview.md)
      * [Connexion Adobe Campaign](./catalog/email-marketing/adobe-campaign.md)
      * [Connexion Orale Eloqua](./catalog/email-marketing/oracle-eloqua.md)
      * [Connexion Oracle Responsys](./catalog/email-marketing/oracle-responsys.md)
      * [Connexion Salesforce Marketing Cloud](./catalog/email-marketing/salesforce-marketing-cloud.md)
      * [Connexion à SendGrid](./catalog/email-marketing/sendgrid.md)
   * Extensions de balises {#launch-extensions}
      * [Présentation des extensions de balises](./catalog/launch-extensions/overview.md)
   * Destinations d’engagement mobile {#mobile-engagement}
      * [Présentation des destinations d’engagement mobile](./catalog/mobile-engagement/overview.md)
      * [Connexion Attributs Airship](./catalog/mobile-engagement/airship-attributes.md)
      * [Connexion Balises Airship](./catalog/mobile-engagement/airship-tags.md)
      * [Connexion Braze](./catalog/mobile-engagement/braze.md)
   * Destinations de personnalisation {#personalization}
      * [Présentation des destinations de personnalisation](./catalog/personalization/overview.md)
      * [Connexion Adobe Target](./catalog/personalization/adobe-target-connection.md)
      * [Extension Adobe Target](./catalog/personalization/adobe-target.md)
      * [Extension Adobe Target v2](./catalog/personalization/adobe-target-v2.md)
      * [Extension Beemray](./catalog/personalization/beemray.md)
      * [Connexion de personnalisation personnalisée](./catalog/personalization/custom-personalization.md)
      * [Extension D&amp;B Visitor Intelligence](./catalog/personalization/dnb.md)
      * [Extension du service Experience Cloud ID](./catalog/personalization/adobe-ecid.md)
      * [Extension Gainsight](./catalog/personalization/gainsight.md)
      * [Extension KickFire](./catalog/personalization/kickfire.md)
      * [Extension Marketo Web Personalization](./catalog/personalization/marketo-web-personalization.md)
   * Destinations sociales {#social}
      * [Présentation des destinations sociales](./catalog/social/overview.md)
      * [Extension Adobe Livefyre](./catalog/social/adobe-livefyre.md)
      * [Connexion Facebook](./catalog/social/facebook.md)
      * [Connexion des audiences correspondantes linkedIn](./catalog/social/linkedin.md)
      * [Connexion [!DNL Twitter Custom Audiences]](./catalog/social/twitter.md)
   * Destinations de diffusion en continu {#streaming}
      * [Connexion via l’API HTTP](./catalog/streaming/http-destination.md)
      * [LISTE AUTORISÉE d’adresses IP pour les destinations de diffusion en continu](./catalog/streaming/ip-address-allow-list.md)
   * Destinations d’enquête {#survey}
      * [Présentation des destinations d’enquête](./catalog/survey/overview.md)
      * [Destination de l’extension Foresee](./catalog/survey/foresee.md)
      * [Extension InMoment](./catalog/survey/inmoment.md)
      * [Extension Website Feedback de Qualtrics](./catalog/survey/qualtrics.md)
      * [Extension Intercept Surveys de QuestionPro](./catalog/survey/web-intercept-surveys.md)
   * Destinations de voix du client {#voice}
      * [Présentation des destinations de voix du client](./catalog/voice/overview.md)
      * [Extension Confirmit Digital Feedback](./catalog/voice/confirmit-digital-feedback.md)
      * [Extension Invoca Tags](./catalog/voice/invoca.md)
      * [Connexion à Medallia](./catalog/voice/medallia-connector.md)
      * [Extension Medallia](./catalog/voice/medallia.md)
      * [Extension Talk URL Inbox](./catalog/voice/talkurl.md)
* Destination SDK {#destination-sdk}
   * [Présentation](./destination-sdk/overview.md)
   * [Conditions préalables à l’intégration](./destination-sdk/integration-prerequisites.md)
   * [Prise en main](./destination-sdk/getting-started.md)
   * Fonctionnalité de Destination SDK {#functionality}
      * [Options de configuration](./destination-sdk/configuration-options.md)
      * [Configuration de destination de diffusion en continu](./destination-sdk/destination-configuration.md)
      * [(Version Beta) Configuration de destinations basées sur des fichiers](./destination-sdk/file-based-destination-configuration.md)
      * [Spécifications de serveur et de modèle pour les destinations de diffusion en continu](./destination-sdk/server-and-template-configuration.md)
      * [(Version Beta) Spécifications de serveur et de fichier pour les destinations basées sur les fichiers](./destination-sdk/server-and-file-configuration.md)
      * [Format des messages](./destination-sdk/message-format.md)
      * [Gérer les métadonnées d’audience](./destination-sdk/audience-metadata-management.md)
      * Authentification {#authentication}
         * [Configuration de l’authentification](./destination-sdk/authentication-configuration.md)
         * [Authentification OAuth 2](./destination-sdk/oauth2-authentication.md)
      * Outils de développeur {#developer-tools}
         * [Créer et tester un modèle de transformation de message](./destination-sdk/create-template.md)
         * [Tester la configuration de votre destination](./destination-sdk/test-destination.md)
   * Opérations dʼAPI {#api}
      * [Référence de l’API Destination SDK (création de destination)](https://www.adobe.io/experience-platform-apis/references/destination-authoring/)
      * [Opérations de l’API du point d’entrée des destinations](./destination-sdk/destination-configuration-api.md)
      * [Opérations de l’API du point d’entrée du serveur de destination](./destination-sdk/destination-server-api.md)
      * [Opérations de l’API du point d’entrée des métadonnées d’audience](./destination-sdk/audience-metadata-api.md)
      * [Opérations des paramètres d’identification de l’API](./destination-sdk/credentials-configuration-api.md)
      * [Opérations de l’API du point d’entrée de publication](./destination-sdk/destination-publish-api.md)
      * Référence des outils du développeur {#developer-tools-reference}
         * API de test de destination en flux continu {#streaming-destination-testing-api}
            * [Opérations dʼAPI pour lʼobtention du modèle](./destination-sdk/sample-template-api.md)
            * [Opérations de l’API pour le rendu du modèle](./destination-sdk/render-template-api.md)
            * [Opérations de l’API pour les tests de destination](./destination-sdk/destination-testing-api.md)
            * [Opérations de l’API pour la génération d’un profil type](./destination-sdk/sample-profile-generation-api.md)
         * API de test de destination basé sur les fichiers {#file-based-destination-testing-api}
            * [API de test de destination basé sur des fichiers - Aperçu](./destination-sdk/file-based-destination-testing-overview.md)
            * [Générer des exemples de profils en fonction d’un schéma source](./destination-sdk/file-based-sample-profile-generation-api.md)
            * [Test de votre destination basée sur des fichiers avec des exemples de profils](./destination-sdk/file-based-destination-testing-api.md)
            * [Affichage des résultats détaillés de l’activation](./destination-sdk/file-based-destination-results-api.md)
            * [Validation des champs de client modélisés](./destination-sdk/file-based-render-template-api.md)
   * Guides {#guides}
      * [Utiliser Destination SDK pour configurer une destination de diffusion en continu](./destination-sdk/configure-destination-instructions.md)
      * [(Version Beta) Utilisez Destination SDK pour configurer une destination basée sur des fichiers.](./destination-sdk/configure-file-based-destination-instructions.md)
      * [Envoyer pour révision une destination créée dans Destination SDK](./destination-sdk/submit-destination.md)
   * Référence {#reference}
      * [Limitation de débit et stratégie de reprise pour les destinations de diffusion en continu](./destination-sdk/rate-limiting-retry-policy.md)
      * [Fonctions de transformation prises en charge](./destination-sdk/supported-functions.md)
   * Documenter votre destination {#document-destination}
      * [Documenter votre destination dans Adobe Experience Platform](./destination-sdk/docs-framework/documentation-instructions.md)
      * [Utiliser l’interface web GitHub pour créer une page de documentation de destination](./destination-sdk/docs-framework/use-github-interface-to-create-documentation.md)
      * [Utiliser un éditeur de texte dans votre environnement local pour créer une page de documentation de destination](./destination-sdk/docs-framework/work-in-local-environment.md)
      * [Modèle de libre-service de documentation](./destination-sdk/docs-framework/self-service-template.md)
      * [Bonnes pratiques de création](./destination-sdk/docs-framework/authoring-best-practices.md)
* [Questions fréquentes](./destinations-faq.md)
* [Notes de mise à jour de Platform](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html?lang=fr)
