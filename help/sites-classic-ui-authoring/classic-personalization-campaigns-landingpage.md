---
title: Pages de destination
description: La fonction Pages de destination permet d’importer rapidement et facilement les conceptions et les contenu directement dans une page AEM. Le code HTML et les ressources connexes préparés par un développeur ou une développeuse web pourront être importés, en intégralité ou partiellement.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 0f1014a7-b0ba-4455-b3a4-5023bcd4c5a1
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '3360'
ht-degree: 100%

---

# Pages de destination{#landing-pages}

La fonction Pages de destination permet d’importer rapidement et facilement les conceptions et les contenu directement dans une page AEM. Le code HTML et les ressources connexes préparés par un développeur web pourront être importés, en intégralité ou partiellement. Cette fonctionnalité est utile pour créer des pages de destination marketing qui ne sont actives que pendant une durée limitée et qui doivent être créées rapidement.

Cette page contient les informations suivantes :

* aspect des pages de destination dans AEM et composants disponibles ;
* méthode de création d’une page de destination et import d’un package de conception ;
* utilisation des pages de destination dans AEM ;
* configuration des pages de destination pour appareils mobiles.

La préparation du package de conception à importer est traitée dans la section [Extension et configuration de l’importateur de conception](/help/sites-administering/extending-the-design-importer-for-landingpages.md). L’intégration à Adobe Analytics est présentée dans la section [Intégration des pages de destination à Adobe Analytics.](/help/sites-administering/integrating-landing-pages-with-adobe-analytics.md)

