---
title: Présentation de l’extension Adobe Privacy
description: Découvrez lʼextension de balise Adobe Privacy dans Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: ht
source-wordcount: '534'
ht-degree: 100%

---

# Présentation de l’extension Adobe Privacy

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

L’extension Adobe Privacy propose des fonctionnalités de collecte et de suppression des ID utilisateurs affectés aux utilisateurs finaux par les solutions Adobe.

## Configuration de solutions durant l’installation

Lorsque vous installez l’extension Adobe Privacy à partir du catalogue d’extensions, vous êtes invité à sélectionner les solutions que vous souhaitez mettre à jour. Actuellement, vous pouvez mettre à jour les solutions suivantes :

* Analytics (AA)
* Audience Manager (AAM)
* Target
* Visitor Service
* AdCloud
* Sélectionnez une ou plusieurs solutions, puis cliquez sur Mettre à jour.
* Lorsque vous avez sélectionné et configuré vos solutions, cliquez sur Enregistrer. L’extension Adobe Privacy est ajoutée à la liste des extensions installées.

   Les options de chaque solution sont décrites ci-dessous.

### Analytics

![](../../../images/ext-privacy-aa.jpg)

Par défaut, vous devez fournir une suite de rapports en saisissant une chaîne ou en sélectionnant un élément de données.

Pour configurer dʼautres éléments, cliquez sur **[!UICONTROL Sélectionner un élément]**, sélectionnez lʼélément que vous souhaitez configurer, puis cliquez sur **[!UICONTROL Ajouter]** et saisissez le paramètre requis ou un élément de données.

### Audience Manager

![](../../../images/ext-privacy-aam.jpg)

Cliquez sur **[!UICONTROL Sélectionner un élément]**, sélectionnez lʼélément à configurer, puis cliquez sur **[!UICONTROL Ajouter]** et saisissez le paramètre requis ou un élément de données. Actuellement, vous ne pouvez configurer que le paramètre `aamUUIDCookieName`.

### Target

![](../../../images/ext-privacy-target.jpg)

Saisissez le code client Target.

### Visitor Service

![](../../../images/ext-privacy-visitor.jpg)

Saisissez votre ID d’organisation IMS.

### AdCloud

![](../../../images/ext-privacy-adcloud.jpg)

Il n’y a aucun paramètre spécifique à configurer pour AdCloud.

## Configuration de l’extension Adobe Privacy

Après avoir installé l’extension, vous pouvez la désactiver ou la supprimer. Cliquez sur **[!UICONTROL Configurer]** sur la carte Adobe Privacy des extensions installées, puis sélectionnez **[!UICONTROL Désactiver]** ou **[!UICONTROL Désinstaller]**.

## Actions

Les actions suivantes sont disponibles lorsque vous configurez une règle à l’aide de l’extension Adobe Privacy.

### Récupération d’identités

Lorsque l’événement et les conditions sont satisfaits, récupérez les informations d’identité stockées pour le visiteur.

Saisissez le nom d’une fonction JavaScript à laquelle vous souhaitez transmettre les données. Cette fonction ou méthode gère les identités récupérées. C’est à vous de décider de les stocker, de les afficher ou de les envoyer à l’API Adobe RGPD.

### Suppression d’identités

Lorsque l’événement et les conditions sont satisfaits, supprimez les informations d’identité stockées pour le visiteur.

Saisissez le nom d’une fonction JavaScript à laquelle vous souhaitez transmettre les données. Cette fonction ou méthode gère les identités récupérées. C’est à vous de décider de les stocker, de les afficher ou de les envoyer à l’API Adobe RGPD.

### Récupération et suppression des identités

Lorsque l’événement et les conditions sont satisfaits, récupérez les informations d’identité stockées pour le visiteur, puis supprimez-les.

## Tutoriel : configuration de l’extension de confidentialité

L’exemple suivant illustre comment configurer un élément de données et l’utiliser avec l’extension de confidentialité.

1. Créez un élément de données intitulé `privacyFunc`.

   ```JavaScript
   window.privacyFunc = function(a,b){
       console.log(a,b);
   }
   return window.privacyFunc
   ```

1. Créez une règle à exécuter au chargement de bibliothèque (en haut de la page), avec une action de l’extension Adobe Privacy. Sélectionnez `privacyFunc` comme élément de données.

   * **Extension :** Adobe Privacy
   * **Type d’action :** Récupération d’identités
Ce type d’action affiche les identités qui ont été créées, supprimées ou non supprimées.
   * **Nom :** Récupération d’identités

1. Mettez à jour votre bibliothèque de développement, puis publiez et testez.
