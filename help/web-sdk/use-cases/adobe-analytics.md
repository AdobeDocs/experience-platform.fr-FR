---
title: Envoi de données à Adobe Analytics à l’aide du SDK Web
description: Découvrez comment envoyer des données à Adobe Analytics avec le SDK Web de Adobe Experience Platform.
keywords: adobe analytics;analytics;données mappées;variables mappées;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 3%

---

# Envoi de données à Adobe Analytics à l’aide du SDK Web

Le SDK Web Adobe Experience Platform peut envoyer des données à Adobe Analytics par le biais du réseau Adobe Experience Platform Edge. Lorsque les données arrivent sur le réseau Edge, elles convertissent l’objet XDM dans un format qu’Adobe Analytics comprend.

## Groupe de champs XDM

Pour faciliter la capture des mesures Adobe Analytics les plus courantes, Adobe fournit un groupe de champs adapté à Adobe Analytics que vous pouvez utiliser. Pour plus d’informations sur ce schéma, voir [Groupe de champs de l’extension complète Adobe Analytics ExperienceEvent](/help/xdm/field-groups/event/analytics-full-extension.md).

## Mappage des variables

Le réseau Edge mappe automatiquement de nombreuses variables XDM. Voir [Mappage des variables Analytics dans le réseau Edge](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=fr) dans le guide de mise en oeuvre d’Adobe Analytics pour obtenir une liste complète des variables mappées automatiquement.

Toutes les variables qui ne sont pas automatiquement mappées sont disponibles sous la forme [Variables de données contextuelles](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=fr). Vous pouvez ensuite utiliser [Règles de traitement](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about.html) pour mapper des variables de données contextuelles à des variables Analytics. Par exemple, si vous aviez un schéma XDM personnalisé qui ressemblait à ce qui suit :

```js
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    "v0",
    "v1",
    "v2"
  ],
  arrayofobjects:[
    {
      obj1key:objval0
    },
    {
      obj2key:objval1
    }
  ]
}
```

Il s’agit alors des clés de données contextuelles disponibles dans l’interface Règles de traitement :

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.arrayofobjects.0.obj1key //objval0
a.x.arrayofobjects.1.obj2key //objval1
```

>[!NOTE]
>
>Avec la collection Edge Network, tous les événements sont envoyés à Analytics et à tous les autres services que vous avez configurés pour votre flux de données. Par exemple, si Analytics et Target sont tous deux configurés en tant que services et que vous effectuez des appels distincts pour la personnalisation et pour Analytics, les deux événements sont envoyés à Analytics et à Target. Ces événements sont enregistrés dans les rapports Analytics et peuvent affecter des mesures telles que le taux de rebond.

## Pages vues et appels de suivi des liens

Dans Adobe Analytics, AppMeasurement utilise des appels de méthode distincts pour les pages vues ([`t()` method](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/t-method.html)) et des appels de suivi des liens ([`tl()` method](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/tl-method.html)). Le SDK Web fournit uniquement la variable [`sendEvent`](../commands/sendevent/overview.md) pour envoyer les pages vues et le suivi des liens. Les données que vous incluez dans un événement déterminent s’il s’agit d’une [page vue](https://experienceleague.adobe.com/docs/analytics/components/metrics/page-views.html?lang=fr) ou [événement de page](https://experienceleague.adobe.com/docs/analytics/components/metrics/page-events.html) dans Adobe Analytics.

Par défaut, tous les événements sont considérés comme des pages vues dans Adobe Analytics. Si vous souhaitez définir un événement SDK Web sur un appel de suivi des liens Adobe Analytics, définissez les champs XDM suivants :

* **`web.webInteraction.URL`**: URL du lien.
* **`web.webInteraction.name`**: nom de la dimension Lien personnalisé, Lien de téléchargement ou Lien de sortie, selon la valeur de la variable `web.webInteraction.type`
* **`web.webInteraction.type`**: détermine le type de lien cliqué. Les valeurs valides sont les suivantes : `other` (Liens personnalisés), `download` (Liens de téléchargement) et `exit` (Liens de sortie).

Si vous activez [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) dans le `configure` , ces champs XDM sont renseignés pour vous.
