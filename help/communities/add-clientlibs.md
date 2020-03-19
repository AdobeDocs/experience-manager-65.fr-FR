---
title: Ajouter Clientlibs
seo-title: Ajouter Clientlibs
description: Ajouter un dossier ClientLibraryFolder
seo-description: Ajouter un dossier ClientLibraryFolder
uuid: 2944923d-caca-4607-81a4-4122a2ce8e41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 46f81c3f-6512-43f1-8ec1-cc717ab6f6ff
docset: aem65
translation-type: tm+mt
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---


# Ajouter Clientlibs {#add-clientlibs}

## Ajouter un dossier ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

Créez un dossier ClientLibraryFolder nommé `clientlibs`qui contiendra les fichiers JS et CSS utilisés pour rendre les pages de votre site.

La valeur de `categories`propriété donnée à cette bibliothèque cliente est l’identifiant utilisé pour inclure directement cette bibliothèque cliente à partir d’une page de contenu ou pour l’incorporer à d’autres bibliothèques clientes.

1. Using **CRXDE Lite**, expand `/etc/designs`

1. Cliquez avec le bouton droit `an-scf-sandbox` et sélectionnez `Create Node`

   * Nom : `clientlibs`
   * Type : `cq:ClientLibraryFolder`

1. Cliquez sur **OK**

![chlimage_1-47](assets/chlimage_1-47.png)

Dans l’onglet **Propriétés** du nouveau `clientlibs` noeud, saisissez la propriété **du** :

* Nom :**catégories**
* Type : **Chaîne**
* Valeur : **apps.an-scf-sandbox**
* Cliquez sur **Ajouter**
* Cliquez sur **Enregistrer tout**

Remarque : la préface de la valeur de  avec &quot;apps&quot;. est une convention permettant d&#39;identifier l&#39;application propriétaire comme se trouvant dans le dossier /apps et non /libs.  IMPORTANT : Ajouter balise d’emplacement `js.tx`t et **`css.txt`** fichiers. (Il ne s’agit pas officiellement d’un dossier cq:ClientLibraryFolder sans eux.)

1. Right-click **`/etc/designs/an-scf-sandbox/clientlibs`**
1. Sélectionner **Créer un fichier...**
1. Enter **Name:** `css.txt`
1. Sélectionner **Créer un fichier...**
1. Enter **Name:** `js.txt`
1. Cliquez sur **Enregistrer tout**

![chlimage_1-48](assets/chlimage_1-48.png)

La première ligne des fichiers css.txt et js.txt identifie l’emplacement de base à partir duquel se trouve le de fichiers suivant.

Essayez de définir le contenu de css.txt sur

```
#base=.
 style.css
```

Créez ensuite un fichier sous clientlibs nommé style.css, puis définissez le contenu sur

`body {`

`background-color: #b0c4de;`

`}`

### Incorporer les bibliothèques clientes SCF {#embed-scf-clientlibs}

