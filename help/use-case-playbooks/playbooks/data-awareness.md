---
solution: Experience Platform
title: Présentation de la prise en compte des données dans les classeurs de cas d’utilisation
description: Découvrez comment accélérer le temps de valorisation en copiant les ressources générées dans l’environnement de test d’inspiration finale vers d’autres environnements de test.
role: Developer
exl-id: 537eff13-f5fe-4cc9-9769-ab47b3cecda7
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# Ressources générées par le lecteur Publish dans d’autres environnements de test {#publish-to-other-sandboxes}

Les scénarios d’utilisation sont des modèles marketing conçus pour générer des ressources telles que des audiences, des schémas ou des parcours pour des cas d’utilisation marketing courants. Vous pouvez tester les ressources créées par des livres de jeu dans l’environnement de test inspirant. Lorsque vous êtes prêt, vous pouvez importer les ressources dans d’autres environnements de test de développement pour effectuer d’autres tests avec les données disponibles dans ces environnements de test. Lorsque vous êtes satisfait des tests, vous pouvez ensuite déplacer les ressources des environnements de test de développement vers les environnements de test de production.

Cependant, dans certains cas, vous avez peut-être déjà configuré vos propres schémas, champs et groupes de champs dans d’autres environnements de test de développement. Cela peut rendre certaines des ressources générées par les modèles de cas d’utilisation, comme les parcours, incompatibles avec vos données. Pour comprendre comment utiliser la fonctionnalité de sensibilisation aux données pour mieux aligner et compléter les ressources générées avec vos ressources existantes, lisez ce tutoriel.

## Conditions préalables {#prerequisites}

