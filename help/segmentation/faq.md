---
title: Questions fréquentes sur les audiences
description: Découvrez les réponses aux questions fréquentes sur les audiences.
source-git-commit: 4dbd20dd3ac596052a3390eb6d3731fac7095c0d
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---


# Questions fréquentes

Adobe Experience Platform [!DNL Segmentation Service] fournit une interface utilisateur et une API RESTful qui vous permettent de créer des audiences par le biais de définitions de segment ou d’autres sources à partir de vos [!DNL Real-Time Customer Profile] data. Ces audiences sont configurées et gérées de manière centralisée sur Platform et sont facilement accessibles par n’importe quelle solution d’Adobe. Vous trouverez ci-dessous une liste des questions fréquemment posées concernant les audiences et la segmentation.

## Ai-je accès à Audience Portal et à la composition de l’audience ?

Audience Portal et composition d’audience sont disponibles pour tous les clients Real-Time CDP Prime et Ultimate (éditions B2C, B2B et B2P) et les clients Journey Optimizer Select, Prime, Ultimate Starter et Ultimate.

À ce stade, seules les audiences basées sur un profil sont prises en charge. La prise en charge des audiences basées sur un compte sera ajoutée dans une version ultérieure.

## Les audiences préconfigurées générées en externe sont-elles prises en charge avec Audience Portal ?

Oui, les audiences préconfigurées générées en externe sont prises en charge avec Audience Portal. À ce stade, vous pouvez importer une audience générée en externe par le biais d’un fichier CSV. À l’avenir, vous pourrez ajouter des audiences par le biais de connecteurs source par lots ou en continu.

## Puis-je réconcilier des données d’audience générées en externe avec un profil existant dans Platform ?

Oui, l&#39;audience générée en externe sera fusionnée avec le profil existant dans Platform si les identifiants Principaux correspondent. La réconciliation de ces données peut prendre jusqu&#39;à 24 heures. Si les données de profil n’existent pas déjà, un nouveau profil est créé lors de l’ingestion des données.

## Puis-je utiliser une audience générée de l’extérieur pour créer d’autres audiences ?

Oui, toute audience générée de l’extérieur apparaîtra dans l’inventaire des audiences et peut être utilisée lors de la création d’audiences dans la variable [Créateur de segments](./ui/segment-builder.md).

## Puis-je utiliser des attributs téléchargés en externe dans le cadre de la segmentation ?

Non, vous ne pouvez pas. Les attributs de profil sont censés être des attributs durables, tandis que les données d’audience générées en externe qui sont téléchargées contiennent uniquement des données contextuelles associées à cette audience générée en externe.

Les données contextuelles de l’audience générées de l’extérieur, ou attributs d’enrichissement, sont **not** durablement, car leur cycle de vie est lié à l’audience chargée. Par conséquent, en raison de sa nature transitoire, ces attributs d’enrichissement sont **not** disponible dans la segmentation.

Cependant, lorsque vous mappez vos audiences vers des destinations basées sur des lots ou des fichiers, vous pouvez utiliser ces attributs d’enrichissement générés en externe pour augmenter vos audiences et d’autres activations en aval.

