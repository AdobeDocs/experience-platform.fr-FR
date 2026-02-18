---
keywords: Experience Platform;profil;profil client en temps réel;schéma;jeu de données;planification;activation
solution: Experience Platform
title: Planification de l’activation du profil client en temps réel
description: Passez en revue les principales considérations à prendre en compte avant d’activer des schémas et des jeux de données pour le profil client en temps réel.
source-git-commit: da40dfde57b17b6a7387451eec48569174ad544b
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 0%

---

# Planification de l’activation du profil client en temps réel

Utilisez cette page pour confirmer que votre schéma et votre jeu de données sont prêts avant de les activer pour le profil client en temps réel. Effectuez cette révision de planification après avoir conçu vos champs de schéma, mais avant d’activer le schéma pour Profile. L’activation du profil applique des changements de comportement permanents à votre modèle de données. Vous ne pouvez pas annuler l’activation du schéma. En outre, l’activation d’un jeu de données affecte le traitement de ses enregistrements dans le profil client en temps réel. Consultez ces conseils pour éviter toute activation involontaire, tout problème de qualité des données ou toute contrainte à long terme dans la conception de votre schéma.

L’activation du profil détermine la manière dont vos données sont regroupées, fusionnées et activées dans Experience Platform. La planification garantit que la structure du schéma, la configuration de l’identité et l’objectif du jeu de données sont corrects avant d’effectuer la modification. Une fois la révision de la planification terminée, vous pouvez activer les données du profil dans l’interface utilisateur de **[!UICONTROL Schema Editor]** ou de **[!UICONTROL Dataset]**.

## Conditions préalables

Avant d’utiliser ce guide de planification, vérifiez que vous disposez des éléments suivants :

* Concevoir un schéma à l’aide de l’API **[!UICONTROL Schema Editor]** ou Schema Registry. Pour commencer, consultez le [tutoriel sur la création de schémas](../tutorials/create-schema-ui.md).
* configuré au moins un champ d’identité dans votre schéma. Consultez le [guide de configuration des champs d’identité](../ui/fields/identity.md) pour obtenir des instructions.
* Compréhension de base du [profil client en temps réel](../../profile/home.md) et de la manière dont il utilise des schémas pour créer des vues client unifiées.
* Autorisations appropriées pour activer les schémas et les jeux de données pour le profil. Contactez votre administrateur système si vous n’avez pas accès aux options d’activation du profil.

Si vous n’avez pas terminé ces conditions préalables, commencez par suivre le tutoriel [création de schémas](../tutorials/create-schema-ui.md) avant de poursuivre avec ce guide de planification.

## Pourquoi la planification est importante {#why-planning-matters}

L’activation du profil modifie définitivement la manière dont Experience Platform traite vos données. Les modifications permanentes suivantes s’appliquent aux schémas et aux jeux de données.

**Schémas** : lorsque vous activez un schéma pour le profil, vous ne pouvez pas le désactiver ni le supprimer. Vous ne pouvez pas non plus supprimer ou renommer les champs du schéma une fois les données ingérées. Cette permanence signifie que votre conception de schéma doit être complète et stable avant d’activer Profile, car vous ne pouvez pas inverser la décision ou simplifier la structure ultérieurement.

**Jeux de données** : lorsque vous activez un jeu de données pour Profil, le profil client en temps réel utilise ses enregistrements pour créer et mettre à jour des profils. Examinez le comportement d’activation des jeux de données dans le [guide d’utilisation des jeux de données](../../catalog/datasets/enable-for-profile.md). Contrairement aux schémas, vous pouvez désactiver ou supprimer le jeu de données ultérieurement, mais en supprimant les enregistrements de profil associés, vous pouvez affecter les workflows de segmentation ou d’activation. Tenez compte de l’impact en aval avant d’apporter des modifications à un jeu de données activé.

Comme ces modifications affectent les processus en aval, vérifiez qu’un schéma et ses jeux de données sont appropriés pour Profile avant de les activer.

### Présentation du workflow d’activation

