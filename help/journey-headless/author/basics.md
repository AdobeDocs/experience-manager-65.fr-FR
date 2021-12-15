---
title: Découvrez les bases de la création
description: Découvrez les concepts et les mécanismes de création de contenu pour votre CMS sans affichage à l’aide de fragments de contenu.
index: true
hide: false
hidefromtoc: false
source-git-commit: 9661061a98c31fbb74bd0716dbedc7abef298f44
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 6%

---

# Principes de base de la création sans affichage avec AEM {#author-headless-basics}

## L&#39;histoire jusqu&#39;à présent {#story-so-far}

Au début du [AEM Parcours de création de contenu sans affichage](overview.md) la valeur [Introduction](introduction.md) couvrait les concepts de base et la terminologie relatifs à la création pour les sans-tête.

Cet article s’appuie sur ces éléments afin que vous compreniez comment créer votre propre contenu pour votre projet AEM sans interface.

## Objectif {#objective}

* **Audience** : débutant
* **Objectif**: Présentation des principes de base de la création CMS sans affichage :
   * Présentation de la création avec AEMaaCS
   * Présentation des fragments de contenu

## Manipulation de base {#basic-handling}

Avant de vous familiariser avec les fragments de contenu, voici une introduction (très) rapide à l’utilisation d’AEM....mais rien ne remplace vraiment l’expérience de connexion et d’utilisation du système.

### Auteur et publication {#author-preview-publish}

Une installation AEM se compose généralement d’au moins deux environnements :

* Création
* Publication

Vous vous connectez et utilisez l’environnement de création pour générer votre contenu. Une fois prêt, vous publiez votre contenu afin qu’il soit disponible en général. Pour les applications sans interface, ce serait pour les autres applications, pour les pages web, ce serait pour les lecteurs sur le web.

Pour plus d’informations, voir Concepts de création.

### Connexion {#signing-in}

Comme pour la plupart des systèmes, vous devrez vous connecter. En tant qu’auteur, vous recevrez les informations suivantes :

* Nom de l’utilisateur (compte)
* Mot de passe
* Lien d&#39;accès à l&#39;écran de connexion

Votre compte a été configuré avec les privilèges dont vous avez besoin. Si vous rencontrez des problèmes, nous vous recommandons de contacter votre équipe d’assistance au projet interne.

### Navigation {#navigation}

La première fois que vous vous connectez à un petit tutoriel en ligne, vous découvrirez certaines des principales fonctionnalités de l’interface utilisateur.

Vous pouvez ensuite utiliser le panneau de navigation pour accéder aux zones clés de l’AEM. Pour les fragments de contenu, vous utiliserez le **Console Ressources**.

Le panneau de navigation peut être ouvert en sélectionnant l’icône d’Adobe en haut à gauche, suivie de la petite icône en forme de boussole :

![Panneau de navigation](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)

>[!NOTE]
>Bien que les fragments de contenu soient une fonctionnalité d’AEM **Sites**, ils se trouvent dans la variable **Ressources** console. Il s’agit d’un détail technique qui ne devrait pas vous affecter, mais qui peut s’avérer utile à connaître.

Dans la console, vous pouvez sélectionner des dossiers pour accéder à votre fragment de contenu ou aux chemins de navigation (dans l’en-tête) pour revenir vers le haut de l’arborescence.

![Chemin de navigation](/help/journey-headless/author/assets/headless-journey-author-navigation-02.png)

### Actions, sélection, affichage {#actions-selecting-viewing}

Le **Ressources** La console est dédiée **Barres d’outils Action**, et **Actions rapides** que vous pouvez utiliser après avoir sélectionné une ressource (par exemple, un dossier ou un fragment de contenu).

Les actions rapides sont disponibles pour une seule ressource, voir **Bâle** dans l’exemple ci-dessous :

![Actions rapides](/help/journey-headless/author/assets/headless-journey-author-navigation-05.png)

