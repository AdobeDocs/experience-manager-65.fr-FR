---
title: Configuration du conteneur et du mode de disposition
seo-title: Configuring Layout Container and Layout Mode
description: Découvrez comment configurer le conteneur et le mode de disposition.
seo-description: Learn how to configure Layout Container and Layout Mode.
uuid: 952b7c86-76ab-4699-8530-8638e46bb50f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 10940000-808a-48ae-8e46-61eccef71eab
legacypath: /content/docs/en/aem/6-2/administer/operations/page-authoring/configuring-responsive-layouting
exl-id: 61152b2d-4c0b-4cfd-9669-cf03d32cb7c7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 100%

---

# Configuration du conteneur et du mode de disposition{#configuring-layout-container-and-layout-mode}

La [disposition réactive](/help/sites-authoring/responsive-layout.md) est un mécanisme qui permet de réaliser un [design web réactif](https://fr.wikipedia.org/wiki/Responsive_Web_design). Les utilisateurs peuvent ainsi créer des pages Web dont la disposition et les dimensions dépendent des appareils utilisés.

>[!NOTE]
>
>Ce mécanisme est comparable aux mécanismes de [Web mobile](/help/sites-developing/mobile-web.md), qui utilisent le design web adaptatif (principalement pour l’interface utilisateur classique).

AEM effectue une mise en page réactive de vos pages en combinant plusieurs mécanismes :

* Composant [**Conteneur de mises en page**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)

   Ce composant fournit un système de paragraphes/grille qui permet d’ajouter et de positionner des composants dans une grille réactive. Il peut être utilisé comme système de paragraphes (parsys) par défaut pour votre page et mis à la disposition des créateurs dans l’explorateur de composants.

   * Le composant **Conteneur de dispositions** par défaut est défini sous :

      /libs/wcm/foundation/components/responsivegrid

   * Vous pouvez définir des conteneurs de mises en page :

      * en tant que composant que l’utilisateur peut ajouter à une page ;
      * comme système de paragraphes par défaut pour la page ;
      * les deux.

         Le conteneur de dispositions peut être utilisé de manière standard pour la page, tout en permettant à l’utilisateur d’y ajouter d’autres conteneurs de mises en page, par exemple, pour contrôler les colonnes.

* **[Mode Disposition](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**
Une fois que le conteneur de disposition est positionné sur la page, vous pouvez utiliser la 
**Disposition** pour positionner le contenu dans la grille réactive.

* [**Émulateur**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)
Permet de créer et de modifier des sites réactifs qui réorganisent la disposition en fonction de l’appareil ou de la taille de la fenêtre, en redimensionnant les composants de manière interactive. L’utilisateur peut ensuite afficher un aperçu du contenu à l’aide de l’émulateur.

>[!CAUTION]
>
>Bien que le composant **Conteneur de mises en page** soit disponible dans l’IU classique, il n’est entièrement fonctionnel et pris en charge que dans l’interface utilisateur optimisée pour les écrans tactiles.

Grâce à ces mécanismes de grille responsive, vous pouvez effectuer les opérations suivantes :

* Utilisez les points d’arrêt (qui indiquent le groupement des appareils) pour définir le comportement du contenu différent en fonction de la disposition de l’appareil.
* Masquez des composants en fonction du groupe d’appareils (définissez le point d’arrêt où un composant est masqué).
* Utilisez l’alignement horizontal sur la grille (placer les composants dans la grille, les redimensionner selon les besoins, définir quand ils doivent être réduits ou développés pour être côte à côte ou l’un au-dessus de l’autre) ;
* Contrôlez les colonnes.

>[!NOTE]
>
>Dans une installation prête à l’emploi, une mise en page responsive a été configurée pour le [site de référence We.Retail](/help/sites-developing/we-retail.md). Vous devez encore [activer le composant Conteneur de dispositions](#enable-the-layout-container-component-for-page) pour d’autres pages.

## Configuration de l’émulateur en responsive design {#configuring-the-responsive-emulator}

Ces tâches vous permettent d’afficher l’**émulateur** en responsive design sur votre site.

### Enregistrement de vos composants Page pour l’émulation {#register-your-page-components-for-emulation}

Pour permettre à l’émulateur de prendre en charge vos pages, vous devez enregistrer vos composants Page. Voir [Enregistrement de composants de page en vue de la simulation](/help/sites-developing/responsive.md#registering-page-components-for-simulation).

### Spécification des groupes d’appareils {#specify-the-device-groups}

Pour spécifier les groupes d’appareils qui s’affichent dans la liste des appareils de l’émulateur, voir [Définition des groupes de périphériques](/help/sites-developing/responsive.md#specifying-the-device-groups).

### Liaison de votre site aux groupes d’appareils spécifiés {#link-your-site-to-the-specified-device-groups}

Pour inclure l’émulateur, vous devez lier votre site aux groupes d’appareils. Consultez [Ajout de la liste des périphériques](/help/sites-developing/responsive.md#adding-the-devices-list) (pour l’interface utilisateur classique et l’interface utilisateur optimisée pour les écrans tactiles).

## Activation du mode Disposition pour votre site {#activate-layout-mode-for-your-site}

Ces procédures sont utilisées pour activer le mode **Disposition** sur votre site.

### Configuration des points d’arrêt {#configure-the-breakpoints}

Les [points d’arrêt](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate) :

* sont utilisés en responsive design ;
* peuvent être définis :

   * dans le modèle de page, à partir duquel les paramètres sont copiés dans les pages créées avec ce modèle ;
   * dans le nœud de page, à partir duquel les paramètres sont hérités par les pages enfants.

* définissent un titre et une largeur :

   * le titre décrit le groupe d’appareils génériques, avec l’orientation si nécessaire, par exemple, téléphone, tablette, tablette orientation Paysage ;
   * la largeur définit la largeur maximale en pixels pour ce groupe d’appareils générique. Par exemple, si le point d’arrêt du téléphone est défini à une largeur de 768 pixels, il s’agit de la largeur maximale de la mise en page utilisée pour un téléphone.

* sont visibles en tant que repères dans la partie supérieure de l’éditeur de page lorsque vous utilisez l’émulateur ;
* sont hérités de la hiérarchie de nœuds parents et peuvent être remplacés à volonté ;
* comportent un point d’arrêt par défaut, qui couvre tout ce qui se trouve au-delà du dernier *point d’arrêt* configuré.

Ils peuvent être définis à l’aide de CRXDE Lite ou de code XML.

>[!NOTE]
>
>Si vous configurez un nouveau projet :
>
>* vous devez ajouter des points d’arrêt aux modèles.
>
>Si vous migrez un projet existant (avec du contenu existant), vous devez :
>
>* ajouter des points d’arrêt aux modèles ;
>* ajouter les mêmes points d’arrêt aux pages existantes.
>
>  Comme l’héritage est en cours d’opération, vous pouvez le limiter à la page racine de votre contenu.

#### Configuration des points d’arrêt à l’aide de CRXDE Lite {#configuring-breakpoints-using-crxde-lite}

1. À l’aide de CRXDE Lite (ou équivalent), accédez à l’un des éléments suivants :

   * Définition de votre modèle
   * Nœud `jcr:content` de votre page

1. Sous `jcr:content`, créez le nœud :

   * Nom : `cq:responsive`
   * Type : `nt:unstructured`

1. En dessous, créez le nœud :

   * Nom : `breakpoints`
   * Type : `nt:unstructured`

1. Sous le nœud Points d’arrêt, vous pouvez créer un nombre illimité de points d’arrêt. Chaque définition correspond à un nœud unique avec les propriétés suivantes :

   * Nom : `<descriptive name>`
   * Type : `nt:unstructured`
   * Titre : `String` * `<descriptive title seen in Emulator>`*
   * Largeur : `Decimal` * `<value of breakpoint>`*

#### Configuration des points d’arrêt à l’aide de code XML {#configuring-breakpoints-using-xml}

Les points d’arrêt se trouvent à l’intérieur de la section `<jcr:content>` du fichier `.context.html` sous le dossier de modèles (ou de contenu) approprié.

Exemple de définition :

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

### Ajout d’un fournisseur d’informations responsive {#add-a-responsive-information-provider}

>[!NOTE]
>
>Cette opération est nécessaire uniquement si le composant Page ne repose pas sur le composant Page de base.

Copiez le nœud `cq:infoProviders` ci-dessous dans votre composant Page parent :

`/libs/foundation/components/page/cq:infoProviders/responsive`

## Activation du redimensionnement des composants pour la page {#enable-component-resizing-for-the-page}

Ces procédures sont nécessaires afin de redimensionner des composants en mode **Disposition**.

### Définition du conteneur de mises en page comme système de paragraphes principal {#set-layout-container-as-main-parsys}

Pour définir le système de paragraphes principal de votre page pour qu’il soit un conteneur de mises en page, vous devez définir le système de paragraphes de la façon suivante :

`wcm/foundation/components/responsivegrid`

Dans :

* le composant Page ;
* ou le modèle de page (pour une utilisation ultérieure).

Les deux exemples ci-dessous illustrent la définition :

* **HTL :**

   ```xml
   <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
   ```

* **JSP :**

   ```
   <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
   ```

### Inclusion du code CSS responsive {#include-the-responsive-css}

#### Code CSS pour les points d’arrêt à l’aide de LESS {#css-for-breakpoints-using-less}

AEM utilise le langage LESS pour générer les parties de code CSS nécessaires, qui doivent être incluses dans vos projets.

Vous devez également créer une [bibliothèque cliente](https://docs.adobe.com/content/docs/en/aem/6-0/develop/the-basics/clientlibs.html) pour fournir des appels de configuration et de fonction supplémentaires. L’extrait LESS ci-dessous est un exemple du code minimal à ajouter à votre projet :

```java
@import (once) "/libs/wcm/foundation/clientlibs/grid/grid_base.less";

/* maximum amount of grid cells to be provided */
@max_col: 12;

/* default breakpoint */
.aem-Grid {
  .generate-grid(default, @max_col);
}

/* phone breakpoint */
@media (max-width: 768px) {
  .aem-Grid {
    .generate-grid(phone, @max_col);
  }
}

/* tablet breakpoint */
@media (min-width: 769px) and (max-width: 1200px) {
  .aem-Grid {
    .generate-grid(tablet, @max_col);
  }
}
```

Vous trouverez la définition de la grille de base ci-dessous :

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### Considérations relatives au style {#styling-considerations}

Les composants contenus dans un conteneur responsive sont redimensionnés (ainsi que les éléments DOM HTML correspondants) en fonction de la taille de la grille responsive. Par conséquent, dans ce cas, il est recommandé d’éviter (ou de mettre à jour) les définitions d’éléments DOM à largeur fixe (contenus).

Par exemple :

* Avant :

   * `width=100px`

* Après :

   * `max-width=100px`

#### Redimensionnement et compatibilité des images adaptatives {#resizing-and-adaptive-image-compliance}

Tout redimensionnement d’un composant dans la grille déclenche les programmes d’écoute ci-dessous de façon appropriée :

* `beforeedit`
* `beforechildedit`
* `afteredit`

* `afterchildedit`

Pour redimensionner et mettre à jour correctement le contenu d’une image adaptative incluse dans une grille responsive, vous devez ajouter un ensemble `afterEdit` au programme d’écoute `REFRESH_PAGE` dans le fichier `EditConfig` de chaque composant contenu.

Par exemple :

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

Le mécanisme d’image adaptative est disponible par le biais d’un script qui contrôle la sélection de l’image appropriée pour la taille actuelle de la fenêtre. Il est activé une fois que le modèle DOM est prêt ou lors de la réception d’un événement dédié. Actuellement, la page doit être actualisée de manière à refléter correctement le résultat de l’action de l’utilisateur.

>[!CAUTION]
>
>Pour que les bibliothèques clientes de feuilles de style personnalisées fonctionnent correctement tant dans un environnement de création que dans un environnement de publication, elles doivent être chargées dans l’en-tête.

## Activation du composant Conteneur de mises en page pour une page {#enable-the-layout-container-component-for-page}

Ces tâches permettent aux créateurs de faire glisser des instances du composant **Conteneur de mises en page** dans la page.

### Activation du composant Conteneur de mises en page pour modifier une page {#enable-the-layout-container-component-for-page-editing}

Pour permettre aux créateurs d’ajouter d’autres grilles responsive dans des pages de contenu, vous devez activer le composant Conteneur de mises en page pour la page. Vous pouvez effectuer cette opération à l’aide de l’une des fonctions suivantes :

* **Environnement de création**

   Utilisez le [mode Conception](/help/sites-authoring/default-components-designmode.md) pour activer le composant **Conteneur de mises en page** pour une page.

* **Définition du composant**

   Lors de la définition du composant, utilisez `allowedComponent` ou une inclusion statique.

### Configuration de la grille du conteneur de mises en page {#configure-the-grid-of-the-layout-container}

Vous pouvez configurer le nombre de colonnes disponibles pour chaque instance spécifique du conteneur de mises en page.

1. **Environnement de création**

   Vous pouvez configurer le nombre de colonnes disponibles pour chaque instance spécifique du conteneur de mises en page.

   À cet effet, utilisez le [mode Conception](/help/sites-authoring/default-components-designmode.md), puis ouvrez la boîte de dialogue de conception pour le conteneur nécessaire. Vous pouvez spécifier le nombre de colonnes disponibles pour le positionnement et le redimensionnement. La valeur par défaut est 12.

1. **XML**

   Les définitions de la grille responsive sont spécifiées dans :

   `etc/design/<*your-project-name*>/.content.xml`

   Les paramètres ci-dessous peuvent être définis :

   * Nombre de colonnes disponibles :

      * `columns="{String}8"`
   * Composants qui peuvent être ajoutés au composant actif :

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`