Vous devez activer le schéma ET les jeux de données qui utilisent ce schéma pour Profile. Activez les ressources dans l’ordre suivant :

1. **Activer le schéma pour Profil** : tout d’abord, activez Profil sur le schéma dans le **[!UICONTROL Schema Editor]**. Cela permet à tout jeu de données utilisant ce schéma d’être activé pour Profil.
2. **Activer les jeux de données individuels pour le profil** : une fois le schéma activé, activez le profil sur chaque jeu de données qui doit contribuer aux profils clients unifiés.

Vous ne pouvez pas activer un jeu de données pour Profil si son schéma n’est pas déjà activé. Le schéma agit comme une condition préalable à l’activation du jeu de données. Ce processus en deux étapes garantit que votre modèle de données est validé avant que le profil client en temps réel ne commence le traitement des enregistrements.

## Quand activer un schéma ou un jeu de données pour Profil {#when-to-enable}

Examinez les critères ci-dessous pour confirmer que l’activation du profil est appropriée pour vos données.

Activez Profile dans les situations suivantes :

* Les données contribuent à un profil client unifié.
* Les données sont requises pour les workflows de segmentation ou d’activation.
* Le schéma comprend des champs d’identité qui représentent une clé au niveau d’une personne ou d’un client.
* Le jeu de données contient des événements d’expérience ou des attributs de profil qui doivent être regroupés sur plusieurs canaux. Consultez la [classe XDM ExperienceEvent](../classes/experienceevent.md) pour confirmer les exigences en matière d’événement.

## Lorsque vous ne souhaitez pas activer un schéma ou un jeu de données pour le profil {#when-not-to-enable}

Évitez d’activer Profile dans les cas suivants :

* Le schéma représente les données de recherche ou de référence uniquement.
* Le jeu de données contient des données de test, temporaires ou hors production.
* Les données n’identifient pas de personne ou ne sont utilisées que pour la création de rapports.
* Le schéma est expérimental ou structurellement incomplet.

L’activation d’un profil dans ces scénarios peut créer des profils inutiles, augmenter l’utilisation des licences ou introduire des contraintes de schéma à long terme.

## Considérations principales avant d’activer Profile {#key-considerations}

Examinez les points à prendre en compte dans cette section pour vous assurer que votre schéma et votre jeu de données prennent en charge les cas d’utilisation de profil et la gouvernance des données à long terme. Avant d’activer Profile, vérifiez la structure de votre schéma, la configuration des identités et l’objectif du jeu de données.

### Préparation du schéma

