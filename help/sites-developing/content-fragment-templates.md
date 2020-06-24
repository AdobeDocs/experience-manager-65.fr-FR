---
title: Modèles de fragment de contenu
seo-title: Modèles de fragment de contenu
description: Les modèles sont sélectionnés lors de la création d’un fragment de contenu et fournissent au nouveau fragment la structure de base, l’élément et la variation
seo-description: Les modèles sont sélectionnés lors de la création d’un fragment de contenu et fournissent au nouveau fragment la structure de base, l’élément et la variation
uuid: d147bac8-b710-40ed-9664-decb5ffcf8e7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: a975ea2e-5e24-4a96-bd62-63bb98836ff2
docset: aem65
translation-type: tm+mt
source-git-commit: a430c4de89bde3b907d342106465d3b5a7c75cc8
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 43%

---


# Modèles de fragment de contenu{#content-fragment-templates}

>[!CAUTION]
>
>Les [modèles de fragment de contenu](/help/assets/content-fragments/content-fragments-models.md) sont désormais recommandés pour créer tous les fragments.
>
>Les modèles de fragment de contenu sont utilisés pour tous les exemples dans We.Retail.

Les modèles sont sélectionnés lors de la création d’un fragment de contenu. Ils fournissent au nouveau fragment la structure de base, les éléments et la variation. Les modèles utilisés pour les fragments de contenu sont soumis au gestionnaire de configuration Granite.

Les modèles prêts à l’emploi sont stockés sous :

* `/libs/settings/dam/cfm/templates`

Vous pouvez créer des modèles spécifiques à vos sites pour les fragments de contenu sous :

* `/apps/settings/dam/cfm/templates`
Emplacement pour l’incrustation de modèles prêts à l’emploi ou la fourniture de modèles spécifiques à l’application à l’utilisateur qui ne sont pas destinés à être étendus/modifiés au moment de l’exécution.

* `/conf/global/settings/dam/cfm/templates`
Emplacement des modèles spécifiques au client à l’échelle de l’instance qui doivent être modifiés au moment de l’exécution.

The order of precedence is (in descending order) `/conf`, `/apps`, `/libs`.

>[!CAUTION]
>
>Vous ne devez ***rien*** modifier dans le chemin `/libs`.
>
>En effet, le contenu de `/libs` est remplacé dès que vous mettez à niveau votre instance (et risque de l’être si vous appliquez un correctif ou un Feature Pack).
>
>La méthode recommandée pour la configuration et d’autres modifications est la suivante :
>
>1. Recreate the required item (i.e. as it exists in `/libs`) under `/apps`
   >
   >
1. Apportez les modifications désirées dans `/apps`
>



La structure de base d’un modèle est stockée sous :

```xml
conf
  global
    settings
      dam
        cfm
          templates
            <template-name>
              ...
```

La structure spécifique étant :

```xml
+ <template-name>
    - jcr:primaryType
    - jcr:title
    - jcr:description
    - initialAssociatedContent
    - precreateElements
    - version
    + elements
        - jcr:primaryType
        + <element-name>
            - jcr:primaryType
            - jcr:title
            - defaultContent
            - initialContentType
            - name
        ... + other element definitions
    + variations
        - jcr:primaryType
        + <variation-name>
            - jcr:primaryType
            - jcr:title
            - jcr:description
            - name
        ... + other variation definitions
```

Plus de détails sur les nœuds et leurs propriétés : 

