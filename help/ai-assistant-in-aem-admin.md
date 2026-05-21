---
title: Configuration de l’assistant IA dans AEM
description: Découvrez comment installer et configurer l’assistant IA à l’aide d’Admin Console dans Adobe Experience Manager.
solution: Experience Manager
feature: Authoring, AI Assistant, AI Tools
role: Admin, Developer, User
exl-id: 06824b3d-f912-4922-8fb6-ee2ca04c6326
autotag-review: '2026-05-18T18:35:37.980Z'
TQID: 'https://experienceleague.adobe.com/5YTQUJbJPlJuxToS6AVhJww1KQ20tuOlRoCVquyfSng'
product_v2: id: e14eb250-3c22-4a07-9061-a78112b2b826id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
feature_v2: id: ac5ecfc1-cc78-4ecc-a90a-0362685062ce
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
source-git-commit: 9c96b6744c7af2f061b4dfbf403560047485f9b5
workflow-type: tm+mt
source-wordcount: 1202
ht-degree: 98%

---

# Configuration de l’assistant IA dans AEM {#aem-ai-asst-admin-setup}

<!-- An Administrator must configure access, permissions, and settings before users in their organization can use the features in AI Assistant in AEM. -->

<!-- badge: label="Beta" type="Positive" -->

Pour utiliser l’assistant IA d’AEM (Adobe Experience Manager), l’autorisation d’accéder à la base de connaissance des produits par l’intermédiaire de l’assistant IA est obligatoire. Cette autorisation est activée par défaut.

Si vous souhaitez contrôler qui peut accéder à la base de connaissance des produits, envoyez un e-mail à [aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com) à partir de l’adresse e-mail associée à votre Adobe ID. Adobe peut activer le contrôle d’accès au niveau de l’utilisateur ou de l’utilisatrice. Lorsqu’il est activé, votre administrateur ou administratrice peut accorder l’accès au niveau de l’utilisateur ou de l’utilisatrice en suivant les étapes décrites ci-dessous.

Si vous avez demandé un contrôle d’accès au niveau de l’utilisateur ou de l’utilisatrice, votre organisation doit s’inscrire par le biais d’Adobe Admin Console. Un administrateur ou une administratrice de produit crée (ou choisit) un groupe d’utilisateurs et d’utilisatrices et lui accorde la nouvelle autorisation « Assistant IA ». Toute personne ajoutée à ce groupe accède instantanément à l’assistant IA d’AEM. Si l’objectif est la disponibilité à l’échelle de l’entreprise, l’administrateur ou l’administratrice affecte simplement l’ensemble des utilisateurs et des utilisatrices à ce groupe.

Du point de vue des membres du personnel, le processus est simple : identifiez l’administrateur ou l’administratrice de produit Adobe Experience Manager dans votre entreprise et demandez votre ajout au groupe d’utilisateurs et d’utilisatrices de l’IA. Une fois que vous apparaissez dans ce groupe, l’icône Assistant s’affiche automatiquement la prochaine fois que vous vous connectez.

Les administrateurs et administratrices doivent garder à l’esprit une gouvernance Cloud Manager normale. Détenez des droits d’administration de produit dans Admin Console pour créer des profils, gérer des groupes d’utilisateurs et d’utilisatrices ou modifier des autorisations. Si les utilisateurs et utilisatrices ont également besoin de la fonctionnalité intégrée **Créer un ticket d’assistance** de l’assistant, ajoutez le rôle standard **Administration de l’assistance** (rôle Admin Console standard) aux mêmes personnes ou groupes.

Le processus de configuration de l’assistant IA d’AEM comprend les étapes suivantes :

