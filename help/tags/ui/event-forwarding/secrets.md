---
title: Configuration de secrets dans le transfert d’événements
description: Découvrez comment configurer des secrets dans lʼinterface utilisateur afin de vous authentifier aux points dʼentrée utilisés dans les propriétés de transfert dʼévénement.
exl-id: eefd87d7-457f-422a-b159-5b428da54189
source-git-commit: a863d65c3e6e330254a58aa822383c0847b0e5f5
workflow-type: tm+mt
source-wordcount: '2182'
ht-degree: 85%

---

# Configuration de secrets dans le transfert d’événements

Dans le transfert dʼévénement, un secret est une ressource qui représente des informations dʼidentification pour sʼauthentifier auprès dʼun autre système, ce qui permet lʼéchange sécurisé de données. Les secrets ne peuvent être créés que dans les propriétés de transfert dʼévénement.

Les types de secret suivants sont actuellement pris en charge :

| Type de secret | Description |
| --- | --- |
| [!UICONTROL Google OAuth 2] | Contient plusieurs attributs pour prendre en charge la spécification d’authentification [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) pour une utilisation dans l’[API Google Ads](https://developers.google.com/google-ads/api/docs/oauth/overview) et l’[API Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview). Le système vous demande les informations requises, puis gère le renouvellement de ces jetons pour vous à un intervalle spécifié. |
| [!UICONTROL HTTP] | Contient deux attributs de chaîne pour un nom dʼutilisateur et un mot de passe, respectivement. |
| [!UICONTROL OAuth 2] | Contient plusieurs attributs pour prendre en charge le [type d’octroi des informations d’identification du client](https://datatracker.ietf.org/doc/html/rfc6749#section-1.3.4) pour la spécification d’authentification [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749). Le système vous demande les informations requises, puis gère le renouvellement de ces jetons pour vous à un intervalle spécifié. |
| [!UICONTROL JWT OAuth 2] | Contient plusieurs attributs pour la prise en charge du profil JSON Web Token (JWT) pour [Autorisation OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc7523#section-2.1) subventions. Le système vous demande les informations requises, puis gère le renouvellement de ces jetons pour vous à un intervalle spécifié. |
| [!UICONTROL Jeton] | Chaîne unique de caractères représentant une valeur de jeton dʼauthentification connue et comprise par les deux systèmes. |

{style="table-layout:auto"}

Ce guide fournit une présentation générale de la configuration des secrets pour une propriété de transfert dʼévénement ([!UICONTROL Edge]) dans lʼinterface utilisateur d’Experience Platform ou l’interface utilisateur de la collecte de données.

>[!NOTE]
>
>Pour obtenir des instructions détaillées sur la gestion des secrets dans lʼAPI Reactor, notamment un exemple JSON de la structure dʼun secret, reportez-vous au [guide de lʼAPI Secrets](../../api/guides/secrets.md).

## Conditions préalables

Avant dʼutiliser ce guide, assurez-vous au préalable de savoir comment gérer les ressources pour les balises et le transfert dʼévénement dans lʼinterface utilisateur, y compris comment créer un élément de données et une règle de transfert dʼévénement. Si vous avez besoin dʼune présentation, consultez le guide sur la [gestion des ressources](../managing-resources/overview.md).

Vous devez également posséder une compréhension pratique du flux de publication pour les balises et le transfert dʼévénement, y compris la manière dʼajouter des ressources à une bibliothèque et dʼinstaller une version de celle-ci sur votre site web à des fins de test. Pour plus dʼinformations, voir [présentation de la publication](../publishing/overview.md).

## Créer un secret {#create}

>[!CONTEXTUALHELP]
>id="platform_eventforwarding_secrets_environments"
>title="Environnements pour les secrets"
>abstract="Pour être utilisé par le transfert dʼévénement, un secret doit dʼabord être affecté à un environnement existant. Si aucun environnement n’est créé pour votre propriété de transfert d’événement, vous devez le configurer avant de continuer."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html?lang=fr" text="Présentation des environnements"

Pour créer un secret, sélectionnez **[!UICONTROL Transfert d’événement]** dans la navigation de gauche, puis ouvrez la propriété de transfert d’événement sous laquelle vous souhaitez ajouter le secret. Ensuite, sélectionnez **[!UICONTROL Secrets]** dans le volet de navigation de gauche, puis **[!UICONTROL Créer un secret]**.

![Création dʼun secret](../../images/ui/event-forwarding/secrets/create-new-secret.png)

Lʼécran suivant vous permet de configurer les détails du secret. Pour être utilisé par le transfert dʼévénement, un secret doit dʼabord être affecté à un environnement existant. Si aucun environnement nʼest créé pour votre propriété de transfert dʼévénement, consultez le guide sur les [environnements](../publishing/environments.md) pour obtenir des conseils sur la façon de les configurer avant de poursuivre.

>[!NOTE]
>
>Si vous souhaitez toujours créer et enregistrer le secret avant de lʼajouter à un environnement, désactivez le bouton **[!UICONTROL Affecter le secret aux environnements]** avant de compléter les autres informations. Notez que vous devrez affecter le secret à un environnement par la suite si vous souhaitez lʼutiliser.
>
>![Désactivation de lʼenvironnement](../../images/ui/event-forwarding/secrets/env-disabled.png)

Sous **[!UICONTROL Environnement cible]**, sélectionnez dans le menu déroulant lʼenvironnement auquel vous souhaitez affecter le secret. Sous **[!UICONTROL Nom du secret]**, attribuez un nom au secret dans le contexte de lʼenvironnement. Chaque secret au sein de la propriété de transfert dʼévénement doit posséder un nom unique.

![Environnement et nom](../../images/ui/event-forwarding/secrets/env-and-name.png)

Un secret ne peut être attribué quʼà un environnement à la fois, mais vous pouvez attribuer les mêmes informations dʼidentification à plusieurs secrets au sein de différents environnements si vous le souhaitez. Sélectionnez **[!UICONTROL Ajouter un environnement]** pour ajouter une autre ligne à la liste.

![Ajout dʼun environnement](../../images/ui/event-forwarding/secrets/add-env.png)

Pour chaque environnement ajouté, vous devez attribuer un nouveau nom unique pour le secret associé. Lorsque tous les environnements disponibles ont été sélectionnés, le bouton **[!UICONTROL Ajouter un environnement]** devient indisponible.

![Ajout dʼun environnement indisponible](../../images/ui/event-forwarding/secrets/add-env-greyed.png)

À partir de là, les étapes de création du secret varient en fonction du type de secret que vous souhaitez créer. Consultez les sous-sections ci-dessous pour plus de détails :

* [[!UICONTROL Jeton]](#token)
* [[!UICONTROL HTTP]](#http)
* [[!UICONTROL OAuth 2]](#oauth2)
* [[!UICONTROL JWT OAuth 2]](#oauth2jwt)
* [[!UICONTROL Google OAuth 2]](#google-oauth2)

### [!UICONTROL Jeton] {#token}

Pour créer un secret de jeton, sélectionnez **[!UICONTROL Jeton]** dans la liste déroulante **[!UICONTROL Type]**. Dans le champ **[!UICONTROL Jeton]** qui s’affiche, indiquez la chaîne d’identification reconnue par le système auquel vous vous authentifiez. Sélectionnez **[!UICONTROL Créer un secret]** pour enregistrer le secret.

![Secret du jeton](../../images/ui/event-forwarding/secrets/token-secret.png)

### [!UICONTROL HTTP] {#http}

Pour créer un secret HTTP, sélectionnez **[!UICONTROL HTTP simple]** dans la liste déroulante **[!UICONTROL Type]**. Dans les champs qui s’affichent ci-dessous, indiquez un nom d’utilisateur et un mot de passe pour les informations d’identification avant de sélectionner **[!UICONTROL Créer un secret]** pour enregistrer le secret.

>[!NOTE]
>
>Lors de l’enregistrement, les informations d’identification sont codées à l’aide du [schéma d’authentification HTTP « basique »](https://www.rfc-editor.org/rfc/rfc7617.html).

![Secret HTTP](../../images/ui/event-forwarding/secrets/http-secret.png)

### [!UICONTROL OAuth 2] {#oauth2}

Pour créer un secret OAuth 2, sélectionnez **[!UICONTROL OAuth 2]** dans la liste déroulante **[!UICONTROL Type]**. Dans les champs qui s’affichent en-dessous, fournissez votre [[!UICONTROL Identifiant client] et votre [!UICONTROL Secret client]](https://www.oauth.com/oauth2-servers/client-registration/client-id-secret/), ainsi que votre [[!UICONTROL URL du jeton]](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) pour votre intégration OAuth. Le champ [!UICONTROL URL du jeton] dans l’interface utilisateur est une concaténation entre l’hôte du serveur d’autorisation et le chemin du jeton.

![Secret OAuth 2](../../images/ui/event-forwarding/secrets/oauth-secret-1.png)

Sous **[!UICONTROL Options d’identification]**, vous pouvez fournir d’autres options d’identification telles que `scope` et `audience` sous la forme de paires clé-valeur. Pour ajouter des paires clé-valeur supplémentaires, sélectionnez **[!UICONTROL Ajouter une autre]**.

![Options d’identification](../../images/ui/event-forwarding/secrets/oauth-secret-2.png)

Enfin, vous pouvez configurer la valeur **[!UICONTROL Actualiser le décalage]** pour le secret. Cette valeur représente le nombre de secondes avant l’expiration du jeton pendant lesquelles le système effectue une actualisation automatique. L’équivalent en heures et minutes s’affiche à droite du champ et se met automatiquement à jour au fur et à mesure que vous tapez.

![Actualiser le décalage](../../images/ui/event-forwarding/secrets/oauth-secret-3.png)

Par exemple, si le décalage d’actualisation est défini sur la valeur par défaut de `14400` (quatre heures) et le jeton d’accès comporte une valeur `expires_in` de `86400` (24 heures), le système actualisera automatiquement le secret dans 20 heures.

>[!IMPORTANT]
>
>Un secret OAuth nécessite au moins quatre heures entre les actualisations et doit également être valide pendant au moins huit heures. Cette restriction vous donne un minimum de quatre heures pour intervenir en cas de problème avec le jeton généré.
>
>Par exemple, si le décalage est défini sur `28800` (huit heures) et le jeton d’accès comporte un `expires_in` de `36000` (dix heures), l’échange échouerait, car la différence en résultant serait inférieure à quatre heures.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Créer un secret]** pour enregistrer le secret.

![Enregistrer le décalage OAuth 2](../../images/ui/event-forwarding/secrets/oauth-secret-4.png)

### [!UICONTROL JWT OAuth 2] {#oauth2jwt}

Pour créer un secret JWT OAuth 2, sélectionnez **[!UICONTROL JWT OAuth 2]** de la **[!UICONTROL Type]** menu déroulant.

![Le [!UICONTROL Créer un secret] avec le secret JWT OAuth 2 mis en surbrillance dans l’onglet [!UICONTROL Type] menu déroulant.](../../images/ui/event-forwarding/secrets/oauth-jwt-secret.png)

>[!NOTE]
>
>La seule [!UICONTROL Algorithme] qui est actuellement pris en charge pour la signature du JWT est RS256.

Dans les champs qui s’affichent ci-dessous, fournissez vos [!UICONTROL Émetteur], [!UICONTROL Objet], [!UICONTROL Audience], [!UICONTROL Demandes personnalisées], [!UICONTROL TTL], puis sélectionnez la variable [!UICONTROL Algorithme] dans la liste déroulante. Ensuite, saisissez le [!UICONTROL Id De Clé Privée], ainsi que vos [[!UICONTROL URL du jeton]](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) pour votre intégration OAuth. Le [!UICONTROL URL du jeton] n’est pas un champ obligatoire. Si une valeur est fournie, le jeton JWT est échangé avec un jeton d’accès. Le secret sera actualisé en fonction de la variable `expires_in` de la réponse et de la variable [!UICONTROL Actualiser le décalage] . Si aucune valeur n’est fournie, le secret envoyé au bord est le JWT. Le jeton JWT sera actualisé en fonction de la variable [!UICONTROL TTL] et [!UICONTROL Actualiser le décalage] valeurs.

![Le [!UICONTROL Créer un secret] avec une sélection de champs de saisie en surbrillance.](../../images/ui/event-forwarding/secrets/oauth-jwt-information.png)

Sous **[!UICONTROL Options d’identification]**, vous pouvez fournir d’autres options d’identification, telles que `jwt_param` sous la forme de paires clé-valeur. Pour ajouter des paires clé-valeur supplémentaires, sélectionnez **[!UICONTROL Ajouter une autre]**.

![Le [!UICONTROL Créer un secret] mise en surbrillance de l’onglet [!UICONTROL Options d’identification] champs.](../../images/ui/event-forwarding/secrets/oauth-jwt-credential-options.png)

Enfin, vous pouvez configurer la valeur **[!UICONTROL Actualiser le décalage]** pour le secret. Cette valeur représente le nombre de secondes avant l’expiration du jeton pendant lesquelles le système effectue une actualisation automatique. L’équivalent en heures et minutes s’affiche à droite du champ et se met automatiquement à jour au fur et à mesure que vous tapez.

![Le [!UICONTROL Créer un secret] mise en surbrillance de l’onglet [!UICONTROL Actualiser le décalage] champ .](../../images/ui/event-forwarding/secrets/oauth-jwt-refresh-offset.png)

Par exemple, si le décalage d’actualisation est défini sur la valeur par défaut de `1800` (30 minutes) et le jeton d’accès comporte une `expires_in` valeur de `3600` (une heure), le système actualise automatiquement le secret en une heure.

>[!IMPORTANT]
>
>Un secret JWT OAuth 2 nécessite au moins 30 minutes entre les actualisations et doit également être valide pendant au moins une heure. Cette restriction vous donne un minimum de 30 minutes pour intervenir en cas de problème avec le jeton généré.
>
>Par exemple, si le décalage est défini sur `1800` (30 minutes) et le jeton d’accès comporte une `expires_in` de `2700` (45 minutes), l’échange échouerait, car la différence résultante serait inférieure à 30 minutes.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Créer un secret]** pour enregistrer le secret.

![Le [!UICONTROL Créer un secret] mise en surbrillance des onglets [!UICONTROL Créer un secret]](../../images/ui/event-forwarding/secrets/oauth-jwt-create-secret.png)

### [!UICONTROL Google OAuth 2] {#google-oauth2}

Pour créer un secret Google OAuth 2, sélectionnez **[!UICONTROL Google OAuth 2]** dans la liste déroulante **[!UICONTROL Type]**. Sous **[!UICONTROL Portées]**, sélectionnez les API Google auxquelles vous souhaitez accorder l’accès à l’aide de ce secret. Les produits suivants sont actuellement pris en charge :

* [API Google Ads](https://developers.google.com/google-ads/api/docs/oauth/overview)
* [API Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Créer un secret]**.

![Secret Google OAuth 2](../../images/ui/event-forwarding/secrets/google-oauth.png)

Une fenêtre contextuelle s’affiche pour vous informer que le secret doit être autorisé manuellement via Google. Sélectionnez **[!UICONTROL Créer et autoriser]** pour continuer.

![Fenêtre contextuelle d’autorisation Google](../../images/ui/event-forwarding/secrets/google-authorization.png)

Une boîte de dialogue s’affiche et vous permet de saisir les informations d’identification de votre compte Google. Suivez les invites pour accorder l’accès au transfert d’événement à vos données sous la portée sélectionnée. Une fois le processus d’autorisation terminé, le secret est créé.

>[!IMPORTANT]
>
>Si votre organisation a défini une politique de réauthentification pour les applications Google Cloud, les secrets créés ne seront pas actualisés avec succès après l’expiration de l’authentification (entre 1 et 24 heures selon la configuration de la politique).
>
>Pour résoudre ce problème, connectez-vous à l’Admin Console Google et accédez à la page **[!DNL App access control]** afin de marquer l’application de transfert d’événement (Adobe Real-Time CDP Event Forwarding) comme [!DNL Trusted]. Reportez-vous à la documentation Google sur comment [définir des durées de session pour les services Google Cloud](https://support.google.com/a/answer/9368756) pour plus d’informations.

## Modifier un secret

Une fois que vous avez créé des secrets pour une propriété, vous pouvez les trouver dans l’espace de travail **[!UICONTROL Secrets]**. Pour modifier les détails d’un secret existant, sélectionnez son nom dans la liste.

![Sélectionner le secret à modifier](../../images/ui/event-forwarding/secrets/edit-secret.png)

L’écran suivant vous permet de modifier le nom et les informations d’identification du secret.

![Modifier un secret](../../images/ui/event-forwarding/secrets/edit-secret-config.png)

>[!NOTE]
>
>Si le secret est associé à un environnement existant, vous ne pouvez pas le réaffecter à un autre environnement. Si vous souhaitez utiliser les mêmes informations d’identification dans un environnement différent, vous devez [créer un nouveau secret](#create). Pour pouvoir réaffecter l’environnement de cet écran, il faut qu’il n’ait jamais préalablement été attribué à un environnement, ou que vous supprimiez l’environnement auquel le secret était attaché.

### Réessayer un échange secret

Vous pouvez réessayer ou actualiser un échange secret depuis l’écran d’édition. Ce processus varie en fonction du type de secret en cours de modification :

| Type de secret | Protocole de nouvel essai |
| --- | --- |
| [!UICONTROL Jeton] | Sélectionnez **[!UICONTROL Échange secret]** pour réessayer l’échange secret. Cette commande n’est disponible que lorsqu’un environnement est attaché au secret. |
| [!UICONTROL HTTP] | Si aucun environnement n’est associé au secret, sélectionnez **[!UICONTROL Échange secret]** afin d’échanger les informations d’identification vers base64. Si un environnement est joint, sélectionnez **[!UICONTROL Échanger et déployer le secret]** pour passer en base64 et déployer le secret. |
| [!UICONTROL OAuth 2] | Sélectionnez **[!UICONTROL Générer un jeton]** pour échanger les informations d’identification et renvoyer un jeton d’accès du fournisseur d’authentification. |

## Supprimer un secret

Pour supprimer un secret existant dans l’espace de travail **[!UICONTROL Secrets]**, cochez la case en regard de son nom avant de sélectionner **[!UICONTROL Supprimer]**.

![Supprimer un secret](../../images/ui/event-forwarding/secrets/delete.png)

## Utilisation de secrets dans le transfert d’événements

Pour utiliser un secret dans le transfert d’événements, vous devez d’abord créer un [élément de données](../managing-resources/data-elements.md) qui fait référence au secret lui-même. Après avoir enregistré l’élément de données, vous pouvez l’inclure dans les [règles](../managing-resources/rules.md) du transfert d’événements et ajouter ces règles à une [bibliothèque](../publishing/libraries.md), qui peut à son tour être déployée sur les serveurs d’Adobe en tant que [version](../publishing/builds.md).

Lors de la création de l’élément de données, sélectionnez l’extension **[!UICONTROL Core]**, puis sélectionnez **[!UICONTROL Secret]** pour le type d’élément de données. Le panneau de droite met à jour et fournit des commandes déroulantes pour attribuer jusqu’à trois secrets à l’élément de données : un pour [!UICONTROL Développement], [!UICONTROL Évaluation] et [!UICONTROL Production], respectivement.

![Élément de données](../../images/ui/event-forwarding/secrets/data-element.png)

>[!NOTE]
>
>Seuls les secrets associés aux environnements de développement, d’évaluation et de production s’affichent pour leurs listes déroulantes respectives.

En attribuant plusieurs secrets à un élément de données unique et en l’incluant dans une règle, vous pouvez faire changer la valeur de l’élément de données en fonction de l’emplacement de la bibliothèque conteneur dans le [flux de publication](../publishing/publishing-flow.md).

![Élément de données avec plusieurs secrets](../../images/ui/event-forwarding/secrets/multi-secret-data-element.png)

>[!NOTE]
>
>Lors de la création de l’élément de données, un environnement de développement doit être affecté. Les secrets des environnements d’évaluation et de production ne sont pas requis, mais les versions qui tentent de passer à ces environnements échouent si leurs éléments de données de type secret n’ont pas de secret sélectionné pour l’environnement en question.

## Étapes suivantes

Ce guide explique comment gérer les secrets dans l’interface utilisateur. Pour plus d’informations sur l’interaction avec les secrets à l’aide de l’API Reactor, voir le [guide de points d’entrée des secrets](../../api/endpoints/secrets.md).
