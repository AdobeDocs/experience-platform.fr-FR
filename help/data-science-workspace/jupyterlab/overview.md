---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics
solution: Experience Platform
title: Guide de l'utilisateur de JupyterLab
topic: Overview
translation-type: tm+mt
source-git-commit: 440310339003bf23c9fcfc69a6ec1eacddc9f413
workflow-type: tm+mt
source-wordcount: '3672'
ht-degree: 11%

---


# Guide de l&#39;utilisateur de JupyterLab

JupyterLab est une interface utilisateur web pour <a href="https://jupyter.org/" target="_blank">Project Jupyter</a> et est étroitement intégrée dans [!DNL Adobe Experience Platform]le projet. Il fournit un environnement de développement interactif pour que les chercheurs en données puissent travailler avec des ordinateurs portables, du code et des données Jupyter.

Ce document fournit un aperçu de JupyterLab et de ses fonctionnalités ainsi que des instructions pour effectuer des actions courantes.

## JupyterLab sur la plate-forme d’expérience

L&#39;intégration JupyterLab de la plateforme Experience Platform s&#39;accompagne de modifications architecturales, de considérations de conception, d&#39;extensions personnalisées de blocs-notes, de bibliothèques préinstallées et d&#39;une interface sur le thème de l&#39;Adobe.

La liste suivante décrit certaines des fonctionnalités propres à JupyterLab sur la plate-forme :

| Fonction | Description |
| --- | --- |
| **Noisettes** | Les noyaux fournissent un bloc-notes et d&#39;autres front-end JupyterLab la possibilité d&#39;exécuter et d&#39;introduire du code dans différents langages de programmation. Experience Platform fournit des noyaux supplémentaires pour prendre en charge le développement en Python, R, PySpark et Spark. Consultez la section [Noisettes](#kernels) pour plus de détails. |
| **Accès aux données** | Accédez directement aux jeux de données existants dans JupyterLab avec la prise en charge complète des fonctions de lecture et d&#39;écriture. |
| **Intégration du service de plateforme** | Les intégrations intégrées vous permettent d&#39;utiliser d&#39;autres services de plate-forme directement depuis JupyterLab. Une liste complète des intégrations prises en charge est fournie dans la section relative à l’ [intégration à d’autres services](#service-integration)de plateforme. |
| **Authentification** | Outre le modèle <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">de sécurité intégré de</a>JupyterLab, chaque interaction entre votre application et la plateforme d’expérience, y compris la communication service-à-service de la plateforme, est chiffrée et authentifiée par le biais de l’ <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Bibliothèques de développement** | Dans Experience Platform, JupyterLab fournit des bibliothèques préinstallées pour Python, R et PySpark. Consultez l’ [annexe](#supported-libraries) pour obtenir une liste complète des bibliothèques prises en charge. |
| **Contrôleur de bibliothèque** | Lorsque les bibliothèques pré-installées manquent à vos besoins, d&#39;autres bibliothèques peuvent être installées pour Python et R, et sont temporairement stockées dans des conteneurs isolés pour maintenir l&#39;intégrité de Platform et protéger vos données. Consultez la section [Noisettes](#kernels) pour plus de détails. |

>[!NOTE] Les bibliothèques supplémentaires ne sont disponibles que pour la session au cours de laquelle elles ont été installées. Vous devez réinstaller les bibliothèques supplémentaires dont vous avez besoin lors du démarrage de nouvelles sessions.

## Intégration à d’autres services de plate-forme {#service-integration}

La normalisation et l&#39;interopérabilité sont les concepts clés qui sous-tendent [!DNL Experience Platform]. L&#39;intégration de JupyterLab sur [!DNL Platform] en tant qu&#39;IDE intégré lui permet d&#39;interagir avec d&#39;autres [!DNL Platform] services, ce qui vous permet d&#39;utiliser [!DNL Platform] au maximum son potentiel. Les [!DNL Platform] services suivants sont disponibles dans JupyterLab :

