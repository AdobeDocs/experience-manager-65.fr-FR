---
title: Aperçu de l’éditeur d’application d’une seule page
seo-title: Aperçu de l’éditeur d’application d’une seule page
description: Cet article présente un aperçu complet de l’éditeur d’application d’une seule page et explique son fonctionnement. Il présente notamment des processus détaillés d’interaction de l’éditeur d’application d’une seule page dans AEM.
seo-description: Cet article présente un aperçu complet de l’éditeur d’application d’une seule page et explique son fonctionnement. Il présente notamment des processus détaillés d’interaction de l’éditeur d’application d’une seule page dans AEM.
uuid: c283abab-f5bc-414a-bc81-bf3bdce38534
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 06b8c0be-4362-4bd1-ad57-ea5503616b17
docset: aem65
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# Aperçu de l’éditeur d’application d’une seule page{#spa-editor-overview}

Les applications d’une seule page (SPA) peuvent améliorer considérablement l’expérience des utilisateurs de sites web. Le souhait des développeurs est de pouvoir créer des sites avec des structures SPA. Les auteurs, pour leur part, souhaitent modifier facilement du contenu dans AEM pour un site conçu à l’aide de telles structures.

L’éditeur de SPA constitue une solution complète pour la prise en charge des SPA dans AEM. Cette page fournit un aperçu de la structure de la prise en charge des SPA dans AEM, du fonctionnement de l’éditeur de SPA et de la synchronisation entre la structure SPA et AEM.

>[!NOTE]
>
>L’éditeur d’application d’une seule page est la solution recommandée pour les projets nécessitant un rendu côté client basé sur la structure d’application d’une seule page (par exemple, Réagir ou Angulaire).

## Présentation {#introduction}

Les sites créés à l’aide de structures SPA courantes, telles que React et AngularJS, chargent leur contenu via le format JSON dynamique et ne fournissent pas la structure HTML dont l’éditeur de page AEM a besoin pour passer des commandes de modification.

Pour activer la modification d’applications d’une seule page dans AEM, il faut qu’il y ait une correspondance entre la sortie JSON de l’application et le modèle de contenu dans le répertoire AEM afin d’enregistrer les modifications apportées au contenu.

La prise en charge des applications d’une seule page dans AEM s’accompagne d’une fine couche JS qui interagit avec le code JS de l’application lorsqu’elle est chargée dans l’éditeur de pages avec lequel des événements peuvent être envoyés. L’emplacement des commandes d’édition peut être activé pour permettre une modification en contexte. Cette fonction repose sur le concept de point de terminaison de l’API Content Services, étant donné que le contenu de l’application d’une seule page doit être chargé par le biais de Content Services.

Pour de plus amples informations sur les SPA dans AEM, consultez les documents suivants :

* [Plan directeur de SPA](/help/sites-developing/spa-blueprint.md) pour connaître les exigences techniques d’une SPA
* [Prise en main des SPA dans AEM](/help/sites-developing/spa-getting-started-react.md) pour une présentation rapide d’une SPA simple

## Concevoir {#design}

Le composant de page d’une application d’une seule page ne fournit pas les composants HTML de ses composants enfants via le fichier HTL ou JSP. Cette opération est déléguée à la structure SPA. La représentation des composants ou du modèle enfant est récupérée sous forme de structure de données JSON du JCR. Les composants SPA sont ensuite ajoutés à la page en fonction de cette structure. Ce comportement permet de différencier la composition initiale du corps du composant de page à partir d’équivalents non SPA.

### Gestion du modèle de page {#page-model-management}

The resolution and the management of the page model is delegated to a provided `PageModel` library. L’application d’une seule page doit utiliser la bibliothèque de modèles de page pour être initialisée et créée par l’éditeur d’applications d’une seule page. La bibliothèque de modèle de page est fournie indirectement au composant de page AEM via le npm `cq-react-editable-components`. Le modèle de page est un interpréteur entre AEM et l’application d’une seule page. Par conséquent, elle doit toujours être présente. Lorsque la page est créée, une bibliothèque supplémentaire `cq.authoring.pagemodel.messaging` doit être ajoutée afin de permettre la communication avec l’éditeur de page.

Si le composant de page SPA hérite du composant principal de la page, deux options sont possibles pour faire en sorte que la catégorie de la bibliothèque cliente `cq.authoring.pagemodel.messaging` soit disponible :

