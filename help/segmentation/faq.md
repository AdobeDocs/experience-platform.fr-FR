---
title: Questions fréquentes sur les audiences
description: Découvrez les réponses aux questions fréquentes sur les audiences et d’autres concepts liés à la segmentation.
exl-id: 79d54105-a37d-43f7-adcb-97f2b8e4249c
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '4096'
ht-degree: 22%

---

# Questions fréquentes

L’interface utilisateur et l’API RESTful du [!DNL Segmentation Service] d’Adobe Experience Platform vous permettent de créer des audiences par le biais de définitions de segment ou d’autres sources à partir de vos données [!DNL Real-Time Customer Profile]. Ces audiences sont configurées et conservées de manière centralisée sur Platform et sont facilement accessibles à partir de n’importe quelle solution Adobe. Vous trouverez ci-dessous les questions fréquentes sur les audiences et la segmentation.

## Audience Portal

La section suivante répertorie les questions relatives à Audience Portal.

### Puis-je accéder au portail d’audience et à la composition d’audience ?

Le portail d’audience et la composition d’audience sont disponibles pour tous les clientes et clients Real-Time CDP Prime et Ultimate (éditions B2C, B2B et B2P) et Journey Optimizer Select, Prime, Ultimate Starter et Ultimate.

Dans la version la plus récente de l’application, seules les audiences basées sur un profil sont prises en charge. La prise en charge des audiences basées sur un compte sera assurée dans une version ultérieure.

### Les audiences préconfigurées générées en externe sont-elles prises en charge par le portail d’audience ?

Oui, les audiences préconfigurées générées en externe sont prises en charge par le portail d’audience. Dans la version la plus récente de l’application, vous pouvez importer une audience générée en externe par le biais d’un fichier CSV. Dans une version ultérieure, vous pourrez ajouter des audiences par le biais de connecteurs source par lots ou en flux continu.

### Quelles autorisations dois-je posséder pour charger des audiences générées en externe ?

Pour charger des audiences générées en externe, vous devez disposer des autorisations &quot;Afficher les segments&quot;, &quot;Gérer les segments&quot; et &quot;Importer des audiences&quot;. Aucun contrôle spécifique basé sur les rôles n’est nécessaire pour charger des audiences générées en externe.

### Que se passe-t-il lorsque je charge une audience générée en externe ?

Lorsque vous téléchargez une audience générée de l’extérieur, les éléments suivants sont créés :

- Jeu de données
   - Le jeu de données sera visible dans l’inventaire du jeu de données et le nom du jeu de données sera le **même** que le nom de l’audience générée en externe que vous avez chargée.
- Tâche par lots
   - Une tâche par lots s’exécute **automatiquement** lorsque vous chargez une audience générée en externe. Cela signifie que vous n’avez **pas** besoin d’attendre l’exécution de la tâche de segmentation quotidienne pour activer l’audience générée en externe.
- Schéma ad hoc
   - Un schéma XDM **new** sera créé pour être utilisé avec l’audience générée en externe. Les champs de ce schéma XDM peuvent être utilisés avec le jeu de données qui a également été créé.

### Qu’est-ce qu’une audience générée en externe comprend et qu’advient-il de ces données lorsqu’elles sont importées dans Platform ?

Au cours du workflow d&#39;import d&#39;audience externe, vous devez spécifier la colonne du fichier CSV correspondant à l&#39; **identité de Principal**. Un exemple d’identité principale inclut une adresse électronique, un ECID ou un espace de noms d’identité personnalisée spécifique à l’organisation.

Les données associées à cette identité principale contiennent les données **uniquement** qui sont jointes au profil. Si aucun profil existant ne correspond aux données de la colonne Identité principale, un nouveau profil est créé. Cependant, ce profil est essentiellement un profil orphelin, car les attributs **no** ou les événements d’expérience sont associés à ce profil.

