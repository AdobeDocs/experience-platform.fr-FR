---
keywords: airship tags;airship destination
title: Destination des balises d'avion
seo-title: Destination des balises d'avion
description: Transmettez en toute transparence les données d'Audience d'Adobe au navire de transport aérien en tant que balises d'Audience pour le ciblage au sein du navire de transport aérien.
seo-description: Transmettez en toute transparence les données d'Audience d'Adobe au navire de transport aérien en tant que balises d'Audience pour le ciblage au sein du navire de transport aérien.
translation-type: tm+mt
source-git-commit: f08b90531455cdbeb73deb83eed05ba7a9b19df6
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 14%

---


# (bêta) [!DNL Airship Tags] Destination {#airship-tags-destination}

>[!IMPORTANT]
>
>La [!DNL Airship Tags] destination à Adobe Experience Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

## Présentation

[!DNL Airship] est la principale plate-forme d’engagement des clients, qui vous aide à fournir à vos utilisateurs un message personnalisé et significatif à chaque étape du cycle de vie des clients.

Cette intégration transmet les données de segment Adobe Experience Platform en [!DNL Airship] tant que [balises](https://docs.airship.com/guides/audience/tags/) pour le ciblage ou le déclenchement.

Pour en savoir plus [!DNL Airship], consultez les [Aéronefs Docs](https://docs.airship.com).


>[!TIP]
>
>Cette page de documentation a été créée par l&#39; [!DNL Airship] équipe. Pour toute demande de renseignements ou de mise à jour, contactez-les directement à [support.airship.com](https://support.airship.com/).

## Conditions préalables 

Avant de pouvoir envoyer vos segments Adobe Experience Platform à [!DNL Airship]:

* Créez un groupe de balises dans votre [!DNL Airship] projet.
* Générez un jeton porteur pour l’authentification.

>[!TIP]
> 
>Créez un [!DNL Airship] compte via [ce lien](https://go.airship.eu/accounts/register/plan/starter/) d&#39;inscription si ce n&#39;est déjà fait.

### Groupes de balises

Le concept de segments dans Adobe Experience Plateforme est similaire aux [balises](https://docs.airship.com/guides/audience/tags/) dans Airship, avec de légères différences d’implémentation. Cette intégration met en correspondance l’état de l’ [appartenance d’un utilisateur à un segment](https://experienceleague.adobe.com/docs/experience-platform/xdm/mixins/profile/segmentation.html?lang=en#mixins) d’Experience Platform avec la présence ou l’absence d’une [!DNL Airship] balise. Par exemple, dans un segment de plateforme où le `xdm:status` changement est `realized`opéré, la balise est ajoutée au [!DNL Airship] canal ou à l’utilisateur nommé auquel ce profil est associé. Si la balise `xdm:status` est remplacée `exited`, elle est supprimée.

Pour activer cette intégration, créez un groupe *de* balises dans [!DNL Airship] nommé `adobe-segments`.

>[!IMPORTANT]
>
>Lors de la création de votre nouveau groupe de balises, **ne cochez** pas le bouton radio qui indique &quot;[!DNL Allow these tags to be set only from your server]&quot;. Ce faisant, l’intégration des balises d’Adobe échouera.

Voir [Gestion des groupes](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) de balises pour obtenir des instructions sur la création du groupe de balises.

### Jeton de porteur

1. Accédez à **[!UICONTROL Paramètres]** &quot; **[!UICONTROL APIs &amp; Integrations]** dans le tableau de bord [](https://go.airship.com) Airship et sélectionnez **[!UICONTROL Tokens dans le menu de gauche.]**
1. Cliquez sur **[!UICONTROL Créer un jeton]**.
1. Donnez un nom convivial à votre jeton, par exemple &quot;Destination des balises d’Adobe&quot;, puis sélectionnez &quot;Accès complet&quot; pour le rôle.
1. Cliquez sur **[!UICONTROL Créer un jeton]** et enregistrez les détails comme confidentiels.


## Cas d’utilisation

Pour vous aider à mieux comprendre comment et quand utiliser la [!DNL Airship Tags] destination, voici des exemples d&#39;utilisation que les clients Adobe Experience Platform peuvent résoudre en utilisant cette destination.

### Cas d’utilisation 1

Les distributeurs ou plates-formes de divertissement peuvent créer des profils d’utilisateurs pour leurs clients fidèles et les transmettre à des fins [!DNL Airship] de ciblage de messages sur les campagnes mobiles.

### Cas d’utilisation no 2

Déclenchez des messages un à un en temps réel lorsque les utilisateurs entrent dans des segments spécifiques ou en sortent dans Adobe Experience Platform.

Par exemple, un détaillant configure un segment de marque jeans dans Platform. Ce détaillant peut désormais déclencher un message mobile dès que quelqu&#39;un place son jeans à une marque spécifique.

## Se connecter à [!DNL Airship Tags] {#connect-airship-tags}

1. Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, faites défiler l’écran jusqu’à la catégorie Engagement **** Mobile. Sélectionnez **[!DNL Airship Tags]**, puis **[!UICONTROL Configurer]**.

   >[!NOTE]
   >
   >Si une connexion à cette destination existe déjà, un bouton **[!UICONTROL Activer]** s’affiche sur la carte de destination. Pour plus d&#39;informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](/help/rtcdp/destinations/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.

   ![Se connecter aux balises Airship](/help/rtcdp/destinations/assets/airship-tags-in-catalog.png)

2. In the **Account** step, if you had previously set up a connection to your [!DNL Airship Tags] destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to [!DNL Airship Tags]. Sélectionnez **[!UICONTROL Se connecter à la destination]** pour connecter Adobe Experience Platform à votre [!DNL Airship] projet à l’aide du jeton porteur que vous avez généré à partir du [!DNL Airship] tableau de bord.

   >[!NOTE]
   >
   >Adobe Experience Platform supports credentials validation in the authentication process and displays an error message if you input incorrect credentials to your [!DNL Airship] account. Ainsi, vous n’effectuez pas le workflow avec des informations d’identification incorrectes.

   ![Se connecter aux balises Airship](/help/rtcdp/destinations/assets/airshiptags1-connect-account.png)

3. Once your credentials are confirmed and Adobe Experience Platform is connected to your [!DNL Airship] project, you can select **[!UICONTROL Next]** to proceed to the **[!UICONTROL Setup]** step.

4. In the **[!UICONTROL Authentication]** step, enter a **[!UICONTROL Name]** and a **[!UICONTROL Description]** for your activation flow. <br> Cette étape vous permet également de sélectionner le centre de données des États-Unis ou de l&#39;UE, en fonction du centre [!DNL Airship] de données qui s&#39;applique à cette destination. Enfin, sélectionnez un ou plusieurs cas d’utilisation marketing pour lesquels les données seront exportées vers la destination. Vous pouvez choisir parmi les cas d’utilisation marketing définis par l’Adobe ou créer les vôtres. Pour plus d’informations sur les cas d’utilisation marketing, voir la page Gouvernance des [données dans le CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) en temps réel. Pour plus d’informations sur les cas d’utilisation marketing définis par l’Adobe, voir la présentation [des stratégies d’utilisation des](/help/data-governance/policies/overview.md#core-actions)données. <br> Sélectionnez **[!UICONTROL Créer une destination]** après avoir rempli les champs ci-dessus.

   ![Se connecter aux balises Airship](/help/rtcdp/destinations/assets/airshiptags2-select-domain.png)

5. Votre destination est maintenant créée. Vous pouvez sélectionner **[!UICONTROL Enregistrer et quitter]** si vous souhaitez activer les segments ultérieurement. Sélectionnez **[!UICONTROL Suivant]** pour poursuivre le workflow et choisir les segments à activer. In either case, see the next section, [Activate segments](#activate-segments), for the rest of the workflow.

## Activation des segments {#activate-segments}

Pour activer des segments dans [!DNL Airship Tags], procédez comme suit :

1. Dans **[!UICONTROL Destinations > Parcourir]**, sélectionnez la destination vers laquelle vous souhaitez activer vos segments. [!DNL Airship Tags] ![activate-flow](/help/rtcdp/destinations/assets/airship-tags-activate1.png)
2. Cliquez sur le nom de la destination. Vous accédez ainsi au flux d’activation.
Si un flux d’activation existe déjà pour une destination, vous pouvez voir les segments qui sont actuellement envoyés vers la destination. Sélectionnez **[!UICONTROL Modifier l’activation]** dans le rail de droite et suivez les étapes ci-dessous pour modifier les informations sur l’activation.  ![activate-flow](/help/rtcdp/destinations/assets/airship-tags-activate2.png)
3. Sélectionnez **[!UICONTROL Activer]**.
4. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to [!DNL Airship Tags].
   ![segments-to-destination](/help/rtcdp/destinations/assets/airshiptags3-select-segments.png)
5. Dans l’étape **[!UICONTROL Mappage]** , sélectionnez les attributs et les identités du schéma [XDM](https://docs.adobe.com/content/help/fr-FR/experience-platform/xdm/home.html) à mapper au schéma de destination. Sélectionnez **[!UICONTROL Ajouter un nouveau mappage]** pour parcourir votre schéma et le mapper à l’identité de cible correspondante.
   ![écran initial de mappage d&#39;identité](/help/rtcdp/destinations/assets/gcm-identity-mapping.png)
   [!DNL Airship] peuvent être définies soit sur un canal, qui représente l’instance de périphérique, par exemple l’iPhone, soit sur un utilisateur nommé, qui mappe tous les périphériques d’un utilisateur à un identifiant commun, tel qu’un ID de client. Si votre schéma contient des adresses électroniques en texte brut (non hachées) en tant qu’identité Principale, sélectionnez le champ d’adresse électronique dans vos attributs **** source et faites correspondre à l’ [!DNL Airship] utilisateur nommé dans la colonne de droite sous Identités **[!UICONTROL de]**Cible, comme illustré ci-dessous.
   ![Mappage](/help/rtcdp/destinations/assets/airshiptags7-mappingoption2.png)utilisateur nommé Pour les identifiants qui doivent être mappés à un canal, c’est-à-dire à un périphérique, mapper sur le canal approprié en fonction de la source. Les illustrations suivantes montrent comment mapper un identifiant Google Advertising ID à un canal [!DNL Airship] Android.
   ![Se connecter aux balises Airship](/help/rtcdp/destinations/assets/airshiptags4-select-source-identity.png)
   ![Se connecter aux balises Airship](/help/rtcdp/destinations/assets/airshiptags5-select-target-identity.png)
   ![Mappage des canaux](/help/rtcdp/destinations/assets/airshiptags6-mappingoption1.png)

6. Sur la page de planification **[!UICONTROL des]** segments, la planification est actuellement désactivée. Cliquez sur **[!UICONTROL Suivant]** pour passer à l’étape de révision.
7. Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

>[!IMPORTANT]
>
>Au cours de cette étape, Adobe Experience Platform recherche les violations de stratégie d’utilisation des données. Vous trouverez ci-dessous un exemple de violation d’une stratégie. Vous ne pouvez pas terminer le processus d’activation de segments tant que vous n’avez pas résolu la violation. Pour plus d’informations sur la manière de résoudre les violations de stratégie, voir Application [de la](/help/rtcdp/privacy/data-governance-overview.md#enforcement) stratégie dans la section de documentation sur la gouvernance des données.

![confirm-selection](/help/rtcdp/destinations/assets/data-policy-violation.png)

Si aucune violation de stratégie n&#39;a été détectée, sélectionnez **[!UICONTROL Terminer]** pour confirmer votre sélection et début d&#39;envoi des données vers la destination.

![confirm-selection](/help/rtcdp/destinations/assets/Airship-tags-review.png)


## Utilisation des données et gouvernance {#data-usage-governance}

Toutes les destinations [!DNL Adobe Experience Platform] sont conformes aux règles d’utilisation des données lors de la gestion de vos données. Pour obtenir des informations détaillées sur la manière d’ [!DNL Adobe Experience Platform] appliquer la gouvernance des données, voir [Data Governance dans le CDP](/help/rtcdp/privacy/data-governance-overview.md)en temps réel.

