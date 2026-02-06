---
keywords: affichage des profils rtcdp;affichage des profils rtcdp;profils rtcdp
title: Parcourir les profils dans Real-Time Customer Data Platform
description: Adobe Real-Time Customer Data Platform vous permet de parcourir les données du profil client en temps réel à l’aide de l’interface utilisateur de Adobe Experience Platform.
feature: Get Started, Profiles
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=fr#rtcdp-editions" newtab=true
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 12%

---


# Parcourir les profils dans Real-Time Customer Data Platform

Le profil client en temps réel offre une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Chaque profil étant agrégé en fonction des données introduites dans le système depuis diverses sources, chaque profil devient un compte d’activité horodaté et exploitable de chaque interaction de votre client avec votre marque.

Dans l’interface utilisateur de Adobe Experience Platform, vous pouvez afficher ces profils en lecture seule et afficher des informations importantes concernant chacun de vos clients, y compris leurs préférences, les événements passés, les interactions et les audiences auxquelles appartient la personne.

Adobe Real-Time Customer Data Platform repose sur Adobe Experience Platform et peut ainsi utiliser les fonctionnalités d’affichage de profil de l’interface utilisateur d’Experience Platform. Pour obtenir un guide détaillé sur l’affichage des profils client dans l’interface utilisateur d’Experience Platform, reportez-vous au [guide d’utilisation du profil client en temps réel](../../profile/ui/user-guide.md).

## Améliorations des profils pour Real-Time CDP, édition B2B

Outre les fonctionnalités de navigation de profil prises en charge par Adobe Experience Platform et Real-Time CDP, les utilisateurs de B2B edition peuvent accéder aux attributs et événements B2B du profil client, respectivement dans les onglets [!UICONTROL Attributes] et [!UICONTROL Events]. Les données B2B peuvent également être utilisées pour effectuer la segmentation, avec ces audiences apparaissant sous l’onglet [!UICONTROL Audience membership] du client avec les audiences non B2B.

Real-Time CDP, B2B edition vous permet également de parcourir les [!UICONTROL Accounts], les [!UICONTROL Opportunities] et les [!UICONTROL Source records] de l’ensemble des sources d’entreprise associées à un client individuel.

Pour explorer ces améliorations, commencez par suivre les étapes décrites dans le [guide d’utilisation du profil client en temps réel](../../profile/ui/user-guide.md) pour parcourir un profil par politique de fusion ou espace de noms d’identité.

![](images/b2b-browse-profile.png)

Les détails du profil incluent l’accès aux onglets [!UICONTROL Accounts], [!UICONTROL Opportunities] et [!UICONTROL Source records] en plus des informations standard fournies dans le profil client qui a également été amélioré avec les événements et attributs B2B.

![](images/b2b-profile-detail.png)

Pour en savoir plus sur les détails du profil fournis dans l’interface utilisateur d’Experience Platform, reportez-vous à la section [détails de la documentation du tableau de bord Profils](../../dashboards/guides/profiles.md#browse-profiles).

### Onglet Comptes

Sélectionnez **[!UICONTROL Accounts]** pour afficher la liste des comptes associés au profil. Cette liste comprend des informations de base provenant du profil du compte, telles que le nom, le site web et le secteur d’activité du compte, ainsi qu’un lien vers le profil du compte.

Pour plus d’informations sur l’affichage et l’exploration des profils de compte, commencez par lire la [présentation des profils de compte](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### Onglet Opportunités

L’onglet **[!UICONTROL Opportunities]** fournit des détails sur les opportunités ouvertes et clôturées liées au compte. Ces opportunités peuvent être ingérées dans Experience Platform à partir de plusieurs sources. Toutefois, Real-Time CDP, B2B edition permet aux spécialistes marketing de voir facilement toutes ces opportunités au même endroit.

Chaque opportunité inclut des informations telles que son nom, son montant, son avancée et si elle est ouverte, clôturée, gagnée ou perdue.

![](images/b2b-profile-opportunities.png)

### Onglet Enregistrements Source

L’onglet **[!UICONTROL Source records]** vous permet de voir facilement les différents enregistrements sources provenant de vos sources d’entreprise qui contribuent au profil client unique. En plus de l’[!UICONTROL Person source key] et de l’adresse e-mail, chaque enregistrement source fournit également le type d’enregistrement (par exemple, un enregistrement « contact » ou « prospect »), ainsi que la source.

![](images/b2b-profile-source-records.png)
