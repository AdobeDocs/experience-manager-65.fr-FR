---
title: Ajout de propriétés personnalisées aux actifs Correspondence Management
seo-title: Add custom properties to Correspondence Management assets
description: Découvrez comment ajouter des propriétés personnalisées aux actifs Correspondence Management.
seo-description: Learn how to add custom properties to Correspondence Management assets.
uuid: 4716e181-d3ea-424b-9544-376cc649bce7
content-type: reference
topic-tags: correspondence-management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 79437b96-7b57-4581-b7e7-fcaedc3d05de
docset: aem65
feature: Correspondence Management
exl-id: ba2e145d-51ee-4844-a9e1-9927971d25a1
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '4435'
ht-degree: 55%

---

# Ajout de propriétés personnalisées aux actifs Correspondence Management{#add-custom-properties-to-correspondence-management-assets}

## Présentation {#overview}

Vous pouvez personnaliser l’interface utilisateur de Correspondence Management et présenter aux utilisateurs un ensemble personnalisé de propriétés et d’onglets. Cette personnalisation inclut l’ajout de champs personnalisés/de propriétés et d’onglets à des types de ressources/lettres spécifiques ou à tous les types de ressources/lettres.

## Ajout de propriétés personnalisées aux actifs Correspondence Management {#adding-custom-properties-to-correspondence-management-assets}

Les scénarios suivants montrent comment ajouter des propriétés/onglets aux actifs et lettres de Correspondence Management :

* Ajout d’une propriété commune à tous les types de ressources
* Ajout d’un onglet commun à tous les types de ressources
* Ajout de propriétés personnalisées à des types de ressources spécifiques

En ajustant les propriétés, chemins et valeurs dans ces scénarios, vous pouvez ajouter des propriétés et des onglets personnalisés à un autre ensemble de ressources en fonction de vos besoins.

### Scénario : Ajout d’un champ commun (propriété) à tous les types de ressources {#scenario-adding-a-common-field-property-to-all-the-asset-types}

Ce scénario indique comment ajouter une propriété personnalisée à tous les types de ressources (texte, liste, condition et fragments de mise en page) et aux lettres. À l’aide de ce scénario, vous pouvez ajouter une propriété, Emplacement des destinataires, à toutes les ressources et lettres. La propriété Emplacement des destinataires permet d’identifier la zone géographique de livraison à laquelle une ressource ou une lettre correspond.

>[!NOTE]
>
>Si vous avez déjà ajouté une propriété personnalisée, celle-ci commence à s’afficher sur la page de création de la ressource. Pour masquer une telle propriété, voir Afficher/masquer les propriétés personnalisées sur les pages de création et de propriétés de ressources.

![Propriété personnalisée ajoutée à tous les types de ressource](assets/lcoationofrecipientsui.png)

procédez comme suit pour ajouter une propriété personnalisée à tous les types de ressources et lettres :

1. Accédez à `https://'[server]:[port]'/[ContextPath]/crx/de` et connectez-vous en tant qu’administrateur.
1. Dans le dossier d’applications, créez un dossier appelé css avec un chemin/une structure semblables au dossier css situé dans le dossier ccrui. Pour cela, suivez les étapes ci-après :

   1. Faites un clic droit sur le dossier des éléments à l’emplacement suivant, puis sélectionnez **Nœud de recouvrement** :

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

      ![Nœud de recouvrement](assets/itemsoverlaynode.png)

   1. Assurez-vous que la boîte de dialogue du nœud de recouvrement possède les valeurs suivantes :

      **Chemin :** /libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items

      **Emplacement :** /apps/

      **Faire correspondre les types de nœud :** sélectionné

      ![Nœud de recouvrement](assets/cmmetapropertiesoverlaynode.png)

   1. Cliquez sur **OK**. La structure du dossier est créée dans le dossier des applications.

   1. Cliquez sur **Enregistrer tout**.

1. Dans le dossier d’éléments que vous avez créé, ajoutez un nœud à la propriété personnalisée dans toute la ressource (exemple : GeoLocation) en procédant comme suit :

   1. Cliquez avec le bouton droit sur le dossier éléments et sélectionnez **Créer** > **Créer un nœud**.

      ![Créer un nœud dans CRX](assets/itemscreatenode.png)

   1. Assurez-vous que la boîte de dialogue de création du nœud possède les valeurs suivantes et cliquez sur **OK** :

      **Nom :** GeoLocation (ou le nom que vous souhaitez donner à cette propriété)

      **Type :** nt:unstructured

      ![Créez un nœud : Geolocation](assets/geographicallocationcreatenode.png)

   1. Cliquez sur le nouveau noeud que vous avez créé (ici GeoLocation). CRX affiche les propriétés du nœud.
   1. Ajoutez les propriétés suivantes au noeud (ici GeoLocation) :

      | **Nom** | **Type** | **Valeur** |
      |---|---|---|
      | fieldLabel | Chaîne | Nom que vous souhaitez donner au champ/à la propriété. (Ici : Emplacement des destinataires) |
      | name | Chaîne | `./extendedproperties/GeoLocation` (conserver la valeur identique au nom du champ que vous avez créé sous le nœud d’éléments) |
      | renderReadOnly | Booléen | true |
      | sling:resourceType | Chaîne | `granite/ui/components/coral/foundation/form/textfield` |

   1. Cliquez sur **Enregistrer tout**.

1. Pour afficher votre personnalisation, passez la souris sur une ressource (texte, liste, condition ou fragment de mise en page) ou une lettre, cliquez sur **Afficher les propriétés**, puis cliquez sur **Modifier**. Le nouveau champ (Emplacement des destinataires) apparaît dans l’onglet De base des propriétés de la ressource/de la lettre.

   >[!NOTE]
   >
   >Vous devrez peut-être vider le cache du navigateur avant que votre personnalisation ne s’affiche dans l’interface utilisateur.

   ![Propriété personnalisée ajoutée à toutes les ressources](assets/lcoationofrecipientsui-1.png)

   >[!NOTE]
   >
   >Les propriétés communes à toutes les ressources que vous ajoutez apparaissent dans l’onglet de base des propriétés de la ressource. Par défaut, les propriétés courantes ajoutées pour toutes les ressources s’affichent sur la page des propriétés ainsi que sur la page de création des ressources. Pour masquer les propriétés communes, vous devez <!--link to show / hide properties]-->.

