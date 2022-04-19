---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;se connecter;se connecter au service de requête;SSL;ssl;sslmode;
title: Options SSL de Query Service
description: Découvrez la prise en charge du protocole SSL pour les connexions tierces à Adobe Experience Platform Query Service et comment vous connecter à l’aide du mode SSL vérification-full.
source-git-commit: 92dac8e75e1ddda860d255ce1b7d278041c89325
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 1%

---

# [!DNL Query Service] Options SSL

Pour une sécurité accrue, Adobe Experience Platform [!DNL Query Service] fournit une prise en charge native des connexions SSL pour chiffrer les communications client/serveur. Ce document couvre les options SSL disponibles pour les connexions de clients tiers à [!DNL Query Service] et comment se connecter à l’aide du `verify-full` Valeur du paramètre SSL.

## Conditions préalables

Ce document suppose que vous avez déjà téléchargé une application cliente de bureau tierce à utiliser avec vos données Platform. Vous trouverez des instructions spécifiques sur la manière d’incorporer la sécurité SSL lors de la connexion à un client tiers dans la documentation de leur guide de connexion respectif. Pour obtenir une liste de tous les [!DNL Query Service] clients pris en charge, voir [présentation des connexions client](./overview.md).

## Options SSL disponibles {#available-ssl-options}

Platform prend en charge diverses options SSL pour répondre à vos besoins en matière de sécurité des données et équilibrer les frais de traitement liés au cryptage et à l’échange de clés.

Les différentes `sslmode` les valeurs de paramètre offrent différents niveaux de protection. En chiffrant vos données en mouvement à l’aide de certificats SSL, vous évitez les attaques par l’intermédiaire (MITM), les écoutes et les usurpations. Le tableau ci-dessous présente la répartition des différents modes SSL disponibles et le niveau de protection qu’ils assurent.

>[!NOTE]
>
> La valeur SSL `disable` n’est pas pris en charge par Adobe Experience Platform en raison de la conformité requise en matière de protection des données.

