---
title: Onglet Résumé
description: Découvrez comment utiliser l’onglet Résumé dans Adobe Experience Platform Debugger.
keywords: debugger;extension Experience Platform Debugger;chrome;extension;récapitulatif;effacer;requêtes;écran récapitulatif;solution;informations;analytics;target;dtm;audience manager;launch;service d’identification
seo-description: Experience Platform Debugger Summary Screen
seo-title: Summary Tab
uuid: 46b17eaa-b611-43cf-8c6a-67b2e9b9d940
exl-id: 91234125-15c4-4111-9ee4-f3af093a3c4d
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 83%

---

# Onglet Résumé

Pour exécuter Adobe Experience Platform Debugger, ouvrez la page à examiner dans le navigateur, puis sélectionnez l’icône (![](images/start-icon.jpg)) sur la barre de votre navigateur. L’extension s’ouvre sur l’onglet **Summary**.

![](images/summary.jpg)

Cet écran affiche également des informations sur chaque solution Adobe Experience Cloud. Les informations affichées varient selon la solution, mais comprennent généralement des données telles que la bibliothèque et la version de la solution (par exemple, « AppMeasurement v2.9 ») et les identifiants de compte (tels que l’identifiant de suite de rapports Analytics, le code client Target, l’identifiant partenaire d’Audience Manager, etc.).

## Informations affichées dans Experience Platform Debugger

Experience Platform Debugger affiche les informations suivantes pour chaque solution :

**Adobe Analytics**

<table id="table_BEB9CC58E59D4D86BC895A8A51D84A2C"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Suite(s) de rapports </p> </td> 
   <td colname="col2"> <p>Une <a href="https://experiencecloud.adobe.com/resources/help/fr_FR/reference/report_suites_admin.html" format="html" scope="external">suite de rapports</a> définit les rapports indépendants et complets d’un site web choisi, d’un ensemble de sites web ou d’un sous-ensemble de pages web. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Version </p> </td> 
   <td colname="col2"> <p>Version d’<a href="https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=fr" format="html" scope="external"> AppMeasurement</a> définie pour la page. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Version du visiteur </p> </td> 
   <td colname="col2"> <p>Version de la bibliothèque <a href="https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html?lang=fr" format="html" scope="external">d’identifiants visiteur</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nom de la page </p> </td> 
   <td colname="col2"> <p>Variable <a href="https://experiencecloud.adobe.com/resources/help/fr_FR/sc/implement/pageName.html" format="html" scope="external">pageName</a> envoyée à Analytics qui contient un nom convivial du site. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Modules </p> </td> 
   <td colname="col2"> <p>Modules chargés par Adobe Analytics. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Audience Manager**

<table id="table_784AEABADBDA4D14BB9A7A9CB9EF07C3"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Partenaire </p> </td> 
   <td colname="col2"> <p><a href="https://experiencecloud.adobe.com/resources/help/fr_FR/aam/r_dil_get_partner.html" format="html" scope="external">Nom du partenaire</a> pour l’instance DIL. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Version </p> </td> 
   <td colname="col2"> <p><a href="https://experiencecloud.adobe.com/resources/help/fr_FR/aam/r_api_return_versions_dil.html" format="html" scope="external">Numéro de version</a> de l’instance DIL. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>UUID </p> </td> 
   <td colname="col2"> <p><a href="https://experiencecloud.adobe.com/resources/help/fr_FR/aam/ids-in-aam.html" format="html" scope="external">ID utilisateur unique</a> associé à l’instance DIL. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Balises Adobe Experience Platform**

<table id="table_E9574975444A407887E26514D1BB1601"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Nom </p> </td> 
   <td colname="col2"> <p>Nom de la balise <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html?lang=fr" format="https" scope="external"> property</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Version </p> </td> 
   <td colname="col2"> <p>Version de Turbine</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Date de version </p> </td> 
   <td colname="col2"> <p>Date de version de la balise <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/libraries.html?lang=fr" format="https" scope="external"> library</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Environnement </p> </td> 
   <td colname="col2"> <p>Environnement <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html?lang=fr" format="https" scope="external"></a> utilisé par la bibliothèque de balises </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Extensions </p> </td> 
   <td colname="col2"> <p>Extensions utilisées sur la page. </p> </td> 
  </tr> 
 </tbody> 
</table>

**SDK web Adobe Experience Platform**

