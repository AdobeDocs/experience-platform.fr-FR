---
keywords: Experience Platform;guide de l’utilisateur;IA dédiée aux clients;rubriques les plus consultées; contrôles d’accès; créer un modèle;
solution: Experience Platform
feature: Customer AI
title: Contrôle d’accès pour l’IA dédiée aux clients
description: Ce document fournit des informations sur le contrôle d’accès basé sur les attributs pour l’IA dédiée aux clients.
exl-id: 02e3b6a4-304a-4ac4-b07c-010531101feb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 93%

---

# Contrôle d’accès basé sur les attributs dans Customer AI

>[!IMPORTANT]
>
>Le contrôle d’accès basé sur les attributs est actuellement disponible dans une version limitée uniquement.

[Le contrôle d’accès basé sur les attributs](../../../access-control/abac/overview.md) est une fonctionnalité d’Adobe Experience Platform qui permet aux administrateurs et administratrices de contrôler l’accès à des objets et/ou fonctionnalités spécifiques en fonction d’attributs. Les attributs peuvent être des métadonnées ajoutées à un objet, comme un libellé ajouté à un champ ou à un segment de schéma. Un administrateur définit des politiques d’accès qui comprennent des attributs afin de gérer les autorisations d’accès des utilisateurs.

Cette fonctionnalité vous permet d’étiqueter les champs de schéma d’un modèle de données d’expérience (XDM) avec des libellés définissant l’utilisation de l’organisation ou des données. En parallèle, les administrateurs peuvent utiliser l’interface d’administration des utilisateurs et des rôles pour définir des politiques d’accès relatives aux champs de schéma XDM. Cela permet ainsi une meilleure gestion des accès accordés aux utilisateurs ou aux groupes d’utilisateurs (utilisateurs internes, externes ou tiers). Enfin, le contrôle d’accès basé sur les attributs permet aux administrateurs de gérer l’accès à des segments spécifiques.

Grâce au contrôle d’accès basé sur les attributs, les administrateurs de votre organisation peuvent contrôler l’accès des utilisateurs aux données personnelles sensibles (SPD) et aux informations d’identification personnelle (PII) sur l’ensemble des workflows et ressources d’Experience Platform. Les administrateurs et administratrices peuvent définir des rôles d’utilisateur qui n’ont accès qu’à des champs spécifiques et aux données correspondant à ces champs.

En raison du contrôle d’accès basé sur les attributs, certains champs et certaines fonctionnalités ont un accès limité et ne sont pas disponibles pour certains modèles de service d’IA dédiée aux clients. Par exemple, « Identité », « Définition de score » et « Clone ».

![L’espace de travail de l’IA dédiée aux clients avec les champs restreints des résultats du modèle de service mis en surbrillance.](../images/user-guide/unavailable-functionalities.png)

En haut de la **page insights** de l’espace de travail de l’IA dédiée aux clients, notez que les détails dans la barre latérale, la définition de score, l’identité et les attributs de profil affichent tous « Accès limité. »

![L’espace de travail de l’IA dédiée aux clients avec les champs restreints du schéma mis en surbrillance.](../images/user-guide/access-restricted.png)

Lorsque vous prévisualisez des jeux de données avec un schéma limité sur la page **[!UICONTROL Créer un modèle de workflow]**, un avertissement s’affiche pour vous informer qu’[!UICONTROL en raison des restrictions d’accès, certaines informations ne s’affichent pas dans l’aperçu du jeu de données.].

![L’espace de travail de l’IA dédiée aux clients avec les champs restreints des jeux de données d’aperçu avec les résultats de schéma limités mis en surbrillance.](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

Après avoir créé un modèle contenant des informations restreintes et procédé à l’étape **[!UICONTROL Définir un objectif]**, un avertissement s’affiche en haut de l’écran : [!UICONTROL En raison des restrictions d’accès, certaines informations ne s’affichent pas dans la configuration.].

![L’espace de travail de l’IA dédiée aux clients avec les champs restreints des résultats du modèle de service mis en surbrillance.](../images/user-guide/information-not-displayed-save-and-exit.png)

Lors de l’utilisation du contrôle d’accès, les privilèges **Afficher I’IA dédiée au client** et **Gérer l’IA dédiée aux clients** permettent d’accéder à différentes fonctionnalités de l’IA dédiée aux clients. L’autorisation **Gérer l’IA dédiée aux clientsI** vous permet de **créer**, **mettre à jour**, **supprimer**, **activer** ou **désactiver** un modèle alors que **Afficher l’IA dédiée aux clients** vous permet de le lire ou de le visualiser. Les actions **créer**, **mettre à jour** et **supprimer** sont enregistrées par les journaux d’audit.

Consultez la documentation pour apprendre à [attribuer des autorisations pour le contrôle d’accès](../../../access-control/home.md) ou comment [utiliser les journaux d’audit pour surveiller l’accès et l’activité](../../../landing/governance-privacy-security/audit-logs/overview.md).

## Étapes suivantes

En lisant ce guide, les principes du contrôle dʼaccès dans [!DNL Experience Platform] vous ont été présentés. Vous pouvez désormais poursuivre en consultant le [guide dʼutilisation du contrôle dʼaccès](../overview.md) pour obtenir des instructions détaillées sur lʼutilisation dʼ[!DNL Admin Console] afin de créer des profils de produit et attribuer des autorisations dans [!DNL Experience Platform].