### Scénario : Ajout d’une liste déroulante et de valeurs personnalisées à une propriété/un champ personnalisé {#scenario-add-custom-drop-down-and-values-to-a-custom-property-field}

Ce scénario indique comment ajouter une propriété personnalisée à tous les types de ressources et y ajouter des valeurs de liste déroulante.

1. Faites un clic droit sur le dossier des éléments à l’emplacement suivant, puis sélectionnez **Nœud de recouvrement** :

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

1. Sous le nœud de recouvrement que vous venez de créer (/apps/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items)
Créez un nœud pour chacune des propriétés (champs) pour lesquelles vous souhaitez créer une liste déroulante (ici `geographicallocation`) de type nt:unstructured.
1. Ajoutez les propriétés suivantes au nœud (ici geographicallocation) et cliquez sur **Enregistrer tout** :

   <table>
   <tbody>
   <tr>
      <td><strong>Nom</strong></td>
      <td><strong>Type</strong></td>
      <td><strong>Valeur</strong></td>
   </tr>
   <tr>
      <td>fieldLabel</td>
      <td>Chaîne</td>
      <td>Nom que vous souhaitez donner au champ/à la propriété. (Ici : geographicallocation)</td>
   </tr>
   <tr>
      <td>name</td>
      <td>Chaîne</td>
      <td>./extendedproperties/geographicallocation (conserver la valeur identique au nom du champ que vous avez créé sous le nœud d’éléments).</td>
   </tr>
   <tr>
      <td>renderReadOnly</td>
      <td>Booléen</td>
      <td>true</td>
   </tr>
   <tr>
      <td>sling:resourceType</td>
      <td>Chaîne</td>
      <td>granite/ui/components/coral/foundation/form/select<br /> </td>
   </tr>
   </tbody>
   </table>

1. Sous le nœud de propriété (ici : geographicallocation), ajoutez un nouveau nœud portant le nom `items`. Sous le noeud éléments , ajoutez un noeud chacun pour les valeurs de la liste déroulante. Il est recommandé d’ajouter le premier noeud vide comme valeur par défaut de la liste déroulante, puis de spécifier aucune valeur pour le champ. Pour ajouter plusieurs options/valeurs de liste déroulante, répétez les étapes suivantes :

   1. Cliquez avec le bouton droit sur le nœud de propriété (ici geographicallocation) et sélectionnez **Créer** > **Créer un nœud**.
   1. Entrez comme nom de champ `item1,`, conservez le type nt:unstructured, puis cliquez sur **OK**.
   1. Ajoutez les propriétés suivantes au nœud que vous venez de créer (ici, item1), puis cliquez sur **Enregistrer tout** :

      <table>
         <tbody>
         <tr>
          <td><strong>Nom</strong></td>
          <td><strong>Type</strong></td>
          <td><strong>Valeur</strong></td>
         </tr>
         <tr>
          <td>text</td>
          <td>Chaîne</td>
          <td>Il s’agit de la valeur de l’option de liste déroulante visible par l’utilisateur. Laissez-la vide pour la valeur vide (par défaut) ou saisissez la valeur, telle que <strong>International</strong> ou <strong>Dans les États-Unis</strong>.<br /> </td>
         </tr>
         <tr>
          <td>value</td>
          <td>Chaîne</td>
          <td>Valeur stockée dans CRXDE pour le texte. Saisissez un mot-clé unique. <br /> </td>
         </tr>
         </tbody>
   </table>

   ![customizationdropdownvaluescrxde](assets/customizationdropdownvaluescrxde.png)

Une liste déroulante personnalisée s’affiche comme suit dans les propriétés des ressources :

![drop-down_customization](assets/drop-down_customization.png)

### Scénario : Onglet commun à tous les types de ressources {#scenario-common-tab-for-all-asset-types}

Ce scénario indique comment ajouter un onglet personnalisé, Destinataires, à tous les types de ressources (texte, liste, condition et fragments de mise en page) et aux lettres. L&#39;onglet Destinataires vous permet de définir toutes vos propriétés personnalisées relatives aux destinataires.

![Onglet personnalisé ajouté à tous les types de ressources](assets/recipientstab.png)

Grâce à la procédure suivante, vous pouvez ajouter un onglet avec un champ à toutes vos ressources :