Examinez la structure du schéma pour confirmer qu’elle prend en charge les exigences de Profile. Le schéma doit contenir les champs requis pour la segmentation et l’activation, tout en excluant les champs qui sont expérimentaux ou qui ne sont pas nécessaires à long terme. N’oubliez pas que tous les champs supplémentaires que vous ajoutez après l’activation doivent être additifs (voir [Contraintes d’immuabilité des schémas](#why-planning-matters) pour plus d’informations). Cette restriction signifie que vous devez valider soigneusement votre sélection de champ avant d’activer Profile. Pour plus d’informations sur les mises à jour autorisées, consultez le [règles d’évolution des schémas](./composition.md#evolution).

### Configuration de l’identité

La configuration des identités détermine la manière dont Profile regroupe les enregistrements dans les jeux de données. Commencez par confirmer qu’une identité principale valide est sélectionnée : ce champ doit être stable, unique et systématiquement renseigné sur tous les enregistrements. Vérifiez que les espaces de noms d’identité sont correctement attribués pour éviter les erreurs de groupement. Si vous utilisez des identités secondaires, vérifiez qu’elles prennent en charge vos cas d’utilisation sans provoquer de conflits de profils, ce qui peut se produire lorsque différents individus partagent la même valeur d’identité. Le profil client en temps réel résout les conflits en appliquant des politiques de fusion qui déterminent quelles données sont prioritaires lorsque des enregistrements en conflit sont regroupés.

### Objectif du jeu de données

Activez un jeu de données pour Profil uniquement s’il contribue directement aux attributs de profil ou aux événements d’expérience utilisés dans les workflows en aval. Évitez d’activer des jeux de données contenant des données de recherche ou de référence non utilisées dans la segmentation, des données de test ou d’exemple, ou des enregistrements générés par le système d’exploitation non destinés à être activés. Ces types de données ne contribuent pas aux profils clients unifiés et créent une surcharge de stockage inutile. Si un jeu de données ne contient pas de champs d’identité ou de données de comportement client prenant en charge la segmentation et l’activation, ne l’activez pas pour le profil.

**Exemple** :

Vous activez un jeu de données « Événements d’achat client » contenant des données de transaction avec des ID client. Le profil client en temps réel utilise ces événements pour créer des chronologies client et activer la segmentation en fonction du comportement d’achat.

Vous n’activez PAS un jeu de données « Catalogue de produits » contenant uniquement des données de référence de SKU sans identifiants de client. L’activation de ce type de jeu de données crée une surcharge de stockage inutile sans contribuer aux profils clients unifiés.

## Liste de contrôle de pré-activation {#pre-enablement-checklist}

Utilisez cette liste de contrôle pour confirmer la préparation avant d’activer un schéma ou un jeu de données pour Profile. Terminez chaque élément avant d’activer le profil.

### Vérifications au niveau du schéma

Commencez par vérifier que la conception de votre schéma est complète et stable. Vérifiez votre schéma pour confirmer que tous les champs requis pour votre cas d’utilisation sont présents et qu’aucun champ expérimental ou temporaire n’est inclus. Consultez les [ bonnes pratiques relatives à la conception de schéma ](./best-practices.md) pour vous assurer que votre schéma suit les modèles recommandés. Obtenez l’approbation de votre équipe sur la liste de champs finale (voir [ Contraintes d’immuabilité des schémas ](#why-planning-matters)).

Ensuite, vérifiez que la configuration de votre identité principale est correcte. Ouvrez votre schéma dans le **[!UICONTROL Schema Editor]** et localisez le champ marqué de l’icône d’identité. Vérifiez que ce champ est systématiquement renseigné dans vos données source et que l’espace de noms d’identité est approprié à votre cas d’utilisation. L’identité principale doit être stable, unique et présente de manière fiable sur tous les enregistrements pour garantir un assemblage correct des profils.

Enfin, vérifiez que vous n’avez pas besoin de renommer ou de réorganiser la structure du schéma. Les modifications de la structure du schéma sont limitées aux mises à jour additifs uniquement (voir [contraintes d’immuabilité du schéma](#why-planning-matters)). Toute ambiguïté à long terme dans le nom ou l’organisation ne peut pas être corrigée ultérieurement. Résolvez donc ces problèmes avant l’activation.

### Vérifications au niveau du jeu de données

Pour chaque jeu de données que vous prévoyez d’activer, commencez par confirmer qu’il contient des données pertinentes pour le profil. Consultez des exemples d’enregistrements pour vérifier qu’ils contiennent des données client ou d’événement plutôt que des informations purement opérationnelles ou de référence. Assurez-vous que les enregistrements incluent des valeurs d’identité liées aux profils client. Les jeux de données sans champ d’identité ou données de comportement du client ne doivent pas être activés pour Profil.

Déterminez si le jeu de données doit contribuer à la combinaison d’identités ou à la segmentation en comprenant la manière dont ses valeurs d’identité sont liées à d’autres jeux de données dans votre environnement activé pour Profile. Indiquez si les enregistrements de ce jeu de données doivent être regroupés avec des profils existants ou créer des fragments de profil. Consultez la [documentation sur la politique de fusion](../../profile/merge-policies/overview.md) pour comprendre comment le profil client en temps réel regroupe des enregistrements dans les jeux de données et comment ce jeu de données s’intègre dans votre stratégie d’identité globale.

Avant d’activer le jeu de données, estimez le nombre de valeurs d’identité uniques qu’il contient et vérifiez que ces valeurs d’identité représentent des clients réels plutôt que des comptes de test ou des identifiants système. Vérifiez que l’activation de ce jeu de données correspond à vos droits de licence, car chaque identité unique contribue à votre nombre de profils des audiences adressable. L’activation du profil augmente les coûts de stockage et de traitement. Assurez-vous donc que le jeu de données fournit la valeur qui justifie cet investissement.

La réalisation de cette liste de contrôle permet d’éviter les problèmes qui ne peuvent pas être résolus après l’activation.

## Activation du profil pour votre schéma et votre jeu de données {#enable-profile}

Une fois la liste de contrôle de préactivation terminée, procédez comme suit pour activer le profil. Comme expliqué dans la section [Comprendre le workflow d’activation](#why-planning-matters), vous devez activer le schéma avant d’activer les jeux de données qui utilisent ce schéma.

### Activation du schéma pour Profil

Commencez par activer le profil sur votre schéma :

1. Accédez à **[!UICONTROL Schemas]** dans l’interface utilisateur d’Experience Platform.
2. Sélectionnez le schéma dans la liste pour l’ouvrir dans la **[!UICONTROL Schema Editor]**.
3. Sélectionnez le bouton (bascule) **[!UICONTROL Profile]** dans le rail de droite. Le panneau des propriétés du schéma affiche une boîte de dialogue de confirmation.
4. Sélectionnez **[!UICONTROL Enable]** pour confirmer. Le schéma est maintenant activé pour Profil.

Pour obtenir des instructions détaillées, consultez le [guide d’activation des schémas](../ui/resources/schemas.md#profile) dans la documentation de l’éditeur de schémas.

### Activer vos jeux de données pour le profil

Une fois que votre schéma est activé pour Profil, activez chaque jeu de données qui doit contribuer aux profils unifiés :

1. Accédez à **[!UICONTROL Datasets]** dans l’interface utilisateur d’Experience Platform.
2. Sélectionnez un jeu de données dans la liste pour ouvrir la page des détails du jeu de données.
3. Sélectionnez le bouton (bascule) **[!UICONTROL Profile]** dans le rail de droite. Le panneau des propriétés du jeu de données se met à jour pour afficher le profil activé.

Répétez ce processus pour chaque jeu de données qui doit contribuer au profil client en temps réel. Pour obtenir des instructions détaillées et des options d’activation des API, consultez le guide d’utilisation des jeux de données référencé dans la section Conditions préalables .

### L’importance de l’ordre

Comme expliqué dans la section [Présentation du workflow d’activation](#why-planning-matters), vous devez activer le schéma avant d’activer les jeux de données. Cela garantit que le profil client en temps réel valide la structure du schéma prend en charge les opérations de profil avant d’autoriser l’activation des jeux de données et que tous les jeux de données utilisant le schéma héritent des définitions de champ correctes pour la segmentation et l’assemblage d’identités.

Une fois que vous avez activé le schéma et les jeux de données, le profil client en temps réel commence à traiter les enregistrements et à créer des profils clients unifiés. Les enregistrements ingérés avant l’activation ne sont pas inclus dans les profils, sauf si vous réingérez les données.

## Étapes suivantes {#next-steps}

Vous avez examiné les effets permanents de l’activation du profil, confirmé que votre schéma et vos jeux de données sont prêts et validé que votre configuration d’identité prend en charge vos cas d’utilisation. Pour mieux comprendre la structure du schéma et les relations entre les champs, consultez la [Principes de base de la composition des schémas](../schema/composition.md) qui explique les règles d’évolution des schémas et la manière dont les champs interagissent dans le modèle de données. Si vous rencontrez des problèmes pendant ou après l’activation, consultez le guide de dépannage [XDM](../troubleshooting-guide.md) pour connaître les problèmes courants et les solutions. Pour en savoir plus sur la manière dont les espaces de noms d’identité affectent l’assemblage et la résolution des profils, consultez la [ présentation des espaces de noms d’identité](../../identity-service/features/namespaces.md).
