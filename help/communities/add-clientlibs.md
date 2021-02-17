---
title: Ajouter les bibliothèques clientes
seo-title: Ajouter les bibliothèques clientes
description: Ajouter un dossier ClientLibrary
seo-description: Ajouter un dossier ClientLibrary
uuid: 2944923d-caca-4607-81a4-4122a2ce8e41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 46f81c3f-6512-43f1-8ec1-cc717ab6f6ff
docset: aem65
translation-type: tm+mt
source-git-commit: fcdae5363e7a0070b5d6b76227e5c65efb71bc03
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 7%

---


# Ajouter les bibliothèques clientes {#add-clientlibs}

## Ajouter un dossier ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

Créez un dossier ClientLibraryFolder nommé `clientlibs` qui contiendra les fichiers JS et CSS utilisés pour générer les pages de votre site.

La valeur de propriété `categories` donnée à cette bibliothèque cliente est l&#39;identifiant utilisé pour inclure directement cette bibliothèque cliente à partir d&#39;une page de contenu ou pour l&#39;incorporer dans d&#39;autres bibliothèques clientes.

1. En utilisant **CRXDE Lite**, développez `/etc/designs`

1. Cliquez avec le bouton droit de la souris sur `an-scf-sandbox` et sélectionnez `Create Node`.

   * Nom : `clientlibs`
   * Type : `cq:ClientLibraryFolder`

1. Cliquez sur **OK**

![add-client-library](assets/add-client-library.png)

Dans l&#39;onglet **Propriétés** du nouveau noeud `clientlibs`, saisissez la propriété **catégories** :

* Nom :**catégories**
* Type :**chaîne**
* Valeur : **apps.an-scf-sandbox**
* Cliquez sur **Ajouter**
* Cliquez sur **Enregistrer tout**

Remarque : la préface de la valeur catégories avec &quot;applications&quot;. est une convention permettant d&#39;identifier l&#39;application propriétaire comme se trouvant dans le dossier /apps et non /libs.  IMPORTANT : Ajoutez les fichiers d’espace réservé `js.tx`t et **`css.txt`**. (Il ne s’agit pas officiellement d’un cq:ClientLibraryFolder sans eux.)

1. Faites un clic-droit **`/etc/designs/an-scf-sandbox/clientlibs`**
1. Sélectionnez **Créer un fichier...**
1. Saisissez **Nom :** `css.txt`
1. Sélectionnez **Créer un fichier...**
1. Saisissez **Nom :** `js.txt`
1. Cliquez sur **Enregistrer tout**

![clientlibs-css](assets/clientlibs-css.png)

La première ligne des fichiers css.txt et js.txt identifie l’emplacement de base à partir duquel les listes de fichiers suivantes doivent être trouvées.

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

Dans l&#39;onglet **Propriétés** du noeud `clientlibs`, saisissez la propriété String à plusieurs valeurs **embed**. Cette opération intègre les bibliothèques [côté client (clientlibs) nécessaires pour les composants SCF](/help/communities/client-customize.md#clientlibs-for-scf). Pour ce tutoriel, de nombreux clientlibs nécessaires aux composants Communautés sont ajoutés.

**Il** convient de noter que cette approche peut ou non être souhaitée pour un site de production car il y a des considérations de commodité par rapport à la taille/vitesse des clientlibs téléchargés pour chaque page.

Si vous n’utilisez qu’une seule fonction sur une page, vous pouvez inclure directement la bibliothèque cliente complète de cette fonction sur la page, par exemple :

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

Dans ce cas, les clients SCF les plus basiques qui sont les clientlibs d&#39;auteur sont privilégiés :

* Nom : **`embed`**
* Type : **`String`**
* Cliquez sur **`Multi`**
* Valeur : **`cq.social.scf`**

   * Il affiche une boîte de dialogue,
cliquez sur **`+`** après chaque entrée pour ajouter les catégories clientlib suivantes :

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * Cliquez sur **OK**

* Cliquez sur **Enregistrer tout**

