---
keywords: Experience Platform;interface utilisateur;interface utilisateur;personnalisation;tableau de bord d’utilisation de la licence;tableau de bord;utilisation des licences;droits;consommation
title: Tableau de bord d’utilisation de la licence
description: Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur l’utilisation des licences de votre entreprise.
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: b1de61b2e7d0dedf2da8ef8ffb02fe5c15e82fb2
workflow-type: tm+mt
source-wordcount: '2720'
ht-degree: 9%

---

# Tableau de bord d’utilisation des licences {#license-usage-dashboard}

>[!CONTEXTUALHELP]
>id="testy-mctestface"
>title="Boîte de dialogue de test qui ne doit pas être visible"
>abstract="L&#39;objet {name} est affiché sur {date}."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_core"
>title="Table des produits principaux"
>abstract="Les produits principaux répertoriés dans le tableau comportent leurs propres mesures, suivi de l’utilisation et vues d’analyse au niveau de l’environnement de test. Ces produits principaux fournissent les mesures clés pour le suivi et les modules complémentaires sont inclus dans ces mesures."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_addons"
>title="Tableau des modules complémentaires"
>abstract="Le tableau des modules complémentaires répertorie les produits dont le montant des licences est combiné aux mesures prises en charge par les produits principaux. Ces modules complémentaires ne comportent pas de mesures distinctes, mais améliorent le suivi de l’utilisation des produits principaux auxquels ils sont associés."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage"
>title="Tableau de bord d’utilisation des licences"
>abstract="Le tableau de bord d’utilisation des licences donne des informations sur les produits Adobe Experience Platform que vous avez achetés. La vue d’ensemble du tableau de bord affiche les mesures principales pour vos produits, notamment votre utilisation pour chacune d’entre elles et la quantité de licences contractées. L’espace de travail des détails affiche une répartition de vos mesures pour chaque produit dans des sandbox spécifiques."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration" text="Expirations automatisées des jeux de données"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/profile/pseudonymous-profiles" text="Expiration des données de profils pseudonymes"

>[!CONTEXTUALHELP]
>id="platform_licenseusage"
>title="Tableau de bord d’utilisation des licences"
>abstract="Le tableau de bord d’utilisation des licences donne des informations sur les produits Adobe Experience Platform que vous avez achetés. La vue d’ensemble du tableau de bord affiche les mesures principales pour vos produits, notamment votre utilisation pour chacune d’entre elles et la quantité de licences contractées. L’espace de travail des détails affiche une répartition de vos mesures pour chaque produit dans des sandbox spécifiques."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration" text="Expirations automatisées des jeux de données"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/profile/pseudonymous-profiles" text="Expiration des données de profils pseudonymes"

Vous pouvez afficher des informations importantes sur l’utilisation des licences de votre entreprise via le tableau de bord [!UICONTROL Utilisation de la licence] de Adobe Experience Platform. Les informations affichées ici sont capturées pendant un instantané quotidien de votre instance Platform.

Les rapports sur l’utilisation des licences fournissent un niveau de granularité élevé par rapport à vos mesures d’utilisation des licences. Le tableau de bord fournit des mesures d’utilisation pour chaque produit acheté, l’utilisation consolidée des mesures dans tous les environnements de test de production ou de développement et la mesure d’utilisation d’un environnement de test spécifique. Les applications Experience Platform suivantes peuvent être suivies avec des mesures d’utilisation : Real-Time Customer Data Platform, Adobe Journey Optimizer et Customer Journey Analytics.

Ce guide explique comment accéder au tableau de bord de l’utilisation des licences dans l’interface utilisateur et l’utiliser. Il fournit également des informations supplémentaires sur les visualisations affichées dans le tableau de bord.

Pour une présentation générale de l’interface utilisateur de Platform, reportez-vous au [guide de l’interface utilisateur Experience Platform](../../landing/ui-guide.md).

## Données du tableau de bord [!UICONTROL Usage de la licence]

Le tableau de bord [!UICONTROL Utilisation de la licence] affiche la liste de tous les produits Experience Platform que vous avez achetés. Dans cette liste, vous pouvez trouver un instantané des données liées aux licences de votre entreprise pour Experience Platform sur n’importe quel environnement de test associé.

