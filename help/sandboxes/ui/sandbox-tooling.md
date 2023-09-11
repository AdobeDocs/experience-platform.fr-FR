---
title: Outils Sandbox
description: Exportez et importez en toute transparence des configurations Sandbox entre des environnements de test.
source-git-commit: 900cb35f6cb758f145904666c709c60dc760eff2
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 9%

---


# [!BADGE Beta] Outils Sandbox

>[!IMPORTANT]
>
>La variable **Outils Sandbox** La fonctionnalité décrite ci-dessous n’est disponible que pour sélectionner les clients bêta.

>[!NOTE]
>
>L’outil Sandbox est une fonctionnalité essentielle qui prend en charge les deux [!DNL Real-Time Customer Data Platform] et [!DNL Journey Optimizer] afin d’améliorer l’efficacité et la précision du cycle de développement.<br><br>Vous devez disposer des deux autorisations de contrôle d’accès basées sur les rôles suivantes pour utiliser la fonctionnalité d’outil d’environnement de test :<br>- `manage-sandbox` ou `view-sandbox`<br>- `manage-package`

Améliorez la précision de la configuration dans les environnements de test et exportez et importez en toute transparence les configurations des environnements de test entre les environnements de test grâce à la fonctionnalité d’outil d’environnement de test. Utilisez l’outil d’environnement de test pour réduire le temps de valorisation du processus de mise en oeuvre et déplacer les configurations réussies entre les environnements de test.

Vous pouvez utiliser la fonction d’outils des environnements de test pour sélectionner différents objets et les exporter dans un package. Un package peut se composer d’un seul objet, de plusieurs objets ou d’un environnement de test entier. Tous les objets inclus dans un package doivent provenir du même environnement de test.

## Objets pris en charge pour les outils Sandbox {#supported-objects}

Le tableau ci-dessous répertorie les objets actuellement pris en charge pour les outils Sandbox :

| Plateforme | Objet |
| --- | --- |
| [!DNL Adobe Journey Optimizer] | Parcours |
| Plateforme de données clients | Sources |
| Plateforme de données clients | Segments |
| Plateforme de données clients | Identités |
| Plateforme de données clients | Politiques |
| Plateforme de données clients | Schémas |
| Plateforme de données clients | Jeux de données |

Les objets suivants sont importés, mais leur état est en version préliminaire ou désactivé :

| Fonctionnalité | Objet | Statut |
| --- | --- | --- |
| Statut de l’importation | Flux de données source | Brouillon |
| Statut de l’importation | Parcours | Brouillon |
| Profil unifié | Schéma | Désactivé |
| Profil unifié | Jeu de données | Désactivé |
| Politiques | Stratégies de consentement | Désactivé |
| Politiques | Stratégies de gouvernance des données | Désactivé |

Les cas de périphérie répertoriés ci-dessous ne sont pas inclus dans le package :

* Relations de schéma

## Exporter des objets dans un package {#export-objects}

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_exit_package"
>title="Enregistrer et quitter le package"
>abstract="Pour quitter le package et enregistrer, les utilisateurs et utilisatrices peuvent simplement utiliser l’option Retour."

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_remove_object"
>title="Supprimer un objet"
>abstract="La personne doit sélectionner la ligne, puis utiliser l’option de suppression (disponible lors de la sélection) pour la supprimer."

>[!CONTEXTUALHELP]
>id="platform_sandbox_package_expiry"
>title="Paramètres d’expiration du package"
>abstract="La date est fixée à 90 jours à partir d’aujourd’hui. Cette date continue de changer jusqu’à la publication du package. Si un utilisateur ou une utilisatrice consulte le package ayant le statut de brouillon demain, la date passe à +1 jour (sauf si elle est définie par l’utilisateur ou l’utilisatrice)."

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_package_status"
>title="Statut du package"
>abstract="Par défaut, le statut est défini sur brouillon. Une fois le package publié, le statut devient publié. Aucune modification ne peut être apportée une fois le package publié."

>[!NOTE]
>
>Vous ne pouvez importer un package que si vous êtes autorisé à accéder aux objets.

Cet exemple documente le processus d’export d’un schéma et de son ajout à un package. Vous pouvez utiliser le même processus pour exporter d’autres objets, par exemple des jeux de données, des parcours, etc.

