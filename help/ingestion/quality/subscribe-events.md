---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: S'abonner aux événements d'assimilation de données
topic: overview
translation-type: tm+mt
source-git-commit: 1498739d753bdb569e0d3e091e4160bdae40a32f
workflow-type: tm+mt
source-wordcount: '851'
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

## S’abonner aux notifications d’état d’assimilation de données

Grâce aux Événements [d’E/S](https://www.adobe.io/apis/experienceplatform/events.html)Adobe, vous pouvez vous abonner à plusieurs types de notification à l’aide de hameçons Web. Les sections ci-dessous décrivent les étapes à suivre pour s’abonner aux notifications de plateforme pour les événements d’assimilation de données à l’aide d’Adobe Developer Console.

### Création d’un projet dans Adobe Developer Console

Accédez à [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) et connectez-vous avec votre Adobe ID. Suivez ensuite les étapes décrites dans le didacticiel relatif à la [création d’un projet](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) vide dans la documentation d’Adobe Developer Console.

### événements de la plateforme Ajouter expérience sur le projet

Une fois que vous avez créé un nouveau projet, accédez à l’écran d’aperçu de ce projet. De là, cliquez sur **[!UICONTROL Ajouter événement]**.

![](../images/quality/subscribe-events/add-event-button.png)

La boîte de dialogue événements __Ajouter apparaît. Cliquez sur Plate-forme****d’expérience pour filtrer la liste des options disponibles, puis sur Notifications**[!UICONTROL  de ]**plateforme avant de cliquer sur**[!UICONTROL  Suivant ]**.

![](../images/quality/subscribe-events/select-platform-events.png)

L’écran suivant affiche une liste de types d&#39;événement auxquels s’abonner. Sélectionnez Notification **[!UICONTROL d’importation de]** données, puis cliquez sur **[!UICONTROL Suivant]**.

![](../images/quality/subscribe-events/choose-event-subscriptions.png)

L’écran suivant vous invite à créer un JSON Web Token (JWT). Vous avez la possibilité de générer automatiquement une paire de clés ou de télécharger votre propre clé publique générée dans le terminal.

Pour les besoins de ce didacticiel, la première option est suivie. Cochez la case d&#39;option **[!UICONTROL Générer une paire]** de clés, puis cliquez sur le bouton **[!UICONTROL Générer la paire]** de clés dans le coin inférieur droit.

![](../images/quality/subscribe-events/generate-keypair.png)

Lorsque la paire de clés est générée, elle est automatiquement téléchargée par le navigateur. Vous devez stocker ce fichier vous-même, car il n’est pas conservé dans la Console développeur.

L’écran suivant vous permet de vérifier les détails de la paire de clés nouvellement générée. Cliquez sur **[!UICONTROL Suivant]** pour continuer.

![](../images/quality/subscribe-events/keypair-generated.png)

Dans l’écran suivant, indiquez le nom et la description de l’enregistrement du événement. Il est recommandé de créer un nom unique et facilement identifiable afin de différencier cette inscription de événement des autres sur le même projet.

![](../images/quality/subscribe-events/registration-details.png)

Plus loin dans le même écran, vous pouvez éventuellement configurer la manière de recevoir des événements. **[!UICONTROL Webhook]** vous permet de fournir une adresse webhook personnalisée pour recevoir des événements, tandis que l’action **** Runtime vous permet de faire de même avec [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html).

Ce didacticiel ignore cette étape de configuration facultative. Une fois que vous avez terminé, cliquez sur **[!UICONTROL Enregistrer les événements]** configurés pour terminer l’enregistrement du événement.

![](../images/quality/subscribe-events/receive-events.png)

La page des détails de l&#39;enregistrement de événement nouvellement créé s&#39;affiche, dans laquelle vous pouvez consulter les événements reçus, effectuer le suivi du débogage et modifier sa configuration.

![](../images/quality/subscribe-events/registration-complete.png)

## Étapes suivantes

Une fois que vous avez enregistré des notifications de plateforme à votre projet, vous pouvez vue recevoir des événements du tableau de bord du projet. Consultez le guide [Suivi des Événements](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) d’E/S Adobe pour obtenir des instructions détaillées sur la manière de suivre vos événements.
