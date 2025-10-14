---
keywords: Experience Platform; accueil;rubriques populaires;query service;Query Service;requête;éditeur de requêtes;éditeur de requêtes;éditeur de requêtes;
solution: Experience Platform
title: Guide des informations d’identification de Query Service
description: Adobe Experience Platform Query Service fournit une interface utilisateur qui peut être utilisée pour écrire et exécuter des requêtes, afficher des requêtes précédemment exécutées et accéder à des requêtes enregistrées par des utilisateurs au sein de votre organisation.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: 58018684a5f042bd4e121f4162e7c1663597c19a
workflow-type: tm+mt
source-wordcount: '2023'
ht-degree: 6%

---

# Guide sur les informations d’identification

Adobe Experience Platform Query Service vous permet de vous connecter à des clients externes. Vous pouvez vous connecter à ces clients externes à l’aide d’informations d’identification arrivant à expiration ou non.

>[!NOTE]
>
>Le panneau des informations d’identification n’est pas automatiquement disponible pour tous les utilisateurs. Contactez l’équipe de votre compte Adobe pour demander que l’onglet [!UICONTROL Informations d’identification] soit inclus dans l’espace de travail de Query Service si vous en avez besoin. Si nécessaire, cette modification est effectuée à l’échelle de l’organisation par l’équipe d’ingénieurs d’Adobe. Il ne s’agit pas d’un paramètre contrôlé par les utilisateurs.

## Expiration des informations d’identification {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="Mode SSL du client"
>abstract="SSL doit être activé dans les clients connectés à Query Service. Assurez-vous que le mode SSL est paramétré sur « exiger »."

Vous pouvez utiliser des informations d’identification arrivant à expiration pour configurer rapidement une connexion à un client externe.

![Onglet Informations d’identification du tableau de bord Requêtes avec la section Informations d’identification arrivant à expiration en surbrillance.](../images/ui/credentials/expiring-credentials.png)

La section **[!UICONTROL Informations d’identification arrivant à expiration]** fournit les informations suivantes :