1. Accédez à `https://'[server]:[port]'/[ContextPath]/crx/de` et connectez-vous en tant qu’administrateur.
1. Dans le dossier d’applications, créez un dossier appelé cmmetadataproperties avec un chemin/une structure semblables au dossier cmmetadataproperties situé dans le dossier de contenu. Pour cela, suivez les étapes ci-après :

   1. Cliquez avec le bouton droit sur le dossier cmmetadataproperties à l’emplacement suivant et sélectionnez **Nœud de recouvrement** :

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties`

      ![Nœud de recouvrement](assets/cmmetadatapropertiesoverlaynode.png)

   1. Assurez-vous que la boîte de dialogue du nœud de recouvrement possède les valeurs suivantes :

      **Chemin :** /libs/fd/cm/ma/gui/content/cmmetadataproperties

      **Emplacement :** /apps/

      **Faire correspondre les types de nœud :** Sélectionné

   1. Cliquez sur **OK**. La structure du dossier est créée dans le dossier des applications.

      ![Structure de dossiers de recouvrement créée dans CRX](assets/cmmetadatapropertiesappsfolder.png)

      Cliquez sur **Enregistrer tout**.

1. Sous le dossier cmmetadataproperties, ajoutez un nœud pour créer un onglet personnalisé pour toutes les ressources (exemple : commontab) en procédant comme suit :

   1. Cliquez avec le bouton droit sur le dossier cmmetadataproperties et sélectionnez **Créer** > **Créer un noeud**.

      ![Créer un nœud](assets/cmmetadatapropertiescreatenode.png)

   1. Assurez-vous que la boîte de dialogue de création du nœud possède les valeurs suivantes et cliquez sur **OK** :

      **Nom :** commontab (ou le nom que vous souhaitez donner à cette propriété)

      **Type :** nt:unstructured

   1. Cliquez sur le nouveau noeud que vous avez créé (ici commontab). CRX affiche les propriétés du nœud.
   1. Ajoutez les propriétés suivantes au nœud (ici commontab) :

      <table>
         <tbody>
         <tr>
          <td><strong>Nom</strong></td>
          <td><strong>Type</strong></td>
          <td><strong>Valeur</strong></td>
         </tr>
         <tr>
          <td>jcr:title</td>
          <td>Chaîne</td>
          <td>Nom que vous souhaitez donner à la colonne. (Ici : Destinataires)</td>
         </tr>
         <tr>
          <td>sling:resourceType</td>
          <td>Chaîne</td>
          <td>granite/ui/components/coral/foundation/container<br /> </td>
   </tr>
         </tbody>
       </table>

   1. Cliquez sur **Enregistrer tout**.

1. Pour le noeud tab créé à la dernière étape (ici commontab), créez un noeud appelé item à l’aide de l’étape suivante :

   1. Cliquez avec le bouton droit sur le noeud approprié (ici commontab) et sélectionnez **Créer** > **Créer un noeud**.
   1. Assurez-vous que la boîte de dialogue de création du nœud possède les valeurs suivantes et cliquez sur **OK** :

      **Nom :** items

      **Type :** nt:unstructured

   1. Cliquez sur **Enregistrer tout:**

1. Dans le nœud d’éléments que vous avez créé à l’étape précédente (sous commontab), ajoutez un nœud pour créer une colonne (ici Column1) dans l’onglet personnalisé (commontab) en suivant les étapes ci-après (pour ajouter d’autres colonnes, répétez cette étape) :

   1. Cliquez avec le bouton droit sur le noeud éléments et sélectionnez **Créer** > **Créer un noeud**.
   1. Assurez-vous que la boîte de dialogue de création du nœud possède les valeurs suivantes et cliquez sur **OK** :

      **Nom :** Column1 (ou le nom que vous souhaitez attribuer au nœud, notez que ce nom n’apparaît pas dans l’interface utilisateur).

      **Type :** nt:unstructured

   1. Ajoutez la propriété suivante au nœud (ici Column1) et cliquez sur **Enregistrer tout** :

      <table>
         <tbody>
         <tr>
           <td><strong>Nom</strong></td>
           <td><strong>Type</strong></td>
           <td><strong>Valeur</strong></td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>Chaîne</td>
           <td>granite/ui/components/coral/foundation/container<br /> </td>
         </tr>
         </tbody>
       </table>

1. Dans le nœud créé à l’étape précédente (ici Column1), ajoutez un nœud appelé items en procédant comme suit :

   1. Cliquez avec le bouton droit sur le noeud (ici Column1) et sélectionnez **Créer** > **Créer un noeud**.
   1. Assurez-vous que la boîte de dialogue de création du nœud possède les valeurs suivantes et cliquez sur **OK** :

      **Nom :** items

      **Type :** nt:unstructured

   1. Cliquez sur **Enregistrer tout**.

1. Pour créer un champ dans l’onglet personnalisé (ici Destinataires), ajoutez un noeud (ici GeographicalLocation). Cette propriété correspond à la colonne que vous avez créée. Pour créer le champ, procédez comme suit (pour créer d’autres champs/noeuds, répétez ces étapes.) :

   1. Cliquez avec le bouton droit sur le noeud éléments et sélectionnez **Créer** > **Créer un noeud**.
   1. Assurez-vous que la boîte de dialogue de création du nœud possède les valeurs suivantes et cliquez sur **OK** :

      **Nom :** GeographicalLocation (ou un autre nom pour la propriété de champ)

      **Type :** nt:unstructured

   1. Ajoutez les propriétés suivantes au noeud de champ (ici GeographicalLocation) et cliquez sur **Enregistrer tout**.

      | **Nom** | **Type** | **Valeur** |
      |---|---|---|
      | fieldLabel | Chaîne | Emplacement des destinataires (ou le nom que vous souhaitez donner au champ.) |
      | name | Chaîne | ./extendedproperties/GeographicalLocation |
      | renderReadOnly | Booléen | true |
      | sling:resourceType | Chaîne | `/libs/granite/ui/components/coral/foundation/form/textfield` |

1. Pour ajouter cet onglet pour les lettres, créez un dossier de recouvrement avec un chemin/une structure similaire au dossier des éléments suivants du chemin ci-après :

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   Afin de créer un recouvrement pour une lettre ou une ressource différente, utilisez le chemin suivant en remplaçant [assettype] par le texte, la condition, la liste, le dictionnaire de données ou le fragment :

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[assettype]/items/tabs/items`

   1. Faites un clic droit sur le dossier des éléments à l’emplacement suivant, puis sélectionnez **Nœud de recouvrement** :

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   1. Assurez-vous que la boîte de dialogue du nœud de recouvrement possède les valeurs suivantes :

      **Chemin:** `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

      **Emplacement :** /apps/

      **Faire correspondre les types de nœud :** Sélectionné

   1. Cliquez sur **OK**. Le dossier est créé. Cliquez sur **Enregistrer tout**.

1. Dans le dossier d’éléments que vous venez de créer, ajoutez un nœud dans l’onglet personnalisé dans la ressource (ici : mytab, ce nom n’apparaît pas dans l’interface utilisateur) en procédant comme suit :

   1. Cliquez avec le bouton droit sur le dossier éléments et sélectionnez **Créer** > **Créer un nœud**.
   1. Assurez-vous que la boîte de dialogue de création du nœud possède les valeurs suivantes et cliquez sur **OK** :

      **Nom :** mytab (ou le nom que vous souhaitez donner à cette propriété)

      **Type :** nt:unstructured

   1. Cliquez sur le nouveau noeud que vous avez créé (ici mytab). CRX affiche les propriétés du nœud.
   1. Ajoutez les deux propriétés suivantes au nœud (ici commontab) :

      <table>
         <tbody>
         <tr>
           <td><strong>Nom</strong></td>
           <td><strong>Type</strong></td>
           <td><strong>Valeur</strong></td>
         </tr>
         <tr>
           <td>path<br /> </td>
           <td>Chaîne</td>
           <td>fd/cm/ma/gui/content/cmmetadataproperties/commontab<br /> </td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>Chaîne</td>
           <td>granite/ui/components/coral/foundation/include<br /> </td>
         </tr>
         </tbody>
       </table>

   1. Cliquez sur **Enregistrer tout**.

1. Pour afficher votre personnalisation, passez la souris sur la ressource appropriée (ici une lettre), cliquez sur Afficher les propriétés, puis cliquez sur **Modifier**. Le nouvel onglet (Destinataires) et le champ (Emplacement des destinataires) apparaissent dans l&#39;interface utilisateur.

   >[!NOTE]
   >
   >Vous devrez peut-être vider le cache du navigateur avant que votre personnalisation ne s’affiche dans l’interface utilisateur.

   ![Onglet personnalisé ajouté aux lettres](assets/recipientstab-1.png)

### Scénario : Ajout de propriétés personnalisées pour des types de ressources spécifiques {#scenario-adding-custom-properties-for-specific-asset-types}

Ce scénario indique comment ajouter une propriété à un type de ressource particulier, tel qu’un champ à toutes les ressources de texte. Grâce à ce processus, vous pouvez ajouter des propriétés à l’une des propriétés suivantes :

* Texte
* Condition
* Liste
* Fragment de disposition
* Dictionnaire de données
* Lettre

Par exemple, vous souhaitez ajouter une propriété, Emplacement des destinataires, uniquement aux ressources de texte, pour identifier la zone géographique à laquelle une ressource correspond.  ![Propriété personnalisée ajoutée à une ressource](assets/newtabui.png)

Procédez comme suit pour ajouter une propriété à un type de ressource :

1. Accédez à `https://'[server]:[port]'/[ContextPath]/crx/de` et connectez-vous en tant qu’administrateur.
1. Pour créer un onglet dans un type de ressource (tel que Texte), créez la structure de dossiers suivante dans le dossier dʼapplications :

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

   [TypeRessource] = texte, condition, liste, lettre, dictionnaire de données ou fragment

   Vous trouverez ci-dessous les étapes à suivre pour créer la structure de dossiers :

   1. Faites un clic droit sur le dossier des éléments à l’emplacement suivant, puis sélectionnez **Nœud de recouvrement** :

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

      Par exemple, si vous souhaitez créer une propriété pour des ressources de texte, sélectionnez le dossier suivant :

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/text/items/tabs/items`

      ![Nœud de recouvrement](assets/textitemstabsitemsoverlaynode1.png)

   1. Assurez-vous que la boîte de dialogue du nœud de recouvrement possède les valeurs suivantes :

      **Chemin :** /libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[TypeRessource]/items/tabs/items

      **Emplacement :** /apps/

      **Faire correspondre les types de nœud :** Sélectionné

   1. Cliquez sur **OK**. La structure du dossier est créée dans le dossier des applications.

      Cliquez sur **Enregistrer tout**.

1. Dans le dossier d’éléments que vous avez créé, ajoutez un nœud à l’onglet personnalisé dans la ressource (exemple : customtab) en procédant comme suit :

   1. Cliquez avec le bouton droit sur le dossier éléments et sélectionnez **Créer** > **Créer un nœud**.
   1. Assurez-vous que la boîte de dialogue de création du nœud possède les valeurs suivantes et cliquez sur **OK** :

      **Nom :** customtab (ou le nom que vous souhaitez donner à cette propriété)

      **Type :** nt:unstructured

   1. Cliquez sur le nouveau noeud que vous avez créé (ici customtab). CRX affiche les propriétés du nœud.
   1. Ajoutez les deux propriétés suivantes au nœud (ici commontab) :

      | **Nom** | **Type** | **Valeur** |
      |---|---|---|
      | sling:resourceType | Chaîne | granite/ui/components/coral/foundation/container |
      | jcr:title | Chaîne | Nom du champ de l’interface utilisateur (ici Mon onglet) |

   1. Cliquez sur **Enregistrer tout**.

1. Dans le nœud créé à l’étape précédente (ici customtab), ajoutez un nœud appelé items en procédant comme suit :

   1. Cliquez avec le bouton droit sur le noeud (ici customtab) et sélectionnez **Créer** > **Créer un noeud**.
   1. Assurez-vous que la boîte de dialogue de création du nœud possède les valeurs suivantes et cliquez sur **OK** :

      **Nom :** items

      **Type :** nt:unstructured

   1. Cliquez sur **Enregistrer tout**.

1. Dans le nœud d’éléments que vous avez créé à l’étape précédente (sous customtab), ajoutez un nœud pour créer une colonne (ici Column1) dans l’onglet personnalisé en procédant comme suit (pour ajouter d’autres colonnes, répétez cette étape) :

   1. Cliquez avec le bouton droit sur le noeud éléments et sélectionnez **Créer** > **Créer un noeud**.
   1. Assurez-vous que la boîte de dialogue de création du nœud possède les valeurs suivantes et cliquez sur **OK** :

      **Nom :** Column1 (ou le nom que vous souhaitez attribuer au nœud)

      **Type :** nt:unstructured

   1. Ajoutez la propriété suivante au nœud (ici Column1) et cliquez sur **Enregistrer tout**.

      <table>
         <tbody>
         <tr>
           <td><strong>Nom</strong></td>
           <td><strong>Type</strong></td>
           <td><strong>Valeur</strong></td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>Chaîne</td>
           <td>granite/ui/components/coral/foundation/container<br /> </td>
         </tr>
         </tbody>
       </table>

1. Pour chaque colonne que vous créez (comme indiqué à l’étape précédente, ici Column1), créez un nœud appelé item en procédant comme suit :

   1. Cliquez avec le bouton droit sur le noeud de colonne approprié (ici Column1) et sélectionnez **Créer** > **Créer un noeud**.
   1. Assurez-vous que la boîte de dialogue de création du nœud possède les valeurs suivantes et cliquez sur **OK** :

      **Nom :** items

      **Type :** nt:unstructured

   1. Cliquez sur **Enregistrer tout:**

1. Pour chacune des colonnes créées, créez un noeud sous le noeud éléments pour créer un champ dans le nouvel onglet de l’interface utilisateur. Répétez cette étape pour créer d&#39;autres champs dans la colonne :

   1. Cliquez avec le bouton droit sur le noeud approprié (ici éléments sous Column1) et sélectionnez **Créer** > **Créer un noeud**.
   1. Assurez-vous que la boîte de dialogue de création du nœud possède les valeurs suivantes et cliquez sur **OK** :

      **Nom :** un nom de votre choix (ici GeoLocation)

      **Type :** nt:unstructured

   1. Ajoutez les propriétés suivantes au nœud et cliquez sur **Enregistrer tout**.

      | **Nom** | **Type** | **Valeur** |
      |---|---|---|
      | fieldLabel | Chaîne | Emplacement des destinataires (ou le nom que vous souhaitez donner au champ.) |
      | name | Chaîne | `./extendedproperties/GeoLocation` |
      | renderReadOnly | Booléen | true |
      | sling:resourceType | Chaîne | granite/ui/components/coral/foundation/form/textfield |

1. Pour afficher votre personnalisation, passez la souris sur la ressource appropriée (ici un texte), cliquez sur Afficher les propriétés, puis cliquez sur **Modifier**. Le nouvel onglet et le nouveau champ (Emplacement des destinataires) apparaissent dans l&#39;interface utilisateur.

   >[!NOTE]
   >
   >Vous devrez peut-être vider le cache du navigateur avant que votre personnalisation ne s’affiche dans l’interface utilisateur.

   ![Propriété personnalisée ajoutée à une ressource spécifique](assets/newtabui-1.png)

### Affichage des propriétés personnalisées sur la page de création des ressources {#display-custom-properties-on-the-asset-creation-page}

Par défaut, les propriétés personnalisées ajoutées à de nouveaux onglets sont visibles uniquement dans la page de propriétés et non sur la page de création des ressources, car cette dernière ne dispose pas de la disposition sous forme d’onglets. Pour afficher les propriétés personnalisées sur la page de création des ressources avec d’autres propriétés, vous devez effectuer les opérations suivantes :

1. Faites un clic droit sur le dossier des éléments à l’emplacement suivant, puis sélectionnez **Nœud de recouvrement** :

   `/libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. Assurez-vous que la boîte de dialogue Noeud de recouvrement possède les valeurs suivantes pour la lettre. Pour les autres types de ressources, le chemin d’accès est indiqué dans le tableau suivant :

   **Chemin :** /libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items

   **Emplacement :** /apps/

   **Faire correspondre les types de nœud :** Sélectionné

   Selon le type de ressource, le chemin d’accès doit être le suivant :

   | **Type de ressource/document** | **Chemin à ajouter** |
   |---|---|
   | Texte | /libs/fd/cm/ma/gui/content/createasset/createtext/jcr:content/body/items/form/items/textwizard/items/editproperties/items/properties/items/tabs/items/tab1/items |
   | Liste | /libs/fd/cm/ma/gui/content/createasset/createlist/jcr:content/body/items/form/items/listwizard/items/editproperties/items/properties/items/tabs/items/tab1/items |
   | Condition | /libs/fd/cm/ma/gui/content/createasset/createcondition/jcr:content/body/items/form/items/condition/wizard/items/editproperties/items/properties/items/tabs/items/tab1/items/items/tab1/items |
   | Fragment | /libs/fd/cm/ma/gui/content/createasset/createfragment/jcr:content/body/items/form/items/fragmentwizard/items/properties/items/items/tabs2/items/tab1/items |
   | Lettre | /libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items/items/items/items/items |

