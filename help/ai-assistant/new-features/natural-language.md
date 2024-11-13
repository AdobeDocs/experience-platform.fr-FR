---
title: Estimation du langage naturel avec assistant d’IA
description: Découvrez comment utiliser les fonctionnalités d’estimation du langage naturel de l’assistant d’IA.
badge: Alpha
source-git-commit: aef3be05ca23abe9ed8275aa562fdd3313a7e2d0
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 0%

---

# Estimation du langage naturel avec assistant d’IA

>[!AVAILABILITY]
>
>Cette fonctionnalité est en Alpha et peut ne pas être disponible pour votre entreprise. Pour participer au programme d’Alpha et accéder à cette fonctionnalité, contactez votre équipe de compte d’Adobe.

Vous pouvez utiliser les fonctionnalités d’estimation du langage naturel de l’assistant d’IA pour Adobe Experience Platform afin d’estimer la taille des audiences et de prédire la propension des audiences en fonction de questions simples et conversationnelles. Grâce à cette fonctionnalité, vous pouvez rendre les informations sur les audiences plus accessibles et intuitives. Cela peut s’avérer particulièrement utile pour les cas d’utilisation de vos opérations commerciales et marketing, en particulier si vous gérez vos audiences quotidiennement et que vous vous fiez à ces informations pour élaborer des stratégies marketing efficaces.

Grâce aux fonctionnalités de traitement du langage naturel de l’assistant d’IA, vous pouvez poser des questions telles que : &quot;Combien de profils ai-je en Californie entre 25 et 35 ans ?&quot; ou &quot;Combien de clients à haute valeur ajoutée avons-nous ?&quot; ou même &quot;Quel pourcentage de mon audience est susceptible d’acheter au cours du mois prochain ?&quot; L’assistant d’IA interprète ensuite ces questions et renvoie des estimations ou des scores de propension que vous pouvez utiliser pour prendre des décisions éclairées par les données.

Lisez ce document pour découvrir comment utiliser les fonctionnalités d’estimation du langage naturel de l’assistant d’IA.

## Terminologie et définitions clés {#key-terminology-and-definitions}

Reportez-vous au tableau ci-dessous pour une liste de la terminologie importante et de leurs définitions correspondantes.

| Terminologie | Définition |
| --- | --- |
| Estimation de la taille de l’audience | Processus de calcul du nombre de membres au sein d’une audience spécifique selon un critère défini. Vous pouvez baser vos estimations de taille sur les données de profil, y compris les profils ne faisant pas partie d’une audience. De plus, vous pouvez récupérer des estimations de taille d’audience sans avoir à créer au préalable une audience. Utilisez ces informations pour comprendre l’ampleur de votre portée pour les campagnes ciblées. |
| Estimation de propension | Prédiction de la probabilité que les membres d’une audience présentent des comportements spécifiques (par exemple : effectuer un achat, une perte de clientèle) au cours d’une certaine période. L’estimation de propension est spécifique aux audiences dans Real-Time Customer Data Platform, mais peut inclure des données de profil, y compris des profils dans n’importe quelle audience. Vous pouvez vous référer à ces informations lors de l’optimisation de vos campagnes et de la gestion des stratégies de rétention de l’audience. |
| Traitement du langage naturel | La capacité de l’assistant d’IA à interpréter et à répondre aux questions posées dans le langage courant, ce qui vous permet d’interagir de manière conversationnelle et de recevoir des informations pertinentes sans avoir recours à des requêtes techniques. |
| Périodes prédéfinies | Plages horaires standard (&quot;mois dernier&quot;, &quot;30 jours suivants&quot;) prises en charge par l’assistant d’IA pour estimer la taille et la propension de l’audience. **Remarque** : Les périodes personnalisées peuvent ne pas être entièrement prises en charge lors de l’étape de l’Alpha. |
| Données instantanées | Jeu de données utilisé par l’assistant d’IA pour fournir des estimations. Ces données sont mises à jour à partir de Real-Time Customer Data Platform toutes les 24 à 48 heures. Par conséquent, les informations peuvent ne pas refléter de changements d’audience en temps réel. |

{style="table-layout:auto"}

## Exemples de cas d’utilisation {#use-case-examples}

Les fonctionnalités d’estimation du langage naturel de l’assistant d’IA peuvent s’avérer particulièrement utiles pour les cas d’utilisation suivants :

### Opérations marketing

En tant que professionnel des opérations marketing, vos responsabilités peuvent inclure la gestion et le suivi des données d’audience pour s’assurer qu’elles correspondent aux objectifs de votre entreprise. Grâce à la fonction d’estimation du langage naturel de l’assistant d’IA, vous pouvez rapidement recueillir des informations sur la taille et la propension des audiences sans avoir à créer une audience d’abord ou à acquérir des connaissances d’analyse de données approfondies.

les aider à maintenir une approche cohérente axée sur les données dans leurs workflows.

### Utilisateurs professionnels et marketeurs

En tant qu’utilisateur professionnel et marketeur, un accès rapide aux données d’audience peut s’avérer essentiel au succès de la planification, du ciblage et de l’évaluation de vos campagnes. Grâce à la fonction d’estimation du langage naturel de l’assistant d’IA, vous pouvez simplifier votre accès aux informations sur les audiences, poser des questions simples et recevoir des informations exploitables qui facilitent la création de vos audiences et l’optimisation de vos campagnes.

## Principales fonctionnalités

>[!IMPORTANT]
>
>Les fonctions suivantes sont en Alpha et se concentrent sur les capacités fondamentales de l’estimation du langage naturel. Comme cette fonctionnalité est en Alpha, vous devez vérifier la précision des réponses que vous recevez de l’assistant d’IA.

### Estimation de la taille de l’audience

