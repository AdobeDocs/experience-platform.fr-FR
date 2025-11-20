---
keywords: Experience Platform;accueil;rubriques populaires;gouvernance des données;guide d’utilisation des politiques d’utilisation des données
solution: Experience Platform
title: Gestion des politiques d’utilisation des données dans l’interface utilisateur
description: La gouvernance des données d’Adobe Experience Platform fournit une interface utilisateur qui vous permet de créer et de gérer des politiques d’utilisation des données. Ce document offre une vue d’ensemble des actions que vous pouvez effectuer dans l’espace de travail Politiques de l’interface utilisateur d’Experience Platform.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: 364a92bde1a1629d2811e7ff16bd6a4fb5287249
workflow-type: tm+mt
source-wordcount: '2380'
ht-degree: 46%

---

# Gestion des politiques d’utilisation des données dans l’interface utilisateur {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_description"
>title="Intégrer et appliquer le consentement client dans vos données de profil"
>abstract="<h2>Description</h2><p>Experience Platform permet d’intégrer dans leurs profils respectifs les données de consentement que vous avez collectées auprès de vos clientes et clients. Vous pouvez ensuite établir des stratégies de consentement pour déterminer si ces données peuvent être incluses dans des segments activés vers certaines destinations.</p>"

Ce document explique comment utiliser l’espace de travail **[!UICONTROL Policies]** dans l’interface utilisateur de Adobe Experience Platform pour créer et gérer des politiques d’utilisation des données.

>[!NOTE]
>
>Pour plus d’informations sur la gestion des politiques de contrôle d’accès dans l’interface utilisateur, reportez-vous au [guide de l’interface utilisateur du contrôle d’accès basé sur les attributs](../../access-control/abac/ui/policies.md).

