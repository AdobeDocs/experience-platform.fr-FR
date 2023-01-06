---
keywords: Experience Platform;accueil;rubriques populaires;visionneuse de graphiques d’identités;visionneuse de graphiques d’identités;visionneuse de graphiques;visionneuse de graphiques;espace de noms d’identité;espace de noms d’identité;identité;service d’identités;service d’identités
solution: Experience Platform
title: Présentation de la visionneuse de graphiques d’identités
description: Un graphique d’identités est une carte des relations entre différentes identités pour un client spécifique, qui vous fournit une représentation visuelle de la manière dont votre client interagit avec votre marque sur différents canaux.
exl-id: ccd5f8d8-595b-4636-9191-553214e426bd
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 9%

---

# Présentation de la visionneuse de graphiques d’identités

Un graphique d’identités est une carte des relations entre différentes identités pour un client spécifique, qui vous fournit une représentation visuelle de la manière dont votre client interagit avec votre marque sur différents canaux. Tous les graphiques d’identités client sont gérés et mis à jour collectivement par le Service d’identités d’Adobe Experience Platform en temps quasi réel, en réponse à l’activité du client.

La visionneuse de graphiques d’identités de l’interface utilisateur de Platform vous permet de visualiser et de mieux comprendre quelles identités de client sont regroupées, et de quelles manières. La visionneuse vous permet de faire glisser différentes parties du graphique et d’interagir avec celles-ci. Vous pouvez ainsi examiner les relations d’identité complexes, effectuer plus efficacement le débogage et bénéficier d’une plus grande transparence en ce qui concerne l’utilisation des informations.

## Tutoriel vidéo

La vidéo suivante est destinée à vous aider à comprendre la visionneuse de graphiques d’identités.

>[!VIDEO](https://video.tv.adobe.com/v/331030/?quality=12&learn=on)

## Prise en main

L’utilisation de la visionneuse de graphiques d’identités nécessite une compréhension des différents services Adobe Experience Platform impliqués. Avant de commencer à utiliser la visionneuse de graphiques d’identités, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Identity Service]](../home.md) : profitez d’une meilleure compréhension de vos clients et de leurs comportements en rapprochant des identités entre appareils et systèmes.

### Terminologie

- **Identité (noeud) :** Une identité ou un noeud sont des données propres à une entité, généralement une personne. Une identité se compose d’un espace de noms et d’une valeur d’identité.
- **Lien (edge) :** Un lien ou un bord représente la connexion entre les identités.
- **Graphique (grappe) :** Un graphique ou un cluster est un groupe d’identités et de liens qui représentent une personne.

## Accès à la visionneuse de graphiques d’identités

Pour utiliser la visionneuse de graphiques d’identités dans l’interface utilisateur, sélectionnez **[!UICONTROL Identités]** dans le volet de navigation de gauche, puis sélectionnez l’option **[!UICONTROL Graphique d’identités]** . Dans la **[!UICONTROL Espace de noms d’identité]** , cliquez sur l’écran **[!UICONTROL Sélectionner un espace de noms d’identité]** pour rechercher l’espace de noms que vous avez l’intention d’utiliser.

![namespace-screen](../images/identity-graph-viewer/identity-namespace.png)

Le **[!UICONTROL Sélectionner un espace de noms d’identité]** s’affiche. Cet écran contient une liste d’espaces de noms disponibles pour votre organisation, y compris des informations sur un espace de noms **[!UICONTROL Nom d’affichage]**, **[!UICONTROL Symbole d’identité]**, **[!UICONTROL Propriétaire]**, **[!UICONTROL Dernière mise à jour]** date et **[!UICONTROL Description]**. Vous pouvez utiliser n’importe quel espace de noms fourni tant qu’une valeur d’identité valide y est connectée.

Sélectionnez l’espace de noms que vous souhaitez utiliser, puis cliquez sur **[!UICONTROL Sélectionner]** pour continuer.

![select-identity-namespace](../images/identity-graph-viewer/select-identity-namespace.png)

Une fois que vous avez sélectionné un espace de noms, saisissez la valeur correspondante pour un client particulier dans la variable **[!UICONTROL Valeur d’identité]** zone de texte et sélectionnez **[!UICONTROL Affichage]**.

![add-identity-value](../images/identity-graph-viewer/identity-value-filled.png)

### Accès à la visionneuse de graphiques d’identités à partir de jeux de données

Vous pouvez également accéder à la visionneuse de graphiques d’identités à l’aide de l’interface des jeux de données. À partir des jeux de données [!UICONTROL Parcourir] , sélectionnez un jeu de données avec lequel interagir, puis sélectionnez **[!UICONTROL Prévisualisation d’un jeu de données]**

![preview-dataset](../images/identity-graph-viewer/preview-dataset.png)

Dans la fenêtre d’aperçu, sélectionnez une icône d’empreinte digitale pour afficher les identités représentées par le biais de la visionneuse de graphiques d’identités.

>[!TIP]
>
>L’icône d’empreinte ne s’affiche que si le jeu de données comporte deux identités ou plus.

![empreinte digitale](../images/identity-graph-viewer/fingerprint.png)