* Si le modèle est modifiable, ajoutez-le à la stratégie de page.
* Vous pouvez également ajouter les catégories via `customfooterlibs.html`.

Pour chaque ressource du modèle exporté, l’application d’une seule page met en correspondance un composant réel qui effectue le rendu. Le modèle, représenté par JSON, est ensuite rendu à l’aide des mappages de composants dans un conteneur.
![screen_shot_2018-08-20at144152](assets/screen_shot_2018-08-20at144152.png)

>[!CAUTION]
>
>The inclusion of the `cq.authoring.pagemodel.messaging` category should be limited to the context of the SPA Editor.

### Type de données de communication {#communication-data-type}

When the `cq.authoring.pagemodel.messaging` category is added to the page, it will send a message to the Page Editor to establish the JSON communication data type. Lorsque le type de données de communication est défini sur JSON, les requêtes GET communiquent avec les points de terminaison du modèle Sling d’un composant. À la suite d’une mise à jour dans l’éditeur de page, la représentation JSON du composant mis à jour est envoyée à la bibliothèque modèle de page. Celle-ci informe ensuite l’application d’une seule page des mises à jour.

![screen_shot_2018-08-20at143628](assets/screen_shot_2018-08-20at143628.png)

## Processus {#workflow}

Vous pouvez comprendre le flux d’interaction entre l’application d’une seule page et AEM en considérant l’éditeur d’une seule page comme un médiateur entre les deux.

* La communication s’effectue au format JSON au lieu du format HTML.
* L’éditeur de page fournit la dernière version du modèle de page à l’application d’une seule page par le biais de l’API de messagerie et de l’iFrame.
* Le gestionnaire de modèles de pages informe l’éditeur qu’il est prêt pour le montage et transmet le modèle de page sous la forme d’une structure JSON.
* L’éditeur ne modifie pas la structure DOM de la page en cours de création ; en fait, il n’y accède même pas. Au lieu de cela, il fournit le modèle de page le plus récent.

![screen_shot_2018-08-20at144324](assets/screen_shot_2018-08-20at144324.png)

### Processus de l’éditeur SPA de base {#basic-spa-editor-workflow}

En gardant à l’esprit les éléments clés de l’éditeur d’application d’une seule page, le flux de travail général de modification d’une application d’une seule page dans AEM s’affiche comme suit pour l’auteur.

![untitled1](assets/untitled1.gif)

1. L’éditeur d’application d’une seule page se charge.
1. L’application d’une seule page est chargée dans un cadre distinct.
1. L’application d’une seule page demande du contenu JSON et effectue le rendu des composants côté client.
1. SPA Editor détecte les composants rendus et génère des incrustations.
1. L’auteur clique sur l’incrustation et affiche la barre d’outils de modification du composant.
1. L’éditeur d’applications monopages (SPA Editor) conserve les modifications avec une requête POST envoyée au serveur.
1. L’éditeur d’application d’une seule page demande à JSON d’être mis à jour vers l’éditeur d’application d’une seule page, qui est envoyé à l’application avec un événement DOM.
1. L’application d’une seule page effectue le rendu du composant concerné, en mettant à jour son DOM.

>[!NOTE]
>
>N’oubliez pas :
>
>* Le SPA est toujours responsable de son affichage.
>* L’éditeur SPA est isolé de l’application SPA elle-même.
>* En production (publication), l’éditeur d’application d’une seule page n’est jamais chargé.
>



### Processus de montage de page client-serveur {#client-server-page-editing-workflow}

Il s’agit d’un aperçu plus détaillé de l’interaction client-serveur lors de la modification d’une application d’une seule page.

![page_editor_spa_authingmediator-2](assets/page_editor_spa_authoringmediator-2.png)

1. L’application d’une seule page s’initialise et demande le modèle auprès de l’exportateur de modèle Sling.
1. À son tour, l’exportateur demande au référentiel les ressources qui composent la page.
1. Le référentiel renvoie alors les ressources demandées.
1. L’exportateur de modèle Sling renvoie le modèle de la page.
1. L’application d’une seule page instancie ses composants sur la base du modèle de page.
1. **6a** Le contenu informe l’éditeur qu’il est prêt pour la création.

   **6b** L’éditeur de page demande les configurations de création du composant.

   **6c** L’éditeur de page reçoit les configurations de composant.
