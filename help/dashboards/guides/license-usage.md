---
keywords: Experience Platform;interface utilisateur;interface utilisateur;personnalisation;tableau de bord d’utilisation de la licence;tableau de bord;utilisation des licences;droits;consommation
title: Tableau de bord d’utilisation de la licence
description: Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur l’utilisation des licences de votre entreprise.
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: 1c31ef58eec727638cab28202afc762da0e226a2
workflow-type: tm+mt
source-wordcount: '3125'
ht-degree: 25%

---

# Tableau de bord d’utilisation des licences {#license-usage-dashboard}

>[!CONTEXTUALHELP]
>id="testy-mctestface"
>title="Boîte de dialogue de test qui ne doit pas être visible"
>abstract="L’objet {name} est affiché le {date}."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_core"
>title="Table des produits principaux"
>abstract="Les produits principaux répertoriés dans le tableau comportent leurs propres mesures, le suivi de l’utilisation et des vues détaillées au niveau du sandbox. Ces produits principaux fournissent les mesures clés pour le suivi et les modules complémentaires sont inclus dans ces mesures."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_addons"
>title="Tableau des modules complémentaires"
>abstract="Le tableau des modules complémentaires répertorie les produits dont le montant des licences est combiné aux mesures prises en charge par les produits principaux. Ces modules complémentaires ne comportent pas de mesures distinctes, mais améliorent le suivi de l’utilisation des produits principaux auxquels ils sont associés."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage"
>title="Tableau de bord d’utilisation des licences"
>abstract="Le tableau de bord d’utilisation des licences donne des informations sur les produits Adobe Experience Platform que vous avez achetés. La vue d’ensemble du tableau de bord affiche les mesures principales pour vos produits, notamment votre utilisation pour chacune d’entre elles et la quantité de licences contractées. L’espace de travail des détails affiche une répartition de vos mesures pour chaque produit dans des sandbox spécifiques."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html?lang=fr" text="Expirations automatisées des jeux de données"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Expiration des données de profils pseudonymes"

>[!CONTEXTUALHELP]
>id="platform_licenseusage"
>title="Tableau de bord d’utilisation des licences"
>abstract="Le tableau de bord d’utilisation des licences donne des informations sur les produits Adobe Experience Platform que vous avez achetés. La vue d’ensemble du tableau de bord affiche les mesures principales pour vos produits, notamment votre utilisation pour chacune d’entre elles et la quantité de licences contractées. L’espace de travail des détails affiche une répartition de vos mesures pour chaque produit dans des sandbox spécifiques."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html?lang=fr" text="Expirations automatisées des jeux de données"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Expiration des données de profils pseudonymes"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_computehours"
>title="Heures de calcul prévues"
>abstract="Votre utilisation est susceptible d’atteindre la quantité autorisée sous licence. Pour évaluer ou réduire vos heures de calcul, accédez à Requêtes > Journal pour consulter l’historique de vos requêtes. Si vous n’avez pas l’autorisation d’accéder à l’espace de travail Requêtes, contactez votre administrateur ou administratrice."
>additional-url="https://experience.adobe.com/#/platform/query/log.html" text="Espace de travail Journal des requêtes"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_addressableaudience"
>title="Audience adressable prévue"
>abstract="Votre utilisation est susceptible d’atteindre la quantité autorisée sous licence. Pour réduire l’utilisation, vous pouvez configurer les expirations des données des jeux de données ou des profils pseudonymes pour les sandbox et les jeux de données."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=fr" text="Expirations des événements d’expérience"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Expiration des données de profils pseudonymes"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_engageableprofiles"
>title="Profils Engageables Prévus"
>abstract="Votre utilisation est susceptible d’atteindre la quantité autorisée sous licence. Pour réduire l’utilisation, vous pouvez configurer les expirations des données des jeux de données ou des profils pseudonymes pour les sandbox et les jeux de données."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=fr" text="Expirations des événements d’expérience"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Expiration des données de profils pseudonymes"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_businesspersonprofile"
>title="Profil professionnel prévu"
>abstract="Votre utilisation est susceptible d’atteindre la quantité autorisée sous licence. Pour réduire l’utilisation, vous pouvez configurer les expirations des données des jeux de données ou des profils pseudonymes pour les sandbox et les jeux de données."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=fr" text="Expirations des événements d’expérience"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Expiration des données de profils pseudonymes"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_corehours"
>title="Heures de base prévues"
>abstract="Votre utilisation est susceptible d’atteindre la quantité autorisée sous licence. Pour réduire l’utilisation, vous pouvez configurer les expirations des données des jeux de données ou des profils pseudonymes pour les sandbox et les jeux de données."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=fr" text="Expirations des événements d’expérience"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Expiration des données de profils pseudonymes"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_totaldatavolume"
>title="Volume total de données prévu"
>abstract="Votre utilisation est susceptible d’atteindre la quantité autorisée sous licence. Pour réduire l’utilisation, vous pouvez configurer les expirations des données des jeux de données ou des profils pseudonymes pour les sandbox et les jeux de données."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=fr" text="Expirations des événements d’expérience"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Expiration des données de profils pseudonymes"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_cjaRowsAvailable"
>title="Lignes CJA Prédites Disponibles"
>abstract="Votre utilisation est susceptible d’atteindre la quantité autorisée sous licence. Pour réduire l’utilisation, vous pouvez configurer les expirations des données des jeux de données ou des profils pseudonymes pour les sandbox et les jeux de données."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=fr" text="Expirations des événements d’expérience"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Expiration des données de profils pseudonymes"

