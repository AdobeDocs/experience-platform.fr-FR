---
title: Outils Sandbox
description: Exportez et importez en toute transparence des configurations Sandbox entre des environnements de test.
exl-id: f1199ab7-11bf-43d9-ab86-15974687d182
source-git-commit: fea62a2aa3c7d175afbfa808f392c3a93a0d31a0
workflow-type: tm+mt
source-wordcount: '2314'
ht-degree: 9%

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

| Platform | Objet | Détails |
| --- | --- | --- |
| Plateforme de données clients | Sources | Les informations d’identification du compte source ne sont pas répliquées dans l’environnement de test cible pour des raisons de sécurité et devront être mises à jour manuellement. Par défaut, le flux de données source est copié dans un état de brouillon. |
| Plateforme de données clients | Audiences | Seule la variable **[!UICONTROL Public du client]** type **[!UICONTROL Service de segmentation]** est prise en charge. Les étiquettes existantes pour le consentement et la gouvernance seront copiées dans la même tâche d’importation. Le système sélectionne automatiquement la stratégie de fusion par défaut dans l’environnement de test cible avec la même classe XDM lors de la vérification des dépendances de stratégie de fusion. |
| Plateforme de données clients | Identités | Le système dédupliquera automatiquement les espaces de noms d’identité standard Adobe lors de la création dans l’environnement de test cible. Les audiences ne peuvent être copiées que lorsque tous les attributs des règles d’audience sont activés dans le schéma d’union. Les schémas nécessaires doivent d’abord être déplacés et activés pour le profil unifié. |
| Plateforme de données clients | Schémas | Les étiquettes existantes pour le consentement et la gouvernance seront copiées dans la même tâche d’importation. L’utilisateur peut importer des schémas sans l’option Profil unifié activée. Les cas de périphérie des relations de schéma ne sont pas inclus dans le package. |
| Plateforme de données clients | Jeux de données | Les jeux de données sont copiés avec le paramètre de profil unifié désactivé par défaut. |
| Plateforme de données clients | Stratégies de consentement et de gouvernance | Ajoutez des stratégies personnalisées créées par un utilisateur à un module et déplacez-les dans des environnements de test. |

Les objets suivants sont importés, mais leur état est brouillon ou désactivé :

| Fonctionnalité | Objet | Statut |
| --- | --- | --- |
| Statut de l’importation | Flux de données source | Brouillon |
| Statut de l’importation | Parcours | Brouillon |
| Profil unifié | Jeu de données | Profil unifié désactivé |
| Politiques | Stratégies de gouvernance des données | Désactivé |

### Objets Adobe Journey Optimizer {#abobe-journey-optimizer-objects}

Le tableau ci-dessous répertorie [!DNL Adobe Journey Optimizer] les objets actuellement pris en charge pour l’outil et les limitations des environnements de test :

| Platform | Objet | Détails |
| --- | --- | --- |
| [!DNL Adobe Journey Optimizer] | Audience | Une audience peut être copiée en tant qu’objet dépendant de l’objet parcours. Vous pouvez sélectionner Créer une audience ou réutiliser une audience existante dans l’environnement de test cible. |
| [!DNL Adobe Journey Optimizer] | Schéma | Les schémas utilisés dans le parcours peuvent être copiés en tant qu’objets dépendants. Vous pouvez sélectionner Créer un nouveau schéma ou en réutiliser un existant dans l’environnement de test cible. |
| [!DNL Adobe Journey Optimizer] | Politique de fusion | Les stratégies de fusion utilisées dans le parcours peuvent être copiées en tant qu’objets dépendants. Dans le sandbox cible, vous **cannot** créer une nouvelle stratégie de fusion, vous ne pouvez utiliser qu’une stratégie existante. |
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
>abstract="Pour supprimer un objet du package, sélectionnez la ligne à supprimer, puis utilisez l’option Supprimer, disponible lors de la sélection. Notez que vous ne pouvez pas supprimer des objets de packages publiés."

>[!CONTEXTUALHELP]
>id="platform_sandbox_package_expiry"
>title="Paramètres d’expiration du package"
>abstract="Les packages sont paramétrés pour expirer après une période d’inactivité lorsqu’ils sont au statut de brouillon. La date par défaut est fixée à 90 jours à partir d’aujourd’hui. Cette date continue de changer jusqu’à la publication du package. Si vous consultez le package au statut de brouillon demain, la date sera décalée de +1 jour (sauf si vous définissez ce paramètre manuellement)."

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_package_status"
>title="Statut du package"
>abstract="Par défaut, le statut est défini sur brouillon. Une fois le package publié, le statut devient Publié. Aucune modification ne peut être apportée une fois le package publié."

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

Dans le menu déroulant, sélectionnez la variable **[!UICONTROL Nom du module]** vous souhaitez importer dans l’environnement de test ciblé. Ajouter un **[!UICONTROL Job name]**, qui sera utilisé pour la surveillance future. Par défaut, le profil unifié sera désactivé lors de l’import des schémas du package. Basculer **Activation des schémas pour le profil** pour activer cette fonction, puis sélectionnez **[!UICONTROL Suivant]**.

