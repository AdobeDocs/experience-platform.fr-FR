---
title: Présentation de l’extension AWS
description: Découvrez l’extension AWS pour le transfert d’événement dans Adobe Experience Platform.
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 8%

---

# [!DNL AWS] présentation de l’extension

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) est une plateforme de cloud computing qui offre un large éventail de services tels que l’informatique distribuée, le stockage de base de données, la diffusion de contenu et la gestion de la relation client (CRM).

Le [!DNL AWS] [transfert d’événement](../../../ui/event-forwarding/overview.md) les leviers d’extension [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) pour envoyer des événements depuis Adobe Experience Platform Edge Network vers [!DNL AWS] pour un traitement ultérieur. Ce guide explique comment installer l’extension et utiliser ses fonctionnalités dans une règle de transfert d’événement.

## Conditions préalables

Vous devez disposer d’un [!DNL AWS] compte avec un compte existant [!DNL Kinesis] flux de données afin d’utiliser cette extension. Si vous ne disposez pas d’un flux de données préexistant, reportez-vous à la section [!DNL AWS] documentation sur [création d’un nouveau flux de données à l’aide de la fonction [!DNL AWS] Console de gestion](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## Installer l’extension {#install}

Pour installer le [!DNL AWS] , accédez à l’interface utilisateur de la collecte de données ou à l’interface utilisateur Experience Platform et sélectionnez **[!UICONTROL Transfert d’événement]** dans le volet de navigation de gauche. À partir de là, sélectionnez une propriété à laquelle ajouter l’extension ou créez une propriété à la place.

Une fois que vous avez sélectionné ou créé la propriété souhaitée, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, puis sélectionnez l’option **[!UICONTROL Catalogue]** . Recherchez le [!UICONTROL AWS] carte, puis sélectionnez **[!UICONTROL Installer]**.

![Le [!UICONTROL Installer] sélectionné pour l’option [!UICONTROL AWS] dans l’interface utilisateur de la collecte de données.](../../../images/extensions/server/aws/install.png)

Sur l’écran suivant, vous devez fournir les informations d’identification de connexion pour votre [!DNL AWS] compte . Plus précisément, vous devez fournir vos [!DNL AWS] Identifiant de la clé d&#39;accès et clé d&#39;accès secrète. Si vous ne connaissez pas ces valeurs, reportez-vous à la section [!DNL AWS] documentation sur [Comment obtenir votre identifiant de clé d’accès et votre clé d’accès secrète](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![L’identifiant de la clé d’accès et la clé d’accès secrète ont été ajoutés dans la vue de configuration de l’extension.](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>Une stratégie d’accès doit être jointe à la variable [!DNL AWS] compte utilisé pour générer les informations d’identification d’accès. Cette stratégie doit être configurée pour accorder des droits d’accès pour envoyer des données à la variable [!DNL Kinesis] flux de données. Voir **Exemple 2** dans le [!DNL AWS] document on [exemples de stratégies pour [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) pour voir comment la stratégie doit être définie.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]** et l’extension est installée.

## Configurer une règle de transfert d’événement {#rule}

Après l’installation de l’extension, créez un transfert d’événement. [règle](../../../ui/managing-resources/rules.md) et configurez ses conditions selon vos besoins. Lors de la configuration des actions de la règle, sélectionnez l’événement **[!UICONTROL AWS]** extension, puis sélectionnez **[!UICONTROL Envoi de données au flux de données Kinesis]** pour le type d’action.

![Le [!UICONTROL Envoi de données au flux de données Kinesis] type d’action sélectionné pour une règle dans l’interface utilisateur de la collecte de données.](../../../images/extensions/server/aws/select-action-type.png)

Le panneau de droite se met à jour afin d’afficher les options de configuration permettant d’envoyer les données. Plus précisément, vous devez affecter [éléments de données](../../../ui/managing-resources/data-elements.md) aux différentes propriétés qui représentent votre [!DNL Event Hub] configuration.

![Les options de configuration de la variable [!UICONTROL Envoi de données au flux de données Kinesis] type d’action affiché dans l’interface utilisateur.](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Détails du flux de données Kinesis]**

| Entrée | Description |
| --- | --- |
| [!UICONTROL Nom de la diffusion] | Le nom du flux vers lequel cette règle de transfert d’événement enverra des enregistrements de données. |
| [!UICONTROL Région AWS] | Le [!DNL AWS] région dans laquelle la variable [!DNL Kinesis] le flux de données est créé. |
| [!UICONTROL Clé de partition] | Le [clé de partition](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) que l’extension utilisera lors de l’envoi de données au flux de données.<br><br>[!DNL Kinesis Data Streams] sépare les enregistrements de données appartenant à un flux en plusieurs éclats. Elle utilise la clé de partition envoyée avec chaque enregistrement de données pour déterminer à quel partage appartient un enregistrement de données donné.<br><br>Une bonne clé de partition pour distribuer les clients peut être le numéro de client, car il est différent pour chaque client. Une mauvaise clé de partition peut leur code postal car ils peuvent tous se trouver dans la même zone à proximité. En règle générale, vous devez choisir une clé de partition ayant la plus grande plage de valeurs potentielles différentes. Voir [!DNL AWS] article sur [effectuez une mise à l’échelle [!DNL Kinesis] flux de données](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) pour connaître les bonnes pratiques en matière de gestion des clés de partition. |

{style=&quot;table-layout:auto&quot;}

**[!UICONTROL Data]** (Données)

| Entrée | Description |
| --- | --- |
| [!UICONTROL Payload] | Ce champ contient les données qui seront transférées à la variable [!DNL Kinesis] flux de données, au format JSON.<br><br>Sous , **[!UICONTROL Brut]** , vous pouvez coller l’objet JSON directement dans le champ de texte fourni ou sélectionner l’icône d’élément de données (![Icône Jeu de données](../../../images/extensions/server/aws/data-element-icon.png)) pour effectuer une sélection dans une liste d’éléments de données existants afin de représenter la charge utile.<br><br>Vous pouvez également utiliser la variable **[!UICONTROL Éditeur de paires clé-valeur JSON]** pour ajouter manuellement chaque paire clé-valeur par le biais d’un éditeur d’interface utilisateur. Chaque valeur peut être représentée par une entrée brute ou un élément de données peut être sélectionné à la place. |

{style=&quot;table-layout:auto&quot;}

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Conserver les modifications]** pour ajouter l’action à la configuration de la règle. Lorsque la règle vous satisfait, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.

Enfin, publiez un nouveau transfert d’événement. [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Étapes suivantes

Ce guide explique comment envoyer des données à [!DNL Kinesis Data Streams] en utilisant la variable [!DNL AWS] extension de transfert d’événement. Pour plus d’informations sur les fonctionnalités de transfert d’événement dans Experience Platform, reportez-vous à la section [transfert d’événement - Aperçu](../../../ui/event-forwarding/overview.md).
