---
title: Configuration de l’assistant IA dans AEM
description: Découvrez comment installer et configurer l’assistant AI à l’aide d’Admin Console dans Adobe Experience Manager.
solution: Experience Manager
feature: Authoring, AI Assistant, AI Tools
role: Admin, Developer, User
exl-id: 06824b3d-f912-4922-8fb6-ee2ca04c6326
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 4%

---

# Configuration de l’assistant IA dans AEM {#aem-ai-asst-admin-setup}

<!-- An Administrator must configure access, permissions, and settings before users in their organization can use the features in AI Assistant in AEM. -->

<!-- badge: label="Beta" type="Positive" -->

Pour utiliser l’assistant AI dans AEM (Adobe Experience Manager), l’autorisation d’accéder à la connaissance des produits par l’intermédiaire de l’assistant AI est obligatoire. Cette autorisation est activée par défaut.

Si vous souhaitez contrôler qui peut accéder à la connaissance des produits, envoyez un e-mail à [aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com) à partir de l’adresse e-mail associée à votre Adobe ID. Adobe peut activer le contrôle d’accès au niveau de l’utilisateur. Lorsqu’il est activé, votre administrateur peut accorder l’accès au niveau de l’utilisateur en suivant les étapes décrites ci-dessous.

Si vous avez demandé un contrôle d’accès au niveau de l’utilisateur, votre organisation doit s’inscrire par le biais du Adobe Admin Console. Un administrateur de produit crée (ou choisit) un groupe d’utilisateurs et lui accorde la nouvelle autorisation « Assistant IA ». Toute personne ajoutée à ce groupe accède instantanément à l’assistant AI dans AEM. Si l’objectif est la disponibilité à l’échelle de l’entreprise, l’administrateur affecte simplement tous les utilisateurs à ce groupe.

Du point de vue de l’employé, le processus est simple : identifiez l’administrateur ou l’administratrice de produit pour Adobe Experience Manager dans votre entreprise et demandez à être ajouté au groupe d’utilisateurs et d’utilisatrices compatible avec l’IA. Une fois que vous apparaissez dans ce groupe, l&#39;icône Assistant s&#39;affiche automatiquement la prochaine fois que vous vous connectez.

Les administrateurs doivent garder à l’esprit une gouvernance Cloud Manager normale. détenir des droits d’administrateur de produit dans Admin Console pour créer des profils, gérer des groupes d’utilisateurs ou modifier des autorisations ; Si les utilisateurs ont également besoin de la fonctionnalité intégrée **Créer un ticket d’assistance** de l’assistant, ajoutez le rôle standard **Administrateur de l’assistance** (rôle Admin Console standard) aux mêmes personnes ou groupes.

Le processus de configuration de l’assistant AI dans AEM comprend les étapes suivantes :

