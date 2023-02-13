---
title: Architecture logicielle
seo-title: Software Architecture
description: Meilleures pratiques pour la conception de votre logiciel
seo-description: Best practices for architecting your software
uuid: a557f6ca-c3f1-486e-a45e-6e1f986fab41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 92971747-1c74-4917-b5a0-7b79b3ae1e68
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: ht
source-wordcount: '614'
ht-degree: 100%

---

# Architecture logicielle{#software-architecture}

## Prise en compte des mises à niveau lors de la conception {#design-for-upgrades}

Lors de l’extension de comportements prêts à l’emploi, il convient de garder à l’esprit les mises à niveau. Appliquez toujours des personnalisations dans le répertoire /apps et superposez-les au-dessus des nœuds correspondants dans le répertoire /libs ou utilisez sling:resourceSuperType pour étendre le comportement standard. Bien que quelques modifications puissent s’avérer nécessaires pour la prise en charge d’une nouvelle version d’AEM, cette dernière ne devrait normalement pas écraser vos personnalisations si cette pratique est observée.

### Réutilisez les modèles et les composants dans la mesure du possible {#reuse-template-and-components-when-possible}

Outre une maintenance plus simple du code, cela permettra au site de conserver une interface plus cohérente. Lorsqu’un nouveau modèle est nécessaire, veillez à l’étendre à partir d’un modèle de base partagé, de sorte que les exigences globales, telles que l’inclusion de clientlib, puissent être codées à un seul endroit. Lorsqu’un nouveau composant est nécessaire, identifiez les possibilités d’extension depuis un composant existant.

### Créez des conceptions de modèles {#design-template-designs}

Définir les composants qui peuvent être inclus dans chaque système de paragraphes sur la page permet de conserver l’homogénéité d’aspect et d’utilisation du site. En limitant l’accès à la conception des pages, des « super auteurs » ou « super autrices » peuvent être autorisé(e)s à modifier les composants autorisés par page sans l’intervention du développeur ou de la développeuse, tout en s’assurant que les autres auteurs et autrices respectent les normes de l’entreprise.

### Développement d’une architecture SOLID {#develop-a-solid-architecture}

SOLID est un acronyme qui décrit cinq principes architecturaux qu’il convient de respecter :

* **S** ingle Responsibility Principle (Principe de responsabilité unique) - Chaque module, classe, méthode ne doit servir qu’à une seule chose.
* **O** pen/Closed Principle (Principe ouvert/fermé) - Les modules doivent être ouverts pour être étendus et fermés pour être modifiés.
* **L** iskov Substitution Principle (Principe de substitution de Liskov) - Les types doivent pouvoir être remplacés par leurs sous-types.
* **I** nterface Segregation Principle (Principe de ségrégation des interfaces) - Aucun client ne devrait être forcé de dépendre de méthodes qu’il n’utilise pas.
* **D** ependency Inversion Principle (Principe d’inversion des dépendances) - Le modules de haut niveau ne doivent pas dépendre de modules de bas niveau. Les deux doivent dépendre d’abstractions. Les abstractions ne doivent pas dépendre des détails. Les détails doivent dépendre des abstractions.

Vous devez vous efforcer de respecter ces cinq principes pour élaborer un système offrant une stricte séparation des préoccupations.

>[!TIP]
>
>SOLID est un concept couramment utilisé dans la programmation orientée objet et chaque élément est largement discuté dans la littérature du secteur.
>
>Ce bref résumé ne vous est présenté que pour vous en donner un aperçu et nous vous encourageons à vous familiariser davantage avec ces concepts.

### Observation du principe de robustesse {#follow-the-robustness-principle}

Le principe de robustesse stipule qu’il faut être tolérant dans ce que l’on accepte, et pointilleux dans ce que l’on envoie. En d’autres termes, lors de l’envoi de messages à un tiers, il convient de respecter scrupuleusement les spécifications. Cependant, lors de la réception de messages envoyés par un tiers, on doit accepter des messages non conformes, pour autant que leur signification soit claire.

### Mise en œuvre de pics dans leurs propres modules {#implement-spikes-in-their-own-modules}

Les pics et le code de test font partie intégrante de toute implémentation logicielle agile. Cependant, nous souhaitons nous assurer qu’ils ne se retrouvent pas dans la base de code d’exploitation sans le niveau de supervision approprié. Il est donc conseillé de créer des pics dans leurs propres modules.

### Mise en œuvre de scripts de migration de données dans leur propre module {#implement-data-migration-scripts-in-their-own-module}

En règle générale, les scripts de migration de données, bien qu’il s’agisse de code d’exploitation, ne sont exécutés qu’une seule fois au lancement initial d’un site. Par conséquent, dès que le site est en ligne, cela devient du code mort. Pour être sûr de ne pas créer du code d’implémentation qui dépend des scripts de migration, ceux-ci doivent être mis en œuvre dans leur propre module. Cela permet, en outre, de supprimer et de mettre hors service ce code juste après le lancement, et d’éliminer ainsi le code mort du système.

### Respect des conventions Maven publiées dans les fichiers POM {#follow-published-maven-conventions-in-pom-files}

Apache a publié des conventions de style, disponibles à l’adresse suivante : [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). Il est conseillé de suivre ces conventions, dans la mesure où elles permettent une mise en route rapide de nouvelles ressources.
