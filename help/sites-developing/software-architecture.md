---
title: Architecture logicielle
description: Découvrez quelques bonnes pratiques pour concevoir l’architecture de votre logiciel pour Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 100%

---

# Architecture logicielle{#software-architecture}

## Conception pour les mises à niveau {#design-for-upgrades}

Lors de l’extension de comportements prêts à l’emploi, il convient de garder à l’esprit les mises à niveau. Appliquez toujours des personnalisations dans le répertoire /apps et superposez-les au-dessus des nœuds correspondants dans le répertoire /libs ou utilisez sling:resourceSuperType pour étendre le comportement standard. Bien que quelques modifications puissent s’avérer nécessaires pour la prise en charge d’une nouvelle version d’AEM, cette dernière ne devrait normalement pas écraser vos personnalisations si cette pratique est suivie.

### Réutilisez les modèles et les composants dans la mesure du possible. {#reuse-template-and-components-when-possible}

Outre une maintenance plus simple du code, cela permettra au site de conserver une interface plus cohérente. Lorsqu’un nouveau modèle est nécessaire, veillez à l’étendre à partir d’un modèle de base partagé, de sorte que les exigences globales, telles que l’inclusion de clientlib, puissent être codées à un seul endroit. Lorsqu’un nouveau composant est nécessaire, identifiez les possibilités d’extension depuis un composant existant.

### Créez des conceptions de modèles {#design-template-designs}

Définir les composants qui peuvent être inclus dans chaque système de paragraphes sur la page permet de conserver l’homogénéité d’aspect et d’utilisation du site. En limitant l’accès à la conception des pages, des « super auteurs » ou « super autrices » peuvent être autorisé(e)s à modifier les composants autorisés par page sans l’intervention du développeur ou de la développeuse, tout en s’assurant que les autres auteurs et autrices respectent les normes de l’entreprise.

### Développer une architecture SOLID {#develop-a-solid-architecture}

SOLID est un acronyme qui décrit cinq principes architecturaux qui doivent être respectés :

* **S** ingle Responsibility Principle (Principe de responsabilité unique) : chaque module, classe, méthode ne doit servir qu’à une seule chose.
* **O** pen/Closed Principle (Principe ouvert/fermé) - Les modules doivent être ouverts pour être étendus et fermés pour être modifiés.
* **L** iskov Substitution Principle (Principe de substitution de Liskov) - Les types doivent pouvoir être remplacés par leurs sous-types.
* **I** nterface Segregation Principle (Principe de ségrégation des interfaces) - Aucun client ne devrait être forcé de dépendre de méthodes qu’il n’utilise pas.
* **D** ependency Inversion Principle (Principe d’inversion des dépendances) - Le modules de haut niveau ne doivent pas dépendre de modules de bas niveau. Les deux doivent dépendre d’abstractions. Les abstractions ne doivent pas dépendre des détails. Les détails doivent dépendre d’abstractions.

Le respect de ces cinq principes devrait aboutir à un système qui sépare strictement les préoccupations.

>[!TIP]
>
>SOLID est un concept couramment utilisé dans la programmation orientée objet et chaque élément est largement discuté dans la documentation du secteur.
>
>Cette information est un bref résumé pour vous donner un aperçu et nous vous encourageons à vous familiariser davantage avec ces concepts.

### Observer le principe de robustesse {#follow-the-robustness-principle}

Le principe de robustesse stipule qu’il faut faire preuve de tolérance dans ce que l’on accepte, et faire preuve de prudence dans ce que l’on envoie. En d’autres termes, lorsque vous envoyez des messages à une tierce partie, vous devez vous conformer entièrement aux spécifications. Cependant, lorsque vous recevez des messages d’une tierce partie, vous devez accepter les messages non conformes tant que la signification du message est claire.

### Implémenter des pics dans leurs propres modules {#implement-spikes-in-their-own-modules}

Les pics et le code de test font partie de toute implémentation de logiciel agile. Cependant, vous devriez vous assurer qu’ils n’entrent pas dans la base de code de production sans le niveau de surveillance approprié. Par conséquent, il est recommandé de créer des pics dans leur propre module.

### Implémenter des scripts de migration de données dans leur propre module {#implement-data-migration-scripts-in-their-own-module}

Les scripts de migration de données, bien qu’il s’agisse de code de production, ne sont exécutés qu’une seule fois lors du lancement initial d’un site. Par conséquent, lorsque le site est mis en production, les scripts deviennent du code mort. Pour vous assurer de ne pas créer du code d’implémentation qui dépend des scripts de migration, ceux-ci doivent être implémentés dans leur propre module. Cela permet de supprimer et de mettre hors service ce code juste après le lancement, et d’éliminer ainsi le code mort du système.

### Respect des conventions Maven publiées dans les fichiers POM {#follow-published-maven-conventions-in-pom-files}

Apache a publié des conventions de style, disponibles à l’adresse suivante : [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). Il est conseillé de suivre ces conventions car elles permettent une mise en route rapide de nouvelles ressources.