| sslmode | Protection des écouteurs | Protection MITM | Description |
|---|---|---|---|
| `allow` | Partiel | Non | La sécurité n’est pas une priorité, la vitesse et une faible surcharge de traitement sont plus importantes. Ce mode opte uniquement pour le cryptage si le serveur insiste dessus. |
| `prefer` | Partiel | Non | Le chiffrement n’est pas nécessaire, mais la communication sera chiffrée si le serveur le prend en charge. |
| `require` | Oui | Non | Le chiffrement est requis pour toutes les communications. Le réseau est approuvé pour la connexion au serveur approprié. La validation du certificat SSL du serveur n’est pas requise. |
| `verify-ca` | Oui | Dépend de la stratégie d’autorité de certification | Le chiffrement est requis pour toutes les communications. La validation du serveur est requise avant le partage des données. Pour ce faire, vous devez configurer un certificat racine dans votre répertoire racine PostgreSQL. [Vous trouverez ci-dessous des informations détaillées](#instructions) |
| `verify-full` | Oui | Oui | Le chiffrement est requis pour toutes les communications. La validation du serveur est requise avant le partage des données. Pour ce faire, vous devez configurer un certificat racine dans votre répertoire racine PostgreSQL. [Vous trouverez ci-dessous des informations détaillées](#instructions). |

>[!NOTE]
>
>La différence entre `verify-ca` et `verify-full` dépend de la stratégie de l’autorité de certification racine (CA). Si vous avez créé votre propre autorité de certification locale pour émettre des certificats privés pour vos applications, utilisez `verify-ca` offre souvent une protection suffisante. Si vous utilisez une autorité de certification publique, `verify-ca` permet les connexions à un serveur que quelqu’un d’autre peut avoir enregistré auprès de l’autorité de certification. `verify-full` doit toujours être utilisé avec une autorité de certification racine publique.

Lors de l’établissement d’une connexion tierce à une base de données Platform, il est recommandé d’utiliser `sslmode=require` au minimum pour garantir une connexion sécurisée pour vos données en cours. Le `verify-full` Le mode SSL est recommandé pour une utilisation dans la plupart des environnements sensibles à la sécurité.

## Configuration d’un certificat racine pour la vérification du serveur {#root-certificate}

Pour garantir une connexion sécurisée, l’utilisation du protocole SSL doit être configurée sur le client et sur le serveur avant que la connexion ne soit établie. Si le protocole SSL est uniquement configuré sur le serveur, le client peut envoyer des informations sensibles telles que des mots de passe avant qu’il ne soit établi que le serveur requiert une sécurité élevée.

Par défaut, [!DNL PostgreSQL] n’effectue aucune vérification du certificat du serveur. Vérification de l’identité du serveur et assurance d’une connexion sécurisée avant l’envoi de données sensibles (dans le cadre du protocole SSL) `verify-full` ), vous devez placer un certificat racine (auto-signé) sur votre ordinateur local (`root.crt`) et un certificat feuille signé par le certificat racine sur le serveur.

Si la variable `sslmode` est défini sur `verify-full`, libpq vérifie que le serveur est fiable en vérifiant la chaîne du certificat jusqu’au certificat racine stocké sur le client. Il vérifie ensuite que le nom d’hôte correspond au nom stocké dans le certificat du serveur.

Pour permettre la vérification des certificats du serveur, vous devez placer un ou plusieurs certificats racine (`root.crt`) dans la variable [!DNL PostgreSQL] dans votre répertoire racine. Le chemin d’accès au fichier serait similaire à `~/.postgresql/root.crt`.

## Activation du mode SSL vérification-full pour une utilisation avec un tiers [!DNL Query Service] connection {#instructions}

Si vous avez besoin d’un contrôle de sécurité plus strict que `sslmode=require`, vous pouvez suivre les étapes indiquées pour connecter un client tiers à [!DNL Query Service] using `verify-full` Mode SSL.

>[!NOTE]
>
>De nombreuses options sont disponibles pour obtenir un certificat SSL. En raison d’une tendance croissante des certificats frauduleux, DigiCert est utilisé dans ce guide, car il s’agit d’un fournisseur mondial de confiance de solutions TLS/SSL, PKI, IoT et de signature haute assurance.

1. Accédez à [la liste des certificats racine DigiCert disponibles ;](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. Recherchez &quot;[!DNL DigiCert Global Root CA]&quot; dans la liste des certificats disponibles.
1. Sélectionner [!DNL **Télécharger PEM**] pour télécharger le fichier sur votre ordinateur local.
   ![La liste des certificats racine DigiCert disponibles avec l’option Télécharger PEM mise en surbrillance.](../images/clients/ssl-modes/digicert.png)
1. Renommez le fichier de certificat de sécurité en `root.crt`.
1. Copiez le fichier dans le [!DNL PostgreSQL] dossier. Le chemin d’accès au fichier nécessaire varie en fonction de votre système d’exploitation. Si le dossier n’existe pas déjà, créez-le.
   - Si vous utilisez macOS, le chemin est `/Users/<username>/.postgresql`
   - Si vous utilisez Windows, le chemin est `%appdata%\postgresql`

>[!TIP]
>
>Pour rechercher votre `%appdata%` emplacement du fichier sur un système d’exploitation Windows, appuyez sur ⊞ **Win + R** et entrée `%appdata%` dans le champ de recherche.

Après la [!DNL DigiCert Global Root CA] Le fichier CRT est disponible dans votre [!DNL PostgreSQL] dossier auquel vous pouvez vous connecter [!DNL Query Service] en utilisant la variable `sslmode=verify-full` ou `sslmode=verify-ca` .

## Étapes suivantes

En lisant ce document, vous comprenez mieux les options SSL disponibles pour connecter un client tiers à [!DNL Query Service]et également comment activer la variable `verify-full` Option SSL pour chiffrer vos données en mouvement.

Si vous ne l’avez pas déjà fait, suivez les instructions de la rubrique [connexion d’un client tiers à [!DNL Query Service]](./overview.md).
