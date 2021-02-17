---
title: Composants d’Adobe Campaign
seo-title: Composants d’Adobe Campaign
description: Lorsque vous procédez à l’intégration à Adobe Campaign, des composants sont disponibles pour l’utilisation de newsletters et de formulaires
seo-description: Lorsque vous procédez à l’intégration à Adobe Campaign, des composants sont disponibles pour l’utilisation de newsletters et de formulaires
uuid: a858d5ca-aa6e-4bde-92db-a6dcd8b48ae6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 9da34dab-7e89-4127-ab26-532687746b2a
docset: aem65
translation-type: tm+mt
source-git-commit: 90c99e527a40bb663d4f32d8746b46cf34a2319f
workflow-type: tm+mt
source-wordcount: '2854'
ht-degree: 82%

---


# Composants d’Adobe Campaign{#adobe-campaign-components}

Lorsque vous procédez à l’intégration à Adobe Campaign, des composants sont disponibles pour l’utilisation de newsletters et de formulaires. Ils sont tous deux décrits dans ce document.

>[!CAUTION]
>
>Les composants de messagerie AEM ont été abandonnés. En raison de la nature de l’e-mail, qui fusionne le contenu et le style, les composants de l’e-mail fournis de manière standard par AEM deviennent de réutilisation limitée pour les clients en raison de la nécessité d’implémenter des styles personnalisés dans les composants requis pour les projets.
>
>Les composants de courrier électronique peuvent être implémentés au niveau du projet et les composants de courrier électronique AEM obsolètes illustrent comment cela peut être réalisé. Cependant, ces composants obsolètes ne doivent pas être utilisés sur les projets.

## Composant Newsletter Adobe Campaign {#adobe-campaign-newsletter-components}

