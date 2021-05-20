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
exl-id: cbf9ce36-53a2-4f4b-a96f-3b05743f6217
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 10%

---

# Application Sandbox initiale {#initial-sandbox-application}

Dans cette section, vous allez créer les éléments suivants :

* **[template](#createthepagetemplate)** qui sera utilisé pour créer des pages de contenu dans l’exemple de site web.
* Composant **[et script](#create-the-template-s-rendering-component)** qui seront utilisés pour le rendu des pages du site web.

## Créer le modèle de contenu {#create-the-content-template}

Un modèle définit le contenu par défaut d’une nouvelle page. Les sites web complexes peuvent utiliser plusieurs modèles pour créer différents types de pages. De plus, l’ensemble de modèles peut devenir un plan directeur utilisé pour déployer les modifications apportées à un cluster de serveurs.

Dans le cadre de cet exercice, toutes les pages sont basées sur un modèle simple.

1. Dans le volet d’exploration du CRXDE Lite :

   * Sélectionner `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL Créer]**  >  **[!UICONTROL Créer un modèle]**

1. Dans la boîte de dialogue Créer un modèle, entrez les valeurs ci-dessous et cliquez ensuite sur **[!UICONTROL Suivant]** :

   * Libellé: `playpage`
   * Titre: `An SCF Sandbox Play Template`
   * Description: `An SCF Sandbox template for play pages`
   * Type de ressource: `an-scf-sandbox/components/playpage`
   * Classement : &lt;laisser comme valeur par défaut>

   Le libellé est utilisé pour le nom du noeud.

   Le type de ressource apparaît sur le noeud jcr:content de `playpage` en tant que propriété `sling:resourceType`. Il identifie le composant (ressource) qui effectue le rendu du contenu lorsqu’il est demandé par un navigateur.

   Dans ce cas, toutes les pages créées à l’aide du modèle `playpage` sont rendues par le composant `an-scf-sandbox/components/playpage`. Par convention, le chemin d’accès au composant est relatif, ce qui permet à Sling de rechercher d’abord la ressource dans le dossier `/apps` et, s’il n’est pas trouvé, dans le dossier `/libs`.

   ![create-content-template](assets/create-content-template-1.png)

1. Si vous utilisez la fonction copier/coller, assurez-vous que la valeur Type de ressource ne comporte aucun espace de début ou de fin.

   Cliquez sur **[!UICONTROL Suivant]**.

1. &quot;Chemins autorisés&quot; fait référence aux chemins d’accès des pages qui utilisent ce modèle, de sorte que le modèle soit répertorié pour la boîte de dialogue **[!UICONTROL Nouvelle page]**.

   Pour ajouter un chemin, cliquez sur le bouton plus `+` et saisissez `/content(/.&ast;)?` dans la zone de texte qui s’affiche. Si vous utilisez la fonction copier/coller, assurez-vous qu’il n’existe aucun espace de début ou de fin.

   Remarque : La valeur de la propriété de chemin autorisée est une *expression régulière*. Les pages de contenu dont le chemin d’accès correspond à l’expression peuvent utiliser le modèle. Dans ce cas, l’expression régulière correspond au chemin du dossier **/content** et de toutes ses sous-pages.

   Lorsqu’un auteur crée une page sous `/content`, le modèle `playpage` intitulé &quot;An SCF Sandbox Page Template&quot; apparaît dans la liste des modèles disponibles à utiliser.

   Une fois la page racine créée à partir du modèle, l’accès au modèle peut être limité à ce site web en modifiant la propriété pour inclure le chemin racine dans l’expression régulière, c’est-à-dire.

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. Cliquez sur **[!UICONTROL Suivant]**.

   Cliquez sur **[!UICONTROL Suivant]** dans le panneau **[!UICONTROL Parents autorisés]** .

   Cliquez sur **[!UICONTROL Suivant]** dans les panneaux **[!UICONTROL Enfants autorisés]**.

   Cliquez sur **[!UICONTROL OK]**.

1. Une fois que vous avez cliqué sur OK et que vous avez fini de créer le modèle, vous remarquerez des triangles rouges apparaissant dans les coins des valeurs de l’onglet Propriétés pour le nouveau modèle `playpage`. Ces triangles rouges indiquent les modifications qui n’ont pas été enregistrées.

   Cliquez sur **[!UICONTROL Enregistrer tout]** pour enregistrer le nouveau modèle dans le référentiel.

   ![verify-content-template](assets/verify-content-template.png)

### Création du composant de rendu du modèle {#create-the-template-s-rendering-component}

Créez le *composant* qui définit le contenu et effectue le rendu des pages créées en fonction du [modèle de page de lecture](#createthepagetemplate).

1. Dans CRXDE Lite, cliquez avec le bouton droit de la souris sur **`/apps/an-scf-sandbox/components`** et cliquez sur **[!UICONTROL Créer > Composant]**.
1. En définissant le nom du noeud (libellé) sur *playpage*, le chemin d’accès au composant est

   `/apps/an-scf-sandbox/components/playpage`

   qui correspond au type de ressource du modèle de page de lecture (éventuellement moins la partie **`/apps/`** initiale du chemin).

   Dans la boîte de dialogue **[!UICONTROL Créer un composant]**, saisissez les valeurs de propriété suivantes :

   * Libellé : **playpage**
   * Titre : **Un composant SCF Sandbox Play**
   * Description : **Il s’agit du composant qui effectue le rendu du contenu pour une page Sandbox SCF.**
   * Super Type : *&lt;laisser vide>*
   * Groupe : *&lt;laisser vide>*

   ![create-template-component](assets/create-template-component.png)

1. Cliquez sur **[!UICONTROL Suivant]** jusqu’à ce que le panneau **[!UICONTROL Enfants autorisés]** de la boîte de dialogue s’affiche :

   * Cliquez sur **[!UICONTROL OK]**.
   * Cliquez sur **[!UICONTROL Enregistrer tout]**.

1. Vérifiez que le chemin d’accès au composant et le resourceType du modèle correspondent.

   >[!CAUTION]
   >
   >La correspondance entre le chemin d’accès au composant playpage et la propriété sling:resourceType du modèle playpage est essentielle au bon fonctionnement du site web.

   ![verify-template-component](assets/verify-template-component.png)
