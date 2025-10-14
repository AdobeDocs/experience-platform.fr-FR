---
keywords: Experience Platform;JupyterLab;notebooks;Espace de travail de science des données;rubriques populaires;jupyterlab
solution: Experience Platform
title: Présentation de l’interface utilisateur de JupyterLab
description: JupyterLab est une interface utilisateur web pour Project Jupyter et est étroitement intégré à Adobe Experience Platform. Elle fournit un environnement de développement interactif pour que les analystes de données puissent travailler avec les notebooks, le code et les données Jupyter. Ce document présente JupyterLab et ses fonctionnalités ainsi que des instructions pour effectuer des actions courantes.
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1838'
ht-degree: 95%

---

# Présentation de l’interface utilisateur de [!DNL JupyterLab]

>[!NOTE]
>
>Le Workspace de science des données ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs sur Data Science Workspace.

[!DNL JupyterLab] est une interface utilisateur web pour [Project Jupyter](https://jupyter.org/) et est étroitement intégré à Adobe Experience Platform. Elle fournit un environnement de développement interactif pour que les analystes de données puissent travailler avec les notebooks, le code et les données Jupyter.

Ce document présente [!DNL JupyterLab] et ses fonctionnalités, et fournit des instructions pour effectuer des actions courantes.

## [!DNL JupyterLab] sur [!DNL Experience Platform]

L’intégration JupyterLab d’Experience Platform est accompagnée de modifications architecturales, de considérations de conception, d’extensions de notebooks personnalisées, de bibliothèques préinstallées et d’une interface sur le thème Adobe.

La liste suivante décrit certaines des fonctionnalités propres à JupyterLab sur Experience Platform :

| Fonctionnalité | Description |
| --- | --- |
| **Noyaux** | Les noyaux permettent aux notebooks et aux autres front-ends [!DNL JupyterLab] d’exécuter et d’inspecter le code dans différents langages de programmation. [!DNL Experience Platform] fournit des noyaux supplémentaires pour prendre en charge le développement en [!DNL Python], R, PySpark et [!DNL Spark]. Pour plus d’informations, consultez la section sur les [noyaux](#kernels). |
| **Accès aux données** | Accédez aux jeux de données existants directement depuis [!DNL JupyterLab] avec la prise en charge intégrale des fonctionnalités de lecture et d’écriture. |
| Intégration du service **[!DNL Experience Platform]** | Les intégrations vous permettent d’utiliser d’autres services [!DNL Experience Platform] directement depuis [!DNL JupyterLab]. Vous trouverez la liste complète des intégrations prises en charge dans la section [&#x200B; Intégration à d’autres services Experience Platform &#x200B;](#service-integration). |
| **Authentification** | Outre le <a href="https://jupyter-notebook.readthedocs.io/en/stable/security.html" target="_blank">modèle de sécurité intégré de JupyterLab</a>, chaque interaction entre votre application et Experience Platform, y compris la communication service à service Experience Platform, est chiffrée et authentifiée via <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Bibliothèques de développement** | Dans [!DNL Experience Platform], [!DNL JupyterLab] fournit des bibliothèques préinstallées pour [!DNL Python], R et PySpark. Consultez l’[annexe](#supported-libraries) pour obtenir une liste complète des bibliothèques prises en charge. |
| **Contrôleur de bibliothèque** | Lorsque les bibliothèques préinstallées ne répondent pas à vos besoins, vous pouvez installer des bibliothèques supplémentaires pour Python et R. Elles seront temporairement stockées dans des conteneurs isolés afin de préserver l’intégrité de [!DNL Experience Platform] et protéger vos données. Pour plus d’informations, consultez la section sur les [noyaux](#kernels). |

>[!NOTE]
>
>Les bibliothèques supplémentaires sont uniquement disponibles pour la session dans laquelle elles ont été installées. Vous devez réinstaller les bibliothèques supplémentaires nécessaires lorsque vous démarrez de nouvelles sessions.

## Intégration à d’autres services [!DNL Experience Platform] {#service-integration}

La normalisation et l’interopérabilité sont des concepts clés pour [!DNL Experience Platform]. L’intégration de [!DNL JupyterLab] sur [!DNL Experience Platform] en tant qu’IDE intégré lui permet d’interagir avec d’autres services [!DNL Experience Platform], ce qui vous permet d’utiliser tout le potentiel de [!DNL Experience Platform]. Les services [!DNL Experience Platform] suivants sont disponibles dans [!DNL JupyterLab] :

* **[!DNL Catalog Service] :** Accédez à des jeux de données et explorez-les avec des fonctionnalités de lecture et d’écriture.
* **[!DNL Query Service] :** accédez aux jeux de données et explorez-les à l’aide de SQL, ce qui vous permet de réduire les frais généraux d’accès aux données lorsque vous traitez de grandes quantités de données.
* **[!DNL Sensei ML Framework] :** développement de modèles avec la possibilité de former et de noter des données, ainsi que de créer des recettes en un seul clic.
* **[!DNL Experience Data Model (XDM)]:** La normalisation et l’interopérabilité sont les concepts clés d’Adobe Experience Platform. [Le modèle de données d’expérience (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr), optimisé par Adobe vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

>[!NOTE]
>
>L’intégration de certains services [!DNL Experience Platform] sur [!DNL JupyterLab] est limitée à des noyaux spécifiques. Pour plus d’informations, consultez la section sur les [noyaux](#kernels).

## Fonctionnalités clés et opérations courantes

Vous trouverez des informations sur les fonctionnalités clés de [!DNL JupyterLab] et des instructions sur l’exécution d’opérations courantes dans les sections suivantes :

* [Accéder à JupyterLab](#access-jupyterlab)
* [Interface de JupyterLab](#jupyterlab-interface)
* [Cellules de code](#code-cells)
* [Noyaux](#kernels)
* [Sessions de noyau](#kernel-sessions)
* [Lanceur](#launcher)

### Accéder à [!DNL JupyterLab] {#access-jupyterlab}

Dans [Adobe Experience Platform](https://platform.adobe.com), sélectionnez **[!UICONTROL Notebooks]** dans la colonne de navigation de gauche. Attendez que [!DNL JupyterLab] soit complètement initialisé.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### Interface [!DNL JupyterLab] {#jupyterlab-interface}

L’interface [!DNL JupyterLab] se compose d’une barre de menus, d’une barre latérale gauche réductible et de l’espace de travail principal contenant des onglets pour les documents et les activités.

**Barre de menus**

La barre de menus en haut de l’interface comporte des menus de niveau supérieur qui affichent les actions disponibles dans [!DNL JupyterLab] ainsi que leurs raccourcis clavier :

* **Fichier :** actions relatives aux fichiers et répertoires
* **Modifier :** actions relatives à la modification des documents et d’autres activités
* **Afficher :** actions qui modifient l’apparence de [!DNL JupyterLab]
* **Exécuter :** actions d’exécution de code dans différentes activités telles que les notebooks et les consoles de code
* **Noyau :** actions de gestion des noyaux
* **Onglets :** une liste des activités et des documents ouverts
* **Paramètres :** paramètres courants et un éditeur de paramètres avancés
* **Aide :** une liste de [!DNL JupyterLab] et des liens d’aide sur les noyaux

**Barre latérale gauche**

La barre latérale gauche contient des onglets cliquables qui permettent d’accéder aux fonctionnalités suivantes :

* **Navigateur de fichiers :** une liste de documents et de répertoires de notebook enregistrés
* **Explorateur de données :** accédez aux jeux de données et aux schémas, explorez-les et parcourez-les
* **Noyaux et terminaux en cours d’exécution :** une liste des sessions de noyau et de terminal actives pouvant être interrompues
* **Commandes :** une liste de commandes utiles
* **Inspecteur de cellule :** un éditeur de cellules qui donne accès aux outils et aux métadonnées utiles pour configurer un notebook à des fins de présentation
* **onglets :** une liste d’onglets ouverts

Sélectionnez un onglet pour afficher ses fonctionnalités ou cliquez sur un onglet développé pour réduire la barre latérale gauche comme illustré ci-dessous :

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Espace de travail principal**

L’espace de travail principal de [!DNL JupyterLab] vous permet d’organiser les documents et les autres activités en panneaux d’onglets qui peuvent être redimensionnés ou subdivisés. Faites glisser un onglet au centre d’un panneau à onglets pour le faire migrer. Divisez un panneau en faisant glisser un onglet vers la gauche, la droite, le haut ou le bas du panneau :

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Configuration du GPU et du serveur de mémoire en [!DNL Python]/R

Dans [!DNL JupyterLab], sélectionnez l’icône d’engrenage dans le coin supérieur droit pour ouvrir la *configuration du serveur Notebook*. Vous pouvez activer le GPU et allouer la quantité de mémoire dont vous avez besoin à l’aide du curseur. La quantité de mémoire que vous pouvez allouer dépend de la quantité de mémoire configurée par votre organisation. Sélectionnez **[!UICONTROL Mettre à jour les configurations]** pour enregistrer.

>[!NOTE]
>
>Un seul GPU est configuré par organisation pour Notebooks. Si le GPU est en cours d’utilisation, vous devez attendre que l’utilisateur ou l’utilisatrice qui a réservé le GPU le libère. Pour ce faire, déconnectez-vous ou laissez le GPU inactif pendant quatre heures ou plus.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### Mettre fin à [!DNL JupyterLab] et redémarrer

Dans [!DNL JupyterLab], vous pouvez mettre fin à votre session pour empêcher l’utilisation d’autres ressources. Commencez par sélectionner l’**icône d’alimentation** ![icône d’alimentation](/help/images/icons/power.png), puis sélectionnez **[!UICONTROL Arrêter]** dans la fenêtre contextuelle qui s’affiche pour mettre fin à votre session. Les sessions Notebook se terminent automatiquement après 12 heures d’absence d’activité.

Pour redémarrer [!DNL JupyterLab], sélectionnez l’**icône de redémarrage** ![icône de redémarrage](/help/images/icons/restart.png) située directement à gauche de l’icône d’alimentation, puis sélectionnez **[!UICONTROL Redémarrer]** dans la fenêtre contextuelle qui s’affiche.

![mettre fin à jupyterlab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### Cellules de code {#code-cells}

Les cellules de code constituent le contenu principal des notebooks. Elles contiennent le code source dans le langage du noyau associé au notebook et la sortie résultant de l’exécution de la cellule de code. Le nombre d’exécutions est affiché à droite de chaque cellule de code qui représente son ordre d’exécution.

![](../images/jupyterlab/user-guide/code_cell.png)

Les actions de cellule courantes sont décrites ci-dessous :

* **Ajouter une cellule :** cliquez sur le symbole plus (**+**) dans le menu du notebook pour ajouter une cellule vide. Les nouvelles cellules sont placées sous la cellule en cours d’interaction ou à la fin du notebook si aucune cellule particulière n’est concernée.

* **Déplacer une cellule :** placez votre curseur à droite de la cellule que vous souhaitez déplacer, puis cliquez sur la cellule et faites-la glisser vers un nouvel emplacement. De plus, le déplacement d’une cellule d’un notebook vers un autre réplique la cellule et son contenu.

* **Exécuter une cellule :** cliquez sur le corps de la cellule que vous souhaitez exécuter, puis sur l’icône **lecture** (**▶**) dans le menu du notebook. Un astérisque (**\***) est affiché dans le compteur d’exécution de la cellule lorsque le noyau traite l’exécution, et est remplacé par un nombre entier une fois l’exécution terminée.

* **Supprimer une cellule :** cliquez sur le corps de la cellule que vous souhaitez supprimer, puis sur l’icône **ciseaux**.

### Noyaux {#kernels}

Les noyaux des notebooks sont les moteurs informatiques spécifiques au langage pour le traitement des cellules des notebooks. En plus de [!DNL Python], [!DNL JupyterLab] fournit une prise en charge supplémentaire pour les langages R, PySpark et [!DNL Spark] (Scala). Lorsque vous ouvrez un document de notebook, le noyau associé est lancé. Lorsqu’une cellule de notebook est exécutée, le noyau effectue le calcul et produit des résultats qui peuvent consommer d’importantes ressources de processeur et de mémoire. Notez que la mémoire allouée n’est pas libérée tant que le noyau n’est pas arrêté.

Certaines fonctionnalités sont limitées à des noyaux particuliers, comme décrit dans le tableau ci-dessous :

| Noyau | Prise en charge de l’installation de la bibliothèque | Intégrations à [!DNL Experience Platform] |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Oui | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Oui | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | Non | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Sessions de noyau {#kernel-sessions}

Chaque notebook actif ou activité sur [!DNL JupyterLab] utilise une session de noyau. Vous trouverez toutes les sessions actives en développant l’onglet **Noyaux et terminaux en cours d’exécution** de la barre latérale gauche. Vous pouvez identifier le type et l’état du noyau d’un notebook en observant le coin supérieur droit de l’interface du notebook. Dans le diagramme ci-dessous, le noyau associé au notebook est **[!DNL Python] 3** et son état actuel est représenté par un cercle gris à droite. Un cercle creux implique un noyau inactif et un cercle plein implique un noyau occupé.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Si le noyau est arrêté ou inactif pendant une longue période, alors **aucun noyau !** avec un cercle plein n’est affiché. Activez un noyau en cliquant sur l’état du noyau et en sélectionnant le type de noyau approprié, comme illustré ci-dessous :

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Lanceur {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

Le *Lanceur* personnalisé fournit des modèles de notebook utiles pour les noyaux pris en charge afin de vous aider à démarrer rapidement vos tâches, notamment :

| Modèle | Description |
| --- | --- |
| Vide | Un fichier de notebook vide. |
| Démarrage | Un notebook prérempli présentant l’exploration des données à l’aide de données d’exemple. |
| Ventes au détail | Un notebook prérempli présentant la [recette des ventes au détail](../pre-built-recipes/retail-sales.md) à l’aide de données d’exemple. |
| Créateur de recettes | Un modèle de notebook pour la création d’une recette dans [!DNL JupyterLab]. Il est prérempli de code et de commentaires qui présentent et décrivent le processus de création de la recette. Consultez le [tutoriel notebook vers recette](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/jupyterlab/create-a-model.html?lang=fr) pour une présentation détaillée. |
| [!DNL Query Service] | Un notebook prérempli présentant l’utilisation de [!DNL Query Service] directement dans [!DNL JupyterLab] avec des exemples de workflows qui analysent les données à grande échelle. |
| Événements XDM | Un notebook prérempli qui présente l’exploration des données sur les données d’événement d’expérience de valeur post, en mettant l’accent sur les fonctionnalités communes à l’ensemble de la structure de données. |
| Requêtes XDM | Un notebook prérempli présentant des exemples de requêtes d’entreprise sur les données d’événement d’expérience. |
| Agrégation | Un notebook prérempli présentant des exemples de processus pour agréger de grandes quantités de données en petits blocs gérables. |
| Mise en cluster | Un notebook prérempli présentant le processus de modélisation de machine learning de bout en bout à l’aide d’algorithmes de mise en cluster. |

Certains modèles de notebook sont limités à des noyaux spécifiques. La disponibilité des modèles pour chaque noyau est mappée dans le tableau suivant :

<table>
    <tr>
        <td></td>
        <th><strong>Vide</strong></th>
        <th><strong>Démarrage</strong></th>
        <th><strong>Ventes au détail</strong></th>
        <th><strong>Créateur de recettes</strong></th>
        <th><strong>[!DNL Query Service]</strong></th>
        <th><strong>Événements XDM</strong></th>
        <th><strong>Requêtes XDM</strong></th>
        <th><strong>Agrégation</strong></th>
        <th><strong>Mise en cluster</strong></th>
    </tr>
    <tr>
        <th><strong>[!DNL Python]</strong></th>
        <td >oui</td>
        <td >oui</td>
        <td >oui</td>
        <td >oui</td>
        <td >oui</td>
        <td >oui</td>
        <td >non</td>
        <td >non</td>
        <td >non</td>
    </tr>
    <tr>
        <th ><strong>R</strong></th>
        <td >oui</td>
        <td >oui</td>
        <td >oui</td>
        <td >non</td>
        <td >non</td>
        <td >non</td>
        <td >non</td>
        <td >non</td>
        <td >non</td>
    </tr>
      <tr>
        <th  ><strong>PySpark 3 ([!DNL Spark] 2.4)</strong></th>
        <td >non</td>
        <td >oui</td>
        <td >non</td>
        <td >non</td>
        <td >non</td>
        <td >non</td>
        <td >oui</td>
        <td >oui</td>
        <td >non</td>
    </tr>
    <tr>
        <th ><strong>Scala</strong></th>
        <td >oui</td>
        <td >oui</td>
        <td >non</td>
        <td >non</td>
        <td >non</td>
        <td >non</td>
        <td >non</td>
        <td >non</td>
        <td >oui</td>
    </tr>
</table>

Pour ouvrir un nouveau *lanceur*, cliquez sur **Fichier > Nouveau lanceur**. Vous pouvez également développer le **navigateur de fichiers** depuis la barre latérale gauche et cliquer sur le symbole plus (**+**) :

![](../images/jupyterlab/user-guide/new_launcher.gif)

## Étapes suivantes

Pour en savoir plus sur chacun des notebooks pris en charge et sur leur utilisation, consultez le guide de développement [Accès aux données des notebooks JupyterLab](./access-notebook-data.md). Ce guide explique comment utiliser les notebooks JupyterLab pour accéder à vos données, y compris la lecture, l’écriture et l’interrogation de données. Le guide d’accès aux données contient également des informations sur la quantité maximale de données pouvant être lues par chaque notebook pris en charge.

## Bibliothèques prises en charge {#supported-libraries}

Pour obtenir la liste des packages pris en charge en Python, R et PySpark, copiez et collez `!conda list` dans une nouvelle cellule, puis exécutez la cellule. Une liste des packages pris en charge est renseignée par ordre alphabétique.

![exemple](../images/jupyterlab/user-guide/libraries.PNG)

En outre, les dépendances suivantes sont utilisées, mais ne sont pas répertoriées :
* CUDA 11.2
* CUDNN 8.1