Les données de ce tableau de bord s’affichent exactement comme elles apparaissent au moment précis où l’instantané a été pris. En d’autres termes, l’instantané n’est pas une approximation ou un échantillon des données et le tableau de bord n’est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis la prise dʼun instantané ne seront pas reflétées dans le tableau de bord avant la prise de lʼinstantané suivant.

## Exploration du tableau de bord de l’utilisation des licences {#explore}

Pour accéder au tableau de bord de l’utilisation des licences dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Utilisation de la licence]** dans le rail de gauche. L’onglet [!UICONTROL Aperçu] s’ouvre, affichant une liste des produits disponibles.

>[!NOTE]
>
>Le tableau de bord de l’utilisation des licences n’est pas activé par défaut. Les utilisateurs doivent disposer de l’autorisation &quot;Afficher le tableau de bord de l’utilisation de la licence&quot; pour pouvoir afficher le tableau de bord. Pour obtenir des instructions sur l’octroi des autorisations d’accès pour l’affichage du tableau de bord d’utilisation des licences, reportez-vous au [guide des autorisations du tableau de bord](../permissions.md).

![ Onglet Aperçu du tableau de bord de l’utilisation de la licence, avec l’utilisation de la licence mise en surbrillance dans la barre de navigation de gauche.](../images/license-usage/dashboard-overview.png)

## Onglet [!UICONTROL Aperçu] {#overview-tab}

Ce tableau de bord affiche sous forme de tableau tous les produits Adobe Experience Platform sous licence, y compris les modules complémentaires. Le tableau fournit des informations clés sur l’utilisation de votre licence pour tous les profils disponibles.

| Nom de la colonne | Description |
|---|---|
| **[!UICONTROL Produit]** | La solution d’Adobe sous licence de votre entreprise. |
| **[!UICONTROL Mesure de Principal]** | Mesure principale utilisée pour le suivi dans pour ce produit. |
| **[!UICONTROL Montant de la licence]** | La valeur contractuelle correspondant au montant maximal de la mesure de Principal, conformément à ce qui est convenu dans votre contrat de licence de produit. |
| **[!UICONTROL Utilisation]** | Montant de la mesure principale utilisée. Cette valeur fournit l’utilisation totale de cette mesure pour tous les environnements de test, que ce soit la production ou le développement. |
| **[!UICONTROL Utilisation %]** | Le pourcentage de votre mesure principale utilisée en fonction de votre montant de licence. |
| **[!UICONTROL Utilisation de prédiction]** | Pourcentage d’utilisation prévu de votre mesure principale en fonction du montant de votre licence. |

>[!NOTE]
>
>Des ajouts au [!UICONTROL montant de la licence] résultant de modules complémentaires sont ajoutés en plus du [!UICONTROL montant de la licence] pour les produits de base tels que Real-Time Customer Data Platform, Adobe Journey Optimizer et Customer Journey Analytics. L’utilisation de ce montant sous licence (après les modules complémentaires) est suivie par le biais des produits de base. Par exemple, si vous achetez un pack de cinq environnements de test, la quantité de cinq est ajoutée à celle du produit de base. Dans ce cas, le module complémentaire affiche un [!UICONTROL montant de la licence] d’un seul et l’utilisation de ce module complémentaire est &quot;vide&quot; car l’utilisation est suivie par le biais du produit de base.

Le tableau indique la mesure principale de chaque produit, car chaque produit peut effectuer le suivi de nombreuses mesures.

### Utilisation prévue {#predicted-usage}

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage_prediction"
>title="Utilisation prévue"
>abstract="Les prédictions sont basées sur l&#39;utilisation des 6 à 7 derniers mois et sont générées le 15 de chaque mois. Notez que les prédictions d’utilisation des licences sont des approximations basées sur l’utilisation passée. Il vous incombe de comprendre l’utilisation réelle de votre entreprise et de vous assurer que cette utilisation ne dépasse pas la portée de la licence de votre entreprise avec Adobe. Pour réduire l’utilisation, vous pouvez configurer des expirations de données de jeu de données ou de profil pseudonymes pour les environnements de test et les jeux de données."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration" text="Expirations automatisées des jeux de données"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/profile/pseudonymous-profiles" text="Expiration des données de profils pseudonymes"