Vous pouvez afficher des informations importantes sur l’utilisation des licences de votre entreprise via le tableau de bord Adobe Experience Platform [!UICONTROL Utilisation des licences]. Les informations affichées ici sont capturées lors d’un instantané quotidien de votre instance Platform.

Les rapports d’utilisation de licence offrent un haut degré de granularité sur les mesures d’utilisation de licence. Le tableau de bord fournit des mesures d’utilisation pour chaque produit acheté (et les modules complémentaires associés), l’utilisation consolidée des mesures dans tous les sandbox de production ou de développement et la mesure d’utilisation d’un sandbox spécifique. Les applications Experience Platform suivantes peuvent être suivies avec des mesures d’utilisation : Real-Time Customer Data Platform, Adobe Journey Optimizer et Customer Journey Analytics.

Ce guide explique comment accéder au tableau de bord d’utilisation des licences et l’utiliser dans l’interface utilisateur. Il fournit également des informations supplémentaires sur les visualisations affichées dans le tableau de bord.

Pour une présentation générale de l’interface utilisateur de Platform, consultez le [guide de l’interface utilisateur d’Experience Platform](../../landing/ui-guide.md).

## [!UICONTROL Utilisation des licences] données du tableau de bord

Le tableau de bord [!UICONTROL  Utilisation des licences ] affiche la liste de tous les produits Experience Platform que vous avez achetés et de tous les modules complémentaires associés. Depuis ce tableau de bord, vous pouvez obtenir un instantané des données liées aux licences de l’entreprise pour Experience Platform dans n’importe quel sandbox associé.

Les données de ce tableau de bord s’affichent exactement comme elles apparaissent au moment précis où l’instantané a été pris. En d’autres termes, l’instantané n’est pas une approximation ou un échantillon des données, et le tableau de bord n’est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis la prise dʼun instantané ne seront pas reflétées dans le tableau de bord avant la prise de lʼinstantané suivant.

## Exploration du tableau de bord d’utilisation des licences {#explore}

Pour accéder au tableau de bord d’utilisation de la licence dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Utilisation de la licence]** dans le rail de gauche. L’onglet [!UICONTROL Aperçu] s’ouvre et affiche une liste des produits disponibles.

>[!NOTE]
>
>Le tableau de bord d’utilisation de la licence n’est pas activé par défaut. Les utilisateurs doivent disposer de l’autorisation « Afficher le tableau de bord d’utilisation des licences » pour pouvoir consulter le tableau de bord. Pour obtenir des instructions sur l’octroi des autorisations d’accès pour l’affichage du tableau de bord d’utilisation des licences, consultez le guide [autorisations des tableaux de bord](../permissions.md).

