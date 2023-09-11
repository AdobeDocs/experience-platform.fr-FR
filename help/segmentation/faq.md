---
title: Questions fréquentes sur les audiences
description: Découvrez les réponses aux questions fréquentes sur les audiences et d’autres concepts liés à la segmentation.
source-git-commit: 9a72d85bfb592012b36826135e24d28983f92e40
workflow-type: tm+mt
source-wordcount: '1935'
ht-degree: 52%

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

### Puis-je associer des données d’audience générées en externe à un profil existant dans Platform ?

Oui, l’audience générée en externe sera fusionnée avec le profil existant dans Platform si les identifiants principaux correspondent. L’intégration des données peut prendre jusqu’à 24 heures. Si les données de profil n’existent pas déjà, un profil est créé lors de l’ingestion des données.

## Puis-je utiliser une audience générée en externe pour créer d’autres audiences ?

Oui, les audiences générées en externe apparaîtront dans l’inventaire des audiences. elles peuvent être utilisés lors de la création d’audiences dans le [Créateur de segments](./ui/segment-builder.md).

### Puis-je utiliser des attributs téléchargés en externe dans le cadre de la segmentation ?

Non. Les attributs de profil sont censés être des attributs durables, tandis que les données d’audience générées en externe qui sont chargées ne contiennent que des données contextuelles associées à cette audience générée en externe.

Les données contextuelles de l’audience générée en externe, ou attributs d’enrichissement, possèdent une durée de vie **limitée**, car leur cycle de vie est lié à l’audience téléchargée. En raison de leur caractère éphémère, les attributs d’enrichissement ne sont **pas** disponibles dans la segmentation.

Cependant, lorsque vous mappez vos audiences vers des destinations par lots ou basées sur des fichiers, vous pouvez utiliser ces attributs d’enrichissement générés en externe pour élargir vos audiences et accroître les activations en aval.

