---
keywords: e-mail;e-mail;destinations d’e-mail;sendgrid;destination sendgrid
title: Connexion à SendGrid
description: La destination SendGrid vous permet d’exporter vos données propriétaires et de les activer dans SendGrid en fonction des besoins de votre entreprise.
exl-id: 6f22746f-2043-4a20-b8a6-097d721f2fe7
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '1475'
ht-degree: 7%

---

# Connexion [!DNL SendGrid]

## Présentation {#overview}

[SendGrid](https://www.sendgrid.com) est une plateforme de communication client populaire pour les emails transactionnels et marketing.

Ceci [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) tire parti de [[!DNL SendGrid Marketing Contacts API]](https://api.sendgrid.com/v3/marketing/contacts), qui vous permet d’exporter vos profils de messagerie propriétaires et de les activer dans un nouveau segment SendGrid en fonction des besoins de votre entreprise.

SendGrid utilise des jetons de support d’API comme mécanisme d’authentification pour communiquer avec l’API SendGrid.

## Conditions préalables {#prerequisites}

Les éléments suivants sont requis avant de commencer à configurer la destination.

1. Vous devez disposer d’un compte SendGrid.
   * Accédez à SendGrid. [inscription](https://signup.sendgrid.com/) pour enregistrer et créer un compte SendGrid, le cas échéant.
1. Une fois connecté au portail SendGrid, vous devez également générer un jeton API.
1. Accédez au site web de SendGrid et accédez au **[!DNL Settings]** > **[!DNL API Keys]** page. Vous pouvez également vous reporter à la section [Documentation SendGrid](https://app.sendgrid.com/settings/api_keys) pour accéder à la section appropriée dans l’application SendGrid.
1. Enfin, sélectionnez l’option **[!DNL Create API Key]** bouton .
   * Reportez-vous à la section [Documentation SendGrid](https://docs.sendgrid.com/ui/account-and-settings/api-keys#creating-an-api-key), si vous avez besoin de conseils sur les actions à effectuer.
   * Si vous souhaitez générer votre clé API par programmation, reportez-vous à la section [Documentation SendGrid](https://docs.sendgrid.com/api-reference/api-keys/create-api-keys).

![](../../assets/catalog/email-marketing/sendgrid/01-api-key.jpg)

Avant d’activer des données vers la destination SendGrid, vous devez disposer d’un [schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=fr), un [dataset](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), et [segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) créé dans [!DNL Experience Platform]. Reportez-vous également à la section [limites](#limits) plus loin dans cette page.

>[!IMPORTANT]
>
>* L’API SendGrid utilisée pour créer la liste de diffusion à partir des profils de messagerie nécessite que des adresses électroniques uniques soient fournies dans chaque profil. Cela n’est pas nécessaire, qu’il soit utilisé comme valeur pour *email* ou *courrier électronique alternatif*. Comme la connexion SendGrid prend en charge les mappages pour les adresses électroniques et les autres valeurs d’adresse électronique, veillez à ce que toutes les adresses électroniques utilisées soient uniques dans chaque profil de *Jeu de données*. Dans le cas contraire, lorsque les profils de courrier électronique sont envoyés à SendGrid, une erreur se produit et ce profil ne sera pas présent dans l’exportation des données.
>
>* Actuellement, aucune fonctionnalité n’est en place pour supprimer des profils de SendGrid lorsqu’ils sont supprimés des segments dans Experience Platform.


## Identités prises en charge {#supported-identities}

SendGrid prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur [identités](/help/identity-service/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| adresse e-mail | Adresse e-mail | Notez que le texte brut et les adresses électroniques hachées SHA256 sont pris en charge par [!DNL Adobe Experience Platform]. Si le champ source Experience Platform contient des attributs non hachés, vérifiez la variable **[!UICONTROL Appliquer la transformation]** option, pour avoir [!DNL Platform] hachage automatique des données lors de l’activation.<br/><br/> Notez que **SendGrid** ne prend pas en charge les adresses électroniques hachées. Par conséquent, seules les données en texte brut sans transformation sont envoyées à la destination. |

{style=&quot;table-layout:auto&quot;}

## Type et fréquence d&#39;export {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil de la fonction [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exports | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont &quot;toujours sur&quot; des connexions basées sur l’API. Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Cas dʼutilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination SendGrid, voici des exemples d’utilisation qui [!DNL Experience Platform] les clients peuvent résoudre ce problème en utilisant cette destination.

### Création d’une liste marketing pour plusieurs activités marketing

Les équipes marketing qui utilisent SendGrid peuvent créer une liste de diffusion dans SendGrid et la remplir avec des adresses électroniques. La liste de diffusion désormais créée dans SendGrid peut être utilisée par la suite pour plusieurs activités marketing.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.


Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Les étapes spécifiques à cette destination sont illustrées en détail ci-dessous.

1. Dans le [!DNL Adobe Experience Platform] console, accédez à **Destinations**.

1. Sélectionnez la **Catalogue** et recherchez *SendGrid*. Sélectionnez **Configuration**. Après avoir établi une connexion à la destination, le libellé de l’interface utilisateur passe à **Activation des segments**.
   ![](../../assets/catalog/email-marketing/sendgrid/02-catalog.jpg)

1. Un assistant vous aide à configurer la destination SendGrid. Créez la destination en sélectionnant **Configuration d’une nouvelle destination**.
   ![](../../assets/catalog/email-marketing/sendgrid/03.jpg)

1. Sélectionnez la **Nouveau compte** et renseignez la variable **Jeton porteur** . Cette valeur est SendGrid. *Clé API* mentionnée précédemment dans la variable [section conditions préalables](#prerequisites).
   ![](../../assets/catalog/email-marketing/sendgrid/04.jpg)

1. Sélectionner **Se connecter à la destination**. Si SendGrid *Clé API* Si la variable fournie est valide, l’interface utilisateur affiche une **Connecté** avec une coche verte, vous pouvez ensuite passer à l’étape suivante pour remplir d’autres champs d’informations.

![](../../assets/catalog/email-marketing/sendgrid/05.jpg)

### Paramètres de connexion {#parameters}

Pendant la [configuration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]**: Nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]**: Description facultative qui vous aidera à identifier cette destination ultérieurement.

![](../../assets/catalog/email-marketing/sendgrid/06.jpg)

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Lecture [Activation des profils et des segments vers des destinations d’exportation de segments en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

Reportez-vous aux images ci-dessous pour plus de détails sur cette destination.

1. Sélectionnez un ou plusieurs segments à exporter vers SendGrid.
   ![](../../assets/catalog/email-marketing/sendgrid/11.jpg)

1. Dans le **[!UICONTROL Mappage]** , après avoir sélectionné **[!UICONTROL Ajouter un nouveau mappage]**, la page de mappage s’affiche pour mapper les champs XDM sources aux champs cibles de l’API SendGrid. Les images ci-dessous montrent comment mapper des espaces de noms d’identité entre Experience Platform et SendGrid. Assurez-vous que la variable **[!UICONTROL Champ source]** *Email* doit être mappé à la propriété **[!UICONTROL Champ cible]** *external_id* comme illustré ci-dessous.
   ![](../../assets/catalog/email-marketing/sendgrid/13.jpg)

   ![](../../assets/catalog/email-marketing/sendgrid/14.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/15.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/16.jpg)

1. De même, mappez les [!DNL Adobe Experience Platform] attributs que vous souhaitez exporter vers la destination SendGrid.
   ![](../../assets/catalog/email-marketing/sendgrid/17.jpg)

   ![](../../assets/catalog/email-marketing/sendgrid/18.jpg)

1. Une fois les mappages terminés, sélectionnez **[!UICONTROL Suivant]** pour accéder à l’écran de révision.
   ![](../../assets/catalog/email-marketing/sendgrid/22.png)

1. Sélectionner **[!UICONTROL Terminer]** pour terminer la configuration.
   ![](../../assets/catalog/email-marketing/sendgrid/23.jpg)

Liste complète des mappages d’attributs pris en charge pouvant être configurés pour la variable [SendGrid Marketing Contacts > Add or Update Contact API](https://docs.sendgrid.com/api-reference/contacts/add-or-update-a-contact) est ci-dessous.

| Champ source | Champ cible | Type | Description | Limites |
|---|---|---|---|---|
| xdm :<br/> homeAddress.street1 | xdm :<br/> address_line_1 | Chaîne | La première ligne de l’adresse. | Longueur max. :<br/> 100 caractères |
| xdm :<br/> homeAddress.street2 | xdm :<br/> address_line_2 | Chaîne | Une seconde ligne facultative pour l’adresse. | Longueur max. :<br/> 100 caractères |
| xdm :<br/> _extconndev.alternate_emails | xdm :<br/> alternate_emails | Tableau de chaîne | Emails supplémentaires associés au contact. | <ul><li>Max : 5 éléments</li><li>Min : 0 élément</li></ul> |
| xdm :<br/> homeAddress.city | xdm :<br/> city | Chaîne | La ville du contact. | Longueur max. :<br/> 60 caractères |
| xdm :<br/> homeAddress.country | xdm :<br/> country | Chaîne | Le pays du contact. Il peut s’agir d’un nom complet ou d’une abréviation. | Longueur max. :<br/> 50 caractères |
| identityMap :<br/> Email | Identité :<br/> external_id | Chaîne | L&#39;Principal email du contact. Il doit s’agir d’un email valide. | Longueur max. :<br/> 254 caractères |
| xdm :<br/> person.name.firstName | xdm :<br/> first_name | Chaîne | Nom du contact | Longueur max. :<br/> 50 caractères |
| xdm :<br/> person.name.lastName | xdm :<br/> last_name | Chaîne | Nom de famille du contact | Longueur max. :<br/> 50 caractères |
| xdm :<br/> homeAddress.postalCode | xdm :<br/> postal_code | Chaîne | Code postal du contact ou autre code postal. |  |
| xdm :<br/> homeAddress.stateProvince | xdm :<br/> state_province_region | Chaîne | État, province ou région du contact. | Longueur max. :<br/> 50 caractères |

## Validation de l’exportation des données dans SendGrid {#validate}

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

1. Sélectionner **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]** pour accéder à la liste des destinations.
   ![](../../assets/catalog/email-marketing/sendgrid/25.jpg)

1. Sélectionnez la destination et vérifiez que l’état est **[!UICONTROL enabled]**.
   ![](../../assets/catalog/email-marketing/sendgrid/26.jpg)

1. Basculez vers le **[!DNL Activation data]** , puis sélectionnez un nom de segment.
   ![](../../assets/catalog/email-marketing/sendgrid/27.jpg)

1. Surveillez le résumé du segment et vérifiez que le nombre de profils correspond au nombre créé dans le jeu de données.
   ![](../../assets/catalog/email-marketing/sendgrid/28.jpg)

1. Le [Listes marketing SendGrid > API Create List](https://docs.sendgrid.com/api-reference/lists/create-list) est utilisé pour créer des listes de contacts uniques dans SendGrid en associant la valeur de la variable *list_name* et l’horodatage de l’exportation des données. Accédez au site SendGrid et vérifiez si la nouvelle liste de contacts conforme au modèle de nom est créée.
   ![](../../assets/catalog/email-marketing/sendgrid/29.jpg)

   ![](../../assets/catalog/email-marketing/sendgrid/30.jpg)

1. Sélectionnez la nouvelle liste de contacts et vérifiez si le nouvel enregistrement email du jeu de données que vous avez créé est renseigné dans la nouvelle liste de contacts.

1. De plus, vérifiez également quelques emails pour vérifier si le mappage des champs est correct.
   ![](../../assets/catalog/email-marketing/sendgrid/31.jpg)

   ![](../../assets/catalog/email-marketing/sendgrid/32.jpg)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, voir [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

Cette destination SendGrid utilise les API suivantes :
* [Listes marketing SendGrid > API Create List](https://docs.sendgrid.com/api-reference/lists/create-list)
* [SendGrid Marketing Contacts > Add or Update Contact API](https://docs.sendgrid.com/api-reference/contacts/add-or-update-a-contact)

### Limites {#limits}

* Le [SendGrid Marketing Contacts > Add or Update Contact API](https://api.sendgrid.com/v3/marketing/contacts) peut accepter 30 000 contacts ou 6 Mo de données, selon la limite inférieure.