![La page de détails de l’importation affiche la variable [!UICONTROL Nom du module] sélection de liste déroulante](../images/ui/sandbox-tooling/import-package-to-sandbox.png)

La variable [!UICONTROL Objet de package et dépendances] fournit une liste de toutes les ressources incluses dans ce module. Le système détecte automatiquement les objets dépendants requis pour réussir l’importation des objets parents sélectionnés. Tous les attributs manquants sont affichés en haut de la page. Sélectionner **[!UICONTROL Afficher les détails]** pour une ventilation plus détaillée.

![La variable [!UICONTROL Objet de package et dépendances] affiche les attributs manquants.](../images/ui/sandbox-tooling/missing-attributes.png)

>[!NOTE]
>
>Les objets dépendants peuvent être remplacés par des objets existants dans l’environnement de test cible, ce qui vous permet de réutiliser des objets existants plutôt que de créer une nouvelle version. Par exemple, lorsque vous importez un package comprenant des schémas, vous pouvez réutiliser des groupes de champs personnalisés et des espaces de noms d’identité existants dans l’environnement de test cible. Vous pouvez également réutiliser des segments existants dans l’environnement de test cible lorsque vous importez un package comprenant des Parcours.

Pour utiliser un objet existant, sélectionnez l’icône en forme de crayon en regard de l’objet dépendant.