* **Template (Modèle)**

   <table>
   <tbody>
    <tr>
     <th>Nom</th>
     <th>Type</th>
     <th>Valeur</th>
    </tr>
    <tr>
     <td><code>&lt;<em>template-name</em>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>Ce noeud est la racine de chaque modèle. Il est obligatoire et doit avoir un nom unique.</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>requis<br /> </p> </td>
     <td>Titre du modèle (affiché dans l’assistant <strong>Créer un fragment</strong> ).</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>facultatif</p> </td>
     <td>Texte décrivant l’objectif du modèle (affiché dans l’assistant <strong>Créer un fragment</strong> ).</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>facultatif</p> </td>
     <td>Tableau contenant les chemins d’accès aux collections qui doivent être associées par défaut à un fragment de contenu nouvellement créé.</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>requis</p> </td>
     <td><p><code>true</code>, si les sous-ressources représentant les éléments (à l’exception de l’élément maître) du fragment de contenu doivent être créées lors de la création du fragment de contenu ; <em>false</em> s’ils doivent être créés "à la volée".</p> <p><strong>Remarque</strong>: actuellement, ce paramètre doit être défini sur <code>true</code>.</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>requis</p> </td>
     <td><p>version de la structure de contenu ; actuellement pris en charge :</p> <p><strong>Remarque</strong>: actuellement, ce paramètre doit être défini sur <code>2</code>.<br /> </p> </td>
    </tr>
   </tbody>
  </table>

* **Éléments**

   <table>
   <tbody>
    <tr>
     <th>Nom</th>
     <th>Type</th>
     <th>Valeur</th>
    </tr>
    <tr>
     <td><code>elements</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>requis</p> </td>
     <td><p>Noeud contenant la définition des éléments du fragment de contenu. It is mandatory and needs to contain at least one child node for the <strong>Main</strong> element, but can contain [1..n] nœuds enfants.</p> <p>Lorsque le modèle est utilisé, la sous-branche éléments est copiée dans la sous-branche modèle du fragment.</p> <p>The first element (as viewed in CRXDE Lite) is automatically considered to be the <i>main</i> element; the node name is irrelevant and the node itself does not have a special significance, apart from the fact that it is represented by the main asset; the other elements are handled as sub assets.</p> </td>
    </tr>
   </tbody>
  </table>

* **Nom de l’élément**

   <table>
   <tbody>
    <tr>
     <th>Nom</th>
     <th>Type</th>
     <th>Valeur</th>
    </tr>
    <tr>
     <td><code>&lt;<i>element-name</i>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>Ce noeud définit un élément. Il est obligatoire et doit avoir un nom unique.</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>requis</p> </td>
     <td>Titre de l’élément (affiché dans le sélecteur d’éléments de l’éditeur de fragments).</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>facultatif</p> <p>default: ""</p> </td>
     <td>Contenu initial de l'élément ; utilisé uniquement si <code>precreateElements</code><i> = </i><code>true</code></td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>facultatif</p> <p>default: <code>text/html</code></p> </td>
     <td><p>Type de contenu initial de l’élément ; utilisé uniquement si <code>precreateElements</code><i> = </i><code>true</code>; actuellement pris en charge :</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>requis</p> </td>
     <td>Nom interne de l’élément ; doit être unique pour le type de fragment.</td>
    </tr>
   </tbody>
  </table>

* **Variations**

   <table>
   <tbody>
    <tr>
     <th>Nom</th>
     <th>Type</th>
     <th>Valeur</th>
    </tr>
    <tr>
     <td><code>variations</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>facultatif</p> </td>
     <td>Ce noeud facultatif contient la définition des variations initiales du fragment de contenu.</td>
    </tr>
   </tbody>
  </table>

* **Nom de la variation**

   <table>
   <tbody>
    <tr>
     <th>Nom</th>
     <th>Type</th>
     <th>Valeur</th>
    </tr>
    <tr>
     <td><code>&lt;<i>variation-name</i>&gt;</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>requis si un noeud de variation est présent</p> </td>
     <td><p>Définit une variation initiale.<br /> La variation est ajoutée à tous les éléments du fragment de contenu par défaut.</p> <p>La variation aura le même contenu initial que l’élément correspondant (voir <code class="code">defaultContent/
       initialContentType</code>).</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>requis</p> </td>
     <td>Titre de la variation (affiché dans l’onglet <strong>Variation</strong> de l’éditeur de fragments (rail de gauche)).</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>facultatif</p> <p>default: ""</p> </td>
     <td>Texte qui fournit une description de la variation <span>(affichée dans l’onglet <strong>Variation</strong> de l’éditeur de fragments (rail de gauche)).</code></td>
    </tr>
   </tbody>
  </table>
