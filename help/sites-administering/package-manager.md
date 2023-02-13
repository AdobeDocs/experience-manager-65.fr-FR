---
title: Gestionnaire de packs
description: Découvrez les principes de base de la gestion des modules AEM avec le gestionnaire de modules.
feature: Administering
role: Admin
uuid: cba76a5f-5d75-4d63-a0f4-44c13fa1baf2
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 6694a135-d1e1-4afb-9f5b-23991ee70eee
docset: aem65
exl-id: e8929d7c-9920-4c02-95a9-6f7f7a365203
source-git-commit: b48b7631c501cea7e4ef1133a452fb6984e4547f
workflow-type: ht
source-wordcount: '3573'
ht-degree: 100%

---


# Gestionnaire de packs {#working-with-packages}

Les packs permettent d’importer et d’exporter le contenu du référentiel. Vous pouvez utiliser des modules pour installer un nouveau contenu, une nouvelle fonctionnalité, transférer du contenu entre les instances et sauvegarder le contenu du référentiel.

À l’aide du gestionnaire de packs, vous pouvez transférer des packs entre votre instance AEM et votre système de fichiers local à des fins de développement.

## Que sont les packs ? {#what-are-packages}

Un pack est un fichier zip contenant le contenu du référentiel dans un formulaire de sérialisation de système de fichiers, appelé sérialisation du coffre, fournissant une représentation des fichiers et des dossiers facile à utiliser et à modifier. Le contenu inclus dans le pack est défini à l’aide de filtres.

Un pack contient également les méta-informations du coffre, notamment les définitions des filtres et les informations de configuration de l’importation. Des propriétés de contenu supplémentaires, qui ne sont pas utilisées pour l’extraction du pack, peuvent être incluses dans le pack, telles qu’une description, une image visuelle ou une icône. Ces propriétés de contenu supplémentaires sont destinées au consommateur du pack de contenu et ne sont fournies qu’à titre d’informations.

>[!NOTE]
>
>Les modules représentent la version actuelle du contenu au moment où le module est créé. Ils n’incluent pas les versions précédentes du contenu qu’AEM conserve dans le référentiel.

## Gestionnaire de packs {#package-manager}

