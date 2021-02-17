---
title: Gestion des catégories affichées dans Workspace
seo-title: Gestion des catégories affichées dans Workspace
description: Dans Workspace, les processus qu’un utilisateur peut démarrer s’affichent dans les catégories du volet de navigation gauche. Découvrez comment gérer ces catégories affichées dans l’espace de travail.
seo-description: Dans Workspace, les processus qu’un utilisateur peut démarrer s’affichent dans les catégories du volet de navigation gauche. Découvrez comment gérer ces catégories affichées dans l’espace de travail.
uuid: c2a275f5-872e-467f-9f07-4b130631e8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0d1536a2-10ac-4031-bd7f-264b02d0d75f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 97%

---


# Gestion des catégories affichées dans Workspace {#managing-the-categories-displayed-in-workspace}

Dans Workspace, les processus qu’un utilisateur peut démarrer s’affichent dans les catégories du volet de navigation gauche. Vous pouvez configurer les catégories dans Administration Console, ou alors les concepteurs de processus peuvent les configurer dans Workbench. Lorsque les concepteurs de processus créent des processus, ils les affectent à des catégories.

Lorsque vous spécifiez des noms de catégorie, vous devez les créer afin qu’ils s’affichent correctement dans le volet de navigation de Workspace. Par défaut, le volet de navigation gauche a une largeur fixe de 210 pixels, soit environ 24 caractères. Si le nom de catégorie que vous indiquez est trop long pour tenir dans la largeur définie du volet de navigation gauche, ce nom est tronqué. Le nom complet ne s’affiche que si le pointeur de la souris est posé dessus. Evitez d’utiliser des noms de catégorie qui seront tronqués. Les deux exemples suivants illustrent les noms de catégories qui conviennent et ceux qui sont tronqués :

**nom de la catégorie qui convient:** Présence et absence

**nom de la catégorie tronquée :** Présence et absence (Etats-Unis)

Dans Workspace, les processus d’une catégorie s’affichent en général sous forme de cartes dans la page Démarrer le processus. En général, l’écran peut afficher six cartes pour une catégorie avant que l’utilisateur ne doive le faire défiler afin de visualiser les autres cartes. Comme le défilement de l’écran rend la recherche d’un processus plus difficile, pensez à limiter chaque catégorie à six processus ou, en fonction de votre résolution, au nombre de processus susceptibles d’être affichés à l’écran sans avoir recours au défilement.

Lorsque vous utilisez MySQL en tant que base de données AEM forms, Administration Console n’est pas en mesure de différencier les noms des deux catégories qui ne diffèrent que par l’utilisation de caractères étendus. Par exemple, si vous créez une catégorie appelée abcde et une autre appelée âbcdè, elles sont considérées comme identiques.

## Ajout d’une catégorie {#add-a-category}

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des catégories.
1. Cliquez sur Ajouter. Si vous souhaitez ajouter une sous-catégorie, sélectionnez une catégorie et cliquez ensuite sur Ajouter.
1. Dans la zone Nom, saisissez le nom de la catégorie, puis dans la zone Description, saisissez une description.
1. Cliquez sur Ajouter. La catégorie s’affiche dans la page Gestion des catégories.

   ***Remarque ** : vous êtes limité à cinq niveaux de hiérarchie lorsque vous créez des catégories.*

## Modification d’une catégorie {#edit-a-category}

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des catégories.
1. Sélectionnez la catégorie que vous souhaitez modifier et cliquez sur Modifier. Vous pouvez également cliquer deux fois sur une catégorie pour la modifier.
1. Modifiez le nom de la catégorie dans la zone Nom.

## Suppression d’une catégorie  {#remove-a-category}

Vous ne pouvez supprimer que les catégories que vous n’utilisez pas.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des catégories.
1. Dans la page Gestion des catégories, cochez la case correspondant à la catégorie à supprimer, puis cliquez sur Supprimer. Cette catégorie n’est plus affichée.

