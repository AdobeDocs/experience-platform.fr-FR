---
title: Présentation de Adobe Experience Platform Assurance
description: Adobe Experience Platform permet de contrôler, de tester, de simuler et de valider la manière dont vous collectez les données ou dont les expériences sont accomplies dans vos applications mobiles.
exl-id: e887f5f6-3db0-4521-be2d-20ef3d08e7d0
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 5%

---

# Assurance d’Adobe Experience Platform Assurance

Adobe Experience Platform Assurance est un produit de [Adobe Experience Cloud](https://www.adobe.com/experience-cloud.html) qui vous aide à inspecter, à tester, à simuler et à valider la manière dont vous collectez des données ou diffusez des expériences dans votre application mobile.

>[!IMPORTANT]
>
> Le projet Griffon est désormais appelé **Assurance** !
>
> Le Griffon du projet est désormais disponible en tant qu&#39;assurance pour tous les clients **Adobe Experience Cloud**. Pour en savoir plus sur cette transition, consultez le [guide d&#39;accès utilisateur](./user-access.md).

>[!INFO]
>
>Les API d’assurance publique sont disponibles !
>
>[Les API d’assurance](https://developer.adobe.com/adobe-assurance-public-apis/) sont un ensemble d’API qui permettent aux utilisateurs de tester et de déboguer leurs applications web et mobiles, lorsqu’ils sont équipés du SDK Mobile Adobe Assurance.

## Disponibilité générale

À compter du 15 octobre 2022, l’assurance sera généralement disponible pour tous les Adobe Experience Cloud.

### Qu&#39;est-ce qui change ?

Le 15 octobre, l’accès à Assurance sera géré par Admin Console. Veuillez lire le [guide d’accès utilisateur](./user-access.md) pour vous assurer que vous disposez toujours d’un accès ininterrompu.

Aucune autre modification ou perturbation n’est attendue des intégrations, sessions et événements Assurance existants. Vous pouvez continuer à y accéder via [https://griffon.adobe.com](https://griffon.adobe.com) **ou** que vous pouvez utiliser (et mettre en signet) [https://experience.adobe.com/assurance](https://experience.adobe.com/assurance).

## Que peut faire Assurance pour vous ?

### Configuration rapide

Commencez rapidement avec peu de lignes de code. Pour les applications mobiles, Assurance fonctionne avec le SDK Mobile Adobe Experience Platform pour vous aider à inspecter, simuler et valider les événements d’application, les signaux d’emplacement, les paramètres de configuration, les journaux de SDK, les informations sur les périphériques, etc.

### Connexion sans tracas

Grâce à Assurance, la connexion de votre application à Platform est simple et fiable. Vous n’avez pas besoin d’utiliser des proxies réseau, [MiTM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)) et d’autres gymnastiques réseau. La connexion de votre application à Assurance est aussi facile que la numérisation d’un code QR ou l’activation d’un bouton.

![](./images/index/no-hassle-connection.png)

### Inspection, simulation et validation en temps réel

Après vous être connecté à Assurance, vous pouvez inspecter les événements et l’activité d’application en continu en direct et filtrer et rechercher afin d’éliminer le bruit. Les événements contiennent des détails sur la validation, le débogage et la résolution des problèmes liés à la mise en oeuvre de votre application mobile. Assurance vous permet également de réaliser une capture d’écran, de simuler des signaux d’emplacement, etc. en temps réel.

![](./images/index/real-time-insepction.png)

### Intégration avec Adobe Experience Cloud

Les données et expériences côté client sont adaptées au contexte selon la manière dont les utilisateurs configurent les règles de création de rapports, les activités et les campagnes sur nos interfaces utilisateur axées sur le spécialiste du marketing. Pour vous aider à connecter les points entre les deux, nous intégrons des solutions Adobe Experience Cloud telles que Adobe Experience Platform, Adobe Analytics, Adobe Target, Places Service, etc.

![](./images/index/integration.png)

## Fonctionnalités

### Événements, journaux et autres SDK Mobile Adobe Experience Platform

Assurance vous aide à inspecter les événements SDK bruts générés par le SDK Mobile Adobe Experience Platform. Tous les événements collectés par le SDK sont disponibles pour inspection. Les événements du SDK sont chargés en mode Liste, triés par heure. Chaque événement dispose d’une vue détaillée qui fournit des détails supplémentaires. Des vues supplémentaires sur la configuration du SDK, les éléments de données, les états partagés et les versions de l’extension du SDK sont également fournies.

### Adobe Analytics

La vue Adobe Analytics > Événements Analytics est une vue sélectionnée qui affiche les événements liés à votre mise en oeuvre mobile Adobe Analytics. Le mode Liste affiche le cycle de vie ou les événements action/état, &quot;status&quot; traité par Post, ainsi que les détails d’événement requis dans une vue spécialement formatée. L’état Post-Processed vous indique comment l’événement a été traité par Adobe Analytics après l’application des règles de traitement sur l’événement.

### Adobe Analytics for Streaming Media

La vue Adobe Analytics > Événements Media Analytics affiche les événements relatifs à votre mise en oeuvre des analyses audio et vidéo. La vue Détails des événements affiche les métadonnées standard et personnalisées qui sont suivies pour chaque session de lecture. En outre, vous pouvez afficher l’état post-traitement et les données d’analyse des médias post-traitement telles que le temps passé sur le média ou la durée totale de la mémoire tampon.

### Places (services de localisation)

La vue Services de localisation est une vue sur appareil qui affiche les événements d’entrée et de sortie de l’emplacement de l’utilisateur pour une validation facile. Cette vue pratique fournit une interface pratique pour afficher des points de données spécifiques à un emplacement à examiner sur le client pour le débogage dans le contexte.

## Assurance est-elle sûre ?

Les mesures de sécurité mises en place par Assurance sont les suivantes :

* L’interface utilisateur Web d’Assurance et d’Assurance dispose d’une liaison sécurisée basée sur un code PIN pour une connexion. L’utilisateur doit créer explicitement une liaison qui empêche la création par un utilisateur final de connexions d’assurance &quot;accidentelles&quot;.
* Seules les connexions entre Assurance et l’interface utilisateur web d’assurance appartenant au même ID d’organisation Adobe Experience Cloud sont prises en charge.
* Les événements des SDK mobiles Adobe Experience Platform sont transportés via HTTPS.
* Les SDK Assurance et Adobe Experience Platform Mobile utilisent TLS 1.2
* Les sessions d’assurance sont supprimées après 30 jours.
* Les données de session d’assurance sont chiffrées au repos, conformément aux bonnes pratiques de stockage.

## Commencer

Pour configurer Assurance, vous devez d’abord installer l’extension Assurance dans votre application. Pour savoir comment procéder, consultez le tutoriel sur la [mise en oeuvre de l’extension Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

Après avoir ajouté l’assurance à votre application, vous pouvez créer une session d’assurance qui peut être connectée à votre appareil. Pour savoir comment utiliser Assurance, consultez le [guide sur l’utilisation de Assurance](./tutorials/using-assurance.md).