La barre d’outils Actions permet d’accéder à l’ensemble des actions applicables au scénario actuel. Les actions disponibles peuvent changer. par exemple, selon votre emplacement ou si vous avez sélectionné plusieurs ressources :

![Barre d’outils d’action](/help/journey-headless/author/assets/headless-journey-author-navigation-06.png)

Vous pouvez sélectionner le format d’affichage de vos ressources à l’aide du sélecteur d’affichage :

![Sélecteur d’affichage](/help/journey-headless/author/assets/headless-journey-author-navigation-03.png)

Vous pouvez afficher des informations supplémentaires sur les éléments à l’aide du sélecteur de rail. Cela donne également accès à des actions supplémentaires.

![Rail de gauche](/help/journey-headless/author/assets/headless-journey-author-navigation-04.png)

## Création de fragments de contenu {#authoring-content-fragments}

C’était donc une introduction très rapide à l’interface utilisateur d’AEM, mais j’espère que vous avez eu la chance de l’essayer. Maintenant, nous en revenons à votre véritable intérêt - Fragments de contenu pour Headless.

Nous devrons passer en revue les éléments du début à la fin, mais il se peut que votre instance ait déjà créé des dossiers et/ou des fragments, et qu’ils se trouvent à des emplacements différents. Les principes sont les mêmes.

### Organisation et navigation {#organizing-and-navigating}

À moins que vous n’ayez très peu de fragments de contenu, vous souhaiterez les organiser afin que vous (et d’autres) puissiez les retrouver à nouveau.

#### Création d’un dossier {#creating-folder}

Pour ce faire, créez une série de dossiers dans **Fichiers** de la console Ressources. Sélectionnez la **Créer** option (en haut à droite), suivie de **Dossier**:

