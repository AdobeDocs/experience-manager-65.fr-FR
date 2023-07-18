---
title: Facultatif - Comment créer des applications d’une seule page (SPA) avec Adobe Experience Manager
description: Dans cette suite facultative du Parcours de développement Adobe Experience Manager (AEM) sans interface utilisateur, vous découvrez comment AEM peut combiner une diffusion sans interface avec des fonctionnalités CMS en pile complète traditionnelles et comment créer des données modifiables à l’aide de la structure de l’éditeur d’.
exl-id: 91eadda2-b881-4e4a-867f-8c5c54e8f8b4
source-git-commit: d3c40d1452217983b01245ec1c81111a3c4e7295
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 63%

---

# Comment créer des applications sur une seule page (SPA) avec AEM {#create-spa}

Dans cette suite facultative de la [AEM Parcours de développement sans affichage,](overview.md) vous découvrez comment Adobe Experience Manager (AEM) peut combiner une diffusion sans interface avec des fonctionnalités CMS en pile complète traditionnelles et comment créer des SPA modifiables à l’aide de la structure d’éditeur d’ et intégrer des  externes, en activant les fonctionnalités d’édition selon les besoins.

## Un peu d’histoire...  {#story-so-far}

À ce stade, vous devriez avoir terminé l’ensemble du [Parcours de développement découplé AEM](overview.md) et comprendre les principes de base de la diffusion découplée dans AEM, ainsi que les éléments suivants :

* La différence entre la diffusion de contenu couplé et découplé
* Les fonctionnalités découplées AEM
* Comment organiser un projet découplé AEM
* Comment créer du contenu découplé dans AEM
* Comment récupérer et mettre à jour du contenu découplé dans AEM
* La mise en ligne d’un projet découplé AEM

Vous avez donc soit mis en ligne avec votre premier projet découplé AEM, soit vous disposez de toutes les connaissances nécessaires pour le faire. Félicitations !

