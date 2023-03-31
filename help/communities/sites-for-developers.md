---
title: Principes élémentaires du site de la communauté
seo-title: Community Site Essentials
description: Exportation et suppression de sites communautaires et création de modèles de site personnalisés
seo-description: Exporting and deleting community sites and creating custom site templates
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
exl-id: 1dc568cd-315c-4944-9a3e-e5d7794e5dc0
source-git-commit: cc0574ae22758d095a3ca6b91f0ceae4a8691f0e
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 2%

---

# Principes élémentaires du site de la communauté {#community-site-essentials}

## Modèle de site personnalisé {#custom-site-template}

Un modèle de site personnalisé peut être spécifié séparément pour chaque copie de langue d’un site de communauté.

Procédez comme suit :

* Créez un modèle personnalisé.
* Recouvrez le chemin d’accès au modèle de site par défaut.
* Ajoutez le modèle personnalisé au chemin de recouvrement.
* Spécifiez le modèle personnalisé en ajoutant une `page-template` à la propriété `configuration` noeud .

**Modèle par défaut**:

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**Modèle personnalisé dans le chemin d’accès à la superposition**:

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**Propriété**: page-template

**Type**: Chaîne

**Valeur**: `template-name` (aucune extension)

**Noeud de configuration**:

`/content/community site path/lang/configuration`

Par exemple : `/content/sites/engage/en/configuration`

>[!NOTE]
>
>Tous les noeuds du chemin d’accès recouvert doivent uniquement être de type `Folder`.

>[!CAUTION]
>
>Si le modèle personnalisé reçoit le nom *sitepage.hbs*, tous les sites de communauté seront alors personnalisés.

### Exemple de modèle de site personnalisé {#custom-site-template-example}

Par exemple : `vertical-sitepage.hbs` est un modèle de site qui entraîne l’emplacement des liens de menu verticalement sur le côté gauche de la page, au lieu de horizontalement sous la bannière.

[Obtenir le fichier](assets/vertical-sitepage.hbs)
Placez le modèle de site personnalisé dans le dossier de recouvrement :

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

Identifiez le modèle personnalisé en ajoutant une `page-template` au noeud de configuration :

`/content/sites/sample/en/configuration`

![crxde-siteconfiguration](assets/crxde-siteconfiguration.png)

Veillez à **Enregistrer tout** et répliquez le code personnalisé sur toutes les instances d’AEM (le code personnalisé n’est pas inclus lorsque le contenu du site de la communauté est publié à partir de la console).

La pratique recommandée pour la réplication du code personnalisé consiste à [créer un package ;](../../help/sites-administering/package-manager.md#creating-a-new-package) et déployez-le sur toutes les instances.

## Exportation d’un site de communauté {#exporting-a-community-site}

Une fois un site communautaire créé, il est possible d’exporter le site sous la forme d’un package AEM stocké dans le gestionnaire de packages et disponible pour téléchargement et chargement.

Cette option est disponible à partir du [Console Sites Communities](sites-console.md#exporting-the-site).

Notez que le contenu généré par l’utilisateur et le code personnalisé ne sont pas inclus dans le package du site de la communauté.

Pour exporter du contenu créé par l’utilisateur, utilisez la variable [Outil de migration UGC AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration), un outil de migration Open Source disponible sur GitHub.

## Suppression d’un site de communauté {#deleting-a-community-site}

Depuis AEM Communities 6.3 Service Pack 1, l’icône Supprimer le site s’affiche lorsque vous placez le curseur de la souris sur le site de la communauté depuis **[!UICONTROL Communautés]** > **[!UICONTROL Sites]** console. Au cours du développement, si vous souhaitez supprimer un site de la communauté et recommencer à zéro, vous pouvez utiliser cette fonctionnalité. La suppression d’un site de communauté supprime les éléments suivants qui lui sont associés :

* [UGC](#user-generated-content)
* [Groupes d’utilisateurs](#community-user-groups)
* [Enregistrements de base de données](#database-records)

### Identifiant de site unique de la communauté {#community-unique-site-id}

Pour identifier l’identifiant de site unique associé au site de la communauté, à l’aide de CRXDE :

* Accédez à la racine de langue du site, telle que `/content/sites/*<site name>*/en/rep:policy`.

* Recherchez le `allow<#>` avec un noeud `rep:principalName` dans ce format `rep:principalName = *community-enable-nrh9h-members*`.

* L’identifiant de site est le troisième composant de `rep:principalName`

   Par exemple, si `rep:principalName = community-enable-nrh9h-members`

   * **nom du site** = *enable*
   * **ID de site** = *nrh9h*
   * **ID de site unique** = *enable-nrh9h*

### Contenu généré par l&#39;utilisateur {#user-generated-content}

Procurez-vous le projet communities-srp-tools de Github :

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

Contient un servlet permettant de supprimer tout le contenu généré par l’utilisateur de toute SRP.

Tout contenu généré par l’utilisateur peut être supprimé ou pour un site spécifique, par exemple :

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

Cela supprime uniquement le contenu généré par l’utilisateur (saisi lors de la publication) et non le contenu créé (saisi lors de la création). Par conséquent, [noeuds fantômes](srp.md#shadownodes) ne sont pas affectées.

### Groupes d’utilisateurs de la communauté {#community-user-groups}

Sur toutes les instances de création et de publication, à partir de [console de sécurité](../../help/sites-administering/security.md), recherchez et supprimez la variable [groupes d’utilisateurs](users.md) qui sont :

* Préfixe avec `community`
* Suivi de [identifiant de site unique](#community-unique-site-id)

Par exemple, `community-engage-x0e11-members`.
