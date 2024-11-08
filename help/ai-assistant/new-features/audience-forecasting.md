---
title: Surveillance des changements significatifs et des prévisions d’audience à l’aide de l’assistant d’IA
description: Découvrez comment utiliser l’assistant d’IA pour surveiller les changements significatifs et les audiences prévisionnelles dans Adobe Experience Platform.
badge: Alpha
source-git-commit: 37d2886cc5d7b3a019d23f76973d79547865298b
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 0%

---

# Surveiller les changements significatifs et prévoir la croissance de l’audience à l’aide d’un assistant d’IA

>[!AVAILABILITY]
>
>Cette fonctionnalité est en Alpha et peut ne pas être disponible pour votre entreprise. Pour participer au programme d’Alpha et accéder à cette fonctionnalité, contactez votre équipe de compte d’Adobe.

Dans le contexte actuel du marketing axé sur les données, des informations opportunes et précises sont essentielles. Que vous soyez un utilisateur chargé des affaires ou des opérations marketing, vous avez besoin de la possibilité d’interagir de manière cohérente avec vos audiences et d’effectuer des ajustements rapides et efficaces sur la base d’informations claires. Pour maintenir l’alignement ou atteindre les objectifs de votre entreprise, vous devez disposer des informations exploitables nécessaires à l’exécution de campagnes efficaces et à l’optimisation des ressources.

Vous pouvez utiliser l’assistant d’IA pour Adobe Experience Platform afin de surveiller les modifications importantes et de fournir des prévisions de croissance pour votre audience et la taille de vos jeux de données. Vous pouvez ensuite utiliser ces informations pour garantir l’intégrité de vos données d’audience et proposer des projections prospectives à l’appui d’une prise de décision éclairée par les données.

Lisez ce document pour découvrir comment surveiller les changements significatifs et prévoir la croissance et les fluctuations de l’audience à l’aide de l’assistant d’IA.

## Terminologie et définitions clés {#key-terminology-and-definitions}

Reportez-vous au tableau ci-dessous pour une liste de la terminologie importante et de leurs définitions correspondantes.

| Terminologie | Définition |
| --- | --- |
| Changement significatif | Un changement significatif est un changement important en pourcentage de la taille de l’audience ou du jeu de données, défini par des seuils spécifiques (par exemple, 10 % pour les grandes audiences). Des modifications significatives permettent d’identifier les anomalies affectant la stabilité des données. |
| Anomalies | Les anomalies correspondent à des variations inattendues des données, telles qu’une croissance soudaine de 20 % dans une audience **Opérateurs à forte valeur**. Une anomalie peut être due à un problème potentiel d’ingestion des données ou à un changement de la définition de l’audience. |
| Données historiques | Les données historiques font référence à des données à long terme, généralement d’une à trois ans. Vous pouvez utiliser des données historiques pour effectuer le suivi des modèles. **Remarque** : pendant l’étape de l’Alpha, l’assistant d’IA fournit des données historiques allant jusqu’à 13 mois. |
| Données récentes/émergentes | Les données récentes ou émergentes se rapportent aux points de données observés sur une courte période, généralement pendant une semaine ou jusqu’à 30 jours. Vous pouvez utiliser les données récentes ou émergentes pour mettre en évidence les tendances immédiates et effectuer des ajustements rapides. |
| Prévisions | Les prévisions sont des prédictions de tailles futures d’audience ou de jeux de données en fonction des tendances passées. Vous pouvez utiliser les données de prévision pour prendre en charge la planification à long terme. |
| Taille de l’audience | La taille de l’audience fait référence au nombre total de profils au sein d’une audience. La taille de l’audience est mise à jour à chaque itération de l’ingestion des données. |
| Période de comparaison | L’assistant d’IA utilise des périodes de comparaison prédéfinies. Par défaut, les anomalies récentes font l’objet d’une analyse en amont de sept jours, tandis que les anomalies antérieures couvrent 30 jours. Les tendances historiques s’étendent sur 13 mois au maximum. |

{style="table-layout:auto"}

## Exemples de cas d’utilisation {#use-case-examples}

La capacité de l’assistant d’IA à surveiller les changements significatifs et les audiences prévisionnelles peut s’avérer particulièrement utile pour les cas d’utilisation suivants :

