---
keywords: profil rtcdp;profils rtcdp;identités rtcdp;stratégies de fusion rtcdp;profil client en temps réel
title: Guide de l’interface utilisateur du profil de compte
description: Grâce aux profils de compte, l’édition B2B de Real-time Customer Data Platform vous permet d’unifier les informations de compte provenant de plusieurs sources. Ce guide fournit des détails sur l’interaction avec les profils de compte dans l’interface utilisateur de Adobe Experience Platform.
exl-id: a05e8b84-026e-4482-a288-aa25b441bd69
source-git-commit: 5bd2afcc594d96878ee51af2e9e99d74b764009e
workflow-type: tm+mt
source-wordcount: '1191'
ht-degree: 0%

---

# Guide de l’interface utilisateur du profil de compte

>[!IMPORTANT]
>
>L’édition B2B de Real-time Customer Data Platform est actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

>[!NOTE]
>
>Les profils de compte ne sont disponibles que pour les clients de Real-time Customer Data Platform B2B Edition. Pour en savoir plus sur la plateforme des données clients en temps réel, y compris sur les fonctionnalités disponibles pour chaque type de licence, commencez par lire la [présentation de la plateforme des données clients en temps réel](../overview.md).

Les profils de compte vous permettent d’unifier les informations de compte de plusieurs sources. Cette vue unifiée d’un compte rassemble les données de vos nombreux canaux marketing et des différents systèmes actuellement utilisés par votre organisation pour stocker les informations de votre compte client. Ce document fournit un guide sur l’interaction avec les profils de compte à l’aide des fonctionnalités de la plateforme de données clients en temps réel et de l’édition B2B disponibles dans l’interface utilisateur de Adobe Experience Platform.

## Parcourir les profils de compte

Pour parcourir les profils de compte, commencez par sélectionner **[!UICONTROL Profils]** sous [!UICONTROL Comptes] dans le volet de navigation de gauche.

![](images/b2b-account-browse.png)

Dans l’onglet **[!UICONTROL Parcourir]**, vous pouvez explorer les profils de compte à l’aide d’un ID de compte provenant d’une source d’entreprise connectée ou en saisissant directement les détails de la source.

![](images/b2b-account-browse-by.png)

### Parcourir par [!UICONTROL source d’entreprise connectée]

Pour parcourir les profils de compte en fonction d’une source d’entreprise connectée, sélectionnez **[!UICONTROL Source d’entreprise connectée]** dans la liste déroulante **[!UICONTROL Parcourir par]**, puis choisissez une source connectée à l’aide du bouton de sélecteur situé en regard du champ **[!UICONTROL Source]**.

![](images/b2b-account-browse.png)

Cela ouvre la boîte de dialogue **[!UICONTROL Sélectionner la source]**, dans laquelle vous pouvez sélectionner une source en fonction des connexions établies par votre organisation.

>[!NOTE]
>
>Plusieurs sources peuvent être configurées pour le même fournisseur de services (par exemple, Marketo) pour votre organisation. Il est donc important de consulter le nom de la connexion, le système source et l’instance du système source pour vous assurer que vous effectuez une recherche par la bonne instance source.

Pour en savoir plus sur la connexion des sources d’entreprise, consultez la [présentation des sources](../sources/sources-overview.md).

![](images/b2b-account-select-source.png)

Vous pouvez choisir une source en sélectionnant le bouton radio en regard du nom de la connexion, puis en utilisant **[!UICONTROL Sélectionner]** pour revenir à l’onglet [!UICONTROL Parcourir].

Une fois la source sélectionnée, vous devez désormais saisir un **[!UICONTROL ID de compte]** associé à la source. Par exemple, pour sélectionner une source Salesforce, vous devez saisir un ID de compte à partir de l’instance Salesforce afin d’afficher le profil de compte associé à cet ID.

>[!NOTE]
>
>Pour les ID de compte Marketo, deux tables de compte peuvent être référencées. Vous devez donc utiliser une syntaxe spécifique pour vous assurer que vous consultez le compte approprié.
>
>La syntaxe la plus courante et standard est l’ID de compte Marketo annexé par `.mkto_org` (par exemple, `1234567.mkto_org`). Les clients Marketing basés sur un compte Marketo peuvent avoir des valeurs supplémentaires qui se trouvent à l’aide de l’ID de compte Marketo annexé par `.mkto_account`. Si vous ne savez pas quelle syntaxe utiliser, contactez votre administrateur Marketo.

![](images/b2b-account-browse-id.png)

### Parcourir par [!UICONTROL Autres]

La plateforme de données clients en temps réel, B2B Edition, prend en charge la possibilité d’effectuer une recherche directe en vous permettant de saisir un **[!UICONTROL nom source]**, **[!UICONTROL instance source]** et **[!UICONTROL ID de compte]** pour un compte que vous souhaitez afficher. En saisissant directement le nom et l’instance de la source, vous fournissez le contexte nécessaire à l’Experience Platform pour rechercher et afficher les données correctes du profil du compte.

