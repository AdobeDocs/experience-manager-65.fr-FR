---
title: Gestionnaire de modules
description: Découvrez les principes de base de la gestion des packages d’AEM avec Package Manager.
feature: Administering
role: Admin
uuid: cba76a5f-5d75-4d63-a0f4-44c13fa1baf2
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 6694a135-d1e1-4afb-9f5b-23991ee70eee
docset: aem65
exl-id: e8929d7c-9920-4c02-95a9-6f7f7a365203
source-git-commit: de58ba638c22b7148e1349417d1f514c26c5887e
workflow-type: tm+mt
source-wordcount: '3525'
ht-degree: 18%

---


# Gestionnaire de modules {#working-with-packages}

Les modules permettent d’importer et d’exporter le contenu du référentiel. Vous pouvez utiliser des packages pour installer un nouveau contenu, installer de nouvelles fonctionnalités, transférer du contenu entre les instances et sauvegarder le contenu du référentiel.

À l’aide de Package Manager, vous pouvez transférer des modules entre votre instance AEM et votre système de fichiers local à des fins de développement.

## Que sont les modules ? {#what-are-packages}

Un package est un fichier zip contenant du contenu de référentiel dans un formulaire de sérialisation de système de fichiers, appelé sérialisation par coffre, fournissant une représentation facile à utiliser et à modifier des fichiers et des dossiers. Le contenu inclus dans le package est défini à l’aide de filtres.

Un module contient également les méta-informations du coffre-fort, dont les définitions des filtres et les informations de configuration de l’importation. D’autres propriétés de contenu, qui ne sont pas utilisées pour l’extraction de package, peuvent être incluses dans le package, telles qu’une description, une image visuelle ou une icône. Ces propriétés de contenu supplémentaires sont destinées au consommateur de module de contenu et à titre d’information uniquement.

>[!NOTE]
>
>Les modules représentent la version actuelle du contenu au moment où le module est créé. Ils n’incluent pas les versions précédentes du contenu qu’AEM conserve dans le référentiel.

## Gestionnaire de modules {#package-manager}

