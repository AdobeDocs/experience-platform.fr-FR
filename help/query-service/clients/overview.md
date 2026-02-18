---
keywords: Experience Platform;accueil;rubriques les plus consultées;Query service;query service;se connecter;se connecter à query service;aqua data studio;Aqua Data Studio;Looker;looker;Postico;Power BI;power bi;psql;rstudio;PSQL;RStudio;Tableau;tableau;
solution: Experience Platform
title: Connecter les clients au service de requête
description: Ce document explique comment se connecter à Query Service à partir de diverses applications de bureau clientes et comment vérifier ces connexions.
exl-id: 2ba20179-5adb-4259-a120-231a40e78054
source-git-commit: 5e5a196074e844826579102fa6b36102c6481096
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 6%

---

# Connexion des clients au service de requête

Cette section explique comment se connecter à Query Service à partir de diverses applications de bureau clientes et comment vérifier ces connexions. Query Service utilise le protocole PostgreSQL. Par conséquent, les instructions de cette section expliquent comment utiliser les outils et pilotes PostgreSQL pour connecter et écrire des requêtes.

>[!IMPORTANT]
>
>Les certificats TLS/SSL sur les environnements de production pour l’API Interactive Postgres de Query Service ont été actualisés le mercredi 24 janvier 2024.<br>Bien qu’il s’agisse d’une exigence annuelle, le certificat racine de la chaîne a également changé cette fois-ci, car le fournisseur de certificats TLS/SSL d’Adobe a mis à jour sa hiérarchie de certificats. Cela peut avoir un impact sur certains clients Postgres si leur liste d’autorités de certification ne dispose pas du certificat racine. Par exemple, un client de ligne de commande PSQL peut avoir besoin que les certificats racines soient ajoutés à une `~/postgresql/root.crt` de fichier explicite, sinon cela peut entraîner une erreur, telle que `psql: error: SSL error: certificate verify failed`. Voir la [documentation officielle de PostgreSQL](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) pour plus d’informations sur ce problème.<br>Le certificat racine à ajouter peut être téléchargé depuis [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

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
>En tant qu’utilisateur de Power BI et de Tableau, vous pouvez connecter Customer Journey Analytics à vos outils BI à l’aide des informations d’identification fournies dans l’onglet des informations d’identification de Query Service. Consultez la documentation des informations d’identification pour obtenir des instructions sur la [connexion de vos outils BI à Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics).
