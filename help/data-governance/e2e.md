---
title: Guide complet sur la gouvernance des données
description: Suivez la procédure complète permettant d’appliquer des contraintes d’utilisation des données aux champs et jeux de données dans Adobe Experience Platform.
exl-id: f18ae032-027a-4c97-868b-e04753237c81
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: ht
source-wordcount: '1513'
ht-degree: 100%

---

# Guide complet sur la gouvernance des données

Pour déterminer les actions marketing pouvant être effectuées sur certains jeux de données et champs dans Adobe Experience Platform, vous devez au préalable réaliser les opérations suivantes :

1. [Appliquez des libellés](#labels) aux jeux de données et aux champs dont vous souhaitez restreindre l’utilisation.
1. [Configurez et activez les stratégies de gouvernance des données](#policy) qui déterminent les types de données libellées qui peuvent être utilisés pour certaines actions marketing.
1. [Appliquez des actions marketing à vos destinations](#destinations) pour indiquer les stratégies qui s’appliquent aux données envoyées vers ces destinations.

Une fois la configuration des libellés, des stratégies de gouvernance et des actions marketing terminée, vous pouvez [tester l’application de votre stratégie](#test) pour vous assurer qu’elle fonctionne comme prévu.

Ce guide aborde l’ensemble du processus de configuration et d’application d’une stratégie de gouvernance des données dans l’interface utilisateur de Platform. Pour des informations plus détaillées sur les fonctionnalités présentées dans ce guide, consultez la documentation de présentation pour les rubriques suivantes :

* [Gouvernance des données d’Adobe Experience Platform](./home.md)
* [Libellés d’utilisation des données](./labels/overview.md)
* [Stratégies d’utilisation des données](./policies/overview.md)
* [Application des stratégies](./enforcement/overview.md)

>[!NOTE]
>
>Ce guide est consacré à la configuration et à l’application des stratégies déterminant la manière dont les données sont utilisées ou activées dans Experience Platform. Si vous souhaitez restreindre l’**accès** aux données proprement dites de certains utilisateurs et utilisatrices de Platform au sein de votre organisation, consultez plutôt le guide complet sur le [contrôle d’accès basé sur les attributs](../access-control/abac/end-to-end-guide.md). Le contrôle d’accès basé sur les attributs utilise également des libellés et des stratégies, mais pour un cas d’utilisation différent de celui de la gouvernance des données.

## Appliquer des libellés {#labels}

Si vous souhaitez appliquer des contraintes d’utilisation des données à un jeu de données spécifique, vous pouvez [appliquer des libellés directement à ce jeu de données](#dataset-labels) ou à des champs spécifiques de celui-ci.

Vous pouvez également [appliquer des libellés à un schéma](#schema-labels) afin que tous les jeux de données basés sur ce schéma héritent des mêmes libellés.

>[!NOTE]
>
>Pour plus d’informations sur les différents libellés d’utilisation des données et leur utilisation prévue, consultez la [référence des libellés d’utilisation des données](./labels/reference.md). Si les libellés de base disponibles ne couvrent pas tous les cas d’utilisation souhaités, vous pouvez également [définir vos propres libellés personnalisés](./labels/user-guide.md#manage-custom-labels).

### Appliquer des libellés à un jeu de données {#dataset-labels}

Sélectionnez **[!UICONTROL Jeux de données]** dans le volet de navigation de gauche, puis cliquez sur le nom du jeu de données auquel appliquer des libellés. Vous pouvez également utiliser le champ de recherche pour réduire la liste des jeux de données affichés.

![Image montrant la sélection d’un jeu de données dans l’interface utilisateur de Platform.](./images/e2e/select-dataset.png)

La vue des détails du jeu de données s’affiche. Sélectionnez l’onglet **[!UICONTROL Gouvernance des données]** pour afficher la liste des champs du jeu de données et des libellés qui y ont déjà été appliqués. Cochez les cases en regard des champs auxquels vous souhaitez ajouter des libellés, puis sélectionnez **[!UICONTROL Modifier les libellés de gouvernance]** dans le rail de droite.

![Image montrant la sélection de plusieurs champs du jeu de données afin de les libeller.](./images/e2e/dataset-field-label.png)

>[!NOTE]
>
>Si vous souhaitez ajouter des libellés à l’ensemble du jeu de données, cochez la case en regard de **[!UICONTROL Nom du champ]** pour mettre en surbrillance tous les champs, puis sélectionnez **[!UICONTROL Modifier les libellés de gouvernance]**.
>
>![Image montrant la mise en surbrillance de l’ensemble des champs d’un jeu de données.](./images/e2e/label-whole-dataset.png)

Dans la boîte de dialogue suivante, sélectionnez les libellés à appliquer aux champs du jeu de données que vous avez choisis à l’étape précédente. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer les modifications]**.

![Image montrant la mise en surbrillance de l’ensemble des champs d’un jeu de données.](./images/e2e/save-dataset-labels.png)

Répétez les étapes ci-dessus pour appliquer des libellés à différents champs (ou à différents jeux de données) si nécessaire. Lorsque vous avez terminé, vous pouvez passer à l’étape suivante et commencer à [activer des stratégies de gouvernance des données](#policy).

### Appliquer des libellés à un schéma {#schema-labels}

Sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche, puis choisissez le schéma auquel vous souhaitez ajouter des libellés dans la liste.

>[!TIP]
>
>Si vous ne savez pas quel schéma s’applique à un jeu de données spécifique, sélectionnez **[!UICONTROL Jeux de données]** dans le volet de navigation de gauche, puis cliquez sur le lien situé sous la colonne **[!UICONTROL Schéma]** pour le jeu de données souhaité. Sélectionnez le nom du schéma dans la fenêtre contextuelle qui s’affiche pour ouvrir le schéma dans l’éditeur de schémas.
>
>![Image montrant un lien vers le schéma d’un jeu de données.](./images/e2e/schema-from-dataset.png)

La structure du schéma s’affiche dans l’éditeur de schémas. Dans cet écran, sélectionnez l’onglet **[!UICONTROL Libellés]** pour afficher une vue en mode liste des champs du schéma et des libellés qui y ont déjà été appliqués. Cochez les cases en regard des champs auxquels vous souhaitez ajouter des libellés, puis sélectionnez **[!UICONTROL Modifier les libellés de gouvernance]** dans le rail de droite.

![Image montrant la sélection d’un champ de schéma unique pour lui appliquer des libellés de gouvernance.](./images/e2e/schema-field-label.png)

>[!NOTE]
>
>Si vous souhaitez ajouter des libellés à tous les champs du schéma, sélectionnez l’icône en forme de crayon sur la ligne supérieure.
>
>![Image montrant la sélection de l’icône en forme de crayon dans la vue des libellés du schéma.](./images/e2e/label-whole-schema.png)

Dans la boîte de dialogue suivante, sélectionnez les libellés à appliquer aux champs de schéma que vous avez choisis dans une étape précédente. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

![Image montrant l’ajout de plusieurs libellés à un champ de schéma.](./images/e2e/save-schema-labels.png)

Répétez les étapes ci-dessus pour appliquer des libellés à différents champs (ou à différents schémas) si nécessaire. Lorsque vous avez terminé, vous pouvez passer à l’étape suivante qui consiste à [activer les stratégies de gouvernance des données](#policy).

## Activer les stratégies de gouvernance des données {#policy}

Une fois l’application des libellés à vos schémas et/ou jeux de données terminée, vous pouvez commencer à créer des stratégies de gouvernance des données qui limitent les actions marketing pour lesquelles certains libellés peuvent être utilisés.

Sélectionnez **[!UICONTROL Stratégies]** dans le volet de navigation de gauche pour afficher la liste des stratégies de base définies par Adobe, ainsi que les stratégies personnalisées créées précédemment par votre organisation.

Chaque libellé principal est associé à une stratégie de base qui, lorsqu’elle est activée, impose les contraintes d’activation appropriées sur toutes données qui contiennent ce libellé. Pour activer une stratégie de base, sélectionnez-la dans la liste, puis positionnez **[!UICONTROL Statut de la stratégie]** sur **[!UICONTROL Activé]**.

![Image montrant une stratégie de base activée dans l’interface utilisateur.](./images/e2e/enable-core-policy.png)

Si les stratégies de base disponibles ne couvrent pas tous vos cas d’utilisation (par exemple lorsque vous utilisez des libellés personnalisés que vous avez définis sous votre organisation), vous pouvez définir une stratégie personnalisée à la place. Dans l’espace de travail **[!UICONTROL Stratégies]**, sélectionnez **[!UICONTROL Créer une stratégie]**.

![Image montrant le bouton [!UICONTROL Créer une stratégie] en cours de sélection dans l’interface utilisateur.](./images/e2e/create-policy.png)

Une fenêtre contextuelle s’affiche, vous invitant à sélectionner le type de stratégie que vous souhaitez créer. Sélectionnez **[!UICONTROL Statégie de gouvernance des données]**, puis sélectionnez **[!UICONTROL Continuer]**.

![Image montrant l’option [!UICONTROL Stratégie de gouvernance des données] sélectionnée.](./images/e2e/governance-policy.png)

Sur l’écran suivant, fournissez un **[!UICONTROL Nom]** et une **[!UICONTROL Description]** facultative pour la stratégie. Dans le tableau ci-dessous, sélectionnez les libellés sur lesquels cette stratégie s’appliquera. En d’autres termes, il s’agit des libellés dont la stratégie empêchera l’utilisation pour les actions marketing de l’étape suivante.

Si vous sélectionnez plusieurs libellés, vous pouvez utiliser les options du rail de droite pour déterminer si tous les libellés doivent être présents pour que la stratégie applique les restrictions d’utilisation, ou si un seul d’entre eux doit être présent. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![Image montrant la configuration de base de la stratégie accomplie dans l’interface utilisateur.](./images/e2e/configure-policy.png)

Dans l’écran suivant, sélectionnez les actions marketing pour lesquelles cette stratégie limitera l’utilisation pour les libellés sélectionnés précédemment. Sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Image montrant une action marketing affectée à une stratégie dans l’interface utilisateur.](./images/e2e/select-marketing-action.png)

Le dernier écran affiche un résumé avec les détails de la stratégie et les actions qu’elle restreint pour chaque libellé. Sélectionnez **[!UICONTROL Terminer]** pour créer la stratégie.

![Image montrant la confirmation de configuration de la stratégie dans l’interface utilisateur.](./images/e2e/confirm-policy.png)

La stratégie est créée, mais est définie sur [!UICONTROL Désactivée] par défaut. Sélectionnez la stratégie dans la liste et définissez le bouton de **[!UICONTROL Statut de la stratégie]** sur **[!UICONTROL Activé]** pour activer la stratégie.

![Image montrant la nouvelle stratégie activée dans l’interface utilisateur.](./images/e2e/enable-created-policy.png)

Continuez à suivre les étapes ci-dessus pour créer et activer les stratégies dont vous avez besoin avant de passer à l’étape suivante.

## Gérer les actions marketing pour les destinations {#destinations}

Pour que vos stratégies activées déterminent avec précision les données qui peuvent être activées vers une destination, vous devez affecter des actions marketing spécifiques à cette destination.

Prenons l’exemple d’une stratégie activée qui empêche toute donnée contenant un libellé `C2` d’être utilisée pour l’action marketing « [!UICONTROL Exporter vers un tiers] ». Lors de l’activation de données vers une destination, la stratégie identifie quelles actions marketing sont présentes sur la destination. Si l’action « [!UICONTROL Exporter vers un tiers] » est présente, une tentative d’activation de données avec un libellé `C2` se traduit par une violation de la stratégie. Si l’action « [!UICONTROL Exporter vers un tiers] » n’est pas présente, la stratégie n’est pas appliquée pour la destination et les données avec les libellés `C2` peuvent être librement activées.

Lorsque vous effectuez la [connexion d’une destination dans l’interface utilisateur](../destinations/ui/connect-destination.md), l’étape **[!UICONTROL Gouvernance]** du workflow vous permet de sélectionner les actions marketing qui s’appliquent à cette destination, ce qui détermine en fait les stratégies de gouvernance des données appliquées à la destination.

![Image montrant les actions marketing sélectionnées pour une destination.](./images/e2e/destination-marketing-actions.png)

## Tester l’application des stratégies {#test}

Une fois que vous avez libellé vos données, activé les stratégies de gouvernance des données et affecté des actions marketing à vos destinations, vous pouvez tester si vos stratégies sont appliquées comme prévu.

Si vous configurez les éléments correctement, lorsque vous tentez d’activer des données qui sont restreintes par vos stratégies, l’activation est automatiquement refusée et un message de violation de la stratégie s’affiche, présentant un historique détaillé des données et les causes de la violation.

Consultez le document [application automatique des stratégies](./enforcement/auto-enforcement.md) pour savoir en détail comment interpréter les messages de violation de stratégie.

## Étapes suivantes

Ce guide décrit les étapes nécéssaires pour configurer et appliquer des stratégies de gouvernance des données dans vos workflows d’activation. Pour plus d’informations sur les composants de gouvernance des données impliqués dans ce guide, consultez la documentation suivante :

* [Libellés d’utilisation des données](./labels/overview.md)
* [Stratégies d’utilisation des données](./policies/overview.md)
* [Application des stratégies](./enforcement/overview.md)
