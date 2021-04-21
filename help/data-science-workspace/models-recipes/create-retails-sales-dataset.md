---
keywords: Experience Platform ; recette de vente au détail ; Espace de travail de données ; rubriques populaires ; recettes
solution: Experience Platform
title: Créer un Schéma de vente au détail et un jeu de données
topic-legacy: tutorial
type: Tutorial
description: Ce tutoriel vous présente les prérequis et les ressources nécessaires à tous les autres tutoriels Data Science Workspace d’Adobe Experience Platform. Une fois que vous aurez terminé, les jeux de données et le schéma de vente au détail seront disponibles pour vous et les membres de votre organisation IMS sur Experience Platform.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 70%

---

# Création de jeux de données et de schéma de vente au détail

Ce didacticiel présente les conditions préalables et les ressources requises pour tous les autres didacticiels [!DNL Adobe Experience Platform] [!DNL Data Science Workspace]. Une fois que vous aurez terminé, les jeux de données et le schéma de vente au détail seront disponibles pour vous et les membres de votre organisation IMS sur [!DNL Experience Platform].

## Prise en main

Avant de commencer ce tutoriel, vous devez disposer des éléments suivants :
- Accès à [!DNL Adobe Experience Platform]. Si vous n&#39;avez pas accès à une organisation IMS dans [!DNL Experience Platform], contactez votre administrateur système avant de continuer.
- Autorisation d&#39;effectuer des appels d&#39;API [!DNL Experience Platform]. Suivez le tutoriel [Authentification et accès aux API Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) afin d’obtenir les valeurs suivantes pour effectuer ce didacticiel :
   - Authorization: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - Client secret: `{CLIENT_SECRET}`
   - Client certificate: `{PRIVATE_KEY}`
- Exemples de données et de fichiers source pour la [Recette des ventes au détail](../pre-built-recipes/retail-sales.md). Téléchargez les ressources requises pour ce didacticiel et d&#39;autres [!DNL Data Science Workspace] didacticiels à partir du [référentiel Git public d&#39;Adobe](https://github.com/adobe/experience-platform-dsw-reference/).
- [ >= 2.7](https://www.python.org/downloads/)[!DNL Python] et les paquets Python suivants :
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

1. Dans le package de ressources du didacticiel [!DNL Experience Platform], accédez au répertoire `bootstrap` et ouvrez `config.yaml` à l&#39;aide d&#39;un éditeur de texte approprié.
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

1. Ouvrez votre application Terminal Server et accédez au répertoire de ressources du didacticiel [!DNL Experience Platform].
2. Définissez le répertoire `bootstrap` comme chemin d’accès opérationnel actuel et exécutez le script `bootstrap.py` en saisissant la commande suivante :[!DNL Python]

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >l’exécution du script peut prendre plusieurs minutes.

## Étapes suivantes

Une fois l’exécution du script de bootstrap terminée, il est possible d’afficher les jeux de données et schémas d’entrée et de sortie de ventes au détail dans [!DNL Experience Platform]. Pour plus d’informations, consultez le [tutoriel de présentation des données de schéma](./preview-schema-data.md).

Vous avez également correctement assimilé des données d&#39;exemple Ventes au détail dans [!DNL Experience Platform] à l&#39;aide du script d&#39;amorçage fourni.

Pour continuer à travailler sur les données ingérées, procédez de la façon suivante :
- [Analyse de vos données à l’aide des ordinateurs portables Jupyter](../jupyterlab/analyze-your-data.md)
   - Utilisez les portables Jupyter de Data Science Workspace pour accéder à vos données, les explorer, les visualiser et les comprendre.
- [Regroupez les fichiers source dans une recette](./package-source-files-recipe.md)
   - Suivez ce tutoriel pour apprendre à importer votre propre modèle dans [!DNL Data Science Workspace] en regroupant les fichiers source dans un fichier Recette important.
