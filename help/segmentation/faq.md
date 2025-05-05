---
title: Questions fréquentes sur les audiences
description: Découvrez les réponses aux questions fréquentes sur les audiences et d’autres concepts liés à la segmentation.
exl-id: 79d54105-a37d-43f7-adcb-97f2b8e4249c
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '4842'
ht-degree: 27%

---

# Questions fréquentes

L’interface utilisateur et l’API RESTful du [!DNL Segmentation Service] d’Adobe Experience Platform vous permettent de créer des audiences par le biais de définitions de segment ou d’autres sources à partir de vos données [!DNL Real-Time Customer Profile]. Ces audiences sont configurées et conservées de manière centralisée sur Experience Platform et sont facilement accessibles depuis n’importe quelle solution Adobe. Vous trouverez ci-dessous les questions fréquentes sur les audiences et la segmentation.

## Audience Portal

La section suivante répertorie les questions relatives à Audience Portal.

### Puis-je accéder au portail d’audience et à la composition d’audience ?

Le portail d’audience et la composition d’audience sont disponibles pour tous les clientes et clients Real-Time CDP Prime et Ultimate (éditions B2C, B2B et B2P) et Journey Optimizer Select, Prime, Ultimate Starter et Ultimate.

Dans la version la plus récente de l’application, seules les audiences basées sur un profil sont prises en charge. La prise en charge des audiences basées sur un compte sera assurée dans une version ultérieure.

### Les audiences préconfigurées générées en externe sont-elles prises en charge par le portail d’audience ?

Oui, les audiences préconfigurées générées en externe sont prises en charge par le portail d’audience. Dans la version la plus récente de l’application, vous pouvez importer une audience générée en externe par le biais d’un fichier CSV. Dans une version ultérieure, vous pourrez ajouter des audiences par le biais de connecteurs source par lots ou en flux continu.

### De quelles autorisations ai-je besoin pour charger des audiences générées en externe ?

Pour charger des audiences générées en externe, vous devez disposer des autorisations « Afficher les segments », « Gérer les segments » et « Importer des audiences ». Aucun contrôle spécifique basé sur les rôles n’est requis pour charger des audiences générées en externe.

### Que se passe-t-il lorsque je charge une audience générée en externe ?

Lorsque vous chargez une audience générée en externe, un jeu de données est créé et visible dans l’inventaire des jeux de données. Le nom du jeu de données sera le **même** que le nom de l’audience générée en externe que vous avez chargée.

### Qu’est-ce qu’une audience générée en externe composée de et qu’advient-il de ces données lorsqu’elles sont importées dans Experience Platform ?

Pendant le workflow d’importation d’audience externe, vous devez spécifier la colonne du fichier CSV qui correspond à l’**identité de Principal**. Parmi les exemples d’identité principale figurent l’adresse e-mail, l’ECID ou un espace de noms d’identité personnalisé spécifique à une organisation.

Les données associées à cette colonne d’identité principale sont les **seules** données associées au profil. S’il n’existe aucun profil correspondant aux données de la colonne d’identité principale, un nouveau profil est créé. Cependant, ce profil est essentiellement un profil orphelin, car **aucun** attribut ni événement d’expérience n’est associé à ce profil.

Toutes les autres données de l’audience générée en externe sont considérées comme des **attributs de payload**. Ces attributs peuvent **uniquement** être utilisés à des fins de personnalisation et d’enrichissement lors de l’activation et ne sont **pas** associés à un profil. Ces attributs sont toutefois stockés dans le lac de données.

Bien que l’audience générée en externe puisse être référencée lors de la création d’audiences à l’aide du créateur de segments, les attributs de profil individuels **ne peuvent pas** être utilisés.

### Puis-je réconcilier des données d’audience générées en externe avec un profil existant dans Experience Platform ?

Oui, l’audience générée en externe sera fusionnée avec le profil existant dans Experience Platform si les identifiants principaux correspondent. La réconciliation de ces données peut prendre jusqu’à 24 heures. Si les données de profil n’existent pas déjà, un profil est créé lors de l’ingestion des données.

### Comment les préférences de consentement des clients sont-elles respectées pour les audiences générées en externe qui sont importées dans Audience Portal ?{#consent}

À mesure que les données clientèle sont capturées à partir de plusieurs canaux, les politiques de combinaison et de fusion d’identités permettent de consolider ces données dans un profil client unique en temps réel. Les informations sur les préférences de consentement des clientes et clients sont stockées et évaluées au niveau du profil.

