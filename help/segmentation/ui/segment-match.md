---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation;Segmentation;Correspondance de segment;correspondance de segment
solution: Experience Platform
title: Présentation de la correspondance de segment
topic-legacy: overview
description: La correspondance de segment est un service de partage de segments dans Adobe Experience Platform qui permet à deux utilisateurs ou plus de Platform d’échanger des données de segment de manière sécurisée, gérée et respectueuse de la confidentialité.
source-git-commit: ee59da6c075573af366403e1059b5318fb924d21
workflow-type: tm+mt
source-wordcount: '1982'
ht-degree: 6%

---


# (Version bêta) [!DNL Segment Match] - Aperçu

>[!IMPORTANT]
>
>[!DNL Segment Match] est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

Adobe Experience Platform Segment Match est un service de partage de segments qui permet à plusieurs utilisateurs de Platform d’échanger des données de segment de manière sécurisée, gérée et respectueuse de la confidentialité. [!DNL Segment Match] utilise des normes de confidentialité de Platform et des identifiants personnels tels que des emails hachés, des numéros de téléphone hachés et des identifiants d’appareil comme les IDFA et les GAID.

Avec [!DNL Segment Match] vous pouvez :

* Gérez le processus de chevauchement d’identités.
* Afficher les estimations de pré-partage.
* Appliquez des libellés d’utilisation des données pour contrôler si les données peuvent être partagées avec des partenaires.
* Maintenez la gestion du cycle de vie des audiences partagées après la publication d’un flux et continuez un échange dynamique de données grâce à la possibilité d’ajouter, de supprimer et d’annuler le partage.

[!DNL Segment Match] utilise un processus de chevauchement d’identités pour s’assurer que le partage de segments est effectué de manière sécurisée et axée sur la confidentialité. Une **identité superposée** est une identité qui a une correspondance dans votre segment et dans celui de votre partenaire sélectionné. Avant de partager un segment entre un expéditeur et un destinataire, le processus de chevauchement d’identités recherche un chevauchement des espaces de noms et des contrôles du consentement entre l’expéditeur et le destinataire. Les deux vérifications de chevauchement doivent réussir pour qu’un segment soit partagé.

Les sections suivantes apportent des informations supplémentaires sur [!DNL Segment Match], notamment des détails sur la configuration et son workflow de bout en bout.

## Configuration

Les sections suivantes décrivent comment configurer et configurer [!DNL Segment Match] :

### Configuration des données d’identité et des espaces de noms {#namespaces}

La première étape pour commencer à utiliser [!DNL Segment Match] consiste à vous assurer que vous ingérez des données par rapport aux espaces de noms d’identité pris en charge.

Les espaces de noms d’identité sont un composant de [Adobe Experience Platform Identity Service](../../identity-service/home.md). Chaque identité client contient un espace de noms associé qui indique le contexte de l’identité. Par exemple, un espace de noms peut distinguer une valeur &quot;name<span>@email.com&quot; comme adresse électronique ou &quot;443522&quot; comme identifiant CRM numérique.

Une identité complète est composée d’une valeur d’identifiant et d’un espace de noms. Lors de la mise en correspondance des données d’enregistrement entre des fragments de profil (par exemple, lorsque [!DNL Real-time Customer Profile] fusionne des données de profil), la valeur d’identité et l’espace de noms doivent correspondre.

Dans le contexte de [!DNL Segment Match], les espaces de noms sont utilisés dans le processus de chevauchement lors du partage de données.

La liste des espaces de noms pris en charge est la suivante :