### Opérations marketing

Les professionnels des opérations marketing (opérations marketing) sont chargés d’assurer l’intégrité et la cohérence des données d’audience. En tant que membre de l’équipe marketing, vos responsabilités peuvent inclure la surveillance de la qualité des données, la réponse aux changements inattendus et la maintenance d’une base stable pour tous les efforts marketing. Vous pouvez utiliser la détection des anomalies de l’assistant d’IA pour détecter et traiter des modifications importantes d’audience ou de jeu de données, afin d’éviter les perturbations susceptibles d’affecter les performances de la campagne.

### Utilisateurs professionnels et marketeurs

En tant qu’utilisateur professionnel et marketeur, vous pouvez vous fier à des informations précises sur les audiences pour prendre des décisions basées sur les données et vous assurer que vos campagnes atteignent efficacement les audiences prévues. Grâce aux fonctionnalités de prévision de l’assistant d’IA, vous pouvez anticiper la croissance ou la réduction des audiences et permettre des ajustements stratégiques des ressources et du ciblage au fil du temps.

## Principales fonctionnalités

>[!IMPORTANT]
>
>Les fonctions suivantes sont en Alpha et se concentrent sur les capacités fondamentales de la surveillance et de la prévision. Comme cette fonctionnalité est en Alpha, vous devez vérifier la précision des réponses que vous recevez de l’assistant d’IA.

### Surveiller les changements significatifs dans l’audience et les données

Vous pouvez utiliser l’assistant d’IA pour identifier les changements significatifs de la taille des audiences et des jeux de données en suivant les écarts par rapport aux modèles typiques. Chaque changement significatif est basé sur des seuils prédéfinis adaptés à l&#39;échelle de l&#39;audience.

| Taille de l’audience | Nombre de profils | Description |
| --- | --- | --- |
| Petites audiences | 1 à 100 000 profils | Marque une modification de 30 % ou plus, sauf si un pourcentage spécifique est spécifié. |
| Audiences Medium | 100 000 à 500 000 profils | Marque une modification de 25 % ou plus, sauf si un pourcentage spécifique est spécifié. |
| Grands publics | 500 000 à 1 million de profils | Marque une modification de 20 % ou plus, sauf si un pourcentage spécifique est spécifié. |
| Très grandes audiences | Plus de 1 million de profils | Marque une modification de 10 % ou plus, sauf si un pourcentage spécifique est spécifié. |

{style="table-layout:auto"}

>[!BEGINSHADEBOX]

#### Exemple de scénario

Des modifications significatives indiquent des anomalies susceptibles d’avoir un impact sur la stabilité de l’audience ou la fiabilité des données. Par exemple, si une audience de **grande valeur Shoppers** enregistre une chute soudaine de 15 % de la taille, l’assistant d’IA la signale comme un changement significatif. Vous pouvez ensuite utiliser ces informations pour étudier et résoudre les problèmes potentiels avant qu’ils n’affectent vos campagnes.

>[!ENDSHADEBOX]

>[!TIP]
>
>L’assistant d’IA ne vous informe pas automatiquement des changements significatifs de tailles d’audience. Vous devez lancer une conversation avec l’assistant d’IA et demander quelles audiences ont considérablement changé ou selon une marge spécifique, au cours d’une période spécifique.

### Prévision de la croissance de l’audience et des jeux de données

Vous pouvez utiliser l’assistant d’IA pour référencer les tendances des données historiques et projeter les futures audiences et les tailles des jeux de données. Vous pouvez ensuite utiliser ces informations pour prendre en charge la planification des ressources et les ajustements de stratégie. Actuellement, vous pouvez utiliser l’assistant d’IA pour prévoir la croissance des audiences et des jeux de données pendant 30 jours. En comprenant la croissance ou le déclin attendu de l’audience, vous pouvez ajuster les stratégies de ciblage et allouer vos ressources en conséquence.

### Informations sur les tailles d’audience historiques

Outre la détection de modifications significatives, vous pouvez utiliser l’assistant d’IA pour récupérer des informations historiques et comparer les tailles d’audience ou de jeu de données actuelles aux données antérieures. Cette fonctionnalité prend en charge le suivi des tendances à long terme et l’évaluation de l’impact des activités marketing précédentes.

