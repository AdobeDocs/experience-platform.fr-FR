---
keywords: airship attributes;airship destination
title: Destination des attributs du navire
seo-title: Destination des attributs du navire
description: Transmettre en toute transparence les données d'Audience d'Adobe au navire de transport aérien en tant qu'attributs d'Audience pour le ciblage au sein du navire de transport aérien.
seo-description: Transmettre en toute transparence les données d'Audience d'Adobe au navire de transport aérien en tant qu'attributs d'Audience pour le ciblage au sein du navire de transport aérien.
translation-type: tm+mt
source-git-commit: 24c8dd0f01d7ea14b2fa5827722e797bd209f50c
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 13%

---


# (bêta) [!DNL Airship Attributes] destination {#airship-attributes-destination}

>[!IMPORTANT]
>
>La [!DNL Airship Attributes] destination à Adobe Experience Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

## Présentation {#overview}

[!DNL Airship] est la principale plate-forme d’engagement des clients, qui vous aide à fournir à vos utilisateurs un message personnalisé et significatif à chaque étape du cycle de vie des clients.

Cette intégration transmet les données de profil d’Adobe en [!DNL Airship] tant qu’ [attributs](https://docs.airship.com/guides/audience/attributes/) pour le ciblage ou le déclenchement.

Pour en savoir plus [!DNL Airship], consultez les [Aéronefs Docs](https://docs.airship.com).


>[!TIP]
>
>Cette page de documentation a été créée par l&#39; [!DNL Airship] équipe. Pour toute demande de renseignements ou de mise à jour, contactez-les directement à [support.airship.com](https://support.airship.com/).

## Conditions préalables  {#prerequisites}

Avant d’envoyer vos segments d’audience à [!DNL Airship], vous devez :

* Activez les attributs dans votre [!DNL Airship] projet.
* Générez un jeton porteur pour l’authentification.

>[!TIP]
>
>Créez un [!DNL Airship] compte via [ce lien](https://go.airship.eu/accounts/register/plan/starter/) d&#39;inscription si ce n&#39;est déjà fait.

### Activer les attributs {#enable-attributes}

Les attributs de profil Adobe Experience Platform sont similaires aux [!DNL Airship] attributs et peuvent être facilement mappés les uns aux autres dans la plate-forme à l&#39;aide de l&#39;outil de mappage présenté plus loin sur cette page.

[!DNL Airship] les projets comportent plusieurs attributs prédéfinis et par défaut. Si vous avez un attribut personnalisé, vous devez le définir en [!DNL Airship] premier. Voir [Configuration et gestion des attributs](https://docs.airship.com/tutorials/audience/attributes/) pour plus d’informations.

### Jeton de porteur {#bearer-token}

Accédez à **[!UICONTROL Paramètres]** &quot; **[!UICONTROL APIs &amp; Integrations]** dans le tableau de bord [](https://go.airship.com) Airship et sélectionnez **[!UICONTROL Tokens dans le menu de gauche.]**

Cliquez sur **[!UICONTROL Créer un jeton]**.

Attribuez un nom convivial à votre jeton, par exemple &quot;Destination des attributs d’Adobe&quot;, puis sélectionnez &quot;Accès complet&quot; pour le rôle.

Cliquez sur **[!UICONTROL Créer un jeton]** et enregistrez les détails comme confidentiels.

## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et quand utiliser la [!DNL Airship Attributes] destination, voici des exemples d&#39;utilisation que les clients Adobe Experience Platform peuvent résoudre en utilisant cette destination.

### Cas d’utilisation 1

Tirez parti des données de profil collectées dans Adobe Experience Platform pour personnaliser le message et le contenu enrichi dans n&#39;importe quel canal [!DNL Airship]de. Par exemple, exploitez les données [!DNL Experience Platform] du profil pour définir les attributs d’emplacement dans [!DNL Airship]. Cela permet à une marque d&#39;hôtel d&#39;afficher une image de l&#39;emplacement d&#39;hôtel le plus proche pour chaque utilisateur.

### Cas d’utilisation no 2

Tirez parti des attributs de Adobe Experience Platform pour enrichir davantage [!DNL Airship] les profils et les combiner à des données de SDK ou [!DNL Airship] prédictives. Par exemple, un détaillant peut créer un segment avec le statut de fidélité et les données d’emplacement (attributs de la plateforme) et prédire qu’ [!DNL Airship] il générera des données pour envoyer des messages très ciblés aux utilisateurs ayant le statut de fidélité à l’or qui vivent à Las Vegas, NV, et qui ont une forte probabilité de déclenchement.

## Se connecter à [!DNL Airship Attributes] {#connect-airship-attributes}

Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, faites défiler l’écran jusqu’à la catégorie Engagement **** Mobile. Sélectionnez **[!DNL Airship Attributes]**, puis **[!UICONTROL Configurer]**.

>[!NOTE]
>
>Si une connexion à cette destination existe déjà, un bouton **[!UICONTROL Activer]** s’affiche sur la carte de destination. Pour plus d&#39;informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](../../ui/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.

![Se connecter aux attributs du navire](../../assets/catalog/mobile-engagement/airship/catalog.png)

In the **Account** step, if you had previously set up a connection to your [!DNL Airship Attributes] destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to [!DNL Airship Attributes]. Sélectionnez **[!UICONTROL Se connecter à la destination]** pour connecter Adobe Experience Platform à votre [!DNL Airship] projet à l’aide du jeton porteur que vous avez généré à partir du [!DNL Airship] tableau de bord.

>[!NOTE]
>
>Adobe Experience Platform supports credentials validation in the authentication process and displays an error message if you input incorrect credentials to your [!DNL Airship] account. Ainsi, vous n’effectuez pas le workflow avec des informations d’identification incorrectes.

![Se connecter aux attributs du navire](../../assets/catalog/mobile-engagement/airship/connect.png)

Once your credentials are confirmed and Adobe Experience Platform is connected to your [!DNL Airship] project, you can select **[!UICONTROL Next]** to proceed to the **[!UICONTROL Setup]** step.

In the **[!UICONTROL Authentication]** step, enter a **[!UICONTROL Name]** and a **[!UICONTROL Description]** for your activation flow.

Cette étape vous permet également de sélectionner le centre de données des États-Unis ou de l&#39;UE, en fonction du centre [!DNL Airship] de données qui s&#39;applique à cette destination. Enfin, sélectionnez un ou plusieurs cas d’utilisation marketing pour lesquels les données seront exportées vers la destination. Vous pouvez choisir parmi les cas d’utilisation marketing définis par l’Adobe ou créer les vôtres. Pour plus d’informations sur les cas d’utilisation marketing, voir la page Gouvernance des [données dans le CDP](../../../rtcdp/privacy/data-governance-overview.md#destinations) en temps réel. Pour plus d’informations sur les cas d’utilisation marketing définis par l’Adobe, voir la présentation [des stratégies d’utilisation des](../../../data-governance/policies/overview.md#core-actions)données.

Select **[!UICONTROL Create Destination]** after you have filled in the fields above.

![Se connecter aux attributs du navire](../../assets/catalog/mobile-engagement/airship/select-domain.png)

Votre destination est maintenant créée. Vous pouvez sélectionner **[!UICONTROL Enregistrer et quitter]** si vous souhaitez activer les segments ultérieurement. Sélectionnez **[!UICONTROL Suivant]** pour poursuivre le workflow et choisir les segments à activer. In either case, see the next section, [Activate segments](#activate-segments), for the rest of the workflow.

## Activation des segments {#activate-segments}

Pour activer des segments dans [!DNL Airship Attributes], procédez comme suit :

Dans **[!UICONTROL Destinations > Parcourir]**, sélectionnez la destination vers laquelle vous souhaitez activer vos segments.[!DNL Airship Attributes]

![activate-flow](../../assets/catalog/mobile-engagement/airship/browse.png)

Cliquez sur le nom de la destination. Vous accédez ainsi au flux d’activation.

Si un flux d’activation existe déjà pour une destination, vous pouvez voir les segments qui sont actuellement envoyés vers la destination. Sélectionnez **[!UICONTROL Modifier l’activation]** dans le rail de droite et suivez les étapes ci-dessous pour modifier les informations sur l’activation.

![activate-flow](../../assets/catalog/mobile-engagement/airship/activate.png)

Select **[!UICONTROL Activate]**. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to [!DNL Airship Attributes].

![segments-to-destination](../../assets/catalog/mobile-engagement/airship/select-segments.png)

Dans l’étape **[!UICONTROL Mappage]** , sélectionnez les attributs et les identités du schéma [XDM](../../../xdm/home.md) à mapper au schéma de destination. Sélectionnez **[!UICONTROL Ajouter un nouveau mappage]** pour parcourir votre schéma et le mapper à l’identité de cible correspondante.

![écran initial de mappage d&#39;identité](../../assets/catalog/mobile-engagement/airship/identity-mapping.png)

[!DNL Airship] les attributs peuvent être définis soit sur un canal, qui représente l’instance de périphérique, par exemple l’iPhone, soit sur un utilisateur nommé, qui mappe tous les périphériques d’un utilisateur à un identifiant commun, tel qu’un ID de client. Si votre schéma contient des adresses électroniques en texte brut (non hachées) en tant qu’identité Principale, sélectionnez le champ d’adresse électronique dans vos attributs **** source et faites correspondre à l’ [!DNL Airship] utilisateur nommé dans la colonne de droite sous Identités **[!UICONTROL de]** Cible, comme illustré ci-dessous.

![Mappage des utilisateurs nommés](../../assets/catalog/mobile-engagement/airship/mapping.png)

Pour les identifiants qui doivent être mappés à un canal, c’est-à-dire un périphérique, faites correspondre le canal approprié en fonction de la source. Les images suivantes montrent comment deux mappages sont créés :

* ID de publicité iOS IDFA sur un canal [!DNL Airship] iOS
* Attribut Adobe `fullName` à l’attribut [!DNL Airship] &quot;Nom complet&quot;

>[!NOTE]
>
>Utilisez le nom convivial qui s’affiche dans le [!DNL Airship] tableau de bord lorsque vous sélectionnez le champ de cible pour votre mappage d’attributs.

**Identité de mappage**

Sélectionner le champ source :

![Se connecter aux attributs du navire](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Sélectionner un champ de cible :

![Se connecter aux attributs du navire](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**Attribut de carte**

Sélectionner l&#39;attribut source :

![Sélectionner le champ source](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Sélectionner un attribut de cible :

![Sélectionner un champ de cible](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Vérifier le mappage :

![Mappage de canal](../../assets/catalog/mobile-engagement/airship/mapping.png)

Sur la page de planification **[!UICONTROL des]** segments, la planification est actuellement désactivée. Cliquez sur **[!UICONTROL Suivant]** pour passer à l’étape de révision.

![Planification actuellement désactivée](../../assets/catalog/mobile-engagement/airship/scheduling.png)

Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

>[!IMPORTANT]
>
>Au cours de cette étape, Adobe Experience Platform recherche les violations de stratégie d’utilisation des données. Vous trouverez ci-dessous un exemple de violation d’une stratégie. Vous ne pouvez pas terminer le processus d’activation de segments tant que vous n’avez pas résolu la violation. Pour plus d’informations sur la manière de résoudre les violations de stratégie, voir Application [de la](../../../rtcdp/privacy/data-governance-overview.md#enforcement) stratégie dans la section de documentation sur la gouvernance des données.

![confirm-selection](../../assets/common/data-policy-violation.png)

Si aucune violation de stratégie n&#39;a été détectée, sélectionnez **[!UICONTROL Terminer]** pour confirmer votre sélection et début d&#39;envoi des données vers la destination.

![examiner](../../assets/catalog/mobile-engagement/airship/review.png)

## Utilisation des données et gouvernance {#data-usage-governance}

Toutes les destinations [!DNL Adobe Experience Platform] sont conformes aux règles d’utilisation des données lors de la gestion de vos données. Pour obtenir des informations détaillées sur la manière d’ [!DNL Adobe Experience Platform] appliquer la gouvernance des données, voir [Data Governance dans le CDP](../../../rtcdp/privacy/data-governance-overview.md)en temps réel.
