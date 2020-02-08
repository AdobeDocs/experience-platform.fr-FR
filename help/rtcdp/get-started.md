---
title: Prise en main de la plateforme de données clientes en temps réel d’Adobe
seo-title: Prise en main de la plateforme de données clientes en temps réel d’Adobe
description: Exemple de scénario pour la plateforme de données clientes en temps réel d’Adobe
seo-description: Exemple de scénario pour la plateforme de données clientes en temps réel d’Adobe
translation-type: tm+mt
source-git-commit: bf4ef1e8ceb38fe20365859bb28772263917030c

---


# Prise en main de la plateforme de données clientes en temps réel d’Adobe

Ce guide de prise en main vous guide tout au long d’un exemple d’implémentation de la plateforme de données clientes en temps réel d’Adobe (CDP en temps réel). Vous pouvez l’utiliser comme exemple lors de la configuration de votre propre implémentation. Bien que ce guide présente des exemples spécifiques, il fournit des liens vers des informations supplémentaires que vous pouvez utiliser lors de la création de votre configuration.

Cet exemple illustre la puissance de la plateforme de données clientes en temps réel d’Adobe, optimisée par Adobe Experience Platform, pour :

* Envoi de données à partir de sources multiples
* Fusionnez-les dans un profil client en temps réel unique
* Proposez une expérience cohérente, pertinente et personnalisée sur tous les périphériques.

## Cas d’utilisation

Luma, une entreprise de vêtements d’athlétisme, essaie toujours d’améliorer l’expérience de ses clients. Ils ont une nouvelle initiative pour augmenter les ventes liées aux cadeaux. Ils veulent également réduire la surexposition, comme les publicités agaçantes qui suivent les clients tout autour.

Actuellement, ils dépensent trop sur les médias qui ciblent à nouveau les éléments que le visiteur n’achètera pas. Par exemple, Luma ne souhaite pas recibler une personne avec un article destiné à un achat unique pour une autre personne.

Actuellement, les données de Luma sont dispersées entre plusieurs sources. Ils sont donc confrontés à des défis importants :

* L’organisation marketing doit travailler avec différentes équipes qui possèdent chacune une source de données, notamment un site Web, une application mobile, des systèmes de fidélité, un service de gestion de la relation client, etc.
* Au moment où l’équipe marketing accède aux données, elles sont souvent obsolètes et ne sont plus pertinentes pour les campagnes sensibles au temps.
* Ils doivent unifier les données pour cibler une personne, pas les canaux.

Par conséquent, Luma a les objectifs commerciaux suivants :

* Créez une vue unique en temps réel de leurs consommateurs à partir de leurs sources de données disparates.
* Personnalisez les campagnes marketing avec des messages pertinents sur différents canaux et périphériques.

Pour atteindre ces objectifs, l’équipe marketing doit être en mesure de gérer les données client à l’échelle.

Grâce au CDP en temps réel, optimisé par Adobe Experience Platform, l’entreprise de marketing de Luma peut :

1. Collecte des données à partir de plateformes disparates et s’assure qu’elles sont disponibles en aval pour d’autres activités marketing.
1. Créez une vue unique en temps réel de leurs clients, indépendamment de l’origine des données.
1. Conduisez une expérience cohérente, pertinente et personnalisée sur chaque point de contact.

## Étapes

Ce didacticiel comprend les étapes suivantes :

