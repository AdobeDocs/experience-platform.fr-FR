---
keywords: Experience Platform;recette de ventes au détail;Workspace de science des données;rubriques populaires;recettes
solution: Experience Platform
title: Créer le schéma et le jeu de données de ventes au détail
type: Tutorial
description: Ce tutoriel vous présente les prérequis et les ressources nécessaires à tous les autres tutoriels sur l’espace de travail de science des données d’Adobe Experience Platform. Une fois l’opération terminée, le schéma et les jeux de données de ventes au détail seront disponibles pour vous et les membres de votre organisation sur Experience Platform.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 41%

---


# Création de jeux de données et de schéma de vente au détail

>[!NOTE]
>
>Le Workspace de science des données ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs sur Data Science Workspace.

Ce tutoriel vous présente les prérequis et les ressources nécessaires à tous les autres tutoriels [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] . Une fois l’opération terminée, le schéma et les jeux de données de ventes au détail seront disponibles pour vous et les membres de votre organisation sur [!DNL Experience Platform].

## Prise en main

Avant de commencer ce tutoriel, vous devez disposer des éléments suivants :

- Accès à [!DNL Adobe Experience Platform]. Si vous n’avez pas accès à une organisation dans [!DNL Experience Platform], contactez votre administrateur système avant de continuer.
- Autorisation d’effectuer des appels API [!DNL Experience Platform]. Suivez le tutoriel [Authentification et accès aux API Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) afin d’obtenir les valeurs suivantes pour effectuer ce didacticiel :
   - Authorization: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{ORG_ID}`
   - Client secret: `{CLIENT_SECRET}`
   - Client certificate: `{PRIVATE_KEY}`
- Données d’exemple et fichiers source pour la [Recette des ventes au détail](../pre-built-recipes/retail-sales.md). Téléchargez les ressources requises pour ce tutoriel et d’autres tutoriels [!DNL Data Science Workspace] à partir du [référentiel Git public d’Adobe](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7](https://www.python.org/downloads/) et les packages [!DNL Python] suivants :
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Une connaissance concrète des concepts suivants employés dans ce tutoriel :
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [Principes de base de la composition des schémas](../../xdm/schema/field-dictionary.md)

## Création de jeux de données et de schéma de vente au détail

Les jeux de données et le schéma de vente au détail sont créés automatiquement à l’aide du script de bootstrap fourni. Suivez les étapes ci-dessous dans l’ordre :

### Fichiers de configuration

1. Dans le package de ressources du tutoriel [!DNL Experience Platform], accédez au `bootstrap` de répertoire, puis ouvrez-le `config.yaml` à l’aide d’un éditeur de texte approprié.
2. Dans la section `Enterprise`, saisissez les valeurs suivantes :

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {ORG_ID}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Modifiez les valeurs figurant dans la section `Platform`, comme indiqué ci-dessous :

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway` : chemin d’accès de base des appels API. Ne modifiez pas cette valeur.
   - `ims_token` : Votre `{ACCESS_TOKEN}` va ici.
   - `ingest_data` : pour les besoins de ce tutoriel, définissez cette valeur sur `"True"` afin de créer les schémas et les jeux de données de ventes au détail. Une valeur `"False"` crée uniquement les schémas.
   - `build_recipe_artifacts` : pour les besoins de ce tutoriel, définissez cette valeur sur `"False"` pour empêcher le script de générer un artefact de recette.
   - `kernel_type` : type d’exécution de l’artefact de recette. Laissez la valeur `Python` si `build_recipe_artifacts` est définie comme `"False"`, sinon spécifiez le type d’exécution correct.

4. Dans la section `Titles`, fournissez les informations suivantes adaptées aux données d’exemple de ventes au détail, enregistrez et fermez le fichier une fois les modifications effectuées. Exemple illustré ci-dessous :

   ```yaml
   Titles:
       input_class_title: retail_sales_input_class
       input_mixin_title: retail_sales_input_mixin
       input_mixin_definition_title: retail_sales_input_mixin_definition
       input_schema_title: retail_sales_input_schema
       input_dataset_title: retail_sales_input_dataset
       file_replace_tenant_id: DSWRetailSalesForXDM0.9.9.9.json
       file_with_tenant_id: DSWRetailSales_with_tenant_id.json
       is_output_schema_different: "True"
       output_mixin_title: retail_sales_output_mixin
       output_mixin_definition_title: retail_sales_output_mixin_definition
       output_schema_title: retail_sales_output_title
       output_dataset_title: retail_sales_output_dataset
   ```

### Exécution du script de bootstrap

1. Ouvrez votre application de terminal et accédez au répertoire des ressources de tutoriel [!DNL Experience Platform].
2. Définissez le répertoire `bootstrap` comme chemin de travail actuel et exécutez le script `bootstrap.py` [!DNL Python] en saisissant la commande suivante :

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >Le script peut prendre plusieurs minutes.

## Étapes suivantes

Une fois l’exécution du script de bootstrap terminée, il est possible d’afficher les jeux de données et schémas d’entrée et de sortie de ventes au détail sur [!DNL Experience Platform]. Pour plus d’informations, consultez le [tutoriel de présentation des données de schéma](./preview-schema-data.md).

Vous avez également ingéré avec succès des données d’exemple de ventes au détail dans [!DNL Experience Platform] à l’aide du script de bootstrap fourni.

Pour continuer à travailler sur les données ingérées, procédez de la façon suivante :

- [Analysez vos données à l’aide de Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Utilisez les notebooks Jupyter dans le Workspace de science des données pour accéder à vos données, les explorer, les visualiser et les comprendre.
- [Regrouper les fichiers sources dans une recette](./package-source-files-recipe.md)
   - Suivez ce tutoriel pour savoir comment importer votre propre modèle dans [!DNL Data Science Workspace] en regroupant les fichiers sources dans un fichier de recette importable.
