---
title: Activer le basculement des fonctionnalités pour intégrer les fonctionnalités Adopteur anticipé et Version préliminaire
description: Le basculement de fonctionnalités est une fonctionnalité d’AEM qui permet aux administrateurs d’activer de nouvelles fonctionnalités dans un environnement d’exécution.
feature: Adaptive Forms, Foundation Components
role: User, Developer
hidefromtoc: true
source-git-commit: 794d93d890ba752f9036a85831f7cbc8391fb545
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 7%

---

# Activation/désactivation des fonctionnalités dans Adobe Experience Manager (AEM) 6.5{#enable-feature-toggle-aem-forms-65}

Le basculement de fonctionnalités est une fonctionnalité d’AEM qui permet aux administrateurs d’activer ou de désactiver dynamiquement des fonctionnalités spécifiques. Cette fonctionnalité est particulièrement utile pour la gestion des **fonctionnalités Adopteur anticipé** et des **fonctionnalités de version préliminaire** sans nécessiter de déploiements majeurs ou de modifications du code base. Elle garantit une flexibilité et un contrôle sur les fonctionnalités accessibles dans un environnement AEM.

## Activer le basculement de fonction {#enable-feature-toggle-65}

Les bascules de fonctionnalités pour les utilisateurs précoces ou les nouvelles fonctionnalités peuvent être configurés par le biais de la **console web d’AEM** en suivant les étapes ci-dessous :

1. Connectez-vous à l’instance AEM Forms.
2. Accédez à `http://<author-instance-url>:portnumber/system/console/configMgr`.
3. Recherchez **Adobe Granite Dynamic Toggle Provider** dans Configuration Manager.
4. Cliquez sur l’icône ![icône représentant un crayon](assets/illustratorcc_penciltool_cur_edit_2_17.png).
5. Dans la section [!UICONTROL Activé Toggles] , cliquez sur ![ icône-crayon](assets/aem6forms_add.png).
6. Ajoutez l’identifiant de basculement de fonction pour la fonction comme illustré dans l’image ci-dessous.
   ![Ajouter un bouton bascule](assets/add_toggle_number_forms.png)

   >[!NOTE]
   >
   >Vous pouvez trouver l’identifiant de basculement de fonction dans le document spécifique aux premières fonctionnalités d’adoption.

7. Cliquez sur Enregistrer.

## Désactiver le basculement de fonction {#disable-feature-toggle-65}

Pour désactiver le ou les bascules de fonction pour les fonctions dont le ou les bascules sont activés, procédez comme suit :

1. Connectez-vous à l’instance AEM Forms.
2. Accédez à `http://<author-instance-url>:portnumber/system/console/configMgr`.
3. Recherchez **Adobe Granite Dynamic Toggle Provider** dans Configuration Manager.
4. Cliquez sur l’icône ![icône représentant un crayon](assets/illustratorcc_penciltool_cur_edit_2_17.png).
5. Dans la section [!UICONTROL Désactivé Toggles] , cliquez sur ![ icône-crayon](assets/aem6forms_add.png).
6. Ajoutez le numéro de basculement de la fonction à désactiver.
   ![Supprimer le bouton bascule](assets/remove_toggle_feature_forms.png)
7. Cliquez sur Enregistrer.

## Considération technique

Les basculement de fonctionnalités sont spécifiques à l’environnement et sont gérés au moment de l’exécution. Ils ne nécessitent donc pas de redémarrage du serveur. Toutefois, certaines fonctionnalités peuvent nécessiter l’actualisation des pages appropriées ou l’effacement du cache pour refléter les modifications.
Vous pouvez accéder à la liste des fonctionnalités activées par activation/désactivation de fonctionnalités pour votre environnement via `http://<author-instance-url>:4502/etc.clientlibs/toggles.json`.