---
keywords: Experience Platform;profil;profil client en temps réel;interface utilisateur;personnalisation;détails du profil;détails
title: Personnalisation des détails du profil dans l’interface utilisateur
description: Ce guide fournit des instructions détaillées pour personnaliser la manière dont les données de Real-time Customer Profile s’affichent dans l’interface utilisateur de Adobe Experience Platform.
topic-legacy: guide
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 0%

---

# Personnalisation détaillée du [!DNL Real-time Customer Profile] {#profile-detail-customization}

Dans l’interface utilisateur de Adobe Experience Platform, vous pouvez afficher et interagir avec [!DNL Real-time Customer Profile] données sous la forme de profils client. Les informations de profil affichées dans l’interface utilisateur ont été fusionnées à partir de plusieurs fragments de profil afin de former une vue unique de chaque client. Cela inclut des détails tels que les attributs de base, les identités liées et les préférences de canal. Les champs par défaut affichés dans les profils peuvent également être modifiés au niveau de l&#39;organisation pour afficher les préférences. [!DNL Profile] attributs. Ce guide fournit des instructions détaillées pour personnaliser la manière dont [!DNL Profile] Les données s’affichent dans l’interface utilisateur de Platform.

Pour obtenir un guide complet sur l’interface utilisateur des profils, consultez la page [Guide de l’interface utilisateur de Profile](user-guide.md).

## Réorganiser et redimensionner les cartes {#reorder-and-resize-cards}

Dans la **[!UICONTROL Détail]** de l’onglet du profil client, vous pouvez sélectionner **[!UICONTROL Modifier le tableau de bord]** pour redimensionner et réorganiser les cartes existantes.

![](../images/profile-customization/profiles-modify-dashboard.png)

Après avoir choisi de modifier le tableau de bord, vous pouvez réorganiser les cartes en sélectionnant le titre de la carte, en les faisant glisser et en les déposant dans l’ordre souhaité. Vous pouvez également redimensionner une carte en sélectionnant le symbole de l’angle dans le coin inférieur droit de la carte (`⌟`) et faites glisser la carte à la taille souhaitée. Dans cet exemple, la variable **[!UICONTROL Attributs de base]** est redimensionnée.

![](../images/profile-customization/profiles-resize-cards.png)

La carte sélectionnée s’ajuste à la taille souhaitée et les cartes environnantes sont repositionnées dynamiquement. Cela peut entraîner le déplacement de certaines cartes vers d’autres lignes, ce qui nécessite de faire défiler la page vers le bas pour afficher toutes les cartes. Par exemple, lorsque la variable[!UICONTROL Attributs de base]&quot; est redimensionné comme suit :[!UICONTROL Identités liées]&quot;n’est plus visible sur la ligne supérieure et apparaît désormais sur une nouvelle deuxième ligne du profil (non affichée). Pour renvoyer le[!UICONTROL Identités liées]&quot; à la ligne supérieure, vous pouvez la faire glisser et la déposer à la position actuelle de l’objet &quot;[!UICONTROL Préférences de canal]&quot;.

![](../images/profile-customization/profiles-card-resized.png)

## Modification et suppression de cartes

Outre le redimensionnement et la réorganisation des cartes, vous pouvez modifier le contenu de certaines cartes et supprimer entièrement certaines cartes du tableau de bord. Sélectionnez les ellipses (`...`) dans le coin supérieur droit de la carte afin de la modifier ou de la supprimer. Une liste déroulante s’ouvre alors avec des options permettant de modifier ou de supprimer la carte, selon les propriétés de la carte sélectionnée.

>[!NOTE]
>
>Toutes les cartes ne peuvent pas être modifiées ni supprimées. En effet, certaines cartes contiennent des informations en lecture seule ou obligatoires. Si une carte ne comporte pas de ellipse dans le coin supérieur droit, elle contient des informations requises EN lecture seule ET ne peut pas être modifiée ni supprimée. Si une carte comporte des ellipses dans le coin et que la sélection de cette option n’affiche qu’une option pour la supprimer, les informations de la carte sont en lecture seule et ne peuvent pas être modifiées.

![](../images/profile-customization/profiles-edit-remove-resized.png)

Sélectionner **[!UICONTROL Modifier]** dans la liste déroulante pour ouvrir le **[!UICONTROL Modifier le widget]** espace de travail dans lequel vous pouvez mettre à jour le titre de la carte, réorganiser ou supprimer les attributs visibles ou ajouter des attributs supplémentaires à l’aide de la fonction **[!UICONTROL Ajout d’attributs]** bouton .

![](../images/profile-customization/profiles-edit-widget-basic-attributes.png)

## Ajout d’attributs {#add-attributes}

Dans la **[!UICONTROL Modifier le widget]** écran, sélectionnez **[!UICONTROL Ajout d’attributs]** dans le coin supérieur droit de la carte pour commencer à ajouter des attributs à cette carte.

![](../images/profile-customization/profiles-edit-widget-basic-add-attributes.png)

