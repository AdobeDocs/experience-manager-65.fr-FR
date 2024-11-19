---
title: Bonnes pratiques pour la création de formulaires dans Forms Designer
description: Découvrez les bonnes pratiques d’accessibilité pour la création de formulaires dans Forms Designer.
feature: Adaptive Forms, Forms Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 3a9d7943-2c34-4e0a-9803-7ce1ef40f676
source-git-commit: 0d491be4fb2605220b1558c8c877151ab4405978
workflow-type: ht
source-wordcount: '11687'
ht-degree: 100%

---

# Bonnes pratiques pour la création de formulaires dans Forms Designer

LiveCycle Designer vous permet de créer du contenu de formulaire enrichi et de respecter les directives de la section 508. Ce guide contient une vue d’ensemble des bonnes pratiques relatives à la création d’un formulaire accessible et des instructions relatives à la mise en œuvre de ces bonnes pratiques à l’aide de LiveCycle Designer. Les bonnes pratiques suivantes sont abordées :

1. [Simplification et facilité d’utilisation des formulaires](#keep-simple)
1. [Configuration des propriétés de formulaire pour générer des informations d’accessibilité](#configure-form-properties)
1. [Choix des commandes appropriées](#choose-right-controls)
1. [Fourniture d’équivalents textuels pour les images](#provide-text-equivalents)
1. [Fourniture de libellés appropriés pour les commandes de formulaire](#provide-proper-labels)
1. [Ordre de lecture et de tabulation corrects](#ensure-reading-tab-order)
1. [Accessibilité des commandes de formulaire avec un clavier](#ensure-keyboard-accessible)
1. [Utilisation responsable des couleurs](#use-color-responsibly)
1. [Fourniture de cellules d’en-tête pour les tableaux](#provide-heading-cells)
1. [Fourniture d’une structure de formulaire navigable](#provide-navigable-form)
1. [Évitement des scripts perturbateurs](#avoid-disruptive-scripting)
1. [Accessibilité de tout le contenu audio et vidéo](#ensure-audio-video-accessible)
1. [Identification du langage naturel et de toute modification linguistique](#identify-natural-language)

## Simplification et facilité d’utilisation des formulaires {#keep-simple}

Un formulaire n’est pas accessible s’il n’est pas facile à utiliser. Vous devez essayer de concevoir des formulaires simples et utilisables. Une disposition simple des commandes et des champs avec des légendes et des info-bulles claires et significatives facilite l’utilisation du formulaire pour l’ensemble des utilisateurs et des utilisatrices.
La conception de formulaires organisés de manière claire et logique, qui fournissent des instructions simples et claires, permettra à l’ensemble des utilisateurs et des utilisatrices de remplir les formulaires aussi facilement que possible. Les fonctionnalités de navigation, telles que l’ordre de tabulation et les raccourcis clavier, doivent prendre en charge l’ordre logique des objets dans le formulaire.

### Éviter le contenu mobile, clignotant ou stroboscopique

Certaines personnes atteintes d’épilepsie photosensible peuvent avoir une crise déclenchée par un mouvement dans des fréquences supérieures à 2 Hz (1 Hz, ou Hertz, est égal à 1 par seconde) et inférieures à 55 GHz (55 par seconde).

Un mouvement à moins de 2 Hz est considéré comme assez lent pour être sûr pour les personnes atteintes d’épilepsie photosensible. Un mouvement à plus de 55 Hz est considéré comme invisible.

Les développeurs et développeuses doivent tenir compte de ces paramètres lorsqu’ils utilisent n’importe quel mouvement dans le contenu web.

D’autres utilisateurs et utilisatrices peuvent avoir des déficiences cognitives qui rendent difficile la concentration lorsque le formulaire comporte du contenu animé ou clignotant.

En règle générale, évitez d’utiliser des effets optiques insérés par des scripts, tels que du texte ou des animations clignotants, dans des formulaires interactifs. Ces effets réduisent la convivialité des formulaires pour certains utilisateurs et utilisatrices.

Points de contrôle connexes
* Section 508 §11934.21

   * (h) Lorsque l’animation est affichée, l’information doit être affichée dans au moins un mode de présentation non animé, au choix de l’utilisateur ou de l’utilisatrice.
   * (k) Le logiciel ne doit pas utiliser de texte clignotant ou stroboscopique, d’objets ou d’autres éléments ayant une fréquence de clignotement supérieure à 2 Hz et inférieure à 55 Hz.
* Section 508 §11934.22
   * (j) Les pages doivent être conçues pour éviter que l’écran scintille avec une fréquence supérieure à 2 Hz et inférieure à 55 Hz.
* WCAG 1.0
   * 7.1 Tant que les agents utilisateurs ne permettent pas aux utilisateurs et utilisatrices de contrôler le scintillement, évitez de provoquer le scintillement de l’écran. (P1)
   * 7.2 Tant que les agents utilisateurs ne permettent pas aux utilisateurs et utilisatrices de contrôler le clignotement, évitez de provoquer le clignotement du contenu (c.-à-d. modifier régulièrement la présentation, comme activer et désactiver) (P2).
   * 7.3 Tant que les agents utilisateurs ne permettent pas aux utilisateurs et utilisatrices de geler le contenu mobile, évitez les mouvements dans les pages.
   * 14.1 Utiliser le langage le plus clair et le plus simple adapté au contenu d’un site.
* WCAG 2.0
   * 2.2.2 Mettre en pause, arrêter, masquer : pour toute information en mouvement, clignotante, défilante ou mise à jour automatiquement, tous les points suivants sont vrais : (Niveau A)
   * 2.3.1 Trois flashs ou sous le seuil : une page web doit être exempte de tout élément qui clignote plus de trois fois dans n’importe quel intervalle d’une seconde, ou ce flash doit se situer sous le seuil de flash générique et le seuil de flash rouge. (Niveau A)
   * 2.3.2 Trois flashs : une page web doit être exempte de tout élément qui flashe plus de trois fois dans n’importe quel intervalle d’une seconde. (Niveau AAA)


## Configuration des propriétés de formulaire pour générer des informations d’accessibilité {#configure-form-properties}

Pour qu’un formulaire soit accessible, il doit être [perceptible](https://www.w3.org/TR/WCAG20/#perceivable) par la technologie d’assistance. Par exemple, la plupart des lecteurs d’écran ne prennent pas en compte la disposition visuelle de votre formulaire, mais plutôt la structure sous-jacente.

Pour implémenter cette structure sous-jacente à l’aide de LiveCycle Designer, vous devez créer un formulaire PDF contenant des informations d’accessibilité (parfois appelées balises), afin que le lecteur d’écran ou toute autre technologie d’assistance puisse lire le texte et les composants du formulaire. Dans un formulaire contenant des informations d’accessibilité, chaque élément contient des informations sur sa propre structure, ainsi que des informations sur sa relation ou sa dépendance à d’autres éléments. Ce n’est que dans les fichiers PDF contenant des informations d’accessibilité que les lecteurs d’écran peuvent identifier et décrire précisément le contenu d’un document.

Pour créer un formulaire accessible, vous devez configurer les propriétés du formulaire de sorte que LiveCycle Designer génère des informations d’accessibilité lors de l’enregistrement de la conception de formulaire en tant que fichier PDF :
1. Sélectionnez Fichier > Propriétés du formulaire.
1. Sélectionnez l’onglet Enregistrer les options et, dans la zone PDF, assurez-vous que l’option Générer les informations d’accessibilité (balises) pour Acrobat est sélectionnée.
1. Cliquez sur OK.

Dans LiveCycle Designer, cette option est sélectionnée par défaut.

>[!NOTE]
> Ces options s’appliquent uniquement lors de l’enregistrement de la conception de formulaire en tant que fichier PDF. Elles ne s’appliquent pas aux fichiers PDF créés avec LiveCycle Forms qui disposent d’options de configuration indépendantes de cette option dans LiveCycle Designer.

**Points de contrôle connexes**

* Section 508 §1194.21
   * (d) Des informations suffisantes sur un élément d’interface d’utilisateur, y compris l’identité, le fonctionnement et l’état de l’élément, doivent être disponibles pour les dispositifs d’assistance. Lorsqu’une image représente un élément de programme, les informations véhiculées par l’image doivent également être disponibles dans le texte.
   * (l) Lorsqu’un formulaire électronique est utilisé, il doit permettre aux personnes utilisant une technologie d’assistance d’accéder aux informations, aux éléments de champ et aux fonctionnalités nécessaires à la réalisation et à l’envoi du formulaire, y compris toutes les instructions et tous les repères.
* Section 508 §1194.22
   * (n) Lorsque les formulaires électroniques sont conçus pour être remplis en ligne, le formulaire doit permettre aux personnes qui utilisent des dispositifs d’assistance d’accéder aux informations, aux éléments de champ et aux fonctionnalités nécessaires à la réalisation et à l’envoi du formulaire, y compris toutes les instructions et tous les repères.


## Choix des commandes appropriées {#choose-right-controls}

Lors de la conception de vos formulaires, utilisez les objets de développement des onglets disponibles dans la bibliothèque d’objets de Designer LiveCycle. Vous pouvez afficher ce panneau en choisissant Fenêtre > Bibliothèque d’objets ou en appuyant sur Maj+F12 (voir l’illustration 1).

![Panneau Bibliothèque d’objets](/help/forms/using/assets/image-1.png)

Illustration 1 : **panneau Bibliothèque d’objets**

Si vous utilisez d’autres objets, ils peuvent être ignorés par les dispositifs d’assistance. L’utilisation d’objets standard uniquement vous évite d’avoir à définir les propriétés d’accessibilité des objets que vous avez vous-même créés. Si vous créez et utilisez vos propres objets personnalisés, veillez à utiliser la palette Accessibilité pour définir les propriétés d’accessibilité telles que Rôle, Info-bulle, Priorité dans le lecteur d’écran et Texte de lecteur d’écran personnalisé. Pour afficher la palette Accessibilité, choisissez Fenêtre > Accessibilité.

**Points de contrôle connexes**
* Section 508 §1194.21
   * (c) Une indication bien définie à l’écran du focus actue doit être fournie pour que les éléments de l’interface interactive se déplacent au fur et à mesure que le focus change. Le focus doit être exposé par programmation afin que la technologie d’assistance puisse suivre le focus et ses changements.
   * (d) Des informations suffisantes sur un élément d’interface d’utilisateur, y compris l’identité, le fonctionnement et l’état de l’élément, doivent être disponibles pour les dispositifs d’assistance. Lorsqu’une image représente un élément de programme, les informations véhiculées par l’image doivent également être disponibles dans le texte.
   * (l) Lorsqu’un formulaire électronique est utilisé, il doit permettre aux personnes utilisant une technologie d’assistance d’accéder aux informations, aux éléments de champ et aux fonctionnalités nécessaires à la réalisation et à l’envoi du formulaire, y compris toutes les instructions et tous les repères.
* Section 508 §1194.22
   * (n) Lorsque les formulaires électroniques sont conçus pour être remplis en ligne, le formulaire doit permettre aux personnes qui utilisent des dispositifs d’assistance d’accéder aux informations, aux éléments de champ et aux fonctionnalités nécessaires à la réalisation et à l’envoi du formulaire, y compris toutes les instructions et tous les repères.

* WCAG 2.0
   * 3.2.4 Identification cohérente : dans un ensemble de pages web, les composants qui ont la même fonctionnalité sont identifiés de la même façon. (Niveau AA).
   * 4.1.2 Nom, rôle et valeur : pour tout composant d’interface utilisateur (comprenant mais n’étant pas limité aux éléments de formulaire, liens et composants générés par des scripts), le nom et le rôle peuvent être déterminés par un programme informatique ; les états, les propriétés et les valeurs qui peuvent être paramétrés par l’utilisateur ou l’utilisatrice peuvent être définis par programmation; et la notification des changements de ces éléments est disponible aux agents utilisateurs, incluant les technologies d’assistance. (Niveau A)


## Fourniture d’équivalents textuels pour les images {#provide-text-equivalents}

Les images peuvent permettre d’améliorer la compréhension pour les utilisateurs et utilisatrices présentant certains types de handicaps. Toutefois, pour les utilisateurs et utilisatrices de lecteurs d’écran, les images diminuent l’accessibilité de votre formulaire si vous ne fournissez pas d’alternative textuelle.

Si vous optez pour l’utilisation d’images, fournissez des descriptions textuelles pour l’ensemble des images et champs associés. Assurez-vous que le texte décrit l’objet et son rôle dans le formulaire. Lorsque vous définissez un texte secondaire, le lecteur d’écran lit cette alternative lorsqu’il rencontre l’image. Pour cette raison, une image contenant des informations doit toujours comporter un texte secondaire.

Vous fournissez des descriptions textuelles à l’aide des propriétés Info-bulle ou Texte de lecteur d’écran personnalisé de la palette Accessibilité ou au moyen de champs de texte, de légendes et de noms d’objet, comme indiqué dans l’option Nom de l’onglet Liaison. Par exemple, l’illustration 2 illustre un exemple d’image contenant le texte « Obtenir Adobe Reader ». Comme un lecteur d’écran ne peut pas lire le texte qui fait partie d’une image, vous devez inclure un texte secondaire dans le champ Texte du lecteur d’écran personnalisé de la palette Accessibilité pour cet objet. Dans la plupart des cas, le texte secondaire doit être identique au texte visible dans l’image (voir l’illustration 2).

![Spécification d’un texte secondaire pour une image à l’aide de la palette Accessibilité](/help/forms/using/assets/image-2.png)

Illustration 2 : **spécification d’un texte secondaire pour une image à l’aide de la palette Accessibilité**

Lorsque vous spécifiez un texte secondaire, tenez compte des points suivants :
* Si l’objet image ou l’image numérisée contient des informations importantes pour le formulaire, créez du texte pour l’image dans la palette Accessibilité qui décrit l’objet et son objectif. Le texte du logo d’une société, par exemple, peut contenir les mots « logo de la société » et le nom de la société.
* Si l’objet image contient des informations de couleur sémantique, incluez-les également dans la description. Une description d’un feu vert de circulation, par exemple, peut être « Transmission réussie » et la description d’un feu rouge peut être « Transmission échouée ».
* Si vous utilisez des graphiques complexes, tels que des graphiques à barres, fournissez les informations dans une autre version accessible, telle qu’un tableau ou une description textuelle plus longue.
* Ne créez pas de descriptions de texte pour les images statiques qui ne sont utilisées que pour la décoration.
* N’utilisez pas les données numérisées comme informations d’arrière-plan. Cela peut se produire lorsqu’un concepteur ou une conceptrice numérise un formulaire imprimé et utilise Adobe LiveCycle Designer pour ajouter de nouveaux champs au formulaire. Les lecteurs d’écran ne peuvent pas détecter les données numérisées dans cet état.

Lorsque vous incluez du contenu graphique purement décoratif dans vos formulaires, vous souhaitez vous assurer que les lecteurs d’écran n’annoncent pas la présence de l’image. Pour la plupart des lecteurs d’écran, cela est possible en définissant la propriété Texte du lecteur d’écran sur Aucun dans la palette Accessibilité. Si vous ne le faites pas, certains lecteurs d’écran peuvent annoncer la présence d’un graphique, sans indiquer ce que le graphique représente. Pour les images dynamiques, telles que les objets de champ d’image, assurez-vous que les équivalents textuels sont correctement mis à jour lorsque l’image est modifiée. Ne créez pas de descriptions de texte pour les objets de champ d’image qui ne sont utilisés que pour la décoration. Vous pouvez utiliser le langage de script FormCalc pour affecter dynamiquement des descriptions textuelles à un objet de champ d’image. FormCalc est le langage de script standard d’Adobe LiveCycle Designer. Prenons l’exemple d’un formulaire avec un champ d’image nommé ImageField1 et le texte associé dans le nœud imagetext des données d’exécution. Vous pouvez utiliser un script pour transmettre ce texte dans un événement approprié (par exemple `form:ready`) comme suit :

`ImageField1.assist.toolTip = $record.imagetext.value`

Points de contrôle connexes
* Section 508 §1194.22
   * (a) Un équivalent textuel pour chaque élément non textuel doit être fourni (par exemple, par « alt », « longdesc » ou dans le contenu de l’élément).
* WCAG 1.0
   * 1.1 Proposer un équivalent textuel pour chaque élément non textuel (par exemple, par « alt », « longdesc » ou dans le contenu de l’élément). Cela comprend : les images, les représentations graphiques du texte (y compris les symboles), les zones cliquables, les animations (par exemple, les GIF animés), les applets et les objets programmatiques, l’art ascii, les cadres, les scripts, les images utilisées comme puces de liste, les espaces, les boutons graphiques, les sons (lus avec ou sans interaction de l’utilisateur ou de l’utilisatrice), les fichiers audio autonomes, les pistes audio de vidéo (P1).
* WCAG 2.0
   * 1.1.1 Contenu non textuel : tout contenu non textuel présenté à l’utilisateur ou à l’utilisatrice possède un texte secondaire qui remplit une fonction équivalente sauf dans les situations énumérées ci-dessous. (Niveau A)


## Fourniture de libellés appropriés pour les commandes de formulaire{#provide-proper-labels}

Le libellé ou la légende d’une commande de formulaire identifie ce que le contrôle de formulaire est censé représenter. Par exemple, le texte « Prénom » indique à l’utilisateur et à l’utilisatrice qu’ils doivent saisir leur prénom dans une zone de texte. Pour être accessible par les lecteurs d’écran, le libellé doit être associé par programmation à la commande de formulaire ou cette dernière doit être configurée avec des informations d’accessibilité supplémentaires à l’aide de la palette Accessibilité. Il ne suffit pas de placer un objet de texte à côté de la commande. Pour les utilisateurs et utilisatrices voyants ou malvoyants, il est important que le libellé soit correctement positionné à côté de la commande. Les deux techniques seront abordées dans les sections suivantes.

### Spécification de texte de libellé accessible à l’aide de la palette Accessibilité

Le libellé perçu par les lecteurs d’écran ne doit pas nécessairement être identique à la légende visuelle. Dans certains cas, vous pouvez faire preuve de plus de précision quant au rôle exact de la commande.
Pour chaque objet de champ d’un formulaire, les options d’accessibilité (voir image 3) permettent de spécifier ce que le lecteur d’écran annonce pour identifier le champ de formulaire spécifique.

Pour utiliser la palette Accessibilité, procédez comme suit :

1. Pour afficher la palette Accessibilité, choisissez Fenêtre > Accessibilité ou appuyez sur les touches Maj+F6.
1. Sélectionnez un objet dans votre formulaire. La palette affiche les propriétés d’accessibilité de l’objet.

![Palette Accessibilité](/help/forms/using/assets/image-3.png)

Illustration 3 : **palette Accessibilité**

Lorsque le formulaire est enregistré en tant que PDF, LiveCycle Designer y recherche les propriétés Texte personnalisé, Info-bulle, Légende et Nom, dans cet ordre, pour trouver le texte à lire par les lecteurs d’écran. Vous pouvez remplacer cet ordre par défaut à l’aide de l’option Priorité dans le lecteur d’écran dans la palette Accessibilité.

1. Sélectionnez l’objet sur la conception de formulaire.
1. Cliquez sur la palette Accessibilité.
1. Sélectionnez une option Priorité dans le lecteur d’écran autre que Aucune.

Les options suivantes sont disponibles :

* **Texte personnalisé**, que vous définissez dans le champ Texte du lecteur d’écran personnalisé de la palette Accessibilité. Cette option vous permet de spécifier le texte que vous souhaitez utiliser pour la technologie d’assistance, comme les lecteurs d’écran. L’utilisation du paramètre Légende est préférable dans la plupart des cas. La création d’un texte de lecteur d’écran personnalisé ne doit être envisagée comme une option que lorsque l’utilisation de la légende ou d’une info-bulle n’est pas possible.
* **Info-bulle**, que vous définissez dans le champ Info-bulle de la palette Accessibilité. Pour la plupart des objets, les info-bulles s’affichent au moment de l’exécution lorsque l’utilisateur ou l’utilisatrice place le pointeur sur l’objet. Les info-bulles s’affichent pour certains objets en lecture seule, tels que l’objet Code à barres d’un formulaire pour support papier, uniquement lorsqu’un lecteur d’écran est en cours d’utilisation.
* **Légende**, ce qui entraîne LiveCycle Designer à utiliser le libellé (visuel) associé au champ de formulaire comme texte de lecteur d’écran.
* **Nom**, que vous définissez dans le champ Nom de l’onglet Liaison. Notez que ce nom ne peut pas contenir d’espaces.
* **Aucun**, ce qui empêchera l’objet de porter un nom. Cela n’est jamais recommandé pour les commandes de formulaire.

Tenez compte des points suivants lorsque vous utilisez la palette Accessibilité pour l’étiquetage des commandes de formulaire :

* Si la légende de votre commande de formulaire décrit correctement la commande,elle est alors accessible aux lecteurs d’écran. Dans ce cas, laissez les champs Texte personnalisé et Info-bulle vides dans la palette Accessibilité ou changez la Priorité dans le lecteur d’écran en Légende.
* Lorsque vous ciblez des lecteurs d’écran, il n’est pas utile de spécifier différentes descriptions de texte pour la même commande de formulaire, car un seul champ sera utilisé : le premier champ non vide dans l’ordre Priorité dans le lecteur d’écran. Par exemple, il n’y a aucune raison de spécifier à la fois le texte personnalisé et le texte d’info-bulle pour un lecteur d’écran.
* Par défaut, le lecteur d’écran lit la légende si rien n’est spécifié dans la zone Info-bulle ou Texte du lecteur d’écran personnalisé.
* N’utilisez pas la palette Accessibilité pour créer des descriptions pour les champs ou zones invisibles.
* Si vous devez créer une description à l’aide des options Info-bulle ou Texte du lecteur d’écran personnalisé, incluez toujours la légende visible sur le formulaire, sauf lorsque la légende visible n’est pas significative, par exemple lorsqu’elle est elle-même est abrégée. Cela permet aux utilisateurs et utilisatrices de lecteurs d’écran de communiquer efficacement avec d’autres utilisateurs et utilisatrices au sujet des éléments de l’interface d’utilisation. Ces différents groupes d’utilisateurs et d’utilisatrices ont des difficultés à identifier le même élément d’IU si le texte de sa légende diffère de l’info-bulle ou du texte du lecteur d’écran personnalisé.
* Pour les cases à cocher et les contrôles de listes déroulantes dans les cellules d’un tableau, le lecteur d’écran annonce la légende, l’info-bulle ou le texte de lecteur d’écran personnalisé que vous spécifiez pour l’objet. Si vous souhaitez utiliser l’en-tête de colonne pour le texte de remplacement de ces objets lorsqu’ils sont placés dans un tableau, ne fournissez pas de légende, d’info-bulle ou de texte de lecteur d’écran personnalisé.
* Si la commande nécessite des instructions supplémentaires, assurez-vous qu’elles sont également incluses dans l’alternative textuelle. Incluez suffisamment d’informations vocales pour que les utilisateurs et utilisatrices sachent quelles entrées sont attendues et comment remplir correctement le champ, mais ne submergez pas les utilisateurs et utilisatrices d’informations redondantes.
* Ne fournissez pas d’informations superflues décrivant comment utiliser les commandes : laissez les technologies d’assistance de la personne gérer cela pour elle. Les utilisateurs et utilisatrices peuvent configurer la terminologie en fonction de leur niveau de confort.

L’illustration 4 présente un exemple de champ de texte avec une légende visuelle qui peut être floue pour certains utilisateurs et utilisatrices de lecteurs d’écran. Dans cet exemple, le texte du lecteur d’écran personnalisé est défini sur « Nombre de pages » et la priorité dans le lecteur d’écran est définie sur Texte personnalisé. Par conséquent, le texte de légende (visuel) réel (« # de pages ») ne sera pas utilisé par le lecteur d’écran. Une info-bulle peut également avoir été spécifiée.

![Spécification de texte du lecteur d’écran personnalisé lorsque le libellé visible est inadéquat.](/help/forms/using/assets/image-4.png)

Illustration 4 : **spécification de texte du lecteur d’écran personnalisé lorsque le libellé visible est inadéquat.**

### Étiquetage des boutons radio

Lorsqu’une personne ayant une déficience visuelle accède à un bouton radio, le lecteur d’écran doit lire deux éléments :
* Une indication de l’objectif du groupe de boutons radio
* Un libellé significatif pour chaque bouton radio
Pour rendre les boutons radio accessibles à l’aide des légendes des boutons, procédez comme suit :
   1. Dans la palette Hiérarchie, sélectionnez le groupe d’exclusion.
   1. Cliquez sur la palette Accessibilité, puis, dans la zone Texte du lecteur d’écran personnalisé, saisissez le texte à lire pour le groupe. Par exemple, pour un groupe d’exclusion indiquant les options de paiement par différentes cartes de crédit, saisissez Sélectionner un mode de paiement.
   1. Si les légendes de chaque bouton radio fournissent du texte qui aura un sens lorsqu’il sera lu par un lecteur d’écran, sélectionnez l’onglet Liaison de la palette Objet, puis désélectionnez l’option Définir la valeur de l’élément.

  Pour rendre les boutons radio accessibles à l’aide d’une valeur d’élément spécifiée, procédez comme suit :
   1. Dans la palette Hiérarchie, sélectionnez le groupe d’exclusion.
   1. Cliquez sur la palette Accessibilité, puis, dans la zone Texte du lecteur d’écran personnalisé, saisissez le texte à lire pour le groupe. Par exemple, pour un groupe d’exclusion indiquant les options de paiement par différentes cartes de crédit, saisissez Sélectionner un mode de paiement.
   1. Dans la palette Hiérarchie, sélectionnez le premier bouton radio du groupe.
   1. Dans la palette Objet, cliquez sur l’onglet Champ. Dans la zone Élément, double-cliquez sur l’élément et saisissez une valeur significative pour le bouton radio sélectionné. Par exemple, pour le premier bouton d’un groupe de modes de paiement, vous pouvez saisir Espèces.
   1. Répétez les étapes 3 et 4 pour chaque bouton radio du groupe d’exclusion.

### Étiquetage des commandes personnalisées

Il est vivement recommandé d’utiliser des composants standard plutôt que des composants personnalisés, car ils fourniront par défaut à la technologie d’assistance les bons repères et informations. Toutefois, si des commandes personnalisées sont utilisées, tenez compte des points suivants :
* Annoncez l’état des cases à cocher et des boutons radio.
* Dans les zones de liste et les listes déroulantes, annoncez l’élément par défaut sélectionné dans la liste. Assurez-vous que la personne sait qu’il faut utiliser les touches Haut et Bas pour parcourir les éléments de la liste. Notez qu’appuyer sur la touche de tabulation ou sur la touche Entrée ou Retour permet de sélectionner l’élément dans la liste. Avec un script, vous pouvez définir l’événement de modification de l’objet pour annoncer l’élément sélectionné dans la liste.
* Annoncez aux utilisateurs et utilisatrices les touches spéciales dont ils ont besoin pour exécuter une fonction, par exemple en appuyant sur la barre d’espace pour sélectionner un bouton ou sur la touche Bas pour sélectionner un élément dans une zone de liste.

### Positionnement correct de la légende d’une commande

Le positionnement d’une légende est important, car les utilisateurs et utilisatrices s’attendent à ce qu’elle se trouve à côté de la commande. Pour les utilisateurs et utilisatrices de l’agrandissement de l’écran, c’est encore plus important, car ils peuvent ne pas pouvoir afficher simultanément la commande et la légende s’ils sont trop éloignés.

Lorsque vous créez un objet, LiveCycle Designer positionne automatiquement la légende comme indiqué par le type d’objet. Les légendes des boutons radio, par exemple, sont placées à droite. Cet emplacement par défaut est toujours le meilleur emplacement pour une légende accessible. Si vous devez modifier la position du texte de la légende, procédez comme suit :
1. Sélectionnez l’objet en y mettant la cible d’action.
1. Dans la palette Disposition, sélectionnez la position de la légende de l’objet à partir de l’option Position de la section Légende située au bas de la palette.

L’exemple illustré dans l’illustration 5 présente une zone de texte avec une légende au-dessus. La position de la palette Disposition est définie sur Haut. L’emplacement par défaut de la légende se trouve à gauche de la zone de texte.

![Modification du positionnement des légendes à l’aide de la palette Disposition](/help/forms/using/assets/image-5.png)

Illustration 5 : **modification du positionnement des légendes à l’aide de la palette Disposition**

Le tableau suivant présente une vue d’ensemble des règles de placement de libellés pour les commandes couramment utilisées.

| Type de commande | Règles de placement |
|--------------|-----------------|
| Entrée de texte (y compris les champs de date, d’heure et de mot de passe) | Placez la légende à gauche de la commande (par défaut). Si cela n’est pas possible, placez-la immédiatement au-dessus ou en dessous. Les libellés doivent être positionnés à proximité de la commande pour les utilisateurs et utilisatrices avec un agrandissement accru afin que le libellé et la commande soient plus susceptibles d’être affichés ensemble dans la vue agrandie. |
| Case à cocher | Placez la légende à droite de la case à cocher (par défaut). Pour les commandes de case à cocher dans les cellules d’un tableau, le lecteur d’écran annonce la légende, l’info-bulle ou le texte du lecteur d’écran personnalisé que vous spécifiez pour l’objet. Si vous souhaitez utiliser l’en-tête de colonne comme texte de remplacement pour une case à cocher dans un tableau, ne fournissez pas de légende, d’info-bulle ou de texte du lecteur d’écran personnalisé. |
| Groupe de boutons radio | Créez un titre visible pour le groupe de boutons radio en créant un élément de texte statique et en le plaçant à gauche ou au-dessus du groupe. Pour chaque bouton radio individuel, placez le libellé à droite (par défaut). |
| Liste déroulante | Placez la légende à gauche de l’objet (par défaut). Si cela n’est pas possible, placez-la immédiatement au-dessus. Pour les commandes de liste déroulante dans les cellules d’un tableau, le lecteur d’écran annonce la légende, l’info-bulle ou le texte du lecteur d’écran personnalisé que vous spécifiez pour l’objet. Si vous souhaitez utiliser l’en-tête de colonne comme texte de remplacement pour ces objets dans un tableau, ne fournissez pas de légende, d’info-bulle ou de texte du lecteur d’écran personnalisé. |
| Zone de liste | La légende est positionnée par défaut au-dessus de la zone de liste lors de sa création. |
| Bouton | La légende est placée automatiquement sur le bouton et ne doit pas être positionnée manuellement. Assurez-vous que l’objectif du bouton est correctement décrit par le texte de la légende. |


### Remplissage dynamique d’une info-bulle ou d’un texte du lecteur d’écran personnalisé

Vous pouvez également remplir de manière dynamique l’équivalent textuel d’une commande de formulaire, comme son info-bulle, avec une valeur issue d’une source de données. Par exemple, vous pouvez afficher une info-bulle personnalisée pour un objet en français.
Les éléments suivants peuvent être définis pour une info-bulle pour le schéma auquel vous vous connectez :


```html
<form>
<tooltip dp_tt="tooltip1"/>
</form>
```


Les éléments suivants peuvent être définis pour une info-bulle pour le fichier de données sur lequel vous pointez :

```html
<form>
<tooltip dp_tt="Quantité - Entrez un nombre inférieur ou égal à 100."/>
</form>
```

1. Dans la palette Bibliothèque d’objets, cliquez sur la catégorie Standard et faites glisser un objet sur la conception de formulaire. Par exemple, insérez un objet de champ de texte.
1. (Facultatif) Dans la palette Objet, cliquez sur l’onglet Champ, puis saisissez la légende de l’objet dans la zone Légende. Par exemple, saisissez Quantité.
1. Dans la palette Accessibilité, cliquez sur le libellé actif Info-bulle.
1. Sélectionnez la connexion de données.
1. Cliquez sur le triangle situé à côté de la zone Liaison et sélectionnez une liaison. Par exemple, sélectionnez info-bulle > @dp_tt.

La chaîne suivante apparaît dans la zone Liaison : $record.tooltip.dp_tt. Conseil : vous pouvez saisir cette chaîne dans la zone Éléments au lieu de la sélectionner.
1. Cliquez sur OK.
1. Affichez le formulaire dans l’onglet Aperçu PDF.

### Fournir du texte de lien

Les utilisateurs et utilisatrices de technologies d’assistance peuvent avoir différentes méthodes de lecture de texte lié. Par exemple, les utilisateurs et utilisatrices de lecteurs d’écran utilisent souvent une liste de liens telle que celle illustrée à l’illustration 6 pour analyser rapidement les liens disponibles sur une page.

![Boîte de dialogue Liste des liens JAWS](/help/forms/using/assets/image-6.png)

Illustration 6 : **boîte de dialogue Liste des liens JAWS**

C’est pourquoi les liens doivent être explicites, c’est-à-dire que leur signification ne doit pas dépendre de leur contexte (le texte environnant). Par exemple, les mots « cliquez ici » peuvent former l’élément de lien réel dans l’expression « cliquez ici pour télécharger notre formulaire de demande ». Un tel lien serait difficile à comprendre lorsqu’il est lu dans une liste de liens, en particulier lorsqu’il existe plusieurs liens contenant le même texte.

Lorsque vous utilisez des liens dans votre formulaire, assurez-vous que chaque lien décrit correctement son objectif, sans dépendre du texte ou de la position environnant sur la page. Par exemple, au lieu d’utiliser une expression telle que « Cliquez ici » comme texte de lien, utilisez « Télécharger le formulaire de demande ».

**Points de contrôle connexes**

* Section 508 §1194.21
   * (d) Des informations suffisantes sur un élément d’interface d’utilisateur, y compris l’identité, le fonctionnement et l’état de l’élément, doivent être disponibles pour les dispositifs d’assistance. Lorsqu’une image représente un élément de programme, les informations véhiculées par l’image doivent également être disponibles dans le texte.
   * (l) Lorsqu’un formulaire électronique est utilisé, il doit permettre aux personnes utilisant une technologie d’assistance d’accéder aux informations, aux éléments de champ et aux fonctionnalités nécessaires à la réalisation et à l’envoi du formulaire, y compris toutes les instructions et tous les repères.
* Section 508 §1194.22
   * (n) Lorsque les formulaires électroniques sont conçus pour être remplis en ligne, le formulaire doit permettre aux personnes qui utilisent des dispositifs d’assistance d’accéder aux informations, aux éléments de champ et aux fonctionnalités nécessaires à la réalisation et à l’envoi du formulaire, y compris toutes les instructions et tous les repères.
* WCAG 1.0
   * 12.4 Associer explicitement les libellés à leurs commandes (P2).
   * 13.1 Identifier clairement la cible de chaque lien (P2).
* WCAG 2.0
   * 1.1.1 Contenu non textuel : tout contenu non textuel présenté à l’utilisateur ou à l’utilisatrice possède un texte secondaire qui remplit une fonction équivalente sauf dans les situations énumérées ci-dessous. (Niveau A)
   * 2.4.6 Titres et libellés : les titres et les libellés décrivent le sujet ou l’objectif. (Niveau AA)
   * 3.2.4 Identification cohérente : dans un ensemble de pages web, les composants qui ont la même fonctionnalité sont identifiés de la même façon. (Niveau AA)
   * 3.3.2 Libellés ou instructions : des libellés ou des instructions sont présentés lorsque le contenu requiert une saisie de l’utilisateur ou de l’utilisatrice. (Niveau A)
   * 4.1.2 Nom, rôle et valeur : pour tout composant d’interface utilisateur (comprenant mais n’étant pas limité aux éléments de formulaire, liens et composants générés par des scripts), le nom et le rôle peuvent être déterminés par un programme informatique ; les états, les propriétés et les valeurs qui peuvent être paramétrés par l’utilisateur ou l’utilisatrice peuvent être définis par programmation; et la notification des changements de ces éléments est disponible aux agents utilisateurs, incluant les technologies d’assistance. (Niveau A)


## Ordre de lecture et de tabulation corrects {#ensure-reading-tab-order}

Il est très important d’assurer un ordre de lecture significatif lors de la conception de formulaires accessibles aux utilisateurs et utilisatrices ayant une déficience visuelle ou autre. Ces utilisateurs et utilisatrices n’utilisent généralement pas de souris pour naviguer dans un formulaire. Ils dépendent donc du clavier. L’ordre de lecture détermine la séquence utilisée par les utilisateurs et utilisatrices de lecteurs d’écran lorsqu’ils lisent votre formulaire. En outre, l’ordre de tabulation permet aux utilisateurs et utilisatrices de passer rapidement d’une commande de formulaire interactif à une autre à l’aide des touches Tabulation ou Maj+Tabulation. Un ordre de tabulation logique permet de s’assurer qu’ils ont accès à tous les champs du formulaire et qu’ils peuvent parcourir le formulaire de manière raisonnable et efficace.

L’ordre de lecture du formulaire comprend tous les objets statiques (texte et images, par exemple) et les objets de champ, mais seules les commandes de formulaire interactif font partie de l’ordre de tabulation.

>[!NOTE]
> Dans de nombreux cas, l’ordre de tabulation est étroitement lié à l’ordre de lecture. Pour plus de simplicité, le terme « ordre de tabulation » sera utilisé à la place de « ordre de tabulation ou de lecture » dans ce guide.

### Ordre de tabulation par défaut dans les formulaires LiveCycle Designer

L’ordre de tabulation par défaut est automatiquement créé lorsque vous enregistrez votre formulaire en tant que PDF balisé. Dans un premier temps, l’ordre de tabulation d’un formulaire est déterminé à partir de la position locale des objets, selon les règles suivantes :

* Tous les objets sont triés de gauche à droite et de haut en bas (ordre local), en commençant par le coin supérieur gauche du formulaire.
* Tous les sous-formulaires que vous créez sont traités comme des unités autonomes et sont également navigables de gauche à droite et de haut en bas. Si deux sous-formulaires sont placés côte à côte et que chaque formulaire contient des objets, l’ordre de lecture parcourt tous les objets du premier sous-formulaire avant de passer au sous-formulaire suivant.

Pour les formulaires simples (c’est-à-dire les formulaires avec une disposition de gauche à droite et de haut en bas), l’ordre de tabulation par défaut est généralement correct. Pour vérifier cela, vous devez examiner l’ordre de tabulation par défaut avant de publier votre formulaire. Vous pouvez rendre l’ordre de tabulation visible à l’aide de l’une des méthodes suivantes :

* Choisissez Affichage > Afficher l’ordre de tabulation.
* Cliquez sur Afficher l’ordre dans la palette Ordre de tabulation.

Un numéro apparaît dans le coin supérieur droit de chaque objet pour indiquer sa place dans l’ordre de tabulation par défaut. Les objets interactifs de cette séquence forment l’ordre de tabulation. L’illustration 7 présente la visualisation de l’ordre de lecture d’un formulaire de base.

![Visualisation de l’ordre de lecture par défaut pour un formulaire de commande type](/help/forms/using/assets/image-7.png)

Illustration 7 : **visualisation de l’ordre de lecture par défaut pour un formulaire de commande type**

Chaque numéro d’ordre de tabulation s’affiche sous une forme colorée. Les formes ont la signification suivante :
* Les cercles gris (n° 1 et n° 4) sont utilisés pour les objets de la zone de contenu.
* Les cercles verts (n° 6 et n° 7) sont utilisés pour les objets de gabarit de page.
* Les carrés lavande (n° 2 et n° 3) sont utilisés pour les objets à l’intérieur d’un fragment.

Vous pouvez choisir d’afficher uniquement les commandes de formulaire interactif (qui constituent l’ordre de tabulation) ou tous les objets de l’ordre de lecture (qui comprennent également les objets statiques tels que le texte et les images). Pour modifier cette préférence, choisissez Outils > Options > Ordre de tabulation, puis sélectionnez Afficher uniquement l’ordre de tabulation des champs.

Sur un formulaire complexe, il peut s’avérer difficile de voir comment la tabulation s’enchaîne d’un objet à l’autre. Vous pouvez utiliser des aides visuelles pour vous aider à voir l’ordre de tabulation sur le formulaire. Quand les aides visuelles sont activées, lorsque vous placez le pointeur sur l’objet, les flèches bleues indiquent l’ordre de tabulation des deux objets précédents et des deux objets suivants (voir l’illustration 8).

![Aides visuelles mettant en surbrillance l’ordre de tabulation](/help/forms/using/assets/image-8.png)

Illustration 8 : **aides visuelles mettant en surbrillance l’ordre de tabulation**

Pour activer les aides visuelles, utilisez les méthodes suivantes :
* Choisissez Outils > Options > Ordre de tabulation, puis, dans le panneau Ordre de tabulation, sélectionnez Afficher d’autres aides visuelles pour l’ordre de tabulation.
* Dans le menu de la palette Ordre de tabulation, choisissez Afficher les aides visuelles.

### Utilisation de la position pour influencer l’ordre de tabulation par défaut

Pour modifier l’ordre de tabulation par défaut, vous pouvez modifier les coordonnées d’un objet en le déplaçant vers un autre emplacement. Par exemple, dans l’illustration 9, le champ Nom du produit apparaît dans l’ordre de tabulation avant le champ Quantité. Pour modifier cet ordre, vous pouvez déplacer le champ Nom du produit afin qu’il soit placé en bas ou à droite du champ Quantité.

![Ordre de tabulation par défaut de gauche à droite](/help/forms/using/assets/image-9.png)

Illustration 9 : **ordre de tabulation par défaut de gauche à droite**

Vous pouvez également modifier la position d’un objet en effectuant l’une des opérations suivantes :
* Faites-le glisser à l’aide de la souris.
* Sélectionnez-le et déplacez-le à l’aide des touches fléchées du clavier.

>[!NOTE]
> Il peut s’avérer utile de maintenir l’alignement de l’objet en choisissant Affichage > Accrocher à la grille.

Vous pouvez modifier plus précisément les coordonnées d’un objet à l’aide de la palette Disposition (présentée dans l’illustration 10). Cette palette permet de définir les coordonnées X et Y, ainsi que la largeur et la hauteur de l’objet.

![Utilisation de coordonnées pour positionner précisément un objet à l’aide de la palette Disposition](/help/forms/using/assets/image-10.png)

Illustration 10 : **utilisation de coordonnées pour positionner précisément un objet avec la palette Disposition**

>[!NOTE]
> Lorsque la légende et la commande ne sont pas fusionnées, la position de la légende d’une commande de formulaire est indépendante de l’ordre dans lequel les lecteurs d’écran lisent l’objet et ses éléments. Pour plus d’informations sur les légendes, voir la section 2.5 Fournir des libellés appropriés pour les commandes de formulaire dans ce guide.

### Utilisation de sous-formulaires pour influencer l’ordre de tabulation par défaut

Comme mentionné ci-dessus, les sous-formulaires vous permettent d’insérer des groupes d’objets ayant leur propre ordre de tabulation. Vous pouvez créer un sous-formulaire en effectuant l’une des opérations suivantes :
* Choisissez Insertion > Standard > Sous-formulaire.
* Sélectionnez vos objets dans la palette Hiérarchie, puis regroupez-les dans un sous-formulaire en choisissant Insertion > Placer dans un sous-formulaire.
* Sélectionnez vos objets dans le formulaire, cliquez avec le bouton droit de la souris sur la sélection, puis choisissez Placer dans un sous-formulaire.

Lorsque deux sous-formulaires contenant des objets de champ sont positionnés côte à côte, l’ordre de tabulation passe par les champs du premier sous-formulaire avant de passer au suivant. Ceci est présenté dans l’illustration 11, où deux sous-formulaires sont utilisés pour créer un ordre de tabulation par défaut basé sur les colonnes.

![Ordre de tabulation par défaut utilisant les sous-formulaires](/help/forms/using/assets/image-11.png)

Illustration 11 : **ordre de tabulation par défaut utilisant les sous-formulaires**

Les sous-formulaires, les cases d’option et les zones de contenu, ainsi que la position verticale des objets sur une page et sur son gabarit de page, influent tous sur l’ordre de tabulation.

### Création d’un ordre de tabulation personnalisé à l’aide de la palette Ordre de tabulation

Vous pouvez modifier l’ordre de tabulation par défaut lorsque vous avez besoin d’une séquence différente dans votre formulaire. La modification ne peut pas être effectuée lors du positionnement ou du regroupement dans les sous-formulaires. Pour modifier l’ordre de tabulation par défaut, vous pouvez créer un ordre de tabulation personnalisé à l’aide de la palette Ordre de tabulation.
La palette Ordre de tabulation (voir l’illustration 12) vous permet d’examiner et de modifier l’ordre dans lequel les objets de votre formulaire sont lus par les dispositifs d’assistance et parcourus par la touche de tabulation de l’utilisateur ou de l’utilisatrice.

![Palette Ordre de tabulation](/help/forms/using/assets/image-12.png)

Illustration 12 : **palette Ordre de tabulation**

La palette Ordre de tabulation offre une autre vue de l’ordre de tabulation dans le formulaire. Elle affiche tous les objets du formulaire sous forme de liste numérotée, où chaque nombre représente la position de l’objet dans l’ordre de tabulation.
Pour ouvrir la palette Ordre de tabulation, choisissez Fenêtre > Ordre de tabulation.


La palette Ordre de tabulation contient les marqueurs visuels suivants :
* Une barre grise marque chaque page du formulaire. L’ordre de tabulation de chaque page commence par le nombre 1.
* La lettre M à l’intérieur d’un cercle vert indique les objets de gabarit de page (elle n’est visible que lorsque vous affichez le formulaire dans le panneau Vue de conception).
* Une plage de nombres indique les objets dans un fragment.
* Un arrière-plan jaune indique l’élément actuellement sélectionné.
* Une icône de verrouillage en regard du premier objet de la page indique que l’objet ne peut pas être déplacé dans l’ordre de tabulation (visible uniquement lors de l’affichage du formulaire dans l’onglet Gabarits).

La liste affiche les mêmes nombres d’ordres de tabulation que les nombres affichés sur le formulaire lui-même lorsque vous choisissez Affichage > Afficher l’ordre de tabulation. Pour changer la position d’un objet dans l’ordre de tabulation, déplacez-le vers le haut ou vers le bas dans la liste de la palette Ordre de tabulation. Vous pouvez déplacer un seul objet ou un groupe d’objets. Pour ce faire, utilisez l’une des méthodes suivantes :

* Faites glisser l’objet sélectionné vers le haut ou le bas de la liste et placez-le à l’emplacement souhaité. Une poignée noire indique votre position actuelle dans la liste avant de placer l’objet.
* Dans la palette Ordre de tabulation, cliquez sur les boutons Haut ou Bas jusqu’à ce que l’objet sélectionné occupe la bonne position. Vous pouvez également appuyer sur Ctrl+Flèche Haut ou Ctrl+Flèche Bas.
* Dans le menu de la palette Ordre de tabulation, choisissez Déplacer vers le haut ou Déplacer vers le bas.
* Dans la liste de la palette Ordre de tabulation, cliquez sur l’objet sélectionné (ou sélectionnez-le et appuyez sur la touche F2) pour rendre modifiable le nombre figurant en regard du nom de l’objet. Saisissez ensuite le numéro correspondant à la nouvelle position de l’objet dans l’ordre de tabulation, puis appuyez sur Entrée.
* Sélectionnez Copier dans le menu de la palette Ordre de tabulation, sélectionnez dans la liste l’objet au-dessus duquel vous souhaitez placer l’objet que vous déplacez, puis choisissez Coller dans le menu.

Lorsque vous déplacez l’objet à un nouvel emplacement dans l’ordre, LiveCycle Designer réaffecte les numéros de l’ordre de tabulation. Bien que l’ordre de tabulation des objets situés sur un gabarit s’affiche dans le panneau Vue de conception, vous ne pouvez le modifier que dans l’onglet Gabarits. Si vous utilisez des références à des fragments dans votre formulaire, l’ordre de tabulation à l’intérieur d’un fragment est visible lors de l’affichage de l’ordre du formulaire. Pour modifier l’ordre de tabulation dans un fragment, vous devez ouvrir le fichier source du fragment à des fins d’édition, apporter la modification et enregistrer le fichier. Tous les formulaires qui utilisent ce fragment sont affectés par cette modification.

Si vous décidez de ne pas respecter l’ordre de tabulation personnalisé dans votre formulaire, vous pouvez rapidement revenir à l’ordre de tabulation automatique (par défaut) en procédant comme suit (vous perdrez toute modification apportée à l’ordre de tabulation) :
1. Dans la palette Ordre de tabulation, sélectionnez Automatique.
1. Dans la zone de message qui s’affiche, cliquez sur Oui pour confirmer la suppression de l’ordre de tabulation personnalisé.

**Points de contrôle connexes**
* Section 508 §1194.21
   * (a) Lorsque le logiciel est conçu pour fonctionner sur un système disposant d’un clavier, les fonctions du produit doivent être exécutables à partir d’un clavier où la fonction elle-même, ou le résultat de l’exécution d’une fonction, peut être détectée textuellement.
* WCAG 1.0
   * 9.2 Assurez-vous que tout élément possédant sa propre interface peut être utilisé de manière indépendante de l’appareil.
* WCAG 2.0
   * 1.3.2 Séquence significative : lorsque la séquence dans laquelle le contenu est présenté influe sur sa signification, il est possible de déterminer par programmation une séquence de lecture correcte. (Niveau A)
   * 2.1.1 Clavier : toutes les fonctionnalités du contenu sont exploitables à l’aide d’une interface clavier, sans nécessiter de minutage spécifique pour les touches individuelles, sauf lorsque la fonction sous-jacente nécessite une entrée dépendant du chemin du mouvement de l’utilisateur ou de l’utilisatrice et pas seulement des points d’entrée. (Niveau A)
   * 2.1.3 Clavier (sans exception) : toutes les fonctionnalités du contenu sont utilisables via une interface clavier sans nécessiter de minutage spécifique pour les touches individuelles. (Niveau AAA)
   * 2.4.3 Ordre de focus : s’il est possible de naviguer de manière séquentielle dans une page web et que les séquences de navigation affectent la signification ou le fonctionnement, l’attribution du focus aux composants concernés obéit à un ordre préservant la signification et la maniabilité. (Niveau A)


## Accessibilité des commandes de formulaire avec un clavier{#ensure-keyboard-accessible}

Les utilisateurs et utilisatrices doivent pouvoir remplir le formulaire entièrement à l’aide du clavier ou d’un autre appareil de saisie équivalent. Certaines personnes ayant une mobilité réduite ou une déficience visuelle sont parfois contraintes de n’utiliser que le clavier. De plus, de nombreuses personnes préfèrent saisir leurs données au moyen du clavier plutôt que de la souris. En proposant différents modes de saisie des données, vous créez non seulement des formulaires accessibles, mais qui répondent également aux préférences de l’ensemble des utilisateurs et utilisatrices.

Dans LiveCycle Designer, le moyen le plus simple de vous assurer que vos commandes sont accessibles via le clavier consiste à utiliser les commandes répertoriées sous l’onglet Commun de la palette Bibliothèque d’objets. Ces commandes répondent par défaut aux saisies de la souris et du clavier. Pour plus d’informations, voir la section 2.3 Choisir les commandes adéquates dans ce guide.

Un autre aspect important de l’accessibilité clavier est de s’assurer que chaque élément interactif fait partie de l’ordre de tabulation du formulaire. La personne peut ainsi déplacer le curseur vers l’avant et vers l’arrière dans le formulaire à l’aide des touches Tab et Maj+Tab. Veillez à définir un ordre de tabulation logique qui inclut tous les champs et boutons. Pour plus d’informations, reportez-vous à la section 2.6. S’assurer que l’ordre de lecture et de tabulation est correct dans ce guide.

Enfin, il est important de s’assurer que le comportement scripté est également accessible depuis le clavier et ne dépend pas des événements spécifiques à l’appareil. L’événement de souris MouseEnter, par exemple, ne peut pas être exécuté à l’aide du clavier. En outre, ces gestionnaires d’événements ne doivent pas interférer avec l’accessibilité clavier. Par exemple, assurez-vous que les événements de modification utilisés dans les listes déroulantes ou les zones de liste ne déclenchent pas d’actions inattendues.

**Points de contrôle connexes**
* Section 508 §1194.21
   * (a) Lorsque le logiciel est conçu pour fonctionner sur un système disposant d’un clavier, les fonctions du produit doivent être exécutables à partir d’un clavier où la fonction elle-même, ou le résultat de l’exécution d’une fonction, peut être détectée textuellement.
* WCAG 1.0
   * 6.4 Pour les scripts et les applets, assurez-vous que les gestionnaires d’événements sont indépendants de l’appareil de saisie (P2).
   * 9.2 Assurez-vous que tout élément possédant sa propre interface peut être utilisé de manière indépendante de l’appareil (P2).
   * 9.3 Pour les scripts, spécifiez des gestionnaires d’événements logiques plutôt que des gestionnaires d’événements dépendants du périphérique (P2).
* WCAG 2.0
   * 2.1.1 Clavier : toutes les fonctionnalités du contenu sont exploitables à l’aide d’une interface clavier, sans nécessiter de minutage spécifique pour les touches individuelles, sauf lorsque la fonction sous-jacente nécessite une entrée dépendant du chemin du mouvement de l’utilisateur ou de l’utilisatrice et pas seulement des points d’entrée. (Niveau A)
   * 2.1.2 Aucun piège au clavier : s’il est possible de déplacer le focus vers un composant de la page à l’aide d’une interface clavier, il peut être transféré ailleurs exclusivement à l’aide de l’interface clavier. Si la sélection nécessite d’autres fonctions que les touches de direction ou de tabulation non modifiées, ou d’autres méthodes de sortie standard, la personne est informée de la méthode nécessaire pour changer de focus. (Niveau A)
   * 2.1.3 Clavier (sans exception) : toutes les fonctionnalités du contenu sont utilisables via une interface clavier sans nécessiter de minutage spécifique pour les touches individuelles. (Niveau AAA)


## Utilisation responsable des couleurs{#use-color-responsibly}

La conception de formulaires pour l’accessibilité implique de prendre en compte des instructions supplémentaires pour l’utilisation de la couleur. Les concepteurs et conceptrices utilisent des couleurs pour améliorer l’apparence des formulaires, en mettant en surbrillance différents composants. Cependant, une utilisation incorrecte de la couleur peut rendre l’information dans votre formulaire difficile ou impossible à lire pour les personnes handicapées.

### Ne pas véhiculer des informations uniquement par la couleur

Les couleurs peuvent mettre en évidence et améliorer certaines parties de votre formulaire, mais vous ne devez pas véhiculer l’information uniquement par la couleur.

Les informations véhiculées uniquement par la couleur (couleurs ayant une signification sémantique) ne sont pas accessibles aux personnes aveugles. Il en va de même pour les personnes présentant des déficiences visuelles en matière de couleurs ou qui utilisent différents schémas de couleurs, comme un écran couleur à contraste élevé avec du texte ou un premier plan blanc sur fond noir. N’oubliez pas que les lecteurs d’écran ne peuvent pas détecter automatiquement les informations de couleur.

Par exemple, l’illustration 13 présente un champ de formulaire avec une légende rouge (indiquée à l’aide de la palette Police) pour indiquer que le champ de formulaire est obligatoire. Dans cet exemple, la couleur est le seul signe de la différence entre les champs de saisie obligatoires et facultatifs, ce qui rend impossible pour les personnes aveugles ou les personnes ayant certains types de daltonisme de les distinguer.

![Utilisation de la couleur seule pour véhiculer l’information](/help/forms/using/assets/image-13.png)

Illustration 13 : **utilisation de la couleur seule pour véhiculer l’information**

Pour résoudre ce problème, indiquez également le statut requis du formulaire dans le texte secondaire de la commande de formulaire (comme décrit dans la section 2.5 Fournir des libellés appropriés pour les commandes de formulaire). Par exemple, vous pouvez définir le texte du lecteur d’écran sur « Code postal (obligatoire) ». Pour les utilisateurs et utilisatrices qui rencontrent des difficultés à voir la couleur dans certaines combinaisons, il est recommandé de définir le type de champ de texte sur Entré par l’utilisateur ou l’utilisatrice - Obligatoire dans la palette Objet en plus du texte secondaire qui indique que le champ est obligatoire. Vous pouvez également utiliser d’autres indications que la couleur, telles que le texte visuel, les styles de texte et les styles de bordure. Toutefois, pour les utilisateurs et utilisatrices de lecteurs d’écran, vous devrez toujours transmettre les informations requises à l’aide de la palette Accessibilité.

En outre, lorsque vous fournissez des descriptions ou des instructions à l’utilisateur ou à l’utilisatrice du formulaire, gardez à l’esprit que les instructions basées sur la seule couleur ne sont pas suffisantes pour les personnes ayant une déficience visuelle. Par exemple, au lieu d’une instruction telle que « Cliquez sur le bouton vert pour continuer », utilisez une description textuelle pour les actions, comme « Cliquez sur le bouton suivant pour continuer ».

>[!NOTE]
> Cette bonne pratique n’interdit pas l’utilisation de la couleur. Elle interdit l’utilisation de la couleur comme seul moyen de transmettre des informations importantes. Si une indication visuelle est toujours souhaitée pour ce type d’informations, le concepteur ou la conceptrice peut utiliser un astérisque ou un indicateur visuel similaire pour marquer les champs requis.

### Fournir un contraste des couleurs suffisant

Les personnes ayant une déficience visuelle s’appuient sur le contraste prononcé entre le texte et l’arrière-plan pour lire des formulaires. Lorsque le contraste entre les couleurs d’arrière-plan et de premier plan n’est pas suffisant, un formulaire peut devenir difficile, voire impossible, à lire pour certains utilisateurs et utilisatrices. L’illustration 14 présente un exemple de formulaire avec un contraste insuffisant.

![Formulaire avec un contraste de couleur insuffisant](/help/forms/using/assets/image-14.png)

Illustration 14 : **formulaire avec un contraste de couleur insuffisant**

Il est fortement conseillé d’utiliser la police et les couleurs d’arrière-plan par défaut, à savoir le contenu noir sur fond blanc. Si vous devez modifier ces couleurs par défaut, veillez à choisir une combinaison appropriée de couleurs à contraste élevé ; utilisez une couleur de premier plan foncée sur un arrière-plan clair, ou inversement. Pour plus de certitude, utilisez un outil (tel que l’analyseur de contraste des couleurs WAT-C) pour vérifier que le contraste est suffisant.

Adobe Reader et Adobe Acrobat permettent aux utilisateurs et aux utilisatrices de spécifier si les couleurs doivent être remplacées pour répondre à leurs besoins visuels. Les utilisateurs et utilisatrices peuvent spécifier leur propre schéma de contraste ou choisir d’utiliser un schéma fourni par le système d’exploitation. En outre, Adobe Reader et Adobe Acrobat ont leur propre modèle de contraste élevé qui peut être activé. Pour ces options, la meilleure approche consiste toujours à utiliser les couleurs par défaut.

Lors de la conception de votre formulaire, testez-le fréquemment à l’aide d’un paramètre de modèle de couleurs similaire à celui que beaucoup de personnes ayant une déficience visuelle utiliseront pour remplir le formulaire. Cette pratique vous permet de détecter et de corriger les problèmes dès le début du processus de conception.

Recommandations pour l’utilisation des couleurs :
* Vérifiez qu’aucune information n’est perdue si la couleur sémantique n’est pas visible.
* Si vous ne pouvez pas utiliser les couleurs par défaut, vérifiez que les couleurs sont très contrastées, comme le noir sur fond clair (blanc). Les utilisateurs et utilisatrices dont la vision est partielle nécessitent généralement un contraste élevé entre le texte et son arrière-plan pour pouvoir le lire.
* Testez la lisibilité de vos formulaires en passant votre écran à un affichage à contraste élevé, à la fois sous Windows et dans Adobe Reader ou Adobe Acrobat. Mac OSX ne propose qu’un filtre en niveaux de gris simple pour un contraste élevé, ce qui n’est pas suffisant pour le test.
* Ne transmettez pas d’informations uniquement basées sur la couleur. Par exemple, n’utilisez pas uniquement la couleur pour mettre en surbrillance des éléments importants de texte. Utilisez également d’autres méthodes de mise en surbrillance et des descriptions de texte.
* N’utilisez pas trop de couleurs, car cela peut rendre difficile la lecture des informations présentes dans le contenu. Veillez toujours à ce que la lisibilité des informations reste votre priorité absolue lorsque vous décidez des couleurs à utiliser.

**Points de contrôle connexes**
* Section 508 §1194.21
   * (i) Le codage par couleur ne doit pas être utilisé comme seul moyen de transmettre des informations, d’indiquer une action, de demander une réponse ou de distinguer un élément visuel.
* WCAG 1.0
   * 2.1 Assurez-vous que toutes les informations véhiculées par la couleur sont également disponibles sans couleur, par exemple à partir du contexte ou des balises.
   * 2.2 Assurez-vous que les combinaisons de couleurs de premier plan et d’arrière-plan offrent un contraste suffisant lorsqu’elles sont affichées par une personne ayant un déficit visuel basé sur les couleurs ou sur un écran noir et blanc. [Priorité 2 pour les images, Priorité 3 pour le texte] (P2).
* WCAG 2.0
   * 1.4.1 Utilisation de la couleur : la couleur n’est pas utilisée comme seul moyen visuel de transmettre des informations, d’indiquer une action, de demander une réponse ou de distinguer un élément visuel. (Niveau A)
   * 1.4.3 Contraste (minimum) : la présentation visuelle du texte et des images du texte présente un rapport de contraste d’au moins 4,5:1, sauf dans les cas suivants : (Niveau AAA)
   * 1.4.6 Contraste (amélioré) : la présentation visuelle du texte et des images du texte présente un rapport de contraste d’au moins 7:1, sauf dans les cas suivants : (Niveau AAA)


## Fourniture de cellules d’en-tête pour les tableaux{#provide-heading-cells}

Les tableaux constituent un moyen efficace d’organiser et de présenter le contenu dans des formulaires accessibles. Utilisées de manière appropriée, les lignes et colonnes d’un tableau fournissent une structure prévisible et cohérente pour le contenu du formulaire. Par exemple, lorsqu’un utilisateur ou une utilisatrice de lecteur d’écran navigue dans une cellule de ligne de contenu, le lecteur d’écran indique l’emplacement de la cellule, puis lit le contenu de celle-ci. Le lecteur d’écran indique l’emplacement de la cellule à l’aide d’une combinaison d’en-têtes de lignes et de colonnes ou de numéros de lignes et de colonnes. Comme les lecteurs d’écran fournissent des informations qui orientent l’utilisateur ou l’utilisatrice vers l’emplacement du contenu dans le tableau, sa disposition affecte directement l’accessibilité de celui-ci.

Vous pouvez spécifier les rôles suivants pour les éléments de tableau au fur et à mesure de la construction des tableaux. Ces rôles permettent aux lecteurs d’écran de parcourir la structure du tableau à l’aide de raccourcis spéciaux et transmettent à l’utilisateur ou à l’utilisatrice la relation entre les cellules du tableau et les cellules d’en-tête correspondantes.
* Tableau
Attribue le rôle d’un tableau au sous-formulaire sélectionné. Lorsque la personne accède à ce sous-formulaire, la plupart des lecteurs d’écran l’identifient comme un tableau et indiquent le nombre de lignes et de colonnes.
* Rangée d’en-tête
Attribue le rôle de rangée d’en-tête au sous-formulaire sélectionné ou à la rangée de tableau sélectionnée. Lorsqu’ils vocalisent le contenu d’une cellule de rangée de contenu, la plupart des lecteurs d’écran identifient d’abord le contenu de la cellule correspondante dans la rangée d’en-tête.
* Rangée de contenu
Attribue le rôle d’une rangée de contenu au sous-formulaire ou à la rangée de tableau sélectionné. Si une cellule contient un sous-formulaire, les lecteurs d’écran vocalisent généralement le contenu de la cellule correspondante dans la rangée d’en-tête, suivie des champs du sous-formulaire.
* Rangée de pied de page
Attribue le rôle de rangée de pied de page au sous-formulaire sélectionné ou à la rangée de tableau sélectionnée.
* (Aucun)
Indique une ligne qui contient des informations sur le tableau ou son contenu. La rangée n’est pas considérée comme faisant partie du tableau ; toutefois, le lecteur d’écran lit son contenu.

Lorsqu’ils sont utilisés correctement, les tableaux constituent un moyen efficace d’organiser et de présenter les informations tabulaires. Évitez les tableaux trop complexes, tels que ceux contenant des tableaux et des sections imbriqués.

### Définition de l’accessibilité des tableaux simples

Il est recommandé d’utiliser des tableaux avec des dispositions simples. Les tableaux simples commencent par une seule rangée d’en-tête suivie de rangées de contenu.

Lors de la conception de tableaux simples pour l’accessibilité, tenez compte des recommandations suivantes :

* L’ordre de tabulation d’un tableau est l’ordre géographique, identique à celui du formulaire. Assurez-vous que le contenu du tableau est organisé de manière à ce qu’il soit logique lorsqu’il est lu de gauche à droite et de haut en bas.
* La plupart des lecteurs d’écran interprètent la première ligne d’un tableau comme la rangée d’en-tête. Lors de la lecture du contenu d’une cellule de rangée de contenu, ces lecteurs d’écran lisent d’abord le contenu de la cellule de rangée d’en-tête associée. Assurez-vous que le contenu de chaque cellule de rangée d’en-tête décrit le contenu de la colonne de manière significative.
* Évitez les cellules qui s’étendent sur plusieurs colonnes, tableaux imbriqués ou sections de tableau. Certains lecteurs d’écran ont des difficultés à interpréter correctement ces fonctions ou peuvent ne pas les utiliser. Par exemple, si une cellule d’une rangée de contenu s’étend sur deux colonnes, les lecteurs d’écran peuvent ne pas référencer le contenu de cellule correct dans la rangée d’en-tête lors de la lecture de la cellule suivante de la rangée.

### Définition de l’accessibilité des tableaux complexes

Lors de la conception de tableaux pour l’accessibilité, assurez-vous que la disposition du tableau reste simple, avec une rangée d’en-tête suivie de rangées de contenu. Bien sûr, certains contenus peuvent nécessiter une disposition de tableau plus complexe. Par exemple, vous devrez peut-être utiliser une cellule s’étendant sur plusieurs en-têtes pour véhiculer efficacement le contenu.

Vous pouvez créer des tableaux complexes en utilisant l’objet de tableau ou en combinant des objets de sous-formulaire. L’objet de tableau vous permet d’utiliser des fonctionnalités destinées à faciliter la conception, telles que des options d’insertion et de redimensionnement de colonnes et de lignes.

À l’aide de la palette Accessibilité, vous pouvez définir des rôles associés à un tableau dans les sous-formulaires afin de créer un tableau complexe accessible. Selon votre expérience et vos préférences de conception, vous pouvez choisir de créer des tableaux complexes en combinant des objets de sous-formulaire. Par exemple, vous pouvez créer un sous-formulaire qui comprend deux rangées et spécifier ce sous-formulaire comme en-tête du tableau, puis spécifier un autre sous-formulaire pour les rangées de contenu du tableau.

Lors de l’utilisation d’objets de sous-formulaire au lieu d’objets de tableau pour créer des tableaux, les étapes supplémentaires suivantes sont requises :
* Dans l’onglet Sous-formulaire, définissez le type de chaque sous-formulaire sur Positionné.
* Dans la palette Accessibilité, définissez le rôle de sous-formulaire approprié pour chaque sous-formulaire composant le tableau. Par exemple, attribuez le rôle Rangée d’en-tête au sous-formulaire utilisé comme en-tête de tableau.
* Pour les rangées qui contiennent des informations sur le tableau ou son contenu, mais qui ne sont pas considérées comme faisant partie du tableau, attribuez le rôle de sous-formulaire Aucun. Le lecteur d’écran lit le contenu de la ligne.

Les fonctionnalités prises en charge par le lecteur d’écran déterminent les informations lues pour un tableau complexe. Prenons l’exemple d’un tableau contenant une rangée d’en-tête et une section contenant une rangée d’en-tête. Lorsque la personne accède à une cellule de rangée de contenu dans la section du tableau, les lecteurs d’écran lisent généralement le contenu suivant, dans l’ordre :
* Contenu de la cellule appropriée dans la rangée d’en-tête du tableau
* Contenu de la cellule appropriée dans la rangée d’en-tête de la section
* Contenu de la cellule sélectionnée
Certains lecteurs d’écran, cependant, peuvent ne pas lire le contenu des deux rangées d’en-tête.

Créez des noms ou des titres visibles significatifs pour vos tableaux. Vous pouvez créer un nom de tableau sous forme de texte statique dans Adobe LiveCycle Designer et le placer devant le tableau. Vous pouvez regrouper un tableau et son nom dans un sous-formulaire. Les sous-formulaires sont particulièrement utiles lorsque vous souhaitez combiner des objets associés dans une mise en page.

Pour les commandes dans les cellules d’un tableau, le lecteur d’écran annonce la légende, l’info-bulle ou le texte du lecteur d’écran personnalisé que vous spécifiez pour l’objet. Si vous souhaitez utiliser l’en-tête de colonne comme texte secondaire d’une commande dans un tableau, ne fournissez pas de légende, d’info-bulle ou de texte du lecteur d’écran personnalisé. Notez toutefois que cette stratégie n’est pas toujours aussi claire pour les utilisateurs et utilisatrices de lecteurs d’écran, car les lecteurs d’écran peuvent uniquement associer l’en-tête de colonne à la commande lorsque la personne n’est pas en mode d’interaction de formulaire du lecteur d’écran.

**Points de contrôle connexes**
* Section 508 §1194.22
   * (g) Les en-têtes de ligne et de colonne doivent être identifiés pour les tableaux de données.
   * (h) Le balisage doit être utilisé pour associer des cellules de données et des cellules d’en-tête aux tableaux de données présentant deux niveaux logiques ou plus d’en-têtes de ligne ou de colonne.
* WCAG 1.0
   * 5.1 Pour les tableaux de données, identifiez les en-têtes de ligne et de colonne (P1).
   * 5.2 Pour les tableaux de données comportant deux niveaux logiques ou plus d’en-têtes de ligne ou de colonne, utilisez les balises pour associer les cellules de données et les cellules d’en-tête (P1).
* WCAG 2.0
   * 1.3.1 Informations et relations : les informations, la structure et les relations de la présentation peuvent être déterminées par programmation ou sont disponibles dans le texte. (Niveau A)


## Fourniture d’une structure de formulaire navigable{#provide-navigable-form}

Lorsqu’un formulaire devient long et complexe, sa facilité d’utilisation est fortement influencée par sa structure. De la même manière qu’un livre est plus facile à comprendre lorsqu’il est divisé en chapitres et en sections, un formulaire devient plus facile à utiliser lorsqu’il est divisé en en-têtes et en sous-en-têtes. Ce partitionnement est particulièrement utile pour les utilisateurs et utilisatrices de lecteurs d’écran, pour les raisons suivantes :
* Chaque en-tête indique à l’utilisateur ou à l’utilisatrice du lecteur d’écran ce qui peut être attendu dans la section qui suit l’en-tête.
* Les lecteurs d’écran fournissent des raccourcis pour passer rapidement d’un en-tête à un autre dans le formulaire. Ils permettent également à la personne d’accéder à une liste d’en-têtes, qui fournit une vue d’ensemble de la structure du document et permet une navigation rapide.

Fournir des mécanismes qui permettent aux utilisateurs et aux utilisatrices d’ignorer d’autres zones du formulaire peut faciliter le processus. Vous pouvez ajouter une structure d’en-tête à votre formulaire à l’aide de la palette Accessibilité de LiveCycle Designer.

### Fournir des mécanismes de saut

Les utilisateurs et utilisatrices sans déficiences visuelles peuvent analyser une page dans n’importe quel ordre. Ils peuvent commencer par consulter le coin inférieur droit de la page et parcourir le contenu à l’envers. Un utilisateur ou une utilisatrice de lecteur d’écran ne dispose pas de cette option, car le lecteur d’écran commence à lire la page en haut à gauche (comme présenté dans le code source) et se déplace dans un ordre linéaire. En outre, un utilisateur ou une utilisatrice sans déficience visuelle peut parcourir la page à la recherche de liens intéressants et les activer avec la souris. Un utilisateur ou une utilisatrice de lecteur d’écran doit parcourir la page de manière séquentielle.

La méthode la plus simple et la plus efficace pour fournir une structure de formulaire navigable consiste à utiliser des en-têtes structurels et des listes correctement définies dans votre formulaire.
Vous pouvez également fournir des mécanismes qui permettent à la personne d’accéder à d’autres zones du formulaire, par exemple en ajoutant des boutons de navigation en haut et en bas du formulaire. Dans la partie supérieure d’un formulaire, vous pouvez inclure des boutons comme Ouvrir le fichier de données, Page précédente et Page suivante. Dans la partie inférieure du formulaire, vous pouvez inclure des boutons comme Enregistrer les données, Envoyer les données par e-mail, Haut de la page et Imprimer.

Les champs intelligents peuvent être un moyen efficace de faciliter le remplissage de certains formulaires. Par exemple, un formulaire de demande de voyage peut comporter plusieurs lignes et colonnes de champs. Si une rangée spécifique est vide, appuyer sur la touche de tabulation du dernier élément de cette rangée peut passer à la section suivante du formulaire plutôt que de continuer à parcourir plusieurs champs qui resteront vides.

### Ajout d’en-têtes à l’aide de la palette Accessibilité

Vous pouvez utiliser la palette Accessibilité pour attribuer des rôles aux objets en fonction de leur objectif. Ces rôles peuvent être appliqués pour créer des en-têtes à différents niveaux.

![Spécification d’un rôle d’en-tête dans la palette Accessibilité](/help/forms/using/assets/image-15.png)
Illustration 15 : **spécification d’un rôle d’en-tête dans la palette Accessibilité**

Pour créer un en-tête dans votre formulaire, procédez comme suit :

1. Identifiez le début de chaque segment logique de votre formulaire à l’aide de libellés de texte statique.
1. Pour chaque libellé, sélectionnez l’une des options d’en-tête Rôle dans la palette Accessibilité. Les différents niveaux d’en-tête (1 à 6) vous permettent de créer une structure d’en-tête dans votre formulaire. Commencez par le niveau 1, puis utilisez le niveau 2 et ainsi de suite pour les sous-sections imbriquées.

La plupart des lecteurs d’écran permettent aux utilisateurs et aux utilisatrices de naviguer rapidement entre les éléments d’en-tête en fonction de leur niveau. L’illustration 16 présente un formulaire divisé en segments plus petits utilisant des en-têtes. Dans cet exemple, la structure d’en-tête suivante est utilisée :

* Niveau d’en-tête 1 : demande de produit
   * Niveau d’en-tête 2 : informations sur la commande
      * Niveau d’en-tête 3 : options de livraison
* Niveau d’en-tête 2 : informations supplémentaires
   * Niveau d’en-tête 3 : informations personnelles
   * Niveau d’en-tête 3 : adresse

![Structuration d’un formulaire à l’aide d’en-têtes](/help/forms/using/assets/image-16.png)

Illustration 16 : **structuration d’un formulaire à l’aide d’en-têtes**

Ces en-têtes sont simplement des éléments de texte statique auxquels ont été attribués une taille de police spécifique et un rôle d’en-tête au niveau approprié.

>[!NOTE]
> La simple modification de l’aspect visuel d’un libellé de texte pour donner l’apparence d’un en-tête n’aura pas pour effet que les lecteurs d’écran le reconnaissent comme en-tête. Vous devez appliquer un rôle d’en-tête.

Assurez-vous toujours que l’ordre des niveaux d’en-tête est logique. Par exemple, une sous-section d’un en-tête de niveau 2 doit toujours être un en-tête de niveau 3 ; vous ne devez jamais ignorer les niveaux lors du balisage des sous-sections. Les utilisateurs et utilisatrices de lecteurs d’écran utilisent les différents niveaux pour mieux comprendre la structure du formulaire. Par exemple, après avoir rencontré un en-tête de niveau 2, la personne peut utiliser un raccourci pour rechercher des en-têtes de niveau 3 et déterminer s’il existe des sous-sections. Si vous ignorez les niveaux, la personne aura des difficultés à identifier ces sous-sections.

### Balisage des listes

Il peut également être utile d’ajouter du contenu de liste à votre formulaire. Les listes sont utiles pour regrouper des éléments connexes. Elles permettent aux utilisateurs et aux utilisatrices de lecteurs d’écran de savoir combien d’éléments se trouvent dans une liste et de naviguer rapidement au-delà. Le balisage correct des listes rend la structure de votre formulaire plus claire pour les utilisateurs et utilisatrices de lecteurs d’écran.

Dans LiveCycle Designer, vous créez des listes à l’aide de sous-formulaires avec les étapes suivantes :

1. Sélectionnez un sous-formulaire contenant le contenu qui sera marqué comme éléments de liste.
1. Dans la palette Accessibilité, sélectionnez Liste comme rôle.
1. Sélectionnez chaque sous-formulaire imbriqué dans le sous-formulaire Liste, puis définissez son rôle sur Élément de liste.

>[!NOTE]
> Un rôle Élément de liste ne peut être attribué qu’à un sous-formulaire contenu dans un sous-formulaire dont le rôle Liste est spécifié. Vous ne pouvez pas définir un tableau ou une ligne de tableau en tant que liste ou élément de liste ; toutefois, un élément de liste peut contenir un tableau.

**Points de contrôle connexes**
* Section 508 §11934.22
   * (o) Une méthode permettant aux utilisateurs et aux utilisatrices d’ignorer les liens de navigation répétitifs doit être fournie.
* WCAG 1.0
   * 3.5 Utiliser des éléments d’en-tête pour transmettre la structure du document et utilisez-les conformément aux spécifications (P2).
   * 3.6 Baliser correctement les listes et les éléments de liste. (P2).
   * 12.3 Diviser de grands blocs d’information en groupes plus faciles à gérer, le cas échéant. (P2).
   * 13.3 Fournir des informations sur la disposition générale d’un site (par exemple, une carte du site ou une table des matières).
   * 13.4 Utiliser les mécanismes de navigation de manière cohérente (P2).
* WCAG 2.0
   * 1.3.2 Séquence significative : lorsque la séquence dans laquelle le contenu est présenté influe sur sa signification, il est possible de déterminer par programmation une séquence de lecture correcte. (Niveau A)
   * 2.4.1 Contournement de blocs : un mécanisme permet de contourner des blocs de contenu répétés sur plusieurs pages web. (Niveau A)
   * 2.4.5 Plusieurs méthodes : différentes méthodes sont possibles pour localiser une page web dans un ensemble de pages, sauf lorsque cette page résulte d’un processus ou d’une étape de processus. (Niveau AA)
   * 2.4.6 Titres et libellés : les titres et les libellés décrivent le sujet ou l’objectif. (Niveau AA)
   * 2.4.10 En-têtes de section : les en-têtes de section permettent d’organiser le contenu. (Niveau AAA)
   * 3.2.3 Navigation cohérente : les mécanismes de navigation répétés sur plusieurs pages web regroupées s’enchaînent selon le même ordre relatif à chaque répétition, sauf si l’utilisateur ou l’utilisatrice effectue une modification. (Niveau AA)


## Évitement des scripts perturbateurs{#avoid-disruptive-scripting}

Dans le cadre du processus de conception de formulaire, les développeurs et développeuses de formulaires peuvent utiliser des scripts pour offrir une expérience client plus riche. Vous pouvez ajouter des scripts à la plupart des champs et objets de formulaire. Par exemple, vous pouvez créer des scripts simples pour mettre à jour dynamiquement les valeurs d’un formulaire interactif en réponse aux entrées de l’utilisateur ou de l’utilisatrice.

Lors de la conception de scripts pour l’accessibilité, tenez compte des instructions générales suivantes :

* N’interrompez pas visuellement le contenu du formulaire. Par exemple, évitez les fonctionnalités qui entraînent le scintillement, le clignotement ou le déplacement du contenu.
* Assurez-vous que les fenêtres contextuelles ne s’affichent que suite à des actions initiées par l’utilisateur ou l’utilisatrice. De même, n’autorisez pas le focus actuel du formulaire (la vue actuelle de l’utilisateur ou de l’utilisatrice) à modifier ou à réafficher le contenu, sauf si la personne est à l’origine de cette action. Par exemple, si la personne remplit des champs dans la moitié inférieure du formulaire, n’autorisez pas le changement de focus dans le coin supérieur gauche du formulaire, sauf si la personne choisit de naviguer jusqu’à cet emplacement.
* Les utilisateurs et utilisatrices présentant un handicap peuvent avoir besoin de plus de temps pour saisir des données dans les champs. Ne spécifiez pas de réponses temporelles pour les champs de saisie.
* N’oubliez pas que les scripts côté client peuvent interférer avec les lecteurs d’écran et les claviers s’ils modifient le focus de l’application cliente. Par exemple, les événements change et mouseEnter, lorsqu’ils sont utilisés avec des listes déroulantes ou des zones de liste, peuvent entraîner des actions inattendues. Vérifiez que les scripts côté client n’entraînent pas de problèmes pour les utilisateurs et utilisatrices de lecteurs d’écran et les personnes utilisant uniquement le clavier.
* Les utilisateurs et utilisatrices de technologies d’assistance ont parfois besoin de temps supplémentaire pour effectuer des tâches. Dans tous les cas où une routine minutée est sur le point d’expirer, affichez un message accessible pour autoriser une prolongation. Les zones d’alerte créées via JavaScript sont utilisables par les technologies d’assistance. Il est également possible de déployer une nouvelle fenêtre comportant un message pour alerter l’utilisateur ou l’utilisatrice d’un délai d’expiration imminent.

**Points de contrôle connexes** :
* Section 508 §1194.22
   * (l) Lorsque les pages utilisent des langages de script pour afficher du contenu ou pour créer des éléments d’interface, les informations fournies par le script doivent être identifiées par un texte fonctionnel pouvant être lu par les dispositifs d’assistance.
   * (p) Lorsqu’une réponse minutée est requise, la personne doit être alertée et disposer d’un temps suffisant pour indiquer qu’elle a besoin de plus de temps.
* WCAG 1.0
   * 1.4 Pour toute présentation multimédia basée sur le temps (par exemple, un film ou une animation), synchronisez les alternatives équivalentes (par exemple, les sous-titres ou les descriptions auditives de la piste visuelle) avec la présentation (P1).
   * 6.2 S’assurer que les équivalents du contenu dynamique sont mis à jour lorsque le contenu dynamique change.
   * 6.3 S&#39;assurer que les pages sont utilisables lorsque les scripts, applets ou autres objets de programmation sont désactivés ou ne sont pas pris en charge. Si cela n’est pas possible, fournissez des informations équivalentes sur une autre page accessible.
   * 6.5 S&#39;assurer que le contenu dynamique est accessible ou fournir une autre présentation ou page (P2).
   * 8.1 Rendre les éléments programmatiques tels que les scripts et les applets directement accessibles ou compatibles avec les technologies d’assistance [Priorité 1 si la fonctionnalité est importante et n’est pas présentée ailleurs], sinon (P2).
   * 9.3 Pour les scripts, spécifiez des gestionnaires d’événements logiques plutôt que des gestionnaires d’événements dépendants du périphérique (P2).
   * 10.1 Tant que les agents utilisateurs ne permettent pas aux utilisateurs et aux utilisatrices de désactiver les fenêtres générées, ne provoquez pas l’affichage de fenêtres contextuelles ou autres et ne modifiez pas la fenêtre active sans en informer l’utilisateur ou l’utilisatrice.
* WCAG 2.0
   * 3.2.1 Au focus : lorsqu’un composant de l’interface utilisateur reçoit le focus, il ne doit pas déclencher de changement de contexte. (Niveau A)
   * 3.2.2 À la saisie : la modification d’un paramètre de composant de l’interface d’utiliseur n’entraîne pas automatiquement un changement de contexte, sauf si la personne a été informée du comportement avant d’utiliser ce composant. (Niveau A)
   * 3.2.5 Changement sur demande : un changement de contexte est initié uniquement sur demande de l’utilisateur ou de l’utilisatrice ou un mécanisme est disponible pour désactiver un tel changement. (Niveau AAA)

## Accessibilité de tout le contenu audio et vidéo{#ensure-audio-video-accessible}

Si vos formulaires contiennent du contenu audio ou vidéo, notamment des clips audio et vidéo, vous devez vous assurer que ce contenu est accessible. Plus précisément, assurez-vous que les clips vidéo incorporés dans les formulaires contiennent des légendes (parfois appelés sous-titres) pour les utilisateurs et utilisatrices sourds et malentendants et des descriptions vidéo pour les utilisateurs et utilisatrices aveugles. Pour les fichiers audio qui ne sont pas synchronisés avec le contenu vidéo, une simple transcription suffit.
Pour les médias basés sur Flash, consultez ce [lien](/help/forms/using/best-practices-for-creating-forms-in-designer.md) pour plus d’informations sur la fourniture de sous-titres.

**Points de contrôle connexes** :
* Section 508 §1194.22
   * (b) Des alternatives équivalentes à toute présentation multimédia doivent être synchronisées avec la présentation.
* WCAG 1.0
   * 1.1 Proposer un équivalent textuel pour chaque élément non textuel (par exemple, par « alt », « longdesc » ou dans le contenu de l’élément). Cela comprend : les images, les représentations graphiques du texte (y compris les symboles), les zones cliquables, les animations (par exemple, les GIF animés), les applets et les objets programmatiques, l’art ascii, les cadres, les scripts, les images utilisées comme puces de liste, les espaces, les boutons graphiques, les sons (lus avec ou sans interaction de l’utilisateur ou de l’utilisatrice), les fichiers audio autonomes, les pistes audio de vidéo (P1).
   * 1.3 Tant que les agents utilisateurs ne peuvent pas lire automatiquement à voix haute l’équivalent textuel d’une piste visuelle, fournissez une description auditive des informations importantes de la piste visuelle d’une présentation multimédia (P1).
   * 1.4 Pour toute présentation multimédia basée sur le temps (par exemple, un film ou une animation), synchronisez les alternatives équivalentes (par exemple, les sous-titres ou les descriptions auditives de la piste visuelle) avec la présentation (P1).
* WCAG 2.0
   * 1.2.1 Contenu audio ou vidéo uniquement (pré-enregistré) : pour les médias audio pré-enregistrés uniquement et les médias vidéo pré-enregistrés uniquement, les faits suivants sont vrais, sauf si l’audio ou la vidéo est un média secondaire pour le texte et qu’il est clairement identifié comme tel : (Niveau A)
   * 1.2.2 Sous-titres (pré-enregistrés) : fournir des sous-titres pour tout contenu audio pré-enregistré dans un média synchronisé, excepté lorsque le média est un média de remplacement pour un texte et qu’il est clairement identifié comme tel. (Niveau A)
   * 1.2.3 Audio-description ou média de remplacement (pré-enregistré) : une alternative pour un média temporel ou une audio-description du contenu vidéo pré-enregistré est fournie pour un média synchronisé, sauf lorsque le média est un média de remplacement pour un texte et qu’il est clairement étiqueté comme tel. (Niveau A)
   * 1.2.4 Sous-titres (en direct) : des sous-titres pour tout contenu audio en direct sont fournis sous fome de média synchronisé. (Niveau AA)
   * 1.2.5 Audio-description (pré-enregistrée) : une audio-description est fournie pour tout contenu vidéo pré-enregistré sous forme de média synchronisé. (Niveau AA)
   * 1.2.6 Langue des signes (pré-enregistrée) : une interprétation en langue des signes est fournie pour tout contenu audio pré-enregistré sous forme de média synchronisé. (Niveau AAA)
   * 1.2.7 Audio-description étendue (pré-enregistrée) : lorsque les blancs présents dans le fond sonore ne sont pas suffisants pour permettre aux descriptions audio de transmettre le sens de la vidéo, fournir une audio-description étendue pour tout contenu vidéo pré-enregistré sous forme de média synchronisé. (Niveau AAA)
   * 1.2.8 Alternative de média (pré-enregistrée) : fournir une alternative pour un média temporel, pour tout contenu de type média synchronisé pré-enregistré et pour tout média vidéo pré-enregistré uniquement. (Niveau AAA)
   * 1.2.9 Audio uniquement (en direct) : fournir une alternative pour un média temporel, donnant des informations équivalentes pour un contenu seulement audio en direct. (Niveau AAA)

## Identification du langage naturel et de toute modification linguistique{#identify-natural-language}

Le contenu du formulaire est lu par les technologies d’assistance qui utilisent des synthétiseurs vocaux spécifiques à la langue. Il est donc important d’identifier correctement la langue principale du formulaire pour s’assurer que les formulaires sont lus dans la langue prévue.

Si le texte (ou le texte secondaire) de vos formulaires est présenté dans plusieurs langues, vous devez identifier les zones de votre formulaire dans lesquelles un changement est effectué d’une langue à l’autre.

Dans LiveCycle Designer, la définition de la langue principale est effectuée en définissant la propriété Paramètre régional du formulaire et la propriété Paramètre régional du sous-formulaire de niveau supérieur. Pour identifier les modifications apportées à la langue principale, modifiez la propriété Paramètre régional de tout objet qui utilise une langue autre que la langue du formulaire.

Pour définir la propriété Paramètre régional d’un formulaire, procédez comme suit :
1. Choisissez Fichier > Propriétés du formulaire, puis sélectionnez l’onglet Par défaut.
2. Sélectionnez la langue appropriée pour le paramètre régional du formulaire (voir l’illustration 17).
3. Cliquez sur OK.

![Modification des paramètres régionaux du formulaire dans la boîte de dialogue Propriétés du formulaire](/help/forms/using/assets/image-17.png)

Illustration 17 : **modification des paramètres régionaux du formulaire dans la boîte de dialogue Propriétés du formulaire**

Pour définir la propriété Paramètre régional du sous-formulaire de niveau supérieur ou d’un objet nécessitant une autre langue, procédez comme suit :
1. Sélectionnez le sous-formulaire ou l’objet de niveau supérieur dans la vue de conception.
1. Pour afficher la palette Objet, choisissez Fenêtre > Objet.
1. Dans la palette Objet, sélectionnez l’onglet Champ, puis, dans la liste Paramètre régional, sélectionnez la langue à utiliser pour l’objet (voir l’illustration 18). Lorsque vous appliquez des paramètres régionaux différents à des objets, gardez à l’esprit que les objets situés dans les tableaux et les sous-formulaires reçoivent automatiquement les mêmes paramètres régionaux que le tableau et l’objet de sous-formulaire.

![Modification des paramètres régionaux d’un objet](/help/forms/using/assets/image-18.png)

Illustration 18 : **modification des paramètres régionaux d’un objet**

**Points de contrôle connexes** :
* WCAG 1.0
   * 4.1 Identifier clairement les changements dans la langue naturelle du texte d’un document et les équivalents textuels (par exemple, les sous-titres).
* WCAG 2.0
   * 3.1.1 Langue de la page : la langue humaine par défaut de chaque page web peut être définie par programmation. (Niveau A)
   * 3.1.2 Langue d’un passage : la langue de chaque passage ou expression du contenu peut être déterminée par programmation sauf pour un nom propre, pour un terme technique, pour un mot dont la langue est indéterminée ou pour un mot ou une expression faisant partie du langage courant de la langue utilisée dans le contexte immédiat. (Niveau AA)
