---
keywords: destinations ; questions ; questions fréquentes; faq; faq destinations
title: FAQ sur les destinations
seo-title: FAQ sur les destinations
description: Réponses aux questions les plus fréquentes sur les destinations Adobe Experience Platform
seo-description: Réponses aux questions les plus fréquentes sur les destinations Adobe Experience Platform
source-git-commit: 61678c5a62980cdb81714420016b7c4b2093f5c6
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 12%

---


# FAQ sur les destinations {#faq}

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**Que dois-je faire avant de pouvoir activer les audiences dans  [!DNL Facebook Custom Audiences]?**

Avant d’envoyer vos segments ciblés à [!DNL Facebook], assurez-vous de respecter les conditions suivantes :

* L&#39;autorisation **[!DNL Manage campaigns]** doit être activée pour votre compte d&#39;utilisateur [!DNL Facebook] pour le compte d&#39;annonce que vous prévoyez d&#39;utiliser.
* Le compte commercial **Adobe Experience Cloud** doit être ajouté en tant que partenaire publicitaire dans votre [!DNL Facebook Ad Account]. Utilisez `business ID=206617933627973`. Pour plus d&#39;informations, consultez [Ajouter des partenaires à votre gestionnaire d&#39;entreprise](https://www.facebook.com/business/help/1717412048538897) dans la documentation de Facebook.
   >[!IMPORTANT]
   >
   > Lors de la configuration des autorisations pour Adobe Experience Cloud, vous devez activer l’autorisation **Gérer des campagnes**. Ceci est obligatoire pour l’intégration de la [!DNL Adobe Experience Platform].
* Lisez et signez les Conditions d’utilisation [!DNL Facebook Custom Audiences]. Pour ce faire, accédez à `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, où `accountID` est votre [!DNL Facebook Ad Account ID].

**Dois-je ajouter des applications ou des pixels à mon compte  [!DNL Facebook] publicitaire ?**

Non. Comme il ne s’agit pas d’une intégration basée sur les pixels, il n’est pas nécessaire d’ajouter des pixels à votre compte publicitaire.

**Combien de temps Facebook prend-il pour traiter les informations de Adobe Experience Platform ?**

En mars 2021, [!DNL Facebook Custom Audiences] a besoin d&#39;une heure pour traiter les informations reçues de [!DNL Platform].

**Puis-je utiliser  [!DNL Facebook Custom Audiences] le ciblage des audiences dans d’autres  [!DNL Facebook] applications, par exemple  [!DNL Instagram]?**

Vous pouvez utiliser la destination [!DNL Facebook Custom Audiences] pour le ciblage des audiences dans la famille Facebook d’applications prises en charge par [!DNL Facebook Custom Audiences], y compris [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] et [!DNL Messenger]. La sélection de l&#39;application sur laquelle les annonceurs souhaitent exécuter des campagnes est indiquée au niveau de l&#39;emplacement dans [!DNL Facebook Ads Manager].

**Quelle est la différence entre la  [!DNL Facebook Custom Audiences] connexion et l&#39; [!DNL Facebook Pixel] extension ?**

La connexion [!DNL Facebook Custom Audiences] utilise les identités [!DNL Platform] lors de l&#39;envoi d&#39;audiences à [!DNL Facebook], tandis que la connexion [[!DNL Facebook Pixel] ](../destinations/catalog/advertising/facebook-pixel.md) utilise le pixel [!DNL Facebook] intégré dans un site Web.

Ces deux intégrations sont complémentaires ; vous pouvez utiliser les deux pour assurer une meilleure couverture d’audience. Par exemple, vous pouvez utiliser l&#39;extension [!DNL Facebook Pixel] pour la prospection de visiteurs de site Web qui n&#39;ont pas créé de compte, alors que [!DNL Facebook Custom Audiences] peut vous aider à cible des clients existants, en fonction d&#39;identités [!DNL Platform].

**L&#39;intégration Adobe Experience Platform avec  [!DNL Facebook Custom Audiences] prise en charge exclut-elle les utilisateurs d&#39;une audience alors qu&#39;ils ne sont plus éligibles ?**

Oui, l’intégration prend en charge la suppression des utilisateurs de [!DNL Facebook Custom Audiences] lorsqu’ils ne sont plus éligibles.

**Comment puis-je hacher les données d&#39;audience avant de les envoyer à  [!DNL Facebook]?**

[!DNL Facebook] exige qu’aucune information d’identification personnelle (identification personnelle) ne soit envoyée en clair. Par conséquent, les audiences activées pour [!DNL Facebook] peuvent être masquées par des identifiants *hachés*, tels que des adresses électroniques ou des numéros de téléphone.

Pour obtenir des explications détaillées sur les exigences de correspondance d’ID, voir [Exigences de correspondance d’ID](catalog/social/facebook.md#id-matching-requirements).

**Dans quel type d&#39;identité puis-je activer  [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] prend en charge l’activation des identités suivantes : e-mails hachés, numéros de téléphone hachés,  [!DNL GAID] [!DNL IDFA]et identifiants externes personnalisés.

## audiences linkedIn Matched {#linkedin}

**Dois-je ajouter des applications ou des pixels à mon compte  [!DNL LinkedIn] publicitaire ?**

Non. Comme il ne s’agit pas d’une intégration basée sur les pixels, il n’est pas nécessaire d’ajouter des pixels à votre compte publicitaire.

**Que dois-je faire avant de pouvoir activer les audiences dans  [!DNL LinkedIn Matched Audiences]?**

Avant d’utiliser la destination [!UICONTROL Audience LinkedIn Matched], assurez-vous que votre compte [!DNL LinkedIn Campaign Manager] a le niveau d’autorisation [!DNL Creative Manager] ou supérieur.

Pour savoir comment modifier vos [!DNL LinkedIn Campaign Manager] autorisations d&#39;utilisateur, voir [Ajouter, modifier et supprimer des autorisations d&#39;utilisateur sur des comptes de publicité](https://www.linkedin.com/help/lms/answer/5753) dans la documentation LinkedIn.

**Comment puis-je hacher les données d&#39;audience avant de les envoyer à  [!DNL LinkedIn]?**

[!DNL LinkedIn] exige qu’aucune information d’identification personnelle (identification personnelle) ne soit envoyée en clair. Par conséquent, les audiences activées pour [!DNL LinkedIn] peuvent être masquées par des identifiants *hachés*, tels que des adresses électroniques ou des numéros de téléphone.

Pour obtenir des explications détaillées sur les exigences de correspondance d’ID, voir [Exigences de correspondance d’ID](catalog/social/linkedin.md#id-matching-requirements).

**Dans quel type d&#39;identité puis-je activer  [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] prend en charge l’activation des identités suivantes : courriers électroniques hachés,  [!DNL GAID]et  [!DNL IDFA].
