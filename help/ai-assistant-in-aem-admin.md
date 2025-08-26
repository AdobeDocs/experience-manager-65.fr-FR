---
title: Configuration de l’assistant AI dans AEM
description: Découvrez comment installer et configurer l’assistant AI à l’aide d’Admin Console dans Adobe Experience Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 38a79bc0dd5e78a49647b123fcdd0f0bacf94f21
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 3%

---

# Configuration de l’assistant AI dans AEM {#aem-ai-asst-admin-setup}

<!-- An Administrator must configure access, permissions, and settings before users in their organization can use the features in AI Assistant in AEM. -->

<!-- badge: label="Beta" type="Positive" -->

Pour utiliser l’assistant d’IA dans AEM (Adobe Experience Manager), votre entreprise doit s’inscrire au niveau d’Admin Console. Un administrateur de produit crée (ou choisit) un groupe d’utilisateurs et lui accorde la nouvelle autorisation « Assistant IA ». Toute personne ajoutée à ce groupe accède instantanément à l’Assistant IA à travers AEM. Si l’objectif est la disponibilité à l’échelle de l’entreprise, l’administrateur affecte simplement tous les utilisateurs à ce groupe.

Du point de vue de l’employé, le processus est simple : identifiez l’administrateur ou l’administratrice de produit pour Adobe Experience Manager dans votre entreprise et demandez à être ajouté au groupe d’utilisateurs et d’utilisatrices compatible avec l’IA. Une fois que vous apparaissez dans ce groupe, l&#39;icône Assistant s&#39;affiche automatiquement la prochaine fois que vous vous connectez.

Les administrateurs doivent garder à l’esprit une gouvernance Cloud Manager normale. détenir des droits d’administrateur de produit dans Admin Console pour créer des profils, gérer des groupes d’utilisateurs ou modifier des autorisations ; Si les utilisateurs ont également besoin de la fonctionnalité intégrée **Créer un ticket d’assistance** de l’assistant, ajoutez le rôle standard **Administrateur de l’assistance** (rôle Admin Console standard) aux mêmes personnes ou groupes.

Le processus de configuration de l’assistant AI dans AEM comprend les étapes suivantes :

