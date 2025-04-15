---
title: Mettre à jour la date de fin des flux de données d’exportation de jeux de données (Action requise pour le 1er mai 2025)
type: Tutorial
hide: true
hidefromtoc: true
description: Découvrez comment mettre à jour la date de fin des flux de données d’exportation de jeux de données avec une date de fin actuelle fixée au 1er mai 2025.
source-git-commit: aeabbb56002f8640b79ff3a7e3dc532d01ebbadf
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Mettre à jour la date de fin des flux de données d’exportation de jeux de données (Action requise pour le 1er mai 2025)

>[!IMPORTANT]
>
>Les actions de cette page s’appliquent si votre organisation a configuré des flux de données d’exportation de jeux de données avant la version de septembre 2024 d’Experience Platform.

## Que se passe-t-il ?

La version [septembre 2024 d’Experience Platform](/help/release-notes/latest/latest.md#destinations) a introduit l’option permettant de définir une date `endTime` pour l’exportation des flux de données de jeux de données. Adobe a également introduit une date de fin par défaut du 1er mai 2025 pour tous les flux de données d’exportation de jeux de données créés *avant la version de septembre 2024*. Ces flux de données affichent actuellement un message similaire à celui illustré ci-dessous.

![Notification de l’interface utilisateur sur la nécessité de mettre à jour la date de fin du flux de données du jeu de données d’exportation.](/help/destinations/assets/ui/export-datasets/update-end-date.png)

**Élément d’action** : pour l’un de ces flux de données, vous devez mettre à jour manuellement la date de fin avant son expiration ; sinon, vos exportations s’arrêteront. Utilisez l’interface utilisateur d’Experience Platform pour identifier les flux de données qui doivent s’arrêter le 1er mai 2025.

## Pourquoi suis-je averti ?

Votre organisation a été identifiée comme ayant des flux de données d’exportation de jeux de données actifs avec une date de fin fixée au 1er mai 2025.

## Utiliser l’interface utilisateur pour mettre à jour la date de fin

Utilisez l’interface utilisateur d’Experience Platform pour identifier les flux de données dont la date de fin est le 1er mai 2025 et les mettre à jour à une date ultérieure.

### Rechercher les flux de données à mettre à jour

Accédez à **Destinations > Parcourir** et recherchez le type de données **Jeux de données** dans la colonne **Type de données**, comme illustré ci-dessous. Sélectionnez les flux de données de votre choix pour les examiner.

![Flux de données d’exportation de jeu de données surligné dans l’onglet Parcourir.](/help/destinations/assets/ui/export-datasets/view-dataset-dataflows.png)

### Mettre à jour la date de fin des flux de données

Pour mettre à jour la date de fin des flux de données :

1. Dans les flux de données que vous avez sélectionnés pour inspection à l’étape précédente, sélectionnez **Exporter des jeux de données**.
   ![Contrôle d’exportation des jeux de données mis en surbrillance dans l’onglet Parcourir.](/help/destinations/assets/ui/export-datasets/export-datasets-control-highlighted.png)
2. Dans le workflow, passez à l’étape **Planification** et sélectionnez **Modifier le planning**.
   ![Modifier le contrôle de planification mis en surbrillance à l’étape Planification.](/help/destinations/assets/ui/export-datasets/edit-schedule-control-highlighted.png)
3. Sélectionnez une date de fin postérieure au 1er mai 2025 et sélectionnez **Enregistrer**.
   ![Sélectionnez le contrôle de date de fin en surbrillance à l’étape Planification.](/help/destinations/assets/ui/export-datasets/select-end-date.png)
4. Passez à la fin du workflow et enregistrez vos mises à jour.

Pour obtenir des informations détaillées sur l’étape de planification, consultez le tutoriel [interface utilisateur d’exportation de jeux de données](/help/destinations/api/export-datasets.md#scheduling).

## Utiliser l’API pour mettre à jour la date de fin

### Rechercher les flux de données à mettre à jour

### Mettre à jour la date de fin des flux de données
