---
title: Présentation de la création de formulaires adaptatifs
seo-title: Introduction to authoring adaptive forms
description: AEM Forms fournit une interface conviviale mais puissante pour la création de formulaires adaptatifs. Les nombreux composants et outils proposés vous permettent de créer des formulaires.
seo-description: AEM Forms provide easy-to-use yet powerful interface for authoring adaptive forms. It provides a host of components and tools that you can use to build forms.
uuid: 3b150507-41b9-47c2-a94c-f85b903b2274
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction, author
discoiquuid: ba70921e-db7e-43f6-902c-1065d3b13aef
docset: aem65
feature: Adaptive Forms
exl-id: 935b734c-6fb1-45e8-8515-e98c8b85286c
source-git-commit: 1683338f02d01d5d9843368955fa42f309718f26
workflow-type: tm+mt
source-wordcount: '3161'
ht-degree: 62%

---

# Présentation de la création de formulaires adaptatifs {#introduction-to-authoring-adaptive-forms}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/introduction-forms-authoring.html) |
| AEM 6.5 | Cet article |


## Présentation {#overview}

Les formulaires adaptatifs vous permettent de créer des formulaires attrayants, réactifs, dynamiques et adaptatifs. AEM Forms fournit une interface utilisateur intuitive et des composants prêts à l’emploi pour la création et l’utilisation de formulaires adaptatifs. Vous pouvez choisir de créer un formulaire adaptatif basé sur un modèle ou un schéma de formulaire ou sans modèle de formulaire. Il est important de choisir avec soin le modèle de formulaire qui convient non seulement à vos besoins, mais qui étend également vos investissements et vos ressources d’infrastructure existantes. Vous pouvez choisir parmi les options suivantes pour créer un formulaire adaptatif :

* **Utilisation d’un modèle de données de formulaire**
  L’[intégration de données](../../forms/using/data-integration.md) vous permet d’intégrer des entités et des services provenant de sources de données disparates dans un modèle de données de formulaire que vous pouvez utiliser pour créer des formulaires adaptatifs. Choisissez le modèle de données de formulaire si le formulaire adaptatif que vous créez implique l’extraction et l’écriture de données depuis et vers plusieurs sources de données.

* **Utilisation d’un modèle de formulaire XDP**
Il s’agit d’un modèle de formulaire idéal si vous investissez dans des formulaires XFA ou XDP. Il fournit un moyen direct de convertir vos formulaires basés sur XFA en formulaires adaptatifs. Toutes les règles XFA existantes sont conservées dans les formulaires adaptatifs associés. Les formulaires adaptatifs obtenus prennent en charge les éléments XFA, tels que les validations, les événements, les propriétés et les modèles.

* **Utilisation d’une définition de schéma XML (XSD) ou d’un schéma JSON**
Les schémas XML et JSON représentent la structure dans laquelle les données sont produites ou consommées par le système principal de votre entreprise. Vous pouvez associer le schéma à un formulaire adaptatif et utiliser ses éléments pour ajouter du contenu dynamique à un formulaire adaptatif. Les éléments du schéma peuvent être utilisés dans l’onglet Objets du modèle de données de l’explorateur de contenu lors de la création de formulaires adaptatifs.

* **Sans ou aucun modèle de formulaire** Les formulaires adaptatifs créés avec cette option n’utilisent aucun modèle de formulaire. Les données XML générées à partir de ce type de formulaire présentent une structure plate avec des champs et des valeurs correspondantes.

Pour plus d’informations sur la création d’un formulaire adaptatif, voir [Création d’un formulaire adaptatif](../../forms/using/creating-adaptive-form.md).

## Interface utilisateur de création de formulaires adaptatifs {#adaptive-form-authoring-ui}

L’interface utilisateur optimisée pour les écrans tactiles pour la création de formulaires adaptatifs est intuitive et fournit les éléments suivants :