| Espace de noms | Description |
| --------- | ----------- |
| Emails (SHA256, avec mise en minuscules) | Espace de noms pour l’adresse électronique préhachée. Les valeurs fournies dans cet espace de noms sont converties en minuscules avant le hachage avec SHA256. Les espaces de début et de fin doivent être supprimés avant qu’une adresse email ne soit normalisée. Ce paramètre ne peut pas être modifié rétroactivement. Pour plus d’informations, consultez le document suivant sur la [prise en charge du hachage SHA-256](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) . |
| Téléphone (SHA256_E.164) | Espace de noms qui représente les numéros de téléphone bruts qui doivent être hachés au format SHA256 et E.164. |
| ECID | Espace de noms représentant une valeur d’identifiant Experience Cloud (ECID). Cet espace de noms peut également être référencé par les alias suivants : &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Pour plus d’informations, consultez la [présentation de l’ECID](../../identity-service/ecid.md) . |
| IDFA Apple (ID pour les annonceurs) | Espace de noms qui représente l’Apple ID pour les annonceurs. Pour plus d’informations, consultez le document suivant sur les [annonces basées sur les intérêts](https://support.apple.com/fr-fr/HT202074). |
| Google Ad ID | Espace de noms qui représente un identifiant Google Advertising. Consultez le document suivant sur [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) pour plus d’informations. |

### Configuration du consentement

Vous devez fournir une configuration de consentement et définir sa valeur par défaut sur `opt-in` ou `opt-out` pour une vérification du consentement.

La vérification du consentement de l’inclusion et de l’exclusion détermine si vous pouvez utiliser avec le consentement pour partager les données utilisateur par défaut. Si la valeur par défaut de la configuration du consentement est `opt-in`, les données utilisateur peuvent être partagées, sauf si un utilisateur s’exclut explicitement. Si la valeur par défaut est `opt-out`, les données utilisateur ne peuvent pas être partagées, à moins qu’un utilisateur ne s’y inscrive explicitement.

La configuration du consentement par défaut pour [!DNL Segment Match] est définie sur `opt-out`. Pour appliquer un modèle d’inclusion à vos données, envoyez une demande par courrier électronique à votre gestionnaire de compte Adobe.

Pour plus d’informations sur l’attribut `share` utilisé pour définir la valeur de consentement du partage de données, consultez la documentation suivante sur le [groupe de champs de confidentialité et consentement](../../xdm/field-groups/profile/consents.md). Pour plus d’informations sur le groupe de champs spécifique utilisé pour recueillir le consentement des consommateurs pour la collecte et l’utilisation de données liées à la confidentialité, la personnalisation et les préférences marketing, voir l’ [exemple GitHub suivant ](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/consent/consent-preferences.schema.md) Consentement pour la confidentialité, la personnalisation et les préférences marketing.

### Configuration des libellés d’utilisation des données

La dernière condition préalable que vous devez établir est de configurer un nouveau libellé d’utilisation des données pour empêcher le partage des données. Grâce aux libellés d’utilisation des données, vous pouvez gérer les données qui peuvent être partagées via [!DNL Segment Match].

Les libellés d’utilisation des données vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. Les bonnes pratiques recommandent de libeller les données dès qu’elles sont ingérées dans Experience Platform, ou dès que les données sont disponibles pour une utilisation dans Platform.

[!DNL Segment Match] utilise l’étiquette C11, une étiquette de contrat spécifique à  [!DNL Segment Match] que vous pouvez ajouter manuellement à n’importe quel jeu de données ou attribut pour vous assurer qu’ils sont exclus du processus de  [!DNL Segment Match] partage avec les partenaires. Le libellé C11 indique les données qui ne doivent pas être utilisées dans les processus [!DNL Segment Match]. Une fois que vous avez déterminé les jeux de données et/ou les champs à exclure de [!DNL Segment Match] et ajouté l’étiquette C11 en conséquence, le libellé est automatiquement appliqué par le workflow [!DNL Segment Match]. [!DNL Segment Match] active automatiquement la stratégie  [!UICONTROL Restreindre le ] partage des données de base. Pour obtenir des instructions spécifiques sur la manière d’appliquer des libellés d’utilisation des données aux jeux de données, consultez le tutoriel sur la [gestion des libellés d’utilisation des données dans l’interface utilisateur](../../data-governance/labels/user-guide.md).

Pour obtenir la liste des libellés d’utilisation des données et leurs définitions, consultez le [glossaire des libellés d’utilisation des données](../../data-governance/labels/reference.md). Pour plus d’informations sur les stratégies d’utilisation des données, consultez la [présentation des stratégies d’utilisation des données](../../data-governance/policies/overview.md).

### Présentation des [!DNL Segment Match] autorisations

Deux autorisations sont associées à [!DNL Segment Match] :

| Autorisation | Description |
| --- | --- |
| Gestion des connexions du partage d’audience | Cette autorisation vous permet de terminer le processus de négociation des liens avec les partenaires, qui connecte deux organisations IMS pour activer les flux [!DNL Segment Match]. |
| Gestion des partages d’audience | Cette autorisation vous permet de créer, de modifier et de publier des flux (le module de données utilisé pour [!DNL Segment Match]) avec des partenaires principaux (partenaires qui ont été connectés par l’utilisateur administrateur avec un accès **[!UICONTROL Connexions de partage d’audience]**). |

Pour plus d’informations sur le contrôle d’accès et les autorisations, consultez la [présentation du contrôle d’accès](../../access-control/home.md) .

## [!DNL Segment Match] workflow de bout en bout

Une fois que vous avez configuré vos données d’identité et espaces de noms, la configuration du consentement et le libellé d’utilisation des données, vous pouvez commencer à utiliser [!DNL Segment Match] et ses fonctionnalités.

### Gérer le partenaire

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Segments]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Flux]** dans l’en-tête supérieur.

