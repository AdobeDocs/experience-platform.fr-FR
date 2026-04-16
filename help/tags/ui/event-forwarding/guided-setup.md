---
title: Configuration guidée du transfert d’événement
description: Découvrez comment configurer le transfert d’événement à l’aide de la configuration guidée.
source-git-commit: cc4abd44dc7fc5facd3011fbc533a08a55ebe33f
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 1%

---

# Présentation de la configuration guidée du transfert d’événement

>[!IMPORTANT]
>
>La fonction de configuration guidée est disponible pour les clients qui ont acheté le package Real-Time CDP Prime et Ultimate. Pour plus dʼinformations, contactez votre représentant commercial Adobe.

>[!NOTE]
>
>Tout client existant peut utiliser les workflows de configuration guidés pour créer une implémentation de référence qui peut être utilisée pour les éléments suivants :
>
>* Utilisez-le comme point de départ d’une toute nouvelle implémentation.
>* Utilisez-la comme une implémentation de référence que vous pouvez examiner pour voir comment elle a été configurée, puis répliquez-la dans vos implémentations de production actuelles.

La fonction de configuration guidée vous permet de configurer facilement et efficacement. Cet outil automatise plusieurs étapes exécutées dans les balises Adobe et le transfert d’événement, ce qui réduit considérablement le temps de configuration.

Cette configuration peut installer automatiquement des extensions. Cette implémentation hybride est recommandée par [!DNL Meta] pour collecter et transférer des conversions d’événement côté serveur. La fonctionnalité de configuration guidée est conçue pour vous aider à commencer une implémentation du transfert d’événement et n’est pas destinée à fournir une implémentation complète et fonctionnelle de bout en bout qui prend en charge tous les cas d’utilisation.

## Prise en main de la configuration guidée {#guided-setup}

Pour commencer à utiliser la fonctionnalité, sélectionnez **[!UICONTROL Get Started]** dans l’interface utilisateur de collecte de données **[!UICONTROL Event Forwarding]**.

![Page d’accueil du transfert d’événement affichant la carte Prise en main dans l’interface utilisateur de Collections de données](../../images/ui/guided-setup/get-started.png)

### Création d’une propriété de balises {#new-property}

Dans la section Configurer les propriétés , sélectionnez **[!UICONTROL New]** et saisissez les détails du nouveau **[!UICONTROL Property Domain]**.

