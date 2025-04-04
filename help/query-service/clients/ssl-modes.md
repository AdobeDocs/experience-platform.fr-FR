---
keywords: Experience Platform;accueil;rubriques les plus consultées;Query service;query service;se connecter;se connecter à query service;SSL;ssl;sslmode;
title: Options SSL de Query Service
description: Découvrez la prise en charge SSL pour les connexions tierces à Adobe Experience Platform Query Service et comment vous connecter à l’aide du mode SSL complet.
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 1%

---

# [!DNL Query Service] les options SSL

Pour une sécurité renforcée, Adobe Experience Platform [!DNL Query Service] fournit une prise en charge native des connexions SSL pour chiffrer les communications client/serveur. Ce document couvre les options SSL disponibles pour les connexions clientes tierces à [!DNL Query Service] et comment se connecter à l’aide de la valeur du paramètre SSL `verify-full`.

## Conditions préalables

Ce document suppose que vous avez déjà téléchargé une application cliente de bureau tierce à utiliser avec vos données Experience Platform. Vous trouverez des instructions spécifiques sur la manière d’incorporer la sécurité SSL lors de la connexion à un client tiers dans la documentation de leur guide de connexion respectif. Pour obtenir la liste de tous [!DNL Query Service] clients pris en charge, reportez-vous à la [présentation des connexions client](./overview.md).

## Options SSL disponibles {#available-ssl-options}

Experience Platform prend en charge différentes options SSL pour répondre à vos besoins en matière de sécurité des données et équilibrer la charge de traitement du chiffrement et de l’échange de clés.

Les différentes valeurs de paramètre `sslmode` fournissent différents niveaux de protection. En chiffrant vos données en mouvement à l’aide de certificats SSL, il contribue à empêcher les attaques « man-in-the-middle » (MITM), les écoutes et l’emprunt d’identité. Le tableau ci-dessous présente une répartition des différents modes SSL disponibles et le niveau de protection qu’ils offrent.

>[!NOTE]
>
> La valeur SSL `disable` n’est pas prise en charge par Adobe Experience Platform en raison de la conformité en matière de protection des données.

