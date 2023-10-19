---
title: Application Sandbox initiale
description: Découvrez comment utiliser le modèle Contenu utilisé pour créer des pages de contenu, ainsi qu’un composant et un script utilisés pour effectuer le rendu des pages du site web.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: cbf9ce36-53a2-4f4b-a96f-3b05743f6217
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 14%

---

# Application Sandbox initiale {#initial-sandbox-application}

Dans cette section, vous allez créer les éléments suivants :

* La variable **[modèle](#createthepagetemplate)** qui est utilisé pour créer des pages de contenu dans l’exemple de site web.
* La variable **[composant et script](#create-the-template-s-rendering-component)** qui est utilisé pour effectuer le rendu des pages du site web.

## Création d’un modèle de contenu {#create-the-content-template}

Un modèle définit le contenu par défaut d’une nouvelle page. Les sites web complexes peuvent utiliser plusieurs modèles pour créer les différents types de pages du site. En outre, l’ensemble de modèles peut devenir un plan directeur utilisé pour déployer les modifications sur un cluster de serveurs.

Dans cet exercice, toutes les pages sont basées sur un modèle simple.

1. Dans le volet d’exploration du CRXDE Lite :

   * Sélectionnez `/apps/an-scf-sandbox/templates`.
   * **[!UICONTROL Créer]** > **[!UICONTROL Créer un modèle]**

1. Dans la boîte de dialogue Créer un modèle, entrez les valeurs ci-dessous et cliquez ensuite sur **[!UICONTROL Suivant]** :

   * Libellé : `playpage`
   * Titre : `An SCF Sandbox Play Template`
   * Description : `An SCF Sandbox template for play pages`
   * Type de ressource: `an-scf-sandbox/components/playpage`
   * Classement : &lt;leave as=&quot;&quot; default=&quot;&quot;>

   Le libellé est utilisé pour le nom du noeud.

   Le type de ressource s’affiche sur la page `playpage`&#39;s `jcr:content` Noeud comme propriété `sling:resourceType`. Il identifie le composant (ressource) qui effectue le rendu du contenu lorsqu’il est demandé par un navigateur.

   Dans ce cas, toutes les pages créées à l’aide de la variable `playpage` sont rendus par la fonction `an-scf-sandbox/components/playpage` composant. Par convention, le chemin d’accès au composant est relatif, ce qui permet à Sling de rechercher d’abord la ressource dans la variable `/apps` et, si elle est introuvable, dans la variable `/libs` dossier.

   ![create-content-template](assets/create-content-template-1.png)

1. Si vous utilisez la fonction copier/coller, assurez-vous que la valeur Type de ressource ne comporte aucun espace de début ou de fin.

   Cliquez sur **[!UICONTROL Suivant]**.

1. &quot;Chemins autorisés&quot; fait référence aux chemins des pages qui utilisent ce modèle, de sorte que le modèle soit répertorié pour la variable **[!UICONTROL Nouvelle page]** boîte de dialogue.

   Pour ajouter un chemin, cliquez sur le bouton plus `+` et type `/content(/.&ast;)?` dans la zone de texte qui s’affiche. Si vous utilisez la fonction copier/coller, assurez-vous qu’il n’existe aucun espace de début ou de fin.

   Remarque : La valeur de la propriété de chemin autorisée est une *expression régulière*. Les pages de contenu dont le chemin d’accès correspond à l’expression peuvent utiliser le modèle. Dans ce cas, l’expression régulière correspond au chemin de la propriété **/content** et toutes ses sous-pages.

   Lorsqu’un auteur crée une page ci-dessous `/content`, la variable `playpage` Le modèle intitulé &quot;Modèle de page d’un environnement de test SCF&quot; apparaît dans la liste des modèles disponibles à utiliser.

   Une fois la page racine créée à partir du modèle, l’accès au modèle peut être limité à ce site web en modifiant la propriété pour inclure le chemin racine dans l’expression régulière.

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. Cliquez sur **[!UICONTROL Suivant]**.

   Cliquez sur **[!UICONTROL Suivant]** dans le **[!UICONTROL Parents autorisés]** du panneau.

   Cliquez sur **[!UICONTROL Suivant]** dans le **[!UICONTROL Enfants autorisés]** du panneau.

   Cliquez sur **[!UICONTROL OK]**.

1. Après avoir cliqué sur OK et fini de créer le modèle, remarquez les triangles rouges qui s’affichent dans les coins des valeurs de l’onglet Propriétés pour le nouveau `playpage` modèle. Ces triangles rouges indiquent les modifications qui n’ont pas été enregistrées.

   Cliquez sur **[!UICONTROL Enregistrer tout]** pour enregistrer le nouveau modèle dans le référentiel.

   ![verify-content-template](assets/verify-content-template.png)

### Création du composant de rendu du modèle {#create-the-template-s-rendering-component}

Créez le *component* qui définit le contenu et effectue le rendu de toutes les pages créées en fonction de la variable [modèle playpage](#createthepagetemplate).

1. Dans CRXDE Lite, cliquez avec le bouton droit sur **`/apps/an-scf-sandbox/components`**, puis cliquez sur **[!UICONTROL Créer > Composant]**.
1. En définissant le nom du noeud (libellé) sur *playpage*, le chemin d’accès au composant est

   `/apps/an-scf-sandbox/components/playpage`

   qui correspond au type de ressource du modèle de page de lecture (éventuellement moins l’initial) **`/apps/`** partie du chemin).

   Dans la boîte de dialogue **[!UICONTROL Créer un composant]**, saisissez les valeurs de propriété suivantes :

   * Libellé : **playpage**
   * Titre : **Un composant SCF Sandbox Play**
   * Description : **Il s’agit du composant qui effectue le rendu du contenu d’une page Sandbox SCF.**
   * Super Type : *&lt;leave blank=&quot;&quot;>*
   * Groupe : *&lt;leave blank=&quot;&quot;>*

   ![create-template-component](assets/create-template-component.png)

1. Cliquez sur **[!UICONTROL Suivant]** jusqu’à ce que la variable **[!UICONTROL Enfants autorisés]** du panneau de la boîte de dialogue s’affiche :

   * Cliquez sur **[!UICONTROL OK]**.
   * Cliquez sur **[!UICONTROL Enregistrer tout]**.

1. Vérifiez que le chemin d’accès au composant et le resourceType du modèle correspondent.

   >[!CAUTION]
   >
   >Correspondance entre le chemin d’accès au composant de page de lecture et le `sling:resourceType` du modèle playpage est essentielle au bon fonctionnement du site web.

   ![verify-template-component](assets/verify-template-component.png)
