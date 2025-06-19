---
source-git-commit: 1ab56cf2495238385d726277f6409d2e0c0cb017
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 3%

---
# Extraits

## Quotas et délais de traitement {#quotas}

Les demandes de suppression d’enregistrements sont soumises à des limites d’envoi d’identifiants quotidiennes et mensuelles, déterminées par les droits de licence de votre entreprise. Ces limites s’appliquent à la fois aux requêtes de suppression basées sur l’interface utilisateur et les API.

>[!NOTE]
>
>Vous pouvez envoyer jusqu’à 1 000 000 **d’identifiants par jour** mais uniquement si votre quota mensuel restant le permet. Si votre limite mensuelle est inférieure à 1 million, vos soumissions quotidiennes ne peuvent pas dépasser cette limite.

### Droit d’envoi mensuel par produit {#quota-limits}

Le tableau ci-dessous présente les limites d’envoi des identifiants par produit et niveau de droit. Pour chaque produit, la limite mensuelle est la moins élevée des deux valeurs suivantes : un plafond d’identifiant fixe ou un seuil basé sur un pourcentage lié à votre volume de données sous licence.

| Produit | Description du droit | Plafond mensuel (le moins élevé) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP ou Adobe Journey Optimizer | Sans Privacy and Security Shield ni module complémentaire Healthcare Shield | 2 000 000 d’identifiants ou 5 % de l’audience adressable |
| Real-Time CDP ou Adobe Journey Optimizer | Avec le module complémentaire Privacy and Security Shield ou Healthcare Shield | 15 000 000 d’identifiants ou 10 % de l’audience adressable |
| Customer Journey Analytics | Sans Privacy and Security Shield ni module complémentaire Healthcare Shield | 2 000 000 d’identifiants ou 100 d’identifiants par million de lignes CJA de droits |
| Customer Journey Analytics | Avec le module complémentaire Privacy and Security Shield ou Healthcare Shield | 15 000 000 d’identifiants ou 200 d’identifiants par million de lignes CJA de droits |

>[!NOTE]
>
> La plupart des entreprises ont des limites mensuelles inférieures en fonction de leur audience adressable réelle ou de leurs droits de ligne CJA.

Les quotas sont réinitialisés le premier jour de chaque mois civil. Le quota inutilisé n **est pas reporté**

>[!NOTE]
>
>Les quotas sont basés sur les droits mensuels sous licence de votre entreprise pour les **identifiants envoyés**. Elles ne sont pas appliquées par les mécanismes de sécurisation du système, mais peuvent être surveillées et examinées.
>
>La suppression d’enregistrements est un **service partagé**. Votre limite mensuelle reflète les droits les plus élevés pour Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics et tous les modules complémentaires Shield applicables.

### Chronologies de traitement des envois d’identifiants {#sla-processing-timelines}

Après l’envoi, les demandes de suppression d’enregistrements sont mises en file d’attente et traitées en fonction de votre niveau de droits.

| Description du produit et des droits | Durée de la file d’attente | Durée Maximale De Traitement (SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| Sans Privacy and Security Shield ni module complémentaire Healthcare Shield | Jusqu’à 15 jours | 30 jours |
| Avec le module complémentaire Privacy and Security Shield ou Healthcare Shield | Généralement 24 heures | 15 jours |

Si votre organisation requiert des limites plus élevées, contactez votre représentant Adobe pour une révision des droits.
