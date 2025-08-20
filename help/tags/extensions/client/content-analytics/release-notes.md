---
title: Notes de mise à jour de l’extension Adobe Content Analytics
description: Dernières notes de mise à jour pour l’extension de balise Content Analytics dans Adobe Experience Platform.
source-git-commit: 24ff17af89bc882f08ec0f331ebae53b61f35d78
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 1%

---

# Notes de mise à jour de l’extension Adobe Content Analytics

Voici une liste de notes de mise à jour pour l’extension de balise Content Analytics.

| Version | Date | Correctifs |
|---|---|---|
| <p>1,0,47</p> | <p>23 Juil 2025</p> | <ul><li>Correction du bug rencontré par un client ou une cliente lorsque les expériences n’étaient pas activées et que la vérification d’expression régulière échouait. En conséquence, les données Content Analytics ne sont pas collectées.</li><li>Correction d’un bug de langue par défaut qui empêchait l’affichage de l’interface utilisateur des balises pour certains utilisateurs dont la langue principale par défaut n’était pas définie dans Experience Cloud.</li></ul> |
| <p>1,0,46</p> | <p>18 Juin 2025</p> | <ul><li>Ajoute une notification toast si un flux de données de production n’est pas présent lors de la tentative d’enregistrement de la configuration de l’extension.</li><li>Correction temporaire de la visibilité de la payload de Content Analytics, mais en plaçant le contenu de la payload Content Analytics fragmentée dans la console.</li><li>Ajoute la localisation à l’interface utilisateur de l’extension.</li><li>Correction partielle d’un problème CSS avec un remplissage supplémentaire autour du contenu de l’interface utilisateur de l’extension.</li></ul> |
| <p>1,0,45</p> | <p>14 Avril 2025</p> | <ul><li>Résout quelques bugs dans les paramètres de configuration pour lors de la conservation d’événements Content Analytics lors de l’attente d’événements de page vue. Désormais, Content Analytics attend par défaut que le PREMIER événement de page vue se produise pour déclencher des événements.</li></ul> |
| <p>1,0,44</p> | <p>31 Mars 2025</p> | <ul><li>Première itération de l’intégration AppMeasurement.</li><li>Cette version ne prend pas en charge le filtrage sur des requêtes spécifiques (par exemple, les pages vues), mais peut être ajoutée ultérieurement.  Cette méthode utilise également la première instance AppMeasurement figurant sur la page.</li></ul> |
| <p>1,0,43</p> | <p>10 Mars 2025</p> | <ul><li>Version initiale de l’extension.</li></ul> |

