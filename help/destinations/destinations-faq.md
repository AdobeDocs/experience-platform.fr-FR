---
keywords: les destinations ; questions; aux questions fréquentes; faq; faq sur les destinations
title: Questions fréquentes
description: Réponses aux questions les plus fréquemment posées sur les destinations Adobe Experience Platform
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 6%

---

# Questions fréquentes {#faq}

## Vue d’ensemble {#overview}

Ce document répond aux questions les plus fréquemment posées sur les destinations Adobe Experience Platform. Pour les questions et le dépannage liés à d’autres [!DNL Platform] services, y compris ceux rencontrés dans toutes les [!DNL Platform] API, reportez-vous à la section [Guide de dépannage des Experience Platform](../landing/troubleshooting.md).

## Questions générales sur les destinations {#general}

### Pourquoi vois-je différents nombres de profils dans l’interface utilisateur de l’Experience Platform et dans les fichiers CSV exportés ?

+++Réponse Il s’agit d’un comportement normal en raison de la manière dont l’Experience Platform effectue la segmentation.

La segmentation par flux met à jour le nombre de profils pour les audiences en continu toute la journée, tandis que la segmentation par lots met à jour le nombre de profils pour les audiences par lots une fois toutes les 24 heures.

Lorsque le planning d’exportation de l’audience diffère du planning de segmentation, le profil est comptabilisé entre l’interface utilisateur et l’exportation [!DNL CSV] sera différent, en particulier en ce qui concerne les audiences en continu.

Voir [Documentation de Segmentation Service](../segmentation/home.md) pour plus d’informations.
+++

## [!DNL Facebook Custom Audiences] {#facebook-faq}

### Que dois-je faire avant d’activer les audiences dans [!DNL Facebook Custom Audiences]?

+++Réponse Avant de pouvoir envoyer vos audiences à [!DNL Facebook], assurez-vous de respecter les conditions suivantes :