1. [Création d’un profil de produit dans le Adobe Admin Console](#create-profile).
1. [Activez l’autorisation Connaissance des produits de l’assistant AI](#enable-permission).
1. [Créez un groupe d’utilisateurs (ou utilisez un groupe d’utilisateurs existant)](#create-user-group).
1. [Ajoutez des utilisateurs au groupe d’utilisateurs](#add-users).
1. [Attribuer le profil de produit au groupe d’utilisateurs](#assign-product-profile).

**Conditions préalables**

Avant de commencer, assurez-vous que les conditions préalables suivantes sont remplies :

* Vous devez au minimum disposer de droits d’administrateur de produit sur le Adobe Admin Console.
* Vous connaissez la structure de gestion des utilisateurs de votre entreprise.

**Considérations relatives à la configuration**

* Temps de traitement : les ressources créées dans Cloud Manager peuvent prendre jusqu’à 2 minutes pour s’afficher dans l’Admin Console pour la configuration des autorisations.
* Profils multiples : les utilisateurs peuvent faire partie de plusieurs profils et les autorisations sont combinées à partir de tous les profils attribués.
* Portée de l’organisation : certaines autorisations peuvent s’appliquer au niveau de l’organisation dans tous les programmes.
* Profils prédéfinis : ne supprimez pas les profils d’autorisation prédéfinis d’Admin Console.


## 1 - Création d’un profil de produit dans Adobe Admin Console{#create-profile}

1. Suivez les instructions détaillées de la section [Création d’un profil de produit dans Adobe Admin Console](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/create-profile) disponible dans la documentation d’Experience Platform.

1. Lors de la création du nouveau profil de produit, vous pouvez utiliser les valeurs suggérées suivantes pour AI Assistant.

   | Champ de texte | Valeur suggérée |
   | --- | --- |
   | Nom du profil de produit | `AI Assistant in AEM` (ou votre nom descriptif préféré) |
   | Nom d’affichage (facultatif) | `AI Assistant` |
   | Description (facultative) | `Product profile for managing AI Assistant in AEM access` |
   | Notification | Configuration d’en fonction des préférences de votre organisation |


## 2 - Activer l’autorisation Connaissance des produits de l’assistant IA{#enable-permission}

Le processus d’attribution d’autorisations personnalisées aux profils de produit suit le processus standard des autorisations personnalisées d’Adobe Cloud Manager .

Article de référence : [Attribuer des autorisations personnalisées au nouveau profil de produit](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. Dans le Admin Console, cliquez sur le nom du profil de produit nouvellement créé (`AI Assistant in AEM`)

   ![Capture d’écran](/help/assets/assets-ai/ai-assistant-console.png)

1. Pour afficher la liste des autorisations modifiables, cliquez sur l’onglet **Permissions** .

1. Dans la liste du tableau, recherchez l’autorisation `AI Assistant Product Knowledge` .

   ![Onglet Autorisations de l’Assistant IA dans Admin Console](/help/assets/assets-ai/ai-assistant-permission.png)

1. À droite du nom de l’autorisation, cliquez sur Icône en forme de crayon ou sur ![l’icône](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) Modifier.

1. Sur la page **Modifier les autorisations pour l’assistant AI**, activez le bouton (bascule) **Connaissance des produits de l’assistant AI**.

   ![Page Modifier les autorisations pour l’option de basculement Connaissance du produit de l’assistant IA ](/help/assets/assets-ai/ai-assistant-prod-knowledge.png)

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

1. Dans la **page Créer un groupe** d’utilisateurs, indiquez les informations suivantes :

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

   ![ Assistant AI de la page de groupes d’utilisateurs AEM, affichant l’onglet Utilisateurs et le bouton Ajouter des utilisateurs ](/help/assets/assets-ai/ai-assistant-add-users.png)

1. Sur la page **`Add users to this user group`**, recherchez et sélectionnez les utilisateurs qui doivent accéder à l’assistant AI dans AEM.

   ![Ajouter des utilisateurs à cette page de groupe d’utilisateurs](/help/assets/assets-ai/ai-assistant-add-users-to-this-group.png)

1. Dans le coin inférieur droit de la page, cliquez sur **Enregistrer**.
1. Affectez maintenant [ profil de produit au groupe d’utilisateurs](#assign-product-profile).

>[!TAB Ajout d’utilisateurs en bloc]

Vous pouvez utiliser la fonction de transfert en vrac dans l’Admin Console.

1. Préparez un fichier CSV avec les informations de l’utilisateur.
1. Utilisez l’option pour des ajouts **`Add users by CSV`** en bloc efficaces.
1. [Attribuez maintenant le profil de produit au groupe](#assign-product-profile) d’utilisateurs.

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

   ![Le profil de produit Assistant AI affiché est affecté à l’Assistant AI dans le groupe d’utilisateurs AEM](/help/assets/assets-ai/ai-assistant-profile-assigned-to-user-group.png)


## Vérification de la configuration

* Vérifiez que votre profil de produit affiche le nombre correct de groupes d’utilisateurs affectés.
* Vérifiez que le groupe d’utilisateurs présente le nombre correct d’utilisateurs.
* Vérifiez que l’autorisation AI Assistant Product Knowledge est activée et correctement configurée.


## Tester le paramétrage

Demandez à un utilisateur du groupe assigné de faire ce qui suit :

1. Connectez-vous à AEM.
2. Vérifiez que les fonctionnalités de l’assistant AI sont accessibles.
3. Testez la fonctionnalité de l’assistant d’IA pour vérifier qu’elle est correctement activée.

## Voir également

* [Assistant AI dans AEM](/help/ai-assistant-in-aem.md)
* [Contrôle d’accès Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview)
<!-- * [Cloud Manager Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md) -->