>[!CONTEXTUALHELP]
>id="platform_licenseusage_prediction"
>title="Utilisation prévue"
>abstract="Les prédictions sont basées sur l&#39;utilisation des 6 à 7 derniers mois et sont générées le 15 de chaque mois. Notez que les prédictions d’utilisation des licences sont des approximations basées sur l’utilisation passée. Il vous incombe de comprendre l’utilisation réelle de votre entreprise et de vous assurer que cette utilisation ne dépasse pas la portée de la licence de votre entreprise avec Adobe. Pour réduire l’utilisation, vous pouvez configurer des expirations de données de jeu de données ou de profil pseudonymes pour les environnements de test et les jeux de données."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration" text="Expirations automatisées des jeux de données"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/profile/pseudonymous-profiles" text="Expiration des données de profils pseudonymes"

Gérez et optimisez vos ressources de licence de manière proactive en fonction de prédictions d’utilisation éclairées. La colonne [!UICONTROL  Utilisation prédite] prédit précisément l’utilisation future des licences au niveau des environnements de test, dans tous les environnements de test de production et de développement, pour tous les produits que vous avez achetés. Cette fonctionnalité d’alerte fournit une prévision de l’utilisation des licences pour six semaines à venir, en fonction de votre utilisation jusqu’au 15 du mois civil. Les prédictions sont fournies avec une limite inférieure et une limite supérieure.

>[!IMPORTANT]
>
>Les prévisions sont actualisées tous les mois. La date d’actualisation est incluse dans une icône d’information (![Cette icône d’information.](../images/license-usage/info-icon.png)) au-dessus du titre de la colonne.

Pour afficher un résumé de l’utilisation des droits des produits, sélectionnez un produit dans la liste [!UICONTROL Aperçu].

![ [!UICONTROL Utilisation de la licence] [!UICONTROL Aperçu] avec un produit et la colonne d’utilisation prédite mise en surbrillance.](../images/license-usage/product-predicted-usage.png)

L’onglet Résumé s’affiche. Vous pouvez utiliser les prédictions granulaires disponibles sur les onglets [!UICONTROL Summary] et [!UICONTROL Details] pour garantir une prise de décision éclairée pour une utilisation efficace de la licence.

>[!NOTE]
>
>Notez que les prédictions d’utilisation des licences sont des approximations basées sur l’utilisation passée. Il vous incombe de comprendre l’utilisation réelle de votre entreprise et de vous assurer que cette utilisation ne dépasse pas la portée de la licence de votre entreprise avec Adobe.

![L’affichage récapitulatif d’un produit Platform avec la colonne d’utilisation prédite mise en surbrillance.](../images/license-usage/summary-predicted-usage.png)

Le pourcentage d’utilisation prévue est déterminé comme suit :

- Si les limites inférieure et supérieure sont significativement différentes, elles s’affichent sous la forme d’une plage (par exemple, entre 32 % et 35 %).
- Si les limites inférieure et supérieure sont presque identiques et non nulles, elles s’affichent sous la forme d’une valeur approximative (par exemple, ~34 %).
- Si les limites inférieure et supérieure sont presque identiques et nulles, elles s’affichent exactement à 0 %.

>[!NOTE]
>
>Dans ce contexte, &quot;Presque identique&quot; signifie que les valeurs sont statistiquement significatives à deux décimales (par exemple, une limite inférieure de 0,342 et une limite supérieure de 0,344 sont toutes deux arrondies à 34 %).

La fonction d’utilisation prévue prend en charge les mesures suivantes :

- [!UICONTROL Audience adressable]
- [!UICONTROL Richesse moyenne du profil]
- [!UICONTROL Heures de calcul]
- [!UICONTROL Nombre de lignes de l’audience du Parcours client]
- [!UICONTROL Stockage total]

