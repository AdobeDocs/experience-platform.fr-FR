---
title: Stripe
description: Découvrez comment ingérer des données de paiement de votre compte de Stripe vers Adobe Experience Platform
badge: Version bêta
exl-id: 191d217e-036d-491a-b7dd-abcad74625ba
source-git-commit: 62bcaa532cdec68a2f4f62e5784c35b91b7d5743
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 9%

---

# [!DNL Stripe]

>[!NOTE]
>
>La source [!DNL Stripe] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Des milliers d&#39;entreprises de toutes tailles utilisent [!DNL Stripe] en ligne et en personne pour accepter des paiements, générer de nouvelles sources de revenus et se développer à l&#39;échelle mondiale avec l&#39;aide de Adobe Experience Platform, Adobe Commerce et [!DNL Magento Open Source].

Utilisez la source [!DNL Stripe] de l’Experience Platform pour ingérer les données capturées pendant le flux d’achat par vos clients. Une fois ingérées, utilisez ces données pour créer des offres personnalisées et déverrouiller des informations commerciales plus riches.

>[!TIP]
>
>Pour toute question sur la source [!DNL Stripe] sur Experience Platform, contactez [!DNL Stripe] à l’adresse adobe-partenariat<span>@stripe.com.

>[!BEGINSHADEBOX]

**Exemple de cas d’utilisation pour la [!DNL Stripe] source**

Votre entreprise permet aux clients d&#39;acheter des articles sur votre boutique en ligne avec l&#39;option **acheter maintenant** et **payer plus tard** (en utilisant [!DNL Klarna], [!DNL Afterpay], [!DNL Affirm] ou [!DNL Zip]).

Utilisez la source de données [!DNL Stripe] pour analyser l’utilisation des options **Buy now** et **Pay later** et expérimenter des offres personnalisées à ces clients. Par exemple, pensez à recommander des éléments supplémentaires pour augmenter le nombre d’articles dans leur panier avant le passage en caisse.

>[!ENDSHADEBOX]

Lisez le document ci-dessous pour plus d’informations sur la configuration de votre compte source [!DNL Stripe], la récupération des informations d’identification nécessaires et la création de vos schémas.

## Conditions préalables {#prerequisites}

Les sections suivantes fournissent des informations sur la configuration prérequise que vous devez effectuer avant de connecter votre compte [!DNL Stripe] à Experience Platform.

### Récupération de votre jeton d’accès

