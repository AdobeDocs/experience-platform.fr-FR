---
title: Estimation du langage naturel avec l’assistant IA
description: Découvrez comment utiliser les fonctionnalités d’estimation du langage naturel de l’assistant d’IA.
badge: Alpha
exl-id: 7997c84f-288b-4b48-9f88-8de4addbae36
TQID: https://experienceleague.adobe.com/tMbm4Vdg5CiVkv4NpyJCO5dl1YWTiWq6-iMrwVNFWfs
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914id: f8e8ea8a-6020-40da-99f7-6504fe599cb1
subfeature_v2: id: af7d4edc-6e6b-4176-bf14-907faf40ebd4
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c4147b6e-073b-4d3c-9ab1-d60f2f4434efid: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e1e0219c-f879-479f-8427-888ed2a6e9c2id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 1327
ht-degree: 0%

---

# Estimation en langage naturel avec l’assistant d’IA

>[!AVAILABILITY]
>
>Cette fonctionnalité se trouve dans Alpha et peut ne pas être disponible pour votre organisation. Pour participer au programme Alpha et accéder à cette fonctionnalité, contactez l’équipe chargée de votre compte Adobe.

Vous pouvez utiliser les fonctionnalités d’estimation du langage naturel de l’assistant AI pour Adobe Experience Platform afin d’estimer la taille des audiences et de prévoir la propension des audiences en fonction de questions simples et conversationnelles. Grâce à cette fonctionnalité, vous pouvez rendre les informations sur les audiences plus accessibles et intuitives. Cela peut s’avérer particulièrement utile pour les cas d’utilisation de vos opérations commerciales et marketing, en particulier si vous gérez vos audiences quotidiennement et que vous vous appuyez sur ces informations pour définir des stratégies marketing efficaces.

Grâce aux fonctionnalités de traitement du langage naturel d’AI Assistant, vous pouvez poser des questions du type : « Combien de profils ai-je en Californie entre 25 et 35 ans ? » ou « Combien de clients à forte valeur ajoutée avons-nous ? » ou même « Quel pourcentage de mon audience est susceptible d’acheter au cours du mois prochain ? » L’assistant AI interprète ensuite ces questions et renvoie des estimations ou des scores de propension que vous pouvez utiliser pour prendre des décisions basées sur les données.

Lisez ce document pour savoir comment utiliser les fonctionnalités d’estimation du langage naturel de l’assistant AI.

## Terminologie et définitions clés {#key-terminology-and-definitions}

Reportez-vous au tableau suivant pour obtenir la liste des termes importants et leurs définitions correspondantes.

| Terminologie | Définition |
| --- | --- |
| Estimation de la taille de l’audience | Processus de calcul du nombre de membres au sein d’une audience spécifique en fonction d’un critère défini. Vous pouvez baser vos estimations de taille sur les données de profil, y compris les profils qui ne se trouvent pas dans une audience. De plus, vous pouvez récupérer des estimations de taille d’audience sans avoir à créer d’audience au préalable. Utilisez cette insight pour déterminer l’ampleur de votre portée pour les campagnes ciblées. |
| Estimation de propension | Prédiction de la probabilité que les membres d’une audience présentent des comportements spécifiques (tels que : réalisation d’un achat, résiliation) au cours d’une certaine période. L’estimation de propension est spécifique aux audiences de Real-Time Customer Data Platform, mais peut inclure des données de profil, y compris des profils de n’importe quelle audience. Vous pouvez vous référer à cette insight lors de l’optimisation de vos campagnes et de la gestion des stratégies de rétention des audiences. |
| Traitement du langage naturel | La capacité de l&#39;assistant AI à interpréter et à répondre aux questions posées dans le langage courant, ce qui vous permet d&#39;interagir par la conversation et de recevoir des informations pertinentes sans utiliser de requêtes techniques. |
| Périodes prédéfinies | Périodes standard (« le mois dernier », « les 30 prochains jours ») prises en charge par l’assistant AI pour estimer la taille et la propension de l’audience. **Remarque** : les périodes personnalisées peuvent ne pas être entièrement prises en charge pendant l’étape Alpha. |
| Données de capture instantanée | Jeu de données utilisé par l’assistant AI pour fournir des estimations. Ces données sont mises à jour à partir de Real-Time Customer Data Platform toutes les 24 à 48 heures. Par conséquent, les informations peuvent ne pas refléter les modifications d’audience en temps réel. |

