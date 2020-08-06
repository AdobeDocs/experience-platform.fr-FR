---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de l’utilisateur du service de segmentation
topic: ui guide
translation-type: tm+mt
source-git-commit: e7266fba14b2dffe46ce77428ad6fe0dd92abdf5
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 30%

---


# [!UICONTROL Guide de l’utilisateur du service] de segmentation

[!DNL Adobe Experience Platform Segmentation Service] fournit une interface utilisateur pour la création et la gestion des définitions de segment.

## Prise en main

Working with segment definitions requires an understanding of the various [!DNL Experience Platform] services involved with segmentation. Avant de lire ce guide d’utilisation, veuillez consulter la documentation relative aux services suivants :

- [[ !Service de segmentation DNL]](../home.md): [!DNL Segmentation Service] vous permet de diviser les données stockées dans [!DNL Experience Platform] des données relatives à des individus (tels que des clients, des prospects, des utilisateurs ou des organisations) en groupes plus petits.
- [[ !Profil client en temps réel DNL]](../../profile/home.md): Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
- [[ !Service d&#39;identité Adobe Experience Platform DNL]](../../identity-service/home.md): Permet la création de profils client en faisant le lien entre les identités issues de sources de données disparates et qui sont incorporées dans [!DNL Platform].
- [[ ! Modèle de données d’expérience DNL (XDM)]](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Platform] organiser les données d’expérience client.

Il est également important de connaître deux termes clés utilisés dans ce document et de comprendre la différence entre eux :
- **Définition de segment** : ensemble des règles utilisées pour décrire les caractéristiques ou les comportements clés d’une audience cible.
- **Audience** : ensemble des profils ainsi obtenus qui répondent aux critères d’une définition de segment.

## Présentation

Dans l’ [[!DNL Experience Platform] interface](http://platform.adobe.com/)utilisateur, sélectionnez **[!UICONTROL Segments]** dans le volet de navigation de gauche pour ouvrir l’onglet **[!UICONTROL Aperçu]** . Cet onglet fournit des liens vers la documentation et les vidéos pour vous aider à comprendre et à commencer à travailler avec les segments.

![](../images/ui/overview/segment-overview.png)

## Parcourir

Sélectionnez l&#39;onglet **[!UICONTROL Parcourir]** pour afficher une liste de toutes les définitions de segment pour votre organisation IMS.

![](../images/ui/overview/segment-browse-all.png)

Cette vue contient des informations sur la définition de segment, y compris la méthode d’évaluation, la date de création et la date de dernière modification.

La méthode d’évaluation peut être soit par flux, soit par lot. Les segments par flux sont constamment évalués au fur et à mesure que les données entrent dans le système. Les segments par lot sont évalués selon un planning établi.

![](../images/ui/overview/segment-browse-segments.png)

En haut de la page se trouvent les options permettant d’ajouter tous les segments à un calendrier et de créer un segment.

Si vous basculez sur **[!UICONTROL Ajouter tous les segments à planifier]** , la segmentation planifiée sera activée. Vous trouverez plus d’informations sur la segmentation planifiée dans la section Segmentation [planifiée de ce guide](#scheduled-segmentation)d’utilisateur.

Si vous sélectionnez **[!UICONTROL Créer un segment]** , vous accédez au créateur de segments. Pour en savoir plus sur la création de segments, consultez la section sur la [création d’un segment dans le guide](#create-segment)d’utilisateur.

![](../images/ui/overview/segment-browse-top.png)

La barre latérale droite contient des informations sur tous les segments au sein de l&#39;organisation du SGI, en indiquant le nombre total de segments, la date de la dernière évaluation, la date de la prochaine évaluation, ainsi qu&#39;une ventilation des segments par méthode d&#39;évaluation.

![](../images/ui/overview/segment-browse-segment-info.png)

La sélection de la ligne de la définition de segment fournit un résumé de la définition de segment, y compris des options permettant de modifier ou de supprimer le segment, l&#39;audience qualifiée du segment, la taille totale de l&#39;audience, en plus du nom du segment, de la description, de la méthode d&#39;évaluation, de la date de création et de la date de dernière modification.

![](../images/ui/overview/segment-browse-details.png)

## Détails de la définition de segment {#segment-details}

Pour en savoir plus sur une définition de segment spécifique, sélectionnez le nom d’un segment dans l’onglet **[!UICONTROL Parcourir]** .

La page Détails du segment s’affiche. En haut, vous trouverez un résumé de la définition de segment, des informations sur la taille d’audience qualifiée, ainsi que les destinations pour lesquelles le segment est activé.

![](../images/ui/overview/segment-details-summary.png)

### Résumé de segment

La section Résumé **** de segment fournit des informations telles que l’ID, le nom, la description et les détails des attributs.

De plus, vous disposez de l’option permettant de modifier le segment. Si vous sélectionnez **[!UICONTROL Modifier le segment]** , vous accédez au [!DNL Segment Builder]segment. Pour plus d&#39;informations sur l&#39;utilisation de l&#39; [!DNL Segment Builder] espace de travail, veuillez lire le guide [[!DNL Segment Builder] d&#39;](./segment-builder.md)utilisation.

### audience totale dans le segment

La section audience **[!UICONTROL totale du segment]** affiche le nombre total de profils admissibles pour le segment.

Les estimations sont générées en utilisant la taille d’échantillon des données d’échantillon de cette journée. S’il y a moins d’un million d’entités dans votre banque de profils, l’ensemble des données est utilisé. Entre 1 et 20 millions d’entités, 1 million d’entités sont utilisées. Et pour plus de 20 millions d’entités, 5 % du total des entités sont utilisés. Vous trouverez plus d’informations sur la génération d’estimations de segments dans la [section Génération d’estimations](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) du tutoriel sur la création de segments.

### Destinations activées

La section Destinations **** activées affiche les destinations pour lesquelles ce segment est activé.

>[!NOTE]
>
> Les destinations sont une fonction disponible avec [!DNL Real-time Customer Data Platform]laquelle vous pouvez exporter des données vers des plateformes externes. For more information on destinations, please read the [destinations overview](../../rtcdp/destinations/destinations-overview.md). Pour savoir comment activer un segment vers une destination, consultez le [guide d’activation des segments vers une destination](../../rtcdp/destinations/activate-destinations.md).

### Échantillons de Profil

Vous trouverez ci-dessous un échantillon des profils qui remplissent les critères du segment, en détaillant des informations, notamment l’ [!DNL Profile] identifiant, le prénom, le nom et l’adresse électronique personnelle.

La façon dont l’échantillonnage des données est déclenché dépend de la méthode d’assimilation.

Pour l’assimilation par lot, le magasin de profils est automatiquement analysé toutes les quinze minutes afin de déterminer si un nouveau lot a été correctement assimilé depuis l’exécution de la dernière tâche d’échantillonnage. Si tel est le cas, le magasin de profils est ensuite analysé pour voir s&#39;il y a eu au moins 5 % de changement dans le nombre d&#39;enregistrements. Si ces conditions sont remplies, une nouvelle tâche d’échantillonnage est déclenchée.

Pour l’assimilation en flux continu, le magasin de profils est automatiquement analysé toutes les heures afin de déterminer s’il y a eu au moins 5 % de changement dans le nombre d’enregistrements. Si cette condition est remplie, une nouvelle tâche d’échantillonnage est déclenchée.

La taille d’échantillon de l’analyse dépend du nombre total d’entités présentes dans votre magasin de profils. Ces tailles d’échantillon sont représentées dans le tableau suivant :

| Entités dans la banque de profils | Taille de l’échantillon |
| ------------------------- | ----------- |
| Moins de 1 million | Jeu de données complet |
| 1 à 20 millions | 1 million |
| Plus de 20 millions | 5 % du total |

Pour obtenir des informations plus détaillées sur chaque [!DNL Profile] identifiant, sélectionnez l’ [!DNL Profile] identifiant. Pour en savoir plus sur les détails d&#39;un profil, veuillez lire le guide [[!DNL Real-time Customer Profile] ](../../profile/ui/user-guide.md#profile-detail)d&#39;utilisation.

![](../images/ui/overview/segment-details-profiles.png)

## Création d’un segment {#create-segment}

Selecting **[!UICONTROL Create segment]** in the top-right corner opens the [!DNL Segment Builder] workspace, where you can begin creating a segment definition.

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] espace de travail

[!DNL Segment Builder] fournit un espace de travail riche qui vous permet d’interagir avec [!DNL Profile] des éléments de données. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données.

Pour plus d&#39;informations sur l&#39;utilisation de l&#39; [!DNL Segment Builder] espace de travail, veuillez lire le guide [[!DNL Segment Builder] d&#39;](./segment-builder.md)utilisation.

![](../images/ui/overview/segment-builder.png)

## Segmentation planifiée {#scheduled-segmentation}

Une fois les définitions de segment créées, vous pouvez les évaluer par le biais d’une évaluation sur demande ou planifiée (continue). Evaluation means moving [!DNL Real-time Customer Profile] data through segment definitions in order to produce corresponding audiences. Once created, the audiences are saved and stored so that they can be exported using [!DNL Experience Platform] APIs.

L’évaluation sur demande nécessite l’utilisation de l’API pour effectuer l’évaluation et créer des audiences selon les besoins, alors que l’évaluation planifiée (également appelée « segmentation planifiée ») vous permet de créer un planning récurrent pour évaluer les définitions de segment à un moment précis (au maximum, une fois par jour).

### Activation de la segmentation planifiée {#enable-scheduled-segmentation}

Vous pouvez activer les définitions de segment pour une évaluation planifiée à l’aide de l’interface utilisateur ou de l’API. In the UI, return to the **[!UICONTROL Browse]** tab within **[!UICONTROL Segments]** and toggle on **[!UICONTROL Add all segments to schedule]**. Tous les segments seront alors évalués en fonction du planning défini par votre organisation.

>[!NOTE]
>
>L’évaluation planifiée peut être activée pour les environnements de test avec un maximum de cinq (5) stratégies de fusion pour [!DNL XDM Individual Profile]. If your organization has more than five merge policies for [!DNL XDM Individual Profile] within a single sandbox environment, you will not be able to use scheduled evaluation.

Actuellement, les plannings ne peuvent être créés qu’à l’aide de l’API. Pour obtenir des instructions détaillées sur la création, la modification et l’utilisation des plannings à l’aide de l’API, suivez le tutoriel relatif à l’évaluation et à l’accès aux résultats de segmentation, en particulier la section sur [l’évaluation planifiée à l’aide de l’API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/ui/overview/segment-browse-scheduled.png)

## Segmentation par flux {#streaming-segmentation}

La segmentation en flux continu permet d’effectuer une segmentation [!DNL Platform] en temps quasi réel, tout en mettant l’accent sur la richesse des données. Avec la segmentation en flux continu, la qualification de segment se produit désormais lorsque les données entrent en [!DNL Platform]jeu, ce qui évite d’avoir à planifier et à exécuter des tâches de segmentation.

Vous trouverez plus d’informations sur la segmentation en flux continu dans le guide [d’utilisation de la segmentation en](./streaming-segmentation.md)flux continu.

>[!NOTE]
>
>Pour que la segmentation en flux continu fonctionne, vous devez activer la segmentation planifiée pour l’entreprise. For details on enabling scheduled segmentation, please refer to [the streaming segmentation section in this user guide](#scheduled-segmentation).

## Violations de stratégie DULE

>[!NOTE]
>
>Les violations de stratégie DULE ne s’appliquent que si vous créez un segment qui a été affecté à une destination.

Once you are done creating your segment, the segment will be analyzed by [!DNL Data Governance] to ensure there are no policy violations within the segment. Pour plus d’informations sur DULE et sur les violations de stratégie, reportez-vous à la [présentation des libellés d’utilisation des données](../../data-governance/labels/overview.md).

![](../images/ui/overview/segment-dule-policy-violations.png)

## Étapes suivantes and additional resources {#next-steps}

The [!DNL Segmentation Service] UI provides a rich workflow allowing you to isolate marketable audiences from [!DNL Real-time Customer Profile] data.

Pour en savoir plus [!DNL Segmentation Service], veuillez continuer à lire la documentation. Pour savoir comment utiliser l&#39; [!DNL Segmentation Service] API, veuillez lire le guide [[!DNL Segmentation Service] du](../api/overview.md)développeur.
