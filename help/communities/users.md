---
title: Gestion des utilisateurs et des groupes d’utilisateurs
description: Les utilisateurs d’AEM Communities peuvent s’auto-enregistrer et modifier leurs profils
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 4237085a-d70d-41de-975d-153f58336daa
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1922'
ht-degree: 1%

---

# Gestion des utilisateurs et des groupes d’utilisateurs {#managing-users-and-user-groups}

## Vue d’ensemble {#overview}

Dans AEM Communities, dans l’environnement de publication, les utilisateurs peuvent s’auto-enregistrer et modifier leurs profils. Avec les autorisations appropriées, ils peuvent également :

* Créer des sous-communautés dans le site de la communauté (voir [groupes de communautés](creating-groups.md)).

* [Modéré](moderation.md) contenu créé par l’utilisateur.

* Soyez [privilégié](#privileged-members-group) pour créer des entrées pour les blogs, les calendriers, QnA et les forums.

Les utilisateurs enregistrés dans l’environnement de publication sont généralement appelés *membres de la communauté)* afin de les distinguer des *utilisateurs* dans l’environnement de création.

Les autorisations sont accordées en attribuant des membres à l’un des [groupes de membres (utilisateurs))](#publish-group-roles) créé dynamiquement lorsque le site de la communauté est [créé](sites-console.md) ou [modifié](sites-console.md#modifying-site-properties) à partir de l’environnement de création. Lorsque vous travaillez dans l’environnement de création, les membres sont visibles à partir de l’environnement de publication au moyen du [service tunnel](#tunnel-service).

Par défaut, les membres et les groupes de membres créés dans l’environnement de publication ne doivent pas apparaître dans l’environnement de création. Les utilisateurs et les groupes d’utilisateurs créés dans l’environnement de création sont également destinés à rester dans l’environnement de création.

Lorsque les utilisateurs en mode de création et les membres en mode de publication proviennent de la même liste d’utilisateurs, par exemple s’ils sont synchronisés à partir du même annuaire LDAP, ils ne sont pas considérés comme le même utilisateur avec les mêmes autorisations et la même appartenance à un groupe dans les environnements de création et de publication. Le ou les rôles des membres et des utilisateurs doivent être établis séparément en matière de publication et de création, selon le cas.

Pour une [ferme de publication](topologies.md), l’enregistrement et les modifications effectués sur une instance de publication doivent être synchronisés avec d’autres instances de publication afin qu’elles aient accès aux mêmes données utilisateur. Pour plus d’informations, consultez la section [Synchronisation des utilisateurs](sync.md) qui décrit [ce qui se passe lorsque...](sync.md#what-happens-when).

### Limites de contribution {#contribution-limits}

Pour vous protéger contre le spam, il est possible de limiter la fréquence de publication du contenu par les membres. De plus, il est possible de limiter automatiquement les contributions des nouveaux membres inscrits.

Pour plus de détails, voir [Limites de contribution des membres](limits.md).

### Groupes d’utilisateurs créés de manière dynamique {#dynamically-created-user-groups}

Lors de la création d’un site de communauté, de nouveaux groupes d’utilisateurs sont créés dynamiquement avec des ID uniques (uid) et des autorisations appropriées pour diverses fonctions administratives nécessaires à la gestion du site de communauté dans l’environnement de création (voir [Rôles de groupe de création](#author-group-roles)) ou dans l’environnement de publication (voir [Rôles de groupe de publication](#publish-group-roles)).

Les noms des groupes sont générés à partir du nom donné au site lors de la [création du site de la communauté](sites-console.md#step13asitetemplate). Les identifiants uniques évitent les conflits de noms pour les sites et groupes de communautés dotés de noms similaires sur le même serveur.

Par exemple, si le nom du site était « *engage* » pour un site intitulé « Engage », l’un des groupes d’utilisateurs créés serait :

* Community *Engage* Members

## Environnement de création {#author-environment}

### Service Tunnel {#tunnel-service}

Lors de l’utilisation de l’environnement de création pour [créer des sites](sites-console.md), [modifier les propriétés du site](sites-console.md#modifying-site-properties) et [gérer les membres de la communauté et les groupes de membres](members.md), il est nécessaire d’accéder aux utilisateurs et aux groupes d’utilisateurs enregistrés dans l’environnement de publication.

Le service de tunnel fournit cet accès à l’aide de l’agent de réplication sur l’auteur.

* Pour plus d’informations, consultez [instructions de configuration](deploy-communities.md#tunnel-service-on-author) sur la page Déploiement .

Les consoles [Membres et groupes de communautés](members.md) servent uniquement à gérer les utilisateurs (membres) et les groupes d’utilisateurs (groupes de membres) enregistrés dans l’environnement de publication.

Pour gérer les utilisateurs et les groupes d’utilisateurs enregistrés dans l’environnement de création, utilisez la console [Sécurité](../../help/sites-administering/security.md)

### Rôles de groupe d’auteurs {#author-group-roles}

| Si le membre du groupe... | Rôle de Principal |
|---|---|
| administrateurs ou administratrices | Le groupe administrateurs est constitué des administrateurs système qui possèdent toutes les capacités d’un administrateur de la communauté et la capacité de gérer le groupe d’administrateurs de la communauté. |
| Administrateurs de la communauté | Le groupe Administrateurs de la communauté devient automatiquement membre de tous les sites de la communauté et de tous les groupes de la communauté créés sur le site. Un membre initial du groupe Administrateurs de la communauté est le groupe Administrateurs . Dans l’environnement de création, les administrateurs de la communauté peuvent créer des sites de communauté, gérer des sites, gérer des membres (ils peuvent interdire des membres de la communauté) et modérer le contenu. |
| Communauté &lt;*nom du site*> Sitecontentmanager | Le gestionnaire de contenu de site communautaire peut effectuer la création, la création et la modification traditionnelles de pages d’AEM pour un site communautaire. |
| Aucun | Un visiteur anonyme du site peut ne pas accéder à l’environnement de création. |

### Administrateurs et administratrices système {#system-administrators}

Les membres du groupe administrateurs sont des administrateurs système qui peuvent effectuer la configuration initiale d’une installation AEM pour les environnements de création et de publication.

À des fins de démonstration et de développement, le groupe d’administrateurs comporte un membre dont l’ID utilisateur est *admin* et le mot de passe est *admin*.

Pour les environnements de production, le groupe d’administrateurs par défaut doit être modifié.

Veillez à suivre la [ Liste de contrôle de sécurité ](../../help/sites-administering/security-checklist.md).

## Environnement de publication {#publish-environment}

### Devenir membre {#becoming-a-member}

Dans l’environnement de publication, en fonction des [paramètres](sites-console.md#user-management) du site de la communauté, un visiteur du site peut devenir membre de la communauté :

* Lorsque le site communautaire est privé (fermé) :
  * Sur invitation
  * Par les actions d’un administrateur

* Lorsque le site communautaire est public (ouvert) :
  * Par auto-inscription
  * Par connexion sociale avec Facebook et Twitter

>[!NOTE]
>
>Si un visiteur du site s’enregistre en tant que membre d’un site communautaire ouvert, il devient automatiquement membre d’autres sites communautaires ouverts dans le même environnement de publication.

### Publier les rôles de groupe {#publish-group-roles}

| Si le membre du groupe... | Rôle de Principal |
|---|---|
| Membres de la communauté &lt;*nom du site*> | Un membre du site communautaire est un utilisateur enregistré. Ils peuvent se connecter, modifier leur profil, rejoindre un groupe communautaire ouvert, publier du contenu à l’intention de la communauté, envoyer des messages à d’autres membres et suivre les activités du site. |
| Modérateurs de la communauté &lt;*nom du site*> | Un modérateur de site de la communauté est un membre de la communauté de confiance qui peut modérer le contenu créé par l’utilisateur en bloc, à l’aide de la console de modération, ou en contexte, sur la page où le contenu est publié. |
| Membres de la communauté &lt;*nom du site*> &lt;*nom du groupe*> | Un membre d’un groupe communautaire est un membre de la communauté qui a rejoint un groupe communautaire ouvert ou qui a été invité à un groupe communautaire fermé. Ils ont les capacités d&#39;un membre de ce groupe communautaire au sein du site. |
| Administrateurs de groupes &lt;*nom du site*> de la communauté | Un administrateur de groupe de sites communautaires est un membre de la communauté de confiance qui est chargé de créer et de gérer des sous-communautés (groupes) au sein d&#39;un site communautaire. Elle offre également la possibilité de fournir une modération en contexte. |
| *Groupe de sécurité Membres privilégiés* | Groupe d’utilisateurs créé et géré manuellement dans le but de restreindre la création de contenu. Voir [Groupe de membres privilégiés](#privileged-members-group). |
| Aucun | Un visiteur anonyme du site, qui découvre le site, peut afficher et rechercher des sites communautaires qui autorisent un accès anonyme. Pour participer et publier du contenu, l’utilisateur doit s’auto-enregistrer (si autorisé) et devenir membre de la communauté. |

### Affectation de membres à des rôles de groupe de publication {#assigning-members-to-publish-group-roles}

Lors de la [création d’un site de la communauté](sites-console.md) dans l’environnement de création, ou lors de la [modification des propriétés du site](sites-console.md#modifying-site-properties) les membres peuvent se voir attribuer différents rôles dans l’environnement de publication, tels que des modérateurs, des administrateurs de groupe, des contacts de ressources ou des membres privilégiés.

[Activation du service tunnel](sync.md#accessingpublishusersfromauthor) entraîne la présentation des choix d’affectation à partir des membres lors de la publication au lieu des utilisateurs lors de la création.

Les membres sélectionnés seront automatiquement affectés au [groupe approprié](#publish-group-roles) et leurs adhésions seront incluses lorsque le site de la communauté sera (re)publié.

### Groupe de membres privilégiés {#privileged-members-group}

L&#39;objectif d&#39;un groupe de sécurité de membres privilégiés est de limiter la création de contenu pour certaines fonctions de communauté à un sous-ensemble privilégié des membres d&#39;un site de communauté.

Le groupe de membres privilégiés est un groupe de membres créé et géré à l’aide de la console [Groupes de communautés](members.md).

Après la création d&#39;un groupe de membres privilégiés, et lorsque le service [tunnel](sync.md#accessingpublishusersfromauthor) est activé, la structure d&#39;un site de communauté existant peut être [modifiée](sites-console.md#modify-structure) pour modifier la configuration de ses fonctions de communauté en &#39;Autoriser les membres privilégiés&#39; et ajouter le groupe créé.

Les fonctions de communauté qui permettent de spécifier un ou plusieurs groupes de membres privilégiés sont les suivantes :

* [Fonction de blog](functions.md#blog-function) - Pour restreindre la création de nouveaux articles.
* [Fonction de calendrier](functions.md#calendar-function) - Pour restreindre la création de nouveaux événements.
* [Fonction de forum](functions.md#forum-function) - Pour restreindre la création de nouvelles rubriques.
* [Fonction QnA](functions.md#qna-function) - Pour restreindre la création de nouvelles questions.

Lorsqu’une fonction de communauté n’est pas sécurisée (aucun groupe de membres privilégiés n’est affecté), tous les membres du site de la communauté sont autorisés à créer du contenu de fonctionnalité (articles, événements, sujets, questions).

>[!NOTE]
>
>L’ajout d’un utilisateur à un groupe de membres privilégiés pour un site communautaire ne lui accorde des privilèges de création que s’il est également membre de ce même site communautaire.

## Création de membres de la communauté {#creating-community-members}

### Emplacement du référentiel {#repository-location}

Pour que certaines fonctionnalités fonctionnent correctement, il est nécessaire de créer des utilisateurs et des groupes d’utilisateurs avec les privilèges appropriés.

Lorsque des membres sont créés dans `/home/users/community`, ils héritent des listes de contrôle d’accès appropriées qui accordent des privilèges de lecture aux profils des membres.

De même, les groupes d’utilisateurs de la communauté personnalisée (tels que les groupes de membres privilégiés) doivent être créés dans `/home/groups/community`.

Les consoles [Membres et groupes de Communities](members.md) permettent de créer des utilisateurs et des groupes dans ces chemins d’accès.

Pour spécifier un chemin personnalisé, utilisez l’interface utilisateur de sécurité classique, accessible à l’adresse [https://&lt;server>:&lt;port>/useradmin](http://localhost:4503/useradmin).

Pour accorder des privilèges de lecture aux chemins d’accès des membres personnalisés, définissez des listes de contrôle d’accès similaires à `/home/users/community` sur toutes les instances de publication :

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="everyone"
  rep:privileges="{Name}[jcr:read]" >
  <rep:restrictions
    jcr:primaryType="rep:Restrictions"
    rep:glob="*/profile*" />
</allow>
```

Pour attribuer les privilèges appropriés aux chemins d’accès des groupes de membres personnalisés, tels que /home/groups/mycompany, sur toutes les instances de publication, définissez des listes de contrôle d’accès similaires à `/home/groups/community` :

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### Consoles {#consoles}

Il existe quatre consoles distinctes disponibles uniquement dans l’environnement de création :

| console | Outils, Sécurité, Utilisateurs | Outils, Sécurité, Groupes | Communities, Members | Communities, Groups |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| gère | utilisateurs en mode de création | groupes d’utilisateurs en mode de création | membres en mode de publication | groupes de membres en mode de publication |
| requiert | autorisation admin | autorisation admin | autorisation admin, service tunnel, synchronisation des utilisateurs pour la batterie de publication | autorisation admin, service tunnel, synchronisation des utilisateurs pour la batterie de publication |

### Rôle Administrateurs de la communauté {#community-administrators-role}

Comme indiqué dans le graphique [Rôles du groupe de création](#author-group-roles), les membres du groupe Administrateurs de la communauté peuvent créer des sites de communauté, gérer des sites, gérer des membres (ils peuvent interdire des membres de la communauté) et modérer le contenu.

Suivez les mêmes étapes que pour créer et affecter un utilisateur au rôle de responsable de l’activation, mais ajoutez le groupe c `ommunity-administrators` sous l’onglet Groupes de l’utilisateur.

### Intégration LDAP {#ldap-integration}

AEM prend en charge l’utilisation de LDAP pour l’authentification des utilisateurs et la création de comptes utilisateur. Vous trouverez des informations détaillées dans la section [Configuration de LDAP avec AEM 6](../../help/sites-administering/ldap-config.md).

Vous trouverez ci-dessous quelques détails de configuration spécifiques aux membres de la communauté et aux groupes de membres.

1. Configurez LDAP pour chaque instance de publication AEM.
2. [Fournisseur d’identité LDAP](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * Pas d’instructions spéciales

3. [Gestionnaire de synchronisation](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * Définissez les propriétés suivantes :

     * **[!UICONTROL Abonnement automatique des utilisateurs]** : `community-<site name>-<uid>-members`
     * **[!UICONTROL Préfixe de chemin d’accès utilisateur]** : `/community`
     * **[!UICONTROL Préfixe de chemin d’accès du groupe]** : `/community`

4. [Le module de connexion externe](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * pas d&#39;instructions particulières

Ainsi, les utilisateurs sont automatiquement affectés au groupe des membres du site de la communauté et l’emplacement du référentiel est `/home/users/community` et `/home/groups/community`, de sorte qu’ils héritent des autorisations appropriées pour voir le profil des uns et des autres.

* La valeur `User auto membership` doit être la propriété `rep:authorizableId`, et non le `givenName` (nom d’affichage) du profil.

## Synchronisation Des Utilisateurs Entre Les Instances AEM {#synchronizing-users-among-aem-instances}

Lors de l’utilisation d’une [ferme de publication](topologies.md), assurez-vous que les utilisateurs disposent du même chemin d’accès sur chaque instance de publication en important les utilisateurs d’abord dans une instance et en [activant la synchronisation des utilisateurs](sync.md) dans Sling pour distribuer les utilisateurs aux autres instances de publication.

Si vous importez des groupes d’utilisateurs, pour vous assurer que les groupes d’utilisateurs disposent du même chemin d’accès sur chaque instance de publication, importez vers une instance, puis [créez un package](../../help/sites-administering/package-manager.md#creating-a-new-package) pour l’exportation et installez-le sur toutes les autres instances de publication.

Bien que la synchronisation des groupes d’utilisateurs par le biais de la synchronisation des utilisateurs soit incluse dans une prochaine version, actuellement seule l’*appartenance* d’un groupe d’utilisateurs est synchronisée lors de l’exécution de la synchronisation des utilisateurs.

## À Propos Des Groupes De La Communauté {#about-community-groups}

Lors de la discussion de groupes, il existe deux sujets distincts :

* **[Groupes communautaires](overview.md#communitygroups)**

  Les groupes communautaires sont les sous-communautés qui peuvent être créées dans l’environnement de publication pour un site communautaire qui prend en charge la création de groupes communautaires. La création d’un groupe de la communauté entraîne l’ajout d’un plus grand nombre de pages au site web et la gestion de celui-ci est similaire au site de la communauté parente. Pour plus d’informations, consultez [Principes de base du groupe de la communauté](essentials-groups.md) pour les développeurs et [Groupe de la communauté](creating-groups.md) pour les auteurs.

* **[Groupes de membres](../../help/sites-administering/security.md)**

  Les groupes de membres sont les groupes auxquels les membres peuvent appartenir. Ils sont gérés via la console Groupes. Une grande partie de la discussion sur cette page a été consacrée aux groupes membres. Les groupes membres créés automatiquement pour un site communautaire, qui comportent le préfixe *`Community`*, peuvent être appelés groupes communautaires, c&#39;est pourquoi le contexte de la discussion doit être pris en compte.