1. Créez le profil [du](#customer-profile)client.
1. [Personnalisez](#personalizing-the-user-experience) l’expérience utilisateur.
1. Utilisez [plusieurs sources](#using-multiple-data-sources)de données.
1. [Configurez une source](#configuring-a-data-source)de données.
1. [Collecte des données](#bringing-the-data-together-for-a-specific-customer) pour un client spécifique.
1. Configurez [des segments](#segments).
1. Configurez [des destinations](#destinations).
1. [Ajustez le profil sur plusieurs périphériques](#cross-device-identity-stitching).
1. [Analysez le profil](#analyzing-the-profile).

## Profil client

Lorsque les clients visitent votre site pour la première fois, vous n’en savez rien.

![image](assets/luma-site.png)

Lors de leur navigation, les données sont capturées en temps réel et envoyées non seulement à une suite de rapports dans Adobe Analytics, mais également directement à Adobe Experience Platform. Au fur et à mesure que les données sont collectées, vous commencez à former une vue unique du consommateur, basée sur les données comportementales du profil client en temps réel d’Experience Platform.

De nombreux visiteurs du site Web sont probablement des clients réguliers qui ont déjà effectué des achats auprès de Luma.  Il est important que Luma personnalise les messages et les offres pour s&#39;adresser aux nouveaux et aux nouveaux visiteurs, ainsi qu&#39;aux clients connus.

### Première visite du nouveau client

Par exemple, un visiteur non identifié accède à la section Hommes sur le site Luma et affiche un couple de chemises en peluche.

![image](assets/luma-sweatshirts.png)

Lorsque le client clique pour en savoir plus sur ces produits, ces consultations de produits sont collectées dans Adobe Analytics et envoyées à Experience Platform.

<!--![image](assets/luma-shirt-detail.png)-->

Luma peut mapper le comportement du visiteur à un profil utilisateur sur Adobe Experience Platform et commencer à assembler une vue plus riche du comportement de ce client.

### Obtention d’une vue plus détaillée du client

Alors que le client continue d&#39;interagir avec le site web, un tableau plus clair se dessine. Supposons, par exemple, que le visiteur ajoute un produit au panier et qu’il se connecte.

Lorsque le client se connecte, elle s’identifie comme Sarah Rose.

![image](assets/luma-login.png)

Deux identités sont fusionnées :

* Données de navigation anonymes
* Données existantes associées au compte de Sarah Rose

Les deux identités sont combinées dans un profil unique dans la plateforme d’expérience. Luma a maintenant une vision unifiée de ce consommateur.

En fonction du comportement de navigation du visiteur anonyme dans la section Hommes du site, on peut supposer que le client était un homme. Maintenant qu’elle est connectée, Luma reconnaît Sarah Rose. Luma utilise la puissance du profil client en temps réel pour affiner les messages qui lui sont transmis sur tous les canaux.

## Personnalisation de l’expérience utilisateur

Sarah est accueillie avec un message de fidélité et remerciée d’être membre du bronze avec plus d’informations sur les avantages et sur la façon d’augmenter son statut et ses points.

Elle clique sur la page d&#39;accueil pour en parcourir d&#39;autres.

![image](assets/luma-personal.png)

Sarah reçoit une expérience de page d’accueil personnalisée diffusée dynamiquement, en fonction de son profil client en temps réel dans Adobe Experience Platform.

Elle voit le contenu pertinent, grâce à la personnalisation Adobe Sensei dans Adobe Target, qui prend en compte ses achats passés et son affinité pour les vêtements et les accessoires de course. Luma adapte également le contenu du catalogue pour hommes à l’équipement de course pour hommes en fonction de sa dernière navigation.

Plus loin dans la page, Sarah affiche les produits phares, ainsi qu’un nouveau bac de Recommandations basé sur ses derniers articles consultés.

Ce contenu personnalisé permet à Sarah de rechercher rapidement les éléments appropriés. Cela augmente les conversions et offre une expérience client plus agréable.

### Ramener le client

Sarah se fait distraire et quitte le site, mettant fin à sa session. Luma peut utiliser ses données dans Adobe Experience Platform pour l’aider à revenir sur le site.

La plate-forme de données clientes Adobe en temps réel, optimisée par Adobe Experience Platform, est conçue pour la gestion de l’expérience client. Il permet aux entreprises de :

* Simplifier l’intégration et l’activation des données
* Gérer l’utilisation des données connues et inconnues
* Accélérer les utilisations du marketing à l’échelle

## Utilisation de plusieurs sources de données

L&#39;équipe de Luma dispose de toutes ses données comportementales et client en un seul endroit.

![image](assets/luma-dash.png)

Ils peuvent assimiler des données à partir de toutes les sources suivantes :

* Données des solutions Adobe Experience Cloud existantes
* Sources non Adobe, telles que le programme de fidélité de Luma, le centre d’appels et les données du système de point de vente
* Données en flux continu en temps réel à partir de sources de données Luma
* Données en temps réel provenant des solutions Adobe (aucune nouvelle balise n’est requise)

Toutes ces données provenant de sources disparates sont fusionnées dans un profil client unique et unifié.

## Configuration d’une source de données

Utilisez la plateforme de données clientes en temps réel pour importer de nouvelles sources de données dans la plateforme. Le CDP en temps réel comprend un catalogue de sources de données qui peut être ajouté au profil en quelques clics seulement.

![image](assets/luma-source-cat.png)

Par exemple, pour assimiler les données de gestion de la relation client de Luma, filtrez le catalogue par *gestion de la relation client* et tous les connecteurs prêts à l&#39;emploi contenant *de la gestion de la relation client* sont répertoriés. Pour ajouter des données Microsoft Dynamics CRM :

1. Autorisez la connexion.

   ![image](assets/luma-source-auth.png)

1. Choisissez ce que vous souhaitez importer dans une liste recommandée de tableaux prémappés XDM.

   <!--    ![image](assets/luma-source-import.png) -->

   Par exemple, sélectionnez **[!UICONTROL Contacts]**. Un aperçu des données des contacts se charge automatiquement afin que vous puissiez vous assurer que tout se présente comme prévu.

   La plate-forme Adobe Experience Manager effectue une grande partie du travail manuel en faisant automatiquement correspondre les champs standard au schéma de profil du modèle de données d’expérience (XDM).

1. Examinez les mappages de champs.

   <!--    ![image](assets/luma-source-mapping.png) -->

   Par exemple, vérifiez que le champ de courrier électronique des contacts est correctement mappé.\
   Vous pouvez prévisualiser les données et effectuer un mappage avancé.

1. Définissez un calendrier.

   ![image](assets/luma-source-sched.png)

C&#39;est fait. Vous venez d’ajouter Microsoft CRM en tant que source de données dans Experience Platform.

## Rassembler les données pour un client spécifique

Dans ce scénario, recherchez des profils pour Sarah Rose. Son profil s’affiche, avec le courrier électronique qu’elle utilisait pour se connecter.

<!-- ![image](assets/luma-find-profile.png) -->

Toutes les informations de profil que Luma possède sur les écrans Sarah. Cela inclut ses informations personnelles comme son adresse et son numéro de téléphone, ses préférences de communication et les segments pour lesquels elle est admissible.

| Catégorie | Description |
|---|---|
| Identités | Affiche les identités liées entre elles dans Platform à partir des interactions de Sarah avec Luma sur les canaux et les périphériques. Son ECID du site Web s’affiche. Son identité comprend également l’ECID de son application mobile, son ID de courrier électronique, un ID de gestion de la relation client du jeu de données Microsoft Dynamics récemment ajouté et un ID de fidélité transmis à Adobe Experience Platform par le système de fidélité Luma. |
| Événements | Affiche toutes les données d’interaction de Sarah avec la marque Luma. Cela inclut l&#39;élément qu&#39;elle vient de voir, tout ce qu&#39;elle a vu dans le passé, les courriels qu&#39;elle a reçus, ses interactions avec le centre d&#39;appels, et sur quel canal et quel périphérique chacune de ces interactions s&#39;est produite. |

Le profil CDP en temps réel réduit le flux de travail de l’équipe marketing Luma de semaines en minutes et déverrouille les possibilités de personnalisation en fonction de cette vue client à 360 degrés. Le profil fusionne les données comportementales du moment où elle a parcouru le site avant de se connecter, avec son profil client existant, créant ainsi une vue d’ensemble de Sarah.

L’équipe marketing peut utiliser ce profil client amélioré en temps réel pour mieux personnaliser l’expérience de Sarah et accroître sa fidélité à sa marque avec Luma.

## Segments

Les puissantes fonctionnalités de segmentation d’Adobe Experience Platform permettent aux spécialistes du marketing de combiner des attributs, des événements et des segments existants, en fonction des données capturées dans le profil client en temps réel.

<!-- ![image](assets/luma-segments.png) -->

Dans ce scénario, les interactions récentes de Sarah sur le site montrent un comportement différent de ses actions passées. Elle achète habituellement des vêtements pour femmes. Cependant, l’objet de sa charrue est un grand sweat-shirt pour homme.

L&#39;équipe de science de données Luma a créé des modèles autour de la propension à acheter. Un modèle indique un changement soudain de catégorie de vêtements (hommes/femmes, par exemple) ou de taille pour le consommateur existant. Le changement de comportement d’achat de Sarah suggère qu’elle n’achète pas pour elle-même.

<!-- ![image](assets/luma-gift.png) -->

### Définition d’un segment

Modifiez ou créez un segment représentant les abandons de panier qui semblent être en train d’acheter un cadeau :

```
Profile: Category != Preferred Category 
AND 
Product Size != Preferred Size 
in last 7 days.  
AND 
Abandoned Cart 
AND 
Loyalty member 
```

<!-- ![image](assets/luma-abandon.png)-->

Comme Sarah a ajouté un objet cadeau apparent dans le panier et l’a abandonné, Luma peut la cibler avec une offre gratuite d’emballage cadeau.

## Destinations

Lorsque vous avez ajouté le segment &quot;Abandons de panier&quot;, vous pouvez voir approximativement combien de personnes font partie de ce segment. Vous pouvez agir dessus et le rendre disponible pour la personnalisation sur plusieurs canaux.

Cliquez sur **[!UICONTROL Envoyer vers les destinations]**.

Dans le CDP en temps réel d’Adobe, Luma peut agir en toute transparence sur les segments d’audience afin de les personnaliser.\
Nous voyons ici toutes les destinations disponibles pour Luma pour envoyer cette destination à des solutions Adobe et non Adobe :

<!-- ![image](assets/luma-dest.png) -->

<!-- ### Privacy

Adobe Experience Platform includes privacy and security controls to ensure a segment is available to be activated to a particular destination based on its profile policy. If your activity violates policy, a warning appears. 

![image](assets/luma-dule.png)

With these controls, Experience Platform helps Luma be compliant with regulations and to market responsibly.  

Luma can confidently address regional and organizational requirements for managing known and unknown customer data with unified governance tools.  

These controls are flexible and can be modified to meet the requirements of Luma’s security and governance teams.
-->

### Sélection de destinations

Dans ce scénario, Luma souhaite cibler à nouveau cette audience avec une personnalisation sur ces destinations :

* Google, pour affichage
   <!--* Facebook -->
* Adobe Campaign, pour courrier électronique

<!-- ![image](assets/luma-sched-dest.png) -->

### Planification des destinations

Vous pouvez également planifier le début ou la fin du segment à un moment donné. Le segment sera publié et automatiquement mis à jour dans les plateformes configurées aux dates planifiées.

>[!NOTE]
>Si vous cliquez dans le champ de date, vous pouvez également planifier automatiquement les 90 jours d’expiration.

Cliquez sur **[!UICONTROL Enregistrer]** pour accéder à la page suivante.

Lorsqu’un client de ce public effectue un achat, son abonnement à ce public est supprimé en temps réel. Ils ne sont plus admissibles parce que leur statut a changé.

Cela permet au directeur de l&#39;équipe média Luma d&#39;économiser des centaines de milliers de dollars en n&#39;utilisant pas l&#39;inventaire pour un public qui n&#39;est pas qualifié.

### Canevas de flux de données

Lors de l’enregistrement, un canevas de flux de données visuel affiche le segment mappé du profil unifié aux trois destinations sélectionnées.

![image](assets/luma-flow.png)

## Pixellisation d’identité sur plusieurs périphériques

Sarah parcourt un site de médias sociaux sur son appareil mobile et voit une publicité Luma. Ça lui rappelle l&#39;objet qu&#39;elle a laissé dans son panier.

Plus tard, elle ouvre son courriel et voit les courriels reciblés. Elle clique sur un lien vers Luma à partir d’un courriel.

Ce lien conduit Sarah à la page d’accueil de Luma mobile, où elle voit une expérience hautement personnalisée pilotée par Adobe Target.

* Elle est accueillie comme membre du bronze.
* Elle voit le message &quot;Cadeau&quot;.
* Elle voit aussi le message &quot;Enveloppement gratuit de cadeaux&quot;, qui fait partie de ses avantages d&#39;adhésion au bronze.
* Elle est toujours ciblée sur l&#39;image de héros en raison de son affinité pour la course.

Elle achète le chandail, ajoute un emballage cadeau et écrit une note-cadeau. Elle a également la possibilité de se souvenir de cet événement et d&#39;obtenir un rappel l&#39;année prochaine pour se faire offrir à cette occasion. Elle dit oui, et est programmée dans une campagne par courriel l&#39;année suivante pour lui rappeler d&#39;acheter un autre cadeau.

Grâce aux capacités de suppression de l&#39;audience, Sarah ne sera pas ciblée avec ce pull pour hommes qui va de l&#39;avant.

## Analyse du profil

Les spécialistes du marketing Luma utilisent Adobe Experience Platform pour analyser le segment des donneurs de cadeaux sur le tableau de bord CDP en temps réel. Ils voient les résultats de cette initiative dans le temps et voient qu&#39;elle grandit. Les clients répondent aux offres et dépensent davantage d’argent.

Ces informations permettent aux spécialistes du marketing d’agir sur ce signal, alimenté par la disponibilité de ces données dans le CDP et l’association de clients comme Sarah au segment.

Luma utilise ces données CDP pour augmenter la fidélité et la satisfaction des clients.
