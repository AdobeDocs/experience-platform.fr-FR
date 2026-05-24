---
title: Surveillance des modifications importantes et prévision des audiences avec l’assistant AI
description: Découvrez comment utiliser l’assistant AI pour surveiller les modifications importantes et prévoir les audiences dans Adobe Experience Platform.
badge: Alpha
exl-id: 8f34d378-a8a0-420d-8e45-39a5aafdd7b7
TQID: https://experienceleague.adobe.com/ozJ5fYFkmPigWF5g7Ig2XQlLsTJrKSf5jh6mxSLW3qE
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914id: f8e8ea8a-6020-40da-99f7-6504fe599cb1
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b4dd41a7-ccf8-4e9d-918e-acaab534a307id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 1919
ht-degree: 2%

---

# Surveillez les modifications importantes et prévoyez la croissance de l’audience avec l’assistant AI

>[!AVAILABILITY]
>
>Cette fonctionnalité se trouve dans Alpha et peut ne pas être disponible pour votre organisation. Pour participer au programme Alpha et accéder à cette fonctionnalité, contactez l’équipe chargée de votre compte Adobe.

Dans le paysage actuel du marketing axé sur les données, des informations précises et en temps opportun sont essentielles. Que vous soyez un utilisateur professionnel ou que vous participiez à des opérations marketing, vous devez être en mesure d’interagir de manière cohérente avec vos audiences et d’apporter des ajustements rapides et percutants, fondés sur des informations claires. Afin de maintenir l’alignement ou d’atteindre vos objectifs commerciaux, vous devez disposer des informations exploitables nécessaires pour mener des campagnes efficaces et optimiser les ressources.

Vous pouvez utiliser l’assistant AI pour Adobe Experience Platform afin de surveiller les modifications importantes et de fournir des prévisions de croissance pour votre audience et les tailles des jeux de données. Vous pouvez ensuite utiliser ces informations pour garantir l’intégrité de vos données d’audience et proposer des projections prospectives à l’appui d’une prise de décision éclairée par les données.

Lisez ce document pour découvrir comment surveiller les modifications importantes et prévoir la croissance et les fluctuations de l’audience à l’aide de l’assistant AI.

## Terminologie et définitions clés {#key-terminology-and-definitions}

Reportez-vous au tableau suivant pour obtenir la liste des termes importants et leurs définitions correspondantes.

| Terminologie | Définition |
| --- | --- |
| Changement Significatif | Un changement significatif est un changement important de l’audience ou de la taille du jeu de données en fonction d’un pourcentage, défini par des seuils spécifiques (par exemple, 10 % pour les audiences importantes). Les modifications importantes permettent d’identifier les anomalies affectant la stabilité des données. |
| Anomalies | Les anomalies sont des variations inattendues dans les données, telles qu’une croissance soudaine de 20 % de l’audience **Acheteurs à forte valeur ajoutée**. Une anomalie peut être provoquée par un problème potentiel d’ingestion de données ou un changement dans la définition de l’audience. |
| Données historiques | Les données historiques font référence à des données à long terme, généralement sur un à trois ans. Vous pouvez utiliser des données historiques pour effectuer le suivi des modèles. **Remarque** : pendant l’étape Alpha , l’assistant AI fournit des données historiques allant jusqu’à 13 mois. |
| Données émergentes/récentes | Les données émergentes ou récentes se rapportent à des points de données observés sur une courte période, généralement pendant une semaine ou jusqu’à 30 jours. Vous pouvez utiliser des données émergentes ou récentes pour mettre en évidence les tendances immédiates et apporter des ajustements rapides. |
| Prévision | Les prévisions sont des prédictions d’audience ou de tailles de jeux de données futurs basées sur les tendances passées. Vous pouvez utiliser les données de prévision pour soutenir la planification à long terme. |
| Taille de l’audience | La taille d’audience fait référence au nombre total de profils au sein d’une audience. La taille de l’audience est mise à jour à chaque itération de l’ingestion des données. |
| Période de comparaison | L’assistant AI utilise des périodes de comparaison prédéfinies. Les anomalies récentes effectuent une recherche arrière de sept jours par défaut, tandis que les anomalies passées s’étendent sur 30 jours. Les tendances historiques s’étendent sur 13 mois. |

