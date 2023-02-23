---
title: Notes de mise à jour de Adobe Experience Platform - Février 2023
description: Notes de mise à jour de février 2023 pour Adobe Experience Platform.
source-git-commit: ff276de35ca2aaeec168f4c4386d849f3352ad57
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 35%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 22 février 2023**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Destinations]](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Query Service](#query-service)
- [Comptes associés dans Real-Time CDP B2B Edition](#related-accounts)
- [Sources](#sources)

## [!DNL Destinations] {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-features}

| Fonctionnalité | Description |
| ----------- | ----------- |
| [Amélioration de la stratégie de consentement](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) pour les intégrations avec [destinations basées sur des fichiers (par lots)](/help/destinations/destination-types.md#file-based) | <p> Lorsque les profils ne sont plus qualifiés pour une stratégie de consentement, l’Experience Platform communique désormais de manière proactive sa sortie de stratégie vers des destinations basées sur des fichiers. Cela suit le [version de février 2023](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) de la même fonctionnalité pour les destinations de diffusion en continu. </p> <p> <b>Remarque</b>: Cette fonctionnalité est disponible uniquement pour les clients de **[!UICONTROL Protection de la vie privée et protection]** et ceux de **[!UICONTROL Bouclier de santé]**. </p> |

{style=&quot;table-layout:auto&quot;}

**Documentation nouvelle ou mise à jour** {#destinations-new-updated-documentation}

| Documentation | Description |
| ----------- | ----------- |
| Fonctionnement de la documentation sur les destinations | <p>Nous avons publié trois nouveaux articles explicatifs sur le fonctionnement des destinations, sur la base des questions courantes des utilisateurs :</p> <p><ul><li>[Paramètres d’exportation configurables et communs des destinations](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[Comportement d’exportation de profils pour différents types de destinations](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[Gestion des identités dans le workflow d’activation des destinations](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

Pour des informations plus générales sur les destinations, consultez la [présentation des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Fonctionnalités mises à jour**
&#x200B; | Fonctionnalité | Description | | — | — | | Dépréciation des champs via l’interface utilisateur | Vous pouvez désormais abandonner les champs de vos schémas une fois les données ingérées. L’obsolescence des champs XDM vous permet de supprimer des champs de l’interface utilisateur tout en les conservant pour les utiliser. Si nécessaire, vous pouvez afficher à nouveau les champs obsolètes. Les segments, requêtes ou solutions en aval qui référencent ces champs s’exécuteront normalement. |

&#x200B; Pour plus d’informations sur XDM dans Platform, lisez la section [Présentation du système XDM](../../xdm/home.md). &#x200B;
<!-- Field deprecation: https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/field-deprecation.html -->

## Query Service {#query-service}

Query Service vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL Data Lake] d’Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données du lac de données et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, Data Science Workspace ou pour ingestion dans Real-Time Customer Profile.

**Fonctionnalités mises à jour**
&#x200B; | Fonctionnalité | Description | | — | — | | Activation des jeux de données pour les profils avec SQL | Utilisez des LIBELLÉS dans les requêtes CTAS pour rendre un jeu de données &quot;profile enabled&quot;, ou utilisez ALTER pour mettre à jour les jeux de données existants à activer pour le profil. | | Surveillance des requêtes planifiées | Utilisez l’onglet Requêtes planifiées pour trouver des informations importantes sur les exécutions de requête et vous abonner aux alertes. Surveillez les requêtes pour connaître les détails du planning, l’état et les messages/codes d’erreur en cas d’échec.  | | Active/désactive la fonction de saisie automatique | Éliminez certaines commandes de métadonnées et améliorez les temps de traitement en activant la fonction de saisie semi-automatique de l’éditeur de requêtes. Cette fonctionnalité suggère automatiquement les mots-clés SQL potentiels et les détails du tableau pour la requête au fur et à mesure que vous l’écrivez. | | Exemples de jeux de données | Spécifiez un taux d’échantillonnage dans votre requête et utilisez des exemples de jeux de données pour créer un échantillon aléatoire uniforme ou créez des exemples conditionnels en fonction de critères spécifiques. |

&#x200B; Pour plus d’informations sur Query Services, reportez-vous à la section [Présentation de Query Service](../../query-service/home.md). &#x200B;
<!-- Links for QS feature docs after release day: -->
<!-- Enable datasets for profile with SQL link: https://experienceleague.adobe.com/docs/experience-platform/query/sql/syntax.html#create-table-as-select -->
<!-- Monitor scheduled queries link: https://experienceleague.adobe.com/docs/experience-platform/query/monitor-queries.html  -->
<!-- Toggle auto-complete feature link: https://experienceleague.adobe.com/docs/experience-platform/query/ui/user-guide.html#auto-complete -->
<!-- dataset samples: https://experienceleague.adobe.com/docs/experience-platform/query/essential-concepts/dataset-samples.html -->

## Comptes associés dans Real-Time CDP B2B Edition {#related-accounts}

>[!NOTE]
>
>La fonctionnalité Comptes associés est disponible uniquement pour les clients de Real-Time CDP B2B Edition.

Comptes associés, [!DNL Real-Time CDP B2B] vous permet d’afficher la liste des comptes similaires au compte que vous parcourez. Vous pouvez inclure les comptes associés dans vos définitions de segment pour élargir votre portée ou appliquer des critères plus larges dans vos segments.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Activation du service de comptes associés | La nouvelle fonction de basculement vous permet d’activer le service de comptes associé sur votre compte. Pour plus d’informations, consultez le guide sur [activation du service de comptes associé](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style=&quot;table-layout:auto&quot;}

Pour en savoir plus sur les fonctions de comptes connexes, consultez les pages de documentation suivantes :

- [Présentation des comptes associés dans Real-Time CDP B2B Edition](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [Section « Comptes associés » du guide de l’interface utilisateur du profil de compte](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [Comment utiliser les comptes associés dans les définitions de segment ?](../../rtcdp/segmentation/b2b.md#related-accounts)

Pour en savoir plus sur l’édition B2B de Real-Time CDP, lisez le [Présentation de Real-Time CDP B2B Edition](../../rtcdp/overview.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes et vous permet de structurer, d’étiqueter et d’améliorer ces données à l’aide des services Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Désigner l’accès au niveau de l’abonnement avec [!DNL Google PubSub] | Vous pouvez désormais définir l’accès à un abonnement à une rubrique spécifique lors de l’utilisation de la propriété [!DNL Google PubSub] source en fournissant l’ID d’abonnement lors de l’authentification. Pour plus d’informations, reportez-vous à la section [!DNL Google PubSub] tutoriel sur l’authentification [utilisation de l’API Flow Service](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) ou [Interface utilisateur de Platform](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| Ingestion de données d’activité personnalisées à partir de [!DNL Marketo] | Vous pouvez désormais importer des données d’activité personnalisées depuis votre [!DNL Marketo] à l’Experience Platform. Pour ingérer des données d’activité personnalisées, vous devez configurer des groupes de champs d’activités personnalisés dans le schéma Activités B2B et créer un flux de données à l’aide du jeu de données des activités. Une fois le flux de données terminé, le jeu de données ingéré contiendra les activités standard et personnalisées de votre [!DNL Marketo] instance. Vous pouvez ensuite utiliser [Query Service](../../query-service/home.md) pour accéder aux enregistrements d’activité personnalisés sur Platform. Pour plus d’informations, consultez le guide sur [création d’un flux de données pour les données d’activité personnalisées](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| Exclure les comptes non réclamés de [!DNL Marketo] | Vous pouvez maintenant configurer si vous souhaitez exclure ou inclure des comptes non réclamés de l’ingestion lors de la création d’un flux de données pour les données d’entreprise. Pour plus d’informations, consultez le guide sur [création d’une connexion source et d’un flux de données pour [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style=&quot;table-layout:auto&quot;}

Pour en savoir plus sur les sources, lisez la [présentation des sources](../../sources/home.md).
