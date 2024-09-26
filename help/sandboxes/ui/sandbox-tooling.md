---
title: Outils Sandbox
description: Exportez et importez en toute transparence des configurations Sandbox entre des environnements de test.
exl-id: f1199ab7-11bf-43d9-ab86-15974687d182
source-git-commit: 50f3976d73c8a34a51179157a7c93e3d9b1c0ff4
workflow-type: tm+mt
source-wordcount: '2404'
ht-degree: 8%

---

# Outil Sandbox

>[!NOTE]
>
>L’outil Sandbox est une fonctionnalité essentielle qui prend en charge [!DNL Real-Time Customer Data Platform] et [!DNL Journey Optimizer] pour améliorer l’efficacité et la précision du cycle de développement et de la configuration.<br><br>Vous devez disposer des deux autorisations de contrôle d’accès basées sur le rôle suivantes pour utiliser la fonctionnalité d’outil d’environnement de test : <br>- `manage-sandbox` ou `view-sandbox`<br>- `manage-package`

Améliorez la précision de la configuration dans les environnements de test et exportez et importez en toute transparence les configurations des environnements de test entre les environnements de test grâce à la fonctionnalité d’outil d’environnement de test. Utilisez l’outil d’environnement de test pour réduire le temps de valorisation du processus de mise en oeuvre et déplacer les configurations réussies entre les environnements de test.

Vous pouvez utiliser la fonction d’outils sandbox pour sélectionner différents objets et les exporter dans un package. Un package peut se composer d’un ou de plusieurs objets. <!--or an entire sandbox.-->Tous les objets inclus dans un package doivent provenir du même environnement de test.

## Objets pris en charge pour les outils Sandbox {#supported-objects}

La fonctionnalité d’outil d’environnement de test vous permet d’exporter des objets [!DNL Adobe Real-Time Customer Data Platform] et [!DNL Adobe Journey Optimizer] dans un package.

### Objets Real-time Customer Data Platform {#real-time-cdp-objects}

Le tableau ci-dessous répertorie les [!DNL Adobe Real-Time Customer Data Platform] objets actuellement pris en charge pour l’utilisation des outils Sandbox :

| Platform | Objet | Détails |
| --- | --- | --- |
| Plateforme de données clients | Sources | Les informations d’identification du compte source ne sont pas répliquées dans l’environnement de test cible pour des raisons de sécurité et devront être mises à jour manuellement. Par défaut, le flux de données source est copié dans un état de brouillon. |
| Plateforme de données clients | Audiences | Seul le **[!UICONTROL service de segmentation]** de type **[!UICONTROL d’audience]** est pris en charge. Les étiquettes existantes pour le consentement et la gouvernance seront copiées dans la même tâche d’importation. Le système sélectionne automatiquement la stratégie de fusion par défaut dans l’environnement de test cible avec la même classe XDM lors de la vérification des dépendances de stratégie de fusion. |
| Plateforme de données clients | Identités | Le système dédupliquera automatiquement les espaces de noms d’identité standard Adobe lors de la création dans l’environnement de test cible. Les audiences ne peuvent être copiées que lorsque tous les attributs des règles d’audience sont activés dans le schéma d’union. Les schémas nécessaires doivent d’abord être déplacés et activés pour le profil unifié. |
| Plateforme de données clients | Schémas | Les étiquettes existantes pour le consentement et la gouvernance seront copiées dans la même tâche d’importation. L’utilisateur peut importer des schémas sans l’option Profil unifié activée. Les cas de périphérie des relations de schéma ne sont pas inclus dans le package. |
| Plateforme de données clients | Jeux de données | Les jeux de données sont copiés avec le paramètre de profil unifié désactivé par défaut. |
| Plateforme de données clients | Stratégies de consentement et de gouvernance | Ajoutez des stratégies personnalisées créées par un utilisateur à un module et déplacez-les dans des environnements de test. |

Les objets suivants sont importés, mais leur état est brouillon ou désactivé :

| Fonctionnalité | Objet | Statut |
| --- | --- | --- |
| Statut de l’importation | Flux de données Source | Brouillon |
| Statut de l’importation | Parcours | Brouillon |
| Profil unifié | Jeu de données | Profil unifié désactivé |
| Politiques | Stratégies de gouvernance des données | Désactivé |

### Objets Adobe Journey Optimizer {#abobe-journey-optimizer-objects}

