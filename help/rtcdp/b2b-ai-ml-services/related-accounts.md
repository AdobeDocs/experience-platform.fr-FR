---
title: Comptes associés dans Real-Time CDP B2B Edition
type: Documentation
description: Présentation et informations supplémentaires sur la fonction des comptes associés dans Real-Time CDP Experience Platform B2B.
feature: Get Started, Profiles, B2B
badgeB2B: label="Édition B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 37fd2cdb-87c0-4e5e-9599-ad4f397f7c28
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 21%

---

# Comptes associés dans Real-Time CDP B2B Edition

## Vue d’ensemble {#overview}

Les entreprises B2B ont souvent leurs informations client stockées dans plusieurs systèmes, chacun ne contenant que des données partielles, voire conflictuelles, pour la même entité commerciale physique. Il est donc très difficile d’avoir une visualisation précise de leurs clients, ce qui réduit l’efficacité et l’efficience de leurs efforts de marketing et de vente B2B.

| Identifiant | Nom | Site web | Secteur industriel | État | Téléphone | A une opportunité ouverte avec quantité > `$1 million` |
|---|---|---|---|---|---|---|
| 1 | Acme | acme.com | Logiciels | CA | (408)536-6000 |   |
| 2 | Acme | acm.com | Logiciels | CA | 4085366000 | x |
| 3 | Acme Inc |   |   | CA | (408)5366000 |   |
| 4 | Service de conseil Acme | `http://www.acme.com/consulting` | Conseil technologique | NY | (212)471-0904 | x |
| 5 | Acm IT |   |   | CA |   |   |

{style="table-layout:auto"}

Avec les comptes associés, [!DNL Real-Time CDP B2B] affiche désormais la liste des comptes similaires au compte que vous parcourez.

![Écran affichant les comptes associés dans l’interface utilisateur de l’Experience Platform.](/help/rtcdp/b2b-ai-ml-services/assets/related-accounts-in-ui.png)

Utilisez cette fonction pour afficher les profils de compte associés pour un profil de compte dans l’interface utilisateur de l’Experience Platform, puis inclure les comptes associés dans vos définitions de segment afin d’élargir votre portée ou d’appliquer des critères plus larges dans vos segments.

## Activation du service de comptes associé {#enable}

Pour activer le service, sélectionnez **[!UICONTROL Profils]** dans la barre latérale suivie de **[!UICONTROL Paramètres]**.

![Interface utilisateur de l’Experience Platform qui surligne les profils et les paramètres.](../assets/../b2b-ai-ml-services/assets/related-account-settings.png)

Sélectionner le bouton bascule en regard de [!UICONTROL Activation des comptes associés] pour activer le service, puis sélectionnez **[!UICONTROL Enregistrer]**.

![L’écran Paramètres du compte met en surbrillance le bouton bascule et l’enregistrement.](../assets/../b2b-ai-ml-services/assets/related-account-toggle.png)

## Fonctionnement {#how-it-works}

Les tâches d’apprentissage automatique exécutées quotidiennement utilisent un algorithme hiérarchique pour regrouper des profils de compte similaires en groupes basés sur trois facteurs :

* Lien du compte parent
* Domaine web
* Nom du compte

Après une tâche de traitement réussie, chaque membre du groupe de profils de compte est balisé avec la liste Comptes associés . Vous pouvez afficher la liste dans le **Comptes associés** de la page Profil de compte , et utilisez les comptes associés dans les définitions de segment.

Pour plus d’informations sur la variable [traitements de comptes liés à l’enrichissement de profil](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).

## Affichage des comptes associés {#how-to-view}

Vous pouvez afficher les comptes associés d’un compte que vous parcourez dans l’interface utilisateur de l’Experience Platform.

Pour plus d’informations sur la variable [comment trouver des comptes associés dans l’interface utilisateur](/help/rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab).

## Utilisation de comptes liés {#how-to-use}

Vous pouvez utiliser des comptes et des comptes associés dans la segmentation. La décision d’utiliser des comptes associés dans vos définitions de segment dépend de votre cas d’utilisation marketing. Par exemple, vous pouvez utiliser des comptes associés pour les campagnes de marketing par e-mail ou de publicité, dans lesquels vous pouvez accepter une précision moindre en échange d’une portée plus large.

Voir [exemple de segmentation](/help/rtcdp/segmentation/b2b.md#related-accounts) qui utilise des comptes associés.
