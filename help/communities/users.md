---
title: Gestion des utilisateurs et des groupes d’utilisateurs
seo-title: Gestion des utilisateurs et des groupes d’utilisateurs
description: 'Les utilisateurs des communautés AEM peuvent s’inscrire et modifier leur '
seo-description: 'Les utilisateurs des communautés AEM peuvent s’inscrire et modifier leur '
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
translation-type: tm+mt
source-git-commit: 2422ed41b18bc558f0cfc9e80f7eb6f4923aa07c

---


# Managing Users and User Groups {#managing-users-and-user-groups}

## Présentation {#overview}

Dans les communautés AEM, dans le  de publication , les utilisateurs peuvent s’inscrire eux-mêmes et modifier leur  de. Compte tenu des autorisations appropriées, ils peuvent également :

* Créez des sous-communautés dans le site de la communauté (voir Groupes [de](creating-groups.md)la communauté).

* [Modération](moderation.md) du contenu généré par l’utilisateur (UGC).

* Soyez [des contacts de ressources](resources.md) d’activation.

* Soyez [privilégié](#privileged-members-group) de créer des entrées pour les blogs, les calendriers, la qualité de vie et les forums.

Les utilisateurs enregistrés dans le  de publication  sont généralement appelés membres de la *communauté (membres)* afin de les distinguer des *utilisateurs* dans l&#39;auteur .

Les autorisations sont accordées en attribuant des membres à l’un des groupes [de](#publish-group-roles) membres (utilisateurs) créés de manière dynamique lorsque le site de la communauté est [créé](sites-console.md) ou [modifié](sites-console.md#modifying-site-properties) à partir de l’auteur  . Lorsque vous travaillez à partir de l&#39;auteur  de , les membres sont visibles à partir du de publication  au moyen du service [](#tunnel-service)tunnel.

Par conception, les membres et les groupes de membres créés dans le  de publication  ne doivent pas apparaître dans le  de de l’auteur. Les utilisateurs et les groupes d’utilisateurs créés dans le  de l’auteur   sont également destinés à rester dans le de l’auteur.

Lorsque les utilisateurs de l’auteur et des membres de la publication proviennent du même d’utilisateurs, tels que synchronisés depuis le même annuaire LDAP, ils ne sont pas considérés comme le même utilisateur avec les mêmes autorisations et le même appartenance de groupe dans l’auteur et la publication . Le(s) rôle(s) des membres et des utilisateurs doit(nt) être établi(s) séparément lors de la publication et de l&#39;auteur, selon le cas.

For a [publish farm](topologies.md), registration and modifications made on one publish instance need to be synchronized with other publish instances in order for them to have access to the same user data. Pour plus d&#39;informations, reportez-vous à la section Synchronisation [](sync.md)utilisateur, qui comprend une section décrivant [ce qui se passe...](sync.md#what-happens-when).

### Limites de contribution {#contribution-limits}

Afin de se protéger contre le spam, il est possible de limiter la fréquence de publication du contenu par les membres. En outre, il est possible de limiter automatiquement les contributions des nouveaux membres inscrits.

Pour plus d’informations, reportez-vous à la page Limites [des contributions des](limits.md)membres.

### Groupes d’utilisateurs créés dynamiquement {#dynamically-created-user-groups}

Lorsqu’un nouveau site communautaire est créé, de nouveaux groupes d’utilisateurs sont créés dynamiquement avec des identifiants uniques (uid) et des autorisations appropriées pour diverses fonctions administratives nécessaires à la gestion du site communautaire, soit dans le  de l’auteur   (voir Rôles [du groupe d’](#author-group-roles)auteurs), soit dans le de publication (voir Rôles [du groupe de](#publish-group-roles)publication).

Les noms des groupes sont générés à partir du nom donné au site pendant la création [du site](sites-console.md#step13asitetemplate)communautaire. Les identifiants uniques évitent les conflits de noms pour les sites communautaires et les groupes communautaires portant le même nom sur le même serveur.

Par exemple, si le nom du site était &quot;*engagez*&quot; pour un site intitulé &quot;We.Retail Engage&quot;, l’un des groupes d’utilisateurs créés serait :

* Communauté *Interagir* avec les membres

## Environnement de création {#author-environment}

### Service Tunnel {#tunnel-service}

Lorsque vous utilisez l’auteur   pour [créer des sites](sites-console.md), [modifier les propriétés](sites-console.md#modifying-site-properties) du site et [gérer les membres de la communauté et les groupes](members.md)de membres, il est nécessaire d’accéder aux utilisateurs et aux groupes d’utilisateurs enregistrés dans le de publication .

Le service tunnel fournit cet accès à l’aide de l’agent de réplication sur l’auteur.

* Pour plus d’informations, voir les instructions [de](deploy-communities.md#tunnel-service-on-author) configuration sur la page de déploiement.

Les consoles [Communautés, Membres et Groupes](members.md) ont pour seul but de gérer les utilisateurs (membres) et les groupes d’utilisateurs (groupes de membres) enregistrés uniquement dans le  de publication.

Pour gérer les utilisateurs et les groupes d’utilisateurs enregistrés dans l’ d’auteur , utilisez la console [de sécurité](../../help/sites-administering/security.md)

### Rôles du groupe d’auteurs {#author-group-roles}

| Si Membre du groupe... | Rôle principal |
|---|---|
| administrators | Le groupe Administrateurs se compose d’administrateurs système dotés de toutes les capacités d’un administrateur de communauté, ainsi que de la capacité de gérer le groupe Administrateurs de communauté. |
| Administrateurs de la communauté | Le groupe Administrateurs de la communauté devient automatiquement membre de tous les sites de la communauté et de tous les groupes de la communauté créés sur le site. Un membre initial du groupe Administrateurs de la communauté est le groupe Administrateurs. Dans l’ de l’auteur , les administrateurs de la communauté peuvent créer des sites communautaires, gérer des sites, gérer des membres (ils peuvent interdire les membres de la communauté) et modérer le contenu. |
| Communauté &lt;nom *du* site> Sitecontentmanager | Le Gestionnaire de contenu du site de la communauté est en mesure d’effectuer la création traditionnelle d’AEM, la création de contenu et la modification de pages pour un site de la communauté. |
| Gestionnaires d’activation de la communauté | Le groupe Gestionnaires d’activation de la communauté se compose d’utilisateurs qui peuvent être affectés à la gestion du groupe Gestionnaires d’activation d’un site de la communauté. |
| Communauté &lt;nom *du* site> Gestionnaire des abonnements au site | Le groupe Gestionnaires d&#39;activation de site de la communauté est constitué d&#39;utilisateurs qui ont été chargés de gérer les [ressources](resources.md)d&#39;activation d&#39;un site de la communauté. |
| Aucun | Un anonyme du site ne peut pas accéder à l&#39;auteur  l&#39;. |

### Administrateurs système {#system-administrators}

Les membres du groupe d’administrateurs sont des administrateurs système qui sont en mesure d’effectuer la configuration initiale d’une installation AEM pour l’auteur et la publication  .

À des fins de démonstration et de développement, le groupe d’administrateurs a un membre dont l’ID utilisateur est *admin* et le mot de passe est *admin*.

Pour les  de production , le groupe d’administrateurs par défaut doit être modifié.

Veillez à suivre la liste de contrôle [de](../../help/sites-administering/security-checklist.md)sécurité.

## Environnement de publication {#publish-environment}

### Devenir membre {#becoming-a-member}

Dans le  de publication , selon les [paramètres](sites-console.md#user-management) du site de la communauté, un de site peut devenir membre de la communauté :

* Lorsque le site communautaire est privé (fermé) :
   * Par invitation
   * Actions d’un administrateur

* Lorsque le site communautaire est public (ouvert) :
   * Par auto-inscription
   * Par connexion sociale avec Facebook et Twitter

>[!NOTE]
>
>Si un de site s&#39;inscrit en tant que membre d&#39;un site communautaire ouvert, il devient automatiquement membre d&#39;autres sites communautaires ouverts sur le même  de publication .


### Publier les rôles de groupe {#publish-group-roles}

| Si Membre du groupe... | Rôle principal |
|---|---|
| Membres de la communauté &lt;*site name*> | Un membre du site communautaire est un utilisateur enregistré. Ils peuvent se connecter, modifier leur , rejoindre un groupe communautaire ouvert, publier du contenu dans la communauté, envoyer des messages à d&#39;autres membres et suivre  du site. |
| Modérateurs de la communauté &lt;*site name*> | Un modérateur de site communautaire est un membre de la communauté de confiance qui peut modérer le contenu UGC en bloc, à l’aide de la console de modération ou dans son contexte, sur la page où le contenu est publié. |
| Communauté &lt;*site name*> &lt;*group name*> Membres | Un membre d’un groupe communautaire est un membre de la communauté qui a soit rejoint un groupe communautaire ouvert, soit été invité à un groupe communautaire fermé. Ils ont les capacités d&#39;un membre pour ce groupe communautaire au sein du site. |
| Communauté &lt;nom *du* site> Administrateurs de groupes | Un administrateur de groupe de sites communautaires est un membre de communauté de confiance qui est chargé de créer et de gérer des sous-communautés (groupes) au sein d’un site communautaire. La possibilité de fournir une modération dans le contexte est incluse. |
| *Groupe de sécurité des membres privilégiés* | Groupe d’utilisateurs créé et conservé manuellement dans le but de limiter la création de contenu. Voir Groupe [de membres](#privileged-members-group)privilégiés. |
| Aucun | Un anonyme, qui découvre le site, peut et rechercher des sites communautaires qui autorisent l&#39;accès anonyme. Pour participer et publier du contenu, l’utilisateur doit s’inscrire (s’il y a lieu) et devenir membre de la communauté. |

### Affectation de membres aux rôles de groupe de publication {#assigning-members-to-publish-group-roles}

Lors de la [création d’un site](sites-console.md) communautaire dans l’auteur  , ou lors de la [modification des propriétés du site,](sites-console.md#modifying-site-properties) les membres peuvent se voir attribuer divers rôles exécutés dans le de publication, tels que des modérateurs, des administrateurs de groupe, des contacts de ressources ou des membres privilégiés.

[L’activation du service](sync.md#accessingpublishusersfromauthor) de tunnel entraîne la présentation des choix d’affectation par les membres lors de la publication au lieu des utilisateurs lors de l’auteur.

Les membres sélectionnés seront automatiquement affectés au groupe [](#publish-group-roles) approprié et leurs membres seront inclus lorsque le site de la communauté sera (re)publié.

### Groupe de membres privilégiés {#privileged-members-group}

Le but d&#39;un groupe de sécurité des membres privilégiés est de restreindre la création de contenu pour certaines fonctions de la communauté à un sous-ensemble privilégié des membres d&#39;un site communautaire.

Le groupe des membres privilégiés est un groupe de membres créé et géré à l’aide de la console [Groupes de](members.md)communautés.

Après la création d&#39;un groupe de membres privilégiés et l&#39;activation [du service de](sync.md#accessingpublishusersfromauthor)tunnel, la structure d&#39;un site communautaire existant peut être [modifiée](sites-console.md#modify-structure) afin de modifier la configuration de ses fonctions de communauté en &quot;Autoriser les membres privilégiés&quot; et d&#39;ajouter le groupe créé.

Les fonctions communautaires qui permettent de préciser un ou plusieurs groupes de membres privilégiés sont les suivantes :

* [Fonction](functions.md#blog-function) de blog - Pour restreindre la création de nouveaux articles.
* [Fonction](functions.md#calendar-function) de calendrier - Pour restreindre la création de nouveaux  de.
* [Fonction](functions.md#forum-function) de forum - Pour restreindre la création de nouvelles rubriques.
* [Fonction](functions.md#qna-function) QnA - Pour restreindre la création de nouvelles questions.

Lorsqu’une fonction de communauté n’est pas sécurisée (aucun groupe de membres privilégiés n’est affecté), tous les membres du site de la communauté sont autorisés à créer du contenu de fonction (articles, , sujets, questions).

>[!NOTE]
>
>L’ajout d’un utilisateur à un groupe de membres privilégiés pour un site communautaire ne lui permet de créer des privilèges que s’il est également membre de ce même site.


## Création de membres de la communauté {#creating-community-members}

### Emplacement du référentiel {#repository-location}

Pour que certaines fonctionnalités fonctionnent correctement, il est nécessaire de créer des utilisateurs et des groupes d’utilisateurs avec les privilèges appropriés.

Lorsque des membres sont créés dans `/home/users/community`, ils héritent des listes de contrôle d’accès appropriées qui donnent des privilèges de lecture aux  des membres.

De même, les groupes d’utilisateurs de la communauté personnalisée (tels que les groupes de membres privilégiés) doivent être créés dans `/home/groups/community`.

L’utilisation des consoles [Communautés, Membres et Groupes](members.md) créera des utilisateurs et des groupes dans ces chemins.

Pour spécifier un chemin personnalisé, vous devez utiliser l’interface utilisateur de sécurité classique, accessible à l’adresse [https://&lt;serveur>:&lt;port>/useradmin](http://localhost:4503/useradmin).

Pour accorder des privilèges de lecture pour les chemins de membres personnalisés, sur toutes les instances de publication, définissez des listes de contrôle d’accès similaires à `/home/users/community`:

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

Pour accorder les privilèges appropriés aux chemins d’accès aux groupes de membres personnalisés, tels que /home/groups/mycompany, définissez sur toutes les instances de publication des listes de contrôle d’accès similaires à `/home/groups/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### Consoles {#consoles}

Il existe quatre consoles distinctes disponibles uniquement dans l’auteur   :

| console | Outils, sécurité, utilisateurs | Outils, sécurité, groupes | Communautés, Membres | Communautés, groupes |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| gère | utilisateurs sur l’auteur | groupes d’utilisateurs sur l’auteur | membres sur publication | groupes de membres lors de la publication |
| exige | autorisation admin | autorisation admin | autorisation d’administrateur, service de tunnel, synchronisation utilisateur pour la batterie de publication | autorisation d’administrateur, service de tunnel, synchronisation utilisateur pour la batterie de publication |

### Rôle Gestionnaire d&#39;activation de la communauté {#community-enablement-manager-role}

En règle générale, la possibilité pour un de site de s&#39;inscrire n&#39;est pas autorisée pour une communauté [d&#39;](overview.md#enablement-community) activation, car des coûts sont associés à chaque membre. Les apprenants et les ressources d’activation sont gérés par un utilisateur auquel est affecté le [rôle](#author-group-roles) de `enablement manager` pendant la création [du site sur l’auteur (ajouté en tant que membre du groupe](sites-console.md#enablement) `Community <site-name> Siteenablementmanagers`). Il `enablement manager` est également responsable de l&#39; [affectation de ressources](resources.md) d&#39;apprentissage aux membres de la communauté sur l&#39;auteur.

Seuls les utilisateurs membres du `Community Enablement Managers` groupe global peuvent être sélectionnés comme `enablement manager` pour un site communautaire spécifique.

Pour créer un utilisateur auquel le rôle de `Community Site Enablement Manager`, utilisez la console de sécurité classique de l’interface utilisateur afin de spécifier le chemin d’accès :

Sur une instance d’auteur :

1. Connecté avec des droits d’administrateur, accédez à la console de sécurité classique de l’interface utilisateur.

   For example, [http://localhost:4502/useradmin](http://localhost:4502/useradmin)

2. Dans le menu Edition, sélectionnez **[!UICONTROL Créer un utilisateur]**.
3. Renseignez la `Create User` boîte de dialogue.
   * Le chemin doit être `/home/users/community`.
4. Sélectionnez **[!UICONTROL Créer]**.

   ![chlimage_1-130](assets/chlimage_1-130.png)

* Dans le volet de gauche, recherchez l’utilisateur nouvellement créé et sélectionnez-le pour l’afficher dans le volet de droite.

   ![chlimage_1-131](assets/chlimage_1-131.png)

Dans le volet de gauche :

1. Effacez la zone de recherche et sélectionnez **[!UICONTROL Masquer les utilisateurs]**.
2. Recherchez et faites glisser `community-enablementmanagers` vers l’onglet **[!UICONTROL Groupes]** du nouvel utilisateur affiché dans le volet de droite.

   ![chlimage_1-132](assets/chlimage_1-132.png)

### Rôle Administrateurs de la communauté {#community-administrators-role}

Comme l’indique le tableau des rôles [du groupe d’](#author-group-roles) auteurs, les membres du groupe Administrateurs de la communauté peuvent créer des sites communautaires, gérer des sites, gérer des membres (ils peuvent interdire les membres de la communauté) et modérer le contenu.

Suivez les mêmes étapes que la création et l’affectation d’un utilisateur au rôle de gestionnaire [d’](#communitysiteenablementmanagerrole)activation, mais ajoutez un groupe c `ommunity-administrators` sous l’onglet Groupes de l’utilisateur.

### Intégration LDAP {#ldap-integration}

AEM prend en charge l’utilisation du protocole LDAP pour l’authentification des utilisateurs ainsi que la création de comptes d’utilisateurs. Cette opération est détaillée dans [Configuration de LDAP avec AEM 6](../../help/sites-administering/ldap-config.md).

Voici quelques détails de configuration spécifiques aux membres de la communauté et aux groupes de membres.

1. Configurez LDAP pour chaque instance de publication AEM.
2. [Fournisseur d’identité LDAP](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * Aucune instruction spéciale

3. [Gestionnaire de synchronisation](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * Définissez les propriétés suivantes :

      * **[!UICONTROL Appartenance]** automatique de l’utilisateur : `community-<site name>-<uid>-members`
      * **[!UICONTROL Préfixe]** de chemin d’accès utilisateur : `/community`
      * **[!UICONTROL Préfixe]** du chemin du groupe : `/community`

4. [Module de connexion externe](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * aucune instruction spéciale

Les utilisateurs sont alors automatiquement affectés au groupe des membres du site de la communauté et à l’emplacement du référentiel `/home/users/community` et `/home/groups/community`, de sorte qu’ils héritent des autorisations appropriées pour voir les  des autres.

* La `User auto membership` valeur doit être la `rep:authorizableId` propriété, et non le `givenName` (nom d’affichage) du.

## Synchronisation des utilisateurs parmi les instances AEM {#synchronizing-users-among-aem-instances}

Lors de l’utilisation d’une batterie de [publication](topologies.md), assurez-vous que les utilisateurs disposent du même chemin sur chaque instance de publication en important d’abord les utilisateurs sur une instance et en [activant la synchronisation](sync.md) utilisateur avec Sling pour répartir les utilisateurs sur les autres instances de publication.

Si vous importez des groupes d’utilisateurs, pour vous assurer que les groupes d’utilisateurs disposent du même chemin sur chaque instance de publication, importez-les dans une instance, puis [créez un package](../../help/sites-administering/package-manager.md#creating-a-new-package) pour l’exportation et installez-le sur toutes les autres instances de publication.

Bien que la synchronisation des groupes d’utilisateurs par le biais de la synchronisation des utilisateurs soit incluse dans une prochaine version, actuellement, seuls les *membres* d’un groupe d’utilisateurs sont synchronisés lors de l’exécution de la synchronisation des utilisateurs.

## A propos des groupes de communautés {#about-community-groups}

Lors de la discussion de groupes, il y a deux sujets distincts :

* **[Groupes communautaires](overview.md#communitygroups)**

   Les groupes communautaires sont les sous-communautés qui peuvent être créées dans le de publication  pour un site communautaire qui soutient la création de groupes communautaires. La création d&#39;un groupe communautaire entraîne l&#39;ajout de plus de pages au site Web et est gérée de la même manière que le site de la communauté parent. Pour plus d&#39;informations, visitez [Community Group Essentials](essentials-groups.md) pour les développeurs et [Community Group](creating-groups.md) pour les auteurs.

* **[Groupes de membres](../../help/sites-administering/security.md)**

   Les groupes de membres sont les groupes auxquels les membres peuvent appartenir et qui sont gérés via la console Groupes. Une grande partie de la discussion sur cette page a été consacrée aux groupes de membres. Les groupes de membres créés automatiquement pour un site communautaire, avec un préfixe *`Community`*, peuvent être appelés un groupe communautaire, de sorte que le contexte de la discussion doit être pris en considération.
