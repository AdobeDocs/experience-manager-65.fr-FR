---
title: Composants d’Adobe Campaign
seo-title: Composants d’Adobe Campaign
description: Lorsque vous procédez à l’intégration à Adobe Campaign, des composants sont disponibles pour l’utilisation de newsletters et de formulaires.
seo-description: Lorsque vous procédez à l’intégration à Adobe Campaign, des composants sont disponibles pour l’utilisation de newsletters et de formulaires.
uuid: cc9417c9-4cc1-4554-858e-2ecd682dc92f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 5afe864d-5794-4ffa-99e7-a3233f982aff
docset: aem65
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4
workflow-type: tm+mt
source-wordcount: '2555'
ht-degree: 81%

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

![chlimage_1-81](assets/chlimage_1-81.png)

### Titre (Campaign) {#heading-campaign}

Le composant Titre permet d’afficher les éléments suivants :

* Nom de la page actuelle (lorsque le champ **Titre** est vide)
* Texte spécifié dans le champ **Titre**

Vous modifiez directement le composant **Titre (Campaign)**. Laissez ce champ vide pour utiliser le titre de la page.

![chlimage_1-82](assets/chlimage_1-82.png)

Vous pouvez configurer les éléments suivants :

* **Titre**
Si vous souhaitez utiliser un autre nom que le titre de la page, saisissez-le ici.

* **Niveau de titre (1, 2, 3, 4)** Niveau de titre d’après la catégorie de titre HTML 1-4.

L’exemple ci-dessous présente le composant Titre (Campaign) affiché.

![chlimage_1-83](assets/chlimage_1-83.png)

### Image (Campaign) {#image-campaign}

Le composant Image (Campaign) affiche une image et le texte qui l’accompagne selon les paramètres spécifiés.

Vous pouvez charger une image, puis la modifier et la manipuler (par exemple, la recadrer, la faire pivoter ou y ajouter un lien/titre/texte).