* Votre [!DNL Facebook] Le compte utilisateur doit avoir la variable **[!DNL Manage campaigns]** autorisation activée pour le compte publicitaire que vous prévoyez d’utiliser.
* Le **Adobe Experience Cloud** votre compte professionnel doit être ajouté en tant que partenaire publicitaire dans votre [!DNL Facebook Ad Account]. Utilisez `business ID=206617933627973`. Voir [Ajout de partenaires à votre compte Business Manager](https://www.facebook.com/business/help/1717412048538897) pour plus d’informations, voir la documentation de Facebook .
  >[!IMPORTANT]
  >
  > Lors de la configuration des autorisations pour Adobe Experience Cloud, vous devez activer l’autorisation **Gérer des campagnes**. Ceci est obligatoire pour l’intégration de la [!DNL Adobe Experience Platform].
* Lisez et signez les Conditions d’utilisation [!DNL Facebook Custom Audiences]. Pour ce faire, accédez à `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, où `accountID` est votre [!DNL Facebook Ad Account ID].
+++

### Dois-je ajouter des applications ou des pixels à mon [!DNL Facebook] compte publicitaire ?

+++Réponse
Non. Puisqu’il ne s’agit pas d’une intégration basée sur les pixels, il n’est pas nécessaire d’ajouter des pixels à votre compte publicitaire.
+++

### Combien de temps prend Facebook pour traiter les informations de Adobe Experience Platform ?

+++Réponse à partir de mars 2021, [!DNL Facebook Custom Audiences] nécessite jusqu’à une heure pour traiter les informations reçues d’ [!DNL Platform].
+++

### Puis-je utiliser [!DNL Facebook Custom Audiences] pour le ciblage d’audience dans d’autres [!DNL Facebook] applications, comme [!DNL Instagram]?

+++Réponse Vous pouvez utiliser la variable [!DNL Facebook Custom Audiences] destination pour le ciblage des audiences dans la famille d’applications Facebook prises en charge par [!DNL Facebook Custom Audiences], y compris [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], et [!DNL Messenger]. La sélection de l’application sur laquelle les annonceurs souhaitent exécuter des campagnes est indiquée au niveau de l’emplacement dans [!DNL Facebook Ads Manager].
+++

### Quelle est la différence entre [!DNL Facebook Custom Audiences] connexion et [!DNL Facebook Pixel] extension ?

+++Répondez Au [!DNL Facebook Custom Audiences] utilisation des connexions [!DNL Platform] identités lors de l’envoi d’audiences à [!DNL Facebook], tandis que la fonction [[!DNL Facebook Pixel] connection](../destinations/catalog/advertising/facebook-pixel.md) utilise la variable [!DNL Facebook] pixel intégré dans un site web.

Ces deux intégrations sont complémentaires ; vous pouvez utiliser les deux pour assurer une meilleure couverture d’audience. À titre d’exemple, vous pouvez utiliser la variable [!DNL Facebook Pixel] extension pour la prospection des visiteurs de sites web qui n’ont pas créé de compte, alors que [!DNL Facebook Custom Audiences] peut vous aider à cibler les clients existants, en fonction des [!DNL Platform] identités.
+++

### L’intégration de Adobe Experience Platform à [!DNL Facebook Custom Audiences] prise en charge de l’exclusion des utilisateurs d’une audience lorsqu’ils ne remplissent plus les critères pour cette exclusion?**

+++Réponse Oui, l’intégration prend en charge la suppression des utilisateurs de [!DNL Facebook Custom Audiences] lorsqu’ils ne remplissent plus les critères.
+++

### Comment dois-je hacher les données d’audience avant de les envoyer à [!DNL Facebook]?

+++Réponse
[!DNL Facebook] exige qu’aucune information d’identification personnelle (PII) ne soit envoyée clairement. Par conséquent, les audiences sont activées vers [!DNL Facebook] peut être désactivé *haché* les identifiants, tels que les adresses électroniques ou les numéros de téléphone.

Pour obtenir des explications détaillées sur les exigences de correspondance des identifiants, voir [Exigences de correspondance des identifiants](catalog/social/facebook.md#id-matching-requirements).
+++

### Quel type d’identités puis-je activer dans [!DNL Facebook Custom Audiences]?

+++Réponse
[!DNL Facebook Custom Audiences] prend en charge l’activation des identités suivantes : e-mails hachés, numéros de téléphone hachés, [!DNL GAID], [!DNL IDFA]et les identifiants externes personnalisés.
+++

### Puis-je créer plusieurs destinations Facebook dans l’interface utilisateur de Platform pour des comptes Facebook distincts ?

+++Réponse
Oui. Dans Experience Platform, une destination Facebook correspond à 1:1 pour un compte publicitaire dans Facebook. Vous pouvez créer une destination Facebook distincte pour chaque compte publicitaire Facebook de votre société. Suivez la [tutoriel sur la connexion à destination](/help/destinations/ui/connect-destination.md) et connectez-vous à un compte Facebook distinct pour chaque nouvelle destination Facebook dans l’interface utilisateur de Platform. Le nombre de comptes publicitaires Facebook auxquels vous pouvez vous connecter est illimité.
+++

## Correspondance client Google {#google-customer-match}

### Lors de l’exportation d’audiences vers la correspondance client Google, pourquoi vois-je des nombres supplémentaires annexés à la fin des noms d’audience dans l’interface de Google ?

+++La réponse Google nécessite que les noms d’audience soient uniques. Les chiffres que vous voyez sont [Horodatages UNIX](https://www.unixtimestamp.com/) et ils sont ajoutés afin de conserver les noms d’audience uniques, si vous avez mappé la même audience à plusieurs destinations Google.
+++

## Audiences mappées linkedIn {#linkedin}

### Dois-je ajouter des applications ou des pixels à mon [!DNL LinkedIn] compte publicitaire ?

+++Réponse
Non. Puisqu’il ne s’agit pas d’une intégration basée sur les pixels, il n’est pas nécessaire d’ajouter des pixels à votre compte publicitaire.
+++

### Que dois-je faire avant d’activer les audiences dans [!DNL LinkedIn Matched Audiences]?

+++Réponse Avant de pouvoir utiliser la variable [!UICONTROL Audience mise en correspondance linkedIn] destination, assurez-vous que [!DNL LinkedIn Campaign Manager] Le compte a la variable [!DNL Creative Manager] niveau d’autorisation ou supérieur.

Pour savoir comment modifier votre [!DNL LinkedIn Campaign Manager] autorisations utilisateur, voir [Ajout, modification et suppression des autorisations d’utilisateur sur les comptes Advertising](https://www.linkedin.com/help/lms/answer/5753) dans la documentation de LinkedIn.
+++

### Comment dois-je hacher les données d’audience avant de les envoyer à [!DNL LinkedIn]?

+++Réponse
[!DNL LinkedIn] exige qu’aucune information d’identification personnelle (PII) ne soit envoyée clairement. Par conséquent, les audiences sont activées vers [!DNL LinkedIn] peut être désactivé *haché* les identifiants, tels que les adresses électroniques ou les numéros de téléphone.

Pour obtenir des explications détaillées sur les exigences de correspondance des identifiants, voir [Exigences de correspondance des identifiants](catalog/social/linkedin.md#id-matching-requirements).
+++

### Quel type d’identités puis-je activer dans [!DNL LinkedIn]?

+++Réponse
[!DNL LinkedIn Matched Audiences] prend en charge l’activation des identités suivantes : les emails hachés, [!DNL GAID], et [!DNL IDFA].
+++

## Personnalisation de la même page et de la page suivante via les destinations Adobe Target et personnalisation personnalisée {#same-next-page-personalization}

### Dois-je utiliser le SDK Web Experience Platform pour envoyer des audiences et des attributs à Adobe Target ?

+++Réponse Non, [SDK Web](../edge/home.md) n’est pas nécessaire pour activer les audiences vers [Adobe Target](catalog/personalization/adobe-target-connection.md).

Cependant, si [[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html?lang=fr) est utilisée à la place du SDK Web, seule la personnalisation de session suivante est prise en charge.

Pour [personnalisation de la même page et de la page suivante](ui/activate-edge-personalization-destinations.md) , vous devez utiliser l’une des méthodes suivantes : [SDK Web](../edge/home.md) ou le [API du serveur réseau Edge](../server-api/overview.md). Consultez la documentation relative à [activation des audiences vers les destinations de périphérie](ui/activate-edge-personalization-destinations.md) pour plus d’informations sur l’implémentation.
+++

### Le nombre d’attributs que je peux envoyer de Real-time Customer Data Platform vers Adobe Target ou vers une destination de personnalisation personnalisée est-il limité ?

+++Réponse Oui, les cas d’utilisation de la personnalisation de la même page et de la page suivante prennent en charge un maximum de 30 attributs par environnement de test lors de l’activation d’audiences vers des destinations Adobe Target ou de personnalisation personnalisée. Pour plus d’informations sur les barrières de sécurité d’activation, voir [documentation sur les barrières de sécurité](guardrails.md#edge-destinations-activation).
+++

### Quels types d’attributs sont pris en charge pour l’activation (par exemple, tableaux, cartes, etc.) ?

+++Réponse Actuellement, seuls les attributs statiques à une seule valeur sont pris en charge, tels que `person.name.firstName`. Les attributs de tableau ne sont actuellement pas pris en charge.
+++

<!-- **Is there a limit on the number of audiences that can be activated to Adobe Target and Custom Personalization destinations?**

Yes, you can activate a maximum of 150 edge audiences per sandbox.  For more information on activation guardrails, see the [default guardrails for activation](guardrails.md#edge-destinations-activation). -->

### Après avoir créé une audience dans Experience Platform, combien de temps faudra-t-il pour qu’elle soit disponible pour les cas d’utilisation de la segmentation Edge ?

+++Réponse Les définitions d’audience sont propagées à la variable [Edge Network](../edge/home.md) jusqu&#39;à une heure. Cependant, si une audience est activée au cours de cette première heure, certains visiteurs qui auraient pu être qualifiés pour l’audience pourraient être manqués.
+++

### Où puis-je voir les attributs activés dans Adobe Target ?

+++Les attributs de réponse peuvent être utilisés dans Target dans [JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html) et [HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html?lang=fr) offres.
+++

### Puis-je créer une destination sans flux de données, puis ajouter un flux de données à la même destination ultérieurement ?

+++Réponse Ceci n’est actuellement pas pris en charge via l’interface utilisateur Destinations . Si vous avez besoin d’aide dans ce cas, contactez votre représentant Adobe.
+++

### Que se passe-t-il si je supprime une destination Adobe Target ?

+++Réponse Lorsque vous supprimez une destination, toutes les audiences et tous les attributs mappés sous la destination sont supprimés d’Adobe Target et ils sont également supprimés du réseau Edge.
+++

### L’intégration fonctionne-t-elle à l’aide de l’API Edge Network Server ?

+++Répondez Oui, l’API Edge Network Server fonctionne avec la destination de personnalisation personnalisée. Comme les attributs de profil peuvent contenir des données sensibles, pour protéger ces données, la destination de personnalisation personnalisée exige que vous utilisiez l’API Edge Network Server pour la collecte des données. En outre, tous les appels API doivent être effectués dans un [contexte authentifié](../server-api/authentication.md).
+++

### Je ne peux avoir qu’une seule stratégie de fusion principale. Puis-je créer des audiences qui utilisent une autre stratégie de fusion et les envoyer tout de même à Adobe Target en tant qu’audiences en continu ?

+++Réponse
Non. Toutes les audiences que vous souhaitez activer dans Adobe Target doivent utiliser un fichier principal sur le serveur. [stratégie de fusion](../profile/merge-policies/ui-guide.md).
+++

### Les stratégies Data Usage Labeling and Enforcement (DULE) et Consent sont-elles appliquées ?

+++Réponse
Oui. Le [Stratégies de gouvernance et de consentement des données](../data-governance/home.md) l’activation des attributs sélectionnés sera régie par les actions marketing créées et associées aux actions marketing sélectionnées.
+++
