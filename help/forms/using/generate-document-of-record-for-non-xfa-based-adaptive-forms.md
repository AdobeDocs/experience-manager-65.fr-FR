---
title: Générer un document d’enregistrement pour les formulaires adaptatifs
seo-title: Generate Document of Record for adaptive forms
description: Explique comment générer un modèle de document d’enregistrement (DE) pour les formulaires adaptatifs.
seo-description: Explains how you can generate a template for a document of record (DoR) for adaptive forms.
uuid: 2dc7e0de-fff9-43fa-9426-e9b047eb2595
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ce65cb5f-94ec-4423-9fa9-d617e9703091
docset: aem65
feature: Adaptive Forms
exl-id: 7240897f-6b3a-427a-abc6-66310c2998f3
source-git-commit: a81367c2a07031d8c6cf549050a1445ff0c1a8dc
workflow-type: ht
source-wordcount: '3483'
ht-degree: 100%

---

# Générer un document d’enregistrement pour les formulaires adaptatifs{#generate-document-of-record-for-adaptive-forms}

## Présentation {#overview}

Après l’envoi d’un formulaire, vos clients veulent généralement conserver un enregistrement, sous forme imprimée ou de document, des informations qu’ils ont intégrées au formulaire pour s’y reporter ultérieurement. On parle ici de document d’enregistrement.

Cet article explique comment vous pouvez générer un document d’enregistrement pour les formulaires adaptatifs.

>[!NOTE]
>
>La génération automatique de document d’enregistrement n’est pas prise en charge pour les formulaires adaptatifs XFA. Cependant, vous pouvez vous servir du fichier XDP utilisé pour créer le formulaire adaptatif comme document d’enregistrement.

## Types de formulaire adaptatif et leurs documents d’enregistrement {#adaptive-form-types-and-their-documents-of-record}

Lorsque vous créez un formulaire adaptatif, vous pouvez sélectionner un modèle de formulaire. Vous avez le choix entre :

* [Modèles de formulaire](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template) Vous permet de sélectionner un modèle XFA pour votre formulaire adaptatif. Lorsque vous sélectionnez un modèle XFA, vous pouvez utiliser le fichier XDP associé pour créer le document d’enregistrement, comme décrit ci-dessus.

* [Schéma XML](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema) Vous permet de sélectionner une définition de schéma XML pour votre formulaire adaptatif. Lorsque vous sélectionnez un schéma XML pour votre formulaire adaptatif, vous pouvez :

   * Associer un modèle XFA pour créer un document d’enregistrement. Assurez-vous que ce modèle XFA associé utilise le même schéma XML que votre formulaire adaptatif.
   * Générer automatiquement un document d’enregistrement

* Aucun Vous permet de créer un formulaire adaptatif sans modèle de formulaire. Le document d’enregistrement est généré automatiquement pour votre formulaire adaptatif.

