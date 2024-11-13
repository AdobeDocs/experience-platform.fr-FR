---
title: Découverte De Champ XDM Avec Assistant D’IA
description: Lisez ce document pour savoir comment utiliser l’assistant d’IA pour la découverte de champs de modèle de données d’expérience (XDM).
badge: Alpha
hide: true
hidefromtoc: true
source-git-commit: 2348001facd7ae3a95254130ae377b4ef3f2a749
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%

---

# Découverte de champs XDM pour avec l’assistant d’IA

>[!AVAILABILITY]
>
>Cette fonctionnalité est en Alpha et peut ne pas être disponible pour votre entreprise. Pour participer au programme d’Alpha et accéder à cette fonctionnalité, contactez votre équipe de compte d’Adobe.

Vous pouvez utiliser l’assistant d’IA pour rechercher et découvrir des champs de modèle de données d’expérience (XDM) que vous pouvez ensuite utiliser pour créer des audiences ciblées dans Experience Platform.

Lisez le tableau suivant pour connaître les modèles de requête et d’invite pris en charge pour la découverte de champs XDM dans l’assistant d’IA.

>[!TIP]
>
>Bien que les modèles de requête et d’invite puissent être identiques dans différents cas d’utilisation, la formulation exacte d’une question varie en fonction des champs XDM et des schémas utilisés pour un environnement de test donné.

| Type de requête | Modèle de requête/invite | Exemples |
| --- | --- | --- |
| Découverte de champ XDM par domaine ou zone de données | Montrez-moi les champs XDM utilisés pour représenter {DATA_DOMAIN/AREA}. | <ul><li>Montrez-moi les champs XDM utilisés pour représenter les données de consentement.</li><li>Montrez-moi les champs XDM utilisés pour représenter des informations sur les abonnements aux emails.</li></ul> |
| Découverte de champ XDM par nom de champ général | <ul><li>Affichez-moi les champs XDM liés à {DATA_DOMAIN/AREA}.</li><li>Quels champs XDM contiennent {GENERAL_FIELD_NAME}.</li></ul> | <ul><li>Montrez-moi les champs XDM liés aux commandes.</li><li>M’afficher les champs XDM liés aux détails de l’interaction.</li><li>Quel champ XDM contient des identifiants visiteur ?</li><li>Quel champ XDM contient des catégories de produits ?</li></ul> |
| Découverte des champs XDM par lignage de modèle de données | <ul><li>Affichez-moi tous les champs de {FIELD_GROUP/CLASS_NAME} qui contiennent {GENERAL_FIELD_NAME}.</li><li>Qu’est-ce que le {FIELD_GROUP/CLASS_NAME} du champ XDM {GENERAL_FIELD_NAME} ?</li></ul> | <ul><li>Affichez-moi tous les champs du groupe de champs qui contiennent les données de produit.</li><li>Affichez-moi tous les champs du groupe de champs qui contient les données d’analyse.</li><li>Quelle est la classe du prénom du champ XDM ?</li><li>Quelle est la classe des abonnements aux emails de champ XDM ?</li></ul> |
| Invite à obtenir des descriptions améliorées avec des noms de champ | {FIELD_DISCOVERY_QUERY}. Incluez également des descriptions améliorées. | <ul><li>Montrez-moi les champs XDM utilisés pour représenter les données de consentement. Incluez également la description améliorée du champ.</li><li>M’afficher les champs XDM liés aux détails de l’interaction. Incluez également la description améliorée du champ.</li></ul> |

{style="table-layout:auto"}