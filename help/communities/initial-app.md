---
title: Application Sandbox initiale
seo-title: Application Sandbox initiale
description: Créer un modèle, un composant et un script
seo-description: Créer un modèle, un composant et un script
uuid: b0d03376-d8bc-4e98-aea2-a01744c64ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f74d225e-0245-4d5a-bb93-0ee3f31557aa
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 10%

---


# Application Sandbox initiale {#initial-sandbox-application}

Dans cette section, vous allez créer les éléments suivants :

* **[modèle](#createthepagetemplate)** qui sera utilisé pour créer des pages de contenu dans l’exemple de site Web.
* Le **[composant et le script](#create-the-template-s-rendering-component)** qui seront utilisés pour générer les pages du site Web.

## Create the Content Template {#create-the-content-template}

Un modèle définit le contenu par défaut d’une nouvelle page. Les sites web complexes peuvent utiliser plusieurs modèles pour créer différents types de pages. En outre, l&#39;ensemble de modèles peut devenir un modèle utilisé pour déployer les modifications apportées à un cluster de serveurs.

Dans le cadre de cet exercice, toutes les pages sont basées sur un modèle simple.

1. Dans le volet explorateur du CRXDE Lite :

   * Sélectionner `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL Créer]** > **[!UICONTROL Créer un modèle]**

1. Dans la boîte de dialogue Créer un modèle, entrez les valeurs ci-dessous et cliquez ensuite sur **[!UICONTROL Suivant]** :

   * Libellé: `playpage`
   * Titre: `An SCF Sandbox Play Template`
   * Description: `An SCF Sandbox template for play pages`
   * Type de ressource: `an-scf-sandbox/components/playpage`
   * Classement : &lt;laisser comme valeur par défaut>

   Le libellé est utilisé pour le nom du noeud.

   Le type de ressource apparaît sur le noeud jcr:content `playpage`en tant que propriété `sling:resourceType`. Il identifie le composant (ressource) qui effectue le rendu du contenu lorsqu&#39;il est demandé par un navigateur.

   In this case, all pages created using the `playpage` template are rendered by the `an-scf-sandbox/components/playpage` component. Par convention, le chemin d’accès au composant est relatif, ce qui permet à Sling de rechercher la ressource en premier dans le `/apps` dossier et, s’il n’est pas trouvé, dans le `/libs` dossier.

   ![create-content-template](assets/create-content-template-1.png)

1. Si vous utilisez copier/coller, assurez-vous que la valeur Type de ressource ne comporte aucun espace de début ou de fin.

   Cliquez sur **[!UICONTROL Suivant]**.

1. &quot;Chemins autorisés&quot; fait référence aux chemins des pages qui utilisent ce modèle, de sorte que le modèle soit répertorié pour la boîte de dialogue **[!UICONTROL Nouvelle page]** .

   Pour ajouter un chemin d’accès, cliquez sur le bouton Plus `+` et tapez `/content(/.&ast;)?` dans la zone de texte qui s’affiche. Si vous utilisez la fonction copier/coller, assurez-vous qu’il n’y a pas d’espace de début ou de fin.

   Note: The value of the allowed path property is a *regular expression*. Les pages de contenu dont le chemin correspond à l’expression peuvent utiliser le modèle. In this case, the regular expression matches the path of the **/content** folder and all its subpages.

   Lorsqu’un auteur crée une page ci-dessous `/content`, le `playpage` modèle intitulé &quot;Modèle de page de sandbox SCF&quot; apparaît dans une liste de modèles disponibles à utiliser.

   Une fois la page racine créée à partir du modèle, l’accès au modèle peut être limité à ce site Web en modifiant la propriété afin d’inclure le chemin racine dans l’expression régulière, c.-à-d.

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. Cliquez sur **[!UICONTROL Suivant]**.

   Cliquez sur **[!UICONTROL Suivant]** dans le panneau Parents **** autorisés.

   Cliquez sur **[!UICONTROL Suivant]** dans les panneaux Enfants **** autorisés.

   Cliquez sur **[!UICONTROL OK]**.

1. Une fois que vous avez cliqué sur OK et que vous avez fini de créer le modèle, des triangles rouges s’affichent dans les coins des valeurs de l’onglet Propriétés pour le nouveau `playpage` modèle. Ces triangles rouges indiquent les modifications qui n&#39;ont pas été enregistrées.

   Cliquez sur **[!UICONTROL Enregistrer tout]** pour enregistrer le nouveau modèle dans le référentiel.

   ![verify-content-template](assets/verify-content-template.png)

### Création du composant de rendu du modèle {#create-the-template-s-rendering-component}

Créez le *composant* qui définit le contenu et effectue le rendu des pages créées en fonction du modèle [de page de](#createthepagetemplate)lecture.

1. In CRXDE Lite, right-click **`/apps/an-scf-sandbox/components`** and click **[!UICONTROL Create > Component]**.
1. En définissant le nom du noeud (Étiquette) sur *la page* de lecture, le chemin d’accès au composant est

   `/apps/an-scf-sandbox/components/playpage`

   qui correspond au type de ressource du modèle de page de lecture (éventuellement moins la partie initiale **`/apps/`** du chemin).

   In the **[!UICONTROL Create Component]** dialog, type the following property values:

   * Libellé : **playpage**
   * Titre : **Composant SCF Sandbox Play**
   * Description : **Il s’agit du composant qui effectue le rendu du contenu de la page Sandbox SCF.**
   * Super Type : *&lt;laisser vide>*
   * Groupe : *&lt;laisser vide>*

   ![create-template-component](assets/create-template-component.png)

1. Click **[!UICONTROL Next]** until the **[!UICONTROL Allowed Children]** panel of the dialog appears:

   * Cliquez sur **[!UICONTROL OK]**.
   * Cliquez sur **[!UICONTROL Enregistrer tout]**.

1. Vérifiez que le chemin d’accès au composant et au resourceType du modèle correspondent.

   >[!CAUTION]
   >
   >La correspondance entre le chemin d’accès au composant de page de lecture et la propriété sling:resourceType du modèle de page de lecture est essentielle au bon fonctionnement du site Web.

   ![verify-template-component](assets/verify-template-component.png)