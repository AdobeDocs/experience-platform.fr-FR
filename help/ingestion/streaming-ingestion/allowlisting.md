---
title: Adresse IP Plaçant sur la liste autorisée pour l’API d’ingestion en flux continu
description: Découvrez comment sécuriser l’accès à l’API d’ingestion en flux continu en autorisant uniquement les adresses IP spécifiées par le biais du placé sur la liste autorisée. Ce guide explique comment configurer, activer et gérer des restrictions basées sur les adresses IP pour la sécurité des API.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: f1d851afae5ad271e3c7d9d887f614058a262874
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 3%

---

# LISTE AUTORISÉE d’adresse IP pour l’API d’ingestion en flux continu

>[!AVAILABILITY]
>
>Placer sur la liste autorisée La prise en charge de l’adressage IP pour l’API d’ingestion en flux continu est en version bêta et votre organisation n’y a peut-être pas encore accès. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

Placer sur la liste autorisée Vous pouvez désormais des adresses IP pour l’API d’ingestion en flux continu. Utilisez cette fonctionnalité pour sécuriser vos points d’entrée d’ingestion en limitant l’accès aux seules adresses IP que vous spécifiez.

## Placer sur la liste autorisée Fonctionnement de l’adressage IP

Placer sur la liste autorisée La fonction de filtrage des adresses IP fonctionne comme suit :

1. **Adresses IP d’envoi :** vous fournissez une liste d’adresses IP de confiance, mappées à vos sandbox.
2. **Configuration :** Adobe configure la liste autorisée au niveau de l’organisation et du sandbox pour votre organisation.
3. **Application :** les demandes entrantes sont évaluées par rapport à la place sur la liste autorisée fournie :
   * Si l’adresse IP correspond à votre place sur la liste autorisée, la demande est traitée normalement.
   * Si l’adresse IP ne figure pas dans la place sur la liste autorisée, la requête est bloquée et une erreur HTTP 403 est reçue sans corps de réponse.

## Considérations principales

* Placer sur la liste autorisée La fonction de limitation des adresses IP s’applique uniquement à l’[API d’ingestion en flux continu](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) (`dcs.adobedc.net`) et ne s’applique **pas** aux `server.adobedc.net` ou aux `edge.adobedc.net`.
* Les nouveaux sandbox sont ouverts par défaut jusqu’à ce que la fonction de liste autorisée soit activée.
* La suppression d’un sandbox de la place sur la liste autorisée le rouvre sur Internet.
* Vous devez tenir à jour la liste complète des mappages sandbox-vers-adresses IP de votre côté et toujours envoyer la liste complète dans le formulaire de liste autorisée des adresses IP. Les mises à jour incrémentielles ne sont pas prises en charge.

## Placer sur la liste autorisée Activer l’adresse IP en cours de traitement

Suivez les étapes ci-dessous pour activer les adresses IP qui placent sur la liste autorisée pour votre organisation :

1. Placer sur la liste autorisée Téléchargez et remplissez le formulaire [adresse IP en cours de ](../images/assets/ip_allowlisting_aep.xlsx.zip).
2. Ouvrez un ticket d’assistance et enregistrez l’objet en tant que **AEP DCS et ingestion par flux - Demande de Liste autorisée d’IP**. Joindre le formulaire complété à ce ticket.
3. Après l’envoi de votre ticket, l’assistance clientèle d’Adobe transmettra votre demande à l’ingénierie.
4. Placer sur la liste autorisée Les ingénieurs activent et confirment la configuration.
5. Vous pouvez ensuite valider l’accès et confirmer à l’aide du ticket d’assistance.

| Organisation | Nom du sandbox | Adresses IP autorisées |
| --- | --- | --- |
| ACME | Prod | 203.0.113.42, 198.51.100.25, 192.0.2.10 |
| ACME | Développement | 203.0.113.43, 198.51.100.26, 192.0.2.11 |
| LUMA | Prod | 203.0.113.46, 198.51.100.29, 192.0.2.14 |

## Questions fréquentes

Lisez les sections suivantes pour obtenir des réponses aux questions fréquentes sur le placé sur la liste autorisée des adresses IP pour l’API d’ingestion en flux continu.

### Quelles API sont couvertes ?

Seuls les points d’entrée `dcs.adobedc.net` de l’API d’ingestion en flux continu.

## Que se passe-t-il si ma requête provient d’une adresse IP non répertoriée ?

Il est bloqué avec une erreur HTTP 403.

### Les nouveaux sandbox sont-ils automatiquement protégés ?

Non. Ils sont ouverts jusqu’à ce que vous fournissiez des mappages d’adresses IP via le formulaire de liste autorisée.

### Puis-je envoyer uniquement des adresses IP mises à jour lorsque ma place sur la liste autorisée change ?

Non. Vous devez toujours envoyer la liste complète des mappages de sandbox et d’adresses IP. Les mises à jour partielles (incrémentielles) ne sont pas acceptées.