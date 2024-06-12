---
title: Tableau de bord des profils de compte
description: Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur les profils de compte B2B de votre entreprise.
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 8e05b0ae06250f8cd55b361a8176963e0dce8e92
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 4%

---

# [!UICONTROL Profils de compte] tableau de bord

L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur vos profils de compte, telles qu’elles sont capturées lors d’un instantané quotidien. Ce guide explique comment accéder à et utiliser le [!UICONTROL Profils de compte] tableau de bord dans l’interface utilisateur et fournit des informations supplémentaires sur les visualisations affichées dans le tableau de bord.

Ce document présente les fonctionnalités de la fonction [!UICONTROL Profils de compte] tableau de bord et détaille les informations standard disponibles. Voir [[!UICONTROL Profils de compte] Guide de l’interface utilisateur](../../rtcdp/accounts/account-profile-ui-guide.md) pour en savoir plus sur les fonctionnalités disponibles.

## Commencer

Vous devez avoir le droit de [Adobe Real-time Customer Data Platform version B2B](../../rtcdp/b2b-overview.md) pour accéder à B2B [!UICONTROL Profils de compte] tableau de bord.

## Données des profils de compte {#data}

La variable [!UICONTROL Profils de compte] le tableau de bord affiche un instantané des informations de votre compte unifié. Ces informations de compte proviennent de plusieurs sources sur vos canaux marketing et des différents systèmes actuellement utilisés par votre entreprise pour stocker les informations de compte client.

Les données de profil de l’instantané affichent les données exactement telles qu’elles apparaissent au moment précis où l’instantané a été pris. En d’autres termes, l’instantané n’est pas une approximation ou un échantillon des données, et la variable [!UICONTROL Profils de compte] le tableau de bord n’est pas mis à jour en temps réel.

>[!NOTE]
>
>Les modifications ou mises à jour apportées aux données depuis la prise dʼun instantané ne seront pas reflétées dans le tableau de bord avant la prise de lʼinstantané suivant.

## Explorez les [!UICONTROL Profils de compte] tableau de bord {#explore}

Pour accéder au [!UICONTROL Profils de compte] Tableau de bord dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Profils]** under [!UICONTROL Comptes] dans le panneau de navigation de gauche.

![L’interface utilisateur de Platform avec les profils de compte dans le volet de navigation de gauche est mise en surbrillance et l’onglet de présentation s’affiche.](../images/account-profiles/account-profiles-dashboard.png)

