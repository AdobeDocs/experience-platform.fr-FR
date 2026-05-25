---
title: Présentation de la source RainFocus
description: Découvrez comment importer des données d’analyse et de gestion des événements de votre compte RainFocus à Experience Platform
last-substantial-update: 2023-06-21T00:00:00.000Z
badge: Beta
exl-id: 88e333e3-2b93-4d66-8412-efadea58ac46
TQID: https://experienceleague.adobe.com/olP6fi0NQZKb4kQcDLgJvHqBV72QX56-af7BMPddSms
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ff2b9b37-92e0-45fc-b853-379d44c08c89
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 1002
ht-degree: 7%

---

# [!DNL RainFocus]

>[!NOTE]
>
>La source [!DNL RainFocus] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

[!DNL RainFocus] est une plateforme que vous pouvez utiliser pour promouvoir vos événements et créer vos audiences. Vous pouvez utiliser [!DNL RainFocus] pour créer de belles pages promotionnelles, suivre les performances des campagnes et optimiser les conversions d’enregistrement.

Utilisez la source de [!DNL RainFocus] dans Adobe Experience Platform et Real-Time Customer Data Platform pour enrichir automatiquement vos profils de données client avec des événements d’expérience des participants en temps réel. Une fois activés, les événements d’expérience sont automatiquement diffusés en continu dans Real-Time CDP, ce qui permet une segmentation puissante des audiences, une analyse des données et l’activation du parcours des participants avec des destinations et des applications en aval telles que Customer Journey Analytics et Adobe Journey Optimizer.

