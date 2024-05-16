---
title: Gérer les catégories affichées dans Workspace
description: Dans Workspace, les processus qu’un utilisateur ou une utilisatrice peut démarrer s’affichent dans les catégories du volet de navigation gauche. Découvrez comment gérer ces catégories affichées dans Workspace.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 62621fe9-f69f-4bc0-aecc-d7bcc3064516
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '482'
ht-degree: 100%

---

# Gérer les catégories affichées dans Workspace {#managing-the-categories-displayed-in-workspace}

Dans Workspace, les processus qu’un utilisateur ou une utilisatrice peut démarrer s’affichent dans les catégories du volet de navigation gauche. Vous pouvez configurer les catégories dans la console d’administration, ou alors les concepteurs ou conceptrices de processus peuvent les configurer dans Workbench. Lorsque les concepteurs ou les conceptrices de processus créent des processus, ils les affectent à des catégories.

Lorsque vous spécifiez des noms de catégorie, vous devez les créer afin qu’ils s’affichent correctement dans le volet de navigation de Workspace. Par défaut, le volet de navigation gauche a une largeur fixe de 210 pixels, soit environ 24 caractères. Si le nom de catégorie que vous indiquez est trop long pour tenir dans la largeur définie du volet de navigation gauche, ce nom est tronqué. Le nom complet ne s’affiche que si le pointeur de la souris est posé dessus. Évitez d’utiliser des noms de catégorie qui seront tronqués. Les deux exemples suivants illustrent les noms de catégories qui conviennent et ceux qui sont tronqués :

**Nom de la catégorie qui est adapté :** présence et absence.

**Nom de la catégorie qui est tronqué :** présence et absence (France).

Dans Workspace, les processus d’une catégorie s’affichent en général sous forme de cartes dans la page Démarrer le processus. En général, l’écran peut afficher six cartes pour une catégorie avant que l’utilisateur ou l’utilisatrice ne doive le faire défiler afin de visualiser les autres cartes. Comme le défilement de l’écran rend la recherche d’un processus plus difficile, pensez à limiter chaque catégorie à six processus ou, en fonction de votre résolution, au nombre de processus susceptibles d’être affichés à l’écran sans avoir recours au défilement.

Lorsque vous utilisez MySQL en tant que base de données AEM Forms, la console d’administration n’est pas en mesure de différencier les noms des deux catégories qui ne diffèrent que par l’utilisation de caractères étendus. Par exemple, si vous créez une catégorie appelée abcde et une autre appelée âbcdè, elles sont considérées comme identiques.

## Ajout d’une catégorie {#add-a-category}

1. Dans la console d’administration, cliquez sur Services > Applications et services > Gestion des catégories.
1. Cliquez sur Ajouter. Si vous souhaitez ajouter une sous-catégorie, sélectionnez une catégorie et cliquez ensuite sur Ajouter.
1. Dans la zone Nom, saisissez le nom de la catégorie, puis dans la zone Description, saisissez une description.
1. Cliquez sur Ajouter. La catégorie s’affiche dans la page Gestion des catégories.

   ***Remarque ** : vous êtes limité à cinq niveaux de hiérarchie lorsque vous créez des catégories.*

## Modification d’une catégorie {#edit-a-category}

1. Dans la console d’administration, cliquez sur Services > Applications et services > Gestion des catégories.
1. Sélectionnez la catégorie que vous souhaitez modifier et cliquez sur Modifier. Vous pouvez également double-cliquer sur une catégorie pour la modifier.
1. Modifiez le nom de la catégorie dans la zone Nom.

## Suppression d’une catégorie {#remove-a-category}

Vous ne pouvez supprimer que les catégories que vous n’utilisez pas.

1. Dans la console d’administration, cliquez sur Services > Applications et services > Gestion des catégories.
1. Dans la page Gestion des catégories, cochez la case correspondant à la catégorie à supprimer, puis cliquez sur Supprimer. Cette catégorie n’est plus affichée.