1. Cliquez sur **OK**. La structure du dossier est créée dans le dossier des applications.

1. Sous le nœud d’éléments de recouvrement que vous avez créé, créez un nœud portant le nom col4 (ou toute autre nom) et cliquez sur **Enregistrer tout**.

   Par exemple, le nœud suivant est le nœud de recouvrement créé pour les lettres.

   `/apps/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. Ajoutez les propriétés suivantes au nœud que vous venez de créer (ici col4) et cliquez sur **Enregistrer tout** :

<table>
 <tbody>
  <tr>
   <td><strong>Nom</strong></td>
   <td><strong>Type</strong></td>
   <td><strong>Valeur</strong></td>
  </tr>
  <tr>
   <td>path</td>
   <td>Chaîne</td>
   <td><p>Ce chemin d'accès est le pointeur vers la colonne créée dans :</p>
    <ul>
     <li>Pour l’onglet commun à tous les types de ressources : /apps/fd/cm/ma/gui/content/cmmetadataproperties/commontab/items/col1</li>
     <li>Pour des propriétés différentes pour différents types de ressource : /apps/fd/cm/ma/gui/content/cmmetadataproperties/properties//items/tabs/items/customtab/items/col1</li>
    </ul> </td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>Chaîne</td>
   <td> granite/ui/components/coral/foundation/include<br /> </td>
  </tr>
 </tbody>
</table>

![customfieldappearinginmainproperties](assets/customfieldappearinginmainproperties.png)

Propriété personnalisée, Langue, qui s’affiche dans l’interface utilisateur pour créer une lettre

## Personnalisation du mode Liste pour afficher les propriétés personnalisées {#customize-the-list-view-to-show-custom-properties}

Après avoir ajouté une propriété personnalisée aux actifs Correspondence Management, vous devez apporter d’autres modifications à CRX/DE pour vous assurer que la propriété personnalisée s’affiche dans l’interface utilisateur de Correspondence Management.

Pour afficher la propriété personnalisée dans l’interface utilisateur de la liste des ressources de Correspondence Management, procédez comme suit :

1. Accédez à `https://'[server]:[port]'/[ContextPath]/crx/de` et connectez-vous en tant qu’administrateur.
1. Créez la structure de dossiers suivante dans le dossier des applications :

   `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   Vous trouverez ci-dessous les étapes à suivre pour créer la structure de dossiers :

   1. Cliquez avec le bouton droit sur le dossier des colonnes à l’emplacement suivant et sélectionnez **Nœud de recouvrement** :

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   1. Assurez-vous que la boîte de dialogue du nœud de recouvrement possède les valeurs suivantes :

      **Chemin :** /libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns

      **Emplacement :** /apps/

      **Faire correspondre les types de nœud :** Sélectionné

   1. Cliquez sur **OK**. La structure du dossier est créée dans le dossier des applications.

      Cliquez sur **Enregistrer tout**.

1. Pour chacune des propriétés créées, créez un noeud sous le noeud columns pour créer une colonne dans l’interface utilisateur. Répétez cette étape pour créer d’autres colonnes dans l’interface utilisateur :

   1. Cliquez avec le bouton droit sur le noeud approprié (colonnes) et sélectionnez **Créer** > **Créer un noeud**.
   1. Assurez-vous que la boîte de dialogue de création du nœud possède les valeurs suivantes et cliquez sur **OK** :

      **Nom :** un nom de votre choix (ici GeographicalLocation)

      **Type :** nt:unstructured

   1. Ajoutez les propriétés suivantes au nœud et cliquez sur **Enregistrer tout**.

      <table>
         <tbody>
         <tr>
           <td><strong>Nom</strong></td>
           <td><strong>Type</strong></td>
           <td><strong>Valeur</strong></td>
         </tr>
         <tr>
           <td>jcr:primaryType</td>
           <td>Nom</td>
           <td><p>nt:unstructured</p> </td>
         </tr>
         <tr>
           <td>jcr:title</td>
           <td>Chaîne</td>
           <td><p>GeographicalLocation</p> <p>Cette valeur apparaît comme en-tête de colonne dans l’interface utilisateur. </p> </td>
         </tr>
         <tr>
           <td>sortable</td>
           <td>Booléen</td>
           <td><p>true</p> <p>La valeur true indique que l’utilisateur peut trier les valeurs de cette colonne. </p> </td>
         </tr>
         </tbody>
       </table>

1. Créez la structure de dossiers suivante dans le dossier des applications :

   `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   Vous trouverez ci-dessous les étapes à suivre pour créer la structure de dossiers :

   1. Cliquez avec le bouton droit sur le dossier des colonnes à l’emplacement suivant et sélectionnez **Nœud de recouvrement** :

      `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   1. Assurez-vous que la boîte de dialogue du nœud de recouvrement possède les valeurs suivantes :

      **Chemin :** /libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage

      **Emplacement :** /apps/

      **Faire correspondre les types de nœud :** Sélectionné

   1. Cliquez sur **OK**. La structure du dossier est créée dans le dossier des applications.

      Cliquez sur **Enregistrer tout**.

1. Copiez le fichier childlistpage.jsp à partir de l’emplacement suivant :

   /libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp

   Collez le fichier à l’emplacement suivant :

   /apps/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/.

1. Ouvrez le fichier childlistpage.jsp (/apps/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp) et apportez les modifications suivantes :

   1. Ajoutez ce qui suit à la ligne 19 du fichier (à la suite de la déclaration de copyright).

      ```jsp
      <%@page import="java.util.Map"%>
      ```

   1. Ajoutez le code suivant d’une fonction qui récupère la valeur de chaque propriété personnalisée à la fin du fichier :

      ```jsp
      <%!
          private String getCustomPropertyValue(Map<String, Object> extendedProperties, String propertyName) {
      
              String propertyValue = "";
              if (extendedProperties.containsKey(propertyName)) {
                  propertyValue = (String) extendedProperties.get(propertyName);
              }
      
              return propertyValue;
          }
      %>
      ```

   1. Ajoutez le texte suivant avant le début de la balise &lt;tr>(&lt;tr &lt;%= attrs.build() %>>) :

      ```jsp
      <%
          String GeoLocation = "";
          if (asset != null) {
                  Map<String, Object> extendedProperties = asset.getExtendedProperties();
                  if (extendedProperties != null) {
                      GeoLocation = getCustomPropertyValue(extendedProperties,"GeoLocation");
                  }
          }
      %>
      ```

      Dans le code, GeoLocation est la valeur que vous définissez dans la propriété name lors de la création du noeud/champ personnalisé. Lors de la création d’un noeud/champ personnalisé, vous avez spécifié le nom de la propriété avec .préfixe /extendedproperties/ : ./extendedproperties/GeoLocation. Dans le code, le préfixe n’est pas obligatoire.

   1. Pour afficher la nouvelle propriété dans l’interface utilisateur, ajoutez une balise TD comme la suivante avant la balise de fermeture tr (&lt;/tr>) :

      ```jsp
      <td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
      ```

      Pour ajouter d’autres colonnes, répétez les étapes 6.3 et 6.4.

   1. Cliquez sur **Enregistrer tout**.

1. Pour afficher votre personnalisation, ouvrez la liste des fragments de document ou des lettres dans lesquelles vous avez ajouté la propriété personnalisée.

   La colonne et la propriété de l’interface utilisateur ajoutées au cours de cette procédure s’affichent pour tous les types de ressources. Toutefois, les valeurs de ces propriétés peuvent être saisies et affichées uniquement pour les types de ressources pour lesquels vous avez initialement ajouté la propriété personnalisée.

   Par exemple, avec le scénario suivant : ajout de propriétés personnalisées à des types de ressources spécifiques, vous ajoutez une propriété personnalisée aux ressources de texte ; vous pouvez saisir des propriétés personnalisées pour les ressources de texte uniquement. Si, toutefois, vous affichez cette propriété personnalisée dans l’interface utilisateur, la colonne s’affiche pour tous les types de fichier.

   ![custompropertyinlistview](assets/custompropertyinlistview.png)

1. (Facultatif) Par défaut, la nouvelle colonne apparaît comme la dernière colonne de l’interface utilisateur. Pour que la colonne s’affiche à une position spécifique, ajoutez la propriété suivante au noeud de colonne :

<table>
 <tbody>
  <tr>
   <td><strong>Nom</strong></td>
   <td><strong>Type</strong></td>
   <td><strong>Valeur</strong></td>
  </tr>
  <tr>
   <td>sling:orderBefore</td>
   <td>Chaîne</td>
   <td><p>Le nom du noeud de colonne au chemin "/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list/columns" devant lequel la colonne personnalisée doit apparaître sur l’interface utilisateur.</p> <p>Ici, si vous souhaitez que la colonne Emplacement géographique apparaisse avant (à gauche) la colonne Version, ajoutez la propriété sling:orderBefore au noeud GeoLocation au chemin "/apps/fd/cm/ma/gui/content/cmassets/jcr:content/views/list/columns/GeoLocation" et définissez la valeur de la propriété sur version.</p> </td>
  </tr>
 </tbody>
</table>

Lorsque vous ajoutez la propriété sling:orderBefore pour spécifier l’emplacement de la colonne, vous devez également mettre à jour l’ordre de la propriété correspondante. &lt;td> balise spécifiée à l’étape 6.4 de cette procédure. Par exemple, dans ce cas, vous devez vous assurer que la variable &lt;td> La balise de l’emplacement géographique est placée avant &lt;td> balise de la colonne Version :

```xml
<td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
<td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(version) %>"><%= xssAPI.encodeForHTML(version) %></td>
```

## Activation de la recherche de propriétés personnalisées {#enable-search-for-custom-properties}

Par défaut, la recherche de texte intégral n’inclut pas les propriétés personnalisées que vous ajoutez à l’interface utilisateur à l’aide de CRX/DE.

Pour inclure les propriétés personnalisées dans la recherche, vous devez autoriser l’indexation des propriétés personnalisées.

Pour ce faire, effectuez les étapes suivantes :

1. Accédez à `https://'[server]:[port]'/[ContextPath]/crx/de` et connectez-vous en tant qu’administrateur.
1. Accédez à `/oak:index/cmLucene`et ajoutez un nœud nommé **aggregates** à cet emplacement.

   1. Cliquez avec le bouton droit sur le dossier cmLucene et sélectionnez **Créer** > **Créer un noeud**.
   1. Assurez-vous que la boîte de dialogue de création du nœud possède les valeurs suivantes et cliquez sur **OK** :

      **Nom :** agrégats

      **Type :** nt:unstructured

   1. Cliquez sur **Enregistrer tout**.

