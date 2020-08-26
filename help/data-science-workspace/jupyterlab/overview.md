---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;jupyterlab
solution: Experience Platform
title: Guide d’utilisation de JupyterLab
topic: Overview
description: JupyterLab est une interface utilisateur web pour Project Jupyter et est étroitement intégré à Adobe Experience Platform. Il fournit un environnement de développement interactif pour que les analystes de données puissent travailler avec les notebooks, le code et les données Jupyter.
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '3684'
ht-degree: 57%

---


# [!DNL JupyterLab] guide de l&#39;utilisateur

[!DNL JupyterLab] est une interface utilisateur web pour [Project Jupyter](https://jupyter.org/) et est étroitement intégré à Adobe Experience Platform. Il fournit un environnement de développement interactif pour que les analystes de données puissent travailler avec les notebooks, le code et les données Jupyter.

This document provides an overview of [!DNL JupyterLab] and its features as well as instructions to perform common actions.

## [!DNL JupyterLab] on [!DNL Experience Platform]

L’intégration JupyterLab d’Experience Platform est accompagnée de modifications architecturales, de considérations de conception, d’extensions de notebooks personnalisées, de bibliothèques préinstallées et d’une interface sur le thème Adobe.

La liste suivante présente quelques-unes des fonctionnalités propres à JupyterLab sur Platform :

| Fonctionnalité | Description |
| --- | --- |
| **Noyaux** | Kernels provide notebook and other [!DNL JupyterLab] front-ends the ability to execute and introspect code in different programming languages. [!DNL Experience Platform] fournit des noyaux supplémentaires pour prendre en charge le développement dans [!DNL Python], R, PySpark et [!DNL Spark]. Pour plus d’informations, consultez la section sur les [noyaux](#kernels). |
| **Accès aux données** | Access existing datasets directly from within [!DNL JupyterLab] with full support for read and write capabilities. |
| **[!DNL Platform]intégration de service** | Built-in integrations allows you to utilize other [!DNL Platform] services directly from within [!DNL JupyterLab]. Une liste complète des intégrations prises en charge est fournie dans la section sur l’[intégration avec d’autres services Platform](#service-integration). |
| **Authentification** | Outre <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">le modèle de sécurité intégré de JupyterLab</a>, chaque interaction entre votre application et Experience Platform, y compris la communication service à service de Platform, est chiffrée et authentifiée à l’aide d’<a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Bibliothèques de développement** | In [!DNL Experience Platform], [!DNL JupyterLab] provides pre-installed libraries for [!DNL Python], R, and PySpark. Consultez l’[annexe](#supported-libraries) pour obtenir une liste complète des bibliothèques prises en charge. |
| **Contrôleur de bibliothèque** | When the the pre-installed libraries are lacking for your needs, additional libraries can be installed for Python and R, and are temporarily stored in isolated containers to maintain the integrity of [!DNL Platform] and keep your data safe. Pour plus d’informations, consultez la section sur les [noyaux](#kernels). |

>[!NOTE]
>
>Les bibliothèques supplémentaires sont uniquement disponibles pour la session dans laquelle elles ont été installées. Vous devez réinstaller les bibliothèques supplémentaires nécessaires lorsque vous démarrez de nouvelles sessions.

## Integration with other [!DNL Platform] services {#service-integration}

Standardization and interoperability are key concepts behind [!DNL Experience Platform]. The integration of [!DNL JupyterLab] on [!DNL Platform] as an embedded IDE allows it to interact with other [!DNL Platform] services, enabling you to utilize [!DNL Platform] to its full potential. The following [!DNL Platform] services are available in [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** Accédez et explorez des jeux de données avec des fonctionnalités de lecture et d&#39;écriture.
* **[!DNL Query Service] :** accédez aux jeux de données et explorez-les à l’aide de SQL, ce qui vous permet de réduire les frais généraux d’accès aux données lorsque vous traitez de grandes quantités de données.
* **[!DNL Sensei ML Framework] :** développement de modèles avec la possibilité de former et de noter des données, ainsi que de créer des recettes en un seul clic.
* **[!DNL Experience Data Model (XDM)]:** La normalisation et l’interopérabilité sont les concepts clés d’Adobe Experience Platform. [Le modèle de données d’expérience (XDM)](https://www.adobe.com/go/xdm-home-en), piloté par l’Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

>[!NOTE]
>
>Some [!DNL Platform] service integrations on [!DNL JupyterLab] are limited to specific kernels. Pour plus d’informations, consultez la section sur les [noyaux](#kernels).

## Fonctionnalités clés et opérations courantes

Information regarding key features of [!DNL JupyterLab] and instructions on performing common operations are provided in the sections below:

* [Accès à JupyterLab](#access-jupyterlab)
* [Interface de JupyterLab](#jupyterlab-interface)
* [Cellules de code](#code-cells)
* [Noyaux](#kernels)
* [Sessions de noyau](#kernel-sessions)
* [Ressource d’exécution PySpark/Spark](#execution-resource)
* [Lanceur](#launcher)

### Accès [!DNL JupyterLab] {#access-jupyterlab}

Dans [Adobe Experience Platform](https://platform.adobe.com), sélectionnez **Ordinateurs portables** dans la colonne de navigation de gauche. Allow some time for [!DNL JupyterLab] to fully initialize.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] interface {#jupyterlab-interface}

The [!DNL JupyterLab] interface consists of a menu bar, a collapsible left sidebar, and the main work area containing tabs of documents and activities.

**Barre de menus**

The menu bar at the top of the interface has top-level menus that expose actions available in [!DNL JupyterLab] with their keyboard shortcuts:

* **Fichier :** actions relatives aux fichiers et répertoires
* **Modifier :** actions relatives à la modification des documents et d’autres activités
* **Afficher :** actions qui modifient l’apparence de [!DNL JupyterLab]
* **Exécuter :** actions d’exécution de code dans différentes activités telles que les notebooks et les consoles de code
* **Noyau :** actions de gestion des noyaux
* **Onglets :** une liste des activités et des documents ouverts
* **Paramètres :** paramètres courants et un éditeur de paramètres avancés
* **Aide :**[!DNL JupyterLab] une liste des liens d’aide de et du noyau

**Barre latérale gauche**

La barre latérale gauche contient des onglets cliquables qui permettent d’accéder aux fonctionnalités suivantes :

* **Navigateur de fichiers :** une liste de documents et de répertoires de notebook enregistrés
* **Explorateur de données :** accédez aux jeux de données et aux schémas, explorez-les et parcourez-les
* **Noyaux et terminaux en cours d’exécution :** une liste des sessions de noyau et de terminal actives pouvant être interrompues
* **Commandes :** une liste de commandes utiles
* **Inspecteur de cellule :** un éditeur de cellules qui donne accès aux outils et aux métadonnées utiles pour configurer un notebook à des fins de présentation
* **onglets :** une liste d’onglets ouverts

Cliquez sur un onglet pour afficher ses fonctionnalités ou cliquez sur un onglet développé pour réduire la barre latérale gauche comme illustré ci-dessous :

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Espace de travail principal**

The main work area in [!DNL JupyterLab] enables you to arrange documents and other activities into panels of tabs that can be resized or subdivided. Faites glisser un onglet au centre d’un panneau à onglets pour le faire migrer. Divisez un panneau en faisant glisser un onglet vers la gauche, la droite, le haut ou le bas du panneau :

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Cellules de code {#code-cells}

Les cellules de code constituent le contenu principal des notebooks. Elles contiennent le code source dans le langage du noyau associé au notebook et la sortie résultant de l’exécution de la cellule de code. Le nombre d’exécutions est affiché à droite de chaque cellule de code qui représente son ordre d’exécution.

![](../images/jupyterlab/user-guide/code_cell.png)

Les actions de cellule courantes sont décrites ci-dessous :

* **Ajouter une cellule :** cliquez sur le symbole plus (**+**) dans le menu du notebook pour ajouter une cellule vide. Les nouvelles cellules sont placées sous la cellule en cours d’interaction ou à la fin du notebook si aucune cellule particulière n’est concernée.

* **Déplacer une cellule :** placez votre curseur à droite de la cellule que vous souhaitez déplacer, puis cliquez sur la cellule et faites-la glisser vers un nouvel emplacement. De plus, le déplacement d’une cellule d’un notebook vers un autre réplique la cellule et son contenu.

* **Exécuter une cellule :** cliquez sur le corps de la cellule que vous souhaitez exécuter, puis sur l’icône **lecture** (**▶**) dans le menu du notebook. Un astérisque (**\***) est affiché dans le compteur d’exécution de la cellule lorsque le noyau traite l’exécution, et est remplacé par un nombre entier une fois l’exécution terminée.

* **Supprimer une cellule :** cliquez sur le corps de la cellule que vous souhaitez supprimer, puis sur l’icône **ciseaux**.

### Noyaux {#kernels}

Les noyaux des notebooks sont les moteurs informatiques spécifiques au langage pour le traitement des cellules des notebooks. In addition to [!DNL Python], [!DNL JupyterLab] provides additional language support in R, PySpark, and [!DNL Spark] (Scala). Lorsque vous ouvrez un document de notebook, le noyau associé est lancé. Lorsqu’une cellule de notebook est exécutée, le noyau effectue le calcul et produit des résultats qui peuvent consommer d’importantes ressources de processeur et de mémoire. Notez que la mémoire allouée n’est pas libérée tant que le noyau n’est pas arrêté.

Certaines fonctionnalités sont limitées à des noyaux particuliers, comme décrit dans le tableau ci-dessous :

| Noyau | Prise en charge de l’installation de la bibliothèque | [!DNL Platform] intégrations |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Oui | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **r** | Oui | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | Non | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Sessions de noyau {#kernel-sessions}

Each active notebook or activity on [!DNL JupyterLab] utilizes a kernel session. Vous trouverez toutes les sessions actives en développant l’onglet **Noyaux et terminaux en cours d’exécution** de la barre latérale gauche. Vous pouvez identifier le type et l’état du noyau d’un notebook en observant le coin supérieur droit de l’interface du notebook. Dans le diagramme ci-dessous, le noyau associé au notebook est **[!DNL Python] 3** et son état actuel est représenté par un cercle gris à droite. Un cercle creux implique un noyau inactif et un cercle plein implique un noyau occupé.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Si le noyau est arrêté ou inactif pendant une longue période, alors **aucun noyau** avec un cercle plein n’est affiché. Activez un noyau en cliquant sur l’état du noyau et en sélectionnant le type de noyau approprié, comme illustré ci-dessous :

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Lanceur {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

Le *Lanceur* personnalisé fournit des modèles de notebook utiles pour les noyaux pris en charge afin de vous aider à démarrer rapidement vos tâches, notamment :

| Modèle | Description |
| --- | --- |
| Vide | Un fichier de notebook vide. |
| Démarrage | Un notebook prérempli présentant l’exploration des données à l’aide de données d’exemple. |
| Ventes au détail | Un notebook prérempli présentant la <a href="https://docs.adobe.com/content/help/fr-FR/experience-platform/data-science-workspace/home.html#!api-specification/markdown/narrative/technical_overview/data_science_workspace_overview/dsw_prebuilt_recipes/retail_sales_recipe/retail_sales_recipe.md" target="_blank">Recette Ventes au détail</a> à l’aide de données d’exemple. |
| Recipe Builder | Un modèle de notebook pour la création d’une recette dans [!DNL JupyterLab]. Il est prérempli de code et de commentaires qui présentent et décrivent le processus de création de la recette. Consultez le <a href="https://docs.adobe.com/content/help/fr-FR/experience-platform/data-science-workspace/jupyterlab/create-a-recipe.html" target="_blank">tutoriel notebook vers recette</a> pour une présentation détaillée. |
| [!DNL Query Service] | A pre-filled notebook demonstrating the usage of [!DNL Query Service] directly in [!DNL JupyterLab] with provided sample workflows that analyzes data at scale. |
| Événements XDM | Un notebook prérempli qui présente l’exploration des données sur les données d’événement d’expérience de valeur post, en mettant l’accent sur les fonctionnalités communes à l’ensemble de la structure de données. |
| Requêtes XDM | Un notebook prérempli présentant des exemples de requêtes d’entreprise sur les données d’événement d’expérience. |
| Agrégation | Un notebook prérempli présentant des exemples de processus pour agréger de grandes quantités de données en petits blocs gérables. |
| Mise en cluster | Un notebook prérempli présentant le processus de modélisation d’apprentissage automatique de bout en bout à l’aide d’algorithmes de mise en cluster. |

Certains modèles de notebook sont limités à des noyaux spécifiques. La disponibilité des modèles pour chaque noyau est mappée dans le tableau suivant :

<table>
    <tr>
        <td></td>
        <th><strong>Vide</strong></th>
        <th><strong>Démarrage</strong></th>
        <th><strong>Ventes au détail</strong></th>
        <th><strong>Recipe Builder</strong></th>
        <th><strong>[ !Service de Requête DNL]</strong></th>
        <th><strong>Événements XDM</strong></th>
        <th><strong>Requêtes XDM</strong></th>
        <th><strong>Agrégation</strong></th>
        <th><strong>Mise en cluster</strong></th>
    </tr>
    <tr>
        <th><strong>[ ! DNL Python]</strong></th>
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

### Configuration du GPU et du serveur de mémoire dans [!DNL Python]/R

Dans [!DNL JupyterLab] sélectionnez l&#39;icône d&#39;engrenage dans le coin supérieur droit pour ouvrir la configuration *du serveur* portable. Vous pouvez activer GPU et allouer la quantité de mémoire dont vous avez besoin en utilisant le curseur. La quantité de mémoire que vous pouvez allouer dépend de la quantité de mémoire allouée par votre organisation. Sélectionnez **[!UICONTROL Mettre à jour les configurations]** pour enregistrer.

>[!NOTE]
>
>Un seul processeur graphique est configuré par organisation pour les ordinateurs portables. Si le GPU est en cours d’utilisation, vous devez attendre que l’utilisateur qui a actuellement réservé le GPU le publie. Pour ce faire, déconnectez-vous ou quittez le GPU en état d&#39;inactivité pendant quatre heures ou plus.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

## Access [!DNL Platform] data using Notebooks

Each supported kernel provides built-in functionalities that allow you to read [!DNL Platform] data from a dataset within a notebook. However, support for paginating data is limited to [!DNL Python] and R notebooks.

### Limites des données des ordinateurs portables

Les informations suivantes définissent la quantité maximale de données pouvant être lues, le type de données utilisé et la période estimée de lecture des données. Pour [!DNL Python] et R, un serveur de portables configuré à 40 Go de RAM a été utilisé pour les tests. Pour PySpark et Scala, une grappe de serveurs de données configurée à 64 Go de RAM, 8 coeurs, 2 DBU avec un maximum de 4 travailleurs a été utilisée pour les bancs d’essai décrits ci-dessous.

Les données du schéma ExperienceEvent utilisées variaient en taille en commençant par un millier de lignes (1K) allant jusqu’à un milliard de lignes (1B). Notez que pour PySpark et les [!DNL Spark] mesures, une période de 10 jours a été utilisée pour les données XDM.

Les données de schéma ad hoc ont été prétraitées à l’aide de la commande [!DNL Query Service] Créer un tableau comme sélection (CTAS). Ces données varient également en taille en commençant par un millier (1K) de lignes allant jusqu&#39;à un milliard (1B) de lignes.

#### [!DNL Python] limites de données des ordinateurs portables

**Schéma XDM ExperienceEvent :** Vous devriez être en mesure de lire un maximum de 2 millions de lignes (environ 6,1 Go de données sur le disque) de données XDM en moins de 22 minutes. L’Ajoute de lignes supplémentaires peut entraîner des erreurs.

| Nombre de lignes | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Taille sur le disque (Mo) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK (en secondes) | 20.3 | 86.8 | 63 | 659 | 1315 |

**schéma ad hoc :** Vous devriez être en mesure de lire un maximum de 5 millions de lignes (environ 5,6 Go de données sur le disque) de données non XDM (ad hoc) en moins de 14 minutes. L’Ajoute de lignes supplémentaires peut entraîner des erreurs.

| Nombre de lignes | 1K | 10K | 100K | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Taille sur le disque (en Mo) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (en secondes) | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

#### Limites de données des ordinateurs portables R

**Schéma XDM ExperienceEvent :** Vous devriez être en mesure de lire un maximum de 1 million de lignes de données XDM (3 Go de données sur le disque) en moins de 13 minutes.

| Nombre de lignes | 1K | 10K | 100K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Taille sur le disque (Mo) | 18.73 | 187.5 | 308 | 3000 |
| Noyau R (en secondes) | 14.03 | 69.6 | 86.8 | 775 |

**schéma ad hoc :** Vous devriez pouvoir lire un maximum de 3 millions de lignes de données ad hoc (293 Mo de données sur le disque) en 10 minutes environ.

| Nombre de lignes | 1K | 10K | 100K | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Taille sur le disque (en Mo) | 0.082 | 0.612 | 9,0 | 91 | 188 | 293 |
| SDK R (en s) | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

#### Limites des données du bloc-notes PySpark ([!DNL Python] noyau) :

**Schéma XDM ExperienceEvent :** En mode Interactif, vous devriez pouvoir lire un maximum de 5 millions de lignes (environ 13,42 Go de données sur disque) de données XDM en 20 minutes environ. Le mode interactif ne prend en charge que jusqu’à 5 millions de lignes. Si vous souhaitez lire des jeux de données plus volumineux, il est conseillé de passer en mode Lot. En mode Batch, vous devriez pouvoir lire un maximum de 500 millions de lignes (environ 1,31 To de données sur disque) de données XDM en 14 heures environ.

| Nombre de lignes | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Taille du disque | 2.93MB | 4.38MB | 29.02 | 2.69 Go   | 5.39 Go   | 8.09 Go   | 13.42 Go   | 26.82 Go   | 134.24 Go   | 268.39 Go   | 1.31TB |
| SDK (mode interactif) | 33s | 32.4s | 55.1s | 253.5s | 489.2s | 729.6s | 1206.8s | - | - | - | - |
| SDK (mode Batch) | 815.8s | 492.8s | 379.1s | 637.4s | 624.5s | 869.2s | 1104.1s | 1786s | 5387.2s | 10624.6s | 50547s |

**schéma ad hoc :** En mode Interactif, vous devriez être en mesure de lire un maximum de 1 milliard de lignes (~1,05 To de données sur disque) de données non-XDM en moins de 3 minutes. En mode Batch, vous devriez être en mesure de lire un maximum de 1 milliard de lignes (environ 1,05 To de données sur disque) de données non-XDM en 18 minutes environ.

| Nombre de lignes | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Taille du disque | 1.12MB | 11.24MB | 109.48MB | 2.69 Go   | 2.14 Go   | 3.21 Go   | 5.36 Go   | 10.71 Go   | 53.58 Go   | 107.52 Go   | 535.88 Go   | 1.05TB |
| Mode interactif SDK (en secondes) | 28.2s | 18.6s | 20.8s | 20.9s | 23.8s | 21.7s | 24.7s | 22s | 28.4s | 40s | 97.4s | 154.5s |
| Mode de traitement par lots du SDK (en secondes) | 428.8s | 578.8s | 641.4s | 538.5s | 630.9s | 467.3s | 411s | 675s | 702s | 719.2s | 1022.1s | 1122.3s |

#### [!DNL Spark] Limites des données des blocs-notes (noyau Scala) :

**Schéma XDM ExperienceEvent :** En mode Interactif, vous devriez pouvoir lire un maximum de 5 millions de lignes (environ 13,42 Go de données sur disque) de données XDM en 18 minutes environ. Le mode interactif ne prend en charge que jusqu’à 5 millions de lignes. Si vous souhaitez lire des jeux de données plus volumineux, il est conseillé de passer en mode Lot. En mode Batch, vous devriez pouvoir lire un maximum de 500 millions de lignes (environ 1,31 To de données sur disque) de données XDM en 14 heures environ.

| Nombre de lignes | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Taille du disque | 2.93MB | 4.38MB | 29.02 | 2.69 Go   | 5.39 Go   | 8.09 Go   | 13.42 Go   | 26.82 Go   | 134.24 Go   | 268.39 Go   | 1.31TB |
| Mode interactif SDK (en secondes) | 37.9s | 22.7s | 45.6s | 231.7s | 444.7s | 660.6s | 1100s | - | - | - | - |
| Mode de traitement par lots du SDK (en secondes) | 374.4s | 398.5s | 527s | 487.9s | 588.9s | 829s | 939.1s | 1441s | 5473.2s | 10118.8 | 49207.6 |

**schéma ad hoc :** En mode Interactif, vous devriez être en mesure de lire un maximum de 1 milliard de lignes (~1,05 To de données sur disque) de données non-XDM en moins de 3 minutes. En mode Batch, vous devriez être en mesure de lire un maximum de 1 milliard de lignes (environ 1,05 To de données sur disque) de données non-XDM en 16 minutes environ.

| Nombre de lignes | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Taille du disque | 1.12MB | 11.24MB | 109.48MB | 2.69 Go   | 2.14 Go   | 3.21 Go   | 5.36 Go   | 10.71 Go   | 53.58 Go   | 107.52 Go   | 535.88 Go   | 1.05TB |
| Mode interactif SDK (en secondes) | 35.7s | 31s | 19.5s | 25.3s | 23s | 33.2s | 25.5s | 29.2s | 29.7s | 36.9s | 83.5s | 139s |
| Mode de traitement par lots du SDK (en secondes) | 448.8s | 459.7s | 519s | 475.8s | 599.9s | 347.6s | 407.8s | 397s | 518.8s | 487.9s | 760.2s | 975.4s |

### Read from a dataset in [!DNL Python]/R

[!DNL Python]Les notebooks et R vous permettent de paginer les données lors de l’accès aux jeux de données. Vous trouverez ci-dessous un exemple de code pour lire des données avec et sans pagination.

[//]: # (In the following samples, the first step is currently required but once the SDK is complete, users are no longer required to explicitly define client_context)

#### Read from a dataset in [!DNL Python]/R without pagination

L’exécution du code suivant lit le jeu de données complet. Si l’exécution est réussie, les données sont enregistrées sous la forme d’un cadre de données pandas référencé par la variable `df`.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

* `{DATASET_ID}` : l’identité unique du jeu de données auquel accéder

#### Read from a dataset in [!DNL Python]/R with pagination

L’exécution du code suivant lit les données du jeu de données spécifié. La pagination est obtenue en limitant et en décalant les données à l’aide des fonctions `limit()` et `offset()` respectivement. La limitation des données fait référence au nombre maximal de points de données à lire, tandis que le décalage fait référence au nombre de points de données à ignorer avant la lecture des données. Si l’opération de lecture s’exécute correctement, les données sont enregistrées sous la forme d’un cadre de données pandas référencé par la variable `df`.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$limit(100L)$offset(10L)$read() 
```

* `{DATASET_ID}` : l’identité unique du jeu de données auquel accéder

### Read from a dataset in PySpark/[!DNL Spark]/Scala

With an an active PySpark or Scala notebook opened, expand the **Data Explorer** tab from the left sidebar and double click **Datasets** to view a list of available datasets. Right-click on the dataset listing you wish to access and click **Explore Data in Notebook**. Les cellules de code suivantes sont générées :

#### PySpark ([!DNL Spark] 2.4) {#pyspark2.4}

Avec l&#39;introduction de Spark 2.4, la magie [`%dataset`](#magic) personnalisée est fournie.

```python
# PySpark 3 (Spark 2.4)

%dataset read --datasetId {DATASET_ID} --dataFrame pd0
pd0.describe()
pd0.show(10, False)
```

#### Scala ([!DNL Spark] 2.4) {#spark2.4}

```scala
// Scala (Spark 2.4)

// initialize the session
import org.apache.spark.sql.{Dataset, SparkSession}
val spark = SparkSession.builder().master("local").getOrCreate()

val dataFrame = spark.read.format("com.adobe.platform.query")
    .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
    .option("ims-org", sys.env("IMS_ORG_ID"))
    .option("api-key", sys.env("PYDASDK_IMS_CLIENT_ID"))
    .option("service-token", sys.env("PYDASDK_IMS_SERVICE_TOKEN"))
    .option("mode", "batch")
    .option("dataset-id", "{DATASET_ID}")
    .load()
dataFrame.printSchema()
dataFrame.show()
```

>[!TIP]
>
>Dans Scala, vous pouvez utiliser `sys.env()` pour déclarer et renvoyer une valeur de l’intérieur `option`.

### Utilisation de la magie %dataset dans les blocs-notes PySpark 3 ([!DNL Spark] 2.4) {#magic}

Avec l&#39;introduction de la [!DNL Spark] 2.4, `%dataset` la magie personnalisée est fournie pour l&#39;utilisation dans les nouveaux portables PySpark 3 ([!DNL Spark] 2.4) (noyau[!DNL Python] 3).

**Utilisation**

`%dataset {action} --datasetId {id} --dataFrame {df}`

**Description**

Commande [!DNL Data Science Workspace] magique personnalisée pour lire ou écrire un jeu de données à partir d&#39;un [!DNL Python] bloc-notes (noyau[!DNL Python] 3).

* **{action}**: Type d’action à exécuter sur le jeu de données. Deux actions sont disponibles &quot;read&quot; ou &quot;write&quot;.
* **—datasetId {id}**: Utilisé pour fournir l&#39;identifiant du jeu de données à lire ou à écrire. Il s&#39;agit d&#39;un argument obligatoire.
* **—dataFrame {df}**: La base de données des pandas. Il s&#39;agit d&#39;un argument obligatoire.
   * Lorsque l&#39;action est &quot;read&quot;, {df} est la variable où les résultats de l&#39;opération de lecture du jeu de données sont disponibles.
   * Lorsque l&#39;action est &quot;write&quot;, ce dataframe {df} est écrit dans le dataset.
* **—mode (facultatif)**: Les paramètres autorisés sont &quot;batch&quot; et &quot;interactive&quot;. Par défaut, le mode est défini sur &quot;interactif&quot;. Il est recommandé d’utiliser le mode &quot;batch&quot; lors de la lecture de grandes quantités de données.

**Exemples**

* **Exemple** de lecture : `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
* **Exemple** d&#39;écriture : `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

### Requête de données à l’aide [!DNL Query Service] de la section [!DNL Python]

[!DNL JupyterLab][!DNL Platform][!DNL Python] sur vous permet d’utiliser SQL dans un notebook pour accéder aux données via <a href="https://docs.adobe.com/content/help/fr-FR/experience-platform/query/home.html" target="_blank">Adobe Experience Platform Query Service</a>. Accessing data through [!DNL Query Service] can be useful for dealing with large datasets due to its superior running times. Be advised that querying data using [!DNL Query Service] has a processing time limit of ten minutes.

Before you use [!DNL Query Service] in [!DNL JupyterLab], ensure you have a working understanding of the <a href="https://docs.adobe.com/content/help/fr-FR/experience-platform/query/home.html#!api-specification/markdown/narrative/technical_overview/query-service/sql/syntax.md" target="_blank">[!DNL Query Service] SQL syntax</a>.

Querying data using [!DNL Query Service] requires you to provide the name of the target dataset. Vous pouvez générer les cellules de code nécessaires en recherchant le jeu de données souhaité à l’aide de l’**explorateur de données**. Cliquez avec le bouton droit de la souris sur la liste de jeux de données et cliquez sur **Query Data dans Notebook** pour générer les deux cellules de code suivantes dans votre notebook :


In order to utilize [!DNL Query Service] in [!DNL JupyterLab], you must first create a connection between your working [!DNL Python] notebook and [!DNL Query Service]. Pour ce faire, exécutez la première cellule générée.

```python
qs_connect()
```

Dans la seconde cellule générée, la première ligne doit être définie avant la requête SQL. Par défaut, la cellule générée définit une variable facultative (`df0`) qui enregistre les résultats des requêtes sous la forme d’un cadre de données pandas. <br>L’argument `-c QS_CONNECTION` est obligatoire et indique au noyau d’exécuter la requête SQL sur [!DNL Query Service]. Consultez l’[annexe](#optional-sql-flags-for-query-service) pour obtenir une liste d’arguments supplémentaires.

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Vous pouvez référencer les variables Python directement dans une requête SQL en utilisant une syntaxe au format chaîne et en mettant les variables entre accolades (`{}`), comme indiqué dans l’exemple suivant :

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filter ExperienceEvent data in [!DNL Python]/R

In order to access and filter an ExperienceEvent dataset in a [!DNL Python] or R notebook, you must provide the ID of the dataset (`{DATASET_ID}`) along with the filter rules that define a specific time range using logical operators. Lorsqu’un intervalle de temps est défini, toute pagination spécifiée est ignorée et le jeu de données complet est pris en compte.

Une liste d’opérateurs de filtrage est décrite ci-dessous :

* `eq()` : égal à
* `gt()` : supérieur à
* `ge()` : supérieur ou égal à
* `lt()` : inférieur à
* `le()` : inférieur ou égal à
* `And()` : opérateur ET logique
* `Or()` : opérateur OU logique

Les cellules suivantes filtrent un jeu de données ExperienceEvent pour obtenir les données qui existent exclusivement entre le 1er janvier 2019 et le 31 décembre 2019 inclus.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

### Filtrage des données ExperienceEvent en PySpark/[!DNL Spark]

Accessing and filtering an ExperienceEvent dataset in a PySpark or Scala notebook requires you to provide the dataset identity (`{DATASET_ID}`), your organization&#39;s IMS identity, and the filter rules defining a specific time range. Un intervalle de temps de filtrage est défini à l’aide de la fonction `spark.sql()`, où le paramètre de fonction est une chaîne de requête SQL.

Les cellules suivantes filtrent un jeu de données ExperienceEvent pour obtenir les données qui existent exclusivement entre le 1er janvier 2019 et le 31 décembre 2019 inclus.

#### PySpark 3 ([!DNL Spark] 2.4) {#pyspark3-spark2.4}

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

#### Scala ([!DNL Spark] 2.4) {#scala-spark}

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

>[!TIP]
>
>Dans Scala, vous pouvez utiliser `sys.env()` pour déclarer et renvoyer une valeur de l’intérieur `option`. Cela évite de définir des variables si vous savez qu’elles ne seront utilisées qu’une seule fois. L’exemple suivant extrait `val userToken` de l’exemple ci-dessus et le déclare en ligne `option` comme alternative :
> 
```scala
> .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
> ```

## Bibliothèques prises en charge {#supported-libraries}

### [!DNL Python] / R

| Bibliothèque | Version |
| :------ | :------ |
| notebook | 6.0.0 |
| requests | 2.22.0 |
| plotly | 4.0.0 |
| folium | 0.10.0 |
| ipywidgets | 7.5.1 |
| bokeh | 1.3.1 |
| gensim | 3.7.3 |
| ipyparallel | 0.5.2 |
| jq | 1.6 |
| keras | 2.2.4 |
| nltk | 3.2.5 |
| pandas | 0.22.0 |
| pandasql | 0.7.3 |
| pillow | 6.0.0 |
| scikit-image | 0.15.0 |
| scikit-learn | 0.21.3 |
| scipy | 1.3.0 |
| scrapy | 1.3.0 |
| seaborn | 0.9.0 |
| statsmodels | 0.10.1 |
| elastic | 5.1.0.17 |
| ggplot | 0.11.5 |
| py-xgboost | 0.90 |
| opencv | 3.4.1 |
| pyspark | 2.4.3 |
| pytorch | 1.0.1 |
| wxpython | 4.0.6 |
| colorlover | 0.3.0 |
| geopandas | 0.5.1 |
| pyshp | 2.1.0 |
| shapely | 1.6.4 |
| rpy2 | 2.9.4 |
| r-essentials | 3.6 |
| r-arules | 1.6_3 |
| r-fpc | 2.2_3 |
| r-e1071 | 1.7_2 |
| r-gam | 1.16.1 |
| r-gbm | 2.1.5 |
| r-ggthemes | 4.2.0 |
| r-ggvis | 0.4.4 |
| r-igraph | 1.2.4.1 |
| r-leaps | 3.0 |
| r-manipulate | 1.0.1 |
| r-rocr | 1.0_7 |
| r-rmysql | 0.10.17 |
| r-rodbc | 1.3_15 |
| r-rsqlite | 2.1.2 |
| r-rstan | 2.19.2 |
| r-sqldf | 0.4_11 |
| r-survival | 2.44_1.1 |
| r-zoo | 1.8_6 |
| r-stringdist | 0.9.5.2 |
| r-quadprog | 1.5_7 |
| r-rjson | 0.2.20 |
| r-forecast | 8.7 |
| r-rsolnp | 1.16 |
| r-reticulate | 1.12 |
| r-mlr | 2.14.0 |
| r-viridis | 0.5.1 |
| r-corrplot | 0.84 |
| r-fnn | 1.1.3 |
| r-lubridate | 1.7.4 |
| r-randomforest | 4.6_14 |
| r-tidyverse | 1.2.1 |
| r-tree | 1.0_39 |
| pymongo | 3.8.0 |
| pyarrow | 0.14.1 |
| boto3 | 1.9.199 |
| ipyvolume | 0.5.2 |
| fastparquet | 0.3.2 |
| python-snappy | 0.5.4 |
| ipywebrtc | 0.5.0 |
| jupyter_client | 5.3.1 |
| wordcloud | 1.5.0 |
| graphviz | 2.40.1 |
| python-graphviz | 0.11.1 |
| azure-storage | 0.36.0 |
| [!DNL jupyterlab] | 1.0.4 |
| pandas_ml | 0.6.1 |
| tensorflow-gpu | 1.14.0 |
| nodejs | 12.3.0 |
| mock | 3.0.5 |
| ipympl | 0.3.3 |
| fonts-anacond | 1.0 |
| psycopg2 | 2.8.3 |
| nose | 1.3.7 |
| autovizwidget | 0.12.9 |
| altair | 3.1.0 |
| vega_datasets | 0.7.0 |
| papermill | 1.0.1 |
| sql_magic | 0.0.4 |
| iso3166 | 1.0 |
| nbimporter | 0.3.1 |

### PySpark

| Bibliothèque | Version |
| :------ | :------ |
| requests | 2.18.4 |
| gensim | 2.3.0 |
| keras | 2.0.6 |
| nltk | 3.2.4 |
| pandas | 0.20.1 |
| pandasql | 0.7.3 |
| pillow | 5.3.0 |
| scikit-image | 0.13.0 |
| scikit-learn | 0.19.0 |
| scipy | 0.19.1 |
| scrapy | 1.3.3 |
| statsmodels | 0.8.0 |
| elastic | 4.0.30.44 |
| py-xgboost | 0.60 |
| opencv | 3.1.0 |
| pyarrow | 0.8.0 |
| boto3 | 1.5.18 |
| azure-storage-blob | 1.4.0 |
| [!DNL python] | 3.6.7 |
| mkl-rt | 11.1 |

## Optional SQL flags for [!DNL Query Service] {#optional-sql-flags-for-query-service}

Ce tableau décrit les indicateurs SQL facultatifs qui peuvent être utilisés pour [!DNL Query Service].

| **Indicateur** | **Description** |
| --- | --- |
| `-h`, `--help` | Affichez le message d’aide et fermez-le. |
| `-n`, `--notify` | Option d’activation et de désactivation pour la notification des résultats de la requête. |
| `-a`, `--async` | L’utilisation de cet indicateur permet d’exécuter la requête de manière asynchrone et de libérer le noyau pendant l’exécution de la requête. Soyez prudent lorsque vous attribuez les résultats de la requête à des variables, car il se peut qu’ils ne soient pas définis si la requête n’est pas terminée. |
| `-d`, `--display` | L’utilisation de cet indicateur empêche l’affichage des résultats. |

