---
keywords: Experience Platform;home;popular topics;identity graph viewer;Identity graph viewer;graph viewer;Graph viewer;identity namespace;Identity namespace;identity;Identity;Identity service;identity service
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: tutorial
description: Un graphique d'identité est une carte des relations entre différentes identités pour un client particulier, qui vous permet de visualiser comment votre client interagit avec votre marque sur différents canaux.
translation-type: tm+mt
source-git-commit: df165baceaf8dc2b21055201ec78bd392044b938
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 3%

---


# (bêta) Visionneuse de graphiques d’identité

>[!NOTE]
>
>Le lecteur de graphique d’identité est actuellement en version bêta. Ses caractéristiques peuvent être modifiées.

Un graphique d&#39;identité est une carte des relations entre différentes identités pour un client particulier, qui vous permet de visualiser comment votre client interagit avec votre marque sur différents canaux. Tous les graphiques d&#39;identité des clients sont gérés et mis à jour collectivement par Adobe Experience Platform Identity Service en temps quasi réel, en réponse à l&#39;activité des clients.

La visionneuse de graphiques d’identité de l’interface utilisateur de la plate-forme vous permet de visualiser et de mieux comprendre les identités des clients qui sont assemblées, et de quelles manières. Le lecteur de contenu vous permet de faire glisser et d’interagir différentes parties du graphique, ce qui vous permet d’examiner les relations d’identité complexes, de déboguer plus efficacement et de bénéficier d’une transparence accrue dans la manière dont les informations sont utilisées.

## Prise en main

L’utilisation du lecteur de graphique d’identité nécessite une compréhension des différents services Adobe Experience Platform impliqués. Avant de commencer à travailler avec la visionneuse de graphiques d&#39;identité, consultez la documentation relative aux services suivants :

- [[!DNL Identity Service]](../home.md) : profitez d’une meilleure compréhension de vos clients et de leurs comportements en rapprochant des identités entre appareils et systèmes.

### Terminologie

- **Identité (noeud) :** Une identité ou un noeud est des données propres à une entité, généralement une personne. Une identité comprend un espace de nommage et une valeur d&#39;identité.
- **Lien (bord) :** Un lien ou un bord représente la connexion entre les identités.
- **Graphique (grappe) :** Un graphique ou une grappe est un groupe d’identités et de liens qui représentent une personne.

## Accès au lecteur de graphique d&#39;identité

Pour utiliser la visionneuse de graphiques d’identité dans l’interface utilisateur, sélectionnez **[!UICONTROL Identités]** dans le volet de navigation de gauche, puis sélectionnez l’onglet Graphique **** d’identité. Dans l&#39;écran Espace de nommage **** d&#39;identité, cliquez sur l&#39;icône **[!UICONTROL Sélectionner un espace de nommage]** d&#39;identité pour rechercher l&#39;espace de nommage que vous avez l&#39;intention d&#39;utiliser.

![espace de nommage-écran](../images/identity-graph-viewer/identity-namespace.png)

Le panneau **[!UICONTROL Sélectionner un espace de nommage]** d&#39;identité s&#39;affiche. Cet écran contient une liste d&#39;espaces de nommage disponibles pour votre organisation, y compris des informations sur un nom **[!UICONTROL d&#39;]** affichage du espace de nommage, un symbole **** d&#39;identité, un **[!UICONTROL propriétaire]**, une date de **[!UICONTROL dernière mise à jour et Description.]****** Vous pouvez utiliser n’importe quel espace de nommage fourni tant que vous disposez d’une valeur d’identité valide qui lui est connectée.

Sélectionnez l’espace de nommage que vous souhaitez utiliser et cliquez sur **[!UICONTROL Sélectionner]** pour continuer.

![select-identity-espace de nommage](../images/identity-graph-viewer/select-identity-namespace.png)

Une fois que vous avez sélectionné un espace de nommage, entrez sa valeur correspondante pour un client particulier dans la zone de texte Valeur **** d’identité et sélectionnez **[!UICONTROL Vue]**.

![add-identity-value](../images/identity-graph-viewer/identity-value-filled.png)

