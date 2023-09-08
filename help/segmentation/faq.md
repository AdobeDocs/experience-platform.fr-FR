---
title: Questions fréquentes sur les audiences
description: Trouvez les réponses aux questions fréquentes sur les audiences.
source-git-commit: 4dbd20dd3ac596052a3390eb6d3731fac7095c0d
workflow-type: ht
source-wordcount: '996'
ht-degree: 100%

---


# Questions fréquentes

L’interface utilisateur et l’API RESTful du [!DNL Segmentation Service] d’Adobe Experience Platform vous permettent de créer des audiences par le biais de définitions de segment ou d’autres sources à partir de vos données [!DNL Real-Time Customer Profile]. Ces audiences sont configurées et conservées de manière centralisée sur Platform et sont facilement accessibles à partir de n’importe quelle solution Adobe. Vous trouverez ci-dessous les questions fréquentes sur les audiences et la segmentation.

## Puis-je accéder au portail d’audience et à la composition d’audience ?

Le portail d’audience et la composition d’audience sont disponibles pour tous les clientes et clients Real-Time CDP Prime et Ultimate (éditions B2C, B2B et B2P) et Journey Optimizer Select, Prime, Ultimate Starter et Ultimate.

Dans la version la plus récente de l’application, seules les audiences basées sur un profil sont prises en charge. La prise en charge des audiences basées sur un compte sera assurée dans une version ultérieure.

## Les audiences préconfigurées générées en externe sont-elles prises en charge par le portail d’audience ?

Oui, les audiences préconfigurées générées en externe sont prises en charge par le portail d’audience. Dans la version la plus récente de l’application, vous pouvez importer une audience générée en externe par le biais d’un fichier CSV. Dans une version ultérieure, vous pourrez ajouter des audiences par le biais de connecteurs source par lots ou en flux continu.

## Puis-je associer des données d’audience générées en externe à un profil existant dans Platform ?

Oui, l’audience générée en externe sera fusionnée avec le profil existant dans Platform si les identifiants principaux correspondent. L’intégration des données peut prendre jusqu’à 24 heures. Si les données de profil n’existent pas déjà, un profil est créé lors de l’ingestion des données.

## Puis-je utiliser une audience générée en externe pour créer d’autres audiences ?

Oui, les audiences générées en externe apparaîtront dans l’inventaire des audiences. elles peuvent être utilisés lors de la création d’audiences dans le [Créateur de segments](./ui/segment-builder.md).

## Puis-je utiliser des attributs téléchargés en externe dans le cadre de la segmentation ?

Non. Les attributs de profil sont censés être des attributs durables, tandis que les données d’audience générées en externe qui sont chargées ne contiennent que des données contextuelles associées à cette audience générée en externe.

Les données contextuelles de l’audience générée en externe, ou attributs d’enrichissement, possèdent une durée de vie **limitée**, car leur cycle de vie est lié à l’audience téléchargée. En raison de leur caractère éphémère, les attributs d’enrichissement ne sont **pas** disponibles dans la segmentation.

Cependant, lorsque vous mappez vos audiences vers des destinations par lots ou basées sur des fichiers, vous pouvez utiliser ces attributs d’enrichissement générés en externe pour élargir vos audiences et accroître les activations en aval.

