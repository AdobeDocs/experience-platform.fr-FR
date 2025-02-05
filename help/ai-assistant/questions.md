---
title: Guide de questions pour l’assistant IA
description: Lisez ce document pour découvrir des exemples de questions que vous pouvez utiliser lors de l’interrogation de l’assistant AI.
exl-id: d16d1262-cc2d-45c9-94c4-b86132183442
source-git-commit: 7268895d0b1924f9d3e7cee24e549c79245ef099
workflow-type: tm+mt
source-wordcount: '2105'
ht-degree: 0%

---

# Guide de questions pour l’assistant IA

Lisez ce document pour obtenir un ensemble d’exemples de questions que vous pouvez utiliser lors de l’interrogation de l’assistant AI.

Vous pouvez également utiliser ce document pour obtenir des conseils sur [comment formuler vos questions](#phrasing-your-questions) afin d’obtenir des réponses optimales de la part de l’assistant d’IA.

## Questions basées sur des objectifs {#objectives-questions}

Les exemples de questions suivants sont regroupés par objectifs que vous pouvez atteindre lors de l’utilisation de l’assistant AI :

| Objectif | Description | Exemple |
| --- | --- | --- |
| Apprendre les concepts et poursuivre les workflows | <ul><li>En tant qu’utilisateur débutant, vous pouvez utiliser l’assistant AI pour apprendre les concepts de Real-Time CDP et de Adobe Journey Optimizer et vous intégrer à des produits et fonctionnalités que vous ne connaissez pas.</li><li>En tant qu’utilisateur expérimenté, vous pouvez utiliser l’assistant AI pour résoudre un cas de figure susceptible de bloquer votre workflow. | <ul><li>Comment configurer un tableau de bord dans Parcours Analytics ?</li><li>Racontez-moi quelques cas d’utilisation pour Real-Time CDP.</li></ul> |
| Dépannage | Utilisez l’assistant AI pour savoir comment déboguer les erreurs de base que vous pouvez rencontrer dans votre workflow. | <ul><li>Que signifie cette erreur {ERROR_MESSAGE} ?</li><li>Pourquoi ne puis-je pas supprimer l’audience nommée « Luma : audience de l’e-mail » ?</li></ul> |
| Hygiène des sandbox | Utilisez l’assistant AI pour identifier les doublons ou les objets inutilisés afin de gérer efficacement votre sandbox. | <ul><li>Pouvez-vous m’afficher des audiences similaires ?</li><li>Existe-t-il des schémas auxquels aucun jeu de données n’est associé ?</li></ul> |
| Analyse des valeurs | Utilisez l’assistant AI pour identifier les objets de données les plus utilisés et évaluer les indicateurs de performance ou trouver les objets de données les plus précieux. | <ul><li>Combien de profils se trouvent dans notre définition de segment « Luma : Audience d’e-mail » ?</li><li>Quand les audiences ont-elles été activées vers la destination Audiences Experience Cloud ?</li></ul> |
| Recherche | Utilisez l’assistant AI pour rechercher les objets Experience Platform pris en charge tels que les audiences, les jeux de données, les destinations, les schémas et les sources. | <ul><li>Répertoriez les audiences dont le nom contient « Luma » et qui ont été créées au cours du dernier trimestre.</li><li>Quels sont les attributs du schéma XDM « Luma : actions personnalisées » ?</li></ul> |
| Analyse d&#39;impact | Utilisez l’assistant AI pour identifier les objets de données qui ont été utilisés dans certains workflows afin de pouvoir évaluer l’impact de toute modification. | <ul><li>Quelles audiences utilisent `homeAddress.city` dans le schéma « Luma : PersonProfiles » ?</li><li>Dans quels jeux de données l’attribut de profil `consents.marketing.push.val` est-il stocké ?</li></ul> |

{style="table-layout:auto"}

## Questions relatives aux informations opérationnelles par entité et à la connaissance des produits{#objects-questions}

Les questions suivantes sont regroupées par objet de données et sont classées [informations opérationnelles](./home.md#operational-insights) ou [connaissance du produit](./home.md#product-knowledge).

![](./images/prompt.png)

* **Audiences - Informations opérationnelles**
   * Quelles audiences utilisent d’autres audiences ?
   * Quelle est la répartition du nombre de profils entre les audiences ?
   * Afficher les audiences qui ont été modifiées pour la dernière fois avant {RELATIVE_DATE}.
   * Quelles audiences ont 0 profil ?
   * Le {USE_AUTO_COMPLETE_TO_FILL_AUDIENCE_NAME} est-il utilisé dans d’autres audiences ?
* **Attributs - Informations opérationnelles**
   * Quelles audiences ont des {ATTRIBUTE_PATH} d’attribut xdm dans leur définition de segment ?
   * Combien d’attributs de schéma XDM ne sont utilisés dans aucune audience ?
   * Quels schémas contiennent des {ATTRIBUTE_PATH} d’attributs xdm ?
   * Quels attributs XDM sont activés ?
   * Quels attributs XDM sont utilisés dans les audiences avec plus de 10 profils ?
* **Flux de données - Informations opérationnelles**
   * Quels flux de données contribuent à {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME} jeu de données ?
   * Quels flux de données source ne sont pas utilisés ou n’ont plus de données entrantes ?
   * Répertorier les flux de données sources dont je dispose
   * Quels flux de données sont configurés pour chaque connecteur source ?
* **Jeux de données - Informations opérationnelles**
   * Combien de jeux de données ont été ingérés à l’aide du même schéma ?
   * Quel connecteur source est associé à {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME} jeu de données ?
   * Quels jeux de données sont utilisés dans chaque audience ?
   * Quels schémas ne sont utilisés dans aucun jeu de données ?
   * De combien de jeux de données dispose-t-on ?
* **Destinations - Informations opérationnelles**
   * Quelles destinations sont à l’état actif ?
   * Quels comptes de destination ont 0 audience activée ?
   * Combien d’audiences sont activées pour chaque destination ?
   * Quelles destinations ont le plus grand nombre d’audiences activées ?
* **Parcours - Informations opérationnelles**
   * Combien de parcours ai-je ?
   * Quels parcours ont été créés en {RELATIVE_DATE} (par exemple la semaine dernière) ou en {RELATIVE_DATE} (par exemple avant/après/à une date spécifique) ?
   * Me montrer la liste des parcours qui ont été modifiés en {RELATIVE_DATE} (par exemple la semaine dernière) ou en {RELATIVE_DATE} (par exemple avant/après/à une date spécifique) ?
   * Répertoriez les parcours en direct que j’ai.
   * Répertoriez les audiences utilisées dans les parcours en direct.
* **Sources - Informations opérationnelles**
   * Quelles sources sont actives ?
   * Connecteur source associé au jeu de données {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}.
   * Quel connecteur source a le plus grand nombre de comptes associés ?
   * Afficher les flux de données et les connecteurs source associés.
* **Apprentissage par points - connaissance des produits (Real-Time CDP et Journey Optimizer)**
   * Que sont les audiences semblables ?
   * Comment les groupes d’utilisateurs sont-ils liés aux rôles ?
   * Quand dois-je utiliser un type de données par rapport à un groupe de champs ?
   * Quelle est la différence entre une identité et une clé primaire ou étrangère ?
* **Dépannage - Connaissance des produits (Real-Time CDP et Journey Optimizer)**
   * En quoi l’assistant IA peut-il vous aider ?
   * Puis-je supprimer un schéma activé pour le profil après l’ingestion des données ?
   * Pourquoi ne puis-je pas supprimer une audience ?
   * Combien de temps faut-il pour que les audiences soient évaluées et que les résultats soient disponibles pour le ciblage ?

## Formulation de vos questions {#phrasing-your-questions}

Vous devez formuler vos questions à l’assistant AI avec clarté et contexte afin d’obtenir une réponse aussi précise que possible. Consultez la liste suivante de conseils pour savoir comment poser une question claire avec du contexte :

* Exposez votre tâche et/ou question de façon concise.
* Évitez le langage ambigu ou une syntaxe trop complexe pour faciliter la compréhension.
* Fournissez un contexte pertinent concernant votre tâche et/ou question, car le contexte peut aider l’assistant d’IA à générer des réponses plus pertinentes.

Lisez les tableaux ci-dessous pour obtenir de plus amples conseils sur les bonnes pratiques à suivre lorsque vous posez des questions à l’assistant AI.

Les tableaux suivants décrivent les bonnes pratiques que vous pouvez suivre lors de l’utilisation de l’assistant AI :

| Faire | Exemple |
| --- | --- |
| <ul><li>Soyez précis quant à l’objet ou aux informations que vous souhaitez récupérer ou analyser.</li><li>Essayez de placer les noms des objets de données entre guillemets. Si vous ne connaissez qu’une partie du nom de l’objet, vous pouvez également la spécifier dans la question.</li><li>Utilisez la [saisie automatique d’objet](./ui-guide.md#use-auto-complete) pour aider l’assistant AI à mieux comprendre le contexte de votre requête.</li></ul> | <ul><li>Quels jeux de données utilisent le schéma « Luma - Fidélité » ?</li><li>Afficher les segments activés dont le nom contient « Luma ». Classez-les par nombre de profils.</li></ul> |
| <ul><li>Évitez toute ambiguïté et utilisez un langage clair</li><li>Utilisez une terminologie précise pour garantir une meilleure clarté dans votre requête.</li><li>Lorsque vous posez des questions concernant Adobe Experience Platform, utilisez une terminologie spécifique à l’Experience Platform afin d’améliorer la pertinence des réponses.</li></ul> | <ul><li>Combien de profils ai-je dans « Audience ACME » ?</li><li>Afficher les 5 principaux attributs XDM utilisés dans les audiences activées.</li></ul> |
| <ul><li>Fournissez un contexte ou spécifiez un critère pour filtrer vos résultats.</li><li>Utilisez un critère de filtre dans les questions pour limiter le volume de données dans la réponse.</li></ul> | <ul><li>Afficher les audiences qui n’ont pas été activées et qui ont été créées il y a plus de 6 mois et qui n’ont jamais été modifiées.</li><li>Montrez-moi les audiences activées vers la « destination ACME » et qui ont plus de 10000 profils.</li></ul> |

{style="table-layout:auto"}

| Ne pas | Exemple |
| --- | --- |
| Utilisez un langage vague ou ambigu. | <ul><li>Me donner des informations sur les jeux de données.</li><li>Combien d’utilisateurs ai-je dans « Audience ACME » ?</li><li>Afficher les segments.</li><li>Attributs de liste.</li></ul> |
| Effectuer des demandes incomplètes | « Luma - Jeu De Données De Fidélité » |
| Supposons des connaissances sans contextes. | <ul><li>Audiences des 6 derniers mois.</li><li>Créez une requête pour moi.</li></ul> |
| Formulez des requêtes trop complexes. | Fournissez une analyse complète de la parenté des données sur tous les objets et leurs dépendances. |
| Omettre les critères ou les paramètres. | Afficher les jeux de données. |

{style="table-layout:auto"}

## Observabilité des jeux de données {#dataset-observability}

L’assistant AI peut désormais répondre à des questions sur des mesures de jeux de données spécifiques, telles que la taille de stockage et le nombre de lignes.

* Quels sont mes plus grands jeux de données par taille ?
* Quels sont mes jeux de données les plus volumineux par ligne ?
* Combien de jeux de données sont vides ?
* Quels jeux de données sont vides ?

De plus, vous pouvez transmettre une intention similaire par le biais de plusieurs variantes différentes aux quatre questions mentionnées ci-dessus.

+++Sélectionner pour afficher les variations acceptées des questions sur l’observabilité des jeux de données

* Quels sont les cinq premiers jeux de données par taille ?
* Quel jeu de données comporte le plus grand nombre de lignes ?
* Combien de jeux de données ne contiennent aucune donnée ?
* Répertorier les jeux de données dont la taille est supérieure à 10 Mo ?
* Répertorier les jeux de données contenant moins de 10 lignes.
* Pouvez-vous m’afficher les jeux de données complètement vides ?
* Quel jeu de données est le plus grand par taille de stockage ?
* Quel est le plus petit jeu de données en termes de nombre de lignes ?
* Combien de mes jeux de données contiennent des données et combien sont vides ?
* Quel est le nombre de lignes pour le jeu de données nommé {DATASET_NAME} ?
* Comment la taille de {DATASET_NAME} se compare-t-elle à mes autres jeux de données ?
* Quelle est la taille de l&#39;{DATASET_NAME} ?
* De combien de lignes {DATASET_NAME} dispose-t-il ?
* Quelle est la taille et le nombre de lignes de {DATASET_NAME} ?
* Pouvez-vous répertorier les jeux de données les plus grands et les plus petits par taille de stockage ?

+++

Vous pouvez également affiner vos questions d’observabilité des données avec un qualificateur pour filtrer votre requête selon une certaine période :

* Jeux de données recevant des lots au cours des derniers (x) jours
* Jeux de données ne recevant pas de lots au cours des derniers (x) jours
* Jeux de données contenant le plus de données ingérées au cours des derniers (x) jours
* Nombre d’enregistrements pour un jeu de données spécifique au cours des derniers (x) jours

+++Sélectionner pour afficher les variations acceptées des questions sur l’observabilité des jeux de données

* Combien de jeux de données ont reçu des lots au cours des derniers (x) jours ?
* Quels jeux de données ont reçu des lots au cours des (x) derniers jours ?
* Pouvez-vous répertorier les jeux de données dont les données ont été ingérées au cours des derniers (x) jours ?
* Combien de jeux de données ont reçu de nouveaux lots au cours des (x) jours précédents ?
* Quels sont les jeux de données qui ont été mis à jour avec de nouvelles données au cours des derniers (x) jours ?
* Répertorier les jeux de données qui ont eu une activité par lots au cours des derniers (x) jours.
* Combien de jeux de données n’ont pas reçu de lots au cours des derniers (x) jours ?
* Quels jeux de données n’ont reçu aucun lot au cours des (x) derniers jours ?
* Pouvez-vous identifier des jeux de données sans ingestion de données au cours des derniers (x) jours ?
* Combien de jeux de données n’ont pas reçu de mises à jour au cours des derniers (x) jours ?
* Quels jeux de données ont été inactifs au cours des (x) derniers jours ?
* Répertorier les jeux de données qui n’ont pas obtenu de nouveaux lots au cours des (x) derniers jours.
* À quand remonte la dernière fois où les données ont été ingérées sur le jeu de données (x) ?
* Quels sont les 10 premiers jeux de données dans lesquels le plus de données ont été ingérées au cours des derniers (x) jours ?
* Quels sont les 10 premiers jeux de données par volume de données ingérés au cours des derniers (x) jours ?
* Quels 10 jeux de données ont eu la plus grande ingestion de données au cours des derniers (x) jours ?
* Afficher les 10 premiers jeux de données avec l’ingestion de données la plus élevée au cours des (x) jours précédents.
* Quels sont les principaux jeux de données par données reçus au cours des derniers (x) jours ?
* Répertoriez les 10 premiers jeux de données qui ont ingéré le plus de données au cours des (x) derniers jours.
* Combien d’enregistrements ont été reçus dans le jeu de données (x) au cours des derniers (y) jours ?
* Combien d’enregistrements le jeu de données (x) a-t-il reçus au cours des derniers jours (y) ?
* Quel est le nombre d’enregistrements ingérés pour le jeu de données (x) au cours des (y) derniers jours ?
* Pouvez-vous fournir le nombre d’enregistrements ajoutés au jeu de données (x) au cours des (y) derniers jours ?
* Quelle quantité de données a été reçue par le jeu de données (x) au cours des derniers (y) jours ?
* Quel est le volume d’enregistrements ingérés pour le jeu de données (x) au cours des (y) jours précédents ?

+++


## Exemples de questions non prises en charge {#unsupported-questions}

Vous trouverez ci-dessous une liste d’exemples de questions qui ne sont actuellement pas prises en charge par l’assistant AI.

+++Sélectionner pour afficher des exemples de questions non prises en charge

### Informations opérationnelles

* Combien de profils de ce sandbox vivent en Californie ? (**Remarque** : pour des questions similaires, vous devez fournir un critère spécifique afin de fournir suffisamment de contexte pour votre demande, dans ce cas, le critère spécifique est « en Californie »).
* Quels sont les segments dans lesquels se trouve ce profil {PROFILE_INFO/ATTRIBUTE_VALUE} ?
* Combien de profils du jeu de données ont un e-mail ?
* Quel jeu de données constitue le nombre maximal de profils dans ce sandbox ?
* Quel jeu de données comporte le plus grand nombre d’enregistrements ?
* Combien de segments ont été supprimés en {RELATIVE_DATE} ?
* Lequel de mes jeux de données a la plus grande taille ?
* Donnez-moi un profil dans la {AUDIENCE_NAME}.
* Quel est le nombre total de profils dans mon sandbox ?
* Combien d’espaces de noms d’identité sont associés aux {AUDIENCE_NAME} d’audience ?
* Afficher un rapport de tous les segments d’audience évalués aujourd’hui
* Combien de segments ont des profils qui se chevauchent ?
* Nombre de lots chargés dans {DATASET_NAME}
* Combien d’offres actives ai-je ?
* Combien de campagnes actives ai-je ?
* D’où viennent mes sources de données ?
* Quel est le jeu de données ou la source de données le plus volumineux ?
* Puis-je obtenir la liste des utilisateurs qui ont créé ces schémas ?

### Dépannage

* Pourquoi ce lot {BATCH_NAME/BATCH_ID} est-il toujours en cours de traitement ?
* Pourquoi personne ne se qualifie-t-il pour ce {AUDIENCE_NAME} d’audience ?
* Je ne suis pas en mesure de voir l’IA dédiée aux clients, pourquoi et comment la corriger ?
* Je ne parviens pas à voir l’aperçu du jeu de données. Pourquoi et comment le corriger ?
* Pourquoi ne puis-je pas supprimer {SEGMENT/DATASET/SCHEMA_NAME} ?
* Ai-je accès à Query Service ?

### Tâche et automatisation

* Écrivez une requête qui me donne un enregistrement du {DATASET_NAME}.
* Écrivez un exemple d’appel API dans /schemas/{schemaId}/fields/{fieldPath}/values.
* Configurer une source/destination pour moi.
* Créez une audience pour moi avec des critères {USER_SPECIFIC_CRITERIA}.

+++

## Étapes suivantes

En lisant ce document, vous comprenez désormais comment optimiser vos questions pour l’assistant AI. Pour plus d’informations sur l’utilisation de cette fonctionnalité au cours de vos workflows, consultez le guide de l’interface utilisateur de l’assistant [AI](ui-guide.md).