Vous pouvez charger une image, puis la modifier et la manipuler (par exemple, la recadrer, la faire pivoter ou y ajouter un lien/titre/texte). Vous pouvez faire glisser et déposer une image à partir de l’[Outil de recherche de contenu](/help/sites-authoring/author-environment-tools.md#thecontentfinderclassicui) directement sur le composant ou sa boîte de dialogue d’édition. Vous pouvez également double-cliquer dans la zone centrale de la boîte de dialogue d’édition pour parcourir votre système de fichiers local et charger une image. Les deux onglets de la boîte de dialogue d’édition contrôlent également toutes les définitions, ainsi que la manipulation de l’image :

![chlimage_1-84](assets/chlimage_1-84.png)

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

![chlimage_1-85](assets/chlimage_1-85.png)

### Lien (Campaign) {#link-campaign}

Le composant Lien (Campaign) permet d’ajouter un lien à votre newsletter. Ce composant n’est disponible que dans l’interface utilisateur classique, mais vous pouvez en ajouter un à l’interface utilisateur optimisée pour les écrans tactiles et l’ouvrir en mode de compatibilité.

![chlimage_1-86](assets/chlimage_1-86.png)

Vous pouvez configurer les éléments ci-dessous sur les onglets **Affichage**, **Informations d’URL** ou **Avancé** :

* **Légende du lien** Légende du lien. Il s’agit du texte que les utilisateurs voient.

* **Info-bulle du lien** Ajoute des informations supplémentaires sur l’utilisation du lien.

* **Type de lien** Dans la liste déroulante, sélectionnez entre un 
**URL** personnalisée et Document **** adaptatif. Ce champ est obligatoire. Si vous sélectionnez l’URL personnalisée, vous pouvez indiquer l’URL du lien. Si vous sélectionnez Document adaptatif, vous pouvez préciser le chemin d’accès au document.

* **Paramètre d’URL supplémentaire** Ajoutez des paramètres d’URL supplémentaires. Cliquez sur Ajouter un élément pour ajouter plusieurs éléments.

>[!NOTE]
>
>You must enter information in the **Link Type** field in the **URL Info** tab, or the component cannot save and you see the following error message:
>
>`Validation failed. Verify the values of the marked fields.`


L’exemple ci-dessous présente le composant Lien (Campaign) affiché.

![chlimage_1-87](assets/chlimage_1-87.png)

### Référence ciblée (Campaign) {#targeted-reference-campaign}

Le composant Référence ciblée (Campaign) permet de créer une référence à un paragraphe ciblé.

Dans ce composant, vous accédez au paragraphe ciblé pour le sélectionner.

Cliquez sur le menu déroulant pour accéder au paragraphe à référencer. Une fois que vous avez terminé, cliquez sur **OK**.

### Texte et image (Campaign) {#text-image-campaign}

Le composant Texte et image (Campaign) permet d’ajouter un bloc de texte et une image.

![chlimage_1-88](assets/chlimage_1-88.png)

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

![chlimage_1-89](assets/chlimage_1-89.png)

### Texte et personnalisation (Campaign) {#text-personalization-campaign}

The Text &amp; Personalization (Campaign) component lets you enter a text block using a WYSIWYG editor, with functionality provided by the [Rich Text editor](/help/sites-authoring/rich-text-editor.md). De plus, ce composant permet d’utiliser des champs de contexte et des blocs de personnalisation, disponibles dans Adobe Campaign. Reportez-vous également à la section [Insertion d’une personnalisation](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#inserting-personalization).

Une série d’icônes permet de mettre en forme le texte (attributs de police, alignement, liens, listes et retrait).

Ajoutez du texte comme vous le feriez normalement dans l’éditeur de texte enrichi. Ajoutez la personnalisation en la sélectionnant dans la liste déroulante Adobe Campaign et en sélectionnant les champs en fonction de vos besoins.

![chlimage_1-90](assets/chlimage_1-90.png)

Vous ajoutez des champs de texte et de contexte ou des blocs de personnalisation pour créer du contenu. Ensuite, sélectionnez ClientContext pour tester les données dans les profils du persona. Après avoir sélectionné un persona, les champs de personnalisation sont remplacés automatiquement par les données du profil sélectionné.

>[!NOTE]
>
>Seuls les champs définis dans le schéma **nms:seedMember** ou l’une de ses extensions sont pris en compte. Les attributs des tables liés à `nms:seedMember` ne sont pas disponibles.

## Composants Formulaire d’Adobe Campaign {#adobe-campaign-form-components}

Vous utilisez des composants Adobe Campaign pour créer un formulaire que les utilisateurs remplissent pour s’abonner à une newsletter, s’en désabonner ou mettre à jour leur profil utilisateur. Pour plus d’informations, reportez-vous à la section [Création de formulaires Adobe Campaign](/help/sites-classic-ui-authoring/classic-personalization-ac-forms.md).

Chaque champ d’un composant peut être associé à un champ de base de données Adobe Campaign. Les champs disponibles varient selon le type de données qu’ils contiennent, comme indiqué dans la section [Composants et type de données](#components-and-data-type). Si vous étendez le schéma de destinataire dans Adobe Campaign, les nouveaux champs sont disponibles dans les composants dont les types de données concordent.

When you open a form that is configured to integrate with Adobe Campaign, you see the following components in the **Adobe Campaign** section:

* Case à cocher (Campaign)
* Champ de date (Campaign) et champ de date/HTML5 (Campaign)
* Clé primaire chiffrée (Campaign)
* Affichage d’erreur (campagne)
* Clé de réconciliation masquée (Campaign)
* Champ numérique (Campaign)
* Champ d’option (Campaign)
* Liste de contrôle d’abonnements (Campaign)
* Champ de texte (Campaign)

Cette section décrit en détail chaque composant.

### Composants et type de données {#components-and-data-type}

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

### Paramètres communs à la plupart des composants {#settings-common-to-most-components}

Les composants Adobe Campaign possèdent des paramètres communs à tous les composants (à l’exception des composants Clé primaire chiffrée et Clé de rapprochement masquée).

Dans la plupart des composants, vous pouvez configurer les éléments suivants :

#### Titre et texte {#title-and-text}

* **Titre** 
Si vous souhaitez utiliser un autre nom que le nom de l’élément, saisissez-le ici.

* **Masquer le titre** Cochez cette case si vous ne voulez pas afficher le titre.

* **Description** Ajoutez une description dans le champ pour indiquer des informations supplémentaires pour les utilisateurs.

* **N’afficher que la valeur** Affiche uniquement la valeur, le cas échéant.

#### Adobe Campaign {#adobe-campaign}

Vous pouvez configurer les éléments suivants :

* **Correspondance** Sélectionnez un champ de personnalisation Adobe Campaign, si cela est approprié.

* **Clé de réconciliation** Cochez cette case si ce champ fait partie de la clé de réconciliation.

#### Contraintes {#constraints}

* **Obligatoire** - Cochez cette case pour que ce composant soit requis ; autrement dit, les utilisateurs doivent saisir une valeur.
* **Message** obligatoire - Ajoutez éventuellement un message indiquant que le champ est requis.

#### Style {#styling}

* **CSS** Indiquez les classes CSS à utiliser pour ce composant.

### Case à cocher (Campaign) {#checkbox-campaign}

Le composant Case à cocher (Campaign) permet à l’utilisateur de modifier les champs de profil Adobe Campaign de type données booléennes. Par exemple, vous pouvez créer un composant Case à cocher (Campaign) qui permet au destinataire d’indiquer qu’il ne souhaite être contacté par aucun canal.

Vous pouvez [configurer les paramètres communs à la plupart des composants Adobe Campaign](#settings-common-to-most-components) dans le composant Case à cocher (Campaign).

L’exemple ci-dessous présente le composant Case à cocher (Campaign) affiché.

![chlimage_1-91](assets/chlimage_1-91.png)

### Champ de date (Campaign) et champ de date/HTML5 (Campaign) {#date-field-campaign-and-date-field-html-campaign}

Utilisez le champ de date pour permettre aux destinataires d’indiquer une date. Par exemple, vous souhaitez peut-être que les destinataires indiquent leur date de naissance. Le format de date correspond au format utilisé dans votre instance Adobe Campaign.

Outre les [paramètres communs à la plupart des composants Adobe Campaign](#settings-common-to-most-components), vous pouvez configurer les éléments suivants :

* **Constraints - Constraint** - You can select - **None** or **Date** to add the constraint of a date or no constraint. Si vous sélectionnez la date, la réponse que les utilisateurs renseignent dans le champ doit correspondre à un format de date.

* **Message** de contrainte : vous pouvez en outre ajouter un message de contrainte afin que les utilisateurs sachent comment formater correctement leurs réponses.
* **Style - Largeur** - Ajustez la largeur du champ en cliquant ou en appuyant sur les icônes **+** et **-** ou en entrant un nombre.

L’exemple ci-dessous présente le composant Champ de date (Campaign), dont la largeur ajustée, affiché.

![chlimage_1-92](assets/chlimage_1-92.png)

### Clé primaire chiffrée (Campaign) {#encrypted-primary-key-campaign}

Ce composant définit le nom du paramètre d’URL qui contient l’identifiant d’un profil Adobe Campaign (**Identifiant de ressource principal** ou **Clé primaire chiffrée** respectivement dans Adobe Campaign Standard et Adobe Campaign 6.1).

Chaque formulaire affichant et modifiant des données de profil Adobe Campaign **doit** comporter un composant Clé primaire chiffrée.

Vous pouvez configurer les éléments ci-dessous dans le composant Clé primaire chiffrée (Campaign) :

* **Titre et texte - Nom** de l’élément - Valeur par défaut de encryptedPK. Il suffit de modifier le nom d’élément lorsqu’il crée un conflit avec le nom d’un autre élément sur le formulaire. Deux champs de formulaire ne peuvent pas porter le même nom d’élément.
* **Adobe Campaign - Paramètre** d&#39;URL - Ajoutez le paramètre d&#39;URL pour l&#39;EPK. Par exemple, vous pouvez utiliser la valeur **epk**.

L’exemple ci-dessous présente le composant Clé primaire chiffrée (Campaign) affiché.

![chlimage_1-93](assets/chlimage_1-93.png)

### Affichage d’erreur (campagne) {#error-display-campaign}

Ce composant permet d’afficher les erreurs du système principal. La gestion des erreurs du formulaire doit être définie vers l’avant pour que le composant fonctionne correctement.

L’exemple ci-dessous présente le composant Affichage d’une erreur (Campaign) affiché.

![chlimage_1-94](assets/chlimage_1-94.png)

### Clé de réconciliation masquée (Campaign) {#hidden-reconciliation-key-campaign}

Le composant Clé de réconciliation masquée (Campaign) vous permet d’ajouter des champs masqués dans le cadre de la clé de réconciliation à un formulaire.

Vous pouvez configurer les éléments ci-dessous dans le composant Clé de réconciliation masquée (Campaign) :

* **Titre et texte - Nom** de l’élément - Par défaut, reconcilKey. Il suffit de modifier le nom d’élément lorsqu’il crée un conflit avec le nom d’un autre élément sur le formulaire. Deux champs de formulaire ne peuvent pas porter le même nom d’élément.
* **Adobe Campaign - Mappage** - Associer à un champ de personnalisation Adobe Campaign.

L’exemple ci-dessous présente le composant Clé de réconciliation masquée (Campaign) affiché.

![chlimage_1-95](assets/chlimage_1-95.png)

### Champ numérique (Campaign) {#numeric-field-campaign}

Utilisez le champ numérique pour permettre aux destinataires de saisir des nombres, comme leur âge.

Outre les [paramètres communs à la plupart des composants Adobe Campaign](#settings-common-to-most-components), vous pouvez configurer les éléments suivants :

* **Contraintes - Liste déroulante Contrainte** Vous pouvez sélectionner - **Aucun** ou **** Numérique - pour ajouter la contrainte d&#39;un nombre ou d&#39;aucune contrainte. Si vous sélectionnez Nombre, la réponse saisie par les utilisateurs dans le champ doit être numérique.

* **Message** de contrainte : vous pouvez en outre ajouter un message de contrainte afin que les utilisateurs sachent comment formater correctement leurs réponses.
* **Style - Largeur** - Ajustez la largeur du champ en cliquant ou en appuyant sur les icônes **+** et **-** ou en entrant un nombre.

L’exemple ci-dessous présente le composant Champ numérique (Campaign), dont la largeur est configurée, affiché.

![chlimage_1-96](assets/chlimage_1-96.png)

### Champ d’option (Campaign) {#option-field-campaign}

Cette liste déroulante permet de sélectionner une option. Par exemple, le sexe ou le statut d’un destinataire.

Vous pouvez [configurer les paramètres communs à la plupart des composants Adobe Campaign](#settings-common-to-most-components) dans le composant Champ d’option (Campaign). Pour remplir la liste déroulante, sélectionnez le champ approprié dans les champs de personnalisation d’Adobe Campaign en cliquant ou en appuyant sur le symbole Adobe Campaign et en accédant au champ.

L’exemple ci-dessous présente le composant Champ d’option (Campaign) affiché.

![chlimage_1-97](assets/chlimage_1-97.png)

### Liste de contrôle d’abonnements (Campaign) {#subscriptions-checklist-campaign}

Utilisez le composant **Liste de contrôle d’abonnements (Campaign)** pour modifier les abonnements associés à un profil Adobe Campaign.

Lorsque vous ajoutez ce composant à un formulaire, il affiche tous les abonnements disponibles sous forme de cases à cocher et permet à l’utilisateur de sélectionner les abonnements souhaités. When users submit the form, this component subscribes the user to or unsubscribes the user from the selected services depending on the form action type (**Adobe Campaign: Subscribe to Services** or **Adobe Campaign: Unsubscribe from Services**).

>[!NOTE]
>
>Le composant ne vérifie pas les services auxquels l’utilisateur est déjà abonné/dont il est désabonné.

Vous pouvez [configurer les paramètres communs à la plupart des composants Adobe Campaign](#settings-common-to-most-components) dans le composant Liste de contrôle d’abonnements (Campaign). (Il n’y a pas de configuration Adobe Campaign disponible pour ce composant.)

L’exemple ci-dessous présente le composant Liste de contrôle d’abonnements (Campaign) affiché.

![chlimage_1-98](assets/chlimage_1-98.png)

### Champ de texte (Campaign) {#text-field-campaign}

Le composant Champ de texte (Campaign) qui vous permet de saisir des données de type chaîne, comme un prénom, un nom de famille, une adresse, une adresse électronique, etc.

Outre les [paramètres communs à la plupart des composants Adobe Campaign](#settings-common-to-most-components), vous pouvez configurer les éléments suivants :

* **Contraintes - Contrainte** - Liste déroulante - Vous pouvez sélectionner **Aucun**, **E-mail**, **Nom** (sans nombre) pour ajouter la contrainte d&#39;une adresse électronique, d&#39;un nom ou d&#39;une aucune contrainte. Si vous sélectionnez l’option Courrier électronique, la réponse saisie par les utilisateurs dans le champ doit correspondre à une adresse électronique. Si vous sélectionnez Nom, il doit s’agit d’un nom (les trémas ne sont pas autorisés).

* **Message** de contrainte : vous pouvez en outre ajouter un message de contrainte afin que les utilisateurs sachent comment formater correctement leurs réponses.
* **Style - Largeur** - Ajustez la largeur du champ en cliquant ou en appuyant sur les icônes **+** et **-** ou en entrant un nombre.

L’exemple ci-dessous présente le composant Champ de texte (Campaign) affiché.

![chlimage_1-99](assets/chlimage_1-99.png)
