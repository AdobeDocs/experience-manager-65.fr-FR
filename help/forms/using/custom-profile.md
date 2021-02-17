---
title: Création d’un profil personnalisé pour HTML5 forms
seo-title: Création d’un profil personnalisé pour HTML5 forms
description: Un profil HTML5 forms est un nœud de ressources dans Apache Sling. Il représente une version personnalisée du service de rendu HTML5 forms.
seo-description: Un profil HTML5 forms est un nœud de ressources dans Apache Sling. Il représente une version personnalisée du service de rendu HTML5 forms.
uuid: b9938280-a92c-4dde-b465-04372db3ca8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 62%

---


# Création d’un profil personnalisé pour HTML5 forms {#creating-a-custom-profile-for-html-forms}

Un profil est un noeud de ressources dans [Apache Sling](https://sling.apache.org/). Il représente une version personnalisée du service de rendu HTML5 forms. Vous pouvez utiliser le service de rendu HTML5 forms pour personnaliser l’apparence, le comportement et les interactions des formulaires HTML5. Un noeud de profil existe dans le dossier `/content` du référentiel JCR. Vous pouvez placer le noeud directement sous le dossier `/content` ou tout sous-dossier du dossier `/content`.

Le nœud de profil présente la propriété **sling:resourceSuperType** et la valeur par défaut est **xfaforms/profile**. Le script de rendu du noeud se trouve dans /libs/xfaforms/profil.

Les scripts Sling sont des scripts JSP. Ces scripts JSP servent de conteneurs pour rassembler le code HTML du formulaire demandé et les artefacts JS/CSS requis. Ces scripts Sling sont également appelés des **scripts de rendu de profil**. Le rendu de profil appelle le service Forms OSGi pour effectuer le rendu du formulaire demandé.

Le script de profil se trouve dans html.jsp et html.POST.jsp pour les demandes de GET et de POST. Vous pouvez copier et modifier un ou plusieurs fichiers à remplacer pour y ajouter vos personnalisations. N&#39;apportez aucune modification statique, la mise à jour du correctif écrase ces modifications.

Un profil comporte divers modules : les modules formRuntime.jsp, config.jsp, toolbar.jsp, formBody.jsp, nav_footer.jsp, et footer.jsp.

## formRuntime.jsp {#formruntime-jsp-br}

Les modules formRuntime.jsp contiennent des références aux bibliothèques clientes. Il décrit également des méthodes pour extraire des informations sur les paramètre régionaux dans la demande et inclure les messages dans la demande. Vous pouvez inclure des libs ou des styles JavaScript personnalisés dans le fichier formRuntime.jsp.

## config.jsp {#config-jsp}

Le module config.jsp contient les différentes configurations telles que les services de journalisation, de proxy, et la version du comportement. Dans config.jsp, vous pouvez personnaliser les configurations et les widgets. Vous pouvez également ajouter des configurations telles que l’enregistrement de widgets personnalisés au module config.jsp.

## toolbar.jsp {#toolbar-jsp}

Le fichier toolbar.jsp contient le code permettant de créer une barre d’outils colorée. Pour supprimer la barre d’outils, supprimez toolbar.jsp du module HTML.jsp

## formBody.jsp  {#formbody-jsp}

Le module formBody.jsp sert à la représentation HTML du formulaire XFA.

## nav_footer.jsp {#nav-footer-jsp}

HTML5 forms commence par générer uniquement la première page du formulaire. Lorsqu’un utilisateur fait défiler le formulaire, le reste des formulaires est chargé. La vitesse de chargement est ainsi optimisée. Le composant nav_footer.jsp contient tous les styles et éléments requis pour faciliter le chargement des pages dans le défilement.

## footer.jsp {#footer-jsp}

Le module footer.jsp est vide. Il vous permet d’ajouter des scripts qui ne sont utilisés que pour les interactions utilisateur.

## Création de profils personnalisés {#creating-custom-profiles}

Pour créer un profil personnalisé, procédez comme suit :

### Créez un nœud de profil {#create-profile-node}

1. Accédez à l’interface CRX DE à l’adresse URL : `https://'[server]:[port]'/crx/de` et connectez-vous à l’interface avec les informations d’identification de l’administrateur.

1. Dans le panneau de gauche, rendez-vous à l’emplacement suivant : */content/xfaforms/profiles*.

1. Copiez le paramètre par défaut du nœud et collez le nœud dans un autre dossier(*/content/profiles*) intitulé *hrform*.

1. Sélectionnez le nouveau nœud, *hrform*, puis ajoutez une propriété de chaîne : *sling:resourceType* avec la valeur : *hrform/demo*.

1. Cliquez sur Enregistrer tout dans le menu de la barre d’outils pour enregistrer les modifications.

### Créez un script de rendu de profil {#create-the-profile-renderer-script}

Après la création d’un profil personnalisé, ajoutez les informations de rendu à ce profil. Lorsqu’il reçoit une demande pour le nouveau profil, CRX vérifie l’existence du dossier/apps pour la page JSP à générer. Créez la page JSP dans le dossier /apps.

1. Dans le volet de gauche, accédez au dossier `/apps`.
1. Cliquez avec le bouton droit sur le dossier `/apps` et choisissez de créer un dossier nommé **hrform**.
1. Dans le dossier **hrform**, créez un dossier nommé **demo**.
1. Cliquez sur le bouton **Enregistrer tout**.
1. Accédez à `/libs/xfaforms/profile/html.jsp` et copiez le noeud **html.jsp**.
1. Collez le noeud **html.jsp** dans le dossier `/apps/hrform/demo` créé ci-dessus avec le même nom **html.jsp**, puis cliquez sur **Enregistrer**.
1. Si vous rencontrez d’autres composants du script de profil, suivez les étapes 1 à 6 pour copier les composants dans le dossier /apps/hrform/demo.

1. Pour vérifier que le profil est créé, ouvrez l’URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

Pour vérifier les formulaires, [Importez les formulaires](/help/forms/using/get-xdp-pdf-documents-aem.md) de votre système de fichiers local vers AEM Forms et [affichez l’aperçu du formulaire](/help/forms/using/previewing-forms.md) sur l’instance d’auteur du serveur AEM.
