---
title: Comportement d’exportation de profils
description: Découvrez comment le comportement d’exportation de profils varie entre les différents modèles d’intégration pris en charge dans les destinations Experience Platform.
source-git-commit: 5d404d723ea0b7cc72c5188dcff1f59a1874cfe2
workflow-type: tm+mt
source-wordcount: '2979'
ht-degree: 24%

---

# Comportement d’exportation de profils pour différents types de destinations

Il existe plusieurs types de destinations dans Experience Platform, comme illustré dans le diagramme ci-dessous. Ces destinations présentent des modèles d’exportation légèrement différents en ce qui concerne ce qui déclenche un export destination et ce qui est inclus dans un export, comme décrit dans les sections ci-dessous.

>[!IMPORTANT]
>
>Cette page de documentation ne décrit que le comportement d’export de profil pour les connexions mises en évidence au bas du diagramme.

![Diagramme Types de destinations](/help/destinations/assets/how-destinations-work/types-of-destinations-v4.png)

## Stratégie de microtraitement et d’agrégation

Avant de passer à des informations spécifiques par type de destination, il est important de comprendre les concepts de la politique de microtraitement et d’agrégation pour *destinations de diffusion en continu*.

Les destinations Experience Platform exportent les données vers des intégrations basées sur l’API sous la forme d’appels HTTPS. Une fois que le service de destinations est informé par d’autres services en amont que les profils ont été mis à jour suite à l’ingestion par lots, à l’ingestion par flux, à la segmentation par lots, à la segmentation par flux ou aux modifications des graphiques d’identité, les données sont exportées et envoyées vers les destinations en continu.

Le processus par lequel les profils sont agrégés dans des messages HTTPS avant d’être envoyés aux points de terminaison de l’API de destination est appelé *microtraitement*.

Prenez le [Destination facebook](/help/destinations/catalog/social/facebook.md) avec un *[agrégation configurable](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation)* stratégie par exemple : les données sont envoyées de manière agrégée, où le service de destinations récupère toutes les données entrantes du service de profil en amont et les agrège par l’une des méthodes suivantes, avant de les distribuer à Facebook :

* Nombre d&#39;enregistrements (maximum 10 000) ou
* Intervalle de fenêtre temporelle (30 minutes)

Les seuils ci-dessus qui sont atteints pour la première fois déclenchent une exportation vers Facebook. Ainsi, dans la variable [!DNL Facebook Custom Audiences] tableau de bord, vous pouvez voir des audiences provenant d’Experience Platform par incréments d’enregistrement de 10 000. Vous pouvez voir 10 000 enregistrements toutes les 10 à 15 minutes, car les données sont traitées et agrégées plus rapidement que l’intervalle d’exportation de 30 minutes, et sont envoyées plus rapidement, donc environ toutes les 10 à 15 minutes jusqu’à ce que tous les enregistrements aient été traités. S’il n’y a pas suffisamment d’enregistrements pour constituer un lot de 10 000, le nombre d’enregistrements actuels est envoyé tel quel lorsque le délai limite est atteint, de sorte que vous pouvez également voir des lots plus petits envoyés à Facebook.

