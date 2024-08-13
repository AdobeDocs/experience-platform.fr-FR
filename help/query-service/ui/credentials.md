---
keywords: Experience Platform; accueil;rubriques populaires;query service;Query Service;requête;éditeur de requêtes;éditeur de requêtes;éditeur de requêtes;
solution: Experience Platform
title: Guide des informations d’identification de Query Service
description: Adobe Experience Platform Query Service fournit une interface utilisateur qui permet d’écrire et d’exécuter des requêtes, d’afficher des requêtes précédemment exécutées et d’accéder aux requêtes enregistrées par les utilisateurs de votre entreprise.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: 569f8f96a1039e52ac374e2eb07fd96ad8138edd
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 3%

---

# Guide sur les informations d’identification

Adobe Experience Platform Query Service vous permet de vous connecter à des clients externes. Vous pouvez vous connecter à ces clients externes à l’aide d’informations d’identification arrivant à expiration ou d’informations d’identification non arrivant à expiration.

>[!NOTE]
>
>Le panneau des informations d’identification n’est pas automatiquement disponible pour tous les utilisateurs. Contactez votre équipe de compte d’Adobe pour demander l’onglet [!UICONTROL Credentials] à inclure dans l’espace de travail Query Service si vous en avez besoin. Si nécessaire, ce changement est effectué à l’échelle de l’entreprise et par l’équipe d’ingénierie de l’Adobe. Il ne s’agit pas d’un paramètre contrôlé par les utilisateurs.

## Expiration des informations d’identification {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="Mode SSL du client"
>abstract="SSL doit être activé dans les clients connectés à Query Service. Assurez-vous que le mode SSL est paramétré sur « exiger »."

Vous pouvez utiliser des informations d’identification arrivant à expiration pour configurer rapidement une connexion à un client externe.

![Onglet Informations d’identification du tableau de bord Requêtes avec la section Informations d’identification arrivant à expiration mise en surbrillance.](../images/ui/credentials/expiring-credentials.png)

La section **[!UICONTROL Informations d’identification d’expiration]** fournit les informations suivantes :

- **[!UICONTROL Hôte]** : nom de l’hôte auquel connecter votre client. Le nom de votre organisation est alors intégré dans le ruban supérieur de l’interface utilisateur de Platform.
- **[!UICONTROL Port]** : numéro de port de l’hôte auquel se connecter.
- **[!UICONTROL Base de données]** : nom de la base de données à laquelle se connecter un client.
- **[!UICONTROL Nom d’utilisateur]** : nom d’utilisateur utilisé pour se connecter à Query Service.
- **[!UICONTROL Mot de passe]** : mot de passe utilisé pour se connecter à Query Service. Les mots de passe de l’interface utilisateur ont été hachés pour des raisons de sécurité. Sélectionnez l’icône de copie (![Icône Copier.](/help/images/icons/copy.png)) pour copier vos informations d’identification complètes et non hachées dans le Presse-papiers.
- **[!UICONTROL Commande PSQL]** : une commande qui a automatiquement inséré toutes les informations pertinentes pour vous connecter à Query Service à l’aide de PSQL sur la ligne de commande.
- **[!UICONTROL Expire]** : date et heure d’expiration des informations d’identification arrivant à expiration. La durée de validité par défaut du jeton est de 24 heures, mais elle peut être modifiée dans les paramètres avancés de l’Admin Console.

