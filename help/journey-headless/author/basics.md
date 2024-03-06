---
title: Découvrez les bases de la création
description: Découvrez les concepts et les mécanismes de la création de contenu pour votre CMS Headless à l’aide de fragments de contenu.
exl-id: 125c4d0b-1572-4dba-823d-cdef2778f275
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 94%

---

# Principes de base de la création en découplage avec AEM {#author-headless-basics}

## Un peu d’histoire… {#story-so-far}

Au début du [Parcours de création de contenu découplé AEM](overview.md), l’[Introduction](introduction.md) présentait les concepts de base et la terminologie relatifs à la création découplée.

Cet article s’appuie sur ces éléments afin que vous compreniez comment créer votre propre contenu pour votre projet AEM découplé.

## Objectif {#objective}

* **Audience** : débutant
* **Objectif** : présentation des principes de base de la création CMS découplée :
   * Présentation de la création avec AEMaaCS
   * Présentation des fragments de contenu

## Manipulation de base {#basic-handling}

Avant de vous familiariser avec les fragments de contenu, voici une introduction (très) rapide à l’utilisation d’AEM...mais rien ne remplace vraiment l’expérience de connexion et d’utilisation du système.

### Auteur et publication {#author-preview-publish}

Une installation AEM se compose généralement d’au moins deux environnements :

* Création
* Publication

Vous vous connectez et utilisez l’environnement de création pour générer votre contenu. Une fois prêt, vous publiez votre contenu afin qu’il soit largement disponible. Pour les applications découplées, il serait destiné aux autres applications, pour les pages web, il serait destiné aux lecteurs sur le web.

Pour plus d’informations, consultez les concepts de création.

### Connexion {#signing-in}

Comme pour la plupart des systèmes, vous devez vous connecter. En tant qu’auteur, vous recevrez les informations suivantes :

* Nom de l’utilisateur (compte)
* Mot de passe
* Lien d’accès à l’écran de connexion

Votre compte a été configuré avec les privilèges dont vous avez besoin. Si vous rencontrez des problèmes, nous vous recommandons de contacter votre équipe interne d’assistance projet.

### Navigation {#navigation}

La première fois que vous vous connectez, un petit tutoriel en ligne vous présentera certaines des principales fonctionnalités de l’interface utilisateur.

Vous pouvez ensuite utiliser le panneau de navigation pour accéder aux principales zones d’AEM. Pour les fragments de contenu, vous utiliserez la **Console Assets**.

Le panneau de navigation peut être ouvert en sélectionnant l’icône d’Adobe en haut à gauche, puis la petite icône en forme de boussole :

![Panneau de navigation](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)

>[!NOTE]
>Bien que les fragments de contenu soient une fonctionnalité d’AEM **Sites**, ils se trouvent dans la console **Ressources**. Ce détail technique ne devrait pas vous affecter, mais il peut s’avérer utile de le savoir.

Dans la console, vous pouvez sélectionner des dossiers pour accéder à votre fragment de contenu ou aux chemins de navigation (dans l’en-tête) pour revenir vers le haut de l’arborescence.

![Chemin de navigation](/help/journey-headless/author/assets/headless-journey-author-navigation-02.png)

### Actions, sélection, affichage {#actions-selecting-viewing}

La console **Ressources** dispose de **Barres d’outils d’Actions** dédiées et d’**Actions rapides** que vous pouvez utiliser après avoir sélectionné une ressource (par exemple, un dossier ou un fragment de contenu).

Les actions rapides sont disponibles pour une seule ressource, comme pour **Bâle** dans l’exemple ci-dessous :

![Actions rapides](/help/journey-headless/author/assets/headless-journey-author-navigation-05.png)

La barre d’outils d’Actions permet d’accéder à l’ensemble des actions applicables au scénario actuel. Les actions disponibles peuvent changer, par exemple, selon votre emplacement ou si vous avez sélectionné plusieurs ressources :

