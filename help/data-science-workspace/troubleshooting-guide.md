---
keywords: Experience Platform;dépannage;Data Science Workspace;rubriques les plus consultées
solution: Experience Platform
title: Guide de dépannage de Data Science Workspace
topic-legacy: Troubleshooting
description: Ce document fournit des réponses aux questions fréquentes sur Adobe Experience Platform Data Science Workspace.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: c2c2b1684e2c2c3c76dc23ad1df720abd6c4356c
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 27%

---

# Guide de dépannage du [!DNL Data Science Workspace]

Ce document répond aux questions les plus fréquentes sur Adobe Experience Platform [!DNL Data Science Workspace]. Pour toute question ou dépannage concernant les API [!DNL Platform] en général, consultez le [guide de dépannage de l’API Adobe Experience Platform](../landing/troubleshooting.md).

## [!DNL JupyterLab] l’environnement ne se charge pas dans  [!DNL Google Chrome]

>[!IMPORTANT]
>
>Ce problème a été résolu, mais il peut toujours être présent dans le navigateur Google Chrome 80.x. Vérifiez que votre navigateur Chrome est à jour.

Avec la version 80.x du navigateur [!DNL Google Chrome], tous les cookies tiers sont bloqués par défaut. Cette stratégie peut empêcher le chargement de [!DNL JupyterLab] dans Adobe Experience Platform.

Pour remédier à ce problème, procédez de la manière suivante :

