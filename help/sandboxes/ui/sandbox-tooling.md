---
title: Outils Sandbox
description: Exportez et importez en toute transparence des configurations Sandbox entre des environnements de test.
exl-id: f1199ab7-11bf-43d9-ab86-15974687d182
source-git-commit: 1f7b7f0486d0bb2774f16a766c4a5af6bbb8848a
workflow-type: tm+mt
source-wordcount: '1859'
ht-degree: 7%

---

# Outil Sandbox

>[!NOTE]
>
>L’outil Sandbox est une fonctionnalité essentielle qui prend en charge les deux [!DNL Real-Time Customer Data Platform] et [!DNL Journey Optimizer] afin d’améliorer l’efficacité et la précision du cycle de développement.<br><br>Vous devez disposer des deux autorisations de contrôle d’accès basées sur les rôles suivantes pour utiliser la fonctionnalité d’outil d’environnement de test :<br>- `manage-sandbox` ou `view-sandbox`<br>- `manage-package`

Améliorez la précision de la configuration dans les environnements de test et exportez et importez en toute transparence les configurations des environnements de test entre les environnements de test grâce à la fonctionnalité d’outil d’environnement de test. Utilisez l’outil d’environnement de test pour réduire le temps de valorisation du processus de mise en oeuvre et déplacer les configurations réussies entre les environnements de test.

Vous pouvez utiliser la fonction d’outils sandbox pour sélectionner différents objets et les exporter dans un package. Un package peut se composer d’un ou de plusieurs objets. <!--or an entire sandbox.-->Tous les objets inclus dans un package doivent provenir du même environnement de test.

## Objets pris en charge pour les outils Sandbox {#supported-objects}

La fonctionnalité d’outil d’environnement de test vous permet d’exporter des [!DNL Adobe Real-Time Customer Data Platform] et [!DNL Adobe Journey Optimizer] dans un package.

### Objets Real-time Customer Data Platform {#real-time-cdp-objects}

Le tableau ci-dessous répertorie [!DNL Adobe Real-Time Customer Data Platform] objets actuellement pris en charge pour les outils Sandbox :

| Plateforme | Objet | Détails |
| --- | --- | --- |
| Plateforme de données clients | Sources | Les informations d’identification du compte source ne sont pas répliquées dans l’environnement de test cible pour des raisons de sécurité et devront être mises à jour manuellement. Par défaut, le flux de données source est copié dans un état de brouillon. |
| Plateforme de données clients | Audiences | Seule la variable **[!UICONTROL Public du client]** type **[!UICONTROL Service de segmentation]** est prise en charge. Les étiquettes existantes pour le consentement et la gouvernance seront copiées dans la même tâche d’importation. |
| Plateforme de données clients | Identités | Le système dédupliquera automatiquement les espaces de noms d’identité standard Adobe lors de la création dans l’environnement de test cible. Les audiences ne peuvent être copiées que lorsque tous les attributs des règles d’audience sont activés dans le schéma d’union. Les schémas nécessaires doivent d’abord être déplacés et activés pour le profil unifié. |
| Plateforme de données clients | Schémas | Les étiquettes existantes pour le consentement et la gouvernance seront copiées dans la même tâche d’importation. L’état du profil unifié du schéma sera copié tel quel depuis l’environnement de test source. Si le schéma est activé pour le profil unifié dans l’environnement de test source, tous les attributs sont déplacés vers le schéma d’union. Les cas de périphérie des relations de schéma ne sont pas inclus dans le package. |
| Plateforme de données clients | Jeux de données | Les jeux de données sont copiés avec le paramètre de profil unifié désactivé par défaut. |

Les objets suivants sont importés, mais leur état est brouillon ou désactivé :

| Fonctionnalité | Objet | Statut |
| --- | --- | --- |
| Statut de l’importation | Flux de données source | Brouillon |
| Statut de l’importation | Parcours | Brouillon |
| Profil unifié | Jeu de données | Profil unifié désactivé |
| Politiques | Stratégies de gouvernance des données | Désactivé |

### Objets Adobe Journey Optimizer {#abobe-journey-optimizer-objects}

Le tableau ci-dessous répertorie [!DNL Adobe Journey Optimizer] les objets actuellement pris en charge pour l’outil et les limitations des environnements de test :

| Plateforme | Objet | Détails |
| --- | --- | --- |
| [!DNL Adobe Journey Optimizer] | Audience | Une audience peut être copiée en tant qu’objet dépendant de l’objet parcours. Vous pouvez sélectionner Créer une audience ou réutiliser une audience existante dans l’environnement de test cible. |
| [!DNL Adobe Journey Optimizer] | Schéma | Les schémas utilisés dans le parcours peuvent être copiés en tant qu’objets dépendants. Vous pouvez sélectionner Créer un nouveau schéma ou en réutiliser un existant dans l’environnement de test cible. |
| [!DNL Adobe Journey Optimizer] | Parcours : détails de la zone de travail | La représentation du parcours sur la zone de travail inclut les objets du parcours, tels que les conditions, les actions, les événements, les audiences de lecture, etc., qui sont copiés. L’activité de saut est exclue de la copie. |
| [!DNL Adobe Journey Optimizer] | Événement | Les événements et les détails de l’événement utilisés dans le parcours sont copiés. Il crée toujours une nouvelle version dans l’environnement de test cible. |
| [!DNL Adobe Journey Optimizer] | Action | Les messages électroniques et push utilisés dans le parcours peuvent être copiés en tant qu’objets dépendants. Les activités d’action de canal utilisées dans les champs de parcours, qui sont utilisées pour la personnalisation dans le message, ne sont pas vérifiées pour être complètes. Les blocs de contenu ne sont pas copiés.<br><br>L’action de mise à jour du profil utilisée dans le parcours peut être copiée. Les actions personnalisées et les détails des actions utilisées dans le parcours sont également copiés. Il crée toujours une nouvelle version dans l’environnement de test cible. |

