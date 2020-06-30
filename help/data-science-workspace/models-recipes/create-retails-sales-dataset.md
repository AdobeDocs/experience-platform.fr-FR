---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Créer un schéma de vente au détail et un jeu de données
topic: Tutorial
translation-type: tm+mt
source-git-commit: 4b0f0dda97f044590f55eaf75a220f631f3313ee
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---


# Créer un schéma de vente au détail et un jeu de données

Ce didacticiel présente les conditions préalables et les ressources requises pour tous les autres [!DNL Adobe Experience Platform][!DNL Data Science Workspace] didacticiels. Une fois terminé, le schéma de vente au détail et les ensembles de données seront disponibles pour vous et les membres de votre organisation IMS le [!DNL Experience Platform]jour.

## Prise en main

Avant de commencer ce didacticiel, vous devez disposer des conditions préalables suivantes :
- Accès à [!DNL Adobe Experience Platform]. Si vous n&#39;avez pas accès à une organisation IMS dans [!DNL Experience Platform]votre entreprise, contactez votre administrateur système avant de continuer.
- Autorisation d’effectuer des appels [!DNL Experience Platform] d’API. Suivez le didacticiel sur les API [](../../tutorials/authentication.md) d&#39;Adobe Experience Platform d&#39;authentification et d&#39;accès pour obtenir les valeurs suivantes afin de terminer ce didacticiel avec succès :
   - Autorisation : `{ACCESS_TOKEN}`
   - x-api-key : `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - Client secret: `{CLIENT_SECRET}`
   - Certificat client : `{PRIVATE_KEY}`
- Exemples de données et de fichiers source pour la Recette [des ventes](../pre-built-recipes/retail-sales.md)au détail. Téléchargez les ressources requises pour ce didacticiel et d’autres [!DNL Data Science Workspace] didacticiels depuis le référentiel [Git public](https://github.com/adobe/experience-platform-dsw-reference/)Adobe.
- [Python >= 2.7](https://www.python.org/downloads/) et les [!DNL Python] packages suivants :
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictateur](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Une compréhension pratique des concepts suivants utilisés dans ce tutoriel :
   - [!DNL Experience Data Model (XDM)](../../xdm/home.md)
   - [Principes de base de la composition des schémas](../../xdm/schema/field-dictionary.md)

## Créer un schéma de vente au détail et un jeu de données

Le schéma Ventes au détail et les jeux de données sont créés automatiquement à l’aide du script d’amorçage fourni. Suivez les étapes ci-dessous pour :

### Configuration des fichiers

1. Dans le package de ressources du [!DNL Experience Platform] didacticiel, accédez au répertoire `bootstrap`et ouvrez-le `config.yaml` à l’aide d’un éditeur de texte approprié.
2. Sous la `Enterprise` section, saisissez les valeurs suivantes :

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Modifiez les valeurs figurant sous la `Platform` section Exemple illustré ci-dessous :

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway` : Chemin d’accès de base pour les appels d’API. Ne modifiez pas cette valeur.
   - `ims_token` : Tu `{ACCESS_TOKEN}` vas ici.
   - `ingest_data` : Pour les besoins de ce didacticiel, définissez cette valeur comme `"True"` afin de créer les schémas de vente au détail et les jeux de données. Une valeur de `"False"` crée uniquement les schémas.
   - `build_recipe_artifacts` : Pour les besoins de ce didacticiel, définissez cette valeur `"False"` afin d’empêcher le script de générer un artefact de recette.
   - `kernel_type` : Type d&#39;exécution de l&#39;artefact de recette. Conservez cette valeur comme `Python` si `build_recipe_artifacts` est défini comme `"False"`, sinon spécifiez le type d’exécution correct.

4. Sous la `Titles` section, fournissez les informations suivantes appropriées pour les données d&#39;exemple Ventes au détail, enregistrez et fermez le fichier une fois les modifications en place. Exemple illustré ci-dessous :

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

### Exécution du script d’amorçage

1. Ouvrez votre application de terminal et accédez au répertoire des ressources du [!DNL Experience Platform] didacticiel.
2. Définissez le répertoire comme chemin d’accès actif et exécutez le `bootstrap` script `bootstrap.py` [!DNL Python] en saisissant la commande suivante :

   ```bash
   python bootstrap.py
   ```

   > [!NOTE] L’exécution du script peut prendre plusieurs minutes.

## Étapes suivantes

Une fois le script d&#39;amorçage terminé, les schémas d&#39;entrée et de sortie des ventes au détail et les jeux de données peuvent être consultés sur [!DNL Experience Platform]. Consultez le didacticiel [sur les données du schéma de](./preview-schema-data.md)prévisualisation pour en savoir plus.

Vous avez également correctement assimilé des données d’exemple Ventes au détail à [!DNL Experience Platform] l’aide du script d’amorçage fourni.

Pour continuer à travailler avec les données imbriquées :
- [Analyse de vos données à l&#39;aide de portables Jupyter](../jupyterlab/analyze-your-data.md)
   - Utilisez les ordinateurs portables Jupyter de Data Science Workspace pour accéder à vos données, les explorer, les visualiser et les comprendre.
- [compresser les fichiers source dans une recette ;](./package-source-files-recipe.md)
   - Suivez ce tutoriel pour apprendre à importer votre propre modèle dans [!DNL Data Science Workspace] en regroupant les fichiers source dans un fichier Recette important.