* Connectez-vous au [[!DNL Stripe] tableau de bord](https://dashboard.stripe.com/login) à l’aide de votre adresse électronique et de votre mot de passe [!DNL Stripe].
* Dans le tableau de bord [!DNL Developers], sélectionnez **[!DNL API keys for developers]**.
* Sous l’onglet **Clés API**, sélectionnez **[!DNL Reveal test key]** pour afficher votre jeton d’accès.
* Vous pouvez désormais utiliser ce jeton comme jeton d’accès lors de la connexion de votre compte [!DNL Stripe] à un Experience Platform, à l’aide de l’API [!DNL Flow Service] ou de l’interface utilisateur Experience Platform.

### Collecter les informations d’identification requises

Pour connecter votre compte [!DNL Stripe] à un Experience Platform, vous devez fournir des valeurs pour les informations d’authentification suivantes :

>[!BEGINTABS]

>[!TAB API]

Vous devez fournir les informations d’identification suivantes lors de la connexion de votre compte [!DNL Stripe] à l’aide de l’API [!DNL Flow Service].

| Informations d’identification | Description |
| --- | --- |
| `accessToken` | Votre jeton d’authentification de code d’actualisation OAuth 2 [!DNL Stripe]. |
| `connectionSpec.id` | Identifiant de spécification de connexion de la source [!DNL Stripe]. Cet identifiant a été corrigé comme suit : `cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3`. |

>[!TAB UI]

Vous devez fournir les informations d’identification suivantes lors de la connexion de votre compte [!DNL Stripe] à l’aide de l’interface utilisateur de l’Experience Platform.

| Informations d’identification | Description |
| --- | --- |
| Jeton d’accès | Votre jeton d’authentification de code d’actualisation OAuth 2 [!DNL Stripe]. |

>[!ENDTABS]

Pour plus d&#39;informations sur l&#39;utilisation des API [!DNL Stripe], consultez la [[!DNL Stripe] documentation sur les clés d&#39;API](https://docs.stripe.com/keys).

### Création d’un schéma de modèle de données d’expérience (XDM)

La source [!DNL Stripe] prend en charge l’ingestion de données à partir des chemins de ressources suivants :

* Frais
* Abonnements
* Remboursement
* Transactions de solde
* Clients
* Prix

Vous devez créer un schéma XDM pour décrire un jeu de données, qui peut stocker les champs et les types de données qui seront envoyés de [!DNL Stripe] à l’Experience Platform.

>[!BEGINTABS]

>[!TAB Frais]

Dans [!DNL Stripe], **charges** représente les tentatives de transfert d&#39;argent dans votre [!DNL Stripe]. Pour plus d’informations sur les attributs de charge spécifiques, consultez le [[!DNL Stripe] guide de l’API sur les frais](https://docs.stripe.com/api/charges) .

+++Sélectionnez cette option pour afficher l’objet Charge du Stripe

```json
{
  "id": "ch_3MmlLrLkdIwHu7ix0snN0B15",
  "object": "charge",
  "amount": 1099,
  "amount_captured": 1099,
  "amount_refunded": 0,
  "application": null,
  "application_fee": null,
  "application_fee_amount": null,
  "balance_transaction": "txn_3MmlLrLkdIwHu7ix0uke3Ezy",
  "billing_details": {
    "address": {
      "city": null,
      "country": null,
      "line1": null,
      "line2": null,
      "postal_code": null,
      "state": null
    },
    "email": null,
    "name": null,
    "phone": null
  },
  "calculated_statement_descriptor": "Stripe",
  "captured": true,
  "created": 1679090539,
  "currency": "usd",
  "customer": null,
  "description": null,
  "disputed": false,
  "failure_balance_transaction": null,
  "failure_code": null,
  "failure_message": null,
  "fraud_details": {},
  "invoice": null,
  "livemode": false,
  "metadata": {},
  "on_behalf_of": null,
  "outcome": {
    "network_status": "approved_by_network",
    "reason": null,
    "risk_level": "normal",
    "risk_score": 32,
    "seller_message": "Payment complete.",
    "type": "authorized"
  },
  "paid": true,
  "payment_intent": null,
  "payment_method": "card_1MmlLrLkdIwHu7ixIJwEWSNR",
  "payment_method_details": {
    "card": {
      "brand": "visa",
      "checks": {
        "address_line1_check": null,
        "address_postal_code_check": null,
        "cvc_check": null
      },
      "country": "US",
      "exp_month": 3,
      "exp_year": 2024,
      "fingerprint": "mToisGZ01V71BCos",
      "funding": "credit",
      "installments": null,
      "last4": "4242",
      "mandate": null,
      "network": "visa",
      "three_d_secure": null,
      "wallet": null
    },
    "type": "card"
  },
  "receipt_email": null,
  "receipt_number": null,
  "receipt_url": "https://pay.stripe.com/receipts/payment/CAcaFwoVYWNjdF8xTTJKVGtMa2RJd0h1N2l4KOvG06AGMgZfBXyr1aw6LBa9vaaSRWU96d8qBwz9z2J_CObiV_H2-e8RezSK_sw0KISesp4czsOUlVKY",
  "refunded": false,
  "review": null,
  "shipping": null,
  "source_transfer": null,
  "statement_descriptor": null,
  "statement_descriptor_suffix": null,
  "status": "succeeded",
  "transfer_data": null,
  "transfer_group": null
}
```

+++

>[!TAB Abonnements]

Dans [!DNL Stripe], vous pouvez utiliser **abonnements** pour facturer un client de manière récurrente. Pour plus d’informations sur les attributs d’abonnement spécifiques, consultez le [[!DNL Stripe] guide de l’API sur les abonnements](https://docs.stripe.com/api/subscriptions) .

+++Sélectionner pour afficher l’objet d’abonnement du Stripe

```json
{
  "id": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
  "object": "subscription",
  "application": null,
  "application_fee_percent": null,
  "automatic_tax": {
    "enabled": false,
    "liability": null
  },
  "billing_cycle_anchor": 1679609767,
  "billing_thresholds": null,
  "cancel_at": null,
  "cancel_at_period_end": false,
  "canceled_at": null,
  "cancellation_details": {
    "comment": null,
    "feedback": null,
    "reason": null
  },
  "collection_method": "charge_automatically",
  "created": 1679609767,
  "currency": "usd",
  "current_period_end": 1682288167,
  "current_period_start": 1679609767,
  "customer": "cus_Na6dX7aXxi11N4",
  "days_until_due": null,
  "default_payment_method": null,
  "default_source": null,
  "default_tax_rates": [],
  "description": null,
  "discount": null,
  "ended_at": null,
  "invoice_settings": {
    "issuer": {
      "type": "self"
    }
  },
  "items": {
    "object": "list",
    "data": [
      {
        "id": "si_Na6dzxczY5fwHx",
        "object": "subscription_item",
        "billing_thresholds": null,
        "created": 1679609768,
        "metadata": {},
        "plan": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "plan",
          "active": true,
          "aggregate_usage": null,
          "amount": 1000,
          "amount_decimal": "1000",
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "interval": "month",
          "interval_count": 1,
          "livemode": false,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "tiers_mode": null,
          "transform_usage": null,
          "trial_period_days": null,
          "usage_type": "licensed"
        },
        "price": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "price",
          "active": true,
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "custom_unit_amount": null,
          "livemode": false,
          "lookup_key": null,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "recurring": {
            "aggregate_usage": null,
            "interval": "month",
            "interval_count": 1,
            "trial_period_days": null,
            "usage_type": "licensed"
          },
          "tax_behavior": "unspecified",
          "tiers_mode": null,
          "transform_quantity": null,
          "type": "recurring",
          "unit_amount": 1000,
          "unit_amount_decimal": "1000"
        },
        "quantity": 1,
        "subscription": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
        "tax_rates": []
      }
    ],
    "has_more": false,
    "total_count": 1,
    "url": "/v1/subscription_items?subscription=sub_1MowQVLkdIwHu7ixeRlqHVzs"
  },
  "latest_invoice": "in_1MowQWLkdIwHu7ixuzkSPfKd",
  "livemode": false,
  "metadata": {},
  "next_pending_invoice_item_invoice": null,
  "on_behalf_of": null,
  "pause_collection": null,
  "payment_settings": {
    "payment_method_options": null,
    "payment_method_types": null,
    "save_default_payment_method": "off"
  },
  "pending_invoice_item_interval": null,
  "pending_setup_intent": null,
  "pending_update": null,
  "quantity": 1,
  "schedule": null,
  "start_date": 1679609767,
  "status": "active",
  "test_clock": null,
  "transfer_data": null,
  "trial_end": null,
  "trial_settings": {
    "end_behavior": {
      "missing_payment_method": "create_invoice"
    }
  },
  "trial_start": null
}
```

+++

>[!TAB Remboursements]

Dans [!DNL Stripe], vous pouvez utiliser les **remboursements** pour rembourser des frais créés précédemment. Pour plus d’informations sur les attributs de remboursement spécifiques, consultez le [[!DNL Stripe] guide de l’API sur les remboursements](https://docs.stripe.com/api/refunds) .

+++Sélectionner pour afficher l’objet de remboursement du Stripe

```json
{
  "id": "re_1Nispe2eZvKYlo2Cd31jOCgZ",
  "object": "refund",
  "amount": 1000,
  "balance_transaction": "txn_1Nispe2eZvKYlo2CYezqFhEx",
  "charge": "ch_1NirD82eZvKYlo2CIvbtLWuY",
  "created": 1692942318,
  "currency": "usd",
  "destination_details": {
    "card": {
      "reference": "123456789012",
      "reference_status": "available",
      "reference_type": "acquirer_reference_number",
      "type": "refund"
    },
    "type": "card"
  },
  "metadata": {},
  "payment_intent": "pi_1GszsK2eZvKYlo2CfhZyoZLp",
  "reason": null,
  "receipt_number": null,
  "source_transfer_reversal": null,
  "status": "succeeded",
  "transfer_reversal": null
}
```

+++

>[!TAB Transactions de solde]

Dans [!DNL Stripe], les **transactions de solde** représentent le mouvement des fonds entre vos comptes [!DNL Stripe]. Pour plus d’informations sur les attributs de transaction des soldes spécifiques, consultez le [[!DNL Stripe] guide de l’API sur les transactions de solde](https://docs.stripe.com/api/balance_transactions) .

+++Sélectionnez cette option pour afficher l’objet Transaction du solde du Stripe

```json
{
  "id": "txn_1MiN3gLkdIwHu7ixxapQrznl",
  "object": "balance_transaction",
  "amount": -400,
  "available_on": 1678043844,
  "created": 1678043844,
  "currency": "usd",
  "description": null,
  "exchange_rate": null,
  "fee": 0,
  "fee_details": [],
  "net": -400,
  "reporting_category": "transfer",
  "source": "tr_1MiN3gLkdIwHu7ixNCZvFdgA",
  "status": "available",
  "type": "transfer"
}
```

+++

>[!TAB Clients]

Dans [!DNL Stripe], **clients** représentent un client donné de votre entreprise. Pour plus d’informations sur des attributs de client spécifiques, consultez le [[!DNL Stripe] guide de l’API sur les clients](https://docs.stripe.com/api/customers) pour plus d’informations sur des attributs de client spécifiques.

+++Sélectionner pour afficher l’objet client du Stripe

```json
{
  "id": "cus_NffrFeUfNV2Hib",
  "object": "customer",
  "address": null,
  "balance": 0,
  "created": 1680893993,
  "currency": null,
  "default_source": null,
  "delinquent": false,
  "description": null,
  "discount": null,
  "email": "jennyrosen@example.com",
  "invoice_prefix": "0759376C",
  "invoice_settings": {
    "custom_fields": null,
    "default_payment_method": null,
    "footer": null,
    "rendering_options": null
  },
  "livemode": false,
  "metadata": {},
  "name": "Jenny Rosen",
  "next_invoice_sequence": 1,
  "phone": null,
  "preferred_locales": [],
  "shipping": null,
  "tax_exempt": "none",
  "test_clock": null
}
```

+++

>[!TAB Prix]

Dans [!DNL Stripe], les **prix** représentent le coût unitaire, la devise et le cycle de facturation facultatif pour les achats récurrents et uniques de produits. Lisez le [[!DNL Stripe] guide de l’API sur les prix](https://docs.stripe.com/api/prices) pour plus d’informations sur les attributs de prix spécifiques.

+++Sélectionner pour afficher l’objet Prix du Stripe

```json
{
  "id": "price_1MoBy5LkdIwHu7ixZhnattbh",
  "object": "price",
  "active": true,
  "billing_scheme": "per_unit",
  "created": 1679431181,
  "currency": "usd",
  "custom_unit_amount": null,
  "livemode": false,
  "lookup_key": null,
  "metadata": {},
  "nickname": null,
  "product": "prod_NZKdYqrwEYx6iK",
  "recurring": {
    "aggregate_usage": null,
    "interval": "month",
    "interval_count": 1,
    "trial_period_days": null,
    "usage_type": "licensed"
  },
  "tax_behavior": "unspecified",
  "tiers_mode": null,
  "transform_quantity": null,
  "type": "recurring",
  "unit_amount": 1000,
  "unit_amount_decimal": "1000"
}
```

+++

>[!ENDTABS]


### Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

### Configuration des autorisations sur Experience Platform

Les autorisations **[!UICONTROL Afficher les sources]** et **[!UICONTROL Gérer les sources]** doivent être activées pour votre compte pour connecter votre compte [!DNL Stripe] à un Experience Platform. Contactez votre administrateur de produit pour obtenir les autorisations nécessaires. Pour plus d’informations, consultez le [guide de l’interface utilisateur du contrôle d’accès](../../../access-control/ui/overview.md).

## Étapes suivantes

Une fois la configuration prérequise terminée, vous pouvez procéder à la connexion et ingérer vos données [!DNL Stripe] vers l’Experience Platform. Lisez les guides suivants pour savoir comment ingérer des données de paiement [!DNL Stripe] vers Experience Platform à l’aide d’API ou de l’interface utilisateur :

* [ Ingérez des données de paiements de votre compte de Stripe vers Experience Platform à l’aide de l’API Flow Service](../../tutorials/api/create/payments/stripe.md).
* [ Ingérez des données de paiements de votre compte de Stripe vers Experience Platform à l’aide de l’interface utilisateur ](../../tutorials/ui/create/payments/stripe.md).
