---
title: Vue d’ensemble d’Adobe Experience Platform Assurance
description: Adobe Experience Platform permet de contrôler, de tester, de simuler et de valider la manière dont vous collectez les données ou dont les expériences sont accomplies dans vos applications mobiles.
exl-id: e887f5f6-3db0-4521-be2d-20ef3d08e7d0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 6%

---

# Assurance d’Adobe Experience Platform Assurance

Adobe Experience Platform Assurance est un produit de [Adobe Experience Cloud](https://www.adobe.com/experience-cloud.html) qui vous permet d’inspecter, de tester, de simuler et de valider la manière dont vous collectez les données ou dont les expériences sont diffusées dans votre application mobile.

>[!IMPORTANT]
>
> Le projet Griffon est désormais connu sous le nom d’**Assurance** !
>
> Le projet Griffon est désormais disponible pour **tous** les clients Adobe Experience Cloud sous la forme d’Assurance. Pour en savoir plus sur cette transition, veuillez lire le [guide d’accès utilisateur](./user-access.md).

>[!INFO]
>
>Les API publiques d’Assurance sont disponibles !
>
>[Les API Assurance](https://developer.adobe.com/adobe-assurance-public-apis/) sont un ensemble d’API qui permettent aux utilisateurs et aux utilisatrices de tester et de déboguer leurs applications web et mobiles, lorsqu’elles sont équipées de la SDK mobile Adobe Assurance.

## Disponibilité générale

À compter du 15 octobre 2022, Assurance sera généralement disponible pour tous les Adobe Experience Cloud.

### Qu&#39;est-ce qui change ?

Le 15 octobre - l’accès à Assurance sera géré via Admin Console. Veuillez lire le [guide d’accès utilisateur](./user-access.md) pour vous assurer que l’accès est toujours disponible sans interruption.

Aucune autre modification ou interruption n’est attendue sur les intégrations, sessions et événements Assurance existants. L’accès à Assurance peut se poursuivre via [https://griffon.adobe.com](https://griffon.adobe.com) **ou** vous pouvez utiliser (et ajouter un signet) [https://experience.adobe.com/assurance](https://experience.adobe.com/assurance).

## Que peut faire Assurance pour vous ?

### Configuration rapide

Commencez rapidement avec quelques lignes de code. Pour les applications mobiles, Assurance fonctionne avec Adobe Experience Platform Mobile SDK pour vous aider à inspecter, simuler et valider les événements d’application, les signaux d’emplacement, les paramètres de configuration, les journaux SDK, les informations sur les appareils, etc.

### Connexion sans tracas

Avec Assurance, la connexion de votre application à Experience Platform est simple et fiable. Vous n’avez pas besoin d’utiliser de serveurs proxy réseau [MiTM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)) ni d’autres outils de gymnastique réseau. La connexion de votre application à Assurance est aussi simple que de numériser un code QR ou d’appuyer sur un bouton.

![](./images/index/no-hassle-connection.png)

### Inspection, simulation et validation en temps réel

Après vous être connecté à Assurance, vous pouvez inspecter les événements et l’activité de l’application diffusés en direct et filtrer et rechercher pour éliminer le bruit. Les événements contiennent des détails sur la validation, le débogage et le dépannage de l’implémentation de votre application mobile. Assurance vous permet également de réaliser des captures d’écran, de simuler des signaux de localisation et bien plus encore en temps réel.

![](./images/index/real-time-insepction.png)

### Intégration avec Adobe Experience Cloud

Les données et expériences côté client sont contextuelles par la manière dont les utilisateurs configurent les règles de création de rapports, les activités et les campagnes sur nos interfaces utilisateur axées sur les spécialistes du marketing. Pour vous aider à faire le lien entre les deux, nous intégrons des solutions Adobe Experience Cloud telles que Adobe Experience Platform, Adobe Analytics, Adobe Target, Places Service, etc.

![](./images/index/integration.png)

## Fonctionnalités

### Événements, journaux, etc. Adobe Experience Platform Mobile SDK

Assurance vous aide à inspecter les événements SDK bruts générés par Adobe Experience Platform Mobile SDK. Tous les événements collectés par le SDK sont disponibles à des fins d’inspection. Les événements SDK sont chargés dans une vue Liste, triés par heure. Chaque événement possède une vue détaillée qui fournit plus de détails. Des vues supplémentaires permettant de parcourir la configuration de SDK, les éléments de données, les états partagés et les versions d’extension de SDK sont également fournies.

### Adobe Analytics

La vue Adobe Analytics > Événements Analytics est une vue ciblée qui affiche les événements liés à votre implémentation mobile Adobe Analytics. La vue Liste affiche le cycle de vie ou les événements d’action/d’état, le « statut » de post-traitement, ainsi que les détails de l’événement requis dans une vue spécialement formatée. Le statut Post-traité indique comment l&#39;événement a été traité par Adobe Analytics après l&#39;application des règles de traitement sur l&#39;événement.

### Adobe Analytics for Streaming Media

La vue Événements Adobe Analytics > Media Analytics affiche des événements pour votre implémentation d’analyses audio et vidéo. La vue détaillée des événements affiche des métadonnées standard et personnalisées qui sont suivies pour chaque session de lecture. En outre, vous pouvez afficher le statut post-traité et les données Media Analytics post-traitées, telles que le temps passé sur le média ou la durée totale de la mémoire tampon.

### Places (Location Services)

La vue Location Services est une vue sur l’appareil qui affiche les événements d’entrée et de sortie de l’emplacement de l’utilisateur pour une validation facile. Cette vue pratique fournit une interface pratique pour afficher des points de données spécifiques à l’emplacement à inspecter sur le client pour le débogage contextuel.

## Assurance est-il sécurisé ?

Assurance a mis en place les mesures de sécurité suivantes :

* Assurance et l’interface utilisateur web d’Assurance disposent toutes deux d’une liaison sécurisée basée sur le code confidentiel pour une connexion. L’utilisateur doit explicitement créer une liaison, ce qui empêche la création « accidentelle » de connexions Assurance par un utilisateur final.
* Seules les connexions entre Assurance et l’interface utilisateur web d’Assurance appartenant au même ID d’organisation Adobe Experience Cloud sont prises en charge.
* Les événements des SDK mobiles Adobe Experience Platform sont transmis par HTTPS.
* Les SDK Assurance et Adobe Experience Platform Mobile utilisent TLS 1.2
* Les sessions Assurance sont supprimées après 30 jours.
* Les données de session Assurance sont chiffrées au repos, conformément aux bonnes pratiques en matière de stockage.

## Commencer

Pour configurer Assurance, vous devez d’abord installer l’extension Assurance dans votre application. Pour savoir comment procéder, consultez le tutoriel sur [l’implémentation de l’extension Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

Après avoir ajouté Assurance à votre application, vous pouvez créer une session Assurance qui peut être connectée à votre appareil. Pour savoir comment utiliser Assurance, consultez le guide [ sur l’utilisation d’Assurance](./tutorials/using-assurance.md).
