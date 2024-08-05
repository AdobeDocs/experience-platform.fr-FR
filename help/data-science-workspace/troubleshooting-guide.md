---
keywords: Experience Platform;dépannage;Espace de travail de science des données;rubriques populaires
solution: Experience Platform
title: Guide de dépannage de l’espace de travail de science des données
description: Ce document fournit des réponses aux questions fréquentes sur l’espace de travail de science des données d’Adobe Experience Platform.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 98%

---

# Guide de dépannage de [!DNL Data Science Workspace]

>[!NOTE]
>
>Data Science Workspace ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs à Data Science Workspace.

Ce document répond aux questions les plus fréquentes sur [!DNL Data Science Workspace] d’Adobe Experience Platform. Pour toute question ou tout dépannage concernant les API [!DNL Platform] en général, reportez-vous au [guide de dépannage des API Adobe Experience Platform](../landing/troubleshooting.md).

## La requête du notebook JupyterLab est bloquée au statut d’exécution.

Un notebook JupyterLab peut indiquer qu’une cellule est en état d’exécution, indéfiniment, dans certaines conditions de mémoire insuffisante. Par exemple, lors de l’interrogation d’un jeu de données volumineux ou de l’exécution de plusieurs requêtes ultérieures, le notebook JupyterLab peut manquer de mémoire disponible pour stocker l’objet Dataframe obtenu. Des indicateurs peuvent apparaître dans cette situation. Tout d’abord, le noyau entre dans l’état inactif même si la cellule s’affiche comme étant en cours d’exécution tel qu’indiqué par l’icône [`*`] à côté de la cellule. En outre, la barre inférieure indique la quantité de RAM utilisée/disponible.

![Ram disponible](./images/jupyterlab/user-guide/allocate-ram.png)

Pendant la lecture des données, la mémoire peut augmenter jusqu’à atteindre la quantité maximale de mémoire allouée. La mémoire est libérée dès que la mémoire maximale est atteinte et que le noyau redémarre. Cela signifie que la mémoire utilisée dans ce scénario peut s’afficher comme étant très faible en raison du redémarrage du noyau, alors qu’un peu avant le redémarrage, la mémoire aurait été très proche de la RAM allouée maximale.

Pour résoudre ce problème, sélectionnez l’icône d’engrenage en haut à droite de JupyterLab et faites glisser le curseur vers la droite, puis sélectionnez **[!UICONTROL Mettre à jour les configurations]** pour allouer plus de RAM. En outre, si vous exécutez plusieurs requêtes et que la valeur de la RAM est proche de la quantité maximale allouée, à moins que vous n’ayez besoin des résultats de requêtes précédentes, redémarrez le noyau pour réinitialiser la quantité de RAM disponible. Vous disposez ainsi de la quantité maximale de RAM disponible pour la requête actuelle.

![allouer plus de ram](./images/jupyterlab/user-guide/notebook-gpu-config.png)

Dans le cas où vous allouez la quantité maximale de mémoire (RAM) et que vous rencontrez toujours ce problème, vous pouvez modifier votre requête pour qu’elle fonctionne sur une taille de jeu de données plus réduite en réduisant les colonnes ou la plage de données. Pour utiliser la quantité intégrale des données, il est recommandé d’utiliser un notebook Spark.

## L’environnement [!DNL JupyterLab] ne se charge pas dans [!DNL Google Chrome].

>[!IMPORTANT]
>
>Ce problème a été résolu, mais il peut toujours être présent dans le navigateur Google Chrome 80.x. Vérifiez que votre navigateur Chrome est à jour.

Avec le navigateur [!DNL Google Chrome] version 80.x, tous les cookies tiers sont bloqués par défaut. Cette politique peut empêcher le chargement de [!DNL JupyterLab] dans Adobe Experience Platform.

Pour remédier à ce problème, procédez de la manière suivante :