Les destinations en aval vérifient les informations de consentement de chaque profil avant l’activation. Les informations de consentement de chaque profil sont comparées aux exigences de consentement pour une destination particulière. Si le profil ne répond pas aux exigences, il n’est pas envoyé vers une destination.

Lorsqu’une audience externe est ingérée dans Audience Portal, elle est jointe aux profils existants à l’aide d’un identifiant principal tel qu’un e-mail ou un ECID. Par conséquent, les politiques de consentement existantes resteront en vigueur tout au long de l’activation.

Notez que vous ne devez **pas** inclure d’informations de consentement avec une audience générée en externe, car les variables de payload sont **non** stockées dans la banque de profils, mais dans le lac de données. Au lieu de cela, vous **devez** utiliser un canal d’ingestion Adobe Experience Platform dans lequel les données de profil sont importées.

### Puis-je utiliser une audience générée en externe pour créer d’autres audiences ?

Oui, les audiences générées en externe apparaîtront dans l’inventaire des audiences. elles peuvent être utilisés lors de la création d’audiences dans le [Créateur de segments](./ui/segment-builder.md).

### À quelle fréquence les audiences générées en externe sont-elles évaluées ?

Les audiences générées en externe sont **uniquement** évaluées au cours de l’importation. Puisque les attributs associés à ces audiences d’importation ne sont pas durables et ne font **pas** partie de la banque de profils, la seule fois où une audience générée en externe sera mise à jour est si l’audience existante est mise à jour manuellement.

### Puis-je utiliser des attributs téléchargés en externe dans le cadre de la segmentation ?

Non. Les attributs de profil sont censés être des attributs durables, tandis que les données d’audience générées en externe qui sont chargées ne contiennent que des données contextuelles associées à cette audience générée en externe.

Les données contextuelles de l’audience générée en externe, ou attributs d’enrichissement, possèdent une durée de vie **limitée**, car leur cycle de vie est lié à l’audience téléchargée. En raison de leur caractère éphémère, les attributs d’enrichissement ne sont **pas** disponibles dans la segmentation.

Cependant, lorsque vous mappez vos audiences vers des destinations par lots ou basées sur des fichiers, vous pouvez utiliser ces attributs d’enrichissement générés en externe pour élargir vos audiences et accroître les activations en aval.

