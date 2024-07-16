---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;connexion;connexion au service de requête;aqua data studio;Aqua Data Studio;Looker;observateur;Postico;Power BI;power bi;psql;studio;PSQL;RStudio;Tableau;tableau;tableau
solution: Experience Platform
title: Connecter les clients au service de requête
description: Ce document explique comment se connecter à Query Service à partir de diverses applications clientes de bureau et comment vérifier ces connexions.
exl-id: 2ba20179-5adb-4259-a120-231a40e78054
source-git-commit: 26f0725f0f239707bd719ed46929648f8d557155
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 5%

---

# Connexion des clients à [!DNL Query Service]

Cette section explique comment se connecter à [!DNL Query Service] à partir de diverses applications clientes de bureau et comment vérifier ces connexions. [!DNL Query Service] utilise le protocole [!DNL PostgreSQL]. Les instructions de cette section expliquent donc comment utiliser les outils et les pilotes [!DNL PostgreSQL] pour se connecter et écrire des requêtes.

>[!IMPORTANT]
>
>Les certificats TLS/SSL sur les environnements de production pour l’API Postgres interactives de Query Service ont été actualisés le mercredi 24 janvier 2024.<br>Bien que cette exigence soit annuelle, à cette occasion, le certificat racine de la chaîne a également changé, car le fournisseur de certificats TLS/SSL de l’Adobe a mis à jour sa hiérarchie de certificats. Cela peut avoir un impact sur certains clients Postgres si leur liste d’autorités de certification ne comporte pas le certificat racine. Par exemple, un client de ligne de commande PSQL peut avoir besoin que les certs racine soient ajoutés à un fichier explicite `~/postgresql/root.crt`, sinon cela peut entraîner une erreur. Par exemple : `psql: error: SSL error: certificate verify failed`. Pour plus d’informations sur ce problème, consultez la [documentation officielle de PostgreSQL](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) .<br>Le certificat racine à ajouter peut être téléchargé à partir de [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

Les instructions concernent les clients suivants :

- [[!DNL Aqua Data Studio]](./aqua-data-studio.md)
- [[!DNL DbVisualizer]](./dbvisulaizer.md)
- [[!DNL Looker]](./looker.md)
- [[!DNL Postico (Mac)]](./postico.md)
- [[!DNL Power BI (PC)]](./power-bi.md)
- [[!DNL PSQL]](./psql.md)
- [[!DNL RStudio]](./rstudio.md)
- [[!DNL Tableau]](./tableau.md)

>[!IMPORTANT]
>
>En tant qu’utilisateur Power BI et Tableau, vous pouvez connecter Customer Journey Analytics à vos outils de BI à partir de l’onglet Informations d’identification de Query Service. Consultez la documentation des informations d’identification pour obtenir des instructions sur la [connexion de vos outils de BI à Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics).