Vous pouvez poser des questions à l’assistant d’IA telles que &quot;Quelle était la taille de mon audience &quot;Clients fidèles&quot; le mois dernier ? pour consulter des données historiques sur la croissance ou le déclin de cette audience spécifique.

## Exemples de questions pour surveiller les modifications significatives

Vous pouvez définir les questions de votre assistant d’IA de différentes manières.

* Si votre question comporte un pourcentage, tel que **&quot;Quelles audiences ont changé plus de 30 % ou plus ?&quot;**, puis l’assistant d’IA utilisera le pourcentage comme point de référence.
* Si votre question n’indique pas de pourcentage, l’assistant d’IA interprètera les modifications importantes en fonction des paramètres par défaut.

Reportez-vous aux tableaux suivants pour consulter des exemples de requêtes qui illustrent la manière dont l’assistant d’IA interprète les modifications importantes en fonction de la taille de l’audience :

| Informations sur l’audience ou modification de l’audience | Exemple |
| --- | --- |
| <ul><li>Quelle est la taille actuelle de {AUDIENCE_NAME} ?</li><li>Affichez les audiences ayant affiché une modification de {PERCENT} sur {DATE_DURATION}.</li></ul> | <ul><li>Quelle est la taille actuelle de l’audience acheteurs à valeur élevée ?</li><li>Afficher les audiences qui ont affiché une modification de 20 % au cours de la semaine dernière.</li></ul> |

{style="table-layout:auto"}

| Requêtes spécifiques à une audience | Exemple |
| --- | --- |
| <ul><li>Quelles audiences ont changé plus de {PERCENT} dans {DATE_OR_DURATION} ?</li><li>Montrez-moi les audiences avec un changement significatif de plus de {DATE_OR_DURATION}.</li><li>Montrez-moi la distribution des audiences avec les modifications les plus importantes de plus de {DATE_OR_DURATION}.</li><li>Montrez-moi les audiences qui ont diminué plus de {PERCENT} sur {DATE_OR_DURATION}.</li></ul> | <ul><li>Quelles audiences ont changé plus de 20 % la semaine dernière ?</li><li>Montrez-moi des audiences avec un changement significatif au cours des six derniers mois.</li><li>Montrez-moi la distribution des audiences avec les modifications les plus importantes du 1er au 31 octobre.</li><li> Montrez-moi les audiences qui ont diminué de plus de 20 % depuis le 31 août. |

{style="table-layout:auto"}

## Informations supplémentaires

### Comprendre le seuil de &quot;changement significatif&quot;

Vous pouvez spécifier un pourcentage spécifique lors de l’interrogation de l’assistant d’IA pour obtenir des informations sur les modifications importantes. Si vous ne fournissez pas de pourcentage spécifique, l’assistant d’IA fera référence à un ensemble prédéfini de seuils pour déterminer ce qui est qualifié de changement significatif. Les seuils par défaut sont basés sur la taille d’une audience donnée. Reportez-vous au tableau suivant pour plus d’informations sur ce qui constitue un changement significatif en fonction de la taille de l’audience :

| Taille de l’audience | Qu&#39;est-ce qui est important ? |
| --- | --- |
| 1 million ou plus | 10 % ou plus |
| 500 à 1 million | 20 % ou plus |
| 100 à 500 k | 25 % ou plus |
| Moins de 100 Ko | 30 % ou plus |

### Chronologies génériques et dates spécifiques

L’assistant d’IA prend en charge les comparaisons temporelles spécifiques et génériques pour les tailles d’audience, en les interprétant en fonction du contexte fourni dans la requête.

>[!BEGINTABS]

>[!TAB Chronologies génériques]

Les chronologies génériques se rapportent aux requêtes qui utilisent une langue telle que &quot;cette semaine&quot; ou &quot;la semaine dernière&quot;. Si vous posez à l’assistant d’IA une question du type &quot;Quelles audiences ont changé de plus de 20 % au cours de la dernière semaine ?&quot;, l’assistant d’IA calculera et comparera la taille **moyenne de l’audience** sur la période spécifiée.

