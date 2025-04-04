---
keywords: destinations ; questions ; questions fréquentes ; faq ; faq sur les destinations
title: Questions fréquentes
description: Réponses aux questions les plus fréquemment posées sur les destinations Adobe Experience Platform
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1675'
ht-degree: 3%

---

# Questions fréquentes {#faq}

## Vue d’ensemble {#overview}

Ce document fournit des réponses aux questions fréquentes sur les destinations Adobe Experience Platform. Pour toute question ou dépannage concernant d’autres services [!DNL Experience Platform], y compris ceux rencontrés sur toutes les API [!DNL Experience Platform], consultez le [guide de dépannage d’Experience Platform](../landing/troubleshooting.md).

## Questions générales sur les destinations {#general}

### Pourquoi est-ce que je vois différents nombres de profils dans l’interface utilisateur d’Experience Platform et dans les fichiers CSV exportés ?

+++Réponse
Il s’agit d’un comportement normal en raison de la manière dont Experience Platform effectue la segmentation.

La segmentation en flux continu met à jour le nombre de profils pour les audiences en flux continu tout au long de la journée, tandis que la segmentation par lots met à jour le nombre de profils pour les audiences par lots une fois toutes les 24 heures.

Lorsque le planning d’exportation de l’audience diffère du planning de segmentation, le nombre de profils entre l’interface utilisateur et le fichier [!DNL CSV] exporté sera différent, en particulier en ce qui concerne les audiences en flux continu.

Pour plus d’informations, consultez la [documentation du service de segmentation](../segmentation/home.md).
+++

### Pourquoi les taux de correspondance sont-ils faibles lors de la désactivation et de la réactivation d’une audience mise à jour vers la même destination ?

+++Réponse

La désactivation et la suppression d’une audience d’une destination de diffusion en streaming ne déclenchent pas de renvoi lors de la réactivation de l’audience vers la même destination de diffusion en streaming.

**Exemple**

Vous avez activé une audience composée de 10 profils vers une destination de diffusion en continu.

Après l’activation de l’audience, vous réalisez que vous souhaitez modifier la configuration de l’audience. Vous désactivez donc l’audience et modifiez ses critères de population, ce qui entraîne une population d’audience de 100 profils.

Vous réactivez l’audience mise à jour vers la même destination, mais comme aucun renvoi n’est déclenché, votre destination ne reçoit pas les 90 profils supplémentaires.

**Solution**

Pour vous assurer que tous les profils sont envoyés à votre destination, vous devez créer une nouvelle audience avec la nouvelle configuration, puis l’activer vers votre destination.

+++

### Lorsqu’une audience est supprimée d’une destination, un signal est-il envoyé à la destination pour indiquer que l’audience est supprimée ?

+++Réponse

Non, il n’existe aucune dépendance entre la destination Experience Platform et l’instance cliente du système cible. Du côté de la réception, la seule indication que le système cible verrait est qu’il a cessé de recevoir ces données d’audience.

+++

<!--
## [!DNL Experience Cloud Audiences] {#eca-faq}

### What are the differences between the Experience Cloud Audiences and Adobe Target destinations?

+++Answer

See the table below for a feature comparison between the Experience Cloud Audiences and Adobe Target destinations.

||Experience Cloud Audiences|Adobe Target|
|---|---|---|
| **Supported Experience Cloud apps** | Supports audience activation to Audience Manager, Adobe Target, Adobe Analytics, Advertising Cloud, Marketo, Adobe Campaign | Supports audience activation only to Adobe Target |
| **Supports audience activation** | ✓ | ✓ |
| **Supports attribute activation** | X | ✓ |
| **Latency** | Profiles begin activating in 6 hours. Full population is visible in 48 hours​. |Depends on implementation​ type. <ul><li>Web SDK enables same-page/next-page​ personalization.</li><li>AT.js enables next-session personalization.</li></ul> |
| **DULE support** | ✓ | ✓ |
| **Marketing actions support** | ✓ | ✓ |
| **Supported IDs** | [!DNL ECID], [!DNL GAID], [!DNL IDFA], [!DNL email_lc_sha256] | Any ID type |
| **Sandbox support** | One sandbox | Multiple sandboxes |
| **Consent support** | X | Yes. Requires Privacy & Security Shield. |
| **Edge segmentation support** | Supports activation of edge audiences. Does not support edge segmentation. | Supports edge segmentation and activation of edge audiences. |
| **Supported audiences** | All types of audiences  | Edge merge policy required for activation.|

+++

-->

## [!DNL Facebook Custom Audiences] {#facebook-faq}

### Que dois-je faire avant de pouvoir activer des audiences dans [!DNL Facebook Custom Audiences] ?

