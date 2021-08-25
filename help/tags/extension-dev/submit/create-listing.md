---
title: Création dʼune liste Exchange pour une extension
description: Découvrez comment ajouter votre extension au catalogue public dans Adobe Experience Platform.
source-git-commit: c8705cfa65cb1d3a738610821ece827c2af33615
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 96%

---

# Création dʼune liste Exchange pour une extension

>[!NOTE]
>
>Adobe Experience Platform Launch a été rebaptisé en tant que suite de technologies de collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Adobe Experience Platform comporte un seul catalogue unifié, au sein duquel les utilisateurs peuvent afficher les extensions de balises disponibles à l’installation. Ce catalogue est disponible dans le produit et contient des extensions de trois types :

1. **Extensions publiques** : il s’agit d’extensions terminées conçues pour être utilisées en production par n’importe quel utilisateur.
1. **Extensions privées** : il s’agit d’extensions terminées conçues pour la production, mais qui ont été développées par d’autres utilisateurs au sein de votre société et qui ne sont disponibles que pour les utilisateurs au sein de votre société.
1. **Extensions de développement** : ces extensions sont en développement actif et ne sont disponibles qu’au sein de votre entreprise et uniquement sur une propriété spécifiquement désignée comme propriété de développement.

En dehors des extensions du catalogue de produits, certaines extensions ont également des listes dans [Experience Cloud Exchange Marketplace](https://exchange.adobe.com/experiencecloud.experience-platform-launch.html#product).

Ces listes permettent aux développeurs d’extensions de publier des descriptions de fonctionnalité, de fournir des liens vers la documentation et de commercialiser des extensions auprès des utilisateurs potentiels qui ne connaissent pas votre société ou les fonctionnalités de votre extension. Dans ce marché, votre extension comportera une liste publique qui pourra être consultée sans que l’utilisateur ne soit authentifié sur Platform.  De nombreux développeurs trouvent avantageux de développer une liste autorisée Exchange, mais cette étape n’est pas obligatoire.

Si vous ne disposez pas d’une société pour charger et tester votre package d’extension, vous devez vous inscrire au programme Exchange et commencer une liste.  Cela déclenchera la création d’un compte d’entreprise (cela prend du temps, vous recevrez un e-mail une fois cette opération terminée) que vous pourrez utiliser pour charger et tester votre extension.  Vous ne serez pas tenu de rendre la liste publique.

Si vous disposez déjà d’un compte d’entreprise ou si vous ne prévoyez pas de terminer votre liste, vous pouvez ignorer le reste de cette étape et passer à [charger et tester votre extension](./upload-and-test.md).

## Créer une liste

>[!NOTE]
>
>Le processus suivant détaille la création d’une liste d’applications dans le programme Adobe Exchange. Il s’agit du terme utilisé pour les différentes intégrations et extensions dans Adobe Experience Platform.

![Emplacement du lien App Manager d’Experience Cloud](../images/getting-started/app-mgr-link.png)

1. Connectez-vous au [site Exchange Partner](https://partners.adobe.com/exchangeprogram/experiencecloud). Une fois connecté, cliquez sur le lien **App Manager** en regard de votre nom.
1. Sélectionnez l’onglet **Créer une application**. Cliquez ensuite sur **Créer une application** pour obtenir une solution personnalisée ou sélectionnez un modèle applicable.
1. Fournissez les informations relatives à votre liste. Pour plus d’informations sur App Manager, consultez l’[article](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024197931) complet. Les informations de la liste doivent être très claires quant à la fonction et l’utilité de l’extension. La liste fonctionne comme un espace marketing pour votre application. Promouvez votre extension ici à l’aide de descriptions claires, de liens vers des pages de destination de votre site ou vers des documents d’aide, d’adresses électroniques de support, etc. Bien que l’espace soit limité dans les vues d’extension, la liste Exchange vous permet de promouvoir votre extension ainsi que votre société. Voici quelques suggestions pour améliorer la promotion de l’extension :
   - **Icône d’application** : Assurez-vous que l’icône de la liste Exchange présente les dimensions appropriées, 512 x 512 pour png ou proportions 1:1 pour jpg.

      >[!NOTE]
      >
      >Il s’agit d’un format de fichier différent de celui utilisé dans votre code d’extension. L’extension elle-même contiendra un fichier svg en tant qu’[icône](../manifest.md).

   - **Image en vedette** : attirez l’attention à l’aide d’une image autonome permettant de présenter votre marque et de mettre en avant votre application.L’image en vedette est celle qui s’affiche lorsqu’une personne partage un lien vers votre liste Exchange ou publie des articles à ce sujet sur les médias sociaux. Par conséquent, elle doit parfaitement représenter votre marque.
   - **Logo de l’éditeur de l’appli** : il s’agit du logo de votre entreprise. Vérifiez que l’icône a les dimensions appropriées, soit 1 280 x 720 ou 2 560 x 1 440 (16:9) au format png ou jpg.
   - **Instructions de configuration** : indiquez à vos clients comment configurer votre extension Adobe Experience Platform. Assurez-vous qu’ils comprennent tous les paramètres requis et les étapes suivantes lorsque votre [vue de configuration](../configuration.md) apparaît immédiatement après l’installation de votre extension dans une propriété. 
   - **Balises** : sur la première page de la modification de votre liste, veillez à inclure le mot « Launch » dans le champ « Balises personnalisées ». Votre liste apparaîtra alors dans les recherches de balises sur Exchange Marketplace :
      ![](../images/getting-started/custom-tags.jpg)
   - **Sandboxes** : votre accès aux solutions Adobe se fait via un compte sandbox qui vous donne accès à une version fonctionnelle d’Adobe Experience Platform. Ces comptes sandbox sont demandés lorsque vous créez votre liste d’applications. Dans la section **Connexions**, sélectionnez les connexions spécifiques qui s’appliquent à l’application que vous avez créée (votre extension de balise). Lorsque vous appuyez sur **Enregistrer**, la demande de sandbox est générée si nécessaire.
1. Envoyez votre liste. L’équipe Adobe Exchange examinera votre application et fournira des commentaires si des mises à jour sont requises. Si vous cochez la case **publier immédiatement** lors de l’envoi de votre liste, elle sera publiée immédiatement après approbation. Si vous souhaitez publier votre application ultérieurement, ne cochez pas cette case. Une fois votre liste d’extensions approuvée, un bouton bleu **Publier** s’affiche en regard de cette dernière sur votre page de liste d’applications (extensions).

### Créer une liste efficace

Veuillez consulter nos [Directives de soumission d’application](https://partners.adobe.com/exchangeprogram/experiencecloud/build/ec-exchange.html) pour obtenir des informations sur la façon de créer la liste la plus attrayante.

#### Après avoir soumis votre liste Exchange

Une fois la liste soumise, l’équipe Adobe Exchange examine la demande et l’approuve, ou répond avec des commentaires sur les modifications à effectuer. Ce processus est décrit en détail dans les directives de soumission d’application.

Si vous ne disposez pas d’une connexion au site Exchange, veillez à ce que votre adresse électronique soit enregistrée pour le programme Exchange en suivant les instructions du [Guide d’inscription au programme](https://partners.adobe.com/content/mcp/us/en/home/reg-guide.html). Chaque utilisateur doit associer son adresse électronique au compte partenaire de sa société. Les questions relatives à ce processus peuvent être envoyées par e-mail à <ExchangeHelpEC@adobe.com>.

#### Mettre à jour votre liste Exchange après votre approbation initiale

Lorsque vous mettez à jour votre extension ou que vous devez simplement mettre à jour votre liste Exchange, connectez-vous au portail partenaire [Partner Portal](https://partners.adobe.com/exchangeprogram/experiencecloud), puis cliquez sur le bouton App Manager en regard de votre nom. Sélectionnez ensuite votre application et suivez le flux au-dessus qui a été initialement utilisé pour créer la liste. Une fois les modifications soumises, l’équipe Adobe Exchange les examinera et les approuvera ou y répondra avec des commentaires sur les nouvelles modifications à effectuer.

## Lier votre package d’extension à votre liste

Une fois votre liste approuvée et publiquement disponible, nous vous recommandons de fournir un lien vers la liste publique dans le champ `exchange_url` du fichier `extension.json` de votre package d’extension.  Cela créera un lien &quot;Plus d’informations&quot; dans le catalogue de l’extension de balise afin que les utilisateurs du produit puissent trouver votre liste et ses informations supplémentaires.
