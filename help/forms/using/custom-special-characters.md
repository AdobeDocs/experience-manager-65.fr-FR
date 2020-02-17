---
title: Caractères spéciaux personnalisés dans Correspondence Management
seo-title: Caractères spéciaux personnalisés dans Correspondence Management
description: Découvrez comment ajouter des caractères spéciaux personnalisés dans Correspondence Management.
seo-description: Découvrez comment ajouter des caractères spéciaux personnalisés dans Correspondence Management.
uuid: a1890f6d-8e0c-471f-a9bd-861acf1f17e6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9f26565c-a7ba-4e9e-bf77-a95eb8e351f2
docset: aem65
translation-type: tm+mt
source-git-commit: 08e53eec26e29c2403cdfc3239da3ea23da3f321

---


# Caractères spéciaux personnalisés dans Correspondence Management{#custom-special-characters-in-correspondence-management}

## Présentation {#overview}

Correspondence Management offre une prise en charge par défaut et intégrée de 210 caractères spéciaux que vous pouvez facilement insérer sous forme de lettres.

Vous pouvez par exemple insérer les caractères spéciaux suivants :

* Symboles de devise tels que €, ¥ et £
* Symboles mathématiques tels que Δ, √, Δet ^
* Symboles de ponctuation ‟ et&quot;

Vous pouvez insérer des caractères spéciaux sous forme de lettres :

* In the [text editor](/help/forms/using/document-fragments.md#createtext)
* In an [editable, inline module in a correspondence](../../forms/using/create-correspondence.md#managecontent)

![spécialcaractérissinlinemodule](assets/specialcharactersinlinemodule.png)

L’administrateur peut ajouter la prise en charge de plus de caractères/de caractères spéciaux grâce à la personnalisation. Cet article fournit les instructions vous permettant d’ajouter la prise en charge de caractères spéciaux personnalisés supplémentaires.

## Ajouter ou modifier la prise en charge des caractères spéciaux personnalisés dans Correspondence Management {#creatingfolderstructure}

Procédez comme suit pour ajouter la prise en charge des caractères spéciaux personnalisés :

1. Go to `https://[server]:[port]/[ContextPath]/crx/de` and login as Administrator.
1. In the apps folder, create a folder named **[!UICONTROL specialcharacters]** with path/structure similar to the specialcharacters folder (located in the textEditorConfig folder under libs):

   1. Right-click the **specialcharacters** folder at the following path and select **Overlay Node**:

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. Assurez-vous que la boîte de dialogue du nœud de recouvrement possède les valeurs suivantes :

      **** Chemin : /libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters

      **** Emplacement de l’incrustation : /apps/

      **** Faire correspondre les types de noeud : Coché

      >[!NOTE]
      >
      >N&#39;apportez pas de modifications dans la branche /libs. Toutes les modifications que vous apportez risquent d’être perdues, car cette branche est exposée aux modifications chaque fois que vous :
      >
      >
      >
      >    * Effectuez une mise à niveau sur votre instance
      >    * Appliquez un correctif
      >    * Configurez un feature pack


   1. Cliquez sur **OK**, puis sur **Enregistrer tout**. Le dossier specialcharacters est créé dans le chemin d’accès spécifié.

      Après avoir créé le recouvrement, vérifiez les balises de structure de nœud. Chaque nœud créé dans /apps à l’aide du recouvrement doit présenter la même classe et les mêmes propriétés que celles définies dans /libs pour ce nœud. Si une propriété ou une balise est manquante dans la structure de nœud sous l’emplacement /apps, synchronisez ses balises avec le nœud correspondant situé sous /libs.



1. Vérifiez que le nœud **[!UICONTROL textEditorConfig]** est doté des valeurs et propriétés suivantes :

   | Nom | Type | Valeur |
   |---|---|---|
   | cmConfigurationType | Chaîne | cmTextEditorConfiguration |
   | cssPath | Chaîne | /libs/fd/cm/ma/gui/components/admin/createasset/textcontrol/clientlibs/textcontrol |

1. Right-click the **[!UICONTROL specialcharacters]** folder at the following path and select **Create > Child Node** and then click **Save All**:

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters/&lt;YourChildNode>

1. Actualisez la page de l’interface utilisateur Éditeur de texte\Création de correspondance. Le nœud que vous avez ajouté apparaît en dernier dans la liste des caractères spéciaux de l’interface utilisateur.
1. Cliquez sur **Enregistrer tout**.
1. Apportez les modifications nécessaires aux caractères spéciaux :

<table>
 <tbody>
  <tr>
   <td><strong>To...</strong></td>
   <td><strong>Effectuez les étapes suivantes</strong></td>
  </tr>
  <tr>
   <td>Ajouter un caractère spécial personnalisé</td>
   <td>
    <ol>
     <li>Ajoutez un noeud enfant sous "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters" avec des propriétés obligatoires.</li>
     <li>Cliquez sur Enregistrer tout</li>
     <li>Actualisez la page de l’interface utilisateur Éditeur de texte\Création de correspondance pour afficher les modifications.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Mettez à jour les propriétés d’un caractère spécial existant.</td>
   <td>
    <ol>
     <li>Recouvrez le nœud pour qu’il soit mis à jour comme expliqué ci-dessus et vérifiez les balises et les classes.</li>
     <li>Remplacez toutes les valeurs, telles que caption, value, endValue et multipleCaption. </li>
     <li>Cliquez sur Enregistrer tout. </li>
     <li>Actualisez la page de l’interface utilisateur Éditeur de texte\Création de correspondance pour afficher les modifications.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Masquer un caractère spécial</td>
   <td>
    <ol>
     <li>Recouvrez le noeud à masquer sous "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters".</li>
     <li>Ajoutez la propriété sling:hideResource (booléenne) au noeud (sous les applications) à masquer. </li>
     <li>Cliquez sur Enregistrer tout. </li>
     <li>Actualisez la page de l’interface utilisateur Éditeur de texte\Création de correspondance pour afficher les modifications.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Masquer plusieurs caractères spéciaux</td>
   <td>
    <ol>
     <li>Ajoutez la propriété "sling:hideChildren (String or String[])" à "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters". </li>
     <li>Ajoutez des noms de nœud (caractères spéciaux à masquer) sous forme de valeurs pour la propriété sling:hideChildren. </li>
     <li>Cliquez sur Enregistrer tout. </li>
     <li>Actualisez la page de l’interface utilisateur Éditeur de texte\Création de correspondance pour afficher les modifications.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>Classement des caractères spéciaux</td>
   <td>
    <ol>
     <li>Ajoutez un noeud enfant sous "/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters" avec des propriétés obligatoires. </li>
     <li>Ajoutez la propriété « sling:orderBefore (String) » au nœud enfant qui vient d’être créé. </li>
     <li>Ajoutez le nom du nœud comme valeur devant laquelle le caractère spécial récemment ajouté doit être affiché. </li>
     <li>Cliquez sur Enregistrer tout. </li>
     <li>Actualisez la page de l’interface utilisateur Éditeur de texte\Création de correspondance pour afficher les modifications.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

