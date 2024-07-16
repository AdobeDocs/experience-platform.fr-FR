---
title: Balises Experience Platform (Chine)
description: Découvrez la fonctionnalité Balises Experience Platform (Chine) pour les balises et comment elle peut être utilisée pour diffuser votre contenu dans plusieurs zones géographiques.
exl-id: 33e36d3b-9e21-44a8-8498-32a5fc20b46b
source-git-commit: 9c39fd5d0353cc171230818d79ac213ce200dc1e
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Balises Experience Platform (Chine)

Lorsque vous utilisez un [hôte géré par l’Adobe](./hosts/managed-by-adobe-host.md) pour diffuser vos ressources de balises Adobe Experience Platform sur votre site web, ces ressources sont distribuées sur divers réseaux de diffusion de contenu (CDN) dans le monde entier pour offrir la vitesse de téléchargement la plus rapide. Cependant, certaines régions exigent que toutes les ressources de site web soient répliquées et hébergées sur un serveur de cette région.

Pour en tenir compte, les balises dans Experience Platform fournissent une fonctionnalité Balises Experience Platform (Chine) qui vous permet de diffuser du contenu vers ces régions spéciales.

La prise en charge des balises Experience Platform (Chine) est une fonctionnalité payante qui doit être achetée par votre organisation pour l’activer et l’utiliser. Ce guide explique comment configurer et utiliser cette fonctionnalité dans l’interface utilisateur de l’Experience Platform ou dans l’interface utilisateur de collecte de données une fois qu’elle a été achetée.

## Activation des balises Experience Platform (Chine) pour votre organisation

Les balises Experience Platform (Chine) sont activées au niveau de l’entreprise. Une fois que votre entreprise a acheté la fonction Balises Experience Platform (Chine), un administrateur d’Adobe l’activera dans l’interface utilisateur de votre entreprise.

## Reconstruire et installer des bibliothèques de balises avec des codes incorporés mis à jour

Une fois les balises Experience Platform (Chine) activées, cela ne signifie pas que vos ressources de balise sont immédiatement répliquées et prêtes à être utilisées dans les nouvelles régions. Cela signifie uniquement que vous pouvez maintenant choisir le moment auquel vous abonner à cette fonctionnalité.

>[!IMPORTANT]
>
>Les bibliothèques construites avant d’activer les balises en Chine continueront à fonctionner comme elles le font aujourd’hui. Cela s’applique également aux bibliothèques qui ne sont pas gérées par l’Adobe, puisque les [environnements archivés](./environments.md#archive) n’utilisent que des URL relatives pour leurs chemins d’accès aux ressources. Notez qu’une fois que vous avez activé les balises Experience Platform (Chine), toute bibliothèque que vous créez et qui n’est pas gérée par Adobe se comporte comme si les balises de la fonction Chine n’étaient pas activées.

Une fois que vous avez activé les balises en Chine et reconstruit toutes les bibliothèques que vous souhaitez utiliser à partir des nouvelles régions d’hébergement, vous pouvez récupérer les nouveaux codes incorporés de région d’hébergement à ajouter à vos sites web.

>[!NOTE]
>
>Le code incorporé de bibliothèque répertorié sous la région d’hébergement [!UICONTROL Standard] continuera à fonctionner en l’état, ainsi que les codes incorporés Haut de page ou Bas de page déjà présents sur vos sites web.

Consultez la page **[!UICONTROL Environnements]** ou consultez les instructions d’installation de l’environnement à partir de l’écran de modification de la bibliothèque pour trouver les nouveaux codes incorporés. Chaque nouvelle région d’hébergement prise en charge apparaît après la région d’hébergement [!UICONTROL Standard] (utilisée pour les zones du monde qui sont prises en charge sans balises Experience Platform (Chine)). La capture d’écran ci-dessous montre un code incorporé pour la région Chine, qui utilise `.cn` comme domaine de niveau supérieur (TLD).

![Code incorporé de la région Chine](../../images/ui/publishing/premium-cdn/embed-codes.png)

Sélectionnez le code incorporé approprié pour la page web et collez-le dans la balise `<head>` de votre document. Pour plus d’informations sur l’utilisation des codes incorporés pour installer les bibliothèques de balises, reportez-vous au [guide de l’interface utilisateur des environnements](./environments.md#installation).

## Étapes suivantes

Ce guide explique comment activer et installer la fonctionnalité Balises Experience Platform (Chine) pour votre mise en oeuvre de balises. Pour plus d’informations sur l’installation et le test des bibliothèques de balises sur vos propriétés web et mobiles, reportez-vous à la [présentation de la publication](./overview.md).
