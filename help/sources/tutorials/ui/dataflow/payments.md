---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Configuration d’un flux de données pour un connecteur de paiement dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 1eb9b470ddb048c5825c18c2a998a6b736ddc42a
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 1%

---


# Configuration d’un flux de données pour un connecteur de paiement dans l’interface utilisateur

Un flux de données est une tâche planifiée qui récupère et ingère des données d’une source dans un jeu de données Adobe Experience Platform. Ce didacticiel décrit les étapes à suivre pour configurer un nouveau flux de données à l’aide de votre compte de paiement.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

- [Système](../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
   - [Principes de base de la composition](../../../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   - [Didacticiel](../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [Profil](../../../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

En outre, ce didacticiel nécessite que vous ayez déjà créé un compte de paiement. Vous trouverez une liste de didacticiels pour la création de différents connecteurs de paiement dans l’interface utilisateur dans l’aperçu [des connecteurs](../../../home.md)source.

## Sélectionner des données

Après avoir créé votre compte de paiement, l&#39;étape *Sélectionner les données* s&#39;affiche, ce qui vous permet d&#39;explorer la hiérarchie des fichiers dans une interface interactive.

- La moitié gauche de l&#39;interface est un navigateur d&#39;annuaire qui affiche les fichiers et répertoires de votre serveur.
- La moitié droite de l&#39;interface vous permet de prévisualisation jusqu&#39;à 100 lignes de données à partir d&#39;un fichier compatible.

Sélectionnez le répertoire que vous souhaitez utiliser, puis sélectionnez **Suivant**.

![add-data](../../../images/tutorials/dataflow/payments/add-data.png)

## Mappage des champs de données à un schéma XDM

L’étape *Mappage* s’affiche, fournissant une interface interactive permettant de mapper les données source à un jeu de données de plateforme.

Choisissez un jeu de données dans lequel les données entrantes doivent être assimilées. Vous pouvez utiliser un jeu de données existant ou en créer un nouveau.

### Utiliser un jeu de données existant

Pour importer des données dans un jeu de données existant, sélectionnez **Utiliser un jeu de données** existant, puis cliquez sur l’icône Jeu de données.

![use-existing-dataset](../../../images/tutorials/dataflow/payments/existing-dataset.png)

La boîte de dialogue *Sélectionner un jeu de données* s&#39;affiche. Recherchez le jeu de données que vous souhaitez utiliser, sélectionnez-le, puis cliquez sur **Continuer**.

![select-existing-dataset](../../../images/tutorials/dataflow/payments/select-dataset.png)

### Utiliser un nouveau jeu de données

Pour importer des données dans un nouveau jeu de données, sélectionnez **Créer un jeu de données** et saisissez un nom et une description pour le jeu de données dans les champs fournis.

Au cours de ce processus, vous pouvez également activer les tests de diagnostic *d&#39;assimilation* *partielle et d&#39;* erreur. L&#39;activation de l&#39;assimilation ** partielle permet d&#39;assimiler des données contenant des erreurs, jusqu&#39;à un certain seuil que vous pouvez définir. L’activation des diagnostics d’erreur fournit des détails sur les données incorrectes qui sont mises en lots séparément. Pour plus d&#39;informations, consultez la présentation [de l&#39;assimilation](../../../../ingestion/batch-ingestion/partial.md)partielle des lots.

Lorsque vous avez terminé, cliquez sur l’icône schéma.

![create-new-dataset](../../../images/tutorials/dataflow/payments/new-dataset.png)

La boîte de dialogue *Sélectionner un schéma* s&#39;affiche. Sélectionnez le schéma à appliquer au nouveau jeu de données, puis cliquez sur **Terminé**.

![sélection-schéma](../../../images/tutorials/dataflow/payments/select-schema.png)

Selon vos besoins, vous pouvez choisir de mapper directement les champs ou utiliser les fonctions de mappage pour transformer les données source afin de dériver des valeurs calculées ou calculées. Pour plus d’informations sur les fonctions de mappage et de mappage de données, consultez le didacticiel sur le [mappage des données CSV aux champs](../../../../ingestion/tutorials/map-a-csv-file.md)de schéma XDM.

L’écran *Mappage* vous permet également de définir la colonne ** Delta. Lorsque le flux de jeux de données est créé, vous pouvez définir n’importe quel champ d’horodatage comme base pour déterminer les enregistrements à importer dans les ingérations incrémentielles planifiées.

Une fois les données source mises en correspondance, cliquez sur **Suivant**.

![](../../../images/tutorials/dataflow/payments/mapping.png)

## Planifier les exécutions d&#39;assimilation

L&#39;étape *Planification* s&#39;affiche, ce qui vous permet de configurer un programme d&#39;assimilation pour assimiler automatiquement les données source sélectionnées à l&#39;aide des mappages configurés. Le tableau suivant décrit les différents champs configurables pour la planification :

| Champ | Description |
| --- | --- |
| Fréquence | Les fréquences sélectionnées sont les suivantes : Minute, Heure, Jour et Semaine. |
| Intervalle | Entier qui définit l’intervalle pour la fréquence sélectionnée. |
| Début | Horodatage UTC pour lequel la toute première importation aura lieu. |
| Renvoi | Valeur booléenne qui détermine quelles données sont initialement ingérées. Si le *renvoi* est activé, tous les fichiers actuels du chemin d’accès spécifié seront ingérés lors de la première assimilation planifiée. Si le *renvoi* est désactivé, seuls les fichiers chargés entre la première exécution de l’assimilation et le délai *de* Début seront ingérés. Les fichiers chargés avant l&#39;heure *de* Début ne seront pas ingérés. |

Les flux de données sont conçus pour intégrer automatiquement les données sur une base planifiée. Si vous souhaitez effectuer une seule assimilation via ce flux de travail, vous pouvez le faire en configurant la **fréquence** sur &quot;Jour&quot; et en appliquant un nombre très élevé pour l’ **intervalle**, tel que 10000 ou un nombre similaire.

Indiquez les valeurs de la planification et cliquez sur **Suivant**.

![scheduling](../../../images/tutorials/dataflow/payments/scheduling.png)

## Nommer votre flux de données

L&#39;étape détaillée *du flux de* jeux de données s&#39;affiche, où vous devez fournir un nom et une description facultative du flux de jeux de données. Sélectionnez **Suivant** lorsque vous avez terminé.

![dataset-flow-details](../../../images/tutorials/dataflow/payments/dataset-flow-details.png)

## Vérifier le flux de vos jeux de données

L’étape *Révision* s’affiche, vous permettant de vérifier votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

- *Connexion*: Indique le type de source, le chemin d’accès approprié du fichier source choisi et le nombre de colonnes qu’il contient.
- *Attribuer des champs* de jeu de données et de mappage : Affiche le jeu de données dans lequel les données source sont ingérées, y compris le schéma auquel le jeu de données adhère.
- *Planification*: Affiche la période active, la fréquence et l&#39;intervalle du programme d&#39;assimilation.

Une fois que vous avez passé en revue votre flux de données, cliquez sur **Terminer** et accordez un certain temps à la création du flux de données.

![examiner](../../../images/tutorials/dataflow/payments/review.png)

## Surveiller le flux de vos jeux de données

Une fois le flux de votre jeu de données créé, vous pouvez surveiller les données qui y sont ingérées. Pour plus d&#39;informations sur la façon de surveiller vos flux de jeux de données, consultez le didacticiel sur les flux de [comptes et de jeux de données](../monitor.md).

## Étapes suivantes

En suivant ce didacticiel, vous avez réussi à créer un flux de jeux de données afin d’importer des données d’un système d’automatisation du marketing et d’obtenir des informations sur la surveillance des jeux de données. Les données entrantes peuvent désormais être utilisées par les services Plateforme en aval, tels que le Profil client en temps réel et l’espace de travail Data Science. Pour plus d’informations, voir les documents suivants :

- [Présentation du profil client en temps réel](../../../../profile/home.md)
- [Présentation de Data Science Workspace](../../../../data-science-workspace/home.md)

## Annexe

Les sections suivantes fournissent des informations supplémentaires sur l’utilisation des connecteurs source.

### Désactivation d’un flux de jeu de données

Lorsqu&#39;un flux de jeu de données est créé, il devient immédiatement actif et ingère les données selon le calendrier qui lui a été donné. Vous pouvez désactiver un flux de jeux de données actif à tout moment en suivant les instructions ci-dessous.

Dans l&#39;écran Flux *de* jeux de données, sélectionnez le nom du flux de jeux de données que vous souhaitez désactiver.

![browse-dataset-flow](../../../images/tutorials/dataflow/payments/view-dataset-flows.png)

La colonne *Propriétés* s’affiche à droite de l’écran. Ce panneau contient un bouton **Activer** la bascule. Cliquez sur la bascule pour désactiver le flux de données. La même bascule peut être utilisée pour réactiver un flux de données après sa désactivation.

![disable](../../../images/tutorials/dataflow/payments/disable.png)

### Activer les données entrantes pour la population de Profils

Les données entrantes de votre connecteur source peuvent être utilisées pour enrichir et renseigner vos données de Profil client en temps réel. Pour plus d’informations sur le renseignement de vos données de Profil client réel, voir le didacticiel sur la population [de](../profile.md)Profils.
