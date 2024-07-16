---
title: Présentation de la source RainFocus
description: Découvrez comment importer des données d’analyse et de gestion d’événements de votre compte RainFocus vers Experience Platform
last-substantial-update: 2023-06-21T00:00:00Z
badge: Version bêta
exl-id: 88e333e3-2b93-4d66-8412-efadea58ac46
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 6%

---

# [!DNL RainFocus]

>[!NOTE]
>
>La source [!DNL RainFocus] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

[!DNL RainFocus] est une plateforme que vous pouvez utiliser pour promouvoir vos événements et créer vos audiences. Vous pouvez utiliser [!DNL RainFocus] pour créer de belles pages promotionnelles, suivre les performances des campagnes et optimiser les conversions d’enregistrement.

Utilisez la source [!DNL RainFocus] de Adobe Experience Platform et Real-Time Customer Data Platform pour enrichir automatiquement vos profils de données client avec des événements d’expérience client en temps réel. Une fois activés, les événements d’expérience sont automatiquement diffusés dans Real-Time CDP, ce qui permet une segmentation puissante de l’audience, une analyse des données et l’activation du parcours du participant avec les destinations et applications en aval telles que Customer Journey Analytics et Adobe Journey Optimizer.

>[!IMPORTANT]
>
>Ce connecteur source et cette page de documentation sont créés et gérés par l’équipe [!DNL RainFocus]. Pour toute question ou demande de mise à jour, contactez-les directement à l’adresse clientcare<span>@rainfocus.com ou rendez-vous sur le [[!DNL RainFocus] centre d’aide](https://help.rainfocus.com/hc/en-us)

## Conditions préalables

Vous devez remplir les conditions préalables suivantes avant d’activer l’intégration [!DNL RainFocus] sur Experience Platform :

[Création d’un compte de service Adobe (JWT) dans le portail Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)

>[!IMPORTANT]
>
>Adobe a récemment annoncé l’abandon des jetons JWT en faveur d’OAuth. Pour tenir compte de cette modification, la source [!DNL RainFocus] sera migrée vers OAuth dans un avenir proche.

### Collecter les informations d’identification requises

Pour vous connecter [!DNL RainFocus] à Experience Platform, vous devez fournir des valeurs pour les propriétés de connexion suivantes dans [!DNL RainFocus] :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| Identifiant client | Vous pouvez obtenir l’ID client à partir du compte de service Adobe sur le portail Adobe Developer. | `b9c32a63e7d41a0f87d3e8b52a16e7a2` |
| Secret client | Le secret client peut être obtenu à partir du compte Adobe Service sur le portail Adobe Developer. | `k1b-p-umplcjtg_arnw-R-Bx44bybu` |
| Identifiant du compte technique | L’identifiant de compte technique peut être obtenu à partir du compte de service Adobe sur le portail Adobe Developer. | `B3F9D2E8A64C573D21ABFE97@techacct.adobe.com` |
| ID d’organisation | L’ID d’organisation peut être obtenu à partir du compte de service Adobe sur le portail Adobe Developer | `D9A6F3BCE82FD147C50E3A19@techacct.adobe.com` |

### Créer un schéma XDM et définir le champ d’identité {#create-an-xdm-schema-and-define-the-identity-field}

Pour stocker les événements d’expérience de [!DNL RainFocus] dans Experience Platform, vous devez créer un schéma de modèle de données d’expérience (XDM) afin de décrire un jeu de données qui peut stocker les champs et les types de données possibles qui seront envoyés depuis [!DNL RainFocus].

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
| `attendee.attendeeId` | Chaîne | 1619119968857001fvLB | Identifiant du participant dans [!DNL RainFocus]. |
| `attendee.externalId` | Chaîne | 1666809456617001wyPj | ID externe spécifié par une organisation. |
| `attendee.clientId` | Chaîne | 8EFC1F57631CAFE70A495ECB@8f3f1f5c631caf3e495fd8.e | Identifiant du client SSO du participant. |
| `attendee.email` | Chaîne | user<span>@company.com | Adresse électronique du participant. |
| `transmissionId` | Chaîne | 1680309557133001Yhz | Identifiant unique utilisé pour la transmission de données. |
| `eventType` | Chaîne | SessionScheduled | Nom de l’événement d’expérience de participant. |
| `timestamp` | DateTime | 2023-04-01T00:41:57.000Z | Horodatage de la transmission de données. |
| `event.name` | Chaîne | Adobe Summit 2023 | Nom de l’événement au cours duquel une transmission a eu lieu. |
| `exhibitor.exhibitorId` | Chaîne | 1680309557133001Yhz | L’identifiant [!DNL RainFocus] de l’exposant. |
| `exhibitor.externalId` | Chaîne | 1666809514105001lSJN | Identifiant de l’exposant dans le système client. |
| `exhibitor.name` | Chaîne | IBM | Nom de l’exposant. |
| `lead.leadId` | Chaîne | 1666809456617001wyPj | L’identifiant [!DNL RainFocus] de la piste. |
| `lead.note` | Chaîne | | |
| `session.sessionId` | Chaîne | 1666809373585001t4aV | L’identifiant [!DNL RainFocus] de la session. |
| `session.externalId` | Chaîne | 1666809456617001wyPj | Identifiant de la session dans le système client. |
| `session.code` | Chaîne | GS3 | Code de la session. |
| `session.title` | Chaîne | Inspiration Keynote | Titre de la session. |
| `session.length` | Nombre entier | 90 | Durée de la session. |
| `sessiontime.sessiontimeId` | Chaîne | 1673033149739001OJLZ | L’identifiant [!DNL RainFocus] de l’heure de la session. |
| `sessiontime.startTime` | Chaîne | 2023-03-22 10:00:00 | Heure de début de la session. |
| `sessiontime.endTime` | Chaîne | 2023-03-22 10:00:00 | Heure de fin de la session. |
| `sessiontime.room` | Chaîne | B32 | La pièce utilisée pour la session. |

{style="table-layout:auto"}

Pour créer votre schéma pour les données [!DNL RainFocus], consultez la documentation suivante pour savoir comment créer un schéma à l’aide d’API ou de l’interface utilisateur.

* [Création du schéma à l’aide de l’interface utilisateur](../../../xdm/tutorials/create-schema-ui.md)
* [Création du schéma à l’aide de l’API](../../../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>* Le schéma doit étendre la **classe XDM ExperienceEvent.**
>* Vous devez vous assurer que le schéma comprend une **identité principale** et qu’il est **activé pour Profile**. Pour plus d’informations, consultez le guide sur la [définition des champs d’identité dans l’interface utilisateur](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
>* Vous pouvez remplacer l’exemple d’identité (adresse électronique) par un autre identifiant approprié, tel qu’un e-mail sha256 ou un ECID.

### Création d’un profil d’intégration dans RainFocus {#create-an-integration-profile-in-rainfocus}

Une fois votre compte de service et votre schéma XDM prêts, vous pouvez désormais activer le [!DNL Integration Profile] via la plateforme [!DNL RainFocus]. [!DNL Integration Profile] est responsable de la diffusion en continu des données vers l’Experience Platform.

Connectez-vous à la [[!DNL RainFocus] plateforme](https://app.rainfocus.com). Dans la navigation principale, sélectionnez **[!DNL Libraries]**, puis **[!DNL Integration Profiles]**.

![L’interface utilisateur de RainFocus avec bibliothèques et profils d’intégration sélectionnés.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile.png)

Pour créer un profil, sélectionnez l’icône **(`+`)** . Ensuite, sélectionnez **Adobe Real-Time Customer Data Platform**, puis **OK**.

![Fenêtre de création de profil d’intégration dans l’interface utilisateur de RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-select.png)

Indiquez ensuite les informations d’identification que vous avez récupérées dans le projet Adobe Developer Portal :

* **Identifiant du client**
* **Secret du client**
* **ID du compte technique**
* **ID d’organisation**

Une fois les informations d’identification fournies, sélectionnez **[!DNL Save]**. Vous devriez maintenant voir le nouveau [!DNL Integration Profile] répertorié dans le tableau de bord [!DNL RainFocus].

Sélectionnez le [!DNL Integration Profile] que vous venez de créer pour afficher une liste de **types push prédéfinis** déjà configurés. Il s’agit des [événements d’expérience](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html?lang=fr) qui seront envoyés à l’Experience Platform lorsqu’ils se produisent.

![Liste des types push prédéfinis dans le tableau de bord RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-setup.png)

Pour récupérer une copie de l’exemple de charge utile JSON, sélectionnez **[!DNL Sample JSON Payload]**. Ensuite, mettez en surbrillance et copiez l’exemple de payload JSON et **enregistrez-le dans un nouveau fichier avec une extension .json**. Il sera utilisé ultérieurement dans Experience Platform pour les [configurations de mappage](../../tutorials/ui/create/analytics/rainfocus.md#mapping).

![Exemple de payload JSON dans le tableau de bord RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-json.png)

>[!TIP]
>
>**La configuration n’est pas encore terminée** : une fois votre flux de données créé, vous devrez revenir au tableau de bord [!DNL RainFocus] pour terminer votre [!DNL Integration Profile] en fournissant votre **URL de point d’entrée de diffusion en continu** et l’ **identifiant de flux de données**.

## Étapes suivantes

En lisant ce document, vous avez terminé la configuration préalable nécessaire pour diffuser les données de votre compte [!DNL RainFocus] vers Experience Platform. Vous pouvez maintenant passer au guide sur la [connexion [!DNL RainFocus] à l’Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/analytics/rainfocus.md).
