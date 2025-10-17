---
title: Packages d’extension privés partagés
description: Découvrez comment partager des packages d’extension privés dans Adobe Experience Platform Tags.
source-git-commit: f45f58b4679b619708204cdb0c18174a4836ce8d
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 0%

---

# Packages d’extension privés partagés

Adobe Experience Platform Tags prend désormais en charge les **[!UICONTROL autorisations d’utilisation]**, une puissante fonctionnalité qui vous permet de partager en toute sécurité des packages d’extension privés avec des partenaires approuvés sans les rendre disponibles publiquement dans le catalogue d’extensions. Cette fonctionnalité crée un pont sécurisé entre les organisations, ce qui vous permet d’exploiter le code d’extension personnalisé des unes et des autres tout en préservant la confidentialité et le contrôle sur vos solutions propriétaires.

## Partage de packages d’extension avec d’autres organisations

>[!NOTE]
>
>Les packages d’extension doivent avoir une version privée ou publique pour être partagés via [!UICONTROL Autorisations d’utilisation]. Les versions marquées comme Disponibilité pour le développement ne sont pas éligibles au partage et n’apparaîtront pas dans la liste déroulante d’autorisation. Cela s’applique même si une version antérieure (par exemple, 1.0.0) a déjà été partagée. Les versions plus récentes (par exemple, 1.0.1) doivent être rendues au moins privées avant de pouvoir être autorisées ou installées par les organisations destinataires.
>
>Toutes les instructions concernant le partage de packages d’extension privés s’appliquent également si vous choisissez par la suite de rendre ces packages publics. Les mêmes considérations concernant la visibilité, le contrôle de version, la sécurité, la compatibilité, la prise en charge et la documentation restent pertinentes, quel que soit le statut de disponibilité du package.

Les packages d’extension publics et privés peuvent être partagés via les [!UICONTROL autorisations d’utilisation], bien que les extensions dans Disponibilité du développement ne puissent pas être associées à des autorisations.

Les entreprises développent souvent des extensions spécialisées adaptées à leurs besoins professionnels uniques. Ces extensions peuvent contenir une logique propriétaire, des intégrations personnalisées ou des configurations sensibles qui ne doivent pas être rendues publiques. Les autorisations d’utilisation résolvent ce défi en activant :

- **Partage sélectif** : partagez des extensions privées uniquement avec des organisations partenaires de confiance
- **Confidentialité préservée** : excluez le code d’extension sensible du catalogue public
- **Développement collaboratif** : permettez à des partenaires de confiance de bénéficier de vos solutions personnalisées
- **Accès contrôlé** : conservez un contrôle total sur les personnes qui peuvent accéder à vos extensions privées et les utiliser

Le processus de partage implique deux participants clés :

1. **Organisation de partage** : l’organisation qui détient et partage le package d’extension privé
2. **Organisation d’accueil** : organisation approuvée qui accède à l’extension partagée

Lorsqu’une version privée est partagée, l’organisation destinataire a accès à cette version spécifique, ce qui crée une connexion directe entre les deux organisations. Si une version plus récente est rendue privée par la suite, elle sera également disponible pour l’organisation destinataire sans nécessiter d’étapes supplémentaires de sa part.

## Créer une autorisation d’utilisation de package d’extension

Pour partager une extension, accédez à l’interface utilisateur de la collecte de données et sélectionnez **[!UICONTROL Balises]** dans le volet de navigation de gauche. À partir de là, sélectionnez une propriété existante ou créez une propriété.

Une fois la propriété souhaitée sélectionnée ou créée, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Autorisations d’utilisation]**.

Vous voyez ici une liste des autorisations partagées existantes organisées en deux catégories :

- **Partagé avec cette organisation** : extensions que d’autres organisations ont partagées avec vous.
- **Partagé avec d’autres organisations** : extensions que vous avez partagées avec d’autres organisations.

Sélectionnez **[!UICONTROL Ajouter une autorisation]**.

![Onglet [!UICONTROL Autorisations d’utilisation] affichant une liste des extensions partagées avec cette organisation, en surbrillance [!UICONTROL Ajouter une autorisation]](../images/shared-extensions/add-authorization.png)

>[!IMPORTANT]
>
>Vous devez obtenir le de l&#39;organisation cible **`Organization ID`** le propriétaire de l&#39;organisation. Les organisations ne peuvent pas être recherchées par nom.

Sélectionnez la **[!UICONTROL Extension]** que vous souhaitez partager parmi les extensions disponibles dans la liste déroulante. La liste affiche les extensions détenues par votre organisation ainsi que leur statut de disponibilité. Les extensions dont la dernière version est en cours de disponibilité **Développement** n’apparaîtront pas dans cette liste.

Saisissez ensuite l’ID de l’organisation de réception, puis sélectionnez **[!UICONTROL Enregistrer]**.

![Page [!UICONTROL Créer une autorisation d’utilisation de package d’extension] affichant une extension sélectionnée et l’ID d’organisation Adobe saisi, en surbrillance [!UICONTROL Enregistrer]](../images/shared-extensions/save-authorization.png)

