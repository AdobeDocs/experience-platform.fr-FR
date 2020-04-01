---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'S''abonner au d''assimilation de données '
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# Notifications d’assimilation de données

Le processus d’importation de données dans Adobe Experience Platform se compose de plusieurs étapes. Une fois que vous avez identifié les fichiers de données qui doivent être assimilés dans la plate-forme, le processus d’assimilation commence et chaque étape se produit consécutivement jusqu’à ce que les données soient correctement assimilées ou échouent. Le processus d’assimilation peut être lancé à l’aide de l’API [d’administration des données d’](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) Adobe Experience Platform ou de l’interface utilisateur de la plateforme d’expérience.

Les données chargées dans Platform doivent suivre plusieurs étapes pour atteindre leur destination, Data Lake ou le magasin de données  du client en temps réel. Chaque étape implique le traitement des données, la validation des données, puis le stockage des données avant leur transmission à l’étape suivante. Selon la quantité de données ingérées, ce processus peut prendre du temps et il est toujours possible que le processus échoue en raison d’erreurs de validation, de sémantique ou de traitement. Dans le  d’un échec, les problèmes de données doivent être résolus, puis l’ensemble du processus d’assimilation doit être redémarré à l’aide des fichiers de données corrigés.

Pour faciliter le suivi du processus d’assimilation, Experience Platform permet de s’abonner à un ensemble de  publiés par chaque étape du processus, en vous notifiant l’état des données assimilées et les éventuels échecs.

## de notification d’état disponible 

Vous trouverez ci-dessous un de notifications d’état d’assimilation de données auxquelles vous pouvez vous abonner.

>[!NOTE] Une seule rubrique  est fournie pour toutes les notifications d’ingestion de données. Afin de faire la distinction entre les différents états, vous pouvez utiliser le code  du.

| Service Plateforme | État | Description des événements | Code  |
| ---------------- | ------ | ----------------- | ---------- |
| Entrée de données | success | Ingestion - Le lot a réussi | ing_load_success |
| Entrée de données | échec | Ingestion - Echec du lot | ing_load_failure |
| Profil client en temps réel | success | Service de  de données - Lot de charge de données réussi | ps_load_success |
| Profil client en temps réel | échec | Service de  - Échec du lot de chargement des données | ps_load_failure |
| Graphique d&#39;identité | success | Graphique d’identité - Succès du lot de chargement des données | ig_load_success |
| Graphique d&#39;identité | échec | Graphique d’identité - Échec du lot de chargement des données | ig_load_failure |

##  de données utiles de notification

Le de notification d’ingestion de données  est unmodèle de données d’expérience (XDM) qui contient des champs et des valeurs qui fournissent des détails sur l’état des données ingérées. Visitez le référentiel public XDM GitHub afin de du dernier de charge utile de [notification](https://github.com/adobe/xdm/blob/master/schemas/common/notifications/ingestion.schema.json).

## S&#39;abonner aux notifications d&#39;état d&#39;assimilation des données

Par le biais des [E/S](https://www.adobe.io/apis/experienceplatform/events.html)Adobe, vous pouvez vous abonner à plusieurs types de notification à l’aide de hameçons Web. Pour en savoir plus sur les hameçons Web et sur la manière de s’abonner à un d’E/S Adobe à l’aide de ces hameçons, reportez-vous à l’ [introduction du guide des hameçons](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) Web d’Adobe I/O.

### Création d’une intégration à l’aide d’Adobe I/O Console

Connectez-vous à [Adobe I/O Console](https://console.adobe.io/home) et cliquez sur l’onglet *Intégrations* ou cliquez sur **Créer une intégration** sous  rapide. Lorsque l’écran *Intégration* s’affiche, cliquez sur **Nouvelle intégration** pour créer une nouvelle intégration.

![Créer une nouvelle intégration](../images/quality/subscribe-events/create_integration_start.png)

L’écran *Créer une nouvelle intégration* s’affiche. Sélectionnez **Recevoir les** proches du, puis cliquez sur **Continuer**.

![Recevez des  en temps quasi réel](../images/quality/subscribe-events/create_integration_receive_events.png)

L’écran suivant fournit des options permettant de créer des intégrations avec différents , produits et services disponibles pour votre organisation en fonction de vos  de vos , de vos droits et de vos autorisations. Pour cette intégration, sélectionnez Notifications **de** plateforme sous Plate-forme d’expérience, puis cliquez sur **Continuer**.

![Sélectionner  fournisseur de](../images/quality/subscribe-events/create_integration_select_provider.png)

Le formulaire Détails *de l’* intégration s’affiche. Vous devez fournir un nom et une description pour l’intégration, ainsi qu’un certificat de clé publique.

Si vous ne disposez pas d’un certificat public, vous pouvez en générer un dans le terminal à l’aide de la commande suivante :

```shell
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub
```

Une fois que vous avez généré un certificat, faites glisser et déposez le fichier dans la zone Certificats **de clés** publiques ou cliquez sur **Sélectionner un fichier** pour parcourir le répertoire des fichiers et sélectionner le certificat directement.

Après avoir ajouté votre certificat, l’option *d’enregistrement* s’affiche. Cliquez sur **Ajouter  Inscription**.

![détails de l’intégration](../images/quality/subscribe-events/create_integration_details.png)

La boîte de dialogue des détails *d’enregistrement du* s’étend pour afficher d’autres commandes. Ici vous pouvez sélectionner votre et enregistrer votre webhook. Entrez un nom pour l’enregistrement du , l’URL du webhook *(facultatif)*, ainsi qu’une brève description. Enfin, sélectionnez le auquel vous souhaitez vous abonner (Notification d’importation de données), puis cliquez sur **Enregistrer**.

![Sélectionner](../images/quality/subscribe-events/create_integration_select_event.png)

## Étapes suivantes

Une fois que vous avez créé votre intégration d&#39;E/S, vous pouvez  les notifications reçues pour cette intégration. Pour obtenir des instructions détaillées sur la manière de suivre votre  d’ [d’E/S Adobe, reportez-vous au](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) guide Tracing Adobe I/O.