Lorsque vous sélectionnez un modèle de formulaire, configurez le document d’enregistrement à l’aide des options disponibles sous Configuration du modèle de document d’enregistrement. Voir [Configuration du modèle de document d’enregistrement](#document-of-record-template-configuration).

## Document d’enregistrement automatiquement généré {#automatically-generated-document-of-record}

Un document d’enregistrement permet aux clients de conserver une copie du formulaire envoyé en vue de son impression. Lorsque vous générez automatiquement un document d’enregistrement, à chaque fois que vous modifiez votre formulaire, son document d’enregistrement est immédiatement mis à jour. Par exemple, imaginons que vous supprimez le champ concernant l’âge pour les clients qui ont sélectionné les États-Unis comme pays. Lorsque ces clients génèrent un document d’enregistrement, le champ relatif à l’âge ne leur est pas accessible.

Voici les avantages apportés par un document d’enregistrement automatiquement généré :

* Il prend en charge la liaison de données.
* Il masque automatiquement les champs marqués comme exclus du document d’enregistrement au moment de l’envoi. Aucune opération supplémentaire n’est nécessaire.
* Il permet de gagner du temps lors de la conception d’un modèle de document d’enregistrement.
* Il permet de tester des styles et des aspects différents à l’aide de différents modèles de base et de sélectionner les meilleurs style et aspect pour le document d’enregistrement. L’utilisation de styles est facultative. Si vous ne spécifiez pas de style, les styles du système sont définis comme valeur par défaut.
* De cette façon, toute modification appliquée au formulaire se répercute immédiatement dans le document d’enregistrement.

## Composants de génération automatique de document d’enregistrement {#components-to-automatically-generate-a-document-of-record}

Pour générer un document d’enregistrement pour les formulaires adaptatifs, il vous faut les éléments suivants :

**Formulaire adaptatif** : un formulaire adaptatif pour lequel vous souhaitez générer un document d’enregistrement.

**Modèle de base (recommandé)** : modèle XFA (fichier XDP) créé dans AEM Designer. Le modèle de base est utilisé pour spécifier les informations en termes de style et d’identité graphique pour le modèle de document d’enregistrement.

Voir [Modèle de base d’un document d’enregistrement](#base-template-of-a-document-of-record).

>[!NOTE]
>
>Le modèle de base d’un document d’enregistrement est également appelé métamodèle de document d’enregistrement.

**Modèle de document d’enregistrement** : modèle XFA (fichier XDP) généré à partir d’un formulaire adaptatif.

Voir [Configuration du modèle de document d’enregistrement](#document-of-record-template-configuration).

**Données de formulaire** : informations renseignées par un utilisateur dans le formulaire adaptatif. Il fusionne avec le modèle de document d’enregistrement pour générer le document d’enregistrement.

## Mappage des éléments du formulaire adaptatif {#mapping-of-adaptive-form-elements}

Les sections suivantes décrivent l’apparence des éléments du formulaire adaptatif dans un document d’enregistrement.

### Champs {#fields}

<table>
 <tbody>
  <tr>
   <th>Composant de formulaire adaptatif</th>
   <th>Composant XFA correspondant</th>
   <th>Inclus par défaut dans le modèle de document d’enregistrement ?</th>
   <th>Remarques</th>
  </tr>
  <tr>
   <td>Bouton</td>
   <td>Bouton</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Case à cocher</td>
   <td>Case à cocher</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Sélecteur de date</td>
   <td>Champ Date/Heure</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Liste déroulante</td>
   <td>Liste déroulante</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Signature tactile</td>
   <td>Signature tactile</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Zone numérique</td>
   <td>Champ numérique</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Zone de mot de passe</td>
   <td>Champ Mot de passe</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Bouton radio</td>
   <td>Bouton radio</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Zone de texte</td>
   <td>Champ de texte</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Bouton Réinitialiser</td>
   <td>Bouton Réinitialiser</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Bouton Envoyer</td>
   <td><p>Bouton Envoyer par messagerie</p> <p>Bouton Envoyer via HTTP</p> </td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>Conditions d’utilisation</td>
   <td> </td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>Pièce jointe</td>
   <td> </td>
   <td>false</td>
   <td>Non disponible dans le modèle de document d’enregistrement. Uniquement disponible dans le document d’enregistrement par les pièces jointes.</td>
  </tr>
 </tbody>
</table>

### Conteneurs {#containers}

<table>
 <tbody>
  <tr>
   <th>Composant de formulaire adaptatif</th>
   <th>Composant XFA correspondant</th>
   <th>Remarques</th>
  </tr>
  <tr>
   <td>Panneau<br /> </td>
   <td>Sous-formulaire<br /> </td>
   <td>Le panneau répétable se mappe au sous-formulaire répétable.</td>
  </tr>
 </tbody>
</table>

### Composants statiques {#static-components}

| Composant de formulaire adaptatif | Composant XFA correspondant | Remarques |
|---|---|---|
| Image | Image | Qu’ils soient liés ou non, les composants TextDraw et Image apparaissent toujours dans le document d’enregistrement relatif à un formulaire adaptatif basé sur XSD, à moins que cela ne soit exclu dans les paramètres de document d’enregistrement. |
| Texte | Texte |

>[!NOTE]
>
>Dans l’interface utilisateur classique, vous disposez de divers onglets pour modifier les propriétés des champs.

### Tableaux {#tables}

Composants tabulaires des formulaires adaptatifs (en-tête, pied de page et lignes) associés aux composants XFA correspondants. Vous pouvez mapper des panneaux répétables aux tableaux dans un document d’enregistrement.

## Modèle de base d’un document d’enregistrement {#base-template-of-a-document-of-record}

Le modèle de base fournit les informations relatives au style et à l’aspect du document d’enregistrement. Vous pouvez ainsi personnaliser l’aspect par défaut du document d’enregistrement généré automatiquement. Imaginons que vous souhaitez ajouter le logo de votre entreprise dans l’en-tête et les informations relatives au droit d’auteur dans le pied de page du document d’enregistrement. Le gabarit du modèle de base est utilisé comme gabarit de modèle de document d’enregistrement. Le gabarit peut comporter des informations telles que l’en-tête, le pied et le numéro de page, que vous pouvez appliquer au document d’enregistrement. Vous pouvez appliquer ces informations au document d’enregistrement à l’aide d’un modèle de base pour générer automatiquement un document d’enregistrement. L’utilisation d’un modèle de base permet de modifier les propriétés par défaut des champs.

Respectez les [conventions relatives aux modèles de base](#base-template-conventions) lorsque vous créez un modèle de base.

## Conventions relatives aux modèles de base {#base-template-conventions}

Un modèle de base sert à définir l’en-tête, le pied de page, le style et l’aspect d’un document d’enregistrement. L’en-tête et le pied de page peuvent comporter des informations, comme le logo de l’entreprise et la mention de droit d’auteur. Le gabarit de page du modèle de base est copié et utilisé comme gabarit de page du document d’enregistrement. Il contient l’en-tête, le pied de page, le numéro de page ainsi que toute autre information devant apparaître sur toutes les pages du document d’enregistrement. Même si vous utilisez un modèle de base non conforme aux conventions relatives aux modèles de base, le gabarit de page du modèle de base est quand même utilisé dans le modèle de document d’enregistrement. Il vous est fortement recommandé de créer votre modèle de base en fonction des conventions correspondantes et de l’utiliser pour la génération automatique du document d’enregistrement.

**Conventions en matière de gabarits de page**

* Dans le modèle de base, il est conseillé de nommer le sous-formulaire racine `AF_METATEMPLATE` et le gabarit de page `AF_MASTERPAGE`.

* Le gabarit de page « `AF_MASTERPAGE` » et situé sous le sous-formulaire racine `AF_METATEMPLATE` est privilégié pour extraire les informations sur l’en-tête, le pied de page et le style.

* En l’absence de gabarit de page `AF_MASTERPAGE`, le premier gabarit de page présent dans le modèle de base est utilisé.

**Conventions an matière de style des champs**

* Pour appliquer un style aux champs du document d’enregistrement, le modèle de base fournit les champs situés dans le sous-formulaire `AF_FIELDSSUBFORM` sous le sous-formulaire racine `AF_METATEMPLATE`.

* Les propriétés de ces champs sont appliquées aux champs du document d’enregistrement. Ces champs doivent respecter la convention d’affectation des noms de `AF_<name of field in all caps>_XFO`. Par exemple, le champ contenant une case à cocher doit être nommé `AF_CHECKBOX_XFO`.

Pour créer un modèle de base, procédez comme suit dans AEM Designer.

1. Cliquez sur **Fichier > Nouveau**.
1. Sélectionnez l’option **Basé sur un modèle**.

1. Choisissez la catégorie **Formulaires - Document d’enregistrement**.
1. Sélectionnez **Modèle de base de DE**.
1. Cliquez sur **Suivant** et renseignez les informations nécessaires.

1. (Facultatif) Modifiez le style et l’aspect que vous souhaitez appliquer aux champs du document d’enregistrement.
1. Enregistrez le formulaire.

Vous pouvez désormais utiliser le formulaire enregistré comme modèle de base de document d’enregistrement.
Ne modifiez ou ne supprimez aucun des scripts du modèle de base.

**Modification du modèle de base**

* Si vous n’appliquez aucun style aux champs du modèle de base, il est recommandé de les supprimer afin que toutes les mises à niveau du modèle de base soient automatiquement reportées.
* Lors de la modification du modèle de base, ne supprimez, n’ajoutez ou ne modifiez pas les scripts.

>[!NOTE]
>
>Créez un modèle de base conforme aux conventions et en suivant scrupuleusement la procédure ci-dessus.

## Configuration du modèle de document d’enregistrement {#document-of-record-template-configuration}

Configurez le modèle de document d’enregistrement de votre formulaire pour permettre à vos clients de télécharger une copie imprimable du formulaire envoyé. Un fichier XDP fait office de modèle de document d’enregistrement. Le téléchargement des clients du document d’enregistrement est formaté selon la mise en page spécifiée dans le fichier XDP.

Effectuez les étapes suivantes pour configurer un document d’enregistrement pour les formulaires adaptatifs :

1. Dans l’instance d’auteur AEM, cliquez sur **Formulaires > Formulaires et documents**.
1. Sélectionnez un formulaire, puis cliquez sur **Afficher les propriétés**.
1. Dans la fenêtre Propriétés, appuyez sur **Modèle de formulaire**.
Vous pouvez également sélectionner un modèle de formulaire lorsque vous créez un formulaire.

   >[!NOTE]
   >
   >Sous l’onglet Modèle de formulaire, veillez à sélectionner **Schéma** ou **Aucun** dans la liste déroulante **Choisir parmi**. **[!UICONTROL Les documents d’enregistrement ne sont pas pris en charge dans le cadre de formulaires basés sur XFA ou de formulaires adaptatifs auxquels un modèle de formulaire est appliqué.]**

1. Dans la section Configuration du modèle de document d’enregistrement de l’onglet Modèle de formulaire, sélectionnez l’une des options suivantes :

   **Aucun** : utilisez cette option si vous ne souhaitez pas configurer de document d’enregistrement pour le formulaire.

   **Associer un modèle de formulaire comme modèle de document d’enregistrement** : sélectionnez cette option si vous disposez d’un fichier XDP que vous souhaitez utiliser comme modèle pour le document d’enregistrement. Lorsque vous sélectionnez cette option, tous les fichiers XDP disponibles dans le référentiel AEM Forms s’affichent. Sélectionnez le fichier approprié.

   Le fichier XDP sélectionné est associé au formulaire adaptatif.

   **Générer un document d’enregistrement** : cette option permet d’utiliser un fichier XDP comme modèle de base pour définir le style et l’aspect du document d’enregistrement. Lorsque vous sélectionnez cette option, tous les fichiers XDP disponibles dans le référentiel AEM Forms s’affichent. Sélectionnez le fichier approprié.

   >[!NOTE]
   >
   >Assurez-vous que le schéma utilisé pour créer le formulaire adaptatif et le schéma (schéma de données) du formulaire XFA sont identiques si :
   >
   >
   >
   >    * Votre formulaire adaptatif est basé sur un schéma
   >    * Vous utilisez l’option **Associer le modèle de formulaire comme modèle de document d’enregistrement** pour les documents d’enregistrement.


1. Cliquez sur **Terminé**.

## Personnaliser les informations d’identité graphique d’un document d’enregistrement {#customize-the-branding-information-in-document-of-record}

Lors de la génération d’un document d’enregistrement, vous pouvez modifier les informations d’identité graphique pour le document d’enregistrement dans l’onglet Document d’enregistrement. L’onglet Document d’enregistrement inclut des options telles que le logo, l’apparence, la mise en page, l’en-tête et le pied de page, la clause de non-responsabilité et si vous souhaitez inclure des options de case à cocher et de bouton radio désélectionnées.

Pour localiser les informations d’identité graphique que vous saisissez dans l’onglet Document d’enregistrement, vous devez vous assurer que le paramètre régional du navigateur est défini correctement. Pour personnaliser les informations d’identité graphique du document d’enregistrement, procédez comme suit :

1. Sélectionnez un panneau (panneau racine) dans le document d’enregistrement, puis appuyez sur ![configurer](assets/configure.png).
1. Appuyez sur ![dortab](assets/dortab.png). L’onglet Document d’enregistrement s’affiche.
1. Sélectionnez le modèle par défaut ou un modèle personnalisé pour le rendu du document d’enregistrement. Si vous sélectionnez le modèle par défaut, une vignette d’aperçu du document d’enregistrement apparaît sous la liste déroulante Modèle.

   ![brandingtemplate](assets/brandingtemplate.png)

   Si vous choisissez de sélectionner un modèle personnalisé, sélectionnez un fichier XDP sur votre serveur AEM Forms. Si vous souhaitez utiliser un modèle qui n’est pas sur votre serveur AEM Forms, vous devez au préalable télécharger le fichier XDP sur votre serveur AEM Forms.

1. Si vous sélectionnez un modèle par défaut ou un modèle personnalisé, certaines ou toutes les propriétés suivantes apparaissent dans l’onglet Document d’enregistrement. Spécifiez-les en conséquence :

   * **Image du logo** : vous pouvez choisir d’utiliser l’image du logo à partir du formulaire adaptatif, en choisir une dans le gestionnaire des actifs numériques ou en télécharger une depuis votre ordinateur.
   * **Titre du formulaire**
   * **Texte d’en-tête**
   * **Libellé de cause de non-responsabilité**
   * **Clause de non-responsabilité**
   * **Texte de la clause de non-responsabilité**
   * **Couleur d’accentuation** : la couleur dans laquelle le texte de l’en-tête et les lignes de séparation sont affichées dans le document ou l’enregistrement PDF
   * **Famille de polices** : la famille de polices du texte dans le document d’enregistrement PDF
   * **Pour les composants de case à cocher et de bouton radio, afficher uniquement les valeurs sélectionnées**
   * **Séparateur pour plusieurs valeurs sélectionnées**
   * **Inclure les objets de formulaire qui ne sont pas associés à un modèle de données**
   * **Exclure les champs masqués du document d’enregistrement**
   * **Masquer la description des panneaux**

   Si le modèle XDP personnalisé que vous sélectionnez comprend plusieurs gabarits, les propriétés de ces pages apparaissent dans la section **[!UICONTROL contenu]** de l’onglet **[!UICONTROL Document d’enregistrement]**.

   ![Propriétés du gabarit de page ](assets/master-page-properties.png)

   Les propriétés du gabarit de page comprennent l’image du logo, le texte de l’en-tête, le titre du formulaire, l’étiquette de la clause de non-responsabilité et le texte de la clause de non-responsabilité. Vous pouvez appliquer les propriétés du formulaire adaptatif ou du modèle XDP au document d’enregistrement. AEM Forms applique par défaut les propriétés des modèles au document d’enregistrement. Vous pouvez également définir des valeurs personnalisées pour les propriétés du gabarit de page. Pour plus d’informations sur la façon d’appliquer plusieurs gabarits de pages dans un document d’enregistrement, voir [Appliquer plusieurs gabarits à un document d’enregistrement](#apply-multiple-master-pages-dor).

   >[!NOTE]
   >
   >Si vous utilisez un modèle de formulaire adaptatif créé avec une version de Designer antérieure à 6.3, pour que les propriétés Couleur d’accentuation et Famille de polices fonctionnent, assurez-vous que les éléments suivants sont présents dans votre modèle de formulaire adaptatif sous le sous-formulaire racine :

   ```xml
   <proto>
   <font typeface="Arial"/>
   <fill>
   <color value="4,166,203"/>
   </fill>
   <edge>
   <color value="4,166,203"/>
   </edge>
   </proto>
   ```

1. Pour enregistrer les modifications d’identité graphique, appuyez sur Terminé.

## Mises en page de tableau et de colonne pour les panneaux d’un document d’enregistrement {#table-and-column-layouts-for-panels-in-document-of-record}

Votre formulaire adaptatif peut être long et comporter plusieurs champs. Vous ne pouvez pas enregistrer un document d’enregistrement en tant que copie exacte du formulaire adaptatif. Vous pouvez maintenant choisir une mise en page de tableau ou de colonne pour enregistrer un ou plusieurs panneaux de formulaires adaptatifs dans le document d’enregistrement PDF.

Avant de générer un document d’enregistrement, dans les paramètres d’un panneau, sélectionnez Tableau ou Colonne pour Mise en page du document d’enregistrement pour ce panneau. Les champs du panneau sont organisés en conséquence dans le document d’enregistrement.

![Champs dans un panneau rendu dans une mise en page de tableau dans le document d’enregistrement](assets/dortablelayout.png)

Champs dans un panneau rendu dans une mise en page de tableau dans le document d’enregistrement

![Champs dans un panneau rendu dans une mise en page de colonne dans le document d’enregistrement](assets/dorcolumnlayout.png)

Champs dans un panneau rendu dans une mise en page de colonne dans le document d’enregistrement

## Paramètres d’un document d’enregistrement {#document-of-record-settings}

Les paramètres du document d’enregistrement vous permettent de choisir les options que vous souhaitez inclure dans celui-ci. Par exemple, une banque accepte les informations suivantes dans un formulaire : nom, âge, numéro de sécurité sociale et numéro de téléphone. Le formulaire génère un numéro de compte bancaire et les informations sur la banque. Vous pouvez choisir de n’afficher que le nom, le numéro de sécurité sociale, le compte bancaire et les informations sur la banque dans le document d’enregistrement.

Les paramètres du document d’enregistrement d’un composant sont disponibles dans ses propriétés. Pour accéder aux propriétés d’un composant, sélectionnez le composant et cliquez sur ![cmppr](assets/cmppr.png) dans le recouvrement. Les propriétés sont répertoriées dans la barre latérale. Vous y trouvez les paramètres suivants.

**Paramètres sur le terrain**

* **Exclure du document d’enregistrement :** la définition de cette propriété sur true exclut le champ du document d’enregistrement. Il s’agit d’une propriété pouvant faire l’objet d’un script appelée « `excludeFromDoR` ». Son comportement dépend de la propriété au niveau du formulaire **Exclure des champs du document d’enregistrement (DE) s’il est masqué**.

* **Afficher le panneau sous forme de tableau :** la définition de cette propriété permet d’afficher le panneau sous forme de tableau dans le document d’enregistrement si le panneau contient moins de 6 champs. Applicable au panneau uniquement.
* **Exclure le titre du document d’enregistrement :** la définition de la propriété exclut le titre du panneau/tableau du document d’enregistrement. Applicable au panneau et à la table uniquement.
* **Exclure la description du document d’enregistrement :** la définition de la propriété exclut la description du panneau/tableau du document d’enregistrement. Applicable au panneau et à la table uniquement.
* **[!UICONTROL Pagination]** > **[!UICONTROL Placer :]** détermine l’emplacement où vous choisissez de placer le panneau.
   * **[!UICONTROL Placer]** > **[!UICONTROL Suivant le précédent :]** place le panneau après l’objet précédent dans le panneau parent.
   * **[!UICONTROL Placer]** > **[!UICONTROL Dans la zone de contenu]** > Nom de la zone de contenu : place le panneau dans la zone de contenu indiquée.
   * **[!UICONTROL Placer]** > **[!UICONTROL Haut de la zone de contenu suivante :]** place le panneau en haut de la zone de contenu suivante.
   * **[!UICONTROL Placer]** > **[!UICONTROL Haut de la zone de contenu]** > Nom de la zone de contenu : place le panneau en haut de la zone de contenu indiquée.
   * **[!UICONTROL Placer]** > **[!UICONTROL Sur la page]** > Nom du gabarit de page : place le panneau sur la page indiquée. Si un saut de page n’est pas inséré automatiquement, [!DNL AEM Forms] ajoute un saut de page.
   * **[!UICONTROL Placer]** > **[!UICONTROL Haut de la page suivante :]** place le panneau en haut de la page suivante. Si un saut de page n’est pas inséré automatiquement, [!DNL AEM Forms] ajoute un saut de page.
   * **[!UICONTROL Placer]** > **[!UICONTROL Haut de la page]** > Nom du gabarit de page : place le panneau en haut de la page, lorsque la page indiquée est générée. Si un saut de page n’est pas inséré automatiquement, [!DNL AEM Forms] ajoute un saut de page.
* **[!UICONTROL Pagination]** > **[!UICONTROL Après]** : détermine la zone à remplir une fois le panneau placé. Les champs suivants sont disponibles dans la section **[!UICONTROL Après]** :
   * **[!UICONTROL Après]** > **[!UICONTROL Continuer à remplir le parent]** : continue de fusionner les données de tous les objets à remplir dans le panneau parent.
   * **[!UICONTROL Après]** > **[!UICONTROL Aller à la zone de contenu suivante]** : commence à remplir la zone de contenu suivante après avoir placé le panneau.
   * **[!UICONTROL Après]** > **[!UICONTROL Aller à la zone de contenu]** > Nom de la zone de contenu : commence à remplir la zone de contenu spécifiée après avoir placé le panneau.
   * **[!UICONTROL Après]** > **[!UICONTROL Aller à la page suivante]** : commence à remplir la page suivante après avoir placé le panneau.
   * **[!UICONTROL Après]** > **[!UICONTROL Aller à la page]** > Nom de la page : commence à remplir la page spécifiée après avoir placé le panneau.
* **[!UICONTROL Pagination]** > **[!UICONTROL Débordement]** : détermine le mode de débordement d’un panneau ou d’un tableau s’étendant sur plusieurs pages. Les champs suivants sont disponibles dans la section **[!UICONTROL Débordement]** :
   * **[!UICONTROL Débordement]** > **[!UICONTROL Aucun]** : commence à remplir la page suivante. Si un saut de page n’est pas inséré automatiquement, [!DNL AEM Forms] ajoute un saut de page.
   * **[!UICONTROL Débordement]** > **[!UICONTROL Aller à la zone de contenu]** > Nom de la zone de contenu : commence à remplir la zone de contenu indiquée.
   * **[!UICONTROL Débordement]** > **[!UICONTROL Aller à la page]** > Nom de la page : commence à remplir la page indiquée.

Pour plus d’informations sur la manière d’appliquer des sauts de page et d’appliquer plusieurs gabarits de page dans un document d’enregistrement, voir [Appliquer un saut de page dans un document d’enregistrement](#apply-page-breaks-in-dor) et [Appliquer plusieurs gabarits de page à un document d’enregistrement](#apply-multiple-master-pages-dor).

**Paramètres des niveaux de formulaires**

* **Inclure les champs non liés dans le document d’enregistrement :** la définition de la propriété comprend les champs non liés du schéma basé sur le formulaire adaptatif du document d’enregistrement. Par défaut, le paramètre est true.
* **Exclure des champs du document d’enregistrement (DE) s’il est masqué** : la définition de cette propriété remplace le comportement de la propriété de niveau de champ Exclure du document d’enregistrement lorsque le paramètre est différent de true. Si des champs sont masqués au moment de l’envoi du formulaire, ils seront exclus du document d’enregistrement si la propriété est définie sur True, à condition que la propriété « Exclure du document d’enregistrement » ne soit pas définie.

## Appliquer un saut de page dans un document d’enregistrement {#apply-page-breaks-in-dor}

Vous pouvez appliquer des sauts de page dans un document d’enregistrement à l’aide de plusieurs méthodes.

Pour appliquer un saut de page à un document d’enregistrement :

1. Appuyez sur le panneau et sélectionnez ![Configurer](assets/configure-icon.svg).

1. Développez le **[!UICONTROL Document d’enregistrement]** pour afficher les propriétés.

1. Dans la section **[!UICONTROL Pagination]**, appuyez sur ![Dossier](assets/folder-icon.svg) dans le champ **[!UICONTROL Placer]**.
1. Appuyez sur **[!UICONTROL Haut de la page suivante]**, puis sur **[!UICONTROL Sélectionner]**. Vous pouvez également appuyer sur **[!UICONTROL Haut de la page]**, sélectionnez le gabarit de page, puis appuyez sur **[!UICONTROL Sélectionner]** pour appliquer le saut de page.
1. Appuyez sur ![Enregistrer](assets/save_icon.svg) pour enregistrer les propriétés.

Le panneau sélectionné passe à la page suivante.

## Appliquer plusieurs gabarits de page à un document d’enregistrement {#apply-multiple-master-pages-dor}

Si le modèle XDP personnalisé que vous sélectionnez comprend plusieurs gabarits de page, les propriétés de ces pages apparaissent dans la section [!UICONTROL Contenu] de l’onglet [!UICONTROL Document d’enregistrement]. Pour plus d’informations, voir [Personnaliser les informations d’identité graphique d’un document d’enregistrement](#customize-the-branding-information-in-document-of-record).

Vous pouvez appliquer plusieurs gabarits de page à un document d’enregistrement en appliquant différents gabarits de page aux composants d’un formulaire adaptatif. Utilisez la section [Pagination](#document-of-record-settings) des propriétés du document d’enregistrement pour appliquer plusieurs gabarits de page.

Voici un exemple d’application de plusieurs gabarits à un document d’enregistrement : 
vous téléchargez un modèle XDP qui comprend quatre gabarits de page dans le serveur [!DNL AEM Forms]. [!DNL AEM Forms] applique par défaut les propriétés du modèle au document d’enregistrement. [!DNL AEM Forms] applique également les propriétés du premier gabarit de page du modèle au document d’enregistrement.

Pour appliquer les propriétés du deuxième gabarit de page à un panneau et les propriétés du troisième gabarit de page aux panneaux qui suivent, procédez comme suit :

1. Appuyez sur le panneau pour appliquer le deuxième gabarit de page et sélectionnez ![Configurer](assets/configure-icon.svg).
1. Dans la section **[!UICONTROL Pagination]**, appuyez sur ![Dossier](assets/folder-icon.svg) dans le champ **[!UICONTROL Placer]**.
1. Appuyez sur **[!UICONTROL Sur la page]**, sélectionnez le deuxième gabarit de page et appuyez sur **[!UICONTROL Sélectionner]**.
AEM Forms applique le deuxième gabarit de page au panneau et à tous les panneaux suivants du formulaire adaptatif.
1. Dans la section **[!UICONTROL Pagination]**, appuyez sur ![Dossier](assets/folder-icon.svg) dans le champ **[!UICONTROL Après]**.
1. Appuyez sur **[!UICONTROL Atteindre la page]**, sélectionnez le troisième gabarit de page et appuyez sur **[!UICONTROL Sélectionner]**.
1. Appuyez sur ![Enregistrer](assets/save_icon.svg) pour enregistrer les propriétés.
AEM Forms applique le troisième gabarit de page au panneau et à tous les panneaux suivants du formulaire adaptatif.


## Considérations essentielles lors de l’utilisation de documents d’enregistrement {#key-considerations-when-working-with-document-of-record}

Gardez à l’esprit les points et restrictions suivants lorsque vous utilisez un document d’enregistrement pour les formulaires adaptatifs.

* Les modèles de document d’enregistrement ne prennent pas en charge le texte enrichi. Par conséquent, tout texte enrichi dans le formulaire adaptatif statique ou dans les informations renseignées par l’utilisateur final est remplacé par du texte brut dans le document d’enregistrement.
* Les fragments de document contenus dans un formulaire adaptatif n’apparaissent pas dans le document d’enregistrement. Les fragments de formulaire adaptatif sont toutefois pris en charge.
* La liaison de contenu dans le document de l’enregistrement généré pour le formulaire adaptatif de schéma XML n’est pas prise en charge.
* La version localisée du document d’enregistrement est créée sur demande pour un paramètre régional lorsque l’utilisateur demande le rendu du document d’enregistrement. La localisation du document d’enregistrement est effectuée en même temps que la localisation du formulaire adaptatif. Pour plus d’informations sur la localisation du document d’enregistrement et des formulaires adaptatifs, voir [Utilisation de processus de traduction AEM pour la localisation des formulaires adaptatifs et du document d’enregistrement](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).
