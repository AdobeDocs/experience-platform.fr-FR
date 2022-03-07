---
keywords: les destinations ; questions; aux questions fréquentes; faq; faq sur les destinations
title: Questions fréquentes
seo-title: Frequently asked questions
description: Réponses aux questions les plus fréquemment posées sur les destinations Adobe Experience Platform
seo-description: Answers to the most frequently asked questions about Adobe Experience Platform destinations
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: b2636377eda6740dceb9bc07fbcc082b85ff3c94
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 9%

---

# Questions fréquentes {#faq}

## Présentation {#overview}

Ce document répond aux questions les plus fréquemment posées sur les destinations Adobe Experience Platform. Pour les questions et le dépannage liés à d’autres [!DNL Platform] services, y compris ceux rencontrés dans toutes les [!DNL Platform] API, reportez-vous à la section [Guide de dépannage des Experience Platform](../landing/troubleshooting.md).

## Questions générales sur les destinations {#general}

**Pourquoi vois-je différents nombres de profils dans l’interface utilisateur de l’Experience Platform et dans les fichiers CSV exportés ?**

Il s’agit d’un comportement normal en raison de la manière dont Experience Platform effectue la segmentation.

La segmentation par flux met à jour le nombre de profils pour les segments en continu toute la journée, tandis que la segmentation par lots met à jour le nombre de profils pour les segments par lot une fois toutes les 24 heures.

Lorsque le planning d’exportation du segment diffère du planning de segmentation, le profil est comptabilisé entre l’interface utilisateur et l’ exporté. [!DNL CSV] sera différent, en particulier en ce qui concerne les segments en flux continu.

Voir [Documentation de Segmentation Service](../segmentation/home.md) pour plus d’informations.

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**Que dois-je faire avant d’activer les audiences dans [!DNL Facebook Custom Audiences]?**

Avant d’envoyer vos segments ciblés à [!DNL Facebook], assurez-vous de respecter les conditions suivantes :

