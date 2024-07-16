---
keywords: Experience Platform;recette de ventes au détail;Data Science Workspace;rubriques les plus consultées;recettes
solution: Experience Platform
title: Création d’un schéma et d’un jeu de données de vente au détail
type: Tutorial
description: Ce tutoriel vous présente les prérequis et les ressources nécessaires à tous les autres tutoriels sur l’espace de travail de science des données d’Adobe Experience Platform. Une fois l’opération terminée, les jeux de données et le schéma de vente au détail seront disponibles pour vous et les membres de votre organisation sur Experience Platform.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 43%

---


# Création de jeux de données et de schéma de vente au détail

Ce tutoriel vous fournit les prérequis et les ressources requis pour tous les autres tutoriels [!DNL Adobe Experience Platform] [!DNL Data Science Workspace]. Une fois l’opération terminée, les jeux de données et le schéma de vente au détail seront disponibles pour vous et les membres de votre organisation sur [!DNL Experience Platform].

## Prise en main

Avant de commencer ce tutoriel, vous devez disposer des éléments suivants :
- Accès à [!DNL Adobe Experience Platform]. Si vous n’avez pas accès à une organisation dans [!DNL Experience Platform], contactez votre administrateur système avant de poursuivre.
- Autorisation d’effectuer des appels d’API [!DNL Experience Platform]. Suivez le tutoriel [Authentification et accès aux API Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) afin d’obtenir les valeurs suivantes pour effectuer ce didacticiel :
   - Authorization: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{ORG_ID}`
   - Client secret: `{CLIENT_SECRET}`
   - Client certificate: `{PRIVATE_KEY}`
- Exemples de données et de fichiers source pour la [Recette des ventes au détail](../pre-built-recipes/retail-sales.md). Téléchargez les ressources requises pour ce tutoriel et d’autres [!DNL Data Science Workspace] à partir du [référentiel Git public Adobe](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7](https://www.python.org/downloads/) et les [!DNL Python] packages suivants :
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

1. Dans le package de ressources de tutoriel [!DNL Experience Platform], accédez au répertoire `bootstrap` et ouvrez `config.yaml` à l’aide d’un éditeur de texte approprié.
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

   - `platform_gateway` : chemin d’accès de base pour les appels API. Ne modifiez pas cette valeur.
   - `ims_token` : votre `{ACCESS_TOKEN}` va ici.
   - `ingest_data` : pour les besoins de ce tutoriel, définissez cette valeur sur `"True"` afin de créer les jeux de données et les schémas de vente au détail. Une valeur `"False"` crée uniquement les schémas.
   - `build_recipe_artifacts` : pour les besoins de ce tutoriel, définissez cette valeur sur `"False"` afin d’empêcher le script de générer un artefact de recette.
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

1. Ouvrez votre application de terminal et accédez au répertoire de ressources du tutoriel [!DNL Experience Platform].
2. Définissez le répertoire `bootstrap` comme chemin d’accès opérationnel actuel et exécutez le script `bootstrap.py` [!DNL Python] en saisissant la commande suivante :

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >L’exécution du script peut prendre plusieurs minutes.

## Étapes suivantes

Une fois le script de bootstrap terminé, les jeux de données et schémas d’entrée et de sortie de Ventes au détail peuvent être affichés sur [!DNL Experience Platform]. Pour plus d’informations, consultez le [tutoriel de présentation des données de schéma](./preview-schema-data.md).

Vous avez également ingéré avec succès des données d’exemple de ventes au détail dans [!DNL Experience Platform] à l’aide du script de bootstrap fourni.

Pour continuer à travailler sur les données ingérées, procédez de la façon suivante :
- [Analysez vos données à l’aide de Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Utilisez les notebooks Jupyter dans Data Science Workspace pour accéder à vos données, les explorer, les visualiser et les comprendre.
- [Regroupement des fichiers source dans une recette](./package-source-files-recipe.md)
   - Suivez ce tutoriel pour apprendre à importer votre propre modèle dans [!DNL Data Science Workspace] en regroupant les fichiers source dans un fichier de recette pouvant être importé.