Vous revenez alors à l’onglet [!UICONTROL &#x200B; Autorisations d’utilisation &#x200B;] où vous pouvez voir l’extension dans votre liste **[!UICONTROL Partagée avec d’autres organisations]**. Le statut indique **En attente d&#39;approbation** jusqu&#39;à ce que l&#39;organisation réceptrice approuve l&#39;autorisation, auquel cas elle est mise à jour sur **Approuvée**.

![Onglet [!UICONTROL Autorisations d’utilisation] affichant une liste des extensions partagées avec d’autres organisations, en mettant en surbrillance la nouvelle autorisation](../images/shared-extensions/new-authorization.png)

>[!TIP]
>
>Vous pouvez également partager des extensions directement à partir du **[!UICONTROL Catalogue d’extensions]** en sélectionnant le menu (⋯) sur la carte d’extension, puis en sélectionnant l’option de partage dans le menu.

Lorsqu’une autorisation est active, l’extension partagée affiche un badge ***Partage*** dans le catalogue indiquant qu’elle est partagée avec d’autres organisations.

![Onglet [!UICONTROL Catalogue] affichant l’extension partagée avec le badge](../images/shared-extensions/sharing-badge.png)

## Autoriser et gérer les extensions partagées

>[!NOTE]
>
>En tant qu’organisation de réception, vous pouvez uniquement approuver ou rejeter les extensions partagées. Vous ne pouvez pas gérer ni modifier les détails d’autorisation, car ils sont contrôlés par l’organisation de partage.

Pour autoriser une extension partagée pour votre organisation, accédez à l’interface utilisateur de collecte de données et sélectionnez **[!UICONTROL Balises]** dans le volet de navigation de gauche, puis sélectionnez la propriété. Sélectionnez ensuite **[!UICONTROL Extensions]** dans le volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Autorisations d’utilisation]**.

La section **Partagées avec cette organisation** répertorie les extensions partagées, y compris celles **[!UICONTROL En attente d’approbation]**. Sélectionnez l’extension à approuver, puis sélectionnez **[!UICONTROL Approuver]**.

![Onglet [!UICONTROL Autorisations d’utilisation] affichant une liste des extensions partagées avec cette organisation avec l’extension en attente d’approbation sélectionnée, en surbrillance [!UICONTROL Approuver]](../images/shared-extensions/approve-authorization.png)

>[!NOTE]
>
>Vous pouvez également rejeter une demande dans l’onglet **[!UICONTROL Autorisations d’utilisation]** si l’extension partagée n’est plus nécessaire pour votre organisation.

Sélectionnez **[!UICONTROL OK]** dans la boîte de dialogue **[!UICONTROL Utilisations d’autorisation]**.

![Boîte de dialogue [!UICONTROL Utilisations d’autorisation], en surbrillance [!UICONTROL OK]](../images/shared-extensions/confirmation.png)

Vous revenez sur l’onglet [!UICONTROL &#x200B; Autorisations d’utilisation &#x200B;] où vous pouvez voir que l’extension affiche désormais un statut **Approuvé**.

![Onglet [!UICONTROL &#x200B; Autorisations d’utilisation] affichant une liste des extensions partagées avec cette organisation, en mettant en surbrillance l’extension avec le statut Approuvé](../images/shared-extensions/approved-authorization.png)

Une fois l’autorisation approuvée, l’extension est disponible dans votre catalogue et peut être installée et utilisée comme toute autre extension. L’extension partagée affiche un badge ***Réception*** indiquant qu’il s’agit d’une extension qui vous est partagée par une autre organisation.

![Onglet [!UICONTROL Catalogue] affichant l’extension partagée avec le badge « Réception »](../images/shared-extensions/receiving-badge.png)

## Révoquer les autorisations

En tant qu’organisation propriétaire, vous pouvez supprimer une autorisation à tout moment, quel que soit son statut actuel (En attente d’approbation, Refusée ou Approuvée).

**Si votre extension n’a jamais été rendue publique :**
- Toute version privée déjà installée par l’organisation de réception apparaîtra toujours dans la liste des extensions installées.
- Si l’organisation réceptrice n’a jamais installé votre extension, elle n’apparaîtra plus nulle part dans son interface.

**Si votre extension a été rendue publique :**
- Toute version privée installée par l’organisation de réception reste visible dans la liste des extensions installées.
- S’il n’a jamais installé votre version privée, il verra toujours la dernière version publique dans son catalogue et pourra l’installer.
- Il peut également rétrograder de votre version privée vers la dernière version publique disponible, si vous le souhaitez.

Lorsque vous révoquez une autorisation, l’organisation destinataire conserve certains droits pour protéger ses implémentations existantes :

- **Utilisation continue** : l’organisation destinataire peut continuer à utiliser toute version privée qu’elle a déjà installée, même après avoir révoqué l’accès.
- **Protection de build** : si l’organisation réceptrice a installé votre version privée v1.0.0 et que vous publiez ultérieurement une version privée v1.0.1, elle ne verra pas la version la plus récente, mais peut continuer à créer avec v1.0.0 sans interruption.
- **Mises à niveau futures** : si vous rendez par la suite votre extension publique (par exemple en publiant la version 2.0.0), l’organisation destinataire peut effectuer directement la mise à niveau de sa version 1.0.0 privée vers la nouvelle version 2.0.0 publique.

>[!IMPORTANT]
>
>La révocation de l’autorisation n’interrompt pas les versions ou implémentations existantes. Les organisations d’accueil conservent l’accès à toutes les versions privées qu’elles ont déjà installées pour assurer la continuité de l’activité.

## Étapes suivantes

Ce document vous a montré comment utiliser la fonctionnalité d’extension partagée dans Experience Platform. Pour plus d’informations sur le développement d’extensions, consultez le [guide d’utilisation du développement d’extensions](./getting-started.md).

Pour une présentation générale du développement des extensions dans Experience Platform, reportez-vous à la [documentation de présentation](./overview.md).
