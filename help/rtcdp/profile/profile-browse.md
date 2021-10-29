---
keywords: afficher les profils rtcdp;vue de profil rtcdp;profils rtcdp
title: Parcourir les profils dans Real-time Customer Data Platform
description: Real-time Customer Data Platform vous permet de parcourir les données de Real-time Customer Profile à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: c15f59de49c60f55b432a39f30fb5f1865fd4671
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 24%

---


# Parcourir les profils dans Real-time Customer Data Platform

Real-time Customer Profile offre une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Chaque profil étant agrégé en fonction des données introduites dans le système depuis diverses sources, chaque profil devient un compte d’activité horodaté et exploitable de chaque interaction de votre client avec votre marque.

Dans l’interface utilisateur de Adobe Experience Platform, vous pouvez afficher ces profils en lecture seule et afficher des informations importantes sur chaque client, notamment ses préférences, ses événements passés, ses interactions et les segments auxquels il appartient.

Real-time Customer Data Platform repose sur Adobe Experience Platform et permet ainsi d’utiliser les fonctionnalités d’affichage des profils dans l’interface utilisateur de l’Experience Platform. Pour obtenir un guide détaillé sur l’affichage des profils client dans l’interface utilisateur de Platform, reportez-vous à la section [Guide d’utilisation de Real-time Customer Profile](../../profile/ui/user-guide.md).

## Améliorations des profils pour la plateforme CDP en temps réel, version B2B (bêta)

>[!IMPORTANT]
>
>L’édition B2B de Real-time Customer Data Platform est actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

Outre les fonctionnalités de navigation des profils prises en charge par Adobe Experience Platform, les utilisateurs de la plateforme de données clients en temps réel de l’édition B2B peuvent accéder aux attributs et événements B2B du profil client sur la page [!UICONTROL Attributs] et [!UICONTROL Événements] les onglets, respectivement. Les données B2B peuvent également être utilisées pour effectuer une segmentation, avec ces segments apparaissant sous le segment du client [!UICONTROL abonnement au segment] à côté des segments non B2B.

La plateforme de données clients en temps réel, B2B Edition, vous permet également de parcourir les [!UICONTROL Comptes], [!UICONTROL Opportunités], et [!UICONTROL Enregistrements source] de toutes les sources de votre entreprise associées à un client individuel.

Pour explorer ces améliorations, commencez par suivre les étapes décrites dans la section [Guide d’utilisation de Real-time Customer Profile](../../profile/ui/user-guide.md) pour parcourir un profil par stratégie de fusion ou espace de noms d’identité.

![](images/b2b-browse-profile.png)

Le détail du profil inclut l’accès à [!UICONTROL Comptes], [!UICONTROL Opportunités], et [!UICONTROL Enregistrements source] onglets en plus des informations standard fournies dans le profil client qui ont également été améliorées avec les événements et attributs B2B.

![](images/b2b-profile-detail.png)

### Onglet Comptes

Sélectionner **[!UICONTROL Comptes]** pour afficher la liste des comptes liés au profil. Cette liste comprend des informations de base du profil du compte, telles que le nom, le site web et le secteur industriel du compte, ainsi qu’un lien vers le profil du compte.

Pour plus d’informations sur l’affichage et l’exploration des profils de compte, commencez par lire la section [présentation des profils de compte](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### Onglet Opportunités

Le **[!UICONTROL Opportunités]** fournit des détails sur les opportunités ouvertes et fermées liées au compte. Ces opportunités peuvent être ingérées dans Experience Platform à partir de sources multiples. Toutefois, l’édition B2B de Real-time CDP permet aux spécialistes marketing de consulter facilement toutes ces opportunités au même endroit.

Chaque opportunité inclut des informations telles que son nom, son montant, son avancée et si elle est ouverte, clôturée, gagnée ou perdue.

![](images/b2b-profile-opportunities.png)

### Onglet Enregistrements source

Le **[!UICONTROL Enregistrements source]** vous permet d’afficher facilement les multiples enregistrements source provenant de sources de votre entreprise qui contribuent au profil client unique. En plus de la variable [!UICONTROL Clé source de la personne] et adresse électronique, chaque enregistrement source fournit également le type d’enregistrement (par exemple, un enregistrement &quot;contact&quot; ou &quot;piste&quot;), ainsi que la source.

![](images/b2b-profile-source-records.png)
