---
solution: Experience Platform
title: Téléchargement de tableaux de bord Experience Platform au format PDF
type: Documentation
description: Enregistrez des copies des visualisations de vos tableaux de bord à l’aide de la fonctionnalité de téléchargement au format PDF disponible dans l’interface utilisateur d’Experience Platform.
exl-id: 838e98a0-ce2e-4dcd-8c8f-d28ef2cb8315
TQID: https://experienceleague.adobe.com/2LtQLhdwTGsXDIs1H3gTvQ1CiZ2KXDKenEZMADWJqOs
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 587
ht-degree: 58%

---

# Téléchargement de tableaux de bord au format PDF

Les tableaux de bord de Adobe Experience Platform peuvent être téléchargés sur PDF à partir de l’interface utilisateur d’Experience Platform afin de faciliter le partage d’informations avec les membres de votre organisation.

Ce document résume la procédure à suivre pour télécharger des tableaux de bord à l’aide de l’interface utilisateur d’Experience Platform et enregistrer le tableau de bord dans PDF à l’aide du menu d’impression par défaut du navigateur.

>[!WARNING]
>
>Les données contenues dans vos tableaux de bord peuvent inclure des informations d’identification personnelle (PII) sur vos clients ou des données sensibles liées à votre organisation. Toutes les données des tableaux de bord enregistrées au format PDF doivent être gérées de manière appropriée, conformément aux directives relatives à la confidentialité des données de votre organisation.

## Téléchargement de tableau de bord

Pour commencer à télécharger un tableau de bord, accédez au tableau de bord que vous souhaitez télécharger (par exemple, le tableau de bord [!UICONTROL Profiles]), puis sélectionnez le menu Plus d’options (**`...`**) dans le coin supérieur droit du tableau de bord. Ensuite, sélectionnez **[!UICONTROL Download]**.

![Tableau de bord Profils Experience Platform avec les points de suspension et le menu déroulant Télécharger mis en surbrillance.](images/download/download-button.png)

## Prévisualisation PDF

Après avoir sélectionné **[!UICONTROL Download]**, le menu d’impression par défaut de votre navigateur s’ouvre. Cet exemple montre l’affichage du menu d’impression de Google Chrome.

Le menu d’impression vous permet de prévisualiser le PDF qui sera enregistré. Le PDF est une véritable représentation des widgets du tableau de bord tels qu’ils apparaissent dans l’interface utilisateur d’Experience Platform. La taille du PDF est automatiquement ajustée pour afficher tous les widgets du tableau de bord actuellement visibles sur une seule page.

![Aperçu du profil affiché sur une seule page avec le panneau Options d’impression à droite.](images/download/download-chrome-print.png)

Le fichier PDF inclut un en-tête généré automatiquement, lequel contient le logo d’Experience Platform, le nom du tableau de bord, votre nom ainsi que la date et l’heure de téléchargement du tableau de bord. Ces informations sont en lecture seule et ne peuvent pas être modifiées dans le PDF.

![Gros plan sur l’aperçu avant impression avec l’en-tête généré automatiquement mis en surbrillance.](images/download/download-pdf.png)

## Enregistrement au format PDF

Après avoir prévisualisé le PDF, sélectionnez **Enregistrer** pour choisir l’emplacement où vous souhaitez enregistrer le fichier PDF.

>[!NOTE]
>
>Si nécessaire, vous pouvez utiliser la liste déroulante **Destination** pour sélectionner **Enregistrer en tant que PDF** si cette option n’est pas automatiquement sélectionnée.

![Aperçu du profil affiché sur une seule page avec la liste déroulante Destination Option Enregistrer en tant qu’impression PDF mise en surbrillance.](images/download/download-chrome-print-destination.png)

## Personnalisation des fichiers PDF de tableaux de bord

Le fichier PDF généré correspond au tableau de bord visible dans l’interface utilisateur et ne comprend que les widgets actuellement visibles dans votre tableau de bord. Certains tableaux de bord peuvent être personnalisés pour modifier la taille et l’emplacement des widgets ou pour ajouter et supprimer des widgets de l’affichage. La personnalisation de l’aspect de votre tableau de bord dans l’interface utilisateur d’Experience Platform modifie également l’aspect du PDF généré.

Par exemple, vous pouvez modifier l’aspect du tableau de bord des profils afin d’inclure plusieurs widgets pleine largeur empilés au-dessus de trois widgets standard.

![Le tableau de bord Profil présentant les affichages de widgets allongés.](images/download/download-modify.png)

Si vous choisissez de télécharger le tableau de bord mis à jour, une nouvelle prévisualisation du fichier PDF reprenant l’aspect du tableau de bord des profils personnalisés s’affiche. En outre, la taille du fichier PDF est automatiquement ajustée pour garantir l’inclusion de tous les widgets visibles dans un fichier PDF d’une seule page.

![Aperçu du profil affiché sur une seule page avec le panneau Options d’impression à droite.](images/download/download-chrome-print-modified.png)

Pour en savoir plus sur la personnalisation des tableaux de bord, commencez par lire la [présentation de la personnalisation des tableaux de bord](customize/overview.md).

## Étapes suivantes

Maintenant que vous avez téléchargé votre tableau de bord et que vous l’avez enregistré au format PDF, vous pouvez répéter ces étapes pour télécharger des tableaux de bord supplémentaires ou partager le fichier PDF avec des membres de votre organisation.
