---
title: Instructions et bonnes pratiques d’accessibilité pour la création de formulaires dans Forms Designer
description: Bonnes pratiques et instructions relatives à l’accessibilité lors du développement de formulaires dans Forms Designer.
feature: Adaptive Forms, Forms Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 0948231a-bd9e-4d29-946d-2d8c17e27c28
source-git-commit: 16b46340c5e0775d19f22f57bca5ea9ab584c51e
workflow-type: ht
source-wordcount: '3366'
ht-degree: 100%

---

# Alignement des conseils et des bonnes pratiques

Les sections suivantes mappent les instructions de la section 508 et WCAG aux bonnes pratiques décrites dans ce guide.

## § 1194.21 Description et bonnes pratiques de directives

### Section 508 §1194.21 : applications logicielles et systèmes d’exploitation

| § 1194.21 Directives | Description des directives | Bonnes pratiques de LiveCycle Designer requises pour la conformité | Notes |
|-----------|-----------------------|-----------------------------------------------------------|-------|
| (a) | Lorsque le logiciel est conçu pour fonctionner sur un système disposant d’un clavier, les fonctions du produit doivent être exécutables à partir d’un clavier où la fonction elle-même, ou le résultat de l’exécution d’une fonction, peut être détectée textuellement. | <li> 2.7 Assurer l’accessibilité au clavier des commandes de formulaire </li><li> 2.6 Assurer l’ordre correct de lecture et de tabulation</li> | |
| (b) | Les applications ne doivent pas perturber ou désactiver les fonctionnalités activées d’autres produits identifiées comme des fonctionnalités d’accessibilité, lorsque ces fonctionnalités sont développées et documentées conformément aux normes du secteur. Les applications ne doivent pas non plus perturber ou désactiver les fonctionnalités activées d’un système d’exploitation identifiées comme des fonctionnalités d’accessibilité lorsque l’interface de programmation de l’application pour ces fonctionnalités d’accessibilité a été documentée par le fabricant du système d’exploitation et est disponible pour le développeur ou la développeuse du produit. | Aucune technique spécifique à LiveCycle Designer : cette directive est gérée par Adobe Reader pour les formulaires PDF. | |
| (c) | Une indication bien définie à l’écran du focus actuel doit être fournie pour que les éléments de l’interface interactive se déplacent au fur et à mesure que le focus change. Le focus doit être exposé par programmation afin que la technologie d’assistance puisse suivre le focus et ses changements. | 2.3 Choisir les commandes appropriées pour s’assurer que la sélection est exposée par programmation et visuellement, en utilisant toujours les commandes standard. | |
| (d) | Les technologies d’assistance doivent disposer d’informations suffisantes sur un élément d’interface d’utilisation, y compris l’identité, le fonctionnement et l’état de l’élément. Lorsqu’une image représente un élément de programme, les informations véhiculées par l’image doivent également être disponibles dans le texte. | <ul><li>2.1 Simplification et facilité d’utilisation des formulaires</li> <li>2.1.1 Éviter le contenu mobile, clignotant ou scintillant</li> <li>2.2 Configurer des propriétés de formulaire pour générer des informations d’accessibilité</li> <li>2.5 Fournir des libellés appropriés pour les commandes de formulaire</li></ul> | |
| (e) | Lorsque des images bitmap sont utilisées pour identifier des commandes, des indicateurs de statut ou d’autres éléments de programmation, la signification qui leur est affectée doit être cohérente tout au long des performances d’une application. | <ul><li>2.4 Fournir des équivalents textuels pour les images</li><li> 2.5 Fournir des libellés appropriés pour les commandes de formulaire. Cette norme s’applique uniquement si vous utilisez la même image à plusieurs endroits sur un formulaire. L’utilisation de commandes personnalisées basées sur des images n’est pas recommandée. Utilisez uniquement les commandes standard fournies par LiveCycle Designer. Si vous utilisez des images dans vos commandes, assurez-vous toujours qu’elles sont utilisées de manière cohérente.</li> | |
| (f) | Les informations textuelles doivent être fournies par le biais des fonctions du système d’exploitation pour l’affichage du texte. Les informations minimales qui doivent être mises à disposition sont le contenu textuel, l’emplacement du caret de saisie de texte et les attributs de texte. | 2.3 Choisir les commandes appropriées. Éviter d’utiliser des images pour véhiculer des informations textuelles. Au lieu d’utiliser des composants d’entrée personnalisés qui peuvent ne pas exposer correctement les propriétés de texte au système d’exploitation, utilisez toujours les commandes standard. | |
| (g) | Les applications ne doivent pas remplacer les sélections de contraste et de couleur sélectionnées par l’utilisateur ou l’utilisatrice, ainsi que d’autres attributs d’affichage individuels. | Aucune technique spécifique à LiveCycle Designer | Si possible, utilisez les couleurs système par défaut de base. |
| (h) | Lorsque l’animation est affichée, l’information doit être affichée dans au moins un mode de présentation non animé, au choix de l’utilisateur ou de l’utilisatrice. | 2.1 Simplifier et faciliter l’utilisation des formulaires. Éviter d’utiliser des animations dans vos formulaires ou fournir des versions distinctes dans lesquelles les animations sont remplacées par des images statiques. | |
| (i) | Le codage par couleur ne doit pas être utilisé comme seul moyen visuel de transmettre des informations, d’indiquer une action, de demander une réponse ou de distinguer un élément visuel. | 2.8 Utiliser des couleurs de manière responsable | |
| (j) | Lorsqu’un produit permet à la personne d’ajuster les paramètres de couleur et de contraste, diverses sélections de couleurs capables de produire une gamme de niveaux de contraste doivent être fournies. | Non applicable | Cette fonctionnalité est généralement fournie par Adobe Reader, et non par le développeur ou la développeuse de formulaires. |
| (k) | Le logiciel ne doit pas utiliser de texte clignotant ou scintillant, d’objets ou d’autres éléments ayant une fréquence de clignotement ou de scintillement supérieure à 2 Hz et inférieure à 55 Hz. | 2.1.1 Éviter le contenu mobile, clignotant ou scintillant | |
| (l) | Lorsque des formulaires électroniques sont utilisés, le formulaire doit permettre aux personnes qui utilisent des dispositifs d’assistance d’accéder aux informations, aux éléments de champ et aux fonctionnalités nécessaires à la réalisation et à l’envoi du formulaire, y compris toutes les instructions et tous les repères. | 2.5 Fournir des libellés appropriés pour les commandes de formulaire | |