![Onglet Aperçu du tableau de bord d’utilisation des licences, avec l’utilisation des licences mise en surbrillance dans la barre latérale de navigation gauche.](../images/license-usage/dashboard-overview.png)

## Onglet [!UICONTROL Aperçu] {#overview-tab}

Le tableau de bord [!UICONTROL  Utilisation des licences ] affiche deux tableaux distincts : **Produits principaux** et **Modules complémentaires**.

- **[!UICONTROL Tableau des produits principaux]** : ce tableau répertorie les principaux produits Adobe Experience Platform sous licence par votre entreprise. Chaque produit principal possède ses propres mesures, suivi de l’utilisation et vues d’exploration au niveau du sandbox. Ces produits principaux fournissent les mesures clés pour le suivi et les modules complémentaires sont inclus dans ces mesures.

- **[!UICONTROL Tableau des modules complémentaires]** : ce tableau répertorie les produits supplémentaires dont le montant des licences est combiné aux mesures prises en charge par les produits principaux. Les modules complémentaires n’ont pas de mesures distinctes, mais améliorent le suivi de l’utilisation des produits principaux auxquels ils sont associés.

| Nom de la colonne | Description |
|---|---|
| **[!UICONTROL Produit]** | La solution Adobe sous licence de votre entreprise. |
| **[!UICONTROL Mesure De Principal]** | Mesure principale utilisée pour le suivi au sein de ce produit. |
| **[!UICONTROL Montant de la licence]** | Valeur convenue dans le contrat pour le montant maximal de la mesure de Principal, comme convenu dans votre contrat de licence de produit. |
| **[!UICONTROL Utilisation]** | Quantité de la mesure principale utilisée. Cette valeur fournit l’utilisation totale de cette mesure dans tous les sandbox, qu’il s’agisse de production ou de développement. |
| **[!UICONTROL Utilisation %]** | Pourcentage de la mesure principale utilisée en fonction du montant de votre licence. |
| **[!UICONTROL Utilisation de la prédiction]** | Pourcentage d’utilisation prévu de votre mesure principale en fonction du montant de votre licence. |

>[!NOTE]
>
>Le montant des licences pour les modules complémentaires est inclus dans le [!UICONTROL Montant de la licence] des produits principaux. Par exemple, si vous achetez un pack de cinq sandbox en tant que module complémentaire, le montant est ajouté à celui du produit de base. Le tableau des modules complémentaires affiche un [!UICONTROL Montant de la licence] spécifique au module complémentaire, mais l’utilisation réelle est suivie via le produit de base.

Les tableaux indiquent la mesure principale pour chaque produit, car chaque produit peut effectuer le suivi de nombreuses mesures.

### Utilisation prédite {#predicted-usage}

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage_prediction"
>title="Utilisation prédite"
>abstract="Les prédictions sont basées sur l’utilisation des 6 à 7 derniers mois et sont générées le 15 de chaque mois. Notez que les prédictions d’utilisation des licences sont des approximations basées sur l’utilisation passée. Il vous incombe de comprendre l’utilisation réelle de votre entreprise et de vous assurer que cette utilisation ne dépasse pas la portée de la licence obtenue par votre entreprise auprès d’Adobe. Pour réduire l’utilisation, vous pouvez configurer les expirations des données des jeux de données ou des profils pseudonymes pour les sandbox et les jeux de données."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html?lang=fr" text="Expirations automatisées des jeux de données"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Expiration des données de profils pseudonymes"

>[!CONTEXTUALHELP]
>id="platform_licenseusage_prediction"
>title="Utilisation prédite"
>abstract="Les prédictions sont basées sur l’utilisation des 6 à 7 derniers mois et sont générées le 15 de chaque mois. Notez que les prédictions d’utilisation des licences sont des approximations basées sur l’utilisation passée. Il vous incombe de comprendre l’utilisation réelle de votre entreprise et de vous assurer que cette utilisation ne dépasse pas la portée de la licence obtenue par votre entreprise auprès d’Adobe. Pour réduire l’utilisation, vous pouvez configurer les expirations des données des jeux de données ou des profils pseudonymes pour les sandbox et les jeux de données."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html?lang=fr" text="Expirations automatisées des jeux de données"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="Expiration des données de profils pseudonymes"

