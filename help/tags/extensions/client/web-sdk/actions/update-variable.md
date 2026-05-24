---
title: Mettre à jour la variable
description: Modifie le contenu d’un élément de données variable.
exl-id: 6c558d1e-85b4-45f9-ba4d-5fed1ec6e308
TQID: https://experienceleague.adobe.com/FHWcaLTAxIT4OeOvFzTnw5Jd3GT3ngHeqAN6ntPJ2uo
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 263
ht-degree: 0%

---

# Mettre à jour la variable

L’action **[!UICONTROL Update variable]** vous permet d’apporter des modifications partielles ou incrémentielles à un [élément de données variable](../data-element-types.md#variable). Vous pouvez utiliser cette action pour créer un objet qui pourra ensuite être référencé dans une action [[!UICONTROL Send event]](send-event.md). Le remplissage d’éléments de données et leur affectation à des propriétés dans un objet XDM correspond à la plupart des cas d’utilisation. Cette action offre plus de flexibilité pour vous permettre de définir de manière conditionnelle des propriétés à différents éléments de données en fonction des conditions de règle.

Avant d’utiliser cette action, vous devez déjà avoir créé un élément de données variable. Une fois que vous avez sélectionné un élément de données de variable à modifier, un éditeur s’affiche, vous permettant de définir tous les champs souhaités pour cette action.

![Capture d’écran de l’action Mettre à jour la variable dans l’interface de configuration des actions](../assets/update-variable.png)

Le schéma XDM utilisé dans l’éditeur correspond au schéma sélectionné dans l’élément de données variable. Vous pouvez définir une ou plusieurs propriétés de l’objet en développant les objets et en sélectionnant les propriétés souhaitées. Par exemple, dans la capture d’écran ci-dessous, la propriété `producedBy` est définie sur l’élément de données `%Produced by data element%`.

![Capture d’écran de l’interface de configuration des actions présentant une propriété mise à jour](../assets/update-variable-set-property.png)

Si vous sélectionnez un élément de données variable qui utilise un objet de données au lieu d’un objet XDM, les champs disponibles dépendent des produits sélectionnés lors de la configuration de l’élément de données. Par exemple, si vous créez un objet de données qui inclut Adobe Analytics, champs , puis que vous sélectionnez l’élément de données variable dans cette interface utilisateur, vous obtiendrez les champs que vous pouvez remplir spécifiques à Adobe Analytics.

![Copie d’écran de l’interface de configuration des actions présentant un élément de données variable basé sur un objet de données](../assets/variable-data-element-data.png)
