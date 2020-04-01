---
keywords: Experience Platform;troubleshooting;Data Science Workspace;popular topics
solution: Experience Platform
title: Guide de dépannage de Data Science Workspace
topic: Troubleshooting
translation-type: tm+mt
source-git-commit: 1f756e7bc71c9ff227757aee64af29e0772c24af

---


# Guide de dépannage de Data Science Workspace

Ce  fournit des réponses aux questions les plus fréquentes sur l’espace de travail Data Science d’Adobe Experience Platform. Pour toute question ou dépannage concernant les API de plateforme en général, consultez le guide [de dépannage des API de plateforme](../landing/troubleshooting.md)Adobe Experience Platform.

##  JupyterLab le  ne se charge pas dans Google Chrome

Avec la dernière mise à jour du navigateur Google Chrome vers la version 80.x, tous les cookies tiers sont bloqués par défaut. Cette nouvelle stratégie peut empêcher le chargement de JupyterLab dans Adobe Experience Platform.

>[!NOTE] C&#39;est un problème temporaire. La dépendance aux cookies tiers est définie pour être supprimée dans une version ultérieure.

Pour résoudre ce problème, procédez comme suit :

Dans votre navigateur Chrome, accédez au coin supérieur droit et sélectionnez **Paramètres** (vous pouvez également copier et coller &quot;chrome://settings/&quot; dans la barre d’adresse). Faites ensuite défiler la page jusqu’au bas de la page et cliquez sur la liste déroulante **Avancé** .

![chrome avancé](./images/faq/chrome-advanced.png)

La section *Confidentialité et sécurité* s’affiche. Cliquez ensuite sur Paramètres **du** site, puis sur **Cookies et données** du site.

![chrome avancé](./images/faq/privacy-security.png)

![chrome avancé](./images/faq/cookies.png)

Enfin, basculez &quot;Bloquer les cookies tiers&quot; sur &quot;Désactivé&quot;.

![chrome avancé](./images/faq/toggle-off.png)

>[!NOTE] Vous pouvez également désactiver les cookies tiers et la liste blanche [*.]ds.adobe.net

Accédez à &quot;chrome://flags/&quot; dans votre barre d&#39;adresse. Recherchez et désactivez l’indicateur intitulé *&quot;Même site par défaut&quot;* en utilisant le menu déroulant à droite.

![désactiver l&#39;indicateur samesite](./images/faq/samesite-flag.png)

Après l’étape 2, vous êtes invité à relancer votre navigateur. Après votre redémarrage, Jupyterlab doit être accessible.

## Pourquoi est-ce que je ne peux pas accéder à JupyterLab dans Safari ?

Par défaut, Safari désactive les cookies tiers. Comme votre instance d’ordinateur virtuel Jupyter réside sur un domaine différent de son cadre parent, Adobe Experience Platform exige actuellement l’activation des cookies tiers. Activez les cookies tiers ou passez à un autre navigateur tel que Google Chrome.

## Pourquoi est-ce que je vois un message &quot;403 interdit&quot; quand je tente de télécharger ou de supprimer un fichier dans JupyterLab ?

Si votre navigateur est activé avec un logiciel de blocage des publicités tel que Ghostery ou AdBlock Plus, le domaine &quot;\*.adobe.net&quot; doit être autorisé dans chaque logiciel de blocage des publicités pour que JupyterLab fonctionne normalement. En effet, les machines virtuelles JupyterLab s’exécutent sur un domaine différent de celui de la plateforme d’expérience.

## Pourquoi certaines parties de mon ordinateur portable Jupyter ont-elles l&#39;air brouillées ou ne sont-elles pas rendues en tant que code ?

Cela peut se produire si la cellule en question est accidentellement passée de &quot;Code&quot; à &quot;Marquage&quot;. Lorsqu’une cellule de code est active, appuyez sur la combinaison de touches **ESC+M** pour changer le type de cellule en Marquage. Le type d&#39;une cellule peut être modifié par l&#39;indicateur déroulant en haut du bloc-notes pour la ou les cellules sélectionnées. Pour modifier un type de cellule en code,  en sélectionnant la cellule à modifier. Cliquez ensuite sur la liste déroulante qui indique le type actuel de la cellule, puis sélectionnez &quot;Code&quot;.

![](./images/faq/code_type.png)

## Comment installer des bibliothèques Python personnalisées ?

Le noyau Python est préinstallé avec de nombreuses bibliothèques d&#39;apprentissage automatique. Cependant, vous pouvez installer d’autres bibliothèques personnalisées en exécutant la commande suivante dans une cellule de code :

```shell
!pip install {LIBRARY_NAME}
```

Pour un complet des bibliothèques Python préinstallées, consultez la section [en annexe du Guide](./jupyterlab/overview.md#supported-libraries)d&#39;utilisation de JupyterLab.

## Puis-je installer des bibliothèques PySpark personnalisées ?

Malheureusement, vous ne pouvez pas installer de bibliothèques supplémentaires pour le noyau PySpark. Vous pouvez toutefois contacter votre représentant du service clientèle Adobe pour que les bibliothèques PySpark personnalisées soient installées pour vous.

Pour un de bibliothèques PySpark préinstallées, reportez-vous à la section [en annexe du Guide](./jupyterlab/overview.md#supported-libraries)d&#39;utilisation de JupyterLab.

## Est-il possible de configurer les ressources de cluster Spark pour le noyau JupyterLab Spark ou PySpark ?

Vous pouvez configurer des ressources en ajoutant le bloc suivant à la première cellule de votre bloc-notes :

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

Pour plus d’informations sur la configuration des ressources de la grappe Spark, y compris le complet des propriétés configurables, consultez le Guide [d’utilisation de](./jupyterlab/overview.md#pyspark-spark-execution-resource)JupyterLab.