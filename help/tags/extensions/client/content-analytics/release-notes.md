---
title: Notes de mise à jour de l’extension Adobe Content Analytics
description: Dernières notes de mise à jour pour l’extension de balise Content Analytics dans Adobe Experience Platform.
exl-id: 37b34915-655b-40de-b17b-43028c579e37
TQID: https://experienceleague.adobe.com/9zJHsVFEb-RMqCQ6GmR6LH-bzIfkir-M1i5dOwaF6do
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 1d1baca838be7d394b5172efb333e59df76f85e2
workflow-type: tm+mt
source-wordcount: 572
ht-degree: 2%

---

# Notes de mise à jour de l’extension Adobe Content Analytics

Voici une liste de notes de mise à jour pour l’extension de balise Content Analytics.

| Version | Date | Correctifs |
|---|---|---|
| 1.0.53 | 13 Mai 2026 | <ul><li>Calcule les tailles des ressources dans un payload de requête et envoie dynamiquement la quantité maximale de ressources possible, afin de réduire le nombre total de requêtes envoyées et d’éviter toute erreur « 413 Contenu trop volumineux ».</li><li>Effectue le suivi des ressources où CSS charge les images en arrière-plan d’un élément dans le DOM et tient correctement compte des images d’arrière-plan CSS avec des attributs src vides.</li><li>Ajout d’un tableau de `permanentlyBlockedURLs` codé en dur contenant `maps.googleapis.com` et `mapsresources-pa.googleapis.com`. Ces URL sont toujours bloquées et il s’agit d’un paramètre par défaut dans la bibliothèque Content Analytics.</li><li>Ajout de champs `idSource` et `channel` à la demande de collecte de données XDM.</li></ul> |
| 1.0.51 | 13 Mars 2026 | <ul><li>Correction d’un bug mineur qui entraînait la mise en cache de `experienceIDs` lors de la navigation entre les pages.</li><li>Correction d’un problème lié à la capture des paramètres de chaîne de requête d’expérience. Les paramètres de requête fonctionnent comme suit :<ul><li>Le champ Paramètres de requête est vide : aucun paramètre de chaîne de requête n’est capturé dans l’ID d’expérience.</li><li>Les paramètres de requête sont explicitement définis (par exemple, un, deux, trois) : seuls ces paramètres et valeurs de chaîne de requête sont capturés dans l’ID d’expérience.</li><li>Le paramètre de requête est défini sur un caractère générique (`.*`) : l’intégralité de la chaîne document.location.search est incluse dans l’URL.</li></ul></li></ul> |
| 1.0.49 | 12 Septembre 2025 | <ul><li>Correction d’un bug mineur en raison duquel l’interface utilisateur de l’extension de balises ne se chargeait pas du tout si l’utilisateur ou l’utilisatrice ne disposait pas des autorisations relatives aux trains de données. L’interface utilisateur affiche désormais un avertissement d’autorisation dans l’option de flux de données **[!UICONTROL Choose from list]** et permet toujours à l’utilisateur de saisir manuellement des valeurs.</li><li>Mise à jour d&#39;un problème de chemin pour l10n.</li><li>Correction d’un problème en raison duquel certaines images qui étaient des éléments enfants de parents non-images ne capturaient pas correctement les clics sur les ressources pour ces éléments d’image enfants.</li><li>Si un utilisateur a configuré le SDK Web dans des balises avec un nom d’instance différent de `alloy`, la bibliothèque Content Analytics détectera la première instance de la bibliothèque SDK Web et l’utilisera pour envoyer des événements Content Analytics.</li></ul> |
| 1.0.48 | 25 Août 2025 | <ul><li>Ajoute la prise en charge du suivi des ressources dans les éléments DOM shadow-root d’un document.</li></ul> |
| 1.0.47 | 23 Juil 2025 | <ul><li>Correction d’un bug qui se produisait lorsque les expériences n’étaient pas activées, ce qui entraînait l’échec de la vérification des expériences par l’expression régulière. Ce problème empêchait la collecte de données Content Analytics.</li><li>Correction d’un problème lié au paramètre de langue par défaut qui empêchait l’affichage de l’interface utilisateur des balises pour certains utilisateurs dont la langue principale par défaut n’était pas définie dans Experience Cloud.</li></ul> |
| 1.0.46 | 18 Juin 2025 | <ul><li>Ajout d’une notification toast lors de la tentative d’enregistrement de la configuration de l’extension, si un flux de données de production est absent.</li><li>Correction temporaire du problème de visibilité de la payload de Content Analytics en plaçant le contenu de la payload singulièrement renforcée dans la console.</li><li>Ajout de la localisation à l’interface utilisateur de l’extension.</li><li>Correction partielle d’un problème CSS qui entraînait une marge intérieure supplémentaire autour du contenu de l’interface utilisateur de l’extension.</li></ul> |
| 1.0.45 | 14 Avril 2025 | <ul><li>Correction de plusieurs bugs dans les paramètres de configuration liés à la conservation d’événements Content Analytics en attente d’événements de page vue. Par défaut, Content Analytics attend désormais que le PREMIER événement de page vue se produise avant de déclencher des événements.</li></ul> |
| 1.0.44 | 31 Mars 2025 | <ul><li>Première itération de l’intégration AppMeasurement.</li><li>Cette version ne prend pas encore en charge le filtrage de requêtes spécifiques (par exemple, les pages vues), mais cette fonctionnalité peut être ajoutée lors d’une prochaine mise à jour. Il utilise actuellement la première instance AppMeasurement trouvée sur la page.</li></ul> |
| 1.0.43 | 10 Mars 2025 | <ul><li>Version initiale de l’extension.</li></ul> |
