---
title: Guide rapide relatif à WCAG 2.0
seo-title: Guide rapide relatif à WCAG 2.0
description: Lisez une introduction rapide aux consignes d’accessibilité WCAG 2.0.
seo-description: Lisez une introduction rapide aux consignes d’accessibilité WCAG 2.0.
uuid: a5cf463e-89e9-4cc0-9c91-69a1fd3d8ea2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-accessibility
content-type: reference
discoiquuid: 3cac0e34-7514-48ce-a93b-592bbdbcd252
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Guide rapide relatif à WCAG 2.0{#quick-guide-to-wcag}

AEM a été développé afin d’optimiser la conformité aux consignes sur l’accessibilité du contenu web :

[WCAG2 (Web Content Accessibility Guidelines version 2.0)](https://www.w3.org/TR/WCAG/) est un ensemble de consignes reconnues internationalement et développées par le [World Wide Web Consortium (W3C)](https://www.w3.org/) dans le cadre de son [initiative sur l’accessibilité du web (WAI)](https://www.w3.org/WAI/).

WCAG 2.0 regroupe un ensemble de consignes et de critères de réussite, qui ne sont pas associés à une technologie particulière, visant à rendre les contenus web plus accessibles aux personnes en situation de handicap. Elles fournissent aux auteurs, aux concepteurs et aux développeurs de contenu web des conseils à suivre afin de s’assurer que les ressources qu’ils produisent sont aussi accessibles que possible pour autant de personnes que possible, quel que soit le handicap qu’elles peuvent avoir ; par exemple, une déficience visuelle, des troubles de l’audition, des difficultés d’apprentissage ou des restrictions liées à l’âge.

Par exemple, la description d’une image (ou de tout autre contenu non textuel) à l’aide de l’attribut `alt` dans le code HTML avantage considérablement les personnes non voyantes ou malvoyantes. The textual description in the `alt` attribute can either be converted into speech output or transmitted to electronic refreshable braille displays.

En outre, WCAG 2.0 peut présenter des avantages pour d’autres bénéficiaires, y compris les personnes qui peuvent être *handicapées par rapport à la situation*, c’est-à-dire les personnes qui, en raison de circonstances telles que la technologie de navigation, la vitesse de la connexion réseau ou l’environnement de navigation, peuvent rencontrer des obstacles similaires à ceux des personnes handicapées.

En utilisant Adobe Experience Manager, les auteurs de contenu et/ou les propriétaires de sites web peuvent créer du contenu web qui satisfait les critères de réussite des niveaux A et AA pertinents de WCAG 2.0.

Par conséquent, la compréhension des objectifs de WCAG 2.0 et de la structure des consignes représente une part importante dans la compréhension de l’accessibilité web, de même que la compréhension de la façon dont les consignes peuvent vous aider à créer du contenu web accessible.

L’objectif de WCAG 2.0 est de fournir des consignes présentant les caractéristiques suivantes :

* Sont **agnostiques en matière de technologie :**

   En d’autres termes, des directives qui peuvent être appliquées à une gamme de formats de contenu Web, et pas seulement au format HTML. Ainsi, WCAG 2.0 peut couvrir le contenu généré par ou fourni au format PDF, Flash, JavaScript, ainsi que d’autres technologies web actuelles et futures. Cela vise à corriger une faiblesse identifiée de WCAG 1.0, dans la mesure où il était axé sur le format HTML au détriment d’autres formats de contenu web.

* Sont **testables :**

   Chaque ligne directrice est rédigée de manière à pouvoir être vérifiée objectivement pour s&#39;assurer qu&#39;un groupe d&#39;experts en accessibilité convienne généralement que la ligne directrice a été respectée. L’un des défis des consignes d’accessibilité est que, alors que certaines peuvent être testées par des moyens techniques, d’autres requièrent un jugement humain afin de vérifier si la consigne a été respectée. WCAG 2.0 a été écrit dans le but de réduire la subjectivité de certaines consignes et certains points de contrôle de WCAG 1.0.

* Prise en charge de l’implémentation contextuelle et **prioritaire :**

   Comme pour WCAG 1.0, les lignes directrices de WCAG 2.0 se voient attribuer des priorités, en ce qui a trait à l&#39;incidence probable de ne pas suivre une ligne directrice sur un groupe particulier d&#39;utilisateurs ayant une déficience. Cela permet aux auteurs de prendre une décision éclairée sur les consignes les plus importantes pour leur situation donnée. En outre, le concept de l’*accessibilité prise en charge* est introduit. Cela permet aux auteurs de prendre des décisions sur la meilleure manière d’utiliser les technologies web qui peuvent ne pas présenter l’accessibilité totale, ou peut exiger des utilisateurs qu’ils disposent de technologies d’assistance et/ou de navigateurs spécifiques, permettant ainsi de tirer profit des fonctions d’accessibilité.

Ces objectifs ont considérablement influencé la structure de WCAG 2.0.

>[!NOTE]
>
>Il n’est pas possible de créer un site web qui traite chaque handicap ou type possible de personne. L’objectif de WCAG 2.0 est d’aider les auteurs de contenu web à créer des sites qui sont, dans la mesure du possible, accessibles dans certaines conditions et dans la limite du raisonnable.

>[!NOTE]
>
>Si vous êtes familiarisé avec WCAG 1.0, vous constaterez certaines modifications dans WCAG 2.0. Elles concernent la portée, l’organisation et l’objectif.

## Structure {#structure}

WCAG 2.0 présente les concepts de création de contenu web accessible d’une manière progressivement détaillée. Cela peut donner l’impression que WCAG 2.0 est un ensemble très complexe de documents liés, mais le but est de fournir (progressivement) des informations plus détaillées à mesure que les auteurs en ont besoin, plutôt que de fournir l’ensemble dans un document très volumineux.

WCAG 2.0 est constitué de quatre principes clés pour la conception accessible. à savoir :

1. **Perceptible** : l’utilisateur peut-il percevoir le contenu web en question ?
1. **Utilisable** : l’utilisateur peut-il saisir des données, ainsi que parcourir le contenu web ou encore interagir avec le contenu web ?
1. **Compréhensible** : l’utilisateur peut-il comprendre le contenu web qui lui est présenté ?
1. **Robuste** : le contenu web est-il disponible de la façon prévue sur une gamme assez large d’environnements de navigation, notamment anciens et émergents ?

Ces principes sont parfois indiqués par l’acronyme POUR en anglais (correspondant à Perceivable, Operable, Understandable et Robust).

* Chaque **principe** consiste en une ou plusieurs **consignes**.

   * Les consignes sont rédigées sous la forme d’instructions, qui sont positives (faites cela…) ou négatives (ne faites pas…).
   * Les consignes sont numérotées de 1.1 à 4.1, où le premier numéro correspond au principe parent.

* Chaque consigne est composée d’un ou de plusieurs **critères de réussite**.

   * Success criteria are written as statements, which are either `True` or `False` for any given web page.
   * Les critères de réussite peuvent inclure des choix ou encore des exceptions (lorsque les critères de réussite ne doivent pas nécessairement être remplis).
   * Les critères de réussite sont numérotés selon la consigne et le principe parents, de 1.1.1 à 4.1.1. Ils ont également un nom court qui récapitule l’objectif du critère, pour plus de commodité. Par exemple, le critère de réussite 1.1.1 est « alternative non textuelle ».
   * Success criteria include a list of related **techniques** (described in more detail below).

## Ressources annexes {#supporting-resources}

Outre les composants fondamentaux de WCAG 2.0 qui sont les principes, consignes et critères de réussite, il existe plusieurs documents annexes. Certains d’entre eux contiennent des conseils spécifiques sur la façon de respecter ces consignes. D’autres sont des références plus générales destinées à aider les programmateurs web, les concepteurs et les développeurs, quelles que soient leurs capacités, à comprendre et à utiliser WCAG 2.0 aussi efficacement que possible.

WCAG 2.0 est un document stable qui ne changera pas. Toutefois, la plupart de ces ressources annexes sont des documents dynamiques ; elles changeront et se développeront au fil du temps, à mesure que de nouvelles technologies et de nouveaux exemples seront disponibles sur la façon de parvenir à l’accessibilité web.

### Ressources WCAG 2.0 {#wcag-resources}

* [Présentation de tous les documents relatifs à WCAG 2.0](https://www.w3.org/WAI/intro/wcag.php)
* [Explication de la manière dont les composants individuels sont liés les uns aux autres](https://www.w3.org/WAI/intro/wcag20)
* [Questions fréquemment posées concernant WCAG 2.0](https://www.w3.org/WAI/WCAG20/wcag2faq.html)

### Techniques relatives à WCAG 2.0 {#techniques-for-wcag}

Les techniques relatives à WCAG 2.0 sont disponibles sur la page [Techniques relatives à WCAG 2.0](https://www.w3.org/TR/WCAG20-TECHS/).

Les **techniques** forment le niveau sous les critères de réussite dans la hiérarchie de WCAG 2.0. Elles sont classées par WAI comme étant informatives, et non normatives. En d’autres termes, une technique spécifique ne doit pas nécessairement être suivie pour qu’une ressource soit conforme à WCAG 2.0.

Étant donné que les techniques sont beaucoup plus spécifiques que les critères de réussite, elles font généralement référence à une technologie, un type de contenu (par exemple, HTML ou vidéo) ou une situation spécifique (par exemple, une application d’e-commerce ou d’apprentissage en ligne). Vous pouvez considérer les techniques comme des exemples attestés de la façon dont les consignes et les critères de réussite peuvent être respectés, de telle manière qu’elles sont utiles aux auteurs et aux développeurs travaillant dans des contextes particuliers.

Les techniques sont accessibles :

* Par collection (les techniques peuvent être générales ou se rapporter à une technologie ou un format spécifique (HTML, CSS ou script côté client, par exemple), ou
* à partir des critères de réussite correspondants. Les techniques peuvent s’appliquer à plusieurs critères de réussite.

Chaque technique a un numéro unique, qui fait référence à sa collection. Par exemple, l’une des techniques ARIA est la *technique ARIA2 : identification des champs obligatoires avec la propriété « required »*.

Les techniques peuvent être suffisantes, consultatives ou un échec :

* Une *technique suffisante* est une technique qui, si elle est suivie, sera suffisante pour répondre à un critère de réussite donné.
* Une *technique consultative* est une technique qui, si elle est suivie, aura un impact positif sur l’accessibilité, mais qui risque de ne pas être suffisante à elle seule pour assurer qu’un critère de réussite donné est rempli.
* Un *échec* est une technique décrivant un exemple spécifique à partir duquel les critères de réussite ne seraient pas remplis.

Les détails des techniques comprennent une description, l’applicabilité, des exemples, des ressources pour plus d’informations, ainsi que des détails sur la façon dont les auteurs peuvent tester la réussite de l’application de cette technique.

La liste des techniques n’est pas terminée, et WAI la met constamment à jour avec de nouveaux exemples en fonction des développements dans la technologie web, les approches de conception et l’état de la recherche. Cela vaut donc vraiment la peine de consulter régulièrement la liste des techniques afin de découvrir les nouveautés.

### Présentation de WCAG 2.0 {#understanding-wcag}

Cela se rapporte à une série de documents, qui fournissent aux lecteurs des conseils pour les aider à comprendre la finalité de consignes et de critères de réussite spécifiques. Vous pouvez [télécharger une introduction, ainsi que des liens vers des informations plus détaillées](https://www.w3.org/TR/2008/NOTE-UNDERSTANDING-WCAG20-20081211/Overview.html).

Chaque consigne individuelle et critère de réussite a également sa propre page de présentation qui fournit des informations sur :

* l’objectif de la consigne ;
* les critères de réussite spécifiques ;
* les techniques consultatives, qui aident à répondre aux exigences de la consigne, mais qui ne correspondent à aucun critère de réussite spécifique.

La page de présentation de chaque critère de réussite fournit des informations sur :

* la finalité du critère de réussite ;
* des exemples généraux sur la manière dont le critère de réussite peut être rempli ;
* des ressources connexes (non W3C) sur la façon de remplir le critère de réussite ;
* Techniques et échecs : exemples spécifiques et détaillés de la manière dont le critère de réussite peut être satisfait (décrits plus en détail ci-dessous)
* Termes clés - glossaire de termes importants pour comprendre le critère de réussite.

En voici un exemple : [Présentation du critère de réussite 1.1.1 (« contenu non textuel »)](https://www.w3.org/TR/2008/NOTE-UNDERSTANDING-WCAG20-20081211/text-equiv-all.html).

### Conformité à WCAG 2.0 {#how-to-meet-wcag}

La section « Comment se conformer » est disponible sur la page [Comment se conformer à WCAG 2.0](https://www.w3.org/WAI/WCAG20/quickref/). Cette section fournit une autre présentation de WCAG, permettant d’affiner le contenu des consignes en fonction de ce qui correspond le plus aux intérêts ou aux circonstances particulières du lecteur. Les lecteurs peuvent filtrer les techniques de critères de réussite qu’ils souhaitent afficher en spécifiant des technologies de contenu web particulières, telles que les feuilles de style en cascade ou les scripts, ou en spécifiant un ou plusieurs niveaux de priorité donnés.

Sans filtrage, cette ressource fournit tous les critères de réussite regroupés par consigne. Pour chaque critère de réussite, les éléments suivants sont disponibles :

* Le texte du critère de réussite
* Un lien vers le document de présentation correspondant
* Une liste des techniques suffisantes associées, avec des liens vers les détails de chaque technique
* Une liste des techniques consultatives relatives, avec des liens vers les détails de chaque technique (s’ils existent)
* Une liste des échecs associés, avec des liens vers les détails de chaque échec