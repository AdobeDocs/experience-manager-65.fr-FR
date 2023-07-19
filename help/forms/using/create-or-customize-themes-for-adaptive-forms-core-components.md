---
title: Comment créer ou personnaliser des thèmes de formulaire adaptatif ?
seo-title: How to create a theme for Adaptive Forms Core Components?
description: Découvrez comment créer ou personnaliser des thèmes pour les composants principaux de Forms adaptatif à l’aide des spécifications BEM
seo-description: Learn to create or customize themes for Adaptive Forms Core Components using BEM specifications
keywords: créer un thème de composants principaux de formulaires adaptatifs, créer un nouveau thème, personnaliser le thème, charger un nouveau thème, utiliser un thème dans les formulaires, supprimer un thème, créer un thème dans AEM 6.5 forms
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
source-git-commit: a5d38ef6b3281992fd9ac3121cdb6c998631b205
workflow-type: tm+mt
source-wordcount: '1961'
ht-degree: 9%

---


# Création ou personnalisation d’un thème de formulaire adaptatif {#introduction-to-theme}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM 6.5 | Cet article |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html) |

**S’applique à :** ✅ Composants principaux de formulaire adaptatif ❎ [Composants de base de formulaires adaptatifs](/help/forms/using/themes.md).

Dans AEM Forms 6.5, un thème est une bibliothèque cliente AEM que vous utilisez pour définir les styles (apparence) d’un formulaire adaptatif. Un thème contient des détails de style pour les composants et les panneaux. Ces styles incluent les propriétés telles que les couleurs d’arrière-plan, les couleurs d’état, la transparence, l’alignement et la taille. Lorsque vous appliquez un thème, le style spécifié se reflète sur les composants correspondants. Un thème est géré indépendamment sans référence à un formulaire adaptatif et peut être réutilisé dans plusieurs Forms adaptatives.

## Thèmes disponibles {#available-theme}

L’environnement AEM 6.5 fournit les thèmes répertoriés ci-dessous pour le Forms adaptatif basé sur les composants principaux :