![segments-feed.png](../images/ui/segment-match/segments-feed.png)

La page [!UICONTROL Flux] contient une liste de flux reçus de partenaires ainsi que des flux que vous avez partagés. Pour afficher la liste des partenaires existants ou établir une connexion avec un nouveau partenaire, sélectionnez **[!UICONTROL Gérer les partenaires]**.

![manage-Partners.png](../images/ui/segment-match/manage-partners.png)

Une connexion entre deux partenaires est une &quot;liaison bidirectionnelle&quot; qui agit comme une méthode en libre-service permettant aux utilisateurs de connecter leurs organisations Platform ensemble à un niveau sandbox. La connexion est nécessaire pour informer Platform qu’un accord a été établi et que Platform peut faciliter le partage de services entre vous et vos partenaires.

>[!NOTE]
>
>La &quot;poignée de main bidirectionnelle&quot; entre vous et votre partenaire est strictement une connexion. Aucune donnée n’est échangée au cours de ce processus.

Vous pouvez afficher une liste des connexions avec des partenaires existants dans l’interface principale de l’écran [!UICONTROL Gérer les partenaires]. Sur le rail droit se trouve le panneau [!UICONTROL Paramètre de partage], qui vous permet de générer un nouvel [!UICONTROL identifiant de connexion] ainsi qu’une zone de saisie dans laquelle vous pouvez saisir l’[!UICONTROL identifiant de connexion] d’un partenaire.

![enable-connection.png](../images/ui/segment-match/establish-connection.png)

Pour créer un [!UICONTROL identifiant de connexion], sélectionnez **[!UICONTROL Régénérer]** sous [!UICONTROL Paramètre de partage], puis sélectionnez l’icône de copie en regard de l’identifiant nouvellement généré.

![share-setting.png](../images/ui/segment-match/share-setting.png)

Pour connecter un partenaire à l’aide de son [!UICONTROL identifiant de connexion], saisissez sa valeur d’identifiant unique dans la zone de saisie sous [!UICONTROL Connecter le partenaire], puis sélectionnez **[!UICONTROL Demander]**.

![connect-partner.png](../images/ui/segment-match/connect-partner.png)

### Création d’un flux

Un **flux** est un groupe de données (segments), les règles d’exposition ou d’utilisation de ces données, ainsi que les configurations qui déterminent la manière dont vos données sont comparées aux données de vos partenaires. Un flux peut être géré indépendamment et échangé avec d’autres utilisateurs de Platform via [!DNL Segment Match].

Pour créer un flux, sélectionnez **[!UICONTROL Créer un flux]** dans le tableau de bord [!UICONTROL Flux].

![create-feed.png](../images/ui/segment-match/create-feed.png)

La configuration de base d’un flux comprend un nom, une description et des configurations concernant les cas d’utilisation marketing et les paramètres d’identité. Attribuez un nom et une description à votre flux, puis appliquez les cas d’utilisation marketing dont vous souhaitez que vos données soient exclues. Vous pouvez sélectionner plusieurs cas d’utilisation dans une liste qui comprend :

* [!UICONTROL Analytics]
* [!UICONTROL Combinaison avec les PII]
* [!UICONTROL Ciblage intersite]
* [!UICONTROL Science des données]
* [!UICONTROL Ciblage des emails]
* [!UICONTROL Exporter vers un tiers]
* [!UICONTROL Publicité sur site]
* [!UICONTROL Personnalisation Onsite]
* [!UICONTROL Correspondance de segments]
* [!UICONTROL Personnalisation d’une seule identité]

