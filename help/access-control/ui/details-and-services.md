---
keywords: Experience Platform;accueil;rubriques populaires;profil produit
solution: Experience Platform
title: Gestion des détails et des services supplémentaires pour un profil de produit
topic-legacy: user guide
description: Ce document reprend les étapes nécessaires à la gestion des détails et des services supplémentaires pour un profil de produit dans Adobe Admin Console. Vous pouvez configurer les détails d’un profil et accéder aux services supplémentaires à partir du menu Paramètres du profil.
exl-id: ac9c2213-f2fb-44be-9334-87fada8a4717
source-git-commit: 2844ffd7270ffcc2fba4da08dda1aea238cf6c9f
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 48%

---

# Gestion des détails et des services supplémentaires pour un profil de produit

Vous pouvez configurer les détails d’un profil et accéder aux services supplémentaires à partir du menu **[!UICONTROL Paramètres du profil]**. Pour accéder au menu, sélectionnez **[!UICONTROL Paramètres]** dans la page **[!UICONTROL Profil du produit]**.

![paramètres](../images/settings.png)

Le menu **[!UICONTROL Modifier le profil de produit]** s’affiche, à partir de l’onglet **[!UICONTROL Modifier les détails du profil]**. Cet onglet vous permet de saisir et de modifier le nom du profil et sa description. Vous pouvez également modifier le nom d’affichage ainsi que les paramètres de notification par e-mail de votre compte.

![edit-product-profile](../images/edit-product-profile.png)

Sélectionnez **[!UICONTROL Suivant]** pour accéder à la page **[!UICONTROL Activer les services]**.

Le menu **[!UICONTROL Activer les services]** permet de modifier l’accès d’un profil à des services [!DNL Platform] supplémentaires qui ont été initialement configurés lors de la création du profil. En fonction de votre abonnement [!DNL Platform], ces services peuvent inclure :

- [!DNL Data Science Workspace]
- [!DNL Query Service]
- L’interface utilisateur de [!DNL Real-Time Customer Data Platform] (pour la plateforme de données client en temps réel uniquement)
- Interface utilisateur B2B

Cliquez sur le bouton à droite d’un service particulier pour l’activer ou le désactiver. Vous pouvez également cocher la case **[!UICONTROL Tout sur]** pour activer ou désactiver tous les services répertoriés.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

![enable-services](../images/enable-services.png)

Les clients autorisés à utiliser l’édition B2B ou B2P ont accès à l’interface utilisateur B2B. L’interface utilisateur B2B peut être configurée pour les utilisateurs via le [!UICONTROL menu Activer les services]. Sélectionnez la bascule en regard de [!UICONTROL L’interface utilisateur B2B] pour activer le service pour un profil de produit particulier, puis sélectionnez **[!UICONTROL Enregistrer]**.

Le bouton d’activation/désactivation de l’interface utilisateur B2B permet aux utilisateurs d’afficher les processus B2B relatifs à la gestion des comptes et des opportunités, ainsi que de créer des segments liés à B2B. Pour plus d’informations, voir la documentation sur [[!DNL Real-time Customer Data Platform B2B Edition]](../../rtcdp/b2b-overview.md).

![enable-b2b](../images/enable-b2b.png)