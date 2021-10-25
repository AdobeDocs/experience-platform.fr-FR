---
title: Modèle de documentation en libre-service // Remplacer par le nom de votre destination
description: Utilisez ce modèle pour créer une documentation publique pour votre destination dans le catalogue Adobe Experience Platform. // Remplacer par le paragraphe de la section Présentation
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: 2b1cde9fc913be4d3bea71e7d56e0e5fe265a6be
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 3%

---

# YOURDESTINATION {#your-destination}

*Lorsque vous passez en revue ce modèle, remplacez ou supprimez tous les paragraphes en italique (à commencer par celui-ci).*

*Commencez par mettre à jour les métadonnées (titre et description) en haut de la page. Veuillez ignorer toutes les instances d&#39;UICONTROL sur cette page. Il s’agit d’une balise qui aide nos processus de traduction automatique à traduire correctement la page dans les multiples langues que nous prenons en charge. Nous ajouterons des balises à votre documentation après l’avoir soumise.*

## Présentation {#overview}

*Fournissez un bref aperçu de votre entreprise, y compris la valeur qu’elle fournit aux clients. Pour plus d’informations, incluez un lien vers la page d’accueil de votre documentation produit.*

>[!IMPORTANT]
>
>Cette page de documentation a été créée par la *YOURDESTINATION* équipe. Pour toute demande de renseignements ou de mise à jour, veuillez les contacter directement à l’adresse *Insertion d’un lien ou d’une adresse e-mail permettant d’accéder aux mises à jour*

## Conditions préalables {#prerequisites}

*Ajoutez dans cette section des informations sur tout ce dont les clients doivent être informés avant de commencer à configurer la destination dans l&#39;interface utilisateur Adobe Experience Platform. Il peut s’agir de :*

* *à ajouter à une liste d&#39;autorisations*
* *conditions requises pour le hachage par courrier électronique*
* *toute spécification de compte de votre côté*
* *comment obtenir une clé d’API pour se connecter à votre plate-forme*

*Si cela s’avère utile aux clients, vous pouvez créer un lien vers votre documentation pertinente.*

## Identités prises en charge {#supported-identities}

*Ajoutez des informations dans cette section sur les identités prises en charge par votre destination. Nous avons prérempli le tableau avec quelques valeurs standard. Supprimez les valeurs qui ne s’appliquent pas à votre destination et les valeurs qui ne sont pas préremplies.*

