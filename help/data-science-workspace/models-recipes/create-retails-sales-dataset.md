---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Création de jeux de données et de schéma de vente au détail
topic: Tutorial
translation-type: tm+mt
source-git-commit: 86ded28b1830d3607c8b5214c8d31dfcbf446252
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 76%

---


# Création de jeux de données et de schéma de vente au détail

Ce didacticiel présente les conditions préalables et les ressources requises pour tous les autres [!DNL Adobe Experience Platform][!DNL Data Science Workspace] didacticiels. Une fois que vous aurez terminé, les jeux de données et le schéma de vente au détail seront disponibles pour vous et les membres de votre organisation IMS sur [!DNL Experience Platform].

## Prise en main

Avant de commencer ce tutoriel, vous devez disposer des éléments suivants :
- Accès à [!DNL Adobe Experience Platform]. If you do not have access to an IMS Organization in [!DNL Experience Platform], please speak to your system administrator before proceeding.
- Authorization to make [!DNL Experience Platform] API calls. Suivez le tutoriel [Authentification et accès aux API Adobe Experience Platform](../../tutorials/authentication.md) afin d’obtenir les valeurs suivantes pour effectuer ce didacticiel :
   - Authorization: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - Client secret: `{CLIENT_SECRET}`
   - Client certificate: `{PRIVATE_KEY}`
- Exemples de données et de fichiers source pour la [Recette des ventes au détail](../pre-built-recipes/retail-sales.md). Download the assets required for this and other [!DNL Data Science Workspace] tutorials from the [Adobe public Git repository](https://github.com/adobe/experience-platform-dsw-reference/).
- [ >= 2.7](https://www.python.org/downloads/)[!DNL Python] et les paquets Python suivants :
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Une connaissance concrète des concepts suivants employés dans ce tutoriel :
   - [!DNL Experience Data Model (XDM)](../../xdm/home.md)
   - [Principes de base de la composition des schémas](../../xdm/schema/field-dictionary.md)

## Création de jeux de données et de schéma de vente au détail

Les jeux de données et le schéma de vente au détail sont créés automatiquement à l’aide du script de bootstrap fourni. Suivez les étapes ci-dessous dans l’ordre :

### Fichiers de configuration

1. Inside the [!DNL Experience Platform] tutorial resource package, navigate into the directory `bootstrap`, and open `config.yaml` using an appropriate text editor.
2. Dans la section `Enterprise`, saisissez les valeurs suivantes :

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
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

   - `platform_gateway` : le chemin d’accès de base des appels API. Ne modifiez pas cette valeur.
   - `ims_token` : emplacement de votre `{ACCESS_TOKEN}`.
   - `ingest_data` : pour les besoins de ce tutoriel, définissez cette valeur comme `"True"` pour créer les jeux de données et les schémas de vente au détail. Une valeur `"False"` crée uniquement les schémas.
   - `build_recipe_artifacts` : pour les besoins de ce tutoriel, définissez cette valeur comme `"False"` pour empêcher le script de générer un artefact de recette.
   - `kernel_type` : type d’exécution de l’artefact de recette. Laissez la valeur `Python` si `build_recipe_artifacts` est définie comme `"False"`, sinon spécifiez le type d’exécution correct.

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

1. Open your terminal application and navigate to the [!DNL Experience Platform] tutorial resource directory.
2. Définissez le répertoire `bootstrap` comme chemin d’accès opérationnel actuel et exécutez le script `bootstrap.py` en saisissant la commande suivante :[!DNL Python]

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >l’exécution du script peut prendre plusieurs minutes.

## Étapes suivantes

Une fois l’exécution du script de bootstrap terminée, il est possible d’afficher les jeux de données et schémas d’entrée et de sortie de ventes au détail dans [!DNL Experience Platform]. Pour plus d’informations, consultez le [tutoriel de présentation des données de schéma](./preview-schema-data.md).

You have also successfully ingested Retail Sales sample data into [!DNL Experience Platform] using the provided bootstrap script.

Pour continuer à travailler sur les données ingérées, procédez de la façon suivante :
- [Analysez vos données à l’aide des notebooks Jupyter](../jupyterlab/analyze-your-data.md)
   - Utilisez les notebooks Jupyter dans Data Science Workspace pour accéder à vos données, les explorer, les visualiser et les comprendre.
- [Regroupez les fichiers source dans une recette](./package-source-files-recipe.md)
   - Follow this tutorial to learn how to bring your own Model into [!DNL Data Science Workspace] by packaging source files in an importable Recipe file.