1. [Création d’un profil de produit dans le Adobe Admin Console](#create-profile).
1. [Autorisation Activer la connaissance du produit de l’assistant AI](#enable-permission).
1. [Créez un groupe d’utilisateurs (ou utilisez un groupe d’utilisateurs existant)](#create-user-group).
1. [Ajoutez des utilisateurs au groupe d’utilisateurs](#add-users).
1. [Attribuer le profil de produit au groupe d’utilisateurs](#assign-product-profile).

**Conditions préalables**

Avant de commencer, assurez-vous d’avoir satisfait aux conditions préalables suivantes :

* Vous devez disposer au minimum des droits d’administrateur de produit dans Adobe Admin Console.
* Vous avez une compréhension de la structure de gestion des utilisateurs de votre entreprise.

**Considérations relatives à la configuration**

* Temps de traitement : l’affichage des ressources créées dans Cloud Manager peut prendre jusqu’à 2 minutes dans Admin Console pour la configuration des autorisations.
* Profils multiples : les utilisateurs peuvent faire partie de plusieurs profils et les autorisations sont combinées à partir de tous les profils attribués.
* Portée de l’organisation : certaines autorisations peuvent s’appliquer au niveau de l’organisation dans tous les programmes.
* Profils prédéfinis : ne supprimez pas les profils d’autorisation prédéfinis d’Admin Console.


## 1 - Création d’un profil de produit dans Adobe Admin Console{#create-profile}

1. Suivez les instructions détaillées de la section [Création d’un profil de produit dans Adobe Admin Console](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/create-profile) disponible dans la documentation d’Experience Platform.

1. Lors de la création du profil de produit, vous pouvez utiliser les valeurs suggérées suivantes pour l’assistant AI.

   | Champ de texte | Valeur suggérée |
   | --- | --- |
   | Nom du profil de produit | `AI Assistant in AEM` (ou votre nom descriptif préféré) |
   | Nom d’affichage (facultatif) | `AI Assistant` |
   | Description (facultative) | `Product profile for managing AI Assistant in AEM access` |
   | Notification | Configuration d’en fonction des préférences de votre organisation |


## 2 - Autorisation Activer la connaissance du produit de l’assistant IA{#enable-permission}

Le processus d’attribution d’autorisations personnalisées aux profils de produit suit le processus standard des autorisations personnalisées d’Adobe Cloud Manager .

Article de référence : [Attribuer des autorisations personnalisées au nouveau profil de produit](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. Dans Admin Console, cliquez sur le nom de votre profil de produit nouvellement créé (`AI Assistant in AEM`)

   ![Capture d’écran](/help/assets/assets-ai/ai-assistant-console.png)

1. Pour afficher la liste des autorisations modifiables, cliquez sur l’onglet **Autorisations**.

1. Dans la liste des tableaux, recherchez l’autorisation `AI Assistant Product Knowledge`.

   ![Onglet Autorisations de l’assistant AI dans Admin Console](/help/assets/assets-ai/ai-assistant-permission.png)

1. À droite du nom de l’autorisation, cliquez sur ![icône Crayon ou icône Modifier](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg).

1. Sur la page **Modifier les autorisations pour l’assistant AI**, activez le bouton (bascule) **Connaissance des produits de l’assistant AI**.

   ![Page Modifier les autorisations pour l’option de basculement Connaissance du produit Assistant IA ](/help/assets/assets-ai/ai-assistant-prod-knowledge.png)

1. Dans le coin inférieur droit de la page, cliquez sur **Enregistrer**.

   L’autorisation Connaissance des produits de l’assistant AI est désormais activée pour votre profil de produit.


## 3 - Créez un groupe d’utilisateurs (ou utilisez un groupe d’utilisateurs existant){#create-user-group}

1. Utilisez l’une des méthodes suivantes :

>[!BEGINTABS]

>[!TAB Créer un groupe d’utilisateurs]

1. Dans Admin Console, cliquez sur **Utilisateurs** > **Groupes d’utilisateurs**.

   ![Groupes d’utilisateurs](/help/assets/assets-ai/ai-assistant-user-groups.png)

1. Sur la page **Groupes d’utilisateurs**, cliquez sur **Nouveau groupe d’utilisateurs**.

   ![Bouton Nouveau groupe d’utilisateurs sur la page Groupes d’utilisateurs](/help/assets/assets-ai/ai-assistant-new-user-group.png)

1. Sur la page **Créer un groupe d’utilisateurs** fournissez les informations suivantes :

   | Option | Valeur suggérée |
   | --- | --- |
   | Nom du groupe d’utilisateurs | `AI Assistant in AEM` (ou votre nom préféré) |
   | Description (facultative) | `User group for managing AI Assistant in AEM access` |

   ![Créer une page de groupe d’utilisateurs](/help/assets/assets-ai/ai-assistant-create-new-user-group.png)

1. Dans le coin inférieur droit de la page, cliquez sur **Enregistrer**.

>[!TAB Utiliser un groupe d’utilisateurs existant]

Vous pouvez utiliser un groupe d’utilisateurs AEM existant s’il répond aux exigences d’accès des assistants AI, au lieu d’en créer un nouveau.

>[!ENDTABS]

## 4 - Ajouter des utilisateurs au groupe d’utilisateurs{#add-users}

1. Utilisez l’une des méthodes suivantes :

>[!BEGINTABS]

>[!TAB Ajouter des utilisateurs individuels]

1. Sur la page **Groupes d’utilisateurs**, dans le tableau **Nom du groupe**, cliquez sur le nom du groupe d’utilisateurs que vous venez de créer ou sur un nom de groupe d’utilisateurs existant.

   ![Page de groupes d’utilisateurs affichant l’assistant AI dans le nom du groupe d’utilisateurs AEM dans le tableau](/help/assets/assets-ai/ai-assistant-user-group-name-in-table.png)

1. Sur la page **Groupes d’utilisateurs** de l’assistant **AI dans AEM**, cliquez sur l’onglet **Utilisateurs** puis sur **Ajouter des utilisateurs**.

   ![Assistant AI dans la page de groupes d’utilisateurs AEM, affichant l’onglet Utilisateurs et le bouton Ajouter des utilisateurs](/help/assets/assets-ai/ai-assistant-add-users.png)

1. Sur la page **`Add users to this user group`**, recherchez et sélectionnez les utilisateurs qui doivent accéder à l’assistant AI dans AEM.

   ![Ajouter des utilisateurs à cette page de groupe d’utilisateurs](/help/assets/assets-ai/ai-assistant-add-users-to-this-group.png)

1. Dans le coin inférieur droit de la page, cliquez sur **Enregistrer**.
1. Affectez maintenant [ profil de produit au groupe d’utilisateurs](#assign-product-profile).

>[!TAB Ajout d’utilisateurs en bloc]

Vous pouvez utiliser la fonction de chargement en bloc dans Admin Console.

1. Préparez un fichier CSV contenant des informations sur l’utilisateur.
1. Utilisez l’option **`Add users by CSV`** pour un ajout en bloc efficace.
1. Affectez maintenant [ profil de produit au groupe d’utilisateurs](#assign-product-profile).

>[!ENDTABS]


## 5 - Attribuer le profil de produit au groupe d’utilisateurs{#assign-product-profile}

Cette étape suit le workflow Adobe Admin Console standard d’affectation de profils de produit à des groupes d’utilisateurs.

Article de référence : [gestion des profils de produit pour les utilisateurs d’entreprise](https://helpx.adobe.com/fr/enterprise/using/manage-product-profiles.html)

1. Toujours dans votre assistant AI dans le groupe d’utilisateurs AEM à partir du [4 - Ajouter des utilisateurs au groupe d’utilisateurs](#add-users), cliquez sur l’onglet **Profils de produit attribués**.
1. Cliquez sur **Attribuer un profil**.

   ![ Assistant AI dans la page du groupe d’utilisateurs AEM avec l’onglet Profils de produit attribués sélectionné](/help/assets/assets-ai/ai-assistant-assign-profile.png)

1. Sur la page **Attribuer des produits et des profils**, dans la boîte de dialogue **Sélectionner des profils de produit**, recherchez et sélectionnez votre profil de produit **Assistant IA**.

   ![ La page « Attribuer des produits et des profils », affichant la boîte de dialogue « Sélectionner des profils de produit » et le profil de produit « Assistant IA » sélectionné](/help/assets/assets-ai/ai-assistant-select-product-profile.png)

1. Dans le coin inférieur droit de la boîte de dialogue, cliquez sur **Appliquer**.
1. Dans le coin inférieur droit de la page **Attribuer des produits et des profils**, cliquez sur **Enregistrer**.

   ![Profil de produit Assistant AI affiché affecté à Assistant AI dans le groupe d’utilisateurs AEM](/help/assets/assets-ai/ai-assistant-profile-assigned-to-user-group.png)


## Vérification de la configuration

* Vérifiez que votre profil de produit affiche le nombre correct de groupes d’utilisateurs affectés.
* Vérifiez que le groupe d’utilisateurs indique le nombre correct d’utilisateurs.
* Vérifiez que l’autorisation de la connaissance du produit de l’assistant AI est activée et correctement configurée.


## Tester la configuration

Demandez à un utilisateur du groupe affecté d’effectuer les opérations suivantes :

1. Connectez-vous à AEM.
2. Vérifiez que les fonctionnalités de l’assistant AI sont accessibles.
3. Testez la fonctionnalité de l’assistant AI pour vous assurer de son activation correcte.

## Voir également

* [Assistant IA dans AEM](/help/ai-assistant-in-aem.md)
* [Contrôle d’accès Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview)
<!-- * [Cloud Manager Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md) -->
