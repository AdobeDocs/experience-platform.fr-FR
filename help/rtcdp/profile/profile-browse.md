---
keywords: affichage des profils rtcdp;affichage des profils rtcdp;profils rtcdp
title: Parcourir les profils dans Real-Time Customer Data Platform
description: Adobe Real-Time Customer Data Platform vous permet de parcourir les données du profil client en temps réel à l’aide de l’interface utilisateur de Adobe Experience Platform.
feature: Get Started, Profiles
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 11%

---


# Parcourir les profils dans Real-Time Customer Data Platform

Le profil client en temps réel offre une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Chaque profil étant agrégé en fonction des données introduites dans le système depuis diverses sources, chaque profil devient un compte d’activité horodaté et exploitable de chaque interaction de votre client avec votre marque.

Dans l’interface utilisateur de Adobe Experience Platform, vous pouvez afficher ces profils en lecture seule et afficher des informations importantes concernant chacun de vos clients, y compris leurs préférences, les événements passés, les interactions et les audiences auxquelles appartient la personne.

Adobe Real-Time Customer Data Platform repose sur Adobe Experience Platform et peut ainsi utiliser les fonctionnalités d’affichage de profil de l’interface utilisateur d’Experience Platform. Pour obtenir un guide détaillé sur l’affichage des profils client dans l’interface utilisateur d’Experience Platform, reportez-vous au [guide d’utilisation du profil client en temps réel](../../profile/ui/user-guide.md).

## Améliorations des profils pour Real-Time CDP, édition B2B

Outre les fonctionnalités de navigation de profil prises en charge par Adobe Experience Platform et Real-Time CDP, les utilisateurs de B2B edition peuvent accéder aux attributs et événements B2B du profil client, respectivement dans les onglets [!UICONTROL Attributs] et [!UICONTROL Événements]. Les données B2B peuvent également être utilisées pour effectuer la segmentation, avec ces audiences apparaissant sous l’onglet [!UICONTROL Appartenance à une audience] du client avec les audiences non B2B.

Real-Time CDP, B2B edition vous permet également de parcourir les enregistrements [!UICONTROL Comptes], [!UICONTROL Opportunités] et [!UICONTROL Source] de l’ensemble de vos sources d’entreprise associées à un client individuel.

Pour explorer ces améliorations, commencez par suivre les étapes décrites dans le [guide d’utilisation du profil client en temps réel](../../profile/ui/user-guide.md) pour parcourir un profil par politique de fusion ou espace de noms d’identité.

![](images/b2b-browse-profile.png)

Les détails du profil incluent l’accès aux onglets [!UICONTROL Comptes], [!UICONTROL Opportunités] et [!UICONTROL Enregistrements Source] en plus des informations standard fournies dans le profil client qui a également été amélioré avec les événements et attributs B2B.

![](images/b2b-profile-detail.png)

Pour en savoir plus sur les détails du profil fournis dans l’interface utilisateur d’Experience Platform, reportez-vous à la section [détails de la documentation du tableau de bord Profils](../../dashboards/guides/profiles.md#browse-profiles).

### Onglet Comptes

Sélectionnez **[!UICONTROL Comptes]** pour afficher une liste des comptes associés au profil. Cette liste comprend des informations de base provenant du profil du compte, telles que le nom, le site web et le secteur d’activité du compte, ainsi qu’un lien vers le profil du compte.

Pour plus d’informations sur l’affichage et l’exploration des profils de compte, commencez par lire la [présentation des profils de compte](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### Onglet Opportunités

L’onglet **[!UICONTROL Opportunités]** fournit des détails sur les opportunités ouvertes et clôturées liées au compte. Ces opportunités peuvent être ingérées dans Experience Platform à partir de plusieurs sources. Toutefois, Real-Time CDP, B2B edition permet aux spécialistes marketing de voir facilement toutes ces opportunités au même endroit.

Chaque opportunité inclut des informations telles que son nom, son montant, son avancée et si elle est ouverte, clôturée, gagnée ou perdue.

![](images/b2b-profile-opportunities.png)

### Onglet Enregistrements Source

L’onglet **[!UICONTROL Enregistrements Source]** vous permet d’afficher facilement les différents enregistrements sources provenant de vos sources d’entreprise qui contribuent au profil client unique. Outre la [!UICONTROL clé source de la personne] et l’adresse e-mail, chaque enregistrement source fournit également le type d’enregistrement (par exemple, un enregistrement « contact » ou « prospect »), ainsi que la source.

![](images/b2b-profile-source-records.png)
