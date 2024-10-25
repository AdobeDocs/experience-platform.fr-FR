---
title: Connexion de GitHub Copilot et de Visual Studio Code à Query Service
description: Découvrez comment connecter GitHub Copilot et Visual Studio Code à Adobe Experience Platform Query Service.
source-git-commit: f0c5b311721497bf2a14ca49dc5f1c9653e85efc
workflow-type: tm+mt
source-wordcount: '1366'
ht-degree: 2%

---

# Connecter [!DNL GitHub Copilot] et [!DNL Visual Studio Code] à Query Service

>[!IMPORTANT]
>
>Avant d’utiliser cet outil intégré, vous devez comprendre les données qui sont partagées avec GitHub. Les données partagées incluent des informations contextuelles sur le code et les fichiers en cours d’édition (&quot;invites&quot;) et des détails sur les actions des utilisateurs (&quot;données d’engagement des utilisateurs&quot;).  Veuillez consulter la déclaration de confidentialité de [[!DNL GitHub Copilot] ](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement#github-privacy-statement) pour en savoir plus sur les données qu’ils collectent. Vous devez également tenir compte des implications sur la sécurité de la participation à des services tiers, car vous êtes responsable de la conformité aux politiques de gouvernance des données de votre entreprise. Adobe n’est responsable d’aucune préoccupation ou de problème liés aux données pouvant résulter de l’utilisation de cet outil. Pour plus d’informations, consultez la documentation de GitHub .

[!DNL GitHub Copilot], optimisé par OpenAI Codex, est un outil piloté par l’IA qui améliore votre expérience de codage en suggérant des fragments de code et des fonctions entières directement dans votre éditeur. Intégré à [!DNL Visual Studio Code] ([!DNL VS Code]), [!DNL Copilot] peut accélérer considérablement votre workflow, en particulier lorsque vous travaillez avec des requêtes complexes. Suivez ce guide pour savoir comment connecter [!DNL GitHub Copilot] et [!DNL VS Code] à Query Service afin d’écrire et de gérer vos requêtes avec plus d’efficacité. Pour plus d&#39;informations sur [!DNL Copilot], consultez la [page produit Copilot de GitHub](https://github.com/pricing) et la [documentation officielle [!DNL Copilot] 5}.](https://docs.github.com/en/copilot/about-github-copilot/what-is-github-copilot)

Ce document décrit les étapes requises pour se connecter [!DNL GitHub Copilot] et [!DNL VS Code] à Adobe Experience Platform Query Service.

## Commencer {#get-started}

Ce guide nécessite que vous ayez déjà accès à un compte GitHub et que vous vous soyez inscrit à [!DNL GitHub Copilot]. Vous pouvez [vous inscrire sur le site Web GitHub](https://github.com/github-copilot/signup). Vous avez également besoin de [!DNL VS Code]. Vous pouvez [télécharger [!DNL VS Code] depuis leur site Web officiel](https://code.visualstudio.com/download).

Une fois que vous avez installé [!DNL VS Code] et activé votre abonnement [!DNL Copilot], acquérez vos informations de connexion pour Experience Platform. Ces informations d’identification se trouvent dans l’onglet [!UICONTROL Credentials] de l’espace de travail [!UICONTROL Queries] de l’interface utilisateur de Platform. Lisez le guide des informations d’identification pour [découvrir comment trouver ces valeurs dans l’interface utilisateur de Platform](../ui/credentials.md). Contactez l’administrateur de votre organisation si vous n’avez pas actuellement accès à l’espace de travail [!UICONTROL Requêtes].

### Extensions [!DNL Visual Studio Code] requises {#required-extensions}

Les extensions [!DNL Visual Studio Code] suivantes sont nécessaires pour gérer et interroger efficacement vos bases de données SQL Platform directement dans l’éditeur de code. Téléchargez et installez ces extensions.

- [SQLTools](https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools) : utilisez l’extension SQLTools pour gérer et interroger plusieurs bases de données SQL. Il comprend des fonctionnalités telles qu’un moteur de requête, un formateur SQL et un explorateur de connexions, avec la prise en charge de pilotes supplémentaires pour accroître la productivité des développeurs. Pour plus d’informations, consultez la présentation de Visual Studio Marketplace .
- [SQLTools PostgreSQL/Cockroach Driver](https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools-driver-pg) : cette extension vous permet de connecter, d’interroger et de gérer des bases de données PostgreSQL et CockroachDB directement dans votre éditeur de code.

Les extensions suivantes activent [!DNL GitHub Copilot] et ses fonctionnalités de chat.

- [[!DNL GitHub Copilot]](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) : fournit des suggestions de codage en ligne au fur et à mesure que vous tapez.
- [[!DNL GitHub Copilot] Chat](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat) : extension compagnon fournissant une assistance IA conversationnelle.

## Créer une connexion {#create-connection}

Sélectionnez l’icône de cylindre (![Icône de cylindre.](../images/clients/github-copilot/cylinder-icon.png)) dans le volet de navigation de gauche de [!DNL VS Code], suivi de **[!DNL Add New Connection]** ou de l’icône du cylindre plus (![Le cylindre plus icône.](../images/clients/github-copilot/cylinder-plus-icon.png)).

![L’interface utilisateur Visual Studio Code avec l’extension SQL Tool et Ajouter une nouvelle connexion mise en surbrillance.](../images/clients/github-copilot/add-new-connection.png)

L’**[!DNL Connection Assistant]** apparaît. Sélectionnez le pilote de base de données **[!DNL PostgreSQL]**.

![La page des paramètres SQLTools dans [!DNL VS Code] avec PostgreSQl en surbrillance.](../images/clients/github-copilot/postgres-database-driver.png)

### Paramètres de connexion d’entrée {#input-connection-settings}

La vue [!DNL Connection Settings] s’affiche. Saisissez vos informations d’identification de connexion Platform dans les champs appropriés des SQLTools [!DNL Connection Assistant]. Les valeurs requises sont expliquées dans le tableau ci-dessous.

| Propriété | Description |
| --- |--- |
| [!DNL Connection name] | Fournissez un &quot;[!DNL Connection name]&quot; tel que `Prod_MySQL_Server` descriptif et indiquant clairement son objectif (par exemple, un environnement de production pour un serveur MySQL). Les bonnes pratiques sont les suivantes :<br><ul><li>Respectez les conventions de dénomination de votre entreprise pour vous assurer qu’elle est unique dans le système.</li><li>Veillez à ce qu’il reste clair et évitez toute confusion avec d’autres liens.</li><li>Incluez les détails pertinents sur la fonction ou l’environnement de la connexion dans le nom.</li></ul> |
| [!DNL Connect using] | Utilisez l’option **[!DNL Server and Port]** pour spécifier l’adresse du serveur (nom d’hôte) et le numéro de port pour établir une connexion directe à Platform. |
| [!DNL Server address] | Saisissez la valeur **[!UICONTROL Host]** fournie dans vos informations d’identification Platform Postgres, telles que `acmeprod.platform-query.adobe.io`. |
| [!DNL Port] | Cette valeur est généralement `80` pour les services Platform. |
| [!DNL Database] | Saisissez la valeur **[!UICONTROL Database]** fournie dans vos informations d’identification Platform Postgres, telles que `prod:all`. |
| [!DNL Username] | Cette propriété fait référence à votre ID d’organisation. Saisissez la valeur **[!UICONTROL Username]** fournie dans vos informations d’identification Platform Postgres. |
| [!DNL Password] | Cette propriété est votre jeton d’accès. Saisissez la valeur **[!UICONTROL Password]** fournie dans vos informations d’identification Platform Postgres. |

![L’espace de travail de l’assistant de connexion avec plusieurs paramètres en surbrillance.](../images/clients/github-copilot/connection-settings.png)

Ensuite, sélectionnez **[!DNL Use Password]**, suivi de **[!DNL Save as plaintext in settings]** dans le menu déroulant qui s’affiche. Le champ [!DNL Password] s’affiche. Utilisez ce champ de saisie de texte pour saisir votre jeton d’accès.

![Le champ Utiliser le mot de passe, son menu déroulant et le champ Mot de passe sont mis en surbrillance.](../images/clients/github-copilot/access-token.png)

Enfin, pour activer SSL, sélectionnez le champ d’entrée [!DNL SSL] et choisissez [!DNL Enabled] dans le menu déroulant qui s’affiche.

![Le champ SSL avec Activé dans le menu déroulant est surligné.](../images/clients/github-copilot/ssl-enabled.png)

>[!TIP]
>
>Une fois que vous avez saisi toutes vos informations d’identification, vous pouvez tester votre connexion avant d’enregistrer la connexion. Faites défiler l’espace de travail vers le bas et sélectionnez **[!DNL Test Connection]**.
>
>![ L’espace de travail de l’assistant de connexion avec Test Connection en surbrillance.](../images/clients/github-copilot/test-connection.png " L’espace de travail de l’assistant de connexion avec Test Connection en surbrillance."){width="100" zoomable="yes"}

Une fois que vous avez saisi correctement les détails de votre connexion, sélectionnez **[!DNL Save Connection]** pour confirmer vos paramètres.

![L’espace de travail de l’assistant de connexion avec l’option Enregistrer la connexion mise en surbrillance.](../images/clients/github-copilot/save-connection.png)

La vue [!DNL Review connection details] apparaît et affiche vos informations d’identification de connexion. Lorsque vous êtes certain que les détails de votre connexion sont précis, sélectionnez **[!DNL Connect Now]**.

![ La vue Détails de la connexion de révision avec l’option Se connecter maintenant mise en surbrillance.](../images/clients/github-copilot/review-and-connect.png)

Votre espace de travail [!DNL VS Code] s’affiche avec une suggestion de [!DNL GitHub Copilot].

![Une session SQL connectée dans [!DNL VS Code].](../images/clients/github-copilot/connected.png)

## Guide rapide [!DNL GitHub Copilot]

Une fois connecté à votre instance Platform, vous pouvez utiliser [!DNL Copilot] comme assistant de codage AI pour vous aider à écrire du code plus rapidement et en toute confiance. Cette section décrit ses fonctionnalités clés et comment les utiliser.

## Prise en main de [!DNL GitHub Copilot] {#get-started-with-copilot}

Tout d’abord, assurez-vous que la dernière version de [!DNL VS Code] est installée. Une version [!DNL VS Code] obsolète peut empêcher les fonctions de clé [!DNL Copilot] de fonctionner comme prévu. Ensuite, assurez-vous que le paramètre [!DNL Enable Auto Completions] est activé. Si [!DNL Copilot] s’exécute correctement, l’icône **[!DNL Copilot]** (![L’icône Copilot](../images/clients/github-copilot/copilot-icon.png)) s’affiche dans votre barre d’état (en cas de problème, l’icône d’erreur [!DNL Copilot] s’affiche à la place). Sélectionnez l’icône **[!DNL Copilot]** pour ouvrir le menu [!DNL [!DNL GitHub Copilot]]. Dans le **[!DNL [!DNL GitHub Copilot] Menu]**, sélectionnez **[!DNL Edit Settings]**

![L’éditeur [!DNL VS Code] avec [!DNL GitHub Copilot Menu] affiché et l’icône [!DNL Copilot] et l’option Modifier les paramètres mise en surbrillance.](../images/clients/github-copilot/github-copilot-menu.png)

Faites défiler les options vers le bas et assurez-vous que la case à cocher est activée pour le paramètre [!DNL Enable Auto Completions] .

![Panneau des paramètres de [!DNL GitHub Copilot] avec la case à cocher Activer les auto-complétions sélectionnée et mise en surbrillance.](../images/clients/github-copilot/enable-auto-completions.png)

## Renvois de code {#code-completions}

Une fois que vous avez installé l’extension [!DNL GitHub Copilot] et que vous vous êtes connecté, elle active automatiquement une fonctionnalité appelée **Ghost Text**, qui suggère des compléments de code au fur et à mesure que vous tapez. Ces suggestions vous aident à écrire du code plus efficacement et avec moins d’interruptions. Vous pouvez également utiliser des commentaires pour guider les suggestions de code AI. Cela signifie que les utilisateurs non techniques peuvent convertir la parole brute en code pour explorer leurs données.

![L’interface utilisateur VSCode avec une suggestion de code et l’icône [!DNL GitHub Copilot] mise en surbrillance.](../images/clients/github-copilot/ghost-text.png)

>[!TIP]
>
>Si vous souhaitez désactiver [!DNL Copilot] pour un fichier ou une langue spécifique, sélectionnez l’icône dans la barre d’état et désactivez-la.

### Accepter des suggestions de texte Ghost complètes ou partielles {#accept-suggestions}

Lorsque [!DNL GitHub Copilot] suggère des compléments de code, vous pouvez accepter des suggestions partielles ou complètes. Sélectionnez **Tabulation** pour accepter l’intégralité de la suggestion ou maintenez la touche **Contrôle (ou Commande sur Mac)** enfoncée et appuyez sur la **flèche vers la droite** pour accepter le texte partiel. Pour ignorer une suggestion, appuyez sur **Échap**.

>[!TIP]
>  
>Si vous ne recevez pas de suggestions, assurez-vous que [[!DNL Copilot] est activé dans la langue de votre fichier ](#get-started-with-copilot).

![ L’éditeur [!DNL VS Code] présentant une suggestion de texte gris faible provenant de [!DNL GitHub Copilot] comme texte fantôme en regard du code partiellement saisi.](../images/clients/github-copilot/accept-partial-suggestions.png)

### Suggestions alternatives {#alternative-suggestions}

Pour passer en revue d’autres suggestions de code, sélectionnez les flèches dans la boîte de dialogue [!DNL Copilot].

![L’éditeur [!DNL VS Code] qui affiche le panneau des suggestions alternatives Copilot.](../images/clients/github-copilot/code-suggestions.png)


## Utilisation de la messagerie instantanée {#inline-chat}

Vous pouvez également discuter directement avec [!DNL Copilot] à propos de votre code. Utilisez **Contrôle (ou Commande) + I** pour déclencher la boîte de dialogue de conversation en ligne. Cette fonctionnalité est utilisée pour itérer sur votre code et pour affiner les suggestions en contexte. Vous pouvez mettre en évidence un bloc de code et utiliser la messagerie instantanée pour voir une solution différente proposée par l’IA avant d’accepter.

![Fenêtre de conversation en ligne avec vue diff](../images/clients/github-copilot/inline-chat.png)

<!-- THis section is poss unnecessary:
There are inline features for chat including doc, expalin, fix and test
![fix, document, explain](../images/clients/github-copilot/fix-document-explain.png)
 -->

## Vue de chat dédiée {#dedicated-chat}

Vous pouvez utiliser une interface de conversation plus traditionnelle avec une barre latérale dédiée pour formuler des idées et des stratégies, résoudre des problèmes de codage et discuter des détails de mise en oeuvre. Sélectionnez l’icône de conversation (![Icône Conversation Copilot .](../images/clients/github-copilot/chat-icon.png)) dans la barre latérale [!DNL VS Code] pour ouvrir une fenêtre de discussion dédiée.

![La barre latérale de la conversation [!DNL GitHub Copilot] avec l’icône de conversation mise en surbrillance.](../images/clients/github-copilot/chat-sidebar.png)

Vous pouvez également accéder à l’historique des conversations en sélectionnant l’icône Historique (![Icône Historique.](../images/clients/github-copilot/history-icon.png)) en haut du panneau de discussion.

## Étapes suivantes

Vous êtes maintenant prêt à interroger efficacement vos bases de données Platform directement à partir de votre éditeur de code et à utiliser les suggestions de code optimisées par l’IA de [!DNL GitHub Copilot] pour rationaliser l’écriture et l’optimisation des requêtes SQL. Pour plus d’informations sur l’écriture et l’exécution de requêtes, reportez-vous aux [conseils pour l’exécution des requêtes](../best-practices/writing-queries.md).
