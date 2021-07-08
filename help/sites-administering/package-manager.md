---
title: Utilisation des modules
seo-title: Utilisation des modules
description: Découvrez les notions fondamentales de l’utilisation des modules dans AEM.
seo-description: Découvrez les notions fondamentales de l’utilisation des modules dans AEM.
uuid: cba76a5f-5d75-4d63-a0f4-44c13fa1baf2
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 6694a135-d1e1-4afb-9f5b-23991ee70eee
docset: aem65
exl-id: e8929d7c-9920-4c02-95a9-6f7f7a365203
source-git-commit: 4a2a9f177049e8199662ed94cf7aace9aa937655
workflow-type: tm+mt
source-wordcount: '3964'
ht-degree: 80%

---

# Utilisation des modules{#how-to-work-with-packages}

Les modules permettent d’importer et d’exporter le contenu du référentiel. Par exemple, vous pouvez utiliser des modules pour installer une nouvelle fonctionnalité, transférer du contenu entre des instances et sauvegarder le contenu d’un référentiel.

Les modules sont accessibles et/ou conservés à partir des pages suivantes :

* [Gestionnaire de modules](#package-manager), que vous utilisez pour gérer les modules dans l’instance locale d’AEM.

* [Distribution logicielle](#software-distribution), un serveur centralisé contenant à la fois des packages disponibles publiquement et des packages privés pour votre entreprise. Les modules publics peuvent contenir des correctifs, des nouvelles fonctionnalités, des documents, etc.

Vous pouvez transférer des modules entre Package Manager, Distribution logicielle et votre système de fichiers.

## Que sont les modules ? {#what-are-packages}

Un module est un fichier ZIP contenant le contenu d’un référentiel sous forme de sérialisation de système de fichiers (appelé sérialisation « coffre-fort »). Il offre une représentation facile à utiliser et à modifier des fichiers et des dossiers.

Les modules comportent du contenu, du contenu du page et du contenu lié au projet, sélectionnés à l’aide de filtres.

Un module contient également les méta-informations du coffre-fort, dont les définitions des filtres et les informations de configuration de l’importation. D’autres propriétés de contenu (qui ne sont pas utilisées pour l’extraction de package) peuvent être incluses dans le package, telles qu’une description, une image visuelle ou une icône ; ces propriétés sont destinées au consommateur du module de contenu et à titre d’information uniquement.

>[!NOTE]
>
>Les modules représentent la version actuelle du contenu au moment où le module est créé. Ils n’incluent pas les versions précédentes du contenu qu’AEM conserve dans le référentiel.

Vous pouvez effectuer les actions ci-dessous sur des modules ou avec des modules :

* Créer des modules, en définissant leurs paramètres et les filtres, au besoin
* Prévisualiser le contenu des modules (avant la création)
* Créer des modules
* Afficher les informations des modules
* Afficher le contenu des modules (après la création)
* Modifier la définition des modules existants
* Recréer des modules existants
* Réencapsuler des modules
* Télécharger des modules d’AEM vers le système de fichiers
* Charger des modules de votre système de fichiers dans votre instance d’AEM locale
* Valider le contenu du module avant l’installation
* Exécution d’une installation d’exécution d’essai
* Installer des modules (AEM n’installe pas automatiquement les modules après le chargement)
* Supprimer des modules
* Télécharger des modules, tels que des correctifs, depuis la bibliothèque Distribution logicielle
* Chargement de modules dans la section interne à l’entreprise de la bibliothèque de distribution de logiciels

## Informations sur les modules {#package-information}

Une définition de module comprend différents types d’informations :

* [Paramètres du module](#package-settings)
* [Filtres de module](#package-filters)
* [Captures d’écran de module](#package-screenshots)
* [Icônes de module](#package-icons)

### Paramètres du module {#package-settings}

Vous pouvez modifier différents paramètres du module pour définir certains aspects comme la description des modules, les bogues associés, les dépendances et les informations sur le fournisseur.

La boîte de dialogue **Paramètres du module** est accessible à l’aide du bouton **Modifier** lors de la [création](#creating-a-new-package) ou de la [modification](#viewing-and-editing-package-information) d’un module. Elle contient trois onglets pour la configuration. Après avoir apporté des modifications, cliquez sur **OK** pour les enregistrer.

![packagesedit](assets/packagesedit.png)

| **Champ** | **Description** |
|---|---|
| Nom | Nom du module. |
| Groupe | Nom du groupe auquel ajouter le module pour l’organisation des modules. Saisissez le nom d’un nouveau groupe ou sélectionnez un groupe existant. |
| Version | Texte à utiliser pour la version personnalisée. |
| Description | Brève description du package. Des balises HTML peuvent être utilisées pour la mise en forme. |
| Miniature | Icône qui s’affiche avec la liste des packages. Cliquez sur Parcourir pour sélectionner un fichier local. |

![chlimage_1-108](assets/chlimage_1-108.png)

<table>
 <tbody>
  <tr>
   <th><strong>Champ</strong></th>
   <th><strong>Description</strong></th>
   <th><strong>Format/Exemple</strong></th>
  </tr>
  <tr>
   <td>Nom</td>
   <td>Nom du fournisseur.</td>
   <td><em>AEM Geometrixx<br /> </em></td>
  </tr>
  <tr>
   <td>URL</td>
   <td>URL du fournisseur.</td>
   <td><em>https://www.aem-geometrixx.com</em></td>
  </tr>
  <tr>
   <td>Lien</td>
   <td>Lien spécifique au module vers une page de fournisseur.</td>
   <td><em>https://www.aem-geometrixx.com/mypackage.html</em></td>
  </tr>
  <tr>
   <td>Requiert<br /> </td>
   <td>
    <ul>
     <li>Admin : sélectionnez cette option lorsque le module ne peut être installé que par un compte disposant des droits d’administrateur.</li>
     <li>Redémarrer : sélectionnez cette option lorsque le serveur doit être redémarré après l’installation du module.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Traitement AC</td>
   <td><p>Indiquez comment les informations de contrôle d’accès définies dans le module sont traitées lors de son importation :</p>
    <ul>
     <li><strong>Ignorer</strong></li>
     <li><strong>Remplacer</strong></li>
     <li><strong>Fusionner</strong></li>
     <li><strong>Effacer</strong></li>
     <li><strong>FusionnerConserver</strong></li>
    </ul> <p>La valeur par défaut est <strong>Ignorer</strong>.</p> </td>
   <td>
    <ul>
     <li><strong>Ignorer</strong> - conserver les listes ACL dans le référentiel</li>
     <li><strong>Remplacer</strong> - remplacer les listes ACL dans le référentiel</li>
     <li><strong>Fusionner</strong> - fusionner les deux ensembles de listes ACL</li>
     <li><strong>Effacer</strong> - effacer les listes ACL</li>
     <li><strong>FusionnerConserver</strong> - fusionner le contrôle d’accès dans le contenu avec celui fourni avec le module en ajoutant les entrées de contrôle d’accès des entités non présentes dans le contenu</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

![packagesdependencies](assets/packagesdependencies.png)

| **Champ** | **Description** | **Format/Exemple** |
|---|---|---|
| Testé avec | Le nom et la version du produit auxquels ce module est ciblé ou est compatible. | *AEM 6* |
| Correction de bogues/problèmes | Un champ de texte vous permettant de répertorier les détails des bogues corrigés avec ce module. Répertoriez chaque bogue sur une ligne distincte. | bug-nr summary |
| Dépend de | Répertorie les informations de dépendance qui doivent être respectées lorsque d’autres modules sont nécessaires pour que le module actuel s’exécute comme prévu. Ce champ est important lorsque vous utilisez des correctifs. | groupId:name:version |
| Remplace | Liste des packages obsolètes que ce package remplace. Avant de procéder à l’installation, assurez-vous que ce module contient tout le contenu nécessaire des modules obsolètes afin qu’aucun contenu ne soit remplacé. | groupId:name:version |

### Filtres de module {#package-filters}

Les filtres identifient les nœuds du référentiel à inclure dans le module. Une **Définition de filtre** spécifie les informations suivantes :

* **Chemin d’accès racine** du contenu à inclure.
* **** Règles qui incluent ou excluent des noeuds spécifiques sous le chemin racine.

Les filtres peuvent ne comporter aucune règle ou en comporter plusieurs. Lorsqu’aucune règle n’est définie, le module contient tout le contenu sous le chemin d’accès racine.

Vous pouvez définir une ou plusieurs définitions de filtre pour un module. Utilisez plusieurs filtres pour inclure le contenu de plusieurs chemins racine.

![chlimage_1-109](assets/chlimage_1-109.png)

Le tableau ci-dessous décrit ces règles et fournit des exemples :

<table>
 <tbody>
  <tr>
   <th> Type de règle</th>
   <th>Description </th>
   <th>Exemple </th>
  </tr>
  <tr>
   <td> inclusion</td>
   <td>Vous pouvez définir un chemin ou utiliser une expression régulière pour spécifier tous les nœuds à inclure.<br /> <br /> L’inclusion d’un répertoire :
    <ul>
     <li>inclura ce répertoire <i>et</i> tous les fichiers et dossiers de ce répertoire (c’est-à-dire la sous-arborescence complète)</li>
     <li><strong>n’inclura pas</strong> d’autres fichiers ou dossiers sous le chemin d’accès racine spécifié</li>
    </ul> </td>
   <td>/libs/sling/install(/.*)? </td>
  </tr>
  <tr>
   <td> exclusion</td>
   <td>Vous pouvez spécifier un chemin d’accès ou utiliser une expression régulière afin de spécifier tous les nœuds à exclure.<br /> <br /> L’exclusion d’un répertoire exclut le répertoire en question et l’ensemble des fichiers <i>et</i> des dossiers de ce répertoire (c’est-à-dire la sous-arborescence entière).<br /> </td>
   <td>/libs/wcm/foundation/components(/.*)?</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Un module peut contenir plusieurs définitions de filtre de manière à pouvoir combiner des nœuds de différents emplacements en un seul module.

Les filtres de module sont le plus souvent définis lorsque vous [créez le module](#creating-a-new-package), mais ils peuvent également être modifiés par la suite (après quoi le module doit être recréé).

### Captures d’écran de module {#package-screenshots}

Vous pouvez associer des captures d’écran au module afin de fournir une représentation visuelle du contenu, par exemple, en fournissant des captures d’écran de la nouvelle fonctionnalité.

### Icônes de module {#package-icons}

Vous pouvez également associer une icône au module afin de fournir une représentation visuelle de référence rapide du contenu du module. Elle est ensuite affichée dans la liste de modules et peut vous aider à identifier facilement le module ou la classe du module.

Dans la mesure où un module peut contenir une icône, les modules officiels suivent les conventions ci-dessous :

>[!NOTE]
>
>Pour éviter toute confusion, utilisez une icône descriptive pour le module et n’utilisez pas l’une des icônes officielles.

Module de correctif officiel :

![](do-not-localize/chlimage_1-28.png)

Module d’installation ou d’extension d’AEM officiel :

Feature Packs officiels :

![](do-not-localize/chlimage_1-29.png)

## Gestionnaire de modules {#package-manager}

Le Gestionnaire de modules gère les modules dans l’installation locale d’AEM. Après avoir [affecté les autorisations nécessaires](#permissions-needed-for-using-the-package-manager), vous pouvez utiliser le Gestionnaire de modules pour différentes actions, dont la configuration, la création, le téléchargement et l’installation des modules. Les principaux éléments à configurer sont les suivants :

* [Paramètres du module](#package-settings)
* [Filtres de module](#package-filters)

### Autorisations nécessaires à l’utilisation du Gestionnaire de modules {#permissions-needed-for-using-the-package-manager}

Pour accorder aux utilisateurs le droit de créer, de modifier, de charger et d’installer des modules, vous devez leur affecter les autorisations appropriées aux emplacements suivants :

* **/etc/packages (tous les droits à l’exception des droits de suppression)**
* nœud contenant le contenu du module

>[!CAUTION]
>
>L’octroi d’autorisations sur les packages peut entraîner une divulgation des informations sensibles et une perte de données.
>
>Pour limiter ces risques, il est vivement recommandé d’accorder uniquement des autorisations de groupe spécifiques sur des sous-arborescences dédiées, par exemple `/etc/packages/site-content`.

Pour plus d’informations sur la modification des autorisations, voir [Définition des autorisations](/help/sites-administering/security.md#setting-page-permissions).

### Création d’un module {#creating-a-new-package}

Pour créer une définition de module :

1. Dans l’écran d’accueil d’AEM, cliquez sur **Packages** (ou dans la console **Outils**, double-cliquez sur **Packages**).

1. Ensuite, sélectionnez **Gestionnaire de modules**.
1. Cliquez sur **Créer un package**.

   >[!NOTE]
   >
   >Si l’instance comporte de nombreux modules, il peut y avoir une arborescence en place afin de pouvoir accéder au dossier cible nécessaire avant de créer le module.

1. Dans la boîte de dialogue :

   ![packagesnew](assets/packagesnew.png)

   Renseignez les champs :

   * **Nom du groupe**

      Nom du groupe cible (ou dossier). Les groupes vous aident à organiser vos modules.

       Si le dossier n’existe pas encore, il est créé pour le groupe. Si vous ne renseignez pas le nom du groupe, le module est créé dans la liste de modules principale (Accueil > Modules).

   * **Nom du module**

      Le nom de votre nouveau package. Sélectionnez un nom explicite pour vous aider (entre autres) à identifier facilement le contenu du module.

   * **Version**

       Champ de texte permettant d’indiquer une version. Il sera ajouté au nom du module pour former le nom du fichier ZIP.
   Cliquez sur **OK** pour créer le module.

1. AEM répertorie le nouveau module dans le dossier de groupe approprié.

   ![packagesitem](assets/packagesitem.png)

   Cliquez sur l’icône ou le nom du module à ouvrir.

   ![packagesitemclicked](assets/packagesitemclicked.png)

   >[!NOTE]
   >
   >Vous pouvez revenir sur cette page ultérieurement, si nécessaire.

1. Cliquez sur **Modifier** pour modifier les paramètres du module [.](#package-settings)

   Ici, vous pouvez ajouter des informations et/ou définir certains paramètres, par exemple, une description, l’[icône](#package-icons), les bogues associés et ajouter des informations sur le fournisseur.

   Une fois que vous avez fini de modifier les paramètres, cliquez sur **OK**.

1. Ajoutez des **[captures d’écran](#package-screenshots)** au module, au besoin. Une seule instance est disponible lorsque le module est créé. Ajoutez-en davantage, si nécessaire, à l’aide de **Captures d’écran de module** à partir du Sidekick.

   Ajoutez l’image réelle en double-cliquant sur le composant Image dans la zone **Captures d’écran**, en ajoutant une image et en cliquant sur **OK**.

1. Définissez les **[filtres de module](#package-filters)** en faisant glisser des instances de la **définition de filtre** à partir du Sidekick, puis en double-cliquant pour l’ouvrir pour le modifier :

   ![packagesfilter](assets/packagesfilter.png)

   Précisez les paramètres suivants :

   * **Chemin d’accès racine** Contenu à grouper. Il peut s’agir de la racine d’une sous-arborescence.
   * **Règles** Les règles sont facultatives. Pour des définitions de module simples, il n’est pas nécessaire de spécifier de règles d’inclusion ou d’exclusion.

       Si nécessaire, vous pouvez définir des règles d’[**inclusion** ou d’**exclusion** ](#package-filters)afin de définir précisément le contenu d’un module.

       Ajoutez des règles à l’aide du symbole **+**. Vous pouvez également supprimer des règles à l’aide du symbole **-**. Les règles sont appliquées selon leur ordre, donc positionnez-les dans l’ordre de votre choix à l’aide des touches **haut** et **bas**.
   Ensuite, cliquez sur **OK** pour enregistrer le filtre.

   >[!NOTE]
   >
   >Vous pouvez utiliser autant de définitions de filtre que nécessaire, mais vous devez veiller à ce qu’elles n’entrent pas en conflit. Utilisez **Aperçu** pour confirmer le contenu du module.

1. Pour confirmer le contenu du module, vous pouvez utiliser **Aperçu**. Une exécution d’essai du processus de création est effectuée, et tout ce qui sera ajouté au module lors de sa création effective est répertorié.
1. Vous pouvez maintenant [créer](#building-a-package) votre module.

   >[!NOTE]
   >
   >Vous n’êtes pas tenu de créer le module à ce stade. Vous pouvez le faire ultérieurement.

### Création d’un module {#building-a-package}

Un module est souvent créé au moment où vous [créez la définition du module](#creating-a-new-package), mais vous pouvez y revenir ultérieurement pour créer ou recréer le module. Cela peut s’avérer utile si le contenu du référentiel a changé.

>[!NOTE]
>
>Avant de créer le module, il peut s’avérer utile de prévisualiser son contenu. Pour ce faire, cliquez sur **Aperçu**.

1. Ouvrez la définition de module à partir du **Gestionnaire de modules** (cliquez sur l’icône de module ou le nom du module).

1. Cliquez sur **Créer**. Une boîte de dialogue vous demande de confirmer que vous souhaitez créer le module.

   >[!NOTE]
   >
   >Cela a une importance particulière lorsque vous recréez un module, car le contenu du module est remplacé.

1. Cliquez sur **OK**. AEM crée le module, en répertoriant tout le contenu ajouté au module. Une fois l’opération terminée, AEM affiche un message de confirmation indiquant que le module a été créé et (lorsque vous fermez la boîte de dialogue) met à jour les informations de la liste de modules.

### Réencapsulation d’un module {#rewrapping-a-package}

Une fois qu’un module a été créé, il peut être réencapsulé, si nécessaire.

La réencapsulation modifie les informations du module, *sans* modifier le contenu du module. Les informations du module sont la vignette, la description, etc., en d’autres termes tous les paramètres que vous pouvez modifier dans la boîte de dialogue **Paramètres du module** (pour l’ouvrir, cliquez sur **Modifier**).

Un cas d’utilisation majeur pour le réencapsulage est lors de la préparation d’un module. Par exemple, vous pouvez avoir un module existant et décider de le partager avec d’autres personnes. À cet effet, vous souhaitez ajouter une vignette et une description. Au lieu de recréer le module entier avec toutes ses fonctionnalités (ce qui peut prendre un certain temps et vous expose au risque que le module ne soit plus identique à l’original), vous pouvez le réencapsuler et ajouter simplement la vignette et la description.

1. Ouvrez la définition de module à partir du **Gestionnaire de modules** (cliquez sur l’icône de module ou le nom du module).

1. Cliquez sur **Modifier** et mettez à jour **[Paramètres du module](#package-settings)**, au besoin. Cliquez sur **OK** pour enregistrer.

1. Cliquez sur **Réencapsuler**. Une boîte de dialogue de confirmation s’affiche.

### Affichage et modification des informations de module {#viewing-and-editing-package-information}

Pour afficher ou modifier des informations sur une définition de module :

1. Dans le Gestionnaire de modules, accédez au module à afficher.
1. Cliquez sur l’icône de module du module à afficher. Cette action affiche la page du module qui répertorie les informations sur la définition du module:

   ![packagesitemclicked-1](assets/packagesitemclicked-1.png)

   >[!NOTE]
   >
   >À partir de cette page, vous pouvez également modifier et effectuer certaines opérations sur le module.
   >
   >Les boutons disponibles varient selon que le module a été créé ou non.

1. Si le module a déjà été créé, cliquez sur **Contenu**. Une fenêtre qui répertorie tout le contenu du module s’affiche :

### Affichage du contenu du module et test de l’installation {#viewing-package-contents-and-testing-installation}

Une fois un module créé, vous pouvez afficher son contenu :

1. Dans le Gestionnaire de modules, accédez au module à afficher.
1. Cliquez sur l’icône de module du module à afficher. Cette action affiche la page du module qui répertorie les informations sur la définition du module.

1. Pour afficher le contenu, cliquez sur **Contenu**. Une fenêtre qui répertorie tout le contenu du module s’affiche :

   ![packgescontents](assets/packgescontents.png)

1. Pour effectuer une exécution d’essai de l’installation, cliquez sur **Tester l’installation**. Une fois que vous avez confirmé l’action, une fenêtre qui répertorie les résultats comme si la configuration avait été effectuée s’affiche :

   ![packagestestinstall](assets/packagestestinstall.png)

### Téléchargement des modules sur votre système de fichiers {#downloading-packages-to-your-file-system}

Cette section décrit comment télécharger un module d’AEM vers votre système de fichiers à l’aide du **Gestionnaire de modules**.

1. Dans l’écran de bienvenue d’AEM, cliquez sur **Packages**, puis sélectionnez **Gestionnaire de modules**.
1. Accédez au module à télécharger.

   ![packagesdownload](assets/packagesdownload.png)

1. Cliquez sur le lien formé par le nom du fichier ZIP (souligné) pour le module à télécharger, par exemple, `export-for-offline.zip`.

   AEM télécharge le module sur votre ordinateur (à l’aide d’une boîte de dialogue de téléchargement de navigateur standard).

### Chargement des modules à partir du système de fichiers {#uploading-packages-from-your-file-system}

Un chargement de package vous permet de charger un package de votre système de fichiers dans AEM Package Manager.
Pour charger un module :

1. Accédez au **Gestionnaire de modules**. Accédez ensuite au dossier du groupe dans lequel vous souhaitez charger le module.

   ![packagesuploadbutton](assets/packagesuploadbutton.png)

1. Cliquez sur **Upload Package** (Télécharger le package).

   ![packagesuploaddialog](assets/packagesuploaddialog.png)

   * **File**

      Vous pouvez saisir directement le nom du fichier ou utiliser la commande **Parcourir...** pour sélectionner le module requis dans votre système de fichiers local (après la sélection, cliquez sur **OK**).

   * **Forcer le chargement**

      Si un package portant ce nom existe déjà, vous pouvez cliquer dessus pour forcer le téléchargement (et remplacer le package existant).
   Cliquez sur **OK** afin que le nouveau module soit chargé et répertorié dans la liste Gestionnaire de modules.

   >[!NOTE]
   >
   >Pour mettre le contenu à disposition dans AEM, veillez à [installer le module](#installing-packages).

### Validation de modules {#validating-packages}

Avant d’installer un module, vous pouvez vérifier son contenu. Comme les packages peuvent modifier des fichiers superposés sous `/apps` et/ou ajouter, modifier et supprimer des listes de contrôle d’accès, il est souvent utile de valider ces modifications avant l’installation.

#### Options de validation {#validation-options}

Le mécanisme de validation permet de vérifier les caractéristiques suivantes du module :

* Importations de modules OSGi
* Recouvrements
* Listes ACL

Ces options sont détaillées ci-dessous.

* **Valider les importations de modules OSGi**

   **Éléments vérifiés**

   Cette option de validation inspecte le module afin de vérifier tous les fichiers JAR (lots OSGi), extrait leur fichier `manifest.xml` (qui contient les dépendances de version sur lesquelles repose le lot OSGi) et vérifie que l’instance AEM exporte les dépendances avec les versions correctes.

   **Comment sont-ils signalés ?**

   Toutes les dépendances versionnées qui ne peuvent pas être satisfaites par l’instance AEM sont répertoriées dans le **Journal d’activité** du gestionnaire de modules.

   **États d’erreur**

   Si les dépendances ne sont pas satisfaites, les lots OSGi du module avec ces dépendances ne démarrent pas. Cela entraîne un déploiement d’application interrompu, puisque tout ce qui repose sur le lot OSGi non démarré ne fonctionnera pas correctement.

   **Résolution d’erreurs**

   Pour résoudre des erreurs dues à des lots OSGi non satisfaits, il faut ajuster la version dépendante du lot avec des importations non satisfaites.

* **Valider les recouvrements**

   **Éléments vérifiés**

   Cette validation détermine si le module en cours d’installation contient un fichier déjà recouvert dans l’instance AEM de destination.

   Par exemple, étant donné qu’une superposition existante se trouve à `/apps/sling/servlet/errorhandler/404.jsp`, un module contenant `/libs/sling/servlet/errorhandler/404.jsp`, de sorte qu’il modifie le fichier existant à `/libs/sling/servlet/errorhandler/404.jsp`.

   **Comment sont-ils signalés ?**

   Ces recouvrements sont décrits dans le **Journal d’activités** du Gestionnaire de modules.

   **États d’erreur**

   Un état d’erreur signifie que le module tente de déployer un fichier déjà recouvert. Les modifications du module seront donc remplacées (et donc masquées) par le recouvrement et ne prendront pas effet.

   **Résolution d’erreurs**

   Pour résoudre ce problème, le responsable de l’ du fichier de recouvrement dans `/apps` doit examiner les modifications apportées au fichier recouvert dans `/libs` et incorporer les modifications nécessaires dans le recouvrement ( `/apps`), puis redéployer le fichier recouvert.

   >[!NOTE]
   >
   >Notez que le mécanisme de validation ne permet pas de réconcilier si le contenu superposé a été correctement incorporé dans le fichier de recouvrement. Par conséquent, cette validation continuera à signaler des conflits même après que les modifications nécessaires auront été apportées.

* **Valider les listes ACL**

   **Éléments vérifiés**

   Cette validation vérifie quelles autorisations sont ajoutées, comment elles seront gérées (fusion/remplacement) et si les autorisations actuelles seront affectées.

   **Comment sont-ils signalés ?**

   Les autorisations sont décrites dans le **Journal d’activités** du Gestionnaire de modules.

   **États d’erreur**

   Aucune erreur explicite ne peut être fournie. La validation indique simplement si de nouvelles autorisations des listes ACL seront ajoutées ou affectées par l’installation du module.

   **Résolution d’erreurs**

   Grâce aux informations fournies par la validation, les nœuds affectés peuvent être révisés dans CRXDE et les listes ACL peuvent être ajustées dans le module si besoin.

   >[!CAUTION]
   >
   >Il est recommandé que les modules n’affectent pas les listes ACL fournies par AEM, car cela pourrait entraîner un comportement inattendu du produit.

#### Validation {#performing-validation}

La validation des modules peut être effectuée de deux manières différentes :

* via l’interface utilisateur du Gestionnaire de modules ;
* via une requête HTTP POST, telle que cURL.

>[!NOTE]
>
>La validation doit toujours avoir lieu après le chargement du module, mais avant son installation.

**Validation de modules via le Gestionnaire de modules**

1. Ouvrez le gestionnaire de modules à l’adresse `https://<server>:<port>/crx/packmgr`
1. Sélectionnez le package dans la liste, puis sélectionnez la liste déroulante **Plus** dans l’en-tête, puis **Valider** dans le menu déroulant.

   >[!NOTE]
   >
   >Cette opération doit être effectuée après le chargement du module de contenu, mais avant son installation.

1. Dans la boîte de dialogue modale qui s’affiche alors, utilisez les cases à cocher pour sélectionner le ou les types de validation et commencez la validation en cliquant sur **Valider**. Vous pouvez également cliquer sur **Annuler**.

1. La ou les validations sélectionnées sont ensuite réalisées. Les résultats sont affichés dans le Journal d’activités du Gestionnaire de modules.

**Validation de modules via une requête HTTP POST**

La requête POST se présente comme suit.

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

>[!NOTE]
>
>Le paramètre `type` peut être n’importe quelle liste non triée séparée par des virgules qui comprend :
>
>* `osgiPackageImports`
>* `overlays`
>* `acls`

>
>
La valeur de `type` est définie par défaut sur `osgiPackageImports` si elle n’est pas transmise.

Voici un exemple illustrant comment exécuter la validation d’un module à l’aide de cURL.

1. Si vous utilisez cURL, exécutez une instruction semblable à celle-ci :

   ```shell
   curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
   ```

1. La validation demandée est exécutée et la réponse est renvoyée sous forme d’objet JSON.

>[!NOTE]
>
>La réponse à une requête de validation HTTP POST sera un objet JSON avec les résultats de la validation.

### Installation des modules {#installing-packages}

Après avoir chargé un module, vous devez installer le contenu. Pour que le contenu du module soit installé et opérationnel, il doit être :

* chargé dans AEM (soit [chargé à partir de votre système de fichiers](#uploading-packages-from-your-file-system) soit téléchargé à partir de [Distribution logicielle](#software-distribution)).

* installé.

>[!CAUTION]
>
>L’installation d’un module peut remplacer ou supprimer le contenu existant. Ne chargez un module que si vous êtes sûr qu’il ne supprime ou ne remplace pas du contenu dont vous avez besoin.
>
>Pour afficher le contenu ou l’impact d’un module, vous pouvez :
>
>* Effectuez un test d&#39;installation du package sans modifier le contenu :
   >  Ouvrez le package (cliquez sur l’icône ou le nom du package) et cliquez sur **Tester l’installation**.
   >
   >
* Consultez la liste des contenus de package :
   >  Ouvrez le package et cliquez sur **Contenu**.

>



>[!NOTE]
>
>Juste avant l’installation du module, un module d’instantané est créé pour contenir le contenu qui va être remplacé.
>
>Cet instantané est réinstallé lorsque vous désinstallez le module.

>[!CAUTION]
>
>Si vous installez des ressources numériques, vous devez effectuer les opérations suivantes :
>
>* Tout d’abord, désactivez WorkflowLauncher.
   >  Utilisez l’option de menu Composants de la console OSGi pour désactiver `com.day.cq.workflow.launcher.impl.WorkflowLauncherImpl`.
   >
   >
* Ensuite, une fois l’installation terminée, réactivez WorkflowLauncher.
>
>
La désactivation de WorkflowLauncher permet de s’assurer que la structure d’importation d’actifs ne manipule pas (involontairement) les actifs lors de l’installation.

1. Dans le Gestionnaire de modules, accédez au module à installer.

   Un bouton **Installer** s’affiche à côté des modules qui n’ont pas encore été installés.

   >[!NOTE]
   >
   >Vous pouvez également ouvrir le module en cliquant sur l’icône associée pour accéder au bouton **Installer**.

1. Pour commencer l’installation, cliquez sur **Installer**. Une boîte de dialogue vous invite à confirmer et répertorie toutes les modifications apportées. Lorsque vous avez terminé, cliquez sur **Fermer** dans la boîte de dialogue.

   Le mot **Installé** s’affiche en regard du module une fois qu’il a été installé.

### Chargement et installation basés sur le système de fichiers {#file-system-based-upload-and-installation}

Il existe une autre façon de charger et d’installer des modules sur votre instance. Dans votre système de fichiers, un dossier `crx-quicksart` avec votre fichier JAR et le fichier `license.properties`. Vous devez créer un dossier nommé `install` sous `crx-quickstart`. Vous aurez alors quelque chose comme ceci : `<aem_home>/crx-quickstart/install`

Dans ce dossier d’installation, vous pouvez ajouter directement des modules. Ils sont chargés et installés automatiquement sur votre instance. Une fois l’opération terminée, vous pouvez afficher les modules dans le Gestionnaire de modules.

Si votre instance est en cours d’exécution, l’ajout d’un module au dossier `install` lance directement le chargement et l’installation sur l’instance. Si votre instance n’est pas en cours d’exécution, les modules que vous placez dans le dossier `install` sont installés au démarrage dans l’ordre alphabétique.

>[!NOTE]
>
>Vous pouvez également effectuer cette opération avant de démarrer l’instance pour la première fois. À cet effet, vous devez créer manuellement le dossier `crx-quickstart`, créer le dossier `install` en dessous et y placer les modules. Lorsque vous lancez votre instance pour la première fois, les modules sont installés dans l’ordre alphabétique.

### Désinstallation des modules {#uninstalling-packages}

AEM vous permet de désinstaller des packages. Cette action renvoie le contenu concerné du référentiel vers l’instantané enregistré juste avant l’installation des modules.

>[!NOTE]
>
>Lors de l’installation, un module d’instantané contenant le contenu qui va être remplacé est créé.
>
>Ce module est réinstallé lorsque vous désinstallez le module.

1. Dans le Gestionnaire de modules, accédez au module à désinstaller.
1. Cliquez sur l’icône de module du module à désinstaller.
1. Pour supprimer le contenu de ce module du référentiel, cliquez sur **Désinstaller**. Une boîte de dialogue vous invite à confirmer et répertorie toutes les modifications apportées. Lorsque vous avez terminé, cliquez sur **Fermer** dans la boîte de dialogue.

### Suppression des modules {#deleting-packages}

Pour supprimer un module dans les listes du Gestionnaire de modules :

>[!NOTE]
>
>Les fichiers/nœuds installés du module ne sont **pas** supprimés.

1. Dans la console **Outils**, développez le dossier **Packages** pour afficher votre package dans le volet de droite.

1. Cliquez sur le module à supprimer afin de le sélectionner, puis :

   * Cliquez sur **Supprimer** dans le menu de la barre d’outils.
   * Cliquez avec le bouton droit de la souris et sélectionnez **Supprimer**.

   ![packagesdelete](assets/packagesdelete.png)

1. AEM demande de confirmation que vous souhaitez supprimer le module. Cliquez sur **OK** pour confirmer la suppression.

>[!CAUTION]
>
>Si ce module a déjà été installé, le contenu *installé* n’est **pas** supprimé.

### Réplication des modules {#replicating-packages}

Répliquez le contenu d’un module afin de l’installer dans l’instance de publication :

1. Dans le **Gestionnaire de modules**, accédez au module à répliquer.

1. Cliquez sur l’icône de module ou le nom du module à répliquer pour le développer.
1. Dans le menu déroulant **Plus** de la barre d’outils, sélectionnez **Répliquer**.

## Partage de modules {#package-share}

Le partage de modules était un serveur centralisé, rendu public, permettant de partager des modules de contenu.

Il a été remplacé par [Distribution logicielle](#software-distribution).

## Distribution logicielle {#software-distribution}

[La ](https://downloads.experiencecloud.adobe.com) distribution logicielle est la nouvelle interface utilisateur conçue pour simplifier la recherche et le téléchargement des packages AEM.

Pour plus d’informations, consultez la [documentation Distribution logicielle](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html).

>[!CAUTION]
>
>AEM gestionnaire de packages n’est pas utilisable avec Distribution logicielle pour l’instant, vous téléchargez vos packages sur votre disque local.