* **Service de catalogue :** Accédez et explorez des jeux de données avec des fonctionnalités de lecture et d&#39;écriture.
* **Requête Service :** Accédez aux jeux de données et explorez-les à l&#39;aide de SQL, ce qui vous permet de réduire les frais généraux d&#39;accès aux données lorsque vous manipulez de grandes quantités de données.
* **Sensei ML Framework :** Développement de modèles avec la possibilité de former et de marquer des données, ainsi que la création de recettes d&#39;un simple clic.
* **Modèle de données d’expérience (XDM) :** La normalisation et l’interopérabilité sont des concepts clés de la plateforme d’expérience Adobe. [Le modèle de données d’expérience (XDM)](https://www.adobe.com/go/xdm-home-en), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

>[!NOTE] Certaines intégrations [!DNL Platform] de service sur JupyterLab sont limitées à des noyaux spécifiques. Consultez la section sur les [noyaux](#kernels) pour plus de détails.

## Fonctions clés et opérations communes

Vous trouverez des informations sur les principales fonctionnalités de JupyterLab et des instructions sur l&#39;exécution d&#39;opérations communes dans les sections suivantes :

* [Accès à JupyterLab](#access-jupyterlab)
* [Interface de JupyterLab](#jupyterlab-interface)
* [Cellules de code](#code-cells)
* [Noisettes](#kernels)
* [Sessions du noyau](#kernel-sessions)
* [Ressource d’exécution PySpark/Spark](#execution-resource)
* [Lanceur](#launcher)

### Accès à JupyterLab {#access-jupyterlab}

Dans [Adobe Experience Platform](https://platform.adobe.com), sélectionnez **Notebooks** dans la colonne de navigation de gauche. Il faut du temps pour que JupyterLab s&#39;initialise complètement.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### Interface de JupyterLab {#jupyterlab-interface}

L&#39;interface JupyterLab est composée d&#39;une barre de menus, d&#39;une barre latérale gauche réductible et de la zone de travail principale contenant des onglets de documents et d&#39;activités.

**Barre de menus**

La barre de menus en haut de l&#39;interface comporte des menus de niveau supérieur qui exposent les actions disponibles dans JupyterLab avec leurs raccourcis clavier :

* **Fichier :** Actions liées aux fichiers et répertoires
* **Modifier :** Actions liées à la modification des documents et autres activités
* **Vue :** Actions qui modifient l&#39;apparence de JupyterLab
* **Exécuter :** Actions d’exécution de code dans différentes activités, telles que les ordinateurs portables et les consoles de code
* **Noyau :** Actions de gestion des noyaux
* **Onglets :** Une liste de documents et d&#39;activités ouverts
* **Paramètres :** Paramètres courants et éditeur de paramètres avancé
* **Aide :** Une liste de liens vers l&#39;aide de JupyterLab et du noyau

**Barre latérale gauche**

La barre latérale gauche contient des onglets cliquables qui permettent d’accéder aux fonctionnalités suivantes :

* **Navigateur de fichiers :** liste de documents et répertoires d&#39;ordinateurs portables enregistrés
* **Explorateur de données :** Parcourir, accéder et explorer des jeux de données et des schémas
* **Noeuds et terminaux en cours d&#39;exécution :** Une liste de sessions actives du noyau et du terminal avec la possibilité d&#39;arrêter
* **Commandes :** liste de commandes utiles
* **Inspecteur de cellule :** Editeur de cellules qui donne accès aux outils et aux métadonnées utiles pour configurer un bloc-notes à des fins de présentation
* **onglets :** liste d’onglets ouverts

Cliquez sur un onglet pour exposer ses fonctionnalités ou cliquez sur un onglet développé pour réduire la barre latérale gauche comme illustré ci-dessous :

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Domaine de travail principal**

L&#39;aire de travail principale de JupyterLab vous permet d&#39;organiser les documents et autres activités en panneaux d&#39;onglets qui peuvent être redimensionnés ou subdivisés. Faites glisser un onglet au centre d’un panneau d’onglets pour migrer l’onglet. Divisez un panneau en faisant glisser un onglet vers la gauche, la droite, le haut ou le bas du panneau :

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Cellules de code {#code-cells}

Les cellules de code sont le contenu principal des blocs-notes. Ils contiennent le code source dans la langue du noyau associé au bloc-notes et la sortie résultant de l&#39;exécution de la cellule de code. Un nombre d’exécutions est affiché à droite de chaque cellule de code qui représente son ordre d’exécution.

![](../images/jupyterlab/user-guide/code_cell.png)

Les actions de cellule courantes sont décrites ci-dessous :

* **Ajouter une cellule :** Cliquez sur le symbole plus (**+**) dans le menu du bloc-notes pour ajouter une cellule vide. Les nouvelles cellules sont placées sous la cellule qui est actuellement en cours d&#39;interaction avec, ou à la fin du bloc-notes si aucune cellule particulière n&#39;est active.

* **Déplacer une cellule :** Placez votre curseur à droite de la cellule que vous souhaitez déplacer, puis cliquez et faites glisser la cellule vers un nouvel emplacement. En outre, le déplacement d&#39;une cellule d&#39;un bloc-notes vers un autre reproduit la cellule avec son contenu.

* **Exécuter une cellule :** Cliquez sur le corps de la cellule à exécuter, puis sur l&#39;icône **play** (**▶**) du menu du bloc-notes. Un astérisque (**\***) s&#39;affiche dans le compteur d&#39;exécution de la cellule lorsque le noyau traite l&#39;exécution et est remplacé par un entier une fois l&#39;exécution terminée.

* **Supprimer une cellule :** Cliquez sur le corps de la cellule à supprimer, puis sur l&#39;icône **ciseau** .

### Noisettes {#kernels}

Les noyaux portables sont les moteurs informatiques spécifiques à la langue pour le traitement des cellules de portables. En plus de Python, JupyterLab fournit une prise en charge linguistique supplémentaire dans R, PySpark et Spark (Scala). Lorsque vous ouvrez un document de bloc-notes, le noyau associé est lancé. Lorsqu&#39;une cellule d&#39;ordinateur portable est exécutée, le noyau effectue le calcul et produit des résultats qui peuvent consommer d&#39;importantes ressources de processeur et de mémoire. Notez que la mémoire allouée n&#39;est pas libérée tant que le noyau n&#39;est pas fermé.

Certaines fonctions et fonctionnalités sont limitées à des noyaux particuliers, comme décrit dans le tableau ci-dessous :

| Noyau | Prise en charge de l’installation de la bibliothèque | Intégrations de plateformes |
| :----: | :--------------------------: | :-------------------- |
| **Python** | Oui | <ul><li>Cadre de gestion de Sensei ML</li><li>Service de catalogue</li><li>Requête Service</li></ul> |
| **r** | Oui | <ul><li>Cadre de gestion de Sensei ML</li><li>Service de catalogue</li></ul> |
| **Scala** | Non | <ul><li>Cadre de gestion de Sensei ML</li><li>Service de catalogue</li></ul> |

### Sessions du noyau {#kernel-sessions}

Chaque bloc-notes ou activité actif sur JupyterLab utilise une session de noyau. Toutes les sessions actives peuvent être trouvées en développant les terminaux **Running et l&#39;onglet kernels** de la barre latérale gauche. Le type et l&#39;état du noyau d&#39;un bloc-notes peuvent être identifiés en observant l&#39;angle supérieur droit de l&#39;interface du bloc-notes. Dans le diagramme ci-dessous, le noyau associé du bloc-notes est **Python 3** et son état actuel est représenté par un cercle gris à droite. Un cercle creux implique un noyau inactif et un cercle plein implique un noyau occupé.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Si le noyau est fermé ou inactif pendant une longue période, alors **Pas de noyau !** avec un cercle plein s’affiche. Activez un noyau en cliquant sur son état et en sélectionnant le type de noyau approprié, comme indiqué ci-dessous :

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Lanceur {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

Le *lanceur* personnalisé fournit des modèles de blocs-notes utiles pour les noyaux pris en charge afin de vous aider à démarrer votre tâche, notamment :

| Modèle | Description |
| --- | --- |
| Vierge | Un fichier bloc-notes vide. |
| Démarrage | Un bloc-notes prérempli présentant l&#39;exploration des données à l&#39;aide de données d&#39;exemple. |
| Ventes au détail | Un bloc-notes prérempli présentant la Recette <a href="https://adobe.ly/2wOgO3L" target="_blank">des ventes</a> au détail à l&#39;aide de données d&#39;exemple. |
| Créateur de recettes | Modèle de bloc-notes pour la création d&#39;une recette dans JupyterLab. Il est prérempli de code et de commentaires qui montrent et décrivent le processus de création de la recette. Pour obtenir une présentation détaillée, reportez-vous au didacticiel <a href="https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en" target="_blank">de recette du</a> bloc-notes. |
| Requête Service | Un cahier de notes prérempli montrant l&#39;utilisation de Requête Service directement dans JupyterLab avec des exemples de workflows qui analysent les données à l&#39;échelle. |
| Événements XDM | Un bloc-notes prérempli présentant l’exploration des données sur les données du Événement d’expérience post-valeur, axé sur les fonctionnalités communes à l’ensemble de la structure de données. |
| Requêtes XDM | Un cahier de notes prérempli présentant des exemples de requêtes commerciales sur les données du Événement d’expérience. |
| Agrégation | Un bloc-notes prérempli présentant des échantillons de workflows pour agrégat de grandes quantités de données en petits blocs gérables. |
| Mise en grappe | Un bloc-notes prérempli présentant le processus de modélisation d’apprentissage automatique de bout en bout à l’aide d’algorithmes de mise en grappe. |

Certains modèles de bloc-notes sont limités à certains noyaux. La disponibilité des modèles pour chaque noyau est mise en correspondance dans le tableau suivant :

<table>
    <tr>
        <td></td>
        <th><strong>Vierge</strong></th>
        <th><strong>Démarrage</strong></th>
        <th><strong>Ventes au détail</strong></th>
        <th><strong>Créateur de recettes</strong></th>
        <th><strong>Requête Service</strong></th>
        <th><strong>Événements XDM</strong></th>
        <th><strong>Requêtes XDM</strong></th>
        <th><strong>Agrégation</strong></th>
        <th><strong>Mise en grappe</strong></th>
    </tr>
    <tr>
        <th><strong>Python</strong></th>
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
        <th ><strong>r</strong></th>
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
        <th  ><strong>PySpark 3 (Spark 2.4)</strong></th>
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

Pour ouvrir un nouveau *lanceur*, cliquez sur **Fichier > Nouveau lanceur**. Vous pouvez également développer le navigateur **** de fichiers depuis la barre latérale gauche et cliquer sur le symbole plus (**+**) :

![](../images/jupyterlab/user-guide/new_launcher.gif)

## Accès aux données de la plate-forme à l’aide de portables

Chaque noyau pris en charge fournit des fonctionnalités intégrées qui vous permettent de lire les données de la plate-forme à partir d&#39;un jeu de données dans un bloc-notes. Cependant, la prise en charge de la pagination des données est limitée aux ordinateurs portables Python et R.

### Limites des données des ordinateurs portables

Les informations suivantes définissent la quantité maximale de données pouvant être lues, le type de données utilisé et la période estimée de lecture des données. Pour Python et R, un serveur de portables configuré à 40 Go de RAM a été utilisé pour les tests. Pour PySpark et Scala, une grappe de serveurs de données configurée à 64 Go de RAM, 8 coeurs, 2 DBU avec un maximum de 4 travailleurs a été utilisée pour les bancs d’essai décrits ci-dessous.

Les données du schéma ExperienceEvent utilisées variaient en taille en commençant par un millier de lignes (1K) allant jusqu’à un milliard de lignes (1B). Notez que pour les mesures PySpark et Spark, une période de 10 jours a été utilisée pour les données XDM.

Les données de schéma ad hoc ont été prétraitées à l’aide de l’outil de création de table en tant que sélection de Requête Service (CTAS). Ces données varient également en taille en commençant par un millier (1K) de lignes allant jusqu&#39;à un milliard (1B) de lignes.

#### Limites de données des ordinateurs portables Python

**schéma XDM ExperienceEvent :** Vous devriez être en mesure de lire un maximum de 2 millions de lignes (environ 6,1 Go de données sur le disque) de données XDM en moins de 22 minutes. Ajouter des lignes supplémentaires peut entraîner des erreurs.

| Nombre de lignes | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Taille sur le disque (Mo) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK (en secondes) | 20.3 | 86.8 | 63 | 659 | 1315 |

**schéma ad hoc :** Vous devriez être en mesure de lire un maximum de 5 millions de lignes (environ 5,6 Go de données sur le disque) de données non XDM (ad hoc) en moins de 14 minutes. Ajouter des lignes supplémentaires peut entraîner des erreurs.

| Nombre de lignes | 1K | 10K | 100K | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Taille sur le disque (en Mo) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (en secondes) | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

#### Limites de données des ordinateurs portables R

**schéma XDM ExperienceEvent :** Vous devriez être en mesure de lire un maximum de 1 million de lignes de données XDM (3 Go de données sur le disque) en moins de 13 minutes.

| Nombre de lignes | 1K | 10K | 100K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Taille sur le disque (Mo) | 18.73 | 187.5 | 308 | 3000 |
| Noyau R (en secondes) | 14.03 | 69.6 | 86.8 | 775 |

**schéma ad hoc :** Vous devriez pouvoir lire un maximum de 3 millions de lignes de données ad hoc (293 Mo de données sur le disque) en 10 minutes environ.

| Nombre de lignes | 1K | 10K | 100K | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Taille sur le disque (en Mo) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| SDK R (en s) | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

#### Limites de données des blocs-notes PySpark (noyau Python) :

**schéma XDM ExperienceEvent :** En mode Interactif, vous devriez pouvoir lire un maximum de 5 millions de lignes (environ 13,42 Go de données sur disque) de données XDM en 20 minutes environ. Le mode interactif ne prend en charge que jusqu’à 5 millions de lignes. Si vous souhaitez lire des jeux de données plus volumineux, il est conseillé de passer en mode Lot. En mode Batch, vous devriez pouvoir lire un maximum de 500 millions de lignes (environ 1,31 To de données sur disque) de données XDM en 14 heures environ.

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

#### Limites des données du bloc-notes Spark (noyau Scala) :

**schéma XDM ExperienceEvent :** En mode Interactif, vous devriez pouvoir lire un maximum de 5 millions de lignes (environ 13,42 Go de données sur disque) de données XDM en 18 minutes environ. Le mode interactif ne prend en charge que jusqu’à 5 millions de lignes. Si vous souhaitez lire des jeux de données plus volumineux, il est conseillé de passer en mode Lot. En mode Batch, vous devriez pouvoir lire un maximum de 500 millions de lignes (environ 1,31 To de données sur disque) de données XDM en 14 heures environ.

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

### Lire à partir d&#39;un jeu de données en Python/R

Les portables Python et R vous permettent de paginer les données lors de l&#39;accès aux jeux de données. L&#39;exemple de code pour lire les données avec et sans pagination est illustré ci-dessous.

[//]: # (In the following samples, the first step is currently required but once the SDK is complete, users are no longer required to explicitly define client_context)

#### Lire à partir d&#39;un jeu de données en Python/R sans pagination

L&#39;exécution du code suivant lit le jeu de données complet. Si l’exécution est réussie, les données sont alors enregistrées en tant que base de données Pandas référencée par la variable `df`.

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

* `{DATASET_ID}`: L&#39;identité unique du jeu de données à accéder

#### Lire à partir d&#39;un jeu de données en Python/R avec pagination

L&#39;exécution du code suivant lit les données du jeu de données spécifié. La pagination est obtenue en limitant et en décalant les données par le biais des fonctions `limit()` et `offset()` respectivement. La limitation des données fait référence au nombre maximal de points de données à lire, tandis que la compensation fait référence au nombre de points de données à ignorer avant la lecture des données. Si l&#39;opération de lecture s&#39;exécute correctement, les données sont enregistrées en tant que base de données Pandas référencée par la variable `df`.

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

* `{DATASET_ID}`: L&#39;identité unique du jeu de données à accéder

### Lecture à partir d’un jeu de données dans PySpark/Spark/Scala

Lorsqu&#39;un bloc-notes PySpark ou Scala actif est ouvert, développez l&#39;onglet Explorateur **de** données dans la barre latérale gauche et cliquez sur **Datasets** par doublon pour vue une liste de jeux de données disponibles. Cliquez avec le bouton droit de la souris sur le jeu de données auquel vous souhaitez accéder et cliquez sur **Explorer les données dans un bloc-notes**. Les cellules de code suivantes sont générées :

#### PySpark (Spark 2.4) {#pyspark2.4}

Avec l&#39;introduction de Spark 2.4, la magie [`%dataset`](#magic) personnalisée est fournie.

```python
# PySpark 3 (Spark 2.4)

%dataset read --datasetId {DATASET_ID} --dataFrame pd0
pd0.describe()
pd0.show(10, False)
```

#### Scala (Spark 2.4) {#spark2.4}

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
>Dans Scala, vous pouvez utiliser `sys.env()` pour déclarer et renvoyer une valeur de l’intérieur `option`.

### Utilisation de la magie %dataset dans les blocs-notes PySpark 3 (Spark 2.4) {#magic}

Avec l&#39;introduction de Spark 2.4, la magie `%dataset` personnalisée est fournie pour les nouveaux portables PySpark 3 (Spark 2.4) (noyau Python 3).

**Utilisation**

`%dataset {action} --datasetId {id} --dataFrame {df}`

**Description**

Commande magique Data Science Workspace personnalisée pour lire ou écrire un jeu de données à partir d&#39;un bloc-notes Python (noyau Python 3).

* **{action}**: Type d’action à exécuter sur le jeu de données. Deux actions sont disponibles &quot;read&quot; ou &quot;write&quot;.
* **—datasetId {id}**: Utilisé pour fournir l&#39;identifiant du jeu de données à lire ou à écrire. Il s&#39;agit d&#39;un argument obligatoire.
* **—dataFrame {df}**: La base de données des pandas. Il s&#39;agit d&#39;un argument obligatoire.
   * Lorsque l&#39;action est &quot;read&quot;, {df} est la variable où les résultats de l&#39;opération de lecture du jeu de données sont disponibles.
   * Lorsque l&#39;action est &quot;write&quot;, ce dataframe {df} est écrit dans le dataset.
* **—mode (facultatif)**: Les paramètres autorisés sont &quot;batch&quot; et &quot;interactive&quot;. Par défaut, le mode est défini sur &quot;interactif&quot;. Il est recommandé d’utiliser le mode &quot;batch&quot; lors de la lecture de grandes quantités de données.

**Exemples**

* **Exemple** de lecture : `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
* **Exemple** d&#39;écriture : `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

### Données de Requête utilisant Requête Service en Python

JupyterLab sur la plate-forme vous permet d&#39;utiliser SQL dans un bloc-notes Python pour accéder aux données via le service <a href="https://www.adobe.com/go/query-service-home-en" target="_blank">de Requête de la plateforme</a>Adobe Experience Platform. L&#39;accès aux données via Requête Service peut s&#39;avérer utile pour traiter des jeux de données volumineux en raison de ses délais d&#39;exécution supérieurs. Notez que l’interrogation de données à l’aide de Requête Service est limitée à dix minutes de temps de traitement.

Avant d’utiliser Requête Service dans JupyterLab, assurez-vous de bien comprendre la syntaxe <a href="https://www.adobe.com/go/query-service-sql-syntax-en" target="_blank">SQL de</a>Requête Service.

Pour interroger des données à l’aide de Requête Service, vous devez indiquer le nom du jeu de données de cible. Vous pouvez générer les cellules de code nécessaires en recherchant le jeu de données de votre choix à l’aide de l’explorateur **de** données. Cliquez avec le bouton droit sur la liste des jeux de données et cliquez sur Données de **Requête dans le bloc-notes** pour générer les deux cellules de code suivantes dans votre bloc-notes :


Pour utiliser Requête Service dans JupyterLab, vous devez d&#39;abord créer une connexion entre votre portable Python et Requête Service. Pour ce faire, vous pouvez exécuter la première cellule générée.

```python
qs_connect()
```

Dans la seconde cellule générée, la première ligne doit être définie avant la requête SQL. Par défaut, la cellule générée définit une variable facultative (`df0`) qui enregistre les résultats de la requête sous la forme d’un cadre de données Pandas. <br>L&#39; `-c QS_CONNECTION` argument est obligatoire et indique au noyau d&#39;exécuter la requête SQL sur Requête Service. Voir l&#39; [annexe](#optional-sql-flags-for-query-service) pour une liste d&#39;arguments supplémentaires.

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Les variables Python peuvent être directement référencées dans une requête SQL en utilisant une syntaxe au format chaîne et en encapsulant les variables entre accolades (`{}`), comme indiqué dans l&#39;exemple suivant :

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filtrage des données ExperienceEvent en Python/R

Pour accéder à un jeu de données ExperienceEvent et le filtrer dans un bloc-notes Python ou R, vous devez fournir l&#39;ID du jeu de données (`{DATASET_ID}`) ainsi que les règles de filtrage qui définissent une plage de temps spécifique à l&#39;aide d&#39;opérateurs logiques. Lorsqu’une plage de temps est définie, toute pagination spécifiée est ignorée et le jeu de données complet est pris en compte.

Une liste d’opérateurs de filtrage est décrite ci-dessous :

* `eq()`: Egal à
* `gt()`: Supérieur à
* `ge()`: Supérieur ou égal à
* `lt()`: Inférieur à
* `le()`: Inférieur ou égal à
* `And()`: Opérateur ET logique
* `Or()`: Opérateur OU logique

Les cellules suivantes filtrent un jeu de données ExperienceEvent en données existant exclusivement entre le 1er janvier 2019 et la fin du 31 décembre 2019.

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

### Filtrage des données ExperienceEvent dans PySpark/Spark

L’accès et le filtrage d’un jeu de données ExperienceEvent dans un bloc-notes PySpark ou Scala nécessitent que vous fournissiez l’identité (`{DATASET_ID}`) du jeu de données, l’identité IMS de votre entreprise et les règles de filtrage définissant une plage de temps spécifique. Une plage de temps de filtrage est définie à l&#39;aide de la fonction `spark.sql()`, où le paramètre de fonction est une chaîne de requête SQL.

Les cellules suivantes filtrent un jeu de données ExperienceEvent en données existant exclusivement entre le 1er janvier 2019 et la fin du 31 décembre 2019.

#### PySpark 3 (Spark 2.4) {#pyspark3-spark2.4}

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

#### Scala (Spark 2.4) {#scala-spark}

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
>Dans Scala, vous pouvez utiliser `sys.env()` pour déclarer et renvoyer une valeur de l’intérieur `option`. Cela évite de définir des variables si vous savez qu’elles ne seront utilisées qu’une seule fois. L’exemple suivant extrait `val userToken` de l’exemple ci-dessus et le déclare en ligne `option` comme alternative :
> 
```scala
> .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
> ```

## Bibliothèques prises en charge {#supported-libraries}

### Python / R

| Bibliothèque | Version |
| :------ | :------ |
| ordinateur portable | 6.0.0 |
| requêtes | 2.22.0 |
| poliment | 4.0.0 |
| folium | 0.10.0 |
| ipywidgets | 7.5.1 |
| bokeh | 1.3.1 |
| gensime | 3.7.3 |
| ipyparallèle | 0.5.2 |
| jq | 1.6 |
| keras | 2.2.4 |
| nltk | 3.2.5 |
| pandas | 0.22.0 |
| pandasql | 0.7.3 |
| oreiller | 6.0.0 |
| scikit-image | 0.15.0 |
| scikit-learn | 0.21.3 |
| scintillement | 1.3.0 |
| effrayant | 1.3.0 |
| seaborn | 0.9.0 |
| statsmodels | 0.10.1 |
| élastique | 5.1.0.17 |
| ggplot | 0.11.5 |
| py-xgboog | 0.90 |
| opencv | 3.4.1 |
| pyspark | 2.4.3 |
| pytorche | 1.0.1 |
| wxpython | 4.0.6 |
| colorlover | 0.3.0 |
| géopandas | 0.5.1 |
| pyshp | 2.1.0 |
| informe | 1.6.4 |
| rpy2 | 2.9.4 |
| essentiels | 3.6 |
| r-arules | 1.6_3 |
| r-fpc | 2.2_3 |
| r-e1071 | 1.7_2 |
| r-gam | 1.16.1 |
| r-gbm | 2.1.5 |
| r-ggthemes | 4.2.0 |
| r-ggvis | 0.4.4 |
| r-igraph | 1.2.4.1 |
| sauts | 3.0 |
| remanipuler | 1.0.1 |
| r-rocr | 1.0_7 |
| r-rmysql | 0.10.17 |
| r-rodbc | 1.3_15 |
| r-rsqlite | 2.1.2 |
| r-rstan | 2.19.2 |
| r-sqldf | 0.4_11 |
| r-survie | 2.44_1.1 |
| r-zoo | 1.8_6 |
| r-string | 0.9.5.2 |
| r-quadprog | 1.5_7 |
| r-rjson | 0.2.20 |
| r-prévision | 8.7 |
| r-rsolnp | 1.16 |
| r-réticulate | 1.12 |
| r-mlr | 2.14.0 |
| r-viridis | 0.5.1 |
| r-corrplot | 0.84 |
| r-fnn | 1.1.3 |
| r-lubridate | 1.7.4 |
| forêt r-aléatoire | 4.6_14 |
| r-tidyverse | 1.2.1 |
| r-tree | 1.0_39 |
| pymongo | 3.8.0 |
| pyflèche | 0.14.1 |
| boto3 | 1.9.199 |
| ipyvolume | 0.5.2 |
| parquet | 0.3.2 |
| python-snappy | 0.5.4 |
| ipywebrtc | 0.5.0 |
| jupyter_client | 5.3.1 |
| wordcloud | 1.5.0 |
| graphviz | 2.40.1 |
| python-graphviz | 0.11.1 |
| enregistrement azur | 0.36.0 |
| jupyterlablablablablablablablablablablabé | 1.0.4 |
| pandas_ml | 0.6.1 |
| tensorflow-gpu | 1.14.0 |
| nodejs | 12.3.0 |
| se moquer | 3.0.5 |
| ipymphe | 0.3.3 |
| fonts-anacond | 1.0 |
| psycopg2 | 2.8.3 |
| nez | 1.3.7 |
| autovizwidget | 0.12.9 |
| altair | 3.1.0 |
| vega_datasets | 0.7.0 |
| papeterie | 1.0.1 |
| sql_Magic | 0.0.4 |
| iso3166 | 1.0 |
| nbimportateur | 0.3.1 |

### PySpark

| Bibliothèque | Version |
| :------ | :------ |
| requêtes | 2.18.4 |
| gensime | 2.3.0 |
| keras | 2.0.6 |
| nltk | 3.2.4 |
| pandas | 0.20.1 |
| pandasql | 0.7.3 |
| oreiller | 5.3.0 |
| scikit-image | 0.13.0 |
| scikit-learn | 0.19.0 |
| scintillement | 0.19.1 |
| effrayant | 1.3.3 |
| statsmodels | 0.8.0 |
| élastique | 4.0.30.44 |
| py-xgboog | 0.60 |
| opencv | 3.1.0 |
| pyflèche | 0.8.0 |
| boto3 | 1.5.18 |
| azure-enregistrement-blob | 1.4.0 |
| python | 3.6.7 |
| mkl-rt | 11.1 |

## Indicateurs SQL facultatifs pour Requête Service {#optional-sql-flags-for-query-service}

Ce tableau décrit les indicateurs SQL facultatifs qui peuvent être utilisés pour Requête Service.

| **Indicateur** | **Description** |
| --- | --- |
| `-h`, `--help` | Afficher le message d’aide et quitter. |
| `-n`, `--notify` | Active/désactive l&#39;option de notification des résultats de la requête. |
| `-a`, `--async` | L&#39;utilisation de cet indicateur exécute la requête de manière asynchrone et peut libérer le noyau pendant l&#39;exécution de la requête. Soyez prudent lorsque vous affectez des résultats de requête à des variables, car il se peut qu’ils ne soient pas définis si la requête n’est pas terminée. |
| `-d`, `--display` | L’utilisation de cet indicateur empêche l’affichage des résultats. |

