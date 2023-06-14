---
title: Architecture logicielle
description: Bonnes pratiques pour la conception de vos logiciels
uuid: a557f6ca-c3f1-486e-a45e-6e1f986fab41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 92971747-1c74-4917-b5a0-7b79b3ae1e68
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 41%

---

# Architecture logicielle{#software-architecture}

## Conception pour les mises à niveau {#design-for-upgrades}

Lors de l’extension de comportements prêts à l’emploi, il convient de garder à l’esprit les mises à niveau. Appliquez toujours des personnalisations dans le répertoire /apps et superposez-les au-dessus des nœuds correspondants dans le répertoire /libs ou utilisez sling:resourceSuperType pour étendre le comportement standard. Bien que certaines modifications puissent être nécessaires pour prendre en charge une nouvelle version d’AEM, la nouvelle version ne doit pas remplacer vos personnalisations si cette pratique est suivie.

### Réutilisez les modèles et les composants dans la mesure du possible {#reuse-template-and-components-when-possible}

Cela permet au site de conserver une apparence plus cohérente et de simplifier la maintenance du code. Lorsqu’un nouveau modèle est nécessaire, veillez à l’étendre à partir d’un modèle de base partagé, de sorte que les exigences globales, telles que l’inclusion de clientlib, puissent être codées à un seul endroit. Lorsqu’un nouveau composant est nécessaire, identifiez les possibilités d’extension depuis un composant existant.

### Créez des conceptions de modèles {#design-template-designs}

Définir les composants qui peuvent être inclus dans chaque système de paragraphes sur la page permet de conserver l’homogénéité d’aspect et d’utilisation du site. En limitant l’accès à la conception des pages, des « super auteurs » ou « super autrices » peuvent être autorisé(e)s à modifier les composants autorisés par page sans l’intervention du développeur ou de la développeuse, tout en s’assurant que les autres auteurs et autrices respectent les normes de l’entreprise.

### Développement d’une architecture SOLID {#develop-a-solid-architecture}

SOLID est un acronyme qui décrit cinq principes architecturaux qui doivent être respectés :

* **s** Principe de responsabilité unique : chaque module, classe, méthode, etc., ne doit avoir qu’une seule responsabilité.
* **O** pen/Closed Principle (Principe ouvert/fermé) - Les modules doivent être ouverts pour être étendus et fermés pour être modifiés.
* **L** iskov Substitution Principle (Principe de substitution de Liskov) - Les types doivent pouvoir être remplacés par leurs sous-types.
* **I** nterface Segregation Principle (Principe de ségrégation des interfaces) - Aucun client ne devrait être forcé de dépendre de méthodes qu’il n’utilise pas.
* **D** ependency Inversion Principle (Principe d’inversion des dépendances) - Le modules de haut niveau ne doivent pas dépendre de modules de bas niveau. Les deux doivent dépendre d&#39;abstractions. Les abstractions ne doivent pas dépendre des détails. Les détails doivent dépendre d’abstractions.

S&#39;efforcer de respecter ces cinq principes devrait aboutir à un système qui se distingue strictement des préoccupations.

>[!TIP]
>
>SOLID est un concept couramment utilisé dans la programmation orientée objet et chaque élément est largement discuté dans la littérature industrielle.
>
>Cette information n&#39;est qu&#39;un bref résumé présenté à des fins de sensibilisation et nous vous encourageons à vous familiariser davantage avec ces concepts.

### Observation du principe de robustesse {#follow-the-robustness-principle}

Le principe de robustesse stipule que vous devez être conservateur dans ce que vous envoyez, mais être libéral dans ce que vous acceptez. En d’autres termes, lorsque vous envoyez des messages à un tiers, vous devez vous conformer entièrement aux spécifications. Cependant, lorsque vous recevez des messages d’un tiers, vous devez accepter les messages non conformes tant que la signification du message est claire.

### Mise en œuvre de pics dans leurs propres modules {#implement-spikes-in-their-own-modules}

Les pics et le code de test font partie de toute implémentation de logiciel Agile. Cependant, vous souhaitez vous assurer qu’ils n’entrent pas dans la base de code de production sans le niveau de surveillance approprié. Par conséquent, il est recommandé de créer des pics dans leur propre module.

### Mise en œuvre de scripts de migration de données dans leur propre module {#implement-data-migration-scripts-in-their-own-module}

Les scripts de migration de données, bien que le code de production, ne sont exécutés qu’une seule fois au lancement initial d’un site. Par conséquent, lorsque le site est actif, les scripts deviennent du code mort. Pour vous assurer que vous ne créez pas de code d’implémentation qui dépend des scripts de migration, ils doivent être implémentés dans leur propre module. Cela nous permet de supprimer et de retirer ce code immédiatement après le lancement, en éliminant le code inactif du système.

### Respect des conventions Maven publiées dans les fichiers POM {#follow-published-maven-conventions-in-pom-files}

Apache a publié des conventions de style, disponibles à l’adresse suivante : [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). Il est préférable de suivre ces conventions car il est plus facile pour de nouvelles ressources de se mettre rapidement à niveau.