{style="table-layout:auto"}

## Exemples de cas d’utilisation {#use-case-examples}

La capacité de l’assistant AI à surveiller les modifications importantes et à prévoir les audiences peut être particulièrement utile pour les cas d’utilisation suivants :

### Opérations marketing

Les professionnels des opérations marketing (opérations marketing) sont chargés d’assurer l’intégrité et la cohérence des données d’audience. En tant que membre d’une équipe des opérations marketing, vous pouvez avoir pour responsabilités de surveiller la qualité des données, de répondre aux changements inattendus et de maintenir une base stable pour tous les efforts de marketing. Vous pouvez utiliser la détection des anomalies de l’assistant AI pour détecter et traiter les modifications importantes d’audience ou de jeu de données, évitant ainsi les perturbations susceptibles d’affecter les performances de la campagne.

### Utilisateurs professionnels et spécialistes du marketing

En tant qu’utilisateur professionnel et spécialiste marketing, vous pouvez vous fier aux informations précises sur les audiences pour prendre des décisions basées sur les données et vous assurer que vos campagnes atteignent efficacement leurs audiences prévues. Grâce aux fonctionnalités de prévision de l’assistant d’IA, vous pouvez anticiper la croissance ou la réduction de l’audience et permettre des ajustements stratégiques des ressources et du ciblage au fil du temps.

## Principales fonctionnalités

>[!IMPORTANT]
>
>Les fonctionnalités suivantes sont présentes dans Alpha et sont axées sur les fonctionnalités fondamentales de surveillance et de prévision. Cette fonctionnalité étant présente dans Alpha, vous devez vérifier que les réponses que vous recevez de l’assistant AI sont exactes.

### Surveiller les modifications importantes de l’audience et des données

Vous pouvez utiliser l’assistant d’IA pour identifier les modifications significatives dans l’audience et les tailles des jeux de données en suivant les écarts par rapport aux modèles standard. Chaque modification significative est basée sur des seuils prédéfinis adaptés à l’échelle de l’audience.

| Taille de l’audience | Nombre de profils | Description |
| --- | --- | --- |
| Petites audiences | 1 à 100 000 profils | Indique une modification de 30 % ou plus, sauf si un pourcentage spécifique est spécifié. |
| Audiences Medium | de 100 000 à 500 000 profils | Indique une modification de 25 % ou plus, sauf si un pourcentage spécifique est spécifié. |
| Audiences volumineuses | 500 000 à 1 million de profils | Indique une modification de 20 % ou plus, sauf si un pourcentage spécifique est spécifié. |
| Très grandes audiences | Plus d’un million de profils | Indique une modification de 10 % ou plus, sauf si un pourcentage spécifique est spécifié. |

{style="table-layout:auto"}

>[!BEGINSHADEBOX]

#### Exemple de scénario

Les modifications importantes indiquent des anomalies qui peuvent avoir un impact sur la stabilité de l’audience ou la fiabilité des données. Par exemple, si une audience **Acheteurs à forte valeur ajoutée** subit une baisse soudaine de 15 % de sa taille, l’assistant AI la signalera comme un changement significatif. Vous pouvez ensuite utiliser ces informations pour étudier et résoudre les problèmes potentiels avant qu’ils n’aient un impact sur vos campagnes.

>[!ENDSHADEBOX]

>[!TIP]
>
>L’assistant AI ne vous informe pas automatiquement de l’occurrence de modifications importantes de la taille de l’audience. Vous devez lancer une conversation avec l’assistant AI et demander quelles audiences ont changé de manière significative ou avec une marge spécifique, au cours d’une période spécifique.

### Prévision de la croissance de l’audience et des jeux de données

Vous pouvez utiliser l’assistant AI pour référencer les tendances des données historiques et prévoir l’audience et les tailles futures des jeux de données. Vous pouvez ensuite utiliser ces informations pour soutenir la planification des ressources et les ajustements de stratégie. Actuellement, vous pouvez utiliser l’assistant AI pour prévoir la croissance de l’audience et des jeux de données pendant 30 jours. En comprenant la croissance ou la baisse attendue de l’audience, vous pouvez ajuster les stratégies de ciblage et allouer vos ressources en conséquence.