### Ajouter un objet à un nouveau package {#add-object-to-new-package}

Sélectionner **[!UICONTROL Schémas]** dans le volet de navigation de gauche, puis sélectionnez l’option **[!UICONTROL Parcourir]** qui répertorie les schémas disponibles. Sélectionnez ensuite les points de suspension (`...`) en regard du schéma sélectionné et une liste déroulante affiche les commandes. Sélectionner **[!UICONTROL Ajouter au package]** dans la liste déroulante.

![Liste des schémas affichant le menu déroulant en surbrillance [!UICONTROL Ajouter au package] contrôle.](../images/ui/sandbox-tooling/add-to-package.png)

Dans la **[!UICONTROL Ajouter au package]** , sélectionnez **[!UICONTROL Créer un package]** . Fournissez une [!UICONTROL Nom] pour votre module et un [!UICONTROL Description], puis sélectionnez **[!UICONTROL Ajouter]**.

![La variable [!UICONTROL Ajouter au package] Boîte de dialogue avec [!UICONTROL Créer un package] sélection et mise en surbrillance [!UICONTROL Ajouter].](../images/ui/sandbox-tooling/create-new-package.png)

Vous revenez alors à la variable **[!UICONTROL Schémas]** environnement. Vous pouvez maintenant ajouter des objets supplémentaires au module que vous avez créé en suivant les étapes ci-dessous.

### Ajouter un objet à un package existant et publier {#add-object-to-existing-package}

Pour afficher la liste des schémas disponibles, sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche, puis sélectionnez l’option **[!UICONTROL Parcourir]** . Sélectionnez ensuite les points de suspension (`...`) en regard du schéma sélectionné pour afficher les options de contrôle dans un menu déroulant. Sélectionner **[!UICONTROL Ajouter au package]** dans la liste déroulante.

![Liste des schémas affichant le menu déroulant en surbrillance [!UICONTROL Ajouter au package] contrôle.](../images/ui/sandbox-tooling/add-to-package.png)

La variable **[!UICONTROL Ajouter au package]** s’affiche. Sélectionnez la variable **[!UICONTROL Package existant]** , puis sélectionnez l’option **[!UICONTROL Nom du module]** et sélectionnez le module requis. Enfin, sélectionnez **[!UICONTROL Ajouter]** pour confirmer vos choix.

![[!UICONTROL Ajouter au package] , affichant un module sélectionné dans la liste déroulante.](../images/ui/sandbox-tooling/add-to-existing-package.png)

La liste des objets ajoutés au package est répertoriée. Pour publier le package et le rendre disponible pour l’importation dans des environnements de test, sélectionnez **[!UICONTROL Publier]**.

![Une liste d’objets dans le module, en surbrillant la fonction [!UICONTROL Publier] .](../images/ui/sandbox-tooling/publish-package.png)

Sélectionner **[!UICONTROL Publier]** pour confirmer la publication du kit.

![Boîte de dialogue de confirmation du module de publication, en surbrillance [!UICONTROL Publier] .](../images/ui/sandbox-tooling/publish-package-confirmation.png)

>[!NOTE]
>
>Une fois qu’il a été publié, le contenu du module ne peut plus être modifié. Pour éviter des problèmes de compatibilité, vérifiez que toutes les ressources nécessaires ont été sélectionnées. Si des modifications doivent être apportées, vous devez créer un module.

Vous revenez alors à la variable **[!UICONTROL Packages]** dans le [!UICONTROL Environnements de test] , où vous pouvez voir le nouveau module publié.

![Liste des packages sandbox qui mettent en évidence le nouveau package publié.](../images/ui/sandbox-tooling/published-packages.png)

## Importation d’un package dans un environnement de test cible {#import-package-to-target-sandbox}

Pour importer le package dans un environnement de test cible, accédez aux environnements de test **[!UICONTROL Parcourir]** et sélectionnez l’option plus (+) en regard du nom de l’environnement de test.

