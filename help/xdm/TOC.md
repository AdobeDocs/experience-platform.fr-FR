---
audience: user
user-guide-title: Aide du système de modèle de données d’expérience (XDM)
breadcrumb-title: Guide de modèle de données d’expérience (XDM)
user-guide-description: Utilisez les classes de modèle de données d’expérience (XDM) et les groupes de champs de schéma pour normaliser les données d’expérience.
feature: Schémas
source-git-commit: dcfdc9c479e8a77296f7cb0bf9f5bb36e9261b75
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 44%

---


# Système de modèle de données d’expérience (XDM) {#xdm}

* [Présentation du système XDM](home.md)
* Schémas {#schema}
   * [Principes de base de la composition des schémas](schema/composition.md)
   * [Meilleures pratiques pour la modélisation des données](schema/best-practices.md)
   * [Contraintes de type de champ XDM](schema/field-constraints.md)
   * [Espace de noms dans XDM](./schema/namespaces.md)
   * [Dictionnaire des champs XDM](schema/field-dictionary.md)
   * Modèles de données du secteur {#industries}
      * [Présentation](./schema/industries/overview.md)
      * [ERD du modèle de données de vente au détail](./schema/industries/retail.md)
      * [ERD, modèle de données des services financiers](./schema/industries/financial.md)
      * [Modèle de données sur les voyages et l&#39;accueil ERD](./schema/industries/travel-hospitality.md)
* Classes {#classes}
   * [XDM Individual Profile](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
   * [Définition de segment](./classes/segment-definition.md)
* Groupes de champs de schéma {#field-groups}
   * Groupes de champs de profil {#profile}
      * [IdentityMap](./field-groups/profile/identitymap.md)
      * [Détails démographiques](./field-groups/profile/demographic-details.md)
      * [Coordonnées personnelles](./field-groups/profile/personal-contact-details.md)
      * [Détails de l’abonnement au segment](./field-groups/profile/segmentation.md)
      * [Détails du contact de travail](./field-groups/profile/work-contact-details.md)
      * [Préférences de confidentialité/personnalisation/marketing (Contenus)](./field-groups/profile/consents.md)
   * Groupes de champs de événement {#event}
      * [Détails de l’ID d’utilisateur final](./field-groups/event/enduserids.md)
      * [Détails de l&#39;Environnement](./field-groups/event/environment-details.md)
   * [Mises à jour du nom du groupe de champs](./field-groups/name-updates.md)
* Types des données {#data-types}
   * [Application](./data-types/application.md)
   * [Balise](./data-types/beacon.md)
   * [Détails du navigateur](./data-types/browser-details.md)
   * [Commerce](./data-types/commerce.md)
   * [Contenus et préférences](./data-types/consents.md)
   * [Appareil](./data-types/device.md)
   * [Adresse électronique](./data-types/email-address.md)
   * [Environnement](./data-types/environment.md)
   * [Champ de consentement générique](./data-types/consent-field.md)
   * [Champ de préférence marketing générique](./data-types/marketing-field.md)
   * [Champ de préférence marketing générique avec Abonnements](./data-types/marketing-field-subscriptions.md)
   * [Champ de préférence Personnalisation générique](./data-types/personalization-field.md)
   * [Géo](./data-types/geo.md)
   * [Cercle géographique](./data-types/geo-circle.md)
   * [Coordonnées géographiques](./data-types/geo-coordinates.md)
   * [Détails de l’interaction géographique](./data-types/geo-interaction-details.md)
   * [Forme géographique](./data-types/geo-shape.md)
   * [Identité](./data-types/identity.md)
   * [Mesure](./data-types/measure.md)
   * [Commande](./data-types/order.md)
   * [Article de paiement](./data-types/payment-item.md)
   * [Personne](./data-types/person.md)
   * [Nom de la personne](./data-types/person-name.md)
   * [Numéro de téléphone](./data-types/phone-number.md)
   * [Contexte de l’emplacement](./data-types/place-context.md)
   * [Détails de la publication](./data-types/poi-details.md)
   * [Interaction POI](./data-types/poi-interaction.md)
   * [Adresse postale](./data-types/postal-address.md)
   * [Recherche](./data-types/search.md)
   * [Abonnement](./data-types/subscription.md)
   * [Interaction Web](./data-types/web-interactions.md)
   * [Détails de la page Web](./data-types/webpage-details.md)
*  SchemasUI  {#ui}
   * [Présentation](./ui/overview.md)
   * [Explorer les ressources XDM](./ui/explore.md)
   * Créer et modifier des ressources {#resources}
      * [Schémas](./ui/resources/schemas.md)
      * [Classes](./ui/resources/classes.md)
      * [Groupes de champs](./ui/resources/field-groups.md)
      * [Types de données](./ui/resources/data-types.md)
   * Définir des champs {#fields}
      * [Présentation](./ui/fields/overview.md)
      * [Champs obligatoires](./ui/fields/required.md)
      * [Champs d’objet](./ui/fields/object.md)
      * [Champs de tableau](./ui/fields/array.md)
      * [Champs Enum](./ui/fields/enum.md)
      * [Champs d’identité](./ui/fields/identity.md)
      * [Champs de relation](./ui/fields/relationship.md)
   * [Générer des exemples de données XDM](./ui/sample.md)
   * [Exporter des schémas XDM](./ui/export.md)
* API Schema Registry {#api}
   * [Présentation](api/overview.md)
   * [Prise en main](api/getting-started.md)
   * [Schémas](api/schemas.md)
   * [Comportements](api/behaviors.md)
   * [Classes](api/classes.md)
   * [Groupes de champs de schéma](api/field-groups.md)
   * [Types de données](api/data-types.md)
   * [Descripteurs](api/descriptors.md)
   * [Unions](api/unions.md)
   * [Exporter/Importer](api/export-import.md)
   * [Sample data](api/sample-data.md)
   * [Journal d’audit](api/audit-log.md)
   * [Schémas ad hoc](api/ad-hoc.md)
   * [Mélanges (obsolète)](api/mixins.md)
   * [Annexe](api/appendix.md)
* Tutoriels {#tutorials}
   * [Création d’un schéma (IU)](tutorials/create-schema-ui.md)
   * [Création d’un schéma (API)](tutorials/create-schema-api.md)
   * [Définition d’une relation entre deux schémas (IU)](tutorials/relationship-ui.md)
   * [Définition d’une relation entre deux schémas (API)](tutorials/relationship-api.md)
   * [Création d’un schéma ad hoc (API)](tutorials/ad-hoc.md)
* [Guide de dépannage](troubleshooting-guide.md)
* [Référence d’API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)
* [Notes de mise à jour de la plateforme](https://docs.adobe.com/content/help/fr-FR/experience-platform/release-notes/latest.html)