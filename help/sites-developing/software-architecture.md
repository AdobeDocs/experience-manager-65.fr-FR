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
source-git-commit: 423e17dadf2e506eb68b37851dde5e68ed950866
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 73%

---

# Architecture logicielle{#software-architecture}

## Prise en compte des mises à niveau lors de la conception {#design-for-upgrades}

Lors de l’extension de comportements prêts à l’emploi, il convient de garder à l’esprit les mises à niveau. Appliquez toujours des personnalisations dans le répertoire /apps et superposez-les au-dessus des nœuds correspondants dans le répertoire /libs ou utilisez sling:resourceSuperType pour étendre le comportement standard. Bien que quelques modifications puissent s’avérer nécessaires pour la prise en charge d’une nouvelle version d’AEM, cette dernière ne devrait normalement pas écraser vos personnalisations si cette pratique est observée.

### Réutilisation du modèle et des composants dans la mesure du possible {#reuse-template-and-components-when-possible}

Outre une maintenance plus simple du code, cela permettra au site de conserver une interface plus cohérente. Lorsqu’un nouveau modèle est nécessaire, veillez à l’étendre à partir d’un modèle de base partagé, de sorte que les exigences globales, telles que l’inclusion de clienlib, puissent être codées à un seul endroit. Lorsqu’un nouveau composant est nécessaire, identifiez les possibilités d’extension depuis un composant existant.

### Création de conceptions de modèle {#design-template-designs}

En définissant les composants qui peuvent être inclus dans chaque système de paragraphes sur la page, une homogénéité d’aspect du site peut être gérée. En limitant l’accès à la conception sur les pages, des « super auteurs » peuvent être autorisés à modifier les composants autorisés par page sans l’intervention du développeur, tout en s’assurant que les autres auteurs respectent les normes de l’entreprise.

### Développement d’une architecture SOLID {#develop-a-solid-architecture}

SOLID est un acronyme qui décrit cinq principes architecturaux qu’il convient de respecter :

* **s** Principe de responsabilité unique : chaque module, classe, méthode, etc., ne doit avoir qu’une seule responsabilité.
* **O** Principe ouvert/fermé : les modules doivent être ouverts pour extension et fermés pour modification.
* **L** Principe de substitution iskov - les types doivent pouvoir être remplacés par leurs sous-types.
* **I** Principe de segmentation de l’interface : aucun client ne doit être contraint à dépendre de méthodes qu’il n’utilise pas.
* **D** Principe d’inversion des dépendances : les modules de haut niveau ne doivent pas dépendre des modules de bas niveau. Les deux doivent dépendre d’abstractions. Les abstractions ne doivent pas dépendre des détails. Les détails doivent dépendre des abstractions.

Vous devez vous efforcer de respecter ces cinq principes pour élaborer un système offrant une stricte séparation des préoccupations.

>[!TIP]
>
>SOLID est un concept couramment utilisé dans la programmation orientée objet et chaque élément est largement discuté dans la littérature de l&#39;industrie.
>
>Ce n&#39;est qu&#39;un bref résumé présenté pour la prise de conscience et nous vous encourageons à vous familiariser davantage avec ces concepts.

### Observation du principe de robustesse {#follow-the-robustness-principle}

Le principe de robustesse stipule qu’il faut être tolérant dans ce que l’on accepte, et pointilleux dans ce que l’on envoie. En d’autres termes, lors de l’envoi de messages à un tiers, nous devons nous conformer entièrement aux spécifications, mais lors de la réception de messages d’un tiers, nous devons accepter les messages non conformes tant que la signification du message est claire.

### Mise en œuvre de spikes dans leurs propres modules {#implement-spikes-in-their-own-modules}

Les pics et le code de test font partie intégrante de toute implémentation logicielle agile. Cependant, nous souhaitons nous assurer qu’ils ne se retrouvent pas dans le codebase de production sans le niveau de supervision approprié. Il est donc conseillé de créer des spikes dans leurs propres modules.

### Mise en œuvre de scripts de migration de données dans leur propre module {#implement-data-migration-scripts-in-their-own-module}

En règle générale, les scripts de migration de données, bien qu’il s’agisse de code de production, ne sont exécutés qu’une seule fois au lancement initial d’un site. Par conséquent, dès que le site est en ligne, cela devient du code mort. Pour être sûr de ne pas créer du code d’implémentation qui dépend des scripts de migration, ceux-ci doivent être mis en œuvre dans leur propre module. Cela permet, en outre, de supprimer et de mettre hors service ce code juste après le lancement, et d’éliminer ainsi le code mort du système.

### Respect des conventions Maven publiées dans les fichiers POM {#follow-published-maven-conventions-in-pom-files}

Apache a publié des conventions de style sur [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). Il est conseillé de suivre ces conventions, dans la mesure où elles permettent une mise en route rapide de nouvelles ressources.
