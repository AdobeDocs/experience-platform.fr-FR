---
keywords: Experience Platform;dépannage;Data Science Workspace;rubriques les plus consultées
solution: Experience Platform
title: Guide de dépannage de Data Science Workspace
description: Ce document fournit des réponses aux questions fréquentes sur Adobe Experience Platform Data Science Workspace.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 19%

---

# Guide de dépannage du [!DNL Data Science Workspace]

Ce document répond aux questions les plus fréquentes sur Adobe Experience Platform [!DNL Data Science Workspace]. Pour toute question ou dépannage concernant [!DNL Platform] Les API en général, voir [Guide de dépannage des API Adobe Experience Platform](../landing/troubleshooting.md).

## L’état de la requête du notebook JupyterLab est bloqué à l’état d’exécution

Un notebook JupyterLab peut indiquer qu’une cellule est en état d’exécution, indéfiniment, dans certaines conditions de mémoire insuffisante. Par exemple, lors de l’interrogation d’un jeu de données volumineux ou de l’exécution de plusieurs requêtes ultérieures, le notebook JupyterLab peut manquer de mémoire disponible pour stocker l’objet de cadre de données obtenu. Il y a quelques indicateurs que l&#39;on peut voir dans cette situation. Tout d’abord, le noyau entre dans l’état inactif même si la cellule s’affiche comme étant en cours d’exécution comme indiqué par la fonction [`*`] en regard de la cellule. En outre, la barre inférieure indique la quantité de RAM utilisée/disponible.

![Rail disponible](./images/jupyterlab/user-guide/allocate-ram.png)

Pendant la lecture des données, la mémoire peut augmenter jusqu’à atteindre la quantité maximale de mémoire allouée. La mémoire est libérée dès que la mémoire maximale est atteinte et que le noyau redémarre. Cela signifie que la mémoire utilisée dans ce scénario peut s’afficher très basse en raison du redémarrage du noyau, alors qu’un peu avant le redémarrage, la mémoire aurait été très proche de la RAM allouée maximale.

Pour résoudre ce problème, sélectionnez l’icône d’engrenage en haut à droite de JupyterLab et faites glisser le curseur vers la droite, puis sélectionnez **[!UICONTROL Mise à jour des configurations]** pour allouer plus de RAM. En outre, si vous exécutez plusieurs requêtes et que la valeur de la RAM est proche de la quantité maximale allouée, à moins que vous n’ayez besoin des résultats de requêtes précédentes, redémarrez le noyau pour réinitialiser la quantité de RAM disponible. Vous disposez ainsi de la quantité maximale de RAM disponible pour la requête actuelle.

![allouer plus de ram](./images/jupyterlab/user-guide/notebook-gpu-config.png)

Dans le cas où vous allouez la quantité maximale de mémoire (RAM) et que vous rencontrez toujours ce problème, vous pouvez modifier votre requête pour qu’elle fonctionne sur une taille de jeu de données plus réduite en réduisant les colonnes ou la plage de données. Pour utiliser toute la quantité de données, il est recommandé d’utiliser un notebook Spark.

## [!DNL JupyterLab] l’environnement ne se charge pas dans [!DNL Google Chrome]

>[!IMPORTANT]
>
>Ce problème a été résolu, mais il peut toujours être présent dans le navigateur Google Chrome 80.x. Vérifiez que votre navigateur Chrome est à jour.

Avec le [!DNL Google Chrome] version 80.x du navigateur, tous les cookies tiers sont bloqués par défaut. Cette stratégie peut empêcher [!DNL JupyterLab] à partir du chargement dans Adobe Experience Platform.

Pour remédier à ce problème, procédez de la manière suivante :

