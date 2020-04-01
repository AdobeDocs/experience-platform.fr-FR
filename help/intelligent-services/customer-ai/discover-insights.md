---
keywords: Experience Platform;insights; customer ai;popular topics
solution: Experience Platform
title: Découverte des informations avec l’API client
topic: Discovering insights
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# Découverte des informations avec l’API client

Dans le cadre d’Intelligent Services, l’API du client permet aux spécialistes du marketing de tirer parti d’Adobe Sensei pour anticiper les prochaines actions de vos clients. Customer AI est utilisée pour générer des scores de propension personnalisés tels que les taux d’attrition et de conversion de profils individuels à grande échelle. Cette opération s’effectue sans qu’il soit nécessaire de transformer les besoins professionnels en un problème d’apprentissage automatique, en choisissant un algorithme, une formation ou un déploiement.

Ce sert de guide pour l’interaction avec les informations d’instance de service dans l’interface utilisateur d’intelligence d’entreprise des services intelligents.

## Prise en main

Pour utiliser les statistiques de l’API client, vous devez disposer d’une instance de service avec un état d’exécution réussi. Pour créer une nouvelle instance de service, consultez le guide [d’utilisation de l’API](./user-guide.md)client. Si vous avez récemment créé une instance de service et qu’elle est toujours en cours d’entraînement et de notation, veuillez compter 24 heures pour qu’elle se termine.

## Présentation de l’instance de service

In the Adobe Experience Platform UI, click **Services** in the left navigation. Le navigateur *Services* s’affiche et affiche les services intelligents disponibles. Dans le conteneur de Customer AI, cliquez sur **Ouvrir**.

![Accès à votre instance](./images/insights/navigate-to-service.png)

La page Service d’API client s’affiche. Cette page  les instances de service de l’API du client et affiche des informations à leur sujet, notamment le nom de l’instance, le type de propension, la fréquence d’exécution de l’instance et l’état de la dernière mise à jour.

>[!NOTE] Seules les instances de service ayant terminé des exécutions de notation réussies ont des informations.

![Créer une instance](./images/insights/dashboard.png)

Cliquez sur le nom d’une instance de service pour commencer.

![Créer une instance](./images/insights/click-the-name.png)

Ensuite, la page d’informations de cette instance de service s’affiche, dans laquelle vous recevez des visualisations de vos données. Les visualisations et ce que vous pouvez faire avec les données sont expliqués plus en détail dans ce guide.

![page de configuration](./images/insights/landing-page.png)


### Détails de l’instance de service

Il existe deux façons de des détails d’instance de service : la première provient du et la seconde de l’instance de service.

Pour  détails à partir de l’ du, cliquez sur une instance de service, puis cliquez sur lelien hypertexte associé au nom. Cela ouvre un rail droit qui fournit des détails supplémentaires tels que la description, la fréquence de notation, l’objectif de prévision et la population admissible. De plus, vous pouvez modifier et supprimer l’instance en cliquant sur **Modifier** ou **Supprimer**.

![rail droit](./images/insights/success-run.png)

>[!NOTE] Dans le  d’échec d’une exécution de score, un message d’erreur est fourni. Le message d’erreur est répertorié sous les détails *de la* dernière exécution dans le rail droit, qui est uniquement visible pour les exécutions ayant échoué.

![message d’exécution en échec](./images/insights/failed-run.png)

La deuxième manière de des détails supplémentaires pour une instance de service se trouve dans la page des connaissances. Vous pouvez cliquer sur **Afficher plus** dans l’angle supérieur droit pour remplir une liste déroulante. Les détails sont répertoriés, tels que la définition du score, la date de création et le type de propension. Pour plus d’informations sur l’une des propriétés répertoriées, consultez le guide [d’utilisation de l’IA](./user-guide.md)du client.

![afficher plus](./images/insights/landing-show-more.png)

![afficher plus](./images/insights/show-more.png)

### Modification d’une instance

Pour modifier une instance, cliquez sur **Modifier** dans le volet de navigation supérieur droit.

![cliquez sur le bouton Modifier](./images/insights/edit-button.png)

