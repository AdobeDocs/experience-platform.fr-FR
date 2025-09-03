---
title: Notes de mise à jour de l’extension Adobe Content Analytics
description: Dernières notes de mise à jour pour l’extension de balise Content Analytics dans Adobe Experience Platform.
exl-id: 37b34915-655b-40de-b17b-43028c579e37
source-git-commit: 77d19ab813f881cd3c48c27ed4a9ac02e268e23f
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 1%

---

# Notes de mise à jour de l’extension Adobe Content Analytics

Voici une liste de notes de mise à jour pour l’extension de balise Content Analytics.

| Version | Date | Correctifs |
|---|---|---|
| 1,0,48 | 25 Août 2025 | <ul><li>Ajoute la prise en charge du suivi des ressources dans les éléments DOM shadow-root d’un document.</li></ul> |
| 1,0,47 | 23 Juil 2025 | <ul><li>Correction d’un bug qui se produisait lorsque les expériences n’étaient pas activées, ce qui entraînait l’échec de la vérification des expériences par l’expression régulière. Ce problème empêchait la collecte de données Content Analytics.</li><li>Correction d’un problème lié au paramètre de langue par défaut qui empêchait l’affichage de l’interface utilisateur des balises pour certains utilisateurs dont la langue principale par défaut n’était pas définie dans Experience Cloud.</li></ul> |
| 1,0,46 | 18 Juin 2025 | <ul><li>Ajout d’une notification toast lors de la tentative d’enregistrement de la configuration de l’extension, si un flux de données de production est absent.</li><li>Correction temporaire du problème de visibilité de la payload de Content Analytics en plaçant le contenu de la payload singulièrement renforcée dans la console.</li><li>Ajout de la localisation à l’interface utilisateur de l’extension.</li><li>Correction partielle d’un problème CSS qui entraînait une marge intérieure supplémentaire autour du contenu de l’interface utilisateur de l’extension.</li></ul> |
| 1,0,45 | 14 Avril 2025 | <ul><li>Correction de plusieurs bugs dans les paramètres de configuration liés à la conservation d’événements Content Analytics en attente d’événements de page vue. Par défaut, Content Analytics attend désormais que le PREMIER événement de page vue se produise avant de déclencher des événements.</li></ul> |
| 1,0,44 | 31 Mars 2025 | <ul><li>Première itération de l’intégration AppMeasurement.</li><li>Cette version ne prend pas encore en charge le filtrage de requêtes spécifiques (par exemple, les pages vues), mais cette fonctionnalité peut être ajoutée lors d’une prochaine mise à jour. Il utilise actuellement la première instance AppMeasurement trouvée sur la page.</li></ul> |
| 1,0,43 | 10 Mars 2025 | <ul><li>Version initiale de l’extension.</li></ul> |