Lorsque la variable **[!UICONTROL Sélectionner le champ de schéma d’union]** La boîte de dialogue s’ouvre ; la partie gauche de la boîte de dialogue affiche l’intégralité [!UICONTROL XDM Individual Profile] schéma d’union, avec des champs imbriqués en dessous. Pour plus d’informations sur les schémas d’union, reportez-vous à la section [section schémas d’union de [!DNL Profile] guide de l’utilisateur](user-guide.md#union-schema).

Le **[!UICONTROL Attributs sélectionnés]** sur le côté droit de la boîte de dialogue, la section affiche les attributs qui sont actuellement inclus dans la carte que vous modifiez. Vous pouvez également supprimer et réorganiser les attributs ici. Le nombre total d’attributs sélectionnés s’affiche, ainsi que le nombre maximal d’attributs (20) pouvant être ajoutés à une seule carte.

![](../images/profile-customization/profiles-select-field-before.png)

Vous pouvez sélectionner l’un des champs de schéma d’union disponibles pour personnaliser les attributs de la carte que vous modifiez. Les champs sélectionnés sont accompagnés d’une coche et sont automatiquement ajoutés à la liste des attributs sélectionnés. Une fois que vous avez ajouté tous les attributs que vous souhaitez afficher sur la carte, choisissez **[!UICONTROL Sélectionner]** pour revenir au **[!UICONTROL Modifier le widget]** écran.

![](../images/profile-customization/profiles-select-field-after.png)

Lorsque vous revenez à la variable **[!UICONTROL Modifier le widget]** , la liste des attributs de la carte doit maintenant être mise à jour pour refléter vos choix. Vous pouvez toujours supprimer ou réorganiser les attributs de carte ou modifier le titre de la carte selon vos besoins. Une fois les modifications effectuées, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer vos modifications.

![](../images/profile-customization/profiles-edit-widget-new-attributes.png)

Après l’enregistrement, vous revenez à la variable **[!UICONTROL Détail]** dans lequel la carte et les attributs mis à jour sont visibles.

![](../images/profile-customization/profiles-resized-card-new-attributes.png)

## Ajouter une nouvelle carte {#add-a-new-card}

Pour personnaliser davantage l’aspect des profils dans Experience Platform, vous pouvez choisir d’ajouter de nouvelles cartes au tableau de bord et de sélectionner les attributs que vous souhaitez afficher sur ces cartes. Pour commencer, sélectionnez **[!UICONTROL Modifier le tableau de bord]** sur le **[!UICONTROL Détail]** .

![](../images/profile-customization/profiles-modify-dashboard.png)

Ensuite, sélectionnez **[!UICONTROL Ajouter un widget]** dans le coin supérieur gauche du tableau de bord.

![](../images/profile-customization/profiles-add-widget.png)

Si vous choisissez d’ajouter une nouvelle carte, le **[!UICONTROL Modifier le widget]** écran dans lequel vous pouvez fournir un titre pour la nouvelle carte et sélectionner les attributs que vous souhaitez afficher. Pour commencer à ajouter des attributs à la carte, sélectionnez **[!UICONTROL Ajout d’attributs]**.

![](../images/profile-customization/profiles-edit-new-widget.png)

Lorsque la variable **[!UICONTROL Sélectionner le champ de schéma d’union]** La boîte de dialogue s’ouvre ; le côté gauche de la boîte de dialogue affiche l’intégralité [!UICONTROL XDM Individual Profile] le schéma d’union et la variable **[!UICONTROL Attributs sélectionnés]** sur le côté droit de la boîte de dialogue, la section affiche les attributs que vous sélectionnez pour votre carte. Pour plus d’informations sur l’ajout d’attributs, voir la section [section sur l’ajout d’attributs](#add-attributes) qui apparaît plus haut dans ce document.

Le nombre total d’attributs sélectionnés s’affiche, ainsi que le nombre maximal d’attributs (20) pouvant être ajoutés à une seule carte. Vous pouvez également supprimer et réorganiser vos attributs sélectionnés à partir de cet écran. Une fois que vous avez ajouté tous les attributs que vous souhaitez afficher sur la carte, choisissez **[!UICONTROL Sélectionner]** pour revenir au **[!UICONTROL Modifier le widget]** écran.

![](../images/profile-customization/profiles-add-fields-new-widget.png)

Lorsque vous revenez à la variable **[!UICONTROL Modifier le widget]** , la liste des attributs de la carte doit refléter vos choix de l’écran précédent. Vous pouvez également réorganiser et supprimer des attributs de carte selon vos besoins.

Pour enregistrer votre nouvelle carte, vous devez d’abord fournir un **[!UICONTROL Titre de carte]**, vous pourrez alors sélectionner **[!UICONTROL Enregistrer]** et terminer le processus de création de la carte.

![](../images/profile-customization/profiles-edit-new-widget-with-fields.png)

Après l’enregistrement, vous revenez à la variable **[!UICONTROL Détail]** dans lequel vos nouvelles cartes et attributs sont visibles.

![](../images/profile-customization/profiles-detail-new-widget.png)

## Restaurer les cartes par défaut

Si vous décidez à tout moment de restaurer les cartes par défaut qui ont été supprimées depuis, vous avez la possibilité de le faire rapidement et facilement. Tout d’abord, sélectionnez **[!UICONTROL Modifier le tableau de bord]**, puis sélectionnez **[!UICONTROL Restaurer les cartes par défaut]**. Une fois les cartes par défaut visibles, vous pouvez sélectionner **[!UICONTROL Enregistrer]** pour enregistrer vos modifications ou sélectionnez **[!UICONTROL Annuler]** si vous ne souhaitez pas restaurer les cartes par défaut.

![](../images/profile-customization/profiles-restore-default.png)

## Étapes suivantes

En suivant ce document, vous devriez maintenant pouvoir mettre à jour la vue de profil de votre entreprise, y compris l’ajout et la suppression de cartes, la modification des détails et des attributs de carte, ainsi que la réorganisation et le redimensionnement des cartes. Pour en savoir plus sur l’utilisation de [!DNL Profile] données de l’interface utilisateur de l’Experience Platform, reportez-vous à la section [[!DNL Profile] guide de l’utilisateur](user-guide.md).
