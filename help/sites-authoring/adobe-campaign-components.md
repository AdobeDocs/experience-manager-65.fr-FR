---
title: Intégration aux composants Adobe Campaign
description: Lors de l’intégration à Adobe Campaign, des composants sont disponibles pour l’envoi de newsletters et de formulaires.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
docset: aem65
exl-id: d1132fcd-e6a0-44a2-8753-d250f68fbd78
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '2859'
ht-degree: 100%

---

# Composants d’Adobe Campaign{#adobe-campaign-components}

Lors de l’intégration à Adobe Campaign, des composants sont disponibles pour l’utilisation de newsletters et de formulaires. Tous deux sont décrits dans ce document.

>[!CAUTION]
>
>Les composants d’e-mail AEM ont été abandonnés. En raison de la nature de l’e-mail, en particulier son contenu et son style, les composants d’e-mail fournis prêts-à-l’emploi par AEM ne sont que rarement réutilisés par les clients car ils ont besoin d’implémenter des styles personnalisés dans les composants requis pour les projets.
>
>Les composants d’e-mail peuvent être implémentés au niveau du projet. Les composants d’e-mail AEM obsolètes illustrent la manière dont cela peut être réalisé. Toutefois, n’utilisez pas ces composants obsolètes sur les projets.

## Composants Newsletter Adobe Campaign {#adobe-campaign-newsletter-components}