1. Dans le dossier aggregates que vous venez de créer, ajoutez un nœud cm:resource. Sous cm:resource, ajoutez un nœud nommé include0.

   1. Cliquez avec le bouton droit sur le dossier aggregates et sélectionnez **Créer** > **Créer un noeud**. Assurez-vous que la boîte de dialogue de création du nœud possède les valeurs suivantes et cliquez sur **OK** :

      **Nom :** cm:resource

      **Type :** nt:unstructured

   1. Cliquez avec le bouton droit sur le dossier cm:resource et sélectionnez **Créer** > **Créer un noeud**. Assurez-vous que la boîte de dialogue de création du nœud possède les valeurs suivantes et cliquez sur **OK** :

      **Nom :** include0

      **Type :** nt:unstructured

   1. Cliquez sur le nouveau noeud que vous avez créé (ici include0). CRX affiche les propriétés du nœud.
   1. Ajoutez la propriété suivante au nœud (ici include0) :

      <table>
         <tbody>
         <tr>
           <td><strong>Nom</strong></td>
           <td><strong>Type</strong></td>
           <td><strong>Valeur</strong></td>
         </tr>
         <tr>
           <td>path</td>
           <td>Chaîne</td>
           <td>extendedProperties<br /> </td>
         </tr>
         </tbody>
       </table>

   1. Cliquez sur **Enregistrer tout**.

