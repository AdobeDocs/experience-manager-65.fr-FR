---
title: Gestion de projets de traduction
seo-title: Gestion de projets de traduction
description: Découvrez comment gérer des projets de traduction dans AEM.
seo-description: Découvrez comment gérer des projets de traduction dans AEM.
uuid: f6f79b5b-dc08-4dde-b464-719345d233a6
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: c8672774-6911-497d-837b-1e5953c4226a
translation-type: tm+mt
source-git-commit: b9c77b9b50ae7f18198baddf82dffcd8de4f30be
workflow-type: tm+mt
source-wordcount: '3453'
ht-degree: 86%

---


# Gestion de projets de traduction{#managing-translation-projects}

Après avoir préparé le contenu à traduire, vous devez compléter la structure de langue en créant des copies de langue manquantes et créer des projets de traduction.

Les projets de traduction permettent de gérer la traduction du contenu d’AEM. Un projet de traduction est un type d&#39;AEM [projet](/help/sites-authoring/projects.md) qui contient des ressources qui doivent être traduites dans d&#39;autres langues. Ces ressources sont les pages et les actifs des [copies de langue](/help/sites-administering/tc-prep.md) créées à partir du gabarit de langue.

Lorsque des ressources sont ajoutées à un projet de traduction, une tâche de traduction est créée pour ces ressources. Les tâches comportent les commandes et les informations sur le statut utilisées pour gérer les processus de traduction humaine et automatique exécutés sur les ressources.

>[!NOTE]
>
>Un projet de traduction peut contenir plusieurs tâches de traduction.

Les projets de traduction sont des éléments dont l’exécution est longue, définis par langue et par méthode/fournisseur de traduction afin d’être en phase avec la gouvernance organisationnelle en matière d’internationalisation. Ils doivent être lancés en une seule fois, lors de la traduction initiale ou manuellement, et restent actifs pendant toute la durée des activités de mise à jour du contenu et de la traduction.

Les projets et les tâches de traduction sont créés avec des processus de préparation de la traduction. Ces processus possèdent trois options pour la traduction initiale (Créer et traduire) et les mises à jour (Mettre à jour une traduction) :

