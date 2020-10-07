---
keywords: Experience Platform;troubleshooting;Data Science Workspace;popular topics
solution: Experience Platform
title: Guide de dépannage de Data Science Workspace
topic: Troubleshooting
description: Ce document fournit des réponses aux questions fréquentes sur Adobe Experience Platform Data Science Workspace.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 42%

---


# [!DNL Data Science Workspace] guide de dépannage

Ce document répond aux questions les plus fréquentes sur Adobe Experience Platform [!DNL Data Science Workspace]. For questions and troubleshooting regarding [!DNL Platform] APIs in general, see the [Adobe Experience Platform API troubleshooting guide](../landing/troubleshooting.md).

## [!DNL JupyterLab] L&#39;environnement ne se charge pas dans [!DNL Google Chrome]

>[!IMPORTANT]
>
>Ce problème a été résolu, mais il peut toujours être présent dans le navigateur Google Chrome 80.x. Assurez-vous que votre navigateur Chrome est à jour.

Avec la version 80.x du [!DNL Google Chrome] navigateur, tous les cookies tiers sont bloqués par défaut. This policy can prevent [!DNL JupyterLab] from loading within Adobe Experience Platform.

Pour remédier à ce problème, procédez de la manière suivante :

In your [!DNL Chrome] browser, navigate to the top-right and select **Settings** (alternatively you can copy and paste &quot;chrome://settings/&quot; in the address bar). Faites ensuite défiler la page jusqu’en bas, puis cliquez sur la liste déroulante **Paramètres avancés**.

![paramètres avancés de Chrome](./images/faq/chrome-advanced.png)

La section **Confidentialité et sécurité** s’affiche. Cliquez ensuite sur **Paramètres des sites**, puis sur **Cookies et données du site**.

![paramètres avancés de Chrome](./images/faq/privacy-security.png)

![paramètres avancés de Chrome](./images/faq/cookies.png)

Enfin, faites basculer « Bloquer les cookies tiers » sur « Désactivé ».

![paramètres avancés de Chrome](./images/faq/toggle-off.png)

>[!NOTE]
>
>Alternatively, you could disable third-party cookies and add [*.]ds.adobe.net vers la liste autorisée.

Saisissez « chrome://flags/ » dans votre barre d’adresse. Recherchez et désactivez l’indicateur intitulé *« SameSite by default cookies »* en utilisant le menu déroulant sur la droite.

![désactiver l’indicateur samesite](./images/faq/samesite-flag.png)

Après l’étape 2, vous êtes invité à relancer votre navigateur. After you relaunch, [!DNL Jupyterlab] should be accessible.

## Why am I unable to access [!DNL JupyterLab] in Safari?

Safari désactive les cookies tiers par défaut dans Safari &lt; 12. Because your [!DNL Jupyter] virtual machine instance resides on a different domain than its parent frame, Adobe Experience Platform currently requires that third-party cookies be enabled. Activez les cookies tiers ou passez à un autre navigateur comme [!DNL Google Chrome].

Pour Safari 12, vous devez remplacer l’agent utilisateur par &quot;[!DNL Chrome]&quot; ou &quot;[!DNL Firefox]&quot;. Pour changer d&#39;agent utilisateur, début en ouvrant le menu *Safari* et en sélectionnant **Préférences**. La fenêtre Préférences s&#39;affiche.

![Préférences Safari](./images/faq/preferences.png)

Dans la fenêtre des préférences de Safari, sélectionnez **Avancé**. Cochez ensuite la case *Afficher le menu Développer dans la barre* de menus. Vous pouvez fermer la fenêtre des préférences une fois cette étape terminée.

![Safari avancé](./images/faq/advanced.png)

Ensuite, dans la barre de navigation supérieure, sélectionnez le menu **Développer** . Dans la liste déroulante **Développer** , passez la souris sur Agent **** utilisateur. Vous pouvez sélectionner la chaîne **[!DNL Chrome]** ou **[!DNL Firefox]** User Agent que vous souhaitez utiliser.

![Menu Développer](./images/faq/user-agent.png)

## Pourquoi un message « 403 Forbidden » apparaît-il lorsque j’essaie de charger ou de supprimer un fichier dans [!DNL JupyterLab]?

If your browser is enabled with advertisement blocking software such as [!DNL Ghostery] or [!DNL AdBlock] Plus, the domain &quot;\*.adobe.net&quot; must be allowed in each advertisement blocking software for [!DNL JupyterLab] to operate normally. This is because [!DNL JupyterLab] virtual machines run on a different domain than the [!DNL Experience Platform] domain.

## Why do some parts of my [!DNL Jupyter Notebook] look scrambled or do not render as code?

Cela peut se produire si la cellule en question est passée par erreur de « Code » à « Markdown ». Lorsqu’une cellule de code est sélectionnée, appuyez sur la combinaison de touches **ESC+M** pour modifier le type de la cellule sur Markdown. Vous pouvez modifier le type d’une cellule à l’aide de l’indicateur déroulant situé en haut du notebook pour la ou les cellules sélectionnées. Pour modifier un type de cellule en code, commencez par sélectionner la cellule donnée que vous souhaitez modifier. Cliquez ensuite sur la liste déroulante qui indique le type actuel de la cellule, puis sélectionnez « Code ».

![](./images/faq/code_type.png)

## How do I install custom [!DNL Python] libraries?

The [!DNL Python] kernel comes pre-installed with many popular machine learning libraries. Cependant, vous pouvez installer d’autres bibliothèques personnalisées en exécutant la commande suivante dans une cellule de code :

```shell
!pip install {LIBRARY_NAME}
```

For a complete list of pre-installed [!DNL Python] libraries, see the [appendix section of the JupyterLab User Guide](./jupyterlab/overview.md#supported-libraries).

## Puis-je installer des bibliothèques PySpark personnalisées ?

Malheureusement, vous ne pouvez pas installer de bibliothèques supplémentaires pour le noyau PySpark. Néanmoins, vous pouvez contacter votre représentant du service client Adobe et lui demander d’installer ces bibliothèques PySpark personnalisées pour vous.

Pour obtenir la liste des bibliothèques PySpark préinstallées, consultez la [section annexe du guide d’utilisation de JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Is it possible to configure [!DNL Spark] cluster resources for [!DNL JupyterLab] [!DNL Spark] or PySpark kernel?

Vous pouvez configurer des ressources en ajoutant le bloc suivant à la première cellule de votre notebook :

```python
%%configure -f 
{
    "numExecutors": 10,
    "executorMemory": "8G",
    "executorCores":4,
    "driverMemory":"2G",
    "driverCores":2,
    "conf": {
        "spark.cores.max": "40"
    }
}
```

For more information on [!DNL Spark] cluster resource configuration, including the complete list of configurable properties, see the [JupyterLab User Guide](./jupyterlab/overview.md#kernels).

## Pourquoi est-ce que je reçois une erreur lorsque je tente d&#39;exécuter certaines tâches pour des jeux de données plus volumineux ?

Si vous recevez une erreur pour une raison telle que `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` Cela signifie généralement que le pilote ou un exécuteur manque de mémoire. Pour plus d&#39;informations sur les limites de données et sur la façon d&#39;exécuter des tâches sur des jeux de données volumineux, consultez la documentation relative à l&#39;accès [aux](./jupyterlab/access-notebook-data.md) données des portables JupyterLab. En règle générale, cette erreur peut être résolue en changeant le `mode` de `interactive` à `batch`.