La visionneuse de graphique d’identités s’affiche. Sur le côté gauche de l’écran se trouve le graphique d’identités qui affiche toutes les identités liées à l’espace de noms que vous avez sélectionné et à la valeur d’identité que vous avez saisie. Chaque noeud d’identité se compose d’un espace de noms et de sa valeur d’identifiant correspondante. Vous pouvez sélectionner et contenir n’importe quelle identité pour faire glisser et interagir avec le graphique. Vous pouvez également placer le pointeur de la souris sur une identité pour afficher des informations sur sa valeur d’identifiant. La sortie du graphique s’affiche également sous la forme d’une liste de tableaux au centre de l’écran.

>[!IMPORTANT]
>
>Un graphique d’identités requiert au minimum deux identités liées à générer, ainsi qu’un espace de noms et une paire d’identifiants valides. Le nombre maximal d’identités que la visionneuse de graphiques peut afficher est de 150. Voir [annexe](#appendix) pour plus d’informations.

![identity-graph](../images/identity-graph-viewer/graph-viewer.png)

Sélectionnez une identité pour mettre à jour la ligne mise en surbrillance sur la page **[!UICONTROL Identités]** et de mettre à jour les informations fournies sur le rail de droite, qui incluent le **[!UICONTROL Valeur]**, **[!UICONTROL Identifiant de lot]**, et **[!UICONTROL Dernière mise à jour]** date.

![select-identity](../images/identity-graph-viewer/select-identity.png)

Vous pouvez filtrer par un graphique et isoler un espace de noms spécifique à l’aide de l’option de tri située en haut de la **[!UICONTROL Identités]** table. Dans le menu déroulant, sélectionnez l’espace de noms à mettre en surbrillance.

![filter-by-namespace](../images/identity-graph-viewer/filter-namespace.png)

La visionneuse de graphiques renvoie, en mettant en surbrillance l’espace de noms que vous avez sélectionné. L’option de filtrage met également à jour la variable **[!UICONTROL Identités]** pour renvoyer des informations uniquement pour l’espace de noms que vous avez sélectionné.

![filtré](../images/identity-graph-viewer/filtered.png)

Le coin supérieur droit de la zone de la visionneuse de graphiques contient des options d’agrandissement. Sélectionnez la **(+)** pour effectuer un zoom avant ou arrière sur le graphique **(-)** pour effectuer un zoom arrière.

![zoom](../images/identity-graph-viewer/zoom.png)

Vous pouvez afficher plus d’informations sur les lots en sélectionnant le **[!UICONTROL Source de données]** dans l’en-tête . Le **[!UICONTROL Source de données]** affiche une liste de **[!UICONTROL Identifiants de lot]** associée au graphique, ainsi qu’à ses **[!UICONTROL ID liés]**, le schéma source et la date d’ingestion.

![data-source](../images/identity-graph-viewer/data-source-table.png)

Vous pouvez sélectionner l’un des liens d’un graphique d’identités pour afficher tous les lots source ayant contribué au lien.

![select-links](../images/identity-graph-viewer/select-edge.png)

Vous pouvez également sélectionner un lot pour afficher tous les liens auxquels ce lot a contribué.

![select-links](../images/identity-graph-viewer/select-batch.png)

Les graphiques d’identités avec des groupes d’identités plus importants sont également accessibles par le biais de la visionneuse de graphiques d’identités.

![grande grappe](../images/identity-graph-viewer/large-cluster.png)

## Annexe

La section suivante fournit des informations supplémentaires sur l’utilisation de la visionneuse de graphiques d’identités.

### Comprendre les messages d’erreur

Des erreurs peuvent se produire lors de l’accès à la visionneuse de graphiques d’identités. Vous trouverez ci-dessous une liste des conditions préalables et des limites à prendre en compte lors de l’utilisation de la visionneuse de graphiques d’identités.

- Une valeur d’identité doit exister dans l’espace de noms sélectionné.
- La visionneuse de graphiques d’identités requiert au moins deux identités liées à générer. Il est possible qu’il n’existe qu’une seule valeur d’identité et aucune identité liée. Dans ce cas, la valeur n’existerait que dans [!DNL Profile] visionneuse.
- La visionneuse de graphiques d’identités ne peut pas dépasser 150 identités au maximum.

![error-screen](../images/identity-graph-viewer/error-screen.png)

## Étapes suivantes

En lisant ce document, vous avez appris à explorer les graphiques d’identités de vos clients dans l’interface utilisateur de Platform. Pour plus d’informations sur les identités dans Platform, reportez-vous à la section [Présentation d’Identity Service](../home.md)

## Journal des modifications

| Date | Action |
| ---- | ------ |
| 2021-01 | <ul><li>Ajout de la prise en charge de la diffusion en continu des données ingérées et des environnements de test hors production.</li><li>Correction de bogues mineurs.</li></ul> |
| 2021-02 | <ul><li>La visionneuse de graphiques d’identités est rendue accessible par l’aperçu du jeu de données.</li><li>Correction de bogues mineurs.</li><li>La visionneuse de graphique d’identités est rendue disponible en général.</li></ul> |
