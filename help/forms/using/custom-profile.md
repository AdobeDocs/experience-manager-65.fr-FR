---
title: Créer un profil personnalisé pour HTML5 forms
description: Un profil HTML5 forms est un nœud de ressources dans Apache Sling. Il représente une version personnalisée du service de rendu des formulaires HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
feature: HTML5 Forms,Mobile Forms
exl-id: cf86c810-c466-4894-acc2-d4faf49754cc
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '656'
ht-degree: 100%

---

# Créer un profil personnalisé pour HTML5 forms {#creating-a-custom-profile-for-html-forms}

Un profil est un nœud de ressources dans [Apache Sling](https://sling.apache.org/). Il représente une version personnalisée du service de rendu HTML5 forms. Vous pouvez utiliser le service de rendu HTML5 Forms pour personnaliser l’apparence, le comportement et les interactions de HTML5 Forms. Un nœud de profil existe dans le dossier `/content` du référentiel JCR. Vous pouvez mettre le nœud directement sous le dossier `/content` ou tout autre sous-dossier du dossier `/content`.

Le nœud de profil présente la propriété **sling:resourceSuperType** et la valeur par défaut est **xfaforms/profile**.  Le script de génération du nœud figure dans le dossier /libs/xfaforms/profile.

Les scripts Sling sont des scripts JSP. Ces scripts JSP servent de conteneurs pour rassembler le code HTML du formulaire demandé et les artefacts JS/CSS requis. Ces scripts Sling sont également appelés des **scripts de rendu de profil**. Le rendu de profil appelle le service Forms OSGi afin de générer le formulaire demandé.

Le script de profil est dans html.jsp et html.POST.jsp pour les demandes GET et POST. Vous pouvez copier et modifier un ou plusieurs fichiers à remplacer pour y ajouter vos personnalisations. N’apportez aucune modification car la mise à jour des correctifs écrase de telles modifications.

Un profil comporte divers modules : les modules formRuntime.jsp, config.jsp, toolbar.jsp, formBody.jsp, nav_footer.jsp, et footer.jsp.

## formRuntime.jsp {#formruntime-jsp-br}

Le module formRuntime.jsp contient des références aux bibliothèques clientes. Il décrit également des méthodes pour extraire des informations sur les paramètre régionaux dans la demande et inclure les messages dans la demande. Dans formRuntime.jsp, vous pouvez inclure des bibliothèques ou des styles javascript personnalisés.

## config.jsp {#config-jsp}

Le module config.jsp contient les différentes configurations telles que les services de journalisation, de proxy, et la version du comportement. Dans config.jsp, vous pouvez personnaliser les configurations et les widgets. Vous pouvez également ajouter des configurations telles que l’enregistrement de widgets personnalisés dans le module config.jsp.

## toolbar.jsp {#toolbar-jsp}

Le module toolbar.jsp contient le code pour créer la barre d’outils colorée. Pour supprimer la barre d’outils, supprimez toolbar.jsp de HTML.jsp.

## formBody.jsp {#formbody-jsp}

Le module de formBody.jsp sert à la représentation HTML du formulaire XFA.

## nav_footer.jsp {#nav-footer-jsp}

HTML5 forms commence par générer uniquement la première page du formulaire. Lorsqu’un utilisateur ou une utilisatrice fait défiler le formulaire, le reste des formulaires est chargé. La vitesse de chargement est ainsi optimisée. Le composant nav_footer.jsp contient tous les styles et éléments requis pour faciliter le chargement des pages dans le défilement.

## footer.jsp {#footer-jsp}

Le module footer.jsp est vide. Ce module vous permet d’ajouter des scripts qui ne sont utilisés que pour l’interaction utilisateur.

## Création de profils personnalisés {#creating-custom-profiles}

Pour créer un profil personnalisé, procédez comme suit :

### Créez un nœud de profil {#create-profile-node}

1. Accédez à l’interface CRX DE à l’adresse `https://'[server]:[port]'/crx/de` et connectez-vous à l’interface avec des informations d’identification administrateur.

1. Dans le panneau de gauche, rendez-vous à l’emplacement suivant : */content/xfaforms/profiles*.

1. Copiez le paramètre par défaut du nœud et collez le nœud dans un autre dossier(*/content/profiles*) intitulé *hrform*.

1. Sélectionnez le nouveau nœud, *hrform*, puis ajoutez une propriété de chaîne : *sling:resourceType* avec la valeur : *hrform/demo*.

1. Cliquez sur Enregistrer tout dans le menu de la barre d’outils pour enregistrer les modifications.

### Créez un script de rendu de profil. {#create-the-profile-renderer-script}

Après avoir créé un profil personnalisé, ajoutez-lui des informations du moteur de rendu. Lors de la réception d’une demande concernant le nouveau profil, CRX vérifie l’existence du dossier /apps pour la page JSP à rendre. Créez la page JSP dans le dossier /apps.

1. Dans le volet de gauche, accédez au dossier `/apps`.
1. Cliquez avec le bouton droit sur le dossier `/apps` et créez un dossier appelé **hrform**.
1. Dans le dossier **hrform**, créez un dossier intitulé **demo**.
1. Cliquez sur le bouton **Enregistrer tout**.
1. Accédez à `/libs/xfaforms/profile/html.jsp` et copiez le nœud **html.jsp**.
1. Collez le nœud **html.jsp** dans le dossier `/apps/hrform/demo` créé au-dessus avec le même nom **html.jsp** et cliquez sur **Enregistrer**.
1. Si vous rencontrez d’autres composants du script de profil, suivez les étapes 1 à 6 pour copier les composants dans le dossier /apps/hrform/demo.

1. Pour vérifier que le profil est créé, ouvrez l’URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

Pour vérifier les formulaires, [Importez les formulaires](/help/forms/using/get-xdp-pdf-documents-aem.md) de votre système de fichiers local vers AEM Forms et [affichez l’aperçu du formulaire](/help/forms/using/previewing-forms.md) sur l’instance d’auteur du serveur AEM.