### Section 508 §11942 : informations et applications web intranet et internet

| §11942 Directives | Description des directives | Bonnes pratiques de LiveCycle Designer requises pour la conformité | Notes |
|-----------|-----------------------|-----------------------------------------------------------|-------|
| (a) | Un équivalent textuel pour chaque élément non textuel doit être fourni (par exemple, par « alt », « longdesc » ou dans le contenu de l’élément). | 2.4 Fournir des équivalents textuels pour les images | |
| (b) | Les alternatives équivalentes à toute présentation multimédia doivent être synchronisées avec la présentation. | 2.12 Assurer l’accessibilité de tout le contenu multimédia | |
| (c) | Les pages web doivent être conçues de sorte que toutes les informations véhiculées par la couleur soient également disponibles sans couleur, par exemple à partir du contexte ou des balises. | 2.8 Utiliser des couleurs de manière responsable | |
| (d) | Les documents doivent être organisés de sorte qu’ils soient lisibles sans qu’une feuille de style associée ne soit nécessaire. | Non applicable | |
| (e) | Des liens de texte redondants doivent être fournis pour chaque zone active d’une image interactive sur le serveur. | Non applicable | |
| (f) | Les images interactives sur le client doivent être fournies au lieu des images interactives sur le serveur, sauf lorsque les zones ne peuvent pas être définies avec une forme géométrique disponible. | Non applicable | |
| (g) | Les en-têtes de ligne et de colonne doivent être identifiés pour les tableaux de données. | 2.9 Fournir des cellules d’en-tête pour les tableaux | |
| (h) | Les balises doivent être utilisées pour associer des cellules de données et des cellules d’en-tête aux tableaux de données qui comportent deux niveaux logiques ou plus d’en-têtes de ligne ou de colonne. | 2.9 Fournir des cellules d’en-tête pour les tableaux | |
| (i) | Les cadres doivent être intitulés avec du texte qui facilite leur identification et leur navigation. | Non applicable | |
| (j) | Les pages doivent être conçues pour éviter que l’écran scintille avec une fréquence supérieure à 2 Hz et inférieure à 55 Hz. | 2.1 Simplification et facilité d’utilisation des formulaires | |
| (k) | Une page texte uniquement, avec des informations ou des fonctionnalités équivalentes, doit être fournie pour qu’un site web soit conforme aux dispositions de la présente partie, lorsque la conformité ne peut être réalisée d’aucune autre manière. Le contenu de la page texte uniquement doit être mis à jour chaque fois que la page principale change. | Non applicable | |
| (l) | Lorsque les pages utilisent des langages de script pour afficher du contenu ou pour créer des éléments d’interface, les informations fournies par le script doivent être identifiées avec du texte fonctionnel pouvant être lu par les dispositifs d’assistance. | 2.11 Éviter les scripts perturbateurs | |
| (m) | Lorsqu’une page web requiert la présence d’une applet, d’un plug-in ou d’une autre application sur le système client pour interpréter le contenu d’une page, elle doit fournir un lien vers un plug-in ou une applet conforme à §1194.21(a) à (l). | Non applicable | Les pages web liées aux formulaires PDF doivent fournir un lien vers Adobe Reader. |
| (n) | Lorsque les formulaires électroniques sont conçus pour être remplis en ligne, le formulaire doit permettre aux personnes qui utilisent des dispositifs d’assistance d’accéder aux informations, aux éléments de champ et aux fonctionnalités nécessaires à la réalisation et à l’envoi du formulaire, y compris toutes les instructions et tous les repères. | 2.5 Fournir des libellés appropriés pour les commandes de formulaire | |
| (o) | Une méthode permettant aux utilisateurs et utilisatrices d’ignorer les liens de navigation répétitifs doit être fournie. | 2.10 Fournir une structure de formulaire navigable | |
| (p) | Lorsqu’une réponse minutée est requise, la personne doit être alertée et disposer de suffisamment de temps pour indiquer qu’il lui faut plus de temps. | 2.11 Éviter les scripts perturbateurs | |

