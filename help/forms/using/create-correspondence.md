---
title: Création de correspondance
seo-title: Création de correspondance
description: Après la création d’un modèle de lettre, vous pouvez l’utiliser pour créer une correspondance dans AEM Forms en gérant les données, le contenu et les pièces jointes.
seo-description: Après la création d’un modèle de lettre, vous pouvez l’utiliser pour créer une correspondance dans AEM Forms en gérant les données, le contenu et les pièces jointes.
uuid: 48cf2b26-c9b4-4127-9ea0-1b36addbff60
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 87742cb2-357b-421f-b79d-e355887ddec0
docset: aem65
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# Création de correspondance{#create-correspondence}

## Créez une correspondance dans l’interface utilisateur Création de correspondance {#create-correspondence-in-the-create-correspondence-user-interface}

After a [letter template is created in Correspondence Management](../../forms/using/create-letter.md), the end user/agent/claim adjustor can open the letter in the Create Correspondence user interface and create a correspondence by entering data, setting up content, and managing attachments. Enfin, l’agent ou l’expert en assurance peut gérer le contenu en mode Aperçu et envoyer la lettre.

### Afficher l’aperçu d’une correspondance {#preview-a-correspondence}

Sélectionnez la lettre à prévisualiser en procédant comme suit :

1. On the Letters page, tap **Select**.
1. Sélectionnez la lettre appropriée en appuyant dessus.

   ![Sélectionner une lettre](assets/1_selectletter.png)

   Sélectionner une lettre