* [Thème Canevas](https://github.com/adobe/aem-forms-theme-canvas)
* [Thème WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Thème EASEL](https://github.com/adobe/aem-forms-theme-easel)

## Comprendre la structure des thèmes {#understanding-structure-of-theme}

Un thème est un module qui englobe le fichier CSS, les fichiers JavaScript et les ressources (comme les icônes) qui définissent le style de votre Forms adaptatif. Un thème de formulaire adaptatif suit une organisation spécifique composée des composants suivants :

* `src/theme.scss`: Ce dossier comprend le fichier CSS qui a un large impact sur l’ensemble du thème. Il sert d’emplacement centralisé pour définir et gérer le style et le comportement de votre thème. En apportant des modifications à ce fichier, vous pouvez apporter des modifications appliquées de manière universelle à l’ensemble du thème, en influençant l’aspect et les fonctionnalités de vos pages Forms adaptatives et AEM Sites.

* `src/site`: Ce dossier contient des fichiers CSS qui sont appliqués à l’ensemble de la page d’un site AEM. Ces fichiers se composent de code et de styles qui affectent la fonctionnalité globale et la disposition de la page de votre site AEM. Toutes les modifications apportées ici sont répercutées sur toutes les pages de votre site.

* `src/components`: Les fichiers CSS de ce dossier sont conçus pour des composants principaux d’AEM individuels. Chaque dossier dédié d’un composant comprend une `.scss` qui met en forme ce composant particulier dans un formulaire adaptatif. Par exemple, la variable `/src/components/button/_button.scss` contient des informations de style pour le composant Bouton Forms adaptatif .

  ![Structure du thème de zone de travail](/help/forms/using/assets/component-based-theme-folder-structure.png)

* `src/resources`: Ce dossier contient des fichiers statiques tels que des icônes, des logos et des polices. Ces ressources sont utilisées pour améliorer les éléments visuels et la conception globale de votre thème.

## Création d’un thème

AEM Forms 6.5 fournit les thèmes répertoriés ci-dessous pour le Forms adaptatif basé sur les composants principaux.

* [Thème Canevas](https://github.com/adobe/aem-forms-theme-canvas)
* [Thème WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Thème EASEL](https://github.com/adobe/aem-forms-theme-easel)

Vous pouvez [personnaliser l’un de ces thèmes pour créer un thème ;](#customize-a-theme-core-components).

## Personnalisation d’un thème {#customize-a-theme-core-components-based-adaptive-forms}

La personnalisation d’un thème fait référence au processus de modification et de personnalisation de l’aspect d’un thème. Lorsque vous personnalisez un thème, vous apportez des modifications à ses éléments de conception, à sa mise en page, à ses couleurs, à sa typographie et parfois au code sous-jacent. Vous pouvez ainsi créer une apparence unique et personnalisée de votre site web ou application tout en conservant la structure et les fonctionnalités de base fournies par le thème.

>[!NOTE]
>
> * Utilisez le gestionnaire de modules pour déployer un thème sur toutes les instances d’auteur et de publication.
> * Une bibliothèque cliente de thème est importée ou exportée via le gestionnaire de modules comme tout autre module.

### Conditions préalables pour personnaliser un thème {#prerequisites}

* [Activation des composants principaux de Forms adaptatif](/help/forms/using/enable-adaptive-forms-core-components.md) pour votre environnement.

* Installez la dernière version de [Apache Maven.](https://maven.apache.org/download.cgi) Apache Maven est un outil d’automatisation de génération couramment utilisé pour les projets Java™. L’installation de la dernière version vous garantit les dépendances nécessaires à la personnalisation du thème.

* Découvrez comment créer une [bibliothèque cliente dans Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html?lang=fr). AEM fournit des bibliothèques clientes qui vous permettent de stocker votre code côté client dans le référentiel, de l’organiser en catégories, et de définir quand et comment chaque catégorie de code doit être diffusée au client.

* Installez un éditeur de texte brut. Par exemple, Microsoft® Visual Studio Code. L’utilisation d’un éditeur de texte brut tel que Microsoft® Visual Studio Code fournit un environnement convivial pour la modification et la modification de fichiers de thème.

* Vérifiez que l’environnement AEM Forms est opérationnel.

### Observations relatives à la personnalisation d’un thème {#consideration}

* Assurez-vous que vous utilisez [Projet Archetype utilisé pour activer les composants principaux de Forms adaptatif](/help/forms/using/enable-adaptive-forms-core-components.md) sur votre environnement pour personnaliser vos thèmes.

* Lors de la publication d’un formulaire adaptatif, les bibliothèques clientes ne sont pas automatiquement publiées sur l’instance de publication. Veillez à publier manuellement la bibliothèque cliente référencée dans un formulaire adaptatif dans vos environnements de publication.

* Adobe recommande de ne pas modifier les noms de classe des bibliothèques clientes.

### Personnalisation d’un thème {#customize-a-theme-core-components}

La création ou la personnalisation d’un thème est un processus à plusieurs étapes. Effectuez les étapes dans l’ordre indiqué pour créer/personnaliser le thème :

1. [Clonage d’un thème](#clone-git-repo-of-theme)
1. [Personnaliser l’aspect du thème](#customize-the-theme)
1. [Préparer le thème pour le déploiement local](#generate-the-clientlib)
1. [Déployer le thème sur un environnement local](#deploy-the-theme-on-a-local-environment)
1. [Déployer le thème dans l’environnement de production](#5-deploy-a-theme-on-your-production-environment)

<!--
 ![Theme Customization workflow](/help/forms/using/assets/custom-theme-steps.png)
-->

Les exemples fournis dans le document reposent sur la variable **Canevas** mais vous pouvez cloner n’importe quel thème et le personnaliser en suivant les mêmes instructions. Ces instructions s’appliquent à n’importe quel thème, ce qui vous permet de modifier des thèmes en fonction de vos besoins spécifiques.

#### 1. Cloner le référentiel Git du thème {#clone-git-repo-of-theme}

Pour cloner un thème pour Forms adaptatif basé sur les composants principaux, choisissez l’un des thèmes suivants :

* [Thème Canevas](https://github.com/adobe/aem-forms-theme-canvas)
* [Thème WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Thème EASEL](https://github.com/adobe/aem-forms-theme-easel)

Suivez les instructions suivantes pour cloner un thème :

1. Ouvrez l’invite de commande ou la fenêtre de terminal dans votre environnement de développement local.

1. Exécutez la variable `git clone` pour cloner un thème.

   ```
      git clone [Path of Git Repository of the theme]
   ```

   Remplacez la variable [Chemin du référentiel Git du thème] avec l’URL réelle du référentiel Git correspondant du thème

   Par exemple, pour cloner le thème Zone de travail, exécutez la commande suivante :

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

1. Sélectionnez **Approbation des auteurs de tous les fichiers du dossier parent** et cliquez sur **Oui, je fais confiance aux auteurs**.

Une fois la commande exécutée correctement, vous disposez d’une copie locale du thème disponible sur votre ordinateur dans le  `aem-forms-theme-canvas` dossier.

#### 2 . Personnaliser le thème {#customize-the-theme}

Vous avez la possibilité de personnaliser des composants individuels ou d’effectuer des modifications au niveau du thème à l’aide des variables globales d’un thème. La modification des variables globales a un effet en cascade sur tous les composants individuels. Vous pouvez, par exemple, utiliser des variables globales pour modifier la couleur de bordure de tous les composants d’un formulaire adaptatif ou appliquer une couleur de fond vibrante aux boutons CTA (Appel à l’action). Vous pouvez :

* [Définition des styles de niveau de thème](#theme-customization-global-level)

* [Définition des styles de niveau de composant](#component-based-customization)

##### Définition des styles de niveau de thème {#theme-customization-global-level}

Le `variable.scss` contient les variables globales du thème. En mettant à jour ces variables, vous pouvez apporter des modifications liées au style au niveau du thème. Pour appliquer des styles au niveau du thème, procédez comme suit :

1. Ouvrez le fichier `<your-theme-sources>/src/site/_variables.scss` en mode d’édition.
1. Modifiez la valeur de n’importe quelle propriété. Par exemple, la couleur d’erreur par défaut est le rouge. Pour changer la couleur de l’erreur du rouge au bleu, modifiez le code hexadécimal de la couleur de la balise `$error`. Par exemple, `$error: #196ee5`.

   ![Exemple : Couleur d’erreur définie sur bleu](/help/forms/using/assets/theme-level-changes.png)

1. Enregistrez et fermez le fichier.


De même, vous pouvez utiliser la variable `variable.scss` pour définir la famille et le type de polices, les couleurs du thème et de la police, la taille de la police, l’espacement des thèmes, l’icône d’erreur, les styles de bordure du thème et d’autres variables ayant un impact sur plusieurs composants de formulaire adaptatif.

##### Définition des styles de niveau de composant {#component-based-customization}

Vous avez également la possibilité de personnaliser la police, la couleur, la taille et d’autres propriétés CSS de composants principaux de formulaire adaptatif spécifiques, tels que les boutons, cases à cocher, conteneurs, pieds de page, etc. En modifiant le fichier CSS associé au composant spécifique, vous pouvez aligner son style avec l’identité graphique de votre entreprise. Pour personnaliser le style d’un composant, procédez comme suit :

1. Ouvrir le fichier `<your-theme-sources>/src/components/<component>/<component.scss>` pour modification. Par exemple, pour modifier la couleur de police du composant Bouton, ouvrez le `<your-theme-sources>/src/components/button/button.scss`, fichier .
1. Modifiez la valeur de n’importe quelle variable selon vos besoins. Par exemple, pour changer la couleur du composant de bouton lorsque vous passez la souris sur Vert, modifiez la valeur de la variable `color: $white` dans la propriété `cmp-adaptiveform-button__widget:hover` vers le code hexadécimal #12b453 ou toute autre nuance de vert. Le code final ressemble à ce qui suit :

   ```
    .cmp-adaptiveform-button__widget:hover {
    background: $dark-gray;
    color: #12b453;
    }
   ```


1. Enregistrez et fermez le fichier.

<!--

   ![Example: Hover color set to green](/help/forms/using/assets/button-customization.png)

-->

>[!NOTE]
>
> Lorsqu’un style est défini au niveau du thème et du composant, le style défini au niveau du composant est prioritaire.

#### 3. Préparer le thème pour le déploiement {#generate-the-clientlib}

Pour déployer un thème sur une instance AEM, il doit être converti en bibliothèque cliente. Pour convertir le thème en bibliothèque cliente, procédez comme suit :

1. Ouvrez l’invite de commande ou la fenêtre de terminal.
1. Accédez au dossier `<your-theme-sources>`. Par exemple, `C:\aem-forms-theme-canvas`.
1. Exécutez la commande suivante :

   ```
      npm run create-clientlib --category=adaptiveform.theme.[yourtheme]
   ```

   Remplacer `[yourtheme]` avec le nom de votre thème personnalisé. Par exemple, si le nom du thème personnalisé est `customcanvastheme`, exécutez la commande suivante :

   ```
       npm run create-clientlib --category=adaptiveform.theme.customcanvastheme
   ```

   Une fois la commande exécutée, un dossier de bibliothèque cliente est créé à l’adresse `themerepo\theme-clientlibs\[yourtheme]`.

   ![Génération de bibliothèques clientes](/help/forms/using/assets/clientlib_created.png)


   ![Emplacement de la bibliothèque cliente](/help/forms/using/assets/adaptiveform.theme.easel.png)

#### 4. Déployer le thème sur un environnement local {#deploy-the-theme-on-a-local-environment}

Pour déployer le thème dans votre environnement de développement ou de test local, procédez comme suit :

1. Copiez la bibliothèque cliente, créée dans la section précédente, dans votre projet Archetype, à l’emplacement suivant :

   `/ui.apps/src/main/content/jcr_root/apps/[AEM Archetype Project Folder]/clientlibs/<yourtheme>`

1. Ouvrez l’invite de commande ou le terminal.
1. Accédez au répertoire racine de votre projet AEM Archetype, le projet utilisé pour activer les composants principaux de formulaire adaptatif.
1. Exécutez la commande suivante pour déployer le thème personnalisé sur votre environnement :

   `mvn clean install`

   ![Version de bibliothèque cliente](/help/forms/using/assets/mvndeploy.png)

<!--

#### 5. Test the theme with a local Adaptive Form {#test-the-theme-with-a-local-adaptive-form}

To apply and test the customized theme with an Adaptive Form:

**Apply theme while creating an Adaptive Form**

1. Log in to your AEM Forms author instance. 

1. Tap **Adobe Experience Manager** > **Forms** > **Forms & Documents**.

1. Click **Create** > **Adaptive Forms**. The wizard for creating Adaptive Form opens.

1. Select the core component template in the **Source** tab.
1. Select the theme in the **Style** tab.
1. Click **Create**.

An Adaptive Form with the selected theme is created. 

**Apply theme to an existing Adaptive Form**

1. Log in to your AEM Forms author instance. 

1. Tap **Adobe Experience Manager** > **Forms** > **Forms & Documents**.

1. Select an Adaptive Form and click Properties. 

1. For the **Theme Client Library** option, select the theme. 

1. Click **Save & Close**.

The selected theme is applied to the Adaptive Form. 
-->

#### 5. Déployez un thème sur votre environnement de production {#deploy-theme}

Une fois que vous avez testé le thème sur votre environnement de développement local, vous pouvez continuer à déployer le thème sur vos environnements de production, y compris les instances d’auteur et de publication. Pour déployer le thème sur vos environnements de production, procédez comme suit :

1. Connectez-vous à votre environnement AEM.
1. Ouvrez le gestionnaire de modules. L’URL par défaut est `https://localhost:4502/crx/packmgr/index.jsp`.
1. Cliquez sur **Télécharger le module** et cliquez sur **Parcourir**.
1. Accédez à et sélectionnez `[AEM Archetype Project Folder]\all\target[appid].all-[version].zip`. Cliquez sur **Ouvrir**.
1. Cliquez sur Installer. Répétez l’étape sur tous les environnements de production.


Une fois le package installé, le thème peut être sélectionné.

![Bibliothèque cliente de thème](/help/forms/using/assets/themeclientlibrary.png)

>[!NOTE]
>
>
> Si vous rencontrez des difficultés pour accéder à la boîte de dialogue de connexion sur une instance de publication afin d’installer le module via le gestionnaire de modules, essayez de vous connecter à l’aide de l’URL suivante : `http://[Publish Server URL]:[PORT]/system/console`. Cela vous permet d’accéder à l’instance de publication et de poursuivre le processus d’installation.

## Application d’un thème à un formulaire adaptatif {#using-theme-in-adaptive-form}

Les étapes pour appliquer un thème à un formulaire adaptatif sont les suivantes :

1. Connectez-vous à votre instance d’auteur d’AEM locale.
1. Entrez vos informations d’identification dans la page de connexion d’Experience Manager. Appuyez sur **Adobe Experience Manager** > **Formulaires** > **Formulaires et documents**.
1. Cliquez sur **Créer** > **Formulaires adaptatifs**.
1. Sélectionnez un modèle de composants principaux de Forms adaptatif et cliquez sur **Suivant**. Le **Ajouter des propriétés** apparaît
1. Spécifiez la variable **Nom** pour votre formulaire adaptatif.


   >[!NOTE]
   >
   > * Par défaut, la variable `adaptiveform.theme.canvas3` Le thème est sélectionné.
   > * Vous pouvez choisir un thème différent dans la **Bibliothèque cliente du thème** menu déroulant.

1. Cliquez sur **Créer**.

Les thèmes de formulaire adaptatif sont utilisés dans le cadre d’un modèle de formulaire adaptatif pour définir le style lors de la création d’un formulaire adaptatif.

## Suppression d’un thème {#delete-a-theme}

Pour supprimer les thèmes inutilisés ou indésirables :

1. Connectez-vous à votre instance d’auteur .
1. Ouvrez `http://[Publish Server URL]:[PORT]/crx/de/index.jsp`.
1. Accédez à `apps/[AEM Archetype Project Folder]/clientlibs/[yourtheme]`.
1. Supprimez le dossier de thème et enregistrez les modifications.


## Questions fréquentes {#faq}

**Q :** Quelle personnalisation est la priorité lorsque vous effectuez des personnalisations dans un dossier de thème au niveau global et au niveau des composants ?

**Réponse :** Lorsqu’un style est défini aux niveaux du thème et du composant, le style défini au niveau du composant est prioritaire.

**Q :** Quelles sont les étapes à suivre si le thème personnalisé n’est pas visible dans la variable **[!UICONTROL Bibliothèque cliente du thème]**?

**Réponse :**  Si votre thème personnalisé n’apparaît pas dans la variable **[!UICONTROL Bibliothèque cliente du thème]** , procédez comme suit :

1. Accédez à l’emplacement où vous avez ajouté votre bibliothèque cliente de thèmes personnalisée. Le chemin recommandé est le suivant : `/ui.apps/src/main/content/jcr_root/apps[AEM Archetype Project Folder]/clientlibs/<yourtheme>`.

1. Ouvrez le `.content.xml` et incluez les métadonnées suivantes :

   ```
       formstheme:true
       allowproxy:true
   ```

1. Enregistrez le fichier et redéployez le thème.

## Voir également

* [Création d’un formulaire adaptatif basé sur des composants principaux](create-an-adaptive-form-core-components.md)
* [Utilisation de l’éditeur de règles pour ajouter un comportement dynamique au formulaire](rule-editor.md)
* [Création ou personnalisation de thèmes pour Forms adaptatif basé sur les composants principaux](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [Création d’un modèle pour le Forms adaptatif basé sur les composants principaux](template-editor.md)
* [Création ou ajout d’un formulaire adaptatif à une page AEM Sites ou à un fragment d’expérience](create-or-add-an-adaptive-form-to-aem-sites-page.md)

