---
title: Mises à niveau possibles
description: Découvrez les mises à niveau possibles dans Adobe Experience Manager 6.4.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
exl-id: b777fdca-e7a5-427a-9e86-688dd7cac636
source-git-commit: 26c0411d6cc16f4361cfa9e6b563eba0bfafab1e
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 18%

---

# Mises à niveau possibles{#sustainable-upgrades}

## Structure de personnalisation {#customization-framework}

### Architecture (fonctionnelle/infrastructure/contenu/application)  {#architecture-functional-infrastructure-content-application}

La fonctionnalité de structure de personnalisation est conçue pour aider à réduire les violations dans les zones non extensibles du code (comme les API) ou du contenu (comme les superpositions) qui ne sont pas compatibles avec la mise à niveau.

Il existe deux composants de la structure de personnalisation : la valeur **Surface d’API** et le **Classification de contenu**.

#### Surface d’API {#api-surface}

Dans les versions précédentes d’Adobe Experience Manager (AEM), de nombreuses API étaient exposées par le biais d’Uber Jar. Certaines de ces API n’étaient pas destinées à être utilisées par les clients, mais étaient exposées à la prise en charge des fonctionnalités AEM entre les lots. Dorénavant, les API Java™ sont marquées comme publiques ou privées pour indiquer aux clients quelles API peuvent être utilisées en toute sécurité dans le cadre des mises à niveau. Voici d’autres observations :

* API Java™ marquées comme `Public` peut être utilisé et référencé par des lots d’implémentation personnalisés.

* Les API publiques sont rétrocompatibles avec l’installation d’un package de compatibilité.
* Le package de compatibilité contient un fichier JAR Uber de compatibilité pour garantir la compatibilité descendante.
* API Java™ marquées comme `Private` sont destinés uniquement à être utilisés par AEM bundles internes et ne doivent pas l’être par des bundles personnalisés.

>[!NOTE]
>
>Le concept de `Private` et `Public` dans ce contexte ne doit pas être confondu avec les notions Java™ de classes publiques et privées.