![Option Créer un dossier](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

Une boîte de dialogue s’ouvre, dans laquelle vous pouvez saisir les détails, puis confirmer avec **Créer**:

![Boîte de dialogue Créer un dossier](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### Utilisation des chemins et des balises pour limiter les modèles de fragment de contenu disponibles dans le dossier {#tags-paths-for-models-in-folder}

Cette section est légèrement plus avancée. Vous n&#39;en avez pas vraiment besoin si vous commencez à essayer des choses, mais c&#39;est le cas *very* utile lorsque vous avez beaucoup de fragments. Il est donc bon de le savoir - même si vous ne l&#39;utilisez pas encore tout à fait.

Votre architecte de contenu aura créé tous les modèles de fragment de contenu requis pour votre projet actuel, ainsi que peut-être d’autres projets également. Pour vous aider à simplifier les choses, ainsi que pour les autres auteurs, vous pouvez limiter la liste des modèles disponibles pour un dossier spécifique.

Après avoir créé votre dossier, vous pouvez l’ouvrir. **Propriétés**. Il existe ici différents onglets avec des informations et des détails de configuration sur le dossier. Pour les fragments de contenu, vous pouvez notamment utiliser la variable **Stratégies** pour définir des chemins d’accès et/ou des balises spécifiques pour ce dossier. Cela limite les modèles de fragment de contenu disponibles dans le dossier, car cela signifie que les modèles de fragment de contenu doivent satisfaire à ces exigences avant de pouvoir être utilisés pour générer des fragments dans ce dossier.

![Création de propriétés de dossier - Stratégies](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>Pour plus d’informations, reportez-vous à la section Modèles de fragment de contenu - Autorisation des modèles de fragment de contenu sur votre dossier de ressources.

Vous pouvez ensuite parcourir ces dossiers pour créer et modifier vos fragments de contenu.

#### Juste au cas où - Configuration des Cloud Services de dossiers {#cloud-services-folder}

Juste au cas où...

Vous recevrez probablement un dossier initial dans lequel vous pourrez créer vos dossiers. En effet, certains détails de configuration doivent être appliqués (généralement par un développeur ou un administrateur système) au dossier racine. Cela ne vous intéressera probablement pas, mais vous pouvez, au besoin, vérifier la variable **Configuration** dans le **Cloud Services** du dossier **Propriétés**:

![Création de propriétés de dossier - Configuration](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>Pour en savoir plus, voir Appliquer la configuration à votre dossier de ressources.

### Création d’un fragment de contenu {#creating-fragment}

La création d’un fragment de contenu est très similaire. Vous utilisez simplement le **Fragment de contenu** à la place :

![Option Créer un fragment de contenu](/help/journey-headless/author/assets/headless-journey-author-content-fragment-01.png)

Cette fois, un assistant s’ouvre. La première étape consiste à sélectionner le modèle de fragment de contenu sur lequel votre fragment sera basé :

![Créer un fragment de contenu - sélectionnez Modèle](/help/journey-headless/author/assets/headless-journey-author-content-fragment-02.png)

Après avoir continué avec **Suivant** vous pouvez fournir les détails (**De base** et **Avancé**) pour votre fragment :

![Créer un fragment de contenu - indiquez le nom](/help/journey-headless/author/assets/headless-journey-author-content-fragment-03.png)

Confirmer avec **Créer** et vous pouvez **Ouvrir** votre fragment dans l’éditeur.

### Modification d’un fragment {#editing-fragment}

Vous pouvez ouvrir un fragment immédiatement après sa création ou en le sélectionnant dans la console Ressources.

Lorsque l’éditeur s’ouvre pour la première fois, les éléments suivants s’affichent :

* Liste des icônes sur le côté gauche : vous donne accès à différentes zones de fonctionnalités. L’éditeur s’ouvre dans le **Variations** , c’est là que la plupart des modifications se produisent. Vous pouvez également être intéressé par la variable **Annotations** et **Métadonnées** onglets.

* En-tête contenant des informations sur le fragment et accès à diverses actions.

* La zone d’édition principale : cela dépend du modèle utilisé pour créer votre fragment.

Par exemple :

* Un fragment qui ne nécessite que plusieurs informations, certaines ayant un type spécifique. Pour le contenu sans interface, les références sont essentielles. Vous en apprendrez plus tard sur votre parcours.

   ![Éditeur de fragment de contenu - Mon fragment](/help/journey-headless/author/assets/headless-journey-author-content-fragment-04.png)

* Un fragment qui vous permet d’écrire une longue section de texte. Il existe ici d’autres options pour gérer et mettre en forme le texte. Vous pouvez même ouvrir les champs de texte individuels dans un éditeur plein écran (à l’aide de la petite icône de type écran située à droite).

   ![Éditeur de fragment de contenu - Espaces de l’Alaska](/help/journey-headless/author/assets/headless-journey-author-content-fragment-05.png)

>[!NOTE]
>
>Une documentation spécifique au projet peut être nécessaire pour aider les auteurs à obtenir des détails sur la manière de remplir certains champs.
>
>Voir Modèles de fragments de contenu - Types et propriétés de données pour obtenir des détails génériques.

Confirmez vos mises à jour en effectuant l’une des opérations suivantes : **Enregistrer** ou **Enregistrer et fermer**.

>[!NOTE]
>
>Pour plus d’informations, vous pouvez lire Variations - Création de fragments de contenu.

#### Ce dont vous n&#39;avez (probablement) pas besoin de vous inquiéter {#what-you-probably-do-not-need-to-worry-about}

Cette section peut sembler un peu étrange, mais une fois que vous avez ouvert l’éditeur de fragments de contenu et que vous commencez à l’explorer, vous verrez diverses options qui (probablement) ne s’appliquent pas à votre parcours sans interface en tant qu’auteur de contenu. C&#39;est juste une rapide mise en garde sur ce que vous devriez pouvoir ignorer dans un contexte sans tête :

* **Modèles de fragment de contenu**

   Le nom du modèle de fragment de contenu s’affiche en haut de l’éditeur, directement sous celui du fragment. Il s’agit également d’un lien qui vous mène à l’éditeur de modèles.
Les modèles de fragment de contenu sont essentiels à vos fragments de contenu, car ils définissent la structure que vous utilisez. Cependant, leur création et leur modification relèvent (généralement) de la responsabilité d’une autre personne, l’architecte de contenu.

   >[!NOTE]
   >
   >Si vous souhaitez en savoir plus, vous pouvez lire le Parcours Architecte de contenu AEM sans affichage .

* **Contenu associé**

   Celui-ci est assez évident car c&#39;est un onglet dans l&#39;éditeur.

   Les fragments de contenu sont disponibles dans AEM depuis plusieurs versions. À l’origine, elles étaient rendues disponibles pour une utilisation &quot;traditionnelle&quot; lors de la création de pages....et elles sont toujours utilisées dans ce contexte. Cela peut impliquer l’association de ressources (des images, par exemple) qui, bien qu’elles ne soient pas incorporées dans le fragment, doivent être disponibles pour l’auteur lors de la création d’une page.

* **Aperçu**

   Il s’agit d’un autre onglet de l’éditeur qui fournit une vue technique, principalement destinée aux développeurs.

* **Mettre à jour les références de page**

   Cette action est disponible à partir du **...** (ellipses). Il n’est pas intéressant pour les auteurs sans interface en ce qui concerne la création de pages.

### Publication {#publishing}

<!-- needs more details -->

Une fois le fragment terminé, vous pouvez **Publier** pour qu’il soit disponible pour les applications sans interface utilisateur graphique.

Les actions de publication sont disponibles dans l’éditeur (ou dans la barre d’outils de la fonction **Ressources** console) :

![Éditeur de fragment de contenu - Mon fragment](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

## Et après ? {#whats-next}

Maintenant que vous avez appris les principes de base, l’étape suivante consiste à [En savoir plus sur les références](references.md). Cette section présente et discute les différentes références disponibles, ainsi que de la manière de créer des niveaux de structure avec les Références de fragment - un élément clé de la création pour les sans-tête.

## Ressources supplémentaires {#additional-resources}

* [Concepts de création](/help/sites-authoring/author.md)

* [Manipulation de base](/help/sites-authoring/basic-handling.md) - cette page est principalement basée sur la variable **Sites** console, mais de nombreuses fonctionnalités/la plupart sont également pertinentes pour la création **Fragments de contenu** sous le **Ressources** console.

   * [Panneau de navigation](/help/sites-authoring/basic-handling.md#navigation-panel)

   * [En-tête](/help/sites-authoring/basic-handling.md#the-header)

   * [Barre d’outils d’action](/help/sites-authoring/basic-handling.md#actions-toolbar)

   * [Actions rapides](/help/sites-authoring/basic-handling.md#quick-actions)

   * [Affichage et sélection de ressources](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)

   * [Sélecteur de rail](/help/sites-authoring/basic-handling.md#rail-selector)

* [Utilisation de fragments de contenu](/help/assets/content-fragments/content-fragments.md)

   * [Gestion des fragments de contenu](/help/assets/content-fragments/content-fragments-managing.md)

      * [Application de la configuration à votre dossier de ressources](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [Création d’un fragment de contenu](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [Variations - création de fragments de contenu](/help/assets/content-fragments/content-fragments-variations.md)

   * [Modèles de fragment de contenu](/help/assets/content-fragments/content-fragments-models.md)

      * [Modèles de fragment de contenu - Types de données](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [Modèles de fragment de contenu - Propriétés](/help/assets/content-fragments/content-fragments-models.md#properties)

      * [Modèles de fragment de contenu - Autorisation des modèles de fragment de contenu sur votre dossier de ressources](/help/assets/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)


* Guides de prise en main
   * [Guide de démarrage rapide sur la création d’un dossier de ressources découplées](/help/sites-developing/headless/getting-started/create-assets-folder.md)

* [AEM Parcours d’architecture de contenu sans affichage](/help/journey-headless/architect/overview.md)

* [AEM Parcours de traduction sans affichage](/help/journey-headless/translation/overview.md)
