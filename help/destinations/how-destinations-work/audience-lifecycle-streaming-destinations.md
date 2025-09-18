---
title: Cycle de vie des audiences dans les destinations Experience Platform et de streaming
description: Découvrez comment les noms d’audience et les mappages d’Experience Platform sont pris en compte dans les plateformes de destination de diffusion en streaming.
source-git-commit: 6b4dfa714e078fb5b97900811aade081ffef0d78
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 3%

---


# Cycle de vie des audiences dans les destinations de diffusion en streaming

Cette page décrit comment les mises à jour et les mappages des noms d’audience dans Experience Platform sont synchronisés avec les plateformes de destination de diffusion en streaming. Lorsque vous modifiez les noms d’audience ou supprimez les mappages d’audience dans Experience Platform, le comportement varie en fonction des fonctionnalités de la plateforme de destination.

Il est important de comprendre ces différences pour gérer les opérations de cycle de vie des audiences et vous assurer que vos plateformes de destination reflètent l’état actuel de vos audiences dans Experience Platform.

## Comportement de propagation du nom de l’audience {#audience-name-propagation}

Lorsque vous activez une audience vers une destination de diffusion en continu, le nom de l’audience est envoyé à la destination au cours de l’activation initiale. Cependant, le comportement de mise à jour du nom de l’audience varie selon la destination :

* **[Destinations prenant en charge les mises à jour de nom d’audience](#name-update-supported)** : si vous modifiez le nom d’une audience dans Experience Platform, le nom mis à jour se propage automatiquement vers ces destinations.
* **[Destinations qui ne prennent pas en charge les mises à jour des noms d’audience](#name-update-not-supported)** : si vous modifiez le nom d’une audience dans Experience Platform, la destination continuera à utiliser le nom d’origine de l’activation initiale.

### Destinations prenant en charge les mises à jour des noms d’audience {#name-update-supported}

Les destinations de diffusion en continu suivantes prennent en charge les mises à jour automatiques des noms d’audience lorsque vous modifiez les noms d’audience dans Experience Platform :

* [Connexion à l’audience Acxiom](../catalog/advertising/acxiom-audience-connection.md)
* [Adobe Campaign Managed Cloud](../catalog/email-marketing/adobe-campaign-managed-services.md)
* [Advertising Cloud DSP](../catalog/advertising/adobe-advertising-cloud-connection.md)
* [Bombora](../catalog/advertising/bombora.md)
* [Criteo](../catalog/advertising/criteo.md)
* [Demandbase](../catalog/advertising/demandbase.md)
* [Demandbase People](../catalog/advertising/demandbase-people.md)
* [Audiences Experience Cloud](../catalog/adobe/experience-cloud-audiences.md)
* [Audience personnalisée Facebook](../catalog/social/facebook.md)
* [Gainsight PX](../catalog/analytics/gainsight-px.md)
* [LINE](../catalog/mobile-engagement/line.md)
* [(Entreprises) LinkedIn Matched Audience](../catalog/social/linkedin-b2b.md)
* [Audience appariée LinkedIn](../catalog/social/linkedin.md)
* [(Hérité) (V2) Marketo Engage](../catalog/adobe/marketo-engage.md)
* [PubMatic Connect](../catalog/advertising/pubmatic.md)
* [SendGrid](../catalog/email-marketing/sendgrid.md)
* [Snap Inc](../catalog/advertising/snap-inc.md)
* [TikTok](../catalog/social/tiktok.md)
* [Audiences personnalisées Twitter](../catalog/social/twitter.md)
* [Yahoo DataX](../catalog/advertising/datax.md)

### Destinations qui ne prennent pas en charge les mises à jour des noms d’audience {#name-update-not-supported}

Pour les destinations non répertoriées ci-dessus, les noms d’audience restent statiques après l’activation initiale. Si vous devez mettre à jour le nom d’une audience pour ces destinations, vous devez :

1. Créez une nouvelle audience dans Experience Platform avec le nom souhaité.
2. Activer la nouvelle audience vers la destination

>[!TIP]
>
>Pour éviter toute confusion, utilisez des noms d’audience descriptifs dès la première activation, en particulier lors de l’activation vers des destinations qui ne prennent pas en charge les mises à jour des noms d’audience.

## Destinations qui prennent en charge la suppression d’audience {#support-removal}

Lorsque vous supprimez (annulez le mappage) une audience d’une destination de diffusion en continu, Experience Platform tente de supprimer l’audience correspondante de la plateforme de destination. Cependant, toutes les destinations ne prennent pas en charge cette fonctionnalité.

Les destinations de diffusion en continu suivantes prennent en charge la suppression automatique d’audience lorsque vous démappez une audience de la destination :

* [(API) Oracle Eloqua](../catalog/email-marketing/oracle-eloqua-api.md)
* [(Entreprises) LinkedIn Matched Audience](../catalog/social/linkedin-b2b.md)
* [(Hérité) (V2) Marketo Engage](../catalog/adobe/marketo-engage.md)
* [Adobe Advertising Cloud DSP](../catalog/advertising/adobe-advertising-cloud-connection.md)
* [Audiences du compte Bombora](../catalog/advertising/bombora.md)
* [Criteo](../catalog/advertising/criteo.md)
* [Audiences Experience Cloud](../catalog/adobe/experience-cloud-audiences.md)
* [Facebook](../catalog/social/facebook.md)
* [Gainsight PX](../catalog/analytics/gainsight-px.md)
* [HubSpot](../catalog/crm/hubspot.md)
* [LINE](../catalog/mobile-engagement/line.md)
* [Audiences correspondantes LinkedIn](../catalog/social/linkedin.md)
* [LiveRamp - Distribution](../catalog/advertising/liveramp-distribution.md)
* [Catégories d’intérêt Mailchimp](../catalog/email-marketing/mailchimp-interest-categories.md)
* [PubMatic Connect](../catalog/advertising/pubmatic.md)
* [Engagement du compte Salesforce Marketing Cloud](../catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md)
* [SendGrid](../catalog/email-marketing/sendgrid.md)
* [Snap Inc](../catalog/advertising/snap-inc.md)
* [TikTok](../catalog/social/tiktok.md)
* [Audiences personnalisées Twitter](../catalog/social/twitter.md)
* [Yahoo DataX](../catalog/advertising/datax.md)

### Destinations qui ne prennent pas en charge la suppression d’audience

Pour les destinations non répertoriées ci-dessus, lorsque vous annulez le mappage d’une audience à la destination, Experience Platform supprime uniquement le mappage. L’audience de la plateforme de destination reste active jusqu’à ce que vous la supprimiez manuellement dans la plateforme du partenaire.
