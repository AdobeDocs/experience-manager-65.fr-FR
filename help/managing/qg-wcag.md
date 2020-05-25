---
title: Guide rapide relatif à WCAG 2.1
description: Guide rapide relatif à WCAG 2.1
translation-type: tm+mt
source-git-commit: a8e7fe89376b30df0b1c5403aabea6862cef09fc
workflow-type: tm+mt
source-wordcount: '1770'
ht-degree: 88%

---


# Guide rapide relatif à WCAG 2.1{#quick-guide-to-wcag}

Adobe Experience Manager (AEM) a été développé pour optimiser la conformité aux directives d’accessibilité du contenu Web.

[Web Content Accessibility Guidelines (WCAG) version 2.1](https://www.w3.org/TR/WCAG/) est un ensemble de consignes reconnues internationalement et développées par le [World Wide Web Consortium (W3C)](https://www.w3.org/) dans le cadre de son [initiative sur l’accessibilité du web (WAI)](https://www.w3.org/WAI/).

>[!NOTE]
> 
> WCAG 2.1 met à jour la version précédente WCAG 2.0, à partir de 2008. Voir [WCAG 2.1 - Comparaison avec WCAG 2.0](https://www.w3.org/TR/WCAG21/#comparison-with-wcag-2-0).

>[!NOTE]
> 
>Une [version mise à jour des instructions, WCAG 2.2](https://www.w3.org/TR/WCAG22/) est actuellement en cours de développement, mais ne sera pas prise en compte pour l’instant.

WCAG 2.1 regroupe un ensemble de consignes et de critères de réussite, qui ne sont pas associés à une technologie particulière, visant à rendre les contenus web plus accessibles aux personnes en situation de handicap. Elles fournissent aux auteurs, aux concepteurs et aux développeurs de contenu web des conseils à suivre afin de s’assurer que les ressources qu’ils produisent sont aussi accessibles que possible pour autant de personnes que possible, quel que soit le handicap qu’elles peuvent avoir ; par exemple, une déficience visuelle, des troubles de l’audition, des difficultés d’apprentissage ou des restrictions liées à l’âge.

Par exemple, la description d’une image (ou de tout autre contenu non textuel) à l’aide de l’attribut `alt` dans le code HTML avantage considérablement les personnes non voyantes ou malvoyantes. La description textuelle dans l’attribut `alt` peut être convertie en sortie vocale ou transmise aux affichages électroniques en braille actualisables.

Additionally, WCAG 2.1 can result in advantages for other beneficiaries, including people who may be considered *situationally disabled*. c’est-à-dire les personnes qui, en raison de circonstances telles que la technologie de navigation, la vitesse de la connexion réseau ou l’environnement de navigation, peuvent rencontrer des obstacles similaires à ceux des personnes handicapées.

En utilisant Adobe Experience Manager, les auteurs de contenu et/ou les propriétaires de sites web peuvent créer du contenu web qui satisfait les critères de réussite des niveaux A et AA pertinents de WCAG 2.1.

Par conséquent, la compréhension des objectifs de WCAG 2.1 et de la structure des consignes représente une part importante dans la compréhension de l’accessibilité web, de même que la compréhension de la façon dont les consignes peuvent vous aider à créer du contenu web accessible.

L’objectif de WCAG 2.1 est de fournir des consignes présentant les caractéristiques suivantes :

* **Agnostiques en ce qui concerne la technologie :**
En d’autres termes, des consignes qui peuvent être appliquées à divers formats de contenu web, pas seulement au format HTML. Ainsi, WCAG 2.1 peut couvrir le contenu généré par ou fourni au format PDF, Flash, JavaScript, ainsi que d’autres technologies web actuelles et futures.

* **Testables** :
Chaque consigne est écrite de manière à pouvoir être testée objectivement pour s’assurer qu’un groupe d’experts en accessibilité conviendrait de façon générale que la consigne a été respectée. L’un des défis des consignes d’accessibilité est que, alors que certaines peuvent être testées par des moyens techniques, d’autres requièrent un jugement humain afin de vérifier si la consigne a été respectée.

* Support **prioritized and contextual implementation:**
WCAG 2.1 guidelines are given priorities, relating to the likely impact of not following a guideline on a particular group of users with disabilities. Cela permet aux auteurs de prendre une décision éclairée sur les consignes les plus importantes pour leur situation donnée. En outre, le concept de l’*accessibilité prise en charge* est introduit. Cela permet aux auteurs de prendre des décisions sur la meilleure manière d’utiliser les technologies web qui peuvent ne pas présenter l’accessibilité totale, ou peut exiger des utilisateurs qu’ils disposent de technologies d’assistance et/ou de navigateurs spécifiques, permettant ainsi de tirer profit des fonctions d’accessibilité.

Ces objectifs ont considérablement influencé la structure de WCAG 2.1.

>[!NOTE]
>
>Il n’est pas possible de créer un site web qui traite chaque handicap ou type possible de personne. L’objectif de WCAG 2.1 est d’aider les auteurs de contenu web à créer des sites qui sont, dans la mesure du possible, accessibles dans certaines conditions et dans la limite du raisonnable.

## Structure {#structure}

WCAG 2.1 présente les concepts de création de contenu web accessible d’une manière progressivement détaillée. Cela peut donner l’impression que WCAG 2.1 est un ensemble très complexe de documents liés, mais le but est de fournir (progressivement) des informations plus détaillées à mesure que les auteurs en ont besoin, plutôt que de fournir l’ensemble dans un document très volumineux.

WCAG 2.1 est constitué de quatre principes clés de conception accessible, parfois évoqués par l’acronyme **POUR**. à savoir :

1. **Perceptible** : l’utilisateur peut-il percevoir le contenu web en question ?
1. **Utilisable** : l’utilisateur peut-il saisir des données, ainsi que parcourir le contenu web ou encore interagir avec le contenu web ?
1. **Compréhensible** : l’utilisateur peut-il comprendre le contenu web qui lui est présenté ?
1. **Robuste** : le contenu web est-il disponible de la façon prévue sur une gamme assez large d’environnements de navigation, notamment anciens et émergents ?

Développons :
* Chaque **principe** consiste en une ou plusieurs **consignes**.

* Les consignes sont rédigées sous la forme d’instructions, qui sont positives (faites cela…) ou négatives (ne faites pas…).
* Les consignes sont numérotées de 1.1 à 4.1, où le premier numéro correspond au principe parent.
* Chaque consigne est composée d’un ou de plusieurs **critères de réussite**.
* Les critères de réussite sont écrits sous la forme d’instructions, qui sont `True` ou `False` pour n’importe quelle page web donnée.
* Les critères de réussite peuvent inclure des choix ou encore des exceptions (lorsque les critères de réussite ne doivent pas nécessairement être remplis).
* Les critères de réussite sont numérotés selon la consigne et le principe parents, de 1.1.1 à 4.1.1. Ils ont également un nom court qui récapitule l’objectif du critère, pour plus de commodité. For example, success criterion [1.1.1 is Non-text Content](https://www.w3.org/TR/WCAG/#non-text-content).
* Les critères de réussite incluent une liste de **techniques** associées (décrites plus en détail ci-dessous).

## Ressources annexes {#supporting-resources}

Outre les composants fondamentaux de WCAG 2.1 qui sont les principes, consignes et critères de réussite, il existe plusieurs documents annexes. Certains d’entre eux contiennent des conseils spécifiques sur la façon de respecter ces consignes. D’autres sont des références plus générales destinées à aider les programmateurs web, les concepteurs et les développeurs, quelles que soient leurs capacités, à comprendre et à utiliser WCAG 2.1 aussi efficacement que possible.

Bien que WCAG 2.1 soit un document stable et ne changera pas, la plupart de ces ressources d&#39;appui sont des documents dynamiques ; ils changeront et se développeront au fil du temps, à mesure que de nouvelles technologies émergeront, et de nouveaux exemples de la façon dont l&#39;accessibilité au web peut être atteinte.

### Ressources WCAG 2.1 {#wcag-resources}

Cette liste ne vise pas à être exhaustive, mais présente les ressources disponibles :
* [Présentation de tous les documents relatifs à WCAG](https://www.w3.org/WAI/standards-guidelines/wcag/)
* [Résumé des différents documents](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)
* [Web Content Accessibility Guidelines (WCAG) 2.1](https://www.w3.org/TR/WCAG21/)
* [Nouveautés de WCAG 2.1](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-21/)
* [Guide de référence rapide pour respecter WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)
* [Questions fréquemment posées concernant WCAG 2](https://www.w3.org/WAI/standards-guidelines/wcag/faq/)


### Nouveautés de WCAG 2.1 {#what-is-new}

Les directives fournissent des informations sur les nouveautés de WCAG 2.1 :

* [Nouveautés de WCAG 2.1](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-21/) fournit des informations précieuses sur le delta entre WCAG 2.0 et WCAG 2.1.

* La section [WCAG 2.0 et 2.1](https://www.w3.org/WAI/standards-guidelines/wcag/#versions) précise plus en détail la façon dont ces deux versions sont liées.

### Techniques relatives à WCAG 2.1 {#techniques-for-wcag}

Les techniques relatives à WCAG 2.1 sont disponibles sur la page [Techniques relatives à WCAG 2.1](https://www.w3.org/WAI/WCAG21/Techniques/).

Les **techniques** forment le niveau sous les critères de réussite dans la hiérarchie de WCAG 2.1. Elles sont classées par WAI comme étant informatives, et non normatives. En d’autres termes, une technique spécifique ne doit pas nécessairement être suivie pour qu’une ressource soit conforme à WCAG 2.1.

Étant donné que les techniques sont beaucoup plus spécifiques que les critères de réussite, elles font généralement référence à une technologie, un type de contenu (par exemple, HTML ou vidéo) ou une situation spécifique (par exemple, une application d’e-commerce ou d’apprentissage en ligne). Vous pouvez considérer les techniques comme des exemples attestés de la façon dont les consignes et les critères de réussite peuvent être respectés, de telle manière qu’elles sont utiles aux auteurs et aux développeurs travaillant dans des contextes particuliers.

Les techniques sont accessibles :

* par collection (les techniques peuvent être générales ou associées à une technologie ou un format spécifique, comme HTML, CSS ou des scripts côté client) ;
* à partir des critères de réussite correspondants. Les techniques peuvent s’appliquer à plusieurs critères de réussite.

Chaque technique a un numéro unique, qui fait référence à sa collection. For example, one of the ARIA techniques is [Technique ARIA2: Identifying a required field with the aria-required property](https://www.w3.org/WAI/WCAG21/Techniques/aria/ARIA2.html).

Les techniques peuvent être suffisantes, consultatives ou un échec :

* Une *technique suffisante* est une technique qui, si elle est suivie, sera suffisante pour répondre à un critère de réussite donné.
* Une *technique consultative* est une technique qui, si elle est suivie, aura un impact positif sur l’accessibilité, mais qui risque de ne pas être suffisante à elle seule pour assurer qu’un critère de réussite donné est rempli.
* Un *échec* est une technique décrivant un exemple spécifique à partir duquel les critères de réussite ne seraient pas remplis.

Les détails des techniques comprennent une description, l’applicabilité, des exemples, des ressources pour plus d’informations, ainsi que des détails sur la façon dont les auteurs peuvent tester la réussite de l’application de cette technique.

La liste des techniques n’est pas terminée, et WAI la met constamment à jour avec de nouveaux exemples en fonction des développements dans la technologie web, les approches de conception et l’état de la recherche. Cela vaut donc vraiment la peine de consulter régulièrement la liste des techniques afin de découvrir les nouveautés.

### Présentation de WCAG 2.1 {#understanding-wcag}

Cela se rapporte à une série de documents, qui fournissent aux lecteurs des conseils pour les aider à comprendre la finalité de consignes et de critères de réussite spécifiques. Vous pouvez [télécharger une introduction, ainsi que des liens vers des informations plus détaillées](https://www.w3.org/WAI/WCAG21/Understanding/).

Chaque consigne individuelle et critère de réussite a également sa propre page de présentation qui fournit des informations sur :

* l’objectif de la consigne ;
* les critères de réussite spécifiques ;
* les techniques consultatives, qui aident à répondre aux exigences de la consigne, mais qui ne correspondent à aucun critère de réussite spécifique.

La page de présentation de chaque critère de réussite fournit des informations sur :

* la finalité du critère de réussite ;
* des exemples généraux sur la manière dont le critère de réussite peut être rempli ;
* des ressources connexes (non W3C) sur la façon de remplir le critère de réussite ;
* des techniques et échecs : exemples spécifiques et détaillés de la façon dont le critère de réussite peut être rempli (décrits plus en détail ci-dessous) ;
* les termes clés : glossaire des termes importants pour comprendre le critère de réussite.

En voici un exemple : [Présentation du critère de réussite 1.1.1 (« contenu non textuel »)](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content).

### Conformité à WCAG 2.1 {#how-to-meet-wcag}

La section « Comment se conformer » est disponible sur la page [Comment se conformer à WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/). Cette section offre une autre présentation de WCAG, qui permet aux lecteurs d&#39;affiner le contenu des lignes directrices à ceux qui sont le plus pertinents pour leurs propres intérêts et/ou circonstances. Les lecteurs peuvent filtrer les techniques de critères de réussite qu’ils souhaitent afficher en spécifiant des technologies de contenu web particulières, telles que les feuilles de style en cascade ou les scripts, ou en spécifiant un ou plusieurs niveaux de priorité donnés.

Sans filtrage, cette ressource fournit tous les critères de réussite regroupés par consigne. Pour chaque critère de réussite, les éléments suivants sont disponibles :

* Le texte du critère de réussite
* Un lien vers le document de présentation correspondant
* Une liste des techniques suffisantes associées, avec des liens vers les détails de chaque technique
* Une liste des techniques consultatives relatives, avec des liens vers les détails de chaque technique (s’ils existent)
* Une liste des échecs associés, avec des liens vers les détails de chaque échec
