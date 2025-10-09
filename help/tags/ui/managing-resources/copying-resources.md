---
title: Copie des ressources
description: Découvrez comment créer une ressource de balise à lʼaide des paramètres dʼune ressource de balise existante dans Adobe Experience Platform.
exl-id: 7e52ceae-97df-4c64-aba3-4f5ba6018a47
source-git-commit: a4e4fe0ae0f52a3b4b5bfa2c42ef4dce7f2a6a59
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 87%

---

# Copie des ressources

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Parfois, il peut s’avérer pratique de créer une nouvelle ressource à l’aide des paramètres d’une ressource existante. Dans ce cas, vous pouvez en faire une copie.

Les propriétés, les extensions, les règles et les éléments de données peuvent tous être copiés.

La copie d’une ressource crée un double de cette ressource dans la destination spécifiée. Il s’agit d’une action ponctuelle discrète, et il n’y a aucune relation constante entre la ressource d’origine et les copies qui ont été réalisées.

## Lancer une copie

Vous pouvez lancer une copie d’une extension en affichant vos extensions installées, puis en cliquant sur la flèche de liste déroulante sur le bouton **[!UICONTROL Configurer]** et en sélectionnant **[!UICONTROL Copier]**.

![Copie de l’extension Analytics](../../images/copy-initiate-extension.png)

Pour les propriétés, les règles et les éléments de données, sélectionnez simplement la ressource que vous voulez copier, puis cliquez sur **[!UICONTROL Copier]** dans le menu d’actions.

![Copie de ma règle Analytics](../../images/copy-initiate-rule.png)

Si vous copiez une règle ou un élément de données, vous pouvez utiliser le menu déroulant de la boîte de dialogue Copier pour sélectionner une propriété de destination vers laquelle vous voulez effectuer la copie (le paramètre par défaut est la propriété active). Les extensions ne peuvent pas être copiées dans la même propriété. Par conséquent, cette option ne sera pas disponible.

>[!NOTE]
>
>Il n’est pas possible de copier des ressources vers une autre propriété si une propriété est configurée pour le développement d’extensions et que l’autre propriété ne l’est pas.

Après avoir configuré le comportement souhaité, cliquez sur **[!UICONTROL Copier]**.

## Copie de propriétés

Lorsque vous faites une copie d’une propriété complète, vous devez tenir compte de quelques éléments pour bien comprendre le processus.

>[!IMPORTANT]
>
>Les ressources utilisant le type de variable de mise à jour de l’élément de données nécessiteront des étapes supplémentaires après la copie. Modifiez chaque action de mise à jour de variable, apportez une modification à n’importe quelle valeur des données ou de l’objet XDM et enregistrez les modifications. La bibliothèque publiée doit alors fonctionner comme prévu. Si vous avez des questions sur ce processus, veuillez contacter le support technique.

* Les paramètres de propriété seront copiés exactement dans leur état d’origine (domaines, paramètres avancés, etc.)
* Les règles, les éléments de données et les extensions de la propriété d’origine sont copiés dans la nouvelle propriété cible. Les adaptateurs, les environnements et les bibliothèques ne seront pas copiés.
* Les extensions requises (extensions requises par tout élément de données ou composant de règle existant) seront copiées dans la propriété cible, même si elles ont été désinstallées de la propriété d’origine.
* La copie d’une propriété peut prendre un certain temps. Cette action s’effectue en arrière-plan. Vous pouvez suivre l’état d’avancement de la copie ou poursuivre d’autres tâches pendant qu’elle est en cours.
* Si vous modifiez une ressource individuelle après qu’elle ait déjà été copiée dans la propriété cible (mais avant que la copie soit terminée), les nouvelles modifications ne seront pas copiées.

## Copie d’extensions

Lorsque vous copiez une extension vers une autre propriété, vous devez tenir compte de certains points.

* Si l’extension n’est pas installée sur la propriété de destination, elle sera installée à l’aide des mêmes paramètres que la propriété d’origine.
* Si l’extension est déjà installée sur la propriété de destination, seuls les paramètres seront copiés.
* Si la version de la propriété de destination dispose d’une version inférieure de l’extension installée, vous recevrez un avis indiquant que vous devez mettre à niveau l’extension sur la propriété de destination avant de pouvoir effectuer la copie. Les développeurs d’extensions peuvent ajouter des paramètres à leurs extensions au fil du temps. Les paramètres provenant d’une extension plus récente ne peuvent donc pas être appliqués de manière fiable aux versions plus anciennes.
* Si la version de la propriété de destination dispose d’une version supérieure de l’extension installée, les paramètres sont copiés, mais aucune rétrogradation n’est effectuée. La propriété de destination conserve toujours son numéro de version actuel.

## Copie de règles et d’éléments de données

Toutes les règles et tous les éléments de données sont fournis par une extension. Par conséquent, lorsque vous copiez plusieurs propriétés, Experience Platform doit tenir compte de ces extensions sous-jacentes.

![Copie d’une règle vers ma propriété de démonstration](../../images/copy-rules-dialog1.png)

La boîte de dialogue Copier fournit une explication de ce qui se passera exactement avant que vous ne commenciez à copier. La boîte de dialogue ci-dessus concerne une règle, mais il en est de même pour les éléments de données.

1. **Les extensions requises par ces règles sont copiées.** Cela vous permet de savoir que les extensions requises vont suivre la règle. Ces copies suivent les mêmes règles qu’une copie d’extension normale décrite ci-dessus.
1. **Les paramètres d’extension ne seront PAS copiés si l’extension est déjà installée.** Cela signifie que si les extensions requises existent déjà sur la propriété de destination, l’extension reste inchangée. Si vous souhaitez également copier les paramètres d’extension, vous pouvez utiliser le bouton d’activation/désactivation **Remplacer les paramètres d’extension sur la propriété de destination** afin que l’explication soit mise à jour en conséquence.
1. **Les éléments de données requis par ces règles ne seront PAS copiés.** Cette explication s’applique uniquement aux règles. Le bon fonctionnement des règles repose souvent sur des éléments de données. Si vous copiez une règle vers une nouvelle propriété, vous devrez également copier les éléments de données requis en tant qu’action distincte.
