---
title: Gestion des utilisateurs et des groupes d’utilisateurs
seo-title: Gestion des utilisateurs et des groupes d’utilisateurs
description: Les utilisateurs d’AEM Communities peuvent s’enregistrer et modifier leurs profils.
seo-description: Les utilisateurs d’AEM Communities peuvent s’enregistrer et modifier leurs profils.
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
role: Administrator
exl-id: 4237085a-d70d-41de-975d-153f58336daa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2183'
ht-degree: 1%

---

# Gestion des utilisateurs et des groupes d’utilisateurs {#managing-users-and-user-groups}

## Présentation {#overview}

Dans AEM Communities, dans l’environnement de publication, les utilisateurs peuvent s’inscrire eux-mêmes et modifier leurs profils. Avec les autorisations appropriées, ils peuvent également :

* Créez des sous-communautés dans le site de la communauté (voir [groupes de communautés](creating-groups.md)).

* [](moderation.md) Contenu généré par l’utilisateur modéré.

* Soyez des contacts [ressource d’activation](resources.md).

* Soyez [privilégié](#privileged-members-group) pour créer des entrées pour les blogs, les calendriers, les Q&amp;R et les forums.

Les utilisateurs enregistrés dans l’environnement de publication sont généralement appelés *membres de la communauté (membres)* pour les distinguer de *utilisateurs* dans l’environnement de création.

Les autorisations sont accordées en attribuant des membres à l’un des groupes [membres (utilisateur)](#publish-group-roles) créés dynamiquement lorsque le site de la communauté est [créé](sites-console.md) ou [modifié](sites-console.md#modifying-site-properties) à partir de l’environnement de création. Lorsque vous travaillez à partir de l’environnement de création, les membres sont visibles à partir de l’environnement de publication au moyen du [service tunnel](#tunnel-service).

Par conception, les membres et les groupes de membres créés dans l’environnement de publication ne doivent pas apparaître dans l’environnement de création. Les utilisateurs et les groupes d’utilisateurs créés dans l’environnement de création sont également destinés à rester dans l’environnement de création.

Lorsque les utilisateurs de l’instance de création et les membres de l’instance de publication proviennent de la même liste d’utilisateurs, tels que synchronisés à partir du même annuaire LDAP, ils ne sont pas considérés comme le même utilisateur disposant des mêmes autorisations et d’une même appartenance à un groupe dans les environnements de création et de publication. Le ou les rôles des membres et des utilisateurs doivent être définis séparément lors de la publication et de l’auteur, selon le cas.

Pour une [ferme de publication](topologies.md), l’enregistrement et les modifications effectués sur une instance de publication doivent être synchronisés avec d’autres instances de publication afin qu’elles aient accès aux mêmes données utilisateur. Pour plus d’informations, voir [Synchronisation des utilisateurs](sync.md), qui comprend une section décrivant [ce qui se passe lorsque..](sync.md#what-happens-when).

### Limites de contribution {#contribution-limits}

Afin de se protéger du spam, il est possible de limiter la fréquence de publication du contenu par les membres. En outre, il est possible de limiter automatiquement les contributions des membres nouvellement enregistrés.

Pour plus d’informations, voir [Limites de contribution des membres](limits.md).

### Groupes d’utilisateurs créés dynamiquement {#dynamically-created-user-groups}

Lors de la création d’un site communautaire, de nouveaux groupes d’utilisateurs sont créés dynamiquement avec des identifiants uniques (uid) et des autorisations appropriées pour diverses fonctions administratives nécessaires à la gestion du site communautaire, soit dans l’environnement de création (voir [Rôles du groupe d’auteur](#author-group-roles)), soit dans l’environnement de publication (voir [Rôles du groupe de publication](#publish-group-roles)).

Les noms des groupes sont générés à partir du nom donné au site lors de la [création du site communautaire](sites-console.md#step13asitetemplate). Les identifiants uniques évitent les conflits de noms pour les sites de communauté et les groupes de communautés portant le même nom sur le même serveur.

Par exemple, si le nom du site était &quot;*engage*&quot; pour un site intitulé &quot;We.Retail Engage&quot;, l’un des groupes d’utilisateurs créés serait :

* Communauté *Interagir* Membres

## Environnement de création {#author-environment}

### Service Tunnel {#tunnel-service}

Lorsque vous utilisez l’environnement de création pour [créer des sites](sites-console.md), [modifier les propriétés du site](sites-console.md#modifying-site-properties) et [gérer les membres de la communauté et les groupes de membres](members.md), il est nécessaire d’accéder aux utilisateurs et aux groupes d’utilisateurs enregistrés dans l’environnement de publication.

Le service tunnel fournit cet accès à l’aide de l’agent de réplication sur l’auteur.

* Pour plus d’informations, voir [instructions de configuration](deploy-communities.md#tunnel-service-on-author) sur la page de déploiement.

Les [consoles Membres et groupes des communautés](members.md) ont pour seul objectif de gérer les utilisateurs (membres) et les groupes d’utilisateurs (groupes de membres) enregistrés uniquement dans l’environnement de publication.

Pour gérer les utilisateurs et les groupes d’utilisateurs enregistrés dans l’environnement de création, utilisez la [console de sécurité](../../help/sites-administering/security.md)

### Rôles du groupe d’auteur {#author-group-roles}

| Si Membre du groupe... | Rôle Principal |
|---|---|
| administrators | Le groupe administrateurs comprend les administrateurs système qui disposent de toutes les fonctionnalités d’un administrateur de la communauté ainsi que de la possibilité de gérer le groupe Administrateurs de la communauté. |
| Administrateurs de la communauté | Le groupe Administrateurs de la communauté devient automatiquement membre de tous les sites de la communauté et de tous les groupes de la communauté créés sur le site. Le groupe Administrateurs est un membre initial du groupe Administrateurs de la communauté. Dans l’environnement de création, les administrateurs de communauté peuvent créer des sites de communauté, gérer des sites, gérer les membres (ils peuvent interdire des membres de la communauté) et modérer le contenu. |
| Communauté &quot;a0/>nom du site&lt;a1/&quot; Sitecontentmanager ** | Le gestionnaire de contenu du site de la communauté peut effectuer des AEM classiques de création, de création de contenu et de modification de pages pour un site de la communauté. |
| Chefs d’activation de la communauté | Le groupe Chefs d’activation de la communauté se compose d’utilisateurs pouvant être affectés à la gestion du groupe Gestionnaires d’activation d’un site de la communauté. |
| Communauté &quot;a0/>nom du site *> Gestionnaire de sites* | Le groupe Responsables de l’activation du site de la communauté est constitué d’utilisateurs chargés de gérer les [ressources](resources.md) d’activation d’un site de la communauté. |
| Aucune | Un visiteur anonyme du site ne peut pas accéder à l’environnement de création. |

### Administrateurs système {#system-administrators}

Les membres du groupe administrateurs sont des administrateurs système qui peuvent effectuer la configuration initiale d’une installation AEM pour les environnements de création et de publication.

À des fins de démonstration et de développement, le groupe d’administrateurs a un membre dont l’ID utilisateur est *admin* et le mot de passe est *admin*.

Pour les environnements de production, le groupe d’administrateurs par défaut doit être modifié.

Veillez à suivre la [liste de contrôle de sécurité](../../help/sites-administering/security-checklist.md).

## Environnement de publication {#publish-environment}

### Devenir membre {#becoming-a-member}

Dans l’environnement de publication, en fonction des [paramètres](sites-console.md#user-management) du site de la communauté, un visiteur du site peut devenir membre de la communauté :

* Lorsque le site de la communauté est privé (fermé) :
   * Par invitation
   * Par actions d’un administrateur

* Lorsque le site de la communauté est public (ouvert) :
   * Par auto-inscription
   * Par connexion sociale avec Facebook et Twitter

>[!NOTE]
>
>Si un visiteur du site s’inscrit en tant que membre d’un site communautaire ouvert, il devient automatiquement membre d’autres sites communautaires ouverts dans le même environnement de publication.

### Publier les rôles du groupe {#publish-group-roles}

| Si Membre du groupe... | Rôle Principal |
|---|---|
| Communauté &quot;a0/>nom du site *Membres* | Un membre du site de la communauté est un utilisateur enregistré. Ils peuvent se connecter, modifier leur profil, rejoindre un groupe de communautés ouvert, publier du contenu dans la communauté, envoyer des messages à d’autres membres et suivre les activités du site. |
| Communauté &quot;a0/>nom du site *Modérateurs* | Un modérateur de site de communauté est un membre de la communauté de confiance qui peut modérer le contenu généré par l’utilisateur en bloc, à l’aide de la console de modération ou en contexte, sur la page où le contenu est publié. |
| Nom de la communauté &quot;a0/>nom du site *&quot;a2/>nom du groupe&lt;a3/&quot; Membres*** | Un membre d’un groupe communautaire est un membre de la communauté qui a rejoint un groupe communautaire ouvert ou qui a été invité à un groupe communautaire fermé. Ils disposent des capacités d’un membre pour ce groupe de la communauté dans le site. |
| Communauté &quot;a0/>nom du site *Administrateurs de groupes* | Un administrateur de groupe de sites de communauté est un membre de communauté de confiance qui est chargé de créer et de gérer des sous-communautés (groupes) au sein d’un site de communauté. Il comprend la possibilité de fournir une modération contextuelle. |
| *Groupe de sécurité des membres privilégiés* | Groupe d’utilisateurs créé et géré manuellement dans le but de limiter la création de contenu. Voir [Groupe de membres privilégiés](#privileged-members-group). |
| Aucune | Un visiteur anonyme, qui découvre le site, peut afficher et rechercher des sites communautaires qui autorisent un accès anonyme. Pour participer et publier du contenu, l’utilisateur doit s’enregistrer (s’il y a lieu) et devenir membre de la communauté. |

### Affectation de membres aux rôles du groupe de publication {#assigning-members-to-publish-group-roles}

Lors de la [création d’un site communautaire](sites-console.md) dans l’environnement de création ou de la [modification des propriétés du site, les membres](sites-console.md#modifying-site-properties) peuvent se voir attribuer différents rôles effectués dans l’environnement de publication, tels que des modérateurs, des administrateurs de groupe, des contacts de ressources ou des membres privilégiés.

[L’activation des ](sync.md#accessingpublishusersfromauthor) services de tunnel entraîne la présentation des choix d’affectation par les membres lors de la publication et non par les utilisateurs lors de l’auteur.

Les membres sélectionnés seront automatiquement affectés au [groupe approprié](#publish-group-roles) et leurs appartenances seront incluses lorsque le site de la communauté sera (re) publié.

### Groupe de membres privilégiés {#privileged-members-group}

Le but d’un groupe de sécurité des membres privilégiés est de restreindre la création de contenu pour certaines fonctions de la communauté à un sous-ensemble privilégié des membres d’un site de communauté.

Le groupe des membres privilégiés est un groupe de membres créé et géré à l’aide de la [console Groupes communautaires](members.md).

Après la création d’un groupe de membres privilégiés et avec le [service tunnel activé](sync.md#accessingpublishusersfromauthor), la structure d’un site de communauté existant peut être [modifiée](sites-console.md#modify-structure) pour modifier la configuration de ses fonctions de communauté en &quot;Autoriser les membres privilégiés&quot; et ajouter le groupe créé.

Les fonctions de communauté qui permettent de spécifier un ou plusieurs groupes de membres privilégiés sont les suivantes :

* [Fonction](functions.md#blog-function)  de blog : pour restreindre la création de nouveaux articles.
* [Fonction](functions.md#calendar-function)  du calendrier : pour limiter la création de nouveaux événements.
* [Fonction Forum](functions.md#forum-function)  : pour limiter la création de nouvelles rubriques.
* [Fonction Q&amp;R](functions.md#qna-function)  : pour restreindre la création de nouvelles questions.

Lorsqu’une fonction de communauté n’est pas sécurisée (aucun groupe de membres privilégiés n’est affecté), tous les membres de la communauté du site sont autorisés à créer du contenu de fonction (articles, événements, sujets, questions).

>[!NOTE]
>
>L’ajout d’un utilisateur à un groupe de membres privilégiés pour un site communautaire ne lui permet de créer des privilèges que s’il est également membre de ce même site communautaire.

## Création de membres de la communauté {#creating-community-members}

### Emplacement du référentiel {#repository-location}

Pour que certaines fonctionnalités fonctionnent correctement, il est nécessaire de créer des utilisateurs et des groupes d’utilisateurs disposant des privilèges appropriés.

Lorsque des membres sont créés dans `/home/users/community`, ils héritent des listes de contrôle d’accès appropriées qui donnent des privilèges de lecture aux profils des membres.

De même, les groupes d’utilisateurs personnalisés de la communauté (tels que les groupes de membres privilégiés) doivent être créés dans `/home/groups/community`.

L’utilisation des [consoles Membres et groupes des communautés](members.md) créera des utilisateurs et des groupes dans ces chemins.

Pour spécifier un chemin personnalisé, vous devez utiliser l’IU de sécurité classique, accessible à l’adresse [https://&lt;server>:&lt;port>/useradmin](http://localhost:4503/useradmin).

Pour accorder des privilèges de lecture aux chemins de membre personnalisés, sur toutes les instances de publication, définissez des listes de contrôle d’accès similaires à `/home/users/community` :

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

Pour accorder les privilèges appropriés aux chemins de groupes de membres personnalisés, tels que /home/groups/mycompany, sur toutes les instances de publication, définissez des listes de contrôle d’accès similaires à `/home/groups/community` :

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
| manage | utilisateurs sur l’auteur | groupes d’utilisateurs sur l’auteur | membres sur publication | groupes de membres lors de la publication |
| require | autorisation d’administrateur | autorisation d’administrateur | autorisation d’administrateur, service tunnel, synchronisation des utilisateurs pour la ferme de publication | autorisation d’administrateur, service tunnel, synchronisation des utilisateurs pour la ferme de publication |

### Rôle du gestionnaire d’activation de la communauté {#community-enablement-manager-role}

La possibilité pour un visiteur du site de s’inscrire lui-même n’est généralement pas autorisée pour une [communauté d’activation](overview.md#enablement-community), car chaque membre a des coûts. Les apprenants et les ressources d’activation sont gérés par un utilisateur auquel est affecté le [rôle](#author-group-roles) de `enablement manager` [lors de la création du site](sites-console.md#enablement) sur l’auteur (ajouté en tant que membre du groupe `Community <site-name> Siteenablementmanagers`). `enablement manager` est également chargé d’[affecter des ressources d’apprentissage](resources.md) aux membres de la communauté sur l’auteur.

Seuls les utilisateurs membres du groupe `Community Enablement Managers` global peuvent être sélectionnés en tant que `enablement manager` pour un site communautaire spécifique.

Pour créer un utilisateur auquel le rôle de `Community Site Enablement Manager` peut être attribué, utilisez la console de sécurité de l’IU classique afin de spécifier le chemin d’accès :

Sur une instance d’auteur :

1. Connecté avec les privilèges d’administrateur, accédez à la console de sécurité de l’interface utilisateur classique.

   Par exemple, [http://localhost:4502/useradmin](http://localhost:4502/useradmin)

2. Dans le menu Edition, sélectionnez **[!UICONTROL Créer un utilisateur]**.
3. Renseignez la boîte de dialogue `Create User`.
   * Le chemin doit être `/home/users/community`.
4. Sélectionnez **[!UICONTROL Créer]**.

   ![create-community-user](assets/create-community-user.png)

* Dans le volet de gauche, recherchez l’utilisateur nouvellement créé et sélectionnez-le pour l’afficher dans le volet de droite.

   ![community-user](assets/view-community-user.png)

Dans le volet de gauche :

1. Effacez la zone de recherche et sélectionnez **[!UICONTROL Masquer les utilisateurs]**.
2. Recherchez et faites glisser `community-enablementmanagers` vers l’onglet **[!UICONTROL Groupes]** du nouvel utilisateur affiché dans le volet de droite.

   ![assign-group](assets/assign-group.png)

### Rôle Administrateurs de la communauté {#community-administrators-role}

Comme indiqué dans le graphique [Rôles du groupe d’auteurs](#author-group-roles) , les membres du groupe Administrateurs de communauté peuvent créer des sites de communauté, gérer des sites, gérer des membres (ils peuvent interdire des membres de la communauté) et modérer le contenu.

Suivez les mêmes étapes que pour créer et affecter un utilisateur au rôle de [gestionnaire d’activation](#communitysiteenablementmanagerrole), mais ajoutez le groupe c `ommunity-administrators` sous l’onglet Groupes de l’utilisateur.

### Intégration LDAP {#ldap-integration}

AEM prend en charge l’utilisation de LDAP pour l’authentification des utilisateurs et la création de comptes d’utilisateurs. Ceci est détaillé dans [Configuration de LDAP avec AEM 6](../../help/sites-administering/ldap-config.md).

Voici quelques détails de configuration spécifiques aux membres de la communauté et aux groupes de membres.

1. Configurez LDAP pour chaque instance de publication AEM.
2. [Fournisseur d’identités LDAP](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * Aucune instruction spéciale

3. [Gestionnaire de synchronisation](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * Définissez les propriétés suivantes :

      * **[!UICONTROL Appartenance automatique de l’utilisateur]** :  `community-<site name>-<uid>-members`
      * **[!UICONTROL Préfixe de chemin d’accès utilisateur]** :  `/community`
      * **[!UICONTROL Préfixe de chemin d’accès au groupe]** :  `/community`

4. [Module de connexion externe](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * pas d’instructions spéciales

Les utilisateurs sont ainsi automatiquement affectés au groupe de membres du site de la communauté et à l’emplacement du référentiel : `/home/users/community` et `/home/groups/community`, de sorte qu’ils héritent des autorisations appropriées pour afficher le profil de l’autre.

* La valeur `User auto membership` doit être la propriété `rep:authorizableId`, et non `givenName` (nom d’affichage) du profil.

## Synchronisation des utilisateurs entre les instances d’AEM {#synchronizing-users-among-aem-instances}

Lors de l’utilisation d’une [ferme de publication](topologies.md), assurez-vous que les utilisateurs ont le même chemin sur chaque instance de publication en important d’abord les utilisateurs sur une instance et en [en activant la synchronisation des utilisateurs](sync.md) pour Sling répartir les utilisateurs sur les autres instances de publication.

Si vous importez des groupes d’utilisateurs, pour vous assurer que les groupes d’utilisateurs ont le même chemin d’accès sur chaque instance de publication, importez-les dans une instance, puis [créez un package](../../help/sites-administering/package-manager.md#creating-a-new-package) pour l’exportation et installez-le sur toutes les autres instances de publication.

Bien que la synchronisation des groupes d’utilisateurs par le biais de la synchronisation des utilisateurs soit incluse dans une prochaine version, actuellement, seule la *appartenance* d’un groupe d’utilisateurs sera synchronisée lors de l’exécution de la synchronisation des utilisateurs.

## Groupes communautaires {#about-community-groups}

Lors de la discussion de groupes, il existe deux sujets distincts :

* **[Groupes communautaires](overview.md#communitygroups)**

   Les groupes communautaires sont les sous-communautés qui peuvent être créées dans l’environnement de publication d’un site communautaire qui prend en charge la création de groupes communautaires. La création d’un groupe de communautés génère davantage de pages ajoutées au site web et est gérée de la même manière que le site de leur communauté parent. Pour plus d’informations, voir [Notions fondamentales sur les groupes de communautés](essentials-groups.md) pour les développeurs et [Groupe de communautés](creating-groups.md) pour les auteurs.

* **[Groupes de membres](../../help/sites-administering/security.md)**

   Les groupes de membres sont les groupes auxquels les membres peuvent appartenir et qui sont gérés via la console Groupes . Une grande partie de la discussion sur cette page a été consacrée aux groupes de membres. Les groupes de membres créés automatiquement pour un site communautaire, précédés du préfixe *`Community`*, peuvent être considérés comme un groupe communautaire. Par conséquent, le contexte de la discussion doit être pris en compte.