Pour en savoir plus sur cette fonctionnalité, veuillez lire le guide sur [activation des données d’audience vers des destinations d’exportation de profils par lots](../destinations/ui/activate-batch-profile-destinations.md#mapping).

## Puis-je activer les audiences générées en externe vers Adobe Journey Optimizer ?

A ce stade, non. Toutefois, cette fonctionnalité sera disponible dans un avenir proche.

## Puis-je supprimer une audience générée de l’extérieur ?

A ce stade, non. Vous pouvez désactiver ou archiver cette audience à la place. Dans cet état, les profils **will** restent principales à utiliser dans les applications en aval. La prise en charge de la suppression des audiences générées en externe sera ajoutée dans une version ultérieure.

## Comment Audience Portal et la composition de l’audience interagiront-ils avec la publication des données du partenaire Real-Time CDP ?

Audience Portal et la composition de l’audience interagissent avec les données du partenaire de deux manières :

1. Si vous ingérez une liste de prospects fournie par les partenaires à l’aide de la classe Profil de prospects et du workflow, les prospects seront conservés. **distinct** à partir de la fusion de profils client dans Profile Service. En conséquence, cela signifie que les listes de prospects seront **not** apparaissent dans Audience Portal ou dans Composition de l’audience pour utilisation.
2. Si vous utilisez les attributs fournis par les partenaires pour enrichir **existant** profils propriétaires, ces audiences enrichies en données de partenaire **will** s’affichent dans Audience Portal et dans la composition de l’audience pour utilisation.

## Puis-je utiliser des audiences générées en externe dans la composition de l’audience ?

A ce stade, non. Toutefois, cette fonctionnalité devrait être disponible dans un avenir proche.

## Puis-je envoyer des audiences de la composition de l’audience vers toutes les destinations et tous les canaux en aval ?

A ce stade, non. Actuellement, vous pouvez utiliser les audiences de la composition de l’audience dans les campagnes Adobe Journey Optimizer et les destinations de la plateforme de données clients en temps réel. Adobe Journey Optimizer Parcours sera pris en charge dans une version ultérieure.

## Y a-t-il des barrières de sécurité sur le nombre de compositions ?

À ce stade, vous pouvez uniquement avoir **10** publications par environnement de test. Cette barrière de sécurité devrait être renforcée dans une prochaine version.

## Quelles sont les barrières de sécurité de workflow pour la composition de l’audience ?

Le placement du composant de composition suit une structure rigide comme suit :

1. You **always** commencer par le [!UICONTROL Audience] pour sélectionner votre activité de départ. Vous pouvez avoir un maximum de **one** [!UICONTROL Audience] block.
2. Vous pouvez éventuellement ajouter une [!UICONTROL Exclure] qui suit le bloc [!UICONTROL Audience] block.
3. Vous pouvez éventuellement ajouter une [!UICONTROL Enrichir] qui suit le bloc [!UICONTROL Exclure] block.
4. Vous pouvez éventuellement ajouter une [!UICONTROL Classement] ou [!UICONTROL Partage] block. Vous pouvez **only** avoir l&#39;un de ces blocs par composition ;
5. You **always** se terminer par un [!UICONTROL Enregistrer] pour sauvegarder votre audience.

Pour plus d’informations sur l’utilisation de la composition de l’audience, veuillez lire la section [Guide de l’interface utilisateur de composition d’audience](./ui/audience-composition.md).

## Puis-je utiliser une composition d’audience dans une autre composition ?

Non, audiences créées à l’aide de la composition de l’audience **cannot** être utilisée comme entrée dans une autre composition d’audience.

## Comment la division fonctionne-t-elle dans la composition de l’audience ?

Le fractionnement de l’audience vous permet de sous-définir davantage votre audience en groupes plus petits. Cette division force l&#39;exclusivité mutuelle entre les groupes. Cela signifie que si un enregistrement répond aux critères de plusieurs chemins de division, il se verra attribuer la variable **first** chemin à partir de la gauche et **not** affectés à l’un des autres chemins.

Pour plus d&#39;informations sur le bloc Partage, veuillez lire le [Guide de l’interface utilisateur de composition d’audience](./ui/audience-composition.md#split).

## Puis-je utiliser tous les types de segmentation dans le workflow Composition de l’audience ?

Oui, tous les types de segmentation ([segmentation par lots, segmentation par flux et segmentation par périphérie](./home.md#evaluate-segments)) sont pris en charge dans le workflow Composition de l’audience . Toutefois, comme les compositions ne sont actuellement exécutées qu’une seule fois par jour, même si des audiences évaluées en périphérie ou en flux continu sont incluses, le résultat sera basé sur l’appartenance à l’audience au moment de l’exécution de la composition.

## Comment puis-je confirmer l’appartenance d’un profil à une audience ?

Pour confirmer l’appartenance à l’audience d’un profil, consultez la page des détails du profil du profil que vous souhaitez confirmer. Sélectionner **[!UICONTROL Attributs]**, suivie de **[!UICONTROL Afficher JSON]**, et vous pouvez confirmer que la variable `segmentMembership` contient l’identifiant de l’audience.