![Environnements de test **[!UICONTROL Parcourir]** surligner la sélection du package d&#39;import.](../images/ui/sandbox-tooling/browse-sandboxes.png)

Dans le menu déroulant, sélectionnez la variable **[!UICONTROL Nom du module]** vous souhaitez importer dans l’environnement de test ciblé. Ajouter une **[!UICONTROL Job name]**, qui sera utilisé pour la surveillance future, puis sélectionnez **[!UICONTROL Suivant]**.

![La page de détails de l’importation affiche la variable [!UICONTROL Nom du module] sélection de liste déroulante](../images/ui/sandbox-tooling/import-package-to-sandbox.png)

La variable [!UICONTROL Objet de package et dépendances] fournit une liste de toutes les ressources incluses dans ce module. Le système détecte automatiquement les objets dépendants requis pour réussir l’importation des objets parents sélectionnés.

![La variable [!UICONTROL Objet de package et dépendances] affiche la liste des ressources incluses dans le module.](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

>[!NOTE]
>
>Les objets dépendants peuvent être remplacés par des objets existants dans l’environnement de test cible, ce qui vous permet de réutiliser des objets existants plutôt que de créer une nouvelle version. Par exemple, lorsque vous importez un package comprenant des schémas, vous pouvez réutiliser des groupes de champs personnalisés et des espaces de noms d’identité existants dans l’environnement de test cible. Vous pouvez également réutiliser des segments existants dans l’environnement de test cible lorsque vous importez un package comprenant des Parcours.

Pour utiliser un objet existant, sélectionnez l’icône en forme de crayon en regard de l’objet dépendant. Les options de création ou d’utilisation d’éléments existants s’affichent. Sélectionner **[!UICONTROL Utiliser existant]**.

![La variable [!UICONTROL Objet de package et dépendances] page affichant les options d’objet dépendant [!UICONTROL Créer] et [!UICONTROL Utiliser existant].](../images/ui/sandbox-tooling/use-existing-object.png)

La variable **[!UICONTROL Groupe de champs]** La boîte de dialogue affiche une liste des groupes de champs disponibles pour l’objet. Sélectionnez les groupes de champs requis, puis cliquez sur **[!UICONTROL Enregistrer]**.

![Une liste de champs affichée sur la [!UICONTROL Groupe de champs] , surligner la boîte de dialogue [!UICONTROL Enregistrer] sélection. ](../images/ui/sandbox-tooling/field-group-list.png)

Vous revenez alors à la variable [!UICONTROL Objet de package et dépendances] page. À partir de là, sélectionnez **[!UICONTROL Terminer]** pour terminer l’importation du package.

![La variable [!UICONTROL Objet de package et dépendances] affiche une liste des ressources incluses dans le module, en surbrillance. [!UICONTROL Terminer].](../images/ui/sandbox-tooling/finish-object-dependencies.png)

## Exportation et importation d’un environnement de test complet

### Exportation d’un environnement de test entier {#export-entire-sandbox}

Pour exporter un environnement de test complet, accédez à la [!UICONTROL Environnements de test] **[!UICONTROL Packages]** et sélectionnez **[!UICONTROL Créer un package]**.

![La variable [!UICONTROL Environnements de test] **[!UICONTROL Packages]** mise en surbrillance des onglets [!UICONTROL Créer un package].](../images/ui/sandbox-tooling/create-sandbox-package.png)

Sélectionner **[!UICONTROL Environnement de test complet]** pour le type de package dans la variable [!UICONTROL Créer un package] boîte de dialogue. Fournissez une [!UICONTROL Nom du module] pour votre module et sélectionnez l’option **[!UICONTROL Sandbox]** dans la liste déroulante. Enfin, sélectionnez **[!UICONTROL Créer]** pour confirmer vos entrées.

![La variable [!UICONTROL Créer un package] Boîte de dialogue affichant les champs remplis et mise en surbrillance [!UICONTROL Créer].](../images/ui/sandbox-tooling/create-package-dialog.png)

Le package a été créé avec succès, sélectionnez **[!UICONTROL Publier]** pour publier le module.

![Liste des packages sandbox qui mettent en évidence le nouveau package publié.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

Vous revenez alors à la variable **[!UICONTROL Packages]** dans le [!UICONTROL Environnements de test] , où vous pouvez voir le nouveau module publié.

### Importez l’intégralité du package sandbox. {#import-entire-sandbox-package}

Pour importer le package dans un environnement de test cible, accédez au [!UICONTROL Environnements de test] **[!UICONTROL Parcourir]** et sélectionnez l’option plus (+) en regard du nom de l’environnement de test.

![Environnements de test **[!UICONTROL Parcourir]** surligner la sélection du package d&#39;import.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

À l’aide du menu déroulant, sélectionnez l’environnement de test complet à l’aide du **[!UICONTROL Nom du module]** menu déroulant. Ajouter une **[!UICONTROL Job name]**, qui sera utilisé pour la surveillance future, puis sélectionnez **[!UICONTROL Suivant]**.

![La page de détails de l’importation affiche la variable [!UICONTROL Nom du module] sélection de liste déroulante](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>Tous les objets sont créés comme nouveaux à partir du package lors de l’importation d’un environnement de test complet. Les objets ne sont pas répertoriés dans la variable [!UICONTROL Objet de package et dépendances] , car il peut y avoir des multiples. Un message intégré s’affiche, vous informant des types d’objets qui ne sont pas pris en charge.

Vous accédez au [!UICONTROL Objet de package et dépendances] où vous pouvez voir le nombre d’objets et de dépendances importés et exclus. À partir de là, sélectionnez **[!UICONTROL Importer]** pour terminer l’importation du package.

![La variable [!UICONTROL Objet de package et dépendances] La page affiche le message intégré des types d’objets non pris en charge, en surbrillance. [!UICONTROL Importer].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)

## Surveillance des traitements d’importation et affichage des détails des objets d’importation

Pour afficher les objets importés et les détails importés, accédez au [!UICONTROL Environnements de test] **[!UICONTROL Imports]** et sélectionnez le package dans la liste. Vous pouvez également utiliser la barre de recherche pour rechercher le module.

![Environnements de test [!UICONTROL Imports] met en surbrillance la sélection du package d’importation.](../images/ui/sandbox-tooling/imports-tab.png)

### Affichage des objets importés {#view-imported-objects}

Sur le **[!UICONTROL Imports]** dans le [!UICONTROL Environnements de test] environnement, sélectionnez **[!UICONTROL Affichage des objets importés]** dans le volet de droite.

Sélectionner **[!UICONTROL Affichage des objets importés]** dans le volet de droite des détails de la **[!UICONTROL Imports]** dans le [!UICONTROL Environnements de test] environnement.

![Environnements de test [!UICONTROL Imports] surligne l’onglet [!UICONTROL Affichage des objets importés] dans le volet de droite.](../images/ui/sandbox-tooling/view-imported-objects.png)

Utilisez les flèches pour développer les objets afin d&#39;afficher la liste complète des champs importés dans le package.

![Environnements de test [!UICONTROL Objets importés] affichant une liste d’objets importés dans le package.](../images/ui/sandbox-tooling/expand-imported-objects.png)

### Affichage des détails d’importation {#view-import-details}

Sélectionner **[!UICONTROL Affichage des détails d’importation]** dans le volet de droite des détails de la **[!UICONTROL Imports]** dans l’environnement Sandbox.

![Environnements de test [!UICONTROL Imports] surligne l’onglet [!UICONTROL Affichage des détails d’importation] dans le volet de droite.](../images/ui/sandbox-tooling/view-import-details.png)

La variable **[!UICONTROL Détails de l’importation]** La boîte de dialogue affiche une ventilation détaillée des importations.

![La variable [!UICONTROL Détails de l’importation] boîte de dialogue présentant une ventilation détaillée des imports.](../images/ui/sandbox-tooling/import-details.png)

>[!NOTE]
>
>Une fois l’importation terminée, vous recevez des notifications dans l’interface utilisateur de Platform. Vous pouvez accéder à ces notifications à partir de l’icône d’alertes. Vous pouvez accéder au dépannage à partir de là si une tâche échoue.

## Étapes suivantes

Ce document a démontré comment utiliser la fonction d’outils des environnements de test dans l’interface utilisateur d’Experience Platform. Pour plus d’informations sur les environnements de test, voir [guide d’utilisation des environnements de test](../ui/user-guide.md).

Pour obtenir des instructions sur l’exécution de différentes opérations à l’aide de l’API Sandbox, consultez le [guide de développement des sandbox](../api/getting-started.md). Pour un aperçu général des environnements de test en Experience Platform, reportez-vous à la section [documentation de présentation](../home.md).
