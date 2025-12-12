---
title: Déploiement de balises JavaScript pour la gestion du consentement client
description: Découvrez comment gérer les signaux d’opt-in et d’opt-out des clients pour diverses solutions d’Adobe dans Adobe Experience Platform.
exl-id: 7762c42f-71c8-4f29-a96b-c6c04b838a91
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 94%

---

# Déploiement de balises JavaScript pour la gestion du consentement client

Les réglementations légales relatives à la confidentialité, telles que le Règlement général sur la protection des données (RGPD), exigent que les entreprises puissent gérer le consentement des utilisateurs. Les clients Adobe peuvent demander aux visiteurs de sʼabonner avant lʼexécution de solutions Adobe pour un visiteur donné. Les visiteurs doivent pouvoir gérer leur état d’inclusion/exclusion.

Les clients Adobe Experience Cloud ont besoin de différentes mises en œuvre de ces exigences. Certains utilisent des gestionnaires de consentement au niveau de l’entreprise, tandis que d’autres créent les leurs.

Les développeurs dʼextension Adobe Experience Platform utilisent les extensions et le créateur de règles pour définir les solutions dʼinclusion/exclusion.

Ce document contient des informations sur la façon d’empêcher le déclenchement des balises Adobe tant que le consentement n’est pas obtenu.

## Advertising Cloud

Adobe Experience Platform ne déclenche pas automatiquement [!DNL Advertising Cloud]. [!DNL Advertising Cloud] se déclenche uniquement si vous le lui indiquez spécifiquement dans une action de règle. Utilisez les conditions de règle pour déterminer ce qu’il convient de déclencher et quand. Par exemple, pour utiliser des cookies afin de déterminer l’état d’inclusion, définissez un élément de données pour lire ce cookie et utilisez-le comme condition dans la règle pour déterminer quand déclencher l’action Track Conversion (Suivi des conversions).

Les intégrations avec les gestionnaires de consentement (tels que OneTrust) peuvent définir et suivre les cookies de consentement pour les clients, qui peuvent ensuite être utilisés dans le créateur de règles.

## Analytics

Dans la section Link Tracking (Suivi des liens) des paramètres de configuration de l’extension [!DNL Analytics], assurez-vous que les éléments suivants ne sont *pas* sélectionnés :

* Track download links (Suivi des liens de téléchargement)
* Track outbound links (Suivi des liens sortants)

Lorsque ces paramètres ne sont pas sélectionnés, Experience Platform ne déclenche pas automatiquement le [!DNL Adobe Analytics]. [!DNL Analytics] se déclenche uniquement si vous le lui indiquez spécifiquement dans une action de règle. Utilisez les conditions de règle pour déterminer ce qu’il convient de déclencher et quand. Par exemple, pour utiliser des cookies afin de déterminer l’état d’inclusion, définissez un élément de données pour lire ce cookie et utilisez-le comme condition dans la règle pour déterminer quand déclencher l’action Envoyer la balise.

Par ailleurs, vous pourriez envisager d’utiliser l’[objet d’accord préalable d’Adobe](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=fr) pour contrôler le déclenchement de cette balise, et ce, en même temps que votre plateforme de gestion du consentement.

Les intégrations avec les gestionnaires de consentement (tels que OneTrust) peuvent définir et suivre les cookies de consentement pour les clients, qui peuvent ensuite être utilisés dans le créateur de règles.

## Audience Manager

La DIL (Bibliothèque d’intégration des données) est actuellement configurée pour se déclencher automatiquement si elle est placée sur une page client. Pensez à utiliser l’[objet d’accord préalable d’Adobe](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=fr) pour contrôler le déclenchement de cette balise, et ce, en même temps que votre plateforme de gestion du consentement.

[!DNL Adobe] vous conseille d’utiliser le transfert côté serveur dans [!DNL Analytics].

## Experience Cloud ID

[!DNL Experience Cloud ID] se déclenche automatiquement s’il est placé sur une page client.

Pensez à utiliser l’[objet d’accord préalable d’Adobe](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=fr) pour contrôler le déclenchement de cette balise, et ce, en même temps que votre plateforme de gestion du consentement.

## Target

Adobe Experience Platform ne déclenche pas automatiquement [!DNL Target]. [!DNL Target] se déclenche uniquement si vous le lui indiquez spécifiquement dans une action de règle. Utilisez les conditions de règle pour déterminer ce qu’il convient de déclencher et quand. Par exemple, pour utiliser des cookies afin de déterminer l’état d’inclusion, définissez un élément de données pour lire ce cookie et utilisez-le comme condition dans la règle pour déterminer quand déclencher l’action Load [!DNL Target] (Charger Target).

Par ailleurs, vous pourriez envisager d’utiliser l’[objet d’accord préalable d’Adobe](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=fr) pour contrôler le déclenchement de cette balise, et ce, en même temps que votre plateforme de gestion du consentement.

Les intégrations avec les gestionnaires de consentement (tels que OneTrust) peuvent définir et suivre les cookies de consentement pour les clients, qui peuvent ensuite être utilisés dans le créateur de règles.
