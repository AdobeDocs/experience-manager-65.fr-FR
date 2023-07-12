---
title: Ajout de bibliothèques clientes
description: Ajout d’un dossier ClientLibraryFolder
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 569f2052-b4fe-4f7f-aec9-657217cba091
source-git-commit: fd937341e26edd0c3edfced8e862066ebc30f9a3
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 7%

---

# Ajout de bibliothèques clientes {#add-clientlibs}

## Ajout d’un dossier ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

Création d’un dossier ClientLibraryFolder nommé `clientlibs` qui contiendra les éléments JS et CSS utilisés pour effectuer le rendu des pages de votre site.

Le `categories` La valeur de propriété donnée à cette bibliothèque cliente est l’identifiant utilisé pour inclure directement cette bibliothèque cliente à partir d’une page de contenu ou pour l’incorporer dans d’autres bibliothèques clientes.

1. Utilisation **CRXDE Lite**, développer `/etc/designs`

1. Clic droit `an-scf-sandbox` et sélectionnez `Create Node`

   * Nom : `clientlibs`.
   * Type : `cq:ClientLibraryFolder`

1. Cliquez sur **OK**

![add-client-library](assets/add-client-library.png)

Dans le **Propriétés** pour le nouvel onglet `clientlibs` , saisissez le **categories** property:

* Nom : **categories**
* Type :**chaîne**
* Valeur : **apps.an-scf-sandbox**
* Cliquez sur **Ajouter**
* Cliquez sur **Enregistrer tout**

Remarque : la préface de la valeur categories avec &quot;apps&quot;. est une convention permettant d’identifier &quot;l’application propriétaire&quot; comme se trouvant dans le dossier /apps, et non /libs. IMPORTANT : Ajouter un espace réservé `js.tx`t et **`css.txt`** fichiers . (Il ne s’agit pas officiellement d’un cq:ClientLibraryFolder sans ces éléments.)

1. Faites un clic-droit **`/etc/designs/an-scf-sandbox/clientlibs`**
1. Sélectionner **Créer un fichier...**
1. Entrée **Nom :** `css.txt`
1. Sélectionner **Créer un fichier...**
1. Entrée **Nom :** `js.txt`
1. Cliquez sur **Enregistrer tout**

![clientlibs-css](assets/clientlibs-css.png)

La première ligne des fichiers css.txt et js.txt identifie l’emplacement de base à partir duquel se trouvent les listes de fichiers suivantes.

Essayez de définir le contenu de css.txt sur

```
#base=.
 style.css
```

Créez ensuite un fichier sous clientlibs nommé style.css et définissez le contenu sur

`body {`

`background-color: #b0c4de;`

`}`

### Incorporer les bibliothèques clientes SCF {#embed-scf-clientlibs}

Dans le **Propriétés** pour la `clientlibs` , saisissez la propriété String à plusieurs valeurs. **embed**. Cela incorpore les [bibliothèques côté client (clientlibs) pour les composants SCF](/help/communities/client-customize.md#clientlibs-for-scf). Pour ce tutoriel, de nombreuses clientlibs nécessaires aux composants Communities sont ajoutées.

Il peut s’agir de l’approche souhaitée pour un site de production, car il y a des considérations pratiques par rapport à la taille/vitesse des clientlibs téléchargées pour chaque page.

Si vous utilisez une seule fonction sur une page, vous pouvez inclure la bibliothèque cliente complète de cette fonction directement sur la page, par exemple :

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

Dans ce cas, incluez-les toutes et ainsi, les clientlibs SCF les plus basiques qui sont les clientlibs de création sont préférées :

* Nom : **`embed`**.
* Type : **`String`**
* Cliquez sur **`Multi`**
* Valeur : **`cq.social.scf`**

   * Une boîte de dialogue s’affiche, puis cliquez sur **`+`** après chaque entrée pour ajouter les catégories clientlib suivantes :

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

![scf-clientlibs-view](assets/scf-clientlibs1.png)

### Inclure les bibliothèques clientes dans le modèle PlayPage {#include-clientlibs-in-playpage-template}

Sans inclure la variable `apps.an-scf-sandbox` Catégorie ClientLibraryFolder sur la page, les composants SCF ne sont pas fonctionnels ni mis en forme, car le code JavaScript et les styles nécessaires ne sont pas disponibles.

Par exemple, sans inclure les clientlibs, le composant de commentaires SCF apparaît sans style :

![clientlibs-comment](assets/clientlibs-comment.png)

Une fois les bibliothèques clientes apps.an-scf-sandbox incluses, le composant de commentaires SCF apparaît avec le style suivant :

![clientlibs-comment-styled](assets/clientlibs-comment1.png)

L’instruction d’inclusion appartient à la variable `head` de la section `html` script. La valeur par défaut **`foundation head.jsp`** inclut un script qui peut être superposé : **`headlibs.jsp`**.

**Copiez headlibs.jsp et incluez clientlibs :**

1. Utilisation **CRXDE Lite**, sélectionnez **`/libs/foundation/components/page/headlibs.jsp`**

1. Cliquez avec le bouton droit et sélectionnez **Copier** (ou sélectionnez Copier dans la barre d’outils)
1. Sélectionner **`/apps/an-scf-sandbox/components/playpage`**
1. Cliquez avec le bouton droit et sélectionnez **Coller** (ou sélectionnez Coller dans la barre d’outils)
1. Double-cliquez **`headlibs.jsp`** pour l’ouvrir
1. Ajoutez la ligne suivante à la fin du fichier.
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

Chargez votre site web dans le navigateur et vérifiez si l’arrière-plan n’est pas bleu.

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![community-play](assets/community-play.png)

### Sauver votre travail jusqu&#39;à présent {#saving-your-work-so-far}

À ce stade, il existe un environnement de test minimaliste. Il peut être intéressant de l’enregistrer sous la forme d’un package. Ainsi, lors de la lecture, si votre référentiel est corrompu et que vous souhaitez recommencer, vous pouvez désactiver votre serveur, renommer ou supprimer le dossier crx-quickstart/, activer votre serveur, télécharger et installer ce package enregistré, sans avoir à répéter ces étapes les plus basiques.

Ce module existe sur la variable [Création d’un exemple de page](/help/communities/create-sample-page.md) tutoriel pour ceux qui ne peuvent pas attendre d’entrer et de commencer à jouer !...

Pour créer un package :

* Dans le CRXDE Lite, cliquez sur [Icône Package](https://localhost:4502/crx/packmgr/)
* Cliquez sur **Créer un package**

   * Nom du module : an-scf-sandbox-minimal-pkg
   * Version : 0,1
   * Groupe : `leave as default`
   * Cliquez sur **OK**

* Cliquez sur **Modifier**

   * Sélectionner **Filtres** tab

      * Cliquez sur **Ajouter un filtre**
      * Chemin racine : accédez à `/apps/an-scf-sandbox`
      * Cliquez sur **Terminé**
      * Cliquez sur **Ajouter un filtre**
      * Chemin racine : accédez à `/etc/designs/an-scf-sandbox`
      * Cliquez sur **Terminé**
      * Cliquez sur **Ajouter un filtre**
      * Chemin racine : accédez à `/content/an-scf-sandbox**`
      * Cliquez sur **Terminé**

   * Cliquez sur **Enregistrer**

* Cliquez sur **Concevoir**

Maintenant, vous pouvez sélectionner **Télécharger** pour l’enregistrer sur le disque et **Télécharger le module** ailleurs, puis sélectionnez **Plus > Répliquer** pour envoyer l’environnement de test vers une instance de publication localhost afin de développer le domaine de votre environnement de test.