* Fonctionnalité glisser-déposer
* Composants standard de formulaire
* Référentiel intégré de ressources

Lorsque vous créez un formulaire adaptatif ou en modifiez un existant, vous utilisez les éléments suivants de l’interface utilisateur :

* [Barre latérale](#sidebar)
* [Barre d’outils de la page](#page-toolbar)
* [Barre d’outils de composants](#component-toolbar)
* [Page de formulaires adaptatifs](#af-page)

![Interface de création de formulaires adaptatifs](assets/formeditor.png)

**A.** Barre latérale **B.** Page de barre d’outils **C.** Page de formulaire adaptatif

### Barre latérale {#sidebar}

La barre latérale vous permet de

* Voir le contenu du formulaire tel que les panneaux, les composants, les champs et la mise en page.
* Modifier les propriétés du composant.
* Rechercher, afficher et utiliser des ressources dans votre référentiel de gestion des ressources numériques (DAM) AEM.
* Ajouter des composants dans le formulaire.

![Barre latérale](assets/sidebar-comps.png)

**A.** Explorateur de contenu **B.** Explorateur de propriétés **C.** Explorateur de ressources **D.** Explorateur de composants

<!--Click to enlarge

](assets/sidebar-comps-1.png) -->

La barre latérale comprend les explorateurs suivants :

* **Explorateur de contenu** Dans l’explorateur de contenu, vous pouvez voir 

   * **Objets de formulaire**
Affiche la hiérarchie des objets du formulaire. L’auteur peut accéder au composant spécifique du formulaire en appuyant sur cet élément dans l’arborescence de l’objet de formulaire. L’auteur peut alors rechercher des objets et les réorganiser depuis l’arborescence.

   * **Objets de modèle de données**
Permet de voir la hiérarchie des modèles de formulaire.
Il vous permet de faire glisser des éléments du modèle de formulaire sur le formulaire adaptatif. Les éléments ajoutés sont automatiquement convertis en composants de formulaire tout en conservant leurs propriétés d’origine. Vous pouvez voir des objets de modèle de données lorsque votre formulaire utilise un schéma XML, un schéma JSON ou un modèle XDP.

* **Explorateur de propriétés**

  Permet de modifier les propriétés d’un composant. Les propriétés affichées varient en fonction d’un composant. Pour voir les propriétés du conteneur de formulaires adaptatifs :

  Sélectionnez un composant, puis appuyez sur ![field-level](assets/field-level.png) > **[!UICONTROL Conteneur de formulaires adaptatifs]** et enfin sur ![cmppr](assets/cmppr.png).

* **Explorateur de ressources**

  Isole différents types de contenu, tels que des images, des documents, des pages, des séquences vidéo, etc.

* **Explorateur de composants**

  Comprend des composants que vous pouvez utiliser pour créer un formulaire adaptatif. Vous pouvez faire glisser des composants sur le formulaire adaptatif afin d’ajouter des éléments de formulaire, puis configurer les éléments ajoutés conformément aux exigences. Le tableau ci-dessous décrit les composants répertoriés dans l’explorateur de composants.

<table>
 <tbody>
  <tr>
   <th><strong>Composant</strong></th>
   <th><strong>Fonctionnalité</strong></th>
  </tr>
  <tr>
   <td>Bloc Adobe Sign</td>
   <td>Ajoute un bloc de texte contenant des espaces réservés pour le remplissage des champs lors de la signature à l’aide d’Adobe Sign.</td>
  </tr>
  <tr>
   <td>Bouton</td>
   <td>Ajoute un bouton que vous pouvez configurer pour exécuter des actions telles que Enregistrer, Réinitialiser, Passer au suivant, Passer au précédent, etc.</td>
  </tr>
  <tr>
   <td>Captcha</td>
   <td>Ajoutez une validation CAPTCHA en utilisant le service reCAPTCHA de Google. Pour plus d’informations, voir <a href="../../forms/using/captcha-adaptive-forms.md" target="_blank">Utilisation de CAPTCHA dans les formulaires adaptatifs</a>.</td>
  </tr>
  <tr>
   <td>Graphique</td>
   <td>Ajoute un graphique que vous pouvez utiliser dans les formulaires et documents adaptatifs pour la représentation visuelle des données bidimensionnelles dans les panneaux et les lignes de tableau répétables.</td>
  </tr>
  <tr>
   <td>Case à cocher</td>
   <td>Ajoute une case à cocher.</td>
  </tr>
  <tr>
   <td>Champ de saisie de date</td>
   <td>Utilisez le composant Champ de saisie de date dans votre formulaire pour permettre aux clients de remplir séparément dans trois cases le jour, le mois et l’année. Vous pouvez personnaliser l’aspect du composant et modifier le format de date. Par exemple, vous pouvez laisser vos clients saisir des dates au format MM/JJ/AAAA ou JJ/MM/AAAA.</td>
  </tr>
  <tr>
   <td>Sélecteur de date</td>
   <td>Ajoute un champ de calendrier pour sélectionner une date.</td>
  </tr>
  <tr>
   <td>Fragment de document</td>
   <td>Permet d’ajouter des composants réutilisables d’une correspondance.</td>
  </tr>
  <tr>
   <td>Groupe de fragments de document</td>
   <td>Vous permet d’ajouter un groupe de fragments de document associés que vous pouvez utiliser dans un modèle de lettre en tant qu’unité unique.</td>
  </tr>
  <tr>
   <td>Liste déroulante</td>
   <td>Ajoute une liste déroulante, à sélection simple ou multiple.</td>
  </tr>
  <tr>
   <td>E-mail</td>
   <td><p>Ajoute un champ pour capturer l’adresse électronique. Par défaut, le composant Email valide les adresses email à l’aide de l’expression régulière suivante.</p> <p><code>^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:.[a-zA-Z0-9-]+)*$</code></p> </td>
  </tr>
  <tr>
   <td>Pièce jointe</td>
   <td><p>Ajoute un bouton qui permet aux utilisateurs de rechercher et de joindre des documents annexes au formulaire. Vous pouvez joindre plusieurs fichiers à un composant de pièce jointe. Vous pouvez également spécifier les commandes **[!UICONTROL Taille maximale du fichier]** et **[!UICONTROL Types de fichiers pris en charge]** pour les pièces jointes dans l’explorateur de propriétés du composant. </p> <p><strong> Remarque : </strong><ul> <li> Le composant ne prend pas en charge la pièce jointe de fichiers dont le nom commence par des caractères (.), contient les caractères \ / : * ? " &lt; &gt; | ; % $, ou contenant des noms de fichier spéciaux réservés au système d’exploitation Windows comme null, prn, con, lpt ou com. </li> <li> Pour joindre plusieurs fichiers à un composant de pièce jointe ouvert dans le navigateur Safari Apple, sélectionnez-les et joignez-les un par un. Vous ne pouvez pas sélectionner et joindre plusieurs fichiers à la fois.</li> <li>Le composant Pièce jointe prend en charge un ensemble prédéfini de formats de fichiers dans des formulaires adaptatifs activés pour Adobe Sign. Pour plus d’informations, voir <a href="https://helpx.adobe.com/fr/document-cloud/help/supported-file-formats-fill-sign.html#main-pars_text">Formats de fichiers pris en charge</a>. </li></ul></p> </td>
  </tr>
  <tr>
   <td>Liste des pièces jointes</td>
   <td>Ajoute un champ qui répertorie toutes les pièces jointes téléchargées à l’aide du composant Pièce jointe .</td>
  </tr>
  <tr>
   <td>En-tête<br /> </td>
   <td>Ajoute un en-tête qui contient habituellement le logo d’une société, le titre du formulaire et le résumé.<br /> </td>
  </tr>
  <tr>
   <td>Pied de page</td>
   <td>Ajoute le pied de page qui contient généralement des informations de copyright, ainsi que des liens vers d’autres pages. </td>
  </tr>
  <tr>
   <td>Image</td>
   <td>Vous permet d’insérer une image.</td>
  </tr>
  <tr>
   <td>Choix d’image</td>
   <td>Permet à vos clients de sélectionner une image pour fournir des informations. Vous pouvez utiliser ces informations pour fournir des services personnalisés à vos clients.</td>
  </tr>
  <tr>
   <td>Bouton Suivant</td>
   <td>Ajoute un bouton permettant d’accéder au panneau suivant d’un formulaire.</td>
  </tr>
  <tr>
   <td>Zone numérique</td>
   <td>Ajoute un champ destiné à la saisie de valeurs numériques.</td>
  </tr>
  <tr>
   <td>Procédure pas à pas numérique</td>
   <td>Utilisez la procédure pas à pas numérique pour permettre à vos clients d’indiquer une valeur numérique, qu’ils peuvent augmenter ou diminuer en fonction d’une étape prédéfinie.</td>
  </tr>
  <tr>
   <td>Panneau</td>
   <td><p>Ajoute un panneau ou un sous-panneau.</p> <p>Vous pouvez également ajouter un composant de panneau à partir de la barre d’outils du panneau parent à l’aide de la propriété <span class="uicontrol">Ajouter un panneau enfant</code> button. De même, vous pouvez ajouter une barre d’outils spécifique au panneau à l’aide de la fonction <span class="uicontrol">Barre d’outils Ajouter un panneau</code> button. Vous pouvez configurer la position de la barre d’outils du panneau à l’aide de la boîte de dialogue Modifier le panneau.</p> </td>
  </tr>
  <tr>
   <td>Zone de mot de passe</td>
   <td>Ajoute un champ destiné à la saisie d’un mot de passe.</td>
  </tr>
  <tr>
   <td>Bouton Précédent</td>
   <td>Ajoute un bouton permettant de revenir à la page ou au panneau précédents.</td>
  </tr>
  <tr>
   <td>Bouton Radio</td>
   <td>Ajoute des boutons radio.</td>
  </tr>
  <tr>
   <td>Bouton de réinitialisation</td>
   <td>Ajoute un bouton pour réinitialiser les champs de formulaire.</td>
  </tr>
  <tr>
   <td>Bouton Enregistrer</td>
   <td>Ajoute un bouton permettant d’enregistrer les données de formulaire.</td>
  </tr>
  <tr>
   <td>Signature tactile</td>
   <td>Ajoute un champ destiné à la saisie de signatures tactiles.</td>
  </tr>
  <tr>
   <td>Séparateur</td>
   <td>Active la ségrégation visuelle des panneaux dans le formulaire.</td>
  </tr>
  <tr>
   <td>Étape de signature</td>
   <td>Affiche les informations fournies dans le formulaire et les champs de signature permettant à l’utilisateur de vérifier et de signer le formulaire.</td>
  </tr>
  <tr>
   <td>Texte</td>
   <td>Permet de spécifier du texte statique.</td>
  </tr>
  <tr>
   <td>Bouton Envoyer</td>
   <td>Ajoute un bouton Envoyer pour envoyer le formulaire à l’action d’envoi configurée.</td>
  </tr>
  <tr>
   <td>Étape de résumé</td>
   <td>Soumet le formulaire et affiche le texte récapitulatif spécifié par les auteurs après la soumission du formulaire. </td>
  </tr>
  <tr>
   <td>Basculer</td>
   <td>Ajoute un commutateur qui exécute une action de basculement ou d’activation/désactivation. Vous ne pouvez pas ajouter plus de deux options dans le composant Basculer. Un bouton ne peut avoir que deux valeurs : Activé ou Désactivé, obligatoire ne s’applique pas. Au moins une valeur est enregistrée, quelle que soit la saisie utilisateur. <br /> </td>
  </tr>
  <tr>
   <td>Tableau</td>
   <td>Ajoute un tableau qui permet de classer les données par lignes et par colonnes. </td>
  </tr>
  <tr>
   <td>Téléphone</td>
   <td><p>Ajoute un champ pour capturer le numéro de téléphone. Le composant Téléphone permet aux auteurs de configurer l’un des types de numéros de téléphone suivants. Chaque type est associé à une expression régulière par défaut pour la validation.</p>
    <ul>
     <li>Le type International est validé par <code>^[+][0-9]{0,14}$</code>.</li>
     <li>Le type USPhoneNumber est validé par <code>{'+1 ('999') '999-9999}</code>.</li>
     <li>Le type UKPhoneNumber est validé par <code>text{'+'99 999 999 9999}</code>.</li>
     <li>Type Personnalisé ne fournit pas de modèle de validation par défaut. Il prend la valeur du dernier type de numéro de téléphone sélectionné. Vous pouvez également spécifier votre propre modèle de validation personnalisé.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Termes et conditions<br /> </td>
   <td>Ajoute un champ que les auteurs peuvent utiliser pour spécifier les conditions générales que les utilisateurs doivent consulter avant de remplir le formulaire.</td>
  </tr>
  <tr>
   <td>Zone de texte </td>
   <td><p>Ajoute une zone de texte dans laquelle un utilisateur peut spécifier les informations requises. </p> <p>Par défaut, le composant Zone de texte accepte uniquement du texte brut. Vous pouvez activer un composant de zone de texte afin de permettre la prise en charge du texte brut. Un composant de texte enrichi fournit des options permettant d’ajouter des en-têtes, de modifier les styles de caractères (gras, italique, soulignement des caractères), de créer des listes ordonnées et non ordonnées, de modifier l’arrière-plan du texte et la couleur du texte, ainsi que d’ajouter des liens hypertexte. Pour activer le texte enrichi pour une zone de texte, activez l’option <strong>Autoriser le texte enrichi</strong> dans les propriétés du composant.</p> </td>
  </tr>
  <tr>
   <td>Titre</td>
   <td>Spécifie un titre pour le formulaire adaptatif.</td>
  </tr>
  <tr>
   <td>Étape de vérification</td>
   <td><p>Ajoute un espace réservé pour afficher le formulaire rempli à des fins de vérification par l’utilisateur.</p> <p><strong>Remarque</strong> : le formulaire adaptatif contenant le composant Vérifier ne prend pas en charge les utilisateurs anonymes. En outre, il n’est pas recommandé d’utiliser le composant Vérifier dans un fragment de formulaire adaptatif.</p> </td>
  </tr>
 </tbody>
</table>

#### Bonnes pratiques pour l’utilisation des composants {#best-practices}

Voici quelques bonnes pratiques et points clés à retenir lorsque vous utilisez des composants de formulaire adaptatif :

* Chaque composant est associé à des propriétés qui contrôlent son apparence et ses fonctionnalités. Pour configurer les propriétés d’un composant, appuyez sur celui-ci et sélectionnez ![cmppr](assets/cmppr.png) pour ouvrir les propriétés du composant dans l’explorateur de propriétés.
* Un composant est identifié par son nom d’élément. Lorsque vous appuyez sur ![cmppr](assets/cmppr.png), vous pouvez changer le nom du composant en modifiant la valeur du champ **[!UICONTROL Nom de l’élément]** dans l’explorateur de propriétés. Le champ Nom de l’élément accepte uniquement les lettres, les chiffres, les tirets (-) et les traits de soulignement (_). Les autres caractères spéciaux ne sont pas autorisés et le nom de l’élément doit commencer par une lettre.

* Vous pouvez modifier la propriété de titre d’un composant de formulaire adaptatif en ligne dans l’éditeur de formulaire sans ouvrir le navigateur de propriétés tant que le titre est visible sur le formulaire. Pour ce faire :

   1. Appuyez pour sélectionner un composant qui a une propriété **[!UICONTROL Titre]** et dont la propriété **[!UICONTROL Masquer le titre]** est désactivée.

   1. Appuyez sur ![aem_6_3_edit](assets/aem_6_3_edit.png) pour rendre le titre modifiable.

   1. Modifiez le titre et appuyez sur la touche Retour ou appuyez n’importe où en dehors du composant pour enregistrer les modifications. Appuyez sur la touche Échap pour annuler les modifications.

* Certains composants de formulaire adaptatifs, tels que Courrier électronique et Téléphone, incluent des modèles de validation prêts à l’emploi. Toutefois, vous pouvez spécifier une validation personnalisée en mettant à jour le champ **[!UICONTROL Modèle de validation]** sous l’accordéon Modèles dans les propriétés du composant. Voir les descriptions des composants dans le tableau ci-dessus pour plus d’informations sur les validations par défaut.

* Les champs de formulaires adaptatifs, tels que la zone numérique et le courrier électronique, peuvent être configurés pour inclure des types d’entrée HTML5 spécialisés. Lorsque ces champs sont actifs sur les appareils mobiles et les tablettes, le clavier affiche un alphabet, des chiffres et des caractères spécifiques qui sont généralement utilisés pour saisir des informations dans les champs. Cela permet aux utilisateurs de saisir les informations rapidement sans avoir à basculer entre les jeux de caractères sur le clavier. Pour activer une entrée spécifique pour un composant, cochez la case **[!UICONTROL Utiliser un numéro de type HTML]** dans ses propriétés de composant.

* Vous pouvez activer un composant de zone de texte afin de permettre la prise en charge du texte brut. Pour activer le texte enrichi pour une zone de texte, activez la case à cocher **[!UICONTROL Autoriser le texte enrichi]** dans les propriétés du composant.

* Vous pouvez activer les composants Zone de texte, Adresse électronique et Téléphone pour remplir automatiquement les champs tels que le nom, l’adresse, la carte de crédit, le téléphone et l’adresse électronique à partir des informations stockées dans les paramètres de remplissage automatique du navigateur. Pour activer cette fonctionnalité, sélectionnez **[!UICONTROL Activer le remplissage automatique]** dans les propriétés du composant et sélectionnez un **[!UICONTROL attribut de remplissage automatique]**. Lorsqu’un utilisateur remplit un formulaire adaptatif, les valeurs sont proposées à partir du profil de remplissage automatique dans le navigateur ou en fonction des valeurs précédemment renseignées par l’utilisateur. Notez que le remplissage automatique fonctionne si les paramètres de remplissage automatique dans le navigateur de l’utilisateur sont activés.

* Spécifiez des valeurs pour les éléments Bouton radio et Case à cocher au format `{value}={text}` dans les propriétés du composant.
* Par défaut, le composant Pièce jointe permet à un utilisateur de joindre un seul fichier. Cependant, vous pouvez configurer les propriétés du composant pour prendre en charge plusieurs pièces jointes. En outre, si un utilisateur joint plusieurs fichiers avec le même nom de fichier, les pièces jointes peuvent entraîner des problèmes. Par conséquent, il est recommandé d’associer un identifiant unique pour chaque pièce jointe envoyée lors de l’envoi du formulaire. Pour ce faire :

   1. Sur votre serveur AEM Forms, accédez à **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console Web]**.
   1. Recherchez **[!UICONTROL Service de configuration de formulaires adaptatifs]** et appuyez dessus.
   1. Dans la boîte de dialogue Service de configuration de formulaires adaptatifs, activez l’option **[!UICONTROL Rendre les noms de fichier uniques]**. Par défaut, elle est désactivée.

* Pour permettre aux utilisateurs de joindre un PDF à l’aide du navigateur Safari, assurez-vous que **application/pdf** est ajouté à la propriété Types de fichiers pris en charge du composant Pièce jointe . Les formulaires adaptatifs créés avec la version précédente d’AEM Forms peuvent contenir **.pdf** au lieu de **application/pdf** dans la propriété Types de fichiers pris en charge.

Pour connaître les bonnes pratiques concernant les formulaires adaptatifs, voir [Bonnes pratiques pour l’utilisation des formulaires adaptatifs](/help/forms/using/adaptive-forms-best-practices.md).

>[!NOTE]
>
>Les composants de formulaire adaptatif ne prennent pas en charge les langues de droite à gauche (RTL). comme l’hébreu.

### Barre d’outils Page {#page-toolbar}

La barre d’outils de la page supérieure propose des options permettant de prévisualiser le formulaire, de modifier ses propriétés et de modifier sa mise en page. Vous pouvez prévisualiser le formulaire lors de sa création et apporter des modifications en conséquence. Dans la barre d’outils de la page, vous voyez :

* **Activer/désactiver le panneau latéral** ![toggle-side-panel](assets/toggle-side-panel.png) : affiche ou masque la barre latérale.

* **Informations sur la page** ![theme-options](assets/theme-options.png) : affiche les propriétés de la page, permet de publier/d’annuler la publication d’un formulaire, de lancer un processus de formulaire et d’ouvrir le formulaire dans une IU classique.

* **Émulateur** ![ruler](assets/ruler.png) : simule l’aspect de votre formulaire pour différentes tailles d’affichage, selon les tablettes et les téléphones, par exemple.

* **Modifier** : permet de sélectionner d’autres modes comme : **[!UICONTROL Modifier]**, **[!UICONTROL Style]**, **[!UICONTROL Développeur]** et **[!UICONTROL Conception]**.

   * **Modifier** : permet de modifier les propriétés du formulaire et de ses composants. Exemple : l’ajout d’un composant, le dépôt d’une image et l’indication des champs obligatoires.
   * **Style** : définit l’aspect des composants de votre formulaire. Par exemple, en mode Style, vous pouvez sélectionner un panneau et définir sa couleur d’arrière-plan.

   * **Développeur** : permet à un développeur de :

      * Découvrez les formulaires composés.
      * Déboguer en temps réel afin de mieux résoudre les problèmes.

   * **Conception**. Permet d’activer ou de désactiver les composants personnalisés ou les composants prêts à l’emploi qui ne sont pas répertoriés dans la barre latérale.

* **Aperçu** : permet de prévisualiser le formulaire avant de le publier.

### Barre d’outils de composants {#component-toolbar}

![Barre d’outils de composants de l’interface utilisateur tactile](assets/component-toolbar.png)

Lorsque vous sélectionnez un composant, une barre d’outils s’affiche, vous permettant de l’utiliser. Vous avez la possibilité de couper, coller, déplacer et spécifier les propriétés des composants. Vous avez le choix entre :

A. **Configurer** : lorsque vous appuyez sur **[!UICONTROL Configurer]**, les propriétés du composant sont visibles dans la barre latérale. La configuration de ces propriétés vous permet de personnaliser l’expérience de capture de données. Vous pouvez modifier le nom de l’élément du composant, spécifier le texte du libellé dans le champ Titre du composant. Le nom de l’élément vous permet de capturer les valeurs saisies par les utilisateurs à l’aide du composant. Dans les propriétés du composant, vous spécifiez le comportement du composant et gérez les entrées utilisateur. Configurez les propriétés dans la barre latérale pour capturer les données utilisateur et les utiliser pour un traitement ultérieur. Les propriétés du conteneur de formulaires adaptatifs permettent de spécifier des bibliothèques clients, des mises en page, des thèmes, des documents d’enregistrement, des paramètres d’enregistrement, des paramètres d’envoi et des paramètres de métadonnées.

B. **Copier** : permet de copier un composant et le coller ailleurs dans le formulaire. Lorsque vous collez un composant, ce dernier obtient un nouveau nom d’élément mais conserve les propriétés du composant copié.

C.**Couper** : Permet de déplacer un composant d’un endroit à un autre dans le formulaire adaptatif.

D. **Supprimer** : permet de supprimer le composant du formulaire.

E. **Insérer** : permet d’insérer un composant au-dessus du composant sélectionné.

F. **Coller** : permet de coller du composant coupé ou copié à l’aide des options décrites ci-dessus.

G. **Éditeur de règles** : permet d’ouvrir l’éditeur de règles. Pour plus d’informations, voir [Éditeur de règles](../../forms/using/rule-editor.md).

H. **Groupe** : permet de sélectionner plusieurs composants permettant de couper, copier ou coller plusieurs composants ensemble.

I. **Parent** : permet de sélectionner le parent d’un composant. Par exemple, un champ de texte se trouve dans une sous-section, qui réside dans une section. La section se trouve dans le panneau racine du guide et le conteneur du formulaire adaptatif est le parent d’un panneau racine de guide. Pour chaque composant s’affichent toutes les options avec la hiérarchie triée de bas en haut.

Par exemple, si vous tapez **[!UICONTROL Parent]** pour une zone de texte, vous pouvez voir les éléments suivants :

* Sous-section
* Section
* guideRootPanel
* Conteneur de formulaires adaptatifs

J. **Autres**: Fournit d’autres options pour utiliser le composant sélectionné.

* Afficher l’expression SOM
* Enregistrement d’un panneau en tant que fragment (pour les panneaux uniquement)
* Ajouter un panneau enfant (pour les panneaux uniquement)
* Barre d’outils Ajouter un panneau (pour les panneaux uniquement)
* Remplacer (pas pour les panneaux)

### Page de formulaires adaptatifs {#af-page}

La page de formulaire adaptatif est le formulaire réel. Elle est identique à toute autre page de gestion de contenu Web modélisée en tant que composant de gestion de contenu Web `cq:Page`. L’illustration suivante présente la structure de contenu d’un formulaire adaptatif standard.

![Structure de contenu d’une page de gestion de contenu Web de formulaires adaptatifs](assets/afstructure.png)

La structure de contenu contient généralement les composants principaux ci-dessous :

* **guideContainer** : racine d’un formulaire adaptatif, indiquée sous la forme **[!UICONTROL Début du formulaire adaptatif]** dans l’interface utilisateur du formulaire. Dans ce composant, vous pouvez spécifier les éléments suivants :

   * *Disposition mobile du formulaire adaptatif*: Définit l’aspect du formulaire sur les périphériques mobiles.
   * *Page de remerciement*: Définit la page vers laquelle l’utilisateur est redirigé après l’envoi du formulaire.
   * *Action Envoyer*: Définit le mode de traitement du formulaire sur le serveur une fois que l’utilisateur l’a envoyé.
   * *Style*: Spécifie le chemin d’accès au fichier CSS utilisé pour personnaliser l’aspect du formulaire.

* **rootPanel** : panneau racine d’un formulaire adaptatif. Il peut contenir des sous-panneaux sous le noeud éléments . Une disposition peut être associée à chaque panneau, y compris le panneau racine. La disposition du panneau détermine la disposition du formulaire. Par exemple, dans la mise en page en accordéon, les éléments constitutifs sont disposés sous la forme d’étapes en accordéon.

* **barre d’outils** : une barre d’outils globale est associée à un conteneur de formulaires adaptatifs. Il s’agit d’une barre d’outils à l’échelle du formulaire. Cette barre d’outils peut être ajoutée à l’aide de l’action **[!UICONTROL Ajouter une barre d’outils]** de la barre d’édition, ce qui permet aux auteurs d’ajouter des actions telles que Envoyer, Enregistrer, réinitialiser, etc.

* **ressources** : ce nœud contient des informations supplémentaires au sujet de la création de formulaires. Il s’agit, par exemple, de détails sur le modèle de formulaire, de détails de localisation, etc).
