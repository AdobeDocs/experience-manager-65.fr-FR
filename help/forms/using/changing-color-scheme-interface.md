---
title: Modification des couleurs de l’interface
seo-title: Changing the color scheme of the interface
description: Comment modifier les couleurs de parties spécifiques de l’interface utilisateur de l’espace de travail AEM Forms.
seo-description: How to modify the color scheme of AEM Forms workspace user interface portions selectively.
uuid: 32c32f7a-8271-4d2c-8a1f-ad5ab3c90b83
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 18dab82a-badf-4c32-83a2-cd5cb04cae89
exl-id: e0a261a2-518b-4984-a5b5-24f0b9222e24
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: ht
source-wordcount: '228'
ht-degree: 100%

---

# Modification des couleurs de l’interface {#changing-the-color-scheme-of-the-interface}

Vous pouvez modifier les couleurs des différentes parties de l’interface utilisateur de l’espace de travail AEM Forms selon vos besoins. Voici quelques exemples de personnalisation des couleurs. En plus des étapes décrites dans cet article, voir [Procédure générique de personnalisation d’AEM Forms Workspace](/help/forms/using/generic-steps-html-workspace-customization.md).

## Barre de navigation supérieure {#top-navigation-bar}

### Utilisation d’une image d’arrière-plan {#using-background-image}

Pour mettre à jour la barre de navigation en haut de l’espace de travail AEM Forms :

1. Créez une image d’arrière-plan pour mettre à jour la couleur. Nommez le fichier newBackground.jpg.
1. Téléchargez le fichier de l’image d’arrière-plan dans le dossier /apps/ws/images à l’aide d’un client WebDAV.

   >[!NOTE]
   >
   >Pour plus d’informations sur l’accès à WebDAV, voir [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr).

1. Référencez la nouvelle image d’arrière-plan dans /apps/ws/css/newStyle.css en ajoutant le style suivant.

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### Utilisation de la propriété de couleur dans CSS {#using-color-property-in-css}

1. Ajoutez le style suivant dans newStyle.css sous /apps/ws/css.

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## Composant de catégories {#category-component}

Le composant de catégories affiche les différentes catégories de vos tâches dans le panneau de gauche. Pour modifier sa couleur, définissez la couleur d’arrière-plan dans l’élément `.category` du fichier CSS.

## Composant de tâches {#task-component}

Les tâches sont affichées dans le volet du milieu appelé TaskList de tâches. Pour modifier sa couleur, modifiez le style associé au sélecteur .task dans la feuille de style.
