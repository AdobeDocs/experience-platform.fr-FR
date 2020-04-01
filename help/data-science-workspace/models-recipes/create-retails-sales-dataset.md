---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Création du  de vente au détail et du jeu de données
topic: Tutorial
translation-type: tm+mt
source-git-commit: 91c7b7e285a4745da20ea146f2334510ca11b994

---


# Création du  de vente au détail et du jeu de données

Ce didacticiel vous présente les prérequis et les ressources requis pour tous les autres didacticiels de la plateforme de données Data Science Workspace d’Adobe Experience Platform. Une fois terminé, le de vente au détail et les jeux de données seront disponibles pour vous et les membres de votre IMS Organization on Experience Platform.

## Prise en main

Avant de commencer ce didacticiel, vous devez disposer des conditions préalables suivantes :
- Accès à Adobe Experience Platform. Si vous n’avez pas accès à une organisation IMS dans Experience Platform, contactez votre administrateur système avant de poursuivre.
- Autorisation d’effectuer des appels à l’API de plateforme d’expérience. Suivez le didacticiel [Authentifier et accéder aux API](../../tutorials/authentication.md) Adobe Experience Platform pour obtenir les valeurs suivantes afin de terminer ce didacticiel :
   - Autorisation : `{ACCESS_TOKEN}`
   - x-api-key : `{API_KEY}`
   - x-gw-ims-org-id : `{IMS_ORG}`
   - Client secret: `{CLIENT_SECRET}`
   - Certificat client : `{PRIVATE_KEY}`
- Exemples de données et de fichiers source pour la Recette des ventes au [détail](../pre-built-recipes/retail-sales.md). Téléchargez les ressources requises pour cet espace de travail et d’autres didacticiels Data Science Workspace depuis le référentiel [Git public](https://github.com/adobe/experience-platform-dsw-reference/)Adobe.
- [Python >= 2.7](https://www.python.org/downloads/) et les paquets Python suivants :
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictateur](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Une compréhension pratique des concepts suivants utilisés dans ce didacticiel :
   - [Modèle de données d’expérience (XDM)](../../xdm/home.md)
   - [Principes de base de la composition](../../xdm/schema/field-dictionary.md)

## Créer des  de vente au détail et un jeu de données

Le Ventes au détail et les jeux de données sont créés automatiquement à l’aide du script d’amorçage fourni. Suivez les étapes ci-dessous dans l’ordre :

### Configuration des fichiers

1. Dans le package de ressources du didacticiel de la plateforme d’expérience, accédez au répertoire `bootstrap`, puis ouvrez-le `config.yaml` à l’aide d’un éditeur de texte approprié.
2. Sous la `Enterprise` section, saisissez les valeurs suivantes :

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Modifiez les valeurs figurant sous la `Platform` section, comme illustré ci-dessous :

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway` : Chemin de base des appels d’API. Ne modifiez pas cette valeur.
   - `ims_token` : Tu `{ACCESS_TOKEN}` vas ici.
   - `ingest_data` : Dans le cadre de ce didacticiel, définissez cette valeur comme `"True"` afin de créer les  de vente au détail et les jeux de données. Une valeur de `"False"` crée uniquement le  du.
   - `build_recipe_artifacts` : Dans le cadre de ce didacticiel, définissez cette valeur `"False"` pour empêcher le script de générer un artefact de recette.
   - `kernel_type` : Type d’exécution de l’artefact de recette. Laissez cette valeur comme `Python` si `build_recipe_artifacts` est définie comme `"False"`, sinon spécifiez le type d’exécution correct.

4. Sous la `Titles` section, fournissez les informations suivantes appropriées pour les données d’exemple Ventes au détail, enregistrez et fermez le fichier une fois les modifications effectuées. Exemple illustré ci-dessous :

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

1. Ouvrez votre application Terminal Server et accédez au répertoire des ressources du didacticiel de la plateforme d’expérience.
2. Définissez le `bootstrap` répertoire comme chemin de travail actuel et exécutez le script `bootstrap.py` python en saisissant la commande suivante :

   ```bash
   python bootstrap.py
   ```

   > [!NOTE] L’exécution du script peut prendre plusieurs minutes.

## Étapes suivantes

Une fois le script d’amorçage terminé, les  d’entrée et de sortie des ventes au détail et les jeux de données peuvent être affichés sur la plateforme d’expérience. Pour plus d’informations, reportez-vous au didacticiel [sur les données de](./preview-schema-data.md)pour plus d’informations.

Vous avez également correctement assimilé des données d’exemple Ventes au détail dans la plateforme d’expérience à l’aide du script d’amorçage fourni.

Pour continuer à travailler avec les données assimilées :
- [Analyse de vos données à l’aide des ordinateurs portables Jupyter](../jupyterlab/analyze-your-data.md)
   - Utilisez les ordinateurs portables Jupyter de Data Science Workspace pour accéder à vos données, les explorer, les visualiser et les comprendre.
- [compresser les fichiers source dans une recette ;](./package-source-files-recipe.md)
   - Suivez ce didacticiel pour apprendre à importer votre propre modèle dans Data Science Workspace en regroupant les fichiers source dans un fichier Recette importable.