Toutes les autres données de l’audience générée en externe sont considérées comme des **attributs de payload**. Ces attributs peuvent **uniquement** être utilisés pour la personnalisation et l’enrichissement lors de l’activation et sont **non** associés à un profil. Ces attributs sont toutefois stockés dans le lac de données.

Bien que l’audience générée en externe puisse être référencée lors de la création d’audiences à l’aide du créateur de segments, les attributs de profil individuels **ne peuvent pas** être utilisés.

### Puis-je réconcilier des données d’audience générées en externe avec un profil existant dans Platform ?

Oui, l’audience générée en externe sera fusionnée avec le profil existant dans Platform si les identifiants principaux correspondent. La réconciliation des données peut prendre jusqu’à 24 heures. Si les données de profil n’existent pas déjà, un profil est créé lors de l’ingestion des données.

### Puis-je utiliser une audience générée en externe pour créer d’autres audiences ?

Oui, les audiences générées en externe apparaîtront dans l’inventaire des audiences. elles peuvent être utilisés lors de la création d’audiences dans le [Créateur de segments](./ui/segment-builder.md).

### Puis-je utiliser des attributs téléchargés en externe dans le cadre de la segmentation ?

Non. Les attributs de profil sont censés être des attributs durables, tandis que les données d’audience générées en externe qui sont chargées ne contiennent que des données contextuelles associées à cette audience générée en externe.

Les données contextuelles de l’audience générée en externe, ou attributs d’enrichissement, possèdent une durée de vie **limitée**, car leur cycle de vie est lié à l’audience téléchargée. En raison de leur caractère éphémère, les attributs d’enrichissement ne sont **pas** disponibles dans la segmentation.

Cependant, lorsque vous mappez vos audiences vers des destinations par lots ou basées sur des fichiers, vous pouvez utiliser ces attributs d’enrichissement générés en externe pour élargir vos audiences et accroître les activations en aval.

