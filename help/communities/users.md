---
title: Gestion des utilisateurs et des groupes d’utilisateurs
seo-title: Managing Users and User Groups
description: Les utilisateurs d’AEM Communities peuvent s’enregistrer et modifier leurs profils.
seo-description: Users of AEM Communities can self-register and edit their profiles
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
role: Admin
exl-id: 4237085a-d70d-41de-975d-153f58336daa
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 1%

---

# Gestion des utilisateurs et des groupes d’utilisateurs {#managing-users-and-user-groups}

## Vue d’ensemble {#overview}

Dans AEM Communities, dans l’environnement de publication, les utilisateurs peuvent s’inscrire eux-mêmes et modifier leurs profils. Avec les autorisations appropriées, ils peuvent également :

* Créez des sous-communautés dans le site de la communauté (voir [groupes communautaires](creating-groups.md)).

* [Modérer](moderation.md) contenu généré par l’utilisateur.

* Be [privilégié](#privileged-members-group) pour créer des entrées pour les blogs, les calendriers, les Q&amp;R et les forums.

Les utilisateurs enregistrés dans l’environnement de publication sont généralement appelés *membres de la communauté (membres)* pour les distinguer de *utilisateurs* dans l’environnement de création.

Les autorisations sont accordées en attribuant des membres à l’un des [groupes de membres (utilisateurs)](#publish-group-roles) créé dynamiquement lorsque le site de la communauté est [created](sites-console.md) ou [modified](sites-console.md#modifying-site-properties) dans l’environnement de création. Lorsque vous travaillez à partir de l’environnement de création, les membres sont visibles à partir de l’environnement de publication au moyen de la fonction [service tunnel](#tunnel-service).

Par conception, les membres et les groupes de membres créés dans l’environnement de publication ne doivent pas apparaître dans l’environnement de création. Les utilisateurs et les groupes d’utilisateurs créés dans l’environnement de création sont également destinés à rester dans l’environnement de création.

Lorsque les utilisateurs de l’instance de création et les membres de l’instance de publication proviennent de la même liste d’utilisateurs, tels que synchronisés à partir du même annuaire LDAP, ils ne sont pas considérés comme le même utilisateur disposant des mêmes autorisations et d’une même appartenance à un groupe dans les environnements de création et de publication. Le ou les rôles des membres et des utilisateurs doivent être définis séparément lors de la publication et de l’auteur, selon le cas.

Pour un [batterie de publication](topologies.md), l’enregistrement et les modifications effectués sur une instance de publication doivent être synchronisés avec d’autres instances de publication afin qu’elles aient accès aux mêmes données utilisateur. Pour plus d’informations, voir [Synchronisation des utilisateurs](sync.md), qui comprend une section décrivant [Que se passe-t-il quand...](sync.md#what-happens-when).

### Limites de contribution {#contribution-limits}

Pour se protéger du spam, il est possible de limiter la fréquence de publication du contenu par les membres. En outre, il est possible de limiter automatiquement les contributions des membres nouvellement enregistrés.

Pour plus d’informations, voir [Limites des contributions des membres](limits.md).

### Groupes d’utilisateurs créés dynamiquement {#dynamically-created-user-groups}

Lorsqu’un nouveau site communautaire est créé, de nouveaux groupes d’utilisateurs sont créés dynamiquement avec des identifiants uniques (uid) et des autorisations appropriées pour diverses fonctions administratives nécessaires à la gestion du site communautaire, que ce soit dans l’environnement de création (voir [Rôles du groupe de création](#author-group-roles)) ou l’environnement de publication (voir [Rôles du groupe de publication](#publish-group-roles)).

Les noms des groupes sont générés à partir du nom donné au site pendant la [création de site communautaire](sites-console.md#step13asitetemplate). Les identifiants uniques évitent les conflits de noms pour les sites de communauté et les groupes de communautés portant le même nom sur le même serveur.

Par exemple, si le nom du site était &quot;*engager*&quot; pour un site intitulé &quot;We.Retail Engage&quot;, l’un des groupes d’utilisateurs créés serait :

* Communauté *Interagir* Membres

## Environnement de création {#author-environment}

### Service Tunnel {#tunnel-service}

Lorsque vous utilisez l’environnement de création pour [créer des sites ;](sites-console.md), [modification des propriétés du site](sites-console.md#modifying-site-properties) et [gestion des membres de la communauté et des groupes de membres](members.md), il est nécessaire d’accéder aux utilisateurs et aux groupes d’utilisateurs enregistrés dans l’environnement de publication.

Le service tunnel fournit cet accès à l’aide de l’agent de réplication sur l’auteur.

* Pour plus d’informations, voir [instructions de configuration](deploy-communities.md#tunnel-service-on-author) sur la page de déploiement.

La variable [Consoles Membres et groupes de communautés](members.md) ne sont destinées qu’à la gestion des utilisateurs (membres) et des groupes d’utilisateurs (groupes de membres) enregistrés dans l’environnement de publication.

Pour gérer les utilisateurs et les groupes d’utilisateurs enregistrés dans l’environnement de création, utilisez le [Console de sécurité](../../help/sites-administering/security.md)

### Rôles du groupe de création {#author-group-roles}

| Si Membre du groupe... | Rôle de Principal |
|---|---|
| administrateurs | Le groupe administrateurs comprend les administrateurs système qui disposent de toutes les fonctionnalités d’un administrateur de la communauté ainsi que de la possibilité de gérer le groupe Administrateurs de la communauté. |
| Administrateurs de la communauté | Le groupe Administrateurs de la communauté devient automatiquement membre de tous les sites de la communauté et de tous les groupes de la communauté créés sur le site. Le groupe Administrateurs est un membre initial du groupe Administrateurs de la communauté. Dans l’environnement de création, les administrateurs de communauté peuvent créer des sites de communauté, gérer des sites, gérer les membres (ils peuvent interdire des membres de la communauté) et modérer le contenu. |
| Communauté &lt;*nom du site*> Gestionnaire de sites | Le gestionnaire de contenu du site de la communauté peut effectuer des AEM classiques de création, de création de contenu et de modification de pages pour un site de la communauté. |
| Aucun | Un visiteur anonyme du site ne peut pas accéder à l’environnement de création. |

### Administrateurs système {#system-administrators}

Les membres du groupe administrateurs sont des administrateurs système qui peuvent effectuer la configuration initiale d’une installation AEM pour les environnements de création et de publication.

À des fins de démonstration et de développement, le groupe d’administrateurs a un membre dont l’ID utilisateur est *admin* et le mot de passe est *admin*.

Pour les environnements de production, le groupe d’administrateurs par défaut doit être modifié.

Veillez à suivre le [Liste de contrôle de sécurité](../../help/sites-administering/security-checklist.md).

## Environnement de publication {#publish-environment}

### Devenir membre {#becoming-a-member}

Dans l’environnement de publication, en fonction de la variable [paramètres](sites-console.md#user-management) sur le site de la communauté, un visiteur du site peut devenir membre de la communauté :

* Lorsque le site de la communauté est privé (fermé) :
   * Par invitation
   * Par actions d’un administrateur

* Lorsque le site de la communauté est public (ouvert) :
   * Par auto-inscription
   * Par connexion sociale avec Facebook et Twitter

>[!NOTE]
>
>Si un visiteur du site s’inscrit en tant que membre d’un site communautaire ouvert, il devient automatiquement membre d’autres sites communautaires ouverts dans le même environnement de publication.

### Rôles du groupe de publication {#publish-group-roles}

| Si Membre du groupe... | Rôle de Principal |
|---|---|
| Communauté &lt;*nom du site*> Membres | Un membre du site de la communauté est un utilisateur enregistré. Ils peuvent se connecter, modifier leur profil, rejoindre un groupe de communautés ouvert, publier du contenu dans la communauté, envoyer des messages à d’autres membres et suivre les activités du site. |
| Communauté &lt;*nom du site*> Modérateurs | Un modérateur de site de communauté est un membre de la communauté de confiance qui peut modérer le contenu généré par l’utilisateur en bloc, à l’aide de la console de modération ou en contexte, sur la page où le contenu est publié. |
| Communauté &lt;*nom du site*> &lt;*nom du groupe*> Membres | Un membre d’un groupe communautaire est un membre de la communauté qui a rejoint un groupe communautaire ouvert ou qui a été invité à un groupe communautaire fermé. Ils disposent des capacités d’un membre pour ce groupe de la communauté dans le site. |
| Communauté &lt;*nom du site*> Administrateurs de groupes | Un administrateur de groupe de sites de communauté est un membre de communauté de confiance qui est chargé de créer et de gérer des sous-communautés (groupes) au sein d’un site de communauté. Il comprend la possibilité de fournir une modération contextuelle. |
| *Groupe de sécurité des membres privilégiés* | Groupe d’utilisateurs créé et géré manuellement dans le but de limiter la création de contenu. Voir [Groupe de membres privilégiés](#privileged-members-group). |
| Aucun | Un visiteur anonyme, qui découvre le site, peut afficher et rechercher des sites communautaires qui autorisent un accès anonyme. Pour participer et publier du contenu, l’utilisateur doit s’enregistrer (s’il y a lieu) et devenir membre de la communauté. |

### Affectation de membres aux rôles du groupe de publication {#assigning-members-to-publish-group-roles}

When [création d’un site communautaire](sites-console.md) dans l’environnement de création ou lorsque [modification des propriétés du site,](sites-console.md#modifying-site-properties) les membres peuvent se voir attribuer différents rôles effectués dans l’environnement de publication, tels que des modérateurs, des administrateurs de groupe, des contacts de ressources ou des membres privilégiés.

[Activation du service tunnel](sync.md#accessingpublishusersfromauthor) entraîne la présentation des choix d’affectation par les membres lors de la publication au lieu des utilisateurs lors de l’auteur.

Les membres sélectionnés seront automatiquement affectés au [groupe approprié](#publish-group-roles) et leurs appartenances seront incluses lorsque le site de la communauté sera (re)publié.

### Groupe de membres privilégiés {#privileged-members-group}

Le but d’un groupe de sécurité des membres privilégiés est de restreindre la création de contenu pour certaines fonctions de la communauté à un sous-ensemble privilégié des membres d’un site de communauté.

Le groupe des membres privilégiés est un groupe de membres créé et géré à l’aide de la variable [Console Groupes de communautés](members.md).

Après la création d’un groupe de membres privilégiés, et avec la variable [service tunnel activé](sync.md#accessingpublishusersfromauthor), la structure d’un site de communauté existant peut être [modified](sites-console.md#modify-structure) pour modifier la configuration de ses fonctions de communauté en &quot;Autoriser les membres privilégiés&quot; et ajouter le groupe créé.

Les fonctions de communauté qui permettent de spécifier un ou plusieurs groupes de membres privilégiés sont les suivantes :

* [Fonction de blog](functions.md#blog-function) - Pour restreindre la création de nouveaux articles.
* [Fonction Calendrier](functions.md#calendar-function) - Pour restreindre la création de nouveaux événements.
* [Fonction Forum](functions.md#forum-function) - Pour restreindre la création de nouvelles rubriques.
* [Fonction Q&amp;R](functions.md#qna-function) - Pour restreindre la création de nouvelles questions.

Lorsqu’une fonction de communauté n’est pas sécurisée (aucun groupe de membres privilégiés n’est affecté), tous les membres de la communauté du site sont autorisés à créer du contenu de fonction (articles, événements, sujets, questions).

>[!NOTE]
>
>L’ajout d’un utilisateur à un groupe de membres privilégiés pour un site communautaire ne lui permet de créer des privilèges que s’il est également membre de ce même site communautaire.

## Création de membres de la communauté {#creating-community-members}

### Emplacement du référentiel {#repository-location}

Pour que certaines fonctionnalités fonctionnent correctement, il est nécessaire de créer des utilisateurs et des groupes d’utilisateurs disposant des privilèges appropriés.

Lorsque des membres sont créés dans `/home/users/community`, ils héritent des listes de contrôle d’accès appropriées qui donnent des privilèges de lecture aux profils des membres.

De même, les groupes d’utilisateurs de communauté personnalisés (tels que les groupes de membres privilégiés) doivent être créés dans `/home/groups/community`.

En utilisant la variable [Consoles Membres et groupes de communautés](members.md) crée des utilisateurs et des groupes dans ces chemins.

Pour spécifier un chemin personnalisé, vous devez utiliser l’interface utilisateur de sécurité classique, accessible à l’adresse [https://&lt;server>:&lt;port>/useradmin](http://localhost:4503/useradmin).

Pour accorder des privilèges de lecture aux chemins de membre personnalisés, sur toutes les instances de publication, définissez des listes de contrôle d’accès similaires à `/home/users/community`:

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

Pour accorder les privilèges appropriés aux chemins d’accès de groupes de membres personnalisés, tels que /home/groups/mycompany, sur toutes les instances de publication, définissez des listes de contrôle d’accès similaires à `/home/groups/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### Consoles {#consoles}

Quatre consoles distinctes sont disponibles uniquement dans l’environnement de création :

| console | Outils, sécurité, utilisateurs | Outils, sécurité, groupes | Communautés, membres | Communautés, groupes |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| manage | utilisateurs sur l’auteur | groupes d’utilisateurs sur l’auteur | membres sur publication | groupes de membres sur publication |
| require | autorisation d’administrateur | autorisation d’administrateur | autorisation d’administrateur, service tunnel, synchronisation des utilisateurs pour la ferme de publication | autorisation d’administrateur, service tunnel, synchronisation des utilisateurs pour la ferme de publication |

### Rôle Administrateurs de la communauté {#community-administrators-role}

Comme indiqué dans la variable [Rôles du groupe de création](#author-group-roles) , les membres du groupe Administrateurs de la communauté peuvent créer des sites de la communauté, gérer les sites, gérer les membres (ils peuvent interdire des membres de la communauté) et modérer le contenu.

Suivez les mêmes étapes que pour créer et affecter un utilisateur au rôle de gestionnaire d’activation, mais ajoutez c `ommunity-administrators` groupe sous l’onglet Groupes de l’utilisateur.

### Intégration LDAP {#ldap-integration}

AEM prend en charge l’utilisation de LDAP pour l’authentification des utilisateurs et la création de comptes d’utilisateurs. Cette procédure est présentée dans la section [Configuration de LDAP avec AEM 6](../../help/sites-administering/ldap-config.md).

Voici quelques détails de configuration spécifiques aux membres de la communauté et aux groupes de membres.

1. Configurez LDAP pour chaque instance de publication AEM.
2. [Fournisseur d’identités LDAP](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * Aucune instruction spéciale

3. [Gestionnaire de synchronisation](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * Définissez les propriétés suivantes :

      * **[!UICONTROL Abonnement automatique des utilisateurs]**: `community-<site name>-<uid>-members`
      * **[!UICONTROL Préfixe du chemin d’accès de l’utilisateur ou de l’utilisatrice]**: `/community`
      * **[!UICONTROL Préfixe de chemin d’accès au groupe]**: `/community`

4. [Module de connexion externe](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * pas d’instructions spéciales

Les utilisateurs sont ainsi automatiquement affectés au groupe des membres du site de la communauté et à l’emplacement du référentiel. `/home/users/community` et `/home/groups/community`, afin qu’ils héritent des autorisations appropriées pour afficher le profil de l’autre.

* La variable `User auto membership` doit être la valeur `rep:authorizableId` , et non la propriété `givenName` (nom d’affichage) du profil.

## Synchronisation des utilisateurs entre les instances d’AEM {#synchronizing-users-among-aem-instances}

Lors de l’utilisation d’un [batterie de publication](topologies.md), assurez-vous que les utilisateurs disposent du même chemin d’accès sur chaque instance de publication en important d’abord les utilisateurs sur une instance et [activation de la synchronisation des utilisateurs](sync.md) à Sling pour distribuer les utilisateurs aux autres instances de publication.

Si vous importez des groupes d’utilisateurs, pour vous assurer que les groupes d’utilisateurs ont le même chemin sur chaque instance de publication, importez-les dans une instance, puis [créer un package ;](../../help/sites-administering/package-manager.md#creating-a-new-package) pour l’exportation et installez ce module sur toutes les autres instances de publication.

Bien que la synchronisation des groupes d’utilisateurs par le biais de la synchronisation des utilisateurs soit incluse dans une prochaine version, actuellement, seule la variable *abonnement* d’un groupe d’utilisateurs se synchronise lors de l’exécution de la synchronisation.

## Groupes communautaires {#about-community-groups}

Lors de la discussion de groupes, il existe deux sujets distincts :

* **[Groupes communautaires](overview.md#communitygroups)**

  Les groupes communautaires sont les sous-communautés qui peuvent être créées dans l’environnement de publication d’un site communautaire qui prend en charge la création de groupes communautaires. La création d’un groupe de communautés génère davantage de pages ajoutées au site web et est gérée de la même manière que le site de leur communauté parent. Pour plus d’informations, voir [Notions fondamentales sur les groupes de communautés](essentials-groups.md) pour les développeurs et [Groupe de communautés](creating-groups.md) pour les auteurs.

* **[Groupes de membres](../../help/sites-administering/security.md)**

  Les groupes de membres sont les groupes auxquels les membres peuvent appartenir et qui sont gérés via la console Groupes . Une grande partie de la discussion sur cette page a été consacrée aux groupes de membres. Les groupes de membres créés automatiquement pour un site de communauté sont précédés du préfixe *`Community`*, qui peut être appelé groupe communautaire, le contexte de la discussion doit donc être pris en compte.