Tous les composants d’Adobe Campaign appliquent les méthodes recommandées décrites dans les [bonnes pratiques pour les modèles d’e-mail](/help/sites-administering/best-practices-for-email-templates.md) et dépendent du langage de balisage [HTL](https://helpx.adobe.com/fr/experience-manager/htl/using/overview.html) d’Adobe.

Lorsque vous ouvrez une newsletter ou un e-mail configuré de manière à être intégré à Adobe Campaign, les composants ci-dessous doivent s’afficher dans la section **Newsletter Adobe Campaign** :

* En-tête (Campaign)
* Image (Campaign)
* Lien (Campaign)
* Modèle d’image Scene7 (Campaign)
* Référence ciblée (Campaign)
* Texte et image (Campaign)
* Texte et personnalisation (Campaign)

Vous trouverez une description de ces composants dans la section suivante.

Les composants se présentent comme suit :

![chlimage_1-43](assets/chlimage_1-43.png)

### En-tête (Campaign) {#heading-campaign}

Le composant d’en-tête peut :

* Afficher le nom de la page active en laissant vide le champ **Titre**.
* Afficher un texte que vous spécifiez dans le champ **Titre**.

Vous modifiez directement le composant **En-tête (Campagne)**. Laissez-le vide pour utiliser le titre de la page.

![chlimage_1-44](assets/chlimage_1-44.png)

Vous pouvez configurer les éléments suivants :

* **Titre**
Si vous souhaitez utiliser un autre nom que le titre de la page, saisissez-le ici.

* **Niveau de titre (1, 2, 3, 4)**
Niveau de titre d’après la catégorie de titre HTML 1-4.

L’exemple ci-dessous présente le composant Titre (Campaign) affiché.

![chlimage_1-45](assets/chlimage_1-45.png)

### Image (Campaign) {#image-campaign}

Le composant image (campagne) affiche une image et le texte qui l’accompagne selon les paramètres spécifiés.

Vous pouvez charger une image, puis la modifier et la manipuler (par exemple, la recadrer, la faire pivoter ou y ajouter un lien/titre/texte).

Vous pouvez faire glisser et déposer une image à partir de l’[explorateur de ressources](/help/sites-authoring/author-environment-tools.md#assetsbrowsertouchoptimizedui) directement sur le composant ou sa [boîte de dialogue Configurer](/help/sites-authoring/editing-content.md#editconfigurecopycutdeletepastetouchoptimizedui). Vous pouvez également charger une image à partir de la boîte de dialogue Configurer ; celle-ci contrôle également toutes les définitions, ainsi que la manipulation de l’image :

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>Pour enregistrer l’image, vous devez renseigner le champ **Texte de remplacement**.

Une fois l’image chargée (pas avant), vous pouvez utiliser la [modification statique](/help/sites-authoring/editing-content.md#editcontenttouchoptimizedui) pour recadrer/faire pivoter l’image selon les besoins :

![Barre d’outils de la modification statique](do-not-localize/chlimage_1-10.png)

>[!NOTE]
>
>L’éditeur statique utilise la taille et les proportions d’origine de l’image lors de l’édition. Vous pouvez également spécifier des propriétés de hauteur et de largeur. Toute restriction de taille et de proportion définie dans les propriétés est appliquée lorsque vous enregistrez vos modifications.
>
>Selon votre instance, des restrictions minimales et maximales peuvent aussi être imposées par la [conception de la page](/help/sites-developing/designer.md). Ces restrictions sont développées lors de la mise en œuvre du projet.

Différentes autres options sont disponibles en mode Plein écran. Par exemple, Carte et Zoom :

![Mode de modification Plein écran](do-not-localize/chlimage_1-11.png)

Lorsqu’une image est chargée, vous pouvez configurer ce qui suit :

* **Mapper**
Pour faire correspondre une image, sélectionnez Mapper. Vous spécifiez ensuite comment créer l’image interactive (rectangle, polygone, etc.) et l’emplacement où doit pointer la zone.

* **Recadrer**
Sélectionnez cette option pour recadrer une image à l’aide de la souris.

* **Rotation**
Pour faire pivoter une image, sélectionnez Rotation, à plusieurs reprises si nécessaire.

* **Effacer**
Permet de supprimer l’image actuelle.

* Barre de zoom (IU classique uniquement)
Pour effectuer un zoom avant ou arrière sur l’image, utilisez le curseur situé sous l’image (au-dessus des boutons OK et Annuler).
* **Titre**
Titre de l’image.

* **Texte de remplacement**
Texte de remplacement à utiliser lors de la création de contenu accessible.

* **Lier à**
Créez un lien vers les ressources ou d’autres pages de votre site Web.

* **Description**
Description de l’image.

* **Taille**
Permet de définir la hauteur et la largeur de l’image.

>[!NOTE]
>
>Pour enregistrer l’image, vous devez renseigner le champ **Texte de remplacement** dans l’onglet **Avancé**. Sinon, l’image n’est pas enregistrée et le message d’erreur ci-dessous s’affiche :
>
>`Validation failed. Verify the values of the marked fields.`
>

L’exemple ci-dessous présente le composant Image (Campaign) affiché.

![chlimage_1-47](assets/chlimage_1-47.png)

### Lien (Campaign) {#link-campaign}

Le composant Lien (Campaign) vous permet d’ajouter un lien à votre newsletter.

Vous pouvez configurer les éléments ci-dessous sur les onglets **Affichage**, **Informations d’URL** ou **Avancé** :

* **Légende du lien**
Légende du lien. Il s’agit du texte que les utilisateurs voient.

* **Info-bulle du lien**
Ajoute des informations supplémentaires sur l’utilisation du lien.

* **LinkType**
Dans la liste déroulante, sélectionnez une **URL personnalisée** ou un **Document adaptatif**. Ce champ est obligatoire. Si vous sélectionnez URL personnalisée, vous pouvez fournir l’URL du lien. Si vous sélectionnez Document adaptatif, vous pouvez fournir le chemin du document.

* **Paramètre d’URL supplémentaire**
Ajoutez des paramètres d’URL supplémentaires. Cliquez sur Ajouter un élément pour ajouter plusieurs éléments.

>[!NOTE]
>
>Pour enregistrer le composant, vous devez renseigner le champ **Type de lien** dans l’onglet **Informations sur l’URL**. Autrement, le composant n’est pas enregistré et le message d’erreur ci-dessous s’affiche :
>
>`Validation failed. Verify the values of the marked fields.`
>

L’exemple ci-dessous présente le composant Lien (Campaign) affiché.

![chlimage_1-48](assets/chlimage_1-48.png)

### Modèle d’image Dynamic Media Classic (Scene7) (Campaign) {#scene-image-template-campaign}

Les modèles d’image Dynamic Media Classic (Scene7) sont des images superposées, où le contenu et les propriétés peuvent être paramétrés pour plus de variabilité. Le composant **[!UICONTROL Modèle d’image]** permet d’utiliser des modèles Scene7 dans des newsletters et de modifier les valeurs des paramètres de modèle. De plus, vous pouvez utiliser des variables de métadonnées Adobe Campaign dans les paramètres de sorte que chaque utilisateur visualise l’image de façon personnalisée.

![chlimage_1-49](assets/chlimage_1-49.png)

Cliquez sur **Modifier** pour configurer le composant. Vous pouvez configurer les paramètres décrits dans cette section. Ce modèle d’image Scene7 est décrit en détail dans la section [Composant Modèle d’image Scene7](/help/assets/scene7.md#image-template).

En outre, le panneau des paramètres répertorie tous les paramètres de modèle définis pour le modèle dans Scene7. Pour chacun de ces paramètres, vous pouvez adapter la valeur, insérer des variables ou les réinitialiser à leur valeur par défaut.

![chlimage_1-50](assets/chlimage_1-50.png)

### Référence ciblée (Campaign) {#targeted-reference-campaign}

Le composant Référence ciblée (Campaign) permet de créer une référence à un paragraphe ciblé.

Dans ce composant, vous accédez au paragraphe ciblé pour le sélectionner.

Cliquez sur l’icône de dossier pour accéder au paragraphe à référencer. Lorsque vous avez terminé, cliquez sur la coche.

### Texte et image (Campaign) {#text-image-campaign}

Le composant Texte et image (Campaign) permet d’ajouter un bloc de texte et une image.

Lorsque vous cliquez pour configurer le composant, sélectionnez Texte ou Image.

![chlimage_1-51](assets/chlimage_1-51.png)

La sélection du composant **Texte** affiche un éditeur en ligne :

![Barre d’outils Texte](do-not-localize/chlimage_1-12.png)

La sélection du composant **Image** affiche l’éditeur statique pour les images :

![Barre d’outils Image](do-not-localize/chlimage_1-13.png)

Voir [Composant Image (Campaign)](#image-campaign) pour plus d’informations sur l’utilisation des images. Voir [Composant Texte et personnalisation (Campaign)](#text-personalization-campaign) pour plus d’informations sur l’utilisation de textes.

Comme pour les composants Texte et personnalisation (Campaign) et Image (Campaign), vous pouvez configurer :

* **Texte**
Permet de saisir du texte. Utilisez la barre d’outils pour modifier la mise en forme, créer des listes et ajouter des liens.

* **Image**
Faites glisser une image à partir de l’Outil de recherche de contenu ou cliquez pour accéder à une image. Vous pouvez la recadrer ou la faire pivoter le cas échéant.

* **Propriétés de l’image** (**Propriétés d’image avancées**)
Permet de spécifier ce qui suit :

   * **Titre**
Titre du bloc ; il s’affiche lorsque l’utilisateur ou l’utilisatrice pointe dessus avec la souris.

   * **Texte de remplacement**
Texte de remplacement à afficher lorsque l’image ne peut pas être affichée.

   * **Lier à**
Créez un lien vers les ressources ou d’autres pages de votre site Web.

   * **Description**
Description de l’image.

   * **Taille**
Permet de définir la hauteur et la largeur de l’image.

>[!NOTE]
>
>Le champ **Texte de remplacement** sur l’onglet **Avancé** est obligatoire. Autrement, vous ne pouvez pas enregistrer le composant, et le message d’erreur ci-dessous s’affiche :
>
>`Validation failed. Verify the values of the marked fields.`
>

L’exemple ci-dessous présente le composant Texte et image (Campaign) affiché.

![chlimage_1-52](assets/chlimage_1-52.png)

### Texte et personnalisation (Campaign) {#text-personalization-campaign}

Le composant Texte et personnalisation (Campaign) permet de saisir un bloc de texte en utilisant un éditeur WYSIWYG, avec les fonctionnalités de l’[éditeur de texte enrichi](/help/sites-authoring/rich-text-editor.md). De plus, ce composant permet d’utiliser des champs de contexte et des blocs de personnalisation, disponibles dans Adobe Campaign. Reportez-vous également à la section [Insertion d’une personnalisation](/help/sites-authoring/campaign.md#inserting-personalization).

Une série d’icônes permet de mettre en forme le texte (attributs de police, alignement, liens, listes et mise en retrait). Les fonctionnalités sont globalement identiques dans [les deux IU](/help/sites-authoring/editing-content.md), même si l’affichage est différent :

![chlimage_1-53](assets/chlimage_1-53.png)

Dans l’éditeur statique, vous pouvez ajouter du texte, modifier la justification, ajouter et supprimer des liens, ajouter des champs contextuels ou des blocs de personnalisation, puis passer en mode plein écran. Une fois l’ajout de texte/la personnalisation terminé, cochez la case pour enregistrer vos modifications (ou x pour annuler). Pour plus d’informations, reportez-vous à la section [Modification statique.](/help/sites-authoring/editing-content.md#editcontenttouchoptimizedui)

>[!NOTE]
>
>* Les champs de personnalisation disponibles dépendent du modèle Adobe Campaign auquel votre newsletter est liée.
>* Après avoir sélectionné un persona dans ContextHub, les champs de personnalisation sont remplacés automatiquement par les données du profil sélectionné.
>
>Voir [Insertion de la personnalisation](/help/sites-authoring/campaign.md#inserting-personalization).

![chlimage_1-54](assets/chlimage_1-54.png)

>[!NOTE]
>
>Seuls les champs définis dans le schéma **nms:seedMember** ou l’une de ses extensions sont pris en compte. Les attributs des tables liés à **nms:seedMember** ne sont pas disponibles.

## Composants Formulaire d’Adobe Campaign {#adobe-campaign-form-components}

Vous utilisez les composants Adobe Campaign pour créer un formulaire que les utilisateurs et utilisatrices remplissent pour s’abonner ou se désinscrire d’une newsletter, ou mettre à jour leurs profils utilisateur. Voir [Création de formulaires Adobe Campaign](/help/sites-authoring/adobe-campaign-forms.md) pour plus d’informations.

Chaque champ de composant peut être associé à un champ de base de données Adobe Campaign. Les champs disponibles varient en fonction du type de données qu’ils contiennent, comme décrit dans la section [Composants et type de données](#components-and-data-type). Si vous étendez votre schéma de destinataires dans Adobe Campaign, les nouveaux champs seront disponibles dans les composants dont les types de données correspondent.

Lorsque vous ouvrez un formulaire configuré pour être intégré à Adobe Campaign, les composants ci-dessous de la section **Adobe Campaign** s’affichent :

* Case à cocher (Campaign)
* Champ de date (Campaign) et champ de date/HTML 5 (Campaign)
* Clé primaire chiffrée (Campaign)
* Affichage d’erreur (campagne)
* Clé de réconciliation masquée (Campaign)
* Champ numérique (Campaign)
* Champ d’option (Campaign)
* Liste de contrôle d’abonnements (Campaign)
* Champ de texte (Campaign)

Les composants se présentent comme suit :

![chlimage_1-55](assets/chlimage_1-55.png)

Cette section décrit en détail chaque composant.

### Composants et type de données {#components-and-data-type}

Le tableau suivant décrit les composants disponibles pour afficher et modifier les données de profil Adobe Campaign. Chaque composant peut être mappé à un champ de profil Adobe Campaign pour afficher sa valeur et mettre à jour le champ lors de l’envoi du formulaire. Les différents composants ne peuvent être associés qu’à des champs d’un type de données approprié.

<table>
 <tbody>
  <tr>
   <td><p><strong>Composant</strong></p> </td>
   <td><p><strong>Type de données du champ Adobe Campaign</strong></p> </td>
   <td><p><strong>Exemple de champ</strong></p> </td>
  </tr>
  <tr>
   <td><p>Case à cocher (Campaign)</p> </td>
   <td><p>booléen</p> </td>
   <td><p>Ne plus contacter (quel que soit le canal)</p> </td>
  </tr>
  <tr>
   <td><p>Champ de date (Campaign)</p> <p>Champ de date/HTML 5 (Campaign)</p> </td>
   <td><p>date</p> </td>
   <td><p>Date de naissance</p> </td>
  </tr>
  <tr>
   <td><p>Champ numérique (Campaign)</p> </td>
   <td><p>numérique (octet, court, long, double)</p> </td>
   <td><p>Âge</p> </td>
  </tr>
  <tr>
   <td><p>Champ d’option (Campaign)</p> </td>
   <td><p>octet avec valeurs associées</p> </td>
   <td><p>Genre</p> </td>
  </tr>
  <tr>
   <td><p>Champ de texte (Campaign)</p> </td>
   <td><p>chaîne</p> </td>
   <td><p>E-mail</p> </td>
  </tr>
 </tbody>
</table>

### Paramètres communs à la plupart des composants {#settings-common-to-most-components}

Les composants d’Adobe Campaign comportent des paramètres communs à tous les composants (à l’exception des composants Clé primaire chiffrée et Clé de réconciliation masquée).

Dans la plupart des composants, vous pouvez configurer les éléments suivants :

#### Titre et texte {#title-and-text}

![chlimage_1-56](assets/chlimage_1-56.png)

* **Titre**
Si vous souhaitez utiliser un autre nom que le nom de l’élément, saisissez-le ici.

* **Masquer le titre**
Cochez cette case si vous ne voulez pas afficher le titre.

* **Description**
Ajoutez une description dans ce champ pour donner des informations supplémentaires pour les utilisateurs.

* **N’afficher que la valeur**
Affiche uniquement la valeur, le cas échéant.

#### Adobe Campaign {#adobe-campaign}

Vous pouvez configurer les éléments suivants :

* **Correspondance**
Sélectionnez un champ de personnalisation Adobe Campaign, si cela est approprié.

* **Clé de réconciliation**
Cochez cette case si ce champ fait partie de la clé de réconciliation.

![chlimage_1-57](assets/chlimage_1-57.png)

#### Contraintes {#constraints}

* **Obligatoire** Cochez cette case pour que ce composant soit obligatoire. En d’autres termes, les utilisateurs doivent saisir une valeur.
* **Message obligatoire** Si vous le souhaitez, ajoutez un message indiquant que le champ est obligatoire.

![chlimage_1-58](assets/chlimage_1-58.png)

#### Style {#styling}

* **CSS**
Indiquez les classes CSS à utiliser pour ce composant.

![chlimage_1-59](assets/chlimage_1-59.png)

### Case à cocher (Campaign) {#checkbox-campaign}

Le composant Case à cocher (Campaign) permet à l’utilisateur ou à l’utilisatrice de modifier les champs de profil Adobe Campaign qui sont de type données booléennes. Par exemple, vous pouvez avoir un composant Case à cocher (Campaign) qui permet au destinataire ou à la destinataire d’indiquer qu’il ou elle ne souhaite être contacté(e) via aucun canal.

Vous pouvez [configurer des paramètres communs à la plupart des composants d’Adobe Campaign](#settings-common-to-most-components) dans le composant Case à cocher (Campaign).

L’exemple ci-dessous présente le composant Case à cocher (Campaign) affiché.

![chlimage_1-60](assets/chlimage_1-60.png)

### Champ de date (Campaign) et champ de date/HTML 5 (Campaign) {#date-field-campaign-and-date-field-html-campaign}

Utilisez le champ date pour permettre aux personnes destinataires d’indiquer une date ; par exemple, vous pourriez souhaiter que les personnes destinataires indiquent leur date de naissance. Le format des dates correspond au format utilisé dans votre instance Adobe Campaign.

Outre les [paramètres communs à la plupart des composants Adobe Campaign](#settings-common-to-most-components), vous pouvez configurer les éléments suivants :

* Liste déroulante **Contraintes – Contrainte**
Vous pouvez sélectionner **Aucune** ou **Date** pour ajouter une contrainte de date ou aucune contrainte. Si vous sélectionnez Date, la réponse que les utilisateurs renseignent dans le champ doit correspondre à un format de date.

* **Message de contrainte** De plus, vous pouvez ajouter un message de contrainte afin que les utilisateurs sachent quel format suivre pour leur réponse.
* **Style – Largeur** Ajustez la largeur du champ en cliquant ou en appuyant sur les icônes « **+** » et « **-** » ou saisissez un nombre.

L’exemple ci-dessous présente le composant Champ de date (Campaign), dont la largeur ajustée, affiché.

![chlimage_1-61](assets/chlimage_1-61.png)

### Clé primaire chiffrée (Campaign) {#encrypted-primary-key-campaign}

Ce composant définit le nom du paramètre d’URL qui contiendra l’identifiant d’un profil Adobe Campaign (**Identifiant de ressource principal** ou **Clé primaire chiffrée** dans Adobe Campaign Standard et la version 6.1, respectivement).

Chaque formulaire affichant et modifiant les données de profil Adobe Campaign **doit** inclure un composant Clé primaire chiffrée.

Vous pouvez configurer les éléments ci-dessous dans le composant Clé primaire chiffrée (Campaign) :

* **Titre et texte – Nom d’élément** Par défaut, la valeur encryptedPK est proposée. Il suffit de modifier le nom de l’élément lorsqu’il entre en conflit avec le nom d’un autre élément du formulaire. Deux champs de formulaire ne peuvent pas avoir le même nom d’élément.
* **Adobe Campaign – Paramètre d’URL** Ajoutez le paramètre d’URL de l’EPK. Par exemple, vous pouvez utiliser la valeur **epk**.

L’exemple ci-dessous présente le composant Clé primaire chiffrée (Campaign) affiché.

![chlimage_1-62](assets/chlimage_1-62.png)

### Affichage d’erreur (campagne) {#error-display-campaign}

Ce composant vous permet d’afficher les erreurs du serveur principal. La gestion des erreurs du formulaire doit être définie sur Transférer pour que le composant fonctionne correctement.

L’exemple suivant présente le composant Affichage d’erreur (Campaign) affiché.

![chlimage_1-63](assets/chlimage_1-63.png)

### Clé de réconciliation masquée (Campaign) {#hidden-reconciliation-key-campaign}

Le composant Clé de réconciliation masquée (Campaign) permet d’ajouter des champs masqués dans le cadre de la clé de réconciliation d’un formulaire.

Vous pouvez configurer les éléments ci-dessous dans le composant Clé de réconciliation masquée (Campaign) :

* **Titre et texte – Nom d’élément** Par défaut, reconcilKey est proposé. Il suffit de modifier le nom de l’élément lorsqu’il entre en conflit avec le nom d’un autre élément du formulaire. Deux champs de formulaire ne peuvent pas avoir le même nom d’élément.
* **Adobe Campaign – Mappage** Mappez-la à un champ de personnalisation Adobe Campaign.

L’exemple ci-dessous présente le composant Clé de réconciliation masquée (Campaign) affiché.

![chlimage_1-64](assets/chlimage_1-64.png)

### Champ numérique (Campaign) {#numeric-field-campaign}

Utilisez le champ numérique pour permettre aux personnes destinataires de saisir des nombres, par exemple leur âge.

Outre les [paramètres communs à la plupart des composants Adobe Campaign](#settings-common-to-most-components), vous pouvez configurer les éléments suivants :

* Liste déroulante **Contraintes – Contrainte**
Vous pouvez sélectionner - **Aucune** ou **Numérique -** pour ajouter une contrainte de nombre ou aucune contrainte. Si vous sélectionnez Numérique, la réponse saisie par les utilisateurs dans le champ doit être numérique.

* **Message de contrainte** De plus, vous pouvez ajouter un message de contrainte afin que les utilisateurs sachent quel format suivre pour leur réponse.
* **Style – Largeur** Ajustez la largeur du champ en cliquant ou en appuyant sur les icônes « **+** » et « **-** » ou saisissez un nombre.

L’exemple ci-dessous présente le composant Champ numérique (Campaign), dont la largeur est configurée.

![chlimage_1-65](assets/chlimage_1-65.png)

### Champ d’option (Campaign) {#option-field-campaign}

Cette liste déroulante vous permet de sélectionner une option. Par exemple, le genre ou le statut d’un ou une destinataire.

Vous pouvez [configurer des paramètres communs à la plupart des composants d’Adobe Campaign](#settings-common-to-most-components) dans le composant Champ d’option (Campaign). Pour remplir la liste déroulante, sélectionnez le champ approprié dans les champs de personnalisation d’Adobe Campaign en cliquant ou en appuyant sur le symbole Adobe Campaign et en accédant au champ.

![chlimage_1-66](assets/chlimage_1-66.png)

L’exemple ci-dessous présente le composant Champ d’option (Campaign) affiché.

![chlimage_1-67](assets/chlimage_1-67.png)

### Liste de contrôle d’abonnements (Campaign) {#subscriptions-checklist-campaign}

Utilisez le composant **Liste de contrôle d’abonnements (Campaign)** pour modifier les abonnements associés à un profil Adobe Campaign.

Lorsque vous ajoutez ce composant à un formulaire, il affiche tous les abonnements disponibles sous forme de cases à cocher et permet à l’utilisateur de sélectionner les abonnements souhaités. Lorsque les utilisateurs envoient le formulaire, ce composant abonne l’utilisateur aux services sélectionnés ou l’en désabonne en fonction du type d’action de formulaire (**Adobe Campaign : S’abonner à des services** ou **Adobe Campaign : Se désabonner de services**).

>[!NOTE]
>
>Le composant ne vérifie pas les services auxquels l’utilisateur est déjà abonné/dont il est désabonné.

Vous pouvez [configurer des paramètres communs à la plupart des composants d’Adobe Campaign](#settings-common-to-most-components) dans le composant Liste de contrôle des abonnements (Campaign). (Aucune configuration Adobe Campaign n’est disponible pour ce composant.)

L’exemple ci-dessous montre l’affichage du composant Liste de contrôle des abonnements (Campaign).

![chlimage_1-68](assets/chlimage_1-68.png)

### Champ de texte (Campaign) {#text-field-campaign}

Le composant Champ de texte (Campaign) qui vous permet de saisir des données de type chaîne, telles qu’un prénom, un nom, une adresse, une adresse e-mail, etc.

Outre les [paramètres communs à la plupart des composants Adobe Campaign](#settings-common-to-most-components), vous pouvez configurer les éléments suivants :

* Liste déroulante **Contraintes – Contrainte**
Vous pouvez sélectionner - **Aucune,** **E-mail** ou **Nom** (pas de trémas) - pour ajouter une contrainte d’adresse électronique, de nom ou aucune contrainte. Si vous sélectionnez l’option E-mail, la réponse saisie par les utilisateurs dans le champ doit correspondre à une adresse électronique. Si vous sélectionnez Nom, il doit s’agit d’un nom (les trémas ne sont pas autorisés).

* **Message de contrainte** De plus, vous pouvez ajouter un message de contrainte afin que les utilisateurs sachent quel format suivre pour leur réponse.
* **Style – Largeur** Ajustez la largeur du champ en cliquant ou en appuyant sur les icônes « **+** » et « **-** » ou saisissez un nombre.

L’exemple ci-dessous présente le composant Champ de texte (Campaign) affiché.

![chlimage_1-69](assets/chlimage_1-69.png)
