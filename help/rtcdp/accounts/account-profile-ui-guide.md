---
keywords: profil rtcdp;profils rtcdp;identités rtcdp;politiques de fusion rtcdp;profil client en temps réel
title: Guide de l’interface utilisateur des profils de compte
description: Grâce aux profils de compte, l’édition B2B d’Adobe Real-time Customer Data Platform permet d’unifier les informations de compte provenant de plusieurs sources. Ce guide fournit des détails sur l’interaction avec les profils de compte dans l’interface utilisateur d’Adobe Experience Platform.
badgeB2B: label="Édition B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
feature: Profiles, B2B
exl-id: a05e8b84-026e-4482-a288-aa25b441bd69
source-git-commit: 96f29d5c64bb29125d8a63dd3ddb3bdedb5ebd52
workflow-type: tm+mt
source-wordcount: '1680'
ht-degree: 55%

---

# Guide de l’interface utilisateur des profils de compte

>[!NOTE]
>
>Les profils de compte ne sont disponibles que pour les clients de Real-time Customer Data Platform B2B Edition. Pour en savoir plus sur Real-Time CDP, y compris sur les fonctionnalités disponibles pour chaque type de licence, veuillez commencer par lire la section [Présentation de Real-Time CDP](../overview.md).

Les profils de compte vous permettent d’unifier les informations de compte provenant de plusieurs sources. Cette vue unifiée d’un compte rassemble les données de vos nombreux canaux marketing et des différents systèmes actuellement utilisés par votre organisation pour stocker les informations du compte client. Ce document fournit un guide sur l’interaction avec les profils de compte à l’aide des fonctionnalités de l’édition B2B de Real-Time CDP disponibles dans l’interface utilisateur de Adobe Experience Platform.

Pour en savoir plus sur la manière dont les profils de compte sont créés dans le cadre du workflow B2B, reportez-vous au [tutoriel de bout en bout](../b2b-tutorial.md).

## Présentation des profils de compte {#account-profiles-overview}

Sélectionner **[!UICONTROL Profils]** under [!UICONTROL Comptes] dans le volet de navigation de gauche pour afficher la présentation des profils de compte. Sous , [!UICONTROL Présentation] , le tableau de bord affiche un graphique ou un graphique affichant des widgets dans un seul point d’entrée.

![L’onglet Aperçu des profils de compte avec les profils dans le volet de navigation de gauche et Aperçu en surbrillance.](images/b2b-account-profile-overview.png)

Consultez la documentation relative à la [[!UICONTROL Profils de compte]](../../dashboards/guides/account-profiles.md) tableau de bord pour en savoir plus. Consultez la documentation relative à [Modèle de données Real-time Customer Data Platform Insights B2B](../../dashboards/data-models/cdp-insights-data-model-b2b.md) pour plus d’informations sur l’utilisation des modèles de données d’insights pour créer des graphiques personnalisés pour vos tableaux de bord.

## Configurer la correspondance de pistes vers les comptes {#configure-lead-to-account-matching}

>[!IMPORTANT]
>
> Seuls les administrateurs de l’IA B2B peuvent activer, désactiver et configurer le prospect vers le service de correspondance de compte. Lors de la désactivation du service, les résultats correspondants seront supprimés dans les 24 heures.

Pour configurer la correspondance de pistes et de comptes, sélectionnez **[!UICONTROL Profils]** under [!UICONTROL Comptes] dans le volet de navigation de gauche. Sur le **[!UICONTROL Présentation]** onglet, sélectionnez **[!UICONTROL Paramètres]** en haut à droite.

![Onglet Aperçu des profils de compte avec la mise en surbrillance des paramètres.](images/b2b-configuring-accounts-profile.png)

La variable **[!UICONTROL Paramètres du compte]** s’ouvre. À partir de là, sélectionnez la variable **[!UICONTROL Activation de la mise en correspondance de pistes/comptes]** pour activer la fonction. Utilisez le menu déroulant pour sélectionner **[!UICONTROL Qualité]** pour le **[!UICONTROL Correspondance de cadence]** . Enfin, sélectionnez la **[!UICONTROL Critères de correspondance]** options suivies de **[!UICONTROL Enregistrer]** pour confirmer vos paramètres et revenir au **[!UICONTROL Profils de compte]** écran.

>[!NOTE]
>
> L&#39;adresse ne peut pas être utilisée comme seul critère correspondant. Un ou plusieurs autres critères correspondants doivent être sélectionnés.

![Configuration des paramètres du compte](images/b2b-configuring-account-settings.png)

