---
title: Utilisation de Sling Resource Merger dans AEM
seo-title: Utilisation de Sling Resource Merger dans AEM
description: Sling Resource Merger propose des services pour accéder à des ressources et les fusionner.
seo-description: Sling Resource Merger propose des services pour accéder à des ressources et les fusionner.
uuid: 0a28fdc9-caea-490b-8f07-7c4a6b802e09
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: ec712ba0-0fd6-4bb8-93d6-07d09127df58
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Utilisation de Sling Resource Merger dans AEM{#using-the-sling-resource-merger-in-aem}

## Objectif {#purpose}

Sling Resource Merger propose des services pour accéder à des ressources et les fusionner. Il fournit des mécanismes de différenciation (diff) pour les deux éléments suivants :

* **[Incrustations](/help/sites-developing/overlays.md)**de ressources à l’aide de[chemins de recherche configurés](/help/sites-developing/overlays.md#configuring-the-search-paths).

* **Remplacements** de boîtes de dialogue de composant pour l’interface utilisateur tactile (`cq:dialog`), à l’aide de la hiérarchie des types de ressource (par le biais de la propriété `sling:resourceSuperType`).

Avec Sling Resource Merger, les ressources et/ou propriétés incrustation/remplacement sont fusionnées avec les ressources/propriétés d’origine :

* Le contenu de la définition personnalisée a une priorité plus élevée que celle d’origine (en d’autres termes, elle la *superpose* ou elle la *remplace*).

* Si nécessaire, les [propriétés](#properties) définies dans la personnalisation indiquent comment utiliser le contenu fusionné à partir de l’original.

>[!CAUTION]
>
>Sling Resource Merger et les méthodes connexes ne peuvent être utilisées qu’avec [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Cela signifie également qu’ils ne sont adaptés qu’à l’interface utilisateur tactile standard ; les remplacements définis de cette manière, notamment, ne s’appliquent qu’à la boîte de dialogue tactile d’un composant.
>
>S’agissant des incrustations/remplacements relatifs à d’autres sections (y compris d’autres aspects d’un composant tactile ou de l’interface utilisateur classique), le nœud et la structure appropriés doivent être copiés à l’endroit où la personnalisation sera définie à partir de l’original.

### Objectifs pour AEM {#goals-for-aem}

Sling Resource Merger est utilisé dans AEM pour deux raisons principales :

* S’assurer que les changements de personnalisation ne sont pas effectués dans `/libs`.
* Réduire la structure qui est répliquée à partir de `/libs`.

   When using the Sling Resource Merger it is not recommended to copy the entire structure from `/libs` as this would result in too much information being held in the customization (usually `/apps`). Dupliquer les informations augmente inutilement le risque que des problèmes surviennent lorsque le système est mis à niveau.

>[!NOTE]
>
>Les remplacements ne dépendent pas des chemins de recherche. Ils utilisent la propriété `sling:resourceSuperType` pour établir la connexion.
>
>However, overrides are often defined under `/apps`, as best practice in AEM is to define customizations under `/apps`; this is because you must not change anything under `/libs`.

>[!CAUTION]
>
>You ***must*** not change anything in the `/libs` path.
>
>This is because the content of `/libs` is overwritten the next time you upgrade your instance (and may well be overwritten when you apply either a hotfix or feature pack).
>
>La méthode recommandée pour la configuration et d’autres modifications est la suivante :
>
>1. Recreate the required item (i.e. as it exists in `/libs`) under `/apps`
   >
   >
1. Make any changes within `/apps`
>



### Propriétés {#properties}

Resource Merger fournit les propriétés suivantes :

* `sling:hideProperties` ( `String` ou `String[]`)

   Indique la propriété, ou liste de propriétés, à masquer.

   The wildcard `*` hides all.

* `sling:hideResource` ( `Boolean`)

   Indique si les ressources doivent être entièrement masquées, y compris ses enfants.

* `sling:hideChildren` ( `String` ou `String[]`)

   Contient le noeud enfant, ou liste des noeuds enfants, à masquer. Les propriétés du nœud seront conservées.

   The wildcard `*` hides all.

* `sling:orderBefore` ( `String`)

   Contient le nom du nœud frère devant lequel le nœud actuel doit être positionné.

These properties affect how the corresponding/original resources/properties (from `/libs`) are used by the overlay/override (often in `/apps`).

### Création de la structure {#creating-the-structure}

Pour créer une incrustation ou un remplacement, vous devez recréer le nœud d’origine, avec la structure équivalente, sous la destination (qui est généralement `/apps`). Par exemple :

* Incrustation

   * La définition de l&#39;entrée de navigation pour la console Sites, comme illustré dans le rail, est définie à l&#39;adresse suivante :

      `/libs/cq/core/content/nav/sites/jcr:title`

   * Pour superposer cette opération, créez le noeud suivant :

      `/apps/cq/core/content/nav/sites`

      Mettez ensuite la propriété à jour `jcr:title` suivant vos besoins.

* Remplacement

   * La définition de la boîte de dialogue tactile pour la console Textes est définie à l’adresse suivante :

      `/libs/foundation/components/text/cq:dialog`

   * Pour le remplacer, créez le noeud suivant, par exemple :

      `/apps/the-project/components/text/cq:dialog`

Pour créer l’un de ces éléments, vous devez simplement recréer l’ossature. To simplify the recreation of the structure all intermediary nodes can be of type `nt:unstructured` (they do not have to reflect the original node type; for example, in `/libs`).

Ainsi, dans l’exemple d’incrustation ci-dessus, les nœuds suivants sont nécessaires :

```shell
/apps
  /cq
    /core
      /content
        /nav
          /sites
```

>[!NOTE]
>
>When using the Sling Resource Merger (i.e. when dealing with the standard, touch-enabled UI) it is not recommended to copy the entire structure from `/libs` as it would result in too much information being held in `/apps`. Cela peut entraîner des problèmes lorsque le système est mis à niveau.

### Cas d’utilisation {#use-cases}

Ces éléments, en liaison avec les fonctionnalités standard, vous permettent d’effectuer les opérations suivantes :

* **Ajouter une propriété**

   The property does not exist in the `/libs` definition, but is required in the `/apps` overlay/override.

   1. Create the corresponding node within `/apps`
   1. Créer une propriété sur ce noeud &quot;

* **Redéfinir une propriété (pas les propriétés créées automatiquement)**

   The property is defined in `/libs`, but a new value is required in the `/apps` overlay/override.

   1. Create the corresponding node within `/apps`
   1. Créez la propriété correspondante sur ce nœud (sous /`apps`).

      * La priorité de la propriété sera basée sur la configuration de Sling Resource Resolver.
      * Le type de la propriété peut être modifié.

         If you use a property type different to the one used in `/libs`, then the property type you define will be used.
   >[!NOTE]
   >
   >Le type de la propriété peut être modifié.

* **Redéfinir une propriété créée automatiquement**

   By default, auto-created properties (such as `jcr:primaryType`) are not subject to an overlay/override to ensure that the node type currently under `/libs` is respected. To impose an overlay/override you have to recreate the node in `/apps`, explicitly hide the property and redefine it:

   1. Create the corresponding node under `/apps` with the desired `jcr:primaryType`
   1. Créez la propriété `sling:hideProperties` sur ce noeud, avec la valeur définie sur celle de la propriété créée automatiquement ;
par exemple, `jcr:primaryType`

      Cette propriété, définie sous `/apps`, prend désormais la priorité sur celle définie sous `/libs`

* **Redéfinir un nœud et ses enfants**

   The node and its children are defined in `/libs`, but a new configuration is required in the `/apps` overlay/override.

   1. Combinez les actions des opérations suivantes :

      1. Masquer les enfants d’un nœud (conserver les propriétés du nœud).
      1. Redéfinir la (les) propriétés.

* **Masquer une propriété**

   The property is defined in `/libs`, but not required in the `/apps` overlay/override.

   1. Create the corresponding node within `/apps`
   1. Create a property `sling:hideProperties` of type `String` or `String[]`. Utilisez-la pour spécifier les propriétés à masquer/ignorer. Des caractères génériques peuvent également être utilisés. Par exemple :

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **Masquer un nœud et ses enfants**

   The node and its children are defined in `/libs`, but not required in the `/apps` overlay/override.

   1. Créez le nœud correspondant sous /apps.
   1. Create a property `sling:hideResource`

      * type: `Boolean`
      * value: `true`

* **Masquer les enfants d’un nœud (tout en conservant les propriétés du nœud)**

   Le nœud, ses propriétés et ses enfants sont définis dans `/libs`. The node and its properties are required in the `/apps` overlay/override, but some or all of the child nodes are not required in the `/apps` overlay/override.

   1. Créez le nœud correspondant sous `/apps`
   1. Create the property `sling:hideChildren`:

      * type: `String[]`
      * value: a list of the child nodes (as defined in `/libs`) to hide/ignore
      &amp;ast; peut être utilisé pour masquer/ignorer tous les noeuds enfants.


* **Réorganiser les nœuds**

   Le nœud et ses frères sont définis dans `/libs`. A new position is required so the node is recreated in the `/apps` overlay/override, where the new position is defined in reference to the appropriate sibling node in `/libs`.

   * Use the `sling:orderBefore` property:

      1. Créez le nœud correspondant sous `/apps`
      1. Create the property `sling:orderBefore`:

         Ceci spécifie le noeud (comme dans `/libs`) où le noeud actuel doit être placé avant :

         * type: `String`
         * value: `<before-SiblingName>`

### Appel de Sling Resource Merger à partir de votre code {#invoking-the-sling-resource-merger-from-your-code}

Sling Resource Merger comprend deux fournisseurs de ressources personnalisés : un pour les incrustations et un autre pour les remplacements. Chacun d’eux peut être appelé dans votre code en utilisant un point de montage :

>[!NOTE]
>
>Lorsque vous accédez à votre ressource, il est conseillé d’utiliser le point de montage approprié.
>
>De cette manière, vous avez la garantie que Sling Resource Merger est appelé et que la ressource entièrement fusionnée est renvoyée (réduction de la structure qui doit être répliquée à partir de `/libs`).

* Incrustation :

   * objectif : fusionner les ressources en fonction de leur chemin de recherche
   * mount point: `/mnt/overlay`
   * usage: `mount point + relative path`
   * Exemple :

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* Remplacement :

   * objectif : fusionner les ressources en fonction de leur super-type
   * mount point: `/mnt/overide`
   * usage: `mount point + absolute path`
   * Exemple :

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### Exemple d’utilisation {#example-of-usage}

Quelques exemples sont traités :

* Incrustation :

   * [Personnalisation des consoles](/help/sites-developing/customizing-consoles-touch.md)
   * [Personnalisation de la création de pages](/help/sites-developing/customizing-page-authoring-touch.md)

* Remplacement :

   * [Configuration de vos propriétés de page](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)

