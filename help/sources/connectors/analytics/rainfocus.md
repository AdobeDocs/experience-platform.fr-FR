---
title: Présentation de la source RainFocus
description: Découvrez comment importer des données d’analyse et de gestion d’événements de votre compte RainFocus vers Experience Platform
badge: Version bêta
hide: true
hidefromtoc: true
source-git-commit: e9728e1e673a4018d1d776a9d9ddad023ad1393e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL RainFocus]

>[!NOTE]
>
>La source [!DNL RainFocus] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

[!DNL RainFocus] est une plateforme que vous pouvez utiliser pour promouvoir vos événements et créer vos audiences. Vous pouvez utiliser [!DNL RainFocus] pour créer de belles pages promotionnelles, suivre les performances de la campagne et optimiser les conversions d’enregistrement.

Utilisez la variable [!DNL RainFocus] source dans Adobe Experience Platform et Real-time Customer Data Platform pour enrichir automatiquement vos profils de données client avec les événements d’expérience client en temps réel. Une fois activés, les événements d’expérience sont automatiquement diffusés dans Real-Time CDP, ce qui permet une segmentation puissante de l’audience, une analyse des données et l’activation du parcours du participant avec les destinations et applications en aval telles que Customer Journey Analytics et Adobe Journey Optimizer.

>[!IMPORTANT]
>
>Cette page de documentation a été créée par la fonction [!DNL RainFocus] l&#39;équipe. Pour toute demande de renseignements ou de mise à jour, contactez-les directement au service clientèle.<span>@rainfocus.com ou rendez-vous sur la page [[!DNL RainFocus] Centre d’aide](https://help.rainfocus.com/hc/en-us)

## Conditions préalables

Vous devez remplir les conditions préalables suivantes avant de pouvoir activer le [!DNL RainFocus] intégration sur Experience Platform :

[Création d’un compte de service Adobe (JWT) dans le portail Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)

>[!IMPORTANT]
>
>Adobe a récemment annoncé l’abandon des jetons JWT en faveur d’OAuth. Pour tenir compte de cette modification, la variable [!DNL RainFocus] La source sera migrée vers OAuth dans un avenir proche.

### Collecter les informations d’identification requises

Pour vous connecter [!DNL RainFocus] pour Experience Platform, vous devez fournir des valeurs pour les propriétés de connexion suivantes dans [!DNL RainFocus]:

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| Identifiant client | Vous pouvez obtenir l’ID client à partir du compte de service Adobe sur le portail Adobe Developer. | `b9c32a63e7d41a0f87d3e8b52a16e7a2` |
| Secret client | Le secret client peut être obtenu à partir du compte Adobe Service sur le portail Adobe Developer. | `k1b-p-umplcjtg_arnw-R-Bx44bybu` |
| Identifiant de compte technique | L’identifiant de compte technique peut être obtenu à partir du compte de service Adobe sur le portail Adobe Developer. | `B3F9D2E8A64C573D21ABFE97@techacct.adobe.com` |
| ID d’organisation | L’ID d’organisation peut être obtenu à partir du compte de service Adobe sur le portail Adobe Developer | `D9A6F3BCE82FD147C50E3A19@techacct.adobe.com` |

### Création d’un schéma XDM et définition du champ d’identité {#create-an-xdm-schema-and-define-the-identity-field}

Pour stocker les événements d’expérience de [!DNL RainFocus] dans Experience Platform, vous devez créer un schéma de modèle de données d’expérience (XDM) pour décrire un jeu de données qui peut stocker les champs et les types de données possibles qui seront envoyés à partir de l’. [!DNL RainFocus].

[!DNL RainFocus] recommande les champs suivants, qui couvrent toutes les données possibles envoyées par défaut.

Les groupes de champs suivants sont également recommandés (identifiés par un préfixe) :

