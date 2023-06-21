---
title: Extension de transfert d’événements de la plateforme Google Cloud
description: Cette extension de transfert d’événement Adobe Experience Platform envoie les événements Adobe Experience Edge Network à Google Cloud Platform.
last-substantial-update: 2023-06-21T00:00:00Z
source-git-commit: d1a34a98efd24a20dc53544eeb0d79490aaf31e7
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 3%

---

# Extension de transfert d’événement [!DNL Google Cloud Platform]

[[!DNL Google Cloud Platform]](https://cloud.google.com/) est une plateforme de cloud computing qui offre un large éventail de services tels que l’informatique distribuée, le stockage de base de données, la diffusion de contenu et les services d’intégration de logiciels en tant que service (SaaS) pour la gestion de la relation client (CRM) et la planification des ressources de l’entreprise (ERP).

Le [!DNL Google Cloud Platform] [transfert d’événement](../../../ui/event-forwarding/overview.md) les leviers d’extension [[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub) pour envoyer des événements du réseau Adobe Experience Platform Edge au [!DNL Google Cloud Platform] pour un traitement ultérieur. Ce guide explique comment installer l’extension et utiliser ses fonctionnalités dans une règle de transfert d’événement.

## Conditions préalables

Pour utiliser cette extension, vous devez disposer d’un [!DNL Google Cloud Platform] compte avec un compte existant [!DNL Cloud Pub/Sub] rubrique. Si vous ne disposez pas d’un flux de données préexistant, reportez-vous à la section [!DNL AWS] documentation sur [création d’un nouveau flux de données à l’aide de la fonction [!DNL AWS] Console de gestion](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

### Création d’un secret et d’un élément de données

Tout d’abord, créez un `Google OAuth 2` [secret de transfert d’événement](../../../ui/event-forwarding/secrets.md), qui sera utilisé pour authentifier la connexion à votre compte tout en gardant la valeur sécurisée.

Ensuite, [créer un élément de données ;](../../../ui/managing-resources/data-elements.md#create-a-data-element) en utilisant la variable **[!UICONTROL Core]** et une **[!UICONTROL Secret]** type d’élément de données pour référencer la variable `Google OAuth 2` secret que vous venez de créer.

## Installez et configurez le [!DNL Google Cloud Platform] extension {#install}

Pour installer l’extension, [création d’une propriété de transfert d’événement](../../../ui/event-forwarding/overview.md#properties) ou choisissez une propriété existante à modifier.

Sélectionner **[!UICONTROL Extensions]** dans le volet de navigation de gauche. Dans le **[!UICONTROL Catalogue]** onglet, sélectionnez **[!UICONTROL Installer]** sur la carte de la variable [!DNL Google Cloud Platform] extension .

![Le catalogue [!DNL Google Cloud Platform] installation de mise en surbrillance de l’extension.](../../../images/extensions/server/google-cloud-platform/install-extension.png)

Dans l’écran de configuration, saisissez le secret de l’élément de données que vous avez créé précédemment dans le champ **[!UICONTROL Jeton d’accès]** champ . Le secret de l’élément de données contiendra votre [!DNL Google Cloud Platform] Jeton OAuth 2. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Enregistrer]**.

![Le [!DNL Google Cloud Platform] page de configuration de l’extension.](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## Créez un [!DNL Send Data to Cloud Pub/Sub] règle {#tracking-rule}

Une fois l’extension installée, créez un transfert d’événement. [règle](../../../ui/managing-resources/rules.md) et configurez ses conditions selon vos besoins. Lors de la configuration des actions de la règle, sélectionnez l’événement **[!UICONTROL Google Cloud Platform]** extension, puis sélectionnez **[!UICONTROL Envoyer des données à Cloud Pub/Sub]** pour le type d’action.

![La vue de configuration des actions pour [!UICONTROL Google Cloud Platform], avec l’action mise en surbrillance et [!UICONTROL Envoyer des données à Cloud Pub/Sub].](../../../images/extensions/server/google-cloud-platform/event-action.png)

| Entrée | Description |
| --- | --- |
| [!UICONTROL Rubrique] | Rubrique qui recevra les événements du transfert d’événement. La valeur doit avoir le format `projects/{projectName}/topics/{topicName}`. |
| [!UICONTROL Data] (Données) | Ce champ contient les données à transférer au [!DNL Cloud Pub/Sub] rubrique au format JSON.<br><br>Sous , **[!UICONTROL Brut]** , vous pouvez coller l’objet JSON directement dans le champ de texte fourni ou sélectionner l’icône d’élément de données (![Icône Jeu de données](../../../images/extensions/server/aws/data-element-icon.png)) pour effectuer une sélection dans une liste d’éléments de données existants afin de représenter les données.<br><br>Vous pouvez également utiliser la variable **[!UICONTROL Éditeur de paires clé-valeur JSON]** pour ajouter manuellement chaque paire clé-valeur par le biais d’un éditeur d’interface utilisateur. Chaque valeur peut être représentée par une entrée brute ou un élément de données peut être sélectionné à la place. |
| [!UICONTROL Attributs] | Ce champ contient l’objet JSON avec des attributs supplémentaires à envoyer avec le message.<br><br>Sous , **[!UICONTROL Brut]** , vous pouvez coller l’objet JSON directement dans le champ de texte fourni ou sélectionner l’icône d’élément de données (![Icône Jeu de données](../../../images/extensions/server/aws/data-element-icon.png)) pour effectuer une sélection dans une liste d’éléments de données existants afin de représenter les données.<br><br>Vous pouvez également utiliser la variable **[!UICONTROL Éditeur de paires clé-valeur JSON]** pour ajouter manuellement chaque paire clé-valeur par le biais d’un éditeur d’interface utilisateur. Chaque valeur peut être représentée par une entrée brute ou un élément de données peut être sélectionné à la place. |

{style="table-layout:auto"}

## Étapes suivantes

Ce guide explique comment envoyer des données à [!DNL Cloud Pub/Sub] en utilisant la variable [!DNL Google Cloud Platform] extension de transfert d’événement. Pour plus d’informations sur les fonctionnalités de transfert d’événement dans Experience Platform, reportez-vous à la section [transfert d’événement - Aperçu](../../../ui/event-forwarding/overview.md).