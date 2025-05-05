---
title: Notes de mise à jour de l’extension Core
description: Notes de mise à jour les plus récentes pour l’extension Core dans Adobe Experience Platform.
exl-id: a049b2d5-7a00-435d-bcc7-112658a53a1e
source-git-commit: 1ce579fc1f8548d1eb5c01d63e9fa4e8b32e2a4f
workflow-type: ht
source-wordcount: '1651'
ht-degree: 100%

---

# Notes de mise à jour de l’extension Core

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

## 23 octobre 2024

v3.4.2

* Correction de l’erreur de validation du schéma pour l’événement Formulaire -> Modifier, lorsque « et ayant certaines valeurs de propriété... » est actif.

## 29 mars 2023

v3.4.1

* Ajoute de nouveaux événements délégués natifs web :
   * Keydown
   * KeyUp
* Ajoute la possibilité de tester par rapport à de nombreuses valeurs (options « Ajouter une autre ») par rapport aux délégués suivants :
   * Événements
      * Changement
   * Conditions
      * Cookie
      * Page de destination
      * Paramètre de chaîne de requête
      * Source de trafic
      * Variable
* Modifie le délégué events/EntersViewport pour utiliser l’[API Intersection Observer](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API) au lieu de la détection manuelle des éléments qui entrent dans la fenêtre d’affichage.
* Supprime le code qui migrait les cookies DTM vers LocalStorage.
* Inscrit un avertissement dans la console lorsque les API LocalStorage et SessionStorage ne sont pas disponibles.

## 4 janvier 2022

v3.3.0

