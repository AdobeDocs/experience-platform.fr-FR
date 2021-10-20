---
keywords: Experience Platform ; dépannage ; Espace de travail Data Science ; rubriques populaires
solution: Experience Platform
title: Guide de dépannage de l'espace de travail Data Science
topic-legacy: Troubleshooting
description: Ce document fournit des réponses aux questions fréquentes sur Adobe Experience Platform Data Science Workspace.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: ec42d80e695ccf57c10c539ae1b5104c7948c473
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 21%

---

# Guide de dépannage du [!DNL Data Science Workspace]

Ce document répond aux questions les plus fréquentes sur Adobe Experience Platform [!DNL Data Science Workspace]. Pour les questions et le dépannage concernant [!DNL Platform] API en général, voir la section [Guide de dépannage des API Adobe Experience Platform](../landing/troubleshooting.md).

## État de la requête Notebook JupyterLab bloqué dans l&#39;état d&#39;exécution

Un ordinateur portable JupyterLab peut indiquer qu&#39;une cellule est en état d&#39;exécution indéfiniment, dans certaines conditions de mémoire insuffisante. Par exemple, lors de l&#39;interrogation d&#39;un ensemble de données volumineux ou de l&#39;exécution de plusieurs requêtes ultérieures, le Bloc-notes JupyterLab peut manquer de mémoire disponible pour stocker l&#39;objet dataframe obtenu. Il y a quelques indicateurs que l&#39;on peut voir dans cette situation. Tout d&#39;abord, le noyau entre dans l&#39;état d&#39;inactivité même si la cellule s&#39;affiche comme étant en cours d&#39;exécution indiqué par la [`*`] en regard de la cellule. En outre, la barre inférieure indique la quantité de RAM utilisée/disponible.

![Barrage disponible](./images/jupyterlab/user-guide/allocate-ram.png)

Pendant la lecture des données, la mémoire peut augmenter jusqu&#39;à atteindre la quantité maximale de mémoire allouée. La mémoire est libérée dès que la mémoire maximale est atteinte et que le noyau redémarre. Cela signifie que la mémoire utilisée dans ce scénario peut apparaître très faible en raison du redémarrage du noyau, alors qu&#39;juste avant le redémarrage, la mémoire aurait été très proche de la RAM allouée maximale.

Pour résoudre ce problème, sélectionnez l’icône d’engrenage en haut à droite de JupyterLab et faites glisser le curseur vers la droite, puis sélectionnez **[!UICONTROL Mettre à jour les configurations]** pour allouer plus de mémoire vive. En outre, si vous exécutez plusieurs requêtes et que votre valeur RAM approche de la quantité maximale allouée, à moins que vous n&#39;ayez besoin des résultats de requêtes précédentes, redémarrez le noyau pour réinitialiser la quantité disponible de RAM. Cela garantit que vous disposez de la quantité maximale de RAM disponible pour la requête en cours.

![allouer plus de mémoire](./images/jupyterlab/user-guide/notebook-gpu-config.png)

Si vous allouez la quantité maximale de mémoire (RAM) et que vous rencontrez toujours ce problème, vous pouvez modifier votre requête pour opérer sur une taille de jeu de données plus petite en réduisant les colonnes ou la plage de données. Pour utiliser la totalité des données, il est recommandé d’utiliser un ordinateur portable Spark.

## [!DNL JupyterLab] l&#39;environnement ne se charge pas dans [!DNL Google Chrome]

>[!IMPORTANT]
>
>Ce problème a été résolu, mais il peut toujours être présent dans le navigateur Google Chrome 80.x. Assurez-vous que votre navigateur Chrome est à jour.

Avec la [!DNL Google Chrome] version 80.x du navigateur, tous les cookies tiers sont bloqués par défaut. Cette stratégie peut empêcher [!DNL JupyterLab] à partir du chargement dans Adobe Experience Platform.

Pour remédier à ce problème, procédez de la manière suivante :