+++Réponse
Avant d’envoyer vos audiences à [!DNL Facebook], veillez à respecter les exigences suivantes :

* L’autorisation **[!DNL Manage campaigns]** doit être activée pour votre compte utilisateur [!DNL Facebook] pour le compte publicitaire que vous prévoyez d’utiliser.
* Le compte professionnel **Adobe Experience Cloud** doit être ajouté en tant que partenaire publicitaire dans votre [!DNL Facebook Ad Account]. Utilisez `business ID=206617933627973`. Voir [Ajouter des partenaires à votre Business Manager](https://www.facebook.com/business/help/1717412048538897) dans la documentation Facebook pour plus d’informations.

  >[!IMPORTANT]
  >
  > Lors de la configuration des autorisations pour Adobe Experience Cloud, vous devez activer l’autorisation **Gérer des campagnes**. Ceci est obligatoire pour l’intégration de la [!DNL Adobe Experience Platform].
* Lisez et signez les Conditions d’utilisation [!DNL Facebook Custom Audiences]. Pour ce faire, accédez à `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, où `accountID` est votre [!DNL Facebook Ad Account ID].
+++

### Dois-je ajouter des applications ou des pixels à mon compte publicitaire [!DNL Facebook] ?

+++Réponse
Non. Comme il ne s’agit pas d’une intégration basée sur les pixels, il n’est pas nécessaire d’ajouter des pixels à votre compte d’annonceur.
+++

### Combien de temps Facebook prend-il pour traiter les informations provenant de Adobe Experience Platform ?

+++Réponse
Depuis mars 2021, [!DNL Facebook Custom Audiences] a besoin d’une heure pour traiter les informations reçues de [!DNL Experience Platform].
+++

### Puis-je utiliser [!DNL Facebook Custom Audiences] pour le ciblage d’audience dans d’autres applications [!DNL Facebook], telles que [!DNL Instagram] ?

+++Réponse
Vous pouvez utiliser la destination [!DNL Facebook Custom Audiences] pour le ciblage d’audience dans la famille d’applications de Facebook prises en charge par [!DNL Facebook Custom Audiences], notamment [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] et [!DNL Messenger]. La sélection de l’application sur laquelle les annonceurs souhaitent exécuter des campagnes est indiquée au niveau de l’emplacement dans [!DNL Facebook Ads Manager].
+++

### Quelle est la différence entre la connexion [!DNL Facebook Custom Audiences] et l’extension [!DNL Facebook Pixel] ?

+++Réponse
La connexion [!DNL Facebook Custom Audiences] utilise des identités [!DNL Experience Platform] lors de l’envoi d’audiences à [!DNL Facebook], tandis que la [[!DNL Facebook Pixel] connexion](../destinations/catalog/advertising/facebook-pixel.md) utilise le pixel [!DNL Facebook] intégré à un site web.

Ces deux intégrations sont complémentaires. Vous pouvez les utiliser afin d’assurer une meilleure couverture de l’audience. Par exemple, vous pouvez utiliser l’extension [!DNL Facebook Pixel] pour prospecter les visiteurs et visiteuses de sites Web qui n’ont pas créé de compte, tandis que [!DNL Facebook Custom Audiences] pouvez vous aider à cibler les clientes et clients existants en fonction d’identités [!DNL Experience Platform].
+++

### L’intégration de Adobe Experience Platform à [!DNL Facebook Custom Audiences] prend-elle en charge la disqualification des utilisateurs d’une audience lorsqu’ils ne sont plus qualifiés pour celle-ci ?**

+++Réponse
Oui, l’intégration prend en charge la suppression d’utilisateurs d’[!DNL Facebook Custom Audiences] lorsqu’ils ne sont plus qualifiés.
+++

### Comment dois-je hacher les données de l’audience avant de les envoyer à [!DNL Facebook] ?

+++Réponse
[!DNL Facebook] nécessite qu’aucune information d’identification personnelle (PII) ne soit envoyée en clair. Par conséquent, les audiences activées pour [!DNL Facebook] peuvent être masquées à partir d’identifiants *hachés* tels que des adresses e-mail ou des numéros de téléphone.

Pour des explications détaillées sur les exigences de correspondance des identifiants, voir [Exigences de correspondance des identifiants](catalog/social/facebook.md#id-matching-requirements).
+++

### Quels types d’identités puis-je activer dans [!DNL Facebook Custom Audiences] ?

+++Réponse
[!DNL Facebook Custom Audiences] prend en charge l’activation des identités suivantes : e-mails hachés, numéros de téléphone hachés, [!DNL GAID], [!DNL IDFA] et identifiants externes personnalisés.
+++

### Puis-je créer plusieurs destinations Facebook dans l’interface utilisateur d’Experience Platform pour des comptes Facebook distincts ?

+++Réponse
Oui. Une destination Facebook dans Experience Platform est 1:1 pour un compte publicitaire dans Facebook. Vous pouvez créer une destination Facebook distincte pour chaque compte publicitaire Facebook de votre entreprise. Suivez le [tutoriel de connexion à la destination](/help/destinations/ui/connect-destination.md) et connectez-vous à un compte Facebook distinct pour chaque nouvelle destination Facebook dans l’interface utilisateur d’Experience Platform. Le nombre de comptes publicitaires Facebook auxquels vous pouvez vous connecter n’est pas limité.
+++

## Ciblage par liste de clients Google {#google-customer-match}

### Lors de l’exportation d’audiences vers Google Customer Match, pourquoi des nombres supplémentaires sont-ils ajoutés à la fin des noms d’audience dans l’interface de Google ?

+++Réponse
Google exige que les noms d’audience soient uniques. Les nombres affichés sont des [horodatages UNIX](https://www.unixtimestamp.com/) et ils sont ajoutés pour que les noms des audiences restent uniques, si vous avez mappé la même audience à plusieurs destinations Google.
+++

## Audiences correspondantes LinkedIn {#linkedin}

### Dois-je ajouter des applications ou des pixels à mon compte publicitaire [!DNL LinkedIn] ?

+++Réponse
Non. Comme il ne s’agit pas d’une intégration basée sur les pixels, il n’est pas nécessaire d’ajouter des pixels à votre compte d’annonceur.
+++

### Que dois-je faire avant de pouvoir activer des audiences dans [!DNL LinkedIn Matched Audiences] ?

+++Réponse
Avant de pouvoir utiliser la destination [!UICONTROL Audience appariée LinkedIn], assurez-vous que votre compte [!DNL LinkedIn Campaign Manager] dispose du niveau d’autorisation [!DNL Creative Manager] ou supérieur.

Pour savoir comment modifier vos autorisations d’utilisateur [!DNL LinkedIn Campaign Manager], voir [Ajouter, modifier et supprimer des autorisations d’utilisateur sur les comptes Advertising](https://www.linkedin.com/help/lms/answer/5753) dans la documentation LinkedIn.
+++

### Comment dois-je hacher les données de l’audience avant de les envoyer à [!DNL LinkedIn] ?

+++Réponse
[!DNL LinkedIn] nécessite qu’aucune information d’identification personnelle (PII) ne soit envoyée en clair. Par conséquent, les audiences activées pour [!DNL LinkedIn] peuvent être masquées à partir d’identifiants *hachés* tels que des adresses e-mail ou des numéros de téléphone.

Pour des explications détaillées sur les exigences de correspondance des identifiants, voir [Exigences de correspondance des identifiants](catalog/social/linkedin.md#id-matching-requirements).
+++

### Quels types d’identités puis-je activer dans [!DNL LinkedIn] ?

+++Réponse
[!DNL LinkedIn Matched Audiences] prend en charge l’activation des identités suivantes : e-mails hachés, [!DNL GAID] et [!DNL IDFA].

+++

## Personnalisation de la même page et de la page suivante via les destinations Adobe Target et Personalization personnalisé {#same-next-page-personalization}

### Dois-je utiliser Experience Platform Web SDK pour envoyer des audiences et des attributs à Adobe Target ?

+++Réponse
Non, [Web SDK](../web-sdk/home.md) n’est pas nécessaire pour activer les audiences dans [Adobe Target](catalog/personalization/adobe-target-connection.md).

Cependant, si [[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html) est utilisé à la place de Web SDK, seule la personnalisation de session suivante est prise en charge.

Pour les cas d’utilisation de [personnalisation de la même page et de la page suivante](ui/activate-edge-personalization-destinations.md) vous devez utiliser [Web SDK](../web-sdk/home.md) ou l’[API du serveur Edge Network](../server-api/overview.md). Pour plus d’informations sur l’implémentation](ui/activate-edge-personalization-destinations.md) consultez la documentation sur l’[activation des audiences vers des destinations Edge.
+++

### Y a-t-il une limite au nombre d’attributs que je peux envoyer de Real-time Customer Data Platform vers Adobe Target ou une destination Personalization personnalisée ?

+++Réponse
Oui, les cas d’utilisation de la personnalisation de la même page et de la page suivante prennent en charge un maximum de 30 attributs par sandbox, lors de l’activation d’audiences vers des destinations Adobe Target ou Custom Personalization. Pour plus d’informations sur les mécanismes de sécurisation d’activation, consultez la [documentation sur les mécanismes de sécurisation](guardrails.md#edge-destinations-activation).
+++

### Quels types d’attributs sont pris en charge pour l’activation (par exemple, tableaux, mappages, etc.) ?

+++Réponse
Actuellement, seuls les attributs statiques à une seule valeur sont pris en charge, tels que `person.name.firstName`. Les attributs de tableau ne sont actuellement pas pris en charge.
+++

<!-- **Is there a limit on the number of audiences that can be activated to Adobe Target and Custom Personalization destinations?**

Yes, you can activate a maximum of 150 edge audiences per sandbox.  For more information on activation guardrails, see the [default guardrails for activation](guardrails.md#edge-destinations-activation). -->

### Après la création d’une audience dans Experience Platform, combien de temps faudra-t-il pour que cette audience soit disponible pour les cas d’utilisation de segmentation Edge ?

+++Réponse
Les définitions d’audience sont propagées à [Edge Network](../web-sdk/home.md) en une heure maximum. Cependant, si une audience est activée au cours de cette première heure, certains visiteurs qui se seraient qualifiés pour l’audience peuvent être manqués.
+++

### Où puis-je voir les attributs activés dans Adobe Target ?

+++Réponse
Les attributs pourront être utilisés dans Target dans les offres [JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html) et [HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html).
+++

### Puis-je créer une destination sans flux de données, puis ajouter un flux de données à la même destination à un moment ultérieur ?

+++Réponse
Actuellement, cela n’est pas pris en charge par l’interface utilisateur des destinations. Si vous avez besoin d’aide dans ce cas, contactez votre représentant ou représentante Adobe.
+++

### Que se passe-t-il si je supprime une destination Adobe Target ?

+++Réponse
Lorsque vous supprimez une destination, toutes les audiences et tous les attributs mappés sous la destination sont supprimés d’Adobe Target et ils sont également supprimés d’Edge Network.
+++

### L’intégration fonctionne-t-elle à l’aide de l’API du serveur Edge Network ?

+++Réponse
Oui, l’API du serveur Edge Network fonctionne avec la destination Personalization personnalisée. Les attributs de profil pouvant contenir des données sensibles, la destination Custom Personalization requiert, pour protéger ces données, que vous utilisiez l’API du serveur Edge Network pour la collecte de données. En outre, tous les appels API doivent être effectués dans un [contexte authentifié](../server-api/authentication.md).
+++

### Je ne peux avoir qu’une seule politique de fusion Active-On-Edge (active sur le bord). Puis-je créer des audiences qui utilisent une autre politique de fusion et les envoyer quand même à Adobe Target en tant qu’audiences de diffusion en continu ?

+++Réponse
Non. Toutes les audiences que vous souhaitez activer dans Adobe Target doivent utiliser une politique de fusion Active-On-Edge [active-on-Edge](../profile/merge-policies/ui-guide.md).
+++

### Les politiques DULE (Data Usage Labeling and Enforcement) et de consentement sont-elles appliquées ?

+++Réponse
Oui. Les [politiques de gouvernance des données et de consentement](../data-governance/home.md) créées et associées aux actions marketing sélectionnées régissent l’activation des attributs sélectionnés.
+++

### Les destinations [!DNL Adobe Target] et [!DNL Custom Personalization] sont-elles conformes au [!DNL HIPAA] ?

+++Réponse
[!DNL Adobe Target] n’est pas [!DNL HIPPA] conforme à [[!DNL Adobe Healthcare Shield]](https://business.adobe.com/solutions/industries/healthcare.html). Les clients doivent consulter leurs propres équipes juridiques pour en savoir plus sur la préparation du [!DNL HIPPA] aux canaux d’optimisation personnalisés avant d’utiliser la personnalisation Edge via [!DNL Adobe Target] ou les destinations [!DNL Custom Personalization].

Pour les cas d’utilisation où la gestion des politiques de consentement doit être appliquée à grande échelle, les clients doivent acheter des [!DNL Adobe Privacy & Security Shield]. [!DNL Adobe Privacy & Security Shield] fonctionnalités sont vendues en tant que suite avancée de fonctionnalités et ne peuvent pas être achetées séparément.

Ce service comprend des clés gérées par le client et des seuils élevés pour gérer le cycle de vie des données client.

Les destinations [!DNL Adobe Target] et [!DNL Custom Personalization] sont intégrées aux [libellés d’utilisation des données Experience Platform](../data-governance/labels/overview.md) et au [service d’application de la politique de consentement](../data-governance/enforcement/overview.md). Ces fonctionnalités sont disponibles pour tous les clients.




+++

