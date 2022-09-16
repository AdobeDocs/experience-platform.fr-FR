---
title: Création dʼune liste Exchange pour une extension
description: Découvrez comment ajouter votre extension au catalogue public dans Adobe Experience Platform.
exl-id: 0395fc99-5e2b-46d6-a067-f8f167733e02
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 100%

---

# Création dʼune liste Exchange pour une extension

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Adobe Experience Platform comporte un catalogue unique et unifié dans lequel les utilisateurs peuvent afficher les extensions de balises disponibles pour lʼinstallation. Ce catalogue est disponible dans le produit et contient des extensions de trois types :

1. **Extensions publiques** : il s’agit d’extensions terminées conçues pour être utilisées en production par n’importe quel utilisateur.
1. **Extensions privées** : il s’agit d’extensions terminées conçues pour la production, mais qui ont été développées par d’autres utilisateurs au sein de votre société et qui ne sont disponibles que pour les utilisateurs au sein de votre société.
1. **Extensions de développement** : ces extensions sont en développement actif et ne sont disponibles qu’au sein de votre entreprise et uniquement sur une propriété spécifiquement désignée comme propriété de développement.

En dehors des extensions du catalogue de produits, certaines extensions ont également des listes dans [Experience Cloud Exchange Marketplace](https://exchange.adobe.com/experiencecloud.experience-platform-launch.html#product).

Ces listes permettent aux développeurs d’extensions de publier des descriptions de fonctionnalité, de fournir des liens vers la documentation et de commercialiser des extensions auprès des utilisateurs potentiels qui ne connaissent pas votre société ou les fonctionnalités de votre extension. Dans ce marché, votre extension comportera une liste publique qui pourra être consultée sans que l’utilisateur ne soit authentifié sur Platform.  De nombreux développeurs trouvent avantageux de développer une liste autorisée Exchange, mais cette étape n’est pas obligatoire.

Si vous ne disposez pas d’une société pour charger et tester votre package d’extension, vous devez vous inscrire au programme Exchange et commencer une liste.  Cela déclenchera la création d’un compte d’entreprise (cela prend du temps, vous recevrez un e-mail une fois cette opération terminée) que vous pourrez utiliser pour charger et tester votre extension.  Vous ne serez pas tenu de rendre la liste publique.

Si vous disposez déjà d’un compte d’entreprise ou si vous ne prévoyez pas de terminer votre liste, vous pouvez ignorer le reste de cette étape et passer à [charger et tester votre extension](./upload-and-test.md).

## Créer une liste

>[!NOTE]
>
>Les étapes suivantes détaillent le processus de création dʼune application dans le programme Adobe Exchange. Il sʼagit du terme utilisé pour les différentes intégrations et extensions dans Adobe Experience Platform.

![Emplacement du lien App Manager d’Experience Cloud](../images/getting-started/app-mgr-link.png)

1. Connectez-vous au [site Exchange Partner](https://partners.adobe.com/exchangeprogram/experiencecloud). Une fois connecté, cliquez sur le lien **App Manager** en regard de votre nom.
1. Sélectionnez lʼonglet **Créer une application**, puis sélectionnez **Créer une application** pour une solution personnalisée ou sélectionnez un modèle approprié.
1. Fournissez les informations relatives à votre liste. Pour plus d’informations sur App Manager, consultez l’[article](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024197931) complet. La description de lʼextension doit renseigner précisément sur les fonctionnalités et lʼutilité de celle-ci. La description constitue votre espace marketing pour lʼapplication. Faites connaître votre extension ici au moyen de descriptions claires, de liens vers des pages de destination de votre site, des documents dʼaide ou des adresses e-mail de support, etc. Bien que lʼespace réservé pour lʼextension soit limité, votre liste Exchange vous offre lʼopportunité de promouvoir à la fois votre extension et votre société. Voici quelques suggestions pour mettre en valeur votre extension :
   - **Icône d’application** : Assurez-vous que l’icône de la liste Exchange présente les dimensions appropriées, 512 x 512 pour png ou proportions 1:1 pour jpg.

      >[!NOTE]
      >
      >Il sʼagit dʼun format de fichier différent de celui que vous utilisez dans votre code dʼextension. L’extension elle-même contiendra un fichier svg en tant qu’[icône](../manifest.md).

   - **Image en vedette** : captez lʼattention en utilisant une image qui, à elle seule, présentera votre marque et mettra en évidence votre application. L’image en vedette est celle qui s’affiche lorsqu’une personne partage un lien vers votre liste Exchange ou publie des articles à ce sujet sur les médias sociaux. Elle doit donc représenter fidèlement votre marque.
   - **Logo de l’éditeur de l’appli** : il s’agit du logo de votre entreprise. Vérifiez que l’icône a les dimensions appropriées, soit 1 280 x 720 ou 2 560 x 1 440 (16:9) au format png ou jpg.
   - **Instructions de configuration** : informez les clients sur la manière de configurer votre extension Adobe Experience Platform. Assurez-vous qu’ils comprennent tous les paramètres requis et les étapes suivantes lorsque votre [vue de configuration](../configuration.md) apparaît immédiatement après l’installation de votre extension dans une propriété. 
   - **Balises** : sur la première page de la modification de votre liste, veillez à inclure le mot « Launch » dans le champ « Balises personnalisées ». Votre extension apparaîtra alors dans les résultats de recherche de balises dans le marketplace Exchange :
      ![](../images/getting-started/custom-tags.jpg)
   - **Environnements de test** : lʼaccès aux solutions Adobe sʼeffectue via un compte Sandbox, au moyen duquel vous avez accès à une version fonctionnelle dʼAdobe Experience Platform. Ces comptes sandbox sont demandés lorsque vous créez votre liste d’applications. Dans la section **Connexions**, sélectionnez les connexions spécifiques relatives à l’application que vous avez créée (votre extension Balise) et lorsque vous appuyez sur **Enregistrer**, la demande d’environnement de test est générée si nécessaire.
1. Soumettez votre liste. L’équipe Adobe Exchange examinera votre application et fournira des commentaires si des mises à jour sont requises. Si vous cochez la case **publier immédiatement** lorsque vous soumettez votre liste, elle sera publiée immédiatement après approbation. Si vous souhaitez publier votre application ultérieurement, ne cochez pas cette case et lorsque votre liste d’extensions sera approuvée, un bouton bleu **Publier** s’affichera en regard de cette dernière sur votre page de liste d’applications (extension).

### Créer une liste efficace

Veuillez consulter nos [Directives de soumission d’application](https://partners.adobe.com/exchangeprogram/experiencecloud/build/ec-exchange.html) pour obtenir des informations sur la façon de créer la liste la plus attrayante.

#### Après avoir soumis votre liste Exchange

Une fois la liste soumise, l’équipe Adobe Exchange examine la demande et l’approuve, ou répond avec des commentaires sur les modifications à effectuer. Ce processus est décrit en détail dans les directives de soumission d’application.

Si vous ne disposez pas d’une connexion au site Exchange, veillez à ce que votre adresse e-mail soit enregistrée pour le programme Exchange en suivant les instructions du [Guide d’inscription au programme](https://partners.adobe.com/content/mcp/us/en/home/reg-guide.html). Chaque utilisateur doit associer son adresse e-mail au compte partenaire de sa société. Les questions relatives à ce processus peuvent être envoyées par e-mail à <ExchangeHelpEC@adobe.com>.

#### Mettre à jour votre liste Exchange après votre approbation initiale

Lorsque vous mettez à jour votre extension ou que vous devez simplement mettre à jour votre liste Exchange, connectez-vous au portail partenaire [Partner Portal](https://partners.adobe.com/exchangeprogram/experiencecloud), puis cliquez sur le bouton App Manager en regard de votre nom. Sélectionnez ensuite votre application et suivez le flux au-dessus qui a été initialement utilisé pour créer la liste. Une fois les modifications soumises, l’équipe Adobe Exchange les examinera et les approuvera ou y répondra avec des commentaires sur les nouvelles modifications à effectuer.

## Lier votre package d’extension à votre liste

Une fois votre liste approuvée et publiquement disponible, nous vous recommandons de fournir un lien vers la liste publique dans le champ `exchange_url` du fichier `extension.json` de votre package d’extension.  Cela crée un lien « Plus d’informations » dans le catalogue d’extensions de balises. Les utilisateurs du produit peuvent ainsi trouver votre liste et ses informations supplémentaires.