1. [Créer un projet](#creating-translation-projects-using-the-references-panel)
1. [Ajouter à un projet existant](#adding-pages-to-a-translation-project)
1. [Structure de contenu uniquement](#creating-the-structure-of-a-language-copy)

>[!NOTE]
>
>L’option 3 est indépendante de la tâche/du projet de traduction. Elle permet de copier les modifications apportées au contenu et à la structure du gabarit de langue aux copies de langue (non traduites). Vous pouvez l’utiliser pour préserver la synchronisation des gabarits de langue, même sans traduction.

## Réalisation de traductions initiales et mise à jour de traductions existantes {#performing-initial-translations-and-updating-existing-translations}

AEM détecte si un projet de traduction est créé pour la traduction initiale du contenu ou pour mettre à jour des copies de langue déjà traduites. Lorsque vous créez un projet de traduction pour une page et que vous indiquez les copies de langue pour lesquelles vous effectuez une traduction, AEM détecte si la page source existe déjà dans les copies de langue ciblées :

* **La copie de langue n’inclut pas la page:** AEM traite cette situation comme la traduction initiale. La page est copiée immédiatement dans la copie de langue et incorporée au projet. Lorsque la page traduite est importée dans AEM, AEM la copie directement dans la copie de langue.
* **La copie de langue comprend déjà la page:** AEM traite cette situation comme une traduction mise à jour. Un lancement est créé, et une copie de la page est ajoutée au lancement et incorporée au projet. Les lancements permettent de réviser les traductions mises à jour avant de les valider dans la copie de langue :

   * Lorsque la page traduite est importée dans AEM, elle remplace la page correspondante dans le lancement.
   * La page traduite ne remplace la copie de langue que lorsque le lancement est converti.

Par exemple, la racine de la langue /content/geometrixx/fr est créée pour la traduction française de la langue principale /content/geometrixx/en. Il n’y a pas d’autres pages dans la copie de langue française.

* Un projet de traduction est créé pour la page /content/geometrixx/en/products et toutes les pages enfants, ciblant la copie de langue française. La copie de langue n’incluant pas la page /content/geometrixx/fr/products, AEM copie immédiatement la page /content/geometrixx/fr/products et toutes les pages enfants dans la copie de langue française. Les copies sont également incluses dans le projet de traduction.
* Un projet de traduction est créé pour la page /content/geometrixx/fr et toutes les pages enfants, en ciblant la copie en français. Dans la mesure où la copie de langue inclut la page qui correspond à la page /content/geometrixx/fr (la racine de la langue), AEM copie la page /content/geometrixx/fr et toutes les pages enfants et les ajoute à un lancement. Les copies sont également incluses dans le projet de traduction.

## Création de projets de traduction à l’aide du panneau Références {#creating-translation-projects-using-the-references-panel}

Créez des projets de traduction afin de pouvoir exécuter et gérer le processus pour traduire les ressources de votre gabarit de langue. Lorsque vous créez des projets, vous spécifiez la page du gabarit de langue que vous traduisez et les copies de langue pour lesquelles vous effectuez la traduction :

* La configuration du cloud de la structure d’intégration de traduction associée à la page sélectionnée détermine de nombreuses propriétés des projets de traduction, comme le processus de traduction à utiliser.
* Un projet est créé pour chaque copie de langue sélectionnée.
* Une copie de la page sélectionnée et des ressources associées est créée et ajoutée à chaque projet. Ces copies sont ensuite envoyées au fournisseur de traduction pour être traduites.

Vous pouvez spécifier que les pages enfants de la page sélectionnée soient elles aussi sélectionnées. Dans ce cas, les copies des pages enfants sont également ajoutées à chaque projet afin d’être traduites. Lorsque des pages enfants sont associées à des configurations de structure d’intégration de traduction différentes, AEM crée des projets supplémentaires.

Vous pouvez également [créer manuellement des projets de traduction](#creating-a-translation-project-using-the-projects-console).

>[!NOTE]
>
>Pour créer un projet, votre compte doit être membre du groupe `project-administrators`.

**Traductions initiales et mise à jour de traductions**

Le panneau Références indique si vous mettez à jour les copies de langue existantes ou si vous créez la première version des copies de langue. Lorsqu’il existe une copie de langue pour la page sélectionnée, l’onglet Mettre à jour les copies de langue s’affiche pour permettre d’accéder aux commandes liées au projet.

![chlimage_1-239](assets/chlimage_1-239.png)

Après la traduction, vous pouvez [réviser la traduction](#reviewing-and-promoting-updated-content) avant de remplacer la copie de langue. Lorsqu’il n’existe pas copie de langue pour la page sélectionnée, l’onglet Créer et traduire s’affiche pour permettre d’accéder aux commandes liées au projet.

![chlimage_1-240](assets/chlimage_1-240.png)

### Création de projets de traduction pour une nouvelle copie de langue {#create-translation-projects-for-a-new-language-copy}

1. Utilisez la console Sites pour sélectionner la page que vous ajoutez aux projets de traduction.

   Par exemple, pour traduire les pages en anglais du site de démonstration Geometrixx, sélectionnez Site de démonstration Geometrixx > Anglais.

1. Dans la barre d’outils, cliquez ou appuyez sur Références.

   ![chlimage_1-241](assets/chlimage_1-241.png)

1. Sélectionnez Copies de langue, puis sélectionnez les copies de langue pour lesquelles vous traduisez les pages source.
1. Cliquez ou appuyez sur Créer et traduire, puis configurez la tâche de traduction :

   * Utilisez la liste déroulante Langues pour sélectionner une copie de langue à traduire. Sélectionnez d’autres langues, au besoin. Les langues qui figurent dans la liste correspondent aux [racines de langue que vous avez créées](/help/sites-administering/tc-prep.md#creating-a-language-root).
   * Pour traduire la page sélectionnée et toutes les pages enfant, sélectionnez Sélectionner toutes les pages secondaires. Pour ne traduire que la page sélectionnée, désélectionnez cette option.
   * Pour le projet, sélectionnez Créer un projet de traduction.
   * Saisissez le nom du projet.

   ![chlimage_1-242](assets/chlimage_1-242.png)

1. Cliquez ou appuyez sur Créer.

### Création de projets de traduction pour une copie de langue existante  {#create-translation-projects-for-an-existing-language-copy}

1. Utilisez la console Sites pour sélectionner la page que vous ajoutez aux projets de traduction.

   Par exemple, pour traduire les pages en anglais du site de démonstration Geometrixx, sélectionnez Site de démonstration Geometrixx > Anglais.

1. Dans la barre d’outils, cliquez ou appuyez sur Références.

   ![chlimage_1-243](assets/chlimage_1-243.png)

1. Sélectionnez Copies de langue, puis sélectionnez les copies de langue pour lesquelles vous traduisez les pages source.
1. Cliquez ou appuyez sur Mettre à jour les copies de langue, puis configurez la tâche de traduction :

   * Pour traduire la page sélectionnée et toutes les pages enfant, sélectionnez Sélectionner toutes les pages secondaires. Pour ne traduire que la page sélectionnée, désélectionnez cette option.
   * Pour le projet, sélectionnez Créer un projet de traduction.
   * Saisissez le nom du projet.

   ![chlimage_1-244](assets/chlimage_1-244.png)

1. Cliquez ou appuyez sur Commencer.

## Ajout de pages à un projet de traduction  {#adding-pages-to-a-translation-project}

Après avoir créé un projet de traduction, vous pouvez utiliser le volet Ressources pour ajouter des pages au projet. Il est utile d’ajouter des pages lorsque vous incorporez des pages de différentes branches dans le même projet.

Lorsque vous ajoutez des pages à un projet de traduction, les pages sont incorporées à une nouvelle tâche de traduction. Vous pouvez également [ajouter des pages à une tâche existante](#adding-pages-assets-to-a-translation-job).

Comme lors de la création d’un projet, lorsque vous ajoutez des pages, des copies des pages sont ajoutées à un lancement, si nécessaire, afin d’éviter de remplacer des copies de langue. (Voir [Création de projets de traduction pour une copie de langue existante](#performing-initial-translations-and-updating-existing-translations).)

1. Utilisez la console Sites pour sélectionner la page que vous ajoutez au projet de traduction.

   Par exemple, pour traduire les pages en anglais du site de démonstration Geometrixx, sélectionnez Site de démonstration Geometrixx > Anglais.

1. Dans la barre d’outils, cliquez ou appuyez sur Références.

   ![chlimage_1-245](assets/chlimage_1-245.png)

1. Sélectionnez Copies de langue, puis sélectionnez les copies de langue pour lesquelles vous traduisez les pages source.

   ![chlimage_1-35](assets/chlimage_1-35.jpeg)

1. Cliquez ou appuyez sur Mettre à jour les copies de langue, puis configurez les propriétés :

   * Pour traduire la page sélectionnée et toutes les pages enfant, sélectionnez Sélectionner toutes les pages secondaires. Pour ne traduire que la page sélectionnée, désélectionnez cette option.
   * Pour le projet, sélectionnez Ajouter à un projet de traduction existant.
   * Sélectionnez le projet.

   >[!NOTE]
   >
   >La langue cible définie dans le projet de traduction doit correspondre au chemin d’accès à la copie de langue, comme indiqué dans le panneau Références.

   ![chlimage_1-36](assets/chlimage_1-36.jpeg)

1. Cliquez ou appuyez sur Commencer.

## Ajout de pages/ressources à une tâche de traduction  {#adding-pages-assets-to-a-translation-job}

Vous pouvez ajouter des pages, des ressources, des balises ou des dictionnaires d’internationalisation (i18n) à la tâche de traduction de votre projet de traduction. Pour ajouter des pages ou des ressources :

1. Dans la partie inférieure de la mosaïque Tâche de traduction du projet de traduction, cliquez ou appuyez sur le bouton de sélection.

   ![chlimage_1-246](assets/chlimage_1-246.png)

1. Cliquez ou appuyez sur Ajouter des pages/ressources.

   ![chlimage_1-247](assets/chlimage_1-247.png)

1. Sélectionnez l’élément le plus élevé de la branche à ajouter, puis cliquez ou appuyez sur l’icône de coche. Vous pouvez sélectionner plusieurs éléments.

   ![chlimage_1-248](assets/chlimage_1-248.png)

1. Vous pouvez également choisir l’icône de recherche pour rechercher des pages ou des ressources à ajouter à la tâche de traduction.

   ![chlimage_1-249](assets/chlimage_1-249.png)

Les pages et/ou les ressources sont ajoutées à la tâche de traduction.

## Ajout de dictionnaires d’internationalisation à une tâche de traduction  {#adding-i-n-dictionaries-to-a-translation-job}

Vous pouvez ajouter des pages, des ressources, des balises ou des dictionnaires d’internationalisation (i18n) à la tâche de traduction de votre projet de traduction. Pour ajouter un dictionnaire d’internationalisation :

1. Dans la partie inférieure de la mosaïque Tâche de traduction du projet de traduction, cliquez ou appuyez sur le bouton de sélection.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Cliquez ou appuyez Ajouter un dictionnaire d’internationalisation.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Sélectionnez le dictionnaire à ajouter, puis cliquez ou appuyez sur le bouton Ajouter.

   ![chlimage_1-252](assets/chlimage_1-252.png)

Le dictionnaire se trouve maintenant dans la tâche de traduction.

![chlimage_1-253](assets/chlimage_1-253.png)

>[!NOTE]
>
>Pour plus d’informations sur les dictionnaires i18n, consultez [Utilisation de Translator pour la gestion des dictionnaires](/help/sites-developing/i18n-translator.md).

## Ajout de balises à une tâche de traduction {#adding-tags-to-a-translation-job}

Vous pouvez ajouter des pages, des ressources, des balises ou des dictionnaires d’internationalisation (i18n) à la tâche de traduction de votre projet de traduction. Pour ajouter des balises :

1. Dans la partie inférieure de la mosaïque Tâche de traduction du projet de traduction, cliquez ou appuyez sur le bouton de sélection.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. Cliquez ou appuyez sur Ajouter, puis sur Balises.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Sélectionnez les balises à ajouter, puis cliquez ou appuyez sur l’icône de coche. Vous pouvez sélectionner plusieurs éléments.

   ![chlimage_1-256](assets/chlimage_1-256.png)

Les balises sont maintenant ajoutées à la tâche de traduction.

![chlimage_1-257](assets/chlimage_1-257.png)

## Affichage des détails d’un projet de traduction {#seeing-translation-project-details}

La mosaïque Résumé de traduction contient les propriétés configurées pour un projet de traduction. Outre les [informations génériques du projet](/help/sites-authoring/projects.md#project-info), l’onglet Traduction contient des propriétés spécifiques à la traduction :

* Langue source : langue des pages qui sont en cours de traduction.
* Langue cible : langue dans laquelle les pages sont traduites.
* Méthode de traduction : processus de traduction. La traduction humaine et la traduction automatique sont prises en charge.
* Fournisseur de traduction : prestataire de services de traduction qui effectue la traduction.
* Catégorie de contenu : (traduction automatique) catégorie de contenu utilisée pour la traduction.
* Configuration du cloud : configuration de cloud pour le connecteur du service de traduction utilisé pour le projet.

Lors de la création d’un projet à l’aide du volet Ressources d’une page, ces propriétés sont configurées automatiquement en fonction des propriétés de la page source.

![chlimage_1-258](assets/chlimage_1-258.png)

## Suivi du statut d’une tâche de traduction {#monitoring-the-status-of-a-translation-job}

La mosaïque Tâche de traduction d’un projet de traduction fournit le statut d’une tâche de traduction, ainsi que le nombre de pages et les ressources de la tâche.

![chlimage_1-259](assets/chlimage_1-259.png)

Le tableau ci-dessous décrit les différents statuts qu’une tâche ou un élément de la tâche peut avoir :

| État | Description |
|---|---|
| Draft | La tâche de traduction n&#39;a pas été démarrée. Lors de leur création, les tâches de traduction présentent le statut BROUILLON. |
| Envoyé | Les fichiers de la tâche de traduction ont ce statut lorsqu’ils ont été correctement envoyés au service de traduction. Cet état peut survenir après l’émission de la commande Request Scope ou de la commande Début. |
| Portée demandée | Pour le processus de traduction humaine, les fichiers de la tâche ont été envoyés au fournisseur de traduction pour l’application de plage. Ce statut est défini après l’exécution de la commande Portée de la demande. |
| Portée terminée | Le fournisseur a défini la portée de la tâche de traduction. |
| Engagé pour la traduction | Le propriétaire du projet a accepté la portée. Ce statut indique que le fournisseur de traduction doit commencer à traduire les fichiers de la tâche. |
| Traduction en cours | Pour une tâche, la traduction d’un ou plusieurs fichiers de la tâche n’est pas encore terminée. Pour un élément de la tâche, l’élément est en cours de traduction. |
| Traduit | Pour une tâche, la traduction de tous les fichiers de la tâche est terminée. Pour un élément de la tâche, l’élément est traduit. |
| Prêt pour la révision | L’élément de la tâche est traduit et le fichier a été importé dans AEM. |
| Terminer | Le propriétaire du projet a indiqué que le contrat de traduction était terminé. |
| Annuler | Indique que le fournisseur de traduction doit arrêter de travailler sur une tâche de traduction. |
| Mise à jour de l’erreur | Une erreur s&#39;est produite lors du transfert de fichiers entre AEM et le service de traduction. |
| Etat inconnu | Une erreur inconnue s&#39;est produite. |

Pour afficher le statut des différents fichiers de la tâche, cliquez ou appuyez sur le bouton de sélection de la mosaïque.

## Définition du délai des tâches de traduction  {#setting-the-due-date-of-translation-jobs}

Spécifiez la date à laquelle le fournisseur de traduction doit renvoyer les fichiers traduits. Vous pouvez définir le délai de livraison du projet ou d’une tâche spécifique :

* **Projet** : les tâches de traduction du projet héritent du délai.
* **Tâche** : le délai défini pour la tâche remplace le délai défini pour le projet.

La définition du délai ne fonctionne correctement que lorsque le fournisseur de traduction auquel vous faites appel prend en charge cette fonctionnalité.

La procédure ci-dessous définit le délai de livraison d’un projet.

1. Cliquez ou appuyez sur le bouton de sélection de la mosaïque Résumé de traduction.

   ![chlimage_1-260](assets/chlimage_1-260.png)

1. Sur l’onglet De base, utilisez le sélecteur de date de la propriété Échéance pour sélectionner le délai.

   ![chlimage_1-261](assets/chlimage_1-261.png)

1. Cliquez ou appuyez sur Terminé.

La procédure ci-dessous définit le délai de livraison d’une tâche de traduction.

1. Sur la mosaïque Tâche de traduction, cliquez ou appuyez sur le menu Commandes, puis sur Échéance.

   ![chlimage_1-262](assets/chlimage_1-262.png)

1. Dans la boîte de dialogue, cliquez ou appuyez sur l’icône de calendrier, sélectionnez la date et l’heure à utiliser comme délai, puis cliquez sur Enregistrer.

   ![chlimage_1-263](assets/chlimage_1-263.png)

## Définition de la portée d’une tâche de traduction {#scoping-a-translation-job}

Définissez la portée de la tâche de traduction afin que le prestataire de services de traduction vous fournisse une estimation du coût de la traduction. Lorsque vous définissez la portée d’une tâche, les fichiers source sont envoyés au fournisseur de traduction, qui compare le texte à son pool de traductions stockées (mémoire de traduction). En règle générale, la portée est le nombre de mots à traduire.

Pour plus d’informations sur les résultats de la définition de la portée, contactez le fournisseur de traduction.

>[!NOTE]
>
>La définition de la portée est facultative. Vous pouvez commencer une tâche de traduction sans définir la portée.

Lorsque vous définissez la portée d’une tâche de traduction, l’état de la tâche est `Scope Requested`. Lorsque le fournisseur de traduction renvoie l’étendue, l’état est remplacé par `Scope Completed`. Lorsque la définition de la portée est terminée, vous pouvez utiliser la commande Afficher la portée pour consulter les résultats de la définition de la portée.

La définition de la portée ne fonctionne correctement que lorsque le fournisseur de traduction auquel vous faites appel prend en charge cette fonctionnalité.

1. Dans la console Projets, ouvrez le projet de traduction.
1. Sur la mosaïque Tâche de traduction, cliquez ou appuyez sur le menu Commandes, puis cliquez ou appuyez sur Portée de la demande.

   ![chlimage_1-264](assets/chlimage_1-264.png)

1. Lorsque le statut de la tâche devient PORTÉE TERMINÉE, sur la mosaïque Tâche de traduction, cliquez ou appuyez sur le menu Commandes, puis cliquez ou appuyez sur Afficher la portée.

## Début d’une tâche de traduction  {#starting-a-translation-job}

Commencez une tâche de traduction pour traduire les pages source dans la langue cible. La traduction est effectuée selon les valeurs des propriétés de la mosaïque Résumé de traduction.

Une fois que vous avez commencé la tâche de traduction, la mosaïque Tâche de traduction affiche le statut Traduction en cours.

![chlimage_1-265](assets/chlimage_1-265.png)

1. Dans la console Projets, ouvrez le projet de traduction.
1. Sur la mosaïque Tâche de traduction, cliquez ou appuyez sur le menu Commandes, puis cliquez ou appuyez sur Commencer.

   ![chlimage_1-266](assets/chlimage_1-266.png)

1. Dans la boîte de dialogue Action qui confirme le début de la traduction, cliquez ou appuyez sur Fermer.

## Annulation d’une tâche de traduction  {#canceling-a-translation-job}

Annulez une tâche de traduction pour suspendre le processus de traduction et empêcher le fournisseur de traduction d’effectuer d’autres traductions. Vous pouvez annuler une tâche lorsque celle-ci a le statut `Committed For Translation` ou `Translation In Progress`.

1. Dans la console Projets, ouvrez le projet de traduction.
1. Sur la mosaïque Tâche de traduction, cliquez ou appuyez sur le menu Commandes, puis cliquez ou appuyez sur Annuler.
1. Dans la boîte de dialogue Action qui confirme l’annulation de la traduction, cliquez ou appuyez sur OK.

## Workflow Accepter/rejeter  {#accept-reject-workflow}

Lorsque le contenu revient après traduction et possède le statut Prêt pour la révision, vous pouvez passer à la tâche de traduction et accepter/rejeter le contenu.

![chlimage_1-267](assets/chlimage_1-267.png)

Si vous sélectionnez Rejeter la traduction, vous avez la possibilité d’ajouter un commentaire.

![chlimage_1-268](assets/chlimage_1-268.png)

Le rejet du contenu le renvoie au fournisseur de traduction, qui peut consulter le commentaire.

## Affichage et promotion d’un contenu mis à jour  {#reviewing-and-promoting-updated-content}

Lorsque le contenu est traduit pour une copie de langue existante, révisez les traductions, apportez-y des modifications, si nécessaire, puis convertissez les traductions pour les déplacer vers la copie de langue. Vous pouvez réviser les fichiers traduits lorsque la tâche de traduction possède le statut Prêt pour la révision.

![chlimage_1-269](assets/chlimage_1-269.png)

1. Sélectionnez la page dans le gabarit de langue, cliquez ou appuyez sur Références, puis cliquez ou appuyez sur Copies de langue.
1. Cliquez ou appuyez sur la copie de langue à réviser.

   ![chlimage_1-270](assets/chlimage_1-270.png)

1. Cliquez ou appuyez sur Lancement pour afficher les commandes liées au lancement.

   ![chlimage_1-271](assets/chlimage_1-271.png)

1. Pour ouvrir la copie de lancement de la page pour réviser et modifier le contenu, cliquez sur Ouvrir la page.
1. Après avoir révisé le contenu et apporté les modifications nécessaires, pour convertir la copie du lancement, cliquez sur Convertir.
1. Dans la page Convertir le lancement, spécifiez les pages à convertir, puis cliquez ou appuyez sur Convertir.

## Comparaison des copies de langue  {#comparing-language-copies}

Pour comparer des copies de langue au gabarit de langue :

1. Dans la console **Sites**, accédez à la copie de langue à comparer.
1. Ouvrez le panneau **[Références](/help/sites-authoring/basic-handling.md#references)**.
1. Sous l&#39;en-tête **Copies**, sélectionnez **Copies de langue.**
1. Sélectionnez votre copie de langue spécifique, puis cliquez sur **Comparer au Principal **ou **Comparer au précédent **si applicable.

   ![chlimage_1-37](assets/chlimage_1-37.jpeg)

1. Les deux pages (de lancement et source) s’ouvrent côte à côte.

   Pour des informations complètes sur l’utilisation de cette fonction, voir [Différence entre les pages](/help/sites-authoring/page-diff.md).

## Fin et archivage des tâches de traduction  {#completing-and-archiving-translation-jobs}

Effectuez une tâche de traduction après avoir révisé les fichiers traduits du fournisseur. Pour les processus de traduction humaine, la réalisation d’une traduction indique au fournisseur que le contrat de traduction est terminé et qu’il doit enregistrer la traduction dans sa mémoire de traduction.

Une fois que vous avez terminé la tâche, elle possède le statut Terminé.

![chlimage_1-272](assets/chlimage_1-272.png)

Archivez une tâche de traduction une fois qu’elle est terminée et que vous n’avez plus besoin de consulter les détails du statut de cette tâche. Lorsque vous archivez la tâche, la mosaïque Tâche de traduction est supprimée du projet.

## Création de la structure d’une copie de langue  {#creating-the-structure-of-a-language-copy}

Remplissez la copie de langue afin qu’elle contienne le contenu de la langue principale que vous traduisez. Avant de renseigner votre copie de langue, [vous devez avoir créé la racine de langue](/help/sites-administering/tc-prep.md#creating-a-language-root) de la copie de langue.

1. Utilisez la console Sites pour sélectionner la racine de langue de la langue principale utilisée comme source. Par exemple, pour traduire les pages en anglais du site de démonstration Geometrixx, sélectionnez Contenu > Site de démonstration Geometrixx > Anglais.
1. Dans la barre d’outils, cliquez ou appuyez sur Références.

   ![chlimage_1-273](assets/chlimage_1-273.png)

1. Sélectionnez Copies de langue, puis sélectionnez les copies de langue à remplir.

   ![chlimage_1-38](assets/chlimage_1-38.jpeg)

1. Cliquez ou appuyez sur Mettre à jour des copies de langue pour afficher les outils de traduction et configurez les propriétés :

   * Cliquez sur l’option Sélectionner toutes les pages secondaires.
   * Pour un projet, sélectionnez Créer uniquement la structure.

   ![chlimage_1-39](assets/chlimage_1-39.jpeg)

1. Cliquez ou appuyez sur Commencer.

## Création d’un projet de traduction à l’aide de la console Projets  {#creating-a-translation-project-using-the-projects-console}

Si vous préférez utiliser la console Projets, vous pouvez créer manuellement un projet de traduction.

>[!NOTE]
>
>Pour créer un projet, votre compte doit être membre du groupe `project-administrators`.

Lorsque vous créez manuellement un projet de traduction, vous devez fournir des valeurs pour les propriétés associées à la traduction ci-dessous en complément des [propriétés de base](/help/sites-authoring/touch-ui-managing-projects.md#creating-a-project) :

* **Nom** : nom du projet.
* **Langue source** : langue du contenu source.
* **Langue cible** : langue vers laquelle le contenu est traduit.
* **Méthode de conversion** : sélectionnez Traduction humaine pour indiquer que la traduction doit être effectuée manuellement.

1. Dans la barre d’outils de la console Projets, cliquez ou appuyez sur Créer.
1. Sélectionnez le modèle Projet de traduction, puis cliquez ou appuyez sur Suivant.
1. Saisissez les valeurs pour les propriétés de base.
1. Cliquez ou appuyez sur Avancé et saisissez les valeurs pour les propriétés liées à la traduction.
1. Cliquez ou appuyez sur Créer. Dans la boîte de dialogue de confirmation, cliquez ou appuyez sur Terminé pour revenir à la console Projets ou cliquez ou appuyez sur Ouvrir un projet pour ouvrir le projet et commencer à le gérer.

## Exportation d’une tâche de traduction  {#exporting-a-translation-job}

Vous pouvez télécharger le contenu d’une tâche de traduction, par exemple, pour l’envoyer à un fournisseur de traduction qui n’est pas intégré à AEM par le biais d’un connecteur ou pour réviser le contenu.

1. Dans le menu déroulant de la mosaïque Tâche de traduction, cliquez ou appuyez sur Exporter.
1. Dans la boîte de dialogue Exporter, cliquez ou appuyez sur Télécharger le fichier exporté et, si nécessaire, utilisez la boîte de dialogue du navigateur web pour enregistrer le fichier.
1. Dans la boîte de dialogue Exporter, cliquez ou appuyez sur Fermer.

## Importation d’une tâche de traduction  {#importing-a-translation-job}

Vous pouvez importer du contenu traduit dans AEM, par exemple, lorsque votre fournisseur de traduction vous l’envoie, car il n’est pas intégré à AEM par le biais d’un connecteur.

1. Dans le menu déroulant de la mosaïque Tâche de traduction, cliquez ou appuyez sur Importer.
1. Utilisez la boîte de dialogue du navigateur web pour sélectionner le fichier à importer.
1. Dans la boîte de dialogue Importer, cliquez ou appuyez sur Fermer.