![La variable [!UICONTROL Objet de package et dépendances] affiche la liste des ressources incluses dans le module.](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

Les options de création ou d’utilisation d’éléments existants s’affichent. Sélectionner **[!UICONTROL Utiliser existant]**.

![La variable [!UICONTROL Objet de package et dépendances] page affichant les options d’objet dépendant [!UICONTROL Créer] et [!UICONTROL Utiliser existant].](../images/ui/sandbox-tooling/use-existing-object.png)

La variable **[!UICONTROL Groupe de champs]** La boîte de dialogue affiche une liste des groupes de champs disponibles pour l’objet. Sélectionnez les groupes de champs requis, puis cliquez sur **[!UICONTROL Enregistrer]**.

![Une liste de champs affichée sur la [!UICONTROL Groupe de champs] , surligner la boîte de dialogue [!UICONTROL Enregistrer] sélection. ](../images/ui/sandbox-tooling/field-group-list.png)

Vous revenez alors à la variable [!UICONTROL Objet de package et dépendances] page. À partir de là, sélectionnez **[!UICONTROL Terminer]** pour terminer l’importation du package.

![La variable [!UICONTROL Objet de package et dépendances] affiche une liste des ressources incluses dans le module, en surbrillance. [!UICONTROL Terminer].](../images/ui/sandbox-tooling/finish-object-dependencies.png)

## Exportation et importation d’un environnement de test complet

>[!NOTE]
>
>Actuellement, seuls les objets Real-time Customer Data Platform sont pris en charge lors de l’exportation ou de l’importation d’un environnement de test complet. Les objets Adobe Journey Optimizer tels que les parcours ne sont actuellement pas pris en charge.

Vous pouvez exporter tous les types d’objets pris en charge dans un package d’environnements de test complet, puis importer le package dans différents environnements de test pour répliquer les configurations d’objet. Par exemple, cette fonctionnalité vous permet d’effectuer les opérations suivantes :

- Réimportez un environnement de test pour reproduire toutes les configurations de l’objet si vous devez réinitialiser l’environnement de test.
- Importez le package dans d’autres environnements de test et utilisez-le comme environnement de test de plan directeur pour accélérer le processus de développement.

### Exportation d’un environnement de test entier {#export-entire-sandbox}

Pour exporter un environnement de test complet, accédez à la [!UICONTROL Environnements de test] **[!UICONTROL Packages]** et sélectionnez **[!UICONTROL Créer un package]**.

![La variable [!UICONTROL Environnements de test] **[!UICONTROL Packages]** mise en surbrillance des onglets [!UICONTROL Créer un package].](../images/ui/sandbox-tooling/create-sandbox-package.png)

Sélectionner **[!UICONTROL Environnement de test complet]** pour le [!UICONTROL Type de package] dans le [!UICONTROL Créer un package] boîte de dialogue. Fournissez une [!UICONTROL Nom du module] pour votre nouveau module et sélectionnez l’option **[!UICONTROL Sandbox]** dans la liste déroulante. Enfin, sélectionnez **[!UICONTROL Créer]** pour confirmer vos entrées.

![La variable [!UICONTROL Créer un package] Boîte de dialogue affichant les champs remplis et mise en surbrillance [!UICONTROL Créer].](../images/ui/sandbox-tooling/create-package-dialog.png)

Le package a été créé avec succès, sélectionnez **[!UICONTROL Publier]** pour publier le module.

![Liste des packages sandbox qui mettent en évidence le nouveau package publié.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

Vous revenez alors à la variable **[!UICONTROL Packages]** dans le [!UICONTROL Environnements de test] , où vous pouvez voir le nouveau module publié.

### Importez l’intégralité du package sandbox. {#import-entire-sandbox-package}

>[!NOTE]
>
>Tous les objets seront importés dans l’environnement de test cible en tant que nouveaux objets. Il est recommandé d’importer un package d’environnement de test complet dans un environnement de test vide.

Pour importer le package dans un environnement de test cible, accédez au [!UICONTROL Environnements de test] **[!UICONTROL Parcourir]** et sélectionnez l’option plus (+) en regard du nom de l’environnement de test.

![Environnements de test **[!UICONTROL Parcourir]** surligner la sélection du package d&#39;import.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

À l’aide du menu déroulant, sélectionnez l’environnement de test complet à l’aide du **[!UICONTROL Nom du module]** menu déroulant. Ajouter un **[!UICONTROL Job name]**, qui sera utilisé pour la surveillance future et une valeur facultative **[!UICONTROL Description de la tâche]**, puis sélectionnez **[!UICONTROL Suivant]**.

![La page de détails de l’importation affiche la variable [!UICONTROL Nom du module] sélection de liste déroulante](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>Vous devez disposer d’autorisations complètes pour tous les objets inclus dans le package. Si vous ne disposez pas d’autorisations, l’opération d’importation échoue et des messages d’erreur s’affichent.

Vous accédez au [!UICONTROL Objet de package et dépendances] où vous pouvez voir le nombre d’objets et de dépendances importés et exclus. À partir de là, sélectionnez **[!UICONTROL Importer]** pour terminer l’importation du package.

![La variable [!UICONTROL Objet de package et dépendances] La page affiche le message intégré des types d’objets non pris en charge, en surbrillance. [!UICONTROL Importer].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)

Patientez un certain temps avant que l’importation ne soit terminée. La durée d’exécution peut varier en fonction du nombre d’objets dans le module. Vous pouvez contrôler la tâche d’importation à partir de la fonction [!UICONTROL Environnements de test] **[!UICONTROL Tâches]** .

## Surveiller les détails de l’importation {#view-import-details}

Pour afficher les détails importés, accédez au [!UICONTROL Environnements de test] **[!UICONTROL Tâches]** et sélectionnez le package dans la liste. Vous pouvez également utiliser la barre de recherche pour rechercher le module.

![Environnements de test [!UICONTROL Tâches] met en surbrillance la sélection du package d’importation.](../images/ui/sandbox-tooling/imports-tab.png)

<!--### View imported objects {#view-imported-objects}

On the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment, select **[!UICONTROL View imported objects]** from the right details pane.

Select **[!UICONTROL View imported objects]** from the right details pane on the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment.

![The sandboxes [!UICONTROL Imports] tab highlights the [!UICONTROL View imported objects] selection in the right pane.](../images/ui/sandbox-tooling/view-imported-objects.png)

Use the arrows to expand objects to view the full list of fields that have been imported into the package.

![The sandboxes [!UICONTROL Imported objects] showing a list of objects imported into the package.](../images/ui/sandbox-tooling/expand-imported-objects.png)-->

Sélectionner **[!UICONTROL Afficher le résumé de l’importation]** dans le volet de droite des détails de la **[!UICONTROL Tâches]** dans l’environnement Sandbox.

![Environnements de test [!UICONTROL Imports] surligne l’onglet [!UICONTROL Affichage des détails d’importation] dans le volet de droite.](../images/ui/sandbox-tooling/view-import-details.png)

La variable **[!UICONTROL Résumé de l&#39;import]** La boîte de dialogue affiche une répartition des importations avec progression en pourcentage.

>[!NOTE]
>
>Vous pouvez afficher une liste d’objets en accédant à des pages d’inventaire spécifiques.

![La variable [!UICONTROL Détails de l’importation] boîte de dialogue présentant une ventilation détaillée des imports.](../images/ui/sandbox-tooling/import-details.png)

Une fois l’importation terminée, une notification est reçue dans l’interface utilisateur de Platform. Vous pouvez accéder à ces notifications à partir de l’icône d’alertes. Vous pouvez accéder au dépannage à partir de là si une tâche échoue.

## Tutoriel vidéo

La vidéo suivante est destinée à vous aider à comprendre l’utilisation de l’environnement de test et explique comment créer un nouveau module, publier un module et importer un module.

>[!VIDEO](https://video.tv.adobe.com/v/3424763/?learn=on)

## Étapes suivantes

Ce document a démontré comment utiliser la fonction d’outils des environnements de test dans l’interface utilisateur d’Experience Platform. Pour plus d’informations sur les environnements de test, voir [guide d’utilisation des environnements de test](../ui/user-guide.md).

Pour obtenir des instructions sur l’exécution de différentes opérations à l’aide de l’API Sandbox, consultez le [guide de développement des sandbox](../api/getting-started.md). Pour un aperçu général des environnements de test en Experience Platform, reportez-vous à la section [documentation de présentation](../home.md).