Dans l’onglet **Propriétés** du `clientlibs` noeud, saisissez la propriété Chaîne à plusieurs valeurs **incorporée**. Cette opération intègre les bibliothèques côté [client (clientlibs) nécessaires pour les composants](/help/communities/client-customize.md#clientlibs-for-scf)SCF. Pour ce tutoriel, de nombreux clients nécessaires aux composants Communautés sont ajoutés.

**Notez** qu’il peut s’agir de l’approche souhaitée ou non pour un site de production, car il y a des considérations de commodité par rapport à la taille/vitesse des clients téléchargés pour chaque page.

Si vous n’utilisez qu’une seule fonction sur une page, vous pouvez inclure directement la bibliothèque cliente complète de cette fonction sur la page, par exemple :

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

Dans ce cas, les clients SCF les plus basiques qui sont les clientlibs d’auteur sont préférés :

* Nom : **`embed`**
* Type : **`String`**
* Cliquez sur **`Multi`**
* Valeur: **`cq.social.scf`**

   * Il affiche une boîte de dialogue, cliquez **`+`** après chaque entrée pour ajouter le clientlib suivant :

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * Cliquez sur **OK**

* Cliquez sur **Enregistrer tout**

![chlimage_1-49](assets/chlimage_1-49.png)

Voici comment `/etc/designs/an-scf-sandbox/clientlibs` apparaître dans le référentiel :

![chlimage_1-50](assets/chlimage_1-50.png)

### Inclure les bibliothèques clientes dans le modèle PlayPage {#include-clientlibs-in-playpage-template}

Sans l’inclusion du `apps.an-scf-sandbox` ClientLibraryFolder sur la page, les composants SCF ne seront pas fonctionnels ni stylisés, car le(s) code(s) JavaScript(s) et le(s) style(s) nécessaire(s) ne seront pas disponibles.

Par exemple, sans inclure les clientlibs, le composant de commentaires SCF apparaît sans style :

![chlimage_1-51](assets/chlimage_1-51.png)

Une fois les clients apps.an-scf-sandbox inclus, le composant de commentaires SCF s’affiche avec le style suivant :

![chlimage_1-52](assets/chlimage_1-52.png)

L’instruction include appartient à la `head` section du `html` script. La valeur par défaut **`foundation head.jsp`** inclut un script qui peut être superposé : **`headlibs.jsp`**.

**Copiez headlibs.jsp et incluez clientlibs :**

1. Using **CRXDE Lite**, select **`/libs/foundation/components/page/headlibs.jsp`**

1. Cliquez avec le bouton droit de la souris et sélectionnez **Copier** (ou sélectionnez Copier dans la barre d’outils).
1. Sélectionner **`/apps/an-scf-sandbox/components/playpage`**
1. Cliquez avec le bouton droit de la souris et sélectionnez **Coller** (ou choisissez Coller dans la barre d’outils).
1. -cliquer **`headlibs.jsp`** pour l’ouvrir
1. Ajouter la ligne suivante à la fin du fichier
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. Cliquez sur **Enregistrer tout**

```xml
<%@ page session="false" %><%
%><%@include file="/libs/foundation/global.jsp" %><%
%><ui:includeClientLib categories="cq.foundation-main"/><%
%>
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
<% currentDesign.writeCssIncludes(pageContext); %>
<ui:includeClientLib categories="apps.an-scf-sandbox"/>
```

Chargez votre site Web dans le navigateur et voyez si l’arrière-plan n’est pas bleu.

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![chlimage_1-53](assets/chlimage_1-53.png)

### Sauver votre travail jusqu&#39;à présent {#saving-your-work-so-far}

A ce stade, il existe un sandbox minimaliste, et il peut être utile d&#39;enregistrer sous forme de package pour que, lors de la lecture, si votre référentiel est corrompu et que vous souhaitez le , vous puissiez désactiver votre serveur, renommer ou supprimer le dossier crx-quickstart/, activer votre serveur, télécharger et installer ce package enregistré, sans avoir à répéter ces étapes de base.

Ce paquet existe dans le didacticiel [Créer un exemple de page](/help/communities/create-sample-page.md) pour ceux qui ne peuvent pas attendre d&#39;entrer et d&#39; jouer!...

Pour créer un pack :

* Dans CRXDE Lite, cliquez sur l’icône [Package](https://localhost:4502/crx/packmgr/)
* Cliquez sur **Créer un package**

   * Nom du package : an-scf-sandbox-minimal-pkg
   * Version : 0.1
   * Groupe: `leave as default`
   * Cliquez sur **OK**

* Cliquez sur **Modifier**

   * Sélectionner l’onglet **de**

      * Click **Add filter**
      * Chemin racine : naviguer vers `/apps/an-scf-sandbox`
      * Cliquez sur **Terminé**
      * Click **Add filter**
      * Chemin racine : naviguer vers `/etc/designs/an-scf-sandbox`
      * Cliquez sur **Terminé**
      * Click **Add filter**
      * Chemin racine : naviguer vers `/content/an-scf-sandbox**`
      * Cliquez sur **Terminé**
   * Cliquez sur **Enregistrer**


* Click **Build**

Vous pouvez maintenant sélectionner **Télécharger** pour l’enregistrer sur le disque et **Télécharger le package** ailleurs, ainsi que **Plus > Répliquer** pour pousser le sandbox vers une instance de publication localhost afin d’étendre le domaine de votre sandbox.