| sslmode | Protection contre les écoutes | Protection MITM | Description |
|---|---|---|---|
| `allow` | Oui | Non | Le chiffrement est requis pour toutes les communications. Le réseau est approuvé pour se connecter au serveur approprié. |
| `prefer` | Oui | Non | Le chiffrement est requis pour toutes les communications. Le réseau est approuvé pour se connecter au serveur approprié. |
| `require` | Oui | Non | Le chiffrement est requis pour toutes les communications. Le réseau est approuvé pour se connecter au serveur approprié. La validation du certificat SSL du serveur n’est pas requise. |
| `verify-ca` | Oui | Dépend de la politique de l’autorité de certification | Le chiffrement est requis pour toutes les communications. La validation du serveur est requise avant le partage des données. Pour ce faire, vous devez configurer un certificat racine dans votre répertoire racine [!DNL PostgreSQL]. [Des détails sont fournis ci-dessous](#instructions) |
| `verify-full` | Oui | Oui | Le chiffrement est requis pour toutes les communications. La validation du serveur est requise avant le partage des données. Pour ce faire, vous devez configurer un certificat racine dans votre répertoire racine [!DNL PostgreSQL]. [Des détails sont fournis ci-dessous](#instructions). |

>[!NOTE]
>
>La différence entre `verify-ca` et `verify-full` dépend de la politique de l’autorité de certification racine (CA). Si vous avez créé votre propre autorité de certification locale pour émettre des certificats privés pour vos applications, l’utilisation de `verify-ca` offre souvent une protection suffisante. Si vous utilisez une autorité de certification publique, `verify-ca` autorise les connexions à un serveur que quelqu’un d’autre a peut-être enregistré auprès de l’autorité de certification. `verify-full` doit toujours être utilisé avec une autorité de certification racine publique.

Lors de l’établissement d’une connexion tierce à une base de données Experience Platform, il est recommandé d’utiliser au minimum `sslmode=require` pour assurer une connexion sécurisée à vos données en mouvement. Le mode SSL `verify-full` est recommandé pour une utilisation dans la plupart des environnements sensibles à la sécurité.

## Configurer un certificat racine pour la vérification du serveur {#root-certificate}

>[!IMPORTANT]
>
>Les certificats TLS/SSL sur les environnements de production pour l’API Interactive Postgres de Query Service ont été actualisés le mercredi 24 janvier 2024.<br>Bien qu’il s’agisse d’une exigence annuelle, le certificat racine de la chaîne a également changé cette fois-ci, car le fournisseur de certificats TLS/SSL d’Adobe a mis à jour sa hiérarchie de certificats. Cela peut avoir un impact sur certains clients Postgres si leur liste d’autorités de certification ne dispose pas du certificat racine. Par exemple, un client de ligne de commande PSQL peut avoir besoin que les certificats racines soient ajoutés à une `~/postgresql/root.crt` de fichier explicite, sinon cela peut entraîner une erreur. Par exemple : `psql: error: SSL error: certificate verify failed`. Voir la [documentation officielle de PostgreSQL](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) pour plus d’informations sur ce problème.<br>Le certificat racine à ajouter peut être téléchargé depuis [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

Pour garantir une connexion sécurisée, l’utilisation de SSL doit être configurée à la fois sur le client et le serveur avant que la connexion ne soit établie. Si le protocole SSL est uniquement configuré sur le serveur, le client peut envoyer des informations sensibles telles que des mots de passe avant qu’il ne soit établi que le serveur requiert une sécurité élevée.

Par défaut, [!DNL PostgreSQL] n’effectue aucune vérification du certificat du serveur. Pour vérifier l’identité du serveur et garantir une connexion sécurisée avant l’envoi de données sensibles (dans le cadre du mode de `verify-full` SSL), vous devez placer un certificat racine (autosigné) sur votre ordinateur local (`root.crt`) et un certificat feuille signé par le certificat racine sur le serveur.

Si le paramètre `sslmode` est défini sur `verify-full`, libpq vérifie que le serveur est fiable en vérifiant la chaîne de certificats jusqu’au certificat racine stocké sur le client. Il vérifie ensuite que le nom d’hôte correspond au nom stocké dans le certificat du serveur.

Pour permettre la vérification du certificat du serveur, vous devez placer un ou plusieurs certificats racine (`root.crt`) dans le fichier [!DNL PostgreSQL] de votre répertoire personnel. Le chemin d’accès au fichier serait similaire à `~/.postgresql/root.crt`.

## Activez le mode SSL complet à utiliser avec une connexion [!DNL Query Service] tierce {#instructions}

Si vous avez besoin d’un contrôle de sécurité plus strict que `sslmode=require`, vous pouvez suivre les étapes mises en surbrillance pour connecter un client tiers à [!DNL Query Service] à l’aide `verify-full` mode SSL.

>[!NOTE]
>
>Il existe de nombreuses options pour obtenir un certificat SSL. En raison d’une tendance croissante des certificats non fiables, DigiCert est utilisé dans ce guide, car il s’agit d’un fournisseur mondial de confiance de solutions TLS/SSL, PKI, IoT et de signature de haute assurance.

1. Accédez à [la liste des certificats racines DigiCert disponibles](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. Recherchez « [!DNL DigiCert Global Root G2] » dans la liste des certificats disponibles.
1. Sélectionnez [!DNL **Télécharger PEM**] pour télécharger le fichier sur votre ordinateur local.
   ![La liste des certificats racine DigiCert disponibles avec Télécharger PEM mis en surbrillance.](../images/clients/ssl-modes/digicert.png)
1. Renommez le fichier de certificat de sécurité en `root.crt`.
1. Copiez le fichier dans le dossier [!DNL PostgreSQL]. Le chemin d’accès au fichier nécessaire varie en fonction de votre système d’exploitation. Si le dossier n’existe pas déjà, créez-le.
   - Si vous utilisez macOS, le chemin est `/Users/<username>/.postgresql`
   - Si vous utilisez Windows, le chemin est `%appdata%\postgresql`

>[!TIP]
>
>Pour trouver l&#39;emplacement de votre fichier `%appdata%` sur un système d&#39;exploitation Windows, appuyez sur ⊞ **Win + R** et saisissez `%appdata%` dans le champ de recherche.

Une fois que le fichier CRT [!DNL DigiCert Global Root G2] est disponible dans votre dossier [!DNL PostgreSQL], vous pouvez vous connecter à [!DNL Query Service] à l’aide de l’option `sslmode=verify-full` ou `sslmode=verify-ca` .

## Étapes suivantes

Grâce à la lecture de ce document, vous comprenez mieux les options SSL disponibles pour connecter un client tiers à [!DNL Query Service], ainsi que la manière d’activer l’option `verify-full` SSL pour chiffrer vos données en mouvement.

Si vous ne l’avez pas déjà fait, suivez les instructions de la section [Connexion d’un client tiers à [!DNL Query Service]](./overview.md).
