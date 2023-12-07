---
title: Introduction à la personnalisation de l’espace de travail AEM Forms
description: Une présentation rapide, avec des informations conceptuelles et techniques, pour personnaliser l’espace de travail AEM Forms LiveCycle pour la gestion des processus.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: b183d42f-343c-4acb-bc73-f80ad72e54df
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1752'
ht-degree: 33%

---

# Introduction à la personnalisation de l’espace de travail AEM Forms{#introduction-to-customizing-aem-form-workspace}

L’espace de travail AEM Forms offre des fonctionnalités permettant de modifier la sémantique de la présentation et la fonctionnalité de son interface. Les types de personnalisations pour modifier le style, la mise en page, le formatage, la marque et les principales fonctionnalités sont décrits ci-dessous.

![cu_customized_workspace_example](assets/cu_customized_workspace_example.png)

Exemple d’espace de travail personnalisé

## Types de personnalisations {#types-of-customizations}

L’espace de travail AEM Forms prend en charge un large éventail de personnalisations pour mettre à jour la mise en page de l’interface utilisateur, son aspect, sa fonctionnalité et bien plus encore. Les personnalisations impliquent la mise à jour d’un ou de plusieurs des éléments suivants :

* Apparences de l’interface utilisateur
* Fonctionnalité utilisant des personnalisations sémantiques
* Réutilisation de composants de HTML dans d’autres applications

### Modifications de l’interface utilisateur {#user-interface-changes}

Vous pouvez modifier l’aspect, la mise en page et la sémantique d’une autre présentation de l’espace de travail AEM Forms. Modifiez l’espace de travail en personnalisant le CSS, les modèles HTML et les fichiers JavaScript™. Tous les fichiers par défaut sont fournis dans l’installation par défaut.

Les étapes applicables les plus courantes sont décrites dans [Procédure générique de personnalisation de l’espace de travail AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). Pour obtenir des exemples spécifiques de ces personnalisations, y compris les étapes détaillées, reportez-vous aux articles connexes à la fin de cet article.

#### Présentation de la feuille de style {#understanding-the-style-sheet}

Avant de personnaliser Workspace, familiarisez-vous avec la feuille de style par défaut fournie avec AEM Forms à l’adresse /libs/ws/css/style.css.

Pour personnaliser l’espace de travail, il est recommandé de vous familiariser avec la feuille de style existante, style.css, dans le dossier /libs/ws/css. Vous trouverez ci-dessous quelques composants importants.

<table>
 <tbody>
  <tr>
   <th><p>Elément CSS</p> </th>
   <th><p>Composant de l’interface utilisateur modifié</p> </th>
  </tr>
  <tr>
   <td><p>#header</p> </td>
   <td><p>En-tête de l’espace de travail AEM Forms</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList</p> </td>
   <td><p>Liste des catégories</p> </td>
  </tr>
  <tr>
   <td><p>.categoryList .header</p> </td>
   <td><p>En-tête de liste de catégories</p> </td>
  </tr>
  <tr>
   <td><p>.categories, .filters</p> </td>
   <td><p>Espace sous la liste des catégories</p> </td>
  </tr>
  <tr>
   <td><p>.category, .filter</p> </td>
   <td><p>Catégorie</p> </td>
  </tr>
  <tr>
   <td><p>.category:hover, .category.selected, .filter:hover, .filter.selected</p> </td>
   <td><p>Catégorie sélectionnée et style de survol de la souris de la catégorie</p> </td>
  </tr>
  <tr>
   <td><p>categoryListBar .tool, categoryListBar .content</p> </td>
   <td><p>Page de démarrage du processus (liste de catégories fermée)</p> </td>
  </tr>
  <tr>
   <td><p>filterListBar .tool, filterListBar .content</p> </td>
   <td><p>Page Tâches (liste des filtres fermée)</p> </td>
  </tr>
  <tr>
   <td><p>processNameListBar .tool, processNameListBar .content</p> </td>
   <td><p>Page de suivi (liste de noms de processus fermée)</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList, .tasklist</p> </td>
   <td><p>La liste des points de départ ou la liste des tâches</p> </td>
  </tr>
  <tr>
   <td><p>.startPointList .header, .tasklist .header</p> </td>
   <td><p>En-tête d’une liste de points de départ ou d’une liste de tâches</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected, .task.selected</p> </td>
   <td><p>Point de départ ou tâche sélectionné</p> </td>
  </tr>
  <tr>
   <td><p>.startpoint.selected.description, .task.selected.description</p> </td>
   <td><p>Description du point de départ ou de la tâche sélectionné</p> </td>
  </tr>
  <tr>
   <td><p>#taskarea</p> </td>
   <td><p>Zone de tâche</p> </td>
  </tr>
  <tr>
   <td><p>#header .dropdown</p> </td>
   <td><p>Liste déroulante utilisateur dans l’en-tête</p> </td>
  </tr>
  <tr>
   <td><p>.sortDrop dd ul</p> </td>
   <td><p>Menu déroulant de la tâche de tri</p> </td>
  </tr>
 </tbody>