### Informations sur les tailles d’audience historiques

Outre la détection des modifications importantes, vous pouvez utiliser l’assistant AI pour récupérer des informations historiques et comparer les tailles actuelles des audiences ou des jeux de données avec les données antérieures. Cette fonctionnalité permet de suivre les tendances à long terme et d’évaluer l’impact des activités marketing précédentes.

Vous pouvez poser des questions à l’assistant d’IA telles que : « Quelle était la taille de mon audience « Clients fidèles » le mois dernier ? pour afficher des données historiques sur la croissance ou le déclin de cette audience spécifique.

## Exemples de questions pour la surveillance des modifications importantes

Vous pouvez cadrer vos questions de l’assistant d’IA de différentes manières.

* Si votre question inclut un pourcentage, par exemple **« Quelles audiences ont changé de plus de 30 % ? »** l’assistant AI utilisera ce pourcentage comme point de référence.
* Si votre question ne spécifie pas de pourcentage, l’assistant AI interprète les modifications importantes en fonction des paramètres par défaut.

Consultez les tableaux suivants pour obtenir des exemples de requêtes qui illustrent la manière dont l’assistant AI interprète les modifications importantes en fonction de la taille de l’audience :

| Informations sur l’audience ou modification de l’audience | Exemple |
| --- | --- |
| <ul><li>Quelle est la taille actuelle des {AUDIENCE_NAME} ?</li><li>Affichez les audiences qui ont présenté un changement de {PERCENT} au fil du {DATE_DURATION}.</li></ul> | <ul><li>Quelle est la taille actuelle de l’audience des acheteurs à forte valeur ajoutée ?</li><li>Affichez les audiences qui ont présenté une modification de 20 % au cours de la dernière semaine.</li></ul> |

{style="table-layout:auto"}

| Requêtes spécifiques à l’audience | Exemple |
| --- | --- |
| <ul><li>Quelles audiences ont changé plus que {PERCENT} dans {DATE_OR_DURATION} ?</li><li>Montrez-moi les audiences avec un changement significatif au fil du {DATE_OR_DURATION}.</li><li>Montrez-moi la répartition des audiences présentant les modifications les plus importantes au fil du {DATE_OR_DURATION}.</li><li>Montrez-moi les audiences qui ont diminué de plus de {PERCENT} sur {DATE_OR_DURATION}.</li></ul> | <ul><li>Quelles audiences ont changé de plus de 20 % au cours de la dernière semaine ?</li><li>Montrez-moi les audiences avec un changement significatif sur les six derniers mois.</li><li>Montrez-moi la répartition des audiences avec les modifications les plus importantes du 1er au 31 octobre.</li><li> Montrez-moi les audiences qui ont diminué de plus de 20 % depuis le 31 août. |

{style="table-layout:auto"}

## Informations supplémentaires

### Comprendre le seuil de « changement significatif »

Vous pouvez spécifier un pourcentage spécifique lors de l’interrogation de l’assistant AI pour obtenir des informations concernant des modifications importantes. Si vous ne fournissez pas de pourcentage spécifique, l’assistant AI référencera un ensemble prédéfini de seuils pour déterminer ce qui est considéré comme une modification significative. Les seuils par défaut sont basés sur la taille d’une audience donnée. Reportez-vous au tableau suivant pour plus d’informations sur ce qui constitue un changement significatif en fonction de la taille de l’audience :

| Taille de l’audience | Qu’est-ce qui est important ? |
| --- | --- |
| 1 million ou plus | 10 % ou plus |
| 500 000 à 1 million | 20 % ou plus |
| 100k à 500k | 25 % ou plus |
| Moins de 100k | 30 % ou plus |

### Chronologies génériques et dates spécifiques

L’assistant AI prend en charge les comparaisons temporelles spécifiques et génériques pour les tailles d’audience, en les interprétant en fonction du contexte fourni dans la requête.

>[!BEGINTABS]

>[!TAB Chronologies génériques]