Pour en savoir plus sur cette fonctionnalité, consultez le guide de l’[activation des données d’audience vers des destinations d’exportation de profils par lots](../destinations/ui/activate-batch-profile-destinations.md#mapping).

### Existe-t-il une politique de fusion spécifique pour les audiences générées en externe ?

La politique de fusion par défaut spécifique à l’organisation est automatiquement appliquée lors du chargement d’audiences générées en externe. Cependant, vous pouvez modifier la politique de fusion appliquée à l’audience générée en externe pendant le workflow d’importation d’audience.

### Où puis-je activer les audiences générées en externe ?

Une audience générée de manière externe peut être mappée à n’importe quelle destination et être utilisée dans les campagnes et parcours Adobe Journey Optimizer.

### Puis-je supprimer une audience générée en externe ?

Oui! Les audiences générées en externe peuvent être supprimées dans Audience Portal.

### Que dois-je faire si j’ai accidentellement chargé une audience générée en externe ?

Si vous avez accidentellement chargé une audience générée en externe et que vous souhaitez supprimer les données, vous pouvez effacer les profils associés à l’audience en chargeant un fichier CSV avec une ligne et aucune donnée.

### Quelle est la durée des audiences générées en externe ?

L’expiration actuelle des données pour les audiences générées en externe est de **30 jours**. Cette expiration des données a été choisie pour réduire la quantité de données excédentaires stockées au sein de votre organisation.

Une fois la période d’expiration des données passée, le jeu de données associé sera toujours visible dans l’inventaire des jeux de données, mais vous ne **pourrez pas** activer l’audience et le nombre de profils s’affichera comme zéro.

### Existe-t-il un nombre maximal d’audiences générées en externe que je peux importer ?

Le nombre d’audiences générées en externe que vous pouvez importer n’est pas limité. Notez toutefois que les audiences importées **ne** sont pas comptabilisées par rapport à la limite d’audience globale.

### Comment le portail d’audience et la composition d’audience interagiront-ils avec les données du partenaire Real-Time CDP ?

Le portail d’audience et la composition d’audience interagissent avec les données du partenaire de deux manières :

1. Si vous ingérez une liste de prospects fournie par le partenaire à l’aide de la classe et du workflow Prospect Profile, les prospects seront conservés **séparément** des profils clients de fusion dans le Profile Service. Cela signifie que les listes de prospects ne seront **pas** disponibles dans le portail d’audience ou dans la composition d’audience.
2. Si vous tirez parti des attributs fournis par le partenaire pour enrichir les profils propriétaires **existants**, ces audiences enrichies en données de partenaire **seront** disponibles dans le portail d’audience et dans la composition d’audience pour être utilisées.

### Comment utiliser des attributs supplémentaires avec mes audiences ?

Avec les audiences, vous pouvez ajouter **deux** différents types d’attributs supplémentaires : attributs de payload (contextuels) et attributs d’enrichissement.

Les attributs de payload sont des attributs ingérés dans le cadre du chargement CSV d’une audience générée en externe. Ces attributs ne sont **pas** ingérés dans le profil client en temps réel, mais peuvent être utilisés dans le cadre d’une destination en aval.

Les attributs d’enrichissement sont des attributs qui proviennent d’un jeu de données et sont joints à une audience dans la composition de l’audience. Actuellement, ces attributs ne peuvent être utilisés que dans les campagnes Adobe Journey Optimizer. La prise en charge des parcours Adobe Journey Optimizer sera bientôt disponible, avec une prise en charge des destinations en aval en attente de publication ultérieure.

| Canal d’activation | Audiences du téléchargement personnalisé d’un fichier CSV | Audiences issues de la composition de l’audience |
| --- | --- | --- |
| Destinations Real-Time CDP | Les attributs de payload et les audiences peuvent être activés. | Seule l’audience peut être activée. Les attributs d’enrichissement **impossible** ne peuvent pas être activés. |
| Campagnes Adobe Journey Optimizer | Ni l’audience ni les attributs de payload ne peuvent être activés. | Les attributs d’audience et d’enrichissement peuvent être activés. |

## États du cycle de vie {#lifecycle-states}

La section suivante répertorie les questions relatives aux états du cycle de vie et à la gestion des états du cycle de vie dans Audience Portal.

### Que représentent les différents états du cycle de vie ?

Le graphique suivant explique les différents statuts de cycle de vie, ce qu’ils représentent, où les audiences avec ce statut peuvent être utilisées, ainsi que l’impact sur les mécanismes de sécurisation de la segmentation.

| État | Définition | Visible dans Audience Portal ? | Visible dans les destinations ? | Affecte-t-il les limites de segmentation ? | Impact sur les audiences basées sur des fichiers | Impact sur l’évaluation de l’audience | Utilisable dans d’autres audiences ? | Modifiable |
| --- | --- | --- | --- | --- | --- | --- | --- | -- |
| Brouillon | Une audience à l’état **Brouillon** est une audience qui est toujours en développement et qui n’est pas encore prête à être utilisée dans d’autres services. | Oui, mais peut être caché. | Non | Oui | Peuvent être importées ou mises à jour pendant le processus d’affinement. | Évalué pour obtenir des chiffres de publication précis. | Oui, mais son utilisation n’est pas recommandée. | Oui |
| Publié | Une audience dont l’état est **Publié** est une audience prête à être utilisée dans tous les services en aval. | Oui | Oui | Oui | Peuvent être importés ou mis à jour. | Évalué à l’aide de la segmentation par lots, en flux continu ou Edge. | Oui | Oui |
| Inactif | Une audience dont l’état est **Inactive** est une audience qui n’est actuellement pas utilisée. Il existe toujours dans Experience Platform, mais il ne sera **pas** utilisable tant qu’il ne sera pas marqué comme brouillon ou publié. | Non, mais peut être affiché. | Non | Non | Plus mise à jour. | n’est plus évalué ou mis à jour par Experience Platform. | Non | Oui |
| Supprimé | Une audience dont l’état est **Supprimée** est une audience qui a été supprimée. L’exécution de la suppression réelle des données peut prendre jusqu’à quelques minutes. | Non | Non | Non | Les données sous-jacentes sont supprimées. | Aucune évaluation ni exécution de données ne se produit une fois la suppression terminée. | Non | Non |

### Dans quels états puis-je modifier mes audiences ?

Les audiences peuvent être modifiées dans les états de cycle de vie suivants :

- **Brouillon** : si une audience est modifiée à l’état de brouillon, elle reste à l’état de brouillon, sauf si elle est publiée explicitement.
- **Publié** : si une audience est modifiée à l’état publié, elle restera publiée et l’audience sera automatiquement mise à jour.
- **Inactive** : si une audience est modifiée à l’état inactif, elle restera inactive. Cela signifie qu’il ne sera ni évalué ni mis à jour. Si vous devez mettre à jour l’audience, vous devez la publier.

Une fois qu’une audience est supprimée, elle **ne peut pas** être modifiée.

### Vers quels états du cycle de vie puis-je déplacer une audience ?

Les états de cycle de vie possibles dans lesquels une audience peut être déplacée dépendent de l’état actuel de l’audience.

![Diagramme décrivant les transitions d’état de cycle de vie possibles disponibles pour les audiences.](./images/faq/lifecycle-state-transition.png)

Si votre audience est en statut de brouillon, vous pouvez la publier ou la supprimer si l’audience ne comporte aucune personne à charge.

Si votre audience est à l’état publié, vous pouvez la désactiver ou la supprimer si l’audience n’a aucune personne à charge.

Si votre audience est inactive, vous pouvez la republier ou la supprimer si l’audience n’a pas de personnes à charge.

### Existe-t-il des avertissements pour les audiences dans certains états du cycle de vie ?

Les audiences à l’état publié ne peuvent être déplacées vers un autre état que si l’audience n’a **pas** de personnes à charge. Cela signifie que si votre audience est utilisée dans un service en aval, elle ne peut pas être désactivée ni supprimée.

Si une audience évaluée à l’aide de la segmentation par lots est republiée, c’est-à-dire lorsqu’une audience passe d’inactive à publiée, l’audience s’actualisera **après** le traitement par lots quotidien. Lorsqu’elle sera republiée pour la première fois, les profils et les données seront les **mêmes** que lorsque l’audience a été rendue inactive.

### Comment puis-je placer une audience à l’état de brouillon ?

La méthode pour mettre une audience à l’état de brouillon dépend de l’origine de l’audience.

Pour les audiences créées à l’aide du créateur de segments, vous pouvez définir l’audience sur l’état de brouillon en sélectionnant « [!UICONTROL Enregistrer en tant que brouillon] » dans le créateur de segments.

Pour les audiences créées dans Composition de l’audience, les audiences sont automatiquement enregistrées en tant que brouillon jusqu’à leur publication.

Pour les audiences créées en externe, les audiences sont automatiquement publiées.

Une fois qu’une audience est à l’état publié, vous **pouvez pas** l’audience d’origine à l’état de brouillon. Cependant, si vous copiez l’audience, celle qui vient d’être copiée est à l’état de brouillon.

### Comment puis-je placer une audience à l’état publié ?

Pour les audiences créées à l’aide du créateur de segments ou de la composition de l’audience, vous pouvez définir l’audience sur l’état publié en sélectionnant « [!UICONTROL Publier] » dans leurs interfaces utilisateur respectives.

Les audiences créées en externe sont automatiquement définies sur publiées.

### Comment mettre une audience à l’état inactif ?

Vous pouvez mettre une audience publiée en statut inactif en ouvrant le menu d’actions rapides dans Audience Portal et en sélectionnant « [!UICONTROL &#x200B; Désactiver &#x200B;].

### Comment republier une audience ?

>[!NOTE]
>
>L’état « republié » est le même que l’état publié pour le comportement de l’audience.

Vous pouvez republier une audience en sélectionnant une audience dont le statut est inactif, en ouvrant le menu d’actions rapides sur Audience Portal et en sélectionnant [!UICONTROL Publier].

### Comment mettre une audience à l’état supprimé ?

>[!IMPORTANT]
>
>Vous pouvez uniquement supprimer les audiences qui ne sont **pas** utilisées dans les activations en aval. De plus, vous ne pouvez pas supprimer une audience référencée dans une autre audience. Si vous ne pouvez pas supprimer votre audience, assurez-vous de ne **pas** l’utiliser dans des services en aval ou comme bloc de création d’une autre audience.

Pour supprimer une audience, ouvrez le menu des actions rapides dans Audience Portal et sélectionnez [!UICONTROL Supprimer].

### Existe-t-il des avertissements pour les transitions d’état de cycle de vie ?

Oui, il existe des avertissements à connaître lorsque vous utilisez des audiences dans des services en aval tels que Adobe Journey Optimizer ou des audiences non basées sur les clients telles que les audiences basées sur les comptes.

À ce stade, vous **devez** vérifier manuellement si l’audience est utilisée en aval dans Adobe Journey Optimizer, car ce statut n’est actuellement pas automatiquement vérifié.

En outre, vous **devez** vérifier manuellement si l’audience est utilisée comme composant d’une audience basée sur un compte, car ce statut n’est pas non plus automatiquement vérifié actuellement.

### Que se passe-t-il lorsque je copie une audience ? {#copy}

Lorsque vous copiez une audience, la nouvelle audience est à l’état de brouillon et conserve les mêmes dossiers, balises et libellés que ceux appliqués à l’audience d’origine.

### L’utilisation d’une audience comme audience enfant affecte-t-elle les transitions d’état du cycle de vie ?

>[!NOTE]
>
>Une audience parente est une audience qui **utilise** une autre audience comme dépendance de l’audience.
>
>Une audience enfant est une audience **utilisée comme** dépendance de l’audience.

Oui, l’utilisation d’une audience comme audience enfant affecte les transitions d’états de cycle de vie que l’audience enfant et parente peuvent entreprendre.

Pour qu’une audience enfant soit déplacée vers l’état publié, toute son audience parente **doit** doit être à l’état publié. Les audiences parentes peuvent être publiées avant la publication de l’audience enfant ou, si l’utilisateur ou l’utilisatrice le confirme, peuvent être automatiquement publiées lorsque l’audience enfant est publiée.

Pour que l’audience parente soit déplacée vers l’état inactif ou supprimé, toutes ses audiences enfants **doivent** doivent être désactivées ou supprimées.

### Puis-je faire référence à une audience dont l’état de cycle de vie est différent ?

Oui! Si votre audience est actuellement à l’état de brouillon, vous pouvez vous y référer dans l’état de brouillon ou publié. Toutefois, pour publier cette audience, vous **devez** publier les autres audiences parentes.

## Inventaire des audiences

La section suivante répertorie les questions relatives à l’inventaire des audiences dans le portail Audience.

### Ai-je besoin d’autorisations supplémentaires pour utiliser les fonctionnalités d’inventaire des audiences ?

Non, vous ne le faites pas. Tant que vous disposez des autorisations de modification des audiences, vous pourrez créer, mettre à jour et gérer vos dossiers et balises dans Audience Portal. Pour plus d’informations sur la gestion des autorisations, consultez le guide [gestion des autorisations](../access-control/ui/permissions.md).

### Y a-t-il une limite au nombre de dossiers que je peux créer ?

Non, le nombre de dossiers que vous pouvez créer n’est pas limité. Pour plus d’informations sur les dossiers, reportez-vous à la section [inventaire des audiences](./ui/audience-portal.md#folders) de la présentation de l’interface utilisateur de Segmentation Service.

### Existe-t-il une limite au nombre de balises pouvant être ajoutées à une audience ?

Non, le nombre de balises pouvant être ajoutées à une audience n’est pas limité. Pour plus d’informations sur les balises, reportez-vous à la section [inventaire des audiences](./ui/audience-portal.md#tags) de la présentation de l’interface utilisateur de Segmentation Service.

### Y a-t-il une limite au nombre de balises que je peux créer ?

Non, le nombre de balises que vous pouvez créer n’est pas limité. Cependant, vous pouvez créer un maximum de 100 catégories **&#x200B;**&#x200B;à appliquer aux balises. Pour plus d’informations sur la gestion des balises, consultez le [guide de gestion des balises](../administrative-tags/ui/managing-tags.md).

### Lorsque je recherche une audience par nom ou balise dans un dossier parent, puis-je également effectuer une recherche dans les dossiers enfants associés ?

Ce comportement n’est pas pris en charge. Cependant, vous pouvez modifier la vue d’inventaire des audiences pour afficher **Toutes les audiences**, puis effectuer une recherche dans tous les dossiers. Pour plus d’informations sur l’utilisation de la recherche dans l’inventaire des audiences, veuillez lire la [section recherche](./ui/audience-portal.md#search) de la présentation de l’interface utilisateur de Segmentation Service.

### Puis-je affecter automatiquement une audience à un dossier au moment de sa création ?

À ce stade, non. Cependant, cette fonctionnalité pourrait être disponible à l’avenir.

### Puis-je déplacer plusieurs audiences dans un dossier en même temps ?

À ce stade, non. Cependant, cette fonctionnalité pourrait être disponible à l’avenir.

## Composition d’audiences

La section suivante répertorie les questions relatives à la composition de l’audience.

### Quand dois-je utiliser la composition de l’audience plutôt que le créateur de segments ?

La composition de l’audience et le créateur de segments jouent tous deux un rôle important dans la création d’audiences dans Experience Platform.

Le créateur de segments est plus adapté à la création d’audiences **création** (pour créer une audience à partir de zéro), tandis que la composition de l’audience est plus adaptée au traitement et à la personnalisation de l’audience **pour créer de nouvelles audiences basées sur une audience existante**.

Le tableau suivant illustre la différence entre les deux services :

| Créateur de segments | Composition d’audiences |
| --------------- | -------------------- |
| <ul><li>Génération d’audiences à une seule étape</li><li>Crée les blocs de base des audiences à partir des données de profil, de série temporelle et multi-entités</li><li>Utilisé pour créer **audience unique**</li></ul> | <ul><li>Génération d’audiences à plusieurs étapes, à l’aide d’opérations basées sur des ensembles</li><li>Utilise les audiences créées par le créateur de segments et applique des options d’enrichissement des données, telles que le classement des attributs de profil et le fractionnement en sous-audiences</li><li>Permet de créer **plusieurs** audiences à la fois</li></ul> |

Pour en savoir plus sur le créateur de segments, consultez le [guide du créateur de segments](./ui/segment-builder.md). Pour en savoir plus sur la composition de l’audience, veuillez lire le guide [Composition de l’audience](./ui/audience-composition.md).

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
3. Vous pouvez éventuellement ajouter un bloc [!UICONTROL Enrichir] qui suit le bloc [!UICONTROL Exclure]. Vous ne pouvez utiliser qu’un seul bloc **one** [!UICONTROL Enrich] par composition.
4. Vous pouvez éventuellement ajouter un bloc [!UICONTROL Classer] ou [!UICONTROL Partager]. Vous pouvez **uniquement** avoir l’un de ces blocs par composition.
5. Vous terminez **toujours** par un bloc [!UICONTROL Enregistrer] pour enregistrer votre audience.

En outre, les restrictions suivantes(?) appliquer lors de l’utilisation de ces blocs :

- Bloc Partager
   - Ce bloc ne prend en charge que les types de données **String**. Le bloc Fractionner ne prend **pas** en charge le type de données date ou booléen.
   - En outre, ce bloc ne prend **pas** en charge les attributs d’enrichissement.
- Exclure le bloc
   - Ce bloc ne prend **pas** en charge le type de données date ou booléen.
- Bloc Classement
   - Ce bloc ne prend **pas** en charge les attributs d’enrichissement.

Pour plus d’informations sur l’utilisation de la composition de l’audience, lisez le [Guide de l’interface utilisateur de la composition d’audience](./ui/audience-composition.md).

### Quand les audiences créées à l’aide de la composition d’audience sont-elles enregistrées et évaluées ?

Les audiences sont automatiquement enregistrées lors de leur création dans la composition de l’audience. L’heure de création de l’audience sera la première fois que cet enregistrement automatique aura lieu.

Une fois la composition de l’audience créée, son évaluation et son activation pour une utilisation dans des services en aval tels qu’une destination Real-Time CDP ou un canal Adobe Journey Optimizer peuvent prendre jusqu’à 48 heures.

### Quand puis-je utiliser l’audience que j’ai créée ?

L’audience créée dans Composition de l’audience s’affichera **immédiatement** dans le portail Audience. Toutefois, pour l’utiliser dans Adobe Journey Optimizer, vous devez attendre au moins 24 heures après l’évaluation.

### Les traitements d’évaluation sont-ils visibles dans la section de suivi ?

Actuellement, les traitements d’évaluation ne sont **pas** affichés dans l’interface utilisateur de surveillance.

### Puis-je utiliser une composition d’audience dans une autre composition ?

Non, les audiences créées à l’aide de la composition de l’audience **ne peuvent pas** être utilisées comme entrée dans une autre composition d’audience.

### Comment le partage fonctionne-t-il dans la composition de l’audience ?

Le fractionnement d’audience permet de sous-définir votre audience en groupes plus petits.

Lors du fractionnement par attribut, il existe une exclusivité mutuelle entre les groupes. Cela signifie que si un enregistrement répond aux critères de plusieurs chemins de partage, le **premier** chemin à partir de la gauche lui sera attribué et **pas** l’un des autres chemins.

Lors du fractionnement par pourcentage, les fractionnements sont **aléatoirement** effectués. Cela signifie que les profils seront attribués de manière aléatoire à chaque chemin d’accès.

Pour plus d’informations sur le bloc Partage, lisez le [Guide de l’interface utilisateur de composition d’audience](./ui/audience-composition.md#split).

### Puis-je utiliser tous les types de segmentation dans le workflow Composition de l’audience ?

Oui, tous les types de segmentation ([segmentation par lots, segmentation en flux continu et segmentation Edge](./home.md#evaluate-segments)) sont pris en charge dans le workflow Composition de l’audience. Toutefois, comme les compositions ne sont actuellement exécutées qu’une seule fois par jour, même si des audiences évaluées par Edge ou en flux continu sont incluses, le résultat sera basé sur l’appartenance à l’audience au moment de l’exécution de la composition.

## Appartenance à une audience

La section suivante répertorie les questions relatives à l’appartenance à une audience.

### Comment puis-je confirmer l’appartenance d’un profil à une audience ?

Pour confirmer l’appartenance à l’audience d’un profil, consultez la page des détails de profil du profil que vous souhaitez confirmer. Sélectionnez **[!UICONTROL Attributs]**, puis **[!UICONTROL Afficher JSON]**, et vous pouvez confirmer que l’objet `segmentMembership` contient l’identifiant de l’audience.

### L’adhésion à l’audience peut-elle dériver entre l’adhésion idéale et l’adhésion réelle ?

Oui, l’appartenance à une audience peut dériver entre l’appartenance idéale et l’appartenance réelle si une audience est évaluée à l’aide de la segmentation par flux **et** cette audience est basée sur une audience évaluée à l’aide de la segmentation par lots.

Par exemple, si l’audience A est basée sur l’audience B et que l’audience B est évaluée à l’aide de la segmentation par lots, puisque l’audience B ne se met à jour que toutes les 24 heures, l’audience A s’éloigne davantage des données réelles jusqu’à ce qu’elle se resynchronise avec les mises à jour de l’audience B.

## Segmentation par lots {#batch-segmentation}

La section suivante répertorie les questions relatives à la segmentation par lots.

### Comment la segmentation par lots résout-elle l’appartenance à un profil ?

Les audiences évaluées à l’aide de la segmentation par lots sont résolues quotidiennement, les résultats de l’appartenance à l’audience étant enregistrés dans l’attribut `segmentMembership` du profil. Les recherches de profils génèrent une nouvelle version du profil au moment de la recherche, mais elles n’actualisent **pas** les résultats de la segmentation par lots.

Par conséquent, lorsque des modifications sont apportées au profil, telles que la fusion de deux profils, ces modifications **apparaîtront** dans le profil lors de la recherche, mais **ne seront pas** reflétées dans l’attribut `segmentMembership` jusqu’à ce que la tâche d’évaluation de segment ait à nouveau été exécutée.

Supposons, par exemple, que vous ayez créé deux audiences qui s’excluent mutuellement : l’audience A est destinée aux personnes qui vivent à Washington et l’audience B est destinée aux personnes qui ne vivent **pas** à Washington. Il existe deux profils : le profil 1 pour une personne qui vit à Washington et le profil 2 pour une personne qui vit en Oregon.

Lorsque le traitement d’évaluation de segmentation par lots s’exécute, le profil 1 passe à l’audience A, tandis que le profil 2 passe à l’audience B. Plus tard, mais avant l’exécution du traitement d’évaluation de segmentation par lots du lendemain, un événement qui réconcilie les deux profils entre dans Experience Platform. Par conséquent, un seul profil fusionné contenant les profils 1 et 2 est créé.

Jusqu’à l’exécution de la tâche d’évaluation de segment par lot suivante, le nouveau profil fusionné aura une appartenance à l’audience dans **les deux** profil 1 et profil 2. Par conséquent, cela signifie qu’elle sera membre des **à la fois** audience A et audience B, bien que ces audiences aient des définitions contradictoires. Pour l’utilisateur final, il s’agit de la **exactement la même situation** qu’avant la connexion des profils, puisqu’il n’y avait toujours qu’une seule personne concernée et qu’Experience Platform ne disposait tout simplement **pas** d’informations suffisantes pour connecter les deux profils.

Si vous utilisez la recherche de profil pour récupérer le profil nouvellement créé et examiner son appartenance à l’audience, elle indique qu’elle est membre des **deux** audience A et audience B, malgré le fait que ces deux audiences ont des définitions contradictoires. Une fois la tâche d’évaluation de segmentation par lots quotidienne exécutée, l’appartenance à l’audience sera mise à jour pour refléter cet état mis à jour des données de profil.

Si vous avez besoin de davantage de résolution d’audience en temps réel, utilisez la diffusion en continu ou la segmentation Edge.

### Combien de temps faut-il pour que les données de diffusion en continu soient disponibles dans les workflows de segmentation par lots ?

La disponibilité des données de diffusion en continu dans les workflows de segmentation par lots peut prendre jusqu’à trois heures.

Par exemple, si une tâche de segmentation par lots s’exécute à 21 heures, il est garanti qu’elle contiendra des données ingérées de diffusion en continu **jusqu’à 18 heures**. Les données ingérées en flux continu qui ont été ingérées après 18h00 mais avant 21h00 **peuvent** incluses.

## Segmentation Edge {#edge-segmentation}

La section suivante répertorie les questions liées à la segmentation Edge.

### Combien de temps faut-il pour qu’une définition de segment soit disponible sur le réseau Edge ?

La disponibilité d’une définition de segment sur le réseau Edge peut prendre jusqu’à une heure.

## Segmentation par streaming {#streaming-segmentation}

La section suivante répertorie les questions relatives à la segmentation en flux continu.

### La « disqualification » de la segmentation en flux continu est-elle également effectuée en temps réel ?

Pour la plupart des instances, la disqualification de la segmentation en fux continu se produit en temps réel. Toutefois, les segments en flux continu qui utilisent des segments de segments ne sont **pas** disqualifiés en temps réel, mais sont disqualifiés après 24 heures.

### Sur quelles données la segmentation en flux continu fonctionne-t-elle ?

La segmentation en flux continu fonctionne sur toutes les données ingérées à l’aide d’une source en flux continu. Les données ingérées à l’aide d’une source par lots seront évaluées chaque nuit, même si elles sont qualifiées pour la segmentation en flux continu. Les événements diffusés dans le système avec une date et une heure de plus de 24 heures seront traités dans le traitement par lots suivant.

### Comment les segments sont-ils définis comme segmentation par lots ou en flux continu ?

Une définition de segment est définie comme une segmentation Edge, par lots ou en flux continu selon une combinaison de type de requêtes et de durée d’historique des événements. Vous trouverez une liste des segments qui seront évalués en tant que segment en flux continu dans la [section types de requête de segmentation en flux continu](#query-types).

Notez que si une définition de segment contient **à la fois** une expression `inSegment` et une chaîne d’événement unique directe, elle ne peut pas être éligible à la segmentation en flux continu. Si vous souhaitez que ce segment soit éligible à la segmentation en flux continu, vous devez faire de la chaîne d’événement unique directe son propre segment.

### Pourquoi le nombre de segments « total qualifié » continue-t-il à augmenter alors que le nombre sous « X derniers jours » reste à zéro dans la section de détails de définition de segment ?

Le nombre total de segments qualifiés est tiré de la tâche de segmentation quotidienne, qui inclut les audiences qui sont qualifiées pour des segments par lots et par diffusion en flux continu. Cette valeur s’affiche pour les segments par lots et en diffusion en flux continu.

Le nombre sous « X derniers jours » comprend **seulement** les audiences qualifiées en segmentation en flux continu, et augmente **seulement** si vous avez diffusé des données en flux continu dans le système et qu’elles sont prises en compte dans cette définition de diffusion en flux continu. Cette valeur est **seulement** affichée pour les segments en diffusion en flux continu. Par conséquent, cette valeur **peut** s’afficher avec une valeur 0 pour les segments par lots.

Par conséquent, si vous constatez que le nombre sous « X derniers jours » est nul et que le graphique linéaire signale également zéro, vous n’avez **pas** diffusé en flux continu dans le système des profils qui sont qualifiés pour ce segment.

### Combien de temps faut-il pour qu’une définition de segment soit disponible ?

La disponibilité d’une définition de segment peut prendre jusqu’à une heure.

### Existe-t-il des limitations aux données diffusées en continu dans ?

Pour que les données diffusées soient utilisées dans la segmentation en flux continu, il **doit** y avoir un espacement entre les événements diffusés en flux continu. Si un trop grand nombre d’événements sont diffusés en continu dans la même seconde, Experience Platform traite ces événements comme des données générées par les robots et ils sont ignorés. En règle générale, vous devez disposer d’au **moins** cinq secondes entre les données d’événement pour vous assurer que les données sont correctement utilisées.