Le tableau ci-dessous répertorie les [!DNL Adobe Journey Optimizer] objets actuellement pris en charge pour les outils et les limites des environnements de test :

| Platform | Objet | Détails |
| --- | --- | --- |
| [!DNL Adobe Journey Optimizer] | Audience | Une audience peut être copiée en tant qu’objet dépendant de l’objet parcours. Vous pouvez sélectionner Créer une audience ou réutiliser une audience existante dans l’environnement de test cible. |
| [!DNL Adobe Journey Optimizer] | Schéma | Les schémas utilisés dans le parcours peuvent être copiés en tant qu’objets dépendants. Vous pouvez sélectionner Créer un nouveau schéma ou en réutiliser un existant dans l’environnement de test cible. |
| [!DNL Adobe Journey Optimizer] | Politique de fusion | Les stratégies de fusion utilisées dans le parcours peuvent être copiées en tant qu’objets dépendants. Dans l’environnement de test cible, vous **ne pouvez pas** créer de stratégie de fusion, vous ne pouvez utiliser qu’une stratégie existante. |
| [!DNL Adobe Journey Optimizer] | Parcours : détails de la zone de travail | La représentation du parcours sur la zone de travail inclut les objets du parcours, tels que les conditions, les actions, les événements, les audiences de lecture, etc., qui sont copiés. L’activité de saut est exclue de la copie. |
| [!DNL Adobe Journey Optimizer] | Événement | Les événements et les détails de l’événement utilisés dans le parcours sont copiés. Il crée toujours une nouvelle version dans l’environnement de test cible. |
| [!DNL Adobe Journey Optimizer] | Action | Les messages électroniques et push utilisés dans le parcours peuvent être copiés en tant qu’objets dépendants. Les activités d’action de canal utilisées dans les champs de parcours, qui sont utilisées pour la personnalisation dans le message, ne sont pas vérifiées pour être complètes. Les blocs de contenu ne sont pas copiés.<br><br>L&#39;action de mise à jour de profil utilisée dans le parcours peut être copiée. Les actions personnalisées et les détails des actions utilisées dans le parcours sont également copiés. Il crée toujours une nouvelle version dans l’environnement de test cible. |
| [!DNL Adobe Journey Optimizer] | Parcours | L’ajout d’un parcours entier à un module permet de copier la majorité des objets dont dépend le parcours, notamment les audiences, les schémas, les événements et les actions. |
| [!DNL Adobe Journey Optimizer] | Modèle de contenu | Un modèle de contenu peut être copié en tant qu’objet dépendant de l’objet de parcours. Modèles autonomes qui vous permettent de réutiliser facilement du contenu personnalisé dans des campagnes et des parcours Journey Optimizer. |
| [!DNL Adobe Journey Optimizer] | Fragment | Un fragment peut être copié en tant qu’objet dépendant de l’objet parcours. Les fragments sont des composants réutilisables qui peuvent être référencés dans un ou plusieurs emails dans des campagnes et parcours Journey Optimizer. |

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

Sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Parcourir]** qui répertorie les schémas disponibles. Sélectionnez ensuite les points de suspension (`...`) en regard du schéma sélectionné et une liste déroulante affiche les commandes. Sélectionnez **[!UICONTROL Ajouter au package]** dans la liste déroulante.

![ Liste des schémas affichant le menu déroulant surlignant le contrôle [!UICONTROL Ajouter au package].](../images/ui/sandbox-tooling/add-to-package.png)

Dans la boîte de dialogue **[!UICONTROL Ajouter au package]**, sélectionnez l’option **[!UICONTROL Créer un package]** . Fournissez un [!UICONTROL nom] pour votre package et une [!UICONTROL description] facultative, puis sélectionnez **[!UICONTROL Ajouter]**.

![ La boîte de dialogue [!UICONTROL Ajouter au package] avec [!UICONTROL Créer un nouveau package] sélectionnée et en surbrillance [!UICONTROL Ajouter].](../images/ui/sandbox-tooling/create-new-package.png)

Vous revenez à l’environnement **[!UICONTROL Schemas]** . Vous pouvez maintenant ajouter des objets supplémentaires au module que vous avez créé en suivant les étapes ci-dessous.

### Ajouter un objet à un package existant et publier {#add-object-to-existing-package}