Dans votre navigateur [!DNL Chrome], allez dans le coin supérieur droit, puis sélectionnez **Paramètres** (vous pouvez également copier et coller « chrome://settings/ » dans la barre d’adresse). Faites ensuite défiler la page jusqu’en bas, puis cliquez sur la liste déroulante **Paramètres avancés**.

![paramètres avancés de Chrome](./images/faq/chrome-advanced.png)

La section **Confidentialité et sécurité** s’affiche. Cliquez ensuite sur **Paramètres des sites**, puis sur **Cookies et données du site**.

![paramètres avancés de Chrome](./images/faq/privacy-security.png)

![paramètres avancés de Chrome](./images/faq/cookies.png)

Enfin, faites basculer « Bloquer les cookies tiers » sur « Désactivé ».

![paramètres avancés de Chrome](./images/faq/toggle-off.png)

>[!NOTE]
>
>Vous pouvez également désactiver les cookies tiers et les ajouter sur [*.]ds.adobe.net sur la liste autorisée.

Saisissez « chrome://flags/ » dans votre barre d’adresse. Recherchez et désactivez l’indicateur intitulé *« SameSite by default cookies »* en utilisant le menu déroulant sur la droite.

![désactiver l’indicateur samesite](./images/faq/samesite-flag.png)

Après l’étape 2, vous êtes invité à relancer votre navigateur. Après avoir redémarré, vous devriez pouvoir accéder à [!DNL Jupyterlab].

## Pourquoi ne puis-je pas accéder à [!DNL JupyterLab] dans Safari ?

Safari désactive les cookies tiers par défaut dans Safari &lt; 12. Comme votre instance de machine virtuelle [!DNL Jupyter] se trouve sur un domaine différent de son cadre parent, Adobe Experience Platform nécessite actuellement l’activation des cookies tiers. Activez les cookies tiers ou passez à un autre navigateur comme [!DNL Google Chrome].

Pour Safari 12, vous devez changer votre Agent utilisateur en &#39;[!DNL Chrome]&#39; ou &#39;[!DNL Firefox]&#39;. Pour changer votre Agent utilisateur, commencez par ouvrir le menu *Safari* et sélectionnez **Préférences**. La fenêtre de préférences suivante s’affiche.

![Préférences Safari](./images/faq/preferences.png)

Dans la fenêtre des préférences de Safari, sélectionnez **Avancé**. Cochez ensuite la case *Afficher le menu Développer dans la barre de menus*. Une fois cette étape terminée, vous pouvez fermer la fenêtre des préférences.

![Safari avancé](./images/faq/advanced.png)

Ensuite, dans la barre de navigation supérieure, sélectionnez le menu **Développer**. Dans la liste déroulante **Développer**, pointez sur **Agent utilisateur**. Vous pouvez sélectionner la chaîne de l’agent utilisateur **[!DNL Chrome]** ou **[!DNL Firefox]** que vous souhaitez utiliser.

![Menu Développer](./images/faq/user-agent.png)

## Pourquoi un message « 403 Forbidden » apparaît-il lorsque j’essaie de charger ou de supprimer un fichier dans [!DNL JupyterLab] ?

Si vous avez activé un bloqueur de publicités sur votre navigateur comme [!DNL Ghostery] ou [!DNL AdBlock] Plus, vous devrez ajouter le domaine « \*.adobe.net » à la liste blanche de chaque bloqueur de publicités pour permettre à [!DNL JupyterLab] de fonctionner normalement. Cela est dû au fait que les machines virtuelles [!DNL JupyterLab] s’exécutent sur un domaine différent du domaine [!DNL Experience Platform].

## Pourquoi certaines parties de mon [!DNL Jupyter Notebook] ont-elles l’air brouillées ou ne s’affichent pas sous forme de code ?

Cela peut se produire si la cellule en question est passée par erreur de « Code » à « Markdown ». Lorsqu’une cellule de code est sélectionnée, appuyez sur la combinaison de touches **ESC+M** pour modifier le type de la cellule sur Markdown. Vous pouvez modifier le type d’une cellule à l’aide de l’indicateur déroulant situé en haut du notebook pour la ou les cellules sélectionnées. Pour modifier un type de cellule en code, commencez par sélectionner la cellule donnée que vous souhaitez modifier. Cliquez ensuite sur la liste déroulante qui indique le type actuel de la cellule, puis sélectionnez « Code ».

![](./images/faq/code_type.png)

## Comment installer des bibliothèques [!DNL Python] personnalisées ?

Le noyau [!DNL Python] est préinstallé sur de nombreuses bibliothèques de machine learning populaires. Cependant, vous pouvez installer d’autres bibliothèques personnalisées en exécutant la commande suivante dans une cellule de code :

```shell
!pip install {LIBRARY_NAME}
```

Pour obtenir la liste complète des bibliothèques [!DNL Python] préinstallées, consultez la [section annexe du guide d’utilisation de JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Puis-je installer des bibliothèques PySpark personnalisées ?

Malheureusement, vous ne pouvez pas installer de bibliothèques supplémentaires pour le noyau PySpark. Néanmoins, vous pouvez contacter votre représentant du service client Adobe et lui demander d’installer ces bibliothèques PySpark personnalisées pour vous.

Pour obtenir la liste des bibliothèques PySpark préinstallées, consultez la [section annexe du guide d’utilisation de JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Est-il possible de configurer des ressources de cluster [!DNL Spark] pour un noyau [!DNL JupyterLab] [!DNL Spark] ou PySpark ?

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

Pour plus d’informations sur la configuration des ressources de cluster [!DNL Spark], notamment la liste complète des propriétés configurables, consultez le [guide d’utilisation de JupyterLab](./jupyterlab/overview.md#kernels).

## Pourquoi est-ce que je reçois une erreur lorsque j’essaie d’exécuter certaines tâches pour des jeux de données plus volumineux ?

Si vous recevez une erreur pour une raison telle que `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.`, cela signifie généralement que la mémoire du pilote ou de l’exécuteur est insuffisante. Consultez la documentation sur l’[accès aux données](./jupyterlab/access-notebook-data.md) des notebooks JupyterLab pour plus d’informations sur les limites de données et sur l’exécution de tâches sur des jeux de données volumineux. En règle générale, cette erreur peut être résolue en modifiant `mode` de `interactive` à `batch`.

En outre, lors de l’écriture de jeux de données Spark/PySpark volumineux, la mise en cache de vos données (`df.cache()`) avant d’exécuter le code d’écriture peut améliorer considérablement les performances.

<!-- remove this paragraph at a later date once the sdk is updated -->

Si vous rencontrez des problèmes lors de la lecture des données et que vous appliquez des transformations aux données, essayez de mettre en cache vos données avant de les transformer. La mise en cache de vos données empêche plusieurs lectures sur le réseau. Commencez par lire les données. Ensuite, mettez en cache (`df.cache()`) les données. Enfin, effectuez vos transformations.

## Pourquoi mes notebooks Spark/PySpark mettent-ils autant de temps à lire et à écrire des données ?

Si vous effectuez des transformations sur des données, par exemple en utilisant `fit()`, ces transformations peuvent s’exécuter plusieurs fois. Pour améliorer les performances, mettez en cache vos données à l’aide de `df.cache()` avant d’exécuter l’action `fit()`. Cela permet de s’assurer que les transformations ne sont exécutées qu’une seule fois et d’empêcher plusieurs lectures sur le réseau.

**Ordre recommandé :** Commencez par lire les données. Ensuite, effectuez vos transformations puis mettez en cache (`df.cache()`) les données. Enfin, effectuez une action `fit()`.

## Pourquoi mes notebooks Spark/PySpark ne fonctionnent-ils pas ?

Si vous recevez l’une des erreurs suivantes :

- Tâche abandonnée en raison d’un échec de test ... Peut uniquement compresser les RDD avec le même nombre d’éléments dans chaque partition.
- Client RPC distant dissocié et autres erreurs de mémoire.
- Mauvaises performances lors de la lecture et de l’écriture de jeux de données.

Vérifiez que vous mettez en cache les données (`df.cache()`) avant de les écrire. Lors de l’exécution de code dans des notebooks, utiliser `df.cache()` avant une action telle que `fit()` peut améliorer considérablement les performances des notebooks. Utiliser `df.cache()` avant d’écrire un jeu de données garantit que les transformations ne sont exécutées qu’une seule fois au lieu de plusieurs fois.

## Restrictions de limite [!DNL Docker Hub] dans l’Espace de travail de science des données

Depuis le 20 novembre 2020, les limites de l’utilisation authentifiée anonyme et gratuite de Docker Hub sont entrées en vigueur. Les utilisateurs de [!DNL Docker Hub] anonyme et gratuit sont limités à 100 demandes d’extraction d’image de conteneur toutes les six heures. Si ces modifications vous affectent, vous recevrez ce message d’erreur : `ERROR: toomanyrequests: Too Many Requests.` ou `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

Actuellement, cette limite n’affecte votre entreprise que si vous tentez de créer 100 notebooks dans les recettes au cours d’une période de six heures ou si vous utilisez des notebooks basés sur Spark dans l’espace de travail de science des données, qui sont fréquemment mis à l’échelle. Toutefois, cela est peu probable, car le cluster sur lequel ils fonctionnent reste actif pendant deux heures avant de devenir inactif. Cela réduit le nombre d’extractions requises lorsque le cluster est actif. Si vous recevez l’une des erreurs ci-dessus, vous devrez attendre que votre limite [!DNL Docker] se réinitialise.

Pour plus d’informations sur les limites [!DNL Docker Hub], consultez la [Documentation DockerHub](https://www.docker.com/increase-rate-limits). Une solution à ce problème est en cours de traitement et attendue dans une version ultérieure.
