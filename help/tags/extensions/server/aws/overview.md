---
title: Présentation de l’extension AWS
description: Découvrez l’extension AWS pour le transfert d’événement dans Adobe Experience Platform.
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 7%

---

# Présentation de l’extension [!DNL AWS]

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) est une plateforme de cloud computing qui offre un large éventail de services tels que l’informatique distribuée, le stockage de base de données, la diffusion de contenu et les services d’intégration de logiciels en tant que service (SaaS) pour la gestion de la relation client (CRM) et la planification des ressources de l’entreprise (ERP).

L’extension [!DNL AWS] [de transfert d’événement](../../../ui/event-forwarding/overview.md) exploite [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) pour envoyer des événements de l’Edge Network Adobe Experience Platform vers [!DNL AWS] en vue d’un traitement ultérieur. Ce guide explique comment installer l’extension et utiliser ses fonctionnalités dans une règle de transfert d’événement.

## Conditions préalables

Pour utiliser cette extension, vous devez disposer d’un compte [!DNL AWS] avec un flux de données [!DNL Kinesis] existant. Si vous ne disposez pas d’un flux de données préexistant, reportez-vous à la documentation [!DNL AWS] sur la [création d’un nouveau flux de données à l’aide de la [!DNL AWS] console de gestion](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## Installation l’extension {#install}

Pour installer l’extension [!DNL AWS], accédez à l’interface utilisateur de collecte de données ou à l’interface utilisateur Experience Platform et sélectionnez **[!UICONTROL Transfert d’événement]** dans le volet de navigation de gauche. À partir de là, sélectionnez une propriété à laquelle ajouter l’extension ou créez une propriété à la place.

Une fois que vous avez sélectionné ou créé la propriété souhaitée, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Catalogue]** . Recherchez la carte [!UICONTROL AWS], puis sélectionnez **[!UICONTROL Installer]**.

![Bouton [!UICONTROL Installer] sélectionné pour l’extension [!UICONTROL AWS] dans l’interface utilisateur de la collecte de données.](../../../images/extensions/server/aws/install.png)

Sur l’écran suivant, vous devez fournir les informations d’identification de connexion pour votre compte [!DNL AWS]. Plus précisément, vous devez fournir votre ID de clé d’accès [!DNL AWS] et votre clé d’accès secrète. Si vous ne connaissez pas ces valeurs, consultez la documentation [!DNL AWS] sur [ comment obtenir votre ID de clé d&#39;accès et votre clé d&#39;accès secrète](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![ L&#39;identifiant de la clé d&#39;accès et la clé d&#39;accès secrète ajoutés dans la vue de configuration de l&#39;extension.](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>Une stratégie d’accès doit être jointe au compte [!DNL AWS] utilisé pour générer les informations d’identification d’accès. Cette stratégie doit être configurée pour accorder des droits d’accès pour envoyer des données au flux de données [!DNL Kinesis]. Reportez-vous à **Exemple 2** dans le document [!DNL AWS] sur [exemples de stratégies pour [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) pour voir comment la stratégie doit être définie.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Save]** et l’extension est installée.

## Configurer une règle de transfert d’événement {#rule}

Après avoir installé l’extension, créez un transfert d’événement [rule](../../../ui/managing-resources/rules.md) et configurez ses conditions selon vos besoins. Lors de la configuration des actions pour la règle, sélectionnez l’extension **[!UICONTROL AWS]**, puis sélectionnez **[!UICONTROL Envoyer les données au flux de données Kinesis]** pour le type d’action.

![Le type d’action [!UICONTROL Envoyer des données au flux de données Kinesis] est sélectionné pour une règle dans l’interface utilisateur de collecte de données.](../../../images/extensions/server/aws/select-action-type.png)

Le panneau de droite se met à jour afin d’afficher les options de configuration permettant d’envoyer les données. Plus précisément, vous devez affecter des [éléments de données](../../../ui/managing-resources/data-elements.md) aux différentes propriétés qui représentent votre configuration [!DNL Event Hub].

![ Les options de configuration pour le type d’action [!UICONTROL Envoyer des données au flux de données Kinesis] affiché dans l’interface utilisateur.](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Détails du flux de données Kinesis]**

| Entrée | Description |
| --- | --- |
| [!UICONTROL Nom du flux] | Le nom du flux vers lequel cette règle de transfert d’événement enverra des enregistrements de données. |
| [!UICONTROL Région AWS] | Région [!DNL AWS] où le flux de données [!DNL Kinesis] est créé. |
| [!UICONTROL Clé de partition] | [clé de partition](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) que l’extension utilisera lors de l’envoi de données au flux de données.<br><br>[!DNL Kinesis Data Streams] divise les enregistrements de données appartenant à un flux en plusieurs partages. Elle utilise la clé de partition envoyée avec chaque enregistrement de données pour déterminer à quel partage appartient un enregistrement de données donné.<br><br>Une bonne clé de partition pour distribuer les clients peut être le numéro de client, car il est différent pour chaque client. Une mauvaise clé de partition peut leur code postal car ils peuvent tous se trouver dans la même zone à proximité. En règle générale, vous devez choisir une clé de partition ayant la plus grande plage de valeurs potentielles différentes. Consultez l’article [!DNL AWS] sur la [mise à l’échelle de vos  [!DNL Kinesis] flux de données](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) pour connaître les bonnes pratiques en matière de gestion des clés de partition. |

{style="table-layout:auto"}

**[!UICONTROL Data]** (Données)

| Entrée | Description |
| --- | --- |
| [!UICONTROL Charge utile] | Ce champ contient les données qui seront transférées vers le flux de données [!DNL Kinesis], au format JSON.<br><br>Sous l’option **[!UICONTROL Brut]**, vous pouvez coller l’objet JSON directement dans le champ de texte fourni, ou vous pouvez sélectionner l’icône d’élément de données (![Icône Jeu de données](/help/images/icons/database.png)) pour effectuer une sélection dans une liste d’éléments de données existants pour représenter la charge utile.<br><br>Vous pouvez également utiliser l’option **[!UICONTROL Éditeur de paires clé-valeur JSON]** pour ajouter manuellement chaque paire clé-valeur via un éditeur d’interface utilisateur. Chaque valeur peut être représentée par une entrée brute ou un élément de données peut être sélectionné à la place. |

{style="table-layout:auto"}

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Conserver les modifications]** pour ajouter l’action à la configuration de la règle. Lorsque la règle vous satisfait, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.

Enfin, publiez un nouveau transfert d’événement [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Étapes suivantes

Ce guide explique comment envoyer des données à [!DNL Kinesis Data Streams] à l’aide de l’extension de transfert d’événement [!DNL AWS]. Pour plus d’informations sur les fonctionnalités de transfert d’événement en Experience Platform, consultez la [présentation du transfert d’événement](../../../ui/event-forwarding/overview.md).
