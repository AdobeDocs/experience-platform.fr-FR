---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;Git;Github
solution: Experience Platform
title: Collaboration dans JupyterLab à l'aide de Git
topic: Tutorial
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 1%

---


# Collaboration dans [!DNL JupyterLab] l’utilisation [!DNL Git]

[!DNL Git] est un système de contrôle de version distribué permettant de suivre les modifications du code source au cours du développement logiciel. Git est préinstallé dans l&#39; [!DNL Data Science Workspace JupyterLab] environnement.

## Conditions préalables 

>[!NOTE]
>
> Le serveur Git que vous avez l&#39;intention d&#39;utiliser doit être accessible via Internet.

L&#39; [!DNL Data Science Workspace JupyterLab] environnement est hébergé et n&#39;est pas déployé dans votre pare-feu d&#39;entreprise. Par conséquent, le serveur Git auquel vous vous connectez doit être accessible à partir de l&#39;Internet public. Il peut s&#39;agir d&#39;un référentiel public ou privé sur [GitHub](https://github.com/) ou d&#39;une autre instance d&#39;un [!DNL Git] serveur que vous avez décidé de héberger vous-même.

## Se connecter [!DNL Git] à l&#39; [!DNL Data Science Workspace JupyterLab Notebooks] environnement

Début en lançant [!DNL Adobe Experience Platform] et en accédant à l&#39; [[ ! DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab) .

Dans [!DNL JupyterLab], sélectionnez **[!UICONTROL Fichier]** , puis passez la souris sur **[!UICONTROL Nouveau]**. Dans la liste déroulante qui s&#39;affiche, sélectionnez **[!UICONTROL Terminal]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

Ensuite, dans l&#39; *utilitaire Terminal* , accédez à votre espace de travail à l&#39;aide de la commande suivante : `cd my-workspace`.

![espace de travail cd](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Pour afficher une liste des commandes git disponibles, émettez la commande : `git -help` dans votre terminal.

Ensuite, cloner le référentiel que vous souhaitez utiliser à l&#39;aide de la `git clone` commande. Clonez votre projet à l’aide d’une `https://` URL plutôt que `ssh://`d’une autre.

**Exemple**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clone](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Pour effectuer des opérations d&#39;écriture (`git push` par exemple), les commandes de configuration suivantes doivent être exécutées pour chaque nouvelle session. Notez également que toute commande push invite à saisir un nom d’utilisateur et un mot de passe.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Étapes suivantes

Une fois le clonage de votre référentiel terminé, vous pouvez utiliser Git comme vous le feriez normalement sur votre ordinateur local pour collaborer avec d&#39;autres utilisateurs sur des ordinateurs portables. Pour plus d&#39;informations sur ce que vous pouvez faire dans [!DNL JupyterLab], consultez le [[ !DNL JupyterLab User guide]](./overview.md).
