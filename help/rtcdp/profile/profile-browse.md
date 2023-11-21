---
keywords: afficher les profils rtcdp;vue de profil rtcdp;profils rtcdp
title: Parcourir les profils dans Real-time Customer Data Platform
description: Adobe Real-time Customer Data Platform vous permet de parcourir les données de Real-time Customer Profile à l’aide de l’interface utilisateur de Adobe Experience Platform.
feature: Get Started, Profiles
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 12%

---


# Parcourir les profils dans Real-time Customer Data Platform

Real-Time Customer Profile offre une vue d’ensemble de chaque client, en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Chaque profil étant agrégé en fonction des données introduites dans le système depuis diverses sources, chaque profil devient un compte d’activité horodaté et exploitable de chaque interaction de votre client avec votre marque.

Dans l’interface utilisateur de Adobe Experience Platform, vous pouvez afficher ces profils en lecture seule et afficher des informations importantes sur chacun de vos clients, notamment leurs préférences, leurs événements passés, leurs interactions et les audiences auxquelles ils appartiennent.

Adobe Real-time Customer Data Platform repose sur Adobe Experience Platform et permet ainsi d’utiliser les fonctionnalités d’affichage des profils dans l’interface utilisateur de l’Experience Platform. Pour obtenir un guide détaillé sur l’affichage des profils client dans l’interface utilisateur de Platform, reportez-vous à la section [Guide d’utilisation de Real-Time Customer Profile](../../profile/ui/user-guide.md).

## Améliorations des profils pour Real-Time CDP, édition B2B

Outre les fonctionnalités de navigation des profils prises en charge par Adobe Experience Platform, Real-Time CDP, les utilisateurs de l’édition B2B peuvent accéder aux attributs et événements B2B du profil client sur la page [!UICONTROL Attributs] et [!UICONTROL Événements] les onglets, respectivement. Les données B2B peuvent également être utilisées pour effectuer une segmentation, avec les audiences apparaissant sous le [!UICONTROL abonnement à l’audience] à côté des audiences non B2B.

Real-Time CDP, B2B Edition vous permet également de parcourir les [!UICONTROL Comptes], [!UICONTROL Opportunités], et [!UICONTROL Enregistrements source] de toutes les sources de votre entreprise associées à un client individuel.

Pour explorer ces améliorations, commencez par suivre les étapes décrites dans la section [Guide d’utilisation de Real-Time Customer Profile](../../profile/ui/user-guide.md) pour parcourir un profil par stratégie de fusion ou espace de noms d’identité.

![](images/b2b-browse-profile.png)

Le détail du profil inclut l’accès à [!UICONTROL Comptes], [!UICONTROL Opportunités], et [!UICONTROL Enregistrements source] onglets en plus des informations standard fournies dans le profil client qui ont également été améliorées avec les événements et attributs B2B.

![](images/b2b-profile-detail.png)

### Onglet Comptes

Sélectionner **[!UICONTROL Comptes]** pour afficher la liste des comptes liés au profil. Cette liste comprend des informations de base du profil du compte, telles que le nom, le site web et le secteur industriel du compte, ainsi qu’un lien vers le profil du compte.

Pour plus d’informations sur l’affichage et l’exploration des profils de compte, commencez par lire la section [présentation des profils de compte](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### Onglet Opportunités

La variable **[!UICONTROL Opportunités]** fournit des détails sur les opportunités ouvertes et fermées liées au compte. Ces opportunités peuvent être ingérées dans Experience Platform à partir de sources multiples. Toutefois, Real-Time CDP, version B2B, permet aux marketeurs de voir facilement toutes ces opportunités ensemble au même endroit.

Chaque opportunité inclut des informations telles que son nom, son montant, son avancée et si elle est ouverte, clôturée, gagnée ou perdue.

![](images/b2b-profile-opportunities.png)

### Onglet Enregistrements source

La variable **[!UICONTROL Enregistrements source]** vous permet d’afficher facilement les multiples enregistrements source provenant de sources de votre entreprise qui contribuent au profil client unique. En plus de la variable [!UICONTROL Clé source de la personne] et adresse électronique, chaque enregistrement source fournit également le type d’enregistrement (par exemple, un enregistrement &quot;contact&quot; ou &quot;piste&quot;), ainsi que la source.

![](images/b2b-profile-source-records.png)
