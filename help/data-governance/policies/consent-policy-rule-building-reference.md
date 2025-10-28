---
title: Référence de création de règle de politique de consentement
description: Découvrez comment utiliser les types de données XDM, les opérateurs pris en charge et la logique avancée pour créer des règles de politique de consentement granulaire dans l’interface utilisateur de Adobe Experience Platform.
source-git-commit: 678220b14cefd4dd31ef7a12355d796575a77a50
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 0%

---

# Référence de création de règle de politique de consentement

Utilisez cette référence sur la logique de règle avancée pour définir des règles précises et juridiquement valides dans la clause **[!UICONTROL Then]** du créateur de politique de consentement dans Adobe Experience Platform.

![Interface du créateur de politiques de consentement qui met en surbrillance la section Clause de [!UICONTROL Then], où les utilisateurs définissent des conditions de règle.](../images/policies/multiple-rules.png)

Découvrez comment les règles de politique s’appliquent à la structure et aux types de vos données de consentement pour appliquer avec précision les préférences de consentement du client.

Lisez ce document pour savoir comment filtrer les profils en fonction du consentement en accédant aux champs conteneurs de votre schéma XDM et en sélectionnant un champ primitif. Utilisez ensuite l’opérateur approprié pour définir la valeur exacte à laquelle un profil doit correspondre.

## Conditions préalables

Avant d’utiliser cette référence, assurez-vous que la configuration de votre politique de consentement est terminée et que vous connaissez les concepts fondamentaux de l’architecture des données et du cadre de gouvernance de Adobe Experience Platform.

Veillez à respecter les conditions préalables suivantes :

