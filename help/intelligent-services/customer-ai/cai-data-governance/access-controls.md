---
keywords: Experience Platform;guide de l’utilisateur;service clientèle;rubriques les plus consultées;contrôles d’accès;créer un modèle ;
solution: Experience Platform
feature: Customer AI
title: Contrôle d’accès pour Customer AI
description: Ce document fournit des informations sur le contrôle d’accès basé sur les attributs pour Customer AI.
source-git-commit: 6f386d859b8553050ead266fad0e473c7cf7095e
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 37%

---


# Contrôle d’accès basé sur les attributs

>[!IMPORTANT]
>
>Le contrôle d’accès basé sur les attributs est actuellement disponible dans une version limitée uniquement.

[Le contrôle d’accès basé sur les attributs est une fonctionnalité d’Adobe Experience Platform qui permet aux administrateurs de contrôler l’accès à des objets et/ou fonctionnalités spécifiques en fonction d’attributs.](../../../access-control/abac/overview.md) Les attributs peuvent être des métadonnées ajoutées à un objet, comme un libellé ajouté à un champ ou à un segment de schéma. Un administrateur définit des stratégies d’accès qui comprennent des attributs afin de gérer les autorisations d’accès des utilisateurs.

Cette fonctionnalité vous permet d’étiqueter les champs de schéma d’un modèle de données d’expérience (XDM) avec des libellés définissant l’utilisation de l’organisation ou des données. En parallèle, les administrateurs peuvent utiliser l’interface d’administration des utilisateurs et des rôles pour définir des politiques d’accès relatives aux champs de schéma XDM. Cela permet ainsi une meilleure gestion des accès accordés aux utilisateurs ou aux groupes d’utilisateurs (utilisateurs internes, externes ou tiers). Enfin, le contrôle d’accès basé sur les attributs permet aux administrateurs de gérer l’accès à des segments spécifiques.

Grâce au contrôle d’accès basé sur les attributs, les administrateurs de votre organisation peuvent contrôler l’accès des utilisateurs aux données personnelles sensibles (SPD) et aux informations d’identification personnelle (PII) sur l’ensemble des workflows et ressources de Platform. Les administrateurs peuvent définir des rôles d’utilisateur qui n’ont accès qu’à des champs spécifiques et aux données correspondant à ces champs.

En raison du contrôle d’accès basé sur les attributs, certains champs et certaines fonctionnalités ont un accès limité et ne sont pas disponibles pour certains modèles de service Customer AI. Par exemple, &quot;Identité&quot;, &quot;Définition de score&quot; et &quot;Cloner&quot;.

![L’espace de travail Customer AI avec les champs restreints des résultats du modèle de service mis en surbrillance.](../images/user-guide/unavailable-functionalities.png)

En haut de l’espace de travail de Customer AI **page insights**, notez que les détails de la barre latérale, de la définition de score, de l’identité et des attributs de profil affichent tous &quot;Accès limité&quot;.

![Espace de travail Customer AI avec les champs restreints du schéma mis en surbrillance.](../images/user-guide/access-restricted.png)

Lorsque vous prévisualisez des jeux de données avec un schéma limité sur l’objet **[!UICONTROL Workflow Créer un modèle]** , un avertissement s’affiche pour vous informer que [!UICONTROL En raison des restrictions d’accès, certaines informations ne s’affichent pas dans l’aperçu du jeu de données.]

![L’espace de travail Customer AI avec les champs restreints des jeux de données d’aperçu avec les résultats de schéma limités mis en surbrillance.](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

Après avoir créé un modèle contenant des informations restreintes, passez à la **[!UICONTROL Définition d’un objectif]** , un avertissement s’affiche en haut de l’écran : [!UICONTROL En raison des restrictions d’accès, certaines informations ne s’affichent pas dans la configuration.]

![L’espace de travail Customer AI avec les champs restreints des résultats du modèle de service mis en surbrillance.](../images/user-guide/information-not-displayed-save-and-exit.png)

Lors de l’utilisation du contrôle d’accès, la variable **Affichage de Customer AI** et **Gestion de Customer AI** Les privilèges permettent d’accéder à différentes fonctionnalités de Customer AI. Le **Gestion de Customer AI** permission vous permet de **create**,**update**, **delete**, **enable** ou **disable** un modèle pendant **Affichage de Customer AI** vous permet de le lire ou de le visualiser. Le **create**, **update** et **delete** Les actions sont enregistrées par les journaux d’audit.

Consultez la documentation pour en savoir plus [attribution d’autorisations pour le contrôle d’accès](../../../access-control/home.md) ou comment [utiliser les journaux d’audit pour surveiller l’accès et l’activité ;](../../../landing/governance-privacy-security/audit-logs/overview.md).

## Étapes suivantes

En lisant ce guide, les principes du contrôle dʼaccès dans [!DNL Experience Platform] vous ont été présentés. Vous pouvez désormais poursuivre en consultant le [guide dʼutilisation du contrôle dʼaccès](../overview.md) pour obtenir des instructions détaillées sur lʼutilisation dʼ[!DNL Admin Console] afin de créer des profils de produit et attribuer des autorisations dans [!DNL Platform].