Dans votre [!DNL Chrome] , accédez à l’angle supérieur droit et sélectionnez **Paramètres** (vous pouvez également copier et coller &quot;chrome://settings/&quot; dans la barre d&#39;adresse). Faites ensuite défiler la page jusqu’en bas, puis cliquez sur la liste déroulante **Paramètres avancés**.

![paramètres avancés de Chrome](./images/faq/chrome-advanced.png)

La section **Confidentialité et sécurité** s’affiche. Cliquez ensuite sur **Paramètres des sites**, puis sur **Cookies et données du site**.

![paramètres avancés de Chrome](./images/faq/privacy-security.png)

![paramètres avancés de Chrome](./images/faq/cookies.png)

Enfin, faites basculer « Bloquer les cookies tiers » sur « Désactivé ».

![paramètres avancés de Chrome](./images/faq/toggle-off.png)

>[!NOTE]
>
>Vous pouvez également désactiver les cookies tiers et ajouter des [*.]ds.adobe.net vers la liste des autorisations.

Saisissez « chrome://flags/ » dans votre barre d’adresse. Recherchez et désactivez l’indicateur intitulé *« SameSite by default cookies »* en utilisant le menu déroulant sur la droite.

![désactiver l’indicateur samesite](./images/faq/samesite-flag.png)

Après l’étape 2, vous êtes invité à relancer votre navigateur. Après avoir redémarré, [!DNL Jupyterlab] doit être accessible.

## Pourquoi suis-je incapable d’accéder à [!DNL JupyterLab] dans Safari ?

Safari désactive les cookies tiers par défaut dans Safari &lt; 12. Parce que [!DNL Jupyter] l&#39;instance de machine virtuelle réside sur un domaine différent de son cadre parent, Adobe Experience Platform exige actuellement l&#39;activation des cookies tiers. Activez les cookies tiers ou passez à un autre navigateur comme [!DNL Google Chrome].

Pour Safari 12, vous devez basculer l’agent utilisateur sur &quot;[!DNL Chrome]&#39; ou &#39;[!DNL Firefox]&#39;. Pour changer d’agent d’utilisateur, commencez par ouvrir la *Safari* et sélectionnez **Préférences**. La fenêtre Préférences s’affiche.

![Préférences Safari](./images/faq/preferences.png)

Dans la fenêtre des préférences de Safari, sélectionnez **Avancé**. Cochez ensuite la case *Afficher le menu Développement dans la barre de menus* boîte. Une fois cette étape terminée, vous pouvez fermer la fenêtre des préférences.

![Safari avancé](./images/faq/advanced.png)

Ensuite, dans la barre de navigation supérieure, sélectionnez **Développement** . De dans **Développement** liste déroulante, survol **Agent utilisateur**. Vous pouvez sélectionner l’option **[!DNL Chrome]** ou **[!DNL Firefox]** Chaîne de l&#39;agent utilisateur que vous souhaitez utiliser.

![Menu Développement](./images/faq/user-agent.png)

## Pourquoi un message « 403 Forbidden » apparaît-il lorsque j’essaie de charger ou de supprimer un fichier dans [!DNL JupyterLab]?

Si votre navigateur est activé avec un logiciel de blocage de publication tel que [!DNL Ghostery] ou [!DNL AdBlock] En outre, le domaine &quot;\*.adobe.net&quot; doit être autorisé dans chaque logiciel de blocage de publication pour [!DNL JupyterLab] pour fonctionner normalement. C&#39;est parce que [!DNL JupyterLab] les machines virtuelles s&#39;exécutent sur un domaine différent de celui [!DNL Experience Platform] domaine.

## Pourquoi faire certaines parties de mes [!DNL Jupyter Notebook] vous avez l’air brouillé ou le rendu n’est pas effectué en tant que code ?

Cela peut se produire si la cellule en question est passée par erreur de « Code » à « Markdown ». Lorsqu’une cellule de code est sélectionnée, appuyez sur la combinaison de touches **ESC+M** pour modifier le type de la cellule sur Markdown. Vous pouvez modifier le type d’une cellule à l’aide de l’indicateur déroulant situé en haut du notebook pour la ou les cellules sélectionnées. Pour modifier un type de cellule en code, commencez par sélectionner la cellule donnée que vous souhaitez modifier. Cliquez ensuite sur la liste déroulante qui indique le type actuel de la cellule, puis sélectionnez « Code ».

![](./images/faq/code_type.png)

## Comment installer des [!DNL Python] bibliothèques ?

Le [!DNL Python] est préinstallé avec de nombreuses bibliothèques d&#39;apprentissage machine populaires. Cependant, vous pouvez installer d’autres bibliothèques personnalisées en exécutant la commande suivante dans une cellule de code :

```shell
!pip install {LIBRARY_NAME}
```

Pour obtenir la liste complète des [!DNL Python] bibliothèques, voir [section annexe du Guide de l’utilisateur de JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Puis-je installer des bibliothèques PySpark personnalisées ?

Malheureusement, vous ne pouvez pas installer de bibliothèques supplémentaires pour le noyau PySpark. Néanmoins, vous pouvez contacter votre représentant du service client Adobe et lui demander d’installer ces bibliothèques PySpark personnalisées pour vous.

Pour obtenir la liste des bibliothèques PySpark préinstallées, consultez la [section annexe du guide d’utilisation de JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Est-il possible de configurer [!DNL Spark] ressources de cluster pour [!DNL JupyterLab] [!DNL Spark] ou du noyau PySpark ?

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

Pour plus d’informations sur [!DNL Spark] configuration des ressources de cluster, y compris la liste complète des propriétés configurables, consultez la section [Guide de l’utilisateur de JupyterLab](./jupyterlab/overview.md#kernels).

## Pourquoi est-ce que je reçois une erreur lors d&#39;une tentative d&#39;exécution de certaines tâches pour des ensembles de données plus volumineux ?

Si vous recevez une erreur pour une raison telle que `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` Cela signifie généralement que le pilote ou l&#39;exécuteur est à court de mémoire. Voir les portables JupyterLab [accès aux données](./jupyterlab/access-notebook-data.md) documentation pour plus d&#39;informations sur les limites de données et comment exécuter des tâches sur des ensembles de données volumineux. En règle générale, cette erreur peut être résolue en modifiant le paramètre `mode` de `interactive` à `batch`.

En outre, lors de l’écriture de jeux de données Spark/PySpark volumineux, mise en cache de vos données (`df.cache()`) avant d’exécuter le code d’écriture peut considérablement améliorer les performances.

<!-- remove this paragraph at a later date once the sdk is updated -->

Si vous rencontrez des problèmes lors de la lecture des données et si vous appliquez des transformations aux données, essayez de mettre en cache vos données avant les transformations. La mise en cache de vos données empêche plusieurs lectures sur le réseau. Commencez par lire les données. Suivant, cache (`df.cache()`) les données. Pour finir, effectuez vos transformations.

## Pourquoi mes ordinateurs portables Spark/PySpark prennent-ils autant de temps pour lire et écrire des données ?

Si vous effectuez des transformations sur des données, par exemple en utilisant `fit()`, les transformations peuvent être exécutées plusieurs fois. Pour améliorer les performances, mettez en cache vos données à l’aide de `df.cache()` avant d’exécuter la `fit()`. Cela permet de s’assurer que les transformations ne sont exécutées qu’une seule fois et d’éviter la lecture multiple sur le réseau.

**Ordre recommandé :** Commencez par lire les données. Ensuite, effectuez des transformations suivies de la mise en cache (`df.cache()`) les données. Enfin, effectuez une `fit()`.

## Pourquoi mes ordinateurs portables Spark/PySpark ne fonctionnent-ils pas ?

Si vous recevez l’une des erreurs suivantes :

- Travail abandonné en raison d&#39;un échec de la phase... Peuvent uniquement compresser des RDD avec le même nombre d&#39;éléments dans chaque partition.
- Client RPC distant dissocié et autres erreurs de mémoire.
- Mauvaise performance lors de la lecture et de l&#39;écriture des ensembles de données.

Vérifiez que vous mettez en cache les données (`df.cache()`) avant d’écrire les données. Lors de l’exécution de code dans des blocs-notes, utilisation `df.cache()` avant une action telle que `fit()` peut considérablement améliorer les performances des ordinateurs portables. Utilisation `df.cache()` avant d&#39;écrire un jeu de données, vous vous assurez que les transformations ne sont exécutées qu&#39;une seule fois au lieu de plusieurs fois.

## [!DNL Docker Hub] restrictions limites dans l&#39;espace de travail Data Science

Depuis le 20 novembre 2020, les limites de taux pour l&#39;utilisation anonyme et authentifiée gratuite de Docker Hub sont entrées en vigueur. Anonymes et libres [!DNL Docker Hub] les utilisateurs sont limités à 100 demandes d’extraction d’images conteneurs toutes les six heures. Si ces modifications vous affectent, vous recevrez ce message d’erreur : `ERROR: toomanyrequests: Too Many Requests.` ou `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

Actuellement, cette limite n’affectera votre entreprise que si vous tentez de créer 100 blocs-notes vers des recettes dans le délai de six heures ou si vous utilisez des blocs-notes basés sur Spark dans l’espace de travail Data Science qui sont fréquemment mis à l’échelle vers le haut et vers le bas. Toutefois, cela est peu probable, puisque le cluster sur lequel ces exécutions sont exécutées reste actif pendant deux heures avant de se retirer. Cela réduit le nombre d&#39;appels requis lorsque le cluster est actif. Si vous recevez l’une des erreurs ci-dessus, vous devrez attendre que votre [!DNL Docker] la limite est réinitialisée.

Pour plus d’informations sur [!DNL Docker Hub] limites de taux, rendez-vous sur la page [Documentation DockerHub](https://www.docker.com/increase-rate-limits). Une solution à ce problème est en cours d’élaboration et attendue dans une version ultérieure.