Tous les composants d’Adobe Campaign appliquent les méthodes recommandées décrites dans les [bonnes pratiques pour les modèles de courrier électronique](/help/sites-administering/best-practices-for-email-templates.md) et dépendent du langage de balisage [HTL](https://helpx.adobe.com/fr/experience-manager/htl/using/overview.html) d’Adobe.

Lorsque vous ouvrez une newsletter/un courrier électronique configuré de manière à être intégré à Adobe Campaign, les composants ci-dessous doivent s’afficher dans la section **Newsletter Adobe Campaign** :

* Titre (Campaign)
* Image (Campaign)
* Lien (Campaign)
* Modèle d’image Scene7 (Campaign)
* Référence ciblée (Campaign)
* Texte et image (Campaign)
* Texte et personnalisation (Campaign)

La section qui suit contient une description de ces composants.

Les composants apparaissent comme suit :

![chlimage_1-43](assets/chlimage_1-43.png)

### Titre (Campaign) {#heading-campaign}

Le composant Titre permet d’afficher les éléments suivants :

* Nom de la page actuelle (lorsque le champ **Titre** est vide)
* Texte spécifié dans le champ **Titre**

Vous modifiez directement le composant **Titre (Campaign)**. Laissez ce champ vide pour utiliser le titre de la page.

![chlimage_1-44](assets/chlimage_1-44.png)

Vous pouvez configurer les éléments suivants :

* **Titre**
Si vous souhaitez utiliser un autre nom que le titre de la page, saisissez-le ici.

* **Niveau de titre (1, 2, 3, 4)** Niveau de titre d’après la catégorie de titre HTML 1-4.

L’exemple ci-dessous présente le composant Titre (Campaign) affiché.

![chlimage_1-45](assets/chlimage_1-45.png)

### Image (Campaign) {#image-campaign}

Le composant Image (Campaign) affiche une image et le texte qui l’accompagne selon les paramètres spécifiés.

Vous pouvez charger une image, puis la modifier et la manipuler (par exemple, la recadrer, la faire pivoter ou y ajouter un lien/titre/texte).

Vous pouvez faire glisser et déposer une image à partir de l’[explorateur de ressources](/help/sites-authoring/author-environment-tools.md#assetsbrowsertouchoptimizedui) directement sur le composant ou sa [boîte de dialogue Configurer](/help/sites-authoring/editing-content.md#editconfigurecopycutdeletepastetouchoptimizedui). Vous pouvez également charger une image à partir de la boîte de dialogue Configurer ; celle-ci contrôle également toutes les définitions, ainsi que la manipulation de l’image :

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>Vous devez entrer des informations dans le champ **Alt Text**, sinon l&#39;image ne peut pas être enregistrée.

Une fois l’image téléchargée (et pas avant), vous pouvez utiliser [l’édition statique](/help/sites-authoring/editing-content.md#editcontenttouchoptimizedui) pour recadrer/faire pivoter l’image selon les besoins :

![](do-not-localize/chlimage_1-10.png)

>[!NOTE]
>
>L’éditeur statique utilise la taille d’origine et les proportions de l’image lors de la modification. Vous pouvez également spécifier les propriétés de hauteur et de largeur. Les restrictions de taille et de format définies dans les propriétés sont appliquées lorsque vous enregistrez vos modifications.
>
>Selon votre instance, des restrictions minimales et maximales peuvent aussi être imposées par la [conception de la page](/help/sites-developing/designer.md). Ces restrictions sont développées lors de la mise en œuvre du projet.

Différentes autres options sont disponibles en mode Plein écran. Par exemple, Carte et Zoom :

![](do-not-localize/chlimage_1-11.png)

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
Créez un lien vers les ressources ou d’autres pages de votre site web.

* **Description**
Description de l’image.

* **Taille**
Permet de définir la hauteur et la largeur de l’image.

>[!NOTE]
>
>Pour enregistrer l’image, vous devez renseigner le champ **Texte de remplacement** sur l’**onglet Avancé**. Sinon, le message d’erreur ci-dessous s’affiche :
>
>`Validation failed. Verify the values of the marked fields.`


L’exemple ci-dessous présente le composant Image (Campaign) affiché.

![chlimage_1-47](assets/chlimage_1-47.png)

### Lien (Campaign) {#link-campaign}

Le composant Lien (Campaign) permet d’ajouter un lien à votre newsletter.

Vous pouvez configurer les éléments ci-dessous sur les onglets **Affichage**, **Informations d’URL** ou **Avancé** :

* **Légende du lien** Légende du lien. Il s’agit du texte que les utilisateurs voient.

* **Info-bulle du lien** Ajoute des informations supplémentaires sur l’utilisation du lien.

* ****
LinkTypeDans la liste déroulante, sélectionnez entre un 
**URL personnalisée**  et Document **** adaptatif. Ce champ est obligatoire. Si vous sélectionnez l’URL personnalisée, vous pouvez indiquer l’URL du lien. Si vous sélectionnez Document adaptatif, vous pouvez préciser le chemin d’accès au document.

* **Paramètre d’URL supplémentaire** Ajoutez des paramètres d’URL supplémentaires. Cliquez sur Ajouter un élément pour ajouter plusieurs éléments.

>[!NOTE]
>
>Vous devez entrer des informations dans le champ **Type de lien** de l&#39;onglet **Informations sur l&#39;URL**, sinon le composant ne peut pas enregistrer et vous voyez le message d&#39;erreur suivant :
>
>`Validation failed. Verify the values of the marked fields.`


L’exemple ci-dessous présente le composant Lien (Campaign) affiché.

![chlimage_1-48](assets/chlimage_1-48.png)

### Modèle d’image Scene7 (Campaign) {#scene-image-template-campaign}

[Les ](https://help.adobe.com/en_US/scene7/using/WS60B68844-9054-4099-BF69-3DC998A04D3C.html) modèles d’image Scene7 sont des fichiers d’image superposés où le contenu et les propriétés peuvent être paramétrés en fonction de la variabilité. Le composant **Modèle d’image** permet d’utiliser des modèles Scene7 dans des newsletters et de modifier les valeurs des paramètres de modèle. En outre, vous pouvez utiliser des variables de métadonnées Adobe Campaign à l’intérieur des paramètres, de sorte que chaque utilisateur expérimente l’image d’une manière personnalisée.

![chlimage_1-49](assets/chlimage_1-49.png)

Cliquez sur **Modifier** pour configurer le composant. Vous pouvez configurer les paramètres décrits dans cette section. Ce modèle d’image Scene7 est décrit en détail dans le composant [Modèle d’image Scene7](/help/assets/scene7.md#image-template).

De plus, le panneau Paramètres répertorie tous les paramètres de modèle définis pour le modèle dans Scene7. Pour chacun de ces paramètres, vous pouvez personnaliser la valeur, insérer des variables ou rétablir leur valeur par défaut.

![chlimage_1-50](assets/chlimage_1-50.png)

### Référence ciblée (Campaign) {#targeted-reference-campaign}

Le composant Référence ciblée (Campaign) permet de créer une référence à un paragraphe ciblé.

Dans ce composant, vous accédez au paragraphe ciblé pour le sélectionner.

Cliquez sur l’icône du dossier pour accéder au paragraphe à référencer. Une fois que vous avez terminé, cliquez sur l’icône de la coche.

### Texte et image (Campaign) {#text-image-campaign}

Le composant Texte et image (Campaign) permet d’ajouter un bloc de texte et une image.

Lorsque vous cliquez pour configurer le composant, sélectionnez Texte ou Image.

![chlimage_1-51](assets/chlimage_1-51.png)

Sélectionnez **Texte** pour afficher un éditeur intégré :

![](do-not-localize/chlimage_1-12.png)

Sélectionnez **Image** pour afficher l’éditeur statique pour les images :

![](do-not-localize/chlimage_1-13.png)

Pour plus d’informations sur l’utilisation des images, reportez-vous à la section [Composant Image (Campaign)](#image-campaign). Pour plus d’informations sur l’utilisation de texte, reportez-vous à la section [Composant Texte et personnalisation (Campaign)](#text-personalization-campaign).

Comme pour les composants Texte et personnalisation (Campaign) et Image (Campaign), vous pouvez configurer :

* **Texte**
Permet de saisir du texte. Utilisez la barre d’outils pour modifier la mise en forme, créer des listes et ajouter des liens.

* **Image**
Faites glisser une image à partir de l’Outil de recherche de contenu ou cliquez pour accéder à une image. Vous pouvez la recadrer ou la faire pivoter le cas échéant.

* **Propriétés de l’image** (**Propriétés d’image avancées**)
Permet de spécifier ce qui suit :

   * **Titre**
Titre du bloc de texte ; il s’affiche lorsque l’utilisateur pointe dessus avec la souris.

   * **Texte de remplacement** Texte de remplacement à afficher lorsque l’image ne peut pas être affichée.

   * **Lier à** 
Créez un lien vers les ressources ou d’autres pages de votre site web.

   * **Description**
Description de l’image.

   * **Taille**
Permet de définir la hauteur et la largeur de l’image.

>[!NOTE]
>
>Le champ **Texte de remplacement** sur l’onglet **Avancé** est obligatoire. Autrement, vous ne pouvez pas enregistrer le composant, et le message d’erreur ci-dessous s’affiche :
>
>`Validation failed. Verify the values of the marked fields.`


L’exemple ci-dessous présente le composant Texte et image (Campaign) affiché.

![chlimage_1-52](assets/chlimage_1-52.png)

### Texte et personnalisation (Campaign) {#text-personalization-campaign}

Le composant Texte et personnalisation (Campaign) vous permet de saisir un bloc de texte à l’aide d’un éditeur WYSIWYG, avec les fonctionnalités fournies par l’[éditeur de texte enrichi](/help/sites-authoring/rich-text-editor.md). De plus, ce composant permet d’utiliser des champs de contexte et des blocs de personnalisation, disponibles dans Adobe Campaign. Reportez-vous également à la section [Insertion d’une personnalisation](/help/sites-authoring/campaign.md#inserting-personalization).

Une série d’icônes permet de mettre en forme le texte (attributs de police, alignement, liens, listes et retrait). La fonctionnalité est essentiellement la même dans [les deux interfaces](/help/sites-authoring/editing-content.md), bien que l&#39;apparence soit différente :

![chlimage_1-53](assets/chlimage_1-53.png)

Dans l’éditeur statique, vous pouvez ajouter du texte, modifier l’alignement, ajouter et supprimer des liens, ajouter des champs de contexte ou des blocs de personnalisation et passer en mode Plein écran. Une fois que vous avez fini d’ajouter du texte/une personnalisation, sélectionnez la coche pour enregistrer vos modifications (ou cliquez sur « x » pour annuler). Pour plus d’informations, voir [Modification en place](/help/sites-authoring/editing-content.md#editcontenttouchoptimizedui).

>[!NOTE]
>
>* Les champs de personnalisation disponibles dépendent du modèle Adobe Campaign auquel votre newsletter est liée.
>* Après avoir sélectionné un persona dans ContextHub, les champs de personnalisation sont remplacés automatiquement par les données du profil sélectionné.

>
>
Reportez-vous à la section [Insertion d’une personnalisation](/help/sites-authoring/campaign.md#inserting-personalization).

![chlimage_1-54](assets/chlimage_1-54.png)

>[!NOTE]
>
>Seuls les champs définis dans le schéma **nms:seedMember** ou l’une de ses extensions sont pris en compte. Les attributs des tables liés à **nms:seedMember** ne sont pas disponibles.

## Composants Formulaire d’Adobe Campaign {#adobe-campaign-form-components}

Vous utilisez des composants Adobe Campaign pour créer un formulaire que les utilisateurs remplissent pour s’abonner à une newsletter, s’en désabonner ou mettre à jour leur profil utilisateur. Pour plus d’informations, reportez-vous à la section [Création de formulaires Adobe Campaign](/help/sites-authoring/adobe-campaign-forms.md).

Chaque champ d’un composant peut être associé à un champ de base de données Adobe Campaign. Les champs disponibles varient selon le type de données qu’ils contiennent, comme indiqué dans la section [Composants et type de données](#components-and-data-type). Si vous étendez le schéma de destinataire dans Adobe Campaign, les nouveaux champs sont disponibles dans les composants dont les types de données concordent.

Lorsque vous ouvrez un formulaire configuré pour l’intégration à Adobe Campaign, vous voyez les composants suivants dans la section **Adobe Campaign** :

* Case à cocher (Campaign)
* Champ de date (Campaign) et champ de date/HTML5 (Campaign)
* Clé primaire chiffrée (Campaign)
* Affichage d’erreur (campagne)
* Clé de réconciliation masquée (Campaign)
* Champ numérique (Campaign)
* Champ d’option (Campaign)
* Liste de contrôle d’abonnements (Campaign)
* Champ de texte (Campaign)

Les composants apparaissent comme suit :

![chlimage_1-55](assets/chlimage_1-55.png)

Cette section décrit en détail chaque composant.

### Composants et type de données  {#components-and-data-type}

Le tableau ci-dessous décrit les composants disponibles pour afficher et modifier des données de profil Adobe Campaign. Chaque composant peut être associé à un champ de profil Adobe Campaign pour afficher sa valeur et mettre à jour le champ lorsque le formulaire est envoyé. Les différents composants ne peuvent être associés qu’aux champs d’un type de données approprié.

<table>
 <tbody>
  <tr>
   <td><p><strong>Composant</strong></p> </td>
   <td><p><strong>Type de données d’un champ Adobe Campaign </strong></p> </td>
   <td><p><strong>Exemple de champ</strong></p> </td>
  </tr>
  <tr>
   <td><p>Case à cocher (Campaign)</p> </td>
   <td><p>booléen</p> </td>
   <td><p>Plus un contact (par n’importe quel canal)</p> </td>
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
   <td><p>octet avec des valeurs associées</p> </td>
   <td><p>Sexe</p> </td>
  </tr>
  <tr>
   <td><p>Champ de texte (Campaign)</p> </td>
   <td><p>chaîne</p> </td>
   <td><p>Courrier électronique</p> </td>
  </tr>
 </tbody>
</table>

### Paramètres communs à la plupart des composants  {#settings-common-to-most-components}

Les composants Adobe Campaign possèdent des paramètres communs à tous les composants (à l’exception des composants Clé primaire chiffrée et Clé de rapprochement masquée).

Dans la plupart des composants, vous pouvez configurer les éléments suivants :

#### Titre et texte  {#title-and-text}

![chlimage_1-56](assets/chlimage_1-56.png)

* **Titre** 
Si vous souhaitez utiliser un autre nom que le nom de l’élément, saisissez-le ici.

* **Masquer le titre** Cochez cette case si vous ne voulez pas afficher le titre.

* **Description** Ajoutez une description dans le champ pour indiquer des informations supplémentaires pour les utilisateurs.

* **N’afficher que la valeur** Affiche uniquement la valeur, le cas échéant.

#### Adobe Campaign {#adobe-campaign}

Vous pouvez configurer les éléments suivants :

* **Correspondance** Sélectionnez un champ de personnalisation Adobe Campaign, si cela est approprié.

* **Clé de réconciliation** Cochez cette case si ce champ fait partie de la clé de réconciliation.

![chlimage_1-57](assets/chlimage_1-57.png)

#### Contraintes {#constraints}

* **Obligatoire** Cochez cette case pour que ce composant soit obligatoire. En d’autres termes, les utilisateurs doivent saisir une valeur.
* **Message obligatoire** Si vous le souhaitez, ajoutez un message indiquant que le champ est obligatoire.

![chlimage_1-58](assets/chlimage_1-58.png)

#### Style {#styling}

* **CSS** Indiquez les classes CSS à utiliser pour ce composant.

![chlimage_1-59](assets/chlimage_1-59.png)

### Case à cocher (Campaign) {#checkbox-campaign}

Le composant Case à cocher (Campaign) permet à l’utilisateur de modifier les champs de profil Adobe Campaign de type données booléennes. Par exemple, vous pouvez créer un composant Case à cocher (Campaign) qui permet au destinataire d’indiquer qu’il ne souhaite être contacté par aucun canal.

Vous pouvez [configurer les paramètres communs à la plupart des composants Adobe Campaign](#settings-common-to-most-components) dans le composant Case à cocher (Campaign).

L’exemple ci-dessous présente le composant Case à cocher (Campaign) affiché.

![chlimage_1-60](assets/chlimage_1-60.png)

### Champ de date (Campaign) et champ de date/HTML5 (Campaign) {#date-field-campaign-and-date-field-html-campaign}

Utilisez le champ de date pour permettre aux destinataires d’indiquer une date. Par exemple, vous souhaitez peut-être que les destinataires indiquent leur date de naissance. Le format de date correspond au format utilisé dans votre instance Adobe Campaign.

Outre les [paramètres communs à la plupart des composants Adobe Campaign](#settings-common-to-most-components), vous pouvez configurer les éléments suivants :

* **Contraintes - Liste déroulante** Contraintes Vous pouvez sélectionner -  **** Aucune  **date -** pour ajouter la contrainte d&#39;une date ou aucune contrainte. Si vous sélectionnez la date, la réponse que les utilisateurs renseignent dans le champ doit correspondre à un format de date.

* **Message de contrainte** De plus, vous pouvez ajouter un message de contrainte afin que les utilisateurs sachent quel format suivre pour leur réponse.
* **Style -** LargeurAjustez la largeur du champ en cliquant ou en appuyant sur les  **+** et  **** les icônes ou en entrant un nombre.

L’exemple ci-dessous présente le composant Champ de date (Campaign), dont la largeur ajustée, affiché.

![chlimage_1-61](assets/chlimage_1-61.png)

### Clé primaire chiffrée (Campaign) {#encrypted-primary-key-campaign}

Ce composant définit le nom du paramètre d’URL qui contient l’identifiant d’un profil Adobe Campaign (**Identifiant de ressource principal** ou **Clé primaire chiffrée** respectivement dans Adobe Campaign Standard et Adobe Campaign 6.1).

Chaque formulaire affichant et modifiant des données de profil Adobe Campaign **doit** comporter un composant Clé primaire chiffrée.

Vous pouvez configurer les éléments ci-dessous dans le composant Clé primaire chiffrée (Campaign) :

* **Titre et texte – Nom d’élément** Par défaut, la valeur encryptedPK est proposée. Il suffit de modifier le nom d’élément lorsqu’il crée un conflit avec le nom d’un autre élément sur le formulaire. Deux champs de formulaire ne peuvent pas porter le même nom d’élément.
* **Adobe Campaign – Paramètre d’URL** Ajoutez le paramètre d’URL de l’EPK. Par exemple, vous pouvez utiliser la valeur **epk**.

L’exemple ci-dessous présente le composant Clé primaire chiffrée (Campaign) affiché.

![chlimage_1-62](assets/chlimage_1-62.png)

### Affichage d’erreur (campagne) {#error-display-campaign}

Ce composant permet d’afficher les erreurs du système principal. La gestion des erreurs du formulaire doit être définie vers l’avant pour que le composant fonctionne correctement.

L’exemple ci-dessous présente le composant Affichage d’une erreur (Campaign) affiché.

![chlimage_1-63](assets/chlimage_1-63.png)

### Clé de réconciliation masquée (Campaign) {#hidden-reconciliation-key-campaign}

Le composant Clé de réconciliation masquée (Campaign) vous permet d’ajouter des champs masqués dans le cadre de la clé de réconciliation à un formulaire.

Vous pouvez configurer les éléments ci-dessous dans le composant Clé de réconciliation masquée (Campaign) :

* **Titre et texte – Nom d’élément** Par défaut, reconcilKey est proposé. Il suffit de modifier le nom d’élément lorsqu’il crée un conflit avec le nom d’un autre élément sur le formulaire. Deux champs de formulaire ne peuvent pas porter le même nom d’élément.
* **Adobe Campaign – Mappage** Associez-la à un champ de personnalisation Adobe Campaign.

L’exemple ci-dessous présente le composant Clé de réconciliation masquée (Campaign) affiché.

![chlimage_1-64](assets/chlimage_1-64.png)

### Champ numérique (Campaign) {#numeric-field-campaign}

Utilisez le champ numérique pour permettre aux destinataires de saisir des nombres, comme leur âge.

Outre les [paramètres communs à la plupart des composants Adobe Campaign](#settings-common-to-most-components), vous pouvez configurer les éléments suivants :

* **Contraintes - Liste déroulante** Contraintes Vous pouvez sélectionner -  **** Non ou  **Numérique -** pour ajouter la contrainte d&#39;un nombre ou d&#39;aucune contrainte. Si vous sélectionnez Nombre, la réponse saisie par les utilisateurs dans le champ doit être numérique.

* **Message de contrainte** De plus, vous pouvez ajouter un message de contrainte afin que les utilisateurs sachent quel format suivre pour leur réponse.
* **Style -** LargeurAjustez la largeur du champ en cliquant ou en appuyant sur les  **+** et  **** les icônes ou en entrant un nombre.

L’exemple ci-dessous présente le composant Champ numérique (Campaign), dont la largeur est configurée, affiché.

![chlimage_1-65](assets/chlimage_1-65.png)

### Champ d’option (Campaign) {#option-field-campaign}

Cette liste déroulante permet de sélectionner une option. Par exemple, le sexe ou le statut d’un destinataire.

Vous pouvez [configurer les paramètres communs à la plupart des composants Adobe Campaign](#settings-common-to-most-components) dans le composant Champ d’option (Campaign). Pour remplir la liste déroulante, sélectionnez le champ approprié dans les champs de personnalisation d’Adobe Campaign en cliquant ou en appuyant sur le symbole Adobe Campaign et en accédant au champ.

![chlimage_1-66](assets/chlimage_1-66.png)

L’exemple ci-dessous présente le composant Champ d’option (Campaign) affiché.

![chlimage_1-67](assets/chlimage_1-67.png)

### Liste de contrôle d’abonnements (Campaign) {#subscriptions-checklist-campaign}

Utilisez le composant **Liste de contrôle d’abonnements (Campaign)** pour modifier les abonnements associés à un profil Adobe Campaign.

Lorsque vous ajoutez ce composant à un formulaire, il affiche tous les abonnements disponibles sous forme de cases à cocher et permet à l’utilisateur de sélectionner les abonnements souhaités. Lorsque les utilisateurs envoient le formulaire, ce composant abonne l’utilisateur ou le désabonne des services sélectionnés en fonction du type d’action de formulaire (**Adobe Campaign: Abonnez-vous à Services** ou **Adobe Campaign : Désabonnez-vous des Services**).

>[!NOTE]
>
>Le composant ne vérifie pas les services auxquels l’utilisateur est déjà abonné/dont il est désabonné.

Vous pouvez [configurer les paramètres communs à la plupart des composants Adobe Campaign](#settings-common-to-most-components) dans le composant Liste de contrôle d’abonnements (Campaign). (Il n’y a pas de configuration Adobe Campaign disponible pour ce composant.)

L’exemple ci-dessous présente le composant Liste de contrôle d’abonnements (Campaign) affiché.

![chlimage_1-68](assets/chlimage_1-68.png)

### Champ de texte (Campaign) {#text-field-campaign}

Le composant Champ de texte (Campaign) qui vous permet de saisir des données de type chaîne, comme un prénom, un nom de famille, une adresse, une adresse électronique, etc.

Outre les [paramètres communs à la plupart des composants Adobe Campaign](#settings-common-to-most-components), vous pouvez configurer les éléments suivants :

* **Contraintes - Liste déroulante** Contraintes Vous pouvez sélectionner -  **Aucun,** **Courriel** ou  **Nom**  (sans nombre) - pour ajouter la contrainte d&#39;une adresse électronique, d&#39;un nom ou d&#39;une contrainte. Si vous sélectionnez l’option Courrier électronique, la réponse saisie par les utilisateurs dans le champ doit correspondre à une adresse électronique. Si vous sélectionnez Nom, il doit s’agit d’un nom (les trémas ne sont pas autorisés).

* **Message de contrainte** De plus, vous pouvez ajouter un message de contrainte afin que les utilisateurs sachent quel format suivre pour leur réponse.
* **Style -** LargeurAjustez la largeur du champ en cliquant ou en appuyant sur les  **+** et  **** les icônes ou en entrant un nombre.

L’exemple ci-dessous présente le composant Champ de texte (Campaign) affiché.

![chlimage_1-69](assets/chlimage_1-69.png)