{style="table-layout:auto"}

## Exemples de cas d’utilisation {#use-case-examples}

Les fonctionnalités d&#39;estimation du langage naturel de l&#39;assistant AI peuvent être particulièrement utiles pour les cas d&#39;utilisation suivants :

### Opérations marketing

En tant que professionnel des opérations marketing, vos responsabilités peuvent inclure la gestion et la surveillance des données d’audience pour vous assurer qu’elles s’alignent sur vos objectifs commerciaux. Grâce à la fonctionnalité d’estimation en langage naturel de l’assistant d’IA, vous pouvez rapidement recueillir des informations sur la taille et la propension des audiences sans avoir à créer d’abord une audience ou à acquérir des connaissances approfondies en analyse de données.

en les aidant à maintenir une approche cohérente et axée sur les données dans leurs workflows.

### Utilisateurs professionnels et spécialistes du marketing

En tant qu’utilisateur professionnel et spécialiste marketing, l’accès rapide aux données d’audience peut être essentiel au succès de la planification, du ciblage et de l’évaluation de vos campagnes. Grâce à la fonctionnalité d’estimation en langage naturel de l’assistant d’IA, vous pouvez simplifier votre accès aux informations de l’audience, poser des questions simples et recevoir des informations exploitables qui vous aideront à créer votre audience et à optimiser vos campagnes.

## Principales fonctionnalités

>[!IMPORTANT]
>
>Les fonctionnalités suivantes sont présentes dans Alpha et sont axées sur les fonctionnalités fondamentales de l’estimation du langage naturel. Cette fonctionnalité étant présente dans Alpha, vous devez vérifier que les réponses que vous recevez de l’assistant AI sont exactes.

### Estimation de la taille de l’audience

Vous pouvez utiliser des requêtes en langage naturel pour demander à l’assistant AI d’estimer la taille d’audiences spécifiques. Cette fonctionnalité peut s’avérer particulièrement utile pour évaluer la portée et l’impact des audiences cibles. Par exemple, en tant que stratège marketing, vous pouvez poser des questions telles que :

* « Combien de profils vivent à New York ? »
* « Combien de profils ai-je avec un e-mail et y ai-je consenti ? »

Utilisez cette fonctionnalité pour simplifier le processus d’estimation des tailles d’audience et obtenir des réponses immédiates sans avoir à parcourir des filtres de données complexes ou des définitions de segment.

### Estimation de propension d’audience

>[!TIP]
>
>Votre compte Experience Platform doit être configuré avec l’[IA dédiée aux clients](../../intelligent-services/customer-ai/overview.md) pour utiliser les fonctionnalités d’estimation de propension de l’assistant IA.

Vous pouvez utiliser l’estimation de la propension de l’audience pour identifier la probabilité de comportements ou d’actions spécifiques dans une audience. Par exemple, vous pouvez poser des questions telles que :

* « Quel pourcentage de mon audience actuelle est susceptible d’acheter au cours du prochain mois ? »
* « Combien de profils ai-je avec une forte propension à la conversion ? »

En posant des questions en langage naturel, vous pouvez récupérer des scores de propension qui indiquent le pourcentage ou la probabilité que les membres de l’audience présentent certains comportements, ce qui vous permet d’apporter des ajustements proactifs à vos campagnes ou à vos stratégies de rétention.

## Exemples de questions sur la taille de l’audience et l’estimation de la propension

