---
title: Détails du modèle d’optimisation de l’heure d’envoi
description: Découvrez le modèle d’IA utilisé pour l’optimisation de l’heure d’envoi dans Adobe Journey Optimizer.
hide: true
hidefromtoc: true
exl-id: 95e1fc8f-1817-40d7-aa55-93daa50f43c0
source-git-commit: 4c3f6ead150a2f793db92d2418df3177eba2d255
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 7%

---

# Détails du modèle d’optimisation de l’heure d’envoi

## Présentation du modèle {#model-overview}

* **Nom et version du modèle** : optimisation de l’heure d’envoi
* **Date de publication du modèle** : septembre 2024
* **Objectif du modèle** : le modèle d’optimisation de l’heure d’envoi de Adobe Journey Optimizer choisit l’heure d’envoi optimale pour les e-mails et les messages push afin d’optimiser l’engagement des consommateurs, en fonction du comportement historique d’ouverture et de clic de vos consommateurs.
* **Utilisateurs prévus** : les principaux utilisateurs de ce modèle sont les professionnels du marketing, les chefs de produit et les équipes d’engagement des clients qui tirent parti de Adobe Journey Optimizer pour piloter les stratégies marketing axées sur les données.
* **Cas d’utilisation** : il est préférable d’utiliser l’optimisation de l’heure d’envoi sur des communications marketing moins urgentes, par exemple, une publicité hebdomadaire, des informations promotionnelles sur un nouveau produit ou des informations sur une vente d’un mois. L’optimisation de l’heure d’envoi n’est disponible que pour les types d’action intégrés E-mail et Push de Journey Optimizer et n’est actuellement pas disponible pour les messages envoyés par le biais d’actions personnalisées ou pour d’autres types d’action.
* **Mauvaise utilisation potentielle** : l’optimisation de l’heure d’envoi ne doit pas être utilisée pour les messages opérationnels urgents et sensibles au temps, comme une confirmation de commande, une notification de réinitialisation de mot de passe ou une notification de changement de porte d’embarquement.

## Détails du modèle {#model-details}

* **Type de modèle** : le modèle d’optimisation de l’heure d’envoi ingère les données de comportement des clients Adobe Journey Optimizer de votre organisation et examine les événements d’ouverture et de clic au niveau de l’utilisateur pour prédire à quel moment vos clients sont les plus susceptibles d’interagir avec vos messages. Le comportement d’ouverture et de clic au niveau du consommateur pour chaque heure de la semaine est pondéré et combiné avec le comportement de consommateur global et similaire à l’aide d’un estimateur de [!DNL Bayesian]. Les prédictions [!DNL Bayesian] pour chaque heure de la semaine sont ensuite classées, ce qui donne lieu à une « carte thermique » pour chaque mesure (ouvertures d’e-mails, clics d’e-mail et ouvertures par notification push), pour chaque client, afin de prédire les heures de la semaine pendant lesquelles le contact avec chaque client est le plus et le moins susceptible d’obtenir le résultat d’engagement souhaité.
* **Input** : l’optimisation de l’heure d’envoi utilise les données de fuseau horaire du client dans le champ `timeZone` du groupe de champs [!UICONTROL Détails des préférences], le cas échéant, pour déterminer le fuseau horaire d’un client. Si le fuseau horaire d’un client n’est pas disponible dans le champ `timeZone` , l’optimisation de l’heure d’envoi tente d’en déduire le fuseau horaire du client, en fonction de la correspondance de fuseau horaire la plus courante avec la première adresse postale trouvée stockée dans le profil du client à l’aide du type de données [ adresse postale ](../../../xdm/data-types/postal-address.md). L’optimisation de l’heure d’envoi effectue des prédictions pour chaque client en fonction de trois types de données comportementales :
   * Comportement d’ouverture et de clic de vos consommateurs dans l’ensemble.
   * Comportement d’ouverture et de clic des consommateurs semblables dans le même fuseau horaire.
   * Comportement d’ouverture et de clic de ce consommateur individuel.
* **Sortie** : ces prédictions sont pondérées et combinées à l’aide d’une approche [!DNL Bayesian], ce qui donne lieu à une « carte thermique » pour chaque mesure (ouvertures d’e-mails, clics d’e-mails et ouvertures push), pour chaque client, qui indique les heures de la semaine où le contact avec ce client est le plus et le moins susceptible d’entraîner le résultat d’engagement souhaité (ouverture/clic), comme illustré dans l’exemple de carte thermique ci-dessous :

![Carte thermique d’optimisation de l’heure d’envoi.](../../images/models/send-time-optimization.png)

* **Exemple d’entrée et de sortie** : afin de minimiser l’impact du modèle sur la richesse des profils, les scores du modèle sont stockés et compressés dans trois attributs de profil stockés dans `_experience.intelligentServices.journeyAI.sendTimeOptimization`, et ne sont pas conçus pour être lisibles par l’utilisateur.

## Modèle de formation {#model-training}

