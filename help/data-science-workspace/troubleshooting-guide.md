---
keywords: Experience Platform ; dépannage ; Espace de travail des données ; rubriques populaires
solution: Experience Platform
title: Guide de dépannage de Data Science Workspace
topic-legacy: Troubleshooting
description: Ce document fournit des réponses aux questions fréquentes sur Adobe Experience Platform Data Science Workspace.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 33%

---

# [!DNL Data Science Workspace] guide de dépannage

Ce document répond aux questions les plus fréquentes sur Adobe Experience Platform [!DNL Data Science Workspace]. Pour toute question et dépannage concernant les API [!DNL Platform] en général, consultez le [Guide de dépannage de l&#39;API Adobe Experience Platform](../landing/troubleshooting.md).

## [!DNL JupyterLab] L&#39;environnement ne se charge pas dans  [!DNL Google Chrome]

>[!IMPORTANT]
>
>Ce problème a été résolu, mais il peut toujours être présent dans le navigateur Google Chrome 80.x. Assurez-vous que votre navigateur Chrome est à jour.

Avec la version 80.x du navigateur [!DNL Google Chrome], tous les cookies tiers sont bloqués par défaut. Cette stratégie peut empêcher le chargement de [!DNL JupyterLab] dans Adobe Experience Platform.

Pour remédier à ce problème, procédez de la manière suivante :

Dans votre navigateur [!DNL Chrome], accédez à l&#39;angle supérieur droit et sélectionnez **Paramètres** (vous pouvez également copier et coller &quot;chrome://settings/&quot; dans la barre d&#39;adresse). Faites ensuite défiler la page jusqu’en bas, puis cliquez sur la liste déroulante **Paramètres avancés**.

![paramètres avancés de Chrome](./images/faq/chrome-advanced.png)

La section **Confidentialité et sécurité** s’affiche. Cliquez ensuite sur **Paramètres des sites**, puis sur **Cookies et données du site**.

![paramètres avancés de Chrome](./images/faq/privacy-security.png)

![paramètres avancés de Chrome](./images/faq/cookies.png)

Enfin, faites basculer « Bloquer les cookies tiers » sur « Désactivé ».

![paramètres avancés de Chrome](./images/faq/toggle-off.png)

>[!NOTE]
>
>Vous pouvez également désactiver les cookies tiers et ajouter [*.]ds.adobe.net vers la liste autorisée.

Saisissez « chrome://flags/ » dans votre barre d’adresse. Recherchez et désactivez l’indicateur intitulé *« SameSite by default cookies »* en utilisant le menu déroulant sur la droite.

![désactiver l’indicateur samesite](./images/faq/samesite-flag.png)

Après l’étape 2, vous êtes invité à relancer votre navigateur. Une fois relancé, [!DNL Jupyterlab] doit être accessible.

## Pourquoi est-ce que je ne peux pas accéder à [!DNL JupyterLab] dans Safari ?

Safari désactive les cookies tiers par défaut dans Safari &lt; 12. Puisque votre instance d&#39;ordinateur virtuel [!DNL Jupyter] réside sur un domaine différent de celui de son cadre parent, Adobe Experience Platform exige actuellement que les cookies tiers soient activés. Activez les cookies tiers ou passez à un autre navigateur comme [!DNL Google Chrome].

Pour Safari 12, vous devez changer votre User Agent en &quot;[!DNL Chrome]&quot; ou &quot;[!DNL Firefox]&quot;. Pour changer d&#39;agent utilisateur, début en ouvrant le menu *Safari* et en sélectionnant **Préférences**. La fenêtre Préférences s&#39;affiche.

![Préférences Safari](./images/faq/preferences.png)

Dans la fenêtre des préférences de Safari, sélectionnez **Avancé**. Cochez ensuite la case *Afficher le menu Développer dans la barre de menus*. Vous pouvez fermer la fenêtre des préférences une fois cette étape terminée.

![Safari avancé](./images/faq/advanced.png)

Ensuite, dans la barre de navigation supérieure, sélectionnez le menu **Développer**. Dans la liste déroulante **Développer**, passez la souris sur **User Agent**. Vous pouvez sélectionner la chaîne **[!DNL Chrome]** ou **[!DNL Firefox]** User Agent que vous souhaitez utiliser.

![Menu Développer](./images/faq/user-agent.png)

## Pourquoi un message « 403 Forbidden » apparaît-il lorsque j’essaie de charger ou de supprimer un fichier dans [!DNL JupyterLab]?

Si votre navigateur est activé avec un logiciel de blocage des publicités tel que [!DNL Ghostery] ou [!DNL AdBlock] Plus, le domaine &quot;\*.adobe.net&quot; doit être autorisé dans chaque logiciel de blocage des publicités pour que [!DNL JupyterLab] fonctionne normalement. En effet, les machines virtuelles [!DNL JupyterLab] s&#39;exécutent sur un domaine différent de celui de [!DNL Experience Platform].

## Pourquoi certaines parties de mon [!DNL Jupyter Notebook] semblent-elles brouillées ou ne s&#39;affichent pas sous forme de code ?

Cela peut se produire si la cellule en question est passée par erreur de « Code » à « Markdown ». Lorsqu’une cellule de code est sélectionnée, appuyez sur la combinaison de touches **ESC+M** pour modifier le type de la cellule sur Markdown. Vous pouvez modifier le type d’une cellule à l’aide de l’indicateur déroulant situé en haut du notebook pour la ou les cellules sélectionnées. Pour modifier un type de cellule en code, commencez par sélectionner la cellule donnée que vous souhaitez modifier. Cliquez ensuite sur la liste déroulante qui indique le type actuel de la cellule, puis sélectionnez « Code ».

![](./images/faq/code_type.png)

## Comment installer des bibliothèques [!DNL Python] personnalisées ?

Le noyau [!DNL Python] est préinstallé avec de nombreuses bibliothèques d&#39;apprentissage automatique populaires. Cependant, vous pouvez installer d’autres bibliothèques personnalisées en exécutant la commande suivante dans une cellule de code :

```shell
!pip install {LIBRARY_NAME}
```

Pour une liste complète des bibliothèques [!DNL Python] préinstallées, consultez la section [annexe du Guide de l&#39;utilisateur de JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Puis-je installer des bibliothèques PySpark personnalisées ?

Malheureusement, vous ne pouvez pas installer de bibliothèques supplémentaires pour le noyau PySpark. Néanmoins, vous pouvez contacter votre représentant du service client Adobe et lui demander d’installer ces bibliothèques PySpark personnalisées pour vous.

Pour obtenir la liste des bibliothèques PySpark préinstallées, consultez la [section annexe du guide d’utilisation de JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Est-il possible de configurer des ressources de cluster [!DNL Spark] pour [!DNL JupyterLab] [!DNL Spark] ou le noyau PySpark ?

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

Pour plus d&#39;informations sur la configuration des ressources de cluster [!DNL Spark], y compris la liste complète des propriétés configurables, consultez le [Guide de l&#39;utilisateur de JupyterLab](./jupyterlab/overview.md#kernels).

## Pourquoi est-ce que je reçois une erreur lorsque je tente d&#39;exécuter certaines tâches pour des jeux de données plus volumineux ?

Si vous recevez une erreur pour une raison telle que `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.`, cela signifie généralement que le pilote ou un exécuteur manque de mémoire. Pour plus d&#39;informations sur les limites de données et sur la façon d&#39;exécuter des tâches sur des jeux de données volumineux, consultez la documentation sur l&#39;accès aux données de JupyterLab [Notebooks data access](./jupyterlab/access-notebook-data.md). En règle générale, cette erreur peut être résolue en remplaçant `mode` de `interactive` par `batch`.

## [!DNL Docker Hub] restriction des limites dans Data Science Workspace

Depuis le 20 novembre 2020, les limites de taux pour l&#39;utilisation anonyme et authentifiée gratuite de Docker Hub sont entrées en vigueur. Les utilisateurs anonymes et Gratuit [!DNL Docker Hub] sont limités à 100 demandes d’extraction d’image par conteneur toutes les six heures. Si ces modifications vous concernent, vous recevrez ce message d’erreur : `ERROR: toomanyrequests: Too Many Requests.` ou `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

Actuellement, cette limite n&#39;affecte votre entreprise que si vous tentez de créer 100 blocs-notes vers Recettes dans les six heures ou si vous utilisez des blocs-notes basés sur Spark dans Data Science Workspace qui évoluent fréquemment vers le haut ou vers le bas. Cependant, cela est peu probable, puisque le cluster s&#39;exécute sur reste principal pendant deux heures avant de se déconnecter. Cela réduit le nombre d’extractions requises lorsque la grappe est principale. Si vous recevez l&#39;une des erreurs ci-dessus, vous devrez attendre que votre limite [!DNL Docker] soit réinitialisée.

Pour plus d&#39;informations sur les limites de taux [!DNL Docker Hub], consultez la [documentation DockerHub](https://www.docker.com/increase-rate-limits). Une solution à ce problème est en cours d’élaboration et attendue dans une version ultérieure.