Voici des exemples de questions que vous pouvez poser à l’assistant AI pour vous aider à comprendre la taille de l’audience et les propensions comportementales :

### Estimation de la taille de l’audience

* « Combien de profils ai-je avec un e-mail ou un numéro de téléphone mobile ? »
* « Combien de profils ai-je à New York ? »
* « Quels sont les 5 premiers États où vivent mes clients ? »

### Estimation de la propension de l’audience

* « Quel pourcentage de mon audience est susceptible d’acheter au cours du prochain mois ? »
* « Combien de clients devraient effectuer une conversion au cours du prochain trimestre ? »

Vous pouvez utiliser la flexibilité offerte par les requêtes en langage naturel pour obtenir des insights rapides sur la dynamique de l’audience sans avoir besoin d’expertise technique.

## Questions fréquentes

Lisez cette section pour obtenir des réponses aux questions fréquentes sur l’estimation du langage naturel avec l’assistant AI.

### À quelle fréquence l’assistant AI actualise-t-il les données d’audience ?

Les données de l’assistant d’IA sont actualisées toutes les 24 à 48 heures. Par conséquent, les estimations peuvent refléter de légers retards. Cela signifie que lorsque vous posez des questions sur les données « actuelles », la réponse reflète l’instantané le plus récent, qui peut avoir jusqu’à 48 heures.

### Puis-je demander des tailles d’audience ou des propensions avec des périodes personnalisées ?

Actuellement, l’assistant d’IA prend en charge les périodes prédéfinies, telles que « le mois dernier » ou « les 30 prochains jours ». Les périodes personnalisées au-delà de ces options prédéfinies ne sont pas entièrement prises en charge à l’étape Alpha. Si une période personnalisée est demandée, l’assistant AI fournit des informations en fonction de la période disponible la plus proche.

### Comment l’assistant AI calcule-t-il les scores de propension ?

Les scores de propension sont calculés à l’aide de l’[IA dédiée aux clients](../../intelligent-services/customer-ai/overview.md). L’assistant AI utilise des modèles de machine learning pour prédire la probabilité de comportements d’audience spécifiques, tels que les achats et l’attrition, dans la période demandée. Lors de l’étape Alpha , le calcul du score de propension dans l’assistant AI n’utilise pas d’événements d’expérience ni de données comportementales.

### L’assistant AI estimera-t-il la taille ou la propension des audiences en fonction des données en temps réel ?

Non, les données en temps réel ne sont pas disponibles à ce stade. Les estimations sont basées sur des instantanés de données récents, mis à jour toutes les 24 à 48 heures. Les mises à jour en temps réel sont hors de portée pendant l’étape Alpha.

### Comment les propensions sont-elles calculées ?

L’assistant AI s’appuie sur les modèles d’IA dédiée aux clients pour répondre aux scores de probabilité ou de propension.

## Fonctionnalités hors de portée

Les fonctionnalités suivantes ne sont actuellement pas prises en charge :

### Estimations de la taille de l’audience basées sur l’événement des données comportementales

L’assistant AI ne peut actuellement pas répondre aux questions basées sur les données comportementales telles que **« Combien d’utilisateurs ont ajouté un produit au panier au cours des 30 derniers jours »**. Cependant, vous pouvez créer un attribut calculé dans Real-Time CDP qui peut pré-calculer de telles valeurs. Ces attributs calculés sont ensuite disponibles dans l’assistant AI. Pour plus d’informations, consultez la documentation sur [les attributs calculés](../../profile/computed-attributes/overview.md).

### Mises À Jour Des Données En Temps Réel

Les estimations fournies par l’assistant AI sont basées sur des instantanés de données récents, mais pas en temps réel. Les données sont actualisées toutes les 24 à 48 heures, de sorte que les informations reflètent ce retard. Cette limitation signifie que les utilisateurs et utilisatrices ne peuvent pas recevoir de mises à jour instantanées si un segment ou un jeu de données change considérablement dans un court laps de temps.
