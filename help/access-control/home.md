---
keywords: Experience Platform;accueil;rubriques populaires;contrôle dʼaccès;adobe admin console
solution: Experience Platform
title: Présentation du contrôle d’accès
description: Dans Adobe Experience Platform, le contrôle dʼaccès est fourni par le biais dʼAdobe Admin Console. Cette fonctionnalité exploite les profils de produit dans l’Admin Console, liant les utilisateurs et utilisatrices à des autorisations et des sandbox.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 6a466770495b226f890ab67b21c5cb027fd46e02
workflow-type: tm+mt
source-wordcount: '3851'
ht-degree: 32%

---

# Présentation du contrôle d’accès

Le contrôle d’accès d’Adobe Experience Platform est fourni via les **[!UICONTROL autorisations]** dans [Adobe Experience Cloud](https://experience.adobe.com/). Cette fonctionnalité exploite les rôles et les politiques, liant les utilisateurs et utilisatrices à des autorisations et des sandbox.

## Hiérarchie et workflow du contrôle d’accès

Pour configurer le contrôle d’accès dans Experience Platform, vous devez posséder des droits d’administrateur système ou produit pour une organisation qui dispose d’un produit Experience Platform. Le rôle minimum qui permet d’accorder ou de retirer des autorisations est un administrateur ou une administratrice de produit. Les autres rôles d’administrateur ou d’administratrice qui peuvent gérer les autorisations sont les administrateurs ou administratrices système (aucune restriction). Pour en savoir plus, consultez l’article du Centre d’aide Adobe sur les [rôles administratifs](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html).

>[!NOTE]
>
>À partir de maintenant, le terme « administrateur ou administratrice » dans ce document désigne un administrateur ou une administratrice de produit ou d’un niveau supérieur (comme indiqué ci-dessus).

Un workflow de haut niveau d’obtention et d’attribution d’autorisations d’accès peut se résumer de la manière suivante :

- Après lʼattribution dʼune licence pour Adobe Experience Platform, ou pour une application/un service applicatif qui utilise Experience Platform, un e-mail est envoyé à lʼadministrateur spécifié lors de lʼattribution de la licence.
- L’administrateur ou l’administratrice se connecte à [Adobe Admin Console](#adobe-admin-console) et sélectionne **Adobe Experience Platform** depuis la liste de produits sur la page de la vue d’ensemble.
- Pour accorder l’accès à Experience Platform, il est recommandé que l’administrateur ajoute des utilisateurs au profil de produit par défaut : `AEP-Default-All-Users`.
- Dans Autorisations dans Experience Platform, l’administrateur ou administratrice peut créer de nouveaux rôles ou modifier les autorisations et les utilisateurs et utilisatrices pour tous les rôles existants.
- Lors de la création ou de la modification dʼun rôle, lʼadministrateur ou administratrice ajoute les utilisateurs et utilisatrices au rôle à lʼaide de lʼonglet **[!UICONTROL Utilisateurs]**, et accorde des autorisations à ces utilisateurs et utilisatrices (comme « [!UICONTROL Lecture des jeux de données] » ou « [!UICONTROL Gestion des schémas] ») en modifiant les autorisations des rôles. De même, l’administrateur ou administratrice peut attribuer des accès aux sandbox à l’aide de la même option de modification.
- Lorsque les utilisateurs et utilisatrices se connectent à l’interface utilisateur Experience Platform, leur accès aux fonctionnalités d’Experience Platform est géré par les autorisations qui leur ont été accordées à l’étape précédente. Par exemple, si un utilisateur ou une utilisatrice ne dispose pas de lʼautorisation « [!UICONTROL Affichage des jeux de données] », lʼonglet **[!UICONTROL Jeux de données]** nʼapparaîtra pas dans le menu latéral pour cet utilisateur ou utilisatrice.

Pour obtenir des instructions plus détaillées sur la manière dont gérer le contrôle d’accès dans Experience Platform, consultez le [guide d’utilisation du contrôle d’accès](./ui/overview.md).

Les autorisations sont activées pour tous les appels vers les API Experience Platform et renverront des erreurs si la ou les autorisations appropriées ne sont pas trouvées dans le contexte de l’utilisateur actuel. Des éléments seront masqués ou modifiés dans l’interface utilisateur en fonction des autorisations accordées à l’utilisateur actuel.

## Autorisations {#platform-permissions}

Les [!UICONTROL autorisations] fournissent un emplacement central pour la gestion de l’accès à Experience Platform pour votre organisation. Grâce aux [!UICONTROL autorisations], vous pouvez accorder des autorisations d’accès à des groupes d’utilisateurs et utilisatrices à différentes fonctionnalités d’Experience Platform telles que [!UICONTROL « Gestion des jeux de données »], [!UICONTROL « Affichage des jeux de données »] ou [!UICONTROL « Gestion des profils »].

### Rôles

Dans la section [!UICONTROL Rôles] , des autorisations sont attribuées aux utilisateurs et utilisatrices par l’intermédiaire de rôles. Les rôles vous permettent d’accorder des autorisations à un ou plusieurs utilisateurs ou utilisatrices, mais aussi de contenir leur accès aux sandbox qui leur sont attribués par le biais des rôles. Les utilisateurs et utilisatrices peuvent recevoir un ou plusieurs rôles appartenant à votre organisation.

### Rôles par défaut

Experience Platform s’accompagne de deux rôles préconfigurés par défaut. Le tableau suivant décrit les fonctionnalités fournies dans chaque profil par défaut, notamment, le sandbox auquel ils accordent l’accès ainsi que les autorisations qu’ils accordent au sein du sandbox.

| Rôle | Accès aux sandbox | Autorisations |
| --- | --- | --- |
| Tous les accès de la production par défaut | Prod | Toutes les autorisations applicables à Experience Platform à l’exception des autorisations Sandbox Administration |
| Administrateurs Sandbox | S/O | Permet d’accéder au sandbox `Prod` et aux autorisations d’administration des sandbox. |

## Sandbox et autorisations

Les sandbox hors production sont une forme de virtualisation des données qui vous permet d’isoler des données des autres sandbox et qui est généralement utilisée à des fins d’expériences de développement, de test ou d’évaluations. Les autorisations d’un rôle donnent aux utilisateurs et utilisatrices du rôle l’accès aux fonctionnalités d’Experience Platform dans les environnements de sandbox auxquels ils se sont vus accorder l’accès. Une licence Experience Platform par défaut vous accorde cinq sandbox (un de production et quatre hors production). Vous pouvez ajouter des packs de dix sandbox hors production jusquʼà un maximum de 75 sandbox au total. Veuillez contacter l’administration de votre organisation ou le service commercial d’Adobe pour plus de détails.

Pour plus d’informations sur les sandbox dans Experience Platform, reportez-vous à la [présentation des sandbox](../sandboxes/home.md).

### Accès aux sandbox

L’accès aux sandbox est géré par l’intermédiaire des rôles. Pour obtenir des instructions détaillées sur la manière d’activer l’accès à un sandbox pour un rôle, consultez le [guide des rôles du contrôle d’accès basé sur les attributs](./abac/ui/roles.md).

Les utilisateurs et utilisatrices peuvent se voir accorder l’accès à un ou plusieurs sandbox au sein d’un rôle. Si un utilisateur ou une utilisatrice fait partie de deux rôles ou plus, il ou elle aura accès à tous les sandbox inclus dans ces rôles.

L’autorisation « Gestion des sandbox » permet aux utilisateurs et aux utilisatrices de gérer, d’afficher ou de réinitialiser des sandbox.

### Autorisations des ressources {#permissions}

Les autorisations de ressources accordent l’accès à des fonctionnalités Experience Platform spécifiques. Les ressources sont divisées en catégories qui contiennent un ensemble d’autorisations pertinentes, qui peuvent être attribuées individuellement aux rôles.

Dans [!UICONTROL Autorisations], l’espace de travail des ressources d’un rôle affiche les sandbox et les autorisations actives pour ce rôle :

![Espace de travail des ressources d’un rôle avec une liste de catégories et d’autorisations sélectionnées.](./images/permissions.png)

Le tableau suivant décrit les catégories de ressources disponibles pour Experience Platform et les applications gérées par le biais d’autorisations :

| Catégorie | Description |
| --- | --- |
| [!DNL Adobe Mix Modeler] | Configurez, gérez et affichez les autorisations pour les [!DNL Adobe Mix Modeler]. |
| [!DNL AI Assistant] | Configurez les autorisations pour les [!DNL AI Assistant]. |
| [!DNL Alerts] | Configurez les autorisations de gestion, de résolution et d’affichage pour les alertes et l’historique des alertes. |
| [!DNL B2B Account Lists] | Configurez les autorisations de gestion, d’affichage et de publication pour les listes de comptes B2B, y compris des actions telles que l’ajout, la suppression, l’importation et la suppression de comptes des listes de comptes. |
| [!DNL B2B Admin Configurations] | Configurez les autorisations de gestion et d’affichage pour les configurations d’administration B2B, y compris les connexions de gestion des ressources numériques, les référentiels de ressources et les événements. |
| [!DNL B2B Assets] | Configurez les autorisations de gestion et d’affichage pour les ressources B2B, notamment les e-mails, SMS, pages de destination, fragments, modèles et images. |
| [!DNL B2B Buying Groups] | Configurez les autorisations de gestion et d&#39;affichage pour les groupes d&#39;achats B2B, y compris les fonctionnalités telles que les intérêts de la solution, les modèles de rôles et le statut du groupe d&#39;achats. |
| [!DNL B2B Channel Configurations] | Configurez les autorisations de gestion et d’affichage pour les configurations de canal B2B, y compris les paramètres tels que les limites de communication, les informations d’identification d’API et les paramètres de sécurité. |
| [!DNL B2B Dashboards] | Configurez les autorisations d’affichage pour les tableaux de bord B2B, y compris des fonctionnalités telles que l’engagement du compte, les étapes du groupe d’achats, l’augmentation des comptes et la couverture des contacts. |
| [!DNL B2B Journeys] | Configurez les autorisations de gestion, d’affichage et de publication pour les parcours B2B, y compris des fonctionnalités telles que les actions de compte et de personne, les écouteurs d’événement et les chemins de partage. |
| [!DNL Campaigns] | Configurez les autorisations de gestion, de publication et d’affichage pour les campagnes dans Journey Optimizer. |
| [!DNL Channel Configurations] | Configurez les fonctionnalités de gestion, d’affichage et d’exportation des configurations de canal telles que les sous-domaines, les groupes d’adresses IP, les préréglages de message, les enregistrements PTR, les listes de suppression, les paramètres de page de destination, les paramètres SMS et le routage de fichiers. |
| [!DNL Collaborations] | Configurez les autorisations de gestion et d’affichage des fonctionnalités Collaboration du profil de données client en temps réel. |
| [!DNL Computed Attributes] | Configurez les autorisations de gestion et d’affichage des attributs calculés publiés ou en version préliminaire. |
| [!DNL Customer Managed Keys] | Configurez les autorisations de gestion pour les clés gérées par le client. |
| [!DNL Dashboards] | Configurez les autorisations de gestion et d’affichage pour les tableaux de bord standard, personnalisés et sous licence. |
| [!DNL Data Collection] | Configurez les autorisations de gestion et d’affichage des flux de données. |
| [!DNL Data Governance] | Configurez les autorisations de gestion, d’application et d’affichage des fonctionnalités de gouvernance des données telles que les libellés, les politiques et les journaux d’activité. |
| [!DNL Data Ingestion] | Configurez les autorisations de gestion et d’affichage des fonctionnalités d’ingestion de données telles que les sources et le partage d’audience. |
| [!DNL Data Lifecycle] | Configurez les autorisations de gestion et d’affichage des fonctionnalités d’hygiène des données. |
| [!DNL Data Management] | Configurez les autorisations de gestion et d’affichage des fonctionnalités de gestion des données telles que les jeux de données et la surveillance des jeux de données et des flux. |
| [!DNL Data Modeling] | Configurez les autorisations de gestion et d’affichage des fonctionnalités de modélisation des données telles que les schémas, les relations et les métadonnées d’identité. |
| [!DNL Data Science Workspace] | Configurez les autorisations de gestion à [!DNL Data Science Workspace]. |
| [!DNL Decision Management] | Configurez la gestion et affichez les autorisations relatives aux fonctionnalités de décisions, d’offres et de stratégie de classement dans la gestion des décisions. |
| [!DNL Destinations] | Configurez les autorisations de gestion et d’affichage des destinations, y compris les fonctionnalités telles que l’activation et la création avec Destinations SDK. |
| [!DNL Federated Data] | Configurez les autorisations de gestion et d’affichage des fonctionnalités de données fédérées. |
| [!DNL Identity Management] | Configurez les autorisations de gestion et d’affichage des fonctionnalités Identity Service telles que les espaces de noms d’identité et le graphique d’identités. |
| [!DNL Intelligent Service] | Configurez les autorisations de gestion et d’affichage pour l’IA dédiée à l’attribution et l’IA dédiée aux clients dans le service intelligent. |
| [!DNL IP Warmup Configurations] | Configurez les autorisations de gestion et d’affichage des plans de préchauffage d’adresses IP et les autorisations d’affichage des rapports de préchauffage d’adresses IP. |
| [!DNL Journey Optimizer Library] | Configurez les autorisations de gestion des éléments de bibliothèque dans Adobe Journey Optimizer. |
| [!DNL Journey Optimizer Rules] | Configurez les autorisations de gestion et d’affichage des règles de fréquence dans Adobe Journey Optimizer. |
| [!DNL Journeys] | Configurez les autorisations de gestion, de publication et d’affichage des parcours, y compris les fonctionnalités telles que le rapport de parcours, les événements, les sources de données et les actions. |
| [!DNL Messages] | Configurez les autorisations de gestion, de publication et d&#39;affichage des messages, y compris les fonctionnalités telles que la prévisualisation et le test des messages. |
| [!DNL Privacy Service] | Configurez les autorisations de gestion et d’affichage des fonctionnalités de Privacy Service. |
| [!DNL Profile Management] | Configurez les autorisations de gestion, d’affichage, d’exportation et d’évaluation des fonctionnalités de service de profil telles que les audiences, les profils et les politiques de fusion. |
| [!DNL Prospects] | Configurez les autorisations de gestion et d’affichage des schémas, profils et audiences de prospects, y compris les fonctionnalités telles que l’affichage de l’accordéon du prospect. |
| [!DNL Query Service] | Configurez les autorisations de gestion pour les fonctionnalités du service de requête telles que les informations d’identification non expirantes et les requêtes SQL structurées. |
| [!DNL Reports] | Configurez les autorisations d’affichage pour les rapports de canal. |
| [!DNL Sandbox Administration] | Configurez les autorisations de gestion, d’affichage et de réinitialisation lors de l’administration des sandbox. |
| [!DNL Traits Configuration] | Configurez les caractéristiques de gestion et d’affichage via l’interface utilisateur des attributs calculés. |
| [!DNL Translation Services] | Configurez les autorisations de gestion et d’affichage des services de traduction pour les projets, les tâches, les révisions, l’interne, les paramètres et les fournisseurs. |

Le tableau suivant décrit les autorisations disponibles pour Experience Platform dans le rôle, avec des descriptions des fonctionnalités spécifiques d’Experience Platform auxquelles elles donnent accès. Pour obtenir des instructions détaillées sur comment ajouter des autorisations à un rôle, consultez le [guide des rôles du contrôle d’accès basé sur les attributs](./abac/ui/roles.md).

| Catégorie | Autorisation | Description |
| --- | --- | --- |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Gérer les données harmonisées Adobe Mix Modeler] | La possibilité d’afficher et de modifier des données harmonisées. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Afficher les données harmonisées d’Adobe Mix Modeler] | Accès en lecture seule aux données harmonisées. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Gérer les configurations des modèles Adobe Mix Modeler] | La possibilité d’afficher et de modifier les configurations de modèles. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Afficher les configurations des modèles Adobe Mix Modeler] | Accès en lecture seule aux configurations de modèles. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Gérer les configurations des plans de modèles Adobe Mix Modeler] | La possibilité d’afficher et de modifier les configurations des plans. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Afficher les configurations des plans des modèles Adobe Mix Modeler] | Accès en lecture seule aux configurations des plans. |
| [!DNL AI Assistant] | [!UICONTROL Activer l’assistant AI] | Possibilité de poser les questions [[!DNL [AI assistant]]](../ai-assistant/access.md). |
| [!DNL AI Assistant] | [!UICONTROL Afficher des informations opérationnelles] | Accès à pour obtenir des réponses aux requêtes [informations opérationnelles](../ai-assistant/home.md##operational-insights). |
| [!DNL AI Assistant] | [!UICONTROL Générer le contenu] | Permet aux utilisateurs de générer du contenu à l’aide de l’[!DNL AI Assistant]. |
| [!DNL AI Assistant] | [!UICONTROL Gérer le kit de marque] | Permettre aux utilisateurs de créer des directives de marque à l’aide du [!DNL AI Assistant]. |
| [!DNL Alerts] | [!UICONTROL Afficher l’historique des alertes] | Accès en lecture seule à l’historique des alertes. |
| [!DNL Alerts] | [!UICONTROL Résoudre les alertes] | Accès à la lecture, la modification et la suppression des alertes. |
| [!DNL Alerts] | [!UICONTROL Affichage des alertes] | Accès en lecture seule aux alertes. |
| [!DNL Alerts] | [!UICONTROL Gérer les alertes] | Accès à la lecture, la création, la modification et la suppression des alertes. |
| [!DNL B2B Account Lists] | [!UICONTROL Gérer Les Listes De Comptes B2B] | Possibilité d’afficher les **[!UICONTROL listes de comptes]** et d’y accéder dans le volet de navigation de gauche. Les utilisateurs ayant accès à **[!UICONTROL Listes de comptes]** doivent avoir accès à toutes les fonctions CRUD des listes de comptes : `/accounts-list`. |
| [!DNL B2B Admin Configurations] | [!UICONTROL Gérer les configurations d’administration B2B] | Possibilité d’afficher et d’accéder aux **[!UICONTROL configurations d’administration B2B]** dans le volet de navigation de gauche. Les utilisateurs ayant accès aux **[!UICONTROL configurations d’administration B2B]** doivent avoir accès à toutes les fonctions CRUD d’informations d’identification d’API SMS : `/admin-configs`. |
| [!DNL B2B Assets] | [!UICONTROL Gestion d’Assets B2B] | Possibilité d’afficher **[!UICONTROL Assets]** et d’y accéder dans le volet de navigation de gauche. Les utilisateurs ayant accès à **[!UICONTROL Assets]** doivent avoir accès à toutes les fonctions CRUD Assets : `/assets-listing`. |
| [!DNL B2B Assets] | [!UICONTROL Gestion des modèles B2B] | Possibilité d’afficher et d’accéder à **[!UICONTROL Modèles]** dans le volet de navigation de gauche. Les utilisateurs ayant accès à **[!UICONTROL Templates]** doivent avoir accès à toutes les fonctions CRUD de modèles : `/b2b-content-templates`. |
| [!DNL B2B Assets] | [!UICONTROL Gestion des fragments B2B] | Possibilité d’afficher et d’accéder à **[!UICONTROL Fragments]** dans le volet de navigation de gauche. Les utilisateurs ayant accès à **[!UICONTROL Fragments]** doivent avoir accès à toutes les fonctions CRUD de fragments : `/fragments`. |
| [!DNL B2B Buying Groups] | [!UICONTROL Gérer Les Groupes D’Achats B2B] | Possibilité d&#39;afficher les **[!UICONTROL groupes d&#39;achat]** et d&#39;y accéder dans le volet de navigation de gauche. Les utilisateurs ayant accès à **[!UICONTROL Groupes d&#39;achat]** doivent avoir accès à toutes les fonctions CRUD des groupes d&#39;achat : `/buying-groups`. |
| [!DNL B2B Dashboards] | [!UICONTROL Gérer les tableaux de bord d’engagement B2B] | Possibilité d’afficher et d’accéder au **[!UICONTROL Tableau de bord]** dans le volet de navigation de gauche. Les utilisateurs ayant accès à **[!UICONTROL Tableaux de bord]** doivent avoir accès à toutes les fonctions CRUD des tableaux de bord : `/insights-dashboard`. |
| [!DNL B2B Channel Configurations] | [!UICONTROL Gérer les configurations des canaux B2B] | Possibilité d’afficher et d’accéder à **[!UICONTROL Canaux]** dans le volet de navigation de gauche. Les utilisateurs ayant accès à **[!UICONTROL Canaux]** doivent avoir accès à toutes les fonctions CRUD de canaux : `/channels-config`. |
| [!DNL B2B Journeys] | [!UICONTROL Gérer les Parcours de compte B2B] | Possibilité d’afficher les **[!UICONTROL Parcours de compte]** et d’y accéder dans le volet de navigation de gauche. Les utilisateurs ayant accès à **[!UICONTROL Parcours de compte]** doivent avoir accès à toutes les fonctions CRUD des Parcours de compte : `/account-journeys`. |
| [!DNL Campaigns] | [!UICONTROL Gérer les campagnes] | Accès à la lecture, la création, la modification et la suppression des campagnes. |
| [!DNL Campaigns] | [!UICONTROL Approuver et publier des campagnes] | La possibilité de valider et de publier des campagnes. |
| [!DNL Campaigns] | [!UICONTROL Publier des campagnes] | Possibilité de publier des campagnes. |
| [!DNL Campaigns] | [!UICONTROL Afficher les campagnes] | Accès en lecture seule aux campagnes. |
| [!DNL Campaigns] | [!UICONTROL Afficher le rapport des campagnes] | Accès en lecture seule aux rapports de campagne. |
| [!DNL Channel Configurations] | [!UICONTROL Afficher les paramètres généraux des messages] | Accès en lecture seule aux paramètres généraux des messages. |
| [!DNL Channel Configurations] | [!UICONTROL Gérer les délégations de sous-domaines] | Accès à la lecture, la création, la modification et la suppression des délégations de sous-domaines. |
| [!DNL Channel Configurations] | [!UICONTROL Gestion des groupes d’adresses IP] | Accès à la lecture, la création et la modification des groupes d’adresses IP. |
| [!DNL Channel Configurations] | [!UICONTROL Gérer les paramètres généraux des messages] | Accès à la lecture, la création, la modification et la suppression des paramètres généraux des messages. |
| [!DNL Channel Configurations] | [!UICONTROL Gestion des préréglages de message] | Accès à la lecture, la création, la modification et la suppression des préréglages de message. |
| [!DNL Channel Configurations] | [!UICONTROL Afficher les préréglages de message] | Accès en lecture seule aux préréglages des messages. |
| [!DNL Channel Configurations] | [!UICONTROL Gérer les enregistrements PTR] | Accès à la lecture et à la modification des enregistrements PTR. |
| [!DNL Channel Configurations] | [!UICONTROL Afficher les enregistrements PTR] | Accès en lecture seule aux enregistrements PTR. |
| [!DNL Channel Configurations] | [!UICONTROL Gérer la suppression] | Accès à la lecture, la création, la modification et la suppression des règles de suppression. |
| [!DNL Channel Configurations] | [!UICONTROL Afficher la liste de suppression] | Accès en lecture seule à la liste de suppression. |
| [!DNL Channel Configurations] | [!UICONTROL Exporter la liste de suppression] | Accès à l’exportation de la liste de suppression au format CSV. |
| [!DNL Channel Configurations] | [!UICONTROL Gérer les paramètres de la page de destination] | Accès à la lecture, la création, la modification et la suppression des paramètres de la page de destination. |
| [!DNL Channel Configurations] | [!UICONTROL Gérer les paramètres SMS] | Accès à la lecture, la création, la modification et la suppression des paramètres des SMS. |
| [!DNL Channel Configurations] | [!UICONTROL Gérer les sous-domaines SMS] | Accès à la lecture, la création, la modification et la suppression des sous-domaines de SMS. |
| [!DNL Channel Configurations] | [!UICONTROL Gérer le routage des fichiers] | Accès à la lecture, la création, la modification et la suppression des routages de fichiers. |
| [!DNL Channel Configurations] | [!UICONTROL Afficher le routage des fichiers] | Accès en lecture seule aux routages de fichiers. |
| [!DNL Channel Configurations] | [!UICONTROL Gérer la liste de contrôle] | La possibilité de créer et de modifier la liste de contrôle. |
| [!DNL Channel Configurations] | [!UICONTROL Gérer les paramètres de langue] | La possibilité de créer et de modifier les paramètres de langue. |
| [!DNL Channel Configurations] | [!UICONTROL Gérer Les Sous-Domaines Web] | La possibilité de créer et de modifier des sous-domaines web CJM. |
| [!DNL Channel Configurations] | [!UICONTROL Gérer les informations d’identification des notifications push] | Possibilité de créer, modifier et supprimer des informations d’identification push. |
| [!DNL Collaborations] | [!UICONTROL Gestion des instances Collaboration] | Afficher, créer, mettre à jour et supprimer les instances de collaboration d’une organisation. Découvrez les instances de collaboration d’autres organisations. |
| [!DNL Collaborations] | [!UICONTROL Lire les instances Collaboration] | Lisez les instances de collaboration d’une organisation et découvrez les instances de collaboration d’autres organisations. |
| [!DNL Collaborations] | [!UICONTROL Gérer les invitations à la connexion] | Affichez, créez et supprimez des invitations à des connexions lancées par votre organisation. Accepter et refuser l’invitation à une connexion lancée par d’autres organisations. |
| [!DNL Collaborations] | [!UICONTROL Lire les invitations de connexion] | Accès en lecture seule aux invitations à une connexion. |
| [!DNL Collaborations] | [!UICONTROL Gérer les connexions Collaboration] | Un annonceur peut afficher, créer et mettre à jour des paramètres, ainsi qu’envoyer et supprimer des connexions. Un éditeur peut afficher, accepter ou refuser des connexions. |
| [!DNL Collaborations] | [!UICONTROL Lire Connexions Collaboration] | Accès en lecture seule aux connexions. |
| [!DNL Collaborations] | [!UICONTROL Gérer les données d’audience] | Intégrez et découvrez les audiences. Mettez à jour des audiences publiques, privées et personnalisées et gérez les paramètres de métadonnées de l’inventaire des audiences. |
| [!DNL Collaborations] | [!UICONTROL Lire les données d’audience] | Lire et découvrir des audiences. |
| [!DNL Collaborations] | [!UICONTROL Gérer les données de mesure] | Intégrez, mettez à jour et supprimez des données de mesure. |
| [!DNL Collaborations] | [!UICONTROL Lire les données de mesure] | Accès en lecture seule aux données de mesure. |
| [!DNL Collaborations] | [!UICONTROL Gérer les projets] | Affichez, créez, mettez à jour et supprimez des projets pour toutes les activités de découverte, de partage, d’activation et de mesure. |
| [!DNL Collaborations] | [!UICONTROL Lire les projets] | Affichez les projets pour n’importe quelle activité de découverte, de partage, d’activation et de mesure. |
| [!DNL Collaborations] | [!UICONTROL Lire les activités utilisateur] | Accès en lecture seule aux activités utilisateur. |
| [!DNL Collaborations] | [!UICONTROL Exporter les activités utilisateur] | Exporter les activités utilisateur. |
| [!DNL Collaborations] | [!UICONTROL Consultez la section Surveillance du crédit Collaboration] | Suivi du crédit au niveau de l’organisation et de l’instance. |
| [!DNL Computed Attributes] | [!UICONTROL Afficher les attributs calculés] | Accès en lecture seule à l’onglet Attributs calculés, à l’inventaire et aux détails. |
| [!DNL Computed Attributes] | [!UICONTROL Gérer les attributs calculés] | Accès à la lecture, la création, la suppression des brouillons et la désactivation des attributs calculés. |
| [!DNL Customer Managed Keys] | [!UICONTROL Gérer les clés gérées par le client] | Accès à l’affichage et à la configuration des clés gérées par le client. |
| [!DNL Dashboards] | [!UICONTROL Afficher le tableau de bord d’utilisation des licences] | Accès en lecture seule pour afficher le tableau de bord de l’utilisation des licences. |
| [!DNL Dashboards] | [!UICONTROL Gestion des tableaux de bord standard] | Ajoutez des attributs personnalisés qui ne se trouvent pas encore dans l’entrepôt de données. |
| [!DNL Dashboards] | [!UICONTROL Afficher les tableaux de bord standard] | Accès en lecture seule aux tableaux de bord Profils, Destinations et Segments. Permet également d’accéder aux tableaux de bord dans le volet de navigation de gauche et l’onglet Inventaire et intégrations des tableaux de bord . |
| [!DNL Dashboards] | [!UICONTROL Gérer les tableaux de bord personnalisés] | Accès pour créer ou modifier un tableau de bord. |
| [!DNL Dashboards] | [!UICONTROL Afficher les tableaux de bord personnalisés] | Accès en lecture seule aux tableaux de bord définis par l’utilisateur. |
| [!DNL Dashboards] | [!UICONTROL Gérer les planifications de rapports] | Possibilité de créer des plannings. |
| [!DNL Dashboards] | [!UICONTROL Exporter les données du tableau de bord] | Contrôle la capacité d’un utilisateur ou d’une utilisatrice à exporter des données tabulaires des tableaux de bord query pro mode. |
| [!DNL Data Collection] | [!UICONTROL Gérer les flux de données] | Accès à la lecture, la création et la modification des flux de données. |
| [!DNL Data Collection] | [!UICONTROL Afficher les flux de données] | Accès en lecture seule aux flux de données. |
| [!DNL Data Governance] | [!UICONTROL Gérer les libellés d’utilisation] | Accès à la lecture, la création et la suppression des étiquettes dʼutilisation des données. |
| [!DNL Data Governance] | [!UICONTROL Gestion des politiques dʼutilisation des données] | Accès à la lecture, la création, la modification et la suppression des politiques dʼutilisation des données. |
| [!DNL Data Governance] | [!UICONTROL Affichage des politiques dʼutilisation des données] | Accès en lecture seule pour les politiques dʼutilisation des données appartenant à votre organisation. |
| [!DNL Data Governance] | [!UICONTROL Afficher le journal d’activité de l’utilisateur] | Accès en lecture seule pour afficher les [journaux d’audit](../landing/governance-privacy-security/audit-logs/overview.md) enregistrés des activités Experience Platform. |
| [!DNL Data Governance] | [!UICONTROL Afficher la console de confidentialité] | Accès en lecture seule aux consoles de confidentialité. |
| [!DNL Data Ingestion] | [!UICONTROL Gestion des sources] | Accès à la lecture, la création, la modification et la désactivation des sources. |
| [!DNL Data Ingestion] | [!UICONTROL Affichage des sources] | Accès en lecture seule aux sources disponibles dans l’onglet **[!UICONTROL Catalogue]** et aux sources authentifiées dans l’onglet **[!UICONTROL Parcourir]**. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Accès à pour créer, accepter et refuser le partage de partenaire afin de connecter deux organisations et d’activer les flux de [!DNL Segment Match]. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Accès à la lecture, la création, la modification et la publication de flux [!DNL Segment Match] avec des partenaires actifs. |
| [!DNL Data Lifecycle] | [!UICONTROL Afficher le cycle de vie des données] | Accès en lecture seule pour le cycle de vie des données. |
| [!DNL Data Lifecycle] | [!UICONTROL Gérer le cycle de vie des données] | Accès à la lecture, la création, la modification et la suppression du cycle de vie des données. |
| [!DNL Data Modeling] | [!UICONTROL Gestion des schémas] | Accès pour lire, créer, modifier et supprimer des schémas et des ressources associées. |
| [!DNL Data Modeling] | [!UICONTROL Affichage des schémas] | Accès en lecture seule aux schémas et aux ressources associées. |
| [!DNL Data Modeling] | [!UICONTROL Gestion des relations] | Accès à la lecture, la création, la modification et la suppression des relations de schéma. |
| [!DNL Data Modeling] | [!UICONTROL Gestion des métadonnées dʼidentité] | Accès à la lecture, la création, la modification et la suppression des métadonnées dʼidentité pour les schémas. |
| [!DNL Data Management] | [!UICONTROL Gestion des jeux de données] | Accès à la lecture, la création, la modification et la suppression des jeux de données. Accès en lecture seule aux schémas. |
| [!DNL Data Management] | [!UICONTROL Affichage des jeux de données] | Accès en lecture seule aux jeux de données et aux schémas. |
| [!DNL Data Management] | [!UICONTROL Surveillance des données] | Accès en lecture seule à la surveillance des jeux de données et des flux. |
| [!DNL Data Science Workspace] | [!UICONTROL Gestion de l’espace de travail de science des données] | Accès à la lecture, la création, la modification et la suppression dans [!DNL Data Science Workspace]. |
| [!DNL Decision Management] | [!UICONTROL Gérer Experience Decisioning] | Capacité à gérer les entités d’Experience Decisioning. |
| [!DNL Decision Management] | [!UICONTROL Afficher Experience Decisioning] | Accès en lecture seule aux entités Experience Decisioning. |
| [!DNL Decision Management] | [!UICONTROL Gérer les décisions] | Accès à la lecture, la création, la modification et la suppression des entités de prise de décision. |
| [!DNL Decisions Management] | [!UICONTROL Afficher les décisions] | Accès en lecture seule aux entités de décision. |
| [!DNL Decision Management] | [!UICONTROL Gérer les offres] | Accès à la lecture, la création, la modification et la suppression de toutes les offres et de tous les composants. Accès en lecture seule aux décisions et aux collections. |
| [!DNL Decsion Management] | [!UICONTROL Gérer les stratégies de classement] | Accès à la lecture, la création, la modification et la suppression des rapports personnalisés et à l’utilisation des fonctions d’action. |
| [!DNL Destinations] | [!UICONTROL Affichage des destinations] | Accès en lecture seule pour afficher les destinations disponibles dans l’onglet **[!UICONTROL Catalogue]** et les destinations authentifiées dans l’onglet **[!UICONTROL Parcourir]**. |
| [!DNL Destinations] | [!UICONTROL Gérer les destinations] | Accès à la lecture, la création et la suppression des connexions de destinations et des comptes de destination. |
| [!DNL Destinations] | [!UICONTROL Activation des destinations] | Capacité à activer les données vers les destinations actives qui ont été créées. Cette autorisation nécessite également d’accorder les autorisations [!UICONTROL Afficher les destinations] ou [!UICONTROL Gérer les destinations] à l’utilisateur ou utilisatrice qui activera les destinations. |
| [!DNL Destinations] | [!UICONTROL Activer un segment sans mappage] | La possibilité d’activer des audiences vers des destinations existantes, sans afficher l’[étape de mappage](../destinations/ui/activate-batch-profile-destinations.md#mapping). Les utilisateurs peuvent ajouter et supprimer des audiences dans les workflows d’activation, mais ne peuvent pas ajouter ni supprimer des attributs ou des identités mappés. Cette autorisation nécessite également d’accorder l’autorisation [!UICONTROL Afficher les destinations] à l’utilisateur ou utilisatrice qui activera les données vers les destinations. |
| [!DNL Destinations] | [!UICONTROL Gérer et activer des destinations de jeu de données] | Possibilité de lire, créer, modifier et désactiver les flux d’exportation des jeux de données. Possibilité d’activer les données vers les jeux de données actifs qui ont été créés. Cette autorisation nécessite également d’accorder l’autorisation [!UICONTROL Afficher les destinations] à l’utilisateur ou utilisatrice qui activera les données vers les destinations. |
| [!DNL Destinations] | [!UICONTROL Création de destinations] | Possibilité de créer des destinations à lʼaide du [SDK Destination Adobe Experience Platform](../destinations/destination-sdk/overview.md). |
| [!DNL Federated Data] | [!UICONTROL Gérer les données fédérées] | La possibilité d’accéder à toutes les fonctionnalités de données fédérées, telles que la création de schémas, de modèles et de compositions. |
| [!DNL Identity Management] | [!UICONTROL Gestion des espaces de noms d’identité] | Accès à la lecture, la création, la modification et la suppression des espaces de noms d’identité. |
| [!DNL Identity Management] | [!UICONTROL Affichages des espaces de noms d’identité] | Accès en lecture seule aux espaces de noms d’identité. |
| [!DNL Identity Management] | [!UICONTROL Afficher un graphique d’identité] | Accès en lecture seule aux graphiques d’identité. |
| [!DNL Identity Management] | [!UICONTROL Gérer les paramètres d’identité] | Accès à la lecture, la création et la modification des paramètres d’identité. |
| [!DNL Identity Management] | [!UICONTROL Afficher les paramètres d’identité] | Accès en lecture seule aux paramètres d’identité. |
| [!DNL Intelligent Services] | [!UICONTROL Afficher IA dédiée à l’attribution] | Accès en lecture seule aux paramètres et informations d’Attribution AI. |
| [!DNL Intelligent Services] | [!UICONTROL Gérer l’IA dédiée à l’attribution] | Accès à la lecture, la création, la modification et la suppression des modèles IA dédiée à l’attribution. |
| [!DNL Intelligent Services] | [!UICONTROL Afficher l’IA dédiée aux clients] | Accès à la lecture ou à l’affichage des modèles d’IA dédiée aux clients. |
| [!DNL Intelligent Services] | [!UICONTROL Gérer l’IA dédiée aux clients] | Accès à la création, la mise à jour, la suppression, l’activation ou la désactivation de modèles d’IA dédiée aux clients. |
| [!DNL IP Warmup Configurations] | [!UICONTROL Afficher les plans de préchauffage d’adresses IP] | Accès en lecture seule aux plans de préchauffage des adresses IP. |
| [!DNL IP Warmup Configurations] | [!UICONTROL Gérer les plans de préchauffage d’adresses IP] | La possibilité de gérer les plans de préchauffage des adresses IP. |
| [!DNL IP Warmup Configurations] | [!UICONTROL Afficher les rapports de préchauffage d’adresses IP] | Accès en lecture seule aux rapports de préchauffage d’adresses IP. |
| [!DNL Journeys] | [!UICONTROL Gérer les Parcours &#x200B;] | Accès à la lecture, la création, la modification et la suppression des parcours. |
| [!DNL Journeys] | [!UICONTROL Afficher les Parcours &#x200B;] | Accès en lecture seule aux parcours. |
| [!DNL Journeys] | [!UICONTROL Afficher le rapport des Parcours &#x200B;] | Accès en lecture seule au rapport parcours. |
| [!DNL Journeys] | [!UICONTROL Gérer les événements Parcours, les sources de données et les actions] | Accès à la lecture, la création, la modification et la suppression des événements, des sources de données ou des actions. |
| [!DNL Journeys] | [!UICONTROL Afficher les événements de Parcours, les sources de données et les actions] | Accès en lecture seule aux événements, aux sources de données ou aux actions. |
| [!DNL Journeys] | [!UICONTROL Approuver et publier des Parcours &#x200B;] | Possibilité d’approuver et de publier des parcours lorsqu’une politique est appliquée. |
| [!DNL Journeys] | [!UICONTROL Publication de Parcours &#x200B;] | Possibilité de publier des parcours. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Gérer les éléments de bibliothèque] | La possibilité d’ajouter et de supprimer des expressions enregistrées. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Publication de fragments] | La possibilité de publier des fragments de contenu. |
| [!DNL Journey Optimizer Library] | [!UICONTROL &#x200B; Simuler du contenu &#x200B;] | Accédez à l’option Simuler du contenu pour la prévisualisation et la relecture. |
| [!DNL Journey Optimizer Rules] | [!UICONTROL Afficher les règles de fréquence] | Accès en lecture seule aux règles de fréquence. |
| [!DNL Journey Optimizer Rules] | [!UICONTROL Gérer les règles de fréquence] | Accès à la lecture, la création, la modification ou la suppression des règles de fréquence. |
| [!DNL Messages] | [!UICONTROL Gérer les messages] | Accès à la lecture, la création, la modification et la suppression des messages. |
| [!DNL Messages] | [!UICONTROL Afficher les messages] | Accès en lecture seule aux messages. |
| [!DNL Messages] | [!UICONTROL Afficher le rapport des messages] | Accès à la lecture et à la modification des rapports de messages. |
| [!DNL Messages] | [!UICONTROL Publier les messages] | Possibilité de publier des messages. |
| [!DNL Messages] | [!UICONTROL Gérer l’aperçu et le test des messages] | Possibilité d’approuver et de publier des messages lorsqu’une politique est appliquée. |
| [!DNL Privacy Service] | [!UICONTROL Gérer Privacy Service] | Accès aux workflows de confidentialité en lecture et écriture. |
| [!DNL Privacy Service] | [!UICONTROL Afficher Privacy Service] | Accès en lecture seule aux workflows de confidentialité. |
| [!DNL Profile Management] | [!UICONTROL Gestion des profils] | Accès à la lecture, la création, la modification et la suppression des jeux de données utilisés pour les profils de clients. Accès en lecture seule aux profils disponibles. |
| [!DNL Profile Management] | [!UICONTROL Affichage des profils] | Accès en lecture seule aux profils disponibles. |
| [!DNL Profile Management] | [!UICONTROL Gestion des segments] | Accès à la lecture, la création, la modification et la suppression des audiences. |
| [!DNL Profile Management] | [!UICONTROL Affichage des segments] | Accès en lecture seule aux audiences disponibles. |
| [!DNL Profile Management] | [!UICONTROL Gestion des politiques de fusion] | Accès à la lecture, la création, la modification et la suppression des politiques de fusion. |
| [!DNL Profile Management] | [!UICONTROL Affichage des politiques de fusion] | Accès en lecture seule aux politiques de fusion disponibles. |
| [!DNL Profile Management] | [!UICONTROL Importer des audiences] | Possibilité d’utiliser le workflow de chargement CSV pour importer de nouvelles audiences. |
| [!DNL Profile Management] | [!UICONTROL Exporter le segment ciblé] | Possibilité d’exporter une audience évaluée vers un jeu de données. |
| [!DNL Profile Management] | [!UICONTROL Évaluation dʼun segment sur une audience] | Possibilité de générer des profils pour une audience en évaluant une définition de segment. |
| [!DNL Profile Management] | [!UICONTROL Afficher IA B2B] | Accès en lecture seule aux paramètres et aux configurations de tous les services IA/ML B2B. |
| [!DNL Profile Management] | [!UICONTROL Gérer l’IA B2B] | Accès à la lecture, la création, la modification et la suppression des paramètres et des configurations pour tous les services IA/ML B2B. |
| [!DNL Profile Management] | [!UICONTROL Afficher le profil B2B] | Accès en lecture seule aux profils d’entité B2B (tels que le compte, l’opportunité, etc.), aux paramètres et aux configurations de tous les services IA/ML B2B et aux widgets de tableau de bord B2B. |
| [!DNL Profile Management] | [!UICONTROL Gérer le profil B2B] | Accès à la lecture, la création, la modification et la suppression des profils d’entité B2B (tels que le compte, l’opportunité, etc.). Accès en lecture seule aux paramètres et aux configurations de tous les services IA/ML B2B et des widgets de tableau de bord B2B. |
| [!DNL Profile Management] | [!UICONTROL Gérer les ressemblances] | Possibilité de créer ou de supprimer des audiences semblables. |
| [!DNL Profile Management] | [!UICONTROL Afficher l’expérience B2B] | Possibilité d’afficher les profils et les attributs B2B. |
| [!DNL Profile Management] | [!UICONTROL Afficher les paramètres du profil] | Accès en lecture seule à tous les paramètres de profil. |
| [!DNL Profile Management] | [!UICONTROL Gérer les paramètres de profil] | Accès à la lecture et à la modification de tous les paramètres de profil. |
| [!DNL Prospects] | [!UICONTROL Afficher les prospects] | Accès en lecture seule aux schémas, aux profils, aux audiences et à l’accordéon du prospect. |
| [!DNL Prospects] | [!UICONTROL Gérer les prospects] | Possibilité de créer et de gérer des schémas, des profils et des audiences de prospects. Accès en lecture seule à l’accordéon du prospect. |
| [!DNL Query Service] | [!UICONTROL Gestion des requêtes] | Accès à la lecture, la création, la modification et la suppression des requêtes SQL structurées pour les données Experience Platform. |
| [!DNL Query Service] | [!UICONTROL Gestion de lʼintégration de Query Service] | Accès à la création, la mise à jour et la suppression des informations dʼidentification sans date dʼexpiration pour lʼaccès à Query Service. |
| [!DNL Query Service] | [!UICONTROL Gérer les sessions de requête] | Capacité à supprimer des sessions existantes. |
| [!DNL Query Service] | [!UICONTROL Gérer la Liste autorisée &#x200B;] | Capacité à gérer les restrictions IP pour votre organisation. |
| [!DNL Reports] | [!UICONTROL Afficher les rapports de canal] | La possibilité d’afficher et de modifier les rapports de canal. |
| [!DNL Sandbox Administration] | [!UICONTROL Gestion des sandbox] | Accès à la lecture, la création, la modification et la suppression des sandbox. |
| [!DNL Sandbox Administration] | [!UICONTROL Affichage des sandbox] | Accès en lecture seule aux sandbox appartenant à votre organisation. |
| [!DNL Sandbox Administration] | [!UICONTROL Réinitialisation d’un sandbox] | Capacité à réinitialiser un sandbox. |
| [!DNL Sandbox Administration] | [!UICONTROL Gérer les packages] | Accès à la création, l’importation ou l’exportation de packages. |
| [!DNL Sandbox Administration] | [!UICONTROL Partager des packages] | Accès au partage de packages entre différentes organisations. |
| [!DNL Traits Configurations] | [!UICONTROL Afficher les caractéristiques] | Accès en lecture seule aux caractéristiques. |
| [!DNL Traits Configurations] | [!UICONTROL Gérer les caractéristiques] | Accès à la gestion des caractéristiques. |
| [!DNL Translation Service] | [!UICONTROL Gestion de projets de traduction] | La possibilité de gérer des projets de traduction. |
| [!DNL Translation Service] | [!UICONTROL Affichage des projets de traduction] | Accès en lecture seule aux projets de traduction. |
| [!DNL Translation Service] | [!UICONTROL Gérer les tâches de traduction] | La possibilité de gérer les tâches de traduction. |
| [!DNL Translation Service] | [!UICONTROL Affichage des tâches de traduction] | Accès en lecture seule aux tâches de traduction. |
| [!DNL Translation Service] | [!UICONTROL Gérer les révisions de traduction] | La possibilité de gérer les révisions de traduction. |
| [!DNL Translation Service] | [!UICONTROL Afficher les révisions de traduction] | Accès en lecture seule aux révisions de traduction. |
| [!DNL Translation Service] | [!UICONTROL Gestion de la traduction en interne] | La possibilité de gérer la traduction en interne. |
| [!DNL Translation Service] | [!UICONTROL Voir la traduction en interne] | Accès en lecture seule à la traduction en interne. |
| [!DNL Translation Service] | [!UICONTROL Gérer les paramètres de traduction] | La possibilité pour les administrateurs de gérer les paramètres de traduction. |
| [!DNL Translation Service] | [!UICONTROL Gestion des fournisseurs de traduction] | La possibilité de gérer les fournisseurs de traduction. |

## Étapes suivantes

En lisant ce guide, les principes du contrôle d’accès dans Experience Platform vous ont été présentés. Vous pouvez maintenant consulter le [guide d’utilisation du contrôle d’accès basé sur les attributs](./abac/overview.md) pour obtenir des instructions détaillées sur l’utilisation d’Experience Cloud pour créer des rôles et attribuer des autorisations à Experience Platform.
