---
keywords: Experience Platform;troubleshooting;Data Science Workspace;popular topics
solution: Experience Platform
title: Guide de dépannage de Data Science Workspace
topic: Troubleshooting
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---


# [!DNL Data Science Workspace] guide de dépannage

Ce document fournit des réponses aux questions fréquentes sur l&#39;Adobe Experience Platform [!DNL Data Science Workspace]. Pour toute question ou dépannage concernant [!DNL Platform] les API en général, consultez le guide [de dépannage de l’API d’](../landing/troubleshooting.md)Adobe Experience Platform.

## [!DNL JupyterLab] L&#39;environnement ne se charge pas dans [!DNL Google Chrome]

>[!IMPORTANT]
>
>Ce problème a été résolu, mais il peut toujours être présent dans le navigateur Google Chrome 80.x. Assurez-vous que votre navigateur Chrome est à jour.

Avec la version 80.x du [!DNL Google Chrome] navigateur, tous les cookies tiers sont bloqués par défaut. Cette stratégie peut empêcher [!DNL JupyterLab] le chargement dans l’Adobe Experience Platform.

Pour résoudre ce problème, procédez comme suit :

Dans votre [!DNL Chrome] navigateur, accédez à l&#39;angle supérieur droit et sélectionnez **Paramètres** (vous pouvez également copier et coller &quot;chrome://settings/&quot; dans la barre d&#39;adresse). Ensuite, faites défiler la page jusqu’au bas de la page et cliquez sur la liste déroulante **Avancé** .

![chrome avancé](./images/faq/chrome-advanced.png)

La section *Confidentialité et sécurité* s&#39;affiche. Cliquez ensuite sur Paramètres **du** site, puis sur **Cookies et données** du site.

![chrome avancé](./images/faq/privacy-security.png)

![chrome avancé](./images/faq/cookies.png)

Enfin, basculez &quot;Bloquer les cookies tiers&quot; sur &quot;Désactivé&quot;.

![chrome avancé](./images/faq/toggle-off.png)

>[!NOTE]
>
>Vous pouvez également désactiver les cookies tiers et ajouter [*.]ds.adobe.net vers la liste autorisée.

Accédez à &quot;chrome://flags/&quot; dans la barre d&#39;adresse. Recherchez et désactivez l’indicateur intitulé *&quot;Même site par défaut&quot;* en utilisant le menu déroulant à droite.

![désactiver l&#39;indicateur samesite](./images/faq/samesite-flag.png)

Après l’étape 2, vous êtes invité à relancer votre navigateur. Une fois que vous avez redémarré, [!DNL Jupyterlab] vous devez être accessible.

## Pourquoi est-ce que je ne peux pas accéder [!DNL JupyterLab] à Safari ?

Safari désactive les cookies tiers par défaut dans Safari &lt; 12. Comme votre instance d&#39;ordinateur [!DNL Jupyter] virtuel réside sur un domaine différent de celui de son cadre parent, l&#39;Adobe Experience Platform exige actuellement l&#39;activation des cookies tiers. Activez les cookies tiers ou passez à un autre navigateur tel que [!DNL Google Chrome].

Pour Safari 12, vous devez remplacer l’agent utilisateur par &quot;[!DNL Chrome]&quot; ou &quot;[!DNL Firefox]&quot;. Pour changer d&#39;agent utilisateur, début en ouvrant le menu *Safari* et en sélectionnant **Préférences**. La fenêtre Préférences s&#39;affiche.

![Préférences Safari](./images/faq/preferences.png)

Dans la fenêtre des préférences de Safari, sélectionnez **Avancé**. Cochez ensuite la case *Afficher le menu Développer dans la barre* de menus. Vous pouvez fermer la fenêtre des préférences une fois cette étape terminée.

![Safari avancé](./images/faq/advanced.png)

Ensuite, dans la barre de navigation supérieure, sélectionnez le menu **Développer** . Dans la liste déroulante *Développer* , passez la souris sur Agent ** utilisateur. Vous pouvez sélectionner la chaîne **[!DNL Chrome]** ou **[!DNL Firefox]** User Agent que vous souhaitez utiliser.

![Menu Développer](./images/faq/user-agent.png)

## Pourquoi vois-je un message &quot;403 interdit&quot; lorsque je tente de télécharger ou de supprimer un fichier dans [!DNL JupyterLab]?

Si votre navigateur est activé avec un logiciel de blocage des publicités tel que [!DNL Ghostery] ou [!DNL AdBlock] Plus, le domaine &quot;\*.adobe.net&quot; doit être autorisé dans chaque logiciel de blocage des publicités pour [!DNL JupyterLab] fonctionner normalement. En effet, [!DNL JupyterLab] les machines virtuelles s&#39;exécutent sur un domaine différent de celui du [!DNL Experience Platform] domaine.

## Pourquoi certaines parties de mon [!DNL Jupyter Notebook] aspect semblent-elles brouillées ou ne s’affichent pas sous forme de code ?

Cela peut se produire si la cellule en question est accidentellement passée de &quot;Code&quot; à &quot;Marquage&quot;. Lorsqu’une cellule de code est activée, appuyez sur la combinaison de touches **ESC+M** pour changer le type de cellule en Marquage. Le type d&#39;une cellule peut être modifié par l&#39;indicateur déroulant situé en haut du bloc-notes pour la ou les cellules sélectionnées. Pour modifier un type de cellule en code, début en sélectionnant la cellule à modifier. Cliquez ensuite sur la liste déroulante indiquant le type actuel de la cellule, puis sélectionnez &quot;Code&quot;.

![](./images/faq/code_type.png)

## Comment installer des [!DNL Python] bibliothèques personnalisées ?

Le [!DNL Python] noyau est préinstallé avec de nombreuses bibliothèques d&#39;apprentissage automatique populaires. Cependant, vous pouvez installer d’autres bibliothèques personnalisées en exécutant la commande suivante dans une cellule de code :

```shell
!pip install {LIBRARY_NAME}
```

Pour une liste complète des [!DNL Python] bibliothèques préinstallées, consultez la section [en annexe du Guide](./jupyterlab/overview.md#supported-libraries)d&#39;utilisation de JupyterLab.

## Puis-je installer des bibliothèques PySpark personnalisées ?

Malheureusement, vous ne pouvez pas installer de bibliothèques supplémentaires pour le noyau PySpark. Toutefois, vous pouvez contacter votre représentant du service à la clientèle Adobe pour que des bibliothèques PySpark personnalisées soient installées pour vous.

Pour une liste des bibliothèques PySpark préinstallées, consultez la section [Annexe du Guide](./jupyterlab/overview.md#supported-libraries)d&#39;utilisation de JupyterLab.

## Est-il possible de configurer des ressources de [!DNL Spark] cluster pour [!DNL JupyterLab] le noyau [!DNL Spark] ou PySpark ?

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

Pour plus d’informations sur la configuration des ressources de [!DNL Spark] cluster, y compris la liste complète des propriétés configurables, consultez le Guide [d’utilisation de](./jupyterlab/overview.md#kernels)JupyterLab.