Enfin, sélectionnez les espaces de noms d’identité appropriés pour votre flux. Pour plus d’informations sur les espaces de noms spécifiques pris en charge par [!DNL Segment Match], consultez la [table des données d’identité et des espaces de noms](#namespaces). Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![audience-share.png](../images/ui/segment-match/audience-sharing.png)

Une fois les paramètres de votre flux définis, sélectionnez les segments que vous souhaitez partager dans la liste des segments propriétaires. Vous pouvez sélectionner plus d’un segment dans la liste et utiliser le rail droit pour gérer votre liste de segments sélectionnés. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![select-segments.png](../images/ui/segment-match/select-segments.png)

La page [!UICONTROL Partager] s’affiche, vous fournissant une interface pour sélectionner les partenaires avec lesquels vous souhaitez partager votre flux. Au cours de cette étape, vous pouvez également afficher le rapport des estimations de chevauchement de pré-partage et voir le nombre d’identités qui se chevauchent par espace de noms entre vous et votre partenaire, le nombre d’identités qui se chevauchent et qui ont le consentement de partager des données.

Sélectionnez **[!UICONTROL Analyser par segment]** pour afficher le rapport des estimations.

![analyze.png](../images/ui/segment-match/analyze.png)

Le rapport des estimations de chevauchement vous permet de gérer les contrôles de chevauchement et de consentement par partenaire et par segment avant de partager votre flux.

| Mesures | Description |
| ------- | ----------- |
| Identités estimées avec consentement | Nombre total d’identités qui se chevauchent et qui répondent aux exigences de consentement configurées pour votre organisation. |
| Estimation des identités chevauchées | Le nombre d’identités qui remplissent les critères pour le segment sélectionné et qui correspondent également au partenaire sélectionné. Ces identités sont affichées par espace de noms et ne représentent pas d’identités de profil individuelles. Les estimations de chevauchement sont basées sur des schémas de profil. |

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Fermer]**.

![duplicate.png](../images/ui/segment-match/overlap-report.png)

Une fois que vous avez sélectionné vos partenaires et consulté votre rapport d’estimations de chevauchement, sélectionnez **[!UICONTROL Suivant]** pour continuer.

![share.png](../images/ui/segment-match/share.png)

L’étape [!UICONTROL Réviser] s’affiche, ce qui vous permet de passer en revue votre nouveau flux avant qu’il ne soit partagé et publié. Cette étape comprend des détails sur le paramètre d’identité appliqué, ainsi que des informations sur les cas d’utilisation marketing, les segments et les partenaires que vous avez sélectionnés.

Sélectionnez **[!UICONTROL Terminer]** pour continuer.

![review.png](../images/ui/segment-match/review.png)

### Mise à jour du flux

Pour ajouter ou supprimer des segments, sélectionnez **[!UICONTROL Créer un flux]** dans la page [!UICONTROL Flux], puis sélectionnez **[!UICONTROL Flux existant]**. Dans la liste des flux existants qui s’affichent, sélectionnez le flux que vous souhaitez mettre à jour, puis sélectionnez **[!UICONTROL Suivant]**.

![liste de flux](../images/ui/segment-match/feed-list.png)

La liste des segments s’affiche. À partir de là, vous pouvez ajouter de nouveaux segments à votre flux et utiliser le rail droit pour supprimer les segments dont vous n’avez plus besoin. Une fois que vous avez terminé de gérer les segments dans votre flux, sélectionnez **[!UICONTROL Suivant]** , puis suivez les étapes décrites ci-dessus pour terminer le flux mis à jour.

![update](../images/ui/segment-match/update.png)

>[!NOTE]
>
>Lorsque vous ajoutez ou supprimez un segment d’un flux partagé, le partenaire de réception doit confirmer la modification en réactivant le bouton [!DNL Profile] dans la liste des flux reçus.

### Acceptation d’un flux entrant

Pour afficher un flux entrant, sélectionnez **[!UICONTROL Reçu]** dans l’en-tête de la page [!UICONTROL Flux] , puis sélectionnez le flux à afficher dans la liste. Pour accepter le flux, sélectionnez **[!UICONTROL Activer pour le profil]** et attendez quelques instants que l’état soit mis à jour de [!UICONTROL En attente] à [!UICONTROL Activé].

![received.png](../images/ui/segment-match/received.png)

Une fois que vous avez accepté un flux partagé, vous pouvez commencer à utiliser les données partagées pour créer de nouveaux segments.

## Étapes suivantes

En lisant ce document, vous avez acquis une compréhension de [!DNL Segment Match], de ses fonctionnalités et de son workflow de bout en bout. Consultez les documents suivants pour en savoir plus sur les autres services Platform :

* [[!DNL Segmentation Service]](../home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [Présentation d’[!DNL Real-time Customer Profile]](../../profile/home.md)