* Votre [!DNL Facebook] Le compte utilisateur doit avoir la variable **[!DNL Manage campaigns]** autorisation activée pour le compte publicitaire que vous prévoyez d’utiliser.
* Le **Adobe Experience Cloud** votre compte professionnel doit être ajouté en tant que partenaire publicitaire dans votre [!DNL Facebook Ad Account]. Utilisez `business ID=206617933627973`. Voir [Ajout de partenaires à votre compte Business Manager](https://www.facebook.com/business/help/1717412048538897) pour plus d’informations, voir la documentation de Facebook .
   >[!IMPORTANT]
   >
   > Lors de la configuration des autorisations pour Adobe Experience Cloud, vous devez activer l’autorisation **Gérer des campagnes**. Ceci est obligatoire pour l’intégration de la [!DNL Adobe Experience Platform].
* Lisez et signez les Conditions d’utilisation [!DNL Facebook Custom Audiences]. Pour ce faire, accédez à `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, où `accountID` est votre [!DNL Facebook Ad Account ID].

**Dois-je ajouter des applications ou des pixels à mon [!DNL Facebook] compte publicitaire ?**

Non. Puisqu’il ne s’agit pas d’une intégration basée sur les pixels, il n’est pas nécessaire d’ajouter des pixels à votre compte publicitaire.

**Combien de temps prend Facebook pour traiter les informations de Adobe Experience Platform ?**

En mars 2021, [!DNL Facebook Custom Audiences] nécessite jusqu’à une heure pour traiter les informations reçues d’ [!DNL Platform].

**Puis-je utiliser [!DNL Facebook Custom Audiences] pour le ciblage d’audience dans d’autres [!DNL Facebook] applications, comme [!DNL Instagram]?**

Vous pouvez utiliser la variable [!DNL Facebook Custom Audiences] destination pour le ciblage des audiences dans la famille d’applications Facebook prises en charge par [!DNL Facebook Custom Audiences], y compris [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], et [!DNL Messenger]. La sélection de l’application sur laquelle les annonceurs souhaitent exécuter des campagnes est indiquée au niveau de l’emplacement dans [!DNL Facebook Ads Manager].

**Quelle est la différence entre [!DNL Facebook Custom Audiences] connexion et [!DNL Facebook Pixel] extension ?**

Le [!DNL Facebook Custom Audiences] utilisation des connexions [!DNL Platform] identités lors de l’envoi d’audiences à [!DNL Facebook], tandis que la fonction [[!DNL Facebook Pixel] connection](../destinations/catalog/advertising/facebook-pixel.md) utilise la variable [!DNL Facebook] pixel intégré dans un site web.

Ces deux intégrations sont complémentaires ; vous pouvez utiliser les deux pour assurer une meilleure couverture d’audience. À titre d’exemple, vous pouvez utiliser la variable [!DNL Facebook Pixel] extension pour la prospection des visiteurs de sites web qui n’ont pas créé de compte, alors que [!DNL Facebook Custom Audiences] peut vous aider à cibler les clients existants, en fonction des [!DNL Platform] identités.

**L’intégration de Adobe Experience Platform à [!DNL Facebook Custom Audiences] prendre en charge les utilisateurs exclus d’une audience lorsqu’ils ne remplissent plus les critères pour cela ?**

Oui, l’intégration prend en charge la suppression des utilisateurs de [!DNL Facebook Custom Audiences] lorsqu’ils ne remplissent plus les critères.

**Comment dois-je hacher les données d’audience avant de les envoyer à [!DNL Facebook]?**

[!DNL Facebook] exige qu’aucune information d’identification personnelle (PII) ne soit envoyée clairement. Par conséquent, les audiences sont activées vers [!DNL Facebook] peut être désactivé *haché* les identifiants, tels que les adresses électroniques ou les numéros de téléphone.

Pour obtenir des explications détaillées sur les exigences de correspondance des identifiants, voir [Exigences de correspondance des identifiants](catalog/social/facebook.md#id-matching-requirements).

**Quel type d’identités puis-je activer dans [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] prend en charge l’activation des identités suivantes : e-mails hachés, numéros de téléphone hachés, [!DNL GAID], [!DNL IDFA]et les identifiants externes personnalisés.

**Puis-je créer plusieurs destinations Facebook dans l’interface utilisateur de Platform pour des comptes Facebook distincts ?**

Oui. Dans Experience Platform, une destination Facebook correspond à 1:1 pour un compte publicitaire dans Facebook. Vous pouvez créer une destination Facebook distincte pour chaque compte publicitaire Facebook de votre société. Suivez la [tutoriel sur la connexion à destination](/help/destinations/ui/connect-destination.md) et connectez-vous à un compte Facebook distinct pour chaque nouvelle destination Facebook dans l’interface utilisateur de Platform. Le nombre de comptes publicitaires Facebook auxquels vous pouvez vous connecter est illimité.

## Correspondance client Google {#google-customer-match}

**Lors de l’exportation de segments vers la correspondance client Google, pourquoi vois-je des nombres supplémentaires annexés à la fin des noms de segment dans l’interface de Google ?**

Google exige que les noms de segment soient uniques. Les chiffres que vous voyez sont [Horodatages UNIX](https://www.unixtimestamp.com/) et ils sont ajoutés afin de conserver les noms de segment uniques, si vous avez mappé le même segment à plusieurs destinations Google.

## Audiences mappées linkedIn {#linkedin}

**Dois-je ajouter des applications ou des pixels à mon [!DNL LinkedIn] compte publicitaire ?**

Non. Puisqu’il ne s’agit pas d’une intégration basée sur les pixels, il n’est pas nécessaire d’ajouter des pixels à votre compte publicitaire.

**Que dois-je faire avant d’activer les audiences dans [!DNL LinkedIn Matched Audiences]?**

Avant d’utiliser la variable [!UICONTROL Audience mise en correspondance linkedIn] destination, assurez-vous que [!DNL LinkedIn Campaign Manager] Le compte a la variable [!DNL Creative Manager] niveau d’autorisation ou supérieur.

Pour savoir comment modifier votre [!DNL LinkedIn Campaign Manager] autorisations utilisateur, voir [Ajout, modification et suppression des autorisations d’utilisateur sur les comptes Advertising](https://www.linkedin.com/help/lms/answer/5753) dans la documentation de LinkedIn.

**Comment dois-je hacher les données d’audience avant de les envoyer à [!DNL LinkedIn]?**

[!DNL LinkedIn] exige qu’aucune information d’identification personnelle (PII) ne soit envoyée clairement. Par conséquent, les audiences sont activées vers [!DNL LinkedIn] peut être désactivé *haché* les identifiants, tels que les adresses électroniques ou les numéros de téléphone.

Pour obtenir des explications détaillées sur les exigences de correspondance des identifiants, voir [Exigences de correspondance des identifiants](catalog/social/linkedin.md#id-matching-requirements).

**Quel type d’identités puis-je activer dans [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] prend en charge l’activation des identités suivantes : les emails hachés, [!DNL GAID], et [!DNL IDFA].