</table>

#### CSS {#css}

L’espace de travail AEM Forms emprunte son apparence à un fichier CSS. En personnalisant le CSS, vous pouvez modifier la sémantique de présentation de l’espace de travail, comme les polices, les couleurs, la marque et la mise en page.

Les étapes de niveau supérieur pour la personnalisation CSS sont les suivantes :

* Créez un fichier CSS.
* Ajoutez des éléments de style dans ce fichier CSS. Pour plus d’informations, voir Présentation des styles CSS .
* Mettez ses références à jour dans `html.jsp`.

Pour connaître les étapes exactes permettant d’effectuer ces personnalisations, voir la [Procédure générique de personnalisation de l’espace de travail AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). Le fichier CSS fourni avec l’espace de travail AEM Forms se trouve sous /libs/ws/css/. Pour les personnalisations CSS, utilisez le [Ship Package](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p). Pour obtenir des exemples spécifiques de personnalisations CSS, reportez-vous aux rubriques d’aide connexes à la fin de cet article.

#### Image {#image}

Vous pouvez personnaliser l’espace de travail AEM Forms pour ajouter des avatars d’utilisateurs ou pour ajouter le logo de votre entreprise. Pour ces personnalisations, utilisez [Ship Package](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p).

Les étapes de niveau supérieur pour la personnalisation des images sont les suivantes :

* Installez et configurez WebDAV.
* Ajoutez de nouvelles images.
* Ajoutez de nouveaux styles correspondant aux images ajoutées.
* Etablissez le lien vers le nouveau fichier CSS dans le fichier `html.jsp`.

Pour vous familiariser avec la personnalisation des images dans l’espace de travail AEM Forms, suivez la [Procédure générique de personnalisation de l’espace de travail AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md). Pour obtenir des exemples spécifiques de personnalisations liées aux images, reportez-vous aux rubriques d’aide connexes à la fin de cet article.

#### Modèle de HTML {#html-template}

Les modèles HTML permettent de définir l’aspect et la mise en page de l’interface utilisateur de l’espace de travail. En mettant à jour les modèles de HTML par défaut, vous pouvez personnaliser l’interface utilisateur par défaut de la mise en page.

Les étapes de niveau supérieur pour les personnalisations du modèle de HTML sont les suivantes :

* Dans un dossier créé par l’utilisateur, effectuez des copies des fichiers par défaut requis.
* Ajoutez de nouveaux modèles dans un dossier défini par l’utilisateur.
* Effectuez les mises à jour appropriées vers les fichiers copiés, par exemple, le chemin d’accès du nouveau modèle.

Vous trouverez des exemples spécifiques de ces personnalisations dans les rubriques d’aide fournies à la fin de cet article. Choisissez parmi les [Ship Package](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p) ou le [Package de développement](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p), selon le modèle à personnaliser.

### Modifications sémantiques {#semantic-changes}

Pour modifier la fonctionnalité de l’espace de travail AEM Forms, changez le code source JavaScript. Les modifications dans les principales fonctionnalités ne sont pas libellées comme modifications sémantiques. Vous pouvez modifier des modèles, des vues et des modèles fournis dans le cadre du code source de l’espace de travail AEM Forms.

Les étapes de niveau supérieur permettant d’effectuer des modifications sémantiques afin de modifier la fonctionnalité de l’espace de travail AEM Forms sont les suivantes :

* Dans un dossier créé par l’utilisateur, effectuez des copies des fichiers par défaut appropriés.
* Ajoutez de nouveaux modèles et vues dans le dossier défini par l’utilisateur.
* Effectuez les mises à jour appropriées, telles que la mise à jour des chemins d’accès des modèles et des vues nouvellement ajoutés dans les fichiers JavaScript par défaut.
* Minifiez le module pour optimiser les performances.

Pour plus d’informations conceptuelles sur les composants qui font partie du code source, voir [Description des composants réutilisables](/help/forms/using/description-reusable-components.md). Pour ces personnalisations, utilisez le module de développement.

### Composants réutilisables {#reusable-components}

Comme l’espace de travail AEM Forms est un logiciel basé sur des composants, il peut être facilement personnalisé et réutilisé. Vous pouvez intégrer facilement les composants de l’espace de travail avec vos applications Web.