Utilisez cette approche pour avoir une vue plus large des changements d’audience au fil du temps, ce qui vous permet de mieux comprendre les tendances au cours d’intervalles hebdomadaires ou mensuels.

>[!TAB Dates spécifiques]

Si votre question fait référence à une date spécifique, l’assistant d’IA compare les **tailles d’audience exactes** à chacune des dates fournies.

Utilisez cette comparaison précise pour analyser les modifications entre des points spécifiques dans le temps et mieux comprendre l’évolution de la taille de l’audience au cours de certains jours.

>[!ENDTABS]

Vous pouvez tirer parti de cette flexibilité pour mieux comprendre la dynamique de l’audience sur des périodes à la fois larges et précises. Que vous effectuiez le suivi des tendances générales ou que vous examiniez les changements exacts entre des dates spécifiques, vous pouvez utiliser le mécanisme adaptatif de l’assistant d’IA pour récupérer la comparaison la plus relative pour votre requête.

## Questions fréquentes {#faq}

Lisez cette section pour obtenir des réponses aux questions fréquentes sur la surveillance des changements significatifs et la prévision des audiences à l’aide de l’assistant d’IA.

### Quelle quantité de données historiques puis-je consulter pour voir la taille de l’audience augmente ou diminue ?

L’assistant d’IA conserve 12 mois de données historiques sur la taille de l’audience. Vous pouvez poser des questions concernant les changements d’audience au cours de cette période afin de comprendre les tendances de croissance ou de déclin au cours de l’année écoulée.

### Jusqu’où puis-je remonter dans l’histoire pour voir les changements d’audience ?

L’assistant d’IA effectue le suivi des changements d’audience à partir du jour où ils sont activés dans votre entreprise et remonte jusqu’au dernier changement de définition d’audience. Une fois activé, l’assistant d’IA surveille en permanence les modifications de définition des enregistrements et les enregistre pendant 12 mois au maximum, ce qui permet un suivi et une comparaison des données futurs.

### Quelle quantité de données historiques est nécessaire pour une prévision ?

Au moins 30 jours de données sont nécessaires pour une prévision fiable à partir du dernier changement de définition de l’audience. Dans certains cas, comme lors des prévisions pour [!DNL Black Friday], l’assistant d’IA peut nécessiter jusqu’à 12 mois de données historiques.

### Comment l’assistant d’IA interprète-t-il &quot;récemment&quot; ?

L’assistant d’IA interprète &quot;récemment&quot; comme les sept derniers jours. Pour les questions faisant référence à des modifications récentes, l’assistant d’IA prend en compte les données de cette période afin d’identifier les tendances ou les changements.

### Comment l’assistant d’IA compare-t-il les tailles d’audience ?

Lorsque des dates spécifiques sont mentionnées, l’assistant d’IA compare les tailles d’audience selon ces jours spécifiques. Pour les questions plus générales, telles que celles qui font référence aux &quot;trois derniers mois&quot; ou à la &quot;semaine dernière&quot;, l’assistant AI compare la taille moyenne de cette période à la moyenne du jour le plus récent.

### À quel point les données d’audience de l’assistant d’IA sont-elles à jour ?

Il peut s’écouler entre 24 et 48 heures avant que l’assistant d’IA n’actualise les données de Real-Time Customer Data Platform. Par conséquent, pour les questions faisant référence à &quot;hier&quot;, l’assistant d’IA interprète cela comme étant la veille de la disponibilité des données les plus récentes.

## Fonctionnalités hors plage

Les fonctionnalités suivantes ne sont actuellement pas prises en charge :

### Analyse avancée des causes racines

Bien que l’assistant d’IA puisse identifier des modifications importantes, il ne peut actuellement pas fournir d’analyse détaillée des causes de ces modifications. Les prochaines itérations de l’assistant d’IA visent à spécifier les jeux de données ou les attributs qui contribuent à des modifications significatives de vos audiences.

### Taille complète des jeux de données historiques

Pour l’instant, le suivi historique complet des tailles de données n’est pas pris en charge. Actuellement, cet assistant fournit un historique des audiences et des jeux de données pendant 13 mois au maximum.