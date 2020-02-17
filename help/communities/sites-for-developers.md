---
title: Site communautaire Essentials
seo-title: Site communautaire Essentials
description: Exportation et suppression de sites de la communauté et création de modèles de site personnalisés
seo-description: Exportation et suppression de sites de la communauté et création de modèles de site personnalisés
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Site communautaire Essentials {#community-site-essentials}

## Modèle de site personnalisé {#custom-site-template}

Un modèle de site personnalisé peut être spécifié séparément pour chaque copie linguistique d’un site communautaire.

Pour ce faire,

* Création d’un modèle personnalisé
* Recouvrir le chemin d’accès au modèle de site par défaut
* Ajouter le modèle personnalisé au chemin d’accès de l’incrustation
* Spécifiez le modèle personnalisé en ajoutant une `page-template` propriété au `configuration` noeud

**Modèle** par défaut :

/**libs**/social/console/components/hbs/sitepage/**sitepage**.hbs

**Modèle personnalisé dans le chemin** d’incrustation :

/**apps**/social/console/components/hbs/sitepage/**&lt;nomdu *modèle*>**.hbs

**Propriété**: page-template **Type**: Chaîne **Valeur**: &lt;*template-name*> (sans extension)

**Noeud** de configuration :

/content/&lt;chemin *du site* de la communauté>/&lt;*lang*>/configuration

Par exemple : /content/sites/engagement/fr/configuration

>[!NOTE]
>
>Tous les noeuds du chemin superposé doivent uniquement être de type `Folder`.

>[!CAUTION]
>
>Si le modèle personnalisé porte le nom *sitepage.hbs,* tous les sites de la communauté seront personnalisés.

### Exemple de modèle de site personnalisé {#custom-site-template-example}

Par exemple, `vertical-sitepage.hbs` est un modèle de site qui permet de placer les liens de menu verticalement sur le côté gauche de la page, plutôt que horizontalement sous la bannière.

[Obtenir un fichier](assets/vertical-sitepage.hbs)Placez le modèle de site personnalisé dans le dossier de recouvrement :

/**apps**/social/console/components/hbs/sitepage/**vertical-sitepage**.hbs

Identifiez le modèle personnalisé en ajoutant une `page-template` propriété au noeud de configuration :

/content/sites/sample/fr/configuration

![chlimage_1-80](assets/chlimage_1-80.png)

Veillez à **Enregistrer tout** et à répliquer le code personnalisé dans toutes les instances AEM (le code personnalisé n’est pas inclus lorsque le contenu du site de la communauté est publié à partir de la console).

La pratique recommandée pour la réplication du code personnalisé consiste à [créer un package](../../help/sites-administering/package-manager.md#creating-a-new-package) et à le déployer sur toutes les instances.

## Exportation d’un site de la communauté {#exporting-a-community-site}

Une fois un site communautaire créé, il est possible d’exporter le site sous la forme d’un package AEM stocké dans le gestionnaire de packages et disponible pour téléchargement et téléchargement.

Cette fonction est disponible dans la console [Sites](sites-console.md#exporting-the-site)des communautés.

Notez que l’UGC et le code personnalisé ne sont pas inclus dans le package du site de la communauté.

Pour exporter l’UGC, utilisez l’outil [de migration UGC des communautés](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)AEM, un outil de migration open source disponible sur GitHub.

## Suppression d’un site de la communauté {#deleting-a-community-site}

Depuis la version 6.3 du Service Pack 1 d’AEM Communities, l’icône Supprimer le site s’affiche lorsque vous passez la souris sur le site de la communauté à partir de la console Communautés > Sites. Au cours du développement, si vous souhaitez supprimer un site communautaire et recommencer à zéro, vous pouvez utiliser cette fonctionnalité. La suppression d’un site communautaire supprime les éléments suivants associés à ce site :

* [UGC](#user-generated-content)
* [Groupes d’utilisateurs](#community-user-groups)
* [Assets](#enablement-assets)
* [Enregistrements de base de données](#database-records)

### Identifiant de site unique de la communauté {#community-unique-site-id}

Pour identifier l’identifiant de site unique associé au site de la communauté, utilisez CRXDE :

* Accédez à la langue racine du site, telle que `/content/sites/*<site name>*/en/rep:policy`

* Rechercher le `allow<#>` noeud avec un `rep:principalName` format dans ce format `rep:principalName = *community-enable-nrh9h-members*`

* L’ID de site est le troisième composant de `rep:principalName`la variable `rep:principalName = community-enable-nrh9h-members`

   * **nom** du site = *enable*
   * **ID** du site = *nrh9h*
   * **ID** de site unique = *enable-nrh9h*

### Contenu généré par l&#39;utilisateur {#user-generated-content}

Obtenez le projet community-srp-tools de Github :

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

Contient une servlet pour supprimer toutes les UGC de tout SRP.

Tout UGC peut être supprimé ou pour un site spécifique, par exemple :

* path=/content/usergenerated/asi/mongo/content/sites/engage

Cela supprime uniquement le contenu généré par l’utilisateur (entré lors de la publication) et non le contenu créé (entré lors de la création). Par conséquent, les noeuds [d’](srp.md#shadownodes) ombre ne sont pas affectés.

### Groupes d’utilisateurs de la communauté {#community-user-groups}

Sur toutes les instances d’auteur et de publication, dans la console [de](../../help/sites-administering/security.md)sécurité, recherchez et supprimez les groupes [d’](users.md) utilisateurs suivants :

* Préfixe avec `community`
* Suivi d’un ID de site [unique](#community-unique-site-id)

Par exemple, `community-engage-x0e11-members`.

### Ressources d’activation {#enablement-assets}

Depuis la console principale :

* Select **[!UICONTROL Assets]**
* Passer en mode **[!UICONTROL Sélectionner]**
* Sélectionner le dossier nommé avec l&#39;ID de site [unique](#community-unique-site-id)
* Sélectionnez **[!UICONTROL Supprimer]** (vous devrez peut-être sélectionner **[!UICONTROL Plus...]**).

### Enregistrements de base de données {#database-records}

Il n&#39;existe aucun outil pour supprimer de manière sélective les entrées de base de données d&#39;un site de la communauté d&#39;activation spécifique.

Lorsque tous les sites de la communauté sont supprimés, déposez les valeurs enablementdb et scormenginedb à l’aide de MySQL Workbench.