## Onglet [!UICONTROL Résumé] {#summary-tab}

Pour afficher d’autres mesures et des informations détaillées sur l’utilisation de votre licence de produit, sélectionnez un nom de produit dans la liste. La vue [!UICONTROL Summary] pour ce produit s’affiche. Toutes les mesures disponibles sont affichées dans l’onglet [!UICONTROL Résumé]. Les mesures disponibles dépendent du produit sous licence. Cette vue fournit **une vue consolidée de toutes les mesures sur tous les environnements de test de production ou de développement**. Le même niveau d’analyse est fourni pour les environnements de test de production et de développement.

![Vue récapitulative d’un produit Platform qui affiche toutes les mesures disponibles pour ce produit.](../images/license-usage/summary-tab.png)

Dans l’onglet Résumé, le tableau comprend la colonne [!UICONTROL Mesure]. Ces descriptions lisibles par l’utilisateur indiquent toutes les mesures utilisées pour ce type d’environnement de test.

### Sélectionner un sandbox {#select-sandbox}

Pour modifier l’affichage entre les types d’environnements de test de production et de développement, sélectionnez [!UICONTROL Environnements de test de production] ou [!UICONTROL Environnements de test de développement]. Le type d’environnement de test sélectionné est indiqué par le bouton radio en regard du nom de l’environnement de test.

La création de rapports de consommation pour les environnements de test est cumulative pour tous les environnements de test du même type. En d’autres termes, la sélection de [!UICONTROL Production] ou [!UICONTROL Développement] fournit des rapports de consommation pour tous les environnements de test de production ou de développement, respectivement.

![L’affichage récapitulatif d’un produit Platform avec des environnements de test de production et des environnements de test de développement mis en surbrillance.](../images/license-usage/summary-tab-sandboxes.png)

>[!WARNING]
>
>L’autorisation d’afficher le tableau de bord de l’utilisation des licences doit être spécifiée au niveau de l’environnement de test. Ajoutez des autorisations à chaque environnement de test individuel pour les afficher dans le tableau de bord. Cette limitation sera corrigée dans une version ultérieure. En attendant, la solution suivante est disponible :
>
>1. Créez un profil de produit dans Adobe Admin Console.
>2. Sous Autorisation dans la catégorie Sandbox , ajoutez tous les environnements de test que vous souhaitez afficher dans le tableau de bord de l’utilisation des licences.
>3. Dans la catégorie Autorisation du tableau de bord utilisateur , ajoutez l’autorisation &quot;Afficher le tableau de bord de l’utilisation de la licence&quot;.

## Onglet [!UICONTROL Détails] {#details-tab}

Pour afficher **une mesure d’utilisation spécifique d’un environnement de test spécifique**, accédez à l’onglet [!UICONTROL Détails] . L’onglet [!UICONTROL Détails] affiche tous les environnements de test disponibles dans les environnements de test de production ou de développement.

![Onglet Détails du tableau de bord Utilisation de la licence.](../images/license-usage/details-tab.png)

Dans cette vue, vous pouvez sélectionner l&#39;icône ![Inspecter.](/help/images/icons/inspect.png) en regard d’un nom d’environnement de test pour afficher la visualisation de cette mesure. Une boîte de dialogue s’ouvre avec une visualisation pour cette mesure.

### Visualisations {#visualizations}

Chaque widget de visualisation comprend les aspects suivants :

- Graphique linéaire qui suit le changement de mesure au fil du temps
- Clé du graphique linéaire.
- Nom de l’environnement de test
- Menu déroulant permettant d’ajuster la période du graphique linéaire.

Les graphiques linéaires comparent les chiffres d’utilisation de votre entreprise au total disponible avec les licences de votre entreprise et fournissent un pourcentage de l’utilisation totale.

![Visualisation d’une mesure.](../images/license-usage/visualization.png)

La période de recherche arrière de l’analyse peut être ajustée à partir du menu déroulant. Valeur par défaut des 30 derniers jours

Pour sélectionner une plage de dates, vous pouvez utiliser la liste déroulante de plage de dates afin de sélectionner la période à afficher dans le tableau de bord. Plusieurs options sont disponibles, notamment la valeur par défaut des 30 derniers jours.