![Barre d’outils d’Actions](/help/journey-headless/author/assets/headless-journey-author-navigation-06.png)

Vous pouvez sélectionner le format d’affichage de vos ressources à l’aide du sélecteur d’affichage :

![Sélecteur d’affichage](/help/journey-headless/author/assets/headless-journey-author-navigation-03.png)

Vous pouvez afficher des informations supplémentaires sur les éléments à l’aide du sélecteur de rail. Celui-ci donne également accès à des actions supplémentaires.

![Rail de gauche](/help/journey-headless/author/assets/headless-journey-author-navigation-04.png)

## Création de fragments de contenu {#authoring-content-fragments}

Fort de cette une introduction très rapide à l’interface utilisateur d’AEM, j’espère que vous avez eu la chance de l’essayer. Maintenant, revenons-en à votre véritable point d’intérêt : les fragments de contenu découplé.

Nous devrons passer en revue les éléments du début à la fin, mais il se peut que votre instance dispose de dossiers ou de fragments déjà créés, et qu’ils se trouvent à des emplacements différents. Les principes restent les mêmes.

### Organisation et navigation {#organizing-and-navigating}

À moins que vous n’ayez que très peu de fragments de contenu, vous souhaiterez les organiser afin que vous (et d’autres) puissiez les retrouver facilement.

#### Création d’un dossier {#creating-folder}

Pour ce faire, créez une série de dossiers dans la section **Fichiers** de la console Ressources. Sélectionnez l’option **Créer** (en haut à droite), puis **Dossier** :