1. Accédez aux propriétés à l’emplacement suivant et ajoutez-y un emplacement de nœud : `/oak:index/cmLucene/indexRules/cm:resource/properties`

   Répétez cette étape pour chacune des propriétés personnalisées que vous souhaitez ajouter à la recherche.

   1. Cliquez avec le bouton droit sur le dossier properties et sélectionnez **Créer** > **Créer un noeud**.
   1. Assurez-vous que la boîte de dialogue de création du nœud possède les valeurs suivantes et cliquez sur **OK** :

      **Nom :** emplacement (ou le nom de la propriété personnalisée que vous souhaitez ajouter à la recherche)

      **Type :** nt:unstructured

   1. Cliquez sur le nouveau noeud que vous avez créé (ici location). CRX affiche les propriétés du nœud.
   1. Ajoutez les propriétés suivantes au nœud (ici location) :

      | **Nom** | **Type** | **Valeur** |
      |---|---|---|
      | analysé | Chaîne | true |
      | name | Chaîne | extendedProperties/location (ou le nom de la propriété à ajouter à la recherche) |
      | propertyIndex | Booléen | true |
      | useInSuggest | Booléen | true |

   1. Cliquez sur **Enregistrer tout**.

1. Vous pouvez désormais utiliser des valeurs de propriété personnalisées dans la recherche de texte intégral pour localiser les ressources appropriées.