>[!TIP]
>
>Pour modifier la durée de vie de la session de votre connexion d’informations d’identification arrivant à expiration à Query Service, accédez à l’ [Admin Console](https://adminconsole.adobe.com/) et sélectionnez les options suivantes à l’écran : **Paramètres** > **Confidentialité et sécurité** > **Paramètres d’authentification** > **Paramètres avancés** > **Durée de session max**.
>
>![L’onglet Paramètres de l’Admin Console avec la confidentialité et la sécurité, les paramètres d’authentification et la durée de vie maximale de la session mise en surbrillance.](../images/ui/credentials/max-session-life.png)
>
>Pour plus d’informations sur les [paramètres avancés](https://helpx.adobe.com/enterprise/using/authentication-settings.html#advanced-settings) proposés par Admin Console, consultez la documentation de l’aide sur les Adobes .

### Connexion aux données du Customer Journey Analytics dans les sessions de requête {#connect-to-customer-journey-analytics}

Utilisez l’extension Customer Journey Analytics BI avec Power BI ou Tableau pour accéder à vos [vues de données](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views) Customer Journey Analytics avec SQL. En intégrant Query Service à l’extension BI, vous pouvez accéder à vos vues de données directement dans les sessions Query Service. Cette intégration simplifie la fonctionnalité des outils de BI qui utilisent Query Service comme interface PostgreSQL. Cette fonctionnalité élimine la nécessité de dupliquer les vues de données dans les outils de BI, garantit la création de rapports cohérents entre les plateformes et simplifie l’intégration des données de Customer Journey Analytics avec d’autres sources dans les plateformes de BI.

Consultez la documentation pour savoir comment [connecter Query Service à diverses applications clientes de bureau](../clients/overview.md) telles que [Power BI](../clients/power-bi.md) ou [Tableau](../clients/tableau.md)

>[!IMPORTANT]
>
>Pour utiliser cette fonctionnalité, un projet d’espace de travail Customer Journey Analytics et une vue de données sont requis.

Pour accéder aux données de votre Customer Journey Analytics dans Power BI ou Tableau, sélectionnez le menu déroulant [!UICONTROL Base de données], puis sélectionnez `prod:cja` dans les options disponibles. Ensuite, copiez vos paramètres d’identification [!DNL Postgres] (Hôte, Port, Base de données, Nom d’utilisateur, etc.) à utiliser dans votre configuration Tableau ou Power BI.

![L’onglet Informations d’identification de Query Service avec la liste déroulante de base de données mise en surbrillance.](../images/ui/credentials/database-dropdown.png)

>[!NOTE]
>
>Lorsque vous connectez Power BI ou Tableau à Customer Journey Analytics, le droit &quot;sessions simultanées&quot; de Query Service est consommé. Si d’autres sessions et requêtes sont requises, un module complémentaire du module des utilisateurs de requêtes ad hoc peut être acheté pour obtenir cinq sessions simultanées supplémentaires et une requête simultanée supplémentaire.

Vous pouvez également accéder à vos données de Customer Journey Analytics directement à partir de l’interface de ligne de commande de Query Editor ou Postgres. Pour ce faire, référencez la base de données `cja` lors de l’écriture de votre requête. Pour plus d’informations sur l’écriture, l’exécution et l’enregistrement de requêtes, consultez le [guide de création de requêtes](./user-guide.md#query-authoring) de l’éditeur de requêtes.

Pour obtenir des instructions complètes sur l’accès à vos vues de données de Customer Journey Analytics avec SQL, consultez le [guide d’extension de BI](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/bi-extension) .

## Informations d’identification sans date d’expiration {#non-expiring-credentials}

Vous pouvez utiliser des informations d’identification non arrivant à expiration pour configurer une connexion plus permanente à un client externe.

>[!NOTE]
>
>Les informations d’identification non expirantes présentent les limites suivantes :
>
>- Les utilisateurs doivent se connecter avec leur nom d’utilisateur et mot de passe au format `{technicalAccountId}:{credential}`. Vous trouverez plus d’informations dans la section [Générer les informations d’identification](#generate-credentials) .
>- Par défaut, les informations d’identification non expirantes se voient accorder les autorisations nécessaires pour exécuter uniquement des requêtes `SELECT`. Pour exécuter des requêtes `CTAS` ou `ITAS`, ajoutez manuellement les autorisations &quot;Gérer le jeu de données&quot; et &quot;Gérer les schémas&quot; au rôle associé aux informations d’identification non arrivées à expiration. L’autorisation &quot;Gérer les schémas&quot; se trouve sous la section &quot;Modélisation des données&quot; et l’autorisation &quot;Gérer les jeux de données&quot; se trouve sous la section &quot;Data Management&quot; de [Adobe Developer Console](<https://developer.adobe.com/console/>).
>- Les clients tiers peuvent réaliser des performances différentes de celles attendues lors de la mise en liste des objets de requête. Par exemple, certains clients tiers tels que [!DNL DB Visualizer] n’afficheront pas le nom de la vue dans le panneau de gauche. Cependant, le nom de la vue est accessible s’il est appelé dans une requête `SELECT`. De même, [!DNL PowerUI] peut ne pas répertorier les vues temporaires créées via SQL pour sélection dans la création du tableau de bord.

### Conditions préalables

Avant de pouvoir générer des informations d’identification non arrivant à expiration, vous devez effectuer les étapes suivantes dans Adobe Admin Console :

1. Connectez-vous à [Adobe Admin Console](https://adminconsole.adobe.com/) et sélectionnez l’organisation appropriée dans la barre de navigation supérieure.
2. [Sélectionnez un profil de produit.](../../access-control/ui/browse.md)
3. [Configurez les **sandbox** et les **autorisations de gestion de l’intégration de Query Service** pour le profil de produit.](../../access-control/ui/permissions.md)
4. [Ajoutez un nouvel utilisateur à un profil de produit](../../access-control/ui/users.md) afin qu’il se voit attribuer les autorisations configurées.
5. [Ajoutez l’utilisateur en tant qu’administrateur de profil de produit](https://helpx.adobe.com/fr/enterprise/using/manage-product-profiles.html) pour permettre la création d’un compte pour tout profil de produit actif.
6. [Ajoutez l’utilisateur en tant que développeur de profil de produit](https://helpx.adobe.com/fr/enterprise/using/manage-developers.html) afin de créer une intégration.

Pour en savoir plus sur l’affectation d’autorisations, consultez la documentation sur le [contrôle d’accès](../../access-control/home.md).

Toutes les autorisations requises sont maintenant configurées dans Adobe Developer Console pour que l’utilisateur puisse utiliser la fonction des informations d’identification arrivant à expiration.

### Générer les informations d’identification {#generate-credentials}

Pour créer un ensemble d’informations d’identification non arrivant à expiration, revenez à l’interface utilisateur de Platform et sélectionnez **[!UICONTROL Requêtes]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Requêtes]. Ensuite, sélectionnez l’onglet **[!UICONTROL Credentials]** suivi de **[!UICONTROL Generate credentials]**.

![Le tableau de bord Requêtes avec l’onglet Informations d’identification et Générer les informations d’identification en surbrillance.](../images/ui/credentials/generate-credentials.png)

Une boîte de dialogue s’affiche, vous permettant de générer des informations d’identification. Pour créer des informations d’identification non expirantes, vous devez fournir les détails suivants :

- **[!UICONTROL Nom]** : nom des informations d’identification que vous générez.
- **[!UICONTROL Description]** : (facultatif) description des informations d’identification que vous générez.
- **[!UICONTROL Affecté à]** : utilisateur auquel les informations d’identification seront attribuées. Cette valeur doit correspondre à l’adresse électronique de l’utilisateur qui crée les informations d’identification.
- **[!UICONTROL Mot de passe]** (facultatif) Mot de passe facultatif pour vos informations d’identification. Si le mot de passe n’est pas défini, Adobe génère automatiquement un mot de passe.

Une fois que vous avez fourni tous les détails requis, sélectionnez **[!UICONTROL Générer les informations d’identification]** pour générer vos informations d’identification.

![La boîte de dialogue Générer les informations d’identification est mise en surbrillance.](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>Lorsque l’option **[!UICONTROL Générer les informations d’identification]** est sélectionnée, un fichier de configuration JSON est téléchargé sur votre ordinateur local. Comme Adobe n’enregistre **pas** les informations d’identification générées, vous devez stocker le fichier téléchargé en toute sécurité et conserver un enregistrement des informations d’identification.
>
>De plus, si les informations d’identification ne sont pas utilisées pendant 90 jours, elles seront expurgées.

Le fichier de configuration JSON contient des informations telles que le nom du compte technique, l’identifiant de compte technique et les informations d’identification. Il est fourni au format suivant.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

Après avoir enregistré vos informations d’identification générées, sélectionnez **[!UICONTROL Fermer]**. Vous pouvez maintenant voir une liste de toutes vos informations d’identification qui ne expirent pas.

![ L&#39;onglet Informations d&#39;identification du tableau de bord Requêtes avec la section Informations d&#39;identification non arrivant à expiration mise en surbrillance.](../images/ui/credentials/list-credentials.png)

Vous pouvez modifier ou supprimer vos informations d’identification non arrivant à expiration. Pour modifier des informations d’identification non expirantes, sélectionnez l’icône représentant un crayon (![Icône représentant un crayon.](/help/images/icons/edit.png)). Pour supprimer des informations d’identification non expirantes, sélectionnez l’icône de suppression (![Icône de corbeille.](/help/images/icons/delete.png)).

Lors de la modification d’informations d’identification non expirantes, un modal s’affiche. Vous pouvez fournir les détails suivants à mettre à jour :

- **[!UICONTROL Nom]** : nom des informations d’identification que vous générez.
- **[!UICONTROL Description]** : (facultatif) description des informations d’identification que vous générez.
- **[!UICONTROL Affecté à]** : utilisateur auquel les informations d’identification seront attribuées. Cette valeur doit correspondre à l’adresse électronique de l’utilisateur qui crée les informations d’identification.

![Boîte de dialogue Mettre à jour le compte.](../images/ui/credentials/update-credentials.png)

Une fois que vous avez fourni tous les détails requis, sélectionnez **[!UICONTROL Mettre à jour le compte]** pour terminer la mise à jour de vos informations d’identification.

## Utilisation des informations d’identification pour se connecter à des clients externes {#use-credential-to-connect}

Vous pouvez utiliser les informations d’identification arrivant à expiration ou non pour vous connecter à des clients externes, tels qu’Aqua Data Studio, Looker ou Power BI. La méthode de saisie de ces informations d’identification varie en fonction du client externe. Reportez-vous à la documentation du client externe pour obtenir des instructions spécifiques sur l’utilisation de ces informations d’identification.

L’image indique l’emplacement de chaque paramètre trouvé dans l’interface utilisateur, à l’exception du mot de passe des informations d’identification non arrivant à expiration. Bien que les informations d’identification non expirantes soient fournies par leurs fichiers de configuration JSON, vous pouvez afficher vos informations d’identification arrivant à expiration sous l’onglet **Informations d’identification** de l’interface utilisateur.

![ L&#39;onglet Informations d&#39;identification de l&#39;espace de travail Requêtes avec la section Informations d&#39;identification arrivant à expiration mise en surbrillance.](../images/ui/credentials/expiring-credentials.png)

Le tableau ci-dessous décrit les paramètres généralement requis pour se connecter à des clients externes.

>[!NOTE]
>
>Lors de la connexion à un hôte à l’aide d’informations d’identification non arrivant à expiration, il est toujours nécessaire d’utiliser tous les paramètres répertoriés dans la section [!UICONTROL EXPIRING CREDENTIALS] , à l’exception du mot de passe et du nom d’utilisateur.
>Le format de saisie de votre nom d’utilisateur et de votre mot de passe utilise des valeurs séparées par deux points, comme illustré dans cet exemple `username:{your_username}` et `password:{password_string}`.

| Paramètre | Description | Exemple |
|---|---|---|
| **Serveur/Hôte** | Nom du serveur/hôte auquel vous vous connectez. <ul><li>Cette valeur est utilisée pour les informations d’identification arrivant à expiration et les informations d’identification non arrivant à expiration et prend la forme `server.adobe.io`. La valeur se trouve sous **[!UICONTROL Host]** dans la section [!UICONTROL EXPIRING CREDENTIALS] .</ul></li> | `acme.platform.adobe.io` |
| **Port** | port du serveur/hôte auquel vous vous connectez. <ul><li>Cette valeur est utilisée pour les informations d’identification arrivant à expiration et non arrivant à expiration. Elle se trouve sous **[!UICONTROL Port]** dans la section [!UICONTROL EXPIRING CREDENTIALS] .</ul></li> | `80` |
| **Base de données** | La base de données à laquelle vous vous connectez. <ul><li>Cette valeur est utilisée pour les informations d’identification arrivant à expiration et non arrivant à expiration et se trouve sous **[!UICONTROL Base de données]** dans la section [!UICONTROL EXPIRING CREDENTIALS] . </ul></li> | `prod:all` |
| **Nom d’utilisateur** | Nom d’utilisateur de l’utilisateur qui se connecte au client externe. <ul><li>Cette valeur est utilisée pour les informations d’identification arrivant à expiration et les informations d’identification non arrivant à expiration. Il prend la forme d’une chaîne alphanumérique avant `@AdobeOrg`. Cette valeur se trouve sous **[!UICONTROL Username]**.</li></ul> | `ECBB80245ECFC73E8A095EC9@AdobeOrg` |
| **Mot de passe** | Mot de passe de l’utilisateur qui se connecte au client externe. <ul><li>Si vous utilisez des informations d’identification arrivant à expiration, vous pouvez le trouver sous **[!UICONTROL Password]** dans la section [!UICONTROL EXPIRING CREDENTIALS] .</li><li>Si vous utilisez des informations d’identification qui ne expirent pas, cette valeur correspond aux arguments concaténés de l’ID de compte technique et aux informations d’identification extraites du fichier JSON de configuration. La valeur du mot de passe se présente comme suit : `{technicalAccountId}:{credential}`.</li></ul> | <ul><li>Le mot de passe des informations d’identification arrivant à expiration est une chaîne alphanumérique de plus de mille caractères. Aucun exemple ne sera donné.</li><li>Le mot de passe des informations d’identification n’expirant pas est le suivant :<br>`4F2611B8613DK3670V495N55:3d182fa9e0b54f33a7881305c06203ee`</li></ul> |

{style="table-layout:auto"}

## Étapes suivantes

Maintenant que vous comprenez le fonctionnement des informations d’identification arrivant à expiration et non arrivant à expiration, vous pouvez utiliser ces informations d’identification pour vous connecter à des clients externes. Pour plus d’informations sur les clients externes, consultez le [guide de connexion des clients à Query Service](../clients/overview.md).