Avant de lire ce tutoriel, parcourez les [modèles de scénario d’utilisation disponibles](/help/use-case-playbooks/playbooks/choose.md#search-and-filter) et [créez une instance](/help/use-case-playbooks/playbooks/create-share-reuse.md) d’un playbook préféré.

La création d’une instance génère un ensemble de ressources telles que des parcours, des segments, des schémas et des messages dans l’environnement de test d’inspiration. Lisez la suite pour découvrir comment copier ces ressources dans d’autres environnements de test.

### Création et publication d’un module {#create-publish-package}

>[!NOTE]
>
> Vous ne pouvez importer des packages que dans d’autres environnements de développement. Une fois que vous avez apporté toutes les modifications ou mises à jour nécessaires, vous pouvez importer en production les ressources ou les modules de ces environnements de test de développement. Vous ne pouvez pas importer directement depuis les environnements de test des cahiers de travail du cas d’utilisation en production.

1. Pour importer des objets de l’environnement de test inspiré dans un autre environnement de test, accédez à une instance souhaitée d’un playbook de cas d’utilisation et sélectionnez **[!UICONTROL Publish sur un autre environnement de test]** pour exporter les artefacts sous la forme d’un package.

   ![GIF montrant les différentes instances de cas d&#39;utilisation](/help/use-case-playbooks/assets/playbooks/data-awareness/browse-to-existing-instances-of-playbook.gif)

2. Une fois que vous avez sélectionné le bouton **[!UICONTROL Publish to a another sandbox]** , un modal s’affiche. Renseignez le nom et la description facultative, puis sélectionnez **[!UICONTROL Créer]**. Cette étape regroupe les ressources générées dans un package qui peut être importé dans un autre environnement de test.

   ![Un modal pour créer un package](/help/use-case-playbooks/assets/playbooks/data-awareness/create-package-modal.png)

3. Accédez à la page **Sandbox** dans le volet de navigation de gauche et sélectionnez l’onglet **Packages** , recherchez votre package et publiez-le. Pour publier un package en état de brouillon, suivez les étapes du document [outil de test](/help/sandboxes/ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish).

   ![Package dans l’état préliminaire ou non publié](/help/use-case-playbooks/assets/playbooks/data-awareness/draft-mode.png)

   ![Publier le package](/help/use-case-playbooks/assets/playbooks/data-awareness/publish-draft.png)

4. Une fois la publication effectuée, un bouton **+** doit être activé en regard du nom sur la page de navigation des packages.

   ![Onglet Packages dans la page Sandbox](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

   >[!NOTE]
   >
   > Le package ne peut pas être importé tant qu’il est toujours en mode préliminaire. Ouvrez donc la page des détails du package et publiez le package.

5. Sélectionnez le contrôle **+** et lancez le workflow pour importer les ressources générées par le manuel de cas d’utilisation dans l’ **[!UICONTROL environnement de test Target]**. Sélectionnez un environnement de test cible et confirmez le nom du module à importer à l’aide de la liste déroulante. Ajoutez les détails de la tâche, tels que le nom et la description de la tâche, avant de passer à l’étape suivante.

   ![Lancer le workflow d&#39;import, sélectionner la cible, confirmer le package, ajouter les détails de la tâche.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-import-settings.png)

6. À l’étape **[!UICONTROL Afficher les dépendances]** , vous pouvez mapper des schémas et copier d’autres ressources de l’environnement de test d’inspiration dans l’environnement de test cible. Le bouton **[!UICONTROL Terminer]** est désactivé tant que vous n’avez pas mappé chaque schéma.

   ![&#x200B; Mappez les schémas à l&#39;étape &#39;Afficher les dépendances&#39;, en activant le bouton Terminer.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-view-dependencies.png)

### Mappage des schémas {#map-schemas}

1. Mappez le premier schéma. La boîte de dialogue de mappage de schéma affiche une liste déroulante pour sélectionner le schéma cible. Si le schéma source est un schéma de profil, il n’existe aucune autre option de schéma cible en plus du [&#x200B; schéma de profil d’union individuel](/help/xdm/classes/individual-profile.md). Vous pouvez voir les recommandations de mappage générées automatiquement entre les données Source et les champs cibles lors du premier affichage de la page. Vous pouvez éditer les mappages en sélectionnant le champ cible, puis en sélectionnant un nouveau champ. Si vous modifiez les mappages suggérés, utilisez le bouton **Valider** pour valider les nouveaux mappages et afficher les erreurs qui peuvent être liées aux nouveaux mappages. Sélectionnez **Enregistrer** une fois le mappage terminé.

   ![&#x200B; Boîte de dialogue de mappage de schéma avec une liste déroulante pour sélectionner un schéma cible.](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-fields.png)

2. Poursuivez le mappage de tous les champs des schémas. Si le schéma est un [schéma d’événement](/help/xdm/classes/experienceevent.md), la boîte de dialogue affiche une liste déroulante dans laquelle vous pouvez afficher tous les schémas d’événement dans l’environnement de test cible.

   ![Sélectionner un schéma cible dans la liste déroulante](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-event-schema.png)

3. Sélectionnez un schéma parmi les schémas disponibles dans l’ **environnement de test Target**.

   ![Sélectionner un schéma](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-available-schemas.png)

4. Effectuez le mappage et sélectionnez **Enregistrer**.

   ![Enregistrer le mappage](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-modal.png)

5. Une fois que vous avez effectué le mappage de tous les champs des schémas, sélectionnez **Terminer** pour terminer le workflow d&#39;import.

   ![Terminer le flux](/help/use-case-playbooks/assets/playbooks/data-awareness/complete-flow.png)

   >[!NOTE]
   >
   > Vous ne pouvez modifier aucune ressource, à l’exception des schémas, car il s’agit d’un environnement de test inspirant, mais ils s’affichent car il s’agit de dépendances du module.

### Statut de l’importation {#import-status}

1. Vous êtes automatiquement redirigé vers la page [**Imports**](/help/sandboxes/ui/sandbox-tooling.md#view-import-details) où vous pouvez voir la progression de votre importation.

   ![Page affichant la progression de l’importation](/help/use-case-playbooks/assets/playbooks/data-awareness/import-progress.png)

2. Pendant l’importation du package, les actifs du package sont créés dans l’environnement de test cible. Une fois l’importation terminée, ils font référence aux champs que vous avez mappés pendant le processus d’importation. Le processus est maintenant terminé et les ressources de l’environnement de test inspirant sont désormais également présentes dans votre environnement de test cible pour que vous puissiez le tester.

   ![Ressources générées dans l’environnement de test cible](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

## Étapes suivantes

Après avoir lu ce guide, vous comprenez mieux comment tirer parti des classeurs de cas d’utilisation avec l’[outil de test](/help/sandboxes/ui/sandbox-tooling.md#monitor-import-jobs-and-view-import-objects-details) pour créer des parcours exécutables qui référencent vos schémas. En savoir plus sur les [cas pratiques Real-Time CDP](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) courants.