La boîte de dialogue Modifier s’affiche, vous permettant de modifier la *description* et la fréquence de *score* de l’instance. Pour confirmer vos modifications et fermer la boîte de dialogue, cliquez sur **Modifier** dans le coin inférieur droit.

![modifier la fenêtre contextuelle](./images/insights/edit-instance.png)

### Autres actions

Le bouton Actions **** Plus se trouve dans le volet de navigation supérieur droit en regard de **Modifier**. Cliquez sur **Plus pour** ouvrir une liste déroulante qui vous permet de sélectionner l’une des opérations suivantes :

- **Supprimer**: Supprime l’instance.
- **Accéder aux scores**: En cliquant sur les scores ** d’accès, vous ouvrez une boîte de dialogue contenant un lien vers les scores de [téléchargement pour le didacticiel d’API](./download-scores.md) client. La boîte de dialogue fournit également l’ID de jeu de données requis pour effectuer des appels d’API.
- **exécuter l&#39;historique**: Une boîte de dialogue contenant un  de toutes les exécutions de notation associées à l’instance de service s’affiche.

![autres actions](./images/insights/more-actions.png)

## Résumé du score

Scoring Summary (Résumé du score) affiche le nombre total de  marqués et les classe dans des compartiments contenant une propension élevée, moyenne et faible. Les intervalles de propension sont déterminés en fonction de la plage de score, faible est inférieur à 24, moyen est de 25 à 74 et élevé est supérieur à 74. Chaque compartiment a une couleur correspondant à la légende.

>[!NOTE] S’il s’agit d’un score de propension à la conversion, les scores élevés sont en vert et les scores faibles en rouge. Si vous prédites la propension de l&#39;enfant à se retourner, les scores élevés sont en rouge et les scores faibles en vert. Le compartiment moyen reste jaune quel que soit le type de propension choisi.

![récapitulatif des notes](./images/insights/scoring-summary.png)

## Distribution des scores

La carte *Distribution des scores* vous donne un résumé visuel de la population en fonction du score. Les couleurs affichées dans la carte *Distribution des scores* représentent le type de score de propension généré.

![distribution des notes](./images/insights/distribution-of-scores.png)

## Facteurs influents

Pour chaque intervalle de score, une carte est générée qui présente les 10 principaux facteurs influents pour ce intervalle. Les facteurs influents vous donnent des détails supplémentaires sur la raison pour laquelle vos clients appartiennent à différents groupes de score.

![Facteurs influents](./images/insights/influential-factors.png)

### Création d’un segment

Le fait de cliquer sur le bouton **Créer un segment** dans l’un des intervalles de propension faible, moyenne et élevée vous redirige vers le créateur de segments.

![Cliquez sur Créer un segment](./images/insights/influential-factors-create-segment.png)

![Création d’un segment](./images/insights/create-segment.png)

Le créateur de segments est utilisé pour définir un segment. Toutefois, l’API du client a déjà effectué le travail pour vous. Pour terminer la création de votre segment, il vous suffit de renseigner le ** Nom *et* Descriptionsitué dans le rail droit de l’interface utilisateur du créateur de segments. Après avoir donné au segment un nom et une description, cliquez sur **Enregistrer** dans le coin supérieur droit.

>!![NOTE] Comme les scores de propension sont écrits pour chaque  de, ils sont disponibles dans le créateur de segments comme tout autre attribut  de. Lorsque vous accédez au créateur de segments pour créer de nouveaux segments, vous pouvez voir tous les scores de propension sous votre   API du client.

![Remplissage de segment dans](./images/insights/segment-saving.png)

Pour  votre nouveau segment dans l’interface utilisateur de la plateforme, cliquez sur **Segments** dans le volet de navigation de gauche. La page *Parcourir* s’affiche et affiche tous les segments disponibles.

![Tous vos segments](./images/insights/Segments-dashboard.png)

## Étapes suivantes

Ce décrit les informations fournies par une instance de service AI du client. Vous pouvez maintenant continuer à suivre le didacticiel sur le [téléchargement des scores dans l’API](./download-scores.md) client ou consulter les autres guides [Adobe Intelligent Services](../home.md) proposés.