---
title: Ajouter des bibliothèques clientes
seo-title: Ajouter des bibliothèques clientes
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
source-git-commit: 2b1cc29fbfdb80aff6b6fc5c6c4fc9093d12e418
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 8%

---


# Ajouter des bibliothèques clientes {#add-clientlibs}

## Ajouter un dossier ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

Créez un dossier ClientLibraryFolder nommé `clientlibs`qui contiendra les fichiers JS et CSS utilisés pour générer les pages de votre site.

La valeur de `categories`propriété donnée à cette bibliothèque cliente est l’identifiant utilisé pour inclure directement cette bibliothèque cliente à partir d’une page de contenu ou pour l’incorporer à d’autres bibliothèques clientes.

1. Using **CRXDE Lite**, expand `/etc/designs`

1. Cliquez avec le bouton droit `an-scf-sandbox` et sélectionnez `Create Node`

   * Nom (name) : `clientlibs`
   * Type : `cq:ClientLibraryFolder`

1. Cliquez sur **OK**

![chlimage_1-220](assets/chlimage_1-220.png)

Dans l’onglet **Propriétés** du nouveau `clientlibs` noeud, saisissez la propriété **catégories** :

* Nom :**catégories**
* Type : **Chaîne**
* Valeur : **apps.an-scf-sandbox**
* Cliquez sur **Ajouter**
* Cliquez sur **Enregistrer tout**

Remarque : la préface de la valeur catégories avec &quot;applications&quot;. est une convention permettant d&#39;identifier l&#39;application propriétaire comme se trouvant dans le dossier /apps et non /libs.  IMPORTANT : Ajoutez l’espace réservé `js.tx`t et **`css.txt`** les fichiers. (Il ne s’agit pas officiellement d’un cq:ClientLibraryFolder sans eux.)

1. Right-click **`/etc/designs/an-scf-sandbox/clientlibs`**
1. Sélectionner **Créer un fichier...**
1. Enter **Name:** `css.txt`
1. Sélectionner **Créer un fichier...**
1. Enter **Name:** `js.txt`
1. Cliquez sur **Enregistrer tout**

![chlimage_1-221](assets/chlimage_1-221.png)

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

Dans l’onglet **Propriétés** du noeud, saisissez la propriété String à plusieurs valeurs `clientlibs` incorporée ****. Cette opération intègre les bibliothèques côté [client (clientlibs) nécessaires pour les composants](/help/communities/client-customize.md#clientlibs-for-scf)SCF. Pour ce tutoriel, de nombreux clientlibs nécessaires aux composants Communautés sont ajoutés.

**Notez** qu’il peut s’agir de l’approche souhaitée pour un site de production, car il y a des considérations de commodité par rapport à la taille/vitesse des clientlibs téléchargés pour chaque page.

Si vous n’utilisez qu’une seule fonction sur une page, vous pouvez inclure directement la bibliothèque cliente complète de cette fonction sur la page, par exemple :

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

Dans ce cas, les clients SCF les plus basiques qui sont les clientlibs d&#39;auteur sont privilégiés :

* Nom (name) : **`embed`**
* Type : **`String`**
* Cliquez sur **`Multi`**
* Valeur: **`cq.social.scf`**

   * Il affiche une boîte de dialogue, **`+`** cliquez après chaque entrée pour ajouter les catégories clientlib suivantes :

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * Cliquez sur **OK**

* Cliquez sur **Enregistrer tout**

![chlimage_1-222](assets/chlimage_1-222.png)

Voici comment `/etc/designs/an-scf-sandbox/clientlibs` doit s’afficher le référentiel :

![chlimage_1-223](assets/chlimage_1-223.png)

### Inclure les bibliothèques clientes dans le modèle PlayPage {#include-clientlibs-in-playpage-template}

Sans inclure la catégorie `apps.an-scf-sandbox` ClientLibraryFolder sur la page, les composants SCF ne seront pas fonctionnels ni mis en forme, car les scripts JavaScript et le(s) style(s) nécessaires ne seront pas disponibles.

Par exemple, sans inclure les clientlibs, le composant de commentaires SCF apparaît sans style :

![chlimage_1-224](assets/chlimage_1-224.png)

Une fois les clientlibs apps.an-scf-sandbox inclus, le composant de commentaires SCF s’affiche avec le style suivant :

![chlimage_1-225](assets/chlimage_1-225.png)

L’instruction include appartient à la `head` section du `html` script. La valeur par défaut **`foundation head.jsp`** inclut un script qui peut être superposé : **`headlibs.jsp`**.

**Copiez headlibs.jsp et incluez clientlibs :**

1. Using **CRXDE Lite**, select **`/libs/foundation/components/page/headlibs.jsp`**

1. Cliquez avec le bouton droit de la souris et sélectionnez **Copier** (ou sélectionnez Copier dans la barre d’outils).
1. Sélectionner **`/apps/an-scf-sandbox/components/playpage`**
1. Cliquez avec le bouton droit de la souris et sélectionnez **Coller** (ou sélectionnez Coller dans la barre d’outils).
1. Doublon-cliquer **`headlibs.jsp`** pour l’ouvrir
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

![chlimage_1-226](assets/chlimage_1-226.png)

### Sauver votre travail jusqu&#39;à présent {#saving-your-work-so-far}

A ce stade, il existe un sandbox minimaliste, et il peut être utile d&#39;enregistrer sous forme de package pour que, lors de la lecture, si votre référentiel est corrompu et que vous souhaitez le début, vous puissiez éteindre votre serveur, renommer ou supprimer le dossier crx-quickstart/, activer votre serveur, télécharger et installer ce package enregistré, et ne pas avoir à répéter ces étapes les plus basiques.

Ce paquet existe sur le tutoriel [Créer un exemple de page](/help/communities/create-sample-page.md) pour ceux qui ne peuvent pas attendre d&#39;entrer et de début de lecture !...

Pour créer un pack :

* Dans CRXDE Lite, cliquez sur l’icône [Package](https://localhost:4502/crx/packmgr/)
* Cliquez sur **Créer un package**

   * Nom du package : an-scf-sandbox-minimal-pkg
   * Version : 0,1
   * Groupe: `leave as default`
   * Cliquez sur **OK**

* Cliquez sur **Modifier**

   * Onglet Sélectionner les **Filtres**

      * Click **Add filter**
      * Chemin racine : accéder à `/apps/an-scf-sandbox`
      * Cliquez sur **Terminé**
      * Click **Add filter**
      * Chemin racine : accéder à `/etc/designs/an-scf-sandbox`
      * Cliquez sur **Terminé**
      * Click **Add filter**
      * Chemin racine : accéder à `/content/an-scf-sandbox**`
      * Cliquez sur **Terminé**
   * Cliquez sur **Enregistrer**


* Click **Build**

Vous pouvez maintenant sélectionner **Télécharger** pour l’enregistrer sur le disque et **Télécharger le package** ailleurs, ainsi que sélectionner **Plus > Répliquer** pour pousser le sandbox vers une instance de publication localhost afin de développer le domaine de votre sandbox.