![La boîte de dialogue de visualisation avec la liste déroulante de période mise en surbrillance.](../images/license-usage/date-range.png)

Vous pouvez également sélectionner **[!UICONTROL Date personnalisée]** pour choisir la période qui s’affiche.

![ L’onglet Aperçu du tableau de bord de l’utilisation de la licence avec les options de période personnalisées surlignées.](../images/license-usage/custom-date-range.png)

## Mesures disponibles {#available-metrics}

Le tableau de bord de l’utilisation des licences répertorie plusieurs mesures uniques qui s’appliquent à plusieurs produits de l’entreprise. Les mesures disponibles sont les suivantes :

| Mesure | Description |
|---|---|
| [!UICONTROL Taille de l’Audience Activation] | Taille totale des profils activés sur toute destination basée sur des fichiers au cours d’une année. Remarque : Cela n’inclut pas les profils envoyés par le biais de destinations de diffusion en continu. |
| [!UICONTROL Audience adressable] | Somme des droits de l’audience de votre entreprise et des droits de l’audience du consommateur. Une audience de consommateur est définie comme le nombre de profils de personne identifiés comme &quot;audience de consommateur&quot; sur la commande client. Une audience métier est définie comme le nombre de profils de personnes économiques identifiées comme le &quot;public professionnel&quot; dans la commande client. |
| [!UICONTROL Packs d’utilisateurs d’Adhoc Query Service] | Module complémentaire permettant d’augmenter les droits des utilisateurs de Query Service simultanés autorisés de cinq autres utilisateurs simultanés de Query Service et d’une requête ad hoc supplémentaire en cours d’exécution par pack. Plusieurs packs d’utilisateur de requête ad hoc supplémentaires peuvent être sous licence. |
| [!UICONTROL Richesse moyenne du profil] | La somme de toutes les données de production stockées dans le service de profil Hub à un moment donné, divisée par cinq fois le nombre de profils de personnes commerciales autorisés. [!UICONTROL Richesse moyenne du profil] est une fonctionnalité partagée. |
| [!UICONTROL Lignes CJA disponibles] | Lignes de données quotidiennes moyennes disponibles pour l’analyse dans Customer Journey Analytics. |
| [!UICONTROL Attributs calculés] | Comptage total des données comportementales de profil agrégées. Les données comportementales de profil agrégées sont basées sur des événements d’expérience convertis en attribut de profil et pouvant être inclus dans un profil de personne ou de personne professionnelle. |
| [!UICONTROL Audience des consommateurs] | Le nombre de profils de personne identifiés comme &quot;Audience client&quot; sur la commande client. |
| [!UICONTROL Taille de l’exportation des données] | La quantité de données envoyée par le biais des activations de jeux de données au cours d’une année. |
| [!UICONTROL Exports de données] | Taille totale des jeux de données pouvant être exportés vers une solution autre qu’un Adobe (directement ou indirectement) au cours d’une année. |
| [!UICONTROL Stockage du lac de données] | Quantité utilisée par l’entrepôt de données analytiques dans Adobe Experience Platform. |
| [!UICONTROL Audience pouvant être activée] | Cette mesure fait référence à l’audience des profils engageants. Un profil engageable est un enregistrement d’informations représentant une personne et est représenté dans le service de profil. Ces enregistrements sont des profils avec lesquels vous avez tenté d’interagir à l’aide des fonctionnalités de création, de prise de décision, de diffusion, d’expérimentation ou d’orchestration de Journey Optimizer au cours des 12 derniers mois. |
| [!UICONTROL Audiences analogue] | Nombre d’audiences générées par la modélisation d’une audience de consommateur existante afin d’identifier les profils de personne similaires à cette audience de consommateur existante. |
| [!UICONTROL Nombre de modèles AMM] | Nombre du modèle d’apprentissage automatique (intégré à l’Adobe Mix Modeler) utilisé pour mesurer et/ou prédire un résultat spécifié en fonction de vos investissements. |
| [!UICONTROL Nombre d’environnements de test] | Nombre de séparations logiques au sein de votre instance de tout service On-Demand Adobe accédant à Adobe Experience Platform pour isoler les données et les opérations. |
| [!UICONTROL Richesse du profil : nombre de packs] | Augmentation de la richesse moyenne autorisée du profil de 25 Ko par profil pour chaque pack de richesse de profil supplémentaire. |
| [!UICONTROL Heures de calcul de Query Service] | Mesure du temps pris par les moteurs Query Service pour lire, traiter et écrire des données dans le lac de données lors de l’exécution d’une requête par lots. |
| [!UICONTROL Segmentation par flux : nombre de packs] | Les packs mettent à jour l’adhésion au segment pour un profil de personne lorsque de nouvelles données entrent dans le service de segmentation par le biais d’un flux continu. L’appartenance au segment est évaluée en fonction des attributs de profil de la personne actuelle et de la valeur de l’événement actuel, sans prendre en compte le comportement historique. La segmentation par flux est une fonctionnalité partagée. |

