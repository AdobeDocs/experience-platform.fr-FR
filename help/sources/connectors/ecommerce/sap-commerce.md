---
title: Présentation de la source SAP Commerce
description: Découvrez comment connecter SAP Commerce à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
last-substantial-update: 2023-07-26T00:00:00Z
hide: true
hidefromtoc: true
badge: Version Beta
source-git-commit: 99edb8b2bcd4225235038e966a367d91375c961a
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 17%

---

# [!DNL SAP Commerce]

>[!NOTE]
>
>La source [!DNL SAP Commerce] est en version Beta. Voir [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

[[!DNL SAP Commerce]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), une solution de plateforme de commerce électronique basée sur le cloud pour les entreprises B2B et B2C est disponible dans le cadre du portefeuille d’expérience client SAP. [[!DNL SAP] Facturation d’abonnement](https://www.sap.com/products/financial-management/subscription-billing.html) est un produit appartenant au portefeuille qui permet une gestion complète du cycle de vie des abonnements avec des expériences de vente et de paiement simplifiées grâce à des intégrations normalisées.

Le [!DNL SAP Commerce] source vous permet d’ingérer des informations sur les clients et les contacts dans Platform à partir du [[!DNL SAP] Facturation d’abonnement](https://www.sap.com/products/financial-management/subscription-billing.html) Points de terminaison de l’API des partenaires commerciaux ci-dessous :

* [Clients](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [Contacts](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

En outre, si [!DNL SAP Commerce] est exécuté pour récupérer les données client, la variable [Relations client-contact](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) L’API est également appelée pour récupérer les informations de contact du client.

## Liste autorisée d’adresses IP {#ip-allow-list}

Il peut être nécessaire d’ajouter une liste d’adresses IP à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Conditions préalables {#prerequisites}

Avant d’apporter votre [!DNL SAP Commerce] pour Experience Platform, vous devez d’abord vous assurer que vous disposez des éléments suivants :

* A [!DNL SAP Subscription Billing] compte . Si vous ne disposez pas déjà d’un compte de facturation valide, contactez votre [!DNL SAP] gestionnaire de compte. Reportez-vous à la section [[!DNL SAP] Configuration de la plateforme](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) pour plus de détails.

* [!DNL SAP] clé de service. Le [!DNL SAP] la clé de service vous permet d’accéder à la [!DNL SAP Subscription Billing] API via Experience Platform. [!DNL SAP Commerce] requiert ce qui suit :
   * Identifiant client
   * Secret client
   * URL. Le modèle d’URL est le suivant : `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Cette valeur sera utilisée ultérieurement pour obtenir des valeurs pour `region` et `tokenEndpoint` lorsque vous [Créer une connexion de base](../../tutorials/api/create/ecommerce/sap-commerce.md#base-connection) à l’aide de l’API ou lorsque vous [Connectez-vous à [!DNL SAP Commerce] account](../../tutorials/ui/create/ecommerce/sap-commerce.md#connect-account) via l’interface utilisateur de Platform.

+++Sélectionnez cette option pour afficher un exemple de clé de service.

```json
{ 
    "url": "https://eu10.revenue.cloud.sap/api",
    "uaa": {
        "clientid": "XXX",
        "clientsecret": "XXX",
        "url": "https://subscriptionbilling.authentication.eu10.hana.ondemand.com",
        "identityzone": "subscriptionbilling",
        "identityzoneid": "XXX",
        "tenantid": "XXX",
        "tenantmode": "dedicated",
        "sburl": "https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
        "apiurl": "https://api.authentication.eu10.hana.ondemand.com",
        "verificationkey": "XXX",
        "xsappname": "XXX",
        "subaccountid": "XXX",
        "uaadomain": "authentication.eu10.hana.ondemand.com",
        "zoneid": "XXX",
        "credential-type": "binding-secret"
    },
    "vendor": "SAP"
}
```

+++

## Étapes suivantes

La documentation ci-dessous fournit des informations sur la connexion d’[!DNL SAP Commerce] à Platform à l’aide d’API ou de l’interface utilisateur :

* [Créer une connexion source et un flux de données à importer [!DNL SAP Commerce] données vers Platform à l’aide d’API](../../tutorials/api/create/ecommerce/sap-commerce.md).
* [Connectez-vous à [!DNL SAP Commerce] compte à Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/ecommerce/sap-commerce.md).
* [Création d’un flux de données pour une source à l’aide de l’interface utilisateur](../../tutorials/ui/dataflow/ecommerce.md)