* **Configuration de la politique terminée** : vous avez créé ou commencé à créer une politique de consentement dans l’interface utilisateur de Adobe Experience Platform. Pour obtenir des instructions détaillées, consultez le guide d’utilisation des [politiques d’utilisation des données](user-guide.md#consent-policy).

* **Connaissance des structures de données** : cette référence nécessite une connaissance pratique des concepts de base suivants :
   * **XDM et schéma d’union** : comprenez comment les structures du modèle de données d’expérience définissent les relations de données et comment le schéma d’union représente les profils client unifiés. Consultez la [ Présentation du système XDM ](../../xdm/home.md) pour en savoir plus.
   * **Cadre de gouvernance des données** : découvrez comment Adobe Experience Platform applique les politiques d’utilisation des données et les règles de gouvernance. Consultez la [présentation de la gouvernance des données](../home.md) pour plus d’informations.
   * **Traitement du consentement du client** : comprenez comment les données de consentement sont collectées, stockées et appliquées dans les workflows d’expérience client. Voir la [présentation du traitement du consentement](../../landing/governance-privacy-security/consent/adobe/overview.md).

## Concepts de base : champs primitifs et conteneurs

Lisez cette section pour découvrir comment les règles de politique de consentement utilisent différents types de champs dans les schémas XDM. Comprendre la distinction entre les champs conteneurs et primitifs vous permet de sélectionner le champ et l’opérateur appropriés lors de la définition des conditions de la politique.

### Types de champs pris en charge et logique de règle

Les politiques de consentement prennent en charge plusieurs types de champ, chacun disposant d’opérateurs spécifiques pour créer des conditions de règle. Les types de champs sont regroupés en deux catégories : **types conteneurs** et **types primitifs**.

### Types de conteneur (navigation par schéma)

Les types de conteneur organisent les données de consentement, mais ne peuvent pas être utilisés directement dans les conditions de politique. Ils servent de chemins de navigation pour atteindre les champs primitifs qui contiennent les valeurs réelles.

| Type de conteneur | Description |
|----------------|-------------|
| **Objet** | Conteneur avec un schéma fixe qui contient plusieurs champs de différents types. |
| **Tableau** | Conteneur contenant plusieurs valeurs du même type. |
| **Carte** | Conteneur avec des clés dynamiques pouvant contenir des objets ou d’autres types de champ. |

>[!IMPORTANT]
>
>Les champs de conteneur ne peuvent pas être sélectionnés directement dans les conditions de la politique de consentement. Vous devez accéder à des conteneurs pour sélectionner des **champs primitifs** (chaîne, nombre ou valeur booléenne, par exemple) en vue de la création de règles. Les opérateurs de conteneur sont utilisés uniquement pour la navigation de schéma, et non pour la définition de conditions de politique.

### Types primitifs (conditions des règles)

Les champs primitifs contiennent les valeurs de données de consentement réelles (par exemple, `true` ou `"weekly"`) et sont les seuls types de champs qui peuvent être utilisés pour définir des conditions de politique.

Le tableau ci-dessous décrit chaque type primitif pris en charge et les opérateurs disponibles.

| Type primitive | Opérateurs pris en charge | Description |
|----------------|---------------------|-------------|
| **Chaîne** | `is equal to`, `is not equal to`, `exists`, `does not exist` | Attributs de consentement textuels. |
| **Nombre** | `is equal to`, `is not equal to`, `is greater than`, `is less than`, `exists`, `does not exist` | Attributs de consentement numériques. |
| **booléen** | `is equal to`, `is not equal to` | Valeurs de consentement vraies ou fausses. |
| **Date** | `is equal to`, `is not equal to`, `exists`, `does not exist` | Attributs de consentement basés sur une date. |


## Utilisation de structures de données complexes

Lisez cette section pour savoir comment parcourir les conteneurs imbriqués dans votre schéma de consentement pour accéder aux champs primitifs. Il introduit des modèles de schéma courants et explique comment des structures plus profondes permettent une logique de consentement plus granulaire.

### Gestion des structures de schéma imbriquées et complexes

Les schémas de consentement complexes incluent souvent des structures de conteneur imbriquées qui prennent en charge une gestion des données flexible et évolutive. Étant donné que les règles de politique ne peuvent référencer que des champs primitifs, vous devez parcourir les hiérarchies de conteneurs pour accéder aux champs qui peuvent être utilisés dans des conditions de politique de consentement. L’imbrication plus profonde permet un ciblage de règle plus granulaire et plus spécifique.

Les modèles de conteneur imbriqués courants incluent :

* **Carte de la carte** - Clés dynamiques qui contiennent d’autres cartes.
* **Mappage d’objet** - Clés dynamiques contenant des objets avec des schémas fixes.
* **Tableau de mappages** - Tableaux contenant des mappages avec des clés dynamiques.
* **Tableau d’objets** - Tableaux contenant des objets avec des schémas fixes.
* **Objet avec propriétés de mappage ou de tableau** - Objets qui incluent des champs de mappage ou de tableau.

### Exemple de structure de champ

La structure suivante sert de référence visuelle pour les exemples de règle dans ce guide.

```
consent.marketing (Object)
├── email (Boolean)
├── sms (Boolean)
├── preferences (Map with dynamic keys)
│   ├── "email_preferences" (Object)
│   │   ├── frequency (String)
│   │   └── channels (Array of Strings)
│   ├── "sms_preferences" (Object)
│   │   ├── frequency (String)
│   │   └── opt_in_time (Date)
│   └── "push_preferences" (Object)
│       ├── frequency (String)
│       └── categories (Array of Strings)
└── lastUpdated (Date)
```

## Création avancée de règles par type de champ

Lisez cette section pour obtenir des conseils détaillés sur la création de règles de politique de consentement basées sur le type de champ. Vous apprendrez à configurer la logique des règles pour les booléens, les mappages, les objets et les tableaux afin de capturer des conditions de consentement précises.

### Composants et étapes de création de règles

Pour créer des règles de politique de consentement efficaces, vous devez comprendre comment naviguer dans la structure de votre schéma et appliquer les opérateurs appropriés pour chaque type de champ. Chaque règle suit la même approche de base : accédez à un champ primitif, sélectionnez l’opérateur approprié et définissez la condition qui doit être remplie.

Pour créer une règle, procédez comme suit :

1. **Sélectionner un champ** - Parcourez les champs de conteneur pour atteindre un champ primitif.
2. **Choisir un opérateur** - Sélectionnez l’opérateur pris en charge par le type de champ.
   ![Panneau de navigation de schéma hiérarchique, qui montre un utilisateur développant un conteneur pour atteindre un champ primitif.](../images/policies/consent-policy-map-field.png)
3. **Définir une valeur** - Définissez la valeur ou la condition à faire correspondre.
4. **Correspondance des clés de mappage** - Choisissez de cibler une clé spécifique ou de faire correspondre toutes les clés d’un mappage.
5. **Ajouter des conditions** - Combinez plusieurs règles à l’aide de la logique AND ou OR selon les besoins.

### Utilisation des champs booléens (logique de consentement implicite)

Les champs booléens stockent les valeurs de consentement vraies ou fausses et représentent les attributs de consentement les plus courants. L’opérateur `is not equal to` vous permet d’inclure des profils qui ne se sont pas explicitement désinscrits, prenant en charge les scénarios de consentement implicite.

**Opérateurs booléens et résultats**

| Opérateur | Valeur | Résultat |
|----------|-------|--------|
| `is equal to` | `true` | Inclut les profils avec consentement explicite (`true`). |
| `is equal to` | `false` | Inclut les profils avec désinscription explicite (`false`). |
| `is not equal to` | `true` | Inclut les profils sans consentement explicite (`false` ou manquants). |
| `is not equal to` | `false` | Inclut les profils qui ne se sont pas explicitement désinscrits (`true` ou manquants). |

**Exemple : consentement implicite par e-mail**

```
Field: consent.marketing.email (boolean)
Operator: is not equal to
Value: false
Result: Includes profiles who have not explicitly opted out of email marketing (includes both true and missing/null values).
```

### Utilisation des champs de mappage (préférences dynamiques)

Les champs de mappage stockent les paires clé-valeur avec des clés dynamiques, contrairement aux objets qui ont des schémas fixes. Les cartes sont souvent utilisées dans les centres de préférences où de nouvelles catégories peuvent être ajoutées sans mises à jour de schéma. Vous pouvez cibler des clés spécifiques ou utiliser la correspondance de caractères génériques pour toutes les clés.

**Correspondance de clés spécifique**

Utilisez cette approche pour cibler une catégorie de préférences spécifique.

```
Field: consent.preferences["email_preferences"].frequency (string) - navigated to from the map container
Operator: is equal to
Value: "weekly"
Result: Includes profiles who set the email frequency to weekly (for the "email_preferences" key)
```

**Toute correspondance de clé**

Utilisez l’option de case à cocher « **[!UICONTROL find any matching item]** » pour faire correspondre toutes les clés dynamiques d’un mappage.

![Créateur de règles affichant la case à cocher « Rechercher tout élément correspondant » pour Mapper les champs, utilisée pour faire correspondre les valeurs de toutes les clés dynamiques.](../images/policies/find-any-matching-item.png)

```
Field: consent.preferences.*.frequency (string)
Operator: is equal to
Value: "weekly"
Result: Includes profiles who set frequency to weekly in ANY preference category (for example, email_preferences, sms_preferences, or push_preferences)
```

### Utilisation des champs d’objet (navigation fixe)

Les champs d’objet agissent comme des conteneurs avec des schémas fixes. Ils sont utilisés uniquement pour la navigation et ne peuvent pas être référencés directement dans les conditions de la politique.

**Exemple de navigation**

```
consent.marketing (object) → consent.marketing.email (boolean)
```

**Exemple de cas d’utilisation :**

```
Field: consent.marketing.email (Boolean) - navigated to from the object
Operator: is equal to
Value: true
Result: Include profiles who have explicitly consented to marketing emails
```


### Utilisation de champs de tableau (valeurs multiples)

Les champs de tableau contiennent plusieurs valeurs du même type et nécessitent une gestion différente selon qu’ils stockent des primitives ou des objets. Les options de navigation et d’opérateur varient selon le type de tableau.

**Exemple de tableau de primitives**

Utilisez l’opérateur `contains` pour identifier les profils en fonction de valeurs spécifiques dans un tableau.

```
Field: consent.communication_channels (array of strings)
Operator: contains
Value: "email"
Result: Include profiles who have consented to email communication
```

**Exemple de tableau d’objets**

Accédez au tableau pour accéder aux champs primitifs dans les objets imbriqués.

```
Field: consent.preferences["email_preferences"].categories[].type - navigated to from the array
Operator: is equal to
Value: "promotional"
Result: Include profiles where any email category is "promotional"
```

## Combinaison de règles avec une logique complexe

Cette section explique comment combiner plusieurs conditions de règle à l’aide de la logique AND ou OR. Vous découvrirez comment les opérateurs logiques travaillent ensemble pour définir des politiques de consentement avancées et multiconditions.

### Combinaison de plusieurs conditions (logique AND ou OR)

Vous pouvez combiner plusieurs conditions de règle à l’aide de la logique AND ou OR afin de créer des politiques de consentement plus élaborées ciblant des segments de profil spécifiques.\
La **logique AND** nécessite que toutes les conditions soient vraies, produisant des correspondances d’audience plus étroites.\
La **logique OR** permet à n’importe quelle condition d’être vraie, ce qui étend la portée de l’audience.

Dans l’interface de la politique de consentement, utilisez le sélecteur logique qui s’affiche entre les conditions des règles pour basculer entre la logique ET et OU.

### Exemple de règle complexe générale

L’exemple suivant combine le statut de consentement de base avec la fréquence des préférences pour créer un segment ciblé.

```
Field: consent.marketing.email
Operator: is equal to true
AND
Field: consent.preferences.frequency
Operator: is not equal to "daily"
Result: Include profiles who consent to email marketing but not to a daily frequency
```

### Logique avancée pour les tableaux d’objets

Lorsque vous combinez des conditions dans des tableaux d’objets, le comportement dépend de l’utilisation de la logique AND ou OR entre les conditions.

**Exemple : tableau d’objets avec des conditions AND**

Utilisez la logique ET lorsque toutes les conditions doivent s’appliquer au *même* élément de tableau.

```
Field: consent.preferences["email_preferences"].categories[].enabled (boolean)
Operator: is equal to
Value: true
AND
Field: consent.preferences["email_preferences"].categories[].type (string)
Operator: is equal to
Value: "promotional"
Result: Includes profiles where the same category entry has both enabled=true and type="promotional".
Note: AND conditions apply to the same array entry. Using OR logic would include profiles if any array entry matches any of the conditions.
```

>[!TIP]
>
>**Bonnes pratiques relatives à la logique ET**
>
>Gardez à l’esprit ces comportements clés lors de la création de conditions de tableau basées sur ET :
>
>* Utilisez la logique ET lorsque toutes les conditions doivent s’appliquer au **même élément de tableau**.
>* N’oubliez pas que ET crée un ciblage restrictif (moins de profils correspondront).
>* Ne vous attendez pas à ce que la logique AND corresponde entre plusieurs entrées de tableau ; elle s’applique à chaque entrée.
>* Évitez d’utiliser la logique ET lorsque vous avez besoin d’une correspondance flexible entre les entrées.

>[!IMPORTANT]
>
>Avec la logique AND, chaque entrée de tableau doit satisfaire simultanément toutes les conditions spécifiées. Ce comportement est idéal lorsque vous devez faire correspondre des attributs combinés, tels que les catégories qui sont activées et promotionnelles.

>[!NOTE]
>
>La logique ET s’applique à la même entrée de tableau **uniquement pour les tableaux d’objets**.\
>Pour les tableaux de primitives, la logique ET est évaluée au niveau du champ sur l’ensemble du tableau.

**Exemple : tableau d’objets avec des conditions OR**

Utilisez la logique OR pour créer des correspondances d’audience inclusives en autorisant toute condition à être vraie sur les entrées de tableau.

```
Field: consent.preferences["email_preferences"].categories[].enabled (boolean)
Operator: is equal to
Value: true
OR
Field: consent.preferences["email_preferences"].categories[].type (string)
Operator: is equal to
Value: "newsletter"
Result: Includes profiles where any category entry has enabled=true or any entry has type="newsletter".
Note: OR logic allows matching across different array entries. One entry can meet the first condition while another meets the second.
```

### Étapes suivantes

Après avoir créé et affiné vos règles de politique de consentement, utilisez les ressources suivantes pour finaliser la configuration, valider l’application des politiques et passer en revue les modèles de données sous-jacents.

* **Workflow de création de politique** : implémentez les règles que vous avez définies dans l’interface utilisateur du créateur de politiques avec le [Guide de l’interface utilisateur de la politique de consentement](user-guide.md#consent-policy.md)
* **Évaluation et application de la politique de consentement** : vérifiez comment la politique activée affecte l’activation de l’audience et l’utilisation des données de profil. Pour plus d’informations, consultez le [guide d’application automatique des politiques](../enforcement/auto-enforcement.md)
* **Types de données de consentement XDM** : référencez les structures de schéma spécifiques et les définitions de champ pour les attributs de consentement utilisés dans vos règles de politique. Consultez le guide [Type de données de consentement et de préférence XDM](../../xdm/data-types/consents.md) .