>[!NOTE]
>
>Si vous ne parvenez toujours pas à effectuer une recherche, cela peut être dû à un problème d’indexation. Pour indexer de nouveau, accédez au nœud suivant et définissez la valeur de la propriété « re-index » sur true :
>
>/oak:index/cmLucene&quot; et modifier la valeur de la propriété

## Modifier l’affichage par défaut de la page de recherche {#change-default-view-of-the-search-page}

1. Accédez à `https://'[server]:[port]'/[ContextPath]/crx/de` et connectez-vous en tant qu’administrateur.
1. Dans le dossier dʼapplications, créez un dossier nommé list dont le chemin d’accès/la structure est similaire au dossier list situé sous /libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views :

   1. Faites un clic droit sur le dossier des éléments à l’emplacement suivant, puis sélectionnez **Nœud de recouvrement** :

      `/libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views/list`

   1. Assurez-vous que la boîte de dialogue du nœud de recouvrement possède les valeurs suivantes :

      **Chemin :** /libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views/list

      **Emplacement :** /apps/

      **Faire correspondre les types de nœud :** Sélectionné

   1. Cliquez sur **OK**. La structure du dossier est créée dans le dossier des applications.

   1. Cliquez sur **Enregistrer tout**.

1. Dans le noeud que vous venez de créer, ajoutez la propriété suivante à la liste, puis cliquez sur **Enregistrer tout**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nom</strong></td>
      <td><strong>Type</strong></td>
      <td><strong>Valeur</strong></td>
   </tr>
   <tr>
      <td>sling:orderBefore<br /> </td>
      <td>Chaîne</td>
      <td>card</td>
   </tr>
   </tbody>
   </table>

