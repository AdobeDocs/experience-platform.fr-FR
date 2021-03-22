---
keywords: balises d'avion ; destination du navire
title: Connexion aux balises d'avion
description: Transmettez en toute transparence les données d'Audience d'Adobe au navire de transport aérien en tant que balises d'Audience pour le ciblage au sein du navire de transport aérien.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 13%

---


# (Bêta) [!DNL Airship Tags] connexion {#airship-tags-destination}

>[!IMPORTANT]
>
>La destination [!DNL Airship Tags] de Adobe Experience Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

## Présentation

[!DNL Airship] est la principale plate-forme d’engagement des clients, qui vous aide à fournir à vos utilisateurs un message personnalisé et significatif à chaque étape du cycle de vie des clients.

Cette intégration transmet les données de segment Adobe Experience Platform dans [!DNL Airship] en tant que [balises](https://docs.airship.com/guides/audience/tags/) pour le ciblage ou le déclenchement.

Pour en savoir plus sur [!DNL Airship], consultez les [Aéronefs Docs](https://docs.airship.com).


>[!TIP]
>
>Cette page de documentation a été créée par l&#39;équipe [!DNL Airship]. Pour toute demande de renseignements ou de mise à jour, contactez-les directement à [support.airship.com](https://support.airship.com/).

## Conditions préalables

Avant de pouvoir envoyer vos segments Adobe Experience Platform à [!DNL Airship], vous devez :

* Créez un groupe de balises dans votre projet [!DNL Airship].
* Générez un jeton porteur pour l’authentification.

>[!TIP]
> 
>Créez un compte [!DNL Airship] via [ce lien d&#39;inscription](https://go.airship.eu/accounts/register/plan/starter/) si vous n&#39;en avez pas déjà créé.

## Groupes de balises

Le concept de segments dans Adobe Experience Platorm est similaire à [Balises](https://docs.airship.com/guides/audience/tags/) dans Airship, avec de légères différences d’implémentation. Cette intégration mappe l’état de l’appartenance [d’un utilisateur à un segment d’Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/xdm/mixins/profile/segmentation.html?lang=en#mixins) à la présence ou à l’absence d’une balise [!DNL Airship]. Par exemple, dans un segment de plateforme où `xdm:status` devient `realized`, la balise est ajoutée au canal [!DNL Airship] ou est nommée utilisateur auquel ce profil est associé. Si `xdm:status` devient `exited`, la balise est supprimée.

Pour activer cette intégration, créez un *groupe de balises* dans [!DNL Airship] nommé `adobe-segments`.

>[!IMPORTANT]
>
>Lors de la création de votre nouveau groupe de balises **Ne cochez pas** le bouton radio qui indique &quot;[!DNL Allow these tags to be set only from your server]&quot;. Ce faisant, l’intégration des balises d’Adobe échouera.

Voir [Gérer les groupes de balises](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) pour obtenir des instructions sur la création du groupe de balises.

## Générer un jeton porteur

Accédez à **[!UICONTROL Paramètres]**&quot; **[!UICONTROL APIs &amp; Integrations]** dans le [tableau de bord Airship](https://go.airship.com) et sélectionnez **[!UICONTROL Tokens]** dans le menu de gauche.

Cliquez sur **[!UICONTROL Créer un jeton]**.

Donnez un nom convivial à votre jeton, par exemple &quot;Destination des balises d’Adobe&quot;, puis sélectionnez &quot;Accès complet&quot; pour le rôle.

Cliquez sur **[!UICONTROL Créer un jeton]** et enregistrez les détails comme confidentiels.

## Cas d’utilisation

Pour vous aider à mieux comprendre comment et quand utiliser la destination [!DNL Airship Tags], voici des exemples de cas d&#39;utilisation que les clients Adobe Experience Platform peuvent résoudre en utilisant cette destination.

### Cas d’utilisation 1

Les détaillants ou plates-formes de divertissement peuvent créer des profils d’utilisateurs sur leurs clients fidèles et les transmettre dans [!DNL Airship] pour le ciblage des messages sur les campagnes mobiles.

### Cas d’utilisation no 2

Déclenchez des messages un à un en temps réel lorsque les utilisateurs entrent dans des segments spécifiques ou en sortent dans Adobe Experience Platform.

Par exemple, un détaillant configure un segment de marque jeans dans Platform. Ce détaillant peut désormais déclencher un message mobile dès que quelqu&#39;un place son jeans à une marque spécifique.

## Se connecter à [!DNL Airship Tags] {#connect-airship-tags}

Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, faites défiler la catégorie **[!UICONTROL Mobile Engagement]**. Sélectionnez **[!DNL Airship Tags]**, puis **[!UICONTROL Configurer]**.

>[!NOTE]
>
>Si une connexion avec cette destination existe déjà, vous pouvez voir un bouton **[!UICONTROL Activer]** sur la carte de destination. Pour plus d&#39;informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](../../ui/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.

![Se connecter aux balises Airship](../../assets/catalog/mobile-engagement/airship-tags/catalog.png)

À l&#39;étape **Compte**, si vous aviez précédemment configuré une connexion à votre destination [!DNL Airship Tags], sélectionnez **[!UICONTROL Compte existant]** et sélectionnez votre connexion existante. Vous pouvez également sélectionner **[!UICONTROL Nouveau compte]** pour configurer une nouvelle connexion à [!DNL Airship Tags]. Sélectionnez **[!UICONTROL Se connecter à destination]** pour connecter Adobe Experience Platform à votre projet [!DNL Airship] à l’aide du jeton porteur que vous avez généré à partir du tableau de bord [!DNL Airship].

>[!NOTE]
>
>Adobe Experience Platform prend en charge la validation des informations d’identification dans le processus d’authentification et affiche un message d’erreur si vous saisissez des informations d’identification incorrectes dans votre compte [!DNL Airship]. Ainsi, vous n’effectuez pas le workflow avec des informations d’identification incorrectes.

![Se connecter aux balises Airship](../../assets/catalog/mobile-engagement/airship-tags/connect-account.png)

Une fois vos informations d’identification confirmées et que Adobe Experience Platform est connecté à votre projet [!DNL Airship], vous pouvez sélectionner **[!UICONTROL Suivant]** pour passer à l’étape **[!UICONTROL Configuration]**.

À l&#39;étape **[!UICONTROL Authentification]**, entrez **[!UICONTROL Nom]** et **[!UICONTROL Description]** pour votre flux d&#39;activation.

Cette étape vous permet également de sélectionner le centre de données des États-Unis ou de l&#39;Union européenne, en fonction du centre de données [!DNL Airship] qui s&#39;applique à cette destination. Enfin, sélectionnez une ou plusieurs **[!UICONTROL actions marketing]** pour lesquelles les données seront exportées vers la destination. Vous pouvez choisir parmi des actions marketing définies par Adobe ou créer les vôtres. Pour plus d&#39;informations sur les actions marketing, consultez la [Présentation des stratégies d&#39;utilisation des données](../../../data-governance/policies/overview.md).

Sélectionnez **[!UICONTROL Créer une destination]** après avoir rempli les champs ci-dessus.

![Se connecter aux balises Airship](../../assets/catalog/mobile-engagement/airship-tags/select-domain.png)

Votre destination est maintenant créée. Vous pouvez sélectionner **[!UICONTROL Enregistrer et quitter]** si vous souhaitez activer les segments ultérieurement. Sélectionnez **[!UICONTROL Suivant]** pour poursuivre le workflow et choisir les segments à activer. Dans les deux cas, consultez la section suivante, [Activer les segments](#activate-segments), pour le reste du flux de travail.

## Activation des segments {#activate-segments}

Pour activer des segments dans [!DNL Airship Tags], procédez comme suit :

Dans **[!UICONTROL Destinations > Parcourir]**, sélectionnez la destination vers laquelle vous souhaitez activer vos segments.[!DNL Airship Tags]

![activate-flow](../../assets/catalog/mobile-engagement/airship-tags/browse.png)

Cliquez sur le nom de la destination. Vous accédez ainsi au flux d’activation.

Si un flux d’activation existe déjà pour une destination, vous pouvez voir les segments qui sont actuellement envoyés vers la destination. Sélectionnez **[!UICONTROL Modifier l’activation]** dans le rail de droite et suivez les étapes ci-dessous pour modifier les informations sur l’activation.

![activate-flow](../../assets/catalog/mobile-engagement/airship-tags/activate.png)

Sélectionnez **[!UICONTROL Activer]**. Dans le flux de travaux **[!UICONTROL Activer la destination]**, sur la page **[!UICONTROL Sélectionner des segments]**, sélectionnez les segments à envoyer à [!DNL Airship Tags].

![segments-to-destination](../../assets/catalog/mobile-engagement/airship-tags/select-segments.png)

À l’étape **[!UICONTROL Mappage]**, sélectionnez les attributs et les identités du schéma [XDM](../../../xdm/home.md) à mapper au schéma de destination. Sélectionnez **[!UICONTROL Ajouter un nouveau mappage]** pour parcourir votre schéma et le mapper à l’identité de cible correspondante.

![écran initial de mappage d&#39;identité](../../assets/catalog/mobile-engagement/airship-tags/identity-mapping.png)

[!DNL Airship] peuvent être définies soit sur un canal, qui représente l’instance de périphérique, par exemple l’iPhone, soit sur un utilisateur nommé, qui mappe tous les périphériques d’un utilisateur à un identifiant commun, tel qu’un ID de client. Si votre schéma contient des adresses électroniques en texte brut (non hachées) en tant qu’identité Principale, sélectionnez le champ d’adresse électronique dans vos **[!UICONTROL Attributs source]** et faites correspondre l’utilisateur [!DNL Airship] nommé dans la colonne de droite sous **[!UICONTROL Identités de Cible]**, comme illustré ci-dessous.

![Mappage des utilisateurs nommés](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Pour les identifiants qui doivent être mappés à un canal, c’est-à-dire un périphérique, faites correspondre le canal approprié en fonction de la source. Les illustrations suivantes montrent comment mapper un identifiant Google Advertising ID à un canal Android [!DNL Airship].

![Se connecter aux ](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![balises AirshipSe connecter aux ](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![balises AirshipMappage des canaux](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

Sur la page **[!UICONTROL Planification des segments]**, la planification est actuellement désactivée. Cliquez sur **[!UICONTROL Suivant]** pour passer à l’étape de révision.

Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer les données à la destination.

>[!IMPORTANT]
>
>Au cours de cette étape, Adobe Experience Platform recherche les violations de stratégie d’utilisation des données. Vous trouverez ci-dessous un exemple de violation d’une stratégie. Vous ne pouvez pas terminer le processus d’activation de segments tant que vous n’avez pas résolu la violation. Pour plus d&#39;informations sur la manière de résoudre les violations de stratégie, voir [Application de la stratégie](../../../data-governance/enforcement/auto-enforcement.md) dans la section de documentation sur la gouvernance des données.

![confirm-selection](../../assets/common/data-policy-violation.png)

Si aucune violation de stratégie n&#39;a été détectée, sélectionnez **[!UICONTROL Terminer]** pour confirmer votre sélection et l&#39;envoi de données par début vers la destination.

![confirmation-sélection](../../assets/catalog/mobile-engagement/airship-tags/review.png)


## Utilisation des données et gouvernance {#data-usage-governance}

Toutes les destinations [!DNL Adobe Experience Platform] sont conformes aux règles d&#39;utilisation des données lors de la gestion de vos données. Pour obtenir des informations détaillées sur la façon dont [!DNL Adobe Experience Platform] applique la gouvernance des données, voir [Présentation de la gouvernance des données](../../../data-governance/home.md).

