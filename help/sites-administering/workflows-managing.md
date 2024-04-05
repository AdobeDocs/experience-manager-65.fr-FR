---
title: Gestion de l’accès aux workflows
description: Découvrez comment configurer des listes de contrôle d’accès en fonction des comptes d’utilisateurs et d’utilisatrices pour autoriser (ou désactiver) le démarrage des workflows et la participation à ceux-ci.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: cc54d637-d66c-49d2-99ee-00d96f1a74e0
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 100%

---

# Gestion de l’accès aux workflows{#managing-access-to-workflows}

Configurez les listes de contrôle d’accès en fonction des comptes d’utilisateurs et d’utilisatrices pour autoriser (ou désactiver) le démarrage des workflows et la participation à ceux-ci.

## Autorisations d’utilisateurs et d’utilisatrices requises pour les workflows {#required-user-permissions-for-workflows}

Des actions sur les workflows peuvent être entreprises dans les cas suivants :

* Vous utilisez le compte `admin`.
* Le compte a été affecté au groupe par défaut `workflow-users` :

   * ce groupe contient tous les privilèges nécessaires pour que vos utilisateurs et utilisatrices puissent exécuter des actions de workflow.
   * lorsque le compte se trouve dans ce groupe, il a uniquement accès aux workflows qu’il a initiés.

* Le compte a été affecté au groupe par défaut `workflow-administrators` :

   * ce groupe contient tous les privilèges nécessaires pour que vos utilisateurs et utilisatrices privilégiés puissent surveiller et administrer les workflows.
   * lorsque le compte se trouve dans ce groupe, il a accès à tous les workflows.

>[!NOTE]
>
>Il s’agit des conditions requises minimales. Votre compte doit également être le participant affecté ou un membre du groupe affecté pour prendre des mesures spécifiques.

## Configurer l’accès aux workflows {#configuring-access-to-workflows}

Les modèles de workflows héritent d’une liste de contrôle d’accès par défaut pour contrôler les interactions possibles des utilisateurs avec les workflows. Pour personnaliser l’accès des utilisateurs et utilisatrices à un workflow, modifiez la liste de contrôle d’accès (ACL) dans le référentiel du dossier contenant le nœud de modèle de workflow :

* [Appliquez une liste de contrôle d’accès pour le modèle spécifique de workflow sous /var/workflow/models.](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [Créez un sous-dossier dans /var/workflow/models et appliquez-lui la liste de contrôle d’accès.](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>Pour plus d’informations sur l’utilisation de CRXDE Lite pour configurer des listes de contrôle d’accès, voir [Gestion des droits d’accès](/help/sites-administering/user-group-ac-admin.md#access-right-management).

### Appliquer une liste de contrôle d’accès pour le modèle spécifique de workflow sous /var/workflow/models {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

Si le modèle de workflow est stocké dans `/var/workflow/models`, vous pouvez affecter une liste de contrôle d’accès spécifique et ne se rapportant qu’à ce workflow, dans le dossier :

1. Ouvrez CRXDE Lite dans votre navigateur web, par exemple [https://localhost:4502/crx/de](http://localhost:4502/crx/de).
1. Dans l’arborescence de nœuds, sélectionnez le nœud du dossier des modèles de workflow :

   `/var/workflow/models`

1. Cliquez sur l’onglet **Contrôle d’accès**.
1. Dans le tableau **Politiques de contrôle d’accès locales** (**Liste de contrôle d’accès**), cliquez sur l’icône plus pour **ajouter une entrée**.
1. Dans la boîte de dialogue **Ajouter une nouvelle entrée**, ajoutez une commande ACE avec les propriétés suivantes :

   * **Principal** : `content-authors`
   * **Type** : `Deny`
   * **Autorisations** : `jcr:read`
   * **rep:glob** : référence au workflow spécifique

   ![wf-108](assets/wf-108.png)

   Le tableau **Liste de contrôle d’accès** comprend maintenant la restriction pour `content-authors` dans le modèle de workflow `prototype-wfm-01`.

   ![wf-109](assets/wf-109.png)

1. Cliquez sur **Enregistrer tout**.

   Le workflow `prototype-wfm-01` n’est plus disponible pour les membres du groupe `content-authors`.

### Créez un sous-dossier dans /var/workflow/models et appliquez-lui la liste de contrôle d’accès. {#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

Votre équipe de développement [ peut créer les workflows dans un sous-dossier ](/help/sites-developing/workflows-models.md#creating-a-new-workflow) de

`/var/workflow/models`

comparable aux workflows de gestion des ressources numériques stockés sous

`/var/workflow/models/dam/`

Vous pouvez alors ajouter une liste de contrôle d’accès dans le dossier proprement dit.

1. Ouvrez CRXDE Lite dans votre navigateur web (par exemple, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. Dans l’arborescence de nœuds, sélectionnez le nœud du dossier individuel dans le dossier des modèles de workflow, comme par exemple :

   `/var/workflow/models/prototypes`

1. Cliquez sur l’onglet **Contrôle d’accès**.
1. Dans le tableau **Politique de contrôle d’accès applicable**, cliquez sur l’icône « + » pour **ajouter** une entrée.
1. Dans le tableau **Politiques de contrôle d’accès locales** (**Liste de contrôle d’accès**), cliquez sur l’icône plus pour **ajouter une entrée**.
1. Dans la boîte de dialogue **Ajouter une nouvelle entrée**, ajoutez une commande ACE avec les propriétés suivantes :

   * **Principal** : `content-authors`
   * **Type** : `Deny`
   * **Autorisations** : `jcr:read`

   >[!NOTE]
   >
   >Comme lors de l’[application d’une liste de contrôle d’accès pour le modèle de workflow spécifique à /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models), vous pouvez inclure une propriété rep:glob pour limiter l’accès à un workflow spécifique.

   ![wf-110](assets/wf-110.png)

   Le tableau **Liste de contrôle d’accès** comprend maintenant la restriction pour `content-authors` dans le dossier `prototypes`.

   ![wf-111](assets/wf-111.png)

1. Cliquez sur **Enregistrer tout**.

   Les modèles du dossier `prototypes` ne sont plus disponibles pour les membres du groupe `content-authors`.
