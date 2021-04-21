---
keywords: Experience Platform ; profil ; profil client en temps réel ; stratégies de fusion ; interface utilisateur ; interface utilisateur ; horodatage ordonné ; priorité du jeu de données
title: Guide de l’interface utilisateur des stratégies de fusion
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform vous permet de rassembler des fragments de données provenant de plusieurs sources et de les combiner afin d’obtenir une vue complète de chacun de vos clients. Lorsque ces données sont regroupées, les stratégies de fusion sont les règles utilisées par Plateforme pour déterminer comment les données seront hiérarchisées et quelles données seront combinées pour créer une vue unifiée.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '3017'
ht-degree: 8%

---

# Guide de l’interface utilisateur des stratégies de fusion

Adobe Experience Platform vous permet de rassembler des fragments de données provenant de plusieurs sources et de les combiner afin d’obtenir une vue complète de chacun de vos clients. Lorsque ces données sont regroupées, les stratégies de fusion sont les règles que [!DNL Platform] utilise pour déterminer comment les données seront hiérarchisées et quelles données seront combinées pour créer une vue unifiée.

Par exemple, si un client interagit avec votre marque sur plusieurs canaux, votre entreprise aura plusieurs fragments de profil liés à ce client unique qui apparaîtront dans plusieurs jeux de données. Lorsque ces fragments sont ingérés dans la plate-forme, ils sont fusionnés ensemble afin de créer un profil unique pour ce client. Lorsque les données provenant de plusieurs sources entrent en conflit (par exemple, un fragment liste le client comme &quot;unique&quot; tandis que les autres listes le client comme &quot;marié&quot;), la stratégie de fusion détermine les informations à inclure dans le profil de la personne.

À l’aide d’API RESTful ou de l’interface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre organisation dans l’interface utilisateur. Ce guide fournit des instructions détaillées sur l’utilisation des stratégies de fusion à l’aide de l’interface utilisateur de Adobe Experience Platform.

Si vous préférez utiliser des stratégies de fusion à l&#39;aide de l&#39;API [!DNL Real-time Customer Profile], suivez les instructions décrites dans le [guide de l&#39;API des stratégies de fusion](../api/merge-policies.md).

## Prise en main

Ce guide nécessite une bonne compréhension de plusieurs fonctions [!DNL Experience Platform] importantes. Avant de suivre ce guide ou d&#39;utiliser les API de Profil, consultez la documentation relative aux services suivants :

* [Real-time Customer Profile](../home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Service](../../identity-service/home.md) d&#39;identité Adobe Experience Platform : Permet le Profil client en temps réel en rapprochant les identités de sources de données disparates qui sont absorbées  [!DNL Platform].
* [Modèle de données d’expérience (XDM)](../../xdm/home.md)[!DNL Platform] : cadre normalisé selon lequel Experience organise les données d’expérience client.

## Fusionner les méthodes {#merge-methods}

Chaque fragment de profil contient des informations relatives à une seule identité sur le nombre total d&#39;identités pouvant exister pour un individu. Lors de la fusion de ces données pour former un profil client, il existe un risque que ces informations soient en conflit et la priorité doit être spécifiée. La sélection d’une méthode de fusion vous permet de spécifier les attributs de jeu de données à classer par priorité en cas de conflit de fusion entre les jeux de données.

Il existe deux méthodes de fusion possibles pour les stratégies de fusion. Chacune de ces méthodes est résumée ci-dessous et des détails supplémentaires sont fournis dans les sections suivantes :