* **Entraînement des données et prétraitement** : le jeu de données d’entraînement de chaque organisation est sourcé uniquement à partir de ses propres données dans Adobe Experience Platform.
   * Une fois que la fonctionnalité d’optimisation de l’heure d’envoi est activée pour votre organisation, le modèle est entraîné sur les événements d’e-mail et de notification push, d’envoi, d’ouverture et de clic dans tous les parcours et actions de votre organisation au cours des 16 dernières semaines, que ces actions utilisent ou non l’optimisation de l’heure d’envoi. Cela permet à l’optimisation de l’heure d’envoi de bénéficier de toutes les données générées par vos consommateurs.
   * Les modèles sont initialement entraînés et évalués chaque semaine. Au bout de 16 semaines, les modèles sont entraînés de nouveau et évalués tous les mois. La notation du modèle inclut tous les profils client (existants et nouveaux) depuis la dernière exécution de notation.
   * Les messages envoyés par l’optimisation de l’heure d’envoi reçoivent l’une des informations suivantes :
      * Heure d’envoi d’un message d’exploration sélectionnée afin de tester différentes heures d’envoi et d’observer la réponse des consommateurs et consommatrices.
      * Heure d’envoi du message « optimisée », sélectionnée pour maximiser les taux de clics/ouvertures. 5 % des événements d’envoi reçoivent une heure d’envoi d’« exploration » et 95 % des événements d’envoi sont « optimisés ».
   * Les heures d’envoi d’exploration sont sélectionnées de manière aléatoire à partir des heures d’envoi rendues disponibles par le temps d’attente maximal configuré. Par exemple, dans le cas où un message est sélectionné un mercredi à 9 h avec l’optimisation de l’heure d’envoi activée et un temps d’attente maximal de 3 heures, les heures d’envoi de l’exploration pour le message seront réparties uniformément entre 9 h, 10 h, 11 h et 12 h.

## Évaluation de modèles {#model-evaluation}

* **Évaluation du modèle** : l’optimisation de l’heure d’envoi peut augmenter le taux de clics des e-mails et le taux d’ouverture des notifications push dans une plage d’environ 2 % à 10 % pour tous les messages optimisés par une organisation.
   * Par exemple, si une organisation qui envoie des e-mails sans optimisation de l’heure d’envoi présente un taux de clic de 5,0 % en moyenne, le même ensemble d’e-mails avec optimisation de l’heure d’envoi peut entraîner un taux de clic de 5,5 % en moyenne (5,0 % * (1+10 %) = 5,5 %).
   * En raison de la variabilité au sein de petites tailles d’échantillon, l’optimisation de l’heure d’envoi peut ne pas être observable sur les envois de messages uniques.
   * Les organisations sont plus susceptibles de tirer de plus grands avantages de l’utilisation de l’optimisation de l’heure d’envoi lorsque les conditions suivantes sont présentes :
      * Les parcours existants utilisent des heures d’envoi fixes et mal optimisées.
      * La variabilité du comportement des consommateurs (clics et ouvertures) correspond à la localisation et aux préférences des consommateurs ;
      * Les entreprises utilisent l’optimisation de l’heure d’envoi sur une plus grande fraction des e-mails et des messages push.
      * Les organisations choisissent des temps d&#39;attente maximums dans la plage recommandée de 6 à 12 heures.

## Déploiement de modèles {#model-deployment}

* **Mise à jour des modèles** : les modèles sont initialement entraînés et notés chaque semaine. Au bout de 16 semaines, les modèles sont entraînés de nouveau et évalués tous les mois. La notation du modèle inclut tous les profils clients - à la fois existants et nouveaux depuis la dernière exécution de notation.

## Équité et partialité {#fairness-and-bias}

* **Équité du modèle** : une inférence incorrecte du fuseau horaire d’un client peut entraîner l’envoi d’un message plus tôt que prévu pour un client donné ou plus tard que prévu pour un client donné. Cependant, tous les consommateurs d’une communication utilisant l’optimisation de l’heure d’envoi recevront finalement un message et auront la possibilité d’interagir avec un message. En outre, ce modèle n’utilise pas de données démographiques des consommateurs ni d’indicateurs pour les données démographiques - seules les données relatives au comportement des consommateurs et au fuseau horaire des consommateurs sont utilisées. Par conséquent, les préoccupations en matière d&#39;équité sont limitées et atténuées.
* **Biais de données** : une inférence incorrecte du fuseau horaire d’un client peut entraîner l’envoi d’un message plus tôt que prévu pour un client donné ou plus tard que prévu pour un client donné. Cependant, tous les consommateurs d’une communication utilisant l’optimisation de l’heure d’envoi recevront finalement un message et auront la possibilité d’interagir avec un message. En outre, ce modèle n’utilise pas de données démographiques des consommateurs ni d’indicateurs pour les données démographiques - seules les données relatives au comportement des consommateurs et au fuseau horaire des consommateurs sont utilisées. Par conséquent, les préoccupations liées aux préjugés sont limitées et atténuées.

## Solidité {#robustness}

* **Robustesse du modèle** : les profils qui ne disposent pas de données suffisantes d’événement d’interaction (ce qui est souvent le cas pour les nouveaux profils) reçoivent soit une heure d’envoi immédiate, soit une heure d’envoi d’exploration dans la fenêtre sélectionnée ou une heure d’envoi basée sur l’heure d’envoi la plus performante pour tous les clients.

## Considérations éthiques {#ethical-considerations}

* **Considérations éthiques associées au modèle** : une inférence incorrecte du fuseau horaire d’un client peut entraîner l’envoi d’un message plus tôt que prévu pour un client donné ou plus tard que prévu pour un client donné. Cependant, tous les consommateurs d’une communication utilisant l’optimisation de l’heure d’envoi recevront finalement un message et auront la possibilité d’interagir avec un message. En outre, ce modèle n’utilise pas de données démographiques des consommateurs ni d’indicateurs pour les données démographiques - seules les données relatives au comportement des consommateurs et au fuseau horaire des consommateurs sont utilisées. Par conséquent, les préoccupations éthiques sont limitées et atténuées.