1. La personnalisation affiche les résultats de la recherche en mode Liste pour toutes les consoles, y compris Forms et les documents, Assets et Sites.

## Modification de la vue par défaut de la page des ressources {#change-default-view-of-the-assets-page}

>[!NOTE]
>
>Ces étapes modifient la vue par défaut de toutes les consoles telles que Forms et Documents, Ressources et Sites.

1. Accédez à `https://'[server]:[port]'/[ContextPath]/crx/de` et connectez-vous en tant qu’administrateur.
1. Dans le dossier dʼapplications, créez un dossier nommé list dont le chemin d’accès/la structure est similaire au dossier list situé sous :

   /libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/

   1. Faites un clic droit sur le dossier des éléments à l’emplacement suivant, puis sélectionnez **Nœud de recouvrement** :

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list`

   1. Assurez-vous que la boîte de dialogue du nœud de recouvrement possède les valeurs suivantes :

      **Chemin :** /libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list

      **Emplacement :** /apps/

      **Faire correspondre les types de nœud :** Sélectionné

   1. Cliquez sur **OK**. La structure du dossier est créée dans le dossier des applications.

   1. Cliquez sur **Enregistrer tout**.

1. Dans le noeud que vous venez de créer, ajoutez la propriété suivante à la liste, puis cliquez sur **Enregistrer tout**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nom</strong></td>
      <td><strong>Type</strong></td>
      <td><strong>Valeur</strong></td>
   </tr>
   <tr>
      <td>sling:orderBefore<br /> </td>
      <td>Chaîne</td>
      <td>card</td>
   </tr>
   </tbody>
   </table>

1. Effacez les cookies du navigateur ou utilisez le mode incognito de votre navigateur pour afficher les ressources. Par défaut, la page Ressources s’affiche dans la mise en page de la carte.

## Afficher/masquer des propriétés personnalisées sur les pages Création de ressources et Propriétés {#show-hide-custom-properties-on-asset-creation-and-properties-pages}

Pour afficher ou masquer les propriétés personnalisées, procédez comme suit :

1. Sous le nœud de propriété personnalisée, tel que geographicallocation, créez un nœud nommé « granite:rendercondition » de type « nt:unstructured ».
1. Ajoutez la propriété suivante au nœud et cliquez sur **Save All** :

   <table>
   <tbody>
   <tr>
      <td><strong>Nom</strong></td>
      <td><strong>Type</strong></td>
      <td><strong>Valeur</strong></td>
   </tr>
   <tr>
      <td>sling:resourceType<br /> </td>
      <td>Chaîne</td>
      <td>fd/cm/ma/gui/components/admin/assetsproperties/custompropertyconfig<br /> </td>
   </tr>
   </tbody>
   </table>

1. Pour masquer cette propriété sur la page de création des ressources, ajoutez la propriété suivante et cliquez sur **Enregistrer tout** :

   <table>
   <tbody>
   <tr>
      <td><strong>Nom</strong></td>
      <td><strong>Type</strong></td>
      <td><strong>Valeur</strong></td>
   </tr>
   <tr>
      <td>hideOnCreate<br /> </td>
      <td>Booléen</td>
      <td>true<br /> </td>
   </tr>
   </tbody>
   </table>

1. Pour masquer la propriété personnalisée sur la page des propriétés des ressources, ajoutez-y la propriété suivante, puis cliquez sur **Enregistrer tout**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nom</strong></td>
      <td><strong>Type</strong></td>
      <td><strong>Valeur</strong></td>
   </tr>
   <tr>
      <td>hideOnEdit<br /> </td>
      <td>Booléen</td>
      <td>true<br /> </td>
   </tr>
   </tbody>
   </table>

   Pour à nouveau afficher les valeurs, réinitialisez les valeurs de propriété sur `false` ou supprimez les entrées de propriété.