![Configurer les propriétés affichant les détails du nouveau domaine](../../images/ui/guided-setup//configure-properties-new.png)

Sélectionnez **[!UICONTROL Add]** pour le [!DNL Meta Conversion API] dans la section Ajouter des extensions . Sur la page Configurer les informations de [!DNL Meta], vous avez la possibilité de saisir manuellement vos **[!UICONTROL Meta Pixel ID]**, **[!UICONTROL Meta System User Access Token]** et **[!UICONTROL Data Layer Path]**, ou d’utiliser l’option **[!UICONTROL Connect to Meta]**.

![Page Configurer les informations de Meta présentant l’option Se connecter à Meta ](../../images/ui/guided-setup/connect-to-meta.png)

#### Connexion à [!DNL Meta] à l’aide de vos informations d’identification {#meta-credentials}

Sélectionnez **[!UICONTROL Connect to Meta]**, puis saisissez vos informations d’identification [!DNL Meta] et sélectionnez **[!UICONTROL Log in]**, puis **[!UICONTROL Next]**.

Vous serez désormais invité à **Créer un portefeuille d’entreprise**. Saisissez le **[!UICONTROL Business portfolio name]** et sélectionnez **[!UICONTROL Next]**.

![Page Créer un portefeuille d’entreprise affichée avec un nom de portefeuille](../../images/ui/guided-setup/portfolio-name.png)

Sélectionnez votre portefeuille d’entreprise dans la liste, puis sélectionnez **[!UICONTROL Next]**. Vous pouvez voir les paramètres de Business Portfolio, de Compte publicitaire et de [!DNL Meta Pixel]. Sélectionnez **[!UICONTROL Continue]** pour confirmer les paramètres, puis sélectionnez **[!UICONTROL Next]**.

Patientez quelques minutes le temps que le processus de configuration se termine, puis sélectionnez **[!UICONTROL Done]**.

Vos **[!UICONTROL Meta Pixel ID]**, **[!UICONTROL Meta System User Access Token]** et **[!UICONTROL Data Layer Path]** seront automatiquement renseignés. Sélectionnez **[!UICONTROL Save]**.

![Page Configurer les informations Meta affichant les informations Meta renseignées](../../images/ui/guided-setup/meta-info.png)

#### Créer des ressources pour votre nouvelle propriété de balises {#create-resources}

Dans la section Créer des ressources , sélectionnez **[!UICONTROL Pre-check resources]** pour vérifier votre organisation et vos propriétés en ce qui concerne les collisions ou les ressources existantes nécessaires à votre implémentation.

![Création de ressources affichant les ressources de pré-vérification](../../images/ui/guided-setup/pre-check-resources.png)

La page Actions de tâche affiche une liste de tâches et d’actions. Sélectionnez **[!UICONTROL Create Resources]** pour créer ces tâches.

![Actions liées à la tâche avec la liste des tâches et actions à entreprendre](../../images/ui/guided-setup/create-resources.png)

Patientez quelques minutes le temps que les règles, éléments de données, extensions, bibliothèques, SDK, etc. requis terminent l’installation. La section Créer des ressources fournit des liens vers les propriétés et les ressources créées.

#### Validation de la mise en œuvre {#validate-implementation}

La section Valider l’implémentation fournit le lien intégré que vous pouvez utiliser sur votre site web. **[!UICONTROL Start Validation]** exécute le test dans la session en cours de votre navigateur sur cette page de configuration guidée. Si la validation réussit ici, la même implémentation doit fonctionner lorsque vous déployez le lien incorporé sur votre site.

Sélectionnez **[!UICONTROL Send PageView Event]** pour envoyer un événement de test via Adobe Experience Platform Edge Network. Il est ensuite transféré côté serveur vers [!DNL Meta]. Sélectionnez **[!UICONTROL Finished Validation]** pour terminer la configuration.

>[!NOTE]
>
>Si des échecs se produisent au cours du processus de validation, cliquez sur le lien **[!UICONTROL Assurance]** pour passer en revue les événements qui ont peut-être échoué.

![Page Validation affichant les résultats de la validation](../../images/ui/guided-setup/finished-validation.png)

### Utiliser une propriété de balises existante {#existing-property}

Dans la section Configurer les propriétés , sélectionnez **[!UICONTROL Existing]**, puis sélectionnez votre propriété Balises dans le menu déroulant. Le système tente de trouver la propriété de transfert d’événement déjà associée à cette propriété par le biais des flux de données. Vous pouvez maintenant continuer à reconfigurer le [!DNL Meta Conversion API], puis pré-vérifier et créer des ressources.

![Configurer une propriété existante affichant la propriété de balise existante sélectionnée](../../images/ui/guided-setup/configure-properties-existing.png)

Si la propriété de balises sélectionnée n’est pas connectée à une propriété de transfert d’événement ou si des flux de données sont manquants, ils sont automatiquement créés.

![Configurer une propriété existante affichant la propriété de balise existante sélectionnée](../../images/ui/guided-setup/configure-properties-existing-no-event-fw.png)

Pour configurer vos [!DNL Meta Conversion API], suivez le processus mis en évidence ci-dessus dans la [Se connecter à [!DNL Meta] à l’aide de vos informations d’identification](#meta-credentials).

Maintenant que vous avez généré des **[!UICONTROL Meta Pixel ID]**, des **[!UICONTROL Meta System User Access Token]** et des **[!UICONTROL Data Layer Path]**, sélectionnez **[!UICONTROL Pre-Check resources]** pour créer le workflow de transfert d’événement.

Étant donné que vous utilisez une propriété de balises existante, le processus de configuration diffère légèrement du workflow de la nouvelle propriété. Comme ils existent déjà, vous pouvez constater que le système ignore la création de la propriété web, de l’hôte et de l’environnement. Enfin, sélectionnez **[!UICONTROL Create Resources]** pour créer les tâches qui ne sont pas encore disponibles.

![Actions liées à la tâche avec la liste des tâches et actions à effectuer, en surlignant celles qui seront ignorées](../../images/ui/guided-setup/create-resources-skip.png)

>[!INFO]
>
>La configuration guidée ajoute automatiquement des notes aux propriétés qui sont mises à jour pendant le processus. Vous pouvez les afficher dans la section Notes du panneau de droite de la propriété Balises en mode d’édition. Vous pouvez voir quand la propriété a été mise à jour ou créée par l’outil de configuration guidée. Ce journal d’audit vous permet de suivre les modifications apportées par la fonction de configuration guidée.

Patientez quelques minutes le temps que les règles, éléments de données, extensions, bibliothèques, SDK, etc. requis terminent l’installation. La section Créer des ressources fournit des liens vers les propriétés et les ressources créées.

La section Valider l’implémentation fournit le lien intégré que vous pouvez utiliser sur votre site web. **[!UICONTROL Start Validation]** exécute le test dans la session en cours de votre navigateur sur cette page de configuration guidée. Si la validation réussit ici, la même implémentation doit fonctionner lorsque vous déployez le lien incorporé sur votre site.

Sélectionnez **[!UICONTROL Send PageView Event]** pour envoyer un événement de test via Adobe Experience Platform Edge Network. Il est ensuite transféré côté serveur vers [!DNL Meta]. Sélectionnez **[!UICONTROL Finished Validation]** pour terminer la configuration.

>[!NOTE]
>
>Si des échecs se produisent au cours du processus de validation, cliquez sur le lien **[!UICONTROL Assurance]** pour passer en revue les événements qui ont peut-être échoué.

![Page Validation affichant les résultats de la validation](../../images/ui/guided-setup/finished-validation.png)

## Étapes suivantes {#next-steps}

Ce guide explique comment utiliser l’outil de configuration guidé pour créer et configurer des propriétés pour le [!DNL Meta Conversions API].

Pour plus d’informations sur la mise en œuvre efficace de votre intégration[!DNL Meta][ consultez la documentation  [!DNL Conversions API] sur ](https://www.facebook.com/business/help/308855623839366?id=818859032317965)les bonnes pratiques relatives à . Pour des informations plus générales sur les balises et le transfert d’événement dans Adobe Experience Cloud, reportez-vous à la [présentation des balises](../../home.md).