Pour plus d’informations conceptuelles, voir la [Description des composants réutilisables](/help/forms/using/description-reusable-components.md) et pour obtenir des instructions sur l’utilisation des composants, voir [Intégrer des composants de l’espace de travail AEM Forms à des applications web](/help/forms/using/description-reusable-components.md).

## Création du code de l’espace de travail AEM Forms {#building-html-workspace-code}

### Package SDK {#sdk-package}

Le package contient le code source de l’espace de travail AEM Forms. Le package est disponible à l’adresse `[LC root]\sdk\html-workspace\adobe-lc-workspace-src.zip`.

Il est principalement destiné aux personnalisations, car il permet de générer les éléments suivants :

* Packages CRX pour les profils Ship, Debug et Dev (mentionnés ci-dessous dans [Packages CRX](../../forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)).
* Version minimisée du code personnalisé (pour les modifications sémantiques).

#### Contenu WS {#ws-content}

* client-pkg :

   * src : contient les artefacts nécessaires pour créer des noeuds CRX.
   * pom.xml - Script pour créer des packages de déploiement pour divers profils WS-Deploy Package

* client-html :

   * assembly - contient le fichier zip.xml utilisé par le script pour créer le SDK de l’espace de travail AEM Forms.
   * src/main/webapp -

      * css : contient des feuilles de style pour l’espace de travail AEM Forms.
      * images : contient les images utilisées dans l’espace de travail AEM Forms.
      * js:

         * libs : contient toutes les bibliothèques tierces utilisées dans l’espace de travail AEM Forms.
         * licences : contient des licences pour les fichiers HTML et JS, ainsi que du code pour préfixer ces licences en fonction des fichiers sources respectifs.
         * minifier - utilisé pour la combinaison, la minification et la laidification du code JavaScript personnalisé.
         * resourcejs_optimizer - utilisé pour la combinaison, la minification de code source javascript et l’utilisation de Uglifier.
         * resource_generator - utilisé pour générer register.js et modelcontrollerpath.js.
         * runtime:

            * initializer : contient initializer.js utilisé pour initialiser les vues Backbone et les modèles utilisés dans l’espace de travail AEM Forms.
            * models : contient les modèles Backbone de tous les composants présents dans l’espace de travail AEM Forms.
            * routes - contient les fichiers JavaScript et HTML qui chargent les composants Démarrer le processus, Tâches, Suivi et Préférences dans l’espace de travail AEM Forms.
            * services : contient le fichier service.js utilisé dans l’espace de travail AEM Forms. Tous les appels au serveur sont effectués via service.js.
            * templates - contient tous les modèles, c’est-à-dire les fichiers de HTML de toutes les vues dans l’espace de travail AEM Forms.
            * util - contient tous les fichiers d’utilitaire (javascript) utilisés dans l’espace de travail AEM Forms.
            * views : contient les vues Backbone de tous les composants dans l’espace de travail AEM Forms.

         * main.js
         * router.js

      * libs/ws: pdf.html et pluginPing.pdf sont utilisés pour le chargement des formulaires PDF dans l’espace de travail AEM Forms et WSNextAdapter.swf est utilisé pour charger des formulaires SWF et des guides dans l’espace de travail AEM Forms.
      * locales :

         * de-DE : contient translation.json pour l’allemand.
         * en-US : contient translation.json pour l’anglais.
         * fr-FR : contient translation.json pour le français.
         * ja-JP : contient translation.json pour le japonais.
         * html.jsp : contient le code permettant de connaître les paramètres régionaux actuels du navigateur.

      * html.jsp
      * GET.jsp

### Package CRX {#crx-package}

Le package CRX peut être déployé sur le référentiel CRX™. Il se trouve sous `[LC root]\crx-repository\install\adobe-lc-workspace-pkg.zip`.

Ce package peut être créé à l’aide des trois profils décrits ci-dessous.

| **Profil** | **Description** | **Utilisation** |
|---|---|---|
| Profil Ship | Ce profil crée un package CRX de la plus petite taille possible à l’aide de la minification. Ce package est le plus efficace. Tous les fichiers JavaScript™ sont combinés et minimisés en un seul fichier JS. | Utilisez ce profil lorsqu’aucune autre modification sémantique n’est requise dans les fichiers JS. |
| Profil de débogage | Ce profil crée un package CRX modérément efficace. La taille du package est légèrement supérieure à celle du paquet créé à l’aide du profil Ship. Ce package contient la plupart des fichiers JavaScript combinés en un seul fichier JS. | Utilisez ce profil pour le débogage. |
| Profil de développement | Ce profil crée un package CRX de la plus grande taille possible. Tous les fichiers JavaScript sont disponibles séparément, car ils se trouvent dans le package SDK. | Utilisez ce profil lors de l’incorporation de modifications sémantiques. |