* Modifie lʼ[action Déclencher l’appel direct](./overview.md#direct-call-action) afin que vous puissiez fournir des informations sur l’événement personnalisé à envoyer aux règles d’appel direct.

## 8 octobre 2021

v3.2.2

* Correction du schéma JSON de l’élément de données de valeur conditionnelle pour tous les opérateurs disponibles.
* Correction du problème https://github.com/adobe/reactor-extension-core/issues/64.

## 23 septembre 2021

v3.2.1

* Correction d’une erreur qui entraînait un dysfonctionnement de l’initialisation d’affichage d’élément de données de valeur conditionnelle lorsque les valeurs de champs étaient égales à 0.

## 23 septembre 2021

v3.2.0

Les modifications suivantes ont été introduites dans l’élément de données de valeur conditionnelle :

* Ajout d’une case à cocher pour les valeurs conditionnelles et de secours, qui permet à l’utilisateur de choisir s’il souhaite que la valeur renvoyée soit indéfinie.
* Les valeurs numériques sont exposées comme des nombres dans l’objet Paramètres.
* La valeur conditionnelle n’est plus nécessaire pour que le comportement soit similaire à celui de la valeur de secours.

## 17 septembre 2021

v3.1.1

* Correction d’une erreur JS qui empêchait le chargement de l’affichage des conditions de période.

## 16 septembre 2021

v3.1.0

De nouveaux éléments de données ont été ajoutés :

* Objet fusionné : sélectionnez plusieurs éléments de données qui fourniront chacun un objet. Ces objets seront profondément (récursivement) fusionnés pour produire un nouvel objet.
* Valeur conditionnelle : renvoyez l’une des deux valeurs (conditionalValue ou fallbackValue) en fonction du résultat de la comparaison.
* Environnement d’exécution : renvoyez l’une des variables d’environnement Launch suivantes (évaluation d’environnement, date de création de la bibliothèque, nom de la propriété, ID de la propriété, nom de la règle, ID de la règle, type d’événement, payload des détails de l’événement, identificateur d’appel direct).
* Outils JavaScript : wrapper pour les opérations JavaScript les plus courantes, par exemple la manipulation de chaînes de base (remplacer, sous-chaîne, correspondance regex, premier et dernier index, fractionner, trancher), les opérations de tableaux de base (trancher, joindre, mise en valeur, déplacer) et les opérations universelles de base (trancher, longueur).
* Attributs d’appareil : renvoyez les attributs d’appareil comme la taille de la fenêtre ou de l’écran.

## 11 août 2021

v3.0.0

* PDCL-6153 : ajoute la prise en charge pour extraire de manière fiable lʼURL complète pour les actions de code personnalisé en mémoire cache.

La version 3.0.0 de lʼextension Core est associée à des modifications dans la [version 27.2.0 de lʼobjet dʼexécution Web Turbine](https://github.com/adobe/reactor-turbine/releases/tag/v27.2.0), ce qui permet aux utilisateurs de charger leur bibliothèque parmi de nombreuses régions dʼhébergement gérées par Adobe si la société de lʼutilisateur prend en charge le réseau CDN Premium.

Cette mise à niveau est facultative et rétrocompatible pour les utilisateurs qui ne possèdent pas le réseau CDN Premium, cependant, elle est obligatoire pour les clients disposant du réseau CDN Premium au sein de leur société.

## 20 mai 2021

v2.0.7

* Correction d’un problème en raison duquel les interactions de la souris sur les entrées de texte ne fonctionnaient plus correctement.
* Utilisation déconseillée des conditions du navigateur et du système d’exploitation.

## 4 mai 2021

v2.0.6

* Mise à jour mineure afin de résoudre le problème des icônes qui se déforment lorsque la taille de l’écran change.

## 11 mars 2021

v2.0.5

* Mise à jour du code dans lʼévaluation de lʼexécution pour les événements et actions avec option de délai, qui prend désormais en charge les valeurs des éléments de données ajoutés dans la version 2.0.4, afin de convertir correctement les chaînes en nombres.

## 9 mars 2021

v2.0.4

* Ajout de la prise en charge des éléments de données dans plusieurs champs - La prise en charge des éléments de données a été ajoutée aux événements suivants : « Temps sur la page », « Entrée dans la fenêtre dʼaffichage », « Survol » et « Temps de lecture du média ». En plus des conditions suivantes : « Temps passé sur le site » et « Comparaison de valeur »
* Ajout de la prise en charge du comportement par défaut pour Ctrl/Cmd + Clic et pour le clic central de la souris lors de lʼutilisation du délai de lien
* **Le délai sur les liens pour lʼévénement Clic a été indiqué comme « nʼest plus pris en charge ».** - Vous trouverez plus d’informations sur le [blog de collecte de données](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/explainer-link-delay/ba-p/398403?profile.language=fr) pour Adobe Experience Platform.

## 6 janvier 2021

v1.9.0

* **Nouvelle action « Déclencher un appel direct »** : l’extension Core inclut désormais un nouveau type d’action appelé `Trigger Direct Call`.  Vous pouvez l’utiliser lorsque vous voulez déclencher une règle d’appel direct par le biais d’une action tirée d’une autre règle. Il correspond directement à la méthode `_satellite.track()`. Un grand merci à Jan Exner pour cette contribution.

## 8 décembre 2020

v1.8.4

* Correction d’un bug en raison duquel un utilisateur ne pouvait pas effacer ou annuler la valeur à usage unique CSP.

## 28 juillet 2020

v1.8.3

* Correction d’un bug en raison duquel la valeur à usage unique CSP n’était lue qu’une seule fois au démarrage de l’extension au lieu d’être extraite de nouveau lors de l’appel d’action de code personnalisé.

## 13 juillet 2020

v1.8.2

* Correction d’un bug en raison duquel l’action de code personnalisé renvoyait une erreur pour le code HTML contenant des jetons sans nom de balise (ex. commentaires).

## 10 juillet 2020

v1.8.1

* Correction d’un bug en raison duquel les entités HTML personnalisées à l’intérieur des attributs des balises `script` et `style` n’étaient pas correctement décodées avant d’être écrites sur la page.
* Correction d’un bug en raison duquel une erreur survenait lorsqu’une action de code personnalisé externe n’avait aucun contenu. L’action de code personnalisé externe est l’action chargée à partir d’un fichier différent de celui de la bibliothèque (cela se produit lorsque l’événement qui déclenche la règle n’est pas libraryLoaded ou pageBottom).

## 6 juillet 2020

v1.8.0

* **Promesses dans le Custom Code (code personnalisé)** : Les conditions du Custom Code (code personnalisé) et des actions JavaScript qui ne s’exécutent pas dans la portée globale peuvent désormais renvoyer des promesses.  Vous pouvez les utiliser pour que les conditions et actions suivantes attendent la fin d’un processus asynchrone dans votre Custom Code (code personnalisé) avant de passer à l’élément suivant.
* **Rappels dans les actions Custom Code (code personnalisé) HTML** : Vous pouvez obtenir la même chose dans les actions Custom Code (code personnalisé) HTML à l’aide des rappels `onCustomCodeSuccess()` et `onCustomCodeFailure()`.

Pour plus d’informations, reportez-vous à la [référence Extension Core](./overview.md) dans Conditions > Code personnalisé et Actions > Code personnalisé.

## 7 avril 2020

v1.7.3

* **Augmentation de la longueur du champ texte** - les champs de saisie de texte ont été modifiés pour une disposition flexible afin de mieux s’adapter à la largeur d’écran de l’utilisateur et de donner plus d’espace pour des chaînes de texte plus longues.

## 1er novembre 2019

v1.7.0

* **Accès à la variable `event` dans l’élément de données de code personnalisé** : vous pouvez désormais référencer l’événement depuis un élément de données de Cutom Code (code personnalisé) lorsqu’il est exécuté dans le contexte d’une règle. L’objet contient des informations utiles sur l’événement qui a déclenché la règle. Un grand merci à Stewart Schilling pour cette contribution.

## 7 octobre 2019

v1.6.2

* **Nouveau type d’élément de données « Constante »** : l’extension Core inclut désormais un nouveau type d’élément de données appelé `Constant`.  Vous pouvez l’utiliser lorsque vous avez besoin de stocker une valeur constante qui sera référencée dans différentes conditions, actions ou code personnalisé (Custom code). Un grand merci à Jan Exner pour cette contribution.

## 11 septembre 2019

v1.6.1

* **Prise en charge de la valeur à usage unique de la CSP** : l’extension Core comporte désormais un paramètre de configuration facultatif. Vous pouvez ajouter un élément de données qui fait référence à une valeur à usage unique. Si celle-ci est configurée, tous les scripts intégrés qu’une balise ajoute à la page utilisent la valeur à usage unique que vous avez configurée. Cette modification prend en charge lʼutilisation dʼune politique de sécurité du contenu (CSP) avec une valeur à usage unique afin que les scripts de balises puissent toujours se charger dans un environnement CSP. Pour en savoir plus sur lʼutilisation des balises avec une stratégie de sécurité du contenu, [cliquez ici](../../../ui/client-side/content-security-policy.md).

## 18 juin 2019

v1.5.0

* **Direct Call Logging** : la connexion du navigateur pour les règles d’appels directs fournit désormais des détails supplémentaires lors de la transmission.

## 8 mai 2019

v1.4.3

* **Input Fields** : les champs d’entrée sont désormais plus longs.
* **Événement personnalisé** : le type de Custom event (Événement personnalisé) peut désormais être utilisé avec les événements envoyés de la fenêtre.
* **Correction de bogue** : correction d’un bogue qui survenait lorsque la condition Value Comparison (Comparaison de valeurs) ne contenait pas une valeur 0.
* **Correction de bogue** : mise à jour du champ exchange\_url afin que la liste des extensions de base s’affiche dans Adobe Exchange.

## 8 janvier 2019

v1.4.2

* **Événement Enters Viewport** : auparavant, l’événement Enters Viewport ne se déclenchait qu’une fois par page. Désormais, il est possible de configurer ce comportement pour que l’événement se déclenche chaque fois que l’élément apparaît dans la fenêtre d’affichage.
* **Événement Custom Event** : les événements personnalisés peuvent désormais contenir des données contextuelles qui peuvent être utilisées dans des conditions et des actions.
* **Événement Click** : lorsque vous définissez un retard de lien sur l’événement Click, celui-ci s’applique désormais à tous les descendants de l’ancre de lien et pas seulement à l’ancre de lien elle-même.

## 8 novembre 2018

* **Option Persist Cohort** : l’option de conservation d’une cohorte a été ajoutée à la condition de l’échantillonnage. Cela a pour effet de conserver un utilisateur dans ou hors de la cohorte de l’échantillon d’une session à l’autre. Par exemple, si la case « Conserver la cohorte » est cochée et que la condition renvoie « true » lors de sa première exécution pour une personne donnée, elle renvoie « true » sur toutes les exécutions suivantes de la condition pour la même personne. De même, si la case « Conserver la cohorte » est cochée et que la condition renvoie « false » lors de sa première exécution pour une personne donnée, elle renvoie « false » sur toutes les exécutions suivantes de la condition pour la même personne.
* **Correctif** : correction d’un bug par lequel une règle utilisant un événement Bas de page et une action de code personnalisé sur une page où les balises étaient chargées de manière synchrone, mais installées de manière incorrecte (aucun appel à `_satellite.pageBottom()`), effaçait le contenu du site web.
* **Correction de bug** : correction dʼun problème qui empêchait l’événement Enters Viewport de fonctionner si la bibliothèque de balises était chargée de manière asynchrone et que le chargement était terminé après le déclenchement de lʼévénement DOMContentLoaded du navigateur.

## 24 mai 2018

* **Fonctionnalité** : ajout d’une condition Value Comparison comparant deux valeurs à l’aide de l’un des opérateurs disponibles. Cette fonctionnalité remplace celles de plusieurs conditions antérieures qui étaient bien trop spécifiques.
* **Fonctionnalité** : ajout d’une condition Max Frequency permettant de spécifier le nombre de fois où la condition doit renvoyer la valeur TRUE dans une période ou une occurrence d’événement. Exemples : 5 fois par jour, 2 fois par visite.

## 11 avril 2018

* **Fonctionnalité** : les éléments de données peuvent désormais référencer d’autres éléments de données.

## 20 mars 2018

* **Bug Fix** : les fenêtres Custom code (Code personnalisé) généraient des erreurs `document.write` et ne s’exécutaient pas dans les déploiements asynchrones
* **Bug Fix** : les modules principaux n’étaient pas inclus dans une bibliothèque
* **Bug Fix** : des problèmes se produisaient avec les valeurs minimum et maximum sur l’élément de données Random Number

## 10 janvier 2018

* **Fonctionnalité** : élément de données Random Number
* **Fonctionnalité** : élément de données de Page Info
* **Fonctionnalité** : condition de date
* **Fonctionnalité** : condition de l’échantillonnage
