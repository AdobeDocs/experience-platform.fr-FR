---
keywords: Experience Platform ; prép. données ; api. prép. données ; dépannage ; API
title: Présentation de l’API d’aperçu des données d’étape
topic-legacy: guide
description: L’API Prép de données vous permet de créer par programmation des jeux de correspondances et des fonctions, ce qui vous permet de transformer vos données entre les schémas source et cible.
exl-id: 740944ae-93ba-4099-a65e-18d6b384c307
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 1%

---

# Guide de l’API du service de mappage

La préparation des données permet aux ingénieurs de données de mapper, de transformer et de valider les données à partir du modèle de données d’expérience (XDM). L’aperçu des données s’affiche sous la forme d’une étape de &quot;mappage&quot; dans les processus d’importation de données, y compris le processus d’importation CSV.

L’API du service de mappage, également appelée API d’aperçu des données, comprend plusieurs points de terminaison décrits ci-dessous. Consultez les guides individuels des points de terminaison pour plus de détails et consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes requis, la lecture d&#39;exemples d&#39;appels d&#39;API, etc.

## Fonctions

Les fonctions d’ensemble de mappages vous permettent de transformer vos données entre les schémas source et de destination. Vous pouvez utiliser le point de terminaison `/languages/el` pour valider vos expressions et obtenir une liste de toutes les fonctions et opérations d&#39;ensemble de mappages disponibles.

Pour plus d&#39;informations sur l&#39;utilisation des fonctions d&#39;ensemble de mappages, consultez le [guide des points de terminaison des fonctions](./functions.md).

## Jeu de mappages

Les jeux de mappage peuvent être utilisés pour définir comment les données d&#39;un schéma source sont mises en correspondance avec celles d&#39;un schéma de destination. Vous pouvez utiliser le point de terminaison `/mappingSets` dans l’API d’aperçu des données pour récupérer, créer, mettre à jour et valider des jeux de mappage par programmation.

Pour plus d&#39;informations sur l&#39;utilisation des jeux de mappages, consultez le [guide du point de terminaison du jeu de mappage](./mapping-set.md).

## Étapes suivantes

Pour commencer à lancer des appels à l’aide de l’API du service de mappage, lisez le [guide de prise en main](./getting-started.md), puis sélectionnez l’un des guides de points de terminaison pour savoir comment utiliser les points de terminaison spécifiques.