La possibilité d’effectuer une recherche directe est utile dans les cas où une connexion source directe aux données n’est pas possible. Par exemple, si votre entreprise a mis en place des politiques de gouvernance des données qui empêchent la connexion directe à un CRM, vous pouvez exporter ces données vers un système de stockage dans le cloud, puis les ingérer dans Experience Platform.

Un autre exemple peut être que vous effectuez une transformation sur les données entre le moment où il quitte un système et celui où il entre dans Platform. Vous pouvez utiliser la fonctionnalité de recherche directe pour fournir un contexte aux données (par exemple, en indiquant qu’il s’agit de données Marketo, bien qu’elles proviennent d’un compartiment Amazon S3, par exemple) afin que le système sache où chercher les données et comment les générer correctement.

Pour lancer une recherche directe, sélectionnez **[!UICONTROL Autres]** dans la liste déroulante **[!UICONTROL Parcourir par]**, puis saisissez un **[!UICONTROL Nom source]**, **[!UICONTROL Instance source]** et **[!UICONTROL ID de compte]** pour le compte que vous souhaitez afficher.

![](images/b2b-account-browse-adhoc.png)

## Affichage des détails du profil du compte

Après avoir utilisé l’onglet **[!UICONTROL Parcourir]** pour localiser un profil de compte, la sélection de l’**[!UICONTROL ID de profil]** ouvre l’onglet **[!UICONTROL Détail]** du profil de compte. Les informations de profil affichées dans l’onglet **[!UICONTROL Détail]** ont été fusionnées à partir de plusieurs fragments de profil pour former une vue unique du compte individuel. Cela inclut les détails du compte, tels que les attributs de base et les données de médias sociaux.

Les champs par défaut affichés peuvent également être modifiés au niveau de l’organisation afin d’afficher les attributs de profil de compte préférés.

>[!NOTE]
>
>Des fonctionnalités similaires sont disponibles pour les profils client et un guide détaillé a été créé avec des instructions sur l’ajout et la suppression d’attributs, le redimensionnement des panneaux, etc. Pour en savoir plus, consultez le [guide de personnalisation des détails du profil](../../profile/ui/profile-customization.md).

![](images/b2b-account-details.png)

Vous pouvez afficher des détails supplémentaires relatifs au compte en sélectionnant un autre des onglets disponibles. Ces onglets comprennent les attributs, les personnes et l’onglet opportunités qui affiche les opportunités ouvertes et fermées liées au compte sur l’ensemble de vos systèmes d’entreprise. Pour plus d’informations sur chaque onglet, reportez-vous aux sections suivantes.

## Onglet Attributs

L’onglet **[!UICONTROL Attributs]** répertorie toutes les informations d’enregistrement liées au compte. Cela inclut les données d’attributs provenant de plusieurs sources qui ont été fusionnées pour former une vue unique du compte.

En plus de pouvoir afficher les données dans une liste, vous pouvez utiliser la barre de recherche pour rechercher des attributs spécifiques ou afficher les données d’enregistrement au format JSON.

![](images/b2b-account-attributes.png)

## Onglet Personnes

L’onglet **[!UICONTROL Personnes]** fournit une liste des personnes associées au compte. Il peut s’agir de contacts et de prospects provenant de différents systèmes d’entreprise gérés par différentes équipes au sein de votre organisation, mais dans la plateforme de données clients en temps réel (CDP), l’édition B2B, ils sont présentés sous la forme d’une liste unique vous permettant d’obtenir une vue plus globale des contacts de votre compte.

>[!NOTE]
>
>L’onglet [!UICONTROL Personnes] affiche une liste de 25 personnes au maximum associées au compte. Pour les comptes comptant plus de 25 personnes associées, le système affiche un échantillonnage aléatoire de 25 enregistrements.

Outre l’affichage d’un instantané des informations du contact, chaque personne répertoriée inclut également un **[!UICONTROL ID de profil]**, qui est un lien cliquable qui vous permet d’explorer le profil client en temps réel de cette personne. Pour en savoir plus sur l’affichage des profils clients individuels liés à vos comptes, consultez le guide de [navigation des profils dans la plateforme de données clients en temps réel, B2B Edition](../profile/profile-browse.md).

![](images/b2b-account-people.png)

## Onglet Opportunités

L’onglet **[!UICONTROL Opportunités]** fournit des informations sur les opportunités ouvertes et fermées liées au compte. Ces opportunités peuvent être ingérées dans Experience Platform à partir de sources multiples. Toutefois, la plateforme de données clients en temps réel, l’édition B2B, permet aux marketeurs de voir facilement toutes ces opportunités ensemble au même endroit.

>[!NOTE]
>
>L’onglet [!UICONTROL Opportunités] affiche une liste de 25 opportunités au maximum associées au compte. Pour les comptes comportant plus de 25 opportunités associées, le système affiche un échantillonnage aléatoire de 25 enregistrements.

Chaque opportunité inclut des informations telles que le nom de l’opportunité, son montant, l’étape et si l’opportunité est ouverte, fermée, gagnée ou perdue.

![](images/b2b-account-opportunities.png)
