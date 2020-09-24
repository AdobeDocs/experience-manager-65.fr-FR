---
title: Migration de ressources et de documents AEM Forms
seo-title: Migration de ressources et de documents AEM Forms
description: L’utilitaire de migration vous permet de migrer des ressources et des documents AEM Forms d’AEM 6.3 Forms ou versions antérieures vers AEM 6.4 Forms.
seo-description: L’utilitaire de migration vous permet de migrer des ressources et des documents AEM Forms d’AEM 6.3 Forms ou versions antérieures vers AEM 6.4 Forms.
uuid: a3fdf940-7fc2-441c-91c8-ad66ba47e5f2
content-type: reference
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-strategy: max-2018
discoiquuid: 39dfef85-d047-4b6d-a0f5-92bd77df103b
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '1809'
ht-degree: 71%

---


# Migration de ressources et de documents AEM Forms{#migrate-aem-forms-assets-and-documents}

The Migration utility converts the [Adaptive Forms assets](../../forms/using/introduction-forms-authoring.md), [cloud configrurations](/help/sites-developing/extending-cloud-config.md), and [Correspondence Management assets](/help/forms/using/cm-overview.md) from the format used in the earlier versions to the format used in AEM 6.5 Forms. Lorsque vous exécutez l’utilitaire de migration, les éléments suivants sont migrés :

* Composants personnalisés pour les formulaires adaptatifs
* Modèles de formulaires adaptatifs et de Correspondence Management
* Configurations cloud
* Correspondence Management et ressources de formulaires adaptatifs

>[!NOTE]
>
>En cas de mise à niveau dynamique, pour les ressources de Correspondence Management, vous pouvez exécuter la migration à chaque importation des actifs. Pour la migration de Correspondence Management, le package de compatibilité Forms doit être installé.

## Approche de la migration {#approach-to-migration}

You can [upgrade](../../forms/using/upgrade.md) to the latest version of AEM Forms 6.5 from AEM Forms 6.4, 6.3, or 6.2 or perform a fresh installation. Selon que vous avez mis à niveau votre installation précédente ou procédé à une nouvelle installation, vous devez effectuer l’une des opérations suivantes :

**En cas de mise à niveau statique**

Si vous avez effectué une mise à niveau statique, l’instance mise à niveau contient déjà les ressources et les documents. Toutefois, afin de pouvoir utiliser les ressources et les documents, vous devez installer le [package de compatibilité AEMFD](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html) (comprenant le package de compatibilité Correspondence Management)