![Option Créer un dossier](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

Une boîte de dialogue s’ouvre dans laquelle vous pouvez saisir les informations ; confirmez ensuite en sélectionnant **Créer** :

![Boîte de dialogue Créer un dossier](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### Utilisation des chemins et des balises pour limiter les modèles de fragment de contenu disponibles dans le dossier {#tags-paths-for-models-in-folder}

Cette section est d’un niveau légèrement plus avancé. Vous n’en avez pas vraiment besoin si vous commencez à essayer des choses, mais il est plus utile lorsque vous avez beaucoup de fragments. Il est donc bon de savoir qu’elle est là, même si vous ne l’exploiterez pas encore à son plein potentiel.

Votre architecte de contenu aura créé tous les modèles de fragment de contenu requis pour votre projet actuel, ainsi que peut-être d’autres projets. Pour vous simplifier les choses ainsi qu’aux autres auteurs, vous pouvez limiter la liste des modèles disponibles pour un dossier spécifique.

Après avoir créé votre dossier, vous pouvez ouvrir ses **Propriétés**. Cette section comporte différents onglets avec des informations et des détails de configuration sur le dossier. Pour les fragments de contenu, vous pouvez notamment utiliser l’onglet **Politiques** pour définir des chemins d’accès ou des balises spécifiques pour ce dossier. Cette configuration limite les modèles de fragment de contenu disponibles dans le dossier, car cela signifie que les modèles de fragment de contenu doivent satisfaire à ces exigences avant de pouvoir être utilisés pour générer des fragments dans ce dossier.

![Création de propriétés de dossier – Politiques](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>Pour plus d’informations, reportez-vous à la section Modèles de fragment de contenu – Autorisation de modèles de fragments de contenu dans votre dossier de ressources.

Vous pouvez ensuite parcourir ces dossiers pour créer et modifier vos fragments de contenu.

#### Juste au cas où – Configuration des services cloud de dossiers {#cloud-services-folder}

Juste au cas où...

Vous recevrez probablement un dossier initial dans lequel vous pourrez créer vos dossiers. En effet, certains détails de configuration doivent être appliqués (généralement par un développeur ou un administrateur système) au dossier racine. Cela ne vous intéresse probablement pas, mais vous pouvez, au besoin, vérifier la variable **Configuration** dans le **Cloud Service** du dossier **Propriétés**:

![Création de propriétés de dossier – Configuration](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>Pour en savoir plus, consultez Application de la configuration à votre dossier de ressources.

### Création d’un fragment de contenu {#creating-fragment}

La création d’un fragment de contenu est très similaire à celle d’un dossier. Vous utiliserez simplement l’option de **Fragment de contenu** :

![Option Créer un fragment de contenu](/help/journey-headless/author/assets/headless-journey-author-content-fragment-01.png)

Cette fois, un assistant s’ouvre. La première étape consiste à sélectionner le modèle de fragment de contenu sur lequel baser votre fragment :

![Créer un fragment de contenu – Sélection du modèle](/help/journey-headless/author/assets/headless-journey-author-content-fragment-02.png)

Continuez avec **Suivant** puis entrez les informations nécessaires (**De base** et **Avancé**) pour votre fragment :

![Créer un fragment de contenu – Saisie du nom](/help/journey-headless/author/assets/headless-journey-author-content-fragment-03.png)

Confirmez avec **Créer** puis **ouvrez** votre fragment dans l’éditeur.

### Modification d’un fragment {#editing-fragment}

Vous pouvez ouvrir un fragment immédiatement après sa création ou en le sélectionnant dans la console Assets.

Lorsque l’éditeur s’ouvre pour la première fois, les éléments suivants s’affichent :

* Une liste des icônes sur le côté gauche qui vous donne accès à différentes zones de fonctionnalités. L’éditeur s’ouvre dans l’onglet **Variations**, où vous opérerez la plupart de vos modifications. Vous pouvez également être intéressé par les onglets **Annotations** et **Métadonnées**.

* En-tête contenant des informations sur le fragment et un accès à différentes actions.

* La zone d’édition principale qui dépend du modèle utilisé pour créer votre fragment.

Par exemple :

* Un fragment qui ne nécessite que plusieurs informations, certaines avec un type spécifique. Pour le contenu découplé, les références sont essentielles. Vous en apprendrez plus tard sur votre parcours.

  ![Éditeur de fragment de contenu – Mon fragment](/help/journey-headless/author/assets/headless-journey-author-content-fragment-04.png)

* Un fragment qui vous permet d’écrire une longue section de texte. Il existe ici d’autres options pour gérer et mettre en forme le texte. Vous pouvez même ouvrir les champs de texte individuels dans un éditeur plein écran (à l’aide de la petite icône d’écran située à droite).

  ![Éditeur de fragment de contenu – Alaska Spirits](/help/journey-headless/author/assets/headless-journey-author-content-fragment-05.png)

>[!NOTE]
>
>Une documentation spécifique au projet peut être nécessaire pour aider les auteurs à obtenir des informations sur la manière de remplir certains champs.
>
>Consultez « Modèles de fragments de contenu – Types et propriétés de données » pour obtenir des informations générales.

Confirmez vos mises à jour en effectuant l’une des opérations suivantes : **Enregistrer** ou **Enregistrer et fermer**.

>[!NOTE]
>
>Pour plus d’informations, vous pouvez lire Variations – Création de fragments de contenu.

#### Ce dont vous ne devez (probablement) pas vous inquiéter {#what-you-probably-do-not-need-to-worry-about}

Cette section peut sembler un peu étrange mais une fois que vous avez ouvert l’éditeur de fragments de contenu et que vous commencez à l’explorer, vous verrez diverses options qui ne s’appliquent (probablement) pas à votre parcours découplé en tant qu’auteur de contenu. Il s’agit simplement d’une rapide mise en garde sur ce que vous devriez pouvoir ignorer dans un contexte découplé :

* **Modèles de fragment de contenu**

  Le nom du modèle de fragment de contenu s’affiche en haut de l’éditeur, directement sous celui du fragment. Il s’agit également d’un lien qui vous mène à l’éditeur de modèles.
Les modèles de fragment de contenu sont essentiels à vos fragments de contenu, car ils définissent la structure que vous utilisez. Cependant, leur création et leur modification relèvent (généralement) de la responsabilité d’une autre personne, l’architecte de contenu.

  >[!NOTE]
  >
  >Si vous souhaitez en savoir plus, vous pouvez consultez le parcours d’architecture de contenu découplé AEM.

* **Contenu associé**

  Celui-ci est assez évident car il s&#39;agit d&#39;un onglet de l&#39;éditeur.

  Les fragments de contenu sont disponibles dans AEM depuis un certain nombre de versions. À l’origine, ils étaient disponibles pour une utilisation « traditionnelle » lors de la création de pages...et ils sont toujours utilisés dans ce contexte. Cela peut impliquer l’association de ressources (par exemple, des images) qui, bien qu’elles ne soient pas incorporées dans le fragment, doivent être disponibles pour l’auteur lors de la création d’une page.

* **Aperçu**

  Il s’agit d’un autre onglet de l’éditeur qui fournit une vue technique, principalement destinée aux développeurs.

* **Mettre à jour les références de page**

  Cette action est disponible à partir du menu déroulant **...** (points de suspension). Elle n’a pas d’intérêt particulier pour les auteurs de contenu découplé, car elle concerne la création de pages.

### Publication {#publishing}

<!-- needs more details -->

Une fois le fragment terminé, vous pouvez le **Publier** pour qu’il soit disponible pour les applications découplées.

Les actions de publication sont disponibles dans l’éditeur (ou dans la barre d’outils de la console **Assets**) :

![Éditeur de fragment de contenu – Mon fragment](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

## Prochaines étapes {#whats-next}

Maintenant que vous avez appris les principes de base, l’étape suivante consiste à [en découvrir plus sur les références](references.md). Cette section présente et discute les différentes références disponibles, ainsi que la manière de créer des niveaux de structure à l’aide des références de fragment, un élément clé de la création de contenu découplé.

## Ressources supplémentaires {#additional-resources}

* [Concepts de création](/help/sites-authoring/author.md)

* [Manipulation de base](/help/sites-authoring/basic-handling.md) : cette page est principalement basée sur la console **Sites**, mais de nombreuses ou la plupart des fonctionnalités sont également pertinentes pour la création de **Fragments de contenu** dans la console **Assets**.

   * [Panneau de navigation](/help/sites-authoring/basic-handling.md#navigation-panel)

   * [En-tête](/help/sites-authoring/basic-handling.md#the-header)

   * [Barre d’outils d’Actions](/help/sites-authoring/basic-handling.md#actions-toolbar)

   * [Actions rapides](/help/sites-authoring/basic-handling.md#quick-actions)

   * [Affichage et sélection de ressources](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)

   * [Sélecteur de rail](/help/sites-authoring/basic-handling.md#rail-selector)

* [Utilisation de fragments de contenu](/help/assets/content-fragments/content-fragments.md)

   * [Gestion des fragments de contenu](/help/assets/content-fragments/content-fragments-managing.md)

      * [Application de la configuration à votre dossier de ressources](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [Création d’un fragment de contenu](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)

   * [Variations – Création de fragments de contenu](/help/assets/content-fragments/content-fragments-variations.md)

   * [Modèles de fragment de contenu](/help/assets/content-fragments/content-fragments-models.md)

      * [Modèles de fragment de contenu – Types de données](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [Modèles de fragment de contenu – Propriétés](/help/assets/content-fragments/content-fragments-models.md#properties)

      * [Modèles de fragment de contenu - Autoriser des modèles de fragments de contenu dans votre dossier de ressources](/help/assets/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)

* Guides de prise en main
   * [Guide de démarrage rapide sur la création d’un dossier de ressources découplées](/help/sites-developing/headless/getting-started/create-assets-folder.md)

* [Parcours d’architecture de contenu découplé AEM](/help/journey-headless/architect/overview.md)

* [Parcours de traduction découplée AEM](/help/journey-headless/translation/overview.md)
