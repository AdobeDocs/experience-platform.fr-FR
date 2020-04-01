---
keywords: Experience Platform;attribution ai;access scores;popular topics
solution: Experience Platform
title: Accès aux scores dans l’attribut AI
topic: Accessing scores
translation-type: tm+mt
source-git-commit: 689b4c7a96856e1167ee435a6740fed006136256

---


# Accès aux scores dans l’attribut AI

>[!IMPORTANT] Pour plus d’informations sur les téléchargements à score brut pour l’exportation en masse de données, contactez attributionai-support@adobe.com.

L’accès aux scores pour Attribution AI se fait par Snowflake. Pour l’instant, vous devez envoyer un courrier électronique à l’assistance Adobe à l’adresse attributionai-support@adobe.com afin de configurer et de recevoir les informations d’identification de votre compte Reader pour Snowflake.

Une fois votre demande traitée par le service d’assistance d’Adobe, vous recevez l’URL du compte Reader pour Snowflake et les informations d’identification correspondantes ci-dessous :

- URL de Snowflake
- Nom d’utilisateur
- Mot de passe

>[!NOTE] Le compte Reader est destiné à interroger les données à l’aide de clients SQL, de feuilles de calcul et de solutions BI prenant en charge le connecteur JDBC.

Une fois que vous disposez de vos informations d’identification et de votre URL, vous pouvez  les tableaux de modèles, soit dans leur format brut, soit agrégé par date de point de contact, soit par date de conversion.

## Trouver votre dans le flocon de neige

A l’aide des informations d’identification fournies, connectez-vous à Snowflake. Cliquez sur l’onglet **Feuilles** de calcul dans le volet de navigation principal supérieur gauche, puis accédez au répertoire de votre base de données dans le volet de gauche.

![Feuilles de calcul et navigation](./images/download-scores/edited_snowflake_1.png)

Cliquez ensuite sur **Sélectionner** dans le coin supérieur droit de l’écran. Dans la fenêtre contextuelle qui s’affiche, vérifiez que la base de données appropriée est sélectionnée. Cliquez ensuite sur la liste *déroulante* du et sélectionnez l’un de vos  de répertoriés. Vous pouvez directement à partir des tableaux de notes répertoriés sous le sélectionné.

![trouver un](./images/download-scores/edited_snowflake_2.png)

## Téléchargement de scores bruts

Pour plus d’informations sur les téléchargements de notes brutes, contactez attributionai-support@adobe.com.

## Connexion de PowerBI à Snowflake (facultatif)

Vos informations d&#39;identification Snowflake peuvent être utilisées pour configurer une connexion entre les bases de données PowerBI Desktop et Snowflake.

Tout d’abord, sous la zone *Serveur* , saisissez l’URL de votre Flocon de neige. Ensuite, sous *Warehouse*, tapez &quot;XSMALL&quot;. Entrez ensuite votre nom d&#39;utilisateur et votre mot de passe.

![exemple de POWERBI](./images/download-scores/powerbi-snowflake.png)

Une fois la connexion établie, sélectionnez votre base de données Snowflake, puis sélectionnez le  approprié. Vous pouvez désormais charger toutes les tables.

Une fois que vous avez sélectionné votre , des tableaux s’affichent avec vos scores d’attribution.

| Tableau | Description |
| ----- | ----------- |
| APP_{APP_ID} | Score d’attribution brut. |
| APP_{APP_ID}_BY_CONV_DATE | Score d’attribution brute agrégé au niveau de la date de conversion. |
| APP_{APP_ID}_BY_TP_DATE | Score d’attribution brute agrégé au niveau de la date du point de contact. |

## Étapes suivantes

Ce décrit les étapes requises pour interroger les données et accéder aux scores pour l’attribut AI. Vous pouvez maintenant continuer à parcourir les autres services [et guides](../home.md) intelligents proposés.