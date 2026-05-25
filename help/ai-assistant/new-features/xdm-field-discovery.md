---
title: Découverte des champs XDM avec l’assistant AI
description: Lisez ce document pour savoir comment utiliser l’assistant AI pour la découverte de champs du modèle de données d’expérience (XDM).
badge: Alpha
hide: true
exl-id: 041034c6-da45-437f-ad46-f9c2ded9f82c
TQID: https://experienceleague.adobe.com/-dXeZqH5-zPYNKFnEZa44lUtTWNkkUhdJso9flRSUQo
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: f8e8ea8a-6020-40da-99f7-6504fe599cb1
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 352
ht-degree: 1%

---

# Découverte des champs XDM avec l’assistant AI

>[!AVAILABILITY]
>
>Cette fonctionnalité se trouve dans Alpha et peut ne pas être disponible pour votre organisation. Pour participer au programme Alpha et accéder à cette fonctionnalité, contactez l’équipe chargée de votre compte Adobe.

Vous pouvez utiliser l’assistant d’IA pour rechercher et découvrir des champs du modèle de données d’expérience (XDM) que vous pouvez ensuite utiliser pour créer des audiences ciblées dans Experience Platform.

Lisez le tableau suivant pour connaître les modèles de requête et d’invite pris en charge pour la découverte de champs XDM dans l’assistant AI.

>[!TIP]
>
>Bien que les modèles de requête et d’invite puissent être identiques dans différents cas d’utilisation, la formulation exacte d’une question varie en fonction des champs XDM et des schémas utilisés pour un sandbox donné.

| Type de requête | Modèle de requête/invite | Exemples |
| --- | --- | --- |
| Découverte de champs XDM par domaine ou zone de données | Montrez-moi les champs XDM utilisés pour représenter {DATA_DOMAIN/AREA}. | <ul><li>Afficher les champs XDM utilisés pour représenter les données de consentement.</li><li>Montrez-moi les champs XDM utilisés pour représenter les informations sur les abonnements aux e-mails.</li></ul> |
| Découverte des champs XDM par nom de champ général | <ul><li>Afficher les champs XDM liés à {DATA_DOMAIN/AREA}.</li><li>Quels champs XDM contiennent des {GENERAL_FIELD_NAME} ?</li></ul> | <ul><li>Afficher les champs XDM liés aux commandes.</li><li>Afficher les champs XDM liés aux détails de l’interaction.</li><li>Quel champ XDM contient des identifiants visiteur ?</li><li>Quel champ XDM contient des catégories de produits ?</li></ul> |
| Découverte des champs XDM par lignage des modèles de données | <ul><li>Afficher tous les champs du {FIELD_GROUP/CLASS_NAME} qui contiennent des {GENERAL_FIELD_NAME}.</li><li>Qu’est-ce que le {FIELD_GROUP/CLASS_NAME} du {GENERAL_FIELD_NAME} de champ XDM ?</li></ul> | <ul><li>Afficher tous les champs du groupe de champs contenant des données de produit.</li><li>Afficher tous les champs du groupe de champs contenant les données d’analyse.</li><li>Quelle est la classe du prénom du champ XDM ?</li><li>Quelle est la classe des abonnements par e-mail aux champs XDM ?</li></ul> |
| Invite pour obtenir des descriptions améliorées avec des noms de champ | {FIELD_DISCOVERY_QUERY}. Incluez également des descriptions améliorées. | <ul><li>Afficher les champs XDM utilisés pour représenter les données de consentement. Incluez également la description améliorée du champ.</li><li>Afficher les champs XDM liés aux détails de l’interaction. Incluez également la description améliorée du champ.</li></ul> |

{style="table-layout:auto"}
