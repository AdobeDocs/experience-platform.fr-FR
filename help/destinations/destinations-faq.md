---
keywords: les destinations ; questions; aux questions fréquentes; faq; faq sur les destinations
title: Questions fréquentes
seo-title: 'Questions fréquemment posées '
description: Réponses aux questions les plus fréquemment posées sur les destinations Adobe Experience Platform
seo-description: Réponses aux questions les plus fréquemment posées sur les destinations Adobe Experience Platform
source-git-commit: a01b53758f4ad42272c39f71a08021d30900e7af
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 11%

---


# Questions fréquemment posées {#faq}

## Présentation {#overview}

Ce document répond aux questions les plus fréquemment posées sur les destinations Adobe Experience Platform. Pour toute question ou dépannage concernant d’autres services [!DNL Platform], y compris ceux rencontrés sur toutes les API [!DNL Platform], reportez-vous au [guide de dépannage Experience Platform](../landing/troubleshooting.md).

## Questions générales sur les destinations {#general}

**Pourquoi vois-je différents nombres de profils dans l’interface utilisateur de l’Experience Platform et dans les fichiers CSV exportés ?**

Il s’agit d’un comportement normal en raison de la manière dont Experience Platform effectue la segmentation.

La segmentation par flux met à jour le nombre de profils pour les segments en continu toute la journée, tandis que la segmentation par lots met à jour le nombre de profils pour les segments par lot une fois toutes les 24 heures.

Lorsque le planning d’exportation de segments diffère du planning de segmentation, le nombre de profils entre l’interface utilisateur et le fichier [!DNL CSV] exporté sera différent, en particulier en ce qui concerne les segments en continu.

Pour plus d’informations, voir la [documentation Segmentation Service](../segmentation/home.md) .

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**Que dois-je faire avant d’activer les audiences dans  [!DNL Facebook Custom Audiences] ?**

Avant d’envoyer vos segments ciblés à [!DNL Facebook], assurez-vous de respecter les conditions suivantes :