* **[!UICONTROL Horodatage ordonné] :** En événement de conflit, la priorité est accordée au fragment de profil qui a été mis à jour le plus récemment.
   * **Horodatages personnalisés :** [!UICONTROL Horodatage ] ordonné prend également en charge les horodatages personnalisés qui ont la priorité sur les horodatages système lors de la fusion de données dans un même jeu de données (identités multiples) ou dans plusieurs jeux de données. Pour en savoir plus, consultez la section [en utilisant des horodatages personnalisés](#custom-timestamps).
* **[!UICONTROL Priorité] du jeu de données :** dans le événement d’un conflit, donnez la priorité aux fragments de profil en fonction du jeu de données à partir duquel ils sont arrivés. Lorsque vous sélectionnez cette option, vous devez choisir les jeux de données connexes et leur ordre de priorité.

### Horodatage commandé {#timestamp-ordered}

Comme les enregistrements de profil sont ingérés dans l&#39;Experience Platform, un horodatage système est obtenu au moment de l&#39;assimilation et ajouté à l&#39;enregistrement. Lorsque **[!UICONTROL Horodatage ordonné]** est sélectionné comme méthode de fusion pour une stratégie de fusion, les profils sont fusionnés en fonction de l’horodatage système. En d’autres termes, la fusion est effectuée en fonction de l’horodatage du moment où l’enregistrement a été ingéré dans la plate-forme.

#### Utilisation d’horodatages personnalisés {#custom-timestamps}

Parfois, il peut être nécessaire de fournir un horodatage personnalisé et de faire en sorte que la stratégie de fusion respecte l’horodatage personnalisé plutôt que l’horodatage système. Par exemple, le renvoi de données ou la vérification de l’ordre correct des événements en cas d’assimilation irrégulière d’enregistrements.

Pour utiliser un horodatage personnalisé, le **[!UICONTROL Mixin des détails de l&#39;audit du système source externe]** doit être ajouté à votre schéma de Profil. Une fois ajouté, l’horodatage personnalisé peut être renseigné à l’aide du champ `lastUpdatedDate`. Lorsqu&#39;un enregistrement est assimilé au champ `lastUpdatedDate` renseigné, l&#39;Experience Platform utilise ce champ pour fusionner des enregistrements dans des jeux de données. Si `lastUpdatedDate` n&#39;est pas présent ou n&#39;est pas renseigné, Platform continuera à utiliser l&#39;horodatage système.

>[!NOTE]
>
>Vous devez vous assurer que l&#39;horodatage `lastUpdatedDate` est renseigné lors de l&#39;importation d&#39;une mise à jour sur le même enregistrement.

La capture d&#39;écran suivante affiche les champs du [!UICONTROL Mixin des détails de l&#39;audit du système source externe ]. Pour obtenir des instructions détaillées sur l’utilisation des schémas à l’aide de l’interface utilisateur de la plate-forme, y compris sur la façon d’ajouter des mixins aux schémas, consultez le [didacticiel sur la création d’un schéma à l’aide de l’interface utilisateur](../../xdm/tutorials/create-schema-ui.md).

![](../images/merge-policies/custom-timestamp-mixin.png)

Pour utiliser des horodatages personnalisés à l’aide de l’API, reportez-vous à la section [du guide des points de terminaison des stratégies de fusion sur l’utilisation des horodatages personnalisés](../api/merge-policies.md#custom-timestamps).

### Priorité du jeu de données {#dataset-precedence}

Lorsque **[!UICONTROL La priorité du jeu de données]** est sélectionnée comme méthode de fusion pour une stratégie de fusion, vous pouvez donner la priorité aux fragments de profil en fonction du jeu de données dont ils proviennent. Par exemple, un cas d’utilisation serait la présence d’informations de votre organisation dans un jeu de données que vous préférez ou dont les données sont davantage de confiance par rapport à un autre jeu de données.

Pour créer une stratégie de fusion à l’aide de **[!UICONTROL l’ordre de priorité des jeux de données]**, vous devez sélectionner les jeux de données Profil et ExperienceEvent qui sont inclus, puis vous pouvez trier manuellement les jeux de données de Profil par priorité. Une fois les jeux de données sélectionnés et triés, le jeu de données le plus important aura la priorité la plus élevée, le deuxième jeu de données sera le deuxième plus élevé, etc.

## [!UICONTROL Accrochage des identifiants] {#id-stitching}

L’assemblage d’identités ([!UICONTROL l’assemblage d’identifiants]) est le processus d’identification des fragments de données et de combinaison pour former un enregistrement de profil complet. Pour illustrer les différents comportements d’assemblage, considérez un client unique qui interagit avec une marque à l’aide de deux adresses électroniques différentes.

* **[!UICONTROL Aucun] :** lorsque cette option est sélectionnée, les ID ne sont pas assemblés ensemble. Lors de la segmentation, les identités qui peuvent appartenir à la même personne ne sont pas assemblées et la segmentation ne prend en compte que les attributs associés à chaque ID individuel lorsqu’elle détermine si un client est admissible pour l’appartenance au segment. Cela peut se traduire par l’existence de plusieurs profils pour un client unique et par la possibilité que chaque profil soit admissible pour des segments différents, ce qui se traduit par l’envoi de plusieurs messages marketing au même client.
* **[!UICONTROL Graphique] privé :** lorsque le graphique privé est sélectionné, plusieurs identités liées à la même personne sont assemblées ensemble. Ainsi, le client dispose d’un profil unique et permet à la segmentation de prendre en compte plusieurs attributs provenant de plusieurs identités liées lors de la détermination de la qualification de segment. Dans ce scénario, le client est susceptible d’avoir un seul profil, de se qualifier pour un segment en fonction de la combinaison d’attributs entre les identités et de ne recevoir qu’un seul message marketing.

Pour en savoir plus sur les identités et leur rôle dans la génération de profils et de segments, veuillez commencer par lire la [Présentation du service d&#39;identité](../../identity-service/home.md).

## Stratégie de fusion par défaut {#default-merge-policy}

Une organisation peut créer une stratégie de fusion par défaut à utiliser pour son organisation lors de la fusion de fragments de profil. Cela permet aux utilisateurs de sélectionner facilement la stratégie par défaut lorsqu’ils effectuent des actions dans un Experience Platform, telles que l’affichage de profils client ou la création de segments. Dans la plupart des cas, à moins qu’une autre stratégie de fusion ne soit spécifiée, la stratégie de fusion par défaut est utilisée.

Chaque organisation peut créer plusieurs stratégies de fusion liées à une seule classe de schéma XDM, mais une seule stratégie de fusion par défaut peut être déclarée pour chaque classe. Par exemple, votre organisation peut avoir une stratégie de fusion par défaut associée à la classe [!DNL XDM Individual Profile] et une autre stratégie de fusion par défaut pour une classe d&#39;inventaire de produits personnalisée.

Si vous créez une nouvelle stratégie de fusion et la définissez comme stratégie par défaut, la précédente stratégie de fusion par défaut sera automatiquement mise à jour par le système pour ne plus être la stratégie par défaut.

>[!WARNING]
>
>Le nombre de profils et les segments associés à une stratégie de fusion par défaut existante peuvent être affectés. Tout segment auquel une stratégie de fusion par défaut est appliquée sera mis à jour vers la nouvelle stratégie de fusion par défaut.

## Affichage des stratégies de fusion {#view-merge-policies}

Dans l&#39;interface utilisateur [!DNL Experience Platform], vous pouvez commencer à utiliser des stratégies de fusion en sélectionnant **[!UICONTROL Profils]** dans le volet de navigation de gauche, puis en sélectionnant l&#39;onglet **[!UICONTROL Fusionner les stratégies]**. Cet onglet comprend une liste de toutes les stratégies de fusion existantes pour votre organisation, ainsi que des détails pour chaque stratégie de fusion, y compris le nom de la stratégie, si la stratégie de fusion est la stratégie de fusion par défaut ou non et la classe de schéma à laquelle la stratégie de fusion se rapporte.

![Page d’entrée des stratégies de fusion](../images/merge-policies/landing.png)

Pour sélectionner les détails visibles ou ajouter d&#39;autres colonnes à l&#39;affichage, sélectionnez **[!UICONTROL Configurer des colonnes]** et cliquez sur le nom d&#39;une colonne pour l&#39;ajouter ou la supprimer de la vue.

![](../images/merge-policies/adjust-view.png)

## Création d’une stratégie de fusion {#create-a-merge-policy}

Pour créer une stratégie de fusion, sélectionnez **[!UICONTROL Créer une stratégie de fusion]** dans l&#39;onglet Stratégies de fusion.

![Fusionnez le landing page de stratégies avec le bouton Créer en surbrillance.](../images/merge-policies/create-new.png)

Dans l&#39;écran de flux de travaux **[!UICONTROL Nouvelle stratégie de fusion]**, vous pouvez fournir des informations importantes pour votre nouvelle stratégie de fusion au moyen d&#39;une série d&#39;étapes guidées.

![Nouveau processus de stratégie de fusion.](../images/merge-policies/create.png)

### [!UICONTROL Configuration] {#configure}

La première étape du processus vous permet de configurer votre stratégie de fusion en fournissant des informations de base. Ces informations comprennent :

* **[!UICONTROL Nom]** : le nom de votre stratégie de fusion devrait être descriptif, mais concis.
* **[!UICONTROL Classe]** de schéma : Classe de schéma XDM associée à la stratégie de fusion. Indique la classe de schéma pour laquelle cette stratégie de fusion est créée. Les organisations peuvent créer plusieurs stratégies de fusion par classe de schéma. Actuellement, seule la classe [!UICONTROL Profil individuel XDM] est disponible dans l’interface utilisateur. Vous pouvez prévisualisation le schéma d&#39;union pour la classe schéma en sélectionnant **[!UICONTROL Schéma d&#39;Union de Vue]**. Pour plus d&#39;informations, consultez la section [Affichage du schéma d&#39;union](#view-union-schema) qui suit.
* **[!UICONTROL Combinaison d’identités]** : ce champ définit la manière de déterminer les identités liées d’un client. Pour en savoir plus, consultez la section [assemblage d’identifiants](#id-stitching) plus tôt dans ce guide. Deux valeurs sont possibles :
   * **[!UICONTROL Aucun]** : ne réalise pas de combinaison d’identités.
   * **[!UICONTROL Graphique privé]** : réalise des combinaisons d’identités basées sur votre graphique d’identités privé.
* **[!UICONTROL Stratégie de fusion par défaut]** : un bouton de basculement qui vous permet de sélectionner cette stratégie de fusion ou non comme stratégie par défaut pour votre organisation. Si le sélecteur est activé, un avertissement s’affiche vous demandant de confirmer que vous souhaitez modifier la stratégie de fusion par défaut de votre organisation. Voir la section [Stratégies de fusion par défaut](#default-merge-policy) plus haut dans ce guide pour en savoir plus.
   ![](../images/merge-policies/create-make-default.png)

Une fois les champs obligatoires terminés, vous pouvez sélectionner **[!UICONTROL Suivant]** pour poursuivre le processus.

![Un écran de configuration complet avec le bouton Suivant en surbrillance.](../images/merge-policies/create-complete.png)

#### [!UICONTROL Schéma vue Union] {#view-union-schema}

Lors de la création ou de la modification d&#39;une stratégie de fusion, vous pouvez vue le schéma d&#39;union pour la classe de schéma choisie en sélectionnant **[!UICONTROL Schéma d&#39;Union de Vue]**.

![](../images/merge-policies/view-union-schema.png)

Cette opération ouvre la boîte de dialogue [!UICONTROL Schéma d&#39;Union de Vue], qui affiche tous les schémas, identités et relations de contribution associés au schéma d&#39;union. Vous pouvez utiliser la boîte de dialogue pour explorer le schéma d&#39;union comme vous le feriez en accédant à l&#39;onglet [!UICONTROL Schéma d&#39;Union] de la section [!UICONTROL Profils] de l&#39;interface utilisateur de la plate-forme.

Pour obtenir des informations détaillées sur les schémas d&#39;union, y compris sur la façon d&#39;interagir avec eux dans l&#39;onglet [!UICONTROL Schéma d&#39;Union] ou dans la boîte de dialogue [!UICONTROL Schéma d&#39;Union de Vue] qui s&#39;affiche dans le flux de travail des stratégies de fusion, consultez le [guide de l&#39;interface utilisateur de l&#39;union](union-schema.md).

![](../images/merge-policies/view-union-schema-dialog.png)


### [!UICONTROL Sélectionner des jeux de données de Profil] {#select-profile-datasets}

Dans l&#39;écran **[!UICONTROL Sélectionner les jeux de données de Profil]**, vous devez sélectionner la **[!UICONTROL méthode de fusion]** que vous souhaitez utiliser pour votre stratégie de fusion. S’affiche également à l’écran le nombre total de [!UICONTROL jeux de données de Profil] dans votre organisation qui se rapportent à la classe de schéma sélectionnée dans l’écran précédent.

Selon la méthode de fusion choisie, tous les jeux de données de Profil seront fusionnés selon l&#39;ordre dans lequel ils ont été mis à jour en dernier lieu (ordre d&#39;horodatage) ou vous devrez sélectionner les jeux de données de Profil à inclure dans la stratégie de fusion et l&#39;ordre dans lequel les fusionner (ordre de priorité des jeux de données). Pour plus d&#39;informations sur les méthodes de fusion, consultez la section [méthodes de fusion](#merge-methods) fournie plus haut dans ce document.

#### Horodatage commandé {#timestamp-ordered-profile}

Si vous sélectionnez **[!UICONTROL Horodatage trié]** comme méthode de fusion, les attributs des jeux de données les plus récents seront prioritaires. Ceci s’applique à tous les jeux de données de Profil.

![](../images/merge-policies/timestamp-ordered.png)

#### Priorité du jeu de données {#dataset-precedence-profile}

Si vous sélectionnez **[!UICONTROL La priorité des jeux de données]** comme méthode de fusion, vous devez sélectionner des jeux de données de Profil et les classer par priorité manuellement. Chaque jeu de données répertorié inclut également l&#39;état du dernier lot ingéré ou affiche un avis indiquant qu&#39;aucun lot n&#39;a été ingéré dans ce jeu de données.

Vous pouvez sélectionner jusqu’à 50 jeux de données dans la liste de jeux de données à inclure dans la stratégie de fusion. A mesure que les jeux de données sont sélectionnés, ils sont ajoutés à la section **[!UICONTROL Sélectionner les jeux de données]**, ce qui vous permet de les faire glisser et de les classer en fonction de votre priorité. Comme les jeux de données sont ajustés dans la liste, l&#39;ordinal (1, 2, 3, etc.) en regard du jeu de données se met à jour, affichant la priorité (1 étant donné que la priorité est la plus élevée, puis 2 et plus).

La sélection d&#39;un jeu de données met également à jour la section **[!UICONTROL schéma d&#39;Union]**, en affichant les champs du schéma d&#39;union auxquels chaque jeu de données fournit des données. Pour plus d’informations sur les schémas d’union, y compris sur la façon d’interagir avec les visualisations dans l’interface utilisateur, consultez le [Guide de l’interface utilisateur du schéma d’union](union-schema.md).

![](../images/merge-policies/dataset-precedence.png)

### [!UICONTROL Sélectionner des jeux de données ExperienceEvent] {#select-experienceevent-datasets}

L’étape suivante du flux de travaux nécessite la sélection des jeux de données ExperienceEvent. Cet écran est influencé par la méthode de fusion que vous avez sélectionnée dans l&#39;écran [[!UICONTROL Sélectionner des jeux de données de Profil]](#select-profile-datasets).

S’affiche également sur cet écran le nombre total de **[!UICONTROL jeux de données ExperienceEvent]** créés par votre organisation en rapport avec la classe de schéma que vous avez sélectionnée dans l’écran de configuration de la stratégie de fusion.

#### Horodatage commandé {#timestamp-ordered-experienceevent}

Si vous avez sélectionné **[!UICONTROL Horodatage ordonné]** comme méthode de fusion pour les jeux de données de Profil, les attributs des jeux de données ExperienceEvent les plus récemment mis à jour seront également prioritaires ici.

![](../images/merge-policies/timestamp-experienceevent.png)

#### Priorité du jeu de données {#dataset-precedence-experienceevent}

Si vous avez sélectionné **[!UICONTROL ordre de priorité des jeux de données]** comme méthode de fusion pour les jeux de données de Profil, vous devez sélectionner les jeux de données ExperienceEvent à inclure. Vous pouvez sélectionner jusqu’à 50 jeux de données ExperienceEvent à partir de la liste de jeux de données. Lorsque des jeux de données sont sélectionnés, ils apparaissent dans la section [!UICONTROL Sélectionner des jeux de données].

Les jeux de données ExperienceEvent ne peuvent pas être triés manuellement. Les attributs des jeux de données ExperienceEvent sont ajoutés aux jeux de données de Profil s’ils font partie du même fragment de profil.

Tout comme la sélection de jeux de données de Profil, la sélection d’un jeu de données ExperienceEvent met également à jour la section **[!UICONTROL schéma d’Union]**, en affichant les champs du schéma d’union auxquels chaque jeu de données fournit des données. Pour plus d’informations sur les schémas d’union, y compris sur la façon d’interagir avec les visualisations dans l’interface utilisateur, consultez le [Guide de l’interface utilisateur du schéma d’union](union-schema.md).

![](../images/merge-policies/dataset-precedence-experienceevent.png)

### [!UICONTROL Révision] {#review}

La dernière étape du processus consiste à revoir votre stratégie de fusion. L&#39;écran **[!UICONTROL Réviser]** affiche le nom de votre nouvelle stratégie de fusion, la classe de schéma sur laquelle elle repose, l&#39;option [!UICONTROL d&#39;assemblage d&#39;identifiants] que vous avez sélectionnée, ainsi que la méthode de fusion et les jeux de données inclus dans la stratégie de fusion. Pour vue de tous les jeux de données Profil ou ExperienceEvent inclus, sélectionnez le nombre de jeux de données à développer la liste déroulante.

Veillez à examiner soigneusement votre stratégie de fusion avant de sélectionner **[!UICONTROL Terminer]** pour terminer le processus de création.

#### Horodatage commandé {#timestamp-ordered-review}

Si vous avez sélectionné **[!UICONTROL Horodatage ordonné]** comme méthode de fusion pour votre stratégie de fusion, la liste des jeux de données de Profil inclut tous les jeux de données créés par votre organisation en rapport avec la classe de schéma, par ordre d&#39;horodatage. La liste des jeux de données ExperienceEvent inclut tous les jeux de données créés par votre organisation pour la classe de schéma choisie et sera ajoutée aux jeux de données de Profil.

![](../images/merge-policies/timestamp-review.png)

#### Priorité du jeu de données {#dataset-precedence-review}

Si vous avez sélectionné **[!UICONTROL ordre de priorité des jeux de données]** comme méthode de fusion pour votre stratégie de fusion, les listes des jeux de données Profil et ExperienceEvent incluent uniquement les jeux de données Profil et ExperienceEvent que vous avez sélectionnés lors du processus de création, respectivement. L’ordre des jeux de données de Profil doit correspondre à celui que vous avez spécifié lors de la création. Si ce n’est pas le cas, utilisez le bouton [!UICONTROL Précédent] pour revenir aux étapes précédentes du flux de travail et ajuster la priorité.

![](../images/merge-policies/dataset-precedence-review.png)

### Liste mise à jour des stratégies de fusion {#updated-list}

Après avoir terminé le processus de création d’une nouvelle stratégie de fusion, vous êtes revenu à l’onglet **[!UICONTROL Fusionner les stratégies]**. La liste des stratégies de fusion pour votre organisation doit maintenant inclure la stratégie de fusion que vous venez de créer.

![](../images/merge-policies/new-merge-policy-created.png)

## Modification d’une stratégie de fusion

Dans l&#39;onglet [!UICONTROL Fusionner les stratégies], vous pouvez modifier une stratégie de fusion existante créée pour la classe [!DNL XDM Individual Profile] en sélectionnant **[!UICONTROL nom de la stratégie]** pour la stratégie de fusion que vous souhaitez modifier.

![Page d’entrée des stratégies de fusion](../images/merge-policies/select-edit.png)

Lorsque l&#39;écran **[!UICONTROL Modifier la stratégie de fusion]** apparaît, vous pouvez modifier le nom et [!UICONTROL l&#39;assemblage d&#39;identifiants], ainsi que changer si cette stratégie est ou non la stratégie de fusion par défaut de votre organisation.

Sélectionnez **[!UICONTROL Suivant]** pour continuer tout au long du processus de stratégie de fusion afin de mettre à jour la méthode de fusion et les jeux de données inclus dans la stratégie de fusion.

![](../images/merge-policies/edit-screen.png)

Après avoir apporté les modifications nécessaires, passez en revue votre stratégie de fusion et sélectionnez **[!UICONTROL Terminer]** pour revenir à l&#39;onglet **[!UICONTROL Fusionner les stratégies]**.

>[!WARNING]
>
>La modification d’une stratégie de fusion peut avoir une incidence sur la segmentation et les résultats des profils, car elle modifiera la manière dont les conflits de données sont résolus.

![](../images/merge-policies/edit-review.png)

## Violations de la politique de gouvernance des données

Lors de la création ou de la mise à jour d’une stratégie de fusion, une vérification est effectuée pour déterminer si la politique de fusion enfreint l’une des stratégies en matière d’utilisation des données définies par votre organisation. Les stratégies d&#39;utilisation des données font partie de Adobe Experience Platform [!DNL Data Governance] et sont des règles qui décrivent les types d&#39;actions marketing que vous pouvez exécuter sur des données [!DNL Platform] spécifiques, ou dont vous êtes limité à l&#39;exécution. Par exemple, si une stratégie de fusion a été utilisée pour créer un segment qui s’est activé sur une destination tierce et si votre entreprise disposait d’une stratégie d’utilisation des données empêchant l’exportation de données spécifiques vers des tiers, vous recevriez une **[!UICONTROL violation de la stratégie de gouvernance des données détectée]** lors de la tentative d’enregistrement de votre stratégie de fusion.

Cette notification inclut une liste des stratégies d’utilisation des données ayant été enfreintes et vous permet de consulter les détails de la violation en sélectionnant une stratégie depuis la liste. Lors de la sélection d&#39;une stratégie violée, l&#39;onglet **[!UICONTROL lignage de données]** fournit la raison de la violation et les activations concernées, en fournissant chacune des informations plus détaillées sur la manière dont la stratégie d&#39;utilisation des données a été violée.

Pour en savoir plus sur la manière dont la gouvernance des données est réalisée au sein d’Adobe Experience Platform, veuillez commencer par lire la [présentation de la gouvernance des données](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## Étapes suivantes

Maintenant que vous avez créé et configuré des stratégies de fusion pour votre organisation, vous pouvez les utiliser pour ajuster la vue des profils client dans la plate-forme et pour créer des segments d’audience à partir des données de Profil. Voir [Présentation de la segmentation](../../segmentation/home.md) pour plus d&#39;informations sur la création et l&#39;utilisation de segments à l&#39;aide de l&#39;interface utilisateur et des API [!DNL Experience Platform].