Dans la [!UICONTROL Profils de compte] tableau de bord, vous pouvez : [parcourir les profils de compte ingérés dans votre organisation ;](#browse-account-profiles), ou [afficher l’intégralité des données de profil de compte en un coup d’oeil à l’aide de widgets ;](#standard-widgets).

### Filtre de date {#date-filter}

La variable [!UICONTROL Présentation] Cet onglet est composé de widgets qui fournissent des mesures en lecture seule pour transmettre des informations importantes sur vos profils de compte. Sélectionnez l’icône ou les dates du calendrier pour modifier le filtre de date global de vos widgets.

>[!IMPORTANT]
>
>La période que vous sélectionnez dans le calendrier déroulant affecte toutes les informations, à l’exception des deux widgets de notation prédictive ([distribution](#predictive-scoring-distribution) et [principaux facteurs d’influence](#predictive-scoring-top-influential-factors)).

![Onglet Aperçu des profils de compte avec le sélecteur de date et l’icône de filtre mise en surbrillance.](../images/account-profiles/date-filter.png)

### Configuration du service de correspondance de comptes {#lead-to-account-matching-service}

Sélectionner **[!UICONTROL Paramètres]** pour configurer le prospect vers le service de correspondance de comptes à partir de la variable [!UICONTROL Paramètres du compte] boîte de dialogue. Pour plus d’informations sur la configuration de l’association de pistes aux comptes, voir la section [Guide de l’interface utilisateur](../../rtcdp/accounts/account-profile-ui-guide.md#configure-lead-to-account-matching). Pour en savoir plus sur la mise en correspondance des prospects avec les comptes, consultez la section [mener à la correspondance des comptes dans la documentation Real-Time CDP B2B ;](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

![Le tableau de bord Profils de compte avec les paramètres en surbrillance.](../images/account-profiles/settings.png)

## Parcourir les profils de compte {#browse-account-profiles}

Dans la [!UICONTROL Parcourir] vous pouvez rechercher et afficher les profils de compte en lecture seule ingérés dans votre organisation. Utilisez un ID de compte provenant d’une source d’entreprise connectée ou saisissez directement les informations sources. Dans cet espace de travail, vous pouvez voir des informations importantes appartenant au profil de compte, notamment leur nom, leur secteur d’activité, leurs recettes et leur audience.

Sélectionnez la variable [!UICONTROL Identifiant de profil] dans les résultats affichés sur la page [!UICONTROL Parcourir] pour ouvrir la [!UICONTROL Détails] pour le profil du compte.

![L’onglet de navigation Profils de compte avec les résultats affichés et l’identifiant de profil mis en surbrillance.](../images/account-profiles/account-profiles-browse-tab.png)

Les informations de profil du compte affichées sur la page [!UICONTROL Détails] a été fusionné à partir de plusieurs fragments de profil pour former une vue unique du compte individuel. Consultez la documentation relative à [navigation dans les profils de compte dans Adobe Real-time Customer Data Platform](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) pour en savoir plus sur les fonctionnalités d’affichage des profils de compte dans l’interface utilisateur de Platform.

## Widgets standard {#standard-widgets}

Adobe fournit des widgets standard que vous pouvez utiliser pour visualiser différentes mesures liées à vos profils de compte.

>[!IMPORTANT]
>
>Si vous ne fournissez pas de filtre de date, le comportement par défaut des insights analyse les données ajoutées de l’année précédente à aujourd’hui.

Pour en savoir plus sur chacun des widgets standards disponibles, sélectionnez le nom d’un widget dans la liste suivante :

* [Profils de compte ajoutés](#account-profiles-added)
* [Nouveaux comptes par secteur](#accounts-by-industry)
* [Nouveaux comptes par type](#accounts-by-type)
* [Nouvelles opportunités par rôle individuel](#opportunities-by-person-role)
* [Nouvelles opportunités par recettes](#opportunities-by-revenue)
* [Nouvelles opportunités par statut et étape](#opportunities-by-status-&-stage)
* [De nouvelles opportunités gagnées](#opportunities-won)
* [Opportunités ajoutées](#opportunities-added)
* [Répartition du score prédictif](#predictive-scoring-distribution)
* [Facteurs les plus influents du score prédictif](#predictive-scoring-top-influential-factors)

### Profils de compte ajoutés {#account-profiles-added}

La variable [!UICONTROL Profils de compte ajoutés] le widget utilise un graphique linéaire pour afficher le nombre de profils de compte ajoutés chaque jour sur une période donnée. Utilisez le filtre de date globale situé en haut de votre tableau de bord pour déterminer la période d’analyse. Si aucun filtre de date n’est fourni, le comportement par défaut répertorie les profils de compte ajoutés pour l’année précédente. Les résultats peuvent être utilisés pour déduire une tendance du nombre de profils de compte ajoutés.

![Le widget Profils de compte ajouté.](../images/account-profiles/account-profiles-added.png)

### Nouveaux comptes par secteur {#accounts-by-industry}

La variable [!UICONTROL Nouveaux comptes par secteur] widget affiche le nombre total de comptes dans une mesure unique au sein d’un graphique en anneau. Le graphique en anneau illustre la composition relative des différentes industries qui composent ce total. Une clé codée par couleur permet de ventiler toutes les industries incluses. Les décomptes individuels de chaque secteur sont affichés dans une boîte de dialogue lorsque le curseur survole la section correspondante du graphique en anneau.

![Le widget Nouveaux comptes par secteur.](../images/account-profiles/new-accounts-by-industry.png)

### Nouveaux comptes par type {#accounts-by-type}

La variable [!UICONTROL Nouveaux comptes par type] widget affiche le nombre total de comptes dans une mesure unique au sein d’un graphique en anneau. Le graphique en anneau illustre la composition relative des différents types de compte qui composent ce total. Une clé codée par couleur fournit une ventilation de tous les types de compte inclus. Les comptes individuels de chaque type de compte s’affichent dans une boîte de dialogue lorsque le curseur survole la section correspondante du graphique en anneau.

![Le widget Nouveaux comptes par type .](../images/account-profiles/new-accounts-by-type.png)

### Nouvelles opportunités par rôle individuel {#opportunities-by-person-role}

La variable [!UICONTROL Nouvelles opportunités par rôle individuel] widget affiche le nombre total de vos opportunités dans une mesure unique au sein d’un graphique en anneau. Le graphique en anneau illustre la composition relative des rôles qui constituent ce nombre total d’opportunités. Une clé codée par couleur fournit une ventilation de tous les rôles inclus. Les décomptes individuels de chaque rôle s’affichent dans une boîte de dialogue lorsque le curseur survole la section correspondante du graphique en anneau.

>[!NOTE]
>
>La variable [!UICONTROL Aucune donnée trouvée] ou [!UICONTROL Impossible de charger] L’erreur est provoquée lorsque la table-pont &#39;Opportunity-Person&#39; n’est pas utilisée dans votre schéma. Si votre insight affiche l’une de ces erreurs, vérifiez votre schéma d’union et assurez-vous que le groupe de champs &#39;Opportunity-Person&#39; ingère des données.

![Le widget Nouvelles opportunités par rôle de personne .](../images/account-profiles/new-opportunities-by-person-role.png)

### Nouvelles opportunités par recettes {#opportunities-by-revenue}

La variable [!UICONTROL Nouvelles opportunités par recettes] widget utilise un graphique à barres pour illustrer le montant total estimé des recettes générées par vos opportunités. Le widget prend en charge jusqu’à six opportunités.

Pour afficher une boîte de dialogue contenant le total des recettes spécifiques d’une opportunité, placez le curseur sur des barres individuelles.

![Le widget Nouvelles opportunités par chiffre d’affaires .](../images/account-profiles/new-opportunities-by-revenue.png)

### Nouvelles opportunités par statut et étape {#opportunities-by-status-&-stage}

Ce widget utilise un graphique à barres pour illustrer le nombre d’opportunités ouvertes ou fermées à toutes les étapes de l’entonnoir marketing/vente. Le widget utilise des couleurs pour différencier l’étape des opportunités. Une clé codée par couleur indique les étapes disponibles pour les opportunités.

![Le widget Nouvelles opportunités par statut et étape .](../images/account-profiles/new-opportunities-by-status-&-stage.png)

### De nouvelles opportunités gagnées {#opportunities-won}

La variable [!UICONTROL De nouvelles opportunités gagnées] widget affiche le nombre total d’opportunités qui ont été finalisées avec succès dans une seule mesure dans un graphique en anneau. Le graphique en anneau illustre la composition relative des opportunités gagnées ou non. Une clé codée en couleur fait la distinction entre les opportunités gagnées et non gagnées. Les décomptes individuels de chaque rôle s’affichent dans une boîte de dialogue lorsque le curseur survole la section correspondante du graphique en anneau.

![Le widget Nouvelles opportunités a gagné.](../images/account-profiles/new-opportunities-won.png)

### Opportunités ajoutées {#opportunities-added}

La variable [!UICONTROL Opportunités ajoutées] le widget utilise un graphique linéaire pour afficher le nombre d’opportunités ajoutées chaque jour sur une période donnée. Utilisez le filtre de date globale situé en haut de votre tableau de bord pour déterminer la période d’analyse. Si aucun filtre de date n’est fourni, le comportement par défaut répertorie les opportunités ajoutées pour l’année précédente. Les résultats peuvent être utilisés pour déduire une tendance du nombre d’opportunités ajoutées.

<!-- Link to date filter documentation from Annamalai -->

![Le widget Opportunités ajoutées .](../images/account-profiles/opportunities-added.png)

### Répartition du score prédictif {#predictive-scoring-distribution}

La variable [!UICONTROL Distribution de notation prédictive] widget affiche la distribution des scores de tous les profils de compte pour vous aider à comprendre en un coup d’oeil l’état de votre pipeline de ventes. Les données de notation sont véhiculées par le biais d’un graphique en anneau et d’un graphique en colonnes.

Le graphique en anneau illustre la proportion de vos profils de compte totaux dans chacune des classes à forte, moyenne et faible propension à acheter. La clé fournit plus de détails sur les sections codées par couleur, y compris les plages de compartiment de notation et le nombre de profils de compte dans cette plage.

Le graphique en colonnes fournit une ventilation de notation plus granulaire. Chaque colonne indique le nombre de profils de compte dans chacun des 20 intervalles de cinq points.

Le menu déroulant du widget vous permet de sélectionner le modèle de notation du compte.

>[!NOTE]
>
>Les filtres de période globaux ne s’appliquent pas aux insights de notation prédictive. Les widgets de notation prédictive analysent les données en fonction du modèle de notation de compte sélectionné dans la liste déroulante.

![Le widget de distribution de notation prédictive.](../images/account-profiles/predictive-scoring-distribution.png)

### Facteurs les plus influents du score prédictif {#predictive-scoring-top-influential-factors}

La variable [!UICONTROL Facteurs d’influence de la notation prédictive] vous aide à comprendre les facteurs les plus significatifs qui génèrent les scores pour chaque compartiment de propension.

Ce widget présente les principaux facteurs d’influence pour chacun des compartiments de propension élevée, moyenne et faible. Une barre pour chaque facteur d’influence indique le pourcentage des profils de compte dans ce compartiment de propension qui contient le facteur d’influence spécifique.

Le menu déroulant du widget vous permet de sélectionner le modèle de notation du compte.

>[!NOTE]
>
>Les filtres de période globaux ne s’appliquent pas aux insights de notation prédictive. Les widgets de notation prédictive analysent les données en fonction du modèle de notation de compte sélectionné dans la liste déroulante.

![Le widget Score prédictif des principaux facteurs d’influence .](../images/account-profiles/predictive-scoring-top-influential-factors.png)

### Erreur de chargement des données impossible {#errors}

Si un widget s’affiche *[!UICONTROL Chargement impossible. Essaie à nouveau.]* car il n’existe aucune donnée disponible pour l’entité B2B. Par exemple, le widget affiché ci-dessous [!UICONTROL Nouvelles opportunités par rôle individuel], affiche le message &quot;[!UICONTROL Chargement impossible. Essaie à nouveau.]&quot;, car cet environnement de test ne dispose pas de données d’opportunité disponibles.

![L’erreur Impossible de charger l’insight.](../images/account-profiles/unable-to-load.png)

Pour résoudre ce problème, vous devez ingérer des données d’entité B2B, telles que *personne en opportunité* données, dans l’environnement de test. Au bout de 48 heures, les données sont répercutées dans les widgets.

## Étapes suivantes

En suivant ce document, vous devez maintenant savoir comment localiser la variable [!UICONTROL Profils de compte] tableau de bord et comprendre également les mesures affichées dans les widgets disponibles. Pour en savoir plus sur l’utilisation des profils de compte dans le cadre de vos données B2B dans l’interface utilisateur Experience Platform, reportez-vous à la section [présentation des profils de compte](../../rtcdp/accounts/account-profile-overview.md) pour Adobe Real-Time CDP, édition B2B.