>[!CAUTION]
>
>L’importateur de conception, utilisé pour importer des pages de destination, [a été abandonné avec AEM 6.5.](/help/release-notes/deprecated-removed-features.md#deprecated-features).

>[!CAUTION]
>
>Étant donné que l’importateur de conception doit pouvoir accéder à `/apps`, il ne fonctionnera pas dans les environnements cloud conteneurisés où `/apps` est immuable.

## Que sont les pages de destination ? {#what-are-landing-pages}

Les pages de destination sont des sites d’une ou de plusieurs pages qui sont le « point d’entrée » d’une diffusion marketing (un e-mail, des mots-clés/bannières, des médias sociaux, etc.). Une page de destination peut avoir plusieurs objectifs, mais tous ont un élément en commun : la personne doit accomplir une tâche, ce qui conditionne le succès de la page de destination.

La fonctionnalité Pages de destination d’AEM permet aux spécialistes marketing de collaborer avec les concepteurs et conceptrices web des agences ou des équipes créatives internes, afin de créer des conceptions de page qui peuvent être facilement importées dans AEM et qui restent modifiables par les spécialistes marketing. Par ailleurs, elles peuvent être publiées sous la même gouvernance que les autres sites optimisés par AEM.

Dans AEM, procédez comme suit pour créer des pages de destination :

1. Créez une page dans AEM qui contient la zone de travail des pages de destination. AEM est fourni avec un exemple nommé **Page d’importateur**.

1. [Préparez le code HTML et les ressources.](/help/sites-administering/extending-the-design-importer-for-landingpages.md)
1. Regroupez les ressources dans un fichier ZIP appelé « package de conception ».
1. Importez le package de conception sur la page de l’importateur.
1. Modifiez et publiez la page.

### Pages de destination pour postes de travail {#desktop-landing-pages}

Voici un exemple de page de destination dans AEM :

![chlimage_1-2](assets/chlimage_1-2.jpeg)

### Pages de destination pour mobiles {#mobile-landing-pages}

Une page de destination peut également avoir une version pour mobiles. Pour disposer d’une version mobile distincte de la page de destination, la conception de l’importation doit comporter deux fichiers HTML : *index.htm(l)* et *mobile.index.htm(l)*.

La procédure d’importation de ces pages de destination est identique à celle d’une page de destination normale ; la conception de page de destination est associée à un fichier HTML supplémentaire correspondant à la page de destination pour mobiles. Ce fichier HTML doit, lui aussi, disposer d’une balise `div` de canevas avec `id=cqcanvas`, comme c’est le cas pour la page de destination pour ordinateurs de bureau. De plus, il prend en charge tous les composants modifiables décrits pour la page de destination pour ordinateurs de bureau.

La page de destination pour mobiles est créée en tant que page enfant de la page de destination pour ordinateurs de bureau. Pour l’ouvrir, accédez à la page de destination dans Sites web et ouvrez la page enfant.

![chlimage_1-22](assets/chlimage_1-22.png)

>[!NOTE]
>
>La page de destination pour mobiles est supprimée/désactivée en même temp que la page de destination pour postes de travail correspondante.

## Composants de page de destination {#landing-page-components}

Pour rendre des parties HTML importées modifiables dans AEM, vous pouvez mapper directement le contenu HTML des pages de destination aux composants AEM. Par défaut, l’importateur de conception comprend les composants suivants :

* Texte, pour tout texte
* Titre, pour le contenu des balises H1-6
* Image, pour les images qui doivent être échangeables
* Appel à action :

   * Lien des clics publicitaires
   * Lien graphique

* Formulaire de piste CTA, pour capturer des informations sur l’utilisateur ou l’utilisatrice
* Système de paragraphe (Parsys), pour permettre l’ajout ou la conversion de composants

En outre, il est possible d’étendre cette fonctionnalité et de prendre en charge les composants personnalisés. Cette section décrit les composants en détail.

### Texte {#text}

Le composant Texte vous permet de saisir un bloc de texte à l’aide d’un éditeur WYSIWYG. Pour plus d’informations, consultez [Composant Texte](/help/sites-authoring/default-components.md#text) .

![chlimage_1-23](assets/chlimage_1-23.png)

Voici un exemple de composant Texte sur une page de destination :

![chlimage_1-24](assets/chlimage_1-24.png)

#### Titre {#title}

Le composant Titre vous permet d’afficher un titre et de configurer la taille (h1-6). Pour plus d’informations, consultez [Composant Titre](/help/sites-authoring/default-components.md#title).

![chlimage_1-25](assets/chlimage_1-25.png)

Voici un exemple de composant Titre sur une page de destination :

![chlimage_1-26](assets/chlimage_1-26.png)

#### Image {#image}

Le composant Image affiche une image que vous pouvez faire glisser à partir de l’outil de recherche de contenu ou sur laquelle vous pouvez cliquer pour la charger. Pour plus d’informations, consultez [Composant Image](/help/sites-authoring/default-components.md).

![chlimage_1-27](assets/chlimage_1-27.png)

Voici un exemple de composant Image sur une page de destination :

![chlimage_1-28](assets/chlimage_1-28.png)

#### Appel à l’action (CTA) {#call-to-action-cta}

Une conception de page de destination peut comporter plusieurs liens. Certains d’entre eux peuvent être conçus comme des « appels à l’action ».

L’appel à l’action (CTA) est utilisé pour inciter le visiteur ou la visiteuse à agir immédiatement sur la page de destination. En voici quelques exemples : « S’abonner maintenant », « Voir cette vidéo », « Durée limitée », etc.

* Lien de clics publicitaires : permet d’ajouter un lien texte qui, lorsqu’il est fait l’objet d’un clic, dirige le visiteur ou la visiteuse vers une URL cible.
* Lien graphique : permet d’ajouter une image qui, lorsqu’elle fait l’objet d’un clic, dirige le visiteur ou la visiteuse vers une URL cible.

Les deux composants CTA disposent d’options similaires. Le lien de clics publicitaires disposent d’autres options de texte enrichi. Les composants sont décrits en détail dans les paragraphes suivants.

#### Lien de clics publicitaires {#click-through-link}

Vous pouvez utiliser ce composant CTA pour ajouter un lien textuel sur la page de destination. Lorsqu’une personne clique sur ce lien, elle accède à l’URL cible spécifiée dans les propriétés du composant. Il fait partie du groupe « Appel à l’action ».

![chlimage_1-29](assets/chlimage_1-29.png)

**Libellé** Il s’agit du texte visible par les utilisateurs. Vous pouvez modifier la mise en forme à l’aide de l’éditeur de texte enrichi.

**Cible URL** Saisissez l’URI à laquelle les utilisateurs accéderont s’ils cliquent sur le texte. 

**Options de rendu** Décrit les options de rendu. Vous pouvez effectuer une sélection parmi les options suivantes :

* Charger la page dans une nouvelle fenêtre de navigateur
* Charger la page dans la fenêtre active
* Charger la page dans le cadre parent
* Annuler tous les cadres et charger la page dans une fenêtre du navigateur

**CSS** Dans l’onglet Style, saisissez le chemin d’accès à votre feuille de styles CSS.

**ID** Dans l’onglet Style, saisissez l’ID du composant afin de l’identifier de manière unique.

Voici un exemple de lien de clics publicitaires :

![chlimage_1-30](assets/chlimage_1-30.png)

#### Lien graphique {#graphical-link}

Vous pouvez utiliser ce composant CTA pour ajouter une image graphique avec un lien sur la page de destination. Il peut s’agir d’un simple bouton ou d’une image en arrière-plan. Lorsqu’une personne clique sur l’image, elle accède à l’URL cible spécifiée dans les propriétés du composant. Cela fait partie du groupe **Appel à l’action**.

![chlimage_1-31](assets/chlimage_1-31.png)

**Libellé** Il s’agit du texte présenté à l’utilisateur dans le diagramme. Vous pouvez modifier la mise en forme à l’aide de l’éditeur de texte enrichi.

**Cible URL** Saisissez l’URI à laquelle les utilisateurs accéderont s’ils cliquent sur l’image.

**Options de rendu** Décrit les options de rendu. Vous pouvez effectuer une sélection parmi les options suivantes :

* Charger la page dans une nouvelle fenêtre de navigateur
* Charger la page dans la fenêtre active
* Charger la page dans le cadre parent
* Annuler tous les cadres et charger la page dans une fenêtre du navigateur

**CSS** Dans l’onglet Style, saisissez le chemin d’accès à votre feuille de styles CSS.

**ID** Dans l’onglet Style, saisissez l’ID du composant afin de l’identifier de manière unique.

Voici un exemple de lien graphique :

![chlimage_1-32](assets/chlimage_1-32.png)

### Formulaire de prospect CTA (appel à l’action) {#call-to-action-cta-lead-form}

Le formulaire de piste est utilisé pour collecter des informations sur le profil d’un visiteur/prospect. Ces informations pourront être stockées et exploitées ultérieurement pour mener une campagne marketing efficace. Il s’agit généralement du titre, du nom, de l’adresse e-mail, de la date de naissance, de l’adresse, du centre d’intérêt, etc. Il fait partie du groupe **Formulaire de prospect CTA**.

Voici un exemple de formulaire de prospect CTA :

![chlimage_1-33](assets/chlimage_1-33.png)

Les formulaires de prospect CTA se composent de plusieurs composants différents :

* **Formulaire de prospect**
Le composant Formulaire de prospect définit le début et la fin d’un nouveau formulaire dans une page. D’autres composants peuvent être placés entre ces éléments, tels que « ID d’e-mail », « Prénom », etc.

* **Champs et éléments de formulaires**
Les champs et les éléments de formulaires peuvent inclure des zones textuelles, des cases d’option, des images, etc. L’utilisateur effectue souvent une action dans un champ de formulaire, comme saisir du texte. Consultez chaque élément de formulaires pour plus d’informations.

* **Composants Profil**
Les composants Profil sont associés aux profils des visiteurs utilisés pour la collaboration sociale et pour tout autre domaine où la personnalisation des visiteurs est requise.

Vous découvrez un exemple de formulaire ci-dessus. Il comprend le composant **Formulaire de prospect** (début et fin), avec les champs **Prénom** et **ID d’e-mail** utilisés comme données d’entrée et un champ **Envoyer**.

Les composants suivants sont disponibles à partir du Sidekick pour le formulaire de prospect CTA :

![chlimage_1-34](assets/chlimage_1-34.png)

#### Paramètres communs à de nombreux composants de formulaire de prospect {#settings-common-to-many-lead-form-components}

Bien que chacun des composants de formulaire de prospect ait un objectif différent, la plupart sont composés d’options et de paramètres similaires.

Lors de la configuration de l’un des composants de formulaire, les onglets suivants sont disponibles dans la boîte de dialogue :

* **Titre et texte**
Cet onglet vous invite à renseigner des informations de base, telles que le titre du composant et tout texte d’accompagnement. Le cas échéant, il vous permet également d’apporter d’autres informations essentielles ; par exemple, s’il s’agit d’un champ à sélection multiple ou encore les différents éléments pouvant être sélectionnés.

* **Valeurs initiales**
Permet d’indiquer une valeur par défaut.

* **Contraintes**
Permet d’indiquer si un champ est obligatoire et les contraintes qui lui sont appliquées (doit être numérique, par exemple).

* **Style**
Indique la taille et le style des champs.

>[!NOTE]
>
>Les champs affichés varient en fonction du composant individuel.
>
>Toutes les options ne sont pas disponibles pour tous les composants du formulaire de prospect. Voir Forms pour plus d’informations sur ces [paramètres communs](/help/sites-authoring/default-components.md#formsgroup).

#### Composants de formulaire de prospect {#lead-form-components}

La section suivante décrit les composants disponibles pour les formulaires de prospect CTA.

**À propos** Permet aux utilisateurs d’ajouter des informations de type « À propos ».

![chlimage_1-35](assets/chlimage_1-35.png)

**Champ d’adresse** Permet aux utilisateurs de saisir les informations d’adresse. Lorsque vous configurez ce composant, vous devez saisir le Nom de l’élément dans la boîte de dialogue. Le Nom de l’élément est le nom de l’élément de formulaire. Indique l’emplacement de stockage des données dans le référentiel.

![chlimage_1-36](assets/chlimage_1-36.png)

**Date de naissance** Les utilisateurs peuvent saisir leur date de naissance.

![chlimage_1-37](assets/chlimage_1-37.png)

**ID d’e-mail** Permet aux utilisateurs de saisir une adresse électronique (identification).

![chlimage_1-38](assets/chlimage_1-38.png)

**Prénom** Champ permettant aux utilisateurs de saisir leur prénom.

![chlimage_1-39](assets/chlimage_1-39.png)

**Genre** Les utilisateurs peuvent sélectionner leur genre dans une liste déroulante.

![chlimage_1-40](assets/chlimage_1-40.png)

**Nom** Les utilisateurs peuvent saisir leurs informations de nom.

![chlimage_1-41](assets/chlimage_1-41.png)

**Formulaire de prospect** Ajoutez ce composant afin d’ajouter un formulaire de prospect à votre page de destination. Un formulaire de prospect comprend automatiquement un champ Début du formulaire de prospect et un champ Fin de formulaire de prospect. Entre les deux, vous ajoutez les composants « Formulaire de prospect » décrits dans cette section.

![chlimage_1-42](assets/chlimage_1-42.png)

Le composant Formulaire de prospect définit le début et la fin d’un formulaire à l’aide des éléments **Début du formulaire** et **Fin de formulaire**. Le début et la fin sont toujours associés pour s’assurer que le formulaire est correctement défini.

Après avoir ajouté le formulaire de prospect, vous pouvez configurer le début ou la fin du formulaire en cliquant sur **Modifier** dans la barre correspondante.

**Début du formulaire de lead**

Deux onglets sont disponibles pour la configuration, **Formulaire** et **Avancé** :

![chlimage_1-43](assets/chlimage_1-43.png)

**Page de remerciement** Page à référencer pour remercier les visiteurs qui ont saisi des données. Si ce champ est laissé vide, le formulaire est réaffiché après la soumission.

**Démarrer le workflow** Détermine quel workflow est déclenché une fois le formulaire de prospect envoyé.

![chlimage_1-44](assets/chlimage_1-44.png)

**Options de publication** Les options de publication suivantes sont disponibles :

* Créer un prospect
* Service de messagerie : permet de créer une personne abonnée et de l’ajouter à la liste. Utilisez cette option si vous utilisez un fournisseur de services de messagerie comme ExactTarget.
* Service de messagerie : permet d’envoyer un message de répondeur automatique. Sélectionnez cette option si vous utilisez un fournisseur de services de messagerie comme ExactTarget.
* Service de messagerie : permet de désabonner l’utilisateur ou l’utilisatrice de la liste. Sélectionnez cette option si vous utilisez un fournisseur de services de messagerie comme ExactTarget.
* Désabonner l’utilisateur

**L’identifiant de formulaire** L’identifiant de formulaire d’un prospect l’identifie de façon unique. Utilisez cet identifiant si plusieurs formulaires figurent sur une seule page ; assurez-vous qu’ils présentent des identifiants différents.

**Chemin de chargement** Chemin d’accès aux propriétés de nœud, utilisé pour charger les valeurs prédéfinies dans les champs du formulaire de prospect.

Il s’agit d’un champ facultatif qui permet de spécifier le chemin à un nœud dans le référentiel. Lorsque ce nœud comporte des propriétés qui correspondent aux noms des champs, les champs adéquats du formulaire sont préchargés avec la valeur de ces propriétés. S’il n’existe aucune correspondance, le champ contient la valeur par défaut.

**Validation du client** Indique si la validation du client est obligatoire pour ce formulaire (la validation de serveur a toujours lieu). Ceci peut être réalisé en conjonction avec le composant Captcha de formulaires.

**Type de ressource de validation** Définit le type de ressource de validation si vous souhaitez valider la totalité du formulaire de prospect (au lieu de chaque champ).

Si vous validez le formulaire dans son intégralité, vous devez également inclure l’un des éléments suivants :

* Un script pour la validation du client
  ` /apps/<myApp>/form/<myValidation>/formclientvalidation.jsp`

* Un script pour la validation du côté serveur
  ` /apps/<myApp>/form/<myValidation>/formservervalidation.jsp`

**Configuration de l’action** La Configuration de l’action change en fonction des sélections effectuées dans Options de publication. Lorsque vous sélectionnez, par exemple, Créer un prospect, vous pouvez configurer la liste à laquelle le prospect est ajouté.

![chlimage_1-45](assets/chlimage_1-45.png)

* **Afficher le bouton Envoyer**
Indique si le bouton Envoyer doit être visible ou non.

* **Nom du bouton Envoyer**
Identifiant à spécifier si vous utilisez plusieurs boutons Envoyer dans un formulaire.

* **Titre du bouton Envoyer**
Nom qui apparaît sur le bouton, Envoyer ou Soumettre, par exemple.

* **Afficher le bouton Réinitialiser**
Cochez la case pour que le bouton Réinitialiser soit visible.

* **Titre du bouton Réinitialiser**
Nom qui apparaît sur le bouton Réinitialiser.

* **Description**
Informations qui s’affichent sous le bouton.

## Créer une page de destination {#creating-a-landing-page}

Lorsque vous créez une page de destination, vous devez effectuer trois étapes :

1. Créez une page d’importateur.
1. [Préparez le code HTML pour l’importation.](/help/sites-administering/extending-the-design-importer-for-landingpages.md)
1. Importez le package de conception.

### Utiliser l’importateur de conception {#use-of-the-design-importer}

Comme l’import de pages implique la préparation du code HTML, la vérification et le test des pages, l’import de pages de destination est conçue comme une tâche d’administration. En tant qu’administrateur, l’utilisateur effectuant l’importation a besoin d’autorisations de lecture, d’écriture, de création et de suppression sur `/apps`. Si l’utilisateur ne dispose pas de ces autorisations, l’importation échouera.

>[!NOTE]
>
>Étant donné que l’importateur de conception est conçu comme un outil d’administration ayant besoin d’autorisations de lecture, d’écriture, de création et de suppression sur `/apps`, Adobe déconseille de l’utiliser en production.

Adobe recommande d’utiliser l’importateur de conception sur une instance d’évaluation. Sur une instance d’évaluation, l’import peut être testé et validé par un développeur ou une développeuse qui est ensuite responsable du déploiement du code sur l’instance de production.

### Créer une page d’importateur {#creating-an-importer-page}

Avant de pouvoir importer votre conception de page de destination, vous devez créer une page d’importateur, par exemple sous une campagne. Le modèle Page d’importateur vous permet d’importer votre page de destination HTML complète. La page contient une zone de dépôt dans laquelle le package de conception de la page de destination peut être importé par glisser-déposer.

>[!NOTE]
>
>Par défaut, une page d’importateur ne peut être créée que sous les campagnes. Vous pouvez toutefois superposer ce modèle afin de créer une page de destination sous `/content/mysite`.

Pour créer une page de destination :

1. Accédez à la console **Sites web**.
1. Sélectionnez votre campagne dans le volet de gauche.
1. Cliquez sur **Nouveau** pour ouvrir la fenêtre **Créer une page**.
1. Sélectionnez le modèle **Page d’importateur**, ajoutez un titre et, éventuellement, un nom, puis cliquez sur **Créer**.

   ![chlimage_1-1-1](assets/chlimage_1-1-1.png)

   La nouvelle page de l’importateur s’affiche.

### Préparer le code HTML pour l’import {#preparing-the-html-for-import}

Avant d’importer le package de conception, le code HTML doit être préparé. Voir [Extension et configuration de l’import de conception](/help/sites-administering/extending-the-design-importer-for-landingpages.md) pour plus d’informations.

### Importer le package de conception {#importing-the-design-package}

Une fois la page d’importateur créée, vous pouvez y importer un package de conception. Vous trouverez des informations détaillées sur la création du package de conception et sa structure recommandée dans la section [Extension et configuration de l’import de conception](/help/sites-administering/extending-the-design-importer-for-landingpages.md).

En supposant que le package de conception soit prêt, les étapes suivantes décrivent comment importer le package de conception sur une page d’importateur.

1. Ouvrez la page d’importateur que vous avez [créée précédemment](#creatingablankcanvaspage).

   ![chlimage_1-46](assets/chlimage_1-46.png)

1. Faites glisser le package de conception et déposez-le dans la zone de dépôt. Notez que la flèche change de direction lorsque vous faites glisser un package dessus.
1. Après avoir effectué un glisser-déposer, la page de destination s’affiche à la place de la page d’importateur. La page de destination HTML a bien été importée.

   ![chlimage_1-2-1](assets/chlimage_1-2-1.png)

>[!NOTE]
>
>Lors de lʼimportation, le balisage est nettoyé pour des raisons de sécurité et afin dʼéviter lʼimportation et la publication d’un balisage non valide. Cela suppose que les balises HTML et que toutes les autres formes d’éléments tels que les SVG en ligne ou les composants web soient filtrées.

>[!NOTE]
>
>Si vous rencontrez des problèmes lors de l’import du package de conception, consultez [Résolutions des problèmes](/help/sites-administering/extending-the-design-importer-for-landingpages.md#troubleshooting).

## Utiliser les pages de destination {#working-with-landing-pages}

La conception et les ressources d’une page de destination sont généralement créées par un concepteur ou une conceptrice, éventuellement au sein d’une agence, avec des outils comme Adobe Photoshop ou Adobe Dreamweaver. Une fois la conception terminée, le concepteur envoie, au service marketing, un fichier compressé contenant tous les éléments. Le contact marketing est alors chargé de déposer le fichier zip dans AEM et de publier le contenu.

En outre, le concepteur ou la conceptrice peut avoir à apporter des modifications à la page de destination après son import en modifiant ou en supprimant du contenu et en configurant les composants d’appel à l’action. Enfin, le spécialiste marketing souhaite afficher un aperçu de la page de destination, puis activer la campagne pour s’assurer que la page de destination est publiée.

Cette section décrit les tâches suivantes :

* Supprimer une page de destination
* Télécharger le package de conception
* Afficher les informations d’import
* Réinitialiser une page de destination
* [Configuration des composants CTA et ajout de contenu à la page](#call-to-action-cta)
* Prévisualiser la page de destination
* Activer/publier une page de destination

Lorsque vous importez le package de conception, les options **Effacer la conception** et **Télécharger le fichier compressé importé** sont disponibles dans le menu des paramètres de la page :

![chlimage_1-3-1](assets/chlimage_1-3-1.png)

### Télécharger le package de conception importé {#downloading-the-imported-design-package}

Le téléchargement du fichier zip permet d&#39;enregistrer le fichier zip importé avec une page de destination spécifique. Les modifications apportées à une page ne sont pas ajoutées au fichier compressé.

Pour télécharger le package de conception importé, cliquez sur **Télécharger le fichier compressé** dans la barre d’outils de la page de destination.

### Afficher les informations d’import {#viewing-import-information}

Vous pouvez à tout moment afficher des informations sur le dernier import en cliquant sur le point d’exclamation bleu en haut de la page de destination dans l’interface utilisateur classique.

![chlimage_1-47](assets/chlimage_1-47.png)

Si le package de conception importé présente certains problèmes, par exemple s’il fait référence à des images/scripts qui n’existent pas dans le package, ou autre, l’importateur de conception affiche ces problèmes sous la forme d’une liste. Pour afficher la liste des problèmes, dans l’interface utilisateur classique, cliquez sur le lien Problèmes dans la barre d’outils de la page de destination. Sur l’image suivante, la fenêtre Problèmes d’importation s’affiche lorsque vous cliquez sur **Problèmes**.

![chlimage_1-3](assets/chlimage_1-3.jpeg)

### Réinitialisation d’une page de destination {#resetting-a-landing-page}

Si vous souhaitez réimporter votre module de conception de la page de destination après y avoir apporté des modifications, vous pouvez « effacer » la page de destination en cliquant sur **Effacer** dans la partie supérieure de la page de destination dans l’interface utilisateur classique ou en cliquant sur Effacer dans le menu Paramètres de l’interface utilisateur optimisée pour les écrans tactiles. La page de destination importée est alors supprimée et une page d’importateur vierge est créée.

Lors de l’effacement de la page de destination, vous pouvez supprimer les modifications du contenu. Si vous cliquez sur **Non**, les modifications du contenu sont conservées. En d’autres termes, la structure sous-jacente de `jcr:content/importer` est conservée, et seuls le composant de page d’importateur et les ressources situées dans `etc/design` sont supprimés. En revanche, si vous cliquez sur **Oui**, `jcr:content/importer` est également supprimé.

>[!NOTE]
>
>Si vous décidez de supprimer les modifications du contenu, toutes les modifications que vous avez effectuées sur la page de destination importée, ainsi que toutes les propriétés de page, seront perdues lorsque vous cliquerez sur **Effacer**.

### Modifier et ajouter des composants sur une page de destination {#modifying-and-adding-components-on-a-landing-page}

Pour modifier des composants sur la page de destination, double-cliquez dessus pour les ouvrir et les modifier comme vous le feriez pour tout autre composant.

Pour ajouter des composants sur la page de destination, faites-les glisser et déposez-les sur la page de destination (depuis le sidekick dans l’interface utilisateur classique ou depuis le volet Composants de l’interface utilisateur optimisée pour les écrans tactiles), puis modifiez-les selon les besoins.

>[!NOTE]
>
>Si un composant de la page de destination ne peut pas être modifié, vous devez réimporter le fichier zip après [modification du fichier HTML.](/help/sites-administering/extending-the-design-importer-for-landingpages.md) Cela signifie que pendant l’import, les parties non modifiables n’ont pas été converties en composants AEM.

### Supprimer une page de destination {#deleting-a-landing-page}

La suppression d’une page de destination fonctionne comme la suppression d’une page AEM normale.

La seule exception est que lorsque vous supprimez une page de destination pour ordinateurs de bureau, cela supprime également la page de destination correspondante pour mobiles (si celle-ci existe), mais l’inverse ne se produit pas.

### Publier une page de destination {#publishing-a-landing-page}

Vous pouvez publier la page de destination et toutes ses dépendances comme vous publieriez une page normale.

>[!NOTE]
>
>La publication de la page de destination pour postes de travail publie également sa version mobile correspondante (le cas échéant). En revanche, la publication d’une page de destination pour mobiles ne publie pas la version pour postes de travail.