Les chronologies génériques font référence aux requêtes qui utilisent un langage tel que « cette semaine » ou « la semaine dernière ». Si vous posez à l’assistant AI une question telle que « Quelles audiences ont changé de plus de 20 % au cours de la dernière semaine ? », l’assistant AI calcule et compare la taille **audience moyenne** sur la période spécifiée.

Utilisez cette approche pour obtenir une vue plus large des modifications d’audience au fil du temps, ce qui vous permet de mieux comprendre les tendances dans des intervalles hebdomadaires ou mensuels.

>[!TAB Dates spécifiques]

Si votre question fait référence à une date spécifique, l’assistant AI comparera les **tailles exactes d’audience** à chacune des dates fournies.

Utilisez cette comparaison précise pour analyser les modifications entre des points spécifiques dans le temps et clarifier la manière dont la taille de l’audience peut évoluer sur des jours particuliers.

>[!ENDTABS]

Vous pouvez tirer parti de cette flexibilité pour mieux comprendre la dynamique de l’audience sur des périodes larges et précises. Que vous traitiez des tendances générales ou que vous examiniez des décalages exacts entre des dates spécifiques, vous pouvez utiliser le mécanisme adaptatif de l’assistant d’IA pour récupérer la comparaison la plus relative pour votre requête.

## Questions fréquentes {#faq}

Lisez cette section pour obtenir des réponses aux questions fréquentes sur la surveillance des modifications importantes et les prévisions d’audience avec l’assistant AI.

### Combien de données historiques puis-je consulter pour voir les augmentations ou les diminutions de taille d’audience ?

L’assistant AI conserve 12 mois de données historiques de taille d’audience. Vous pouvez poser des questions sur les changements d’audience au cours de cette période pour comprendre les modèles de croissance ou de déclin de l’année écoulée.

### Jusqu’à quand puis-je remonter dans l’histoire pour voir les changements d’audience ?

L’assistant AI effectue le suivi des modifications d’audience à partir du jour de son activation dans votre organisation et remonte au dernier changement de définition d’audience. Une fois activé, l’assistant AI surveille et enregistre en permanence les modifications apportées aux définitions pendant 12 mois au maximum, ce qui permettra de suivre et de comparer les données à l’avenir.

### Quelle quantité de données historiques est nécessaire pour une prévision ?

Au moins 30 jours de données sont requis pour une prévision fiable à partir du dernier changement de définition d’audience. Dans certains cas, par exemple pour les prévisions de [!DNL Black Friday], l’assistant AI peut avoir besoin de données historiques pendant 12 mois au maximum.

### Comment l’assistant AI interprète-t-il « récemment » ?

L’assistant AI interprète « récemment » comme les sept derniers jours. Pour les questions faisant référence à des modifications récentes, l’assistant AI prend en compte les données de cette période afin d’identifier les tendances ou les modifications.

### Comment l’assistant AI compare-t-il la taille des audiences ?

Lorsque des dates spécifiques sont mentionnées, l’assistant AI compare les tailles de l’audience à ces jours spécifiques. Pour des questions plus générales, telles que celles faisant référence aux « trois derniers mois » ou à la « semaine dernière », AI Assistant compare la taille moyenne de cette période à la moyenne du jour le plus récent.

### À quel point les données d’audience de l’assistant d’IA sont-elles récentes ?

L’actualisation des données à partir de Real-Time Customer Data Platform peut prendre entre 24 et 48 heures pour l’assistant AI. Par conséquent, pour les questions référençant « hier », AI Assistant interprète cela comme la veille de la disponibilité des données les plus récentes.

## Fonctionnalités hors de portée

Les fonctionnalités suivantes ne sont actuellement pas prises en charge :

### Analyse avancée des causes premières

Bien que l’assistant AI puisse identifier des modifications importantes, il ne peut actuellement pas fournir d’analyse détaillée des causes profondes de ces changements. Les itérations futures de l’assistant d’IA visent à spécifier quels jeux de données ou attributs contribuent à des changements importants dans vos audiences.

### Tailles complètes des jeux de données historiques

Le suivi historique complet des tailles de données n’est pas pris en charge pour le moment. Actuellement, l’assistant AI fournit l’historique des audiences et des jeux de données pendant 13 mois maximum.