* Participant
* Exposant
* Prospect
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
| `transmissionId` | Chaîne | 1680309557133001YHhz | Identifiant unique utilisé pour la transmission de données. |
| `eventType` | Chaîne | SessionScheduled | Nom de l’événement d’expérience du participant. |
| `timestamp` | DateTime | 2023-04-01T00:41:57,000Z | Horodatage de la transmission de données. |
| `event.name` | Chaîne | Adobe Summit 2023 | Nom de l’événement au cours duquel une transmission a eu lieu. |
| `exhibitor.exhibitorId` | Chaîne | 1680309557133001YHhz | Le [!DNL RainFocus] identifiant de l’exposant. |
| `exhibitor.externalId` | Chaîne | 1666809514105001lSJN | Identifiant de l’exposant dans le système client. |
| `exhibitor.name` | Chaîne | IBM | Nom de l’exposant. |
| `lead.leadId` | Chaîne | 1666809456617001wyPj | Le [!DNL RainFocus] identifiant de la piste. |
| `lead.note` | Chaîne | | |
| `session.sessionId` | Chaîne | 1666809373585001t4aV | Le [!DNL RainFocus] identifiant de la session. |
| `session.externalId` | Chaîne | 1666809456617001wyPj | Identifiant de la session dans le système client. |
| `session.code` | Chaîne | GS3 | Code de la session. |
| `session.title` | Chaîne | Inspiration Keynote | Titre de la session. |
| `session.length` | Nombre entier | 90 | Durée de la session. |
| `sessiontime.sessiontimeId` | Chaîne | 1673033149739001OJLZ | Le [!DNL RainFocus] pour l’heure de la session. |
| `sessiontime.startTime` | Chaîne | 2023-03-22 10:00:00 | Heure de début de la session. |
| `sessiontime.endTime` | Chaîne | 2023-03-22 10:00:00 | Heure de fin de la session. |
| `sessiontime.room` | Chaîne | B32 | La pièce utilisée pour la session. |

{style="table-layout:auto"}

Pour créer votre schéma pour [!DNL RainFocus] pour savoir comment créer un schéma à l’aide d’API ou de l’interface utilisateur, consultez la documentation suivante.

* [Création du schéma à l’aide de l’interface utilisateur](../../../xdm/tutorials/create-schema-ui.md)
* [Création du schéma à l’aide de l’API](../../../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>* Le schéma doit étendre la variable **Classe XDM ExperienceEvent.**
>* Vous devez vous assurer que le schéma comprend une **Principale identité**, et est **activé pour Profile**. Pour plus d’informations, consultez le guide sur [définition des champs d’identité dans l’interface utilisateur](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
>* Vous pouvez remplacer l’exemple d’identité (adresse électronique) par un autre identifiant approprié, tel qu’un e-mail sha256 ou un ECID.

### Création d’un profil d’intégration dans RainFocus {#create-an-integration-profile-in-rainfocus}

Une fois votre compte de service et votre schéma XDM prêts, vous pouvez désormais activer la variable [!DNL Integration Profile] via la [!DNL RainFocus] plateforme. Le [!DNL Integration Profile] est chargé de la diffusion en continu des données vers l’Experience Platform.

Connectez-vous au [[!DNL RainFocus] platform](https://app.rainfocus.com). Dans la navigation Principale, sélectionnez **[!DNL Libraries]** puis sélectionnez **[!DNL Integration Profiles]**

![L’interface utilisateur de RainFocus avec les bibliothèques et les profils d’intégration sélectionnés.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile.png)

Pour créer un profil, sélectionnez l’option **(`+`)** icône . Ensuite, sélectionnez **Adobe Real-time Customer Data Platform** puis sélectionnez **OK**.

![La fenêtre Créer un profil d’intégration dans l’interface utilisateur de RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-select.png)

Indiquez ensuite les informations d’identification que vous avez récupérées dans le projet Adobe Developer Portal :

* **Identifiant client**
* **Secret client**
* **Identifiant de compte technique**
* **ID d’organisation**

Une fois les informations d’identification fournies, sélectionnez **[!DNL Save]**.Vous devriez maintenant voir la nouvelle [!DNL Integration Profile] répertorié dans le [!DNL RainFocus] tableau de bord.

Sélectionnez la [!DNL Integration Profile] que vous venez de créer pour voir une liste prédéfinie **types push** déjà configuré. Voici les [Événements d’expérience](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html?lang=fr) qui seront envoyés à l’Experience Platform lorsqu’ils se produisent.

![Liste des types push prédéfinis dans le tableau de bord RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-setup.png)

Pour récupérer une copie de l’exemple de charge utile JSON, sélectionnez **[!DNL Sample JSON Payload]**. Ensuite, mettez en surbrillance et copiez l’exemple de charge utile JSON et **l’enregistrer dans un nouveau fichier avec une extension .json ;**. Il sera utilisé ultérieurement dans Experience Platform pour [configurations de mappage](../../tutorials/ui/create/analytics/rainfocus.md#mapping).

![Exemple de payload JSON dans le tableau de bord RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-json.png)

>[!TIP]
>
>**La configuration n’est pas encore terminée**: Une fois votre flux de données créé, vous devez revenir à la variable [!DNL RainFocus] tableau de bord pour terminer [!DNL Integration Profile] en fournissant votre **URL du point de fin de diffusion** et **identifiant de flux de données**.

## Étapes suivantes

En lisant ce document, vous avez terminé la configuration préalable nécessaire pour diffuser des données à partir de votre [!DNL RainFocus] compte à Experience Platform. Vous pouvez maintenant passer au guide sur [connexion [!DNL RainFocus] Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/analytics/rainfocus.md).