### Points de contrôle de priorité 1 WCAG 1.0

| Point de contrôle | Description du point de contrôle | Bonnes pratiques de LiveCycle Designer requises pour la conformité | Notes |
|------------|------------------------|-----------------------------------------------------------|-------|
| [1.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-text-equivalent) | Fournir une équivalence de texte pour chaque élément non textuel (par exemple, par « alt », « longdesc » ou dans le contenu de l’élément). Cela comprend : les images, les représentations graphiques du texte (y compris les symboles), les zones cliquables, les animations (par exemple, les GIF animés), les applets et les objets programmatiques, les illustrations ASCII, les cadres, les scripts, les images utilisées comme puces de liste, les espaces, les boutons graphiques, les sons (lus avec ou sans interaction de l’utilisateur ou de l’utilisatrice), les fichiers audio autonomes, les pistes audio de vidéo et les fichiers vidéo. | <ul><li>2.4 Fournir des équivalents textuels pour les images</li> <li>2.12 Assurer l’accessibilité de tout le contenu multimédia</li> | |
| [1.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-redundant-server-links) | Fournir des liens de texte redondants pour chaque zone active d’une zone cliquable côté serveur. | Non applicable | |
| [1.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-auditory-descriptions) | Tant que les agents utilisateurs ne sont pas en mesure de lire automatiquement à voix haute l’équivalent textuel d’une piste visuelle, fournir une description auditive des informations importantes de la piste visuelle d’une présentation multimédia. | 2.12 Assurer l’accessibilité de tout le contenu multimédia | |
| [1.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-synchronize-equivalents) | Pour toute présentation multimédia temporisée (par exemple, un film ou une animation), synchroniser les alternatives équivalentes (par exemple, les sous-titres ou la description auditive de la piste visuelle) avec la présentation. | 2.12 Assurer l’accessibilité de tout le contenu multimédia | |
| [2.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-color-convey) | S’assurer que toute information véhiculée par des couleurs est également accessible sans couleur, par exemple à partir du contexte ou de balises. | 2.8 Utiliser des couleurs de manière responsable | |
| [4.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-identify-changes) | Identifier clairement les changements survenus dans le langage naturel du texte d’un document et équivalents (par exemple, les légendes). | 2.13 Identifier les changements dans le langage | |
| [5.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-headers) | Pour les tableaux de données, identifier les en-têtes de lignes et de colonnes. | 2.9 Fournir des cellules d’en-tête pour les tableaux | |
| [5.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-structure) | Pour les tableaux de données qui ont deux niveaux logiques d’en-tête de ligne ou de colonne ou plus, utiliser des balises pour associer les cellules de données et les cellules d’en-tête. | 2.9 Fournir des cellules d’en-tête pour les tableaux | |
| [6.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-order-style-sheets) | Organiser les documents de manière à ce qu’ils puissent être lus sans feuilles de style. Par exemple, lorsqu’un document HTML est restitué sans feuille de style associée, il doit rester lisible. | Non applicable | |
| [6.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-dynamic-source) | S’assurer que les équivalences pour le contenu dynamique soient mises à jour lorsque ledit contenu dynamique change. | 2.11 Éviter les scripts perturbateurs | |
| [6.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-scripts) | S’assurer que les pages soient visibles lorsque les scripts, les applets ou autres objets de programmation sont désactivés ou non pris en charge. Si cela n’est pas possible, fournissez des informations équivalentes sur une autre page accessible. | 2.11 Éviter les scripts perturbateurs | |
| [7.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-flicker) | Tant que les agents utilisateurs ne permettent pas aux utilisateurs et utilisatrices de contrôler le clignotement, éviter de faire clignoter l’écran. | 2.1 Simplification et facilité d’utilisation des formulaires | |
| [9.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-client-side-maps) | Prévoir des zones cliquables côté client au lieu de zones cliquables côté serveur, sauf lorsque les zones ne peuvent pas être définies par des formes géométriques disponibles. | Non applicable | |
| [11.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-alt-pages) | Si, malgré vos efforts, vous ne parvenez pas à créer de page accessible, fournissez un lien vers une autre page qui utilise les technologies W3C, est accessible, dispose d’informations (ou de fonctionnalités) équivalentes et est mise à jour aussi souvent que la page inaccessible (d’origine). | Non applicable | |
| [12.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-frame-titles) | Donner un titre à chaque cadre pour faciliter l’identification et la navigation entre les cadres. | Non applicable | |
| [14.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-simple-and-straightforward) | Utiliser le langage le plus clair et le plus simple possible adapté au contenu de votre site. | 2.1 Simplification et facilité d’utilisation des formulaires | |

