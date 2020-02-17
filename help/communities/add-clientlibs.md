---
title: Ajouter des bibliothèques clientes
seo-title: Ajouter des bibliothèques clientes
description: Ajout d’un dossier ClientLibrary
seo-description: Ajout d’un dossier ClientLibrary
uuid: 2944923d-caca-4607-81a4-4122a2ce8e41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 46f81c3f-6512-43f1-8ec1-cc717ab6f6ff
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Ajouter des bibliothèques clientes{#add-clientlibs}

## Ajout d’un dossier ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

Créez un dossier ClientLibraryFolder nommé `clientlibs`qui contiendra les fichiers JS et CSS utilisés pour rendre les pages de votre site.

La valeur de `categories`propriété donnée à cette bibliothèque cliente est l’identifiant utilisé pour inclure directement cette bibliothèque cliente à partir d’une page de contenu ou pour l’incorporer à d’autres bibliothèques clientes.

1. using **CRXDE Lite**, expand `/etc/designs`

1. cliquez avec le bouton droit `an-scf-sandbox` et sélectionnez `Create Node`

   * Nom : `clientlibs`
   * Type : `cq:ClientLibraryFolder`

1. Cliquez sur **OK**

![chlimage_1-47](assets/chlimage_1-47.png)

Dans l’onglet **Propriétés** du nouveau `clientlibs` noeud, saisissez la propriété **`categories`**property :

* Nom :**catégories**
* Type : **Chaîne**
* Valeur : **apps.an-scf-sandbox**
* click **Add**
* click **Save All**

Remarque : la préface de la valeur de catégories avec &quot;apps&quot;. est une convention permettant d&#39;identifier l&#39;application propriétaire comme se trouvant dans le dossier /apps et non /libs.  IMPORTANT : Ajoutez les fichiers d’espace réservé `js.tx`t et**`css.tx`**t. (Il ne s’agit pas officiellement d’un dossier cq:ClientLibraryFolder sans eux.)

1. clic droit **`/etc/designs/an-scf-sandbox/clientlibs`**
1. sélectionner **Créer un fichier...**
1. **enter** Name : `css.txt`
1. sélectionner **Créer un fichier...**
1. **enter** Name : `js.txt`
1. click **Save All**

![chlimage_1-48](assets/chlimage_1-48.png)

La première ligne de css.txt et js.txt identifie l’emplacement de base à partir duquel les listes de fichiers suivantes doivent être trouvées.

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

Si vous utilisez une seule fonctionnalité sur une page, vous pouvez inclure directement la bibliothèque cliente complète de cette fonctionnalité sur la page, par exemple, &lt;% ui:includeClientLib categories=cq.social.hbs.forum&quot; %>

Dans ce cas, les clients SCF les plus basiques qui sont les clientlibs d’auteur sont préférés :

* Nom : **`embed`**
* Type : **`String`**
* click **`Multi`**
* Valeur : **`cq.social.scf`***&lt;enter> affiche un clic de boîte de dialogue **[+] **après chaque entrée pour ajouter les catégories clientlib suivantes :*

   * **`cq.ckeditor`**
   * **`cq.social.author.hbs.comments`**
   * **`cq.social.author.hbs.forum`**
   * **`cq.social.author.hbs.rating`**
   * **`cq.social.author.hbs.reviews`**
   * **`cq.social.author.hbs.voting`**
   * Cliquez sur **OK**

* click **Save All**

![chlimage_1-49](assets/chlimage_1-49.png)

Voici comment `/etc/designs/an-scf-sandbox/clientlibs` apparaître dans le référentiel :

![chlimage_1-50](assets/chlimage_1-50.png)

### Inclure les bibliothèques clientes dans le modèle PlayPage {#include-clientlibs-in-playpage-template}

Sans inclure la catégorie `apps.an-scf-sandbox` ClientLibraryFolder sur la page, les composants SCF ne seront pas fonctionnels ni stylisés, car les scripts JavaScript et le ou les styles nécessaires ne seront pas disponibles.

Par exemple, sans inclure les clientlibs, le composant de commentaires SCF apparaît sans style :

![chlimage_1-51](assets/chlimage_1-51.png)

Une fois les clients apps.an-scf-sandbox inclus, le composant de commentaires SCF s’affiche avec le style suivant :

![chlimage_1-52](assets/chlimage_1-52.png)

L’instruction include appartient au <head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> de la section <html> script. La valeur par défaut **`foundation head.jsp`** inclut un script qui peut être superposé : **`headlibs.jsp`**.

**Copiez headlibs.jsp et incluez clientlibs :**

1. using **CRXDE Lite**, select **`/libs/foundation/components/page/headlibs.jsp`**

1. cliquez avec le bouton droit et sélectionnez **Copier **(ou sélectionnez Copier dans la barre d’outils).
1. select**`/apps/an-scf-sandbox/components/playpage`**
1. cliquez avec le bouton droit et sélectionnez **Coller **(ou sélectionnez Coller dans la barre d’outils).
1. double-cliquez **`headlibs.jsp`** pour l’ouvrir
1. ajouter la ligne suivante à la fin du fichier
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. click **Save All**

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

A ce stade, il existe un sandbox minimaliste, et il peut être utile d&#39;enregistrer sous forme de package pour que, lors de la lecture, si votre référentiel est corrompu et que vous souhaitez recommencer, vous puissiez désactiver votre serveur, renommer ou supprimer le dossier crx-quickstart/, activer votre serveur, télécharger et installer ce package enregistré, et ne pas avoir à répéter ces étapes de base.

Ce paquet existe dans le didacticiel [Créer un exemple de page](/help/communities/create-sample-page.md) pour ceux qui ne peuvent pas attendre d&#39;entrer et commencer à jouer!...

Pour créer un pack :

* de CRXDE Lite, cliquez sur l’icône [Package](https://localhost:4502/crx/packmgr/)
* click **Create Package**

   * Nom du package : an-scf-sandbox-minimal-pkg
   * Version : 0.1
   * Groupe : &lt;laisser comme valeur par défaut>
   * Cliquez sur **OK**

* click **Edit**

   * sélectionner **Filtres **onglet

      * click **Add filter**
      * Chemin racine : &lt;accédez à** /apps/an-scf-sandbox**>
      * click **Done**
      * click **Add filter**
      * Chemin racine : &lt;accédez à **/etc/designs/an-scf-sandbox**>
      * click **Done**
      * click **Add filter**
      * Chemin racine : &lt;accédez à **/content/an-scf-sandbox**>
      * click **Done**
   * click **Save**


* click **Build**

Vous pouvez maintenant sélectionner **Télécharger** pour l’enregistrer sur le disque et **Télécharger le package** ailleurs, ainsi que **Plus > Répliquer** pour pousser le sandbox vers une instance de publication localhost afin d’étendre le domaine de votre sandbox.