Vous pouvez utiliser des requêtes en langage naturel pour demander à l’assistant d’IA d’estimer la taille de certaines audiences. Cette fonction peut s’avérer particulièrement utile pour évaluer la portée et l’impact des audiences cibles. En tant que stratège marketing, par exemple, vous pouvez poser des questions telles que :

* &quot;Combien de profils vivent à New York ?&quot;
* &quot;Combien de profils ai-je avec un email et que j&#39;ai consenti ?&quot;

Utilisez cette fonction pour simplifier le processus d’estimation des tailles d’audience et obtenir des réponses immédiates sans avoir à parcourir des filtres de données ou des définitions de segment complexes.

### Estimation de la propension de l’audience

>[!TIP]
>
>Votre compte Experience Platform doit être configuré avec [Customer AI](../../intelligent-services/customer-ai/overview.md) pour utiliser les fonctionnalités d’estimation de propension de l’assistant d’IA.

Vous pouvez utiliser l’estimation de la propension de l’audience pour identifier la probabilité de comportements ou d’actions spécifiques au sein d’une audience. Par exemple, vous pouvez poser des questions telles que :

* &quot;Quel pourcentage de mon audience actuelle est susceptible d’acheter au cours du mois prochain ?&quot;
* &quot;Combien de profils ai-je avec une forte propension à la conversion ?&quot;

En posant des questions en langage naturel, vous pouvez récupérer les scores de propension qui indiquent le pourcentage ou la probabilité que les membres de l’audience exposent certains comportements, ce qui vous aide à effectuer des ajustements proactifs à vos campagnes ou stratégies de rétention.

## Exemples de questions sur la taille de l’audience et l’estimation de la propension

Vous trouverez ci-dessous des exemples de questions que vous pouvez poser à l’assistant d’IA pour vous aider à comprendre les tailles d’audience et les propensions comportementales :

### Estimation de la taille de l’audience

* &quot;Combien de profils ai-je avec un email ou un numéro de téléphone portable ?&quot;
* &quot;Combien de profils ai-je à New York ?&quot;
* &quot;Quels sont les 5 premiers états où vivent mes clients ?&quot;

### Estimation de propension de l’audience

* &quot;Quel pourcentage de mon audience sera susceptible d’acheter au cours du mois prochain ?&quot;
* &quot;Combien de clients sont-ils censés convertir au cours du prochain trimestre ?&quot;

Vous pouvez utiliser la flexibilité que les requêtes de langage naturel offrent pour obtenir rapidement des informations sur la dynamique des audiences sans avoir besoin d’expertise technique.

## Questions fréquentes

Lisez cette section pour obtenir des réponses aux questions fréquentes sur l’estimation du langage naturel à l’aide de l’assistant d’IA.

### À quelle fréquence l’assistant d’IA actualise-t-il les données d’audience ?

Les données de l’assistant d’IA sont actualisées toutes les 24 à 48 heures. Par conséquent, les estimations peuvent refléter de légers retards. Cela signifie que lorsque vous posez des questions sur les données &quot;actuelles&quot;, la réponse reflète l’instantané le plus récent, qui peut avoir jusqu’à 48 heures.

### Puis-je demander des tailles d’audience ou des propensions avec des périodes personnalisées ?

Actuellement, l’assistant d’IA prend en charge des périodes prédéfinies, telles que &quot;le mois dernier&quot; ou &quot;les 30 prochains jours&quot;. Les périodes personnalisées au-delà de ces options prédéfinies ne sont pas entièrement prises en charge à l’étape de l’Alpha. Si une période personnalisée est demandée, l’assistant d’IA fournit des informations sur la période la plus proche disponible.

### Comment l’assistant d’IA calcule-t-il les scores de propension ?

Les scores de propension sont calculés à l’aide de [Customer AI](../../intelligent-services/customer-ai/overview.md). L’assistant d’IA utilise des modèles d’apprentissage automatique pour prédire la probabilité de comportements d’audience spécifiques, tels que les achats et la perte de clientèle, pendant la période demandée. Pendant l’étape de l’Alpha, le calcul du score de propension dans l’assistant d’IA n’utilise ni les événements d’expérience, ni les données comportementales.

### L’assistant d’IA va-t-il estimer la taille ou la propension des audiences en fonction des données en temps réel ?

Non, les données en temps réel ne sont pas disponibles à ce stade. Les estimations sont basées sur des instantanés de données récents, mis à jour toutes les 24 à 48 heures. Les mises à jour en temps réel ne sont pas incluses lors de l’Alpha.

### Comment les propensions sont-elles calculées ?

L’assistant d’IA dépend des modèles de Customer AI pour répondre à tous les scores de probabilité ou de propension.

## Fonctionnalités hors plage

Les fonctionnalités suivantes ne sont actuellement pas prises en charge :

### Estimation de la taille de l’audience basée sur l’événement des données comportementales

Actuellement, l’assistant d’IA ne peut pas répondre aux questions basées sur des données comportementales telles que **&quot;Combien d’utilisateurs ont ajouté un produit au panier au cours des 30 derniers jours&quot;**. Cependant, vous pouvez créer un attribut calculé dans Real-Time CDP qui peut pré-calculer ces valeurs. Ces attributs calculés sont ensuite disponibles dans l’assistant d’IA. Pour plus d’informations, consultez la documentation sur les [attributs calculés](../../profile/computed-attributes/overview.md).

### Mises à jour de données en temps réel

Les estimations fournies par l’assistant d’IA sont basées sur des instantanés de données récents, mais pas en temps réel. Les données sont actualisées toutes les 24 à 48 heures. Les informations reflètent donc ce délai. Cette limitation signifie que les utilisateurs ne peuvent pas recevoir de mises à jour instantanées si un segment ou un jeu de données change considérablement au cours d’une courte période.