Pour en savoir plus sur cette fonctionnalité, consultez le guide de l’[activation des données d’audience vers des destinations d’exportation de profils par lots](../destinations/ui/activate-batch-profile-destinations.md#mapping).

## Puis-je activer les audiences générées en externe dans Adobe Journey Optimizer ?

À ce stade, non. Cette fonctionnalité sera disponible dans un avenir proche.

## Puis-je supprimer une audience générée en externe ?

À ce stade, non. Comme solution de contournement, désactivez ou archivez l’audience. Notez que les profils **restent** disponibles dans les applications en aval. La prise en charge de la suppression des audiences générées en externe sera assurée dans une version ultérieure.

## Comment le portail d’audience et la composition d’audience interagiront-ils avec les données du partenaire Real-Time CDP ?

Le portail d’audience et la composition d’audience interagissent avec les données du partenaire de deux manières :

1. Si vous ingérez une liste de prospects fournie par le partenaire à l’aide de la classe et du workflow Prospect Profile, les prospects seront conservés **séparément** des profils clients de fusion dans le Profile Service. Cela signifie que les listes de prospects ne seront **pas** disponibles dans le portail d’audience ou dans la composition d’audience.
2. Si vous tirez parti des attributs fournis par le partenaire pour enrichir les profils propriétaires **existants**, ces audiences enrichies en données de partenaire **seront** disponibles dans le portail d’audience et dans la composition d’audience pour être utilisées.

## Puis-je utiliser des audiences générées en externe dans la composition de l’audience ?

À ce stade, non. Cette fonctionnalité sera disponible dans un avenir proche.

## Puis-je envoyer des audiences de la composition d’audience à toutes les destinations et tous les canaux en aval ?

À ce stade, non. Pour l’instant, vous pouvez utiliser les audiences de la composition d’audience dans les campagnes Adobe Journey Optimizer et les destinations Real-time CDP. Les parcours Adobe Journey Optimizer seront pris en charge dans une version ultérieure.

## Existe-t-il des barrières de sécurité qui limitent le nombre de compositions ?

À ce stade, la limite est fixée à **10** compositions publiées par sandbox. Ce nombre devrait augmenter dans une prochaine version.

## Quelles sont les barrières de sécurité du workflow de composition d’audience ?

Le placement du composant de composition suit une structure rigide comme suit :

1. Vous commencez **toujours** par le bloc [!UICONTROL Audience] pour sélectionner votre activité de départ. Vous pouvez avoir un maximum d’**un** bloc [!UICONTROL Audience].
2. Vous pouvez éventuellement ajouter un bloc [!UICONTROL Exclure] qui suit le bloc [!UICONTROL Audience].
3. Vous pouvez éventuellement ajouter un bloc [!UICONTROL Enrichir] qui suit le bloc [!UICONTROL Exclure].
4. Vous pouvez éventuellement ajouter un bloc [!UICONTROL Classer] ou [!UICONTROL Partager]. Vous pouvez **uniquement** avoir l’un de ces blocs par composition.
5. Vous terminez **toujours** par un bloc [!UICONTROL Enregistrer] pour enregistrer votre audience.

Pour plus d’informations sur l’utilisation de la composition de l’audience, lisez le [Guide de l’interface utilisateur de la composition d’audience](./ui/audience-composition.md).

## Puis-je utiliser une composition d’audience dans une autre composition ?

Non, les audiences créées à l’aide de la composition de l’audience **ne peuvent pas** être utilisées comme entrée dans une autre composition d’audience.

## Comment le partage fonctionne-t-il dans la composition de l’audience ?

Le partage de l’audience vous permet de créer davantage de sous-ensembles de votre audience sous la forme de groupes plus petits. Ce partage force l’exclusivité mutuelle entre les groupes. Cela signifie que si un enregistrement répond aux critères de plusieurs chemins de partage, le **premier** chemin à partir de la gauche lui sera attribué et **pas** l’un des autres chemins.

Pour plus d’informations sur le bloc Partage, lisez le [Guide de l’interface utilisateur de composition d’audience](./ui/audience-composition.md#split).

## Puis-je utiliser tous les types de segmentation dans le workflow Composition de l’audience ?

Oui, tous les types de segmentation ([segmentation par lots, segmentation en flux continu et segmentation Edge](./home.md#evaluate-segments)) sont pris en charge dans le workflow Composition de l’audience. Toutefois, comme les compositions ne sont actuellement exécutées qu’une seule fois par jour, même si des audiences évaluées par Edge ou en flux continu sont incluses, le résultat sera basé sur l’appartenance à l’audience au moment de l’exécution de la composition.

## Comment puis-je confirmer l’appartenance d’un profil à une audience ?

Pour confirmer l’appartenance à l’audience d’un profil, consultez la page des détails de profil du profil que vous souhaitez confirmer. Sélectionnez **[!UICONTROL Attributs]**, puis **[!UICONTROL Afficher JSON]**, et vous pouvez confirmer que l’objet `segmentMembership` contient l’identifiant de l’audience.