#### Profil Ship {#ship-profile}

#### Commande {#command}

* mvn clean -P Ship install sur le dossier client-pkg du package source fourni au client.
* L’exécution de la commande du profil Ship fonctionne uniquement sur un JVM de 64 bits.

#### Contenu WS {#ws-content-1}

* css : contient style.css, ie.css et jquery-ui.css.
* images : contient toutes les images.
* js:

   * libs:

      * require : contient require.js.
      * jqueryui - Contient jquery.ui.datepicker.ja.js.

   * runtime:

      * templates - contient tous les modèles, c’est-à-dire les fichiers de HTML de tous les composants dans l’espace de travail AEM Forms.

   * main.js (combiné, minimisé et unifié).
   * registry.js

* libs:

   * ws - contient pluginPing.pdf, pdf.html et WSNextAdapter.swf.

* Paramètres régionaux : contient .content.xml.
* locales :

   * de-DE : contient translation.json pour l’allemand.
   * en-US : contient translation.json pour l’anglais.
   * fr-FR : contient translation.json pour le français.
   * ja-JP : contient translation.json pour le japonais.
   * html.jsp : contient le code permettant de connaître les paramètres régionaux actuels du navigateur.

* Index : contient .content.xml
* profile : contient offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Debug Profile {#debug-profile}

#### Commande {#command-1}

* mvn clean -P Debug install sur client-pkg
* L’exécution de la commande de profil de débogage fonctionne uniquement sur JVM 64 bits.

#### Contenu WS {#ws-content-2}

* css : contient style.css, ie.css et jqueri-ui.css.
* images : contient toutes les images.
* js:

   * libs:

      * require : contient require.js.
      * jqueryui - Contient jquery.ui.datepicker.ja.js.

   * runtime:

      * templates - contient tous les modèles, c’est-à-dire les fichiers de HTML de tous les composants dans l’espace de travail AEM Forms.

   * main.js (combiné).
   * registry.js

* libs:

   * ws - contient pluginPing.pdf, pdf.html et WSNextAdapter.swf.

* Paramètres régionaux : contient .content.xml.
* locales :

   * de-DE : contient translation.json pour l’allemand.
   * en-US : contient translation.json pour l’anglais.
   * fr-FR : contient translation.json pour le français.
   * ja-JP : contient translation.json pour le japonais.
   * html.jsp : contient le code permettant de connaître les paramètres régionaux actuels du navigateur.

* Index : contient .content.xml
* profile : contient offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml

#### Profil Dev {#dev-profile}

#### Commande {#command-2}

mvn clean -P Dev install sur client-pkg

#### Contenu WS {#ws-content-3}

* css : contient style.css, ie.css et jqueri-ui.css.
* images : contient toutes les images.
* js:

   * libs : contient toutes les bibliothèques utilisées dans l’espace de travail AEM Forms.
   * require : contient require.js.
   * jqueryui - Contient jquery.ui.datepicker.ja.js
   * runtime:

      * initializer : contient initializer.js et modelcontroller erpath.js.
      * models : contient les modèles de tous les composants dans l’espace de travail AEM Forms.
      * routes - contient les fichiers JavaScript et HTML qui chargent les composants Démarrer le processus, Tâches, Suivi et Préférences dans l’espace de travail AEM Forms.
      * services : contient le fichier service.js utilisé dans l’espace de travail AEM Forms.
      * templates - contient tous les modèles, c’est-à-dire les fichiers de HTML de tous les composants dans l’espace de travail AEM Forms.
      * util - contient tous les fichiers d’utilitaire (JavaScript) utilisés dans l’espace de travail AEM Forms.
      * views - contient des vues de tous les composants dans l’espace de travail AEM Forms.

   * main.js
   * registry.js
   * router.js

* libs:

   * ws - contient pluginPing.pdf, pdf.html et WSNextAdapter.swf.

* Paramètres régionaux : contient .content.xml.
* locales :

   * de-DE : contient translation.json pour l’allemand.
   * en-US : contient translation.json pour l’anglais.
   * fr-FR : contient translation.json pour le français.
   * ja-JP : contient translation.json pour le japonais.
   * html.jsp : contient le code permettant de connaître les paramètres régionaux actuels du navigateur.

* Index : contient .content.xml
* profile : contient offline.jsp.
* GET.jsp
* html.jsp
* content.xml
* _rep_policy.xml
