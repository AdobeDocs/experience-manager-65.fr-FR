---
title: Préparation et envoi d’une communication interactive à l’aide de l’interface utilisateur de l’agent
seo-title: Préparation et envoi d’une communication interactive à l’aide de l’interface utilisateur de l’agent
description: L’interface utilisateur de l’agent permet aux agents de préparer et d’envoyer la communication interactive au post-traitement. L’agent apporte les modifications nécessaires dans la mesure du possible et envoie la communication interactive en post-traitement, comme un courrier électronique ou une impression.
seo-description: Préparation et envoi d’une communication interactive à l’aide de l’interface utilisateur de l’agent
uuid: d1a19b83-f630-4648-9ad2-a22374e31aa9
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 110c86ea-9bd8-4018-bfcc-ca33e6b3f3ba
translation-type: tm+mt
source-git-commit: 06335b9a85414b6b1141dd19c863dfaad0812503

---


# Préparation et envoi d’une communication interactive à l’aide de l’interface utilisateur de l’agent {#prepare-and-send-interactive-communication-using-the-agent-ui}

L’interface utilisateur de l’agent permet aux agents de préparer et d’envoyer la communication interactive au post-traitement. L’agent apporte les modifications nécessaires dans la mesure du possible et envoie la communication interactive en post-traitement, comme un courrier électronique ou une impression.

## Présentation {#overview}

Après la création d’une communication interactive, l’agent peut ouvrir la communication interactive dans l’interface utilisateur de l’agent et préparer une copie spécifique au destinataire en saisissant des données et en gérant le contenu et les pièces jointes. Enfin, l’agent peut envoyer la communication interactive à un post-processus.

Lors de la préparation de la communication interactive à l’aide de l’interface utilisateur de l’agent, l’agent gère les aspects suivants de la communication interactive dans l’interface utilisateur de l’agent avant de l’envoyer à un post-processus :

* **Données** : l’onglet Données de l’interface utilisateur de l’agent affiche toutes les variables modifiables par l’agent et les propriétés du modèle de données du formulaire non verrouillées dans la communication interactive. Ces variables/propriétés sont créées lors de la modification ou de la création de fragments de documents inclus dans la communication interactive. L’onglet Données comprend également tous les champs intégrés dans le modèle de canal d’impression/XDP. L’onglet Données s’affiche uniquement lorsqu’il existe dans Interactive Communication des variables, des propriétés de modèle de données de formulaire ou des champs modifiables par l’agent.
* **Contenu** : dans l’onglet Contenu, l’agent gère le contenu, tel que des fragments de documents et des variables de contenu dans la communication interactive. L’agent peut apporter les modifications dans le fragment de document comme autorisé lors de la création de la communication interactive dans les propriétés de ces fragments de document. L’agent peut également réorganiser, ajouter/supprimer un fragment de document et ajouter des sauts de page, si cela est autorisé.
* **Pièces jointes**: L’onglet Pièces jointes apparaît dans l’interface utilisateur de l’agent uniquement si la communication interactive comporte des pièces jointes ou si l’agent a accès à la bibliothèque. L’agent peut être autorisé ou non à modifier les pièces jointes.

## Prepare Interactive Communication using the Agent UI {#prepare-interactive-communication-using-the-agent-ui}

1. Sélectionnez **[!UICONTROL Formulaires]** > **[!UICONTROL Formulaires et documents]**.
1. Select the appropriate Interactive Communication and tap **[!UICONTROL Open Agent UI]**.

   >[!NOTE]
   >
   >L’interface utilisateur de l’agent fonctionne uniquement si la communication interactive sélectionnée dispose d’un canal d’impression.

   ![openagentiui](assets/openagentiui.png)

   En fonction du contenu et des propriétés de la communication interactive, l’interface utilisateur de l’agent affiche les trois onglets suivants : Données, Contenu et Pièces jointes.

   ![agentuitabs](assets/agentuitabs.png)

   Procédez à la saisie des données, à la gestion du contenu et à la gestion des pièces jointes.

### Saisir des données {#enter-data}