1. Lorsque l’auteur modifie un composant, l’éditeur de page envoie une demande de modification au servlet POST par défaut.
1. La ressource est mise à jour dans le référentiel.
1. La ressource mise à jour est fournie au servlet POST.
1. Le servlet POST par défaut informe l’éditeur de page que la ressource a été mise à jour.
1. L’éditeur de page demande le nouveau modèle de page.
1. Les ressources qui composent la page font l’objet d’une demande auprès du référentiel.
1. Les ressources qui composent la page sont fournies à l’exportateur de modèle Sling par le référentiel.
1. Le modèle de page mis à jour est renvoyé à l’éditeur.
1. L’éditeur de page met à jour la référence de modèle de page de l’application d’une seule page.
1. L’application d’une seule page met à jour ses composants en fonction de la nouvelle référence de modèle de page.
1. Les configurations de composant des éditeurs de page sont mises à jour.

   **17a** L’application d’une seule page signale à l’éditeur de page que le contenu est prêt.

   **17b** L’éditeur de page fournit les configurations de composant à l’application d’une seule page.

   **17c** L’application d’une seule page fournit des configurations de composant mises à jour.

### Processus de création {#authoring-workflow}

Il s’agit d’un aperçu plus détaillé axé sur l’expérience de création.

![spa_content_authingmodel](assets/spa_content_authoringmodel.png)

1. L’application d’une seule page récupère le modèle de page.
1. **2a** Le modèle de page fournit à l’éditeur les données requises pour la création.

   **2b** Une fois informé, l’orchestrateur de composants met à jour la structure de contenu de la page.
1. L’orchestrateur de composants interroge le mappage entre le type de ressource AEM et un composant SPA.
1. L’orchestrateur de composants instancie, de manière dynamique, le composant SPA sur la base du mappage entre le modèle de page et le composant.
1. L’éditeur de page met à jour le modèle de page.
1. **6a** Le modèle de page fournit des données de création mises à jour à l’éditeur de page.

   **6b** Le modèle de page distribue les modifications à l’orchestrateur de composants.
1. L’orchestrateur de composants récupère le mappage de composant.
1. L’orchestrateur de composants met à jour le contenu de la page.
1. Une fois que l’application d’une seule page a terminé la mise à jour du contenu de la page, l’éditeur de page charge l’environnement de création.

## Conditions requises et limites {#requirements-limitations}

Pour permettre à l’auteur d’utiliser l’éditeur de page pour modifier le contenu d’une application d’application d’une seule page, vous devez mettre en oeuvre votre application d’application d’une seule page pour interagir avec le SDK de l’éditeur d’applications d’une seule page. Consultez le document [Prise en main des applications monopages dans AEM](/help/sites-developing/spa-getting-started-react.md) pour obtenir le minimum de connaissances nécessaires à l’exécution de votre application.

### Structures prises en charge {#supported-frameworks}

Le SDK SPA Editor prend en charge les versions minimales suivantes :

* Réaction 16.3
* Angular 6.x

Les versions précédentes de ces structures peuvent fonctionner avec le SDK d’AEM SPA Editor, mais ne sont pas prises en charge.

### Cadres supplémentaires {#additional-frameworks}

D’autres infrastructures d’application d’une seule page peuvent être mises en oeuvre pour fonctionner avec le SDK d’AEM SPA Editor. Consultez le document [SPA Blueprint](/help/sites-developing/spa-blueprint.md) pour connaître les exigences qu’une structure doit satisfaire pour créer une couche spécifique à la structure composée de modules, de composants et de services pour travailler avec l’éditeur d’application d’application d’une seule page.

### Restrictions {#limitations}

Le SDK AEM SPA Editor a été introduit avec le Service Pack 2 d’AEM 6.4. Il est entièrement pris en charge par Adobe et, en tant que nouvelle fonctionnalité, il continue d’être amélioré et étendu. Les fonctionnalités AEM suivantes ne sont pas encore prises en charge par l’éditeur d’applications monopages :

* Mode cible
* ContextHub
* Modification d’images intégrées
* Modifier les configurations (ex. écouteurs)
* Système de style
* Annuler/rétablir
* Différence de page et déformation temporelle
* Fonctionnalités de réécriture HTML côté serveur, telles que le vérificateur de liens, le service de réécriture CDN, le raccourcissement d’URL, etc.
* Mode Développeur
* Lancements d’AEM