Gérez et optimisez vos ressources de licence de manière proactive en fonction de prévisions d’utilisation pertinentes. La colonne [!UICONTROL  Utilisation prévue ] prédit avec précision l’utilisation future des licences au niveau du sandbox, sur tous les sandbox de production et de développement, pour tous les produits que vous avez achetés. Cette fonctionnalité d’alerte fournit une prévision de l’utilisation des licences pour les six semaines à venir, en fonction de votre utilisation jusqu’au 15 de ce mois civil. Les prédictions sont fournies avec une limite inférieure et une limite supérieure.

>[!IMPORTANT]
>
>Les prévisions sont actualisées tous les mois. La date d’actualisation est incluse dans une icône d’informations (![Cette icône d’informations.](../images/license-usage/info-icon.png)) au-dessus du titre de la colonne.

Pour afficher un résumé de l’utilisation des droits d’un produit, sélectionnez un produit dans le tableau [!UICONTROL Produits principaux].

![[!UICONTROL  Utilisation de la licence] [!UICONTROL Présentation] avec un produit et la colonne Utilisation prévue mise en surbrillance.](../images/license-usage/product-predicted-usage.png)

L’onglet Résumé s’affiche. Vous pouvez utiliser les prédictions granulaires disponibles dans les onglets [!UICONTROL Résumé] et [!UICONTROL Détails] pour garantir une prise de décision éclairée afin d’utiliser efficacement la licence.

>[!NOTE]
>
>Notez que les prédictions d’utilisation des licences sont des approximations basées sur l’utilisation passée. Il vous incombe de comprendre l’utilisation réelle par votre organisation et de vous assurer que cette utilisation ne dépasse pas la portée de la licence de votre organisation avec Adobe.

![Vue récapitulative d’un produit Platform avec la colonne d’utilisation prévue mise en surbrillance.](../images/license-usage/summary-predicted-usage.png)

Le pourcentage d&#39;utilisation prévu est déterminé comme suit :

- Si les limites inférieure et supérieure sont sensiblement différentes, elles sont affichées sous la forme d’une plage (par exemple, 32 % à 35 %).
- Si les limites inférieure et supérieure sont presque identiques et non nulles, elles sont affichées sous forme de valeur approximative (par exemple, ~34 %).
- Si les limites inférieure et supérieure sont presque identiques et égales à zéro, elles s&#39;affichent exactement à 0 %.

>[!NOTE]
>
>« Presque identique » dans ce contexte signifie que les valeurs sont statistiquement significatives à deux décimales (par exemple, une limite inférieure de 0,342 et une limite supérieure de 0,344 sont toutes deux arrondies à 34 %).

La fonctionnalité d’utilisation prévue prend en charge les mesures suivantes :

- [!UICONTROL  Audience adressable ]
- [!UICONTROL Heures de calcul]
- [!UICONTROL Nombre de lignes de l’audience du Parcours client]
- [!UICONTROL Volume total de données]

## Onglet [!UICONTROL Résumé] {#summary-tab}

Pour afficher plus de mesures et d’informations détaillées sur l’utilisation de votre licence de produit, sélectionnez un nom de produit dans la liste. La vue [!UICONTROL Résumé] de ce produit s’affiche. Toutes les mesures disponibles s’affichent dans l’onglet [!UICONTROL Résumé]. Les mesures disponibles dépendent du produit sous licence. Cette vue fournit **une vue consolidée de toutes les mesures dans tous les sandbox de production ou de développement**. Le même niveau d’analyse est fourni pour les sandbox de production et de développement.

![Vue récapitulative d’un produit Platform qui affiche toutes les mesures disponibles pour ce produit.](../images/license-usage/summary-tab.png)

Dans l’onglet Résumé , le tableau comprend la colonne [!UICONTROL Mesure]. Ces descriptions lisibles par l’utilisateur indiquent toutes les mesures utilisées pour ce type de sandbox.

