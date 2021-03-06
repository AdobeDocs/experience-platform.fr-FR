---
title: Configuration de secrets dans le transfert d’événements
description: Découvrez comment configurer des secrets dans lʼinterface utilisateur de la collecte de données afin de vous authentifier aux points dʼentrée utilisés dans les propriétés de transfert dʼévénement.
exl-id: eefd87d7-457f-422a-b159-5b428da54189
source-git-commit: 737354ca3b286f6c39cb71bc09aa4d6141c4d9a4
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 98%

---

# Configuration de secrets dans le transfert d’événements

Dans le transfert dʼévénement, un secret est une ressource qui représente des informations dʼidentification pour sʼauthentifier auprès dʼun autre système, ce qui permet lʼéchange sécurisé de données. Les secrets ne peuvent être créés que dans les propriétés de transfert dʼévénement.

Il existe actuellement trois types de secret pris en charge :

| Type de secret | Description |
| --- | --- |
| [!UICONTROL Jeton] | Chaîne unique de caractères représentant une valeur de jeton dʼauthentification connue et comprise par les deux systèmes. |
| [!UICONTROL HTTP] | Contient deux attributs de chaîne pour un nom dʼutilisateur et un mot de passe, respectivement. |
| [!UICONTROL OAuth2] | Contient plusieurs attributs pour la prise en charge de la spécification dʼauthentification [OAuth2](https://datatracker.ietf.org/doc/html/rfc6749). Le système vous demande les informations requises, puis gère le renouvellement de ces jetons pour vous à un intervalle spécifié. Seule la version dʼOAuth2 utilisant les [Informations dʼidentification client](https://datatracker.ietf.org/doc/html/rfc6749#section-1.3.4) est actuellement prise en charge. |

{style=&quot;table-layout:auto&quot;}

Ce guide fournit une présentation générale de la configuration des secrets pour une propriété de transfert dʼévénement ([!UICONTROL Edge]) dans lʼinterface utilisateur de la collecte de données.

>[!NOTE]
>
>Pour obtenir des instructions détaillées sur la gestion des secrets dans lʼAPI Reactor, notamment un exemple JSON de la structure dʼun secret, reportez-vous au [guide de lʼAPI Secrets](../../api/guides/secrets.md).

## Conditions préalables

Avant dʼutiliser ce guide, assurez-vous au préalable de savoir comment gérer les ressources pour les balises et le transfert dʼévénement dans lʼinterface utilisateur de la collecte de données, y compris comment créer un élément de données et une règle de transfert dʼévénement. Si vous avez besoin dʼune présentation, consultez le guide sur la [gestion des ressources](../managing-resources/overview.md).

Vous devez également posséder une compréhension pratique du flux de publication pour les balises et le transfert dʼévénement, y compris la manière dʼajouter des ressources à une bibliothèque et dʼinstaller une version de celle-ci sur votre site web à des fins de test. Pour plus dʼinformations, voir [présentation de la publication](../publishing/overview.md).

## Créer un secret {#create}

Pour créer un secret, connectez-vous à lʼinterface utilisateur de la collecte de données et ouvrez la propriété de transfert dʼévénement sous laquelle vous souhaitez ajouter le secret. Ensuite, sélectionnez **[!UICONTROL Secrets]** dans le volet de navigation de gauche, puis **[!UICONTROL Créer un secret]**.

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
* [[!UICONTROL OAuth2]](#oauth2)

### [!UICONTROL Jeton] {#token}

Pour créer un secret de jeton, sélectionnez **[!UICONTROL Jeton]** dans la liste déroulante **[!UICONTROL Type]**. Dans le champ **[!UICONTROL Jeton]** qui s’affiche, indiquez la chaîne d’identification reconnue par le système auquel vous vous authentifiez. Sélectionnez **[!UICONTROL Créer un secret]** pour enregistrer le secret.

![Secret du jeton](../../images/ui/event-forwarding/secrets/token-secret.png)

### [!UICONTROL HTTP] {#http}

Pour créer un secret HTTP, sélectionnez **[!UICONTROL HTTP simple]** dans la liste déroulante **[!UICONTROL Type]**. Dans les champs qui s’affichent ci-dessous, indiquez un nom d’utilisateur et un mot de passe pour les informations d’identification avant de sélectionner **[!UICONTROL Créer un secret]** pour enregistrer le secret.

>[!NOTE]
>
>Lors de l’enregistrement, les informations d’identification sont codées à l’aide du [schéma d’authentification HTTP « basique »](https://www.rfc-editor.org/rfc/rfc7617.html).

![Secret HTTP](../../images/ui/event-forwarding/secrets/http-secret.png)

### [!UICONTROL OAuth2] {#oauth2}

Pour créer un secret OAuth2, sélectionnez **[!UICONTROL OAuth2]** dans la liste déroulante **[!UICONTROL Type]**. Dans les champs qui s’affichent ci-dessous, fournissez vos [[!UICONTROL identifiant client] et [!UICONTROL secret client]](https://www.oauth.com/oauth2-servers/client-registration/client-id-secret/), ainsi que votre [URL d’autorisation](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) pour votre intégration OAuth. Le champ [!UICONTROL URL d’autorisation] dans l’interface utilisateur de collecte de données est une concaténation entre l’hôte du serveur d’autorisation et le chemin d’accès au jeton.

![Secret OAuth2](../../images/ui/event-forwarding/secrets/oauth-secret-1.png)

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

![Enregistrer le décalage OAuth2](../../images/ui/event-forwarding/secrets/oauth-secret-4.png)

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
| [!UICONTROL HTTP] | Si aucun environnement n’est associé au secret, sélectionnez **[!UICONTROL Échange secret]** afin d’échanger les informations d’identification vers base64. Si un environnement est joint, sélectionnez Sélectionner . **[!UICONTROL Secret Exchange et déploiement]** pour échanger vers base64 et déployer le secret. |
| [!UICONTROL OAuth2] | Sélectionnez **[!UICONTROL Générer un jeton]** pour échanger les informations d’identification et renvoyer un jeton d’accès du fournisseur d’authentification. |

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

Ce guide explique comment gérer les secrets dans l’interface utilisateur de collecte de données. Pour plus d’informations sur l’interaction avec les secrets à l’aide de l’API Reactor, voir le [guide de points d’entrée des secrets](../../api/endpoints/secrets.md).
