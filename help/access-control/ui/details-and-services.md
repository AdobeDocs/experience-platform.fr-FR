---
keywords: Experience Platform;accueil;rubriques populaires;profil produit
solution: Experience Platform
title: Gestion des détails et des services supplémentaires pour un profil de produit
description: Ce document reprend les étapes nécessaires à la gestion des détails et des services supplémentaires pour un profil de produit dans Adobe Admin Console. Vous pouvez configurer les détails d’un profil et accéder aux services supplémentaires à partir du menu Paramètres du profil.
exl-id: ac9c2213-f2fb-44be-9334-87fada8a4717
TQID: https://experienceleague.adobe.com/cd5Su-Bo-e4yNu4mhX-8MrD2Jw0dFLm-HYHJGb01MR4
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 273
ht-degree: 63%

---

# Gestion des détails et des services supplémentaires pour un profil de produit

Vous pouvez configurer les détails d’un profil et accéder aux services supplémentaires à partir du menu **[!UICONTROL Profile Settings]**. Pour accéder au menu, sélectionnez **[!UICONTROL Settings]** dans la page de **[!UICONTROL Product Profile]**.

![paramètres](../images/settings.png)

Le menu **[!UICONTROL Edit product profile]** s’affiche, en commençant par l’onglet **[!UICONTROL Edit profile details]** . Cet onglet vous permet de saisir et de modifier le nom du profil et sa description. Vous pouvez également modifier le nom d’affichage ainsi que les paramètres de notification par e-mail de votre compte.

![edit-product-profile](../images/edit-product-profile.png)

Sélectionnez **[!UICONTROL Next]** pour accéder à la page **[!UICONTROL Enable services]**.

Le menu **[!UICONTROL Enable services]** vous permet de modifier l’accès d’un profil aux services de [!DNL Experience Platform] supplémentaires qui ont été initialement configurés lors de la création du profil. En fonction de votre abonnement [!DNL Experience Platform], ces services peuvent inclure :

- [!DNL Data Science Workspace]
- [!DNL Query Service]
- Interface utilisateur de [!DNL Adobe Real-Time Customer Data Platform] (pour Real-Time CDP uniquement)
- Interface utilisateur B2B

Cliquez sur le bouton à droite d’un service particulier pour l’activer ou le désactiver. Vous pouvez également cocher la case **[!UICONTROL All on]** pour activer ou désactiver tous les services répertoriés.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Save]**.

![enable-services](../images/enable-services.png)

Les clients éligibles à l’édition B2B ou B2P ont accès à l’interface utilisateur B2B. L’interface utilisateur B2B peut être fournie aux utilisateurs par le biais du [!UICONTROL Enable services menu] . Sélectionnez le bouton bascule en regard de [!UICONTROL B2B UI] pour activer le service pour un profil de produit spécifique, puis sélectionnez **[!UICONTROL Save]**.

L’option Activer/Désactiver de l’interface utilisateur B2B permet d’afficher les workflows B2B relatifs à la gestion des comptes et des opportunités, ainsi que de créer des segments liés au B2B. Pour plus d’informations, consultez la documentation sur [[!DNL Adobe Real-Time Customer Data Platform B2B Edition]](../../rtcdp/b2b-overview.md).

![enable-b2b](../images/enable-b2b.png)