1. For a Data Dictionary based letter, select **Preview** > **Preview**. Ou pour une lettre qui n’est pas basée sur un dictionnaire de données, sélectionnez **Aperçu**. Vous pouvez également survoler une lettre (sans la sélectionner) et appuyer sur l’icône d’aperçu de la lettre pour la prévisualiser.

   >[!NOTE]
   >
   >Si aucun dictionnaire de données n’est associé à la lettre, l’aperçu de la lettre s’affiche. Dans le cas contraire, si la lettre est basée sur un dictionnaire de données, Correspondence Management affiche les options  et personnalisées dans le menu  du et vous pouvez sélectionner l’une des deux options. Vous pouvez également associer des données de test à un dictionnaire de données. When the [Data Dictionary has associated test data](../../forms/using/data-dictionary.md#p-working-with-test-data-p), then on selecting the preview option, the normal preview opens with the test data populated.

1. Pour pouvoir générer une correspondance lors de sa prévisualisation, vous devez être administrateur ou faire partie d’un des groupes suivants :

   * forms-users (pour prévisualiser sur instance d’auteur)
   * cm-agent-users (pour le rendu sur une instance de publication)
   Si vous ne disposez pas des autorisations requises, contactez votre administrateur pour obtenir des droits d’accès appropriés. For more information on creating and adding users to groups, see [Adding Users or Groups to a Group](/help/sites-administering/security.md). Si vous tentez de générer une correspondance sans disposer des autorisations appropriées, la page d’erreur 404 s’affiche.

1. Si vous avez sélectionné **Aperçu**> **Personnalisation**, une boîte de dialogue s&#39;ouvre. In the dialog, select a data file, corresponding to the data dictionary, to preview the letter with and then select **Preview**. Un fichier de données est créé à partir d’un dictionnaire de données pour une lettre particulière. For more information on the data file, see [Data Dictionary](../../forms/using/data-dictionary.md#p-working-with-test-data-p).

   ![Aperçu de la lettre](assets/8_previewcustomdatafile.png)

1. L’aperçu HTML de la lettre (aperçu de formulaires mobiles) s’ouvre sur l’onglet Données actif par défaut.

   For more information on mobile forms and the features they support, see [Feature differentiation between Mobile Forms and PDF Forms](https://helpx.adobe.com/fr/livecycle/help/mobile-forms/feature-differentiation-mobile-forms-pdf.html).

   Il existe trois onglets : données, contenu et pièces jointes. S’il n’existe pas d’éléments de données (variables d’espace réservé et champs de mise en page), la lettre s’ouvre alors directement dans l’onglet Contenu. L’onglet de pièces jointes est disponible uniquement lorsque des pièces jointes sont présentes ou que l’accès à la bibliothèque est activé.

   >[!NOTE]

   >For more information on switching between HTML or PDF rendition mode of letter preview, see [Change rendition mode of letter](#changerenditionmode). For more information on PDF support in Correspondence Management and AEM, see [Discontinuation of NPAPI browser plug-ins and its impact](https://helpx.adobe.com/fr/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html) and [PDF Forms to HTML5 Forms](https://helpx.adobe.com/fr/aem-forms/kb/pdf-forms-to-html5-forms.html).

### Saisir des données {#enterdata}

Sous l’onglet Données, renseignez les champs de mise en page et les espaces réservés disponibles.

1. Entrez les données et les variables de contenu dans les champs requis. Fill up all the mandatory fields marked with an asterisk (*) to enable the **Submit** button.

   Appuyez sur une valeur de champ de données dans l’aperçu de lettre HTML pour mettre en surbrillance le champ de données correspondant dans l’onglet Données.

   ![Saisir des données dans la lettre](assets/2_enterdata.png) ![2_1_entdata](assets/2_1_enterdata.png)

### Gérer le contenu {#managecontent}

Dans l’onglet Contenu, vous pouvez gérer du contenu tel que des fragments de documents et des variables de contenu dans la lettre.

1. Sélectionnez **Contenu**. Correspondence Management affiche l’onglet de contenu de la lettre.

   ![Onglet Contenu - mettre en surbrillance le module dans le contenu](assets/3_content.png)

1. Modifiez les modules de contenu, selon les besoins, dans l’onglet Contenu. Pour centrer l’attention sur le module de contenu approprié dans la hiérarchie des contenus, vous pouvez appuyer sur la ligne ou le paragraphe approprié dans l’aperçu de la lettre ou appuyer sur le module de contenu directement dans la hiérarchie Contenu.

   Par exemple, la ligne « Nous avons passé en revue… » est choisie dans le graphique ci-dessous et le module de contenu approprié est choisi dans l’onglet Contenu.

   ![4_surligntmoduleincontent](assets/4_highlightmoduleincontent.png)

   In the Content or Data tab, by tapping Highlight Selected Modules ( ![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png)) on upper left of the HTML letter preview, you can disable or enable functionality to go to the content/data module when the relevant text, paragraph, or data field is selected in the letter preview.

   For more information on the actions available for various modules in the Create Correspondence user interface, see [Actions and info available in the Create Correspondence user interface](#actions-and-info-available-in-the-create-correspondence-content-tab).

1. Pour localiser plusieurs modules de contenu, utilisez le champ Rechercher. Saisissez tout ou partie du nom ou titre du module de contenu pour le rechercher dans la correspondance.
1. Tap the Display icon ( ![display](assets/display.png)) in front of a list, text, condition, or target area to show or hide it in the letter.
1. To edit an inline or editable text module, tap the relevant **Edit** icon ( ![edittextmodule](assets/edittextmodule.png)) or double-click the relevant text module in the letter preview.

   Le système affiche un éditeur de texte pour modifier et formater le texte.

   Le vérificateur orthographique par défaut dans les vérifications orthographiques des navigateurs dans l’éditeur de texte. Pour gérer les vérifications d’orthographe et de grammaire, vous pouvez modifier les paramètres du vérificateur orthographique de votre navigateur ou installer des modules/adjonctions externes de navigateur pour vérifier l’orthographe et la grammaire.

   Vous pouvez également utiliser les différents raccourcis clavier de l’éditeur de texte pour gérer, modifier et mettre en forme le texte. For more information on [Text Editor](/help/forms/using/keyboard-shortcuts.md#correspondence-management) keyboard shortcuts in Correspondence Management Keyboard Shortcuts.

   ![5_edittextmodule](assets/5_edittextmodule.png)

   Vous souhaiterez peut-être réutiliser un ou plusieurs paragraphes de texte existant dans une autre application de document. Vous pouvez directement copier et coller du texte, par exemple du texte issu de MS Word, de pages HTML ou de toute autre application.

   Vous pouvez copier et coller un ou plusieurs paragraphes de texte dans un module de texte modifiable. Par exemple, vous pouvez disposer d’un document MS Word contenant une liste à puces de preuves de résidence acceptables comme suit :

   ![pastetextmsword](assets/pastetextmsword.png)

   Vous pouvez directement copier et coller le texte à partir du document MS Word vers un module de texte modifiable. La mise en forme, telle que la liste à puces, la police et la couleur du texte, est conservée dans le module de texte.

   ![pastetexteditablemodule](assets/pastetexteditablemodule.png)

   >[!NOTE]
   >
   >Toutefois, la mise en forme du texte collé présente certaines [restrictions](https://helpx.adobe.com/aem-forms/kb/cm-copy-paste-text-limitations.html).

   Vous pouvez mettre le texte et les chiffres en retrait dans votre lettre à l’aide de la touche de tabulation. Par exemple, vous pouvez utiliser la touche de tabulation pour l’alignement de plusieurs colonnes de texte dans une liste dans un format tabulaire.

   ![tabspaces](assets/tabspaces.png)

   Exemple : vous pouvez utiliser la touche de tabulation pour aligner plusieurs colonnes de texte sous forme de tableau.

   >[!NOTE]
   >
   >For more information on setting up tab spacing for your text modules and letters, see [More information on using tab spacing for arranging text](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).

1. Si nécessaire, insérez des caractères spéciaux dans la correspondance. Vous pouvez, par exemple, utiliser la palette des caractères spéciaux pour insérer les caractères suivants :

   * Symboles de devise tels que €, ¥ et £
   * Symboles mathématiques tels que Δ, √, Δet ^
   * Symboles de ponctuation tels que ‟ et&quot;
   ![specialcharacters](assets/specialcharacters.png)

   Correspondence Management offre une prise en charge intégrée de 210 caractères spéciaux. The admin can [add support for more/custom special characters by customization](../../forms/using/custom-special-characters.md).

1. Pour mettre en surbrillance\mettre en évidence des parties de texte dans un module incorporé modifiable, sélectionnez le texte et appuyez sur Couleur de surbrillance.

   ![letterbackgroundcolor](assets/letterbackgroundcolor.png)

   You can either directly tap a basic color `**[A]**` present in the Basic Colors palette or tap **Select** after using the slider `**[B]**` to choose the appropriate shade of the color.

   Optionally, you can also go to the Advanced tab to select the appropriate Hue, Lightness, and Saturation `**[C]**` to create the precise color and then tap Select `**[D]**` to apply the color to highlight the text.

   ![textbackgroundcolor](assets/textbackgroundcolor.png)

1. Make the appropriate content and format changes and tap **Save**. Tap ( ![editnextmoduleccr](assets/editnextmoduleccr.png)) to move between editable text modules, or tap **Save and Next** to save the changes and move to the next editable text module.
1. Le système affiche également les variables vides pour chacune des branches. Lorsqu’il n’y a aucune variable vide, le chiffre 0 est indiqué pour les variables vides. S’il y a des variables vides, vous pouvez appuyer sur une branche pour la développer et rechercher la variable vide. Utilisez la barre d’outils de contenu pour supprimer du contenu, augmenter ou diminuer le retrait du contenu, et insérer des sauts de page avant ou après le contenu.

   Vous pouvez insérer des sauts de page au-dessus et en dessous des modules de données, même s’ils font partie de listes et de conditions.

1. Tap Open/Close Content Variable ( ![opencontentvariables](assets/opencontentvariables.png)) to open the content variables and fill them appropriately.
1. Lorsque vous renseignez la variable vide correctement, le nombre de variables vides est défini sur 0.

   Dans l’interface utilisateur Création de correspondance, le nombre de variables vides est affiché à chaque niveau de la hiérarchie de tout module qui contient au moins une variable. Si un module contient des variables vides, le nombre est affiché au niveau de la variable, du module, de la zone cible et du modèle de lettre.

   Le nombre de variables vides inclut :

   * Uniquement des variables du dictionnaire de données non protégées et d’espace réservé. Le nombre de variables n’inclut pas les variables de mise en page ou du dictionnaire de données protégées.
   * Champs obligatoires.
   * Champs de mise en page s’ils sont obligatoires et liés à l’utilisateur.
   * Uniquement les instances de variables uniques. Si un module, une zone de cible ou un modèle de lettre contient au moins deux instances de la même variable, le nombre affiché est 1 (un). Toutefois, pour chacune des instances, le nombre affiché est 1.
   Le nombre de variables vides ne comprend pas les modules non sélectionnés. Si un module est inclus dans un modèle de lettre, mais n’est pas dans la lettre, le nombre de variables vides de ce module n’est pas affiché.

   Pour la zone cible, le module et la variable, le nombre est affiché à droite de chaque objet dans le modèle de lettre. Toutefois, pour le modèle complet, le nombre s’affiche dans la barre d’état de création de correspondance.

   Les modules d’un modèle de lettre affichent le nombre de variables vides comme décrit ci-dessous :

   * **Texte** Affiche la somme des variables d’espace réservé vides uniques et des éléments de dictionnaire de données contenus dans le module de texte.
   * **Condition** Affiche la somme des variables de condition vides uniques contenues dans la condition et des variables contenues dans les modules résultants.
   * **** du Affiche la somme de toutes les variables vides uniques contenues dans les modules affectés au  du.
   * **Zone** de  Affiche la somme de toutes les variables vides uniques contenues dans les modules affectés à la zone de .
   Notez ce qui suit concernant les variables avec des valeurs par défaut :

   * Un champ de variable booléenne est défini par défaut sur *false*. Toutefois, la variable est considérée comme vide. This implies that the variable count includes all Boolean variable fields with value *false*.

   * Un champ de variable numérique est défini par défaut sur *0 (zéro)*. Toutefois, la variable est considérée comme vide. Cela signifie que le nombre de variables inclut tous les champs de variable numérique avec la valeur *0 (zéro)*.



#### Actions et informations disponibles dans l’onglet Contenu de la création de correspondance {#actions-and-info-available-in-the-create-correspondence-content-tab}

**Zone cible**

* Insertion d’une ligne vide : permet d’insérer une nouvelle ligne vide.
* Insertion de texte en ligne : permet d’insérer un nouveau module de texte.
* Verrouillage d’ordre (information) : indique que l’ordre du contenu ne peut pas être modifié.
* Valeurs vides (information) : indique le nombre de variables vides dans la zone cible.

**Module**

* Sélection (icône représentant un œil) : permet d’inclure ou d’exclure le module de la lettre.
* Ignorer les puces (applicable pour les modules de liste et leurs modules enfants) : ignore les puces dans un module particulier.
* Saut de page avant (applicable pour les modules enfants de la zone cible) : insère un saut de page avant le module.
* Saut de page après (applicable pour les modules enfants de la zone  du) : Insère un saut de page avant le module.
* Valeurs vides (information) : indique le nombre de variables vides dans la zone cible.
* Modification (modules de texte uniquement) : ouvrez l’éditeur de texte enrichi pour modifier le module de texte.
* Panneau de données (modules de texte et de condition) : permet de déverrouiller toutes les variables du module.

**Module de liste**

* Insertion d’une ligne vide : permet d’insérer une nouvelle ligne vide.
* Bibliothèque de contenu : ouvre la bibliothèque de contenu pour ajouter des modules à la liste.
* Paramètre de  (imbriqué  uniquement) :
* Verrouillage d’ordre (information) : indique que l’ordre des éléments de la liste ne peut pas être modifié.

### Gestion des pièces jointes {#manage-attachments}

1. Sélectionnez **les pièces jointes**. Correspondence Management affiche les pièces jointes disponibles, telles qu’elles sont configurées lors de la création du modèle de lettre.
1. Vous pouvez choisir de ne pas envoyer une pièce jointe avec la lettre en appuyant sur l’icône Afficher et en appuyant sur la croix dans la pièce jointe pour la supprimer de la lettre. Pour les pièces jointes spécifiées, lors de la création d’un modèle de lettre, comme étant obligatoires, les icônes Afficher et Supprimer sont désactivées.
1. Tap the Library Access ( ![libraryaccess](assets/libraryaccess.png)) icon to access Content Library to insert DAM assets as attachments.

   >[!NOTE]
   >
   >L’icône d’accès à la bibliothèque n’est disponible que si l’accès à la bibliothèque a été activé lors de la création de la lettre.

1. Si l’ordre des pièces jointes n’a pas été verrouillé lors de la création de la correspondance, vous pouvez réorganiser les pièces jointes en sélectionnant une pièce jointe et en appuyant sur les flèches montantes et descendantes.

   Pour plus d’informations, consultez [Livraison des pièces jointes](#attachmentdelivery).

### Gestion du contenu dans l’aperçu et envoi de la lettre {#manage-content-in-preview-and-submit-the-letter}

Vous pouvez effectuer des modifications relatives à la mise en page et au contenu pour vous assurer que la lettre apparaît exactement comme vous le souhaitez et l’envoyer aux différents post-processus.

1. To highlight all the editable content in the letter, tap **Highlight Editable Sections**.

   Les contenus modifiables de la lettre sont mis en surbrillance avec un arrière-plan gris.

   ![Mettre en surbrillance le contenu modifiable](assets/4_highlightmoduleincontent-1.png)

1. Modifiez les modules de contenu, selon les besoins, dans l’onglet Contenu. Pour centrer l’attention sur le module de contenu approprié dans la hiérarchie des contenus, vous pouvez appuyer sur la ligne ou le paragraphe approprié dans l’aperçu de la lettre ou appuyer sur le module de contenu directement dans la hiérarchie Contenu.

   Par exemple, la ligne « Pour accéder à… » est sélectionnée dans le graphique ci-dessous et le module de contenu correspondant est sélectionné dans l’onglet Contenu.

   By tapping Highlight Selected Modules in Content ( ![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png)), you can disable or enable functionality to highlight the content module in Content tab when the relevant text, paragraph, or data field is tapped in the letter preview.

   For more information on the actions available for various modules in the Create Correspondence user interface, see [Actions and info available in the Create Correspondence user interface](#actions-and-info-available-in-the-create-correspondence-content-tab).

1. To add a page break to the letter, tap where you want to insert a page break and select Page Break Before or Page Break After ( ![pagebreakbeforeafter](assets/pagebreakbeforeafter.png)).

   Un espace réservé explicite de saut de page est inséré dans la lettre. Pour voir comment un saut de page explicite affecte la lettre, reportez-vous à l’aperçu PDF aplati.

   >[!NOTE]
   >
   >Les formulaires mobiles ne prenant pas en charge les sauts de page, les en-têtes et les pieds de page apparaissent qu’une seule fois. En revanche, vous pouvez définir explicitement les en-têtes et pieds de page dans la mise en page (par page) pour qu’ils s’affichent dans l’aperçu des formulaires mobiles. En outre, les pages vierges dans la lettre, le cas échéant, n’apparaissent pas dans l’aperçu de formulaires pour périphériques mobiles.

   ![Saut de page explicite](assets/8_pagebreak.png)

1. Pour enregistrer la lettre en tant que brouillon, que vous pouvez continuer d’utiliser ultérieurement, appuyez sur Enregistrer en tant que brouillon. Pour utiliser cette option, votre lettre doit être[ publiée](../../forms/using/publishing-unpublishing-forms.md#publishanasset). Pour plus d’informations, voir Instance Brouillon sous [Enregistrement de brouillons et envoi d’instances de lettre](#savingdrafts).

   ![saveasdraft](assets/saveasdraft.png)

   La boîte de dialogue Nom du brouillon de la lettre s’affiche avec l’ID d’instance de lettre. Vous pouvez également modifier cet ID. Notez l’ID de lettre, puis appuyez sur **Terminer**. Vous pouvez utiliser cet ID ultérieurement pour [recharger le brouillon de la lettre](submit-letter-topostprocess.md#reloaddraft).

1. To preview the letter as a flattened PDF with the exact layout and page breaks as it will be submitted, tap ( ![preview](assets/preview.png)) Preview.

   La lettre s’affiche sous forme de fichier PDF aplati. Le fichier PDF aplati est la représentation exacte de la lettre telle qu’elle sera envoyée, avec les polices, les pauses et la mise en page appropriées de la lettre.

   >[!NOTE]
   >
   >Si vous utilisez le type de rendu Mozilla Firefox et HTML pour prévisualiser la lettre sous la forme d’un fichier PDF aplati, veillez à utiliser le module externe natif du navigateur et non le module externe d’Acrobat. Pour sélectionner le module externe natif du navigateur, accédez aux paramètres de Mozilla Firefox et, pour le type de contenu PDF, sélectionnez Aperçu dans Firefox.

1. If you find the flattened PDF preview to be satisfactory, tap **Submit** to submit the letter. Or to make changes to the letter, tap **Exit Preview** to go back to the Create Correspondence UI preview of the letter to make changes in the letter. Lorsque vous appuyez sur Envoyer, si la configuration Gestion des instances de lettre est activée sur l’instance de publication, l’instance d’envoi de lettre est générée.

   Pour plus d’informations, voir Instance Brouillon sous Enregistrement de brouillons et envoi d’instances de lettre.

   Vous pouvez également enregistrer la lettre en tant que brouillon pour apporter des modifications à la lettre ultérieurement.

   Après avoir apporté les modifications requises, vous pouvez envoyer la lettre depuis l’aperçu HTML5 ou appuyez de nouveau sur Aperçu pour revoir la sortie PDF aplati.

   For information on differences between HTML5 forms and PDF forms, see [Feature differentiation between HTML5 forms and PDF forms](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

## Enregistrement des brouillons et envoi d’instances de lettre {#savingdrafts}

Lorsqu’une lettre est générée dans l’interface utilisateur de création de correspondance, vous pouvez enregistrer la lettre comme étant en cours de consultation.

Il existe deux types d’instances de lettre pouvant être enregistrées : instance Brouillon ou instance Envoyer.

* **Instance Brouillon** : l’instance Brouillon capture l’état actuel de la lettre que vous prévisualisez. Pour enregistrer une instance Brouillon, assurez-vous d’abord que la lettre et tous les actifs auxquels la lettre fait référence sont à l’état Publié. Pour plus d’informations sur la publication d’une lettre, voir [Publication d’un actif](../../forms/using/publishing-unpublishing-forms.md#publishanasset). Vous devez publier une lettre avant de pouvoir l’enregistrer en tant que brouillon, car lorsque vous publiez une lettre, vous créez une version de la lettre, de ses actifs dépendants et de données à ce stade. La version publiée d’une lettre ne peut pas être modifiée par vous ou un autre utilisateur et peut être restaurée ultérieurement sans aucune incompatibilité inattendue à partir de la version publiée. Vous pouvez retourner à cette instance plus tard et reprendre où vous en étiez.

* **Instance Envoyer** : l’instance Envoyer capture l’état de la lettre envoyée. L’instance Envoyer stocke l’état PDF de l’instance de lettre après son post-traitement, ainsi que les données saisies par l’utilisateur dans l’interface utilisateur de création de correspondance.

Ces instances peuvent être enregistrées uniquement lorsque la lettre est en cours de consultation sur l’instance Publication. Par défaut, l’enregistrement sur les instances est désactivé. Pour activer l’enregistrement des instances de lettre, effectuez les étapes suivantes.

1. Dans AEM, ouvrez la configuration de la console Web Adobe Experience Manager pour votre serveur à l’aide de l’URL suivante : https://&lt;serveur>:&lt;port>/&lt;chemin_contexte>/system/console/configMgr
1. Locate **[!UICONTROL Correspondence Management Configurations]** and click it.
1. Cochez la configuration **[!UICONTROL Gestion des instances de lettre sur Publication]**, puis cliquez sur **[!UICONTROL Enregistrer]**.

Lorsque l’enregistrement des instances de lettre est activé, vous avez la possibilité de sélectionner l’emplacement où enregistrer les instances de lettre. Il existe deux options pour enregistrer les instances de lettre : enregistrement local ou enregistrement à distance.

### Enregistrement local {#local-save}

Les instances de lettre sont enregistrées sur l’instance de publication et répliquées de manière inversée sur l’instance d’auteur.

### Enregistrement à distance {#remote-save}

Cette option est destinée aux personnes ayant des inquiétudes quant à l’enregistrement des données utilisateur sur les instances Publication, ce qui est généralement le cas hors du pare-feu d’entreprise. Lorsque l’enregistrement à distance est activé, les instances de lettre ne sont pas enregistrées sur l’instance Publication mais sont enregistrées à distance sur l’auteur de traitement spécifié via les configurations LiveCycle Client SDK.

#### Activer l’enregistrement à distance {#enable-remote-save}

1. Dans AEM, ouvrez la configuration de la console Web Adobe Experience Manager pour votre serveur à l’aide de l’URL suivante : `https://<server>:<port>/<contextpath>/system/console/configMgr`
1. Search for **[!UICONTROL Correspondence Management Configurations]** and click it.
1. Locate the **[!UICONTROL Remote Save]** configuration, check it, and the click **[!UICONTROL Save]**.

#### Spécifiez les paramètres d’auteur de traitement {#specify-processing-author-settings}

1. Dans AEM, ouvrez la configuration de la console Web Adobe Experience Manager pour votre serveur à l’aide de l’URL suivante : `https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![Configuration de la console Web d’Adobe Experience Manager](assets/2configmanager.png)

1. Sur cette page, recherchez Adobe LiveCycle Client SDK Configuration et développez-le en cliquant dessus.

1. In the Processing Server URL, enter the name of your LiveCycle server, provide the login information, and then click **Save**.

   ![Saisie du nom et des informations de connexion de votre serveur LiveCycle](assets/3configmanager.png)

1. Si nécessaire, définissez le nom d’utilisateur et le mot de passe avec lesquels accéder au serveur.

#### Livraison des pièces jointes {#attachmentdelivery}

* Les pièces jointes de la lettre sont disponibles après le processus dans le PDF, qui est créé après l’envoi de la lettre.
* Si la lettre est rendue à l’aide des API côté serveur sous la forme d’un PDF, interactif ou non, alors le PDF rendu contient des pièces jointes au format PDF.
* Si un post-traitement associé à un modèle de lettre est chargé dans le cadre des opérations d’envoi ou de finalisation de correspondance à l’aide de l’interface utilisateur Création de correspondance, les pièces jointes sont transmises en tant que liste &lt;com.adobe.idp.Document> dans le paramètre AttachmentDocs.
* Les mécanismes de livraison prêts à l’emploi, tels que l’envoi par courrier électronique et l’impression, livrent les pièces jointes avec le PDF de la correspondance générée.

## Modes de rendu d’aperçu de lettre : Aperçu de formulaires pour périphériques mobiles et aperçu au format PDF {#rendition-modes-of-letter-preview-mobile-forms-preview-and-pdf-preview}

Dans AEM Forms, la solution Correspondence Management affiche une lettre en tant que document HTML dans l’IU Création de correspondance. Toutefois, la solution Correspondence Management prend toujours en charge le retour à un aperçu au format PDF au lieu de l’aperçu HTML. Pour plus d’informations sur le basculement entre les modes d’aperçu HTML et PDF, consultez [Changement de mode de rendu de lettre](#changerenditionmode).

Vous trouverez ci-dessous les avantages et les fonctionnalités disponibles dans l’aperçu HTML et PDF.

**Avantages de l’aperçu HTML/formulaires mobile** 

* **Appuyez sur une valeur de champ de données pour mettre en surbrillance le champ de données correspondant** : dans l’interface utilisateur Création de correspondance, vous pouvez appuyer sur une valeur de champ de données de la lettre pour mettre en surbrillance le champ de données correspondant dans l’onglet Données. Pour plus d’informations, consultez [Saisir des données](#enterdata).

* **Prise en charge du navigateur** : retrait graduel de la prise en charge des navigateurs NPAPI, ce qui affecte l’aperçu PDF de la lettre. L’aperçu des formulaires mobiles/HTML d’une lettre n’est pas affecté par ce problème.
* **Mettre en surbrillance le contenu modifiable dans une lettre** : dans l’interface utilisateur Création de correspondance, vous pouvez appuyer sur Mettre en surbrillance le contenu modifiable pour mettre en surbrillance tout le contenu modifiable de la lettre en gris. Pour plus d’informations, consultez [Gestion du contenu](#managecontent).

`<li>` `<li>Benefits of HTML preview  <ul>   <li>Right to left</li>   <li>NPAPI</li>   <li>Highlight Editable Content</li>  </ul> </li>` `<li>Benefits of PDF preview  <ul>   <li>Page Break</li>   <li>Final Preview</li>  </ul> </li>`
`<li>` `<li>Benefits of HTML preview  <ul>   <li>Right to left</li>   <li>NPAPI</li>   <li>Highlight Editable Content</li>  </ul> </li>` `<li>Benefits of PDF preview  <ul>   <li>Page Break</li>   <li>Final Preview</li>  </ul> </li>`  **Avantages de l’aperçu PDF**

* **Saut de page** : dans l’aperçu au format PDF, vous pouvez afficher précisément comment les sauts de page dans la lettre affectent sa sortie.
* **Aperçu final** : dans l’aperçu au format PDF, vous pouvez afficher le formatage et l’aspect exacts de la lettre telle qu’elle apparaîtra à sa sortie.

Pour plus d’informations sur la prise en charge des scripts dans des formulaires PDF, reportez-vous à la section [Prise en charge des scripts](https://help.adobe.com/en_US/livecycle/11.0/ScriptingSupport/index.html).

For more information on scripting support in HTML5 forms, see [Scripting support for HTML5 forms](/help/forms/using/scripting-support.md).

### Changement du mode de rendu d’une lettre {#changerenditionmode}

Par défaut, l’interface utilisateur Création de correspondance utilise des formulaires HTML ou des formulaires mobiles pour rendre l’aperçu d’une lettre. L’aperçu des formulaires mobiles n’a aucun problème de rendu dans un navigateur, car il utilise le module externe natif du navigateur et ne requiert aucun module externe supplémentaire. Vous pouvez changer le mode de  de lettre en PDF. Toutefois, les contraintes de navigateur peuvent créer des problèmes pour les différentes fonctionnalités de l’aperçu au format PDF interactif de la lettre.

For more information on browser compatibility with letter preview, see [Discontinuation of NPAPI browser plug-ins and its impact](https://helpx.adobe.com/fr/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html).

Pour changer le mode d’aperçu de la lettre, effectuez les étapes suivantes :

1. Go to `https://[system]:'port'/system/console/configMgr` and, if necessary, log in as Admin.
1. Accédez à **[!UICONTROL Configurations de Correspondence Management]** > **[!UICONTROL Type de rendu]** et sélectionnez **Rendu HTML** (par défaut) ou **Rendu PDF**.
1. Cliquez sur **[!UICONTROL Save]** (Enregistrer).

