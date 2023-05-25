---
title: Comportement d’exportation de profils
description: Découvrez comment le comportement d’exportation de profils varie entre les différents modèles d’intégration pris en charge dans les destinations Experience Platform.
exl-id: 2be62843-0644-41fa-a860-ccd65472562e
source-git-commit: c54fa206b673868ca3d0ccfa5b0936b83cfd3ed4
workflow-type: tm+mt
source-wordcount: '2933'
ht-degree: 93%

---

# Comportement d’exportation de profils selon les types de destinations

Il existe plusieurs types de destinations dans Experience Platform, comme illustré dans le diagramme ci-dessous. Ces destinations ont des schémas d&#39;exportation légèrement différents en ce qui concerne les éléments qui déclenchent une exportation de destination et ce qui est inclus dans une exportation, comme décrit dans les sections ci-dessous.

>[!IMPORTANT]
>
>Cette page de documentation ne décrit que le comportement d’exportation de profil pour les connexions mises en évidence en bas du diagramme.

![Diagramme Types de destinations](/help/destinations/assets/how-destinations-work/types-of-destinations-v4.png)

## Politique de microtraitement et d’agrégation

Avant de passer à des informations spécifiques par type de destination, il est important de comprendre les concepts de la politique de microtraitement et d’agrégation pour les *destinations de streaming*.

Les destinations Experience Platform exportent les données vers des intégrations basées sur les API sous la forme d’appels HTTPS. Une fois que le service de destinations est informé par d’autres services en amont que les profils ont été mis à jour suite à l’ingestion par lots, à l’ingestion par streaming, à la segmentation par lots, à la segmentation par streaming ou aux modifications des graphiques d’identité, les données sont exportées et envoyées vers les destinations de streaming.

Le processus par lequel les profils sont agrégés dans des messages HTTPS avant d’être envoyés aux points d’entrée de l’API de destination est appelé *microtraitement*.

Prenez par exemple la [destination Facebook](/help/destinations/catalog/social/facebook.md) avec une politique d’*[agrégation configurable](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)*. Dans ce cas, les données sont envoyées de manière agrégée, où le service de destinations récupère toutes les données entrantes du service de profil en amont et les agrège par l’une des méthodes suivantes, avant de les distribuer à Facebook :

* Nombre d&#39;enregistrements (maximum 10 000) ou
* Intervalle de fenêtre de délai (30 minutes)

Les seuils ci-dessus qui sont les premiers atteints déclenchent une exportation vers Facebook. Ainsi, dans la variable [!DNL Facebook Custom Audiences] tableau de bord, vous pouvez voir des audiences provenant d’Experience Platform par 10 000 incréments d’enregistrement. Vous pouvez voir 10 000 enregistrements toutes les 10 à 15 minutes, car les données sont traitées et agrégées plus rapidement que l’intervalle d’exportation de 30 minutes et sont envoyées plus rapidement, donc environ toutes les 10 à 15 minutes jusqu’à ce que tous les enregistrements aient été traités. S’il n’y a pas suffisamment d’enregistrements pour constituer un lot de 10 000, le nombre d’enregistrements actuels est envoyé tel quel lorsque le délai limite est atteint, de sorte que vous pouvez également voir des lots plus petits envoyés à Facebook.

Prenons un autre exemple, la [destination de l’API HTTP](/help/destinations/catalog/streaming/http-destination.md), qui a une politique *[d’agrégation de meilleurs effots](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)*, avec `maxUsersPerRequest: 10`. Cela signifie qu’un maximum de dix profils seront agrégés avant qu’un appel HTTP ne soit déclenché vers cette destination, mais Experience Platform tente d’envoyer des profils vers la destination dès que le service de destinations reçoit des informations de réévaluation mises à jour d’un service en amont.

La politique d’agrégation est configurable et les développeurs de destination peuvent décider comment la configurer pour respecter au mieux les limites de taux des points d’entrée de l’API en aval. Obtenez des informations supplémentaires sur la [politique d’agrégation](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) dans la documentation de Destination SDK.

## Destinations d&#39;exportation de profils de streaming (entreprise) {#streaming-profile-destinations}

>[!IMPORTANT]
>
> Les destionations d’entreprise sont disponibles uniquement pour la clientèle d’[Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html).