Pour en savoir plus sur cette fonctionnalité, consultez le guide de l’[activation des données d’audience vers des destinations d’exportation de profils par lots](../destinations/ui/activate-batch-profile-destinations.md#mapping).

### Existe-t-il une stratégie de fusion spécifique pour les audiences générées en externe ?

La stratégie de fusion par défaut propre à l’organisation est automatiquement appliquée lors du téléchargement d’audiences générées en externe. Vous pouvez toutefois modifier la stratégie de fusion appliquée à l’audience générée en externe au cours du workflow d’import d’audience.

### Où puis-je activer les audiences générées en externe vers ?

Une audience générée en externe peut être mappée à n’importe quelle destination RTCDP et peut être utilisée dans des campagnes Adobe Journey Optimizer.

### Dans combien de temps les audiences générées en externe sont-elles prêtes à être activées ?

Si cette option est activée vers une destination de diffusion en continu, les données de l’audience générée en externe sont disponibles dans les deux heures.

S’il est activé sur une destination par lot, les données de l’audience générée en externe seront synchronisées avec la tâche de segmentation de 24 heures suivante.

### Puis-je supprimer une audience générée en externe ?

Oui! Les audiences générées de manière externe peuvent être supprimées dans Audience Portal.

### Que dois-je faire si j’ai téléchargé accidentellement une audience générée en externe ?

Si vous avez accidentellement chargé une audience générée en externe et que vous souhaitez supprimer les données, vous pouvez effacer les profils associés à l’audience en chargeant un fichier CSV avec une ligne et aucune donnée.

### Combien de temps durent les audiences générées en externe ?

L’expiration actuelle des données pour les audiences générées en externe est de **30 jours**. Cette expiration de données a été choisie pour réduire la quantité de données excédentaires stockées au sein de votre organisation.

Une fois la période d’expiration des données écoulée, le jeu de données associé sera toujours visible dans l’inventaire du jeu de données, mais vous **not** pourrez activer l’audience et le nombre de profils s’affichera comme nul.

### Comment le portail d’audience et la composition d’audience interagiront-ils avec les données du partenaire Real-Time CDP ?

Le portail d’audience et la composition d’audience interagissent avec les données du partenaire de deux manières :

1. Si vous ingérez une liste de prospects fournie par le partenaire à l’aide de la classe et du workflow Prospect Profile, les prospects seront conservés **séparément** des profils clients de fusion dans le Profile Service. Cela signifie que les listes de prospects ne seront **pas** disponibles dans le portail d’audience ou dans la composition d’audience.
2. Si vous tirez parti des attributs fournis par le partenaire pour enrichir les profils propriétaires **existants**, ces audiences enrichies en données de partenaire **seront** disponibles dans le portail d’audience et dans la composition d’audience pour être utilisées.

### Comment utiliser des attributs supplémentaires avec mes audiences ?

Avec les audiences, il existe **deux** différents types d’attributs supplémentaires que vous pouvez ajouter : attributs de payload (contextuels) et attributs d’enrichissement.

Les attributs de payload sont des attributs ingérés dans le cadre du chargement au format CSV d’une audience générée de l’extérieur. Ces attributs sont **non** ingérés dans le profil client en temps réel, mais peuvent être utilisés comme partie d’une destination en aval.

Les attributs d’enrichissement sont des attributs qui proviennent d’un jeu de données et qui sont associés à une audience dans la composition de l’audience. Actuellement, ces attributs ne peuvent être utilisés que dans les campagnes Adobe Journey Optimizer. La prise en charge des parcours Adobe Journey Optimizer est bientôt disponible, avec la prise en charge des destinations en aval dans l’attente d’une version ultérieure.

| Canal d’activation | Audiences à partir d’un téléchargement personnalisé CSV | Audiences de la composition de l’audience |
| --- | --- | --- |
| Destinations Real-Time CDP | Les attributs de payload et les audiences peuvent être activés. | Seule l’audience peut être activée. Les attributs d’enrichissement **ne peuvent pas** être activés. |
| Campagnes Adobe Journey Optimizer | Ni l’audience ni les attributs de payload ne peuvent être activés. | Les attributs audience et enrichissement peuvent être activés. |

## États du cycle de vie {#lifecycle-states}

La section suivante répertorie les questions relatives aux états du cycle de vie et à la gestion de l’état du cycle de vie dans Audience Portal.

### Que représentent les différents états du cycle de vie ?

Le graphique suivant explique les différents états du cycle de vie, ce qu’ils représentent, où les audiences avec cet état peuvent être utilisées, ainsi que l’impact sur les barrières de sécurité de segmentation.

| État | Définition | Visible dans Audience Portal ? | Visible dans les destinations ? | Affecte les limites de segmentation ? | Impact sur les audiences basées sur des fichiers | Impact sur l’évaluation des audiences | Utilisable dans d’autres audiences ? | Modifiable |
| --- | --- | --- | --- | --- | --- | --- | --- | -- |
| Brouillon | Une audience dans l’état **Draft** est une audience qui est encore en cours de développement et qui n’est pas encore prête à être utilisée dans d’autres services. | Oui, mais peut être caché. | Non | Oui | Peuvent être importées ou mises à jour pendant le processus d’affinage. | Évalués pour obtenir des comptes de publication précis. | Oui, mais non recommandé. | Oui |
| Publié | Une audience à l’état **Publiée** est une audience prête à être utilisée sur tous les services en aval. | Oui | Oui | Oui | Peut être importé ou mis à jour. | Évalués à l’aide de la segmentation par lots, par flux ou par périphérie. | Oui | Oui |
| Inactif | Une audience à l’état **Inactive** est une audience qui n’est actuellement pas utilisée. Il existe toujours dans Platform, mais **pas** pourra être utilisé jusqu’à ce qu’il soit marqué comme brouillon ou publié. | Non, mais peut être affiché. | Non | Non | N’est plus mis à jour. | N’est plus évalué ou mis à jour par Platform. | Non | Oui |
| Supprimé | Une audience à l’état **Supprimée** est une audience qui a été supprimée. L’exécution de la suppression des données peut prendre jusqu’à quelques minutes. | Non | Non | Non | Les données sous-jacentes sont supprimées. | Aucune évaluation ou exécution des données n’a lieu une fois la suppression terminée. | Non | Non |

### Dans quels états puis-je modifier mes audiences ?

Les audiences peuvent être modifiées dans les états de cycle de vie suivants :

- **Version préliminaire** : si une audience est modifiée à l’état préliminaire, elle reste à l’état préliminaire sauf si elle est publiée explicitement.
- **Publié** : si une audience est modifiée à l’état publié, elle reste publiée et l’audience est automatiquement mise à jour.
- **Inactive** : si une audience est modifiée à l’état inactif, elle reste inactive. Cela signifie qu’il ne sera pas évalué ni mis à jour. Si vous devez mettre à jour l’audience, vous devez la publier.

Une fois qu’une audience est supprimée, elle **ne peut pas** être modifiée.

### À quels états de cycle de vie puis-je déplacer une audience ?

Le cycle de vie possible indique qu’une audience peut être déplacée en fonction de l’état actuel de l’audience.

![ Diagramme décrivant les transitions possibles de l’état de cycle de vie disponibles pour les audiences.](./images/faq/lifecycle-state-transition.png)

Si votre audience est à l’état de brouillon, vous pouvez la publier ou la supprimer si elle n’a aucune dépendance.

Si votre audience est à l’état publié, vous pouvez la désactiver ou la supprimer si elle n’a aucune dépendance.

Si votre audience est à l’état inactif, vous pouvez la republier ou la supprimer si elle n’a aucune dépendance.

### Existe-t-il des avertissements pour les audiences dans certains états de cycle de vie ?

Les audiences dans l’état publié ne peuvent être déplacées vers un autre état que si l’audience **et non** a des dépendances. Cela signifie que si votre audience est utilisée dans un service en aval, elle ne peut pas être désactivée ni supprimée.

Si une audience évaluée à l’aide de la segmentation par lots est republiée, c’est-à-dire lorsqu’une audience passe d’inactive à publiée, l’audience actualise **après** la tâche par lots quotidienne. Lors de sa première republication, les profils et les données sont **identiques** comme lorsque l’audience a été inactive.

### Comment placer une audience dans l’état de brouillon ?

La méthode pour placer une audience dans l’état de brouillon dépend de l’origine de l’audience.

Pour les audiences créées à l’aide du créateur de segments, vous pouvez définir l’audience sur l’état de brouillon en sélectionnant &quot;[!UICONTROL Enregistrer en tant que brouillon]&quot; dans le créateur de segments.

Pour les audiences créées dans la composition de l’audience, les audiences sont automatiquement enregistrées en tant que brouillon jusqu’à publication.

Pour les audiences créées en externe, les audiences sont automatiquement publiées.

Une fois qu’une audience est à l’état publié, vous **ne pouvez pas** redéfinir l’audience d’origine en état de brouillon. Cependant, si vous copiez l’audience nouvellement copiée, elle se trouve à l’état de brouillon.

### Comment placer une audience dans l’état publié ?

Pour les audiences créées à l’aide du créateur de segments ou de la composition de l’audience, vous pouvez définir l’audience sur l’état publié en sélectionnant &quot;[!UICONTROL Publish]&quot; dans leurs interfaces utilisateur respectives.

Les audiences créées en externe sont automatiquement définies sur la publication.

### Comment placer une audience à l’état inactif ?

Vous pouvez placer une audience publiée dans l’état inactif en ouvrant le menu des actions rapides dans Audience Portal et en sélectionnant &quot;[!UICONTROL Désactiver]&quot;.

### Comment republier une audience ?

>[!NOTE]
>
>L’état &quot;republié&quot; est identique à l’état publié pour le comportement de l’audience.

Vous pouvez republier une audience en sélectionnant une audience inactive, en ouvrant le menu des actions rapides sur Audience Portal et en sélectionnant [!UICONTROL Publish].

### Comment placer une audience dans l’état supprimé ?

>[!IMPORTANT]
>
>Vous ne pouvez supprimer que les audiences **et non** utilisées dans les activations en aval. De plus, vous ne pouvez pas supprimer une audience référencée dans une autre audience. Si vous ne pouvez pas supprimer votre audience, assurez-vous que vous ne l’utilisez **pas** dans les services en aval ou comme bloc de création d’une autre audience.

Vous pouvez placer une audience dans l’état de suppression en ouvrant le menu des actions rapides dans Audience Portal et en sélectionnant [!UICONTROL Supprimer].

### Existe-t-il des avertissements pour les transitions d’état de cycle de vie ?

Oui, vous devez tenir compte de certains avertissements lorsque vous utilisez des audiences dans des services en aval tels que Adobe Journey Optimizer ou des audiences non basées sur les clients telles que les audiences basées sur un compte.

Actuellement, vous **devez** vérifier manuellement si l’audience est utilisée en aval dans Adobe Journey Optimizer, car ce statut n’est actuellement pas automatiquement vérifié.

De plus, vous **devez** vérifier manuellement si l’audience est utilisée comme composant d’une audience basée sur un compte, car ce statut n’est pas actuellement vérifié automatiquement.

### Que se passe-t-il lorsque je copie une audience ? {#copy}

Lorsque vous copiez une audience, la nouvelle audience se trouve à l’état de brouillon et conserve les mêmes dossiers, balises et libellés qui ont été appliqués à l’audience d’origine.

### L’utilisation d’une audience en tant qu’audience enfant affecte-t-elle les transitions d’état de cycle de vie ?

>[!NOTE]
>
>Une audience parente est une audience que **utilise** une autre audience comme dépendance de l’audience.
>
>Une audience enfant est une audience **utilisée comme** une dépendance pour l’audience.

Oui, l’utilisation d’une audience en tant qu’audience enfant affecte les états de cycle de vie des transitions que peuvent entreprendre l’audience enfant et parente.

Pour qu’une audience enfant soit déplacée vers l’état publié, l’ensemble de l’audience parent **doit** se trouve dans l’état publié. Les audiences parents peuvent être publiées avant la publication de l’audience enfant ou, si l’utilisateur le confirme, peuvent être automatiquement publiées lorsque l’audience enfant est publiée.

Pour que l’audience parent soit déplacée vers l’état inactif ou supprimé, toutes ses audiences enfants **doivent** être désactivées ou supprimées.

### Puis-je faire référence à une audience dont l’état de cycle de vie est différent ?

Oui! Si votre audience se trouve actuellement à l’état de brouillon, vous pouvez vous référer aux audiences à l’état de brouillon ou de publication. Cependant, pour publier cette audience, vous **devez** publier les autres audiences parentes.

## Inventaire de l’audience

La section suivante répertorie les questions relatives à l’inventaire des audiences dans Audience Portal.

### Ai-je besoin d’autorisations supplémentaires pour utiliser les fonctionnalités d’inventaire des audiences ?

Non, ce n&#39;est pas le cas. Tant que vous disposez des autorisations de modification des audiences, vous pouvez créer, mettre à jour et gérer vos dossiers et balises dans le portail Audience. Pour plus d’informations sur la gestion des autorisations, consultez le [guide de gestion des autorisations](../access-control/ui/permissions.md).

### Le nombre de dossiers que je peux créer est-il limité ?

Non, le nombre de dossiers que vous pouvez créer n’est pas limité. Pour plus d’informations sur les dossiers, consultez la [section d’inventaire des audiences](./ui/audience-portal.md#folders) de la présentation de l’interface utilisateur de Segmentation Service.

### Le nombre de balises pouvant être ajoutées à une audience est-il limité ?

Non, il n’existe pas de limite au nombre de balises pouvant être ajoutées à une audience. Pour plus d’informations sur les balises, consultez la [section d’inventaire des audiences](./ui/audience-portal.md#tags) de la présentation de l’interface utilisateur de Segmentation Service.

### Le nombre de balises que je peux créer est-il limité ?

Non, il n’y a pas de limite au nombre de balises que vous pouvez créer. Cependant, vous pouvez créer un maximum de catégories **100** à appliquer aux balises. Pour plus d’informations sur la gestion des balises, consultez le [guide de gestion des balises](../administrative-tags/ui/managing-tags.md).

### Lorsque je recherche une audience par nom ou balise dans un dossier parent, puis-je également effectuer une recherche dans les dossiers enfants associés ?

Non, ce comportement n’est pas pris en charge. Cependant, vous pouvez modifier la vue d’inventaire des audiences pour consulter **Toutes les audiences**, puis effectuer une recherche dans tous les dossiers. Pour plus d’informations sur l’utilisation de la recherche dans l’inventaire des audiences, consultez la [section de recherche](./ui/audience-portal.md#search) de la présentation de l’interface utilisateur de Segmentation Service.

### Puis-je affecter automatiquement une audience à un dossier au moment de sa création ?

À ce stade, non. Toutefois, cette fonctionnalité pourrait être disponible à l’avenir.

### Puis-je déplacer plusieurs audiences simultanément dans un dossier ?

À ce stade, non. Toutefois, cette fonctionnalité pourrait être disponible à l’avenir.

## Composition de l’audience

La section suivante répertorie les questions relatives à la composition de l’audience.

### Quand dois-je utiliser la composition de l’audience plutôt que le créateur de segments ?

La composition de l’audience et le créateur de segments ont des rôles importants dans la création d’audiences dans Platform.

Le créateur de segments est plus adapté à la **création** de l’audience (pour créer une audience à partir de zéro), tandis que la composition de l’audience est plus adaptée à la **conservation et personnalisation** de l’audience (pour créer de nouvelles audiences basées sur une audience existante).

Le tableau suivant illustre la différence entre les deux services :

| Créateur de segments | Composition de l’audience |
| --------------- | -------------------- |
| <ul><li>Génération d’audiences à un seul niveau</li><li>Crée les blocs de base d’audiences à partir de données de profil, de séries temporelles et multi-entités.</li><li>Utilisé pour créer une audience **une**</li></ul> | <ul><li>Génération d’audiences à plusieurs étapes, à l’aide d’opérations basées sur des ensembles</li><li>Utilise les audiences créées par le créateur de segments et applique les options d’enrichissement de données telles que le classement des attributs de profil et la division en sous-audiences</li><li>Utilisé pour créer **plusieurs** audiences à la fois</li></ul> |

Pour en savoir plus sur le créateur de segments, consultez le [guide du créateur de segments](./ui/segment-builder.md). Pour en savoir plus sur la composition de l’audience, consultez le [guide sur la composition de l’audience](./ui/audience-composition.md).

### Puis-je utiliser des audiences générées en externe dans la composition de l’audience ?

À ce stade, non. Cette fonctionnalité sera disponible dans un avenir proche.

### Puis-je envoyer des audiences de la composition d’audience à toutes les destinations et tous les canaux en aval ?

À ce stade, non. Actuellement, vous pouvez utiliser les audiences de la composition de l’audience dans les campagnes Adobe Journey Optimizer et les destinations Real-Time CDP. Les parcours Adobe Journey Optimizer seront pris en charge dans une version ultérieure.

### Existe-t-il des barrières de sécurité qui limitent le nombre de compositions ?

À ce stade, la limite est fixée à **10** compositions publiées par sandbox. Ce nombre devrait augmenter dans une prochaine version.

### Quelles sont les barrières de sécurité du workflow de composition d’audience ?

Le placement du composant de composition suit une structure rigide comme suit :

1. Vous commencez **toujours** par le bloc [!UICONTROL Audience] pour sélectionner votre activité de départ. Vous pouvez avoir un maximum d’**un** bloc [!UICONTROL Audience].
2. Vous pouvez éventuellement ajouter un bloc [!UICONTROL Exclure] qui suit le bloc [!UICONTROL Audience].
3. Vous pouvez éventuellement ajouter un bloc [!UICONTROL Enrichir] qui suit le bloc [!UICONTROL Exclure]. Vous ne pouvez utiliser que **un** [!UICONTROL bloc Enrichir] par composition.
4. Vous pouvez éventuellement ajouter un bloc [!UICONTROL Classer] ou [!UICONTROL Partager]. Vous pouvez **uniquement** avoir l’un de ces blocs par composition.
5. Vous terminez **toujours** par un bloc [!UICONTROL Enregistrer] pour enregistrer votre audience.

En outre, les restrictions suivantes(?) appliquer lors de l’utilisation de ces blocs :

- Bloc de partage
   - Ce bloc ne prend en charge que les types de données **String**. Le bloc de partage ne prend **pas** en charge la date ou le type de données booléen.
   - De plus, ce bloc ne prend pas en charge les attributs d&#39;enrichissement **et non**.
- Exclure le bloc
   - Ce bloc ne prend **pas** en charge la date ou le type de données booléen.
- Bloc de classement
   - Ce bloc ne prend **pas** en charge les attributs d&#39;enrichissement.

Pour plus d’informations sur l’utilisation de la composition de l’audience, lisez le [Guide de l’interface utilisateur de la composition d’audience](./ui/audience-composition.md).

### Quand les audiences sont-elles créées à l’aide de la composition de l’audience enregistrée et évaluée ?

Les audiences sont automatiquement enregistrées lors de leur création dans la composition de l’audience. L’heure de création de l’audience sera la première fois que cet enregistrement automatique se produit.

Une fois l’audience créée, l’évaluation peut prendre jusqu’à 24 heures.

### Quand puis-je utiliser l’audience que j’ai créée ?

L’audience créée dans la composition de l’audience s’affichera **immédiatement** dans Audience Portal. Toutefois, pour l’utiliser dans Adobe Journey Optimizer, vous devez attendre au moins 24 heures après l’évaluation.

### Les tâches d’évaluation sont-elles visibles dans la section de surveillance ?

À l’heure actuelle, les tâches d’évaluation ne sont **pas** affichées dans l’interface utilisateur de surveillance.

### Puis-je utiliser une composition d’audience dans une autre composition ?

Non, les audiences créées à l’aide de la composition de l’audience **ne peuvent pas** être utilisées comme entrée dans une autre composition d’audience.

### Comment le partage fonctionne-t-il dans la composition de l’audience ?

Le fractionnement de l’audience vous permet de sous-définir davantage votre audience en groupes plus petits.

En se divisant par attribut, il existe une exclusivité mutuelle entre les groupes. Cela signifie que si un enregistrement répond aux critères de plusieurs chemins de partage, le **premier** chemin à partir de la gauche lui sera attribué et **pas** l’un des autres chemins.

Lors de la division par pourcentage, les divisions sont **aléatoirement** effectuées. Cela signifie que les profils seront affectés de manière aléatoire à chaque chemin d’accès. La division **est** persistante, ce qui signifie que le profil sera dans la même sous-audience sur chaque évaluation.

>[!NOTE]
>
>Auparavant, les divisions dans la composition de l’audience étaient **et non** persistantes.

Pour plus d’informations sur le bloc Partage, lisez le [Guide de l’interface utilisateur de composition d’audience](./ui/audience-composition.md#split).

### Puis-je utiliser tous les types de segmentation dans le workflow Composition de l’audience ?

Oui, tous les types de segmentation ([segmentation par lots, segmentation en flux continu et segmentation Edge](./home.md#evaluate-segments)) sont pris en charge dans le workflow Composition de l’audience. Toutefois, comme les compositions ne sont actuellement exécutées qu’une seule fois par jour, même si des audiences évaluées par Edge ou en flux continu sont incluses, le résultat sera basé sur l’appartenance à l’audience au moment de l’exécution de la composition.

## Appartenance à une audience

La section suivante répertorie les questions relatives à l’appartenance à une audience.

### Comment puis-je confirmer l’appartenance d’un profil à une audience ?

Pour confirmer l’appartenance à l’audience d’un profil, consultez la page des détails de profil du profil que vous souhaitez confirmer. Sélectionnez **[!UICONTROL Attributs]**, puis **[!UICONTROL Afficher JSON]**, et vous pouvez confirmer que l’objet `segmentMembership` contient l’identifiant de l’audience.

### Comment la segmentation par lots résout-elle l’appartenance à un profil ?

Les audiences évaluées à l’aide de la segmentation par lots se résolvent tous les jours, les résultats de l’adhésion à l’audience étant enregistrés dans l’attribut `segmentMembership` du profil. Les recherches de profil génèrent une nouvelle version du profil au moment de la recherche, mais elles n’actualisent **pas** les résultats de la segmentation par lots.

Par conséquent, lorsque des modifications sont apportées au profil, par exemple la fusion de deux profils ensemble, ces modifications **apparaissent dans le profil lors de la recherche, mais** not **sont répercutées dans l’attribut `segmentMembership` jusqu’à ce que la tâche d’évaluation de segment soit exécutée à nouveau.**

Supposons, par exemple, que vous ayez créé deux audiences mutuellement exclusives : l’audience A est destinée aux personnes qui vivent à Washington et l’audience B est destinée aux personnes qui **ne vivent pas** à Washington. Il existe deux profils : le profil 1 pour une personne qui vit à Washington et le profil 2 pour une personne qui vit dans l’Oregon.

Lorsque la tâche d’évaluation de la segmentation par lots s’exécute, le profil 1 accède à l’audience A, tandis que le profil 2 passe à l’audience B. Plus tard, mais avant que la tâche d’évaluation de la segmentation par lots du lendemain ne s’exécute, un événement qui réconcilie les deux profils entre dans Platform. Par conséquent, un seul profil fusionné contenant les profils 1 et 2 est créé.

Jusqu’à l’exécution de la tâche d’évaluation de segment par lot suivante, le nouveau profil fusionné aura une appartenance à l’audience dans **profile 1} et profile 2.** Par conséquent, cela signifie qu’il sera membre de l’**audience A et de l’audience B, même si ces audiences ont des définitions contradictoires.** Pour l&#39;utilisateur final, il s&#39;agit de la **même situation** qu&#39;avant la connexion des profils, puisqu&#39;il n&#39;y avait toujours qu&#39;une seule personne impliquée, et que Platform n&#39;avait **pas** assez d&#39;informations pour connecter les deux profils ensemble.

Si vous utilisez la recherche de profil pour récupérer le profil nouvellement créé et examinez son appartenance à l’audience, elle montrera qu’elle est membre de **à la fois** Audience A et Audience B, bien que ces deux audiences aient des définitions contradictoires. Une fois la tâche d’évaluation de la segmentation par lots exécutée quotidiennement, l’appartenance à l’audience est mise à jour pour refléter cet état mis à jour des données de profil.

Si vous avez besoin d’une résolution d’audience plus élevée en temps réel, utilisez la segmentation par flux ou en périphérie.

### Combien de temps faut-il pour que les données en continu soient disponibles dans les workflows de segmentation par lots ?

Il peut s’écouler jusqu’à trois heures avant que les données en continu ne soient disponibles dans les workflows de segmentation par lots.

Par exemple, si une tâche de segmentation par lots s’exécute à 21 h, elle contient certainement des données ingérées par flux **jusqu’à** 18 h. La diffusion en continu des données ingérées après 18h00 mais avant 21h00 **may** doit être incluse.