Dans votre navigateur [!DNL Chrome], accédez au coin supérieur droit et sélectionnez **Paramètres** (vous pouvez également copier et coller &quot;chrome://settings/&quot; dans la barre d’adresse). Faites ensuite défiler la page jusqu’en bas, puis cliquez sur la liste déroulante **Paramètres avancés**.

![paramètres avancés de Chrome](./images/faq/chrome-advanced.png)

La section **Confidentialité et sécurité** s’affiche. Cliquez ensuite sur **Paramètres des sites**, puis sur **Cookies et données du site**.

![paramètres avancés de Chrome](./images/faq/privacy-security.png)

![paramètres avancés de Chrome](./images/faq/cookies.png)

Enfin, faites basculer « Bloquer les cookies tiers » sur « Désactivé ».

![paramètres avancés de Chrome](./images/faq/toggle-off.png)

>[!NOTE]
>
>Vous pouvez également désactiver les cookies tiers et ajouter [*.]ds.adobe.net à la liste autorisée.

Saisissez « chrome://flags/ » dans votre barre d’adresse. Recherchez et désactivez l’indicateur intitulé *« SameSite by default cookies »* en utilisant le menu déroulant sur la droite.

![désactiver l’indicateur samesite](./images/faq/samesite-flag.png)

Après l’étape 2, vous êtes invité à relancer votre navigateur. Une fois que vous avez redémarré, [!DNL Jupyterlab] doit être accessible.

## Pourquoi ne puis-je pas accéder à [!DNL JupyterLab] dans Safari ?

Safari désactive les cookies tiers par défaut dans Safari &lt; 12. Étant donné que votre instance [!DNL Jupyter] de machine virtuelle réside sur un domaine différent de son cadre parent, Adobe Experience Platform nécessite actuellement l’activation des cookies tiers. Activez les cookies tiers ou passez à un autre navigateur comme [!DNL Google Chrome].

Pour Safari 12, vous devez changer votre Agent utilisateur en &#39;[!DNL Chrome]&#39; ou &#39;[!DNL Firefox]&#39;. Pour changer votre agent utilisateur, commencez par ouvrir le menu *Safari* et sélectionnez **Préférences**. La fenêtre Préférences s’affiche.

![Préférences Safari](./images/faq/preferences.png)

Dans la fenêtre des préférences de Safari, sélectionnez **Avancé**. Cochez ensuite la case *Afficher le menu Développer dans la barre de menus* . Une fois cette étape terminée, vous pouvez fermer la fenêtre des préférences.

![Safari avancé](./images/faq/advanced.png)

Ensuite, dans la barre de navigation supérieure, sélectionnez le menu **Développer** . Dans la liste déroulante **Développer**, passez la souris sur **Agent utilisateur**. Vous pouvez sélectionner la chaîne **[!DNL Chrome]** ou **[!DNL Firefox]** User Agent que vous souhaitez utiliser.

![Menu Développer](./images/faq/user-agent.png)

## Pourquoi un message « 403 Forbidden » apparaît-il lorsque j’essaie de charger ou de supprimer un fichier dans [!DNL JupyterLab]?

Si votre navigateur est activé avec un logiciel de blocage des publicités tel que [!DNL Ghostery] ou [!DNL AdBlock] Plus, le domaine &quot;\*.adobe.net&quot; doit être autorisé dans chaque logiciel de blocage des publicités pour que [!DNL JupyterLab] fonctionne normalement. En effet, les machines virtuelles [!DNL JupyterLab] s’exécutent sur un domaine différent du domaine [!DNL Experience Platform].

## Pourquoi certaines parties de ma [!DNL Jupyter Notebook] semblent-elles brouillées ou ne s’affichent-elles pas sous forme de code ?

Cela peut se produire si la cellule en question est passée par erreur de « Code » à « Markdown ». Lorsqu’une cellule de code est sélectionnée, appuyez sur la combinaison de touches **ESC+M** pour modifier le type de la cellule sur Markdown. Vous pouvez modifier le type d’une cellule à l’aide de l’indicateur déroulant situé en haut du notebook pour la ou les cellules sélectionnées. Pour modifier un type de cellule en code, commencez par sélectionner la cellule donnée que vous souhaitez modifier. Cliquez ensuite sur la liste déroulante qui indique le type actuel de la cellule, puis sélectionnez « Code ».

![](./images/faq/code_type.png)

## Comment installer des bibliothèques [!DNL Python] personnalisées ?

Le noyau [!DNL Python] est préinstallé avec de nombreuses bibliothèques d’apprentissage automatique populaires. Cependant, vous pouvez installer d’autres bibliothèques personnalisées en exécutant la commande suivante dans une cellule de code :

```shell
!pip install {LIBRARY_NAME}
```

Pour obtenir la liste complète des bibliothèques [!DNL Python] préinstallées, consultez la section [annexe du Guide de l’utilisateur de JupyterLab](./jupyterlab/overview.md#supported-libraries).

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

Pour plus d’informations sur la [!DNL Spark] configuration des ressources de cluster, y compris la liste complète des propriétés configurables, consultez le [Guide de l’utilisateur de JupyterLab](./jupyterlab/overview.md#kernels).

## Pourquoi est-ce que je reçois une erreur lorsque j’essaie d’exécuter certaines tâches pour des jeux de données plus volumineux ?

Si vous recevez une erreur pour une raison telle que `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` Cela signifie généralement que la mémoire du pilote ou de l’exécuteur est insuffisante. Pour plus d’informations sur les limites de données et sur l’exécution des tâches sur les jeux de données volumineux, reportez-vous à la documentation JupyterLab Notebooks [accès aux données](./jupyterlab/access-notebook-data.md) . En règle générale, cette erreur peut être résolue en remplaçant `mode` de `interactive` par `batch`.

En outre, lors de l’écriture de jeux de données Spark/PySpark volumineux, la mise en cache de vos données (`df.cache()`) avant d’exécuter le code d’écriture peut améliorer considérablement les performances.

<!-- remove this paragraph at a later date once the sdk is updated -->

Si vous rencontrez des problèmes lors de la lecture des données et que vous appliquez des transformations aux données, essayez de mettre en cache vos données avant les transformations. La mise en cache de vos données empêche plusieurs lectures sur le réseau. Commencez par lire les données. Ensuite, mettez en cache (`df.cache()`) les données. Enfin, effectuez vos transformations.

## Pourquoi mes notebooks Spark/PySpark prennent-ils autant de temps à lire et à écrire des données ?

Si vous effectuez des transformations sur des données, par exemple en utilisant `fit()`, les transformations peuvent s’exécuter plusieurs fois. Pour améliorer les performances, mettez en cache vos données à l’aide de `df.cache()` avant d’exécuter `fit()`. Cela permet de s’assurer que les transformations ne sont exécutées qu’une seule fois et d’empêcher plusieurs lectures sur le réseau.

**Ordre recommandé :** commencez par lire les données. Ensuite, effectuez des transformations suivies de la mise en cache (`df.cache()`) des données. Enfin, exécutez un `fit()`.

## Pourquoi mes notebooks Spark/PySpark ne fonctionnent-ils pas ?

Si vous recevez l’une des erreurs suivantes :

- Traitement abandonné en raison d’un échec de test... Peuvent uniquement compresser les RDD avec le même nombre d&#39;éléments dans chaque partition.
- Client RPC distant dissocié et autres erreurs de mémoire.
- Mauvaises performances lors de la lecture et de l’écriture de jeux de données.

Vérifiez que vous mettez en cache les données (`df.cache()`) avant d’écrire les données. Lors de l’exécution du code dans les notebooks, l’utilisation de `df.cache()` avant une action telle que `fit()` peut améliorer considérablement les performances du notebook. L’utilisation de `df.cache()` avant d’écrire un jeu de données garantit que les transformations ne sont exécutées qu’une seule fois au lieu de plusieurs fois.

## [!DNL Docker Hub] restrictions de limite dans Data Science Workspace

Depuis le 20 novembre 2020, les limites de taux pour l’utilisation anonyme et authentifiée gratuite de Docker Hub sont entrées en vigueur. Les utilisateurs anonymes et libres [!DNL Docker Hub] sont limités à 100 demandes d’extraction d’image de conteneur toutes les six heures. Si ces modifications vous affectent, vous recevrez ce message d’erreur : `ERROR: toomanyrequests: Too Many Requests.` ou `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

Actuellement, cette limite n’affecte votre entreprise que si vous tentez de créer 100 notebooks vers les recettes au cours de la période de six heures ou si vous utilisez des notebooks basés sur Spark dans Data Science Workspace, qui sont fréquemment mis à l’échelle. Cependant, cela est peu probable, car le cluster s’exécute pendant deux heures principal avant de se déconnecter. Cela réduit le nombre d’appels requis lorsque la grappe est principale. Si vous recevez l’une des erreurs ci-dessus, vous devrez attendre que votre limite [!DNL Docker] soit réinitialisée.

Pour plus d’informations sur les limites de taux [!DNL Docker Hub], consultez la [documentation DockerHub](https://www.docker.com/increase-rate-limits). Une solution à ce problème est en cours de traitement et attendue dans une version ultérieure.
