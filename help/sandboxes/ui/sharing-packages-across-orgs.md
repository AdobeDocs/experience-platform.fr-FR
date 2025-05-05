---
title: Partage de modules à l’échelle de l’entreprise à l’aide d’outils Sandbox
description: Découvrez comment utiliser les outils Sandbox dans Adobe Experience Platform pour partager des modules entre différentes organisations.
source-git-commit: 77994c1cdd185cc8a2963c5aa2eb345c8702fe02
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 0%

---

# Partage de modules entre différentes organisations à l’aide des outils Sandbox

Améliorez la précision de la configuration dans les environnements de test et exportez et importez en toute transparence les configurations des environnements de test entre les environnements de test de différentes organisations à l’aide de la fonctionnalité d’outil d’environnement de test. Ce document explique comment utiliser les outils Sandbox dans Adobe Experience Platform pour partager des modules entre différentes organisations. Il existe deux types de packages partagés :

- **Package privé**

Les [packages privés](#private-packages) ne peuvent être partagés qu’avec les organisations qui ont approuvé la demande de partage de l’organisation source.

- **Package public**

[Les packages publics](#public-packages) peuvent être importés sans approbation supplémentaire. Ces modules peuvent être partagés sur le site web, le blog ou la plateforme d’un partenaire. La payload du module permet de copier et coller des modules de ces canaux vers l’organisation cible.

## Packages privés {#private-packages}

>[!NOTE]
>
>Pour lancer et approuver une demande de partage et partager des modules entre différentes organisations, vous devez disposer de l’autorisation de contrôle d’accès basé sur le rôle **package-share** .

Utilisez la fonction Outils Sandbox pour créer des partenariats, suivre les statuts des demandes de partenariat, gérer les partenariats existants et partager des modules avec des organisations partenaires.

### Création d’une demande de partenariat d’organisation

Pour créer une demande de partenariat d’organisation, accédez à l’onglet **[!UICONTROL Sandbox]** **[!UICONTROL Partner Orgs]** . Sélectionnez ensuite **[!UICONTROL Gérer les organisations partenaires]**.

![L’interface utilisateur des environnements de test, avec l’onglet Organisations partenaires et Gérer les organisations partenaires en surbrillance.](../images/ui/sandbox-tooling/private-manage-partner-orgs.png)

Dans la boîte de dialogue [!UICONTROL Gestion des partenaires de package], saisissez l’ID d’organisation dans **[!UICONTROL Saisir l’ID d’organisation]** et appuyez sur Entrée (Windows) ou Retour (Mac). L’ID d’organisation s’affiche dans la section **[!UICONTROL ID d’organisation sélectionnés]** ci-dessous. Après avoir ajouté les ID, sélectionnez **[!UICONTROL Confirmer]**.

>[!TIP]
>
>Vous pouvez saisir plusieurs ID d’organisation à la fois à l’aide de listes séparées par des virgules ou en saisissant chaque ID d’organisation suivi d’une entrée.

![La boîte de dialogue des organisations partenaires de package avec Entrer l’ID d’organisation, les ID d’organisation sélectionnés et Confirmer mise en surbrillance.](../images/ui/sandbox-tooling/private-enter-org-id.png)

La demande de partage est envoyée avec succès à l’organisation partenaire et vous êtes renvoyé à l’onglet [!UICONTROL Sandbox] **&#x200B;**&#x200B;, qui affiche la **[!UICONTROL requête sortante]**.

![Onglet Organisations partenaires avec la requête sortante mise en surbrillance.](../images/ui/sandbox-tooling/private-outgoing-request.png)

### Autoriser une demande de partenariat {#authorize-request}

Pour autoriser une demande de partenariat d’organisation, accédez à l’onglet [!UICONTROL Sandbox] **[!UICONTROL Partner Orgs]** . Sélectionnez ensuite **[!UICONTROL Demande entrante]**.

![L’interface utilisateur des environnements de test avec l’onglet Organisations partenaires et la Requête entrante mise en surbrillance.](../images/ui/sandbox-tooling/private-authorise-partner-org.png)

Actuellement, le **[!UICONTROL Statut]** de la requête est **En attente**. Pour approuver la requête, sélectionnez les points de suspension (`...`) en regard de la requête sélectionnée, puis sélectionnez **[!UICONTROL Approuver]** dans la liste déroulante.

![ Liste des requêtes entrantes affichant le menu déroulant avec l’option Approuver mise en surbrillance.](../images/ui/sandbox-tooling/private-approve-partner-org.png)

La boîte de dialogue **[!UICONTROL Réviser la demande d’organisation du partenaire]** affiche des détails sur la demande de partenariat de l’organisation. Saisissez un [!UICONTROL motif] pour approbation, puis sélectionnez **[!UICONTROL Approuver]**.

![ Boîte de dialogue de demande d’organisation du partenaire d’examen avec motif et approbation en surbrillance.](../images/ui/sandbox-tooling/private-approval-partner-org.png)

Vous êtes renvoyé à la page [!UICONTROL Requête entrante] et l’état de la requête a été mis à jour vers **[!UICONTROL Approuvé]**.

![Liste des requêtes entrantes avec Approuvé en surbrillance.](../images/ui/sandbox-tooling/private-approved-partner-org.png)

Utilisez ce processus/processus pour partager des modules entre votre organisation et l’organisation source.

### Partage de modules avec des organisations partenaires {#share-package}

>[!NOTE]
>
>Seuls les modules dont l’état est **Publié** peuvent être partagés.

Pour partager un package avec une organisation partenaire approuvée, accédez à l’onglet [!UICONTROL Sandbox] **[!UICONTROL Packages]** . Ensuite, sélectionnez les points de suspension (`...`) en regard du module, puis sélectionnez **[!UICONTROL Partager le module]** dans le menu déroulant.

![Liste des packages affichant le menu déroulant avec le partage de package en surbrillance.](../images/ui/sandbox-tooling/private-share-package.png)

Dans la boîte de dialogue **[!UICONTROL Partager le package]**, sélectionnez le package à partager dans la liste déroulante **[!UICONTROL Partager les paramètres]**, puis sélectionnez **[!UICONTROL Confirmer]**.

>[!TIP]
>
>Il est possible de sélectionner plusieurs organisations. Les organisations sélectionnées s’affichent sous la liste déroulante [!UICONTROL Paramètres de partage].

![Boîte de dialogue Partager le package avec les paramètres de partage et Confirmer mise en surbrillance.](../images/ui/sandbox-tooling/private-share-package-confirm.png)

## Packages publics {#public-packages}

Utilisez la fonction Outils Sandbox pour créer des modules publics partageables qui ne nécessitent aucune approbation supplémentaire et qui sont facilement importés avec l’utilisation de la charge utile du module.

### Mettre à jour la disponibilité des packages au public {#update-package}

Pour mettre à jour le type de disponibilité d’un package, accédez à l’onglet [!UICONTROL Sandbox] **[!UICONTROL Packages]** . Sélectionnez ensuite les points de suspension (`...`) en regard du package, puis sélectionnez **[!UICONTROL Mettre à jour vers le package public]** dans le menu déroulant.

![L’interface utilisateur des environnements de test avec l’onglet Packages et le menu d’option de liste déroulante avec l’option Mettre à jour vers le package public mise en surbrillance.](../images/ui/sandbox-tooling/update-to-public.png)

Dans la boîte de dialogue **[!UICONTROL Remplacer la disponibilité du package par public]** , vérifiez que le nom du package est correct et sélectionnez **[!UICONTROL Confirmer]**.

>[!IMPORTANT]
>
> Une fois qu’un kit a été rendu public, il ne peut plus être reconverti en kit privé.

![Modifiez la disponibilité du package dans la boîte de dialogue publique avec l&#39;option Confirmer mise en surbrillance.](../images/ui/sandbox-tooling/change-package-availability.png)

### Partage de modules à l’aide de la charge utile du module

Pour partager le package public, sélectionnez les ellipses (`...`) en regard du package, puis sélectionnez **[!UICONTROL Copier la payload du package]**.

![L’interface utilisateur des environnements de test affiche un menu déroulant de packages individuels avec la charge utile Copier le package mise en surbrillance.](../images/ui/sandbox-tooling/copy-package-payload.png)

La boîte de dialogue **[!UICONTROL Copier la payload du module]** affiche le nom et la payload du module. Sélectionnez **[!UICONTROL Copier la payload du module]** pour copier la payload associée au module.

![Boîte de dialogue Copier la payload du package présentant la charge JSON avec la charge utile Copier le package mise en surbrillance.](../images/ui/sandbox-tooling/confirm-payload-copy.png)

### Création d’un module à l’aide d’une charge utile de module

Pour créer un package à l’aide d’une payload de package, accédez à l’onglet [!UICONTROL Sandbox] **[!UICONTROL Packages]** . Sélectionnez ensuite **[!UICONTROL Créer un package]**.

![L’interface utilisateur des environnements de test présentant l’option Créer un package mise en surbrillance.](../images/ui/sandbox-tooling/create-package.png)

Dans la boîte de dialogue **[!UICONTROL Créer un package]**, sélectionnez l’option **[!UICONTROL Coller la payload du package]**, puis sélectionnez **[!UICONTROL Sélectionner]**.

![ Boîte de dialogue Créer un package avec la payload du package collé sélectionnée et Sélectionner mise en surbrillance.](../images/ui/sandbox-tooling/create-package-options.png)

Collez la payload du package copié dans le champ de texte et sélectionnez **[!UICONTROL Créer]**.

![Créez une boîte de dialogue de package avec le champ de texte vide et Créer en surbrillance.](../images/ui/sandbox-tooling/paste-payload.png)

Pour afficher l’état actuel de votre demande de partage, accédez à l’**[!UICONTROL état du partage]**. L’état actuel de la requête s’affiche dans la colonne **[!UICONTROL État du partage]** .

![L’onglet Statut du partage affiche une requête de payload en attente.](../images/ui/sandbox-tooling/sharing-status.png)

## Étapes suivantes {#next-steps}

Ce document explique comment utiliser la fonction d’outil Sandbox pour partager des modules entre différentes organisations. Pour plus d’informations, consultez le [guide d’outils Sandbox](../ui/sandbox-tooling.md).

Pour savoir comment effectuer différentes opérations à l’aide de l’API Sandbox, consultez le [guide de développement sandbox](../api/getting-started.md). Pour un aperçu général des environnements de test en Experience Platform, reportez-vous à la [documentation de présentation](../home.md).