1. [Créez un profil de produit dans Adobe Admin Console](#create-profile).
1. [Activez l’autorisation de la connaissance des produits de l’assistant IA](#enable-permission).
1. [Créez un groupe d’utilisateurs et d’utilisatrices (ou utilisez un groupe existant](#create-user-group).
1. [Ajoutez des utilisateurs et des utilisatrices au groupe](#add-users).
1. [Attribuez le profil de produit au groupe d’utilisateurs et d’utilisatrices](#assign-product-profile).

**Conditions préalables**

Avant de commencer, assurez-vous de remplir les conditions préalables suivantes :

* Vous devez disposer au minimum des droits d’administration de produit dans Adobe Admin Console.
* Vous comprenez la structure de la gestion des utilisateurs et des utilisatrices de votre entreprise.

**Considérations relatives à la configuration**

* Délai de traitement : les ressources créées dans Cloud Manager peuvent mettre jusqu’à deux minutes pour s’afficher dans Admin Console pour la configuration des autorisations.
* Profils multiples : les utilisateurs et utilisatrices peuvent faire partie de plusieurs profils et les autorisations sont combinées à partir de tous les profils attribués.
* Portée de l’organisation : certaines autorisations peuvent s’appliquer au niveau de l’organisation dans tous les programmes.
* Profils prédéfinis : ne supprimez pas les profils d’autorisation prédéfinis d’Admin Console.


## 1 - Créer un profil de produit dans Adobe Admin Console{#create-profile}

1. Suivez les instructions détaillées de la section [Créer un profil de produit dans Adobe Admin Console](https://experienceleague.adobe.com/fr/docs/experience-platform/access-control/ui/create-profile) disponible dans la documentation d’Experience Platform.

1. Lors de la création du profil de produit, vous pouvez utiliser les valeurs suggérées suivantes pour l’assistant IA.

   | Champ de texte | Valeur suggérée |
   | --- | --- |
   | Nom du profil de produit | `AI Assistant in AEM` (ou le nom descriptif de votre choix) |
   | Nom d’affichage (facultatif) | `AI Assistant` |
   | Description (facultative) | `Product profile for managing AI Assistant in AEM access` |
   | Notification | Configuration en fonction des préférences de votre organisation |


## 2 - Activer l’autorisation de la connaissance des produits de l’assistant IA{#enable-permission}

Le processus d’attribution d’autorisations personnalisées aux profils de produit suit le workflow standard des autorisations personnalisées d’Adobe Cloud Manager.

Article de référence : [Attribuer des autorisations personnalisées au nouveau profil de produit](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-manager/content/requirements/custom-permissions#assign-permissions)

1. Dans Admin Console, cliquez sur le nom du profil de produit que vous venez de créer (`AI Assistant in AEM`).

   ![Capture d’écran](/help/assets/assets-ai/ai-assistant-console.png)

1. Pour afficher la liste des autorisations modifiables, cliquez sur l’onglet **Autorisations**.

1. Dans la liste du tableau, recherchez l’autorisation `AI Assistant Product Knowledge`.

   ![Onglet Autorisations de l’assistant IA dans Admin Console](/help/assets/assets-ai/ai-assistant-permission.png)

1. À droite du nom de l’autorisation, cliquez sur ![icône Crayon ou icône Modifier](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg).

1. Sur la page **Modifier les autorisations de l’assistant IA**, activez le bouton (bascule) **Connaissance des produits de l’assistant IA**.

   ![Page Modifier les autorisations pour l’option du bouton (bascule) Connaissance des produits de l’assistant IA](/help/assets/assets-ai/ai-assistant-prod-knowledge.png)

1. Dans le coin inférieur droit de la page, cliquez sur **Enregistrer**.

   L’autorisation Connaissance des produits de l’assistant IA est désormais activée pour votre profil de produit.


## 3 - Créer un groupe d’utilisateurs et d’utilisatrices (ou utiliser un groupe existant){#create-user-group}

1. Utilisez l’une des méthodes suivantes :

>[!BEGINTABS]

>[!TAB Créer un groupe d’utilisateurs et d’utilisatrices]

1. Dans Admin Console, cliquez sur **Utilisateurs et utilisatrices** > **Groupes d’utilisateurs et d’utilisatrices**.

   ![Groupes d’utilisateurs](/help/assets/assets-ai/ai-assistant-user-groups.png)

1. Sur la page **Groupes d’utilisateurs et d’utilisatrices**, cliquez sur **Nouveau groupe d’utilisateurs et d’utilisatrices**.

   ![Bouton Nouveau groupe d’utilisateurs et d’utilisatrices sur la page Groupes d’utilisateurs et d’utilisatrices](/help/assets/assets-ai/ai-assistant-new-user-group.png)

1. Sur la page **Créer un groupe d’utilisateurs et d’utilisatrices**, fournissez les informations suivantes :

   | Option | Valeur suggérée |
   | --- | --- |
   | Nom du groupe d’utilisateurs et d’utilisatrices | `AI Assistant in AEM` (ou le nom de votre choix) |
   | Description (facultative) | `User group for managing AI Assistant in AEM access` |

   ![Page Créer un groupe d’utilisateurs et d’utilisatrices](/help/assets/assets-ai/ai-assistant-create-new-user-group.png)

1. Dans le coin inférieur droit de la page, cliquez sur **Enregistrer**.

>[!TAB Utiliser un groupe existant d’utilisateurs et d’utilisatrices]

Vous pouvez utiliser un groupe existant d’utilisateurs d’utilisatrices AEM s’il répond aux exigences d’accès de l’assistant IA, au lieu d’en créer un nouveau.

>[!ENDTABS]

## 4 - Ajouter des utilisateurs et des utilisatrices au groupe{#add-users}

1. Utilisez l’une des méthodes suivantes :

>[!BEGINTABS]

>[!TAB Ajouter des utilisateurs et des utilisatrices individuellement]

1. Sur la page **Groupes d’utilisateurs et d’utilisatrices**, dans le tableau **Nom du groupe**, cliquez sur le nom du groupe d’utilisateurs et d’utilisatrices que vous venez de créer ou sur un nom de groupe existant.

   ![Page Groupes d’utilisateurs et d’utilisatrices affichant le nom du groupe d’utilisateurs et d’utilisatrices de l’assistant IA d’AEM dans le tableau](/help/assets/assets-ai/ai-assistant-user-group-name-in-table.png)

1. Sur la page **Groupes d’utilisateurs et d’utilisatrices** de l’**assistant IA d’AEM**, cliquez sur l’onglet **Utilisateurs et utilisatrices**, puis sur **Ajouter des utilisateurs et des utilisatrices**.

   ![Assistant AI dans la page de groupes d’utilisateurs AEM, affichant l’onglet Utilisateurs et le bouton Ajouter des utilisateurs](/help/assets/assets-ai/ai-assistant-add-users.png)

1. Sur la page **`Add users to this user group`**, recherchez et sélectionnez les utilisateurs et utilisatrices qui doivent accéder à l’assistant IA d’AEM.

   ![Pager Ajouter des utilisateurs et des utilisatrices à ce groupe](/help/assets/assets-ai/ai-assistant-add-users-to-this-group.png)

1. Dans le coin inférieur droit de la page, cliquez sur **Enregistrer**.
1. Maintenant, [attribuez le profil de produit au groupe d’utilisateurs et d’utilisatrices](#assign-product-profile).

>[!TAB Ajout d’utilisateurs en bloc]

Vous pouvez utiliser la fonctionnalité de chargement en masse dans Admin Console.

1. Préparez un fichier CSV contenant des informations sur les utilisateurs et les utilisatrices.
1. Utilisez l’option **`Add users by CSV`** pour un ajout en masse efficace.
1. Maintenant, [attribuez le profil de produit au groupe d’utilisateurs et d’utilisatrices](#assign-product-profile).

>[!ENDTABS]


## 5 - Attribuer le profil de produit au groupe d’utilisateurs et d’utilisatrices{#assign-product-profile}

Cette étape suit le workflow Adobe Admin Console standard d’affectation de profils de produit à des groupes d’utilisateurs et d’utilisatrices.

Article de référence : [Gérer des profils de produit pour les utilisateurs et les utilisatrices de la formule Entreprise](https://helpx.adobe.com/fr/enterprise/using/manage-product-profiles.html)

1. Toujours dans votre groupe d’utilisateurs et d’utilisatrices de l’assistant IA d’AEM, à partir de [4 - Ajouter des utilisateurs et des utilisatrices au groupe](#add-users), cliquez sur l’onglet **Profils de produit attribués**.
1. Cliquez sur **Attribuer un profil**.

   ![Page du groupe d’utilisateurs et d’utilisatrices de l’assistant IA d’AEM avec l’onglet Profils de produit attribués sélectionné](/help/assets/assets-ai/ai-assistant-assign-profile.png)

1. Sur la page **Attribuer des produits et des profils**, dans la boîte de dialogue **Sélectionner des profils de produit**, recherchez et sélectionnez votre profil de produit **Assistant IA**.

   ![La page « Attribuer des produits et des profils », affichant la boîte de dialogue « Sélectionner des profils de produit » et le profil de produit « Assistant IA » sélectionné](/help/assets/assets-ai/ai-assistant-select-product-profile.png)

1. Près du coin inférieur droit de la boîte de dialogue, cliquez sur **Appliquer**.
1. Près du coin inférieur droit de la page **Attribuer des produits et des profils**, cliquez sur **Enregistrer**.

   ![Profil de produit Assistant IA affiché affecté au groupe d’utilisateurs et d’utilisatrices de l’assistant IA d’AEM](/help/assets/assets-ai/ai-assistant-profile-assigned-to-user-group.png)


## Vérifier la configuration

* Vérifiez que votre profil de produit affiche le nombre correct de groupes d’utilisateurs et d’utilisatrices affectés.
* Vérifiez que le groupe d’utilisateurs et d’utilisatrices indique le bon nombre de personnes.
* Vérifiez que l’autorisation de la connaissance des produits de l’assistant IA est activée et correctement configurée.


## Tester la configuration

Demandez à une personne du groupe affecté d’effectuer les opérations suivantes :

1. Connectez-vous à AEM.
2. Vérifiez que les fonctionnalités de l’assistant IA sont accessibles.
3. Testez la fonctionnalité de l’assistant IA pour vous assurer de son activation correcte.

## Voir également

* [Assistant IA dans AEM](/help/ai-assistant-in-aem.md)
* [Contrôle d’accès dans Adobe Experience Platform](https://experienceleague.adobe.com/fr/docs/experience-platform/access-control/ui/overview)
<!-- * [Cloud Manager Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md) -->
