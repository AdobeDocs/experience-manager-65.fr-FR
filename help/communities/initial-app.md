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

* **[modèle](#createthepagetemplate)** qui sera utilisé pour créer des pages de contenu dans l&#39;exemple de site Web.
* Composant **[et script](#create-the-template-s-rendering-component)** qui seront utilisés pour générer les pages du site Web.

## Créer un modèle de contenu {#create-the-content-template}

Un modèle définit le contenu par défaut d’une nouvelle page. Les sites web complexes peuvent utiliser plusieurs modèles pour créer différents types de pages. En outre, l&#39;ensemble de modèles peut devenir un modèle utilisé pour déployer les modifications apportées à un cluster de serveurs.

Dans le cadre de cet exercice, toutes les pages sont basées sur un modèle simple.

1. Dans le volet explorateur du CRXDE Lite :

   * Sélectionner `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL Créer]**  >  **[!UICONTROL Créer un modèle]**

1. Dans la boîte de dialogue Créer un modèle, entrez les valeurs ci-dessous et cliquez ensuite sur **[!UICONTROL Suivant]** :

   * Libellé: `playpage`
   * Titre: `An SCF Sandbox Play Template`
   * Description: `An SCF Sandbox template for play pages`
   * Type de ressource: `an-scf-sandbox/components/playpage`
   * Classement : &lt;laisser comme valeur par défaut>

   Le libellé est utilisé pour le nom du noeud.

   Le type de ressource apparaît sur le noeud jcr:content de `playpage` en tant que propriété `sling:resourceType`. Il identifie le composant (ressource) qui effectue le rendu du contenu lorsqu&#39;il est demandé par un navigateur.

   Dans ce cas, toutes les pages créées à l&#39;aide du modèle `playpage` sont rendues par le composant `an-scf-sandbox/components/playpage`. Par convention, le chemin d’accès au composant est relatif, ce qui permet à Sling de rechercher d’abord la ressource dans le dossier `/apps` et, s’il n’est pas trouvé, dans le dossier `/libs`.

   ![create-content-template](assets/create-content-template-1.png)

1. Si vous utilisez copier/coller, assurez-vous que la valeur Type de ressource ne comporte aucun espace de début ou de fin.

   Cliquez sur **[!UICONTROL Next]** (Suivant).

1. &quot;Chemins autorisés&quot; fait référence aux chemins des pages qui utilisent ce modèle, de sorte que le modèle soit répertorié pour la boîte de dialogue **[!UICONTROL Nouvelle page]**.

   Pour ajouter un chemin d’accès, cliquez sur le bouton Plus `+` et tapez `/content(/.&ast;)?` dans la zone de texte qui s’affiche. Si vous utilisez la fonction copier/coller, assurez-vous qu’il n’y a pas d’espace de début ou de fin.

   Remarque : La valeur de la propriété de chemin autorisée est une *expression régulière*. Les pages de contenu dont le chemin correspond à l’expression peuvent utiliser le modèle. Dans ce cas, l’expression régulière correspond au chemin d’accès du dossier **/content** et de toutes ses sous-pages.

   Lorsqu&#39;un auteur crée une page sous `/content`, le modèle `playpage` intitulé &quot;Modèle de page de sandbox SCF&quot; apparaît dans une liste de modèles disponibles à utiliser.

   Une fois la page racine créée à partir du modèle, l’accès au modèle peut être limité à ce site Web en modifiant la propriété afin d’inclure le chemin racine dans l’expression régulière, c.-à-d.

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. Cliquez sur **[!UICONTROL Next]** (Suivant).

   Cliquez sur **[!UICONTROL Suivant]** dans le panneau **[!UICONTROL Parents autorisés]**.

   Cliquez sur **[!UICONTROL Suivant]** dans les panneaux **[!UICONTROL Enfants autorisés]**.

   Cliquez sur **[!UICONTROL OK]**.

1. Une fois que vous avez cliqué sur OK et que vous avez fini de créer le modèle, vous remarquerez que des triangles rouges s&#39;affichent dans les coins des valeurs de l&#39;onglet Propriétés pour le nouveau modèle `playpage`. Ces triangles rouges indiquent les modifications qui n&#39;ont pas été enregistrées.

   Cliquez sur **[!UICONTROL Enregistrer tout]** pour enregistrer le nouveau modèle dans le référentiel.

   ![verify-content-template](assets/verify-content-template.png)

### Créer le composant de rendu du modèle {#create-the-template-s-rendering-component}

Créez le composant ** qui définit le contenu et effectue le rendu des pages créées en fonction du modèle de page de lecture [](#createthepagetemplate).

1. Dans le CRXDE Lite, cliquez avec le bouton droit de la souris sur **`/apps/an-scf-sandbox/components`** et cliquez sur **[!UICONTROL Créer > Composant]**.
1. En définissant le nom du noeud (libellé) sur *playpage*, le chemin d’accès au composant est

   `/apps/an-scf-sandbox/components/playpage`

   qui correspond au type de ressource du modèle de page de lecture (éventuellement moins la partie initiale **`/apps/`** du chemin).

   Dans la boîte de dialogue **[!UICONTROL Créer un composant]**, saisissez les valeurs de propriété suivantes :

   * Libellé : **page de lecture**
   * Titre : **Composant SCF Sandbox Play**
   * Description : **Il s&#39;agit du composant qui effectue le rendu du contenu d&#39;une page Sandbox SCF.**
   * Super Type : *&lt;laisser vide>*
   * Groupe : *&lt;laisser vide>*

   ![create-template-component](assets/create-template-component.png)

1. Cliquez sur **[!UICONTROL Suivant]** jusqu’à ce que le panneau **[!UICONTROL Enfants autorisés]** de la boîte de dialogue s’affiche :

   * Cliquez sur **[!UICONTROL OK]**.
   * Cliquez sur **[!UICONTROL Enregistrer tout]**.

1. Vérifiez que le chemin d’accès au composant et au resourceType du modèle correspondent.

   >[!CAUTION]
   >
   >La correspondance entre le chemin d’accès au composant de page de lecture et la propriété sling:resourceType du modèle de page de lecture est essentielle au bon fonctionnement du site Web.

   ![verify-template-component](assets/verify-template-component.png)