- **[!UICONTROL Hôte]** : nom de l’hôte auquel connecter votre client. Le nom de votre organisation est intégré, comme illustré dans le ruban supérieur de l’interface utilisateur d’Experience Platform.
- **[!UICONTROL Port]** : numéro de port de l’hôte auquel se connecter.
- **[!UICONTROL Base de données]** : nom de la base de données à laquelle connecter un client.
- **[!UICONTROL Nom d’utilisateur]** : nom d’utilisateur utilisé pour la connexion à Query Service.
- **[!UICONTROL Mot de passe]** : mot de passe utilisé pour se connecter à Query Service. Les mots de passe de l’interface utilisateur ont été hachés pour des raisons de sécurité. Sélectionnez l’icône de copie (![&#x200B; Icône de copie .](/help/images/icons/copy.png)) pour copier vos informations d’identification complètes et non hachées dans le presse-papiers.
- **[!UICONTROL Commande PSQL]** : commande qui a inséré automatiquement toutes les informations pertinentes pour que vous puissiez vous connecter à Query Service à l’aide de PSQL sur la ligne de commande.
- **[!UICONTROL Expires]** : date et heure d’expiration des informations d’identification arrivant à expiration. La durée de validité par défaut du jeton est de 24 heures, mais elle peut être modifiée dans les paramètres avancés d’Admin Console.

>[!TIP]
>
>Pour modifier la durée de vie de la session de votre connexion d’informations d’identification arrivant à expiration à Query Service, accédez à [Admin Console](https://adminconsole.adobe.com/) et sélectionnez les options à l’écran suivantes : **Paramètres** > **Confidentialité et sécurité** > **Paramètres d’authentification** > **Paramètres avancés** > **Durée de vie de session maximale**.
>
>![Onglet Paramètres d’Admin Console avec Confidentialité et sécurité, Paramètres d’authentification et Durée de vie maximale de la session mis en surbrillance.](../images/ui/credentials/max-session-life.png)
>
>Consultez la documentation d’aide d’Adobe pour plus d’informations sur les [&#x200B; Paramètres avancés &#x200B;](https://helpx.adobe.com/fr/enterprise/using/authentication-settings.html#advanced-settings) proposés par Admin Console.

### Connexion aux données Customer Journey Analytics dans les sessions de requête {#connect-to-customer-journey-analytics}

Utilisez l’extension Customer Journey Analytics BI avec Power BI ou Tableau pour accéder à vos Customer Journey Analytics [vues de données](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/cja-dataviews/data-views) avec SQL. En intégrant Query Service à l’extension BI, vous pouvez accéder à vos vues de données directement dans les sessions Query Service. Cette intégration simplifie les fonctionnalités des outils de BI qui utilisent Query Service comme interface PostgreSQL. Cette fonctionnalité élimine la nécessité de dupliquer les vues de données dans les outils de BI, assure la cohérence des rapports entre les plateformes et simplifie l’intégration des données de Customer Journey Analytics à d’autres sources dans les plateformes de BI.

Consultez la documentation pour savoir comment [connecter Query Service à diverses applications de bureau clientes](../clients/overview.md) telles que [Power BI](../clients/power-bi.md) ou [Tableau](../clients/tableau.md)

>[!IMPORTANT]
>
>Un projet d’espace de travail Customer Journey Analytics et une vue de données sont nécessaires pour utiliser cette fonctionnalité.

Pour accéder à vos données Customer Journey Analytics dans Power BI ou Tableau, sélectionnez le menu déroulant [!UICONTROL Base de données], puis sélectionnez `prod:cja` dans les options disponibles. Copiez ensuite vos paramètres d&#39;identification [!DNL Postgres] (hôte, port, base de données, nom d&#39;utilisateur, etc.) à utiliser dans votre configuration Power BI ou Tableau.

![Onglet Informations d’identification de Query Service avec le menu déroulant de la base de données en surbrillance.](../images/ui/credentials/database-dropdown.png)

>[!NOTE]
>
>Lorsque vous connectez Power BI ou Tableau à Customer Journey Analytics, le droit « sessions simultanées » de Query Service est utilisé. Si des sessions et des requêtes supplémentaires sont requises, il est possible d’acheter un module complémentaire de pack d’utilisateurs de requêtes ad hoc supplémentaire pour obtenir cinq sessions simultanées supplémentaires et une requête simultanée supplémentaire.

Vous pouvez également accéder à vos données Customer Journey Analytics directement à partir de Query Editor ou de l’interface de ligne de commande Postgres. Pour ce faire, référencez la base de données `cja` lors de l’écriture de votre requête. Pour plus d’informations sur l’écriture, l’exécution et l’enregistrement de requêtes[&#x200B; consultez le guide de création de requêtes &#x200B;](./user-guide.md#query-authoring)Query Editor).

Consultez le guide d’extension [BI](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/cja-dataviews/bi-extension) pour obtenir des instructions complètes sur l’accès à vos vues de données Customer Journey Analytics avec SQL.

## Informations d’identification n’expirant pas {#non-expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_migratenonexpiringcredentials"
>title="Migrez vers les informations d’identification OAuth serveur à serveur."
>abstract="Cette migration est requise, car les informations d’identification JWT cesseront de fonctionner après le 30 juin 2025. Elle prend entre 30 et 40 secondes et ne peut pas être annulée une fois démarrée. Toutes les tâches et intégrations existantes continueront à fonctionner avec OAuth après la migration. Vous pouvez quitter cet écran et revenir à tout moment pour vérifier le statut."

Vous pouvez utiliser des informations d’identification non expirantes pour configurer une connexion plus permanente à un client externe.

>[!IMPORTANT]
>
>La première fois que vous créez ou migrez des informations d’identification non expirantes vers OAuth de serveur à serveur, vous devez utiliser un compte d’administrateur système. Seul un administrateur système peut effectuer cette action pour votre organisation. Si un non-administrateur système tente cette étape, le processus échoue avec une erreur d’autorisation. Après la configuration initiale, les informations d’identification non expirantes suivantes peuvent être créées ou migrées par les utilisateurs avec les autorisations requises.

>[!NOTE]
>
>Les informations d’identification non expirantes présentent les limites suivantes :
>
>- Les utilisateurs doivent se connecter avec leur nom d’utilisateur et leur mot de passe au format `{technicalAccountId}:{credential}`. Vous trouverez plus d’informations dans la section [Générer des informations d’identification](#generate-credentials).
>- Par défaut, les informations d’identification sans date d’expiration sont autorisées à exécuter uniquement des requêtes `SELECT`. Pour exécuter des requêtes `CTAS` ou `ITAS`, ajoutez manuellement les autorisations « Gérer le jeu de données » et « Gérer les schémas » au rôle associé aux informations d’identification non expirantes. L’autorisation « Gérer les schémas » se trouve sous la section « Modélisation des données » et l’autorisation « Gérer les jeux de données » se trouve sous la section « Gestion des données » de [Adobe Developer Console](<https://developer.adobe.com/console/>).
>- Les performances des clients tiers peuvent être différentes de celles attendues lors de la mise en liste des objets de requête. Par exemple, certains clients tiers tels que [!DNL DB Visualizer] n’afficheront pas le nom de la vue dans le panneau de gauche. Cependant, le nom de la vue est accessible s’il est appelé dans une requête `SELECT`. De même, [!DNL PowerUI] peut ne pas répertorier les vues temporaires créées via SQL pour la sélection lors de la création du tableau de bord.

### Conditions préalables

Avant de pouvoir générer des informations d’identification non expirantes, vous devez effectuer les étapes suivantes dans Adobe Admin Console :

1. Connectez-vous à [Adobe Admin Console](https://adminconsole.adobe.com/) et sélectionnez l’organisation appropriée dans la barre de navigation supérieure.
2. [Sélectionnez un profil de produit.](../../access-control/ui/browse.md)
3. [Configurez les autorisations **Sandbox** et **Gérer l’intégration de Query Service** pour le profil de produit](../../access-control/ui/permissions.md).
4. [Ajoutez un nouvel utilisateur à un profil de produit](../../access-control/ui/users.md) afin qu’il se voit accorder ses autorisations configurées.
5. [Ajoutez l’utilisateur en tant qu’administrateur de profil de produit](https://helpx.adobe.com/fr/enterprise/using/manage-product-profiles.html) pour autoriser la création d’un compte pour tout profil de produit actif.
6. [Ajoutez l’utilisateur en tant que développeur de profil de produit](https://helpx.adobe.com/fr/enterprise/using/manage-developers.html) afin de créer une intégration.

Après ces étapes, les autorisations requises sont configurées dans [Adobe Developer Console](https://developer.adobe.com/console/) pour que vous puissiez générer des informations d’identification OAuth de serveur à serveur et utiliser les fonctions d’informations d’identification expirantes ou non expirantes.

Pour plus d’informations sur l’attribution d’autorisations, consultez la [documentation sur le contrôle d’accès](../../access-control/home.md).

### Générer les informations d’identification {#generate-credentials}

Pour créer un ensemble d’informations d’identification non expirantes, revenez à l’interface utilisateur d’Experience Platform et sélectionnez **[!UICONTROL Requêtes]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Requêtes]. Sélectionnez ensuite l’onglet **[!UICONTROL Informations d’identification]** suivi de **[!UICONTROL Générer les informations d’identification]**.

![Le tableau de bord Requêtes avec l’onglet Informations d’identification et Générer des informations d’identification en surbrillance.](../images/ui/credentials/generate-credentials.png)

Une boîte de dialogue s’affiche, vous permettant de générer des informations d’identification. Pour créer des informations d’identification non expirantes, vous devez fournir les détails suivants :

- **[!UICONTROL Name]** : nom des informations d’identification que vous générez.
- **[!UICONTROL Description]** : (facultatif) description des informations d’identification que vous générez.
- **[!UICONTROL Affecté à]** : utilisateur auquel les informations d’identification seront affectées. Cette valeur doit correspondre à l’adresse e-mail de l’utilisateur qui crée les informations d’identification.
- **[!UICONTROL Mot de passe]** (facultatif) Mot de passe facultatif pour vos informations d’identification. Si le mot de passe n’est pas défini, Adobe génère automatiquement un mot de passe pour vous.

Une fois que vous avez fourni tous les détails requis, sélectionnez **[!UICONTROL Générer les informations d’identification]** pour générer vos informations d’identification.

![La boîte de dialogue Générer les informations d’identification est mise en surbrillance.](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>Lorsque l’option **[!UICONTROL Générer les informations d’identification]** est sélectionnée, un fichier JSON de configuration est téléchargé sur votre ordinateur local. Comme Adobe n’enregistre **pas** les informations d’identification générées, vous devez stocker le fichier téléchargé en toute sécurité et conserver un enregistrement des informations d’identification.
>
>En outre, si les informations d’identification ne sont pas utilisées pendant 90 jours, elles seront effacées.

Le fichier JSON de configuration contient des informations telles que le nom du compte technique, l’ID du compte technique et les informations d’identification. Il est fourni au format suivant.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

Après avoir enregistré vos informations d’identification générées, sélectionnez **[!UICONTROL Fermer]**. Vous pouvez maintenant voir une liste de toutes vos informations d’identification non expirantes.

![Onglet Informations d’identification du tableau de bord Requêtes avec la section Informations d’identification non expirantes en surbrillance.](../images/ui/credentials/list-credentials.png)

Vous pouvez modifier ou supprimer vos informations d’identification non expirantes. Pour modifier des informations d’identification non expirantes, sélectionnez l’icône en forme de crayon (![Icône en forme de crayon.](/help/images/icons/edit.png)). Pour supprimer des informations d’identification non expirantes, sélectionnez l’icône de suppression (![Icône de corbeille.](/help/images/icons/delete.png)).

Lors de la modification d’informations d’identification non expirantes, une boîte de dialogue modale s’affiche. Vous pouvez fournir les détails suivants à mettre à jour :

- **[!UICONTROL Name]** : nom des informations d’identification que vous générez.
- **[!UICONTROL Description]** : (facultatif) description des informations d’identification que vous générez.
- **[!UICONTROL Affecté à]** : utilisateur auquel les informations d’identification seront affectées. Cette valeur doit correspondre à l’adresse e-mail de l’utilisateur qui crée les informations d’identification.

![Boîte de dialogue Mettre à jour le compte.](../images/ui/credentials/update-credentials.png)

Une fois que vous avez fourni tous les détails requis, sélectionnez **[!UICONTROL Mettre à jour le compte]** pour terminer la mise à jour de vos informations d’identification.

### Migration des informations d’identification vers OAuth {#migrate-credentials}

Si vous utilisez des informations d’identification JWT non expirantes, vous devez migrer chacune d’elles vers OAuth de serveur à serveur avant le 30 juin 2025 afin d’éviter toute interruption de service.

>[!IMPORTANT]
>
>Les identifiants JWT cesseront de fonctionner après le 30 juin 2025. Vous devez effectuer manuellement cette migration pour conserver les autorisations.

Pour savoir comment identifier les informations d’identification affectées et terminer la migration, consultez le guide des informations d’identification de serveur à serveur [migration de JWT vers OAuth](./migrate-jwt-to-oauth.md).

Pour les questions courantes, reportez-vous à la [FAQ sur la migration](./migrate-jwt-to-oauth.md#faq).

## Utiliser les informations d’identification pour la connexion aux clients externes {#use-credential-to-connect}

Vous pouvez utiliser les informations d’identification arrivant à expiration ou non pour vous connecter à des clients externes, tels qu’Aqua Data Studio, Looker ou Power BI. La méthode d’entrée de ces informations d’identification varie en fonction du client externe. Reportez-vous à la documentation du client externe pour obtenir des instructions spécifiques sur l’utilisation de ces informations d’identification.

L’image indique l’emplacement de chaque paramètre trouvé dans l’interface utilisateur, à l’exception du mot de passe des informations d’identification non expirantes. Bien que les informations d’identification non expirantes soient fournies par leurs fichiers de configuration JSON, vous pouvez afficher vos informations d’identification expirantes sous l’onglet **Informations d’identification** dans l’interface utilisateur.

![Onglet Informations d’identification de l’espace de travail Requêtes avec la section Informations d’identification arrivant à expiration mise en surbrillance.](../images/ui/credentials/expiring-credentials.png)

Le tableau ci-dessous décrit les paramètres généralement requis pour établir une connexion à des clients externes.

>[!NOTE]
>
>Lors de la connexion à un hôte à l’aide d’informations d’identification non expirantes, il est toujours nécessaire d’utiliser tous les paramètres répertoriés dans la section [!UICONTROL &#x200B; INFORMATIONS D’IDENTIFICATION EXPIRANTES &#x200B;], à l’exception du mot de passe et du nom d’utilisateur.
>&#x200B;>Le format de saisie de votre nom d’utilisateur et de votre mot de passe utilise des valeurs séparées par deux points, comme illustré dans cet exemple de `username:{your_username}` et de `password:{password_string}`.

| Paramètre | Description | Exemple |
|---|---|---|
| **Serveur/Hôte** | Nom du serveur/hôte auquel vous vous connectez. <ul><li>Cette valeur est utilisée pour les informations d’identification arrivant à expiration et les informations d’identification non expirantes et se présente sous la forme d’`server.adobe.io`. La valeur se trouve sous **[!UICONTROL Hôte]** dans la section [!UICONTROL INFORMATIONS D’IDENTIFICATION ARRIVANT À EXPIRATION].</ul></li> | `acme.platform.adobe.io` |
| **Port** | Port du serveur/hôte auquel vous vous connectez. <ul><li>Cette valeur est utilisée pour les informations d’identification expirantes et non expirantes. Elle se trouve sous **[!UICONTROL Port]** dans la section [!UICONTROL INFORMATIONS D’IDENTIFICATION EXPIRANTES].</ul></li> | `80` |
| **Base de données** | Base de données à laquelle vous vous connectez. <ul><li>Cette valeur est utilisée pour les informations d’identification arrivant à expiration et les informations d’identification non expirantes. Elle se trouve sous **[!UICONTROL Base de données]** dans la section [!UICONTROL INFORMATIONS D’IDENTIFICATION ARRIVANT À EXPIRATION]. </ul></li> | `prod:all` |
| **Nom d’utilisateur** | Nom d’utilisateur de l’utilisateur qui se connecte au client externe. <ul><li>Cette valeur est utilisée pour les informations d’identification arrivant à expiration et les autres. Elle se présente sous la forme d’une chaîne alphanumérique avant `@AdobeOrg`. Cette valeur se trouve sous **[!UICONTROL Nom d’utilisateur]**.</li></ul> | `ECBB80245ECFC73E8A095EC9@AdobeOrg` |
| **Mot de passe** | Mot de passe de l’utilisateur qui se connecte au client externe. <ul><li>Si vous utilisez des informations d’identification arrivant à expiration, elles se trouvent sous **[!UICONTROL Mot de passe]** dans la section [!UICONTROL INFORMATIONS D’IDENTIFICATION ARRIVANT À EXPIRATION].</li><li>Si vous utilisez des informations d’identification non expirantes, cette valeur correspond aux arguments concaténés de l’ID de compte technique et aux informations d’identification extraites du fichier JSON de configuration. La valeur du mot de passe se présente comme suit : `{technicalAccountId}:{credential}`.</li></ul> | <ul><li>Un mot de passe d’identification arrivant à expiration comporte plus d’un millier de caractères alphanumériques. Aucun exemple ne sera donné.</li><li>Un mot de passe d’identification non expirant est le suivant :<br>`4F2611B8613DK3670V495N55:3d182fa9e0b54f33a7881305c06203ee`</li></ul> |

{style="table-layout:auto"}

## Étapes suivantes

Maintenant que vous comprenez comment fonctionnent les informations d’identification expirantes et non expirantes, vous pouvez utiliser ces informations d’identification pour vous connecter à des clients externes. Pour plus d’informations sur les clients externes, consultez le guide [connecter les clients à Query Service](../clients/overview.md).
