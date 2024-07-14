---
title: Principes de base du site de la communauté
description: Exportation et suppression de sites communautaires et création de modèles de site personnalisés
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 1dc568cd-315c-4944-9a3e-e5d7794e5dc0
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 2%

---

# Principes de base du site de la communauté {#community-site-essentials}

## Modèle de site personnalisé {#custom-site-template}

Un modèle de site personnalisé peut être spécifié séparément pour chaque copie de langue d’un site de communauté.

Procédez comme suit :

* Créez un modèle personnalisé.
* Recouvrez le chemin du modèle de site par défaut.
* Ajoutez le modèle personnalisé au chemin de recouvrement.
* Spécifiez le modèle personnalisé en ajoutant une propriété `page-template` au noeud `configuration`.

**Modèle par défaut** :

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**Modèle personnalisé dans le chemin de recouvrement** :

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**Propriété** : page-template

**Type** : chaîne

**Valeur** : `template-name` (sans extension)

**Noeud de configuration** :

`/content/community site path/lang/configuration`

Par exemple : `/content/sites/engage/en/configuration`

>[!NOTE]
>
>Tous les noeuds du chemin d’accès superposé doivent uniquement être de type `Folder`.

>[!CAUTION]
>
>Si le modèle personnalisé est nommé *sitepage.hbs*, tous les sites de la communauté sont personnalisés.

### Exemple de modèle de site personnalisé {#custom-site-template-example}

Par exemple, `vertical-sitepage.hbs` est un modèle de site qui entraîne l’emplacement des liens de menu verticalement le long du côté gauche de la page, au lieu de horizontalement sous la bannière.

[Obtenir un fichier](assets/vertical-sitepage.hbs)
Placez le modèle de site personnalisé dans le dossier de recouvrement :

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

Identifiez le modèle personnalisé en ajoutant une propriété `page-template` au noeud de configuration :

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

Veillez à **Enregistrer tout** et répliquer le code personnalisé sur toutes les instances Adobe Experience Manager (AEM) (le code personnalisé n’est pas inclus lorsque le contenu du site de la communauté est publié à partir de la console).

La pratique recommandée pour répliquer le code personnalisé consiste à [créer un package](../../help/sites-administering/package-manager.md#creating-a-new-package) et le déployer sur toutes les instances.

## Exportation d’un site de communauté {#exporting-a-community-site}

Une fois qu’un site communautaire est créé, il est possible d’exporter le site sous la forme d’un package AEM stocké dans le gestionnaire de modules et disponible pour téléchargement et chargement.

Elle est disponible à partir de la [console Sites de communautés](sites-console.md#exporting-the-site).

Le contenu généré par l’utilisateur et le code personnalisé ne sont pas inclus dans le module de site de la communauté.

Pour exporter du contenu créé par l’utilisateur, utilisez l’[outil de migration du contenu créé par l’utilisateur AEM Communities](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration), un outil de migration open source disponible sur GitHub.

## Suppression d’un site de communauté {#deleting-a-community-site}

Depuis AEM Communities 6.3 Service Pack 1, l’icône Supprimer le site s’affiche en survolant le site de la communauté à partir de la console **[!UICONTROL Communautés]** > **[!UICONTROL Sites]** . Au cours du développement, si vous souhaitez supprimer un site de la communauté et recommencer à zéro, vous pouvez utiliser cette fonctionnalité. La suppression d’un site de communauté supprime les éléments suivants qui lui sont associés :

* [UGC](#user-generated-content)
* [Groupes d’utilisateurs et d’utilisatrices](#community-user-groups)
* [Enregistrements de base de données](#database-records)

### Identifiant de site unique de la communauté {#community-unique-site-id}

Pour identifier l’identifiant de site unique associé au site de la communauté, à l’aide de CRXDE :

* Accédez à la racine de langue du site, par exemple `/content/sites/*<site name>*/en/rep:policy`.

* Recherchez le noeud `allow<#>` avec un `rep:principalName` au format `rep:principalName = *community-enable-nrh9h-members*`.

* L’identifiant du site est le troisième composant de `rep:principalName`

  Par exemple, si `rep:principalName = community-enable-nrh9h-members`

   * **nom du site** = *enable*
   * **ID du site** = *nrh9h*
   * **identifiant de site unique** = *enable-nrh9h*

### Contenu généré par l’utilisateur {#user-generated-content}

Procurez-vous le projet communities-srp-tools à partir de GitHub :

* [https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

Contient un servlet permettant de supprimer tout le contenu généré par l’utilisateur de toute SRP.

Tout contenu généré par l’utilisateur peut être supprimé ou pour un site spécifique, par exemple :

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

Cela supprime uniquement le contenu généré par l’utilisateur (saisi lors de la publication) et non le contenu créé (saisi lors de la création). Par conséquent, les [noeuds fantômes](srp.md#shadownodes) ne sont pas affectés.

### Groupes d’utilisateurs communautaires {#community-user-groups}

Sur toutes les instances d’auteur et de publication, à partir de la [console de sécurité](../../help/sites-administering/security.md), recherchez et supprimez les [groupes d’utilisateurs](users.md) qui sont les suivants :

* Préfixe avec `community`
* Suivi de [identifiant de site unique](#community-unique-site-id)

Par exemple, `community-engage-x0e11-members`.
