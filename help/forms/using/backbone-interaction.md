---
title: Interaction de Backbone
description: Informations conceptuelles sur l’utilisation des modèles JavaScript Backbone dans l’espace de travail AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 8fd9770b-6ec4-4b09-b6b2-47a5e5d40f79
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms, Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 100%

---

# Interaction de Backbone{#backbone-interaction}

Backbone est une bibliothèque qui permet de créer et de suivre une architecture MVC dans des applications web. L’idée de base de Backbone est d’organiser votre interface en vues logiques, reposant sur des modèles, chacune d’elles pouvant être mise à jour indépendamment lorsque le modèle change, sans avoir à redessiner la page. Pour plus d’informations sur Backbone, consultez la section [https://backbonejs.org](https://backbonejs.org/).

Voici quelques concepts clés :

**Modèle Backbone** : contient des données et une majeure partie de la logique liée à ces données.

**Vue Backbone** : utilisée pour représenter l’état du modèle correspondant. Une vue Backbone se comporte en fait comme un contrôleur, écoutant les événements de l’interface utilisateur comme les clics de l’utilisateur, ou les événements de modèle (comme les modifications de données), et modifie l’interface utilisateur en fonction des besoins.

**Modèle HTML** : modèle d’enveloppe qui contient des balises d’emplacement renseignées par le modèle.

**Espace de travail AEM Forms** : contient plusieurs composants individuels. Chaque composant :

* Représente un seul élément d’interface utilisateur logique.
* Il peut s’agir d’une collection de composants similaires.
* Comprend le modèle Backbone, la vue Backbone et le modèle de HTML.
* Contient une référence à un service.
* Contient une référence aux utilitaires requis.

Lorsqu’un composant est initialisé, les objets suivants sont créés :

* Une nouvelle instance du modèle Backbone du composant est créée. Le service est injecté dans le modèle.
* Une nouvelle instance de la vue Backbone est créée.
* L’instance du modèle correspondant, du modèle HTML et des utilitaires est injectée dans la vue.

Dans la vue Backbone, il existe une carte d’événements qui mappe les différents événements qui peuvent survenir en raison d’interactions de l’interface utilisateur avec un gestionnaire correspondant. Ce mappage est lancé une fois qu’un composant est initialisé.

Lorsqu’une vue est initialisée, elle appelle son modèle correspondant pour récupérer les données du serveur. Une fois que toutes les données requises par une vue sont disponibles, la vue génère les données dans le format spécifié par le modèle HTML. Plusieurs vues peuvent partager un même modèle de communication.

![Vue Backbone d’AEM Forms](do-not-localize/aem_forms_workflow.png)

Exemple :

1. L’utilisateur ou l’utilisatrice clique sur un modèle de tâche dans la liste des tâches.
1. La vue Tâche écoute le clic et appelle la fonction de rendu sur le modèle de tâche.
1. Le modèle de tâche appelle ensuite le service qui constitue un point commun pour toutes les communications avec le serveur AEM Forms.
1. La classe service appelle le point d’entrée REST d’AEM Forms pour obtenir la méthode de rendu via ajax.
1. Le rappel de succès de cet appel Ajax est défini dans le modèle de tâche.
1. Le modèle de tâche génère un événement Backbone en tant que notification indiquant que l’appel de rendu est terminé.
1. Une autre vue, la vue Détails de la tâche, écoute cet événement à partir du modèle de tâche.
1. La vue Détails de la tâche modifie ensuite le modèle Détails de la tâche pour afficher la tâche rendue (formulaire, détails, pièces jointes, notes, etc.) pour l’utilisateur ou l’utilisatrice.
