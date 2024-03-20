---
title: Utiliser l’espace de travail AEM Forms
description: Prise en main de l’espace de travail AEM Forms avec cet aperçu rapide des workflows de processus.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 0bedcbd9-2cf8-47da-9440-c773982e550c
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 26%

---

# Utiliser l’espace de travail AEM Forms{#working-with-aem-forms-workspace}

## Présentation {#introduction}

AEM Forms Workspace fait partie d’AEM Forms. Workspace facilite le rendu de HTML Forms en plus des PDF forms. Vous pouvez désormais vous lancer dans des processus d’entreprise à partir d’interfaces mobiles et d’applications web.

En outre, l’espace de travail AEM Forms est hautement personnalisable à l’aide de la norme HTML et des méthodologies de développement JavaScript™. Il s’agit d’un logiciel basé sur des composants qui s’intègre facilement à vos autres applications web.

Pour plus d’informations, voir [Présentation de l’espace de travail AEM Forms](/help/forms/using/introduction-html-workspace.md).

## Se familiariser {#getting-familiar}

Pour vous familiariser avec le processus de bout en bout de création d’une application de formulaires pour automatiser un processus d’entreprise, suivez la présentation. Vous pouvez créer, gérer et tester une application à l’aide de Workbench, Designer et l’espace de travail AEM Forms après avoir suivi la présentation. Pour plus d’informations sur l’implémentation, voir [Création de votre première application AEM Forms](https://helpx.adobe.com/fr_FR/livecycle/11.0/CreateFirstApp/index.html).

## Présentation fonctionnelle {#functional-overview}

Vous pouvez utiliser l’espace de travail AEM Forms pour effectuer les tâches suivantes :

**Démarrer une gestion commerciale :** l’espace de travail AEM Forms classe les processus comme prévu et défini par l’entreprise. Vous pouvez marquer comme favori les catégories fréquemment utilisées pour accéder rapidement aux catégories. Lorsque vous démarrez un processus, vous remplissez généralement un formulaire pour démarrer un processus d’entreprise contrôlé par le processus des formulaires. Pour plus d’informations, voir [Démarrage des processus](/help/forms/using/starting-processes.md).

**Afficher et agir sur les tâches :** lorsque vous affichez les listes de tâches, vous visualisez les tâches de gestion commerciale qui vous sont affectées, ou qui sont affectées à des groupes auxquels vous appartenez, ou qui sont les tâches partagées d’autres utilisateurs. Vous pouvez ouvrir, travailler et effectuer les tâches selon vos besoins. En règle générale, l’exécution d’une tâche implique de fournir des informations, d’approuver ou de rejeter un formulaire. Pour plus d’informations, voir [Utilisation de listes de tâches](/help/forms/using/todo-lists.md).

**Suivi des tâches**: pour effectuer le suivi de vos tâches, utilisez l’onglet Tracking de l’espace de travail AEM Forms. Vous pouvez rechercher les processus actifs ou terminés que vous avez démarrés ou modifiés. Vous pouvez afficher les tâches, les affectations et les formulaires qui faisaient partie du processus. Vous pouvez également lancer de nouveaux processus à l’aide des données de formulaire issues d’un processus que vous avez précédemment lancé. Pour plus d’informations, voir [Suivi des processus](/help/forms/using/tracking-processes.md).

## Nouvelle offre de l’espace de travail AEM Forms {#new-offering-of-aem-forms-workspace}

**Prise en charge de l’approbation en bloc des tâches**:

Vous pouvez approuver plusieurs tâches du même type. Une fois que vous sélectionnez une tâche à approuver, seules les tâches avec le même processus, les mêmes noms de tâche et les mêmes options de routage restent activées. Voir [Utilisation de listes de tâches](/help/forms/using/todo-lists.md) pour les détails d’implémentation.

## Migration de Workspace Flex vers l’espace de travail AEM Forms {#migrating-from-flex-workspace-to-aem-forms-workspace}

Flex Workspace n’est pas pris en charge pour les clients AEM Forms. Tous les clients qui utilisent Flex Workspace doivent passer à AEM Forms Workspace.

Dans l’espace de travail AEM Forms, les services de rendu et d’envoi par défaut, dans le profil d’action par défaut, associés aux formulaires XDP ont changé et de nouveaux services ont été ajoutés. Pour plus d’informations, voir [Nouveau service de rendu et d’envoi](/help/forms/using/new-render-submit-service.md). Pour migrer vos processus existants, qui fonctionnent avec les formulaires XDP, afin d’utiliser ces services, vous pouvez suivre [ces étapes](new-render-submit-service.md).

**Mappage des personnalisations de l’espace de travail Flex avec l’espace de travail AEM Forms**

Le mappage entre différents types de personnalisations dans les deux espaces de travail se présente comme suit.

<table>
 <tbody>
  <tr>
   <td><strong>Type de personnalisation </strong></td>
   <td><strong>Personnalisations abordées </strong></td>
   <td><strong>Scénario de personnalisation de l’espace de travail AEM Forms correspondant</strong></td>
  </tr>
  <tr>
   <td>Personnalisation de la localisation</td>
   <td>
    <ol>
     <li>Modification des paramètres régionaux de Workspace</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-locale-user-interface.md">Modification des paramètres régionaux de l’espace de travail AEM Forms</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Personnalisation du thème</td>
   <td>
    <ol>
     <li>Remplacement des images</li>
     <li>Modification des couleurs</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-organization-logo-branding.md">Modification du logo de l’organisation</a> </li>
     <li><a href="/help/forms/using/changing-color-scheme-interface.md">Modification du modèle de couleur </a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Personnalisation de la mise en page</td>
   <td>
    <ol>
     <li>Simplification de l’interface utilisateur de Workspace<br /> </li>
     <li>Création d’un nouvel écran de connexion</li>
     <li>Création d’un conteneur d’approbation personnalisé</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">Utilisation de composants réutilisables </a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">Création d’un écran de connexion</a></li>
     <li>Le conteneur d’approbation est obsolète.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

Les caractéristiques suivantes de l’espace de travail Flex ne sont pas disponibles dans l’espace de travail AEM Forms : messages et notification, page d’accueil, conteneur d’approbation et l’option de gestion des en-têtes de colonne. Pour obtenir une liste complète, voir [Fonctionnalités de Flex Workspace non disponibles dans l’espace de travail AEM Forms](/help/forms/using/features-flex-workspace-available-html.md).

## Développement avec l’espace de travail AEM Forms {#developing-with-aem-forms-workspace}

### Architecture {#architecture}

AEM Forms Workspace est une application web basée sur HTML et JavaScript™ hébergée sur CRX™. Lorsque l’URL de l’espace de travail est ouverte dans un navigateur, une ressource CRX™ est accessible et l’application est rendue en tant que page de HTML dans le navigateur. Les bibliothèques JavaScript et le code JavaScript personnalisé gèrent le comportement interne et externe de l’application, tel que l’interface utilisateur, l’interaction utilisateur et la communication avec le serveur AEM Forms. Pour plus d’informations, voir Espace de travail AEM Forms [Architecture](/help/forms/using/html-workspace-architecture.md).

### Personnalisation de l’espace de travail AEM Forms {#aem-forms-workspace-customization}

L’espace de travail AEM Forms prend en charge un large éventail de personnalisations pour mettre à jour la mise en page de l’interface utilisateur, son aspect, sa fonctionnalité et bien plus encore. Les personnalisations impliquent la mise à jour d’un ou de plusieurs des éléments suivants :

* Apparences de l’interface utilisateur
* Fonctionnalité utilisant des personnalisations sémantiques
* Réutilisation de composants de HTML dans d’autres applications web

La variable [personnalisation](introduction-customizing-html-workspace.md#types-of-customizations) Cet article explique les types de ces personnalisations.

### Configuration de l’environnement de développement {#set-up-the-developer-environment}

Les éléments livrables de l’espace de travail AEM Forms comprennent un package CRX déployé sur CRX, une archive SDK contenant le code source complet, des bibliothèques JavaScript tierces et des scripts de génération de l’espace de travail AEM Forms. Utilisez-les pour configurer l’environnement de développement afin d’effectuer les personnalisations mentionnées ci-dessus. Pour plus d’informations, voir [Création du code de l’espace de travail AEM Forms](introduction-customizing-html-workspace.md#building-html-workspace-code).

Vous pouvez personnaliser une grande partie de l’interface et des fonctionnalités de base, telles que les polices, le modèle de couleurs, le logo, l’écran de connexion, les boîtes de dialogue d’erreur, l’intégration à des applications tierces et la réutilisation de composants dans une application tierce. Vous pouvez également améliorer le contenu affiché sur la page Résumé de la tâche, afficher des images pour les actions d’itinéraire de la tâche, et même modifier les modèles et vues Backbone de bas niveau qui créent l’application de l’espace de travail AEM Forms.

### Rendu du HTML de XDP Forms {#html-rendering-of-xdp-forms}

Par défaut, pour un nouveau processus, un formulaire XDP est rendu au format PDF sur un bureau et au format HTML sur une tablette. Il est possible de toujours effectuer le rendu d’un formulaire XDP au format HTML. Pour plus d’informations, voir [Nouveaux services de rendu et d’envoi](/help/forms/using/new-render-submit-service.md).

La fonction [Mobile Forms](https://helpx.adobe.com/fr/livecycle/help/mobile-forms/introduction.html), qui fonctionne avec les [profils](https://helpx.adobe.com/fr/livecycle/help/mobile-forms/creating-profile.html), permet le rendu HTML des formulaires XDP. Par défaut, « Rendre le nouveau formulaire HTML » utilise le profil `default.html`, qui peut être modifié. Vous pouvez également ajouter des modifications personnalisées qui surviennent avant de générer un formulaire XDP au format HTML.

## Application d’espace de travail AEM Forms {#aem-forms-workspace-app}

Pour travailler sur vos processus d’entreprise sur un périphérique mobile, vous pouvez utiliser l’offre de l’application AEM Forms Workspace d’AEM Forms. Pour plus d’informations, voir [Présentation de l’application d’espace de travail AEM Forms](https://helpx.adobe.com/fr/livecycle/help/mobile-workspace/mobile-workspace-overview.html).