* L’autorisation [!DNL Facebook] doit être activée pour votre compte utilisateur **[!DNL Manage campaigns]** pour le compte publicitaire que vous prévoyez d’utiliser.
* Le compte commercial **Adobe Experience Cloud** doit être ajouté en tant que partenaire publicitaire dans votre [!DNL Facebook Ad Account]. Utilisez `business ID=206617933627973`. Pour plus d’informations, voir [Ajout de partenaires à votre compte Business Manager](https://www.facebook.com/business/help/1717412048538897) dans la documentation Facebook.
   >[!IMPORTANT]
   >
   > Lors de la configuration des autorisations pour Adobe Experience Cloud, vous devez activer l’autorisation **Gérer des campagnes**. Ceci est obligatoire pour l’intégration de la [!DNL Adobe Experience Platform].
* Lisez et signez les Conditions d’utilisation [!DNL Facebook Custom Audiences]. Pour ce faire, accédez à `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, où `accountID` est votre [!DNL Facebook Ad Account ID].

**Dois-je ajouter des applications ou des pixels à mon compte  [!DNL Facebook] publicitaire ?**

Non. Puisqu’il ne s’agit pas d’une intégration basée sur les pixels, il n’est pas nécessaire d’ajouter des pixels à votre compte publicitaire.

**Combien de temps prend Facebook pour traiter les informations de Adobe Experience Platform ?**

En mars 2021, [!DNL Facebook Custom Audiences] doit prendre jusqu’à une heure pour traiter les informations reçues de [!DNL Platform].

**Puis-je utiliser  [!DNL Facebook Custom Audiences] pour le ciblage des audiences dans d’autres  [!DNL Facebook] applications, par exemple  [!DNL Instagram]?**

Vous pouvez utiliser la destination [!DNL Facebook Custom Audiences] pour le ciblage des audiences dans la famille Facebook d’applications prises en charge par [!DNL Facebook Custom Audiences], y compris [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] et [!DNL Messenger]. La sélection de l’application sur laquelle les annonceurs souhaitent exécuter des campagnes est indiquée au niveau de l’emplacement dans [!DNL Facebook Ads Manager].

**Quelle est la différence entre la  [!DNL Facebook Custom Audiences] connexion et l’ [!DNL Facebook Pixel] extension ?**

La connexion [!DNL Facebook Custom Audiences] utilise les identités [!DNL Platform] lors de l’envoi d’audiences à [!DNL Facebook], tandis que la connexion [[!DNL Facebook Pixel] a4/> utilise le pixel [!DNL Facebook] intégré à un site web.](../destinations/catalog/advertising/facebook-pixel.md)

Ces deux intégrations sont complémentaires ; vous pouvez utiliser les deux pour assurer une meilleure couverture d’audience. À titre d’exemple, vous pouvez utiliser l’extension [!DNL Facebook Pixel] pour la prospection des visiteurs d’un site web qui n’ont pas créé de compte, tandis que [!DNL Facebook Custom Audiences] peut vous aider à cibler les clients existants, en fonction des identités [!DNL Platform].

**L’intégration de Adobe Experience Platform avec la  [!DNL Facebook Custom Audiences] prise en charge disqualifie-t-elle les utilisateurs d’une audience lorsqu’ils ne remplissent plus les critères ?**

Oui, l’intégration prend en charge la suppression des utilisateurs de [!DNL Facebook Custom Audiences] lorsqu’ils ne remplissent plus les critères.

**Comment dois-je hacher les données d’audience avant de les envoyer à  [!DNL Facebook]?**

[!DNL Facebook] exige qu’aucune information d’identification personnelle (PII) ne soit envoyée clairement. Par conséquent, les audiences activées vers [!DNL Facebook] peuvent être masquées à partir des identifiants *hachés*, tels que les adresses électroniques ou les numéros de téléphone.

Pour obtenir des explications détaillées sur les exigences de correspondance des ID, voir [Exigences de correspondance des ID](catalog/social/facebook.md#id-matching-requirements).

**Dans quel type d’identités puis-je activer  [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] prend en charge l’activation des identités suivantes : e-mails hachés, numéros de téléphone hachés,  [!DNL GAID],  [!DNL IDFA] et identifiants externes personnalisés.

## Audiences mappées linkedIn {#linkedin}

**Dois-je ajouter des applications ou des pixels à mon compte  [!DNL LinkedIn] publicitaire ?**

Non. Puisqu’il ne s’agit pas d’une intégration basée sur les pixels, il n’est pas nécessaire d’ajouter des pixels à votre compte publicitaire.

**Que dois-je faire avant d’activer les audiences dans  [!DNL LinkedIn Matched Audiences] ?**

Avant de pouvoir utiliser la destination [!UICONTROL Audience mise en correspondance LinkedIn], assurez-vous que votre compte [!DNL LinkedIn Campaign Manager] a le niveau d’autorisation [!DNL Creative Manager] ou supérieur.

Pour savoir comment modifier vos [!DNL LinkedIn Campaign Manager] autorisations d’utilisateur, voir [Ajout, modification et suppression des autorisations d’utilisateur sur les comptes Advertising](https://www.linkedin.com/help/lms/answer/5753) dans la documentation LinkedIn.

**Comment dois-je hacher les données d’audience avant de les envoyer à  [!DNL LinkedIn]?**

[!DNL LinkedIn] exige qu’aucune information d’identification personnelle (PII) ne soit envoyée clairement. Par conséquent, les audiences activées vers [!DNL LinkedIn] peuvent être masquées à partir des identifiants *hachés*, tels que les adresses électroniques ou les numéros de téléphone.

Pour obtenir des explications détaillées sur les exigences de correspondance des ID, voir [Exigences de correspondance des ID](catalog/social/linkedin.md#id-matching-requirements).

**Dans quel type d’identités puis-je activer  [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] prend en charge l’activation des identités suivantes : e-mails hachés,  [!DNL GAID] et  [!DNL IDFA].