Vous devez ensuite les mettre à jour en [exécutant l’utilitaire de migration](#runningmigrationutility).

**En cas d’installation dynamique**

If it is an out of place (fresh) installation, before you can use the assets and documents, you will need to install [AEMFD Compatibility package](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html) (includes the Correspondence Management Compatibility package).

Then you need to import your asset package (zip or cmp) on the new setup and then update the assets and documents by [running the Migration utility](#runningmigrationutility). adobe recommande de créer de nouveaux actifs sur la nouvelle configuration uniquement après avoir exécuté l’utilitaire de migration.

En raison de changements [liés à la rétrocompatibilité](/help/sites-deploying/backward-compatibility.md), les emplacements de quelques dossiers dans crx-repository ont changé. Exportez et importez manuellement les dépendances (bibliothèques et ressources personnalisées) de la configuration précédente vers un nouvel environnement.

## Read before you proceed with the migration {#prerequisites}

Pour les ressources de Correspondence Management :

* For the assets that are imported from the previous platform, a property gets added: **fd:version=1.0**.
* Depuis AEM 6.1 Forms, les commentaires ne sont pas disponibles hors champ. Les commentaires ajoutés précédemment sont disponibles dans les actifs mais ne sont pas automatiquement affichés sur l’interface. Vous devez personnaliser la propriété extendedProperties dans l’interface utilisateur d’AEM Forms pour rendre les commentaires visibles.
* Dans certaines versions précédentes telles que LiveCycle ES4, le texte était modifié à l’aide de Flex RichTextEditor, mais depuis AEM 6.1 Forms, un éditeur HTML est utilisé. En raison du rendu et de l’apparence des polices, les tailles et les marges des polices peuvent varier par rapport à celles des versions précédentes dans l’interface utilisateur d’auteur. Toutefois, l’apparence des lettres est la même une fois rendue.
* Les listes dans les modules de texte sont améliorées et leur rendu est maintenant différent. Des différences visuelles peuvent exister. Nous vous recommandons d’afficher et de visualiser les lettres si vous utilisez des listes dans des modules de texte.
* Etant donné que les modules de contenu image sont convertis en ressources de gestion des actifs numériques et que les mises en page et les fragments sont ajoutés aux formulaires pendant la migration, la propriété Mis à jour par de ces modules est définie sur Administrateur.
* L’historique des versions des actifs n’est pas migré et n’est pas disponible après la migration. L’historique des versions suivant, intervenant après la migration, est conservé.
* L’état Prêt à publier est déprécié depuis AEM 6.1 Forms, de sorte que tous les actifs à l’état Prêt à publier passent à l’état Modifié.
* L’interface utilisateur étant mise à jour dans AEM Forms 6.3, les étapes d’exécution des personnalisations sont également différentes. Vous devez de nouveau effectuer la personnalisation si vous migrez depuis une version antérieure à 6.3.
* Les fragments de mise en page passent de /content/apps/cm/layouts/fragmentlayouts/1001 à /content/apps/cm/modules/fragmentlayouts. La référence au dictionnaire de données dans les ressources affiche le chemin du dictionnaire de données au lieu de son nom.
* Tous les espaces de tabulation utilisés pour l’alignement dans les modules de texte doivent être réajustés. Pour plus d’informations, voir [Correspondence Management - Utilisation de l’espacement des tabulations pour organiser le texte](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).
* Les configurations du compositeur d’actifs sont modifiées dans les configurations de Correspondence Management.
* Les ressources sont déplacées dans des dossiers portant des noms tels que Texte existant et Liste existante.

## Utilisation de l’utilitaire de migration {#using-the-migration-utility}

### Exécution de l’utilitaire de migration {#runningmigrationutility}

Exécutez l’utilitaire de migration avant toute modification ou création de ressources. Nous vous recommandons de ne pas exécuter l’utilitaire après une modification ou création de ressources. Assurez-vous que l’interface utilisateur Correspondence Management ou Ressources Forms adaptatives n’est pas ouverte pendant l’exécution du processus de migration.

Lorsque vous exécutez l’utilitaire de migration pour la première fois, un journal est créé avec le chemin et le nom suivants : \[aem-installation-directory]\cq-quickstart\logs\aem-forms-migration.log. Ce journal conserve les informations de migration mises à jour de Correspondence Management et des formulaires adaptatifs, telles que le déplacement des ressources.

>[!NOTE]
>
>Avant d’exécuter l’utilitaire de migration, assurez-vous d’avoir sauvegardé votre crx-repository.

1. Dans une session de navigateur, connectez-vous à l’instance d’auteur AEM en tant qu’administrateur.

1. Ouvrez l’URL suivante dans le navigateur :

   https://[*hostname*]:[*port*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   Le navigateur affiche quatre options :

   * Migration des ressources d’AEM Forms
   * Migration de composants personnalisés de formulaires adaptatifs
   * Migration de modèles de formulaires adaptatifs
   * Migration des configurations cloud AEM Forms

1. Procédez comme suit pour effectuer la migration :

   * Pour migrer les **ressources**, appuyez sur Migration des ressources d’AEM Forms et dans l’écran suivant, appuyez sur **Lancer la migration**. Les éléments suivants sont migrés :

      * Formulaires adaptatifs
      * Fragments de document
      * Thèmes
      * Lettres
      * Dictionnaires de données

   >[!NOTE]
   >
   >Pendant la migration des actifs, des messages d’avertissement tels que « Conflit détecté pour ... » peuvent s’afficher. Ces messages indiquent que les règles de certains composants des formulaires adaptatifs n’ont pas pu être migrées. Par exemple, si le composant possède un événement qui contient à la fois des règles et des scripts, si les règles se produisent après un script, aucune des règles du composant n’est migrée. Cependant, de telles règles peuvent être migrées en ouvrant l’éditeur de règles dans la création de formulaires adaptatifs.
   >
   >
   >Ces composants peuvent être migrés en les ouvrant dans l’éditeur de règles dans l’éditeur de formulaires adaptatifs.
   >
   >
   >
   >    * Pour migrer des règles et des scripts (non requis si la mise à niveau de la version 6.3) dans des composants personnalisés, appuyez sur Migration des composants personnalisés de Forms adaptatif et, dans l’écran suivant, appuyez sur Migration des Débuts. Les éléments suivants sont migrés :    >
      >
      >
      >        

      * Règles et scripts créés à l’aide de éditeur de règles (6.1 FP1 et versions ultérieures)
      >        * Scripts créés à l’aide de l’onglet Script dans l’interface utilisateur de la version 6.1 et versions antérieures
   >
   >
   >    * Pour migrer des modèles (non requis si la mise à niveau est effectuée à partir des versions 6.3 et 6.4), appuyez sur Migration de modèles Forms adaptatif et, dans l’écran suivant, appuyez sur Migration de Débuts. Les éléments suivants sont migrés :

      >
      >
      >
      >        


      * Anciens modèles : modèles de formulaires adaptatifs créés sous /apps à l’aide d’AEM version Forms 6.1 ou antérieure. Ceci inclut les scripts qui ont été définis dans les composants du modèle.
      >        * Nouveaux modèles - Modèles de formulaires adaptatifs créés à l’aide de l’éditeur de modèles sous /conf. Cela inclut la migration des règles et des scripts créés à l’aide de l’éditeur de règles.


   * To migrate adaptive form custom components, tap **Adaptive Forms Custom Components Migration** and in the Custom Components Migration page, tap **Start Migration**. Les éléments suivants sont migrés :

      * Composants personnalisés écrits pour les formulaires adaptatifs
      * Incrustations de composants, le cas échéant.
   * To migrate adaptive form templates, tap **Adaptive Forms Template Migration** and in the Custom Components Migration page, tap **Start Migration**. Les éléments suivants sont migrés :

      * Les modèles de formulaire adaptatif créés sous /apps ou /conf à l’aide de l’éditeur de modèles AEM.
   * Migrez les services de configuration cloud d’AEM Forms pour exploiter le nouveau paradigme de service cloud contextuel comprenant l’interface utilisateur tactile (sous /conf). Lorsque vous migrez les services de configuration cloud d’AEM Forms, les services cloud dans /etc sont déplacés vers /conf. Si vous ne disposez d’aucune personnalisation des services de cloud qui dépend des chemins hérités (/etc), il est recommandé d’exécuter l’utilitaire de migration juste après la mise à niveau vers la version 6.5 et d’utiliser l’interface utilisateur tactile de configuration de cloud pour toute autre tâche. Si vous disposez déjà de personnalisations de services cloud, continuez à utiliser l’interface utilisateur classique dans la configuration mise à niveau jusqu’à ce que les personnalisations soient mises à jour et concordent avec les chemins migrés (/conf), puis exécutez l’utilitaire de migration.

   To migrate **AEM Forms cloud services**, which include the following, tap AEM Forms Cloud Configuration Migration (cloud config migration is independent of AEMFD Compatibility package), tap AEM Forms Cloud Configurations Migration and then on the Configuration Migration page, tap **Start Migration**:

   * Services cloud du modèle de données de formulaire

      * Chemin d’accès source : /etc/cloudservices/fdm
      * Chemin d’accès cible : /conf/global/settings/cloudconfigs/fdm
   * Recaptcha

      * Chemin d’accès source : /etc/cloudservices/recaptcha
      * Chemin d’accès cible : /conf/global/settings/cloudconfigs/recaptcha
   * Adobe Sign

      * Chemin d’accès source : /etc/cloudservices/echosign
      * Chemin d’accès cible : /conf/global/settings/cloudconfigs/echosign
   * Services cloud typekit

      * Chemin d’accès source : /etc/cloudservices/typekit
      * Chemin d’accès cible : /conf/global/settings/cloudconfigs/typekit

   La fenêtre du navigateur affiche les éléments suivants pendant le processus de migration :

   * Lorsque les actifs sont mis à jour : mise à jour des actifs effectuée avec succès.
   * Une fois la migration terminée : migration des actifs terminée.

   Lorsqu’il est exécuté, l’utilitaire de migration effectue les opérations suivantes :

   * **Ajoute les balises aux actifs** : ajoute la balise « Correspondence Management : actifs migrés » / « Formulaires adaptatifs : actifs migrés » aux actifs migrés, afin que les utilisateurs puissent identifier les actifs migrés. Lorsque vous exécutez l’utilitaire de migration, tous les actifs existants du système sont marqués comme migrés.
   * **Génération des balises** : les catégories et les sous-catégories présentes dans le système précédent sont créées sous forme de balises et ces balises sont associées aux actifs appropriés de Correspondence Management dans AEM. Par exemple, une catégorie (Réclamations) et une sous-catégorie (Réclamations) d’un modèle de lettre sont générées sous forme de balises.

















1. Une fois l’utilitaire de migration en cours d’exécution, passez aux [ tâches de maintenance](#housekeepingtasks).

### Tâches de maintenance après l’exécution de l’utilitaire de migration {#housekeepingtasks}

Après avoir exécuté l’utilitaire de migration, effectuez les tâches de gestion interne suivantes :[](../../forms/using/import-export-forms-templates.md)

1. Assurez-vous que la version XFA des mises en page et des mises en page de fragments est 3.3 ou ultérieure. Si vous utilisez des mises en page et des mises en page de fragments d’une version antérieure, il se peut que le rendu de la lettre pose problème. Pour mettre à jour une version d’un XFA plus ancien vers la dernière version, procédez comme suit :

   1. [Téléchargez XFA sous la forme d’un fichier zip](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) depuis l’interface utilisateur de Forms.
   1. Extrayez le fichier.
   1. Ouvrez le fichier XFA dans la dernière version de Designer et enregistrez-le. La version de XFA est mise à jour vers la version la plus récente.
   1. Téléchargez le fichier XFA dans l’interface utilisateur de Forms.

1. Publiez tous les actifs qui ont été publiés dans le système précédent avant migration. L’utilitaire de migration met à jour les actifs uniquement dans l’instance d’auteur. Pour mettre à jour les actifs dans la ou les instances de publication, vous devez les publier.
1. Dans AEM Forms 6.4 et 6.5, certains droits des groupes d’utilisateurs de formulaires sont modifiés. Si vous souhaitez que vos utilisateurs puissent charger des fichiers XDP et des formulaires adaptatifs contenant des scripts ou utiliser un éditeur de code, vous devez les ajouter au groupe forms-power-users. De même, le groupe template-authors ne peut plus utiliser l’éditeur de code dans l’éditeur de règles. Pour que les utilisateurs puissent utiliser l’éditeur de code, ajoutez-les au groupe af-template-script-writers. For instructions on adding users to groups, see [Managing Users and User Groups](/help/communities/users.md).