### Sélectionner un sandbox {#select-sandbox}

Pour changer l’affichage entre les types de sandbox de production et de développement, sélectionnez [!UICONTROL sandbox de production] ou [!UICONTROL sandbox de développement]. Le type de sandbox sélectionné est indiqué par le bouton radio en regard du nom du sandbox.

Les rapports de consommation pour les sandbox sont cumulatifs pour tous les sandbox du même type. En d’autres termes, la sélection des options [!UICONTROL Production] ou [!UICONTROL Développement] fournit des rapports de consommation pour tous les sandbox de production ou de développement, respectivement.

![Vue récapitulative d’un produit Platform avec les sandbox de production et de développement mis en surbrillance.](../images/license-usage/summary-tab-sandboxes.png)

>[!WARNING]
>
>L’autorisation d’affichage du tableau de bord d’utilisation de la licence doit être spécifiée au niveau du sandbox. Ajoutez des autorisations à chaque sandbox individuel pour les afficher dans le tableau de bord. Cette limitation sera corrigée dans une version ultérieure. En attendant, la solution de contournement suivante est disponible :
>
>1. Création d’un profil de produit dans le Adobe Admin Console.
>2. Sous Autorisation dans la catégorie Sandbox , ajoutez tous les sandbox que vous souhaitez afficher dans le tableau de bord d’utilisation des licences.
>3. Dans la catégorie Autorisation du tableau de bord des utilisateurs , ajoutez l’autorisation « Afficher le tableau de bord d’utilisation des licences ».

## Onglet [!UICONTROL Détails] {#details-tab}

Pour afficher **une mesure d’utilisation particulière d’un sandbox spécifique**, accédez à l’onglet [!UICONTROL Détails]. L’onglet [!UICONTROL Détails] affiche tous les sandbox disponibles dans les sandbox de production ou de développement.

![Onglet Détails du tableau de bord Utilisation de la licence.](../images/license-usage/details-tab.png)

Dans cette vue, vous pouvez sélectionner ![Icône Inspecter .](/help/images/icons/inspect.png) en regard d’un nom de sandbox pour afficher la visualisation de cette mesure. Une boîte de dialogue s’ouvre avec une visualisation pour cette mesure.

### Visualisations {#visualizations}

Chaque widget de visualisation comprend les aspects suivants :

- Graphique linéaire suivant les modifications de la mesure au fil du temps
- Une clé pour le graphique linéaire
- Nom du sandbox
- Menu déroulant permettant d’ajuster la période du graphique linéaire

Les graphiques linéaires comparent les chiffres d’utilisation de votre organisation au total disponible avec la licence de votre organisation et fournissent un pourcentage de l’utilisation totale.

![Visualisation d’une mesure.](../images/license-usage/visualization.png)

La période de recherche en amont de l’analyse peut être ajustée à partir du menu déroulant. Valeur par défaut des 30 derniers jours

Pour sélectionner une période, vous pouvez utiliser le menu déroulant des périodes pour sélectionner la période à afficher dans le tableau de bord. Plusieurs options sont disponibles, y compris la valeur par défaut des 30 derniers jours.

![Boîte de dialogue de visualisation avec le menu déroulant de la période en surbrillance.](../images/license-usage/date-range.png)

Vous pouvez également sélectionner **[!UICONTROL Date personnalisée]** pour choisir la période affichée.

![Onglet Aperçu du tableau de bord d’utilisation des licences avec les options de période personnalisée en surbrillance.](../images/license-usage/custom-date-range.png)

## Mesures disponibles {#available-metrics}

>[!IMPORTANT]
>
>À compter du 20 août, les clients disposant de droits pour « [!UICONTROL Richesse moyenne du profil] » et « [!UICONTROL Stockage total] » ont plutôt vu « [!UICONTROL Volume total de données] » dans le tableau de bord d’utilisation des licences. Les droits des clients n’ont pas été modifiés, mais les mesures de suivi ont été simplifiées. Le [!UICONTROL  Volume total de données ] représente les données disponibles dans le service de profil Adobe Experience Platform pour les workflows d’engagement et de personnalisation. Cette mesure simplifiée a amélioré la gestion et la mesure de l’utilisation du service de profil. Les clients sont invités à contacter leur représentant Adobe pour plus d’informations sur cette modification.

