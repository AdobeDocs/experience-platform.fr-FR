---
title: Assistant AI dans Adobe Experience Platform
description: Découvrez comment utiliser l’assistant d’IA pour parcourir et comprendre les concepts d’Experience Platform et de Real-Time Customer Data Platform, ainsi que des informations d’utilisation sur vos objets.
exl-id: 3fed2b1d-75fc-47ce-98d1-a811eb8a1d8e
source-git-commit: 8b0632efe10e280149d68facea44ea1f62267e3e
workflow-type: tm+mt
source-wordcount: '1946'
ht-degree: 0%

---

# Guide de l’interface utilisateur de l’assistant AI (hérité)

>[!IMPORTANT]
>
>Ce document s’applique à l’assistant d’IA (hérité). Pour plus d’informations sur l’assistant AI (Next-Gen), consultez le guide de l’interface utilisateur de l’assistant [AI](https://experienceleague.adobe.com/fr/docs/experience-cloud-ai/experience-cloud-ai/ai-assistant/ai-assistant-ui) dans la documentation [AI dans Experience Cloud](https://experienceleague.adobe.com/fr/docs/experience-cloud-ai/experience-cloud-ai/home).

Reportez-vous au tableau suivant pour une comparaison de l’assistant AI (hérité) et de l’assistant AI (nouvelle génération) :

| Domaine de fonctionnalités | Assistant AI (hérité) | Assistant IA (nouvelle génération) |
| --- | --- | --- |
| Expérience utilisateur | L’assistant d’IA (hérité) est disponible dans un panneau du rail de droite uniquement. | L’assistant d’IA (version suivante) est disponible dans le panneau du rail droit et dans une expérience immersive en plein écran. |
| Portée des fonctionnalités | Vous pouvez utiliser l’assistant d’IA (hérité) pour obtenir des connaissances sur les produits et des informations opérationnelles. | Vous pouvez utiliser l’assistant d’IA (nouvelle génération) pour acquérir des connaissances sur les produits, obtenir des informations opérationnelles, ainsi que des compétences avancées en matière d’agentisme et exécuter des tâches en plusieurs étapes. |
| Architecture de Platform | L’assistant AI (hérité) n’est pas créé sur la pile Agent Orchestrator. | L’assistant d’IA (nouvelle génération) est optimisé par [Adobe Experience Platform Agent Orchestrator](https://experienceleague.adobe.com/fr/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator), ce qui permet l’extensibilité et une coordination avancée entre les fonctionnalités. |
| Couverture de l’application | L’assistant d’IA (hérité) est une implémentation spécifique à l’application. | Vous pouvez utiliser l’assistant d’IA (version suivante) pour une expérience d’assistant d’IA unifiée dans toutes les applications Adobe Experience Cloud. |
| Modèle d’accès et d’autorisation | Modèle d’accès au niveau de l’application aligné sur les limites de chaque produit. | Tous les utilisateurs ont accès à l’assistant AI (version suivante) et aux agents Experience Platform associés. **Remarque** : <ul><li>**Adobe Experience Manager** : votre administrateur doit vous accorder l’autorisation d’accéder à l’assistant AI (Next-Gen) via [Adobe Admin Console](https://helpx.adobe.com/fr/enterprise/using/admin-console.html).</li><li>**Customer Journey Analytics** : votre administrateur doit vous accorder l’autorisation d’accéder à l’assistant AI par le biais du contrôle d’accès de [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/technotes/access-control?lang=en). Cela vous permet de poser des questions sur la connaissance des produits et les informations sur les données. |

Lisez ce guide pour savoir comment utiliser l’assistant AI dans l’interface utilisateur de Adobe Experience Platform.

## Accéder à l’assistant AI dans l’interface utilisateur d’Experience Platform

Pour lancer l’assistant d’IA, sélectionnez le **[!UICONTROL AI Assistant icon]** dans l’en-tête supérieur de l’interface utilisateur d’Experience Platform.

![Page d’accueil d’Experience Platform, avec l’icône Assistant AI sélectionnée et l’interface de l’Assistant AI ouverte.](./images/ai-assistant-full-icon.png)

L’interface de l’assistant d’IA s’affiche et vous fournit immédiatement des informations pour commencer. Vous pouvez utiliser les options fournies sous [!UICONTROL Ideas to get started] pour répondre aux questions et aux commandes, telles que :

* [!UICONTROL Which of my audiences are activated?]
* [!UICONTROL What is a schema?]
* [!UICONTROL Tell me some common use cases for Real-Time CDP]

## Guide de l’interface utilisateur de l’assistant AI

>[!NOTE]
>
>Le workflow suivant est un exemple qui utilise le processus de création de schéma d’événement d’expérience pour illustrer comment vous pouvez utiliser l’assistant AI lors de l’utilisation de l’interface utilisateur d’Experience Platform.

Supposons que vous créiez un **schéma d’échange d’appareils sous forme d’événement**. Lors du processus de création du schéma d’événement d’expérience, vous tombez sur le champ `eventType` . « À ce stade, vous avez la possibilité de quitter votre workflow et de vous reporter aux [principes de base d’une composition de schémas](../xdm/schema/composition.md) de la documentation, ou vous pouvez utiliser l’assistant AI pour récupérer les réponses à vos questions et trouver des ressources supplémentaires via les liens de documentation recommandés par l’assistant AI. »

Pour commencer, entrez votre question dans la zone de texte fournie à cet effet. Dans l’exemple ci-dessous, l’assistant AI reçoit la question « **Quel est le champ eventType dans un schéma ExperienceEvent ?** »

![Assistant AI pour Experience Platform avec la question suivante préparée pour l’interrogation : « Quel est le champ eventType dans un schéma ExperienceEvent ?](./images/question.png)

L’assistant AI interroge ensuite sa base de connaissances et calcule une réponse. Après quelques instants, l’assistant AI renvoie une réponse et des suggestions associées que vous pouvez utiliser comme invites de suivi.

![Assistant AI pour Experience Platform avec une réponse à la requête précédente.](./images/answer.png)

Après avoir reçu une réponse de l’assistant d’IA, vous pouvez choisir parmi de nombreuses options pour décider comment vous souhaitez procéder.

### Fonctionnalités de l’assistant AI {#features}

Cette section décrit les différentes fonctionnalités de l’assistant AI que vous pouvez utiliser pendant vos workflows sur Experience Platform.

### Affichage des objets de données opérationnelles {#view-operational-data-objects}

Selon votre requête, l’assistant AI fournit des informations supplémentaires relatives aux données de votre sandbox. Pour voir comment la réponse à votre requête s’applique à votre sandbox spécifique, sélectionnez **[!UICONTROL In your sandbox].**

Lors de l’affichage des données relatives à votre sandbox, l’assistant AI peut fournir des liens directs vers des pages d’interface utilisateur spécifiques qui affichent les données interrogées.

+++Sélectionner pour afficher l’exemple

Dans cet exemple, l’assistant AI renvoie des informations supplémentaires concernant les schémas XDM existants de votre sandbox, y compris leur nombre total et les cinq champs les plus couramment utilisés.

![La fenêtre déroulante « dans votre sandbox » s’ouvre, affichant des informations supplémentaires sur vos schémas.](./images/in-your-sandbox.png)

+++

### Afficher les citations {#view-citations}

Vous pouvez vérifier les réponses qui vous sont renvoyées par l’assistant AI en examinant les citations disponibles avec chaque réponse de la connaissance du produit.

+++Sélectionner pour afficher un exemple d’affichage des sources

Pour afficher les citations et valider la réponse de l’assistant AI, sélectionnez **[!UICONTROL Show sources]**.

![La réponse de l’assistant AI avec « Afficher les sources » sélectionné.](./images/show-sources.png)

L’assistant AI met à jour l’interface et vous fournit des liens vers la documentation qui corrobore la réponse initiale. En outre, lorsque les citations sont activées, l’assistant AI met à jour la réponse pour inclure des notes de bas de page afin d’indiquer les parties spécifiques de la réponse qui font référence à la documentation fournie.

![Un menu déroulant des citations que l’assistant AI fournit pour les questions de concept.](./images/citations.png)

+++

### Informations opérationnelles {#operational-insights}

Vous devez être dans un sandbox actif pour que l’assistant AI puisse répondre de manière suffisante à une question sur vos informations opérationnelles.

+++Sélectionner pour afficher un exemple de question d’informations opérationnelles

Dans l’exemple ci-dessous, l’assistant AI est invité à répondre à la requête suivante : **« Afficher les flux de données créés à l’aide de la source Amazon S3 »**.

![Une question sur les informations opérationnelles.](./images/op-insights-question.png)

L’assistant AI répond ensuite avec un tableau répertoriant vos flux de données et leurs identifiants correspondants. Sélectionnez l’icône de téléchargement (![icône de téléchargement](/help/images/icons/download.png)) pour télécharger le tableau au format CSV. Pour afficher le tableau entier, sélectionnez l’icône Développer (![icône Développer](/help/images/icons/expand.png)).

![Réponse d’informations opérationnelles](./images/op-insights-answer.png)

Une vue développée du tableau s’affiche, vous fournissant une liste plus complète des flux de données en fonction des paramètres de votre requête.

![Vue de la table développée.](./images/table.png)

Lorsqu’une question sur les informations opérationnelles lui est posée, l’assistant AI fournit une explication de la manière dont il a calculé la réponse. Dans l’exemple ci-dessous, l’assistant AI décrit les étapes effectuées pour identifier les flux de données créés à l’aide de la source [!DNL Amazon S3].

![Assistant AI fournissant une explication sur la manière dont il a calculé sa réponse.](./images/answer-explained.png)

Vous pouvez également fournir des filtres et des modifications à vos questions, et demander à l’assistant AI de rendre ses résultats en fonction des filtres que vous incluez. Par exemple, vous pouvez demander à l’assistant AI de vous montrer une tendance du nombre de définitions de segment dans l’ordre de leur date de création, de supprimer des définitions de segment avec zéro profil total et d’utiliser des noms de mois au lieu de nombres entiers lors de l’affichage des données.

+++

### Vérifier les réponses des informations opérationnelles {#verify-responses}

Vous pouvez vérifier chaque réponse liée aux questions d’informations opérationnelles à l’aide d’une requête SQL fournie par l’assistant AI.

+++Sélectionner pour afficher un exemple de vérification des réponses des informations opérationnelles

Après réception d’une réponse à une question sur les informations opérationnelles, sélectionnez **[!UICONTROL Show sources]** puis **[!UICONTROL View source query]**.

![afficher la requête source](./images/view-source-query.png)

Lorsqu’il est interrogé avec une question d’informations opérationnelles, l’assistant AI fournit une requête SQL que vous pouvez utiliser pour vérifier le processus nécessaire au calcul de sa réponse. Cette requête source est fournie à des fins de vérification uniquement et n’est pas prise en charge sur Query Service.

![exemple de requête source](./images/source-query.png)

+++

### Utiliser la saisie automatique d’entité {#use-entity-auto-complete}

Vous pouvez utiliser la fonction de saisie semi-automatique pour recevoir une liste d’objets de données qui existent dans votre sandbox. Les recommandations de saisie semi-automatique sont disponibles pour les domaines suivants : audiences, schémas, jeux de données, parcours, sources et destinations.

+++Sélectionnez pour afficher un exemple de saisie automatique

Vous pouvez utiliser la saisie automatique en incluant le symbole plus (**`+`**) dans votre requête. Vous pouvez également sélectionner le signe plus (**`+`**) situé au bas de la zone de saisie de texte. Une fenêtre s’affiche avec une liste des objets de données recommandés pour votre sandbox.

![Exemple de saisie automatique](./images/autocomplete.png)

+++

### Utiliser multi-tour {#use-multi-turn}

Vous pouvez utiliser les fonctionnalités multi-tours de l&#39;assistant AI pour avoir une conversation plus naturelle au cours de votre expérience. L’assistant d’IA est en mesure de répondre aux questions de suivi, si nécessaire. ce contexte peut être déduit d’une interaction précédente.

+++Sélectionner pour afficher un exemple de tour multiple

Dans l’exemple ci-dessous, l’assistant AI est d’abord invité à indiquer le nombre total de flux de données, puis à répertorier les 10 flux de données les plus récents.

![Exemple de multi-tour](./images/multiturn.png)

+++

### Démarrer une nouvelle conversation

Vous pouvez changer de sujet avec l’assistant AI en réinitialisant et en démarrant une nouvelle conversation.

+++Sélectionnez pour afficher un exemple de réinitialisation de votre conversation

Pour réinitialiser, sélectionnez les points de suspension (**`...`**) dans l’interface de l’assistant d’IA, puis sélectionnez **[!UICONTROL Start new conversation]**. Cela indique à l’assistant AI que vous avez l’intention de changer de rubrique et peut s’avérer particulièrement utile lors de la résolution de problèmes liés à des requêtes qui échouent ou qui référencent des informations incorrectes.

![Les points de suspension sélectionnés et l’option Démarrer une nouvelle conversation sont sélectionnées.](./images/reset.png)

+++

### Utilisation de la visibilité {#use-discoverability}

Vous pouvez utiliser la fonctionnalité de visibilité de l&#39;assistant AI pour afficher une liste des sujets généraux, regroupés en entités, que l&#39;assistant AI prend en charge.

+++Sélectionner pour afficher un exemple de capacité de découverte

Pour afficher la visibilité, sélectionnez l’icône en forme d’ampoule dans l’en-tête supérieur de l’interface de l’assistant AI.

![La fonctionnalité de visibilité de l’assistant AI.](./images/lightbulb.png)

Sélectionnez ensuite une catégorie, puis une invite dans la liste fournie. Vous pouvez utiliser cette fonctionnalité pour avoir une meilleure idée des types de questions auxquelles l’assistant AI peut répondre. Vous pouvez également mettre à jour les invites préexistantes avec des détails spécifiques relatifs à votre sandbox à l’aide de texte libre ou de la [saisie semi-automatique](#use-auto-complete).

![L’assistant d’IA vous invite dans la visibilité.](./images/prompt.png)

+++

### Utiliser la saisie semi-automatique des questions {#use-question-autocomplete}

Vous pouvez utiliser la fonction de saisie automatique des questions de l’assistant AI pour sélectionner une question dans une liste de recommandations de l’assistant AI.

+++Sélectionner pour afficher un exemple de saisie semi-automatique des questions

Pour afficher le panneau des questions suggérées, tapez au moins sept (7) caractères dans la zone de saisie. Sélectionnez ensuite la question qui vous intéresse dans le menu qui s’affiche.

![Panneau pop-up contenant les questions suggérées par l’assistant d’IA.](./images/suggested_questions.png)

Vous devrez peut-être mettre à jour les espaces réservés dans certains cas où une question suggérée implique des informations opérationnelles. Par exemple, vous pouvez avoir besoin d’ajouter le nom spécifique d’un jeu de données ou d’une audience si la suggestion de l’assistant AI comprend des espaces réservés.

![Une suggestion de l’assistant AI qui inclut des espaces réservés.](./images/placeholder.png)

Les espaces réservés sont surlignés en bleu. Sélectionnez l’espace réservé pour commencer à mettre à jour sa valeur. Pour de meilleurs résultats sur les espaces réservés numériques, veillez à utiliser des chiffres au lieu du texte. Vous pouvez également utiliser la fonction de saisie automatique des entités pour mettre à jour les valeurs des espaces réservés. Vous ne pouvez pas envoyer une question qui contient des espaces réservés vides.

**REMARQUE** : les suggestions sont activées par défaut. Sélectionnez le bouton (bascule) **[!UICONTROL Suggest ideas]** pour désactiver la fonction.

![Une suggestion de l’assistant AI avec des espaces réservés mis à jour.](./images/updated_placeholder.png)

+++

### Utiliser les suggestions associées {#use-related-suggestions}

Vous pouvez utiliser la section de suggestions associée de chaque réponse de l’assistant d’IA pour poursuivre votre conversation.

+++Sélectionner pour afficher un exemple de suggestions associées

Les suggestions associées sont renvoyées avec chaque réponse de l’assistant AI. Pour poursuivre votre conversation, sélectionnez l’une des suggestions de la section suggestions associée.

![Liste des suggestions associées de l’assistant AI.](./images/related_suggestions.png)

Comme pour les espaces réservés en question, vous devez mettre à jour les espaces réservés inclus dans les suggestions associées avant de pouvoir envoyer la requête.

![Requête à partir des suggestions associées avec les espaces réservés mis à jour.](./images/related_suggestions_placeholder.png)

+++

## Fournir des commentaires {#feedback}

Vous pouvez fournir un retour d’expérience avec l’assistant d’IA à l’aide des options fournies avec la réponse.

Pour faire part de vos commentaires, sélectionnez l’une des options suivantes : pouces vers le haut, pouces vers le bas ou indicateur , après avoir reçu une réponse de l’assistant AI, puis saisissez vos commentaires dans la zone de texte fournie.

![Option Commentaires dans l’assistant d’IA.](./images/provide-feedback.png)

+++Sélectionner pour afficher d’autres exemples

>[!BEGINTABS]

>[!TAB Pouce vers le haut]

Sélectionnez l’icône pouces vers le haut pour fournir des commentaires sur le bon fonctionnement de votre expérience avec l’assistant d’IA.

![La fenêtre de commentaires positifs.](./images/thumbs-up.png)

>[!TAB Pouces vers le bas]

Sélectionnez l’icône pouces baissés pour fournir des commentaires sur les améliorations qui pourraient être apportées en fonction de votre expérience avec l’assistant d’IA. Au cours de cette étape, vous pouvez également fournir des commentaires spécifiques concernant votre expérience. Les commentaires fournis dans les commentaires sont examinés quotidiennement.

![Fenêtre de commentaires négatifs.](./images/thumbs-down.png)

>[!TAB Indicateur]

Sélectionnez l’icône d’indicateur pour fournir d’autres rapports sur votre expérience à l’aide de l’assistant AI.

![Fenêtre des résultats du rapport.](./images/flag.png)

>[!ENDTABS]

+++
