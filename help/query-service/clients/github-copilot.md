---
title: Connecter le pilote GitHub et Visual Studio Code à Query Service
description: Découvrez comment connecter le Copilote GitHub et Visual Studio Code à Adobe Experience Platform Query Service.
exl-id: c5b71cc8-1d30-48c0-a8e2-135445a66639
source-git-commit: 9f4ce2a3a8af72342683c859caa270662b161b7d
workflow-type: tm+mt
source-wordcount: '1370'
ht-degree: 2%

---

# Connecter [!DNL GitHub Copilot] et [!DNL Visual Studio Code] à Query Service

>[!IMPORTANT]
>
>Avant d’utiliser cet outil intégré, vous devez comprendre quelles données sont partagées avec GitHub. Les données partagées incluent des informations contextuelles sur le code et les fichiers modifiés (« invites ») et des détails sur les actions de l&#39;utilisateur (« données d&#39;engagement de l&#39;utilisateur »).  Veuillez consulter la déclaration de confidentialité de [[!DNL GitHub Copilot]](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement#github-privacy-statement) pour en savoir plus sur les données qu&#39;ils collectent. Vous devez également tenir compte des implications en matière de sécurité de l’implication de services tiers, car vous êtes responsable de la conformité aux politiques de gouvernance des données de votre entreprise. Adobe n’est pas responsable des problèmes liés aux données qui peuvent résulter de l’utilisation de cet outil. Pour plus d’informations, consultez la documentation de GitHub .