![scf-clientlibs](assets/scf-clientlibs.png)

Voici comment `/etc/designs/an-scf-sandbox/clientlibs` doit maintenant apparaître dans le référentiel :

![scf-clientlibs-vue](assets/scf-clientlibs1.png)

### Inclure les bibliothèques clientes dans le modèle PlayPage {#include-clientlibs-in-playpage-template}

Sans inclure la catégorie `apps.an-scf-sandbox` ClientLibraryFolder sur la page, les composants SCF ne seront pas fonctionnels ni stylisés, car le(s) code(s) JavaScript et le(s) style(s) nécessaire(s) ne seront pas disponibles.

Par exemple, sans inclure les clientlibs, le composant de commentaires SCF apparaît sans style :

![clientlibs-comment](assets/clientlibs-comment.png)

Une fois les clientlibs apps.an-scf-sandbox inclus, le composant de commentaires SCF s’affiche avec le style suivant :

![clientlibs-comment-style](assets/clientlibs-comment1.png)

L&#39;instruction include appartient à la section `head` du script `html`. Le **`foundation head.jsp`** par défaut comprend un script qui peut être superposé : **`headlibs.jsp`**.

**Copiez headlibs.jsp et incluez clientlibs :**

1. En utilisant **CRXDE Lite**, sélectionnez **`/libs/foundation/components/page/headlibs.jsp`**

1. Cliquez avec le bouton droit de la souris et sélectionnez **Copier** (ou sélectionnez Copier dans la barre d’outils).
1. Sélectionner **`/apps/an-scf-sandbox/components/playpage`**
1. Cliquez avec le bouton droit de la souris et sélectionnez **Coller** (ou sélectionnez Coller dans la barre d’outils).
1. Doublon-cliquer sur **`headlibs.jsp`** pour l’ouvrir
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

Chargez votre site Web dans le navigateur et vérifiez si l’arrière-plan n’est pas bleu.

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![communauté-play](assets/community-play.png)

### Sauvegarder votre travail jusqu&#39;à présent {#saving-your-work-so-far}

A ce stade, il existe un sandbox minimaliste, et il peut être utile d&#39;enregistrer sous forme de package pour que, lors de la lecture, si votre référentiel est corrompu et que vous souhaitez le début, vous puissiez désactiver votre serveur, renommer ou supprimer le dossier crx-quickstart/, activer votre serveur, télécharger et installer ce package enregistré, et ne pas avoir à répéter ces étapes les plus basiques.

Ce package existe sur le didacticiel [Créer un exemple de page](/help/communities/create-sample-page.md) pour ceux qui ne peuvent pas attendre d&#39;entrer et de jouer à début !...

Pour créer un pack :

* Dans le CRXDE Lite, cliquez sur l’icône [Package](https://localhost:4502/crx/packmgr/)
* Cliquez sur **Créer un package**

   * Nom du package : an-scf-sandbox-minimal-pkg
   * Version : 0,1
   * Groupe: `leave as default`
   * Cliquez sur **OK**

* Cliquez sur **Modifier**

   * Sélectionner **Filtres** onglet

      * Cliquez sur **Ajouter le filtre**
      * Chemin racine : accédez à `/apps/an-scf-sandbox`
      * Cliquez sur **Terminé**
      * Cliquez sur **Ajouter le filtre**
      * Chemin racine : accédez à `/etc/designs/an-scf-sandbox`
      * Cliquez sur **Terminé**
      * Cliquez sur **Ajouter le filtre**
      * Chemin racine : accédez à `/content/an-scf-sandbox**`
      * Cliquez sur **Terminé**
   * Cliquez sur **Enregistrer**


* Cliquez sur **Créer**

Vous pouvez désormais sélectionner **Télécharger** pour l’enregistrer sur le disque et **Télécharger le package** ailleurs, ainsi que **Plus > Répliquer** pour pousser le sandbox vers une instance de publication hôte local afin de développer le domaine de votre sandbox.