---
keywords: Experience Platform;guide de l’utilisateur;ia dédiée aux clients;rubriques les plus consultées;configurer l’instance;créer une instance;
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Configuration d’une instance IA dédiée aux clients
description: Les services d’IA/ML fournissent l’IA dédiée aux clients en tant que service Adobe Sensei simple d’utilisation configurable pour différents cas d’utilisation. Les sections suivantes décrivent les étapes de configuration d’une instance de Customer AI.
exl-id: 78353dab-ccb5-4692-81f6-3fb3f6eca886
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2829'
ht-degree: 7%

---


# Configuration d’une instance IA dédiée aux clients

L’IA dédiée aux clients, dans le cadre des services d’IA/ML, vous permet de générer des scores de propension personnalisés sans avoir à vous soucier du machine learning.

Les services d’IA/ML fournissent l’IA dédiée aux clients en tant que service Adobe Sensei simple d’utilisation configurable pour différents cas d’utilisation. Les sections suivantes décrivent les étapes de configuration d’une instance de Customer AI.

## Création d’une instance {#set-up-your-instance}

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Services]** dans le volet de navigation de gauche. Le navigateur **[!UICONTROL Services]** apparaît et affiche tous les services disponibles. Dans le conteneur de l’IA dédiée aux clients, sélectionnez **[!UICONTROL Ouvrir]**.

![](../images/user-guide/navigate-to-service.png)

L’interface utilisateur **IA dédiée aux clients** s’affiche et affiche toutes vos instances de service.

- La mesure **[!UICONTROL Nombre total de profils notés]** se trouve dans le coin inférieur droit du conteneur **[!UICONTROL Créer une instance]**. Cette mesure effectue le suivi du nombre total de profils notés par l’IA dédiée aux clients pour l’année civile en cours, y compris tous les environnements de test et toutes les instances de service supprimées.

![](../images/user-guide/total-profiles.png)

Les instances de service peuvent être modifiées, clonées et supprimées à l’aide des commandes situées sur le côté droit de l’interface utilisateur. Pour afficher ces commandes, sélectionnez une instance parmi vos **[!UICONTROL instances de service]** existantes. Les contrôles contiennent les éléments suivants :

- **[!UICONTROL Modifier]** : la sélection de **[!UICONTROL Modifier]** permet de modifier une instance de service existante. Vous pouvez modifier le nom, la description et la fréquence de notation de l’instance.
- **[!UICONTROL Cloner]** : la sélection de **[!UICONTROL Cloner]** copie la configuration de l’instance de service actuellement sélectionnée. Vous pouvez ensuite modifier le workflow pour apporter des ajustements mineurs et le renommer en tant que nouvelle instance.
- **[!UICONTROL Supprimer]** : vous pouvez supprimer une instance de service, y compris les exécutions historiques. Le jeu de données de sortie correspondant sera supprimé d’Experience Platform. Toutefois, les scores synchronisés avec le profil client en temps réel ne sont pas supprimés.
- **[!UICONTROL Source de données]** : lien vers le jeu de données utilisé par cette instance. Si plusieurs jeux de données sont utilisés, la sélection du texte de l’hyperlien ouvre la fenêtre contextuelle d’aperçu du jeu de données.
- **[!UICONTROL Détails de la dernière exécution]** : ils s’affichent uniquement lorsqu’une exécution échoue. Des informations sur les raisons de l’échec de l’exécution, telles que les codes d’erreur, sont affichées ici.
- **[!UICONTROL Définition d’un score]** : aperçu rapide de l’objectif que vous avez configuré pour cette instance.

![](../images/user-guide/service-instance-panel.png)

Pour créer une instance, sélectionnez **[!UICONTROL Créer une instance]**.

![](../images/user-guide/dashboard.png)

## Configurer

Le workflow de création d’instance apparaît, en commençant par l’étape **[!UICONTROL Configurer]**.

Vous trouverez ci-dessous des informations importantes sur les valeurs que vous pouvez renseigner dans l’instance :

- **[!UICONTROL Nom] :** le nom de l’instance est utilisé partout où les scores de l’IA dédiée aux clients sont affichés. Par conséquent, les noms doivent décrire ce que représentent les scores de prédiction. Par exemple, « Probabilité d’annuler un abonnement à un magazine ».

