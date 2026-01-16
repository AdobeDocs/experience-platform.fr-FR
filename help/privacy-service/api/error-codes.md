---
title: Codes d’erreur Privacy Service dans Adobe Experience Platform
description: Découvrez les codes d’erreur Privacy Service afin de diagnostiquer les échecs, de gérer les résultats des tâches par programmation et de déterminer les étapes suivantes lors de l’envoi ou de la surveillance des tâches de confidentialité.
keywords: privacy service, codes d’erreur, tâches de confidentialité, erreurs api
solution: Experience Platform
source-git-commit: a312dabf5b8c3b52af31e2e127cd4bbeb8dd0021
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 5%

---

# Codes d’erreur Privacy Service {#privacy-service-error-codes}

Utilisez cette référence pour identifier les résultats des tâches Privacy Service, diagnostiquer les échecs et déterminer les étapes suivantes appropriées lors de l&#39;envoi ou de la surveillance des tâches de confidentialité dans **Adobe Experience Platform**. Pour savoir comment créer, envoyer et surveiller les tâches de confidentialité, consultez le guide de point d’entrée des tâches de confidentialité [guide](./privacy-jobs.md) ou le guide d’utilisation de l’interface utilisateur de Privacy Service [&#128279;](../ui/user-guide.md).

Les codes d’erreur Privacy Service sont un contrat public stable. Chaque code d’erreur identifie de manière unique un état d’échec ou d’achèvement sur lequel vous pouvez compter pour la gestion programmatique et les workflows opérationnels.

Les garanties suivantes s’appliquent lors de la création de workflows d’automatisation ou de surveillance :

* Les codes d’erreur sont stables une fois publiés.
* Les messages d’erreur peuvent changer pour améliorer la clarté, mais pas la valeur du code.
* De nouveaux codes d’erreur peuvent être ajoutés au fil du temps ; les codes existants ne sont pas réutilisés.

Utilisez des codes d’erreur, et non du texte de message, pour implémenter l’automatisation ou la logique de décision. Pour obtenir des conseils sur le traitement efficace des tâches de confidentialité, la surveillance du statut des tâches et la gestion des erreurs sans se fier aux interrogations ou aux chaînes de message, consultez [Bonnes pratiques relatives à Privacy Service](../best-practices.md).

## Format de réponse d’erreur {#error-response-format}

Privacy Service renvoie des informations d’erreur dans les réponses de tâche et de requête. La réponse inclut un code d’erreur numérique et un message lisible par l’utilisateur dans la payload de réponse.

Le code d’erreur transmet le résultat faisant autorité. Le message fournit un contexte supplémentaire pour la résolution des problèmes.