Les [destinations d’entreprise](/help/destinations/destination-types.md#streaming-profile-export) dans Experience Platform sont Amazon Kinesis, Azure Event Hubs et l’API HTTP.

Experience Platform optimise le comportement d’exportation de profils vers votre destination d’entreprise afin de n&#39;exporter des données vers votre point d’entrée API que lorsque des mises à jour pertinentes d&#39;un profil ont eu lieu suite à la qualification d&#39;un segment ou à d&#39;autres événements importants. Les profils sont exportés vers votre destination dans les situations suivantes :

* La mise à jour du profil a été déterminée par une modification de l’[appartenance à un segment](/help/xdm/field-groups/profile/segmentation.md) pour au moins un des segments mappés à la destination. Par exemple, le profil est qualifié pour l’un des segments mappés à la destination ou a quitté l’un de ces segments.
* La mise à jour du profil a été déterminée par une modification dans le [mappage d’identités](/help/xdm/field-groups/profile/identitymap.md). Par exemple, une nouvelle identité a été ajoutée dans l’attribut de mappage d’identités à un profil qui était déjà qualifié pour l’un des segments mappés à la destination.
* La mise à jour du profil a été déterminée par une modification des attributs pour au moins un des attributs mappés à la destination. Par exemple, l’un des attributs mappés à la destination dans l’étape de mappage est ajouté à un profil.

Dans tous les cas décrits ci-dessus, seuls les profils pour lesquels des mises à jour pertinentes se sont produites sont exportés vers votre destination. Par exemple, si un segment mappé au flux de destination comporte cent membres et que cinq nouveaux profils sont qualifiés pour ce segment, l’exportation vers votre destination est incrémentielle et inclut uniquement les cinq nouveaux profils.

Notez que tous les attributs mappés sont exportés pour un profil, quel que soit l’emplacement des modifications. Ainsi, dans l’exemple ci-dessus, tous les attributs mappés pour ces cinq nouveaux profils seront exportés même si les attributs eux-mêmes restent inchangés.

### Ce qui détermine une exportation de données et ce qui est inclus dans l’exportation.

Concernant les données exportées pour un profil donné, il est important de comprendre les deux concepts différents entre *ce qui détermine l’exportation de données vers votre destination d’entreprise* et *quelles données sont incluses dans l’exportation*.

| Ce qui détermine une exportation de destination | Éléments inclus dans l’exportation de destination |
|---------|----------|
| <ul><li>Les attributs et segments mappés servent de repère pour une exportation de destination. Cela signifie que si des segments mappés changent d’états (à partir de `null` to `realized` ou de `realized` to `exiting`) ou si les attributs mappés sont mis à jour, une exportation de destination est déclenchée.</li><li>Comme les identités ne peuvent actuellement pas être mappées aux destinations d’entreprise, les modifications d’identité sur un profil donné déterminent également les exportations de destination.</li><li>Toute modification pour un attribut est considérée comme une mise à jour, qu’il s’agisse ou non de la même valeur. Cela signifie qu’une réécriture sur un attribut est considérée comme une modification, même si la valeur elle-même n’a pas changé.</li></ul> | <ul><li>L’objet `segmentMembership` inclut le segment mappé dans le flux de données d’activation, pour lequel le statut du profil a changé suite à un événement de qualification ou de sortie de segment. Notez que d’autres segments non mappés pour lesquels le profil s’est qualifié peuvent faire partie de l’exportation de destination, si ces segments appartiennent à la même [politique de fusion](/help/profile/merge-policies/overview.md) que le segment mappé dans le flux de données d’activation. </li><li>Toutes les identités dans l’objet `identityMap` sont également incluses (Experience Platform ne prend actuellement pas en charge le mappage d’identités dans la destination d’entreprise).</li><li>Seuls les attributs mappés sont inclus dans l’exportation de destination.</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>Les destinations d’entreprise diffusent des données de renvoi lors de l’activation de profils vers une destination. Cela signifie que la première exportation de données après la configuration d’un workflow d’activation vers une destination inclut les profils qualifiés pour le segment activé avant que le segment ne soit mappé à la destination.

>[!BEGINSHADEBOX]

Prenons l’exemple d’un flux de données vers une destination HTTP dans lequel trois segments sont sélectionnés et quatre attributs sont mappés à la destination.

![flux de données de destination d’entreprise](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Une exportation de profil vers la destination peut être déterminée par un profil éligible ou sortant de l’un des *trois segments mappés*. Toutefois, au cours de l’exportation des données, dans l’objet `segmentMembership`, d’autres segments non mappés peuvent apparaître si ce profil spécifique en est membre et s’ils partagent la même politique de fusion que le segment qui a déclenché l’exportation. Si un profil est qualifié pour le segment **Client avec des voitures DeLorean**, mais qu’il est également membre des segments **Film « Retour vers le futur » visionné** et **Fans de science-fiction**, alors ces deux autres segments seront aussi présents dans l’objet `segmentMembership` de l’exportation des données, même s’ils ne sont pas mappés dans le flux de données, si ceux-ci partagent la même politique de fusion que le segment **Client avec des voitures DeLorean**.

Du point de vue des attributs de profil, toute modification apportée aux quatre attributs mappés ci-dessus déterminera une exportation de destination et chacun de ces quatre attributs mappés et présents sur le profil sera présent dans l’exportation des données.

>[!ENDSHADEBOX]

>[!TIP]
>
> Vous pouvez consulter des exemples de données exportées vers différentes destinations d’entreprise dans les pages de documentation sur les destinations [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md#exported-data), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md#exported-data) et [API HTTP](/help/destinations/catalog/streaming/http-destination.md#exported-data).

## Destinations basées sur les API de streaming {#streaming-api-based-destinations}

Le comportement d’exportation des profils pour les destinations de streaming telles que Facebook, Trade Desk et d’autres intégrations basées sur les API est très similaire au comportement décrit ci-dessus pour les destinations d’entreprise.

Les destinations appartenant aux [catégories sociales et publicitaires](/help/destinations/destination-types.md#categories) du catalogue sont des exemples de destinations de streaming.

Experience Platform optimise le comportement d’exportation des profils vers votre destination de streaming afin d’exporter les données vers les destinations basées sur les API de streaming uniquement quand des mises à jour importantes d’un profil se sont produites à la suite d’une qualification de segment ou d’autres événements significatifs. Les profils sont exportés vers votre destination dans les situations suivantes :

* La mise à jour du profil a été déterminée par une modification de l’[appartenance à un segment](/help/xdm/field-groups/profile/segmentation.md) pour au moins un des segments mappés à la destination. Par exemple, le profil est qualifié pour l’un des segments mappés à la destination ou a quitté l’un de ces segments.
* La mise à jour du profil a été déterminée par une modification du [mappage d’identités](/help/xdm/field-groups/profile/identitymap.md) pour un espace de noms d’identité marqué pour l’exportation pour cette instance de destination. Par exemple, une nouvelle identité a été ajoutée dans l’attribut de mappage d’identités à un profil qui était déjà qualifié pour l’un des segments mappés à la destination.
* La mise à jour du profil a été déterminée par une modification des attributs pour au moins un des attributs mappés à la destination. Par exemple, l’un des attributs mappés à la destination dans l’étape de mappage est ajouté à un profil.
* Modifications du consentement pour un profil lorsque l’application automatisée du consentement est configurée et qu’un profil choisit de s’y opposer. L’application automatisée du consentement envoie un événement de sortie d’audience à la destination, afin que le profil ne soit inclus dans aucun ciblage à la destination.

Dans tous les cas décrits ci-dessus, seuls les profils pour lesquels des mises à jour pertinentes se sont produites sont exportés vers votre destination. Par exemple, si un segment mappé au flux de destination comporte cent membres et que cinq nouveaux profils sont qualifiés pour ce segment, l’exportation vers votre destination est incrémentielle et inclut uniquement les cinq nouveaux profils.

Notez que tous les attributs mappés sont exportés pour un profil, quel que soit l’emplacement des modifications. Ainsi, dans l’exemple ci-dessus, tous les attributs mappés pour ces cinq nouveaux profils seront exportés même si les attributs eux-mêmes restent inchangés.

### Ce qui détermine une exportation de données et ce qui est inclus dans l’exportation.

Concernant les données exportées pour un profil donné, il est important de comprendre les deux concepts différents entre ce qui détermine l’exportation de données vers votre destination d’API de streaming et les données incluses dans l’exportation.

| Ce qui détermine une exportation de destination | Éléments inclus dans l’exportation de destination |
|---------|----------|
| <ul><li>Les attributs et segments mappés servent de repère pour une exportation de destination. Cela signifie que si des segments mappés changent d’états (à partir de `null` to `realized` ou de `realized` to `exiting`) ou si les attributs mappés sont mis à jour, une exportation de destination est déclenchée.</li><li>La modification du mappage d’identités correspond à une identité ajoutée/supprimée pour le [graphique d’identités](/help/identity-service/ui/identity-graph-viewer.md) du profil, pour les espaces de noms d’identité mappés pour l’exportation.</li><li>La modification d’un attribut correspond à toute mise à jour de l’attribut, pour les attributs mappés à la destination.</li></ul> | <ul><li>Les segments qui sont mappés à la destination et qui ont été modifiés seront inclus dans l’objet `segmentMembership`. Dans certains scénarios, ils peuvent être exportés à l’aide de plusieurs appels. En outre, dans certains scénarios, certains segments qui n’ont pas été modifiés peuvent également être inclus dans l’appel. Dans tous les cas, seuls les segments mappés seront exportés.</li><li>Toutes les identités des espaces de noms qui sont mappés à la destination dans l’objet `identityMap` sont également inclus.</li><li>Seuls les attributs mappés sont inclus dans l’exportation de destination.</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>Les destinations d’API de diffusion en continu diffusent les données de renvoi lors de l’activation de profils vers une destination. Cela signifie que la première exportation de données après la configuration d’un workflow d’activation vers une destination inclut les profils qualifiés pour le segment activé avant que le segment ne soit mappé à la destination.

>[!BEGINSHADEBOX]

Prenons l’exemple de ce flux de données vers une destination de diffusion en continu où trois segments sont sélectionnés dans le flux de données.

![flux de données de destination de diffusion en continu](/help/destinations/assets/how-destinations-work/streaming-destination-example-dataflow.png)

Une exportation de profil vers la destination peut être déterminée par un profil éligible ou sortant de l’un des trois segments mappés. Si un profil est qualifié pour le segment **Client avec des voitures DeLorean**, cela déclenche une exportation. Les autres segments (**Ville - Dallas** et **Principal de base du site**) peut également être exporté si le segment est présent dans le profil avec l’un des états possibles (`realized` ou `exited`). Les segments non mappés (comme **Fans de science-fiction**) ne sont pas exportés.

Du point de vue des attributs de profil, toute modification des trois attributs mappés ci-dessus déterminera une exportation de destination.

>[!ENDSHADEBOX]

## Destinations de lot (basées sur des fichiers) {#file-based-destinations}

Lors de l’exportation de profils vers des [destinations basées sur des fichiers](/help/destinations/destination-types.md#file-based) dans Experience Platform, vous pouvez utiliser trois types de plannings (répertoriés ci-dessous) et deux options d’exportation de fichiers (fichiers complets ou incrémentiels). Tous ces paramètres sont définis au niveau du segment, même lorsque plusieurs segments sont mappés à un seul flux de données de destination.

* Exports planifiés : configurez une destination, ajoutez un ou plusieurs segments, puis choisissez si vous souhaitez exporter des fichiers complets ou incrémentiels. Sélectionnez ensuite une heure précise chaque jour ou plusieurs fois par jour à laquelle les fichiers doivent être exportés. Par exemple, une heure d’exportation de 17 heures signifie que les profils qualifiés pour le segment seront exportés à 17 heures.
* Après l’évaluation du segment : l’exportation est déclenchée immédiatement après l’exécution de le traitement d’évaluation de segment quotidien. Cela signifie que les numéros de profil exportés dans le fichier sont aussi proches que possible de la dernière population évaluée du segment.
* Exportations à la demande ([exporter le fichier maintenant](/help/destinations/ui/export-file-now.md)) : en fonction du dernier traitement d’évaluation de segment, un fichier complet est exporté une fois de plus que les exportations régulièrement planifiées.

Dans l’une des situations d’exportation ci-dessus, les fichiers exportés incluent les profils qualifiés pour l’exportation, ainsi que les colonnes que vous avez sélectionnées en tant qu’attributs XDM pour l’exportation.

>[!TIP]
>
>Lorsqu’un segment en flux continu est mappé à une destination par lots, il est plus probable que le nombre de profils dans le fichier exporté soit plus proche du nombre d’utilisateurs et d’utilisatrices dans le segment. En effet, il y a plus de chances que la dernière évaluation de segment se rapproche de l’heure d’exportation.

### Exportations de fichiers incrémentiels {#incremental-file-exports}

Toutes les mises à jour d’un profil n’entraînent pas l’inclusion de celui-ci dans les exportations de fichiers incrémentiels. Par exemple, si un attribut a été ajouté à un profil ou supprimé de celui-ci, le profil n’est pas inclus dans l’exportation. Seuls les profils pour lesquels l’attribut `segmentMembership` a changé sera inclus dans les fichiers exportés. En d’autres termes, ce n’est que si le profil fait partie du segment ou est supprimé du segment qu’il est inclus dans les exportations de fichiers incrémentiels.

De même, si une nouvelle identité (nouvelle adresse e-mail, numéro de téléphone, ECID, etc.) est ajoutée à un profil dans le [graphique d’identité](/help/identity-service/ui/identity-graph-viewer.md), cela ne représente pas une raison d’inclure le profil dans une nouvelle exportation de fichiers incrémentiels.

Si un nouveau segment est ajouté à un mappage de destination, cela n’a aucune incidence sur les qualifications et les exportations pour un autre segment. Les plannings d’exportation sont configurés individuellement par segment et les fichiers sont exportés séparément pour chaque segment, même si les segments ont été ajoutés au même flux de données de destination.

>[!BEGINSHADEBOX]

Par exemple, dans le paramètre d’exportation illustré ci-dessous, dans lequel un segment exporte des mises à jour de fichiers incrémentiels, notez les circonstances suivantes selon lesquelles un profil est inclus ou non dans une exportation de fichiers incrémentiels :

![Paramètre d’exportation avec plusieurs attributs sélectionnés.](/help/destinations/assets/how-destinations-work/export-selection-batch-destination.png)

* Un profil est inclus dans une exportation de fichiers incrémentiels qu’il remplisse ou pas les critères pour le segment.
* Un profil n’est *pas* inclus dans une exportation de fichiers incrémentiels lorsqu’un nouveau numéro de téléphone est ajouté au graphique d’identité.
* Un profil n’est *pas* inclus dans une exportation de fichiers incrémentiels lorsque la valeur de l’un des champs XDM mappés, comme `xdm: loyalty.points`, `xdm: loyalty.tier`, `xdm: personalEmail.address` est mise à jour sur un profil.
* Lorsque le champ XDM `segmentMembership.status` est mappé dans le workflow d’activation de destination, les profils qui sortent du segment sont également inclus dans les fichiers incrémentiels exportés, avec un statut `exited`.

>[!ENDSHADEBOX]

### Ce qui détermine une exportation de données et ce qui est inclus dans l’exportation.

Selon les informations de la section ci-dessus, le comportement d’exportation de profils vers les destinations basées sur des fichiers peut être résumé comme suit :

**Exportations de fichiers complets**

La totalité de la population active du segment est exportée tous les jours.

| Ce qui détermine une exportation de destination | Éléments inclus dans le fichier exporté |
|---------|----------|
| <ul><li>Le planning d’exportation défini dans l’interface utilisateur ou l’API et l’action de l’utilisateur ou de l’utilisatrice (qui sélectionne [Exporter le fichier maintenant](/help/destinations/ui/export-file-now.md) dans l’IU ou qui utilise l’[API d’activation ad hoc](/help/destinations/api/ad-hoc-activation-api.md)) déterminent le début d’une exportation de destination.</li></ul> | Dans les exportations de fichiers complets, tous des profils actifs d’un segment, selon la dernière évaluation de segment, sont inclus dans chaque exportation de fichiers. Les dernières valeurs pour chaque attribut XDM sélectionné pour l’exportation sont également incluses en tant que colonnes dans chaque fichier. Notez que les profils à l’état de sortie ne sont pas inclus dans l’exportation du fichier. |

{style="table-layout:fixed"}

**Exportations de fichiers incrémentiels**

Dans la première exportation de fichiers, après avoir configuré le workflow d&#39;activation, la population intégrale du segment est exportée. Lors des exportations suivantes, seuls les profils modifiés sont exportés.

| Ce qui détermine une exportation de destination | Éléments inclus dans le fichier exporté |
|---------|----------|
| <ul><li>Le planning d’exportation défini dans l’interface utilisateur ou l’API détermine le début d’une exportation de destination.</li><li>Toute modification de l’appartenance à un segment d’un profil, qu’il remplisse les critères pour le segment ou non, qualifie un profil pour être inclus dans les exportations incrémentielles. Les modifications des attributs ou des mappages d’identité d’un profil ne qualifient *pas* un profil pour qu’il soit inclus dans les exportations incrémentielles.</li></ul> | <p>Les profils pour lesquels l’appartenance au segment a changé, ainsi que les informations les plus récentes pour chaque attribut XDM sélectionné pour l’exportation.</p><p>Les profils à l’état de sortie sont inclus dans les exportations de destination si le champ XDM `segmentMembership.status` est sélectionné à l’étape de mappage.</p> |

{style="table-layout:fixed"}

>[!TIP]
>
>Pour rappel, les modifications apportées aux valeurs d’attribut ou aux mappages d’identité d’un profil ne qualifie pas un profil pour qu’il soit inclus dans une exportation de fichier incrémentiel.

## Étapes suivantes {#next-steps}

Après avoir lu ce document, vous savez maintenant à quoi vous attendre dans les exportations de profils vers des destinations en flux continu, d’entreprise et basées sur des fichiers.

Vous pouvez ensuite découvrir comment [les identités sont gérées](/help/destinations/how-destinations-work/identity-handling.md) dans le workflow d’activation.