<table id="table_DC76D63FA6EF4891906B9E1D3E4A8A6C"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Version de la bibliothèque </p> </td> 
   <td colname="col2"> <p>Numéro de <a href="https://experienceleague.adobe.com/docs/experience-platform/web-sdk/extension/web-sdk-ext-release-notes.html" format="html" scope="external">version de la bibliothèque</a> SDK web Adobe Experience Platform. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Namespace (Espace de nom du visiteur)</p> </td> 
   <td colname="col2"> <p>Le nom identifié dans l’extension.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>ID de propriété </p> </td> 
   <td colname="col2"> <p>Nom de la propriété de balise spécifié dans l’extension </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Domaine Edge </p> </td> 
   <td colname="col2"> <p>Le domaine vers lequel/à partir duquel l’extension Adobe Experience Platform envoie et reçoit des données. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Identifiant IMS de l’organisation </p> </td> 
   <td colname="col2"> <p>L’organisation à laquelle vous souhaitez envoyer les données chez Adobe, comme indiqué dans l’extension. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Journalisation activée </p> </td> 
   <td colname="col2"> <p>Indique si la journalisation a été activée pour cette propriété.</p> </td> 
  </tr> 
 </tbody> 
</table>

**Service Adobe Experience Cloud ID**

<table id="table_274CFCEFA8F34D16BB546B4669EC0209"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Experience Cloud Org ID (ID d’organisation d’Experience Cloud) </p> </td> 
   <td colname="col2"> <p>Votre <a href="https://experiencecloud.adobe.com/resources/help/fr_FR/mcvid/" format="https" scope="external"> ID d’organisation</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Version </p> </td> 
   <td colname="col2"> <p>Version de la bibliothèque<a href="https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html?lang=fr" format="html" scope="external"> d’identifiants visiteur</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Target**

<table id="table_D30E0CD20FB04E41862B22655136E043"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Code client </p> </td> 
   <td colname="col2"> <p>Votre <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/deploy-at-js/implementing-target-without-a-tag-manager.html" format="html" scope="external"> code client </a>Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Version </p> </td> 
   <td colname="col2"> <p>Votre version actuelle d’<a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/target-atjs-versions.html" format="html" scope="external"> at.js</a> ou de mbox.js. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nom global de la demande </p> </td> 
   <td colname="col2"> <p>La<a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/global-mbox/understanding-global-mbox.html" format="html" scope="external"> mbox globale</a> désigne l’appel de serveur unique effectué en haut de chaque page web dans votre mise en œuvre Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Événement de chargement de page </p> </td> 
   <td colname="col2"> <p>Type d’<a href="https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target/overview.html" format="html" scope="external">événement</a> qui se déclenche au chargement de la page. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nom de la demande </p> </td> 
   <td colname="col2"> <p>Le nom d’une requête autour d’un <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/global-mbox/understanding-global-mbox.html" format="html" scope="external"> emplacement</a> sur la page. Disponible sans authentification uniquement si vous implémentez le récepteur d’événements de débogage dans votre gestionnaire de codes ou de balises et si vous activez les <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> jetons de réponse</a> nécessaires dans l’interface utilisateur de Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nom de l’activité </p> </td> 
   <td colname="col2"> <p>Nom de la <a href="https://experienceleague.adobe.com/docs/target/using/activities/activities.html" format="html" scope="external"> campagne ou de l’activité</a> de Target. Disponible sans authentification uniquement si vous implémentez le récepteur d’événements de débogage dans votre gestionnaire de codes ou de balises et si vous activez les <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> jetons de réponse</a> nécessaires dans l’interface utilisateur de Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Code d’activité </p> </td> 
   <td colname="col2"> <p>ID de l’activité de Target. Disponible sans authentification uniquement si vous implémentez le récepteur d’événements de débogage dans votre gestionnaire de codes ou de balises et si vous activez les <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> jetons de réponse</a> nécessaires dans l’interface utilisateur de Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nom de l’expérience </p> </td> 
   <td colname="col2"> <p>Nom de <a href="https://experienceleague.adobe.com/docs/target/using/experiences/experiences.html" format="html" scope="external"> l’expérience</a> de Target. Disponible sans authentification uniquement si vous implémentez le récepteur d’événements de débogage dans votre gestionnaire de codes ou de balises et si vous activez les <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> jetons de réponse</a> nécessaires dans l’interface utilisateur de Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>ID d’expérience </p> </td> 
   <td colname="col2"> <p>ID de l’expérience Target. Disponible sans authentification uniquement si vous implémentez le récepteur d’événements de débogage dans votre gestionnaire de codes ou de balises et si vous activez les <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> jetons de réponse</a> nécessaires dans l’interface utilisateur de Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nom de l’offre</p> </td> 
   <td colname="col2"> <p>Nom de <a href="https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html" format="html" scope="external"> l’offre</a> de Target. Disponible sans authentification uniquement si vous implémentez le récepteur d’événements de débogage dans votre gestionnaire de codes ou de balises et si vous activez les <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> jetons de réponse</a> nécessaires dans l’interface utilisateur de Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>ID d’offre </p> </td> 
   <td colname="col2"> <p>ID de l’offre de Target. Disponible sans authentification uniquement si vous implémentez le récepteur d’événements de débogage dans votre gestionnaire de codes ou de balises et si vous activez les <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> jetons de réponse</a> nécessaires dans l’interface utilisateur de Target. </p> </td> 
  </tr> 
 </tbody> 
</table>