![image2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### Classifications de contenu {#content-classifications}

AEM a longtemps utilisé le principe des incrustations et Sling Resource Merger pour permettre aux clients d’étendre et de personnaliser les fonctionnalités d’AEM. Les fonctionnalités prédéfinies qui alimentent les consoles AEM et l’interface utilisateur sont stockées dans **/libs**. Les clients ne doivent jamais modifier quoi que ce soit sous **/libs** mais peut ajouter du contenu supplémentaire sous **/apps** pour superposer et étendre les fonctionnalités définies dans **/libs** (Voir Développement avec des superpositions pour plus d’informations). Cela provoquait toujours de nombreux problèmes lors de la mise à niveau d’AEM en tant que contenu dans **/libs** peut changer, ce qui entraîne une interruption inattendue de la fonctionnalité de recouvrement. Les clients peuvent également étendre les composants d’AEM par le biais de l’héritage `sling:resourceSuperType`, ou simplement référencer un composant dans **/libs** directement par le biais de sling:resourceType. Des problèmes de mise à niveau similaires peuvent se produire avec les cas d’utilisation de référence et de remplacement.

Pour que les clients puissent comprendre plus facilement et plus en toute sécurité les zones d’ **/libs** peuvent utiliser et superposer le contenu en toute sécurité dans **/libs** a été classé avec les mixins suivants :

* **Public (granite:PublicArea)** - Définit un noeud comme étant public afin qu’il puisse être superposé, hérité ( `sling:resourceSuperType`) ou utilisé directement ( `sling:resourceType`). Les noeuds situés sous /libs marqués comme publics peuvent être mis à niveau en toute sécurité avec l’ajout d’un module de compatibilité. En général, les clients ne doivent utiliser que les noeuds publics.

* **Résumé (granite:AbstractArea)** : définit un nœud en tant que résumé. Les noeuds peuvent être superposés ou hérités ( `sling:resourceSupertype`), mais non utilisé directement ( `sling:resourceType`).

* **Final (granite:FinalArea)** : définit un nœud comme étant final. Les nœuds classés en tant que finaux ne doivent idéalement pas être recouverts ni hérités. Les noeuds finaux peuvent être utilisés directement au moyen de `sling:resourceType`. Par défaut, les nœuds secondaires placés sous le nœud final sont considérés comme internes.

* ***Interne (granite:InternalArea)*** *- * Définit un nœud comme interne. Les nœuds classés dans la catégorie Interne ne peuvent pas être superposés, hérités, ni utilisés directement. Ces noeuds sont destinés uniquement aux fonctionnalités internes de AEM

* **Aucune annotation** - Les noeuds héritent de la classification en fonction de la hiérarchie de l’arborescence. La racine / est par défaut Public. **Les noeuds dont le parent est classé comme Interne ou Final doivent également être traités comme Interne.**

>[!NOTE]
>
Ces stratégies ne sont appliquées que par rapport aux mécanismes basés sur des chemins de recherche Sling. D’autres zones de **/libs**, comme une bibliothèque côté client, peuvent se voir affecter la classification `Internal`. Cependant, elles peuvent toujours être utilisées avec l’inclusion clientlib standard. Il est important qu’un client continue à respecter la classification interne dans ces cas.

#### Indicateurs de type de contenu CRXDE Lite {#crxde-lite-content-type-indicators}

Les mixins appliqués dans CRXDE Lite affichent les noeuds de contenu et les arborescences marqués comme `INTERNAL` comme étant grisé. Pour `FINAL`, seule l’icône est grisée. Les enfants de ces noeuds apparaissent également grisés. La fonctionnalité Noeud de recouvrement est désactivée dans les deux cas.

**Public**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**Final**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**Interne**

![image2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**Contrôle de l’intégrité du contenu**

>[!NOTE]
>
Depuis la version 6.5 d’AEM, Adobe recommande d’utiliser l’Outil de détection des motifs pour détecter les violations d’accès au contenu. Les rapports du détecteur de motifs sont plus détaillés, détectent plus de problèmes et réduisent la probabilité de faux positifs.
>
Pour plus d’informations, consultez la section [Évaluation de la complexité de la mise à niveau à l’aide de l’Outil de détection des motifs](/help/sites-deploying/pattern-detector.md).

AEM version 6.5 est fournie avec un contrôle de l’intégrité afin d’alerter les clients si du contenu superposé ou référencé est utilisé de manière incohérente avec la classification de contenu.

La **Vérification de l’accès au contenu Sling/Granite** est un nouveau contrôle d’intégrité qui surveille le référentiel afin de détecter si du code client accède, de manière non autorisée, à des nœuds protégés dans AEM.

Cette analyse **/apps** et dure généralement plusieurs secondes.

Pour accéder à ce nouveau contrôle de l’intégrité, procédez comme suit :

1. Dans l’écran d’accueil AEM, accédez à **Outils > Opérations > Rapports d’intégrité**
1. Cliquez sur **Vérification de l’accès au contenu Sling/Granite**.

   ![screen_shot_2017-12-14at55648pm](assets/screen_shot_2017-12-14at55648pm.png)

Une fois l’analyse terminée, une liste d’avertissements s’affiche, informant l’utilisateur final du noeud protégé qui est incorrectement référencé :

![screenshot-2018-2-5healthreports](assets/screenshot-2018-2-5healthreports.png)

Après avoir corrigé les violations, il revient à l’état vert :

![screenshot-2018-2-5healthreports-violations](assets/screenshot-2018-2-5healthreports-violations.png)

Le contrôle de l’intégrité affiche les informations collectées par un service en arrière-plan qui vérifie de manière asynchrone chaque fois qu’une superposition ou un type de ressource est utilisé sur tous les chemins de recherche Sling. Si les mixins de contenu sont utilisés de manière incorrecte, une violation est signalée.
