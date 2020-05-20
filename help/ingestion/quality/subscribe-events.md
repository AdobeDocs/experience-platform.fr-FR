---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: S'abonner aux événements d'assimilation de données
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 2%

---


# Notifications d’assimilation de données

Le processus d’importation de données dans Adobe Experience Platform comprend plusieurs étapes. Une fois que vous avez identifié les fichiers de données à ingérer dans la plate-forme, le processus d’assimilation commence et chaque étape se produit consécutivement jusqu’à ce que les données soient correctement ingérées ou échouent. Le processus d’assimilation peut être lancé à l’aide de l’API [d’administration des données de la plateforme](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) Adobe Experience Platform ou à l’aide de l’interface utilisateur de la plate-forme Experience Platform.

Les données chargées dans Platform doivent passer par plusieurs étapes pour atteindre leur destination, Data Lake ou le magasin de données du Profil client en temps réel. Chaque étape implique de traiter les données, de les valider, puis de les stocker avant de les transmettre à l’étape suivante. Selon la quantité de données ingérées, ce processus peut prendre du temps et il est toujours possible que le processus échoue en raison d’erreurs de validation, de sémantique ou de traitement. En événement d’échec, les problèmes de données doivent être résolus, puis l’ensemble du processus d’assimilation doit être redémarré à l’aide des fichiers de données corrigés.

Pour faciliter le contrôle du processus d’assimilation, Experience Platform permet de s’abonner à un ensemble de événements publiés par chaque étape du processus, en vous informant de l’état des données assimilées et de tout échec éventuel.

## événements de notification d&#39;état disponibles

Vous trouverez ci-dessous une liste de notifications d&#39;état d&#39;assimilation de données à laquelle vous pouvez vous abonner.

>[!NOTE] Une seule rubrique de événement est fournie pour toutes les notifications d&#39;assimilation de données. Pour distinguer les différents états, il est possible d&#39;utiliser le code du événement.

| Service Plateforme | État | Description des événements | Code Événement |
| ---------------- | ------ | ----------------- | ---------- |
| Entrée de données | success | Ingestion - Le lot a réussi | ing_load_success |
| Entrée de données | échec | Ingestion - Échec du lot | ing_load_failure |
| Profil client en temps réel | success | Service de Profil - Lot de chargement de données terminé | ps_load_success |
| Profil client en temps réel | échec | Service de Profil - Échec du lot de chargement des données | ps_load_failure |
| Graphique d&#39;identité | success | Graphique d’identité - Succès du lot de chargement des données | ig_load_success |
| Graphique d&#39;identité | échec | Graphique d’identité - Échec du lot de chargement des données | ig_load_failure |

## schéma de charge utile de notification

Le schéma de événement de notification d’ingestion de données est un schéma de modèle de données d’expérience (XDM) contenant des champs et des valeurs qui fournissent des détails sur l’état des données ingérées. Veuillez visiter le repo public XDM GitHub afin de vue du dernier schéma [de charge utile de](https://github.com/adobe/xdm/blob/master/schemas/common/notifications/ingestion.schema.json)notification.

## S&#39;abonner aux notifications d&#39;état d&#39;importation de données

Grâce aux Événements [d’E/S](https://www.adobe.io/apis/experienceplatform/events.html)Adobe, vous pouvez vous abonner à plusieurs types de notification à l’aide de hameçons Web. Pour en savoir plus sur les hameçons WebHooks et sur la façon de s’abonner à des Événements d’E/S Adobe à l’aide de hameçons WebHooks, reportez-vous à l’ [introduction du guide des hameçons](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) WebHooks des Événements d’E/S Adobe.

### Créer une nouvelle intégration à l’aide de la console d’E/S d’Adobe

Connectez-vous à la console [d’E/S](https://console.adobe.io/home) Adobe et cliquez sur l’onglet *Intégrations* ou sur **Créer une intégration** sous Début rapide. Lorsque l’écran *Intégration* s’affiche, cliquez sur **Nouvelle intégration** pour créer une nouvelle intégration.

![Créer une nouvelle intégration](../images/quality/subscribe-events/create_integration_start.png)

L’écran *Créer une nouvelle intégration* s’affiche. Sélectionnez **Recevoir des événements temps réels** proches, puis cliquez sur **Continuer**.

![Recevoir des événements en temps quasi réel](../images/quality/subscribe-events/create_integration_receive_events.png)

L’écran suivant fournit des options permettant de créer des intégrations avec différents événements, produits et services disponibles pour votre organisation en fonction de vos abonnements, droits et autorisations. Pour cette intégration, sélectionnez Notifications **de** plateformes sous Plate-forme d’expérience, puis cliquez sur **Continuer**.

![Sélectionner le fournisseur de événements](../images/quality/subscribe-events/create_integration_select_provider.png)

Le formulaire Détails *de l’* intégration s’affiche, vous obligeant à fournir un nom et une description pour l’intégration, ainsi qu’un certificat de clé publique.

Si vous ne disposez pas d’un certificat public, vous pouvez en générer un dans le terminal à l’aide de la commande suivante :

```shell
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub
```

Une fois que vous avez généré un certificat, faites glisser et déposez le fichier dans la zone Certificats **de clés** publiques ou cliquez sur **Sélectionner un fichier** pour parcourir votre répertoire de fichiers et sélectionner directement le certificat.

Après avoir ajouté votre certificat, l’option Enregistrement *du* Événement s’affiche. Cliquez sur **Ajouter Événement Inscription**.

![détails de l’intégration](../images/quality/subscribe-events/create_integration_details.png)

La boîte de dialogue des détails *d&#39;enregistrement du* Événement s&#39;étend pour afficher d&#39;autres commandes. Ici vous pouvez sélectionner vos types d&#39;événement et enregistrer votre webhook. Entrez un nom pour l’enregistrement du événement, l’URL du crochet Web *(Facultatif)*, ainsi qu’une brève description. Enfin, sélectionnez les types d&#39;événement auxquels vous souhaitez vous abonner (Notification d&#39;importation de données), puis cliquez sur **Enregistrer**.

![Sélectionner des événements](../images/quality/subscribe-events/create_integration_select_event.png)

## Étapes suivantes

Une fois que vous avez créé votre intégration d&#39;E/S, vous pouvez vue les notifications reçues pour cette intégration. Consultez le guide [Suivi des Événements](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) d’E/S Adobe pour obtenir des instructions détaillées sur la manière de suivre vos événements.