La visionneuse de graphiques d&#39;identité s&#39;affiche. Sur le côté gauche de l&#39;écran se trouve le graphique d&#39;identité qui affiche toutes les identités liées à l&#39;espace de nommage sélectionné et la valeur d&#39;identité saisie. Chaque noeud d’identité est constitué d’un espace de nommage et de sa valeur d’ID correspondante. Vous pouvez sélectionner et conserver toute identité pour faire glisser et interagir avec le graphique. Vous pouvez également placer le pointeur de la souris sur une identité pour afficher des informations sur sa valeur d’identifiant. La sortie du graphique s’affiche également sous la forme d’une liste déposée au centre de l’écran.

>[!IMPORTANT]
>
>Un graphique d’identité requiert au moins deux identités liées à générer, ainsi qu’une paire d’espaces de nommage et d’identifiants valide. Le nombre maximal d’identités pouvant être affichées par la visionneuse de graphiques est de 400. Pour plus d&#39;informations, consultez la section de l&#39; [annexe](#appendix) ci-dessous.

![identity-graph](../images/identity-graph-viewer/graph-viewer.png)

Sélectionnez une identité pour mettre à jour la ligne mise en surbrillance de la table **[!UICONTROL Identités]** et pour mettre à jour les informations fournies sur le rail de droite, notamment la **[!UICONTROL valeur]** d&#39;une identité, l&#39;ID **** de lot et sa date de **[!UICONTROL dernière mise à jour.]**

![select-identity](../images/identity-graph-viewer/select-identity.png)

Vous pouvez filtrer un graphique et isoler un espace de nommage spécifique à l’aide de l’option de tri située en haut du tableau **[!UICONTROL Identités]** . Dans le menu déroulant, sélectionnez l’espace de nommage à mettre en surbrillance.

![filtre par espace de nommage](../images/identity-graph-viewer/filter-namespace.png)

La visionneuse de graphiques renvoie l’espace de nommage sélectionné en surbrillance. L’option de filtre met également à jour le tableau **[!UICONTROL Identités]** afin de renvoyer des informations uniquement pour l’espace de nommage sélectionné.

![filtré](../images/identity-graph-viewer/filtered.png)

Le coin supérieur droit de la zone de visualisation des graphiques contient des options de zoom. Sélectionnez l’icône **(+)** pour effectuer un zoom avant sur le graphique ou l’icône **(-)** pour effectuer un zoom arrière.

![zoom](../images/identity-graph-viewer/zoom.png)

Vous pouvez vue plus d’informations sur les lots en sélectionnant la source **[!UICONTROL de]** données dans l’en-tête. Le tableau Source **[!UICONTROL de]** données affiche une liste d’ID de **[!UICONTROL lot]** associés au graphique, ainsi que ses ID **** liés, son schéma source et sa date d’assimilation.

![source de données](../images/identity-graph-viewer/data-source-table.png)

Vous pouvez sélectionner n’importe quel lien dans un graphique d’identité pour afficher tous les lots source qui ont contribué au lien.

![select-links](../images/identity-graph-viewer/select-edge.png)

Vous pouvez également sélectionner un lot pour afficher tous les liens auxquels ce lot a contribué.

![select-links](../images/identity-graph-viewer/select-batch.png)

Les graphiques d’identité avec de plus grands groupes d’identités sont également accessibles par le biais de la visionneuse de graphiques d’identité.

![à grande grappe](../images/identity-graph-viewer/large-cluster.png)

## Annexe

La visionneuse de graphiques renvoie une erreur si les conditions préalables suivantes ne sont pas remplies :

- La valeur d&#39;identité n&#39;existe pas dans l&#39;espace de nommage sélectionné.
- Le graphique comporte moins de deux identités.
- Le graphique dépasse le maximum de 400 identités.
- Vous êtes dans un environnement sandbox hors production.

![à grande grappe](../images/identity-graph-viewer/error-screen.png)

## Étapes suivantes

En lisant ce document, vous avez appris à explorer les graphiques d’identité de vos clients dans l’interface utilisateur de la plate-forme. Pour plus d&#39;informations sur les identités dans Platform, reportez-vous à la présentation de [Identity Service.](../home.md)