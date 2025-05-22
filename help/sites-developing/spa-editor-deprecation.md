---
title: Abandon de l’éditeur de SPA
description: Bien que l’éditeur de SPA reste pris en charge par Adobe, découvrez ce que sa dépréciation signifie pour votre projet et les options dont vous disposez pour les projets futurs.
feature: Developing
role: Admin, Architect, Developer
source-git-commit: bd29ae46ead836e16362ad3a9a63bb31548415ff
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 3%

---


# Abandon de l’éditeur de SPA {#spa-editor-deprecation}

Bien que l’éditeur de SPA reste pris en charge par Adobe, découvrez ce que sa dépréciation signifie pour votre projet et les options dont vous disposez pour les projets futurs.

## Résumé {#summary}

Adobe a abandonné l’éditeur de SPA avec la version [6.5.23 d’AEM 6.5](/help/release-notes/release-notes.md#spa-editor) ce qui signifie qu’aucune autre amélioration ou mise à jour ne sera apportée à ses SDK. Adobe vous incite à utiliser l’[éditeur universel](/help/sites-developing/universal-editor/introduction.md) pour tout nouveau projet découplé afin de tirer parti des dernières innovations d’AEM.

## Détails de l’obsolescence {#details}

L’obsolescence de l’éditeur de SPA **ne signifie pas sa suppression immédiate** et si vous disposez déjà d’implémentations, **vous pouvez continuer à l’utiliser tant qu’il répond à vos besoins.** Toutefois, gardez à l’esprit les implications suivantes de son abandon.

* À l’avenir, Adobe ne traitera que les problèmes P1 et P2 et les vulnérabilités de sécurité.
* Aucun autre développement, amélioration ou mise à jour ne sera apporté à ses SDK.

L’obsolescence signifie que les SDK suivants sont maintenant bloqués.

* [Archétype de projet AEM](https://github.com/adobe/aem-project-archetype/)
* [Code de projet SPA AEM](https://github.com/adobe/aem-spa-project-core)
* [Gestionnaire de modèles de page SPA AEM](https://github.com/adobe/aem-spa-page-model-manager)
* [Mappage du composant SPA AEM](https://github.com/adobe/aem-spa-component-mapping)
* [Composants React modifiables de SPA d’AEM.](https://github.com/adobe/aem-react-editable-components)
   * [Composants principaux AEM React](https://github.com/adobe/aem-react-core-wcm-components)
   * [Base des composants principaux AEM React](https://github.com/adobe/aem-react-core-wcm-components-base)
   * [SPA des composants principaux AEM React](https://github.com/adobe/aem-react-core-wcm-components-spa)
   * [Exemples de composants principaux React d’AEM](https://github.com/adobe/aem-react-core-wcm-components-examples)
* [Composants modifiables AEM SPA Angular](https://github.com/adobe/aem-angular-editable-components)
   * [Composants principaux AEM Angular](https://github.com/adobe/aem-angular-core-wcm-components)
   * [Base de composants principaux AEM Angular](https://github.com/adobe/aem-angular-core-wcm-components-base)
   * [SPA des composants principaux AEM Angular](https://github.com/adobe/aem-angular-core-wcm-components-spa)
   * [Exemples de composants principaux AEM Angular](https://github.com/adobe/aem-angular-core-wcm-components-examples)
* [Composants AEM SPA Vue modifiables](https://github.com/mavicellc/aem-vue-editable-components)

## Alternatives à l’éditeur de SPA {#alternatives}

Le remplacement le plus approprié pour l’éditeur de SPA dépend des besoins de vos projets.

* **[L’éditeur universel](/help/sites-developing/universal-editor/introduction.md)** est le meilleur remplacement direct de l’éditeur de SPA.
   * L’éditeur universel est également un éditeur visuel et a été conçu spécifiquement pour les implémentations découplées, incorporant toute l’expérience d’Adobe à partir de l’éditeur de SPA.
   * L’éditeur universel a également été [publié pour AEM as a Cloud Service](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction) et prend donc en charge les cas d’utilisation AMS et On-Prem en plus des Cloud Services.
* **[l’éditeur de fragment de contenu](/help/sites-developing/universal-editor/introduction.md)** est une alternative pour ceux qui préfèrent un éditeur basé sur les formulaires.
   * L’éditeur de fragment de contenu est mieux adapté lorsque votre contenu est structuré sous la forme de fragments de contenu plutôt que de pages.

La structuration du contenu avec des fragments de contenu n’exclut pas l’utilisation de l’éditeur universel comme éditeur visuel, et les deux éditeurs peuvent être utilisés ensemble.

## Migration vers l’éditeur universel {#migrate-ue}

L’éditeur universel offre de nombreux avantages, ce qui fait de la migration une solution idéale pour les nouveaux projets.

* **Modification visuelle :** comme pour l’éditeur de SPA, les auteurs et autrices peuvent modifier le contenu directement dans l’aperçu et voir instantanément comment leurs modifications affectent l’expérience du visiteur.
* **Préparation à l’avenir :** la feuille de route d’AEM donne la priorité à l’éditeur universel en tant qu’éditeur visuel. Son adoption garantit l’accès aux dernières innovations et améliorations.
* **Intégration plus simple :** aucun SDK spécifique à AEM n’est nécessaire pour utiliser l’éditeur universel, ce qui réduit le verrouillage de tech stack.
* **Apportez votre propre application :** l’éditeur universel prend en charge n’importe quelle structure ou architecture web, ce qui permet l’adoption sans nécessiter de refactorisation complexe.
* **Extensibilité :** l’éditeur universel bénéficie d’un cadre d’extension [ robuste,](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/extending) qui comprend des intégrations à GenAI, Workfront, etc.

Il n’existe pas de chemin de migration direct de l’éditeur de SPA vers l’éditeur universel. Cela est dû à des différences fondamentales entre les deux technologies.

* L’éditeur universel ne réintroduit pas de fonctionnalités telles que l’éditeur de modèles, le système de style ou la grille réactive.
   * Ces cas d’utilisation peuvent désormais être gérés plus efficacement avec des feuilles CSS et JS front-end allégées dans les projets Edge Delivery Services ou découplés.
* Comme l’éditeur universel est un éditeur en tant que service, il ne peut pas permettre aux personnes en charge de l’implémentation d’injecter des éléments CSS ou JS dans les boîtes de dialogue des composants.
   * Cela empêche la conversion automatique des boîtes de dialogue de composant à partir de l’éditeur de page.
   * Cela affecte de nombreux domaines des boîtes de dialogue, tels que les widgets personnalisés, la validation des champs, l’affichage/le masquage des règles et les personnalisations basées sur des modèles.

Compte tenu de ces différences techniques, Adobe recommande de :

* Gardez les sites d’éditeur de SPA existants tels quels, car la prise en charge se poursuit.
* Adoptez l’éditeur universel pour tous les nouveaux développements, y compris les nouveaux sites, sections ou pages.

Gardez à l’esprit que même s’il n’y a pas d’implémentation directe de certaines fonctionnalités de l’éditeur universel de SPA, il existe de nouvelles façons de résoudre les mêmes problèmes à l’aide de la nouvelle flexibilité de l’éditeur universel.

## Comparaison entre l’éditeur de SPA et l’éditeur universel {#spa-vs-ue}

L’éditeur universel offre beaucoup plus de liberté aux personnes qui mettent en œuvre des applications web, comme illustré dans ce diagramme.

![Comparaison des architectures de l’éditeur universel et de l’éditeur de SPA](assets/spa-editor-vs-ue.png)

|  | Éditeur de SPA | Éditeur universel |
|---|---|---|
| **Thème** | L’application doit implémenter la disposition avec la grille CSS d’AEM. | L’application peut utiliser n’importe quelle technique CSS moderne pour la mise en page. |
| **Rendu** | L’application doit suivre la structure de routage de l’éditeur de SPA. | L’application peut être mise en œuvre librement, sans règles ni modèles imposés à suivre. |
| **SDK** | La mise en œuvre doit intégrer étroitement le SDK. | Au niveau création, l’application charge uniquement `corlib.js` et indique à l’éditeur universel via les annotations d’HTML. |
| **Framework** | L’application doit utiliser une version prise en charge de React ou d’Angular. | L’application peut utiliser n’importe quel framework ou architecture. |
| **Hébergement** | L’application doit être hébergée sur un domaine AEM. | L’application peut être entièrement découplée et hébergée n’importe où. |
| **API** | L’application doit récupérer le contenu à partir de l’API `model.json`. | L’application peut utiliser n’importe quelle API, y compris des API personnalisées. |
| **Persistance** | L’éditeur de SPA prend uniquement en charge le contenu de page pour la modification visuelle. | L’éditeur universel prend en charge la modification visuelle des pages et des fragments de contenu de manière native. |
|  |  | L’éditeur universel peut être étendu pour modifier du contenu externe avec les mêmes fonctionnalités visuelles. |
|  | Les développeurs doivent déployer les modèles et les `cq:Dialog` Sling dans AEM. | Les développeurs ont besoin de peu ou pas d’expérience AEM et n’ont pas besoin d’écrire de code Java. |
