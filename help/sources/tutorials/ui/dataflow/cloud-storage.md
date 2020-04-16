---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Configuration d’un flux de données pour un connecteur de Cloud  dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 298afbd97096fc01c7fcc05fa794b8e356c6835e

---


# Configuration d’un flux de données pour un connecteur de Cloud  dans l’interface utilisateur

Un flux de données est un planifié qui récupère et ingère des données d’une source dans un jeu de données de la plateforme. Ce didacticiel décrit les étapes à suivre pour configurer un nouveau flux de données à l’aide de votre connecteur de base de  Cloud.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Système](../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
   * [Principes de base de la composition](../../../../xdm/schema/composition.md)de  : Découvrez les éléments de base des  XDM, y compris les principes clés et les bonnes pratiques en matière de composition de .
   * [Didacticiel](../../../../xdm/tutorials/create-schema-ui.md)de l’éditeur de  : Découvrez comment créer des  personnalisées à l’aide de l’interface utilisateur de l’éditeur de  de.
* [](../../../../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.

En outre, ce didacticiel nécessite que vous ayez déjà créé un cloud  connecteur . Vous trouverez un de didacticiels pour la création de différents connecteurs de cloud  dans l’interface utilisateur dans la présentation [des connecteurs](../../../home.md)source.

### Formats de fichiers pris en charge

Experience Platform prend en charge les formats de fichier suivants pour être assimilés à partir d’un  externe  :

* Valeurs séparées par des délimiteurs (DSV) : La prise en charge des fichiers de données au format DSV est actuellement limitée aux valeurs séparées par des virgules. La valeur des en-têtes de champ dans les fichiers au format DSV ne doit être composée que de caractères alphanumériques et de traits de soulignement. La prise en charge des fichiers DSV généraux sera assurée à l’avenir.
* Notation d’objet JavaScript (JSON) : Les fichiers de données au format JSON doivent être compatibles XDM.
* Apache Parquet : Les fichiers de données au format Parquet doivent être compatibles XDM.

## Sélectionner des données

Après avoir créé votre cloud   connecteur, l’étape *Sélectionner les données* s’affiche, ce qui vous permet d’explorer votre cloud  la hiérarchie des.

* La moitié gauche de l&#39;interface est un navigateur de répertoires, qui affiche les fichiers et répertoires de votre serveur.
* La moitié droite de l’interface vous permet de  jusqu’à 100 lignes de données à partir d’un fichier compatible.

Le fait de cliquer sur un dossier répertorié vous permet de parcourir la hiérarchie des dossiers dans des dossiers plus approfondis. Une fois que vous avez sélectionné un fichier ou un dossier compatible, la liste déroulante **Sélectionner le format** de données s’affiche, dans laquelle vous pouvez choisir un format pour afficher les données dans la fenêtre de  du.

![](../../../images/tutorials/dataflow/cloud-storage/select-data.png)

Une fois la fenêtre de  renseignée, vous pouvez cliquer sur **Suivant** pour télécharger tous les fichiers du dossier sélectionné. Si vous souhaitez télécharger vers un fichier spécifique, sélectionnez ce fichier dans la liste avant de cliquer sur **Suivant**.

>[!NOTE] Les formats de fichier pris en charge sont CSV, JSON et Parquet. Les fichiers JSON et Parquet doivent être compatibles XDM.

![](../../../images/tutorials/dataflow/cloud-storage/select-data-next.png)

## Mappage des champs de données à un XDM

L’étape *Mappage* s’affiche, fournissant une interface interactive permettant de mapper les données source à un jeu de données de plateforme. Les fichiers source au format JSON ou Parquet doivent être conformes XDM et vous ne devez pas configurer manuellement le mappage. A l’inverse, les fichiers CSV nécessitent de configurer explicitement le mappage, mais vous permettent de sélectionner les champs de données source à mapper.

Choisissez un jeu de données dans lequel les données entrantes doivent être assimilées. Vous pouvez utiliser un jeu de données existant ou en créer un nouveau.

**Utiliser un jeu de données existant**

Pour importer des données dans un jeu de données existant, sélectionnez **Utiliser un jeu de données** existant, puis cliquez sur l’icône Jeu de données.

![](../../../images/tutorials/dataflow/cloud-storage/use-existing-data.png)

La boîte de dialogue _Sélectionner un jeu de données_ s’affiche. Recherchez le jeu de données que vous souhaitez utiliser, sélectionnez-le, puis cliquez sur **Continuer**.

![](../../../images/tutorials/dataflow/cloud-storage/select-existing-data.png)

**Utiliser un nouveau jeu de données**

Pour importer des données dans un nouveau jeu de données, sélectionnez **Créer un jeu de données** et saisissez un nom et une description pour le jeu de données dans les champs fournis. Cliquez ensuite sur l’icône  du.

![](../../../images/tutorials/dataflow/cloud-storage/use-new-schema.png)

La boîte de dialogue _Sélectionner_ du s’affiche. Sélectionnez le à appliquer au nouveau jeu de données, puis cliquez sur **Terminé**.

![](../../../images/tutorials/dataflow/cloud-storage/select-schema.png)

Selon vos besoins, vous pouvez choisir de mapper directement les champs ou utiliser les fonctions de mappage pour transformer les données source afin de dériver des valeurs calculées ou calculées. Pour plus d’informations sur les fonctions de mappage et de mappage des données, reportez-vous au didacticiel sur le [mappage des données CSV aux champs](../../../../ingestion/tutorials/map-a-csv-file.md)de  XDM.

Une fois les données source mises en correspondance, cliquez sur **Suivant**.

![](../../../images/tutorials/dataflow/cloud-storage/mapping.png)

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

![](../../../images/tutorials/dataflow/cloud-storage/scheduling.png)

## Nommer votre flux de données

L’étape de flux ** Nom s’affiche, vous permettant de nommer et de décrire brièvement votre nouveau flux de données.

Spécifiez les valeurs du flux de données, puis cliquez sur **Suivant**.

![](../../../images/tutorials/dataflow/cloud-storage/name-your-dataflow.png)

### Consultez votre flux de données

L’étape *Révision* s’affiche, vous permettant de vérifier votre nouveau flux de données avant sa création. Les détails sont regroupés dans le  suivant :

* *Détails* de la source : Affiche le type de source, le chemin d’accès approprié du fichier source choisi et le nombre de colonnes contenues dans ce fichier source.
* *Détails* du : Indique dans quel jeu de données les données source sont assimilées, y compris le auquel le jeu de données adhère.
* *Détails* de planification : Affiche la période active, la fréquence et l’intervalle du calendrier d’assimilation.

Une fois que vous avez examiné votre flux de données, cliquez sur **Terminer** et accordez un peu de temps pour que le flux de données soit créé.

![](../../../images/tutorials/dataflow/cloud-storage/review.png)

## Surveiller votre flux de données

Une fois que votre cloud   flux de données a été créé, vous pouvez surveiller les données qui y sont assimilées. Suivez les étapes ci-dessous pour accéder au moniteur de jeux de données d’un flux de données.

Dans l’espace de travail *Sources* , cliquez sur l’onglet **Parcourir** pour vos connexions de base. Dans le  affiché, recherchez la connexion qui contient le flux de données à surveiller en cliquant sur son nom.

![](../../../images/tutorials/dataflow/cloud-storage/browse.png)

L’écran  *Source* s’affiche. A partir de là, cliquez sur le nom d’un jeu de données dont   vous souhaitez surveiller.

![](../../../images/tutorials/dataflow/cloud-storage/source-activity.png)

L’écran  de de *données* s’affiche. Cette page affiche le taux de messages consommés sous forme de graphique.

![](../../../images/tutorials/dataflow/cloud-storage/dataset-activity.png)

Sous le graphique se trouve un  de lots qui ont été assimilés dans le jeu de données, indiquant leur état (réussi ou échoué) et le nombre d&#39;enregistrements ingérés. Si un lot est assimilé à un jeu de données compatible avec les , le nombre d’ et d’identités assimilées s’affiche.

Vous pouvez  plus de détails sur un lot répertorié en cliquant sur son ID.

Pour plus d&#39;informations sur la surveillance des jeux de données et l&#39;assimilation, consultez le didacticiel sur la [surveillance des flux de données](../../../../ingestion/quality/monitor-data-flows.md)en flux continu.

## Étapes suivantes

En suivant ce didacticiel, vous avez réussi à créer un flux de données pour importer des données à partir d’un Cloud externe   et à mieux comprendre la surveillance des jeux de données. Les données entrantes peuvent désormais être utilisées par les services Plateforme en aval, tels que les  de clients en temps réel et l’espace de travail des sciences de données. Pour plus d’informations, reportez-vous au  suivant :

* [Présentation du profil client en temps réel](../../../../profile/home.md)
* [Présentation de l’espace de travail Data Science](../../../../data-science-workspace/home.md)

## Annexe

Les sections suivantes fournissent des informations supplémentaires sur l’utilisation des connecteurs source.

### Désactivation d’un flux de données

Lorsqu’un flux de données est créé, il devient immédiatement actif et ingère les données selon la planification qui lui a été donnée. Vous pouvez désactiver un flux de données actif à tout moment en suivant les instructions ci-dessous.

Dans l’espace de travail *Sources* , cliquez sur l’onglet **Parcourir** . Cliquez ensuite sur le nom de la connexion de base associée au flux de données actif que vous souhaitez désactiver.

![](../../../images/tutorials/dataflow/cloud-storage/browse.png)

La page  *source* du s’affiche. Sélectionnez le flux de données actif dans le pour ouvrir sa colonne *Propriétés* sur le côté droit de l’écran, qui contient un bouton d’activation **** de l’option de basculement. Cliquez sur la bascule pour désactiver le flux de données. La même bascule peut être utilisée pour réactiver un flux de données après sa désactivation.

![](../../../images/tutorials/dataflow/cloud-storage/disable-source.png)

### Activation des données d’entrée pour la population de 

Les données entrantes de votre connecteur source peuvent être utilisées pour enrichir et renseigner vos données de client en temps réel. Pour plus d’informations sur le renseignement de vos données de Real-Customer, consultez le didacticiel sur la population [de ](../profile.md).
