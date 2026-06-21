---
solution: Experience Platform
title: Présentation de la connaissance des données dans les playbooks de cas d’utilisation
description: Découvrez comment accélérer le délai de valorisation en copiant les ressources générées dans le sandbox d’inspiration final vers d’autres sandbox.
role: Developer
exl-id: 537eff13-f5fe-4cc9-9769-ab47b3cecda7
TQID: https://experienceleague.adobe.com/1YhhTYyxgj-PKTqU3NDs0BWg4OHRLAmqWiOpc0R5T4E
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: e0eb8757-182f-49f3-94a4-1587d16f5094id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 915
ht-degree: 0%

---

# Publication de ressources générées par un playbook dans d’autres sandbox {#publish-to-other-sandboxes}

Les playbooks de cas d’utilisation sont des modèles marketing conçus pour générer des ressources telles que des audiences, des schémas ou des parcours pour des cas d’utilisation marketing courants. Vous pouvez tester les ressources créées par les playbooks dans le sandbox d’inspiration et, lorsque vous êtes prêt(e), vous pouvez importer les ressources dans d’autres sandbox de développement pour les tester davantage avec les données disponibles dans ces sandbox. Une fois les tests effectués, vous pouvez déplacer les ressources des sandbox de développement vers les sandbox de production.

Cependant, dans certains cas, vous avez peut-être déjà configuré vos propres schémas, champs et groupes de champs dans d’autres sandbox de développement. Cela peut rendre certaines des ressources générées par les modèles de cas d’utilisation, telles que les parcours, incompatibles avec vos données. Pour comprendre comment utiliser la fonctionnalité de connaissance des données afin de mieux aligner et compléter les ressources générées avec vos ressources existantes, consultez ce tutoriel.

## Conditions préalables {#prerequisites}