>[!IMPORTANT]
>
>Toutes les politiques d’utilisation des données (y compris les politiques de base fournies par Adobe) sont désactivées par défaut. Pour qu’une politique individuelle soit prise en compte pour l’application, vous devez l’activer manuellement. Consultez la section relative à l’[activation des politiques](#enable) pour savoir comment procéder dans l’interface utilisateur.

## Conditions préalables

Ce guide nécessite une bonne compréhension des concepts [!DNL Experience Platform] suivants :

* [Gouvernance des données](../home.md)
* [Politiques d’utilisation des données](./overview.md)

## Affichage des politiques existantes {#view-policies}

Dans l’interface utilisateur de [!DNL Experience Platform], sélectionnez **[!UICONTROL Policies]** pour ouvrir l’espace de travail **[!UICONTROL Policies]**. Dans l’onglet **[!UICONTROL Browse]** , vous pouvez voir une liste des politiques disponibles, y compris leurs libellés associés, les actions marketing et les états.

![](../images/policies/browse-policies.png)

Si vous avez accès aux politiques de consentement, activez le bouton (bascule) **[!UICONTROL Consent policies]** pour les afficher dans l’onglet [!UICONTROL Browse] .

![](../images/policies/consent-policy-toggle.png)

Cliquez sur une politique répertoriée pour en afficher la description et le type. Si une politique personnalisée est sélectionnée, d’autres contrôles s’affichent pour la modifier, la supprimer ou [activer/désactiver la politique](#enable).

![](../images/policies/policy-details.png)

## Création dʼune politique personnalisée {#create-policy}

Pour créer une politique d’utilisation des données personnalisée, sélectionnez **[!UICONTROL Create policy]** dans le coin supérieur droit de l’onglet **[!UICONTROL Browse]** dans l’espace de travail **[!UICONTROL Policies]** .

![](../images/policies/create-policy-button.png)

La boîte de dialogue [!UICONTROL Choose type of policy] s’affiche. Sélectionnez une [politique de consentement](#consent-policy) ou une [politique de gouvernance des données](#create-governance-policy).

![Boîte de dialogue Choisir le type de politique.](../images/policies/choose-policy-type.png)

### Utilisation conjointe de la gouvernance des données et des politiques de consentement {#combine-policies}

>[!NOTE]
>
>Actuellement, les politiques de consentement ne sont disponibles que pour les organisations qui ont acheté Adobe Healthcare Shield ou Adobe Privacy &amp; Security Shield.

Les politiques de gouvernance et de consentement peuvent être utilisées conjointement pour créer des règles solides afin de gérer les audiences mappées à une destination. Les politiques de consentement sont de nature inclusive, ce qui signifie qu’elles déterminent les profils pouvant être inclus dans chaque expérience marketing. À l’inverse, les politiques de gouvernance empêchent que les attributs étiquetés spécifiques soient utilisés pour être configurés pour l’activation.

En utilisant ce comportement, vous pouvez configurer une combinaison de politiques et de règles de consentement incluant les profils corrects, mais vous ne pouvez pas inclure des données qui vont à l’encontre de vos règles d’organisation définies. C’est le cas par exemple si vous souhaitez exclure des données sensibles de l’inclusion, mais que vous pouvez toujours cibler les utilisateurs et utilisatrices consentants pour le marketing via les médias sociaux. Les étapes nécessaires à ce scénario sont décrites dans l’infographie ci-dessous.

![Infographie décrivant les étapes à suivre pour utiliser conjointement les politiques de gouvernance et de consentement afin de créer des règles solides pour les audiences de gouvernance.](../images/policies/governance-and-consent-policies-infographic.png)

### Créer une politique de gouvernance des données {#create-governance-policy}

Le workflow **[!UICONTROL Create policy]** s’affiche. Commencez par fournir un nom et une description à la nouvelle politique.

![](../images/policies/create-policy-description.png)

Ensuite, sélectionnez les libellés d’utilisation des données sur lesquels la politique sera basée. Lors de la sélection de plusieurs libellés, vous avez la possibilité de choisir si les données doivent contenir tous les libellés ou un seul pour que la politique s’applique. Sélectionnez **[!UICONTROL Next]** (Enregistrer) une fois terminé.

![](../images/policies/add-labels.png)

L’étape **[!UICONTROL Select marketing actions]** s’affiche. Sélectionnez les actions marketing appropriées dans la liste fournie, puis sélectionnez **[!UICONTROL Next]** pour continuer.

>[!NOTE]
>
>Lors de la sélection de plusieurs actions marketing, la politique les interprète comme une règle « OU ». En d’autres termes, la politique s’applique si **l’une** des actions marketing sélectionnées est exécutée.

![](../images/policies/add-marketing-actions.png)

L’étape **[!UICONTROL Review]** s’affiche et vous permet de consulter les détails de la nouvelle politique avant de la créer. Une fois que vous êtes satisfait, sélectionnez **[!UICONTROL Finish]** pour créer la politique.

![](../images/policies/policy-review.png)

L’onglet **[!UICONTROL Browse]** réapparaît, qui répertorie désormais la nouvelle politique au statut « Version préliminaire ». Pour activer la politique, consultez la section suivante.

![](../images/policies/created-policy.png)

### Créer une politique de consentement {#consent-policy}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_instructions"
>title="Instructions"
>abstract="<ul><li>Assurez-vous d’ingérer les données relatives aux préférences dans vos schémas d’union via le connecteur source OneTrust ou le schéma XDM standard pour le consentement.</li><li>Sélectionnez <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=fr">Stratégies</a> dans le volet de navigation de gauche, puis cliquez sur <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=fr#create-governance-policy">Créer une stratégie</a>.</li><li>Dans la section <b>Si</b>, indiquez les conditions ou actions qui déclencheront la vérification de la stratégie.</li><li>Dans la section <b>Alors</b>, indiquez les attributs de consentement devant être présents pour qu’un profil soit inclus dans l’action qui a déclenché la stratégie.</li><li>Sélectionnez <b>Enregistrer</b> pour créer la stratégie. Pour activer immédiatement la stratégie, activez le bouton (bascule) <b>Statut</b> dans le rail de droite.</li><li>Experience Platform applique automatiquement vos stratégies de consentement activées lorsque vous activez des segments vers des destinations et fournit des détails sur la manière dont chaque stratégie affecte la taille de votre audience.</li><li>Pour obtenir de l’aide sur cette fonctionnalité, consultez le guide sur la <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html#consent-policy?lang=fr">création de stratégies de consentement</a> sur Experience League.</li></ul>"

>[!IMPORTANT]
>
>Les politiques de consentement ne sont disponibles que pour les organisations qui ont acheté **Adobe Healthcare Shield** ou **Adobe Privacy &amp; Security Shield**.

Si vous choisissez de créer une politique de consentement, un nouvel écran vous permettant de configurer la nouvelle politique s’affiche.

![](../images/policies/consent-policy-dialog.png)

Pour pouvoir utiliser des politiques de consentement, des attributs de consentement doivent être présents dans vos données de profil. Consultez le guide sur le [traitement du consentement dans Experience Platform](../../landing/governance-privacy-security/consent/adobe/overview.md) pour obtenir des instructions détaillées sur la manière d’inclure les attributs obligatoires dans votre schéma d’union.

Les politiques de consentement se composent de deux éléments logiques :

* **[!UICONTROL If]** : condition qui déclenchera la vérification de la politique. Elle peut dépendre d’une certaine action marketing en cours, de la présence de certains libellés d’utilisation des données ou d’une combinaison des deux.
* **[!UICONTROL Then]** : attributs de consentement devant être présents pour qu’un profil soit inclus dans l’action qui a déclenché la politique.

>[!NOTE]
>
>Les politiques de consentement prennent en charge la création avancée de règles avec divers types de champs et opérateurs. Pour obtenir une référence complète des types de champs pris en charge, des opérateurs et des exemples de création de règles, consultez la [référence des règles de politique de consentement](./consent-policy-rule-building-reference.md).

#### Configurer les conditions {#consent-conditions}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentif"
>title="Condition Si"
>abstract="Définissez d’abord les conditions qui déclencheront la vérification de la politique. Les conditions peuvent inclure certaines actions marketing entreprises, certaines étiquettes de gouvernance des données présentes ou une combinaison des deux. Utilisez la logique AND/OR pour créer des relations conditionnelles complexes entre plusieurs conditions."

Sous la section **[!UICONTROL If]** , sélectionnez les actions marketing et/ou les libellés d’utilisation des données qui doivent déclencher cette politique. Sélectionnez **[!UICONTROL View all]** et **[!UICONTROL Select labels]** pour afficher les listes complètes des actions marketing et des libellés disponibles, respectivement.

Une fois que vous avez ajouté au moins une condition, vous pouvez sélectionner **[!UICONTROL Add condition]** pour continuer à ajouter d’autres conditions si nécessaire, en choisissant le type de condition approprié dans la liste déroulante.

![](../images/policies/add-condition.png)

Si vous sélectionnez plusieurs conditions, vous pouvez utiliser l’icône qui s’affiche entre elles pour changer la relation conditionnelle entre « ET » et « OU ».

![](../images/policies/and-or-selection.png)

#### Sélectionner les attributs de consentement {#consent-attributes}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentthen"
>title="Condition Alors"
>abstract="Une fois votre condition « Si » définie, utilisez la section « Alors » pour sélectionner au moins un attribut de consentement dans le schéma d’union. Vous devez parcourir les champs de conteneur (objet, mappage, tableau) pour atteindre les champs primitifs (chaîne, nombre, valeur booléenne, etc.) pour la création de règles. Ce champ primitif est l’attribut qui doit être présent pour que les profils soient inclus dans l’action régie par cette politique."

Sous la section **[!UICONTROL Then]** , sélectionnez au moins un attribut de consentement dans le schéma d’union. Il s’agit de l’attribut qui doit être présent pour que les profils soient inclus dans l’action régie par cette politique. Vous pouvez choisir l’une des options suggérées ou sélectionner **[!UICONTROL View all]** pour sélectionner directement l’attribut dans le schéma d’union.

>[!NOTE]
>
>Les politiques de consentement prennent en charge les types de champs primitifs (chaîne, nombre, valeur booléenne, date) et les types de conteneurs (objet, mappage, tableau). Vous pouvez naviguer dans les conteneurs pour sélectionner des attributs spécifiques et appliquer la logique AND/OR afin de combiner des règles. Pour consulter la liste complète des types de champs pris en charge, des opérateurs et des exemples de création de règles, reportez-vous à la [référence de création de règles de politique de consentement](./consent-policy-rule-building-reference.md).

![Interface utilisateur du créateur de politiques de consentement affichant les sections Si et Alors, avec Afficher tout en surbrillance.](../images/policies/view-all.png)

Si vous sélectionnez **[!UICONTROL View all]**, la boîte de dialogue **[!UICONTROL Select consent attribute]** s’affiche. Sélectionnez le ou les attributs de consentement que vous souhaitez que cette politique vérifie. Dans cette boîte de dialogue, vous pouvez également sélectionner **[!UICONTROL Advanced Schema search]** pour choisir un champ primitif imbriqué à évaluer dans le cadre de la politique. Sélectionnez **[!UICONTROL Done]** pour confirmer vos paramètres.

![La boîte de dialogue Sélectionner un attribut de consentement avec un attribut et terminé est mise en surbrillance.](../images/policies/select-consent-attribute.png)

### Recherche avancée de schémas {#advanced-schema-search}

Dans la boîte de dialogue **[!UICONTROL Select consent attribute]**, sélectionnez **[!UICONTROL Advanced Schema search]** pour ouvrir la boîte de dialogue **[!UICONTROL Select union schema field]**. Dans cette vue, sélectionnez les attributs de niveau racine ou imbriqués des types de champ primitifs tels que la chaîne, le nombre, la valeur booléenne et la date, ainsi que les types de conteneur tels que l’objet, le mappage et le tableau.

![Chemin d’accès au clic pour parcourir la recherche de schéma avancée.](../images/policies/consent-advanced-schema-search.gif)

#### Champs à valeur fixe pour une condition de politique {#fixed-value-fields}

Lorsque vous sélectionnez un champ à valeur fixe comme condition de politique, le panneau [!UICONTROL Selected attributes] affiche les valeurs prédéfinies définies dans votre schéma de données.

>[!NOTE]
>
>Si un champ est configuré avec un ensemble fixe de valeurs (par exemple, sous la forme d’une énumération ou d’un autre vocabulaire contrôlé), le créateur de politiques applique cette contrainte pour s’assurer que les conditions sont évaluées uniquement par rapport à des données normalisées valides.

Pour maintenir la qualité et la cohérence des données, l’interface utilisateur affiche ces valeurs sous la forme de cases à cocher sélectionnables plutôt que de champs de texte libre. Cette approche réduit la validation manuelle et permet à votre politique de consentement d’évaluer les données de manière fiable.

Pour définir la condition, cochez les cases correspondant aux valeurs que la politique doit évaluer.

![&#x200B; La boîte de dialogue « Sélectionner le champ de schéma d’union » avec un champ de schéma et les cases à cocher à valeur fixe disponibles en surbrillance.](../images/policies/select-schema-field.png)

#### Mapper des champs de type données pour une condition de politique {#map-data-type-fields}

Lorsque vous sélectionnez un champ primitif contenu dans un type de données Mappage , des options de configuration supplémentaires s’affichent dans le panneau **[!UICONTROL Selected attributes]**. Utilisez ces options pour configurer les vérifications de consentement sur plusieurs clés sans avoir besoin d’une politique distincte pour chaque clé. Cette méthode de configuration simplifie la gestion des politiques en réduisant le nombre de politiques à créer.

![Section Mappage des politiques de consentement mise en surbrillance dans le panneau Attributs.](../images/policies/consent-policies-map.png)

##### Configurer les attributs de type de données Map {#configure-map-attributes}

Pour configurer un attribut de type Map, procédez comme suit :

Dans le diagramme de schéma d’union, sélectionnez un champ primitif (une chaîne ou un nombre, par exemple) contenu dans un type de données Mappage . Le panneau **[!UICONTROL Selected attributes]** se met à jour pour afficher des options de configuration supplémentaires pour ce champ.

![Mise à jour des options d’attribut pour un champ primitif contenu dans un type de données Mappage.](../images/policies/select-union-schema-field.png)

Dans le panneau **[!UICONTROL Selected attributes]**, configurez la manière dont la politique évalue les clés de mappage en cochant ou décochant la case **[!UICONTROL Find any matching item]** .

| Option | Action | Comportement en matière de politique |
| --- | --- | --- |
| **[!UICONTROL Find any matching item]** case est **cochée** | Le champ de texte **[!UICONTROL within]** est désactivé. | La politique vérifie **chaque clé** dans la carte. Toute clé pour laquelle le champ imbriqué remplit la condition de valeur est considérée comme correspondant à la politique. Cela s’avère utile pour appliquer la conformité globale sur les attributs indexés dynamiquement. |
| **[!UICONTROL Find any matching item]** case est **non cochée** | Vous devez saisir un nom de clé spécifique dans le champ de texte **[!UICONTROL within]**. | La politique vérifie uniquement la clé de mappage spécifiée dans le champ **[!UICONTROL within]** . Seuls les profils pour lesquels le champ imbriqué pour une clé spécifique atteint la valeur définie sont mis en correspondance. Cela s’avère utile pour les politiques ciblant un programme spécifique ou une clé de fréquence (par exemple, `frequencyMap.m1`). |

Saisissez la valeur du champ primitif sélectionné que la politique doit évaluer. Par exemple, si le type de champ est `Integer`, saisissez une valeur numérique.

![La barre latérale Attributs sélectionnés avec les options de configuration de mappage mises en surbrillance.](../images/policies/within-option.png)

Sélectionnez **[!UICONTROL Select]** pour confirmer la configuration et revenir au créateur de politiques.

Après avoir sélectionné au moins un attribut de consentement, le panneau **[!UICONTROL Policy properties]** se met à jour pour afficher l’estimation du nombre de profils inclus dans cette politique, ainsi que le pourcentage de profils affectés dans la banque de profils. Le nombre estimé de profils est automatiquement mis à jour lorsque vous modifiez la configuration de la politique.

![L’interface utilisateur du créateur de politiques affiche une condition Alors configurée avec le rail de droite Propriétés de la politique affichant le nombre estimé de profils qualifiés.](../images/policies/audience-preview.png)

Pour ajouter des attributs de consentement supplémentaires, sélectionnez **[!UICONTROL Add result]**. Une autre règle est ainsi créée pour inclure les profils basés sur ces attributs.

![Interface utilisateur du créateur de politiques de consentement avec l’option Ajouter un résultat mise en surbrillance.](../images/policies/add-result.png)

>[!NOTE]
>
>Pour modifier un attribut existant, sélectionnez le nom de l’attribut, puis sélectionnez l’icône en forme de crayon (![Icône en forme de crayon.](/help/images/icons/edit.png)). La boîte de dialogue **[!UICONTROL Select union schema field]** s’ouvre pour que vous puissiez apporter des modifications.
>
>![Interface utilisateur du créateur de politiques de consentement avec l’attribut de consentement et l’icône de modification en surbrillance.](../images/policies/edit-then-attributes.png)

Continuez à ajouter ou à ajuster des conditions et des attributs de consentement jusqu’à ce que la politique réponde à vos besoins. Lorsque vous avez terminé, saisissez un nom et une description (facultative), puis sélectionnez **[!UICONTROL Save]** pour créer la politique.

![](../images/policies/name-and-save.png)

La politique de consentement est maintenant créée et son statut est défini sur [!UICONTROL Disabled] par défaut. Pour activer immédiatement la politique, activez le bouton (bascule) **[!UICONTROL Status]** dans le rail de droite.

![](../images/policies/enable-consent-policy.png)


#### Vérifier l’application des politiques

Après avoir créé et activé une politique de consentement, vous pouvez prévisualiser l’impact de cette règle sur vos audiences consentantes lors de l’activation de segments vers les destinations. Voir la section sur l’[évaluation des politiques de consentement](../enforcement/auto-enforcement.md#consent-policy-evaluation) pour plus d’informations.

## Activation ou désactivation d’une politique {#enable}

Toutes les politiques d’utilisation des données (y compris les politiques de base fournies par Adobe) sont désactivées par défaut. Pour qu’une politique individuelle soit prise en compte pour son application, vous devez l’activer manuellement par le biais de l’API ou de l’interface utilisateur.

Vous pouvez activer ou désactiver les politiques à partir de l’onglet **[!UICONTROL Browse]** de l’espace de travail **[!UICONTROL Policies]**. Sélectionnez une politique personnalisée dans la liste pour afficher ses détails à droite. Sous **[!UICONTROL Status]**, sélectionnez le bouton bascule pour activer ou désactiver la politique.

![](../images/policies/enable-policy.png)

## Affichage des actions marketing {#view-marketing-actions}

Dans l’espace de travail **[!UICONTROL Policies]**, sélectionnez l’onglet **[!UICONTROL Marketing actions]** pour afficher la liste des actions marketing disponibles définies par Adobe et votre organisation.

![](../images/policies/marketing-actions.png)

## Création d’une action marketing {#create-marketing-action}

Pour créer une action marketing personnalisée, sélectionnez **[!UICONTROL Create marketing action]** dans le coin supérieur droit de l’onglet **[!UICONTROL Marketing actions]** dans l’espace de travail **[!UICONTROL Policies]**.

![](../images/policies/create-marketing-action.png)

La boîte de dialogue **[!UICONTROL Create marketing action]** s’affiche. Saisissez un nom et une description pour l’action marketing, puis sélectionnez **[!UICONTROL Create]**.

![](../images/policies/create-marketing-action-details.png)

L’action nouvellement créée s’affiche dans l’onglet **[!UICONTROL Marketing actions]** . Vous pouvez désormais utiliser l’action marketing lors de la [création de politiques d’utilisation des données](#create-policy).

![](../images/policies/created-marketing-action.png)

## Modification ou suppression d’une action marketing {#edit-delete-marketing-action}

>[!NOTE]
>
>Seules les actions marketing personnalisées définies par votre organisation peuvent être modifiées. Il n’est pas possible de modifier ou supprimer des actions marketing définies par Adobe.

Dans l’espace de travail **[!UICONTROL Policies]**, sélectionnez l’onglet **[!UICONTROL Marketing actions]** pour afficher la liste des actions marketing disponibles définies par Adobe et votre organisation. Sélectionnez une action marketing personnalisée répertoriée dans la liste, puis utilisez les champs fournis dans la section de droite pour modifier les détails de cette action.

![](../images/policies/edit-marketing-action.png)

Si l’action marketing n’est utilisée par aucune politique d’utilisation existante, vous pouvez la supprimer en sélectionnant **[!UICONTROL Delete marketing action]**.

>[!NOTE]
>
>Si vous tentez de supprimer une action marketing utilisée par une politique existante, un message d’erreur s’affiche, indiquant que la tentative de suppression a échoué.

![](../images/policies/delete-marketing-action.png)

## Étapes suivantes

Ce document offre un aperçu de la gestion des politiques d’utilisation des données dans l’interface utilisateur [!DNL Experience Platform]. Pour savoir comment gérer les politiques à l’aide de l’[!DNL Policy Service API], consultez le [guide du développement](../api/getting-started.md). Pour plus d’informations sur l’application des stratégies d’utilisation des données, voir la [présentation de l’application des politiques](../enforcement/overview.md).

La vidéo qui suit montre comment utiliser les politiques d’utilisation dans l’interface utilisateur [!DNL Experience Platform] :

>[!VIDEO](https://video.tv.adobe.com/v/37130?captions=fre_fr&quality=12&learn=on)