Alors pourquoi lire cette section supplémentaire et facultative du parcours ? Vous vous souvenez sans doute que dans la [Prise en main](getting-started.md#integration-levels) nous avons discuté brièvement de la manière dont AEM prend non seulement en charge la livraison sans interface utilisateur et les modèles traditionnels de pile complète, mais peut également prendre en charge les modèles hybrides qui combinent les avantages des deux. Bien qu’il ne s’agisse pas de modèles découplés classiques, de tels modèles hybrides peuvent offrir une flexibilité sans précédent à certains projets.

Cet article s’appuie sur vos connaissances d’AEM sans affichage en explorant en profondeur la manière dont vous pouvez créer vos propres applications d’une seule page (SPA) modifiables dans l’Adobe Experience Platform. Ainsi, vous pouvez créer du contenu et le diffuser intégralement vers un SPA, mais ce SPA reste modifiable dans l’.

## Objectif {#objective}

Ce document vous aide à comprendre comment les applications d’une seule page sont développées à l’aide du cadre de l’éditeur de SPA AEM. Après avoir lu ce document, vous devriez :

* comprendre la fonction de base de l’éditeur de SPA ;
* connaître les exigences relatives à la création d’une SPA entièrement modifiable pour AEM ;
* comprendre comment les SPA externes peuvent être intégrées à AEM ;
* Comprenez comment le rendu côté serveur doit ou ne doit pas être implémenté.

## Exigences et conditions préalables {#requirements-prerequisites}

Avant de commencer à travailler avec SPA dans AEM, plusieurs conditions sont requises.

### Connaissances {#knowledge}

* Expérience de développement de création de SPA avec des frameworks React ou Angular
* Compétences AEM de base pour la création de fragments de contenu et l’utilisation de l’éditeur
* Veillez à consulter le document [En tête et sans tête en AEM](/help/sites-developing/headful-headless.md) pour comprendre les différents niveaux d’intégration SPA possibles.

### Outils {#tools}

* Accès aux sandbox pour tester le déploiement de votre projet
* Instance de développement locale pour la modélisation et le test des données
* SPA externe existante (facultatif, selon le modèle d’intégration choisi)
* Archétype de projet AEM

## Qu’est-ce qu’une SPA ?  {#what-is-a-spa}

Une application d’une seule page (SPA) diffère d’une page conventionnelle en ce qu’elle est rendue côté client et qu’elle est principalement pilotée par JavaScript, en utilisant les appels Ajax pour charger les données et mettre à jour dynamiquement la page. La plupart ou la totalité du contenu est récupérée une fois au chargement d’une seule page avec des ressources supplémentaires chargées de manière asynchrone, selon les besoins, en fonction de l’interaction de l’utilisateur avec la page.

Cela limite la nécessité d’actualiser la page et offre à l’utilisateur une expérience harmonieuse, rapide et rappelant davantage l’expérience d’une application native.

L’éditeur de SPA AEM permet aux développeurs front-end de créer des SPA qui peuvent être intégrées à un site AEM, ce qui permet aux créateurs de contenu de modifier le contenu SPA aussi facilement qu’un autre contenu AEM.

## Pourquoi une SPA ?  {#why-spa}

En étant plus rapide, fluide et ressemblant davantage à une application native, une SPA devient une expérience attrayante non seulement pour le visiteur de la page web, mais aussi pour les marketeurs et les développeurs en raison de la nature du fonctionnement de SPA.

Pour obtenir une description complète des SPA et des raisons de leur utilisation, reportez-vous à la section [Ressources supplémentaires](#additional-resources) pour obtenir des liens vers une documentation plus détaillée.

## Comment AEM gère les SPA

Le développement d’applications sur une seule page sur AEM suppose que le développeur front-end respecte les bonnes pratiques standard lors de la création d’une SPA. Si, en tant que développeur front-end, vous suivez ces bonnes pratiques générales et quelques principes spécifiques à AEM, votre SPA sera fonctionnel avec l’AEM et ses fonctionnalités de création de contenu.

* **Portabilité** : comme pour tout composant, les composants de SPA créés doivent être aussi portables que possible. La SPA doit être créée avec des composants portables et réutilisables.
* **AEM détermine la structure du site** - Le développeur front-end crée des composants et possède leur structure interne, mais s’appuie sur AEM pour définir la structure de contenu du site.
* **Rendu dynamique** : tout le rendu doit être dynamique.
* **Routage dynamique** : la SPA assure le routage, et AEM l’écoute et s’appuie dessus pour l’extraction. Tout routage devrait également être dynamique.

Pour une description complète de la façon dont AEM gère les SPA, consultez la section [Ressources supplémentaires](#additional-resources) pour obtenir des liens vers une documentation plus détaillée.

## Éditeur de SPA AEM {#aem-spa-editor}

Les sites créés à l’aide de frameworks SPA courantes, telles que React et AngularJS, chargent leur contenu via le format JSON dynamique et ne fournissent pas le framework HTML dont l’éditeur de page AEM a besoin pour passer des commandes de modification.

Pour activer la modification d’applications sur une seule page dans AEM, il faut qu’il y ait une correspondance entre la sortie JSON de l’application et le modèle de contenu dans le répertoire AEM afin d’enregistrer les modifications apportées au contenu.

La prise en charge des applications sur une seule page dans AEM s’accompagne d’une fine couche JS qui interagit avec le code JS de l’application lorsqu’elle est chargée dans l’éditeur de pages avec lequel des événements peuvent être envoyés. L’emplacement des commandes d’édition peut être activé pour permettre une modification en contexte. Cette fonctionnalité repose sur le concept de point de terminaison de l’API Content Services, car le contenu de la SPA doit être chargé au moyen de Content Services.

Pour une description complète de la façon dont AEM gère l’éditeur de SPA, consultez la section [Ressources supplémentaires](#additional-resources) pour obtenir des liens vers une documentation plus détaillée.

## Hébergement des SPA existantes {#existing-spas}

Si vous disposez d’un SPA existant, AEM prend en charge son intégration dans afin qu’il soit visible par les auteurs de contenu dans l’éditeur d’. Cela peut s’avérer utile pour afficher le contenu qu’ils créent via des fragments de contenu dans le contexte de l’application finale où il sera utilisé.

En outre, avec seulement de petites modifications, vous pouvez activer certaines fonctionnalités d’édition pour les SPA externes dans l’éditeur AEM.

Le composant RemotePage permet le rendu d’une SPA externe dans AEM.

Pour une description complète de la manière de rendre les SPA externes modifiables dans AEM, consultez la section [Ressources supplémentaires](#additional-resources) pour obtenir des liens vers une documentation plus détaillée.

## Et après ? {#what-is-next}

Pour commencer à développer votre propre SPA pour AEM, consultez les documents suivants :

* [Tutoriel sur SPA WKND](/help/sites-developing/spa-wknd.md)
* [Prise en main avec React](/help/sites-developing/spa-getting-started-react.md)
* [Prise en main avec Angular](/help/sites-developing/spa-getting-started-angular.md)

Si vous devez adapter un SPA existant pour l’utiliser dans AEM, consultez les documents suivants :

* [Composant RemotePage](/help/sites-developing/spa-remote-page.md)
* [Modification d’une SPA externe dans AEM](/help/sites-developing/spa-edit-external.md)

Consultez ci-dessous les [ressources supplémentaires](#additional-resources) qui peuvent vous aider à approfondir les sujets relatifs aux SPA dans AEM.

## Ressources supplémentaires {#additional-resources}

Vous trouverez ci-dessous quelques ressources supplémentaires qui approfondissent certains concepts mentionnés dans ce document.

* [Couplage et découplage dans AEM](/help/sites-developing/headful-headless.md) : description des différents modèles de diffusion disponibles dans AEM
* [Introduction et présentation des applications monopage (SPA).](/help/sites-developing/spa-walkthrough.md) ; une bonne présentation des SPA en AEM
* [Développement de SPA pour AEM](/help/sites-developing/spa-architecture.md) : consignes sur la manière de développer des SPA pour AEM
* [Aperçu sur l’éditeur de SPA](/help/sites-developing/spa-overview.md) : informations détaillées sur le fonctionnement de l’éditeur de SPA
* [Rendu côté serveur](/help/sites-developing/spa-ssr.md) - Comment configurer le rendu côté serveur pour AEM SPA
* [Documents de référence pour les SPA](/help/sites-developing/spa-reference-materials.md) : références et liens de l’API JavaScript vers les projets GitHub de SPA AEM open source
* [Fragments de contenu](/help/assets/content-fragments/content-fragments.md) : comment créer des fragments de contenu
* [Archétype de projet AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=fr) : modèle Maven qui crée un projet Adobe Experience Manager (AEM) minimal qui s’appuie sur des bonnes pratiques pour démarrer votre site web
