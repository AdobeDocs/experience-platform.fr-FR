---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un  à l’aide de l’éditeur de  de
topic: tutorials
translation-type: tm+mt
source-git-commit: c07f926a71447e840c692ed15e85c9e02f1106ab

---


# Création d’un  à l’aide de l’éditeur de  de

Le Registre des  de fournit une interface utilisateur et une API RESTful à partir de laquelle vous pouvez et gérer toutes les ressources de la bibliothèque de  de la plateforme d’expérience Adobe. La bibliothèque de  de contient les ressources mises à votre disposition par Adobe, les partenaires de la plate-forme d’expérience et les fournisseurs dont vous utilisez les applications, ainsi que les ressources que vous définissez et enregistrez dans le registre  de.

Ce didacticiel décrit les étapes de création d’un  à l’aide de l’éditeur de  de dans la plateforme d’expérience. Si vous préférez composer un  à l&#39;aide de l&#39;API de Registre, veuillez commencer par lire le guide [du développeur de Registre de l&#39;](../api/getting-started.md) avant d&#39;essayer le didacticiel [Création d&#39;un à l&#39;aide de l&#39;API](create-schema-api.md).

Ce didacticiel comprend également des étapes pour [définir une nouvelle classe](#create-new-class) que vous pourrez ensuite utiliser pour composer un .

## Prise en main

Ce didacticiel nécessite une compréhension pratique des différents aspects d’Adobe Experience Platform impliqués dans l’utilisation de l’éditeur de  de. Avant de commencer ce didacticiel, veuillez consulter la documentation pour connaître les concepts suivants :

* [Modèle de données d’expérience (XDM)](../home.md): Cadre normalisé selon lequel la plateforme organise les données d’expérience client.
* [Principes de base de la composition](../schema/composition.md)de  : Présentation des  XDM et de leurs blocs de création, y compris les classes, les mixins, les types de données et les champs.
* [](../../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.

Ce didacticiel nécessite que vous ayez accès à Experience Platform. Si vous n’avez pas accès à une organisation IMS dans Experience Platform, contactez votre administrateur système avant de poursuivre.

## Parcourir les  de existants dans l’espace de travail  de

L’espace de travail  dans Experience Platform fournit une visualisation de la bibliothèque de , ce qui vous permet degérer et de gérer l’ensemble des disponibles et d’en composer de nouveaux. L’espace de travail inclut également l’éditeur de  de, le canevas sur lequel vous allez composer un  de tout au long de ce didacticiel.

Après vous être connecté à Experience Platform, cliquez sur **** dans le volet de navigation de gauche et vous serez redirigé vers l’espace de travail . Vous verrez un de  de (une représentation de la bibliothèque de de laBande) où vous pourrez vous y connecter, gérer et personnaliser tous les disponibles. Le  inclut le nom, le type, la classe et le comportement (enregistrement ou série chronologique) sur lesquels le  est basé, ainsi que la date et l’heure de la dernière modification de l’ de la page.

Cliquez sur l’icône de filtre en regard de la barre de recherche pour utiliser les fonctionnalités de filtrage pour toutes les ressources du registre, y compris les classes, les mixins et les types de données.

![la bibliothèque](../images/tutorials/create-schema/schemas_filter.png)

## Création et attribution d’un nom à un 

Pour commencer à composer un  de, cliquez sur **Créer un** dans le coin supérieur droit de l’espace de travailde la  de travail.

![Bouton Créer un](../images/tutorials/create-schema/create_schema_button.png)

L’éditeur *de* s’affiche. C&#39;est la toile sur laquelle vous allez composer votre . Lorsque vous arrivez dans l’éditeur, un &quot; sans titre&quot; dans la section *Structure* du canevas est automatiquement créé pour que vous puissiez commencer à le personnaliser.

![Éditeur de](../images/tutorials/create-schema/schema_editor.png)

Sur le côté droit de l’éditeur, vous trouverez les propriétés ****dans lesquelles vous pouvez attribuer un nom au  de (à l’aide du champ Nom** d’affichage). Une fois le nom saisi, le canevas est mis à jour pour refléter le nouveau nom du .

![Canevas](../images/tutorials/create-schema/name_schema.png)

Plusieurs considérations importantes doivent être prises en compte lors du choix du nom d’un :

* Les noms des  doivent être courts et descriptifs afin que le  du puisse être trouvé plus tard dans la bibliothèque.
* Les noms de  doivent être uniques, ce qui signifie qu’ils doivent également être suffisamment précis pour ne pas être réutilisés à l’avenir. Si, par exemple, votre organisation dispose d’un de fidélité distinct pour différentes marques, il serait judicieux de nommer vos  &quot;Membres de la marque A&quot; afin de faciliter la distinction avec d’autrestermes de fidélité que vous pourrez définir plus tard.
* Vous pouvez éventuellement fournir des informations supplémentaires sur le  du à l’aide du champ **Description** .

Ce didacticiel compose un pour ingérer des données relatives aux membres d’un de fidélité. Par conséquent, leterme &quot;Membres de fidélité&quot; est nommé &quot;Membres de loyauté&quot;.

## Affecter une classe

Sur le côté gauche de l’éditeur se trouve la section *Composition* . Il contient actuellement deux sous-sections :  ** et *classe*.

Maintenant que le  a un nom, il est temps d&#39;attribuer la classe que le  implémentera. Cliquez sur **Attribuer** en regard de *la classe*.

![](../images/tutorials/create-schema/assign_class_button.png)

La boîte de dialogue *Attribuer une classe* s’affiche. Cette fenêtre affiche un  de toutes les classes disponibles, y compris toutes les classes définies par votre organisation (le propriétaire étant &quot;Client&quot;) ainsi que les classes standard définies par Adobe.

Cliquez sur le nom de la classe pour afficher la description de la classe. Vous pouvez également choisir de **Structure** de classe pour afficher les champs et les métadonnées associés à la classe.

Ce didacticiel utilise la classe XDM Individuel . Cliquez sur le bouton radio en regard de la classe pour la sélectionner, puis cliquez sur **Attribuer une classe**.

![Boîte de dialogue Attribuer une classe](../images/tutorials/create-schema/assign_class.png)

La trame réapparaît. La section *Classe* contient désormais la classe que vous avez sélectionnée ( XDM Individuel) et les champs fournis par la classe XDM Individuel  sont désormais visibles dans la section *Structure* .

![XDM Classe de spécifique attribuée](../images/tutorials/create-schema/class_assigned_structure.png)

Les champs apparaissent au format &quot;fieldName&quot;| Type de données&quot;. Les étapes de définition des champs  de l’interface utilisateur sont décrites plus loin dans ce didacticiel.

>[!NOTE] Vous pouvez [modifier la classe d’un](#change-class) à tout moment pendant le processus de composition initial avant que le n’ait été enregistré, mais cela doit être fait avec une extrême prudence. Les mixins ne sont compatibles qu’avec certaines classes. Par conséquent, la modification de la classe réinitialise le canevas et les champs que vous avez ajoutés.

## Ajouter un mixin

Maintenant qu’une classe a été affectée, la section *Composition* contient une troisième sous-section : *Mixins*.

Vous pouvez maintenant commencer à ajouter des champs à votre  en ajoutant des mixins. Un mixin est un groupe d’un ou de plusieurs champs qui décrivent un concept particulier. Ce didacticiel utilise des mixins pour décrire les membres du de fidélité et capturer des informations clés telles que le nom, l’anniversaire, le numéro de téléphone, l’adresse, etc.

Pour ajouter un mixin, cliquez sur **Ajouter** dans la sous-section *Mixins* .

![](../images/tutorials/create-schema/add_mixin_button.png)

La boîte de dialogue *Ajouter Mixin* s’affiche. Les mixins ne sont destinés qu’à des classes spécifiques. Par conséquent, l’ des mixins n’affiche que celles compatibles avec la classe que vous avez sélectionnée (dans ce cas, la classe de XDM Individuel ).

La sélection du bouton radio en regard d’un mixin vous donne la possibilité de **Structure** mixte. Sélectionnez le mixin &quot;Détails de la personne &quot;, puis cliquez sur **Ajouter Mixin**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

Le canevas  réapparaît. La section *Mixins* désormais le mixin &quot;Détails de la personne de la&quot; et la section *Structure* inclut les champs fournis par le mixin.

![](../images/tutorials/create-schema/person_details_structure.png)

Ce mixin fournit plusieurs champs sous le nom de niveau supérieur &quot;personne&quot; avec le type de données &quot;Personne&quot;. Ce groupe de champs décrit des informations sur un individu, y compris son nom, sa date de naissance et son sexe.

>[!NOTE] N’oubliez pas que les champs peuvent utiliser des types scalaires (chaîne, entier, tableau ou date, par exemple) comme type de données, ainsi que tout type de données (un groupe de champs représentant un concept commun) dans le Registre des  de.

Notez que le champ &quot;nom&quot; possède un type de données &quot;Nom de la personne&quot;, ce qui signifie qu’il décrit également un concept commun et qu’il contient des sous-champs liés au nom, tels que le prénom, le nom et le nom complet.

Cliquez sur les différents champs du canevas pour afficher les champs supplémentaires qu’ils contribuent à la structure du .

## Ajouter un autre mixin

Vous pouvez maintenant répéter les mêmes étapes pour ajouter un autre mixin. Lorsque vous  la boîte de dialogue *Ajouter Mixin* cette fois-ci, notez que le mixin &quot;Détails de la personne de l’&quot; a été grisé et que le bouton radio situé à côté ne peut pas être sélectionné. Cela vous évite de dupliquer accidentellement les mixins que vous avez déjà inclus dans le  actuel.

Vous pouvez maintenant ajouter le mixin &quot;Détails personnels du&quot; à partir de la boîte de dialogue *Ajouter Mixin* .

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

Une fois ajouté, le canevas réapparaît. Les &quot;Détails personnels &quot; sont maintenant répertoriés sous *Mélanges* dans la section *Composition* , et les champs pour l’adresse de domicile, le téléphone mobile, etc. ont été ajoutés sous *Structure*.

Tout comme le champ &quot;nom&quot;, les champs que vous venez d’ajouter représentent des concepts à plusieurs champs. Par exemple, &quot;homeAddress&quot; a un type de données &quot;Address&quot; et &quot;mobilePhone&quot; a un type de données &quot;Phone Number&quot;. Vous pouvez cliquer sur chacun de ces champs pour les développer et afficher les champs supplémentaires inclus dans le type de données.

![](../images/tutorials/create-schema/personal_details_structure.png)

## Définir un nouveau mixage

Le &quot;Membres de la fidélité&quot; est destiné à capturer les données relatives aux membres d’un de fidélité. Il nécessite donc des champs spécifiques liés à la fidélité. Il n’existe pas de mixins standard qui contiennent les champs nécessaires. Vous devrez donc définir un nouveau mixin.

Cette fois-ci, lorsque vous ouvrez la boîte de dialogue *Ajouter Mixin* , sélectionnez **Créer un nouveau mélange**. Vous serez alors invité à fournir un nom **d’** affichage et une **description** pour votre mixin.

![](../images/tutorials/create-schema/mixin_create_new.png)

Comme pour les noms de classe, le nom du mixin doit être court et simple, décrivant ce que le mixin apportera au . Ces noms sont également uniques, vous ne pourrez donc pas réutiliser le nom et devez donc vous assurer qu&#39;il est suffisamment spécifique.

Pour ce didacticiel, nommez le nouveau mixin &quot;Détails de fidélité&quot;.

Cliquez sur **Ajouter Mixin** pour revenir à l’éditeur de  de. Les &quot;Détails de fidélité&quot; doivent maintenant apparaître sous *Mélanges* sur le côté gauche de la trame, mais aucun champ n’y est encore associé et, par conséquent, aucun nouveau champ n’apparaît sous *Structure*.

## Ajouter des champs au mixin

Maintenant que vous avez créé le mixin &quot;Détails de fidélité&quot;, il est temps de définir les champs que le mixin contribuera au .

Pour commencer, cliquez sur le nom du mixin dans la section *Mixins* . Une fois que vous avez effectué cette opération, *les propriétés* mixtes apparaissent sur le côté droit de l’éditeur et un bouton Champ **** Ajouter apparaît en regard du nom du sous *Structure*.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Cliquez sur **Ajouter champ** en regard de &quot;Membres fidèles&quot; pour créer un nouveau noeud dans la structure. Ce noeud (appelé &quot;_locataireId&quot; dans cet exemple) représente l’ID de client de votre organisation IMS, précédé d’un trait de soulignement. La présence de l’ID de client indique que les champs que vous ajoutez sont contenus dans le  de votre organisation.

En d&#39;autres termes, les champs que vous ajoutez sont propres à votre organisation et seront enregistrés dans le Registre des  dans une zone spécifique accessible uniquement à votre organisation IMS. Les champs que vous définissez doivent toujours être ajoutés à votre   pour éviter les collisions avec des noms provenant d’autres classes, mixins, types de données et champs standard.

À l’intérieur de ce noeud, l’espace de noms est un &quot;nouveau champ&quot;. C&#39;est le début du mixin &quot;Détails de fidélité&quot;.

![](../images/tutorials/create-schema/new_field_loyalty.png)

En utilisant les propriétés *de* champ sur le côté droit de l’éditeur, en créant un champ de fidélité avec le type &quot;Objet&quot; qui sera utilisé pour conserver vos champs liés à la fidélité. Lorsque vous avez terminé, cliquez sur **Appliquer**.

![](../images/tutorials/create-schema/loyalty_object.png)

Les modifications sont appliquées et le nouvel objet &quot;loyalty&quot; s’affiche. Cliquez sur **Ajouter champ** en regard de l’objet pour ajouter d’autres champs liés à la fidélité. Un &quot;Nouveau champ&quot; apparaît et la section Propriétés *du* champ est visible sur le côté droit du canevas.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Chaque champ nécessite les informations suivantes :

* **Nom du champ :** Le nom du champ, écrit dans le cas du chameau. Exemple : loyaltyLevel
* **Nom d’affichage :** Nom du champ, écrit dans la casse du titre. Exemple : Niveau de fidélité
* **Type :** Type de données du champ. Cela inclut les types scalaires de base et tous les types de données définis dans le Registre des  de. Exemples : chaîne, entier, booléen, Personne, Adresse, Numéro de téléphone, etc.
* **Description :** Une description facultative du champ doit être incluse, écrite en cas de condamnation. (200 caractères max.)

Le premier champ de l’objet Loyalty sera une chaîne appelée &quot;loyaltyId&quot;. Lorsque vous définissez le type du nouveau champ sur &quot;Chaîne&quot;, la fenêtre Propriétés *du* champ est renseignée avec plusieurs options permettant d’appliquer des contraintes, notamment la valeur **par** défaut, le **format** et la longueur **maximale.**

![](../images/tutorials/create-schema/string_constraints.png)

Différentes options de contrainte sont disponibles selon le type de données sélectionné. Puisque &quot;loyaltyId&quot; sera une adresse électronique, sélectionnez &quot;email&quot; dans le menu déroulant **Format** . Sélectionnez **Appliquer** pour appliquer vos modifications.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Ajouter d’autres champs à mixer

Maintenant que vous avez ajouté le champ &quot;loyaltyId&quot;, vous pouvez ajouter des champs supplémentaires pour capturer des informations liées à la fidélité, telles que :

* Points (entiers)
* Membre depuis (date)

Chaque champ est ajouté en cliquant sur **Ajouter champ** sur l’objet de fidélité et en renseignant les informations requises.

Une fois terminé, l’objet Fidélité contient des champs pour : Identifiant de fidélité, Points et Membre depuis.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Ajouter champ &quot;enum&quot; à mixer

Lors de la définition de champs dans l’éditeur de  de, vous pouvez appliquer d’autres options aux types de champs de base afin de limiter davantage les données que le champ peut contenir.

Par exemple, un champ &quot;Niveau de fidélité&quot;, où la valeur ne peut être que l’une des quatre options possibles. Pour ajouter ce champ au , cliquez sur **Ajouter Champ** en regard de l’objet &quot;loyauté&quot; et renseignez les champs obligatoires sous Propriétés *du* champ.

Pour **Type**, sélectionnez &quot;Chaîne&quot; et d’autres cases à cocher s’affichent pour **Tableau**, **Enum** et **Identité.**

Cochez la case **Enum** pour ouvrir la section Valeurs ** Enum ci-dessous. Ici, vous pouvez saisir la **valeur** (dans camelCase) et le **libellé** (un nom facultatif et convivial dans le cas du titre) pour chaque niveau de fidélité acceptable.

Une fois toutes les propriétés de champ terminées, cliquez sur **Appliquer** et le champ &quot;loyaltyLevel&quot; est ajouté à l’objet &quot;loyalty&quot;.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

Informations supplémentaires sur les contraintes supplémentaires disponibles :

* **Obligatoire :** Indique que le champ est requis pour l’assimilation des données. Toute donnée téléchargée dans un jeu de données basé sur ce qui ne contient pas ce champ échoue lors de l’assimilation.
* **Tableau :** Indique que le champ contient un tableau de valeurs, chacune avec le type de données spécifié. Par exemple, la sélection d’un type de données &quot;String&quot; et la coche de la case &quot;Array&quot; signifient que le champ contiendra un tableau de chaînes.
* **Enum :** Indique que ce champ doit contenir l’une des valeurs d’un énuméré de valeurs possibles.
* **Identité :** Indique que ce champ est un champ d’identité. Vous trouverez plus d’informations sur les champs d’identité [plus loin dans ce didacticiel](#identity-field).

## Conversion d’un objet à champs multiples en un type de données

Après avoir ajouté plusieurs champs spécifiques à la fidélité, l’objet &quot;loyalty&quot; contient désormais une structure de données commune qui peut s’avérer utile dans d’autres  de.

Lorsque vous pensez qu’une structure à plusieurs champs peut être réutilisable et que vous souhaitez avoir la flexibilité d’utiliser la même structure de données ailleurs, l’éditeur de  de permet de convertir cette structure en type de données.

Les types de données permettent l’utilisation cohérente de structures à champs multiples et offrent plus de flexibilité qu’un mixin, car ils peuvent être utilisés n’importe où dans un . Pour ce faire, définissez le **type** d’un champ d’un mixin sur celui de tout type de données défini dans le registre.

Pour convertir l’objet &quot;loyalty&quot; en type de données, cliquez sur le champ &quot;loyalty&quot; sous *Structure* et sélectionnez **Convertir en nouveau type** de données à droite de l’éditeur sous Propriétés *du* champ. Une petite fenêtre contextuelle verte s’affiche, confirmant &quot;Objet converti en type de données&quot;.

Maintenant, lorsque vous regardez sous *Structure*, vous pouvez voir que le champ &quot;fidélité&quot; a un type de données &quot;fidélité&quot; et que les champs ont de petites icônes de verrouillage à côté indiquant qu’ils ne sont plus des champs individuels, mais qu’ils font partie d’une structure à plusieurs champs.

Dans un futur , vous pouvez désormais affecter à un champ le **type** de fidélité et inclure automatiquement les champs Niveau de fidélité, Points, Membre depuis et Identifiant de fidélité.

![](../images/tutorials/create-schema/loyalty_data_type.png)

## Définir un champ de  de comme champ d’identité {#identity-field}

Les  de sont utilisées pour l’assimilation de données dans la plateforme d’expérience. Ces données sont en fin de compte utilisées pour identifier les individus et rassembler les informations provenant de sources multiples. Pour faciliter ce processus, les champs clés peuvent être marqués comme des champs &quot;Identité&quot;.

Experience Platform facilite la désignation d’un champ d’identité grâce à l’utilisation d’une case à cocher **Identité** dans l’éditeur de  de.

Par exemple, il peut y avoir des milliers de membres du de fidélité appartenant au même &quot;niveau&quot;, mais chaque membre du de fidélité a un &quot;loyaltyId&quot; unique (qui dans ce cas est l’adresse électronique du membre individuel). Le fait que &quot;loyaltyId&quot; soit un identifiant unique pour chaque membre en fait un bon candidat pour un champ d’identité, contrairement à &quot;level&quot;.

Dans la section *Structure* de l’éditeur, cliquez sur le champ &quot;loyaltyId&quot; que vous avez créé et la case à cocher **Identity** apparaît sous Propriétés *du* champ. Cochez la case et vous aurez la possibilité de définir cette option comme identité **** principale. Cochez cette case aussi.

Ensuite, vous devez fournir un espace de noms **d’identité**. Il existe plusieurs   prédéfinis, mais puisque &quot;loyaltyId&quot; est l’adresse électronique du membre, sélectionnez &quot;Email&quot; dans la liste déroulante des. Vous pouvez maintenant cliquer sur **Appliquer** pour confirmer les mises à jour du champ &quot;loyaltyId&quot;.

Désormais, toutes les données saisies dans le champ &quot;loyaltyId&quot; seront utilisées pour identifier cette personne et assembler un seul  de ce client.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE] Une fois qu’un champ de  a été défini comme identité principale, vous recevrez un message d’erreur si vous tentez par la suite de définir un autre champ du comme champ principal. Chaque  ne peut contenir qu&#39;un seul champ d&#39;identité principal.

Pour en savoir plus sur l’utilisation des identités, consultez la documentation [Identity Service](../../identity-service/home.md) .

<!-- ## Relationship

Schemas define a static view of a concept, but do not provide specific details on how data based on these schemas (datasets, etc) may relate to one another. Adobe Experience Platform allows you to describe these relationships through the **Relationship** checkbox in the schema editor. 

In order to define a relationship, click on the field and check the **Relationship** checkbox on the right-side of the canvas. 

![](../images/tutorials/create-schema/relationship.png)

More information about relationships and other schema metadata can be found in the [Schema Registry API Developer Guide](../schema_registry_developer_guide.md). -->

## Activez le  à utiliser dans le client en temps réel {#profile}

L’éditeur de  de permet d’activer un  de à utiliser avec le [service d’](../../profile/home.md)intervention en temps réel des clients. fournit un holistique de chaque client en construisant un solidejeu d’attributs du client à 360°, ainsi qu’un compte horodaté de chaque interaction du client dans tout système intégré à Experience Platform.

Pour qu’un puisse être activé pour une utilisation avec le client en temps réel, il doit avoir une identité principale définie. Vous recevrez un message d’erreur &quot;Identité principale manquante&quot; si vous tentez d’activer un sans définir au préalable une identité principale.

![](../images/tutorials/create-schema/missing_primary_identity.png)

Pour activer le &quot;Membres de la loyauté&quot; à utiliser dans les  de, commencez par cliquer sur &quot;Membres de la loyauté&quot; dans la section *Structure* de l&#39;éditeur.

Sur le côté droit de l’éditeur, sous Propriétés *de*, des informations sur le sont affichées, y compris son nom d’affichage, sa description et son type. En plus de cette information, il y a un bouton bascule intitulé ****.

![](../images/tutorials/create-schema/unified_profile_toggle.png)

Cliquez sur **de** et une fenêtre contextuelle s’affiche, vous demandant de confirmer que vous souhaitez activer le  de pour l’ de l’.

![](../images/tutorials/create-schema/enable_unified_profile.png)

>[!NOTE] Une fois qu’un  a été activé pour l’ en temps réel du client et enregistré, il ne peut plus être désactivé.

## Étapes suivantes

Maintenant que vous avez fini de composer un  &quot;Membres de la Fidélité&quot;, vous pouvez voir le complet dans la section *Structure* de l&#39;éditeur. Cliquez sur **Enregistrer** et le  du sera enregistré dans la bibliothèque de , ce qui le rendra accessible par le registre de l&#39;.

Votre nouveau peut désormais être utilisé pour assimiler des données dans la plateforme. N’oubliez pas qu’une fois que le a été utilisé pour ingérer des données, seules des modifications additifs peuvent être apportées. Voir les [bases de la composition](../schema/composition.md) de  pour plus d’informations sur le contrôle de version  des.

Le  &quot;Membres de la fidélité&quot; est également disponible pour être affiché et géré à l’aide de l’API de registre . Pour commencer à travailler avec l&#39;API,  en lisant le guide [du développeur de l&#39;API de registre de l&#39;](../api/getting-started.md).

## Annexe

Les informations suivantes sont complémentaires au didacticiel de l’éditeur de  de.

### Create a new class {#create-new-class}

Experience Platform offre la possibilité de définir un  de basé sur une classe propre à votre entreprise.

Ouvrez la boîte de dialogue *Attribuer une classe* en cliquant sur **Attribuer** dans la section *Classe* de l’éditeur de  de. Dans la boîte de dialogue, sélectionnez **Créer une classe**.

Vous pouvez ensuite attribuer à votre nouvelle classe un nom **d’** affichage (un nom court, descriptif, unique et convivial pour la classe), une **description** et un **comportement** (&quot;Enregistrement&quot; ou &quot;Série de temps&quot;) pour les données que le va définir.

![Détails de la nouvelle classe](../images/tutorials/create-schema/create_new_class.png)

>[!NOTE] Lors de la création d’un qui implémente une classe définie par votre organisation, n’oubliez pas que les mixins sont disponibles uniquement pour une utilisation avec des classes compatibles. La classe que vous avez définie étant nouvelle, il n’existe aucun mixin compatible répertorié dans la boîte de dialogue *Ajouter Mixin* . Vous devez sélectionner **Créer un nouveau mixin** et définir un mixin à utiliser avec cette classe. La prochaine fois que vous composez un  qui implémente la nouvelle classe, le mixin que vous avez défini sera répertorié et disponible pour utilisation.

### Modification de la classe d’un {#change-class}

A tout moment au cours du processus initial de composition , avant l’enregistrement de la  de, vous pouvez modifier la classe sur laquelle repose la .

>[!WARNING] Veuillez faire attention avant de changer de classe. Les mixins ne sont compatibles qu’avec certaines classes. Par conséquent, la modification de la classe réinitialise le canevas et supprime tous les champs que vous avez ajoutés à ce point.

Pour modifier la classe, cliquez sur **Attribuer** en regard de *la classe* dans la section *Composition* de l’éditeur.

Lorsque la boîte de dialogue *Attribuer une classe* s’ouvre, vous pouvez choisir une nouvelle classe dans le  de disponible. Cliquez sur **Attribuer une classe** et une nouvelle boîte de dialogue s’ouvre vous demandant de confirmer que vous souhaitez affecter une nouvelle classe.

![Changer de classe](../images/tutorials/create-schema/assign_new_class_warning.png)

Si vous confirmez le changement de classe, le canevas sera réinitialisé et toutes les étapes de la composition seront perdues.