1. Dans l’onglet Données, saisissez les données pour les variables, les propriétés du modèle de données de formulaire et les champs du modèle d’impression (XDP), selon les besoins. Fill up all the mandatory fields marked with an asterisk (&amp;ast;) to enable the **Submit** button.

   Appuyez sur une valeur de champ de données dans l’aperçu Communication interactive pour mettre en surbrillance le champ de données correspondant dans l’onglet Données ou vice versa.

### Gérer le contenu {#manage-content}

Dans l’onglet Contenu, vous pouvez gérer du contenu, tel que des fragments de documents et des variables de contenu dans la communication interactive.

1. Sélectionnez **[!UICONTROL Contenu]**. L’onglet Contenu de la communication interactive s’affiche.

   ![agentuicontenttab](assets/agentuicontenttab.png)

1. Modifiez les fragments de document, selon les besoins, dans l’onglet Contenu. Pour mettre l’accent sur le fragment approprié dans la hiérarchie du contenu, vous pouvez soit appuyer sur la ligne ou le paragraphe approprié dans l’aperçu de la communication interactive, soit appuyer directement sur le fragment dans la hiérarchie Contenu.

   Par exemple, le fragment de document avec la ligne « Effectuer un paiement en ligne dès maintenant… » est sélectionné dans l’aperçu du graphique ci-dessous et le même fragment de document est sélectionné dans l’onglet Contenu.

   ![contentmodulefocus](assets/contentmodulefocus.png)

   In the Content or Data tab, by tapping Highlight Selected Modules In Content ( ![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png)) on upper left of the preview, you can disable or enable functionality to go to the document fragment when the relevant text, paragraph, or data field is tapped/selected in the preview.

   The fragments that are allowed to be edited by the agent while creating the Interactive Communication have the Edit Selected Content ( ![iconeditselectedcontent](assets/iconeditselectedcontent.png)) icon. Appuyez sur l’icône Modifier le contenu sélectionné pour lancer le fragment en mode édition et y apporter des modifications. Utilisez les options suivantes pour formater et gérer le texte :

   * [Options de mise en forme](#formattingtext)

      * [Copier-coller du texte formaté depuis d’autres applications](#pasteformattedtext)
      * [Parties du texte en surbrillance](#highlightemphasize)
   * [Caractères spéciaux](#specialcharacters)
   * [Raccourcis clavier](/help/forms/using/keyboard-shortcuts.md)
   For more information on the actions available for various document fragments in the Agent user interface, see [Actions and info available in the Agent user interface](#actionsagentui).

1. To add a page break to the print output of the Interactive Communication, place the cursor where you want to insert a page break and select Page Break Before or Page Break After ( ![pagebreakbeforeafter](assets/pagebreakbeforeafter.png)).

   Un espace réservé explicite de saut de page est inséré dans la communication interactive. Pour voir comment un saut de page explicite affecte la communication interactive, reportez-vous à l’aperçu avant impression.

   ![explicitpagebreak](assets/explicitpagebreak.png)

   Procédez à la gestion des pièces jointes de la communication interactive.

### Gestion des pièces jointes {#manage-attachments}

1. Select **[!UICONTROL Attachment]**. L’interface utilisateur de l’agent affiche les pièces jointes disponibles de la manière dont elles ont été configurées lors de la création de la communication interactive.

   Vous pouvez choisir de ne pas envoyer une pièce jointe avec la communication interactive en appuyant sur l’icône d’affichage et appuyer sur la croix de la pièce jointe pour la supprimer (si l’agent est autorisé à supprimer ou à masquer la pièce jointe) de la communication interactive. Pour les pièces jointes spécifiées comme obligatoires, lors de la création de la communication interactive, les icônes Afficher et Supprimer sont désactivées.

   ![attachmentsagentui](assets/attachmentsagentui.png)

1. Tap the Library Access ( ![libraryaccess](assets/libraryaccess.png)) icon to access Content Library to insert DAM assets as attachments.

   >[!NOTE]
   >
   >L’icône Accès à la bibliothèque est disponible uniquement si l’accès à la bibliothèque a été activé lors de la création de la communication interactive (dans les propriétés du conteneur de documents du canal d’impression).

1. Si l’ordre des pièces jointes n’a pas été verrouillé lors de la création de la communication interactive, vous pouvez réorganiser les pièces jointes en sélectionnant une pièce jointe et en appuyant sur les flèches haut et bas.
1. Utilisez Aperçu web et Aperçu avant impression pour voir si les deux sorties sont conformes à vos besoins.

   If you find the previews to be satisfactory, tap **[!UICONTROL Submit]** to submit/send the Interactive Communication to a post process. Pour apporter des modifications, quittez l’aperçu pour revenir à l’étape d’apport des modifications.

## Formatage du texte {#formattingtext}

Lors de l’édition d’un fragment de texte dans l’interface utilisateur de l’agent, la barre d’outils change en fonction du type d’édition que vous choisissez d’effectuer (Police, Paragraphe ou Liste) :

![typeofformattinbarre d’outils](assets/typeofformattingtoolbar.png) de la barre d’outils ![Police](do-not-localize/fonttoolbar.png)

Barre d’outils de la police

![Barre d’outils Paragraphe](do-not-localize/paragraphtoolbar.png)

Barre d’outils Paragraphe

![Barre d’outils de la liste](do-not-localize/listtoolbar.png)

Barre d’outils de la liste

### Mettre des parties de texte en surbrillance/en évidence {#highlightemphasize}

Pour mettre des parties de texte en surbrillance\en évidence dans un fragment modifiable, sélectionnez le texte et appuyez sur Couleur de surbrillance.

![surlignextagentui](assets/highlighttextagentui.png)

### Coller le texte formaté {#pasteformattedtext}

![texte collé](assets/pastedtext.png)

### Insérer des caractères spéciaux dans le texte {#specialcharacters}

L’interface utilisateur de l’agent offre une prise en charge intégrée de 210 caractères spéciaux. The admin can [add support for more/custom special characters by customization](/help/forms/using/custom-special-characters.md).

#### Livraison des pièces jointes {#attachmentdelivery}

* Lorsque la communication interactive est générée à l’aide d’API côté serveur sous forme de PDF interactif ou non interactif, le PDF rendu contient des pièces jointes au format PDF.
* Lorsqu’un post-processus associé à une communication interactive est chargé dans le cadre de l’interface utilisateur d’envoi à l’aide de l’agent, les pièces jointes sont transmises en tant que paramètre List&lt;com.adobe.idp.Document> inAttachmentDocs.
* Les processus du mécanisme de livraison, tels que l’envoi par courrier électronique et l’impression, livrent les pièces jointes avec la version PDF de la communication interactive.

## Actions et informations disponibles dans l’interface utilisateur de l’agent {#actionsagentui}

### Fragments de document {#document-fragments}

![](do-not-localize/contentoptionsdocfragments.png)

* **Flèches haut/bas** : flèches permettant de déplacer les fragments de document vers le haut ou vers le bas dans la communication interactive.
* **Supprimer** : si cela est autorisé, supprimez le fragment de document de la communication interactive.
* **Saut de page avant** (applicable aux modules enfant de la zone cible) : insère un saut de page avant le fragment de document.
* **Retrait** : augmente ou réduit le retrait d’un fragment de document.
* **Saut de page après** (applicable pour les fragments enfants de la zone cible) : Insère un saut de page après le fragment de document.

![docfragoptions](assets/docfragoptions.png)

* Modification (fragments de texte uniquement) : ouvrez l’éditeur de texte enrichi pour modifier le fragment de document texte. Pour plus d’informations, voir [Formatage de texte](#formattingtext).

* Sélection (icône représentant un œil) : inclut\exclut le fragment de document de la communication interactive.
* Valeurs vides (information) : indique le nombre de variables vides dans le fragment de document.

### Fragments de document de la liste {#list-document-fragments}

![listoptions](assets/listoptions.png)

* Insertion d’une ligne vide : permet d’insérer une nouvelle ligne vide.
* Sélection (icône représentant un œil) : inclut\exclut le fragment de document de la communication interactive.
* Ignorer les puces/numérotations : permet d’ignorer les puces/numéros dans le fragment de document de la liste.
* Valeurs vides (information) : indique le nombre de variables vides dans le fragment de document.