*YOURDESTINATION* prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur [identités](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr#getting-started).

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | Google Advertising ID | Sélectionnez l’identité cible GAID lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez l’identité cible IDFA lorsque votre identité source est un espace de noms IDFA. |
| ECID | Experience Cloud ID | Espace de noms qui représente ECID. Cet espace de noms peut également être référencé par les alias suivants : &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Voir le document suivant sur [ECID](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html) pour plus d’informations. |
| phone_sha256 | Numéros de téléphone hachés avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés SHA256. Lorsque votre champ source contient des attributs non hachés, cochez la case **[!UICONTROL Appliquer la transformation]** option, pour avoir [!DNL Platform] hachage automatique des données lors de l’activation. |
| email_lc_sha256 | Adresses électroniques hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses électroniques hachées SHA256. Lorsque votre champ source contient des attributs non hachés, cochez la case **[!UICONTROL Appliquer la transformation]** option, pour avoir [!DNL Platform] hachage automatique des données lors de l’activation. |
| extern_id | ID utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. |

{style=&quot;table-layout:auto&quot;}

## Type d’exportation {#export-type}

**Exportation de segments** - vous exportez tous les membres d’un segment (public) avec les identificateurs (nom, numéro de téléphone ou autres) utilisés dans le fichier *YOURDESTINATION* destination.

## Cas d’utilisation

Pour vous aider à mieux comprendre comment et quand utiliser le *YOURDESTINATION* destination, voici des exemples de cas d&#39;utilisation que les clients Adobe Experience Platform peuvent résoudre en utilisant cette destination.

### Cas d’utilisation #1

*Pour les plates-formes de messagerie mobile :*

*Une plate-forme de location et de vente de maisons veut envoyer des notifications mobiles aux appareils Android et iOS des clients afin de leur faire savoir qu&#39;il y a 100 annonces mises à jour dans la zone où ils recherchaient auparavant une location.*

### Cas d’utilisation n° 2

*Pour les plateformes de réseaux sociaux :*

*Une marque de vêtements d&#39;athlétisme veut atteindre les clients existants par le biais de leurs comptes sur les réseaux sociaux. La marque de vêtements peut assimiler des adresses électroniques de sa propre CRM à Adobe Experience Platform, créer des segments à partir de ses propres données hors ligne et envoyer ces segments à YOURDESTINATION, afin d&#39;afficher des publicités dans les flux de médias sociaux de ses clients.*

## Se connecter à la destination {#connect}

Pour vous connecter à cette destination, suivez les étapes décrites dans la section [didacticiel sur la configuration de destination](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html).

### Paramètres de connexion {#parameters}

En [configuration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) cette destination, vous devez fournir les informations suivantes :

*Ajoutez les champs que les clients doivent renseigner lors de la configuration d’une nouvelle destination. Ces champs sont spécifiques à la destination et dépendent de votre configuration dans le SDK de destination. Les champs de votre destination peuvent ne pas être les mêmes que ceux répertoriés ci-dessous.*

* **[!UICONTROL Nom]**: Nom par lequel vous reconnaîtrez cette destination dans le futur.
* **[!UICONTROL Description]**: Description qui vous aidera à identifier cette destination à l&#39;avenir.
* **[!UICONTROL ID de compte]**: Votre *YOURDESTINATION* ID de compte.


<!--

*Replace YOURDESTINATION with your destination name and TOBEFILLEDIN with the category that your destination belongs to.*

1. In **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, scroll to the ***TOBEFILLEDIN*** category. Select ***YOURDESTINATION***, then select **[!UICONTROL Configure]**.


    >[!NOTE]
    >
    >If a connection with this destination already exists, you can see an **[!UICONTROL Activate]** button on the destination card. For more information about the difference between **[!UICONTROL Activate]** and **[!UICONTROL Configure]**, refer to the [Catalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destinations-workspace.html#catalog) section of the destination workspace documentation.  

    ![Connect to YOURDESTINATION](./assets/yourdestination1.png)

2. In the **Account** step, if you had previously set up a connection to your *YOURDESTINATION* destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to *YOURDESTINATION*. Select **[!UICONTROL Connect to destination]** to log in and connect Adobe Experience Cloud to your *YOURDESTINATION* account.

    >[!NOTE]
    >
    >Adobe Experience Platform supports credentials validation in the authentication process and displays an error message if you input incorrect credentials to your ***YOURDESTINATION*** account. This ensures that you don't complete the workflow with incorrect credentials.

3. Once your credentials are confirmed and Adobe Experience Cloud is connected to your ***YOURDESTINATION*** account, you can select **[!UICONTROL Next]** to proceed to the **[!UICONTROL Setup]** step.

4. In the **[!UICONTROL Authentication]** step, enter a **[!UICONTROL Name]** and a **[!UICONTROL Description]** for your activation flow and fill your account ID. <br> Also in this step, you can select any marketing action that should apply to this destination. Marketing actions indicate the intent for which data will be exported to the destination. You can select from Adobe-defined marketing actions or you can create your own marketing action. For more information about marketing actions, see the [Data usage policies overview](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html).

    ![Connect to YOURDESTINATION](./assets/yourdestination2.png)

5. Your destination is now created. You can select **[!UICONTROL Save & Exit]** if you want to activate segments later on or you can select **[!UICONTROL Next]** to continue the workflow and select segments to activate. In either case, see the next section, [Activate segments](#activate-segments), for the rest of the workflow.

-->

## Activer les segments vers cette destination {#activate}

Lire [Activer les profils et les segments vers les destinations d’exportation de segments en flux continu](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

<!--

To activate segments to *YOURDESTINATION*, follow the steps below: 

1. In **[!UICONTROL Destinations > Browse]**, select the *YOURDESTINATION* destination where you want to activate your segments.

2. Click the name of the destination. This takes you to the Activate flow.
    ![activate-flow](./assets/yourdestination3.png)
    Note that if an activation flow already exists for a destination, you can see the segments that are currently being sent to the destination. Select **[!UICONTROL Edit activation]** in the right rail and follow the steps below to modify the activation details.
3. Select **[!UICONTROL Activate]**;
4. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to *YOURDESTINATION*.
    ![segments-to-destination](./assets/activate-segments-google-customer-match.png)
5.  In the **[!UICONTROL Mapping]** step, select which attributes and identities from the source XDM schema to map to the target schema. Select **[!UICONTROL Add new mapping]** and browse your schema, select identity namespaces and map them to the corresponding target identity.  
![identity mapping initial screen](./assets/gcm-identity-mapping.png) <br>&nbsp;
   *Plain text email address as primary identity*: If you have plain text (unhashed) email addresses as primary identity in your schema, select the email field in your **[!UICONTROL Source Attributes]** and map to the Email field in the right column under **[!UICONTROL Target Identities]**, as shown below. Set up a mapping between any other attributes you plan to use.
   ![identity mapping step](./assets/ssd-template-identity.png) <br>&nbsp;
6. On the **[!UICONTROL Segment schedule]** page, you can set the start date for sending data to the destination.
7. On the **[!UICONTROL Review]** page, you can see a summary of your selection. Select **[!UICONTROL Cancel]** to break up the flow, **[!UICONTROL Back]** to modify your settings, or **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

>[!IMPORTANT]
>
>In this step, Adobe Experience Platform checks for data usage policy violations. Shown below is an example where a policy is violated. You cannot complete the segment activation workflow until you have resolved the violation. For information on how to resolve policy violations, see [Policy enforcement](https://experienceleague.adobe.com/docs/experience-platform/data-governance/enforcement/auto-enforcement.html#enforcement) in the data governance documentation section.
 
![confirm-selection](./assets/data-policy-violation.png)

If no policy violations have been detected, select **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

![confirm-selection](./assets/gcm-review.png)

-->

## Données exportées {#exported-data}

*Ajoutez une note sur la manière dont les données sont exportées vers votre destination. Cela aiderait le client à s&#39;assurer qu&#39;il s&#39;est correctement intégré à votre destination. Par exemple, vous pouvez fournir un exemple JSON comme celui ci-dessous.*

```
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## Utilisation des données et gouvernance {#data-usage-governance}

Tout [!DNL Adobe Experience Platform] les destinations sont conformes aux règles d’utilisation des données lors de la gestion de vos données. Pour plus d’informations sur [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez [Présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Ressources supplémentaires {#additional-resources}

*Vous pouvez fournir d’autres liens vers la documentation de votre produit ou toute autre ressource que vous jugez importante pour le succès du client.*
