---
title: Configuration de la détection des robots pour les flux de données
description: Découvrez comment configurer la détection des robots pour les flux de données afin de différencier le trafic humain et non humain.
exl-id: 6b221d97-0145-4d3e-a32d-746d72534add
source-git-commit: ff95e5e105f7b3e1213eab90456b9fa9000918d3
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 0%

---

# Configuration de la détection des robots pour les flux de données

Le trafic provenant d’entités non humaines, telles que les programmes automatisés, les web-scrapers, les araignées, les scanneurs à scripts, peut rendre plus difficile l’identification des événements provenant de visiteurs humains. Ce type de trafic peut avoir une incidence négative sur les mesures commerciales importantes, ce qui entraîne des rapports de trafic incorrects.

La détection des robots permet d’identifier les événements générés par le [SDK Web](../web-sdk/home.md), le [SDK mobile](https://developer.adobe.com/client-sdks/home/) et [[!DNL Server API]](../server-api/overview.md) comme étant générés par des araignées et des robots connus.

En configurant la détection des robots pour vos flux de données, vous pouvez identifier des adresses IP, des plages d’adresses IP et des en-têtes de requête spécifiques que vous souhaitez classer comme événements de robots.

L’identification du trafic de robots peut vous fournir une mesure plus précise de l’activité des utilisateurs sur votre site ou application mobile.

Lorsqu’une requête à l’Edge Network correspond à l’une des règles de détection de robots, le schéma XDM est mis à jour avec une notation de robot (toujours définie sur 1), comme illustré ci-dessous.

```json
{
  "botDetection": {
    "score": 1
  }
}
```

Ce score de robot permet aux solutions qui reçoivent la demande d’identifier correctement le trafic de robots.

>[!IMPORTANT]
>
>La détection des robots ne supprime aucune requête de robot. Il ne met à jour que le schéma XDM avec la notation des robots et transfère l’événement au [service datastream](configure.md) que vous avez configuré.
>
>Les solutions Adobe peuvent gérer la notation des robots de différentes manières. Par exemple, Adobe Analytics utilise son propre [service de filtrage de robots](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/bot-removal/bot-rules.html) et n’utilise pas le score défini par l’Edge Network. Les deux services utilisent la même [liste de robots IAB](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/), de sorte que la notation des robots est identique.

Les règles de détection de robots peuvent prendre jusqu’à 15 minutes pour se propager dans l’Edge Network après sa création.

## Conditions préalables {#prerequisites}

Pour que la détection des robots fonctionne sur votre flux de données, vous devez ajouter le groupe de champs **[!UICONTROL Informations sur la détection des robots]** à votre schéma. Consultez la documentation [Schéma XDM](../xdm/ui/resources/schemas.md#add-field-groups) pour savoir comment ajouter des groupes de champs à un schéma.

## Configuration de la détection des robots pour les flux de données {#configure}

Vous pouvez configurer la détection des robots après avoir créé une configuration de flux de données. Consultez la documentation sur la façon de [créer et configurer un flux de données](configure.md), puis suivez les instructions ci-dessous pour ajouter des fonctionnalités de détection de robots à votre flux de données.

Accédez à la liste des flux de données et sélectionnez le flux de données auquel vous souhaitez ajouter la détection des robots.

![Interface utilisateur des flux de données présentant la liste des flux de données.](assets/bot-detection/datastream-list.png)

Dans la page des détails de la banque de données, sélectionnez l’option **[!UICONTROL Détection de robots]** sur le rail de droite.

![Option de détection des robots mise en surbrillance dans l’interface utilisateur des flux de données.](assets/bot-detection/bot-detection.png)

La page **[!UICONTROL Règles de détection des robots]** s’affiche.

![Paramètres de détection des robots dans la page des paramètres de la banque de données.](assets/bot-detection/bot-detection-page.png)

Sur la page Règles de détection des robots , vous pouvez configurer la détection des robots à l’aide des fonctionnalités suivantes :

* Utilisation de [!DNL [IAB/ABC International Spiders and Bots List]](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/).
* Création de vos propres règles de détection de robots.

### Utilisation de la liste internationale des robots (Robots) fournie par l’IAB/ABC {#iab-list}

La [ liste internationale des robots et araignées IAB/ABC ](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/) est une liste tierce, standard du secteur, d’araignées et de robots Internet, qui vous permet d’identifier le trafic automatisé, tel que les robots de moteur de recherche, les outils de surveillance et d’autres trafics non humains, que vous ne souhaitez peut-être pas afficher dans vos comptes d’analyses.

Pour configurer votre flux de données de manière à utiliser le [!DNL IAB/ABC International Spiders and Bots List], activez l’option **[!UICONTROL Utiliser la liste internationale des robots et araignées IAB/ABC pour la détection des robots dans cette banque de données]**, puis sélectionnez Enregistrer pour appliquer les paramètres de détection des robots à votre flux de données.

![Les araignées IAB et la liste de robots sont activées.](assets/bot-detection/bot-detection-list.png)

### Création de règles de détection de robots {#rules}

Outre l’utilisation de la [liste internationale des robots et araignées IAB/ABC ](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/), vous pouvez définir vos propres règles de détection des robots pour chaque flux de données.

Vous pouvez créer des règles de détection de robots basées sur les **adresses IP** et les **plages d’adresses IP**.

Si vous avez besoin de règles de détection de robots plus granulaires, vous pouvez combiner les conditions d’IP avec des conditions d’en-tête de requête. Les règles de détection de robots peuvent utiliser les en-têtes suivants :

| En-tête HTTP | Description |
| --- | --- |
| `user-agent` | En-tête qui permet aux serveurs et aux pairs réseau d’identifier l’application, le système d’exploitation, le fournisseur et/ou la version de l’agent utilisateur requérant. |
| `content-type` | Indique le type de support d’origine de la ressource (avant tout codage de contenu appliqué à l’envoi). |
| `referer` | Identifie l’adresse de la page web à partir de laquelle la ressource a été demandée. |
| `sec-ch-ua` | Fournit la marque et la version significative de chaque marque associée au navigateur dans une liste séparée par des virgules. |
| `sec-ch-ua-mobile` | Indique si le navigateur se trouve sur un appareil mobile. Il peut également être utilisé par un navigateur de bureau pour indiquer une préférence pour une expérience utilisateur mobile. |
| `sec-ch-ua-platform` | Fournit la plateforme ou le système d’exploitation sur lequel l’agent utilisateur est en cours d’exécution. Par exemple : Windows ou Android. |
| `sec-ch-ua-platform-version` | Fournit la version du système d’exploitation sur lequel l’agent utilisateur est en cours d’exécution. |
| `sec-ch-ua-arch` | Fournit l’architecture sous-jacente du processeur de l’agent utilisateur, telle qu’ARM ou x86. |
| `sec-ch-ua-model` | Indique le modèle d’appareil sur lequel le navigateur est en cours d’exécution. |
| `sec-ch-ua-bitness` | Fournit l’&quot;amertume&quot; de l’architecture sous-jacente du processeur de l’agent utilisateur. Il s’agit de la taille en bits d’un entier ou d’une adresse de mémoire, généralement 64 ou 32 bits. |
| `sec-ch-ua-wow64` | Indique si un binaire de l’agent utilisateur s’exécute en mode 32 bits sous Windows 64 bits. |

Pour créer une règle de détection de robots, procédez comme suit :

1. Sélectionnez **[!UICONTROL Ajouter une nouvelle règle]**.

   ![Écran des paramètres de détection des robots avec le bouton Ajouter une nouvelle règle surligné.](assets/bot-detection/bot-detection-new-rule.png)

2. Saisissez un nom pour la règle dans le champ **[!UICONTROL Nom de la règle]**.

   ![Écran de règle de détection des robots avec le nom de règle en surbrillance.](assets/bot-detection/rule-name.png)

3. Sélectionnez **[!UICONTROL Ajouter une nouvelle condition IP]** pour ajouter une nouvelle règle basée sur IP. Vous pouvez définir la règle par adresse IP ou plage d’adresses IP.

   ![Écran de règle de détection des robots avec le champ d’adresse IP en surbrillance.](assets/bot-detection/ip-address-rule.png)

   ![Écran de règle de détection de robots avec le champ de plage d’adresses IP surligné.](assets/bot-detection/ip-range-rule.png)

   >[!TIP]
   >
   >Les conditions IP sont basées sur une opération `OR` logique. Une demande est marquée comme provenant d’un robot si correspond à l’une des conditions IP que vous avez définies.

4. Si vous souhaitez ajouter des conditions d’en-tête à votre règle, sélectionnez **[!UICONTROL Ajouter un groupe de conditions d’en-tête]**, puis sélectionnez les en-têtes que la règle doit utiliser.

   ![Écran des règles de détection de robots avec les conditions d’en-tête surlignées.](assets/bot-detection/header-conditions.png)

   Ajoutez ensuite les conditions à utiliser pour l’en-tête sélectionné.

   ![Écran des règles de détection de robots avec les conditions d’en-tête surlignées.](assets/bot-detection/header-condition-rule.png)

5. Après avoir configuré les règles de détection de robots souhaitées, sélectionnez **[!UICONTROL Enregistrer]** pour que les règles soient appliquées à votre flux de données.

   ![Écran des règles de détection de robots avec les conditions d’en-tête surlignées.](assets/bot-detection/bot-detection-save.png)


## Exemples de règles de détection de robots {#examples}

Pour vous aider à prendre en main la détection des robots, vous pouvez utiliser les exemples présentés ci-dessous pour créer des règles de détection de robots.

### Détection des robots à partir d’une adresse IP {#one-ip}

Pour marquer comme trafic de robots toutes les requêtes provenant d’une adresse IP spécifique, créez une nouvelle règle de détection de robots qui évalue une seule adresse IP, comme illustré dans l’image ci-dessous.

![Règle de détection des robots basée sur une adresse IP.](assets/bot-detection/bot-detection-one-ip.png)

### Détection des robots à partir de deux adresses IP {#two-ip}

Pour marquer comme trafic de robots toutes les requêtes provenant de l’une des deux adresses IP spécifiques, créez une nouvelle règle de détection de robots qui évalue deux adresses IP, comme illustré dans l’image ci-dessous.

![Règle de détection des robots basée sur deux adresses IP.](assets/bot-detection/bot-detection-two-ips.png)

### Détection des robots à partir d’une plage d’adresses IP {#range}

Pour marquer comme trafic de robots toutes les requêtes provenant d’une adresse IP sur une plage spécifique, créez une nouvelle règle de détection de robots qui évalue une plage d’adresses IP entière, comme illustré dans l’image ci-dessous.

![Règle de détection de robots basée sur une plage IP.](assets/bot-detection/bot-detection-range.png)

### Détection des robots à partir d’une adresse IP et d’un en-tête de requête {#ip-header}

Pour marquer toutes les requêtes provenant d’une adresse IP spécifique et contenant un en-tête de requête spécifique comme trafic de robots, créez une règle de détection de robots comme illustré dans l’image ci-dessous.

Cette règle vérifie si la requête provient d’une adresse IP spécifique et si l’en-tête de la requête `referer` commence par `www.adobe.com`.

![Règle de détection de robots basée sur l’adresse IP et l’en-tête de requête.](assets/bot-detection/bot-detection-header-ip.png)

### Détection de robots selon plusieurs conditions {#multiple-conditions}

Vous pouvez créer des règles de détection de robots basées sur les éléments suivants :

* **Plusieurs conditions différentes** : différentes conditions sont évaluées en tant qu’opération `AND` logique, ce qui signifie que les conditions doivent être remplies simultanément pour que la demande soit identifiée comme provenant d’un robot.
* **Plusieurs conditions du même type** : les conditions du même type sont évaluées en tant qu’opération `OR` logique, ce qui signifie que si l’une des conditions est remplie, la demande est identifiée comme provenant d’un robot.

La règle affichée dans l’image ci-dessous identifie une demande d’origine de robots si les conditions suivantes sont remplies :

La requête provient de l’une des deux adresses IP, l’en-tête `referer` commence par `www.adobe.com` et l’en-tête `sec-ch-ua-mobile` identifie la requête comme provenant d’un navigateur de bureau.

![Règle de détection des robots basée sur plusieurs conditions.](assets/bot-detection/bot-detection-multiple.png)
