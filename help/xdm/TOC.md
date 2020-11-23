---
product: experience-platform
audience: user
user-guide-title: Aide du système de modèle de données d’expérience (XDM)
breadcrumb-title: Guide de Data Model (XDM)
user-guide-description: Utilisez les classes et les mixins d’Experience Data Model (XDM) pour normaliser les données d’expérience.
translation-type: tm+mt
source-git-commit: 321dc16a1296aeb28ba78825f191a0368df16547
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 66%

---


# Système de modèle de données d’expérience (XDM) {#xdm}

* [Présentation du système XDM](home.md)
* Schémas {#schema}
   * [Principes de base de la composition des schémas](schema/composition.md)
   * [Meilleures pratiques pour la modélisation des données](schema/best-practices.md)
   * [Contraintes de type de champ XDM](schema/field-constraints.md)
   * [Dictionnaire des champs XDM](schema/field-dictionary.md)
   * Cas d&#39;utilisation de schéma {#use-cases}
      * [Mélange de consentement de confidentialité](schema/privacy-consent.md)
* Classes {#classes}
   * [XDM Individual Profile](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
* Mélanges {#mixins}
   * Mélanges profils {#profile}
      * [IdentityMap](./mixins/profile/identitymap.md)
      * [Détails démographiques](./mixins/profile/person-details.md)
      * [Coordonnées personnelles](./mixins/profile/personal-details.md)
      * [Détails de l’abonnement au segment](./mixins/profile/segmentation.md)
      * [Détails du contact de travail](./mixins/profile/work-details.md)
   * Mélanges événements {#event}
      * [Détails de l’ID d’utilisateur final](./mixins/event/enduserids.md)
      * [Détails de l&#39;Environnement](./mixins/event/environment-details.md)
   * [Mises à jour des noms mixtes](./mixins/name-updates.md)
* Types des données {#data-types}
   * [Balise](./data-types/beacon.md)
   * [Détails du navigateur](./data-types/browser-details.md)
   * [Appareil](./data-types/device.md)
   * [Adresse électronique](./data-types/email-address.md)
   * [Environnement](./data-types/environment.md)
   * [Géo](./data-types/geo.md)
   * [Cercle géographique](./data-types/geo-circle.md)
   * [Coordonnées géographiques](./data-types/geo-coordinates.md)
   * [Détails de l’interaction géographique](./data-types/geo-interaction-details.md)
   * [Forme géographique](./data-types/geo-shape.md)
   * [Identité](./data-types/identity.md)
   * [Nom de la personne](./data-types/person-name.md)
   * [Numéro de téléphone](./data-types/phone-number.md)
   * [Contexte de l’emplacement](./data-types/place-context.md)
   * [Détails de la publication](./data-types/poi-details.md)
   * [Interaction POI](./data-types/poi-interaction.md)
   * [Adresse postale](./data-types/postal-address.md)
* API Schema Registry {#api}
   * [Présentation](api/overview.md)
   * [Prise en main](api/getting-started.md)
   * [Schémas](api/schemas.md)
   * [Classes](api/classes.md)
   * [Mélanges](api/mixins.md)
   * [Types des données](api/data-types.md)
   * [Descripteurs](api/descriptors.md)
   * [Unions](api/unions.md)
   * [Schémas ad hoc](api/ad-hoc.md)
   * [Annexe](api/appendix.md)
* Tutoriels {#tutorials}
   * [Création d’un schéma (API)](tutorials/create-schema-api.md)
   * [Création d’un schéma (IU)](tutorials/create-schema-ui.md)
   * [Définition d’une relation entre deux schémas (API)](tutorials/relationship-api.md)
   * [Définition d’une relation entre deux schémas (IU)](tutorials/relationship-ui.md)
   * [Création d’un schéma ad hoc (API)](tutorials/ad-hoc.md)
* [Guide de dépannage](troubleshooting-guide.md)
* [Référence d’API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)
* [Notes de mise à jour de la plateforme](https://docs.adobe.com/content/help/fr-FR/experience-platform/release-notes/latest.html)