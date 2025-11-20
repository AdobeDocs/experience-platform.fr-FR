---
title: Flux de publication
description: Découvrez le processus de création des bibliothèques, de test et d’approbation des versions pour la production dans Adobe Experience Platform.
exl-id: 4885f60b-6401-4ec7-aa1a-29c135087847
source-git-commit: 2d71eafb00098d958c8cff9350caa27bd3f0260d
workflow-type: tm+mt
source-wordcount: '1407'
ht-degree: 84%

---

# Flux de publication {#publishing-flow}

>[!CONTEXTUALHELP]
>id="platform_tags_publishing_flow"
>title="Flux de publication"
>abstract="Découvrez les niveaux d’autorisation requis des utilisateurs et utilisatrices pour le flux de publication, y compris les droits de développement, d’approbation et de publication."

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Le flux de publication des balises dans Adobe Experience Platform fait référence au processus de création de bibliothèques, de test des versions et dʼapprobation pour la production.

Les actions disponibles que vous pouvez réaliser sur une bibliothèque dépendent de l’état de la bibliothèque et du niveau d’autorisation que vous possédez. En outre, l’état d’une bibliothèque affecte également les ressources qu’elle contient (règles, éléments de données et extensions) en fonction de ce qui se trouve en amont dans le flux de publication.

Les sections ci-dessous couvrent les détails concernant les autorisations, l’état de la bibliothèque et les éléments en amont qui se rapportent au flux de publication.

## Autorisations {#permissions}

Il existe différents niveaux d’autorisations d’utilisateur importants pour le flux de publication, qui sont précisément les droits de propriété [!UICONTROL Develop], [!UICONTROL Approve] et [!UICONTROL Publish] :

* **[!UICONTROL Develop]** : prévoit la possibilité de créer des bibliothèques, de créer à des fins de développement et d’envoyer pour approbation.
* **[!UICONTROL Approve]** : prévoit la possibilité de créer pour l’évaluation et d’approuver les versions évaluées.
* **[!UICONTROL Publish]** : prévoit la possibilité de publier une bibliothèque approuvée.

Les droits ne sont pas inclusifs. Pour qu’une seule personne effectue le processus du début à la fin, cette personne doit se voir attribuer les trois droits au sein d’une propriété donnée.

Pour plus dʼinformations sur la gestion des autorisations pour les balises, consultez le [guide des autorisations utilisateur](../administration/user-permissions.md).

## État de la bibliothèque {#state}

En ce qui concerne le flux de publication, une bibliothèque peut se trouver dans quatre états de base :