### Points de contrôle de priorité 2 WCAG 1.0

| Point de contrôle de priorité 2 | Description du point de contrôle | Bonnes pratiques LiveCycle requises pour la conformité | Notes |
|------------|------------------------|-------------------------------------------------|-------|
| [2.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-color-contrast) | S’assurer que la combinaison de couleurs entre le premier plan et l’arrière-plan offre suffisamment de contraste lorsqu’elle est utilisée par des personnes souffrant d’un déficit de perception des couleurs ou sur un écran noir et blanc. [Priorité 2 pour les images, priorité 3 pour le texte]. | 2.8 Utiliser des couleurs de manière responsable | |
| [3.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-use-markup) | Quand un langage de balisage approprié existe, utiliser des balises plutôt que des images pour véhiculer l’information. | <ul><li>2.1 Simplification et facilité d’utilisation des formulaires</li><li> 2.1.1 Éviter le contenu mobile, clignotant ou scintillant</li> <li>2.2 Configurer les propriétés du formulaire pour générer des informations d’accessibilité. Utiliser toujours du texte réel plutôt que des images de texte.</li> | |
| [3.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-identify-grammar) | Créez des documents qui valident la grammaire formelle publiée. | | Les formulaires PDF doivent correspondre à la spécification de PDF publiée pour effectuer le rendu dans Adobe Reader. |
| [3.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-style-sheets) | Utilisez des feuilles de style pour contrôler la disposition et la présentation. | Non applicable | |
| [3.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-relative-units) | Utilisez des unités relatives plutôt que des unités absolues dans les valeurs d’attribut de langage de balisage et les valeurs de propriété de feuille de style. | Non applicable | |
| [3.5](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-logical-headings) | Utilisez des éléments d’en-tête pour transmettre la structure du document et utilisez-les selon les spécifications. | 2.10 Fournir une structure de formulaire navigable | |
| [3.6](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-list-structure) | Balisez correctement les listes et les éléments de liste. | 2.10.3 Balisage des listes. Balisez le contenu basé sur une liste en tant que listes à l’aide des rôles Liste et Élément de liste. | |
| [3.7](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-quotes) | Balisez les citations. N’utilisez pas de balises de citation pour les effets de formatage tels que la mise en retrait. | Non applicable | |
| [5.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-table-for-layout) | N’utilisez pas de tableaux pour la disposition, sauf si le tableau est linéarisé. Sinon, si le tableau n’a pas de sens, fournissez un équivalent (qui peut être une version linéarisée). | Aucune technique de LiveCycle spécifique | Il n’y a aucune raison d’utiliser des tableaux pour la disposition dans les formulaires LiveCycle. Utilisez plutôt la palette Disposition pour placer les champs du formulaire dans un modèle de grille. N’utilisez un tableau que lorsque vous utilisez des fonctionnalités spécifiques au tableau, telles que les en-têtes de tableau. |
| [5.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-table-layout) | Si un tableau est utilisé pour la disposition, n’utilisez pas de balisage structurel dans le cadre de la mise en forme visuelle. | Aucune technique de LiveCycle spécifique | |
| [6.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-keyboard-operable-scripts) | Pour les scripts et les applets, assurez-vous que les gestionnaires d’événements sont indépendants de l’appareil d’entrée. | 2.7 Assurer l’accessibilité au clavier des commandes de formulaire | |
| [6.5](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-fallback-page) | Assurez-vous que le contenu dynamique est accessible ou fournissez une autre présentation ou page. | 2.11 Éviter les scripts perturbateurs | |
| [7.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-blinking) | Tant que les agents utilisateurs et agentes utilisatrices ne permettent pas aux utilisateurs et utilisatrices de contrôler le clignotement, évitez de provoquer le clignotement du contenu (c’est-à-dire, modifiez régulièrement la présentation, par exemple en activant et en désactivant). | 2.1 Simplification et facilité d’utilisation des formulaires | |
| [7.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-movement) | Tant que les agents utilisateurs et agentes utilisatrices ne permettent pas aux utilisateurs et utilisatrices de geler le contenu en mouvement, évitez les mouvements dans les pages. | 2.1 Simplification et facilité d’utilisation des formulaires | |
| [7.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-no-periodic-refresh) | Tant que les agents utilisateurs et agentes utilisatrices ne permettent pas d’arrêter l’actualisation, ne créez pas de pages à actualisation automatique périodique. | Non applicable | |
| [7.5](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-no-auto-forward) | Tant que les agents utilisateurs et agentes utilisatrices ne permettent pas d’arrêter la redirection automatique, n’utilisez pas de balisage pour rediriger automatiquement les pages. Configurez plutôt le serveur pour effectuer les redirections. | Non applicable | |
| [8.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-directly-accessible) | Rendez les éléments de programmation tels que les scripts et les applets directement accessibles ou compatibles avec les technologies d’assistance [Priorité 1 si la fonctionnalité est importante et n’est pas présentée ailleurs, sinon Priorité 2.] | 2.11 Éviter les scripts perturbateurs | |
| [9.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-keyboard-operable) | Assurez-vous que tout élément possédant sa propre interface peut être utilisé indépendamment de l’appareil. | 2.7 Assurer l’accessibilité au clavier des commandes de formulaire | |
| [9.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-device-independent-events) | Pour les scripts, spécifiez des gestionnaires d’événements logiques plutôt que des gestionnaires d’événements dépendants de l’appareil. | 2.7 Assurer l’accessibilité au clavier des commandes de formulaire | |
| [10.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-pop-ups) | Tant que les agents utilisateurs et agentes utilisatrices ne permettent pas aux utilisateurs et utilisatrices de désactiver les fenêtres générées, ne provoquez pas l’affichage de fenêtres contextuelles ou autres et ne modifiez pas la fenêtre active sans en informer l’utilisateur ou l’utilisatrice. | 2.11 Éviter les scripts perturbateurs | |
| [10.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-unassociated-labels) | Tant que les agents utilisateurs et agentes utilisatrices ne prennent pas en charge les associations explicites entre les libellés et les commandes de formulaire, pour toutes les commandes de formulaire avec des libellés implicitement associés, assurez-vous que le libellé est correctement positionné. | 2.5 Fournir des libellés appropriés pour les commandes de formulaire | |
| [11.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-latest-w3c-specs) | Utilisez les technologies W3C lorsqu’elles sont disponibles et adaptées à une tâche et utilisez les dernières versions lorsqu’elles sont prises en charge. | Non applicable | |
| [11.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-avoid-deprecated) | Évitez les fonctionnalités obsolètes des technologies W3C. | Non applicable | |
| [12.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-frame-longdesc) | Décrivez l’objectif des cadres et la façon dont les cadres se relient les uns aux autres si leurs seuls titres ne sont pas évidents. | Non applicable | |
| [12.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-group-information) | Divisez de grands blocs d’informations en groupes plus faciles à gérer, le cas échéant. | 2.10 Fournir une structure de formulaire navigable | |
| [12.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-associate-labels) | Associez explicitement les libellés à leurs commandes. | 2.5 Fournir des libellés appropriés pour les commandes de formulaire | |
| [13.1](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-meaningful-links) | Identifiez clairement la cible de chaque lien. | 2.5 Fournir des libellés appropriés pour les commandes de formulaire 2.5.6 Fourniture du texte de lien | |
| [13.2](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-use-metadata) | Fournir des métadonnées pour ajouter des informations sémantiques aux pages et aux sites. | Non applicable | |
| [13.3](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-site-description) | Fournissez des informations sur la disposition générale d’un site (par exemple, un plan de site ou une table des matières). | 2.10 Fournir une structure de formulaire navigable | |
| [13.4](https://www.w3.org/TR/WCAG10/wai-pageauth.html#tech-clear-nav-mechanism) | Utilisez les mécanismes de navigation de manière cohérente. | 2.10 Fournir une structure de formulaire navigable | Utilisez des gabarits pour créer un contenu de navigation cohérent. |

### Critères de réussite WCAG 2.0

| Points de contrôle Priorité 1 G 2 | Bonnes pratiques LiveCycle requises pour la conformité | Notes |
| --- | --- | --- |
| 1.1 [Équivalents textuels](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv.html) | | |
| 1.1.1 [Contenu non textuel](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv-all.html) | 2.4 Fournir des équivalents textuels pour les images | |
| | 2.5 Fournir des libellés appropriés pour les commandes de formulaire | |
| 1.2 [Média temporel](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv.html) | | |
| 1.2.1 [Contenu seulement audio ou vidéo (pré-enregistré)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-av-only-alt.html) | 2.12 Assurer l’accessibilité de tout le contenu audio et vidéo | |
| 1.2.2 [Légendes (pré-enregistrées)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-captions.html) | 2.12 Assurer l’accessibilité de tout le contenu audio et vidéo | |
| 1.2.3 [Audio-description ou version de remplacement pour un média (pré-enregistré)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc.html) | 2.12 Assurer l’accessibilité de tout le contenu audio et vidéo | |
| 1.2.4 [Légendes (en direct)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-real-time-captions.html) | 2.12 Assurer l’accessibilité de tout le contenu audio et vidéo | |
| 1.2.5 [Audio-description (pré-enregistrée)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc-only.html) | 2.12 Assurer l’accessibilité de tout le contenu audio et vidéo | |
| 1.2.6 [Langue des signes (pré-enregistrée)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-sign.html) | 2.12 Assurer l’accessibilité de tout le contenu audio et vidéo | |
| 1.2.7 [Audio-description étendue (pré-enregistrée)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-extended-ad.html) | 2.12 Assurer l’accessibilité de tout le contenu audio et vidéo | |
| 1.2.8 [Média de remplacement (pré-enregistré)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-text-doc.html) | 2.12 Assurer l’accessibilité de tout le contenu audio et vidéo | |
| 1.2.9 [Contenu audio uniquement (en direct)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-live-audio-only.html) | 2.12 Assurer l’accessibilité de tout le contenu audio et vidéo | |
| 1.3 [Adaptable](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation.html) | | |
| 1.3.1 [Informations et relations](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html) | 2.9 Fournir des cellules d’en-tête pour les tableaux | |
| 1.3.2 [Séquence significative](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-sequence.html) | 2.6 Assurer l’ordre correct de lecture et de tabulation | |
| | 2.10 Fournir une structure de formulaire navigable | |
| 1.3.3 [Caractéristiques sensorielles](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-understanding.html) | 2.8 Utiliser des couleurs de manière responsable | |
| 1.4 [Perceptible](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast.html) | | |
| 1.4.1 [Utilisation de la couleur](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-without-color.html) | 2.8 Utiliser des couleurs de manière responsable | |
| 1.4.2 [Commande audio](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-dis-audio.html) | Aucune technique de LiveCycle spécifique | |
| 1.4.3 [Contraste (minimum)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html) | 2.8 Utiliser des couleurs de manière responsable | |
| 1.4.4 [Redimensionner le texte](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-scale.html) | Aucune technique de LiveCycle spécifique | |
| 1.4.5 [Texte sous forme d’image](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-presentation.html) | Aucune technique de LiveCycle spécifique | |
| 1.4.6 [Contraste (amélioré)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast7.html) | 2.8 Utiliser des couleurs de manière responsable | |
| 1.4.7 [Audio en arrière-plan faible ou nul](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-noaudio.html) | Aucune technique de LiveCycle spécifique | |
| 1.4.9 [Texte sous forme d’image (sans exception)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-images.html) | Aucune technique de LiveCycle spécifique | |
| 2.1 [Accessibilité au clavier](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation.html) | | |
| 2.1.1 [Clavier](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-keyboard-operable.html) | 2.6 Assurer l’ordre correct de lecture et de tabulation | |
| | 2.7 Assurer l’accessibilité au clavier des commandes de formulaire | |
| 2.1.2 [Aucun piège au clavier](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-trapping.html) | 2.7 Assurer l’accessibilité au clavier des commandes de formulaire | |
| 2.1.3 [Clavier (sans exception)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/keyboard-operation-all-funcs.html) | 2.6 Assurer l’ordre correct de lecture et de tabulation | |
| | 2.7 Assurer l’accessibilité au clavier des commandes de formulaire | |
| 2.2 [Accorder un temps suffisant](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits.html) | | |
| 2.2.1 [Réglage du minutage](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-required-behaviors.html) | Aucune technique de LiveCycle spécifique | |
| 2.2.2 [Mettre en pause, arrêter, masquer](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-pause.html) | 2.1 Simplification et facilité d’utilisation des formulaires | |
| 2.2.3 [Pas de délai d’exécution](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-no-exceptions.html) | Aucune technique de LiveCycle spécifique | |
| 2.2.4 [Interruptions](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-postponed.html) | Aucune technique de LiveCycle spécifique | |
| 2.2.5 [Nouvelle authentification](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-server-timeout.html) | Aucune technique de LiveCycle spécifique | |
| 2.3 [Crises] | | |
| 2.3.1 [Pas plus de trois flashs ou sous le seuil critique](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-does-not-violate.html) | 2.1 Simplification et facilité d’utilisation des formulaires | |
| 2.3.2 [Trois Flashs](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-three-times.html) | 2.1 Simplification et facilité d’utilisation des formulaires | |
| 2.4 [Navigabilité](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms.html) | | |
| 2.4.1 [Contourner des blocs](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-skip.html) | 2.10 Fournir une structure de formulaire navigable | |
| 2.4.2 [Titre de page](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-title.html) | Aucune technique de LiveCycle spécifique | |
| 2.4.3 [Parcours du focus](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-focus-order.html) | 2.6 Assurer l’ordre correct de lecture et de tabulation | |
| 2.4.4 [Fonction du lien (selon le contexte)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-refs.html) | Aucune technique de LiveCycle spécifique | La fonction du lien dépend du choix de texte significatif pour les éléments liés de la part des personnes chargées de la création. |
| 2.4.5 [Accès multiples](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-mult-loc.html) | 2.10 Fournir une structure de formulaire navigable | |
| 2.4.6 [En-têtes et libellés](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-descriptive.html) | <ul><li>2.5 Fournir des libellés appropriés pour les commandes de formulaire</li><li>2.10 Fournir une structure de formulaire navigable</li> | |
| 2.4.7 [Visibilité du focus](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-focus-visible.html) | Aucune technique de LiveCycle spécifique | Le focus par défaut est visible dans les formulaires LiveCycle. |
| 2.4.8 [Localisation](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-location.html) | Aucune technique de LiveCycle spécifique | Non applicable : les formulaires LiveCycle ne nécessitent pas de systèmes de navigation. |
| 2.4.9 [Fonction du lien (lien uniquement)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-link.html) | Aucune technique de LiveCycle spécifique | La fonction du lien dépend du choix de texte significatif pour les éléments liés de la part des personnes chargées de la création. |
| 2.4.10 [En-têtes de section](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-headings.html) | 2.10 Fournir une structure de formulaire navigable | |
| 3.1 [Lisible](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning.html) | | |
| 3.1.1 [Langue de la page](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-doc-lang-id.html) | 2.13 Identifier le langage naturel et tout changement de langage | |
| 3.1.2 [Langue d’un passage](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-other-lang-id.html) | 2.13 Identifier le langage naturel et tout changement de langage | |
| 3.1.3 [Mots rares](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-idioms.html) | Aucune technique de LiveCycle spécifique | |
| 3.1.4 [Abréviations](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-located.html) | Aucune technique de LiveCycle spécifique | |
| 3.1.5 [Niveau de lecture](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-supplements.html) | Aucune technique de LiveCycle spécifique | |
| 3.1.6 [Prononciation](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-pronunciation.html) | Aucune technique de LiveCycle spécifique | |
| 3.2 [Prévisible](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior.html) | | |
| 3.2.1 [Au focus](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-receive-focus.html) | 2.11 Éviter les scripts perturbateurs | |
| 3.2.2 [À la saisie](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-unpredictable-change.html) | 2.11 Éviter les scripts perturbateurs | |
| 3.2.3 [Navigation cohérente](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-consistent-locations.html) | 2.10 Fournir une structure de formulaire navigable | |
| 3.2.4 [Identification cohérente](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-consistent-functionality.html) | <ul><li>2.3 Choisir les commandes appropriées</li><li>2.5 Fournir des libellés appropriés pour les commandes de formulaire</li> | |
| 3.2.5 [Changement à la demande](https://www.w3.org/TR/UNDERSTANDING-WCAG20/consistent-behavior-no-extreme-changes-context.html) | 2.11 Éviter les scripts perturbateurs | |
| 3.3 [Assistance à la saisie](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error.html) | | |
| 3.3.1 [Identification des erreurs](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-identified.html) |  | LiveCycle Designer fournit des outils permettant de marquer les champs de formulaire selon les besoins et d’effectuer la validation des entrées de formulaire. |
| 3.3.2 [Libellés ou instructions](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-cues.html) | 2.5 Fournir des libellés appropriés pour les commandes de formulaire | |
| 3.3.3 [Suggestion après une erreur](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-suggestions.html) |  | LiveCycle Designer fournit des outils permettant de marquer les champs de formulaire selon les besoins et d’effectuer la validation des entrées de formulaire. |
| 3.3.4 [Prévention des erreurs (juridiques, financières, de données)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-reversible.html) | Aucune technique de LiveCycle spécifique | |
| 3.3.5 [Aide](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-context-help.html) | Aucune technique de LiveCycle spécifique | |
| 3.3.6 [Prévention des erreurs (toutes)](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-reversible-all.html) | Aucune technique de LiveCycle spécifique | |
| 4.1 [Compatible](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat.html) | | |
| 4.1.1 [Analyse](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat-parses.html) | Aucune technique de LiveCycle spécifique | |
| 4.1.2 [Nom, rôle et valeur](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat-rsv.html) | <ul><li>2.3 Choisir les commandes appropriées</li> <li>2.5 Fournir des libellés appropriés pour les commandes de formulaire</li> | |