Pour en savoir plus sur cette fonctionnalité, consultez le guide de l’[activation des données d’audience vers des destinations d’exportation de profils par lots](../destinations/ui/activate-batch-profile-destinations.md#mapping).

### Puis-je activer les audiences générées en externe dans Adobe Journey Optimizer ?

À ce stade, non. Cette fonctionnalité sera disponible dans un avenir proche.

### Puis-je supprimer une audience générée en externe ?

À ce stade, non. Comme solution de contournement, désactivez ou archivez l’audience. Notez que les profils **restent** disponibles dans les applications en aval. La prise en charge de la suppression des audiences générées en externe sera assurée dans une version ultérieure.

### Que représentent les différents états du cycle de vie ?

Le graphique suivant explique les différents états du cycle de vie, ce qu’ils représentent, où les audiences avec cet état peuvent être utilisées, ainsi que l’impact sur les barrières de sécurité de segmentation.

| État | Définition | Visible dans Audience Portal ? | Visible dans les destinations ? | Affecte les limites de segmentation ? | Impact sur les audiences basées sur des fichiers | Impact sur l’évaluation des audiences | Utilisable dans d’autres audiences ? |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Brouillon | Une audience dans le **Version préliminaire** state est une audience qui est encore en cours de développement et qui n’est pas encore prête à être utilisée dans d’autres services. | Oui, mais peut être caché. | Non | Oui | Peuvent être importées ou mises à jour pendant le processus d’affinage. | Peuvent être évaluées afin d’obtenir des comptes de publication précis. | Oui, mais non recommandé. |
| Publié | Une audience dans le **Publié** state est une audience prête à être utilisée sur tous les services en aval. | Oui | Oui | Oui | Peut être importé ou mis à jour. | Évalués à l’aide de la segmentation par lots, par flux ou par périphérie. | Oui |
| Inactif | Une audience dans le **Inactif** state est une audience qui n’est actuellement pas utilisée. Il existe toujours dans Platform, mais il le sera **not** être utilisable jusqu’à ce qu’il soit marqué comme brouillon ou publié. | Non, mais peut être affiché. | Non | Non | Non mise à jour plus longue. | N’est plus évalué ou mis à jour par Platform. | Oui |
| Supprimé | Une audience dans le **Supprimé** state est une audience qui a été supprimée. L’exécution de la suppression des données peut prendre jusqu’à quelques minutes. | Non | Non | Non | Les données sous-jacentes sont supprimées. | Aucune évaluation ou exécution des données n’a lieu une fois la suppression terminée. | Non |

### Comment le portail d’audience et la composition d’audience interagiront-ils avec les données du partenaire Real-Time CDP ?

Le portail d’audience et la composition d’audience interagissent avec les données du partenaire de deux manières :

1. Si vous ingérez une liste de prospects fournie par le partenaire à l’aide de la classe et du workflow Prospect Profile, les prospects seront conservés **séparément** des profils clients de fusion dans le Profile Service. Cela signifie que les listes de prospects ne seront **pas** disponibles dans le portail d’audience ou dans la composition d’audience.
2. Si vous tirez parti des attributs fournis par le partenaire pour enrichir les profils propriétaires **existants**, ces audiences enrichies en données de partenaire **seront** disponibles dans le portail d’audience et dans la composition d’audience pour être utilisées.

### Comment utiliser des attributs supplémentaires avec mes audiences ?

Avec les audiences, il existe **two** différents types d’attributs supplémentaires que vous pouvez ajouter : attributs de payload (contextuels) et attributs d’enrichissement.

Les attributs de payload sont des attributs ingérés dans le cadre du chargement au format CSV d’une audience générée de l’extérieur. Ces attributs sont **not** ingéré dans Real-time Customer Profile, mais peut être utilisé dans le cadre d’une destination en aval.

Les attributs d’enrichissement sont des attributs qui proviennent d’un jeu de données et qui sont associés à une audience dans la composition de l’audience. Actuellement, ces attributs ne peuvent être utilisés que dans les campagnes Adobe Journey Optimizer. La prise en charge des parcours Adobe Journey Optimizer est bientôt disponible, avec la prise en charge des destinations en aval dans l’attente d’une version ultérieure.

| Canal d’activation | Audiences à partir d’un téléchargement personnalisé CSV | Audiences de la composition de l’audience |
| --- | --- | --- |
| Destinations Real-Time CDP | Les attributs de payload et les audiences peuvent être activés. | Seule l’audience peut être activée. Attributs d’enrichissement **cannot** être activée. |
| Campagnes Adobe Journey Optimizer | Ni l’audience ni les attributs de payload ne peuvent être activés. | Les attributs audience et enrichissement peuvent être activés. |

## Inventaire de l’audience

Les sections suivantes répertorient les questions relatives à l’inventaire des audiences dans Audience Portal.

### Ai-je besoin d’autorisations supplémentaires pour utiliser les fonctionnalités d’inventaire des audiences ?

Non, ce n&#39;est pas le cas. Tant que vous disposez des autorisations de modification des audiences, vous pouvez créer, mettre à jour et gérer vos dossiers et balises dans le portail Audience. Pour plus d’informations sur la gestion des autorisations, consultez la section [guide de gestion des autorisations](../access-control/ui/permissions.md).

### Le nombre de dossiers que je peux créer est-il limité ?

Non, le nombre de dossiers que vous pouvez créer n’est pas limité. Pour plus d’informations sur les dossiers, veuillez lire le [section d’inventaire des audiences](./ui/overview.md#folders) de la présentation de l’interface utilisateur de Segmentation Service.

### Le nombre de balises pouvant être ajoutées à une audience est-il limité ?

Non, il n’existe pas de limite au nombre de balises pouvant être ajoutées à une audience. Pour plus d’informations sur les balises, veuillez lire le [section d’inventaire des audiences](./ui/overview.md#tags) de la présentation de l’interface utilisateur de Segmentation Service.

### Le nombre de balises que je peux créer est-il limité ?

Non, il n’y a pas de limite au nombre de balises que vous pouvez créer. Cependant, vous pouvez créer un maximum de **100** catégories à appliquer aux balises. Pour plus d’informations sur la gestion des balises, consultez la section [Guide de gestion des balises](../administrative-tags/ui/managing-tags.md).

### Lorsque je recherche une audience par nom ou balise dans un dossier parent, puis-je également effectuer une recherche dans les dossiers enfants associés ?

Non, ce comportement n’est pas pris en charge. Cependant, vous pouvez modifier la vue de l’inventaire de l’audience pour examiner **Toutes les audiences**, puis effectuez une recherche dans tous les dossiers. Pour plus d’informations sur l’utilisation de la recherche dans l’inventaire des audiences, veuillez lire la section [section de recherche](./ui/overview.md#search) de la présentation de l’interface utilisateur de Segmentation Service.

### Puis-je affecter automatiquement une audience à un dossier au moment de sa création ?

À ce stade, non. Toutefois, cette fonctionnalité pourrait être disponible à l’avenir.

### Puis-je déplacer plusieurs audiences simultanément dans un dossier ?

À ce stade, non. Toutefois, cette fonctionnalité pourrait être disponible à l’avenir.

## Composition de l’audience

La section suivante répertorie les questions relatives à la composition de l’audience.

### Quand dois-je utiliser la composition de l’audience plutôt que le créateur de segments ?

La composition de l’audience et le créateur de segments ont des rôles importants dans la création d’audiences dans Platform.

Le créateur de segments est plus adapté à l’audience **création** (pour créer une audience à partir de zéro), tandis que la composition de l’audience est plus adaptée à l’audience **traitement** (pour créer de nouvelles audiences basées sur une audience existante).

Le tableau suivant illustre la différence entre les deux services :

| Créateur de segments | Composition de l’audience |
| --------------- | -------------------- |
| <ul><li>Génération d’audiences à un seul niveau</li><li>Crée les blocs de base d’audiences à partir de données de profil, de séries temporelles et multi-entités.</li><li>Utilisé pour créer **one** audience</li></ul> | <ul><li>Génération d’audiences à plusieurs étapes, à l’aide d’opérations basées sur des ensembles</li><li>Utilise les audiences créées par le créateur de segments et applique les options d’enrichissement de données telles que le classement des attributs de profil</li><li>Utilisé pour créer **multiple** audiences à la fois</li></ul> |

Pour en savoir plus sur le créateur de segments, veuillez lire le [Guide du créateur de segments](./ui/segment-builder.md). Pour en savoir plus sur la composition de l’audience, veuillez lire le [Guide sur la composition de l’audience](./ui/audience-composition.md).

### Puis-je utiliser des audiences générées en externe dans la composition de l’audience ?

À ce stade, non. Cette fonctionnalité sera disponible dans un avenir proche.

### Puis-je envoyer des audiences de la composition d’audience à toutes les destinations et tous les canaux en aval ?

À ce stade, non. Pour l’instant, vous pouvez utiliser les audiences de la composition d’audience dans les campagnes Adobe Journey Optimizer et les destinations Real-time CDP. Les parcours Adobe Journey Optimizer seront pris en charge dans une version ultérieure.

### Existe-t-il des barrières de sécurité qui limitent le nombre de compositions ?

À ce stade, la limite est fixée à **10** compositions publiées par sandbox. Ce nombre devrait augmenter dans une prochaine version.

### Quelles sont les barrières de sécurité du workflow de composition d’audience ?

Le placement du composant de composition suit une structure rigide comme suit :

1. Vous commencez **toujours** par le bloc [!UICONTROL Audience] pour sélectionner votre activité de départ. Vous pouvez avoir un maximum d’**un** bloc [!UICONTROL Audience].
2. Vous pouvez éventuellement ajouter un bloc [!UICONTROL Exclure] qui suit le bloc [!UICONTROL Audience].
3. Vous pouvez éventuellement ajouter un bloc [!UICONTROL Enrichir] qui suit le bloc [!UICONTROL Exclure].
4. Vous pouvez éventuellement ajouter un bloc [!UICONTROL Classer] ou [!UICONTROL Partager]. Vous pouvez **uniquement** avoir l’un de ces blocs par composition.
5. Vous terminez **toujours** par un bloc [!UICONTROL Enregistrer] pour enregistrer votre audience.

Pour plus d’informations sur l’utilisation de la composition de l’audience, lisez le [Guide de l’interface utilisateur de la composition d’audience](./ui/audience-composition.md).

### Puis-je utiliser une composition d’audience dans une autre composition ?

Non, les audiences créées à l’aide de la composition de l’audience **ne peuvent pas** être utilisées comme entrée dans une autre composition d’audience.

### Comment le partage fonctionne-t-il dans la composition de l’audience ?

Le partage de l’audience vous permet de créer davantage de sous-ensembles de votre audience sous la forme de groupes plus petits. Ce partage force l’exclusivité mutuelle entre les groupes. Cela signifie que si un enregistrement répond aux critères de plusieurs chemins de partage, le **premier** chemin à partir de la gauche lui sera attribué et **pas** l’un des autres chemins.

Pour plus d’informations sur le bloc Partage, lisez le [Guide de l’interface utilisateur de composition d’audience](./ui/audience-composition.md#split).

### Puis-je utiliser tous les types de segmentation dans le workflow Composition de l’audience ?

Oui, tous les types de segmentation ([segmentation par lots, segmentation en flux continu et segmentation Edge](./home.md#evaluate-segments)) sont pris en charge dans le workflow Composition de l’audience. Toutefois, comme les compositions ne sont actuellement exécutées qu’une seule fois par jour, même si des audiences évaluées par Edge ou en flux continu sont incluses, le résultat sera basé sur l’appartenance à l’audience au moment de l’exécution de la composition.

## Comment puis-je confirmer l’appartenance d’un profil à une audience ?

Pour confirmer l’appartenance à l’audience d’un profil, consultez la page des détails de profil du profil que vous souhaitez confirmer. Sélectionnez **[!UICONTROL Attributs]**, puis **[!UICONTROL Afficher JSON]**, et vous pouvez confirmer que l’objet `segmentMembership` contient l’identifiant de l’audience.