* [[!UICONTROL Development]](#development)
* [[!UICONTROL Submitted]](#submitted)
* [[!UICONTROL Approved]](#approved)
* [[!UICONTROL Published]](#published)

Ces quatre états sont représentés sous forme de colonnes dans l’onglet **[!UICONTROL Publishing Flow]**.

![](./images/approval-workflow/flow-ui.png)

Des mesures spécifiques doivent être prises pour déplacer une bibliothèque entre ces états. Le diagramme suivant décrit chaque action qui déplace une bibliothèque entre les états :

![](./images/approval-workflow/library-state.png)

### [!UICONTROL Development] {#development}

Lorsque de nouvelles bibliothèques sont créées, elles démarrent à l’état [!UICONTROL Development]. Toute modification apportée à une bibliothèque doit être effectuée lorsque la bibliothèque est dans l’état [!UICONTROL Development]. Une fois le développement et les tests terminés, la bibliothèque peut être envoyée pour approbation.

Le tableau suivant décrit les actions disponibles pour une bibliothèque à l’état [!UICONTROL Development] :

| Action | Description |
| --- | --- |
| [!UICONTROL Edit] | Utilisez l’écran [!UICONTROL Edit Library] pour ajouter ou supprimer des composants de la bibliothèque. |
| [!UICONTROL Build to Development] | Créez une version pour la bibliothèque. La version est compilée et déployée dans l’environnement auquel la bibliothèque est attribuée. Cette étape échoue si la bibliothèque n’est pas attribuée à un environnement ou si elle contient une modification déjà définie en amont. |
| [!UICONTROL Submit for Approval] | Annulez l’attribution de la bibliothèque à partir de l’environnement de développement et déplacez la bibliothèque dans la colonne [!UICONTROL Submitted] pour permettre à un utilisateur disposant des autorisations d’approbation de travailler dessus. Pour que cette option soit activée, la dernière version de la bibliothèque doit avoir été installée avec succès. |
| [!UICONTROL Submit & Build to Staging] | Cela ne peut être effectué que par un utilisateur disposant des droits Développer et Approuver. Cette action annule l’affectation de la bibliothèque à partir de l’environnement de développement, déplace la bibliothèque vers l’état [!UICONTROL Submitted] et crée la bibliothèque dans l’environnement d’évaluation. Pour que cette option soit activée, la dernière version de la bibliothèque doit avoir été installée avec succès. |
| [!UICONTROL Approve for Publishing] | Cela ne peut être effectué que par un utilisateur disposant des droits Développer et Approuver. Cette action annule l’affectation de la bibliothèque à partir de l’environnement de développement et la déplace vers l’état [!UICONTROL Approved], en ignorant entièrement l’environnement d’évaluation et l’état [!UICONTROL Submitted]. Pour que cette option soit activée, la dernière version de la bibliothèque doit avoir été installée avec succès. |
| [!UICONTROL Approve & Publish to Production] | Cela ne peut être effectué que par un utilisateur disposant des droits Développer, Approuver et Publier. Cette action annule l’affectation de la bibliothèque à partir de l’environnement de développement, la déplace vers l’état [!UICONTROL Approved] et la publie en production. Une fois la création de l’environnement de production terminée, la bibliothèque passe à l’état [!UICONTROL Published]. Pour que cette option soit activée, la dernière version de la bibliothèque doit avoir été installée avec succès. |
| [!UICONTROL Delete] | Supprimez la bibliothèque du système. Cela ne supprime pas la version de l’environnement. |

### [!UICONTROL Submitted] {#submitted}

Lorsqu’une bibliothèque se trouve à l’état [!UICONTROL Submitted], un utilisateur disposant d’autorisations d’approbation peut tester la bibliothèque au sein de l’environnement d’évaluation. Lorsque le test est terminé, la bibliothèque peut être approuvée ou refusée. Les versions refusées reviennent au niveau du [!UICONTROL Development] afin que d’autres modifications puissent être apportées avant de redémarrer le flux de publication.

Le tableau suivant décrit les actions disponibles pour une bibliothèque à l’état [!UICONTROL Submitted] :

| Action | Description |
| --- | --- |
| [!UICONTROL Open] | Affichez le contenu de la bibliothèque. Les modifications ne sont pas autorisées pour les bibliothèques qui se trouvent en dehors de la colonne [!UICONTROL Development]. Si des modifications sont nécessaires, la bibliothèque doit être refusée afin que des modifications puissent être apportées dans l’état [!UICONTROL Development]. |
| [!UICONTROL Build for Staging] | Créez la bibliothèque dans l’environnement d’évaluation pour le déploiement. |
| [!UICONTROL Approve for Publishing] | Déplacez la bibliothèque dans la colonne [!UICONTROL Approved] pour permettre à un utilisateur disposant d’autorisations de publication de travailler dessus. |
| [!UICONTROL Approve & Publish to Production] | Cette opération ne peut être effectuée que par un utilisateur disposant des droits Approuver et Publier. Cette action annule l’affectation de la bibliothèque à partir de l’environnement d’évaluation, la déplace vers l’état [!UICONTROL Approved] et la publie en production. Une fois la création de l’environnement de production terminée, la bibliothèque passe à l’état [!UICONTROL Published]. Cela peut être effectué avec ou sans une version réussie dans l’environnement d’évaluation. |
| [!UICONTROL Reject] | Pour effectuer d’autres modifications, annulez l’attribution de la bibliothèque à partir de l’environnement d’évaluation et déplacez-la de nouveau dans la colonne [!UICONTROL Development]. |

### [!UICONTROL Approved] {#approved}

Une fois qu’une bibliothèque a été approuvée, un utilisateur disposant d’autorisations de publication peut la publier ou la refuser. Les versions refusées reviennent à l’état [!UICONTROL Development], de sorte que des modifications supplémentaires puissent être apportées avant que le flux de publication ne recommence.

Le tableau suivant décrit les actions disponibles pour une bibliothèque à l’état [!UICONTROL Approved] :

| Action | Description |
| --- | --- |
| [!UICONTROL Open] | Affichez le contenu de la bibliothèque. Les modifications ne sont pas autorisées pour les bibliothèques qui se trouvent en dehors de la colonne [!UICONTROL Development]. Si des modifications sont nécessaires, la bibliothèque doit être refusée afin de pouvoir apporter des modifications dans l’état [!UICONTROL Development]. |
| [!UICONTROL Build and Publish to Production] | Annulez l’attribution de la bibliothèque à son environnement d’évaluation, affectez-la à l’environnement de production et déployez-la.<br><br>**Important** : lorsque cette option est sélectionnée, votre bibliothèque est activée dans votre environnement de production. Assurez-vous que la bibliothèque contient les modifications souhaitées avant de sélectionner cette option. |
| [!UICONTROL Reject] | Annulez l’attribution de la bibliothèque à son environnement d’évaluation et déplacez-la dans la colonne [!UICONTROL Development] pour effectuer d’autres modifications. |

### [!UICONTROL Published] {#published}

La colonne [!UICONTROL Published] indique les bibliothèques qui ont été publiées et leurs dates de publication. La bibliothèque actuellement publiée s’affiche avec un point vert en regard de celle-ci. À moins que vous n’ayez effectué une republication sur une bibliothèque précédente, il s’agira toujours de la bibliothèque en haut de la colonne.

| Action | Description |
| --- | --- |
| [!UICONTROL Open] | Affichez le contenu de la bibliothèque. Les modifications ne sont pas autorisées pour les bibliothèques qui se trouvent en dehors de la colonne [!UICONTROL Development]. Si vous souhaitez modifier les éléments qui se trouvent dans votre environnement de production, vous devez créer une nouvelle bibliothèque et la déplacer tout au long du processus de publication. |
| [!UICONTROL Republish] | Cette action n’est disponible que sur les cinq bibliothèques publiées le plus récemment et uniquement si l’environnement de production est (A) configuré avec l’option Archiver désactivée et (b) utilise un hôte [!UICONTROL Managed by Adobe] au moment de la génération. |
| [!UICONTROL Download] | Cette action n’est disponible que sur les cinq bibliothèques publiées le plus récemment et uniquement si l’environnement de production est (A) configuré avec l’option Archiver sur et (b) utilise un hôte [!UICONTROL Managed by Adobe] au moment de la génération. |

## En amont {#upstream}

Après avoir publié votre première bibliothèque, comprendre le rôle des éléments en amont lorsque vous déplacez de nouvelles bibliothèques dans le flux de publication est important.

Si une bibliothèque se trouve actuellement à l’étape [!UICONTROL Development], [!UICONTROL Submitted] ou [!UICONTROL Approved], elle héritera des règles, des éléments de données et des extensions de toutes les bibliothèques en amont. Ces ressources héritées constituent une « ligne de base » pour chaque bibliothèque tandis qu’elles se déplacent dans le flux de publication. Dans l’absolu, vous pouvez simplement considérer chaque nouvelle bibliothèque comme une série de changements sur la ligne de base établie par les éléments en amont. Ainsi, aucun élément d’une bibliothèque précédente n’est écrasé de manière inattendue lors de la publication d’une nouvelle itération.

Ce qui est inclus en amont dépend de l’étape actuelle de la bibliothèque. Par exemple, les bibliothèques de la colonne [!UICONTROL Approved] héritent uniquement des ressources de la bibliothèque [!UICONTROL Published], tandis que les bibliothèques qui se trouvent dans l’état [!UICONTROL Development] héritent des ressources de toutes les autres colonnes.

![](./images/approval-workflow/upstream.png)

Lors de la modification d’une bibliothèque dans l’interface utilisateur, toutes les ressources héritées des éléments en amont sont représentées dans la section **[!UICONTROL Resources Upstream]** . Pour afficher ces ressources, sélectionnez l’onglet Développer situé sous l’en-tête de la section.

![](./images/approval-workflow/upstream-collapse.png)

La section se développe pour afficher les ressources individuelles héritées des éléments en amont. Vous pouvez utiliser le rail de gauche pour effectuer un filtrage entre les [!UICONTROL Rules], [!UICONTROL Data Elements] et [!UICONTROL Extensions], ou utiliser la barre de recherche pour rechercher une ressource spécifique à l’aide de son nom.

![](./images/approval-workflow/upstream-resources.png)

## Étapes suivantes

Ce guide fournit une présentation détaillée du flux de publication pour les bibliothèques dans Adobe Experience Platform. Pour en savoir plus sur la façon de publier vos bibliothèques, consultez la section [Présentation de la publication](./overview.md).