- **[!UICONTROL Description] :** description indiquant ce que vous essayez de prédire.

- **[!UICONTROL Type de propension] :** le type de propension détermine le but du score et la polarité des mesures. Vous pouvez choisir **[!UICONTROL Attrition]** ou **[!UICONTROL Conversion]**. Pour plus d’informations sur l’impact du type de propension sur votre instance, consultez la note située sous [résumé de notation](./discover-insights.md#scoring-summary) dans le document d’informations sur les découvertes.

![Écran Configuration](../images/user-guide/create-instance.png)

Fournissez les valeurs requises, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

## Sélectionner les données {#select-data}

Par défaut, l’IA dédiée aux clients utilise Adobe Analytics, Adobe Audience Manager, les événements d’expérience en général et les données d’événement d’expérience client pour calculer des scores de propension. Lors de la sélection d’un jeu de données, seuls les jeux compatibles avec l’IA dédiée aux clients sont répertoriés. Pour sélectionner un jeu de données, sélectionnez le symbole (**+**) en regard du nom du jeu de données ou cochez la case pour ajouter plusieurs jeux de données à la fois. Utilisez l’option de recherche pour trouver rapidement les jeux de données qui vous intéressent.

![Sélectionner et rechercher un jeu de données](../images/user-guide/configure-dataset-page-save-and-exit-cai.png)

Après avoir sélectionné les jeux de données que vous souhaitez utiliser, cliquez sur le bouton **[!UICONTROL Ajouter]** pour ajouter les jeux de données au volet d’aperçu du jeu de données.

![Sélectionner des jeux de données](../images/user-guide/select-datasets.png)

Si vous sélectionnez l’icône d’informations ![icône d’informations](/help/images/icons/info.png) en regard du jeu de données, la fenêtre contextuelle d’aperçu du jeu de données s’ouvre.

![Sélectionner et rechercher un jeu de données](../images/user-guide/dataset-info.png)

L’aperçu du jeu de données contient des données telles que l’heure de la dernière mise à jour, le schéma source et un aperçu des dix premières colonnes.

Sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer les brouillons tout au long du workflow. Vous pouvez également enregistrer les configurations de modèle de brouillon et passer à l’étape suivante du workflow. Utilisez **[!UICONTROL Enregistrer et continuer]** pour créer et enregistrer des brouillons lors des configurations de modèle. La fonction vous permet de créer et d&#39;enregistrer des brouillons de la configuration du modèle. Elle est particulièrement utile lorsque vous devez définir de nombreux champs dans le processus de configuration.

![Le workflow Créer de l’onglet IA dédiée aux clients des services de science des données avec Enregistrer et Enregistrer et continuer en surbrillance.](../images/user-guide/cai-save-and-exit.png)

### Exhaustivité du jeu de données {#dataset-completeness}

L’aperçu du jeu de données contient une valeur de pourcentage d’exhaustivité du jeu de données. Cette valeur fournit un instantané rapide du nombre de colonnes vides/nulles de votre jeu de données. Si un jeu de données contient de nombreuses valeurs manquantes et que ces valeurs sont capturées ailleurs, il est vivement recommandé d’inclure le jeu de données contenant les valeurs manquantes. Dans cet exemple, l’ID de personne est vide, mais il est capturé dans un jeu de données distinct qui peut être inclus.

>[!NOTE]
>
>L’exhaustivité des jeux de données est calculée à l’aide de la fenêtre d’entraînement maximale pour l’IA dédiée aux clients (un an). Cela signifie que les données de plus d’un an ne sont pas prises en compte lors de l’affichage de la valeur d’exhaustivité de votre jeu de données.

![ Exhaustivité du jeu de données ](../images/user-guide/dataset-info-2.png)

### Sélectionner une identité {#identity}

Vous pouvez désormais joindre plusieurs jeux de données les uns aux autres en fonction du mappage d’identité (champ). Vous devez sélectionner un type d’identité (également appelé « espace de noms d’identité ») et une valeur d’identité dans cet espace de noms. Si vous avez affecté plusieurs champs en tant qu’identité dans votre schéma sous le même espace de noms, toutes les valeurs d’identité affectées apparaissent dans la liste déroulante d’identités précédée de l’espace de noms, par exemple `EMAIL (personalEmail.address)` ou `EMAIL (workEmail.address)`.

[sélectionner le même espace de noms](../images/user-guide/cai-identity-map.png)

>[!IMPORTANT]
>
>Le même type d’identité (espace de noms) doit être utilisé pour chaque jeu de données que vous sélectionnez. Une coche verte apparaît en regard du type d’identité dans la colonne d’identité, indiquant que les jeux de données sont compatibles. Par exemple, lors de l’utilisation de l’espace de noms Téléphone et `mobilePhone.number` comme identifiant, tous les identifiants des jeux de données restants doivent contenir et utiliser l’espace de noms Téléphone .

Pour sélectionner une identité, sélectionnez la valeur soulignée située dans la colonne d’identité. La fenêtre contextuelle de sélection d’une identité s’affiche.

<!-- ![select same namespace](../images/user-guide/identity-type.png) -->
[sélectionner le même espace de noms](../images/user-guide/cai-identity-namespace.png)

Dans le cas où plusieurs identités sont disponibles dans un espace de noms, veillez à sélectionner le champ d’identité approprié à votre cas d’utilisation. Par exemple, deux identités d’e-mail sont disponibles dans l’espace de noms e-mail, une adresse e-mail professionnelle et une adresse e-mail personnelle. Selon le cas d’utilisation, un e-mail personnel est plus susceptible d’être renseigné et plus utile dans les prédictions individuelles. Cela signifie que `EMAIL (personalEmail.address)` sera sélectionné comme identité.

![Clé du jeu de données non sélectionnée](../images/user-guide/select-identity.png)

>[!NOTE]
>
> S’il n’existe aucun type d’identité valide (espace de noms) pour un jeu de données, vous devez définir une identité principale et l’affecter à un espace de noms d’identité à l’aide de l’[éditeur de schéma](../../../xdm/schema/composition.md#identity). Pour en savoir plus sur les espaces de noms et les identités, consultez la documentation [ Espaces de noms du service d’identités ](../../../identity-service/features/namespaces.md).

## Définition d’un objectif {#define-a-goal}

<!-- https://www.adobe.com/go/cai-define-a-goal -->

L’étape **[!UICONTROL Définir l’objectif]** s’affiche et fournit un environnement interactif dans lequel vous pouvez définir visuellement un objectif de prédiction. Un objectif est composé d’un ou de plusieurs événements, où l’occurrence de chaque événement est basée sur la condition qu’il contient. L’objectif d’une instance de Customer AI est de déterminer la probabilité d’atteindre l’objectif au cours d’une période donnée.

Pour créer un objectif, sélectionnez **[!UICONTROL Saisir le nom du champ]** puis un champ dans la liste déroulante. Sélectionnez la deuxième entrée, une clause pour la condition de l’événement, puis fournissez éventuellement la valeur cible pour terminer l’événement. D’autres événements peuvent être configurés en sélectionnant **[!UICONTROL Ajouter un événement]**. Enfin, complétez l’objectif en appliquant un délai de prédiction en nombre de jours, puis sélectionnez **[!UICONTROL Suivant]**.

<!-- ![](../images/user-guide/define-a-goal.png) -->
![](../images/user-guide/cai-define-a-goal.png)

### Se produira et ne se produira pas

Lors de la définition de votre objectif, vous avez la possibilité de sélectionner **[!UICONTROL Aura lieu]** ou **[!UICONTROL N’aura pas lieu]**. Sélectionner **[!UICONTROL Se produira]** signifie que les conditions d’événement que vous définissez doivent être remplies pour que les données d’événement d’un client soient incluses dans l’interface utilisateur des insights.

Par exemple, si vous souhaitez configurer une application pour prédire si un client effectuera un achat, vous pouvez sélectionner **[!UICONTROL Se produira]** suivi de **[!UICONTROL Tous les]**, puis saisir **commerce.purchases.id** (ou un champ similaire) et **[!UICONTROL existe]** en tant qu’opérateur.

<!-- ![will occur](../images/user-guide/occur.png) -->
![se produira](../images/user-guide/cai-will-occur.png)

Cependant, il peut y avoir des cas où vous souhaitez prédire si un événement ne se produira pas dans une certaine période. Pour configurer un objectif avec cette option, sélectionnez **[!UICONTROL Ne se produira pas]** dans la liste déroulante de niveau supérieur.

Par exemple, si vous souhaitez prédire quels clients seront moins engagés et que vous ne consultez pas la page de connexion à votre compte le mois prochain. Sélectionnez **[!UICONTROL Ne se produira pas]** suivi de **[!UICONTROL Tous les]**, puis saisissez **web.webInteraction.URL** (ou un champ similaire) et **[!UICONTROL est égal à]** en tant qu’opérateur avec **account-login** comme valeur.

![ne se produira pas](../images/user-guide/not-occur.png)

### Tous les et tous les

Dans certains cas, vous pouvez vouloir prédire si une combinaison d’événements se produira et, dans d’autres cas, vous pouvez vouloir prédire l’occurrence de n’importe quel événement à partir d’un ensemble prédéfini. Pour prédire si un client aura une combinaison d’événements, sélectionnez l’option **[!UICONTROL Tout le]** dans la liste déroulante de deuxième niveau de la page **[!UICONTROL Définir l’objectif]**.

Par exemple, vous pouvez vouloir prédire si un client achète un produit particulier. Cet objectif de prédiction est défini par deux conditions : une `commerce.order.purchaseID` **existe** et la `productListItems.SKU` **est égale** à une valeur spécifique.

![Tous les exemples](../images/user-guide/all-of.png)

Pour prédire si un client disposera d’un événement d’un ensemble donné, vous pouvez utiliser l’option **[!UICONTROL N’importe lequel]**.

Par exemple, vous pouvez vouloir prédire si un client visite une certaine URL ou une page web avec un nom particulier. Cet objectif de prédiction est défini par deux conditions : `web.webPageDetails.URL` **commence par** une valeur particulière et `web.webPageDetails.name` **commence par** une valeur particulière.

![N’importe quel exemple](../images/user-guide/any-of.png)

### Population éligible *(facultatif)*

Par défaut, les scores de propension sont générés pour tous les profils, sauf si une population éligible est spécifiée. Vous pouvez spécifier une population éligible en définissant des conditions pour inclure ou exclure des profils en fonction des événements.

![population éligible](../images/user-guide/eligible-population.png)

### Événements personnalisés (*facultatif*) {#custom-events}

Si vous disposez d’informations supplémentaires en plus des [champs d’événement standard](../data-requirements.md#standard-events) utilisés par l’IA dédiée aux clientes et clients pour générer des scores de propension, une option d’événements personnalisés est fournie. L’utilisation de cette option vous permet d’ajouter des événements supplémentaires que vous jugez influents, ce qui peut améliorer la qualité de votre modèle et contribuer à fournir des résultats plus précis. Si le jeu de données sélectionné contient des événements personnalisés définis dans votre schéma, vous pouvez les ajouter à votre instance.

>[!NOTE]
>
> Pour une explication détaillée de l’impact des événements personnalisés sur les résultats de notation de l’IA dédiée aux clients, consultez la section [Exemple d’événement personnalisé](#custom-event).

![fonctionnalité d’événement](../images/user-guide/event-feature.png)

Pour ajouter un événement personnalisé, sélectionnez **[!UICONTROL Ajouter un événement personnalisé]**. Saisissez ensuite un nom d’événement personnalisé, puis mappez-le au champ d’événement de votre schéma. Les noms des événements personnalisés s’affichent à la place de la valeur des champs lorsque vous examinez des facteurs d’influence et d’autres informations. Cela signifie que le nom de l’événement personnalisé sera utilisé au lieu de l’ID/la valeur de l’événement. Pour plus d’informations sur l’affichage des événements personnalisés, consultez la section [exemple d’événement personnalisé](#custom-event). Ces événements personnalisés supplémentaires sont utilisés par l’IA dédiée aux clientes et clients pour améliorer la qualité de votre modèle et fournir des résultats plus précis.

![Champ d’événement personnalisé](../images/user-guide/custom-event.png)

Sélectionnez ensuite l’opérateur que vous souhaitez utiliser dans le menu déroulant des opérateurs disponibles . Seuls les opérateurs compatibles avec l&#39;événement sont répertoriés.

![Opérateur d’événement personnalisé](../images/user-guide/custom-operator.png)

Enfin, saisissez la ou les valeurs du champ si l&#39;opérateur sélectionné en a besoin. Dans cet exemple, il nous suffit de voir s’il existe une réservation d’hôtel ou de restaurant. Cependant, pour être plus précis, nous pouvons utiliser l’opérateur égal à et saisir une valeur exacte dans l’invite de valeur.

![Valeur du champ Événement personnalisé](../images/user-guide/custom-value.png)

Une fois l’opération terminée, sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour continuer.

### Attributs de profil personnalisés (*facultatif*)

Vous pouvez définir des champs de jeu de données de profil importants (avec horodatages) dans vos données en plus des [ champs d’événement standard ](../data-requirements.md#standard-events) utilisés par l’IA dédiée aux clientes et clients pour générer des scores de propension. L’utilisation de cette option vous permet d’ajouter des attributs de profil supplémentaires que vous jugez influents, ce qui peut améliorer la qualité de votre modèle et fournir des résultats plus précis. En outre, l’ajout d’attributs de profil personnalisés permet à l’IA dédiée aux clientes et clients de mieux présenter la manière dont des profils particuliers ont fini dans un compartiment de propension.

>[!NOTE]
>
>L’ajout d’un attribut de profil personnalisé suit le même processus que l’ajout d’un événement personnalisé. Tout comme les événements personnalisés, les attributs de profil personnalisés affectent la notation de votre modèle de la même manière. Pour une explication détaillée, consultez la section [Exemple d’événement personnalisé](#custom-event).

![ajouter un attribut de profil personnalisé](../images/user-guide/profile-attributes.png)

#### Sélection des attributs de profil à partir de l’exportation de l’instantané de profil

Vous pouvez également choisir d’inclure les attributs de profil à partir de l’exportation quotidienne d’instantanés de profil. Ces attributs sont synchronisés avec l’exportation de l’instantané de profil et affichent la valeur disponible la plus récente. Elles s’affichent automatiquement et ne nécessitent pas de sélectionner un jeu de données à l’étape de configuration.

>[!WARNING]
>
> Ne sélectionnez pas d’attribut de profil qui a été mis à jour en raison de l’objectif de prédiction ou qui est fortement corrélé à l’objectif de prédiction. Cela entraîne une fuite de données et un ajustement excessif du modèle. Par exemple, `total_purchases_in_the_last_3_months` est un attribut qui prédit la conversion des achats.

### Ajout d’un exemple d’événement personnalisé {#custom-event}

Dans l’exemple suivant, un événement personnalisé et un attribut de profil sont ajoutés à une instance IA dédiée aux clients. L’objectif de l’instance IA dédiée aux clients est de prédire la probabilité qu’un client achète un autre produit Luma au cours des 60 prochains jours. Normalement, les données de produit sont liées à un SKU de produit. Dans ce cas, le SKU est `prd1013`. Une fois le modèle de l’IA dédiée aux clients formé/noté, ce SKU peut être lié à un événement et affiché comme un facteur d’influence pour un intervalle de propension.

L’IA dédiée aux clients applique automatiquement la génération de fonctionnalités telles que « Jours écoulés » ou « Nombre de » par rapport aux événements personnalisés tels que **Observer l’achat**. Si cet événement a été considéré comme un facteur d’influence sur les raisons pour lesquelles les clients présentent une propension élevée, moyenne ou faible, Customer AI l’affiche comme `Days since prd1013 purchase` ou `Count of prd1013 purchase`. En créant cet événement en tant qu&#39;événement personnalisé, vous pouvez lui donner un nouveau nom, ce qui facilite la lecture des résultats. Par exemple : `Days since Watch purchase`. En outre, l’IA dédiée aux clientes et clients utilise cet événement dans son entraînement et sa notation même si l’événement n’est pas standard. Cela signifie que vous pouvez ajouter plusieurs événements que vous pensez pouvoir influencer et personnaliser davantage votre modèle en incluant des données telles que des réservations, des journaux des visiteurs et d’autres événements. L’ajout de ces points de données améliore encore la précision de votre modèle d’IA dédiée aux clients.

![exemple d’événement personnalisé](../images/user-guide/custom-event-name.png)

## Définir les options

L’étape de définition des options vous permet de configurer un planning pour automatiser les exécutions de prévisions, de définir des exclusions de prévisions pour filtrer certains événements et d’activer/désactiver **[!UICONTROL Profile]**.

### Configuration d’un planning *(facultatif)* {#configure-a-schedule}

Pour configurer un planning de notation, commencez par configurer la **[!UICONTROL fréquence de notation]**. Les opérations de prédiction automatisées peuvent être planifiées pour une exécution hebdomadaire ou mensuelle.

![](../images/user-guide/schedule.png)

### Exclusions de prévision *(facultatif)*

Si votre jeu de données contient des colonnes ajoutées en tant que données de test, vous pouvez ajouter cette colonne ou cet événement à une liste d’exclusions en sélectionnant **[!UICONTROL Ajouter une exclusion]** puis en saisissant le champ que vous souhaitez exclure. Cela empêche l’évaluation des événements répondant à certaines conditions lors de la génération de scores. Cette fonctionnalité peut être utilisée pour filtrer les entrées de données ou les promotions non pertinentes.

Pour exclure un événement, sélectionnez **[!UICONTROL Ajouter une exclusion]** et définissez l’événement. Pour supprimer une exclusion, sélectionnez les points de suspension (**[!UICONTROL ...]**) en haut à droite du conteneur d’événements, puis sélectionnez **[!UICONTROL Supprimer le conteneur]**.

![](../images/user-guide/exclusion.png)

### Basculement de profil

Le bouton Profile permet à Customer AI d’exporter les résultats de notation dans le profil client en temps réel. La désactivation de ce bouton empêche l’ajout des résultats de notation des modèles au profil. Les résultats de notation de l’IA dédiée aux clients sont toujours disponibles avec cette fonctionnalité désactivée.

Lorsque vous utilisez l’IA dédiée aux clientes et clients pour la première fois, vous pouvez désactiver cette fonctionnalité jusqu’à ce que vous soyez satisfait des résultats de sortie du modèle. Cela vous empêche de charger plusieurs jeux de données de notation vers vos profils clients tout en affinant votre modèle. Une fois l’étalonnage de votre modèle terminé, vous pouvez cloner le modèle à l’aide de l’option [cloner](#set-up-your-instance) de la page **Instances de service**. Vous pouvez ainsi créer une copie de votre modèle et activer le profil.

![Bascule des profils](../images/user-guide/advanced-workflow-save.png)

Une fois votre planning de notation défini, les exclusions de prédiction incluses et le bouton (bascule) du profil où vous souhaitez qu’il soit, sélectionnez **[!UICONTROL Terminer]** dans le coin supérieur droit pour créer votre instance IA dédiée aux clients.

Si l’instance est créée avec succès, une opération de prédiction se déclenche immédiatement et les suivantes s’exécutent selon le planning défini.

>[!NOTE]
>
>Selon la taille des données d’entrée, les exécutions de prédiction peuvent prendre jusqu’à 24 heures.

En suivant cette section, vous avez configuré une instance de l’IA dédiée aux clients et exécuté une exécution de prédiction. Une fois l’exécution réussie, les informations notées renseignent automatiquement les profils avec les scores prévus si le bouton (bascule) Profil est activé. Veuillez patienter jusqu’à 24 heures avant de passer à la section suivante de ce tutoriel.

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez configuré une instance de Customer AI et généré des scores de propension. Vous pouvez désormais choisir d’utiliser le créateur de segments pour [créer des segments de clients avec les scores prévus](./create-segment.md) ou [découvrir des informations avec l’IA dédiée aux clients](./discover-insights.md).

## Ressources supplémentaires

La vidéo suivante est conçue pour vous aider à comprendre le workflow de configuration de l’IA dédiée aux clients. Vous trouverez également les bonnes pratiques et des exemples de cas d’utilisation.

>[!IMPORTANT]
>
> La vidéo suivante est obsolète. Pour obtenir les informations les plus récentes, reportez-vous à la documentation .

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)

<!-- comment -->