Dans votre [!DNL Chrome] , accédez au coin supérieur droit et sélectionnez **Paramètres** (vous pouvez également copier et coller &quot;chrome://settings/&quot; dans la barre d’adresse). Faites ensuite défiler la page jusqu’en bas, puis cliquez sur la liste déroulante **Paramètres avancés**.

![paramètres avancés de Chrome](./images/faq/chrome-advanced.png)

La section **Confidentialité et sécurité** s’affiche. Cliquez ensuite sur **Paramètres des sites**, puis sur **Cookies et données du site**.

![paramètres avancés de Chrome](./images/faq/privacy-security.png)

![paramètres avancés de Chrome](./images/faq/cookies.png)

Enfin, faites basculer &quot;Bloquer les cookies tiers&quot; sur &quot;Désactivé&quot;.

![paramètres avancés de Chrome](./images/faq/toggle-off.png)

>[!NOTE]
>
>Vous pouvez également désactiver les cookies tiers et ajouter des [*.]ds.adobe.net à la liste autorisée.

Accédez à &quot;chrome://flags/&quot; dans votre barre d’adresse. Recherchez et désactivez l’indicateur intitulé *&quot;Cookies samesite par défaut&quot;* en utilisant le menu déroulant sur la droite.

![désactiver l’indicateur samesite](./images/faq/samesite-flag.png)

Après l’étape 2, vous êtes invité à relancer votre navigateur. Après avoir redémarré, [!DNL Jupyterlab] doit être accessible.

## Pourquoi ne puis-je pas accéder à [!DNL JupyterLab] dans Safari ?

Safari désactive les cookies tiers par défaut dans Safari &lt; 12. Parce que votre [!DNL Jupyter] l’instance de machine virtuelle réside sur un domaine différent de son cadre parent, Adobe Experience Platform requiert actuellement l’activation des cookies tiers. Activez les cookies tiers ou passez à un autre navigateur comme [!DNL Google Chrome].

Pour Safari 12, vous devez changer votre Agent utilisateur en &#39;[!DNL Chrome]&#39; ou &#39;[!DNL Firefox]&#39;. Pour changer votre agent utilisateur, commencez par ouvrir la *Safari* et sélectionnez **Préférences**. La fenêtre Préférences s’affiche.

![Préférences Safari](./images/faq/preferences.png)

Dans la fenêtre des préférences de Safari, sélectionnez **Avancé**. Cochez ensuite la case *Afficher le menu Développer dans la barre de menus* de la boîte. Une fois cette étape terminée, vous pouvez fermer la fenêtre des préférences.

![Safari avancé](./images/faq/advanced.png)

Ensuite, dans la barre de navigation supérieure, sélectionnez l’option **Développer** . Depuis dans **Développer** déroulant, survolez **Agent utilisateur**. Vous pouvez sélectionner la variable **[!DNL Chrome]** ou **[!DNL Firefox]** Chaîne de l’agent utilisateur que vous souhaitez utiliser.

![Menu Développer](./images/faq/user-agent.png)

## Pourquoi un message « 403 Forbidden » apparaît-il lorsque j’essaie de charger ou de supprimer un fichier dans [!DNL JupyterLab]?

Si votre navigateur est activé avec un logiciel de blocage des publicités tel que [!DNL Ghostery] ou [!DNL AdBlock] De plus, le domaine &quot;\*.adobe.net&quot; doit être autorisé dans chaque logiciel de blocage des publicités pour [!DNL JupyterLab] pour fonctionner normalement. Ceci est dû au fait que [!DNL JupyterLab] les machines virtuelles s’exécutent sur un domaine différent de celui du [!DNL Experience Platform] domaine.

## Pourquoi faire certaines parties de mes [!DNL Jupyter Notebook] avez-vous l’air brouillé ou n’effectuez pas le rendu sous forme de code ?

Cela peut se produire si la cellule en question est passée par erreur de « Code » à « Markdown ». Lorsqu’une cellule de code est sélectionnée, appuyez sur la combinaison de touches **ESC+M** pour modifier le type de la cellule sur Markdown. Vous pouvez modifier le type d’une cellule à l’aide de l’indicateur déroulant situé en haut du notebook pour la ou les cellules sélectionnées. Pour modifier un type de cellule en code, commencez par sélectionner la cellule donnée que vous souhaitez modifier. Cliquez ensuite sur la liste déroulante qui indique le type actuel de la cellule, puis sélectionnez « Code ».

![](./images/faq/code_type.png)

## Comment installer des [!DNL Python] bibliothèques ?

Le [!DNL Python] Le noyau est préinstallé avec de nombreuses bibliothèques d’apprentissage automatique populaires. Cependant, vous pouvez installer d’autres bibliothèques personnalisées en exécutant la commande suivante dans une cellule de code :

```shell
!pip install {LIBRARY_NAME}
```

Pour obtenir la liste complète des [!DNL Python] bibliothèques, voir [section de l’annexe du guide de l’utilisateur de JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Puis-je installer des bibliothèques PySpark personnalisées ?

Malheureusement, vous ne pouvez pas installer de bibliothèques supplémentaires pour le noyau PySpark. Néanmoins, vous pouvez contacter votre représentant du service client Adobe et lui demander d’installer ces bibliothèques PySpark personnalisées pour vous.

Pour obtenir la liste des bibliothèques PySpark préinstallées, consultez la [section annexe du guide d’utilisation de JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Est-il possible de configurer [!DNL Spark] ressources de cluster pour [!DNL JupyterLab] [!DNL Spark] ou noyau PySpark ?

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

Pour plus d’informations sur [!DNL Spark] la configuration des ressources du cluster, y compris la liste complète des propriétés configurables, voir la section [Guide de l’utilisateur de JupyterLab](./jupyterlab/overview.md#kernels).

## Pourquoi est-ce que je reçois une erreur lorsque j’essaie d’exécuter certaines tâches pour des jeux de données plus volumineux ?

Si vous recevez une erreur pour une raison telle que `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` Cela signifie généralement que la mémoire du pilote ou de l’exécuteur est insuffisante. Voir les notebooks JupyterLab [accès aux données](./jupyterlab/access-notebook-data.md) documentation pour plus d’informations sur les limites de données et sur l’exécution de tâches sur des jeux de données volumineux. En règle générale, cette erreur peut être résolue en modifiant la variable `mode` de `interactive` to `batch`.

En outre, lors de l’écriture de jeux de données Spark/PySpark volumineux, la mise en cache de vos données (`df.cache()`) avant d’exécuter le code d’écriture peut améliorer considérablement les performances.

<!-- remove this paragraph at a later date once the sdk is updated -->

Si vous rencontrez des problèmes lors de la lecture des données et que vous appliquez des transformations aux données, essayez de mettre en cache vos données avant les transformations. La mise en cache de vos données empêche plusieurs lectures sur le réseau. Commencez par lire les données. Ensuite, mettez en cache (`df.cache()`) les données. Enfin, effectuez vos transformations.

## Pourquoi mes notebooks Spark/PySpark prennent-ils autant de temps à lire et à écrire des données ?

Si vous effectuez des transformations sur des données, par exemple en utilisant `fit()`, les transformations peuvent s’exécuter plusieurs fois. Pour améliorer les performances, mettez en cache vos données à l’aide de `df.cache()` avant d’exécuter la fonction `fit()`. Cela permet de s’assurer que les transformations ne sont exécutées qu’une seule fois et d’empêcher plusieurs lectures sur le réseau.

**Ordre recommandé :** Commencez par lire les données. Ensuite, effectuez des transformations suivies de la mise en cache (`df.cache()`) les données. Enfin, effectuez une `fit()`.

## Pourquoi mes notebooks Spark/PySpark ne fonctionnent-ils pas ?

Si vous recevez l’une des erreurs suivantes :

- Traitement abandonné en raison d’un échec de test... Peuvent uniquement compresser les RDD avec le même nombre d&#39;éléments dans chaque partition.
- Client RPC distant dissocié et autres erreurs de mémoire.
- Mauvaises performances lors de la lecture et de l’écriture de jeux de données.

Vérifiez que vous mettez en cache les données (`df.cache()`) avant d’écrire les données. Lors de l’exécution de code dans des notebooks, à l’aide de `df.cache()` avant une action telle que `fit()` peut améliorer considérablement les performances des notebooks. Utilisation `df.cache()` avant d’écrire un jeu de données, vous avez la garantie que les transformations ne sont exécutées qu’une seule fois au lieu de plusieurs fois.

## [!DNL Docker Hub] restrictions de limite dans Data Science Workspace

Depuis le 20 novembre 2020, les limites de taux pour l’utilisation anonyme et authentifiée gratuite de Docker Hub sont entrées en vigueur. Anonyme et libre [!DNL Docker Hub] Les utilisateurs sont limités à 100 demandes d’extraction d’image de conteneur toutes les six heures. Si ces modifications vous affectent, vous recevrez ce message d’erreur : `ERROR: toomanyrequests: Too Many Requests.` ou `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

Actuellement, cette limite n’affecte votre entreprise que si vous tentez de créer 100 notebooks vers les recettes au cours de la période de six heures ou si vous utilisez des notebooks basés sur Spark dans Data Science Workspace, qui sont fréquemment mis à l’échelle. Cependant, cela est peu probable, car le cluster s’exécute pendant deux heures principal avant de se déconnecter. Cela réduit le nombre d’appels requis lorsque la grappe est principale. Si vous recevez l’une des erreurs ci-dessus, vous devrez attendre que votre [!DNL Docker] La limite est réinitialisée.

Pour plus d’informations sur [!DNL Docker Hub] limites de taux, rendez-vous sur la page [Documentation DockerHub](https://www.docker.com/increase-rate-limits). Une solution à ce problème est en cours de traitement et attendue dans une version ultérieure.