Ce document décrit la signification et l’intention de chaque code d’erreur. Pour les schémas de réponse au niveau du champ et les détails de la requête, consultez la documentation de l’API Privacy Service [&#128279;](https://developer.adobe.com/experience-platform-apis/references/privacy-service/).

## Domaines d’erreur {#error-domains}

Les codes d’erreur sont regroupés par domaine fonctionnel pour vous aider à diagnostiquer les problèmes plus rapidement.

Les domaines utilisés dans ce document sont les suivants :

* **Validation de la demande** : la demande est incorrecte ou contient des valeurs non valides. Pour connaître la structure des requêtes et les exigences de validation[&#x200B; consultez le &#x200B;](./privacy-jobs.md) guide des points d’entrée des tâches de confidentialité .
* **Autorisation et mise en service** : votre organisation ou votre utilisateur ne dispose pas de l’accès requis. Voir [Gestion des autorisations](../permissions.md) pour consulter les exigences d’autorisation basées sur les rôles.
* **Identité et applicabilité** : les identifiants ou les espaces de noms ne s’appliquent pas à la requête. Voir [Données d’identité pour les demandes d’accès à des informations personnelles](../identity-data.md) pour les types d’identité pris en charge et les exigences en espace de noms.
* **Limitation du débit** : le volume des envois dépasse les limites de la plateforme. Lorsque cette erreur se produit, réduisez le taux d’envoi, puis réessayez.
* **Accès aux données et traitement des données** : le système ne peut pas accéder aux données demandées ni les traiter. Voir le [guide de dépannage](../troubleshooting-guide.md) pour connaître les causes courantes et les étapes de résolution des problèmes.
* **Chiffrement et gestion des clés** : les clés de chiffrement requises ne sont pas disponibles. Voir [Clés gérées par le client](../../landing/governance-privacy-security/customer-managed-keys/overview.md) pour obtenir des conseils sur l’accès, la configuration et la récupération des clés.
* **État d’exécution de la tâche** : la tâche s’est terminée entièrement, partiellement ou avec des échecs. Consultez le [guide des points d’entrée des tâches de confidentialité](./privacy-jobs.md#status-categories) pour obtenir une description des catégories de statut des tâches et de leur signification.

>[!NOTE]
>
>Les affectations de domaine reflètent l’intention du code d’erreur, et non les limites de service internes.

## Référence du code d’erreur {#error-code-reference}

Le tableau suivant répertorie tous les codes d’erreur Privacy Service publics.

| Code d’erreur | Statut HTTP | Titre | Description |
| ---------- | ----------- | ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------| 
| 1000-400 | 400 | Erreur de formatage | Une ou plusieurs valeurs de données pour l’application spécifiée présentent des problèmes de mise en forme. Pour plus d’informations, consultez les détails du traitement. |
| 1001-400 | 400 | Non autorisé | Votre organisation n’est pas approvisionnée. Contactez votre administrateur pour plus d’informations. |
| 1010-400 | 400 | Autorisations manquantes | Vous ne disposez pas des autorisations requises pour effectuer cette action. Contactez votre administrateur pour demander l’accès. |
| 1020-400 | 400 | Échec du chargement et de l’archivage | Un problème est survenu lors du chargement et de l&#39;archivage des données d&#39;accès. Chargez les données d’accès et réessayez. |
| 1021-400 | 400 | Échec du traitement | Une ou plusieurs tâches de confidentialité créées à partir de la requête ont échoué. Pour plus d’informations, consultez les détails des tâches ayant échoué. |
| 1022-400 | 400 | Échec d’accès aux données | Un problème s&#39;est produit lors de l&#39;accès aux données spécifiées. Pour plus d’informations, consultez les détails de la tâche. |
| 1023-400 | 400 | Échec d’accès aux données | Un problème s’est produit lors de l’accès ou de la localisation des ID de jeu de données spécifiés. Vérifiez que les identifiants fournis sont valides, puis réessayez. |
| 1024-400 | 400 | Erreur inattendue | Une erreur inattendue sʼest produite. Pour plus d’informations, consultez les détails de la tâche. |
| 1030-400 | 400 | Limite de taux de documents dépassée | La charge de travail a dépassé la limite de taux de documents. Réduisez le taux d’envoi, puis réessayez. |
| 1040-400 | 400 | Échec d’accès au chiffrement de la clé | Les données n’ont pas pu être traitées car le magasin de données est chiffré et l’accès à la clé a été révoqué. Contactez votre administrateur de coffre de clés pour restaurer l’accès à la clé du client. |
| 6000-200 | 200 | Réussite | Le traitement s’est terminé avec succès. Passez en revue les détails de la tâche pour confirmer les enregistrements traités et les résultats. |
| 6051-200 | 200 | Non approvisionné | Votre organisation ne dispose pas des privilèges d’accès pour l’application demandée. La requête n’est pas applicable. |
| 6052-200 | 200 | ID d’utilisateur introuvables | Certains ID d&#39;utilisateur sont introuvables et les ID d&#39;utilisateur inconnus ne s&#39;appliquent pas à ce produit. Vérifiez que les ID utilisateur sont valides, puis réessayez. |
| 6053-200 | 200 | Espace de noms non valide | L’espace de noms d’identité fourni n’est pas valide pour cette application. Utilisez un espace de noms reconnu par le système. |
| 6054-200 | 200 | Partiellement terminé | La tâche s’est terminée pour les données applicables, mais certaines données ne s’appliquaient pas à la requête. Pour plus d’informations, consultez les détails de la tâche. |

{style="table-layout:auto"}