Pour en savoir plus sur la mise en correspondance des prospects avec les comptes, reportez-vous à la section [Correspondance de comptes dans Real-Time CDP B2B - Aperçu](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

## Parcourir les profils de compte {#browse-account-profiles}

Pour parcourir les profils de compte, commencez par sélectionner **[!UICONTROL Profils]** sous [!UICONTROL Comptes] dans le volet de navigation de gauche.

Dans l’onglet **[!UICONTROL Parcourir]**, vous pouvez explorer les profils de compte à l’aide d’un identifiant de compte provenant d’une source d’entreprise connectée ou en saisissant directement les détails de la source.

![Utiliser l’identifiant de compte pour explorer les profils](images/b2b-account-browse-by.png)

### Parcourir par [!UICONTROL source d’entreprise connectée] {#browse-by-connected-enterprise-source}

Pour parcourir les profils de compte par source d’entreprise connectée, sélectionnez **[!UICONTROL Source d’entreprise connectée]** dans la liste déroulante **[!UICONTROL Parcourir par]**, puis choisissez une source connectée à l’aide du bouton de sélection situé en regard du champ **[!UICONTROL Source]**.

![Parcourir les profils de compte par source d’entreprise connectée](images/b2b-account-browse.png)

Cela ouvre la boîte de dialogue **[!UICONTROL Sélectionner la source]**, dans laquelle vous pouvez sélectionner une source en fonction des connexions établies par votre organisation.

>[!NOTE]
>
>Plusieurs sources peuvent être configurées pour le même fournisseur de services (par exemple, Marketo) pour votre organisation. Il est donc important de vérifier le nom de la connexion, le système source et l’instance du système source pour vous assurer que vous utilisez la bonne instance source pour votre recherche.

Pour en savoir plus sur la connexion des sources d’entreprise, consultez la [présentation des sources](../sources/sources-overview.md).

Vous pouvez choisir une source en sélectionnant le bouton radio en regard du nom de la connexion, puis en utilisant **[!UICONTROL Sélectionner]** pour revenir à l’onglet [!UICONTROL Parcourir].

![Sélectionner le processus source](images/b2b-account-select-source.png)

Une fois la source sélectionnée, vous devez saisir un **[!UICONTROL identifiant de compte]** associé à la source. Par exemple, pour sélectionner une source Salesforce, vous devez saisir un identifiant de compte à partir de l’instance Salesforce afin d’afficher le profil de compte associé à cet identifiant.

>[!NOTE]
>
>Pour les identifiants de compte Marketo, deux tables de compte peuvent être référencées. Vous devez donc utiliser une syntaxe spécifique pour vous assurer que vous consultez le compte approprié.
>
>La syntaxe standard la plus courante est l’identifiant de compte Marketo suivi de `.mkto_org` (par exemple, `1234567.mkto_org`). Les clients Marketing basés sur un compte Marketo peuvent avoir des valeurs supplémentaires qui se trouvent à l’aide de l’identifiant de compte Marketo suivi de `.mkto_account`. Si vous ne savez pas quelle syntaxe utiliser, contactez votre administrateur Marketo.

![Sélection de l’ID de compte](images/b2b-account-browse-id.png)

### Parcourir par [!UICONTROL Autres] {#browse-by-others}

Real-Time CDP, Édition B2B, prend en charge la possibilité d’effectuer une recherche directe en vous permettant de saisir une **[!UICONTROL Nom de la source]**, **[!UICONTROL Instance source]**, et **[!UICONTROL Identifiant de compte]** pour un compte que vous souhaitez afficher. En saisissant directement le nom et l’instance de la source, vous fournissez le contexte nécessaire pour qu’Experience Platform recherche et affiche les données de profil de compte correctes.

La possibilité d’effectuer une recherche directe est utile dans les cas où une connexion source directe aux données n’est pas possible. Par exemple, si votre entreprise a mis en place des politiques de gouvernance des données qui empêchent la connexion directe à un CRM, vous pouvez exporter ces données vers un système de stockage dans le cloud, puis les ingérer dans Experience Platform.

Autre exemple : vous effectuez une transformation sur les données entre le moment où elles quittent un système et celui où elles entrent dans Platform. Vous pouvez utiliser la fonctionnalité de recherche directe pour fournir un contexte aux données (par exemple, en indiquant qu’il s’agit de données Marketo, bien qu’elles proviennent d’un compartiment Amazon S3) afin que le système sache où chercher les données et comment en effectuer le rendu correct.

Pour lancer une recherche directe, sélectionnez **[!UICONTROL Autres]** dans la liste déroulante **[!UICONTROL Parcourir par]**, puis saisissez un **[!UICONTROL Nom source]**, une **[!UICONTROL Instance source]** et un **[!UICONTROL ID de compte]** pour le compte que vous souhaitez afficher.

![Navigation par d’autres](images/b2b-account-browse-adhoc.png)

## Affichage des détails du profil de compte {#view-account-profile-details}

Après avoir utilisé l’onglet **[!UICONTROL Parcourir]** pour localiser un profil de compte, sélectionner l’**[!UICONTROL Identifiant de profil]** ouvre l’onglet **[!UICONTROL Détail]** du profil de compte. Les informations de profil affichées dans l’onglet **[!UICONTROL Détail]** ont été fusionnées à partir de plusieurs fragments de profil afin de former une vue unique du compte individuel. Cela inclut les détails du compte, tels que les attributs de base et les données de médias sociaux.

L’affichage des champs par défaut peut également être modifié au niveau de l’organisation afin d’afficher les attributs de profils de compte préférés.

>[!NOTE]
>
>Des fonctionnalités similaires sont disponibles pour les profils clients. Un guide détaillé a également été créé et fournit des instructions sur l’ajout et la suppression d’attributs, le redimensionnement des panneaux, etc. Pour en savoir plus, consultez le [guide de personnalisation des détails du profil](../../profile/ui/profile-customization.md).

![Affichage des détails du profil du compte](images/b2b-account-details.png)

Vous pouvez afficher des détails supplémentaires concernant le compte en sélectionnant l’un des autres onglets disponibles. Ces onglets comprennent les attributs, les personnes et l’onglet relatif aux opportunités, qui affiche les opportunités ouvertes et clôturées liées au compte sur l’ensemble de vos systèmes d’entreprise. Pour plus d’informations sur chaque onglet, consultez les sections suivantes.

## Onglet Attributs {#attributes-tab}

L’onglet **[!UICONTROL Attributs]** répertorie toutes les informations d’enregistrement liées au compte. Cela inclut les données d’attributs provenant de plusieurs sources qui ont été fusionnées pour former une vue unique du compte.

En plus de pouvoir afficher les données dans une liste, vous pouvez utiliser la barre de recherche pour rechercher des attributs spécifiques ou afficher les données d’enregistrement au format JSON.

![Onglet Attributs](images/b2b-account-attributes.png)

## Onglet Personnes {#people-tab}

L’onglet **[!UICONTROL Personnes]** fournit une liste des personnes associées au compte. Il peut s’agir de contacts et de prospects provenant de différents systèmes d’entreprise gérés par différentes équipes au sein de votre entreprise. Toutefois, dans Real-Time CDP, Edition B2B, ils sont présentés sous la forme d’une liste unique qui vous permet d’obtenir une vue plus globale des contacts de votre compte.

>[!NOTE]
>
>L’onglet [!UICONTROL Personnes] affiche une liste comportant au maximum 25 personnes associées au compte. Pour les comptes comptant plus de 25 personnes associées, le système affiche un échantillonnage aléatoire de 25 enregistrements.

En plus de vous montrer un instantané des informations du contact, chaque personne répertoriée inclut également un **[!UICONTROL Identifiant de profil]**, qui est un lien cliquable qui vous permet d’explorer le profil client en temps réel de cette personne. Pour en savoir plus sur l’affichage des profils clients individuels liés à vos comptes, consultez le guide pour [exploration des profils dans Real-Time CDP, édition B2B](../profile/profile-browse.md).

![Onglet Personnes](images/b2b-account-people.png)

## Onglet Opportunités {#opportunities-tab}

L’onglet **[!UICONTROL Opportunités]** fournit des informations sur les opportunités ouvertes et clôturées liées au compte. Ces opportunités peuvent être ingérées dans Experience Platform à partir de sources multiples. Toutefois, Real-Time CDP, version B2B, permet aux marketeurs de voir facilement toutes ces opportunités ensemble au même endroit.

>[!NOTE]
>
>L’onglet [!UICONTROL Opportunités] affiche une liste comportant au maximum 25 opportunités associées au compte. Pour les comptes comportant plus de 25 opportunités associées, le système affiche un échantillonnage aléatoire de 25 enregistrements.

Chaque opportunité inclut des informations telles que son nom, son montant, son avancée et si elle est ouverte, clôturée, gagnée ou perdue.

![Onglet Opportunités de compte](images/b2b-account-opportunities.png)

## Onglet Comptes associés {#related-accounts-tab}

La variable **[!UICONTROL Comptes associés]** fournit des informations sur d’autres comptes susceptibles d’être liés au compte que vous parcourez. Pour obtenir des informations détaillées sur la fonctionnalité, reportez-vous à la section [présentation des comptes liés](/help/rtcdp/b2b-ai-ml-services/related-accounts.md).

>[!NOTE]
>
>* Un groupe de comptes associés peut comporter 30 profils de compte au maximum. Si plus de 30 profils de compte ont été trouvés associés, ils sont arbitrairement divisés en plusieurs groupes, chacun ne comptant pas plus de 30 membres. Le groupe Comptes associés d’un profil de compte s’inclut toujours.
>* La variable [!UICONTROL Comptes associés] affiche actuellement une liste de 25 comptes associés au compte que vous parcourez. Il s’agit d’une limitation qui sera corrigée lors d’une prochaine mise à jour. Malgré cette limite de l’interface utilisateur, lorsque vous utilisez des comptes associés dans des définitions de segment, pour les groupes de 30 profils de compte associés, tous les profils sont utilisés pour le ciblage.

Chaque compte associé comprend des informations telles que l’identifiant et le nom du profil du compte, sa clé de source de compte, ainsi que d’autres informations relatives à la page d’accueil, à l’adresse, au compte parent, au téléphone, au secteur industriel et aux recettes annuelles.

![Onglet Comptes associés](images/b2b-account-related-accounts.png)

Vous pouvez utiliser les comptes associés de cette liste à des fins de segmentation. Voir [exemple de segmentation](/help/rtcdp/segmentation/b2b.md#related-account) pour comprendre comment utiliser les comptes associés afin d’étendre votre portée dans les définitions de segment.