Les surfaces (par exemple, les paramètres prédéfinis) ne sont pas copiées. Le système sélectionne automatiquement la correspondance la plus proche possible sur l’environnement de test de destination en fonction du type de message et du nom de la surface. Si aucune surface n’est trouvée sur l’environnement de test cible, la copie de surface échoue, ce qui entraîne l’échec de la copie du message, car un message nécessite qu’une surface soit disponible pour la configuration. Dans ce cas, au moins une surface doit être créée pour le bon canal du message pour que la copie fonctionne.

Les types d’identité personnalisés ne sont pas pris en charge en tant qu’objets dépendants lors de l’exportation d’un parcours.

## Exporter des objets dans un package {#export-objects}

>[!NOTE]
>
>Toutes les actions d’exportation sont enregistrées dans les journaux d’audit.

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_remove_object"
>title="Supprimer un objet"
>abstract="Pour supprimer un objet du package, sélectionnez la ligne à supprimer, puis utilisez l’option de suppression, disponible lors de la sélection. Notez que vous ne pouvez pas supprimer des objets des modules publiés."

>[!CONTEXTUALHELP]
>id="platform_sandbox_package_expiry"
>title="Paramètres d’expiration du package"
>abstract="Les packages sont définis pour expirer après une période d’inactivité dans le statut de brouillon. La date par défaut est définie sur 90 jours à partir d’aujourd’hui. Cette date continue de changer jusqu’à la publication du package. Si vous consultez le package en état de brouillon demain, la date est déplacée de +1 jour, sauf si vous définissez cela manuellement."

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

>[!NOTE]
>
>Toutes les actions d’importation sont enregistrées dans les journaux d’audit.

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

<!--
## Export and import an entire sandbox 

>[!NOTE]
>
>All export and import actions are recorded in the audit logs.

### Export an entire sandbox {#export-entire-sandbox}

To export an entire sandbox, navigate to the [!UICONTROL Sandboxes] **[!UICONTROL Packages]** tab and select **[!UICONTROL Create package]**.

![The [!UICONTROL Sandboxes] **[!UICONTROL Packages]** tab highlighting [!UICONTROL Create package].](../images/ui/sandbox-tooling/create-sandbox-package.png)

Select **[!UICONTROL Entire sandbox]** for the Type of package in the [!UICONTROL Create package] dialog. Provide a [!UICONTROL Package name] for your package and select the **[!UICONTROL Sandbox]** from the dropdown. Finally, select **[!UICONTROL Create]** to confirm your entries.

![The [!UICONTROL Create package] dialog showing completed fields and highlighting [!UICONTROL Create].](../images/ui/sandbox-tooling/create-package-dialog.png)

The package is created successfully, select **[!UICONTROL Publish]** to publish the package.

![List of sandbox packages highlighting the new published package.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

You are returned to the **[!UICONTROL Packages]** tab in the [!UICONTROL Sandboxes] environment, where you can see the new published package.

### Import the entire sandbox package {#import-entire-sandbox-package}

To import the package into a target sandbox, navigate to the [!UICONTROL Sandboxes] **[!UICONTROL Browse]** tab and select the plus (+) option beside the sandbox name.

![The sandboxes **[!UICONTROL Browse]** tab highlighting the import package selection.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

Using the dropdown menu, select the full sandbox using the **[!UICONTROL Package name]** dropdown. Add an optional **[!UICONTROL Job name]**, which will be used for future monitoring, then select **[!UICONTROL Next]**.

![The import details page showing the [!UICONTROL Package name] dropdown selection](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>All objects are created as new from the package when importing an entire sandbox. The objects are not listed in the [!UICONTROL Package object and dependencies] page, as there can be multiples. An inline message is displayed, advising of object types that are not supported.

You are taken to the [!UICONTROL Package object and dependencies] page where you can see the number of objects and dependencies that are imported and excluded objects. From here, select **[!UICONTROL Import]** to complete the package import.

 ![The [!UICONTROL Package object and dependencies] page shows the inline message of object types not supported, highlighting [!UICONTROL Import].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)
-->

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

## Tutoriel vidéo

La vidéo suivante est destinée à vous aider à comprendre l’utilisation de l’environnement de test et explique comment créer un nouveau module, publier un module et importer un module.

>[!VIDEO](https://video.tv.adobe.com/v/3424763/?learn=on)

## Étapes suivantes

Ce document a démontré comment utiliser la fonction d’outils des environnements de test dans l’interface utilisateur d’Experience Platform. Pour plus d’informations sur les environnements de test, voir [guide d’utilisation des environnements de test](../ui/user-guide.md).

Pour obtenir des instructions sur l’exécution de différentes opérations à l’aide de l’API Sandbox, consultez le [guide de développement des sandbox](../api/getting-started.md). Pour un aperçu général des environnements de test en Experience Platform, reportez-vous à la section [documentation de présentation](../home.md).
