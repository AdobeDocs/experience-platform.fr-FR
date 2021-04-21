---
keywords: Experience Platform ; JupyterLab ; blocs-notes ; Espace de travail des sciences de données ; sujets populaires ; Git ; Github
solution: Experience Platform
title: Collaboration dans JupyterLab avec Git
topic-legacy: tutorial
type: Tutorial
description: Git est un système de contrôle de version distribué qui permet de suivre les modifications du code source au cours du développement logiciel. Git est préinstallé dans l’environnement JupyterLab de Data Science Workspace.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# Collaborez dans [!DNL JupyterLab] en utilisant [!DNL Git]

[!DNL Git] est un système de contrôle de version distribué permettant de suivre les modifications du code source au cours du développement logiciel. Git est préinstallé dans l&#39;environnement [!DNL Data Science Workspace JupyterLab].

## Conditions préalables

>[!NOTE]
>
> Le serveur Git que vous avez l&#39;intention d&#39;utiliser doit être accessible via Internet.

L&#39;environnement [!DNL Data Science Workspace JupyterLab] est un environnement hébergé et non déployé dans votre pare-feu d&#39;entreprise. Par conséquent, le serveur Git auquel vous vous connectez doit être accessible à partir de l&#39;Internet public. Il peut s’agir d’un référentiel public ou privé sur [GitHub](https://github.com/) ou d’une autre instance d’un serveur [!DNL Git] que vous avez décidé de héberger vous-même.

## Connectez [!DNL Git] à l&#39;environnement [!DNL Data Science Workspace JupyterLab Notebooks]

Début en lançant [!DNL Adobe Experience Platform] et en accédant à l&#39;environnement [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab).

Dans [!DNL JupyterLab], sélectionnez **[!UICONTROL Fichier]**, puis passez la souris sur **[!UICONTROL Nouveau]**. Dans la liste déroulante qui s&#39;affiche, sélectionnez **[!UICONTROL Terminal]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

Ensuite, dans *Terminal*, accédez à votre espace de travail en utilisant la commande suivante : `cd my-workspace`.

![espace de travail cd](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Pour afficher une liste des commandes git disponibles, émettez la commande : `git -help` dans votre terminal.

Ensuite, clonez le référentiel que vous souhaitez utiliser à l&#39;aide de la commande `git clone`. Clonez votre projet en utilisant une URL `https://` plutôt que `ssh://`.

**Exemple**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clone](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Pour effectuer des opérations d&#39;écriture (`git push`, par exemple), les commandes de configuration suivantes doivent être exécutées pour chaque nouvelle session. Notez également que toute commande push invite à saisir un nom d’utilisateur et un mot de passe.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Étapes suivantes

Une fois le clonage de votre référentiel terminé, vous pouvez utiliser Git comme vous le feriez normalement sur votre ordinateur local pour collaborer avec d&#39;autres utilisateurs sur des ordinateurs portables. Pour plus d&#39;informations sur ce que vous pouvez faire dans [!DNL JupyterLab], consultez le [[!DNL JupyterLab user guide]](./overview.md).