Prenons un autre exemple : [Destination de l’API HTTP](/help/destinations/catalog/streaming/http-destination.md), qui a une *[agrégation des meilleurs efforts](/help/destinations/destination-sdk/destination-configuration.md#best-effort-aggregation)* avec `maxUsersPerRequest: 10`. Cela signifie qu’un maximum de dix profils seront agrégés avant qu’un appel HTTP ne soit déclenché vers cette destination, mais l’Experience Platform tente d’envoyer des profils vers la destination dès que le service de destinations reçoit des informations de réévaluation mises à jour d’un service en amont.

La stratégie d’agrégation est configurable et les développeurs de destination peuvent décider comment configurer la stratégie d’agrégation pour respecter au mieux les limites de taux des points de terminaison de l’API en aval. En savoir plus sur [stratégie d’agrégation](/help/destinations/destination-sdk/destination-configuration.md#aggregation) dans la documentation de la Destination SDK.

## Destinations d’exportation de profils en flux continu (entreprise) {#streaming-profile-destinations}

>[!IMPORTANT]
>
> Les destinations d’entreprise ne sont disponibles que pour [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html) clients.

Le [destinations d’entreprise](/help/destinations/destination-types.md#streaming-profile-export) dans l’Experience Platform se trouvent Amazon Kinesis, Azure Event Hubs et l’API HTTP.

Experience Platform optimise le comportement d’exportation de profils vers la destination de votre entreprise, afin de n’exporter les données vers votre point de terminaison API que lorsque des mises à jour pertinentes d’un profil se sont produites à la suite de la qualification de segment ou d’autres événements significatifs. Les profils sont exportés vers votre destination dans les situations suivantes :

* La mise à jour du profil a été déterminée par une modification de la variable [abonnement au segment](/help/xdm/field-groups/profile/segmentation.md) pour au moins un des segments mappés à la destination. Par exemple, le profil est qualifié pour l’un des segments mappés à la destination ou a quitté l’un de ces segments.
* La mise à jour du profil a été déterminée par une modification dans le [mappage d’identités](/help/xdm/field-groups/profile/identitymap.md). Par exemple, une nouvelle identité a été ajoutée dans l’attribut de mappage d’identités à un profil qui était déjà qualifié pour l’un des segments mappés à la destination.
* La mise à jour du profil a été déterminée par une modification des attributs pour au moins un des attributs mappés à la destination. Par exemple, l’un des attributs mappés à la destination dans l’étape de mappage est ajouté à un profil.

Dans tous les cas décrits ci-dessus, seuls les profils pour lesquels des mises à jour pertinentes se sont produites sont exportés vers votre destination. Par exemple, si un segment mappé au flux de destination comporte cent membres et que cinq nouveaux profils sont qualifiés pour ce segment, l’exportation vers votre destination est incrémentielle et inclut uniquement les cinq nouveaux profils.

Notez que tous les attributs mappés sont exportés pour un profil, quel que soit l’emplacement des modifications. Ainsi, dans l’exemple ci-dessus, tous les attributs mappés pour ces cinq nouveaux profils seront exportés même si les attributs eux-mêmes restent inchangés.

### Ce qui détermine une exportation de données et ce qui est inclus dans l’exportation

En ce qui concerne les données exportées pour un profil donné, il est important de comprendre les deux concepts différents de *ce qui détermine l’exportation des données vers votre destination d’entreprise* et *les données incluses dans l’exportation ;*.

| Ce qui détermine une exportation de destination | Éléments inclus dans l’exportation de destination |
|---------|----------|
| <ul><li>Les attributs et segments mappés servent de repère pour une exportation de destination. Cela signifie que si un segment mappé change d’état (de nul à réalisé ou de réalisé/existant à sorti), ou qu’un attribut mappé est mis à jour, une exportation de destination est déclenchée.</li><li>Comme les identités ne peuvent actuellement pas être mappées aux destinations d’entreprise, les modifications d’identité sur un profil donné déterminent également les exportations de destination.</li><li>Toute modification pour un attribut est considérée comme une mise à jour, qu’il s’agisse ou non de la même valeur. Cela signifie qu’une réécriture sur un attribut est considérée comme une modification, même si la valeur elle-même n’a pas changé.</li></ul> | <ul><li>Le `segmentMembership` inclut le segment mappé dans le flux de données d’activation, pour lequel l’état du profil a changé suite à un événement de qualification ou de sortie de segment. Notez que d’autres segments non mappés pour lesquels le profil est qualifié peuvent faire partie de l’exportation de destination, si ces segments appartiennent au même type. [stratégie de fusion](/help/profile/merge-policies/overview.md) comme segment mappé dans le flux de données d’activation. </li><li>Toutes les identités dans la variable `identityMap` sont également inclus (Experience Platform ne prend actuellement pas en charge le mappage d’identité dans la destination de l’entreprise).</li><li>Seuls les attributs mappés sont inclus dans l’exportation de destination.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

>[!IMPORTANT]
>
>Les destinations d’entreprise diffusent des données de renvoi lors de l’activation de profils vers une destination. Cela signifie que la première exportation de données après la configuration d’un workflow d’activation vers une destination inclut les profils qui remplissent les critères pour le segment activé avant que le segment ne soit mappé à la destination.

>[!BEGINSHADEBOX]

Prenons l’exemple d’un flux de données vers une destination HTTP dans lequel trois segments sont sélectionnés et quatre attributs sont mappés à la destination.

![flux de données de destination d’entreprise](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Une exportation de profil vers la destination peut être déterminée par un profil éligible ou sortant de l’un des *trois segments mappés*. Toutefois, dans l’exportation des données, dans la variable `segmentMembership` , d’autres segments non mappés peuvent apparaître si ce profil particulier en est membre et s’ils partagent la même stratégie de fusion que le segment qui a déclenché l’exportation. Si un profil est admissible pour la variable **Client avec des voitures DeLorean** , mais est également membre de la fonction **Regardez le film &quot;Retour vers le futur&quot;** et **Fans de science-fiction** , ces deux autres segments seront également présents dans la variable `segmentMembership` de l’exportation des données, même si elles ne sont pas mappées dans le flux de données, si elles partagent la même stratégie de fusion avec l’objet **Client avec des voitures DeLorean** segment.

Du point de vue des attributs de profil, toute modification apportée aux quatre attributs mappés ci-dessus déterminera une exportation de destination et chacun de ces quatre attributs mappés et présents sur le profil sera présent dans l’exportation des données.

>[!ENDSHADEBOX]

>[!TIP]
>
> Vous pouvez consulter des exemples de données exportées vers différentes destinations d’entreprise dans le [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md#exported-data), [Centre d’événements Azure](/help/destinations/catalog/cloud-storage/azure-event-hubs.md#exported-data), et [API HTTP](/help/destinations/catalog/streaming/http-destination.md#exported-data) pages de documentation de destination.

## Destinations basées sur des API de diffusion en continu {#streaming-api-based-destinations}

Le comportement d’exportation de profils pour les destinations de diffusion en continu telles que Facebook, le bureau commercial et d’autres intégrations basées sur les API est très similaire au comportement décrit ci-dessus pour les destinations d’entreprise.

Les destinations appartenant à la variable [catégories sociales et publicitaires](/help/destinations/destination-types.md#categories) dans le catalogue.

Experience Platform optimise le comportement d’exportation de profils vers votre destination de diffusion en continu, afin de n’exporter que les données vers des destinations basées sur l’API de diffusion en continu lorsque des mises à jour pertinentes d’un profil se sont produites à la suite de la qualification du segment ou d’autres événements significatifs. Les profils sont exportés vers votre destination dans les situations suivantes :

* La mise à jour du profil a été déterminée par une modification de la variable [abonnement au segment](/help/xdm/field-groups/profile/segmentation.md) pour au moins un des segments mappés à la destination. Par exemple, le profil est qualifié pour l’un des segments mappés à la destination ou a quitté l’un de ces segments.
* La mise à jour du profil a été déterminée par une modification de la variable [identity map](/help/xdm/field-groups/profile/identitymap.md) pour un espace de noms d’identité marqué pour l’exportation pour cette instance de destination. Par exemple, une nouvelle identité a été ajoutée dans l’attribut de mappage d’identités à un profil qui était déjà qualifié pour l’un des segments mappés à la destination.
* La mise à jour du profil a été déterminée par une modification des attributs pour au moins un des attributs mappés à la destination. Par exemple, l’un des attributs mappés à la destination dans l’étape de mappage est ajouté à un profil.
* Modifications du consentement pour un profil lorsque l’application automatisée du consentement est configurée et qu’un profil s’exclut. L’application automatisée du consentement envoie un événement de sortie d’audience à la destination afin que le profil ne soit inclus dans aucun ciblage à la destination.

Dans tous les cas décrits ci-dessus, seuls les profils pour lesquels des mises à jour pertinentes se sont produites sont exportés vers votre destination. Par exemple, si un segment mappé au flux de destination comporte cent membres et que cinq nouveaux profils sont qualifiés pour ce segment, l’exportation vers votre destination est incrémentielle et inclut uniquement les cinq nouveaux profils.

Notez que tous les attributs mappés sont exportés pour un profil, quel que soit l’emplacement des modifications. Ainsi, dans l’exemple ci-dessus, tous les attributs mappés pour ces cinq nouveaux profils seront exportés même si les attributs eux-mêmes restent inchangés.

### Ce qui détermine une exportation de données et ce qui est inclus dans l’exportation

En ce qui concerne les données exportées pour un profil donné, il est important de comprendre les deux concepts différents qui déterminent ce qui détermine une exportation de données vers votre destination d’API de diffusion en continu et quelles données sont incluses dans l’exportation.

| Ce qui détermine une exportation de destination | Éléments inclus dans l’exportation de destination |
|---------|----------|
| <ul><li>Les attributs et segments mappés servent de repère pour une exportation de destination. Cela signifie que si un segment mappé change d’état (de nul à réalisé ou de réalisé/existant à sorti), ou qu’un attribut mappé est mis à jour, une exportation de destination est déclenchée.</li><li>Une modification de la carte des identités est définie comme une identité ajoutée/supprimée pour la variable [graphique d’identités](/help/identity-service/ui/identity-graph-viewer.md) du profil, pour les espaces de noms d’identité mappés pour l’exportation.</li><li>Une modification pour un attribut est définie comme toute mise à jour de l’attribut, pour les attributs mappés à la destination.</li></ul> | <ul><li>Les segments qui sont mappés à la destination et qui ont été modifiés seront inclus dans la variable `segmentMembership` . Dans certains scénarios, ils peuvent être exportés à l’aide de plusieurs appels. En outre, dans certains scénarios, certains segments qui n’ont pas été modifiés peuvent également être inclus dans l’appel . Dans tous les cas, seuls les segments mappés seront exportés.</li><li>Toutes les identités des espaces de noms qui sont mappés à la destination dans la variable `identityMap` sont également inclus .</li><li>Seuls les attributs mappés sont inclus dans l’exportation de destination.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

>[!IMPORTANT]
>
>Les destinations d’API de diffusion en continu diffusent les données de renvoi lors de l’activation de profils vers une destination. Cela signifie que la première exportation de données après la configuration d’un workflow d’activation vers une destination inclut les profils qui remplissent les critères pour le segment activé avant que le segment ne soit mappé à la destination.

>[!BEGINSHADEBOX]

Prenons l’exemple de ce flux de données vers une destination de diffusion en continu où trois segments sont sélectionnés dans le flux de données.

![flux de données de destination de diffusion en continu](/help/destinations/assets/how-destinations-work/streaming-destination-example-dataflow.png)

Une exportation de profil vers la destination peut être déterminée par un profil éligible ou sortant de l’un des trois segments mappés. Si un profil est qualifié pour la variable **Client avec des voitures DeLorean** , cela déclenche une exportation. Les autres segments (**Ville - Dallas** et **Principal de base du site**) peut également être exporté si le segment est présent dans le profil avec l’un des états possibles (`realized`, `existing`, `exited`). Segments non mappés (comme **Fans de science-fiction**) ne seront pas exportés.

Du point de vue des attributs de profil, toute modification des trois attributs mappés ci-dessus déterminera une exportation de destination.

>[!ENDSHADEBOX]

## Destinations de lot (basées sur des fichiers) {#file-based-destinations}

Lors de l’exportation de profils vers [destinations basées sur des fichiers](/help/destinations/destination-types.md#file-based) dans Experience Platform, vous pouvez utiliser trois types de plannings (répertoriés ci-dessous) et deux options d’exportation de fichiers (fichiers complets ou incrémentiels). Tous ces paramètres sont définis au niveau du segment, même lorsque plusieurs segments sont mappés à un seul flux de données de destination.

* Exports planifiés : Configurez une destination, ajoutez un ou plusieurs segments, choisissez si vous souhaitez exporter des fichiers complets ou incrémentiels et sélectionnez une heure définie chaque jour ou plusieurs fois par jour où les fichiers doivent être exportés. Par exemple, une heure d’exportation de 17 heures signifie que les profils qualifiés pour le segment seront exportés à 17 heures.
* Après l’évaluation du segment : L’exportation est déclenchée immédiatement après l’exécution de la tâche d’évaluation de segment quotidienne. Cela signifie que les numéros de profil exportés dans le fichier sont aussi proches que possible de la dernière population évaluée du segment.
* Exports à la demande ([exporter le fichier maintenant](/help/destinations/ui/export-file-now.md)) : En fonction de la dernière tâche d’évaluation de segment, un fichier complet est exporté une fois en plus des exportations régulièrement planifiées.

Dans l’une des situations d’exportation ci-dessus, les fichiers exportés incluent les profils qualifiés pour l’exportation, ainsi que les colonnes que vous avez sélectionnées en tant qu’attributs XDM pour l’exportation.

>[!TIP]
>
>Lorsqu’un segment en continu est mappé à une destination par lot, il est plus probable que le nombre de profils dans le fichier exporté soit plus proche du nombre d’utilisateurs dans le segment. En effet, il y a plus de chances que la dernière évaluation de segment se rapproche du délai d’exportation.

### Exports incrémentiels de fichiers {#incremental-file-exports}

Toutes les mises à jour d’un profil ne qualifient pas un profil à inclure dans les exportations incrémentielles de fichiers. Par exemple, si un attribut a été ajouté ou supprimé d’un profil, il n’inclut pas le profil dans l’exportation. Uniquement les profils pour lesquels la variable `segmentMembership` a changé sera inclus dans les fichiers exportés. En d’autres termes, ce n’est que si le profil fait partie du segment ou est supprimé du segment qu’il est inclus dans les exportations incrémentielles de fichiers.

De même, si une nouvelle identité (nouvelle adresse électronique, numéro de téléphone, ECID, etc.) est ajoutée à un profil dans la variable [graphique d’identités](/help/identity-service/ui/identity-graph-viewer.md), qui ne représente pas une raison d’inclure le profil dans une nouvelle exportation de fichier incrémentielle.

Si un nouveau segment est ajouté à un mappage de destination, cela n’a aucune incidence sur les qualifications et les exportations pour un autre segment. Les plannings d’exportation sont configurés individuellement par segment et les fichiers sont exportés séparément pour chaque segment, même si les segments ont été ajoutés au même flux de données de destination.

>[!BEGINSHADEBOX]

Par exemple, dans le paramètre d’exportation illustré ci-dessous, lorsqu’un segment exporte des mises à jour de fichier incrémentielles, notez les circonstances suivantes lorsqu’un profil est inclus ou non dans un export de fichier incrémentiel :

![Paramètre d’exportation avec plusieurs attributs sélectionnés.](/help/destinations/assets/how-destinations-work/export-selection-batch-destination.png)

* Un profil est inclus dans une exportation de fichier incrémentielle lorsqu’il est admissible ou non pour le segment.
* Un profil est *not* inclus dans un export de fichier incrémentiel lorsqu’un nouveau numéro de téléphone est ajouté au graphique d’identités.
* Un profil est *not* inclus dans une exportation de fichier incrémentielle lorsque la valeur de l’un des champs XDM mappés, comme `xdm: loyalty.points`, `xdm: loyalty.tier`, `xdm: personalEmail.address` est mis à jour sur un profil.
* Lorsque la variable `segmentMembership.status` Le champ XDM est mappé dans le workflow d’activation de destination, les profils qui sortent du segment sont également inclus dans les fichiers incrémentiels exportés, avec une `exited` statut.

>[!ENDSHADEBOX]

### Ce qui détermine une exportation de données et ce qui est inclus dans l’exportation

Selon les informations de la section ci-dessus, le comportement d’exportation de profils vers des destinations basées sur des fichiers peut être résumé comme décrit ci-dessous :

**Exports de fichiers complets**

La population principale totale du segment est exportée tous les jours.

| Ce qui détermine une exportation de destination | Éléments inclus dans le fichier exporté |
|---------|----------|
| <ul><li>Le planning d’exportation défini dans l’interface utilisateur ou l’API et l’action de l’utilisateur (en sélectionnant [Exporter le fichier maintenant](/help/destinations/ui/export-file-now.md) dans l’interface utilisateur ou à l’aide de la fonction [API d’activation ad hoc](/help/destinations/api/ad-hoc-activation-api.md)) déterminent le début d’une exportation de destination.</li><li>Toute modification de l’appartenance à un segment d’un profil, qu’il soit admissible ou non dans le segment, qualifie un profil à inclure dans les exportations incrémentielles.</li></ul> | Dans les exportations complètes de fichiers, la population principale de profils d’un segment, basée sur la dernière évaluation de segment, est incluse avec chaque exportation de fichiers. Les dernières valeurs pour chaque attribut XDM sélectionné pour l’exportation sont également incluses en tant que colonnes dans chaque fichier. Notez que les profils à l’état de sortie ne sont pas inclus dans l’exportation du fichier. |

{style=&quot;table-layout:fixed&quot;}

**Exports incrémentiels de fichiers**

Dans le premier export de fichier, après avoir configuré le workflow d&#39;activation, la population entière du segment est exportée. Lors des exports suivants, seuls les profils modifiés sont exportés.

| Ce qui détermine une exportation de destination | Éléments inclus dans le fichier exporté |
|---------|----------|
| <ul><li>Le planning d’exportation défini dans l’interface utilisateur ou l’API détermine le début d’une exportation de destination.</li><li>Toute modification de l’appartenance à un segment d’un profil, qu’il soit admissible ou non dans le segment, qualifie un profil à inclure dans les exportations incrémentielles. Modifications des attributs ou des mappages d’identité d’un profil *ne pas* qualifier un profil à inclure dans les exportations incrémentielles.</li></ul> | <p>Profils pour lesquels l’appartenance au segment a changé, ainsi que les informations les plus récentes pour chaque attribut XDM sélectionné pour l’exportation.</p><p>Les profils avec le statut de sortie sont inclus dans les exportations de destination, si la variable `segmentMembership.status` Le champ XDM est sélectionné à l’étape de mappage.</p> |

{style=&quot;table-layout:fixed&quot;}

>[!TIP]
>
>Pour rappel, les modifications apportées aux valeurs d’attribut ou aux mappages d’identité d’un profil ne répondent pas aux critères d’inclusion d’un profil dans une exportation de fichier incrémentielle.

## Étapes suivantes {#next-steps}

Après avoir lu ce document, vous savez maintenant quoi attendre dans les exportations de profils vers des destinations en flux continu, d’entreprise et basées sur des fichiers.

Ensuite, vous pouvez découvrir comment [les identités sont gérées](/help/destinations/how-destinations-work/identity-handling.md) dans le workflow d’activation.