<!-- |  [!UICONTROL Sandbox No of Packs] |  A logical separation within your instance of any Adobe On-demand Service that accesses Adobe Experience Platform isolating data and operations | -->

>[!TIP]
>
>Vous pouvez vérifier vos droits de licence dans votre commande de ventes pour calculer des mesures telles que votre &quot;Autorisation de stockage&quot;.<br>Par exemple,<ul><li>Allocation de stockage = nombre de &quot;profils autorisés&quot; dans votre contrat X Richesse moyenne du profil</li></ul>

La disponibilité de ces mesures et la définition spécifique de chacune d’elles varient en fonction des licences achetées par votre entreprise. Pour obtenir des définitions détaillées de chaque mesure, reportez-vous à la documentation Description du produit appropriée :

| Licence | Description du produit |
|---|---|
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD LITE</li><li>ADOBE EXPERIENCE PLATFORM:OD STANDARD</li><li>ADOBE EXPERIENCE PLATFORM:OD HEAVY</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD</li></ul> | [Experience Platform, App Services et Intelligent Services](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT CUSTOMOMENT DATA PLATFORM:OD</li><li>RT CUSTOMER DATA PLATFORM:OD PRFL À 10M</li><li>RT CUSTOMER DATA PLATFORM:OD PRFL À 50M</li></ul> | [Adobe Real-Time Customer Data Platform](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>ACTIVATION AEP:OD</li><li>AEP:OD ACTIVATION PRFL À 10M</li><li>AEP:PRFL D’ACTIVATION OD JUSQU’À 50 M</li></ul> | [Adobe Experience Platform Activation](https://helpx.adobe.com/fr/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:INTELLIGENCE OD</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>JOURNEY OPTIMIZER SELECT:OD</li><li>JOURNEY OPTIMIZER PRIME : OD</li><li>JOURNEY OPTIMIZER ULTIMATE:OD</li><li>UNP AJO PRIME STARTER:OD</li><li>UNP AJO ULTIMATE STARTER:OD</li><li>UNP REAL-TIME CDP : ORCHESTRATION DU PROFIL OD</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/fr/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>Le tableau de bord de l’utilisation des licences ne tient compte que de la dernière licence configurée pour votre entreprise. Si la dernière licence configurée pour votre entreprise n’apparaît pas dans le tableau ci-dessus, le tableau de bord de l’utilisation des licences peut ne pas s’afficher correctement. La prise en charge de licences supplémentaires et de plusieurs licences au sein d’une même organisation est prévue pour une version ultérieure.

## Étapes suivantes

Après avoir lu ce document, vous pouvez localiser le tableau de bord d’utilisation des licences et afficher les mesures d’utilisation de chaque produit acheté, pour tous les environnements de test de production ou de développement, ainsi que pour un environnement de test spécifique. Vous trouverez plus d’informations sur les mesures disponibles pour votre entreprise, en fonction des licences achetées par celle-ci.

Pour en savoir plus sur les autres fonctionnalités disponibles dans l’interface utilisateur de l’Experience Platform, consultez le [guide de l’interface utilisateur de Platform](../../landing/ui-guide.md).