Avant de lire ce tutoriel, parcourez les [modèles de playbook de cas d’utilisation disponibles](/help/use-case-playbooks/playbooks/choose.md#search-and-filter) et [créez une instance](/help/use-case-playbooks/playbooks/create-share-reuse.md) d’un playbook préféré.

La création d’une instance génère un ensemble de ressources telles que des parcours, des segments, des schémas et des messages dans le sandbox source d’inspiration. Lisez la suite pour savoir comment copier ces ressources dans d’autres sandbox.

### Création et publication d’un package {#create-publish-package}

>[!NOTE]
>
> Vous ne pouvez importer des packages que dans d’autres sandbox de développement. Une fois toutes les modifications ou mises à jour nécessaires effectuées, vous pouvez importer les ressources ou les packages de ces sandbox de développement en production. Vous ne pouvez pas importer directement des sandbox des playbooks de cas d’utilisation vers la production.

1. Pour importer des objets du sandbox source d’inspiration dans un autre sandbox, accédez à l’instance souhaitée d’un playbook de cas d’utilisation, puis sélectionnez **[!UICONTROL Publier dans un autre sandbox]** pour exporter les artefacts en tant que package.

   ![GIF présentant les différentes instances de cas d’utilisation](/help/use-case-playbooks/assets/playbooks/data-awareness/browse-to-existing-instances-of-playbook.gif)

2. Une fois que vous avez sélectionné le bouton **[!UICONTROL Publier dans un autre sandbox]**, une boîte de dialogue modale s’affiche. Renseignez le nom et la description facultative, puis sélectionnez **[!UICONTROL Créer]**. Cette étape regroupe les ressources générées dans un package qui peut être importé dans un autre sandbox.

   ![Boîte de dialogue modale pour la création d’un package](/help/use-case-playbooks/assets/playbooks/data-awareness/create-package-modal.png)

3. Accédez à la page **Sandbox** dans le volet de navigation de gauche, sélectionnez l’onglet **Packages**, recherchez votre package et publiez-le. Pour publier un package à l’état de brouillon, suivez les étapes du document [outils sandbox](/help/sandboxes/ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish).

   ![Package à l’état de brouillon ou dépublié](/help/use-case-playbooks/assets/playbooks/data-awareness/draft-mode.png)

   ![ Publication du package ](/help/use-case-playbooks/assets/playbooks/data-awareness/publish-draft.png)

4. Une fois la publication réussie, sur la page de navigation des packages, un bouton **+** doit s’afficher en regard du nom.

   ![ Onglet Packages de la page Sandbox ](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

   >[!NOTE]
   >
   > Le package ne peut pas être importé s’il est toujours en mode brouillon. Par conséquent, ouvrez la page des détails du package et publiez-le.

5. Sélectionnez le contrôle **+** et lancez le workflow pour importer les ressources générées par le playbook de cas d’utilisation dans le **[!UICONTROL sandbox cible]**. Sélectionnez un sandbox cible et confirmez le nom du package que vous souhaitez importer à l’aide de la liste déroulante. Ajoutez les détails de la tâche, tels que son nom et sa description, avant de passer à l’étape suivante.

   ![Lancer le workflow d’importation, sélectionner la cible, confirmer le package et ajouter les détails de la tâche.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-import-settings.png)

6. Dans l’étape **[!UICONTROL Afficher les dépendances]**, vous pouvez mapper des schémas et copier d’autres ressources du sandbox source d’inspiration vers le sandbox cible. Le bouton **[!UICONTROL Terminer]** est désactivé jusqu’à ce que vous mappez chaque schéma.

   ![Mappez les schémas à l’étape « Afficher les dépendances » en activant le bouton Terminer.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-view-dependencies.png)

### Mappage des schémas {#map-schemas}

1. Mappez le premier schéma. La boîte de dialogue de mappage de schéma affiche une liste déroulante pour sélectionner le schéma cible. Si le schéma source est un schéma de profil, il n’existe aucune autre option de schéma cible en dehors du [schéma de profil d’union individuel](/help/xdm/classes/individual-profile.md). Vous pouvez voir les recommandations de mappage générées automatiquement entre les champs Source Data et Target lorsque la page est affichée pour la première fois. Vous pouvez modifier les mappages en sélectionnant le champ cible, puis en sélectionnant un nouveau champ. Si vous modifiez les mappages suggérés, utilisez le bouton **Valider** pour valider les nouveaux mappages et afficher les erreurs qui peuvent être liées aux nouveaux mappages. Sélectionnez **Enregistrer** une fois le mappage terminé.

   ![Boîte de dialogue de mappage de schéma avec une liste déroulante pour sélectionner un schéma cible.](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-fields.png)

2. Poursuivez le mappage de tous les champs des schémas. Si le schéma est un [schéma d’événement](/help/xdm/classes/experienceevent.md), la boîte de dialogue affiche une liste déroulante dans laquelle vous pouvez afficher tous les schémas d’événement du sandbox cible.

   ![Sélectionner un schéma cible dans la liste déroulante](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-event-schema.png)

3. Sélectionnez un schéma parmi les schémas disponibles dans le **sandbox cible**.

   ![Sélectionner un schéma](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-available-schemas.png)

4. Terminez le mappage et sélectionnez **Enregistrer**.

   ![ Enregistrer le mappage ](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-modal.png)

5. Une fois que vous avez terminé de mapper tous les champs des schémas, sélectionnez **Terminer** pour terminer le workflow d’importation.

   ![ Terminer le flux ](/help/use-case-playbooks/assets/playbooks/data-awareness/complete-flow.png)

   >[!NOTE]
   >
   > Vous ne pouvez modifier aucune ressource, à l’exception des schémas , car il s’agit d’un sandbox source d’inspiration, mais elles s’affichent en tant que dépendances du package.

### Etat de l’import {#import-status}

1. Vous êtes automatiquement redirigé vers la page [**Imports**](/help/sandboxes/ui/sandbox-tooling.md#view-import-details) où vous pouvez voir la progression de votre importation.

   ![Page affichant la progression de l’importation](/help/use-case-playbooks/assets/playbooks/data-awareness/import-progress.png)

2. Pendant l’importation du package, les ressources du package sont créées dans le sandbox cible. Une fois terminés, ils référencent les champs que vous avez mappés pendant le processus d’importation. Le processus est maintenant terminé et les ressources du sandbox source d’inspiration sont désormais également présentes dans votre sandbox cible pour que vous puissiez les tester.

   ![ Ressources générées dans le sandbox cible ](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

## Étapes suivantes

Vous êtes arrivé au bout de ce guide. À présent, vous comprenez mieux comment tirer parti des playbooks de cas d’utilisation avec l’[outil Sandbox](/help/sandboxes/ui/sandbox-tooling.md#monitor-import-jobs-and-view-import-objects-details) pour créer des parcours exécutables qui référencent vos schémas. En savoir plus sur les cas d’utilisation courants de [](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md).