Le Gestionnaire de packs gère les packs de votre installation AEM. Après avoir [attribué les autorisations nécessaires](#permissions-needed-for-using-the-package-manager), vous pouvez utiliser le Gestionnaire de packs pour différentes actions, comme la configuration, la création, le téléchargement et l’installation des packs.

### Autorisations requises {#required-permissions}

Pour créer, modifier, charger et installer des packs, les utilisateurs doivent disposer des autorisations appropriées sur les nœuds suivants :

* Droits complets à l’exception de la suppression sur `/etc/packages`
* Le nœud contenant le contenu du pack

>[!CAUTION]
>
>L’octroi d’autorisations pour les packs peut entraîner la divulgation d’informations sensibles et la perte de données.
>
>Pour limiter ces risques, il est vivement recommandé d’accorder des autorisations à des groupes spécifiques sur des sous-arborescences dédiées uniquement.

### Accéder au gestionnaire de packs {#accessing}

Vous pouvez accéder au gestionnaire de packs de trois façons :

1. À partir du menu principal d’AEM -> **Outils** -> **Déploiement** -> **Packs**
1. Depuis [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) en utilisant la barre de sélection supérieure
1. Directement en accédant à `http://<host>:<port>/crx/packmgr/`

### Interface utilisateur du gestionnaire de packs {#ui}

Le gestionnaire de packs est divisé en quatre zones fonctionnelles principales :

* **Panneau de navigation de gauche** - Ce panneau vous permet de filtrer et de trier la liste des packs.
* **Liste de packs** - Il s’agit de la liste des packs de votre instance, filtrée et triée selon les sélections effectuées dans le panneau de navigation de gauche.
* **Journal d’activité** - Ce panneau est d’abord réduit et se développe pour détailler l’activité du gestionnaire de packs, comme lorsqu’un pack est créé ou installé. L’onglet Journal d’activité comporte des boutons supplémentaires pour :
   * **Effacer le journal**
   * **Afficher/Masquer**
* **Barre d’outils** - La barre d’outils contient des boutons d’actualisation pour le panneau de navigation de gauche et la liste des packs, ainsi que des boutons pour rechercher, créer et charger des packs.

![Interface utilisateur du gestionnaire de packs](assets/package-manager-ui.png)

Cliquez sur une option dans le panneau de navigation de gauche pour filtrer immédiatement la liste des packs.

Cliquez sur le nom d’un pack pour développer l’entrée dans la liste des packs et afficher plus de détails sur le pack.

![Détails développés du pack](assets/package-expand.png)

Plusieurs actions peuvent être effectuées sur un pack via les boutons de la barre d’outils disponibles lorsque les détails du pack sont développés.

* [Modifier](#edit-package)
* [Créer](#building-a-package)
* [Réinstaller](#reinstalling-packages)
* [Télécharger](#downloading-packages-to-your-file-system)
* [Partager](#share)

D’autres actions sont disponibles sous le bouton **Plus**.

* [Supprimer](#deleting-packages)
* [Couverture](#package-coverage)
* [Contenu](#viewing-package-contents-and-testing-installation)
* [Réencapsuler](#rewrapping-a-package)
* [Autres versions](#other-versions)
* [Désinstaller](#uninstalling-packages)
* [Tester l’installation](#viewing-package-contents-and-testing-installation)
* [Valider](#validating-packages)
* [Répliquer](#replicating-packages)

### Statut du pack {#package-status}

Chaque entrée de la liste des packs comporte un indicateur de statut qui vous permet de connaître d’un coup d’œil le statut du pack. Si vous passez la souris sur le statut, vous verrez apparaître une info-bulle contenant le détail du statut.

![Statut du pack](assets/package-status.png)

Si le pack a été modifié ou n’a jamais été conçu, le statut est présenté comme un lien permettant de prendre des mesures rapides afin de le concevoir à nouveau ou de l’installer.

## Paramètres du pack {#package-settings}

Un pack est essentiellement un ensemble de filtres et les données du référentiel basées sur ces filtres. Dans l’interface utilisateur du gestionnaire de packs, vous pouvez cliquer sur un pack, puis sur le bouton **Modifier** pour afficher les détails d’un pack, y compris les paramètres suivants.

* [Paramètres généraux](#general-settings)
* [Filtres de pack](#package-filters)
* [Dépendances des packs](#package-dependencies)
* [Paramètres avancés](#advanced-settings)
* [Captures d’écran des packs](#package-screenshots)

### Paramètres généraux {#general-settings}

Vous pouvez modifier différents paramètres du pack pour définir des informations telles que la description du pack, les dépendances et les informations sur le fournisseur.

La boîte de dialogue **Paramètres du pack** est accessible via le bouton **Modifier** lors de la [création](#creating-a-new-package) ou de la [modification](#viewing-and-editing-package-information) d’un pack. Une fois les modifications effectuées, cliquez sur **Enregistrer**.

![Boîte de dialogue Modifier le pack, paramètres généraux](assets/general-settings.png)

| Champ | Description |
|---|---|
| Nom | Le nom du pack |
| Groupe | Pour organiser des packs, vous pouvez saisir le nom d’un nouveau groupe ou sélectionner un groupe existant. |
| Version | Texte à utiliser pour la version |
| Description | Brève description du pack permettant le balisage HTML pour le formatage |
| Miniature | L’icône qui s’affiche dans la liste des packs |

#### Miniatures des modules {#thumbnails}

Une miniature fournit une représentation visuelle pour savoir rapidement ce que contient le module. Elle est ensuite affichée dans la liste de modules et peut vous aider à identifier facilement le module ou la classe de module.

Voici des exemples de conventions utilisées pour les modules officiels :

Correctif officiel

![Miniature de correctif officiel](assets/official-hotfix.png)

Extension ou installation officielle AEM

![Module officiel d’installation ou d’extension d’AEM ](assets/official-installation.png)

Pack de services officiel

![Icône de pack de services officiel d’AEM ](assets/official-service-pack.png)

Utilisez une icône unique pour votre module. Ne réutilisez pas une icône utilisée par Adobe.

### Filtres de pack {#package-filters}

Les filtres identifient les nœuds du référentiel à inclure dans le module. Une **définition de filtre** spécifie les informations suivantes :

* **Chemin d’accès racine** du contenu à inclure
* **Règles** incluant ou excluant certains nœuds sous le chemin d’accès racine

Ajoutez des règles à l’aide du bouton **+**. Supprimez des règles à l’aide du bouton **-**.

Les règles sont appliquées selon leur ordre, donc positionnez-les dans l’ordre de votre choix à l’aide des boutons fléchés **haut** et **bas**.

Les filtres peuvent ne comporter aucune règle ou en comporter plusieurs. Lorsqu’aucune règle n’est définie, le module contient tout le contenu sous le chemin d’accès racine.

Vous pouvez définir une ou plusieurs définitions de filtre pour un module. Utilisez plusieurs filtres de manière à inclure le contenu de différents chemins d’accès racine.

![Onglet Filtres](assets/edit-filter.png)

Lors de la création de filtres, vous pouvez définir un chemin dʼaccès ou utiliser une expression régulière pour spécifier tous les nœuds à inclure ou exclure.

| Type de règle | Description |
|---|---|
| inclusion | L’inclusion d’un répertoire inclut le répertoire en question et l’ensemble des fichiers et des dossiers de ce répertoire (c’est-à-dire la sous-arborescence entière) mais n’inclut **pas** d’autres fichiers ou dossiers situés sous le chemin d’accès racine spécifié. |
| exclusion | L’exclusion d’un répertoire exclut le répertoire en question et l’ensemble des fichiers et des dossiers de ce répertoire (c’est-à-dire la sous-arborescence entière). |

Les filtres de module sont le plus souvent définis lors de la première [création du module.](#creating-a-new-package) Cependant, ils peuvent également être modifiés ultérieurement. Le module devra alors être recréé pour mettre à jour son contenu en fonction des nouvelles définitions de filtre.

>[!TIP]
>
>Un module peut contenir plusieurs définitions de filtre de manière à pouvoir combiner facilement des nœuds de différents emplacements en un seul module.

### Dépendances {#dependencies}

![Onglet Dépendances](assets/dependencies.png)

| Champ | Description | Exemple/Détails |
|---|---|---|
| Testé avec | Le nom et la version du produit auquel ce paquet est destiné ou avec lequel il est compatible. | `6.5` |
| Problèmes résolus | Champ de texte permettant de répertorier les informations relatives aux bugs corrigés dans ce module, un bug par ligne. | - |
| Dépend de | Répertorie les autres modules nécessaires pour que le module actuel s’exécute comme prévu une fois installé. | `groupId:name:version` |
| Remplace | Liste des modules obsolètes que ce module remplace | `groupId:name:version` |

### Paramètres avancés {#advanced-settings}

![Onglet Paramètres avancés](assets/advanced-settings.png)

| Champ | Description | Exemple/Détails |
|---|---|---|
| Nom | Nom du fournisseur du module | `WKND Media Group` |
| URL | Adresse URL du fournisseur | `https://wknd.site` |
| Lien | Lien spécifique au module vers une page de fournisseur | `https://wknd.site/package/` |
| Requiert | Définit s’il existe des restrictions lors de l’installation du module. | **Administrateur** - Le module ne doit être installé qu’avec des privilèges Administrateur <br>**Redémarrage** - AEM doit être redémarré après l’installation du module |
| Traitement AC | Indique comment les informations de contrôle d’accès définies dans le module sont traitées lors de son importation | **Ignorer** - Les listes ACL dans le référentiel sont conservées <br>**Remplacer** - Les listes ACL dans le référentiel sont remplacées <br>**Fusionner** - Les deux ensembles de listes ACL sont fusionnés <br>**FusionnerConserver** - Le contrôle dʼaccès dans le contenu est fusionné avec celui fourni avec le module en ajoutant les entrées de contrôle dʼaccès des entités non présentes dans le contenu <br>**Effacer** - Les listes ACL sont effacées |

### Captures d’écran des packs {#package-screenshots}

Vous pouvez joindre plusieurs captures dʼécran à votre module pour fournir une représentation visuelle de la façon dont le contenu apparaît.

![Onglet Captures d’écran](assets/screenshots.png)

## Actions de module {#package-actions}

De nombreuses actions peuvent être entreprises sur un module.

### Création d’un module {#creating-a-new-package}

1. [Accédez au Gestionnaire de modules.](#accessing)

1. Cliquez sur **Créer un module**.

   >[!TIP]
   >
   >Si votre instance comporte de nombreux packs, une structure de dossiers peut être mise en place. Il est alors plus facile de naviguer vers le dossier cible requis avant de créer le nouveau pack.

1. Dans la boîte de dialogue **Nouveau pack**, saisissez les champs suivants :

   ![Boîte de dialogue Nouveau pack](assets/new-package-dialog.png)

   * **Nom du pack** - Sélectionnez un nom explicite pour vous aider (vous et les autres) à identifier facilement le contenu du pack.

   * **Version** - Champ de texte permettant d’indiquer une version. Elle est ajoutée au nom du pack pour former le nom du fichier ZIP.

   * **Groupe** - Il s’agit du nom du groupe (ou du dossier) cible. Les groupes vous aident à organiser vos packs. Si le dossier n’existe pas encore, il est créé pour le groupe. Si vous ne renseignez pas le nom du groupe, le pack est créé dans la liste des packs principale.

1. Cliquez sur **OK** pour créer le pack.

1. AEM place le nouveau pack en haut de la liste des packs.

   ![Nouveau pack](assets/new-package.png)

1. Cliquez sur **Modifier** pour définir le [contenu du pack.](#package-contents) Une fois que vous avez fini de modifier les paramètres, cliquez sur **Enregistrer**.

1. Vous pouvez maintenant [créer](#building-a-package) votre pack.

Il n’est pas obligatoire de concevoir immédiatement le pack après lʼavoir créé. Un pack non conçu ne contient aucun contenu et se compose uniquement des données du filtre et des autres métadonnées.

### Concevoir un pack {#building-a-package}

Un pack est souvent conçu au moment où vous [créez le pack](#creating-a-new-package), mais vous pouvez y revenir ultérieurement pour concevoir ou reconcevoir le pack. Cela peut s’avérer utile si le contenu du référentiel ou les filtres du pack ont été modifiés.

1. [Accédez au Gestionnaire de modules.](#accessing)

1. Ouvrez les détails du module dans la liste des modules en cliquant sur son nom.

1. Cliquez sur **Concevoir**. Une boîte de dialogue vous demande de confirmer que vous souhaitez concevoir le pack, car tout contenu existant du pack sera remplacé.

1. Cliquez sur **OK**. AEM crée le pack et répertorie tout le contenu ajouté au pack dans la liste des activités. Une fois l’opération terminée, AEM affiche un message de confirmation indiquant que le pack a été conçu et (lorsque vous fermez la boîte de dialogue) met à jour les informations de la liste de packs.

### Modifier un pack {#edit-package}

Une fois quʼun pack est téléchargé dans AEM, vous pouvez modifier ses paramètres.

1. [Accédez au Gestionnaire de modules.](#accessing)

1. Ouvrez les détails du module dans la liste des modules en cliquant sur son nom.

1. Cliquez sur **Modifier** et mettez à jour les **[Paramètres du pack](#package-settings)**, au besoin.

1. Cliquez sur **Enregistrer**.

En fonction des modifications que vous avez apportées, vous devrez peut-être [concevoir à nouveau le pack](#building-a-package) pour mettre à jour son contenu.

### Réencapsuler un pack {#rewrapping-a-package}

Une fois qu’un pack a été créé, il peut être réencapsulé. La réencapsulation modifie les informations du pack telles que la miniature, la description, etc. sans toucher à son contenu.

1. [Accédez au Gestionnaire de modules.](#accessing)

1. Ouvrez les détails du module dans la liste des modules en cliquant sur son nom.

1. Cliquez sur **Modifier** et mettez à jour les **[Paramètres du pack](#package-settings)**, au besoin.

1. Cliquez sur **Enregistrer**.

1. Cliquez sur **Plus** -> **Réencapsuler**. Une boîte de dialogue vous demandera une confirmation.

### Afficher d’autres versions de package {#other-versions}

Comme chaque version d’un pack apparaît dans la liste comme n’importe quel autre pack, le gestionnaire de packs peut trouver d’autres versions d’un pack sélectionné.

1. [Accédez au Gestionnaire de modules.](#accessing)

1. Ouvrez les détails du module dans la liste des modules en cliquant sur son nom.

1. Cliquez sur **Plus** -> **Autres versions** et une boîte de dialogue s’ouvre avec une liste d’autres versions du même pack avec des informations sur le statut.

### Afficher le contenu du pack et test de l’installation {#viewing-package-contents-and-testing-installation}

Une fois un pack créé, vous pouvez afficher son contenu.

1. [Accédez au Gestionnaire de modules.](#accessing)

1. Ouvrez les détails du module dans la liste des modules en cliquant sur son nom.

1. Pour afficher le contenu, cliquez sur **Plus** -> **Contenu**, et le gestionnaire de packs répertorie l’intégralité du contenu du pack dans le journal des activités.

   ![Contenu du pack](assets/package-contents.png)

1. Pour exécuter une essai de l’installation, cliquez sur **Plus** -> **Test de l’installation** et le Gestionnaire de packs établit un rapport sur les résultats dans le journal d’activité comme si l’installation avait été effectuée.

   ![Test de l’installation](assets/test-install.png)

### Télécharer des packs sur votre système de fichiers {#downloading-packages-to-your-file-system}

1. [Accédez au Gestionnaire de modules.](#accessing)

1. Ouvrez les détails du module dans la liste des modules en cliquant sur son nom.

1. Cliquez sur le bouton **Télécharger** ou sur le nom du fichier lié au pack dans la zone des détails du pack.

1. AEM télécharge le pack sur votre ordinateur.

### Partage d’un module {#share}

Le partage de modules était un service public centralisé pour distribuer des modules de contenu. Le partage de modules a été remplacé par la [Distribution logicielle](#software-distribution) et ce bouton ne fonctionne plus.

### Chargement des modules à partir du système de fichiers {#uploading-packages-from-your-file-system}

1. [Accédez au Gestionnaire de modules.](#accessing)

1. Sélectionnez le dossier de groupe dans lequel vous souhaitez que le module soit chargé.

1. Cliquez sur le bouton **Charger le module**.

1. Fournissez les informations nécessaires sur le module chargé.

   ![Boîte de dialogue de chargement de module](assets/package-upload-dialog.png)

   * **Module** - Servez-vous du bouton **Parcourir..** pour sélectionner le module requis dans votre système de fichiers local.
   * **Forcer le chargement** - Si un module portant ce nom existe déjà, cette option force le chargement et remplace le module existant.

1. Cliquez sur **OK**, le module sélectionné est chargé et la liste des modules est mise à jour en conséquence.

Le contenu du module existe désormais sur AEM, mais pour rendre le contenu disponible, veillez à [installer le module](#installing-packages).

### Validation de modules {#validating-packages}

Les modules pouvant modifier le contenu existant, il est souvent utile de valider ces modifications avant de les installer.

#### Options de validation {#validation-options}

Le gestionnaire de modules peut effectuer les validations suivantes :

* [Importations de modules OSGi](#osgi-package-imports)
* [Recouvrements](#overlays)
* [Listes ACL](#acls)

##### Valider les importations de modules OSGi {#osgi-package-imports}

**Contenu vérifié**

Cette validation inspecte le module pour tous les fichiers JAR (lots OSGi), extrait leur `manifest.xml` (qui contient les dépendances de version sur lesquelles le lot OSGi repose) et vérifie que l’instance AEM exporte lesdites dépendances avec les versions correctes.

**Comment c’est rapporté ?**

Toutes les dépendances de version qui ne peuvent pas être satisfaites par l’instance AEM est répertoriées dans le journal d’activité du Gestionnaire de modules.

**États d’erreur**

Si les dépendances ne sont pas satisfaites, les lots OSGi du module avec ces dépendances ne démarrent pas. Cela entraîne un déploiement d’application interrompu, car tout ce qui repose sur le lot OSGi non démarré ne fonctionnera pas correctement.

**Résolution d’erreurs**

Pour résoudre des erreurs dues à des lots OSGi non satisfaits, il faut ajuster la version dépendante du lot avec des importations non satisfaites.

##### Valider les recouvrements {#overlays}

**Contenu vérifié**

Cette validation détermine si le module en cours d’installation contient un fichier déjà recouvert dans l’instance AEM de destination.

Par exemple, étant donné un recouvrement présent dans `/apps/sling/servlet/errorhandler/404.jsp`, un module contenant `/libs/sling/servlet/errorhandler/404.jsp`, il modifiera donc le fichier existant dans `/libs/sling/servlet/errorhandler/404.jsp`.

**Comment sont-ils signalés ?**

Ces recouvrements sont décrits dans le Journal d’activités du Gestionnaire de modules.

**États d’erreur**

Un état d’erreur signifie que le module tente de déployer un fichier déjà recouvert. Les modifications du module seront donc remplacées (et donc masquées) par le recouvrement et ne prendront pas effet.

**Résolution d’erreurs**

Pour résoudre ce problème, le responsable du fichier de recouvrement dans `/apps` doit réviser les modifications apportées au fichier recouvert dans `/libs` et incorporer les modifications requises, le cas échéant, dans le recouvrement (`/apps`) et redéployer le fichier recouvert.

>[!NOTE]
>
>Le mécanisme de validation ne peut pas vérifier si le contenu recouvert a été correctement incorporé dans le fichier recouvert. Par conséquent, cette validation continuera à signaler des conflits même après que les modifications nécessaires auront été apportées.

##### Valider les listes ACL {#acls}

**Contenu vérifié**

Cette validation vérifie quelles autorisations sont ajoutées, comment elles seront gérées (fusion/remplacement) et si les autorisations actuelles seront affectées.

**Comment est-ce rapporté ?**

Les autorisations sont décrites dans le Journal d’activités du Gestionnaire de modules.

**États d’erreur**

Aucune erreur explicite ne peut être fournie. La validation indique simplement si de nouvelles autorisations des listes ACL seront ajoutées ou affectées par l’installation du module.

**Résolution d’erreurs**

Grâce aux informations fournies par la validation, les nœuds affectés peuvent être révisés dans CRXDE et les listes ACL peuvent être ajustées dans le module si besoin.

>[!CAUTION]
>
>Il est recommandé de sʼassurer que les modules n’affectent pas les listes ACL fournies par AEM, car cela pourrait entraîner un comportement inattendu du produit.

#### Validation {#performing-validation}

La validation des modules peut être effectuée de deux manières différentes :

* [via l’interface utilisateur du Gestionnaire de modules ;](#via-package-manager)
* [via une requête HTTP POST, telle que cURL.](#via-post-request)

La validation doit toujours avoir lieu après le chargement du module, mais avant son installation.

##### Validation de modules via le Gestionnaire de modules {#via-package-manager}

1. [Accédez au Gestionnaire de modules.](#accessing)

1. Ouvrez les détails du module dans la liste des modules en cliquant sur son nom.

1. Pour valider le module, cliquez sur **Plus** -> **Valider**.

1. Dans la boîte de dialogue modale qui s’affiche alors, utilisez les cases à cocher pour sélectionner le ou les types de validation et commencez la validation en cliquant sur **Valider**.

1. La ou les validations sélectionnées sont ensuite exécutées et les résultats sont affichés dans le Journal d’activité du Gestionnaire de modules.

##### Validation de modules via une requête HTTP POST {#via-post-request}

La requête POST se présente comme suit.

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

Le paramètre `type` peut être n’importe quelle liste non triée séparée par des virgules qui comprend :

* `osgiPackageImports`
* `overlays`
* `acls`

La valeur par défaut de `type` est `osgiPackageImports` si elle n’est pas explicitement transmise.

Si vous utilisez cURL, exécutez une instruction semblable à celle-ci :

```shell
curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
```

Lors de la validation par le biais dʼune requête POST, la réponse est renvoyée sous la forme d’un objet JSON.

### Affichage de la couverture du module {#package-coverage}

Les packs sont définis par leurs filtres. Vous pouvez demander au Gestionnaire de packs d’appliquer les filtres d’un pack au contenu de votre référentiel existant, afin de montrer le contenu du référentiel qui est couvert par la définition du filtre du pack.

1. [Accédez au Gestionnaire de modules.](#accessing)

1. Ouvrez les détails du module dans la liste des modules en cliquant sur son nom.

1. Cliquez sur **Plus** -> **Couverture**.

1. Les détails de la couverture sont répertoriés dans le journal d’activité.

### Installation des packs {#installing-packages}

Le chargement d’un pack ajoute uniquement le contenu du pack au référentiel, mais il n’est pas accessible. Vous devez installer le pack chargé pour utiliser son contenu.

>[!CAUTION]
>
>L’installation d’un module peut remplacer ou supprimer le contenu existant. Ne chargez un module que si vous êtes sûr qu’il ne supprime ou ne remplace pas du contenu dont vous avez besoin.

Avant l’installation de votre pack, le Gestionnaire de packs crée automatiquement un pack instantané qui contient le contenu qui sera remplacé. Cet instantané est réinstallé lorsque vous désinstallez le pack.

>[!CAUTION]
>
>* Si vous installez des ressources numériques, vous devez effectuer les opérations suivantes :
>  Tout d’abord, désactivez WorkflowLauncher.
>  Utilisez l’option du menu Composants de la console OSGi pour le désactiver.
>  `com.day.cq.workflow.launcher.impl.WorkflowLauncherImpl.`
>* Ensuite, une fois l’installation terminée, réactivez WorkflowLauncher.
>
>La désactivation de WorkflowLauncher permet de s’assurer que la structure d’importation d’actifs ne manipule pas (involontairement) les actifs lors de l’installation.

1. [Accédez au Gestionnaire de modules.](#accessing)

1. Ouvrez les détails du pack que vous souhaitez installer à partir de la liste des packs en cliquant sur le nom du pack.

1. Cliquez soit sur le bouton **Installer** dans les détails de l’élément, soit sur le lien **Installer** dans le statut du pack.

1. Une boîte de dialogue demande confirmation et permet de spécifier des options supplémentaires.

   * **Extraire uniquement** - Extraire le pack uniquement afin qu’aucun instantané ne soit créé et que la désinstallation ne soit pas possible
   * **Enregistrer le seuil** - Nombre de nœuds transitoires jusqu’au déclenchement de la sauvegarde automatique (augmentez si vous rencontrez des exceptions de modifications simultanées).
   * **Extraire les sous-packs** - Activer l’extraction automatique des sous-packs
   * **Gestion du contrôle d’accès** - Spécifie comment les informations de contrôle d’accès définies dans le pak sont traitées lors de l’installation du pack (les options sont les mêmes que les [paramètres avancés des packs](#advanced-settings))
   * **Gestion des dépendances** - Spécifier comment les dépendances sont gérées lors de l’installation

1. Cliquez sur **Installer**.

1. Le journal des activités détaille la progression de l’installation.

Une fois l’installation terminée et réussie, la liste des packs est mise à jour et le mot **Installé** apparaît dans le statut du pack.

### Réinstaller les packs {#reinstalling-packages}

La réinstallation des packs effectue les mêmes étapes sur un pack déjà installé que celle traitées lors de [l’installation initiale du pack.](#installing-packages)

### Chargement et installation basés sur le système de fichiers {#file-system-based-upload-and-installation}

Vous pouvez complètement renoncer au gestionnaire de packs lors de l’installation de packs. AEM peut détecter les packs placés à un emplacement spécifique du système de fichiers local de l’ordinateur hôte et les charger et installer automatiquement.

1. Sous le dossier d’installation d’AEM, il y a un dossier `crx-quicksart` à côté du fichier jar et du fichier `license.properties`. Créez un dossier nommé `install` sous `crx-quickstart` résultant au chemin d’accès `<aem-home>/crx-quickstart/install`.

1. Dans ce dossier, ajoutez vos packs. Ils sont chargés et installés automatiquement sur votre instance.

1. Une fois le chargement et l’installation terminés, vous pouvez voir les packs dans Gestionnaire de packs comme si vous aviez utilisé l’interface utilisateur du Gestionnaire de packs pour les installer.

Si l’instance est en cours d’exécution, le chargement et l’installation démarrent immédiatement lorsque vous l’ajoutez au pack dans le dossier `install`.

Si l’instance n’est pas en cours d’exécution, les packs placés dans le dossier `install` sont installés au démarrage par ordre alphabétique.

### Désinstaller les packs {#uninstalling-packages}

La désinstallation d’un pack ramène le contenu du référentiel à l’instantané réalisé automatiquement par le gestionnaire de packs avant l’installation.

1. [Accédez au Gestionnaire de modules.](#accessing)

1. Ouvrez les détails du pack que vous souhaitez désinstaller à partir de la liste des packs en cliquant sur le nom du pack.

1. Pour supprimer le contenu de ce pack du référentiel, cliquez sur **Plus** -> **Désinstaller**.

1. Une boîte de dialogue vous invite à confirmer et énumère toutes les modifications apportées.

1. Le pack est supprimé et l’instantané est appliqué. La progression du processus s’affiche dans le journal des activités.

### Supprimer des packs {#deleting-packages}

La suppression d’un pack supprime uniquement ses détails du gestionnaire de packs. Si ce pack a déjà été installé, le contenu installé n’est pas supprimé.

1. [Accédez au Gestionnaire de modules.](#accessing)

1. Ouvrez les détails du pack que vous souhaitez supprimer de la liste des packs en cliquant sur le nom du pack.

1. Le Gestionnaire de modules vous invite à confirmer que vous souhaitez supprimer le module. Cliquez sur **OK** pour confirmer la suppression.

1. Les informations sur le pack sont supprimées et les détails sont signalés dans le journal d’activité.

### Répliquer les packs {#replicating-packages}

Répliquez le contenu d’un pack afin de l’installer dans l’instance de publication.

1. [Accédez au Gestionnaire de modules.](#accessing)

1. Ouvrez les détails du pack que vous souhaitez répliquer depuis la liste des packs en cliquant sur le nom du pack.

1. Cliquez sur **Plus** -> **Répliquer**.

1. Le package est répliqué et les détails sont signalés dans le journal d’activité.

## Distribution logicielle {#software-distribution}

Les modules AEM peuvent être utilisés pour créer et partager du contenu dans les environnements AEM.

La [Distribution logicielle](https://downloads.experiencecloud.adobe.com) est un service centralisé conçu pour simplifier la recherche et le téléchargement des modules AEM.

Pour plus d’informations, reportez-vous à la [documentation sur la Distribution logicielle.](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=fr)

>[!NOTE]
>
>Le gestionnaire de modules n’est actuellement pas intégré à Distribution logicielle, comme c’était le cas avec l’ancien service de partage de modules. Par conséquent, les boutons de partage et autres liens vers le partage de modules dans le gestionnaire de modules ne fonctionnent plus. La solution consiste à télécharger des modules sur votre disque local.
