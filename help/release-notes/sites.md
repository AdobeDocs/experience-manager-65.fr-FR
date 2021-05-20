---
title: Notes de mise à jour d’AEM Sites
description: Notes de mise à jour spécifiques à Adobe Experience Manager 6.5 Sites.
exl-id: 0bd0933c-f14d-4be2-9ad0-3f8207d7fa5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 63%

---

# Notes de mise à jour d’AEM Sites {#aem-sites-release-notes}

Lisez ce qui suit pour une description détaillée des améliorations d’AEM Sites 6.5 :

## Développement de composants et de modèles {#component-amp-template-development}

* Maven Project Archetype 18+ pour les nouveaux projets, accédez à [Github pour les notes de mise à jour](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases).
* Application monopage Maven Project Archetype 1.0.6+ pour les nouveaux projets, accédez à [Github pour les notes de mise à jour](https://github.com/adobe/aem-spa-project-archetype/releases).
* HTL version 1.4, accédez à [Github pour les notes de mise à jour](https://github.com/adobe/htl-spec/releases/tag/1.4).

   * Opérateur &quot;in&quot; pour les chaînes, les tableaux et les objets :

      ```html
      ${'a' in 'abc’}
      ${100 in myArray}
      ${'a' in myObject}
      ```

   * Déclarations de variables avec data-sly-set :
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * Paramètres de contrôle de liste et de répétition : début, étape, fin :
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * Identifiants pour data-sly-unwrap :

      ```html
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
      text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
      </div>
      ```

   * Prise en charge des nombres négatifs

* Core Components 2.3.2+, accédez à [Github pour les notes de mise à jour](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases).
* Système de grille pour le conteneur de mises en page, voir [Github](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid).
* Gestionnaire de bibliothèques clientes : Le compilateur de fermetures Google a été défini par défaut sur la minimisation des bibliothèques clientes JavaScript (l’ancienne valeur par défaut était Yahoo YUI) et Google Closure Compiler a été mis à jour vers la version v20190121.
* Éditeur de modèles et stratégies

   * Création et modification de modèles pour les applications monopages qui utilisent le SDK JS (également appelé éditeur de SPA)

* Pour le site de référence We.Retail 4.0, accédez à [Github pour les notes de mise à jour](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases).
* Kit d’outils pour mettre à niveau des sites existants afin d’exploiter les dernières fonctionnalités d’éditeur, voir [Référentiel Github](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM inclut la version 1.12.4 de la bibliothèque jQuery afin de fournir une compatibilité maximale avec le code personnalisé existant. Adobe a procédé à des modifications de façon à résoudre les problèmes de sécurité connus.

## Administration de sites {#site-administration}

* Le rail [Référence](/help/sites-authoring/author-environment-tools.md#references) comporte une nouvelle section permettant de répertorier les liens internes pointant vers la page sélectionnée. Cela s’avère utile lorsque vous envisagez de supprimer une page hors ligne ou de la supprimer, pour voir quelles pages doivent être ajustées avant de les mettre hors ligne.
* La [vue de liste](/help/sites-authoring/basic-handling.md#list-view) comporte une nouvelle colonne de workflow indiquant le statut de la page dans un workflow.
* Dans les [propriétés de la page](/help/sites-authoring/editing-page-properties.md), il est désormais possible de parcourir les ressources existantes en affectant une vignette à la page (onglet Vignette).

## Éditeur de page {#page-editor}

* Autorisez l’édition en contexte et la composition d’expériences d’application monopage avec des composants côté client React et Angular utilisant le SDK JS (également appelé éditeur de SPA)
* Le mode Génération de modèles automatique s’affiche uniquement si la page possède une page de modèle automatique configurée.

## Fragments de contenu et éditeur {#content-fragments-amp-editor}

* Nouveau rail [Annotations](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) dans l’éditeur de fragment de contenu permettant de faire des commentaires généraux et d’afficher des commentaires dans le texte (à afficher également dans le rail de la chronologie)
* Possibilité de définir le type de contenu par défaut d’un élément de texte multiligne dans un [modèle de fragment de contenu](/help/assets/content-fragments/content-fragments-models.md) sur du texte simple, du texte enrichi ou du markdown.
* Ajoutez des [commentaire/annotations](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) en sélectionnant le texte dans l’éditeur de texte enrichi (vue plein écran)
* [Comparaison des différentes versions](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) d’un fragment de contenu côte à côte via le rail Référence
* Le rapport sur le téléchargement des ressources affiche désormais des fragments de contenu en conséquence
* Ajoutez [la prise en charge des fragments de contenu à l’API HTTP Assets](/help/assets/assets-api-content-fragments.md) par l’intermédiaire de /api.json. Il existe des API pour créer, mettre à jour, lire et supprimer des fragments de contenu.

## Fragments d’expérience {#experience-fragments}

* Amélioration de l’indexation des [fragments d’expérience](/help/sites-authoring/experience-fragments.md) afin que leur contenu soit trouvé dans la recherche des pages où ils sont utilisés.
* L’option [Exporter vers la cible](/help/sites-administering/experience-fragments-target.md) permet désormais d’envoyer le fragment d’expérience sous forme de fichier JSON (HTML par défaut), ou les deux.

## Traduction {#translation}

* Simplifiez la création de projets de traduction à l’aide de Project Masters
* Simplifiez l’exécution des projets de traduction en définissant les tâches de traduction sur l’état approuvé par défaut.
* Autorisez la mise à jour des pages traduites avec des modifications dans la mémoire de traduction tierce
* Autorisez l’exportation de travaux de traduction au format JSON
* Mise à jour de l’intégration Microsoft Traduction pour utiliser l’API V3

## Gestion multisite (MSM, Multi-Site Management) {#multi-site-management-msm}

* Pour les configurations de déploiement qui utilisent PushOnModify, une meilleure gestion de l’opération de déplacement de page pour éviter des incohérences d’état
* La création d’une nouvelle page dans la structure de livecopy créera désormais par défaut une page autonome.
* Utilisation des fonctionnalités MSM dans les applications d’une seule page qui utilisent le SDK JS (également appelé Éditeur SPA)

## Lancements {#launches}

* Nouveau workflow de révision et d’approbation pour les lancements et possibilité de promouvoir uniquement les pages de lancement approuvées
* Ajout d’une [ option dans l’interface utilisateur permettant de choisir la suppression du lancement juste après l’étape de promotion](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

## Ciblage et simulation de contenu  {#content-targeting-simulation}

* Le code JavaScript de la couche de données ContextHub et du moteur de règles côté client a été mis à jour pour utiliser jQuery 3 par défaut.

## AEM et Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>Actuellement :
>
>* Seul `at.js 1.x` est pris en charge si vous utilisez Adobe Target comme moteur de ciblage dans AEM console Activités.
   >
   >
* `at.js. 1.x` et `at.js 2.x` sont pris en charge si vous utilisez l’exportation de fragments d’expérience vers Target et que vous exécutez des activités dans la console de Target.


* L’intégration Adobe Target peut désormais utiliser l’API Target Standard. Les versions précédentes d’AEM utilisent l’API HTTP Target Classic, désormais obsolète.
* Adobe Target `mbox.js` version 63 est incluse. Adobe recommande vivement de passer à la version `at.js` v1.x.
* `at.js` La version 1.5.0 est désormais incluse. Adobe vous recommande d’utiliser [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) pour provisionner `at.js` v1.x dans le site.

## AEM et Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` H.27.5 est inclus. Adobe vous recommande de passer à la mise en oeuvre `AppMeasurement.js`
* `AppMeasurement.js` v1.8.0 est inclus. Adobe recommande d’utiliser [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) pour configurer AppMeasurement.js dans le site.

## AEM et Commerce {#aem-commerce}

Les améliorations apportées à Commerce Integration Framework suivent un cycle de publication plus rapide depuis AEM 6.4. [En savoir plus ici](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/docs.html).

## Module complémentaire Communities {#communities-add-on}

Voir la [page de notes de mise à jour sur Communities](../release-notes/communities-release-notes.md)

## Module complémentaire Screens  {#screens-add-on}

* Utilisation des lancements pour planifier les futures modifications de contenu pour le contenu de signalétique
* Lecture mesurée dans un canal de séquence
* Création automatique d’une structure de projet à l’aide d’un fichier source, une feuille de calcul Excel par exemple.

Pour plus d’informations sur les modifications apportées à AEM Screens, voir les Notes de mise à jour du [Guide de l’utilisateur d’AEM Screens](https://docs.adobe.com/content/help/fr-FR/experience-manager-screens/user-guide/aem-screens-introduction.html).