Le tableau de bord d’utilisation des licences établit des rapports sur plusieurs mesures uniques qui s’appliquent à plusieurs produits dans l’organisation. Les mesures disponibles sont les suivantes :

| Mesure | Description |
|---|---|
| [!UICONTROL Taille D’Audience Activation] | La taille totale des profils activés vers une destination basée sur des fichiers au cours d’une année. Remarque : les profils envoyés par le biais de destinations de diffusion en streaming ne sont pas inclus. |
| [!UICONTROL Audience adressable] | La somme des droits de votre audience commerciale et des droits de l’audience client. Une audience de consommateurs est définie comme le nombre de profils de personnes identifiés comme une « audience de consommateurs » sur la commande client. Une audience commerciale est définie comme le nombre de profils professionnels identifiés comme « audience commerciale » sur la commande client. |
| [!UICONTROL Packs d’utilisateurs d’Adhoc Query Service] | Un module complémentaire pour augmenter vos droits d’utilisateurs Query Service simultanés autorisés de cinq utilisateurs Query Service simultanés supplémentaires et d’une requête ad hoc supplémentaire en cours d’exécution simultanée par pack. Plusieurs packs d’utilisateurs de requêtes ad hoc supplémentaires peuvent être sous licence. |
| [!UICONTROL Richesse moyenne du profil] | **Obsolète** - La somme de toutes les données de production stockées à tout moment dans le service de profil Hub, divisée par cinq fois le nombre de profils professionnels autorisés. [!UICONTROL richesse moyenne du profil] est une fonctionnalité partagée. |
| [!UICONTROL Lignes CJA Disponibles] | Lignes de données moyennes par jour disponibles pour analyse dans Customer Journey Analytics. |
| [!UICONTROL Attributs calculés] | Nombre total de données comportementales de profil agrégées. Les données comportementales de profil agrégées sont basées sur des événements d’expérience qui sont convertis en un attribut de profil et peuvent être inclus dans un profil de personne ou d’entrepreneur. |
| [!UICONTROL Audience des consommateurs] | Nombre de profils de personnes identifiés comme « Audience des consommateurs » sur la commande client. |
| [!UICONTROL Taille de l’exportation des données] | La quantité de données envoyées par le biais des activations de jeux de données au cours d’une année. |
| [!UICONTROL Exportations de données] | La taille totale des jeux de données qui peuvent être exportés vers une solution non Adobe (directement ou indirectement) au cours d’une année. |
| [!UICONTROL Data Lake Storage] | Quantité utilisée de la banque de données analytique dans Adobe Experience Platform. |
| [!UICONTROL Audience Modifiable] | Cette mesure fait référence à l’audience des profils engageables. Un profil engageable est un enregistrement d’informations représentant une personne et est représenté dans le service de profil. Ces enregistrements sont des profils avec lesquels vous avez tenté d’interagir à l’aide des fonctionnalités de création, de prise de décision, de diffusion, d’expérimentation ou d’orchestration de Journey Optimizer au cours des 12 derniers mois. |
| [!UICONTROL Audiences semblables] | Nombre d’audiences générées en modélisant une audience de consommateurs existante pour identifier des profils de personnes similaires à cette audience de consommateurs existante. |
| [!UICONTROL  Nombre de modèles AMM ] | Décompte du modèle de machine learning (intégré à Adobe Mix Modeler) utilisé pour mesurer et/ou prédire un résultat spécifié en fonction de vos investissements. |
| [!UICONTROL Nombre de sandbox] | Nombre de séparations logiques au sein de votre instance d’un service à la demande Adobe qui accède à Adobe Experience Platform pour isoler les données et les opérations. |
| [!UICONTROL Richesse du profil - Nombre de packs] | Augmentation du volume total de données autorisé de 25 Ko par profil pour chaque pack d’augmentation de la richesse du profil. |
| [!UICONTROL Heures de calcul de Query Service] | Mesure du temps pris par les moteurs de Query Service pour lire, traiter et écrire des données dans le lac de données lorsqu’une requête par lots est exécutée. |
| [!UICONTROL Nombre de packs de segmentation en flux continu] | Les packs mettent à jour l’appartenance à un segment pour un profil de personne au fur et à mesure que de nouvelles données entrent dans le service de segmentation par le biais d’un flux de diffusion en continu. L’appartenance à un segment est évaluée en fonction des attributs de profil de la personne actuelle et de la valeur de l’événement actuel, sans prendre en compte le comportement historique. La segmentation en flux continu est une fonctionnalité partagée. |
| [!UICONTROL Volume total de données] | Quantité totale de données disponibles que le service de profil Adobe Experience Platform peut utiliser dans les workflows d’engagement. Pour en savoir plus, consultez les [questions fréquentes sur le volume total de données](../../landing/license-usage-and-guardrails/total-data-volume.md). |

