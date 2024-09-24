---
title: Guide de questions pour l’assistant d’IA
description: Lisez ce document pour découvrir des exemples de questions que vous pouvez utiliser lors de l’interrogation de l’assistant d’IA.
exl-id: d16d1262-cc2d-45c9-94c4-b86132183442
source-git-commit: 0926a0e8c7ae560bf5f4f9ff6853b191af047738
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 1%

---

# Guide de questions pour l’assistant d’IA

Lisez ce document pour obtenir un ensemble d’exemples de questions que vous pouvez utiliser lors de l’interrogation de l’assistant d’IA.

Vous pouvez également utiliser ce document pour obtenir des conseils sur [la manière d&#39;adresser vos questions](#phrasing-your-questions) afin d&#39;obtenir des réponses optimales de l&#39;assistant d&#39;IA.

## Questions basées sur des objectifs {#objectives-questions}

Les exemples de questions suivants sont regroupées par objectifs que vous pouvez atteindre lorsque vous utilisez l’assistant d’IA :

| Objectif | Description | Exemple |
| --- | --- | --- |
| Concepts d’apprentissage et workflows continus | <ul><li>En tant qu’utilisateur novice, vous pouvez utiliser l’assistant d’IA pour découvrir les concepts de Real-Time CDP et de Adobe Journey Optimizer et vous inscrire à des produits et fonctionnalités que vous ne connaissez pas.</li><li>En tant qu’utilisateur expérimenté, vous pouvez utiliser l’assistant d’IA pour résoudre un cas de périphérique qui bloque peut-être votre workflow. | <ul><li>Comment configurer un tableau de bord dans Parcours Analytics ?</li><li>Indiquez-moi quelques cas d’utilisation pour Real-Time CDP.</li></ul> |
| Dépannage | Utilisez l’assistant d’IA pour découvrir comment déboguer les erreurs de base que vous pouvez rencontrer dans votre workflow. | <ul><li>Que signifie cette erreur {ERROR_MESSAGE} ?</li><li>Pourquoi ne puis-je pas supprimer l’audience nommée &quot;Luma : Email Audience&quot; ?</li></ul> |
| hygiène des environnements de test | Utilisez l’assistant d’IA pour identifier les doublons ou les objets inutilisés afin de gérer efficacement votre environnement de test. | <ul><li>Pouvez-vous me montrer des audiences qui sont similaires ?</li><li>Existe-t-il des schémas qui n’ont pas de jeu de données associé ?</li></ul> |
| Analyse de valeur | Utilisez l’assistant d’IA pour identifier les objets de données les plus utilisés et évaluer les indicateurs de performances ou rechercher les objets de données les plus précieux. | <ul><li>Combien de profils se trouvent dans notre définition de segment &quot;Luma: Email Audience&quot; ?</li><li>Quand les audiences ont-elles été activées vers la destination Audiences Experience Cloud ?</li></ul> |
| Recherche | Utilisez l’assistant d’IA pour rechercher les objets Experience Platform pris en charge tels que les audiences, les jeux de données, les destinations, les schémas et les sources. | <ul><li>Répertorier les audiences contenant &quot;Luma&quot; dans le nom qui ont été créées au cours du dernier trimestre.</li><li>Quels attributs se trouvent dans le schéma XDM &quot;Luma: Custom Actions&quot; ?</li></ul> |
| Analyse de l’impact | Utilisez l’assistant d’IA pour identifier les objets de données qui ont été utilisés dans certains workflows afin que vous puissiez évaluer l’impact de toute modification. | <ul><li>Quelles audiences utilisent `homeAddress.city` dans le schéma &quot;Luma: PersonProfiles&quot; ?</li><li>Dans quels jeux de données l’attribut de profil `consents.marketing.push.val` est-il stocké ?</li></ul> |

{style="table-layout:auto"}

## Connaissances opérationnelles par entité et questions sur les connaissances des produits{#objects-questions}

Les questions suivantes sont regroupées par objet de données et classées comme [informations opérationnelles](./home.md#operational-insights) ou [connaissance du produit](./home.md#product-knowledge).

![](./images/prompt.png)

* **Audiences - insights opérationnels**
   * Quelles audiences utilisent d’autres audiences ?
   * Quelle est la distribution du nombre de profils entre les audiences ?
   * Montrez-moi les audiences qui ont été modifiées pour la dernière fois avant {RELATIVE_DATE}.
   * Quelles audiences ont 0 profil ?
   * {USE_AUTO_COMPLETE_TO_FILL_AUDIENCE_NAME} est-il utilisé dans d’autres audiences ?
* **Attributs - insights opérationnels**
   * Quelles audiences ont l’attribut xdm {ATTRIBUTE_PATH} dans leur définition de segment ?
   * Combien d’attributs de schéma XDM ne sont pas utilisés dans les audiences ?
   * Quels schémas comportent l’attribut xdm {ATTRIBUTE_PATH} ?
   * Quels attributs XDM sont activés ?
   * Quels attributs XDM sont utilisés dans les audiences avec plus de 10 profils ?
* **Flux de données - insights opérationnels**
   * Quels flux de données contribuent au jeu de données {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME} ?
   * Quels flux de données sources ne sont pas utilisés ou ne contiennent plus de données ?
   * Liste des flux de données source dont je dispose.
   * Quels flux de données sont configurés pour chaque connecteur source ?
* **Jeux de données - insights opérationnels**
   * Combien de jeux de données ont été ingérés à l’aide du même schéma ?
   * Quel connecteur source est associé à un jeu de données {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME} ?
   * Quels jeux de données sont utilisés dans chaque audience ?
   * Quels schémas ne sont utilisés dans aucun jeu de données ?
   * Combien de jeux de données ai-je ?
* **Destinations - insights opérationnels**
   * Quelles destinations sont à l’état actif ?
   * Quels comptes de destination ont 0 audience activée ?
   * Combien d’audiences sont activées pour chaque destination ?
   * Quelles destinations ont le plus grand nombre d’audiences activées ?
* **Parcours - insights opérationnels**
   * Combien de parcours ai-je ?
   * Quels parcours ont été créés dans {RELATIVE_DATE} (par exemple, la dernière semaine) ou {RELATIVE_DATE} (par exemple, avant/après/à une date spécifique) ?
   * Me montrer la liste des parcours qui ont été modifiés dans {RELATIVE_DATE} (par exemple la dernière semaine) ou {RELATIVE_DATE} (par exemple, avant/après/à une date spécifique) ?
   * Liste des parcours vivants que j&#39;ai.
   * Répertorier les audiences utilisées dans les parcours en direct.
* **Sources - insights opérationnels**
   * Quelles sont les sources actives ?
   * Quel connecteur source est associé au jeu de données {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}.
   * Quel est le connecteur source qui a le plus grand nombre de comptes associés ?
   * Montrez-moi les flux de données et leurs connecteurs source associés.
* **Apprentissage pointé - Connaissances produit (Real-Time CDP et Journey Optimizer)**
   * Que sont les audiences semblables ?
   * Comment les groupes d’utilisateurs sont-ils liés aux rôles ?
   * Quand dois-je utiliser un type de données par rapport à un groupe de champs ?
   * Quelle est la différence entre une identité et une clé primaire ou étrangère ?
* **Dépannage - Connaissances produit (Real-Time CDP et Journey Optimizer)**
   * En quoi l’assistant IA peut-il vous aider ?
   * Puis-je supprimer un schéma activé pour le profil une fois les données ingérées ?
   * Pourquoi ne puis-je pas supprimer une audience ?
   * Combien de temps faut-il pour que les audiences soient évaluées et que les résultats soient disponibles pour le ciblage ?

## Expression de vos questions {#phrasing-your-questions}

Vous devez envoyer vos questions à l’assistant d’IA avec clarté et contexte afin d’obtenir une réponse aussi précise que possible. Reportez-vous à la liste suivante de conseils pour savoir comment poser une question claire avec contexte :

* Exposez votre tâche et/ou votre question de manière concise.
* Évitez d’utiliser un langage ambigu ou une syntaxe trop complexe pour faciliter la compréhension.
* Fournissez un contexte pertinent concernant votre tâche et/ou votre question, car le contexte peut aider l’assistant d’IA à générer des réponses plus pertinentes.

Lisez les tableaux ci-dessous pour plus d’informations sur les bonnes pratiques à suivre lorsque vous posez des questions à l’assistant d’IA.

Les tableaux suivants décrivent les bonnes pratiques que vous pouvez suivre lors de l’utilisation de l’assistant d’IA :

| Do | Exemple |
| --- | --- |
| <ul><li>Soyez précis sur l’objet ou les informations que vous souhaitez récupérer ou analyser.</li><li>Essayez de placer les noms des objets de données entre guillemets. Si vous ne connaissez qu’une partie du nom de l’objet, vous pouvez également l’indiquer dans la question.</li><li>Utilisez la [saisie automatique d’objet](./ui-guide.md#use-auto-complete) pour aider l’assistant d’IA à mieux comprendre le contexte de votre requête.</li></ul> | <ul><li>Quels jeux de données utilisent le schéma &quot;Luma - Loyalty&quot; ?</li><li>Montrez-moi les segments activés dont le nom contient &quot;Luma&quot;. Classement par nombre de profils.</li></ul> |
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

## Exemples de questions non prises en charge {#unsupported-questions}

Vous trouverez ci-dessous une liste d’exemples de questions qui ne sont actuellement pas prises en charge par l’assistant d’IA.

+++Sélectionner pour afficher des exemples de questions non prises en charge

### Informations opérationnelles

* Combien de profils de cet environnement de test vivent en Californie ? (**Remarque** : pour des questions similaires, vous devez fournir un critère spécifique afin de donner suffisamment de contexte à votre requête. Dans ce cas, le critère spécifique est &quot;En situation de vie en Californie&quot;).
* Dans quels segments se trouve ce profil {PROFILE_INFO/ATTRIBUTE_VALUE} ?
* Combien de profils du jeu de données comportent un email ?
* Quel jeu de données représente le nombre maximal de profils dans cet environnement de test ?
* Quel jeu de données possède le plus grand nombre d’enregistrements ?
* Combien de segments ont été supprimés dans {RELATIVE_DATE} ?
* Lequel de mes jeux de données a la plus grande taille ?
* Donnez-moi un profil dans le {AUDIENCE_NAME}.
* Quel est le nombre total de profils dans mon environnement de test ?
* Combien d’espaces de noms d’identité sont associés à l’audience {AUDIENCE_NAME} ?
* M’afficher un rapport de tous les segments d’audience qui ont été évalués aujourd’hui ;
* Combien de segments comportent des profils se chevauchant ?
* Nombre de lots chargés dans {DATASET_NAME}
* Combien d’offres actives ai-je ?
* Combien de campagnes actives ai-je ?
* D’où proviennent mes sources de données ?
* Quel est le jeu de données ou la source de données le plus important ?
* Puis-je obtenir la liste des utilisateurs qui ont créé ces schémas ?

### Dépannage

* Pourquoi ce lot {BATCH_NAME/BATCH_ID} est-il toujours en cours de traitement ?
* Pourquoi personne ne se qualifie-t-il pour cette audience {AUDIENCE_NAME} ?
* Je ne suis pas en mesure de voir Customer AI, pourquoi et comment le corriger ?
* Je ne parviens pas à voir l’aperçu du jeu de données, pourquoi et comment le corriger ?
* Pourquoi ne puis-je pas supprimer {SEGMENT/DATASET/SCHEMA_NAME} ?
* Ai-je accès à Query Service ?

### Tâche et automatisation

* Écrivez une requête qui me donne un enregistrement de {DATASET_NAME}.
* Rédigez un exemple d’appel API à /schemas/{schemaId}/fields/{fieldPath}/values.
* Configurez une source/destination pour moi.
* Créez une audience pour moi avec les critères {USER_SPECIFIC_CRITERIA}.

+++

## Étapes suivantes

En lisant ce document, vous savez maintenant comment optimiser vos questions pour l’assistant d’IA. Pour plus d’informations sur l’utilisation de la fonctionnalité pendant vos workflows, consultez le [guide de l’interface utilisateur de l’assistant d’IA](ui-guide.md).
