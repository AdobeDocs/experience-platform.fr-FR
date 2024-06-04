---
title: Guide de questions pour l’assistant d’IA
description: Lisez ce document pour découvrir des exemples de questions que vous pouvez utiliser lors de l’interrogation de l’assistant d’IA.
source-git-commit: a1092e21940c5e4ba9b598bc51ba1243b57a0051
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 0%

---

# Guide de questions pour l’assistant d’IA

Lisez ce document pour obtenir un ensemble d’exemples de questions que vous pouvez utiliser lors de l’interrogation de l’assistant d’IA.

Vous pouvez également utiliser ce document pour obtenir des conseils sur les [comment formuler vos questions](#phrasing-your-questions) pour obtenir des réponses optimales de la part de l’assistant d’IA.

## Questions basées sur des objectifs {#objectives-questions}

Les exemples de questions suivants sont regroupées par objectifs que vous pouvez atteindre lorsque vous utilisez l’assistant d’IA :

| Objectif | Description | Exemple |
| --- | --- | --- |
| Concepts d’apprentissage et workflows continus | <ul><li>En tant qu’utilisateur novice, vous pouvez utiliser l’assistant d’IA pour découvrir les concepts de Real-Time CDP et de Adobe Journey Optimizer et vous inscrire à des produits et fonctionnalités que vous ne connaissez pas.</li><li>En tant qu’utilisateur expérimenté, vous pouvez utiliser l’assistant d’IA pour résoudre un cas de périphérique qui bloque peut-être votre workflow. | <ul><li>Comment configurer un tableau de bord dans Parcours Analytics ?</li><li>Indiquez-moi quelques cas d’utilisation pour Real-Time CDP.</li></ul> |
| Dépannage | Utilisez l’assistant d’IA pour découvrir comment déboguer les erreurs de base que vous pouvez rencontrer dans votre workflow. | <ul><li>Que fait cette erreur ? {ERROR_MESSAGE} vous voulez dire ?</li><li>Pourquoi ne puis-je pas supprimer l’audience nommée &quot;Luma : Email Audience&quot; ?</li></ul> |
| hygiène des environnements de test | Utilisez l’assistant d’IA pour identifier les doublons ou les objets inutilisés afin de gérer efficacement votre environnement de test. | <ul><li>Pouvez-vous me montrer des audiences qui sont similaires ?</li><li>Existe-t-il des schémas qui n’ont pas de jeu de données associé ?</li></ul> |
| Analyse de valeur | Utilisez l’assistant d’IA pour identifier les objets de données les plus utilisés et évaluer les indicateurs de performances ou rechercher les objets de données les plus précieux. | <ul><li>Combien de profils se trouvent dans notre définition de segment &quot;Luma: Email Audience&quot; ?</li><li>Quand les audiences ont-elles été activées vers la destination Audiences Experience Cloud ?</li></ul> |
| Recherche | Utilisez l’assistant d’IA pour rechercher les objets Experience Platform pris en charge tels que les audiences, les jeux de données, les destinations, les schémas et les sources. | <ul><li>Répertorier les audiences contenant &quot;Luma&quot; dans le nom qui ont été créées au cours du dernier trimestre.</li><li>Quels attributs se trouvent dans le schéma XDM &quot;Luma: Custom Actions&quot; ?</li></ul> |
| Analyse de l’impact | Utilisez l’assistant d’IA pour identifier les objets de données qui ont été utilisés dans certains workflows afin que vous puissiez évaluer l’impact de toute modification. | <ul><li>Quelles audiences utilisent `homeAddress.city` dans le schéma &quot;Luma: PersonProfiles&quot; ?</li><li>Quels jeux de données sont les `consents.marketing.push.val` attribut de profil stocké dans ?</li></ul> |

{style="table-layout:auto"}

## Connaissances opérationnelles par entité et questions sur les connaissances des produits{#objects-questions}

Les questions suivantes sont regroupées par objet de données et classées comme [informations opérationnelles](./home.md#operational-insights) ou [connaissance du produit](./home.md#product-knowledge).

| Objet | Description |
| --- | --- |
| Audiences - Aperçu opérationnel | <ul><li>Quelles audiences utilisent d’autres audiences ?</li><li>Quelle est la distribution du nombre de profils entre les audiences ?</li><li>Me montrer les audiences qui ont été modifiées pour la dernière fois avant {RELATIVE_DATE}.</li><li>Quelles audiences ont 0 profil ?</li><li>Is {USE_AUTOCOMPLETE_TO_FILL_AUDIENCE_NAME} utilisé dans d’autres audiences ?</li></ul> |
| Attributs - insights opérationnels | <ul><li>Quelles audiences ont un attribut XDM ? {ATTRIBUTE_PATH} dans leur définition de segment ?</li><li>Combien d’attributs de schéma XDM ne sont pas utilisés dans les audiences ?</li><li>Quels schémas ont un attribut XDM ? {ATTRIBUTE_PATH} en eux ?</li><li>Quels attributs XDM sont activés ?</li><li>Les attributs XDM utilisés dans les audiences ayant plus de 10 profils</li></ul> |
| Flux de données - Informations opérationnelles | <ul><li>Quels flux de données contribuent à {DATASET_NAME} jeu de données ?</li><li>Quels flux de données sources ne sont pas utilisés ou ne contiennent plus de données ?</li><li> |
| Jeux de données - insights opérationnels | <ul><li>Combien de jeux de données ont été ingérés à l’aide du même schéma ?</li><li>Quel connecteur source est associé à {DATASET_NAME} dataset></li><li>Quels jeux de données sont utilisés dans chaque audience ?</li><li>Quels schémas ne sont utilisés dans aucun jeu de données ?</li><li>Combien de jeux de données ai-je ?</li></ul> |
| Destinations - insights opérationnels | <ul><li>Quelles destinations sont à l’état actif ?</li><li>Quels comptes de destination ont 0 audience activée ?</li><li> |
| Parcours - insights opérationnels | <ul><li>Combien de parcours ai-je ?</li><li>Les parcours créés dans {RELATIVE_DATE} (par exemple, la semaine dernière) ou {RELATIVE_DATE} (par exemple, avant/après/à une date spécifique) ?</li><li>Afficher la liste des parcours qui ont été modifiés dans {RELATIVE_DATE} (par exemple, la semaine dernière) ou {RELATIVE_DATE} (par exemple, avant/après/à une date spécifique) ?</li><li>Liste les parcours que j&#39;ai.</li><li>Répertorier les audiences utilisées dans les parcours en direct.</li></ul> |
| Schémas - insights opérationnels | <ul><li>Quels champs du schéma ont contribué au plus grand nombre d’audiences ?</li><li>Combien de schémas le profil est-il activé ?</li><li>Liste de tous les schémas modifiés la semaine dernière.</li><li>Quels schémas ne sont utilisés dans aucun jeu de données ?</li><li>Liste de tous les schémas créés la semaine dernière.</li></ul> |
| Sources - insights opérationnels | <ul><li>Quelles sont les sources actives ?</li><li>Quel connecteur source est associé à un jeu de données ? {DATASET_NAME}?</li><li>Quel est le connecteur source qui a le plus grand nombre de comptes associés ?</li><li>Montrez-moi les flux de données et leurs connecteurs source associés.</li></ul> |
| Apprentissage en points - Connaissances produit (Real-Time CDP et Journey Optimizer) | <ul><li>Avec quoi l’assistant d’IA peut-il vous aider ?</li><li>Que sont les audiences semblables ?</li><li>Comment les groupes d’utilisateurs sont-ils liés aux rôles ?</li><li>Quand dois-je utiliser un type de données par rapport à un groupe de champs ?</li><li>Quelle est la différence entre une identité et une clé primaire ou étrangère ?</li><li>Comment est calculé la richesse des profils ?</li></ul> |
| Dépannage - Connaissances produit (Real-Time CDP et Journey Optimizer) | <ul><li>Avec quoi l’assistant d’IA peut-il vous aider ?</li><li>Puis-je supprimer un schéma activé par le profil une fois les données ingérées ?</li><li>Pourquoi ne puis-je pas supprimer une audience ?</li><li>Combien de temps faut-il pour que les audiences soient évaluées et que les résultats soient disponibles pour le ciblage ?</li></ul> |

{style="table-layout:auto"}

## Expression de vos questions {#phrasing-your-questions}

Vous devez envoyer vos questions à l’assistant d’IA avec clarté et contexte afin d’obtenir une réponse aussi précise que possible. Reportez-vous à la liste suivante de conseils pour savoir comment poser une question claire avec contexte :

* Exposez votre tâche et/ou votre question de manière concise.
* Évitez d’utiliser un langage ambigu ou une syntaxe trop complexe pour faciliter la compréhension.
* Fournissez un contexte pertinent concernant votre tâche et/ou votre question, car le contexte peut aider l’assistant d’IA à générer des réponses plus pertinentes.

Lisez les tableaux ci-dessous pour plus d’informations sur les bonnes pratiques à suivre lorsque vous posez des questions à l’assistant d’IA.

Les tableaux suivants décrivent les bonnes pratiques que vous pouvez suivre lors de l’utilisation de l’assistant d’IA :

| Do | Exemple |
| --- | --- |
| <ul><li>Soyez précis sur l’objet ou les informations que vous souhaitez récupérer ou analyser.</li><li>Essayez de placer les noms des objets de données entre guillemets. Si vous ne connaissez qu’une partie du nom de l’objet, vous pouvez également l’indiquer dans la question.</li><li>Utilisation [saisie automatique d’objet](./ui-guide.md#use-auto-complete) pour aider l’assistant d’IA à mieux comprendre le contexte de votre requête.</li></ul> | <ul><li>Quels jeux de données utilisent le schéma &quot;Luma - Loyalty&quot; ?</li><li>Montrez-moi les segments activés dont le nom contient &quot;Luma&quot;. Classement par nombre de profils.</li></ul> |
| <ul><li>Éviter l’ambiguïté et utiliser un langage clair</li><li>Utilisez une terminologie précise pour une meilleure clarté dans votre requête.</li><li>Lorsque vous posez des questions concernant Adobe Experience Platform, essayez d’utiliser une terminologie spécifique à Experience Platform afin d’améliorer la pertinence des réponses.</li></ul> | <ul><li>Combien de profils ai-je dans &quot;Audience ACME&quot; ?</li><li>Montrez-moi les 5 premiers attributs XDM utilisés dans les audiences activées.</li></ul> |
| <ul><li>Précisez un contexte ou spécifiez un critère pour filtrer vos résultats.</li><li>Utilisez un critère de filtrage dans les questions pour limiter le volume de données dans la réponse.</li></ul> | <ul><li>Montrez-moi les audiences qui n’ont pas été activées et qui ont été créées il y a plus de 6 mois et n’ont jamais été modifiées.</li><li>Affichez-moi les audiences activées vers &quot;destination ACME&quot; et qui ont plus de 10 000 profils.</li></ul> |

{style="table-layout:auto"}

| Ne le faites pas | Exemple |
| --- | --- |
| Utilisez un langage vague ou ambigu. | <ul><li>Donnez-moi des informations sur les jeux de données.</li><li>Combien d’utilisateurs ai-je dans &quot;Audience ACME&quot; ?</li><li>Afficher les segments.</li><li>Attributs de liste.</li></ul> |
| Effectuez des requêtes incomplètes. | &quot;Luma - Jeu de données de fidélité&quot; |
| Prenons le savoir sans contextes. | <ul><li>Audiences des 6 derniers mois.</li><li>Construisez une requête pour moi.</li></ul> |
| Formuler des requêtes trop complexes. | Fournissez une analyse complète de la liaison des données entre tous les objets et leurs dépendances. |
| Omission des critères ou des paramètres. | Montrez-moi des jeux de données. |

{style="table-layout:auto"}

## Étapes suivantes

En lisant ce document, vous savez maintenant comment optimiser vos questions pour l’assistant d’IA. Pour plus d’informations sur l’utilisation de la fonctionnalité pendant vos workflows, consultez la section [Guide de l’interface utilisateur de l’assistant IA](ui-guide.md).