<!-- |  [!UICONTROL Sandbox No of Packs] |  A logical separation within your instance of any Adobe On-demand Service that accesses Adobe Experience Platform isolating data and operations | -->

>[!TIP]
>
>Vous pouvez vérifier vos droits de licence dans votre commande client pour calculer des mesures telles que votre « quota de stockage ».<br>Par exemple,<ul><li>Allocation de stockage = Nombre de « profils autorisés » dans votre contrat X Richesse moyenne du profil</li></ul>

La disponibilité de ces mesures et la définition spécifique de chacune d’elles varient en fonction des licences achetées par votre entreprise. Pour obtenir des définitions détaillées de chaque mesure, reportez-vous à la documentation de description du produit appropriée :

| Licence | Description du produit |
| --- | --- |
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD LITE</li><li>ADOBE EXPERIENCE PLATFORM:OD STANDARD</li><li>ADOBE EXPERIENCE PLATFORM:OD LOURD</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD</li></ul> | [Experience Platform, App Services et Intelligent Services](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT CUSTOMER DATA PLATFORM:OD</li><li>RT CUSTOMER DATA PLATFORM : OD PRFL À 10M</li><li>RT CUSTOMER DATA PLATFORM : OD PRFL JUSQU’À 50 MILLIONS</li></ul> | [Adobe Real-Time Customer Data Platform](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>ACTIVATION D’AEP:OD</li><li>AEP:OD ACTIVATION PRFL TO 10M</li><li>PRFL D’ACTIVATION AEP:OD JUSQU’À 50 MILLIONS</li></ul> | [Activation de Adobe Experience Platform](https://helpx.adobe.com/fr/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD INTELLIGENCE</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>JOURNEY OPTIMIZER SELECT:OD</li><li>JOURNEY OPTIMIZER PRIME:OD</li><li>JOURNEY OPTIMIZER ULTIMATE:OD</li><li>UNP AJO PRIME STARTER:OD</li><li>UNP AJO ULTIMATE STARTER:OD</li><li>REAL-TIME CDP UNP:OD PROFILE ORCHESTRATION</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/fr/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>Le tableau de bord d’utilisation de la licence ne répertorie que la dernière licence configurée pour votre organisation. Si la dernière licence configurée pour votre organisation n’apparaît pas dans le tableau ci-dessus, le tableau de bord d’utilisation de la licence risque de ne pas s’afficher correctement. La prise en charge de licences supplémentaires et de licences multiples dans une seule organisation est prévue pour une version ultérieure.

## Étapes suivantes

Après lecture de ce document, vous êtes en mesure de localiser le tableau de bord d’utilisation de la licence et d’afficher les mesures d’utilisation de chaque produit acheté, pour tous les sandbox de production ou de développement, ainsi que pour un sandbox spécifique. Vous trouverez plus d’informations sur les mesures disponibles pour votre organisation, en fonction des licences achetées par celle-ci.

Pour en savoir plus sur les autres fonctionnalités disponibles dans l’interface utilisateur d’Experience Platform, reportez-vous au [guide de l’interface utilisateur de Platform](../../landing/ui-guide.md).
