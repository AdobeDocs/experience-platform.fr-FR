---
title: Barrières de sécurité pour Identity Service (avec logique de suppression)
description: Découvrez les barrières de sécurité pour Identity Service.
hide: true
hidefromtoc: true
source-git-commit: db8edbbc3ea5d8fcec3de95b9a37387bea493693
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 9%

---

# Barrières de sécurité pour [!DNL Identity Service] données (avec logique de suppression)

Ce document fournit des informations sur l’utilisation et les limites de taux pour [!DNL Identity Service] pour vous aider à optimiser l’utilisation du graphique d’identités. Lors de la révision des mécanismes de sécurisation suivants, on suppose que vous avez correctement modélisé les données. Si vous avez des questions sur la manière de modéliser vos données, contactez votre représentant du service client.

## Prise en main

Les services Experience Platform suivants sont impliqués dans la modélisation des données d’identité :

* [Identités](home.md) : associez les identités à partir de sources de données disparates lors de leur ingestion dans Platform.
* [[!DNL Real-Time Customer Profile]](../profile/home.md) : créez des profils clients unifiés à l’aide de données provenant de plusieurs sources.

## Limites du modèle de données

Les tableaux ci-dessous fournissent des conseils sur les barrières de sécurité pour les limites statiques et les règles de validation à prendre en compte pour les espaces de noms d’identité.

### Limites statiques

Le tableau suivant décrit les limites statiques appliquées aux données d’identité.

| Mécanisme de sécurisation | Limite | Notes |
| --- | --- | --- |
| Nombre d’identités dans un graphique [!BADGE Beta]{type=Informative} | 50 | Lorsqu’un graphique comportant 50 identités liées est mis à jour, Identity Service applique un mécanisme &quot;premier entré, premier sorti&quot; et supprime l’identité la plus ancienne afin de libérer de l’espace pour la nouvelle identité. La suppression est basée sur le type d’identité et l’horodatage. La limite est appliquée au niveau de l’environnement de test. Lisez la section [annexe](#appendix) pour plus d’informations sur la manière dont Identity Service supprime les identités une fois la limite atteinte. |
| Nombre d’identités dans un enregistrement XDM | 20 | Le nombre minimum d’enregistrements XDM requis est de deux. |
| Nombre d’espaces de noms personnalisés | Aucun | Il n’existe aucune limite au nombre d’espaces de noms personnalisés que vous pouvez créer. |
| Nombre de graphiques | Aucun | Il n’existe aucune limite au nombre de graphiques d’identités que vous pouvez créer. |
| Nombre de caractères pour un nom d’affichage d’espace de noms ou un symbole d’identité | Aucun | Le nombre de caractères du nom d’affichage ou du symbole d’identité d’un espace de noms est illimité. |

### Validation de la valeur d’identité

Le tableau suivant décrit les règles existantes que vous devez suivre pour garantir une validation réussie de votre valeur d’identité.

| Espace de noms | Règle de validation | Comportement du système en cas de violation de la règle |
| --- | --- | --- |
| ECID | <ul><li>La valeur d’identité d’un ECID doit comporter exactement 38 caractères.</li><li>La valeur d’identité d’un ECID ne doit être composée que de nombres.</li></ul> | <ul><li>Si la valeur d’identité d’ECID ne comporte pas exactement 38 caractères, l’enregistrement est ignoré.</li><li>Si la valeur d’identité d’ECID contient des caractères non numériques, l’enregistrement est ignoré.</li></ul> |
| Non ECID | La valeur d’identité ne peut pas dépasser 1 024 caractères. | Si la valeur d’identité dépasse 1 024 caractères, l’enregistrement est ignoré. |

### Ingestion des espaces de noms d’identité

À compter du 31 mars 2023, Identity Service bloquera l’ingestion d’Adobe Analytics ID (AAID) pour les nouveaux clients. Cette identité est généralement ingérée via la variable [Source Adobe Analytics](../sources/connectors/adobe-applications/analytics.md) et la variable [Source Adobe Audience Manager](../sources//connectors/adobe-applications/audience-manager.md) et est redondant, car l’ECID représente le même navigateur web. Si vous souhaitez modifier cette configuration par défaut, contactez votre équipe de compte d’Adobe.

## Étapes suivantes

Pour plus d’informations sur la [!DNL Identity Service]:

* [Présentation des [!DNL Identity Service]](home.md)
* [Graphique d’identités observateur](ui/identity-graph-viewer.md)

## Annexe {#appendix}

La section suivante contient des informations supplémentaires sur les barrières de sécurité pour Identity Service.

### [!BADGE Beta]{type=Informative} Comprendre la logique de suppression lorsqu’un graphique d’identités à la capacité est mis à jour {#deletion-logic}

Lorsqu’un graphique d’identités complet est mis à jour, Identity Service supprime l’identité la plus ancienne du graphique avant d’ajouter la dernière identité. Cela permet de maintenir la précision et la pertinence des données d’identité. Ce processus de suppression suit deux règles Principales :

#### Règle #1 La suppression est prioritaire en fonction du type d’identité d’un espace de noms.

La priorité de suppression est la suivante :

1. ID de cookie
2. ID de périphérique
3. Identifiant, courrier électronique et téléphone multi-appareils

#### Règle #2 La suppression est basée sur l’horodatage stocké sur l’identité.

Chaque identité liée dans un graphique possède son propre horodatage correspondant. Lorsqu’un graphique complet est mis à jour, Identity Service supprime l’identité avec l’horodatage le plus ancien.

Lorsqu’un graphique complet est mis à jour avec une nouvelle identité, ces deux règles fonctionnent conjointement pour désigner l’ancienne identité qui sera supprimée. Identity Service supprime d’abord l’ID de cookie le plus ancien, puis l’ID d’appareil le plus ancien, et enfin l’ID multi-appareils le plus ancien, l’e-mail/le téléphone.

>[!NOTE]
>
>Si l’identité désignée pour être supprimée est liée à plusieurs autres identités du graphique, les liens reliant cette identité seront également supprimés.

Dans l’exemple ci-dessous, avant que le graphique de gauche puisse être mis à jour avec une nouvelle identité, Identity Service doit d’abord supprimer l’identité existante avec l’horodatage le plus ancien. Cependant, comme l’identité la plus ancienne est un identifiant d’appareil, Identity Service ignore cette identité jusqu’à ce qu’elle atteigne l’espace de noms avec un type plus élevé sur la liste de priorité de suppression, qui dans ce cas est `ecid-3`. Une fois l’identité la plus ancienne avec un type de priorité de suppression plus élevé supprimé, le graphique est mis à jour avec un nouveau lien, `ecid-51`.

>[!NOTE]
>
>Dans le rare cas où il existe deux identités avec le même horodatage et le même type d’identité, Identity Service triera les identifiants en fonction du XID et effectuera la suppression.

![Exemple de suppression de l’identité la plus ancienne pour tenir compte de la dernière identité](./images/graph-limits-v3.png)