>[!IMPORTANT]
>
>Ce connecteur source et cette page de documentation sont créés et gérés par l’équipe [!DNL RainFocus]. Pour toute demande ou information, contactez directement le service clientèle<span>@rainfocus.com ou rendez-vous sur le [[!DNL RainFocus] Centre d&#39;aide](https://help.rainfocus.com/hc/en-us)

## Conditions préalables

Vous devez remplir les conditions préalables suivantes avant de pouvoir activer l’intégration [!DNL RainFocus] sur Experience Platform :

[Création d’un compte de service Adobe (JWT) dans le portail Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)

>[!IMPORTANT]
>
>Adobe a récemment annoncé l’abandon des jetons JWT au profit d’OAuth. Pour tenir compte de cette modification, la source de [!DNL RainFocus] va migrer vers OAuth dans un avenir proche.

### Collecter les informations d’identification requises

Pour connecter [!DNL RainFocus] à Experience Platform, vous devez fournir des valeurs pour les propriétés de connexion suivantes dans [!DNL RainFocus] :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| Identifiant client | L’identifiant client peut être obtenu à partir du compte de service Adobe sur le portail Adobe Developer. | `b9c32a63e7d41a0f87d3e8b52a16e7a2` |
| Secret client | Le secret client peut être obtenu à partir du compte de service Adobe sur le portail Adobe Developer. | `k1b-p-umplcjtg_arnw-R-Bx44bybu` |
| Identifiant de compte technique | L’identifiant de compte technique peut être obtenu à partir du compte de service Adobe sur le portail Adobe Developer. | `B3F9D2E8A64C573D21ABFE97@techacct.adobe.com` |
| ID d’organisation | L’ID d’organisation est accessible à partir du compte de service Adobe sur le portail Adobe Developer | `D9A6F3BCE82FD147C50E3A19@techacct.adobe.com` |

### Création d’un schéma XDM et définition du champ d’identité {#create-an-xdm-schema-and-define-the-identity-field}

Pour stocker les événements d’expérience de [!DNL RainFocus] dans Experience Platform, vous devez créer un schéma de modèle de données d’expérience (XDM) pour décrire un jeu de données pouvant stocker les champs et types de données possibles qui seront envoyés depuis [!DNL RainFocus].

[!DNL RainFocus] recommande les champs suivants, qui couvrent toutes les données possibles envoyées par défaut.

Les groupes de champs suivants sont également recommandés (identifiés par un préfixe) :

* Participant
* Exposant
* Lead
* Session
* SessionTime

**Le schéma doit contenir les champs suivants :**

| Champ | Type | Exemple | Description |
| --- | --- | --- | --- |
| `attendee.registered` | Chaîne | Oui | Indicateur qui détermine si le participant est considéré comme enregistré. |
| `attendee.attendeeId` | Chaîne | 1619119968857001fvLB | ID de participant dans [!DNL RainFocus]. |
| `attendee.externalId` | Chaîne | 1666809456617001wyPj | ID externe spécifié par une organisation. |
| `attendee.clientId` | Chaîne | 8EFC1F57631CAFE70A495ECB@8f3f1f5c631caf3e495fd8.e | Identifiant du client SSO du participant. |
| `attendee.email` | Chaîne | user<span>@company.com | Adresse e-mail du participant. |
| `transmissionId` | Chaîne | 1680309557133001YHhz | Identifiant unique utilisé pour les notifications push de données. |
| `eventType` | Chaîne | SessionScheduled | Nom de l’événement d’expérience Participant. |
| `timestamp` | DateTime | 2023-04-:41:57.000Z | Date et heure de la notification push de données. |
| `event.name` | Chaîne | Adobe Summit 2023 | Nom de l’événement au cours duquel une transmission a eu lieu. |
| `exhibitor.exhibitorId` | Chaîne | 1680309557133001YHhz | Identifiant [!DNL RainFocus] de l’exposant. |
| `exhibitor.externalId` | Chaîne | 1666809514105001lSJN | Identifiant de l’exposant dans le système client. |
| `exhibitor.name` | Chaîne | IBM | Nom de l’exposant. |
| `lead.leadId` | Chaîne | 1666809456617001wyPj | Identifiant [!DNL RainFocus] du prospect. |
| `lead.note` | Chaîne | | |
| `session.sessionId` | Chaîne | 1666809373585001t4aV | Identifiant [!DNL RainFocus] de la session. |
| `session.externalId` | Chaîne | 1666809456617001wyPj | Identifiant de la session dans le système client. |
| `session.code` | Chaîne | GS3 | Code de la session. |
| `session.title` | Chaîne | Keynote sur l’inspiration | Titre de la session. |
| `session.length` | Entier | 90 | Durée de la session. |
| `sessiontime.sessiontimeId` | Chaîne | 1673033149739001OJLZ | Identifiant de [!DNL RainFocus] pour l’heure de la session. |
| `sessiontime.startTime` | Chaîne | 2023-03-22 10:00:00 | Heure de début de la session. |
| `sessiontime.endTime` | Chaîne | 2023-03-22 10:00:00 | Heure de fin de la session. |
| `sessiontime.room` | Chaîne | B32 | Salle utilisée pour la session. |

{style="table-layout:auto"}

Pour créer votre schéma pour les données [!DNL RainFocus], consultez la documentation suivante pour savoir comment créer un schéma à l’aide d’API ou de l’interface utilisateur.

* [Création du schéma à l’aide de l’interface utilisateur](../../../xdm/tutorials/create-schema-ui.md)
* [Créer le schéma à l’aide de l’API](../../../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>* Le schéma doit étendre la classe **XDM ExperienceEvent**.
>* Vous devez vous assurer que le schéma inclut une **identité principale** et est **activé pour Profil**. Pour plus d’informations, consultez le guide sur la [définition de champs d’identité dans l’interface utilisateur](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html?lang=fr)
>* Vous pouvez remplacer l’exemple d’identité (E-mail) par un autre identifiant approprié, tel qu’un e-mail sha256 ou un ECID.

### Création d’un profil d’intégration dans Rainfocus {#create-an-integration-profile-in-rainfocus}

Une fois votre compte de service et votre schéma XDM prêts, vous pouvez activer le [!DNL Integration Profile] via la plateforme [!DNL RainFocus]. Le [!DNL Integration Profile] est chargé de diffuser des données en continu vers Experience Platform.

Connectez-vous à la [[!DNL RainFocus] plateforme](https://app.rainfocus.com). Dans la navigation principale, sélectionnez **[!DNL Libraries]** puis **[!DNL Integration Profiles]**

![L’interface utilisateur RainFocus avec les bibliothèques et les profils d’intégration sélectionnés.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile.png)

Pour créer un profil, sélectionnez l’icône **(`+`)** . Ensuite, sélectionnez **&#x200B;**&#x200B;puis **OK**.

![Fenêtre Créer un profil d’intégration dans l’interface utilisateur de RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-select.png)

Indiquez ensuite les informations d’identification que vous avez récupérées dans le projet Adobe Developer Portal :

* **Identifiant du client**
* **Secret du client**
* **Identifiant de compte technique**
* **ID d’organisation**

Une fois les informations d’identification fournies, sélectionnez **[!DNL Save]**. Vous devriez maintenant voir les nouvelles [!DNL Integration Profile] répertoriées dans le tableau de bord [!DNL RainFocus].

Sélectionnez la [!DNL Integration Profile] que vous venez de créer pour afficher une liste de **types push** prédéfinis déjà configurés. Il s’agit des [événements d’expérience](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html?lang=fr) qui seront envoyés à Experience Platform lorsqu’ils se produiront.

![Liste des types push prédéfinis dans le tableau de bord RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-setup.png)

Pour récupérer une copie de l’exemple de payload JSON, sélectionnez **[!DNL Sample JSON Payload]**. Ensuite, mettez en surbrillance et copiez l’exemple de payload JSON et **enregistrez-le dans un nouveau fichier avec une extension .json**. Elle sera utilisée ultérieurement dans Experience Platform pour les [configurations de mappage](../../tutorials/ui/create/analytics/rainfocus.md#mapping).

![Exemple de payload JSON dans le tableau de bord RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-json.png)

>[!TIP]
>
>**La configuration n’est pas encore terminée** : une fois votre flux de données créé, vous devrez revenir au tableau de bord [!DNL RainFocus] pour terminer votre [!DNL Integration Profile] en fournissant votre **URL de point d’entrée de diffusion en continu** et **identifiant de flux de données**.

## Étapes suivantes

En lisant ce document, vous avez terminé la configuration requise pour diffuser des données de votre compte [!DNL RainFocus] vers Experience Platform. Vous pouvez maintenant passer au guide sur la [connexion [!DNL RainFocus] à Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/analytics/rainfocus.md).
