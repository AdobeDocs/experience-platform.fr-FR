---
title: Déploiement de balises JavaScript pour la gestion du consentement client
description: Découvrez comment gérer les signaux d’opt-in et d’opt-out des clients pour diverses solutions d’Adobe dans Adobe Experience Platform.
exl-id: 7762c42f-71c8-4f29-a96b-c6c04b838a91
TQID: https://experienceleague.adobe.com/PkcvM2FHjglClEhm6zvl8hkMAgcjPgDngniEMTANFeo
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1id: df80eeb1-8d72-467e-b0df-9d51c7d3a0a1id: e43347a8-f2c5-4aa4-8623-6f13875d7e3aid: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: a8b0238e-1d43-4679-a3b4-5ba1bad83baaid: b82b475d-1e7d-46c6-9172-1f9c73004b11id: c93393a4-e558-47e1-992e-c91ed4d480ceid: daec7ead-f475-492a-a3b3-02ae08565d6fid: e08599ea-8888-4294-ba74-3ba0a7762a46id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: eb9732ab-8232-4b21-bc4c-89de86dbe4d7id: ed0d8d0e-04b9-4326-be72-a0fbca265377id: f7c7de77-382f-4f48-8b36-61a170f06d3did: fc7979f3-56c3-43ca-9784-f1ea3dc69c4b
subfeature_v2: id: d9830f6f-ceb6-4faa-9744-f281fe4439f9id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d095671a-1355-40aa-8b5f-06c33c68080bid: d3cdead0-685a-4489-9250-4bb709942f66id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 625
ht-degree: 94%

---

# Déploiement de balises JavaScript pour la gestion du consentement client

Les réglementations légales relatives à la confidentialité, telles que le Règlement général sur la protection des données (RGPD), exigent que les entreprises puissent gérer le consentement des utilisateurs. Les clients Adobe peuvent demander aux visiteurs de sʼabonner avant lʼexécution de solutions Adobe pour un visiteur donné. Les visiteurs doivent pouvoir gérer leur état d’inclusion/exclusion.

Les clients Adobe Experience Cloud ont besoin de différentes mises en œuvre de ces exigences. Certains utilisent des gestionnaires de consentement au niveau de l’entreprise, tandis que d’autres créent les leurs.

Les développeurs dʼextension Adobe Experience Platform utilisent les extensions et le créateur de règles pour définir les solutions dʼinclusion/exclusion.

Ce document contient des informations sur la façon d’empêcher le déclenchement des balises Adobe tant que le consentement n’est pas obtenu.

## Adobe Advertising

Adobe Experience Platform ne déclenche pas automatiquement [!DNL Adobe Advertising]. [!DNL Advertising] se déclenche uniquement si vous le lui indiquez spécifiquement dans une action de règle. Utilisez les conditions de règle pour déterminer ce qu’il convient de déclencher et quand. Par exemple, pour utiliser des cookies afin de déterminer l’état d’inclusion, définissez un élément de données pour lire ce cookie et utilisez-le comme condition dans la règle pour déterminer quand déclencher l’action Track Conversion (Suivi des conversions).

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
