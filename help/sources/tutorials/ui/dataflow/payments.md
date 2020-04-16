---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Configuration d’un flux de données pour un connecteur de paiement dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 1eb9b470ddb048c5825c18c2a998a6b736ddc42a

---


# Configuration d’un flux de données pour un connecteur de paiement dans l’interface utilisateur

Un flux de données est un planifié qui récupère et ingère des données d’une source dans un jeu de données Adobe Experience Platform. Ce didacticiel décrit les étapes à suivre pour configurer un nouveau flux de données à l’aide de votre compte de paiement.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

- [Système](../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
   - [Principes de base de la composition](../../../../xdm/schema/composition.md)de  : Découvrez les éléments de base des  XDM, y compris les principes clés et les bonnes pratiques en matière de composition de .
   - [Didacticiel](../../../../xdm/tutorials/create-schema-ui.md)de l’éditeur de  : Découvrez comment créer des  personnalisées à l’aide de l’interface utilisateur de l’éditeur de  de.
- [](../../../../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.

En outre, ce didacticiel nécessite que vous ayez déjà créé un compte de paiement. Un de didacticiels pour la création de différents connecteurs de paiement dans l’interface utilisateur se trouve dans la présentation [des connecteurs](../../../home.md)source.

## Sélectionner des données

Après avoir créé votre compte de paiement, l’étape *Sélectionner les données* s’affiche, ce qui vous permet d’explorer la hiérarchie des fichiers dans une interface interactive.

- La moitié gauche de l&#39;interface est un navigateur de répertoires, qui affiche les fichiers et répertoires de votre serveur.
- La moitié droite de l’interface vous permet de  jusqu’à 100 lignes de données à partir d’un fichier compatible.

Sélectionnez le répertoire que vous souhaitez utiliser, puis sélectionnez **Suivant**.

![add-data](../../../images/tutorials/dataflow/payments/add-data.png)

## Mappage des champs de données à un XDM

L’étape *Mappage* s’affiche, fournissant une interface interactive permettant de mapper les données source à un jeu de données de plateforme.

Choisissez un jeu de données dans lequel les données entrantes doivent être assimilées. Vous pouvez utiliser un jeu de données existant ou en créer un nouveau.

### Utiliser un jeu de données existant

Pour importer des données dans un jeu de données existant, sélectionnez **Utiliser un jeu de données** existant, puis cliquez sur l’icône Jeu de données.

![use-existing-dataset](../../../images/tutorials/dataflow/payments/existing-dataset.png)

La boîte de dialogue *Sélectionner un jeu de données* s’affiche. Recherchez le jeu de données que vous souhaitez utiliser, sélectionnez-le, puis cliquez sur **Continuer**.

![select-existing-dataset](../../../images/tutorials/dataflow/payments/select-dataset.png)

### Utiliser un nouveau jeu de données

Pour importer des données dans un nouveau jeu de données, sélectionnez **Créer un jeu de données** et saisissez un nom et une description pour le jeu de données dans les champs fournis.

Au cours de ce processus, vous pouvez également activer les tests *d’assimilation* partielle et les tests de diagnostic des *erreurs*. L’activation de l’assimilation ** partielle permet d’assimiler des données contenant des erreurs, jusqu’à un certain seuil que vous pouvez définir. L’activation des diagnostics d’erreur fournit des détails sur les données incorrectes qui sont mises en lots séparément. Pour plus d’informations, voir la présentation [de l’assimilation par lots](../../../../ingestion/batch-ingestion/partial.md)partielle.

Lorsque vous avez terminé, cliquez sur l’icône  du.

![create-new-dataset](../../../images/tutorials/dataflow/payments/new-dataset.png)

La boîte de dialogue *Sélectionner* du s’affiche. Sélectionnez le à appliquer au nouveau jeu de données, puis cliquez sur **Terminé**.

![select-](../../../images/tutorials/dataflow/payments/select-schema.png)

Selon vos besoins, vous pouvez choisir de mapper directement les champs ou utiliser les fonctions de mappage pour transformer les données source afin de dériver des valeurs calculées ou calculées. Pour plus d’informations sur les fonctions de mappage et de mappage des données, reportez-vous au didacticiel sur le [mappage des données CSV aux champs](../../../../ingestion/tutorials/map-a-csv-file.md)de  XDM.

L’écran *Mappage* vous permet également de définir la colonne ** Delta. Lors de la création du flux de jeux de données, vous pouvez définir n’importe quel champ d’horodatage comme base pour décider quels enregistrements importer dans les impressions incrémentielles planifiées.

Une fois les données source mises en correspondance, cliquez sur **Suivant**.

![](../../../images/tutorials/dataflow/payments/mapping.png)

## Planifier les exécutions d&#39;assimilation

L’étape *Planification* s’affiche, ce qui vous permet de configurer une planification d’assimilation afin d’assimiler automatiquement les données source sélectionnées à l’aide des mappages configurés. Le tableau suivant décrit les différents champs configurables pour la planification :

| Champ | Description |
| --- | --- |
| Fréquence | Les fréquences sélectionnables sont les suivantes : minute, heure, jour et semaine. |
| Intervalle | Entier qui définit l’intervalle pour la fréquence sélectionnée. |
|  de | Horodatage UTC pour lequel la première ingestion aura lieu. |
| Renvoi | Valeur booléenne qui détermine les données qui sont initialement assimilées. Si le *renvoi* est activé, tous les fichiers actuels du chemin spécifié seront assimilés lors de la première assimilation planifiée. Si le *renvoi* est désactivé, seuls les fichiers chargés entre la première exécution de l’assimilation et l’heure *de  du* sont assimilés. Les fichiers chargés avant l’heure *du* ne seront pas assimilés. |

Les flux de données sont conçus pour assimiler automatiquement les données sur une base planifiée. Si vous souhaitez effectuer une seule assimilation via ce flux de travail, vous pouvez le faire en configurant la **fréquence** sur &quot;Jour&quot; et en appliquant un nombre très élevé pour l’ **intervalle**, par exemple 10000 ou un nombre similaire.

Indiquez les valeurs de la planification et cliquez sur **Suivant**.

![scheduling](../../../images/tutorials/dataflow/payments/scheduling.png)

## Nommer votre flux de données

L’étape détaillée *du flux des jeux de* données s’affiche, où vous devez indiquer un nom et une description facultative du flux des jeux de données. Sélectionnez **Suivant** lorsque vous avez terminé.

![dataset-flow-details](../../../images/tutorials/dataflow/payments/dataset-flow-details.png)

## Vérifier le flux des jeux de données

L’étape *Révision* s’affiche, vous permettant de vérifier votre nouveau flux de données avant sa création. Les détails sont regroupés dans le  suivant :

- *Connexion*: Affiche le type de source, le chemin d’accès approprié du fichier source choisi et le nombre de colonnes contenues dans ce fichier source.
- *Affecter des champs* de jeu de données et de mappage : Indique dans quel jeu de données les données source sont assimilées, y compris le auquel le jeu de données adhère.
- *Planification*: Affiche la période active, la fréquence et l’intervalle du calendrier d’assimilation.

Une fois que vous avez examiné votre flux de données, cliquez sur **Terminer** et accordez un peu de temps pour que le flux de données soit créé.

![révision](../../../images/tutorials/dataflow/payments/review.png)

## Surveiller le flux des jeux de données

Une fois que votre flux de jeux de données a été créé, vous pouvez surveiller les données qui y sont assimilées. Pour plus d&#39;informations sur la manière de surveiller vos flux de jeux de données, consultez le didacticiel sur les flux de [comptes et de jeux de données](../monitor.md).

## Étapes suivantes

En suivant ce didacticiel, vous avez réussi à créer un flux de jeux de données afin d’importer des données d’un système d’automatisation marketing et d’obtenir des informations sur la surveillance des jeux de données. Les données entrantes peuvent désormais être utilisées par les services Plateforme en aval, tels que les  de clients en temps réel et l’espace de travail des sciences de données. Pour plus d’informations, reportez-vous au  suivant :

- [Présentation du profil client en temps réel](../../../../profile/home.md)
- [Présentation de l’espace de travail Data Science](../../../../data-science-workspace/home.md)

## Annexe

Les sections suivantes fournissent des informations supplémentaires sur l’utilisation des connecteurs source.

### Désactivation d’un flux de jeux de données

Lors de la création d’un flux de jeux de données, il devient immédiatement actif et ingère les données selon la planification qui lui a été donnée. Vous pouvez désactiver un flux de jeux de données actif à tout moment en suivant les instructions ci-dessous.

Dans l’écran Flux *de* jeux de données, sélectionnez le nom du flux de jeux de données que vous souhaitez désactiver.

![browse-dataset-flow](../../../images/tutorials/dataflow/payments/view-dataset-flows.png)

La colonne *Propriétés* s’affiche sur le côté droit de l’écran. Ce panneau contient un bouton bascule **Activé** . Cliquez sur la bascule pour désactiver le flux de données. La même bascule peut être utilisée pour réactiver un flux de données après sa désactivation.

![disable](../../../images/tutorials/dataflow/payments/disable.png)

### Activation des données d’entrée pour la population de 

Les données entrantes de votre connecteur source peuvent être utilisées pour enrichir et renseigner vos données de client en temps réel. Pour plus d’informations sur le renseignement de vos données de Real-Customer, consultez le didacticiel sur la population [de ](../profile.md).
