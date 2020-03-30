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
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Création d’un profil personnalisé pour HTML5 forms {#creating-a-custom-profile-for-html-forms}

A profile is a resource node in [Apache Sling](https://sling.apache.org/). Il représente une version personnalisée du service de rendu HTML5 forms. Vous pouvez utiliser le service de rendu de formulaires HTML5 pour personnaliser l’apparence, le comportement et les interactions des formulaires HTML5. A profile node exists in the `/content` folder in the JCR repository. You can place the node directly under the `/content` folder or any subfolder of the `/content` folder.

Le nœud de profil présente la propriété **sling:resourceSuperType** et la valeur par défaut est **xfaforms/profile**. Le script de rendu du noeud se trouve dans /libs/xfaforms/.

Les scripts Sling sont des scripts JSP. Ces scripts JSP servent de conteneurs pour rassembler le code HTML du formulaire demandé et les artefacts JS/CSS requis. Ces scripts Sling sont également appelés des **scripts de rendu de profil**. Le rendu  appelle le service Forms OSGi pour générer le formulaire demandé.

Le script de  est dans html.jsp et html.POST.jsp pour les requêtes GET et POST. Vous pouvez copier et modifier un ou plusieurs fichiers à remplacer pour y ajouter vos personnalisations. N’apportez aucune modification statique, la mise à jour du correctif écrase ces modifications.

Un profil comporte divers modules : les modules formRuntime.jsp, config.jsp, toolbar.jsp, formBody.jsp, nav_footer.jsp, et footer.jsp.

## formRuntime.jsp {#formruntime-jsp-br}

Les modules formRuntime.jsp contiennent des références aux bibliothèques clientes. Il décrit également des méthodes pour extraire des informations sur les paramètre régionaux dans la demande et inclure les messages dans la demande. Vous pouvez inclure vos propres libs ou styles JavaScript personnalisés dans le fichier formRuntime.jsp.

## config.jsp {#config-jsp}

Le module config.jsp contient les différentes configurations telles que les services de journalisation, de proxy, et la version du comportement. Dans config.jsp, vous pouvez personnaliser les configurations et les widgets. Vous pouvez également ajouter des configurations telles que l’enregistrement de widgets personnalisés au module config.jsp.

## toolbar.jsp {#toolbar-jsp}

Le fichier toolbar.jsp contient le code permettant de créer une barre d’outils colorée. Pour supprimer la barre d’outils, supprimez toolbar.jsp du module HTML.jsp

## formBody.jsp {#formbody-jsp}

Le module formBody.jsp est destiné à la représentation HTML du formulaire XFA.

## nav_footer.jsp {#nav-footer-jsp}

HTML5 forms commence par générer uniquement la première page du formulaire. Lorsqu’un utilisateur fait défiler le formulaire, le reste des formulaires est chargé. La vitesse de chargement est ainsi optimisée. Le composant nav_footer.jsp contient tous les styles et éléments requis pour faciliter le chargement des pages dans le défilement.

## footer.jsp {#footer-jsp}

Le module footer.jsp est vide. Il vous permet d’ajouter des scripts utilisés uniquement pour l’interaction de l’utilisateur.

## Création de profils personnalisés {#creating-custom-profiles}

Pour créer un  personnalisé, procédez comme suit :

### Créez un nœud de profil {#create-profile-node}

1. Navigate to the CRX DE interface at the URL: `https://'[server]:[port]'/crx/de` and log in to the interface with administrator credentials.

1. Dans le panneau de gauche, rendez-vous à l’emplacement suivant : */content/xfaforms/profiles*.

1. Copiez le paramètre par défaut du nœud et collez le nœud dans un autre dossier(*/content/profiles*) intitulé *hrform*.

1. Sélectionnez le nouveau nœud, *hrform*, puis ajoutez une propriété de chaîne : *sling:resourceType* avec la valeur : *hrform/demo*.

1. Cliquez sur Enregistrer tout dans le menu de la barre d’outils pour enregistrer les modifications.

### Créez un script de rendu de profil {#create-the-profile-renderer-script}

Après la création d’un profil personnalisé, ajoutez les informations de rendu à ce profil. Lorsqu’il reçoit une demande pour le nouveau profil, CRX vérifie l’existence du dossier/apps pour la page JSP à générer. Créez la page JSP dans le dossier /apps.

1. In the left pane, navigate to the `/apps` folder.
1. Right-click on the `/apps` folder and choose to create a folder with name **hrform**.
1. Insider the **hrform** folder create a folder named **demo**.
1. Cliquez sur le bouton **Enregistrer tout**.
1. Accédez au noeud `/libs/xfaforms/profile/html.jsp` html.jsp **** et copiez-le.
1. Paste **html.jsp** node into the `/apps/hrform/demo` folder created above with same name **html.jsp** and click **Save**.
1. Si vous rencontrez d’autres composants du script de profil, suivez les étapes 1 à 6 pour copier les composants dans le dossier /apps/hrform/demo.

1. Pour vérifier que le est créé, ouvrez l’URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

Pour vérifier les formulaires, [Importez les formulaires](/help/forms/using/get-xdp-pdf-documents-aem.md) de votre système de fichiers local vers AEM Forms et [affichez l’aperçu du formulaire](/help/forms/using/previewing-forms.md) sur l’instance d’auteur du serveur AEM.

[Contacter le support technique](https://www.adobe.com/account/sign-in.supportportal.html)