Package Manager gère les modules de votre installation AEM. Après avoir [attribué les autorisations nécessaires](#permissions-needed-for-using-the-package-manager) vous pouvez utiliser le gestionnaire de modules pour diverses actions, notamment la configuration, la création, le téléchargement et l’installation de vos modules.

### Autorisations requises {#required-permissions}

Pour créer, modifier, charger et installer des packages, les utilisateurs doivent disposer des autorisations appropriées sur les noeuds suivants :

* Droits complets à l’exception de la suppression sur `/etc/packages`
* Noeud contenant le contenu du package

>[!CAUTION]
>
>L’octroi d’autorisations pour les packages peut entraîner une divulgation des informations sensibles et une perte de données.
>
>Pour limiter ces risques, il est vivement recommandé d’accorder des autorisations de groupe spécifiques sur des sous-arborescences dédiées uniquement.

### Accès au gestionnaire de modules {#accessing}

Vous pouvez accéder au gestionnaire de modules de trois façons :

1. Dans le menu principal AEM -> **Outils** -> **Déploiement** -> **Packages**
1. De [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) utilisation de la barre de sélecteur supérieure
1. En accédant directement à `http://<host>:<port>/crx/packmgr/`

### Interface utilisateur de Package Manager {#ui}

Package Manager se divise en quatre principaux domaines fonctionnels :

* **Panneau de navigation gauche** - Ce panneau vous permet de filtrer et de trier la liste des packages.
* **Liste de modules** - Il s’agit de la liste des packages de votre instance filtrés et triés par sélection dans le panneau de navigation de gauche.
* **Journal d’activité** - Ce panneau est d’abord réduit et se développe pour détailler l’activité de Package Manager, comme lorsqu’un package est créé ou installé. L’onglet Journal d’activité comporte des boutons supplémentaires pour :
   * **Effacer le journal**
   * **Afficher/masquer**
* **Barre d’outils** - La barre d’outils contient des boutons d’actualisation pour le panneau de navigation de gauche et la liste de modules, ainsi que des boutons permettant de rechercher, créer et charger des modules.

![Interface utilisateur de Package Manager](assets/package-manager-ui.png)

Cliquer sur une option dans le panneau de navigation de gauche filtre immédiatement la liste de modules.

Cliquez sur le nom d’un module pour développer l’entrée dans la liste des modules afin d’afficher plus de détails sur le module.

![Détails du module étendu](assets/package-expand.png)

Plusieurs actions peuvent être effectuées sur un package via les boutons de la barre d’outils disponibles lorsque le détail du package est développé.

* [Modifier](#edit-package)
* [Compilation](#building-a-package)
* [Réinstaller](#reinstalling-packages)
* [Télécharger](#downloading-packages-to-your-file-system)
* [Partager](#share)

D’autres actions sont disponibles sous la variable **Plus** bouton .

* [Supprimer](#deleting-packages)
* [Couverture](#package-coverage)
* [Sommaire](#viewing-package-contents-and-testing-installation)
* [Réencapsuler](#rewrapping-a-package)
* [Autres versions](#other-versions)
* [Désinstaller](#uninstalling-packages)
* [Test Install](#viewing-package-contents-and-testing-installation)
* [Valider](#validating-packages)
* [Répliquer](#replicating-packages)

### État du package {#package-status}

Chaque entrée de la liste des packages comporte un indicateur d’état pour vous informer en un coup d’oeil du statut du package. Pointez sur l’état pour afficher l’info-bulle avec le détail de l’état.

![État du package](assets/package-status.png)

Si le package a été modifié ou n’a jamais été créé, l’état est présenté sous la forme d’un lien pour effectuer une action rapide afin de le recréer ou de l’installer.

## Paramètres du module {#package-settings}

Un package est essentiellement un ensemble de filtres et de données de référentiel basés sur ces filtres. À l’aide de l’interface utilisateur du gestionnaire de modules, vous pouvez cliquer sur un module, puis sur le **Modifier** pour afficher les détails d’un package, y compris les paramètres suivants.

* [Paramètres généraux](#general-settings)
* [Filtres de module](#package-filters)
* [Dépendances de modules](#package-dependencies)
* [Paramètres avancés](#advanced-settings)
* [Captures d’écran de module](#package-screenshots)

### Paramètres généraux {#general-settings}

Vous pouvez modifier divers paramètres de package pour définir des informations telles que la description du package, les dépendances et les détails du fournisseur.

Le **Paramètres du module** est disponible via la boîte de dialogue **Modifier** lorsque [création](#creating-a-new-package) ou [édition](#viewing-and-editing-package-information) un package. Une fois les modifications effectuées, cliquez sur **Enregistrer**.

![Boîte de dialogue Modifier le module, paramètres généraux](assets/general-settings.png)

| Champ | Description |
|---|---|
| Nom | Nom du module |
| Groupe | Pour organiser des modules, vous pouvez saisir le nom d’un nouveau groupe ou sélectionner un groupe existant. |
| Version | Texte à utiliser pour la version |
| Description | Brève description du module permettant le balisage de HTML pour le formatage |
| Miniature | Icône qui s’affiche avec la liste des packages |

#### Miniatures des modules {#thumbnails}

Une miniature fournit une représentation visuelle de référence rapide de ce que contient le module. Elle est ensuite affichée dans la liste des modules et peut aider à identifier facilement le module, ou la classe du module.

Voici des exemples de conventions utilisées pour les packages officiels :

Correctif officiel

![Miniature officielle du correctif](assets/official-hotfix.png)

Installation officielle de l’AEM de l’extension

![Miniature officielle de l’installation ou de l’extension AEM](assets/official-installation.png)

Service Pack officiel

![Icône du Service Pack d’AEM officiel](assets/official-service-pack.png)

Utilisez une icône unique pour votre module. Ne réutilisez pas une icône utilisée par Adobe.

### Filtres de module {#package-filters}

Les filtres identifient les nœuds du référentiel à inclure dans le module. A **Définition du filtre** indique les informations suivantes :

* **Chemin d’accès racine** du contenu à inclure
* **Règles** qui incluent ou excluent des noeuds spécifiques sous le chemin d’accès racine

Ajoutez des règles à l’aide du **+** bouton . Supprimez les règles à l’aide de la fonction **-** bouton .

Les règles sont appliquées selon leur ordre, positionnez-les selon vos besoins à l’aide de la fonction **Monter** et **Descendre** boutons fléchés.

Les filtres peuvent ne comporter aucune règle ou en comporter plusieurs. Lorsqu’aucune règle n’est définie, le module contient tout le contenu sous le chemin d’accès racine.

Vous pouvez définir une ou plusieurs définitions de filtre pour un module. Utilisez plusieurs filtres pour inclure le contenu de plusieurs chemins racine.

![Onglet Filtres](assets/edit-filter.png)

Lors de la création de filtres, vous pouvez définir un chemin d’accès ou utiliser une expression régulière pour spécifier tous les noeuds que vous souhaitez inclure ou exclure.

| Type de règle | Description |
|---|---|
| inclusion | L’inclusion d’un répertoire inclut ce répertoire et tous les fichiers et dossiers de ce répertoire (c’est-à-dire la sous-arborescence entière), mais **ne sera pas** d’inclure d’autres fichiers ou dossiers sous le chemin d’accès racine spécifié. |
| exclusion | L’exclusion d’un répertoire exclut le répertoire en question et l’ensemble des fichiers et des dossiers de ce répertoire (c’est-à-dire la sous-arborescence entière). |

Les filtres de module sont le plus souvent définis lors de votre première utilisation. [créez le package.](#creating-a-new-package) Cependant, elles peuvent également être modifiées ultérieurement, après quoi le module doit être recréé pour mettre à jour son contenu en fonction des nouvelles définitions de filtre.

>[!TIP]
>
>Un package peut contenir plusieurs définitions de filtre afin que les noeuds de différents emplacements puissent être facilement combinés en un seul package.

### Dépendances {#dependencies}

![Onglet Dépendances](assets/dependencies.png)

| Champ | Description | Exemple/Détails |
|---|---|---|
| Testé avec | Le nom et la version du produit auxquels ce module est ciblé ou est compatible. | `6.5` |
| Problèmes résolus | Un champ de texte permettant de répertorier les détails des bogues corrigés avec ce module, un bogue par ligne. | - |
| Dépend de | Répertorie les autres packages nécessaires pour que le package actuel s’exécute comme prévu lorsqu’il est installé. | `groupId:name:version` |
| Remplace | Liste des modules obsolètes que ce module remplace | `groupId:name:version` |

### Paramètres avancés {#advanced-settings}

![Onglet Paramètres avancés](assets/advanced-settings.png)

| Champ | Description | Exemple/Détails |
|---|---|---|
| Nom | Nom du fournisseur du package | `WKND Media Group` |
| URL | URL du fournisseur | `https://wknd.site` |
| Lien | Lien spécifique au module vers une page de fournisseur | `https://wknd.site/package/` |
| Requiert | Définit s’il existe des restrictions lors de l’installation du package. | **Administration** - Le package ne doit être installé qu’avec les privilèges d’administrateur.<br>**Redémarrer** - AEM doit être redémarré après l’installation du package |
| Traitement AC | Indique le mode de traitement des informations de contrôle d’accès définies dans le package lors de l’importation du package. | **Ignorer** - Conserver les listes de contrôle d’accès dans le référentiel <br>**Remplacer** - Remplacer les listes de contrôle d’accès dans le référentiel <br>**Fusion** - Fusionner les deux ensembles de listes de contrôle d’accès <br>**MergePreserve** - Fusionner le contrôle d’accès dans le contenu avec celui fourni avec le package en ajoutant les entrées de contrôle d’accès des entités non présentes dans le contenu <br>**Effacer** - Effacer les listes ACL |

### Captures d’écran de module {#package-screenshots}

Vous pouvez joindre plusieurs captures d’écran à votre module afin de fournir une représentation visuelle de l’affichage du contenu.

![Onglet Captures d’écran](assets/screenshots.png)

## Actions de module {#package-actions}

De nombreuses actions peuvent être entreprises sur un package.

### Création d’un module {#creating-a-new-package}

1. [Accédez à Package Manager.](#accessing)

1. Cliquez sur **Créer un package**.

   >[!TIP]
   >
   >Si votre instance comporte de nombreux packages, il se peut qu’une structure de dossiers soit en place. Dans ce cas, il est plus facile d’accéder au dossier cible requis avant de créer le module.

1. Dans le **Nouveau package** saisissez les champs suivants :

   ![Boîte de dialogue Nouveau package](assets/new-package-dialog.png)

   * **Nom du module** - Sélectionnez un nom explicite pour vous aider (et d’autres) à identifier facilement le contenu du package.

   * **Version** - Il s’agit d’un champ de texte que vous pouvez spécifier une version. Il est ajouté au nom du module pour former le nom du fichier zip.

   * **Groupe** - Il s’agit du nom du groupe cible (ou dossier). Les groupes vous aident à organiser vos modules. Un dossier est créé pour le groupe s’il n’existe pas déjà. Si vous laissez le nom du groupe vide, il crée le module dans la liste des modules principaux.

1. Cliquez sur **OK** pour créer le module.

1. AEM liste le nouveau package en haut de la liste des packages.

   ![Nouveau package](assets/new-package.png)

1. Cliquez sur **Modifier** pour définir la variable [contenu du module.](#package-contents) Cliquez sur **Enregistrer** une fois que vous avez terminé de modifier les paramètres.

1. Vous pouvez maintenant [créer](#building-a-package) votre module.

Il n’est pas obligatoire de créer immédiatement le package après sa création. Un module non créé ne contient aucun contenu et se compose uniquement des données de filtre et autres métadonnées du module.

### Création d’un module {#building-a-package}

Un module est souvent créé en même temps que vous [créer le module ;](#creating-a-new-package), mais vous pouvez renvoyer ultérieurement pour créer ou recréer le module. Cela peut s’avérer utile si le contenu du référentiel a changé ou si les filtres de package ont changé.

1. [Accédez à Package Manager.](#accessing)

1. Ouvrez les détails du module dans la liste des modules en cliquant sur le nom du module.

1. Cliquez sur **Créer**. Une boîte de dialogue vous demande de confirmer que vous souhaitez créer le module, car tout contenu existant du module sera remplacé.

1. Cliquez sur **OK**. AEM crée le module, répertoriant tout le contenu ajouté au module comme il le fait dans la liste des activités. Une fois l’opération terminée, AEM affiche un message de confirmation indiquant que le module a été créé et (lorsque vous fermez la boîte de dialogue) met à jour les informations de la liste de modules.

### Modification d’un module {#edit-package}

Une fois un package téléchargé dans AEM, vous pouvez modifier ses paramètres.

1. [Accédez à Package Manager.](#accessing)

1. Ouvrez les détails du module dans la liste des modules en cliquant sur le nom du module.

1. Cliquez sur **Modifier** et mettez à jour **[Paramètres du module](#package-settings)**, au besoin.

1. Cliquez sur **Enregistrer** pour enregistrer.

Vous devrez peut-être [recréer le module](#building-a-package) pour mettre à jour son contenu en fonction des modifications que vous avez apportées.

### Réencapsulation d’un module {#rewrapping-a-package}

Une fois qu’un package a été créé, il peut être réencapsulé. Le retour à la ligne modifie les informations du module sans qu’il y ait de miniature, de description, etc., sans modifier le contenu du module.

1. [Accédez à Package Manager.](#accessing)

1. Ouvrez les détails du module dans la liste des modules en cliquant sur le nom du module.

1. Cliquez sur **Modifier** et mettez à jour **[Paramètres du module](#package-settings)**, au besoin.

1. Cliquez sur **Enregistrer** pour enregistrer.

1. Cliquez sur **Plus** -> **Réencapsuler** et une boîte de dialogue de confirmation s’affiche.

### Affichage d’autres versions de module {#other-versions}

Comme chaque version d’un module apparaît dans la liste comme n’importe quel autre module, le gestionnaire de modules peut trouver d’autres versions d’un module sélectionné.

1. [Accédez à Package Manager.](#accessing)

1. Ouvrez les détails du module dans la liste des modules en cliquant sur le nom du module.

1. Cliquez sur **Plus** -> **Autres versions** et une boîte de dialogue s’ouvre avec une liste d’autres versions du même package avec des informations d’état.

### Affichage du contenu du module et test de l’installation {#viewing-package-contents-and-testing-installation}

Une fois qu’un module a été créé, vous pouvez en afficher le contenu.

1. [Accédez à Package Manager.](#accessing)

1. Ouvrez les détails du module dans la liste des modules en cliquant sur le nom du module.

1. Pour afficher le contenu, cliquez sur **Plus** -> **Contenu** et Package Manager répertorie l’intégralité du contenu du module dans le journal d’activité.

   ![Contenu du package](assets/package-contents.png)

1. Pour exécuter une exécution d’essai de l’installation, cliquez sur **Plus** -> **Test Install** et les rapports Gestionnaire de modules dans l’activité consignent les résultats comme si l’installation avait été effectuée.

   ![Test de l’installation](assets/test-install.png)

### Téléchargement des modules sur votre système de fichiers {#downloading-packages-to-your-file-system}

1. [Accédez à Package Manager.](#accessing)

1. Ouvrez les détails du module dans la liste des modules en cliquant sur le nom du module.

1. Cliquez sur le bouton **Télécharger** ou le nom du fichier lié du package dans la zone des détails du package.

1. AEM télécharge le module sur votre ordinateur.

### Partage d’un package {#share}

Le partage de modules était un service public centralisé pour distribuer des modules de contenu. Le partage de modules a été remplacé par [Distribution logicielle](#software-distribution) et ce bouton ne fonctionne plus.

### Chargement des modules à partir du système de fichiers {#uploading-packages-from-your-file-system}

1. [Accédez à Package Manager.](#accessing)

1. Sélectionnez le dossier du groupe dans lequel vous souhaitez charger le package.

1. Cliquez sur le bouton **Télécharger le module** bouton .

1. Fournissez les informations nécessaires sur le package téléchargé.

   ![Boîte de dialogue de chargement de module](assets/package-upload-dialog.png)

   * **Package** - Utilisez la variable **Parcourir..** pour sélectionner le package requis dans votre système de fichiers local.
   * **Forcer le chargement** - Si un package portant ce nom existe déjà, cette option force le téléchargement et remplace le package existant.

1. Cliquez sur **OK** et le package sélectionné est téléchargé et la liste des packages est mise à jour en conséquence.

Le contenu du module existe désormais sur AEM, mais pour rendre le contenu disponible, veillez à [installer le package](#installing-packages).

### Validation de modules {#validating-packages}

Les packages pouvant modifier du contenu existant, il est souvent utile de valider ces modifications avant l’installation.

#### Options de validation {#validation-options}

Le gestionnaire de modules peut effectuer les validations suivantes :

* [Importations de modules OSGi](#osgi-package-imports)
* [Recouvrements](#overlays)
* [Listes ACL](#acls)

##### Valider les importations de modules OSGi {#osgi-package-imports}

**Éléments vérifiés**

Cette validation inspecte le package pour tous les fichiers JAR (lots OSGi), extrait leurs `manifest.xml` (qui contient les dépendances versionnées sur lesquelles repose le bundle OSGi) et vérifie que l’instance AEM exporte ces dépendances avec les versions correctes.

**Comment sont-ils signalés ?**

Toutes les dépendances versionnées qui ne peuvent pas être satisfaites par l’instance AEM sont répertoriées dans le Journal d’activité de Package Manager.

**États d’erreur**

Si les dépendances ne sont pas satisfaites, les lots OSGi du module avec ces dépendances ne démarrent pas. Cela entraîne un déploiement d’application interrompu, car tout ce qui dépend du lot OSGi non démarré ne fonctionnera pas correctement.

**Résolution d’erreurs**

Pour résoudre les erreurs dues à des lots OSGi insatisfaits, la version de dépendance du lot avec des importations insatisfaites doit être ajustée.

##### Valider les recouvrements {#overlays}

**Éléments vérifiés**

Cette validation détermine si le module en cours d’installation contient un fichier déjà recouvert dans l’instance AEM de destination.

Par exemple, selon une superposition existante à l’emplacement `/apps/sling/servlet/errorhandler/404.jsp`, un module contenant `/libs/sling/servlet/errorhandler/404.jsp`, de sorte qu’il modifie le fichier existant à l’adresse `/libs/sling/servlet/errorhandler/404.jsp`.

**Comment sont-ils signalés ?**

Toutes ces superpositions sont décrites dans le Journal d’activité du Gestionnaire de modules.

**États d’erreur**

Un état d’erreur signifie que le module tente de déployer un fichier déjà recouvert. Les modifications du module seront donc remplacées (et donc masquées) par le recouvrement et ne prendront pas effet.

**Résolution d’erreurs**

Pour résoudre ce problème, le responsable du fichier de recouvrement dans `/apps` doit réviser les modifications apportées au fichier recouvert dans `/libs` et incorporer les modifications nécessaires dans le recouvrement ( `/apps`), puis redéployez le fichier recouvert.

>[!NOTE]
>
>Le mécanisme de validation ne permet pas de réconcilier le contenu superposé correctement incorporé dans le fichier de recouvrement. Par conséquent, cette validation continuera à signaler des conflits même après que les modifications nécessaires auront été apportées.

##### Valider les listes ACL {#acls}

**Éléments vérifiés**

Cette validation vérifie quelles autorisations sont ajoutées, comment elles seront gérées (fusion/remplacement) et si les autorisations actuelles seront affectées.

**Comment sont-ils signalés ?**

Les autorisations sont décrites dans le Journal d’activité du Gestionnaire de modules.

**États d’erreur**

Aucune erreur explicite ne peut être fournie. La validation indique simplement si de nouvelles autorisations des listes ACL seront ajoutées ou affectées par l’installation du module.

**Résolution d’erreurs**

Grâce aux informations fournies par la validation, les nœuds affectés peuvent être révisés dans CRXDE et les listes ACL peuvent être ajustées dans le module si besoin.

>[!CAUTION]
>
>Il est recommandé que les packages n’affectent pas les listes de contrôle d’accès fournies par AEM, car cela peut entraîner un comportement inattendu.

#### Validation {#performing-validation}

La validation des modules peut être effectuée de deux manières différentes :

* [via l’interface utilisateur du Gestionnaire de modules ;](#via-package-manager)
* [via une requête HTTP POST, telle que cURL.](#via-post-request)

La validation doit toujours avoir lieu après le chargement du module, mais avant son installation.

##### Validation De Package Via Package Manager {#via-package-manager}

1. [Accédez à Package Manager.](#accessing)

1. Ouvrez les détails du module dans la liste des modules en cliquant sur le nom du module.

1. Pour valider le package, cliquez sur **Plus** -> **Valider**,

1. Dans la boîte de dialogue modale qui s’affiche alors, utilisez les cases à cocher pour sélectionner le ou les types de validation et commencez la validation en cliquant sur **Valider**.

1. La ou les validations sélectionnées sont ensuite exécutées et les résultats s’affichent dans le Journal d’activité du Gestionnaire de modules.

##### Validation de modules via une requête HTTP POST {#via-post-request}

La requête POST se présente comme suit.

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

Le `type` peut être n’importe quelle liste non triée séparée par des virgules composée des éléments suivants :

* `osgiPackageImports`
* `overlays`
* `acls`

La valeur de `type` par défaut : `osgiPackageImports` si elle n’est pas explicitement transmise.

Lors de l’utilisation de cURL, exécutez une instruction similaire à celle-ci :

```shell
curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
```

Lors de la validation via une requête de POST, la réponse est renvoyée sous la forme d’un objet JSON.

### Affichage de la couverture de module {#package-coverage}

Les packages sont définis par leurs filtres. Vous pouvez demander au gestionnaire de modules d’appliquer des filtres d’un module au contenu de votre référentiel existant afin d’afficher le contenu du référentiel couvert par la définition de filtre du module.

1. [Accédez à Package Manager.](#accessing)

1. Ouvrez les détails du module dans la liste des modules en cliquant sur le nom du module.

1. Cliquez sur **Plus** -> **Couverture**.

1. Les détails de la couverture sont répertoriés dans le journal d’activité.

### Installation des modules {#installing-packages}

Le téléchargement d’un package ajoute uniquement le contenu du package au référentiel, mais il n’est pas accessible. Vous devez installer le package téléchargé pour utiliser le contenu du package.

>[!CAUTION]
>
>L’installation d’un module peut remplacer ou supprimer le contenu existant. Ne chargez un module que si vous êtes sûr qu’il ne supprime ou ne remplace pas du contenu dont vous avez besoin.

Avant l’installation de votre package, Package Manager crée automatiquement un package instantané qui contient le contenu qui sera remplacé. Cet instantané sera réinstallé si vous désinstallez votre package.

1. [Accédez à Package Manager.](#accessing)

1. Ouvrez les détails du package que vous souhaitez installer dans la liste des packages en cliquant sur le nom du package.

1. Cliquez sur l’icône **Installer** dans les détails de l’élément ou le **Installer** dans le statut du package.

1. Une boîte de dialogue vous invite à confirmer la demande et vous permet de spécifier des options supplémentaires.

   * **Extract Only** - Extrayez le package uniquement afin qu’aucun instantané ne soit créé et que la désinstallation ne soit donc pas possible
   * **Seuil d’enregistrement** - Nombre de noeuds transitoires jusqu’au déclenchement de l’enregistrement automatique (augmenter si vous rencontrez des exceptions de modification simultanée)
   * **Extraire les sous-modules** - Activer l&#39;extraction automatique des sous-packages
   * **Gestion du contrôle d’accès** - Indique la manière dont les informations de contrôle d’accès définies dans le package sont gérées lors de l’installation du package (les options sont les mêmes que la variable [paramètres de package avancés](#advanced-settings))
   * **Gestion des dépendances** - Spécifier la manière dont les dépendances sont gérées lors de l’installation

1. Cliquez sur **Installer**.

1. Le journal des activités détaille la progression de l’installation.

Une fois l’installation terminée et réussie, la liste des packages est mise à jour et le mot **Installé** apparaît dans le statut du package.

### Réinstallation des modules {#reinstalling-packages}

La réinstallation des packages effectue les mêmes étapes sur un package déjà installé qui est traité lors du [installez d’abord le package.](#installing-packages)

### Chargement et installation basés sur le système de fichiers {#file-system-based-upload-and-installation}

Vous pouvez complètement renoncer au gestionnaire de modules lors de l’installation des modules. AEM peut détecter les packages placés à un emplacement spécifique sur le système de fichiers local de l’ordinateur hôte et les télécharger et les installer automatiquement.

1. Sous le dossier d’installation d’AEM, une `crx-quicksart` dossier à côté du jar et `license.properties` fichier . Créez un dossier nommé `install` under `crx-quickstart` ce qui entraîne le chemin `<aem-home>/crx-quickstart/install`.

1. Dans ce dossier, ajoutez vos packages. Ils sont chargés et installés automatiquement sur votre instance.

1. Une fois le chargement et l’installation terminés, vous pouvez voir les modules dans Package Manager comme si vous aviez utilisé l’interface utilisateur de Package Manager pour les installer.

Si l’instance est en cours d’exécution, le téléchargement et l’installation démarrent immédiatement lorsque vous l’ajoutez au module dans la `install` folder

Si l’instance n’est pas en cours d’exécution, les modules placés dans la variable `install` sont installés au démarrage par ordre alphabétique.

### Désinstallation des modules {#uninstalling-packages}

La désinstallation du package rétablit l’instantané automatique du contenu du référentiel par Package Manager avant l’installation.

1. [Accédez à Package Manager.](#accessing)

1. Ouvrez les détails du package que vous souhaitez désinstaller dans la liste des packages en cliquant sur le nom du package.

1. Cliquez sur **Plus** -> **Désinstaller**, pour supprimer le contenu de ce module du référentiel.

1. Une boîte de dialogue vous invite à confirmer et répertorie toutes les modifications apportées.

1. Le package est supprimé et l’instantané est appliqué. La progression du processus s’affiche dans le journal des activités.

### Suppression de modules {#deleting-packages}

La suppression d’un module supprime uniquement ses détails du gestionnaire de modules. Si ce package a déjà été installé, le contenu installé ne sera pas supprimé.

1. [Accédez à Package Manager.](#accessing)

1. Ouvrez les détails du module que vous souhaitez supprimer de la liste des modules en cliquant sur le nom du module.

1. Le gestionnaire de modules vous demande de confirmer que vous souhaitez supprimer le module. Cliquez sur **OK** pour confirmer la suppression.

1. Les informations sur le module sont supprimées et les détails sont signalés dans le journal d’activité.

### Réplication des modules {#replicating-packages}

Répliquez le contenu d’un package pour l’installer sur l’instance de publication.

1. [Accédez à Package Manager.](#accessing)

1. Ouvrez les détails du module que vous souhaitez répliquer dans la liste des modules en cliquant sur le nom du module.

1. Cliquez sur **Plus** -> **Répliquer**.

1. Le module est répliqué et les détails sont signalés dans le journal d’activité.

## Distribution logicielle {#software-distribution}

AEM Les packages peuvent être utilisés pour créer et partager du contenu dans les environnements AEM.

[Distribution logicielle](https://downloads.experiencecloud.adobe.com) est un service centralisé conçu pour simplifier la recherche et le téléchargement des packages d’AEM.

Pour plus d’informations, reportez-vous à la section [Distribution logicielle .](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html)

>[!NOTE]
>
>Le gestionnaire de modules n’est actuellement pas intégré à Distribution logicielle, comme c’était le cas avec l’ancien service de partage de modules. Par conséquent, les boutons de partage et autres liens vers le partage de modules dans le gestionnaire de modules ne fonctionnent plus. La solution consiste à télécharger des modules sur votre disque local.