Pour afficher la liste des schémas disponibles, sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Parcourir]** . Sélectionnez ensuite les points de suspension (`...`) en regard du schéma sélectionné pour afficher les options de contrôle dans un menu déroulant. Sélectionnez **[!UICONTROL Ajouter au package]** dans la liste déroulante.

![ Liste des schémas affichant le menu déroulant surlignant le contrôle [!UICONTROL Ajouter au package].](../images/ui/sandbox-tooling/add-to-package.png)

La boîte de dialogue **[!UICONTROL Ajouter au package]** s’affiche. Sélectionnez l’option **[!UICONTROL Package existant]**, puis la liste déroulante **[!UICONTROL Nom du package]** et sélectionnez le package requis. Enfin, sélectionnez **[!UICONTROL Ajouter]** pour confirmer vos choix.

![[!UICONTROL Boîte de dialogue Ajouter au package], affichant un package sélectionné dans la liste déroulante.](../images/ui/sandbox-tooling/add-to-existing-package.png)

La liste des objets ajoutés au package est répertoriée. Pour publier le package et le rendre disponible pour l’importation dans des environnements de test, sélectionnez **[!UICONTROL Publish]**.

![Liste d&#39;objets dans le package, en surbrillant l&#39;option [!UICONTROL Publish].](../images/ui/sandbox-tooling/publish-package.png)

Sélectionnez **[!UICONTROL Publish]** pour confirmer la publication du package.

![Boîte de dialogue de confirmation du package Publish, surlignant l’option [!UICONTROL Publish].](../images/ui/sandbox-tooling/publish-package-confirmation.png)

>[!NOTE]
>
>Une fois qu’il a été publié, le contenu du module ne peut plus être modifié. Pour éviter des problèmes de compatibilité, vérifiez que toutes les ressources nécessaires ont été sélectionnées. Si des modifications doivent être apportées, vous devez créer un module.

Vous revenez à l’onglet **[!UICONTROL Packages]** dans l’environnement [!UICONTROL Sandbox] où vous pouvez voir le nouveau package publié.

![Liste des packages sandbox qui mettent en surbrillance le nouveau package publié.](../images/ui/sandbox-tooling/published-packages.png)

## Importation d’un package dans un environnement de test cible {#import-package-to-target-sandbox}

>[!NOTE]
>
>Toutes les actions d’importation sont enregistrées dans les journaux d’audit.

Pour importer le package dans un environnement de test cible, accédez à l’onglet **[!UICONTROL Parcourir]** des environnements de test et sélectionnez l’option plus (+) en regard du nom de l’environnement de test.

![L’onglet **[!UICONTROL Parcourir]** des environnements de test mettant en évidence la sélection de package d’importation.](../images/ui/sandbox-tooling/browse-sandboxes.png)

Dans le menu déroulant, sélectionnez le **[!UICONTROL Nom du module]** à importer dans l’environnement de test ciblé. Ajoutez un **[!UICONTROL nom de la tâche]** qui sera utilisé pour la surveillance future. Par défaut, le profil unifié sera désactivé lors de l’import des schémas du package. Activez **Activer les schémas pour profile** pour activer cette fonction, puis sélectionnez **[!UICONTROL Suivant]**.

![La page des détails de l’importation présentant la liste déroulante [!UICONTROL Nom du package]](../images/ui/sandbox-tooling/import-package-to-sandbox.png)

La page [!UICONTROL Objet de module et dépendances] fournit une liste de tous les actifs inclus dans ce module. Le système détecte automatiquement les objets dépendants requis pour réussir l’importation des objets parents sélectionnés. Tous les attributs manquants sont affichés en haut de la page. Sélectionnez **[!UICONTROL Afficher les détails]** pour une ventilation plus détaillée.

![ La page [!UICONTROL Objet de module et dépendances] affiche les attributs manquants.](../images/ui/sandbox-tooling/missing-attributes.png)

>[!NOTE]
>
>Les objets dépendants peuvent être remplacés par des objets existants dans l’environnement de test cible, ce qui vous permet de réutiliser des objets existants plutôt que de créer une nouvelle version. Par exemple, lorsque vous importez un package comprenant des schémas, vous pouvez réutiliser des groupes de champs personnalisés et des espaces de noms d’identité existants dans l’environnement de test cible. Vous pouvez également réutiliser des segments existants dans l’environnement de test cible lorsque vous importez un package comprenant des Parcours.

Pour utiliser un objet existant, sélectionnez l’icône en forme de crayon en regard de l’objet dépendant.

![La page [!UICONTROL Objet de module et dépendances] affiche une liste des ressources incluses dans le module.](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

Les options de création ou d’utilisation d’éléments existants s’affichent. Sélectionnez **[!UICONTROL Utiliser existant]**.

![ La page [!UICONTROL Objet de module et dépendances] présentant les options d’objet dépendant [!UICONTROL Créer ] et [!UICONTROL Utiliser existant].](../images/ui/sandbox-tooling/use-existing-object.png)

La boîte de dialogue **[!UICONTROL Groupe de champs]** affiche la liste des groupes de champs disponibles pour l’objet. Sélectionnez les groupes de champs requis, puis sélectionnez **[!UICONTROL Enregistrer]**.

![Liste des champs affichés dans la boîte de dialogue [!UICONTROL Groupe de champs], mettant en surbrillance la sélection [!UICONTROL Enregistrer]. ](../images/ui/sandbox-tooling/field-group-list.png)

Vous revenez à la page [!UICONTROL Objet de package et dépendances] . À partir de là, sélectionnez **[!UICONTROL Terminer]** pour terminer l’importation du package.

![La page [!UICONTROL Objet de module et dépendances] affiche une liste des ressources incluses dans le module, en surbrillant [!UICONTROL Terminer].](../images/ui/sandbox-tooling/finish-object-dependencies.png)

## Exportation et importation d’un environnement de test complet

>[!NOTE]
>
>Actuellement, seuls les objets Real-time Customer Data Platform sont pris en charge lors de l’exportation ou de l’importation d’un environnement de test complet. Les objets Adobe Journey Optimizer tels que les parcours ne sont actuellement pas pris en charge.

Vous pouvez exporter tous les types d’objets pris en charge dans un package d’environnements de test complet, puis importer le package dans différents environnements de test pour répliquer les configurations d’objet. Par exemple, cette fonctionnalité vous permet d’effectuer les opérations suivantes :

- Réimportez un environnement de test pour reproduire toutes les configurations de l’objet si vous devez réinitialiser l’environnement de test.
- Importez le package dans d’autres environnements de test et utilisez-le comme environnement de test de plan directeur pour accélérer le processus de développement.

### Exportation d’un environnement de test entier {#export-entire-sandbox}

Pour exporter un environnement de test complet, accédez à l’onglet [!UICONTROL Sandbox] **[!UICONTROL Packages]** et sélectionnez **[!UICONTROL Créer un package]**.

![ L’onglet [!UICONTROL Sandbox] **[!UICONTROL Packages]** qui surplombe l’onglet .](../images/ui/sandbox-tooling/create-sandbox-package.png)

Sélectionnez **[!UICONTROL Entier sandbox]** pour le [!UICONTROL type de package] dans la boîte de dialogue [!UICONTROL Créer un package]. Fournissez un [!UICONTROL nom de module] pour votre nouveau module et sélectionnez **[!UICONTROL Sandbox]** dans la liste déroulante. Enfin, sélectionnez **[!UICONTROL Créer]** pour confirmer vos entrées.

![ La boîte de dialogue [!UICONTROL Créer un package] présentant les champs terminés et mettant en surbrillance [!UICONTROL Créer].](../images/ui/sandbox-tooling/create-package-dialog.png)

Le module a été créé avec succès. Sélectionnez **[!UICONTROL Publish]** pour le publier.

![Liste des packages sandbox qui mettent en surbrillance le nouveau package publié.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

Vous revenez à l’onglet **[!UICONTROL Packages]** dans l’environnement [!UICONTROL Sandbox] où vous pouvez voir le nouveau package publié.

### Importez l’intégralité du package sandbox. {#import-entire-sandbox-package}

>[!NOTE]
>
>Tous les objets seront importés dans l’environnement de test cible en tant que nouveaux objets. Il est recommandé d’importer un package d’environnement de test complet dans un environnement de test vide.

Pour importer le package dans un environnement de test cible, accédez à l’onglet [!UICONTROL Sandbox] **** et sélectionnez l’option plus (+) en regard du nom de l’environnement de test.

![L’onglet **[!UICONTROL Parcourir]** des environnements de test mettant en évidence la sélection de package d’importation.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

À l’aide du menu déroulant, sélectionnez l’environnement de test complet à l’aide de la liste déroulante **[!UICONTROL Nom du module]** . Ajoutez un **[!UICONTROL nom de la tâche]** qui sera utilisé pour la surveillance future et une **[!UICONTROL description de la tâche]** facultative, puis sélectionnez **[!UICONTROL Suivant]**.

![La page des détails de l’importation présentant la liste déroulante [!UICONTROL Nom du package]](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>Vous devez disposer d’autorisations complètes pour tous les objets inclus dans le package. Si vous ne disposez pas d’autorisations, l’opération d’importation échoue et des messages d’erreur s’affichent.

Vous accédez à la page [!UICONTROL Objet de package et dépendances] où vous pouvez voir le nombre d’objets et de dépendances importés et exclus. À partir de là, sélectionnez **[!UICONTROL Importer]** pour terminer l’importation du package.

![ La page [!UICONTROL Objet de package et dépendances] affiche le message intégré des types d&#39;objets non pris en charge, en surbrillant [!UICONTROL Import].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)

Patientez un certain temps avant que l’importation ne soit terminée. La durée d’exécution peut varier en fonction du nombre d’objets dans le module. Vous pouvez surveiller la tâche d’importation à partir de l’onglet [!UICONTROL Sandbox] **[!UICONTROL Tâches]** .

## Surveiller les détails de l’importation {#view-import-details}

Pour afficher les détails importés, accédez à l’onglet [!UICONTROL Sandbox] **[!UICONTROL Tâches]** et sélectionnez le package dans la liste. Vous pouvez également utiliser la barre de recherche pour rechercher le module.

![L’onglet [!UICONTROL Tâches] des environnements de test met en évidence la sélection de package d’importation.](../images/ui/sandbox-tooling/imports-tab.png)

<!--### View imported objects {#view-imported-objects}

On the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment, select **[!UICONTROL View imported objects]** from the right details pane.

Select **[!UICONTROL View imported objects]** from the right details pane on the **[!UICONTROL Jobs]** tab in the [!UICONTROL Sandboxes] environment.

![The sandboxes [!UICONTROL Imports] tab highlights the [!UICONTROL View imported objects] selection in the right pane.](../images/ui/sandbox-tooling/view-imported-objects.png)

Use the arrows to expand objects to view the full list of fields that have been imported into the package.

![The sandboxes [!UICONTROL Imported objects] showing a list of objects imported into the package.](../images/ui/sandbox-tooling/expand-imported-objects.png)-->

Sélectionnez **[!UICONTROL Afficher la synthèse de l’importation]** dans le volet de détails de droite de l’onglet **[!UICONTROL Tâches]** de l’environnement Sandbox.

![L’onglet [!UICONTROL Imports] des environnements de test met en évidence la sélection [!UICONTROL Afficher les détails de l’importation] dans le volet de droite.](../images/ui/sandbox-tooling/view-import-details.png)

La boîte de dialogue **[!UICONTROL Résumé de l&#39;import]** affiche une ventilation des importations avec progression en pourcentage.

>[!NOTE]
>
>Vous pouvez afficher une liste d’objets en accédant à des pages d’inventaire spécifiques.

![La boîte de dialogue [!UICONTROL Détails de l’importation] présentant une ventilation détaillée des importations.](../images/ui/sandbox-tooling/import-details.png)

Une fois l’importation terminée, une notification est reçue dans l’interface utilisateur de Platform. Vous pouvez accéder à ces notifications à partir de l’icône d’alertes. Vous pouvez accéder au dépannage à partir de là si une tâche échoue.

## Tutoriel vidéo

La vidéo suivante est destinée à vous aider à comprendre l’utilisation de l’environnement de test et explique comment créer un nouveau module, publier un module et importer un module.

>[!VIDEO](https://video.tv.adobe.com/v/3424763/?learn=on)

## Étapes suivantes

Ce document a démontré comment utiliser la fonction d’outils des environnements de test dans l’interface utilisateur d’Experience Platform. Pour plus d’informations sur les environnements de test, consultez le [guide d’utilisation des environnements de test](../ui/user-guide.md).

Pour obtenir des instructions sur l’exécution de différentes opérations à l’aide de l’API Sandbox, consultez le [guide de développement des sandbox](../api/getting-started.md). Pour un aperçu général des environnements de test en Experience Platform, reportez-vous à la [documentation de présentation](../home.md).