[!DNL GitHub Copilot], optimisé par OpenAI Codex, est un outil piloté par l’IA qui améliore votre expérience de codage en suggérant des fragments de code et des fonctions entières directement dans votre éditeur. Intégré à [!DNL Visual Studio Code] ([!DNL VS Code]), [!DNL Copilot] peut accélérer considérablement votre workflow, en particulier lorsque vous travaillez avec des requêtes complexes. Suivez ce guide pour savoir comment connecter [!DNL GitHub Copilot] et [!DNL VS Code] à Query Service afin d’écrire et de gérer vos requêtes avec une plus grande efficacité. Pour plus d’informations sur [!DNL Copilot], consultez [la page produit Copilot de GitHub](https://github.com/pricing) et la [documentation [!DNL Copilot] officielle](https://docs.github.com/en/copilot/about-github-copilot/what-is-github-copilot).

Ce document décrit les étapes à suivre pour connecter [!DNL GitHub Copilot] et [!DNL VS Code] à Adobe Experience Platform Query Service.

## Commencer {#get-started}

Ce guide nécessite que vous ayez déjà accès à un compte GitHub et que vous vous soyez inscrit pour [!DNL GitHub Copilot]. Vous pouvez vous [inscrire sur le site web GitHub](https://github.com/github-copilot/signup). Vous avez également besoin de [!DNL VS Code]. Vous pouvez [télécharger [!DNL VS Code] depuis leur site officiel](https://code.visualstudio.com/download).

Une fois que vous avez installé [!DNL VS Code] et activé votre abonnement [!DNL Copilot], obtenez vos informations d’identification de connexion pour Experience Platform. Ces informations d’identification se trouvent dans l’onglet [!UICONTROL Credentials] de l’espace de travail [!UICONTROL Queries] de l’interface utilisateur d’Experience Platform. Lisez le guide des informations d’identification pour [savoir comment trouver ces valeurs dans l’interface utilisateur d’Experience Platform](../ui/credentials.md). Contactez l’administrateur ou administratrice de votre organisation si vous n’avez pas actuellement accès à l’espace de travail [!UICONTROL Queries].

### Extensions de [!DNL Visual Studio Code] requises {#required-extensions}

Les extensions [!DNL Visual Studio Code] suivantes sont nécessaires pour gérer et interroger efficacement vos bases de données SQL Experience Platform directement dans l’éditeur de code. Téléchargez et installez ces extensions.

- [SQLTools](https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools) : utilisez l’extension SQLTools pour gérer et interroger plusieurs bases de données SQL. Il comprend des fonctionnalités telles qu’un exécuteur de requête, un formateur SQL et un explorateur de connexions, avec la prise en charge de pilotes supplémentaires pour améliorer la productivité des développeurs. Lisez la présentation de Visual Studio Marketplace pour plus d’informations.
- [Pilote SQLTools PostgreSQL/Cockroach](https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools-driver-pg) : cette extension vous permet de connecter, d’interroger et de gérer les bases de données PostgreSQL et CockroachDB directement dans votre éditeur de code.

Les extensions suivantes activent [!DNL GitHub Copilot] et ses fonctionnalités de chat.

- [[!DNL GitHub Copilot]](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) : fournit des suggestions de codage en ligne au fur et à mesure que vous tapez.
- [[!DNL GitHub Copilot] Chat](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat) : extension d’accompagnement qui fournit une assistance d’IA conversationnelle.

## Créer une connexion {#create-connection}

Sélectionnez l’icône de cylindre (![Icône de cylindre.](../images/clients/github-copilot/cylinder-icon.png)) dans le volet de navigation de gauche de [!DNL VS Code], suivi de **[!DNL Add New Connection]** ou de l’icône cylindre plus (![icône cylindre plus.](../images/clients/github-copilot/cylinder-plus-icon.png)).

![L’interface utilisateur Visual Studio Code avec l’extension SQL Tool et Ajouter une nouvelle connexion mise en surbrillance.](../images/clients/github-copilot/add-new-connection.png)

L’**[!DNL Connection Assistant]** apparaît. Sélectionnez le pilote de base de données **[!DNL PostgreSQL]**.

![Page des paramètres SQLTools en [!DNL VS Code] avec PostgreSQl en surbrillance.](../images/clients/github-copilot/postgres-database-driver.png)

### Paramètres de connexion d’entrée {#input-connection-settings}

La vue [!DNL Connection Settings] s’affiche. Saisissez vos informations d’identification de connexion Experience Platform dans les champs appropriés du [!DNL Connection Assistant] SQLTools. Les valeurs requises sont expliquées dans le tableau ci-dessous.

| Propriété | Description |
| --- |--- |
| [!DNL Connection name] | Fournissez un « [!DNL Connection name] » comme `Prod_MySQL_Server`, qui est descriptif et indique clairement son objectif (par exemple, un environnement de production pour un serveur MySQL). Les bonnes pratiques incluent <br><ul><li>Respectez les conventions de dénomination de votre organisation pour vous assurer qu’elle est unique dans le système.</li><li>Veillez à ce qu’il soit concis pour maintenir la clarté et éviter toute confusion avec d’autres connexions.</li><li>Incluez des détails pertinents sur la fonction ou l’environnement de la connexion dans le nom.</li></ul> |
| [!DNL Connect using] | Utilisez l’option **[!DNL Server and Port]** pour spécifier l’adresse du serveur (nom d’hôte) et le numéro de port afin d’établir une connexion directe à Experience Platform |
| [!DNL Server address] | Saisissez la valeur **[!UICONTROL Host]** fournie dans vos informations d’identification Experience Platform Postgres, par exemple `acmeprod.platform-query.adobe.io`. |
| [!DNL Port] | Cette valeur est généralement `80` pour les services Experience Platform. |
| [!DNL Database] | Saisissez la valeur **[!UICONTROL Database]** fournie dans vos informations d’identification Experience Platform Postgres, par exemple `prod:all`. |
| [!DNL Username] | Cette propriété fait référence à votre ID d’organisation. Saisissez la valeur **[!UICONTROL Username]** fournie dans vos informations d’identification Experience Platform Postgres. |
| [!DNL Password] | Cette propriété est votre jeton d’accès. Saisissez la valeur **[!UICONTROL Password]** fournie dans vos informations d’identification Experience Platform Postgres. |

![Espace de travail de l’assistant Connexion avec plusieurs paramètres mis en surbrillance.](../images/clients/github-copilot/connection-settings.png)

Sélectionnez ensuite **[!DNL Use Password]**, puis **[!DNL Save as plaintext in settings]** dans le menu déroulant qui s’affiche. Le champ [!DNL Password] s’affiche. Utilisez ce champ de saisie de texte pour saisir votre jeton d’accès.

![Le mot de passe utilisé, son menu déroulant et le champ Mot de passe mis en surbrillance.](../images/clients/github-copilot/access-token.png)

Enfin, pour activer le protocole SSL, sélectionnez le champ de saisie [!DNL SSL] et choisissez [!DNL Enabled] dans le menu déroulant qui s’affiche.

![Le champ SSL avec Activé dans le menu déroulant est mis en surbrillance.](../images/clients/github-copilot/ssl-enabled.png)

>[!TIP]
>
>Une fois que vous avez saisi toutes vos informations d’identification, vous pouvez tester votre connexion avant d’enregistrer la connexion. Faites défiler l’écran jusqu’au bas de l’espace de travail, puis sélectionnez **[!DNL Test Connection]**.
>
>![Espace de travail de l’assistant Connexion avec Tester la connexion en surbrillance.](../images/clients/github-copilot/test-connection.png "Espace de travail de l’assistant Connexion avec Tester la connexion en surbrillance."){width="100" zoomable="yes"}

Une fois que vous avez correctement saisi les détails de votre connexion, sélectionnez **[!DNL Save Connection]** pour confirmer vos paramètres.

![Espace de travail de l’assistant Connexion avec Enregistrer la connexion mis en surbrillance.](../images/clients/github-copilot/save-connection.png)

La vue [!DNL Review connection details] s’affiche et affiche vos informations d’identification de connexion. Lorsque vous êtes sûr que les détails de votre connexion sont exacts, sélectionnez **[!DNL Connect Now]**.

![La vue Vérifier les détails de la connexion avec Se connecter maintenant mise en surbrillance.](../images/clients/github-copilot/review-and-connect.png)

Votre espace de travail [!DNL VS Code] s’affiche avec une suggestion de [!DNL GitHub Copilot].

![Une session SQL connectée dans [!DNL VS Code].](../images/clients/github-copilot/connected.png)

## guide rapide [!DNL GitHub Copilot]

Une fois connecté à votre instance Experience Platform, vous pouvez utiliser [!DNL Copilot] comme assistant de codage d’IA pour vous aider à écrire du code plus rapidement et en toute confiance. Cette section couvre ses fonctionnalités clés et leur utilisation.

## Prise en main de [!DNL GitHub Copilot] {#get-started-with-copilot}

Tout d’abord, assurez-vous que la dernière version de [!DNL VS Code] est installée. Une version [!DNL VS Code] obsolète peut empêcher les principales fonctionnalités [!DNL Copilot] de fonctionner comme prévu. Assurez-vous ensuite que le paramètre [!DNL Enable Auto Completions] est activé. Si [!DNL Copilot] s’exécute correctement, l’icône **[!DNL Copilot]** (![Icône Copilote](../images/clients/github-copilot/copilot-icon.png)) s’affiche dans la barre d’état (en cas de problème, l’icône d’erreur [!DNL Copilot] s’affiche à la place). Sélectionnez l’icône **[!DNL Copilot]pour** le [!DNL [!DNL GitHub Copilot] Menu]. Dans le **[!DNL [!DNL GitHub Copilot] Menu]**, sélectionnez **[!DNL Edit Settings]**

![Éditeur de [!DNL VS Code] avec la [!DNL GitHub Copilot Menu] affichée et l’icône [!DNL Copilot] et les paramètres d’édition mis en surbrillance.](../images/clients/github-copilot/github-copilot-menu.png)

Faites défiler les options vers le bas et assurez-vous que la case est cochée pour le paramètre [!DNL Enable Auto Completions] .

![Panneau des paramètres pour [!DNL GitHub Copilot] avec la case à cocher Activer les auto-compléments sélectionnée et mise en surbrillance.](../images/clients/github-copilot/enable-auto-completions.png)

## Saisies de code {#code-completions}

Une fois que vous avez installé l’extension [!DNL GitHub Copilot] et que vous vous êtes connecté, elle active automatiquement une fonctionnalité appelée **Texte fantôme**, qui vous suggère de compléter le code au fur et à mesure que vous le tapez. Ces suggestions vous aident à écrire du code plus efficacement et avec moins d’interruptions. Vous pouvez également utiliser des commentaires pour guider les suggestions de code de l’IA. Cela signifie que les utilisateurs n’ayant pas de connaissances techniques peuvent convertir du langage clair en code pour explorer leurs données.

![Interface utilisateur de VSCode avec une suggestion de code et l’icône [!DNL GitHub Copilot] mise en surbrillance.](../images/clients/github-copilot/ghost-text.png)

>[!TIP]
>
>Si vous souhaitez désactiver le [!DNL Copilot] pour un fichier ou une langue spécifique, sélectionnez l’icône dans la barre d’état et désactivez-la.

### Accepter les suggestions de texte fantôme en tout ou en partie {#accept-suggestions}

Lorsque [!DNL GitHub Copilot] suggère des compléments de code, vous pouvez accepter des suggestions partielles ou complètes. Sélectionnez **Tab** pour accepter l’intégralité de la suggestion, ou maintenez la touche **Ctrl (ou Commande sous Mac)** enfoncée et appuyez sur la **flèche de droite** pour accepter une partie du texte. Pour ignorer une suggestion, appuyez sur **Échap**.

>[!TIP]
>  
>Si vous n’obtenez aucune suggestion, assurez-vous que [[!DNL Copilot]  est activé dans la langue de votre fichier](#get-started-with-copilot).

![Éditeur de [!DNL VS Code] affichant une suggestion de texte gris pâle de [!DNL GitHub Copilot] en tant que texte fantôme à côté du code partiellement tapé.](../images/clients/github-copilot/accept-partial-suggestions.png)

### Suggestions alternatives {#alternative-suggestions}

Pour passer en revue les autres suggestions de code, sélectionnez les flèches dans la boîte de dialogue [!DNL Copilot].

![Éditeur de [!DNL VS Code] affichant le panneau de suggestions alternatives Copilote.](../images/clients/github-copilot/code-suggestions.png)


## Utiliser le chat en ligne {#inline-chat}

Vous pouvez également discuter directement avec [!DNL Copilot] à propos de votre code. Utilisez **Contrôle (ou Commande) + I** pour déclencher la boîte de dialogue de conversation en ligne. Cette fonctionnalité est utilisée pour effectuer une itération sur votre code et affiner les suggestions en contexte. Vous pouvez mettre en surbrillance un bloc de code et utiliser le chat en ligne pour voir une solution différente proposée par l’IA avant d’accepter.

![Fenêtre de conversation intégrée avec vue diff](../images/clients/github-copilot/inline-chat.png)

<!-- THis section is poss unnecessary:
There are inline features for chat including doc, expalin, fix and test
![fix, document, explain](../images/clients/github-copilot/fix-document-explain.png)
 -->

## Vue de conversation dédiée {#dedicated-chat}

Vous pouvez utiliser une interface de chat plus traditionnelle avec une barre latérale de chat dédiée pour former des idées et une stratégie, résoudre des problèmes de codage et discuter des détails de mise en œuvre. Sélectionnez l’icône de chat (![l’icône Copilote de chat).](../images/clients/github-copilot/chat-icon.png)) dans la barre latérale [!DNL VS Code] pour ouvrir une fenêtre de conversation dédiée.

![Barre latérale de conversation [!DNL GitHub Copilot] avec l’icône de conversation mise en surbrillance.](../images/clients/github-copilot/chat-sidebar.png)

Vous pouvez également accéder à l’historique de la conversation en sélectionnant l’icône d’historique (![ L’icône d’historique.](../images/clients/github-copilot/history-icon.png)) en haut du panneau de conversation.

## Étapes suivantes

Vous êtes maintenant prêt à interroger efficacement vos bases de données Experience Platform directement à partir de votre éditeur de code et à utiliser les suggestions de code optimisées par l’IA de [!DNL GitHub Copilot] pour rationaliser l’écriture et l’optimisation des requêtes SQL. Pour plus d’informations sur l’écriture et l’exécution de requêtes, reportez-vous aux [conseils pour l’exécution des requêtes](../best-practices/writing-queries.md).
