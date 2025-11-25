---
title: Groupes d’utilisateurs fermés dans AEM
description: Découvrez les groupes fermés d’utilisateurs et d’utilisatrices et les avantages qu’ils apportent en termes d’évolutivité et de sécurité dans AEM.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 39e35a07-140f-4853-8f0d-8275bce27a65
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '6654'
ht-degree: 97%

---

# Groupes d’utilisateurs fermés dans AEM{#closed-user-groups-in-aem}

## Présentation {#introduction}

Depuis AEM 6.3, une nouvelle mise en œuvre des groupes fermés d’utilisateurs et d’utilisatrices est disponible pour résoudre les problèmes de performances, d’évolutivité et de sécurité liés à la mise en œuvre existante.

>[!NOTE]
>
>Par souci de simplicité, l’abréviation CUG (Closed User Group) sera utilisée dans cette documentation pour se référer aux groupes fermés d’utilisateurs et d’utilisatrices.

Cette nouvelle mise en œuvre a pour objectif de couvrir les fonctionnalités existantes en fonction des besoins, tout en résolvant les problèmes et les limites de conception des versions antérieures. Le résultat est une nouvelle conception de CUG avec les caractéristiques suivantes :

* Séparation claire des éléments d’authentification et d’autorisation, qui peuvent être utilisés individuellement ou combinés ;
* Modèle d’autorisation dédié pour refléter l’accès en lecture restreint aux arborescences de CUG configurées sans interférer avec d’autres exigences de configuration et d’autorisation du contrôle d’accès ;
* Séparation entre la configuration de contrôle de l’accès en lecture restreint, qui est nécessaire généralement sur les instances de création, et évaluation des permissions, qui n’est généralement souhaitée que sur l’instance de publication ;
* Modification d’un accès en lecture limité sans transmission de privilèges ;
* Extension de type de nœud dédiée pour signaler l’exigence d’authentification ;
* Chemin de connexion facultatif associé à l’exigence d’authentification.

### Nouvelle mise en œuvre d’un groupe personnalisé d’utilisateurs et d’utilisatrices {#the-new-custom-user-group-implementation}

Un CUG, dans le contexte d’AEM, comprend les étapes suivantes :

* Restreindre l’accès en lecture sur l’arborescence qui doit être protégée et uniquement autoriser la lecture pour les principaux qui sont soit répertoriés avec une instance de données CUG spécifique, soit exclus de l’évaluation des CUG. Il s’agit de l’élément d’**autorisation**.
* Renforcer l’authentification sur une arborescence donnée et spécifier éventuellement une page de connexion dédiée pour cette arborescence qui est ensuite exclue. Il s’agit de l’élément d’**authentification**.

La nouvelle mise en œuvre a été conçue pour distinguer les éléments d’authentification des éléments d’autorisation. Depuis AEM 6.3, il est possible de restreindre l’accès en lecture sans ajouter explicitement une exigence d’authentification. Par exemple, si une instance donnée nécessite une authentification complète ou si une arborescence donnée réside déjà dans une sous-arborescence qui nécessite déjà une authentification.

Aussi, une arborescence donnée peut être marquée par une exigence d’authentification sans modifier la configuration de permission effective. Les combinaisons et les résultats sont répertoriés dans la section [Combiner des politiques CUG et l’exigence d’authentification](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement).

## Vue d’ensemble {#overview}

### Autorisation : limiter l’accès en lecture {#authorization-restricting-read-access}

La fonctionnalité clé d’un CUG est de restreindre l’accès en lecture sur une arborescence donnée dans le référentiel de contenu pour tous à l’exception des principaux sélectionnés. Au lieu de manipuler à la volée le contenu du contrôle d’accès par défaut, la nouvelle mise en œuvre adopte une approche différente en définissant un type dédié de politique de contrôle d’accès qui représente un CUG.

#### Politique de contrôle d’accès pour les CUG {#access-control-policy-for-cug}

Ce nouveau type de politique présente les caractéristiques suivantes :

* Politique de contrôle d’accès de org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy (définie par l’API Apache Jackrabbit)
* PrincipalSetPolicy accorde des privilèges à un ensemble modifiable d’entités de sécurité
* Les privilèges accordés et la portée de la politique constituent des détails de la mise en œuvre.

La mise en œuvre de PrincipalSetPolicy utilisée pour représenter les CUG définit en outre les points suivants :

* les politiques CUG accordent uniquement l’accès en lecture aux éléments JCR standard (par exemple, le contenu du contrôle d’accès est exclu) ;
* la portée est définie par le nœud à accès contrôlé qui détient la politique du CUG ;
* les politiques CUG peuvent être imbriquées, un CUG imbriqué démarre un nouveau CUG sans hériter de l’ensemble principal du CUG « parent » ;
* L’effet de la politique, si l’évaluation est activée, est hérité vers l’ensemble de la sous-arborescence jusqu’au CUG imbriqué suivant.

Ces politiques de CUG sont déployées sur les instances AEM par l’intermédiaire d’un module d’autorisation distinct appelé oak-authorization-cug. Ce module est fourni avec ses propres fonctions d’évaluation des permissions et de gestion du contrôle d’accès. En d’autres termes, la configuration par défaut d’AEM est livrée avec une configuration de référentiel de contenu Oak qui combine plusieurs mécanismes d’autorisation. Pour plus d’informations, consultez [cette page sur la documentation Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html).

Dans cette configuration composite, un nouveau CUG ne remplace pas le contenu de contrôle d’accès existant associé au nœud cible. Il s’agit plutôt d’un supplément qui peut également être supprimé ultérieurement sans affecter le contrôle d’accès d’origine, qui par défaut dans AEM serait une liste de contrôle d’accès.

Contrairement à la mise en œuvre précédente, les nouvelles politiques de CUG sont systématiquement reconnues et traitées comme contenu de contrôle d’accès. Cela signifie qu’elles sont créées et modifiées à l’aide de l’API de gestion du contrôle d’accès JCR. Pour plus d’informations, consultez [Gestion des politiques de CUG](#managing-cug-policies).

#### Évaluation des autorisations des politiques CUG {#permission-evaluation-of-cug-policies}

Outre la gestion de contrôle d’accès dédiée pour les CUG, le nouveau modèle d’autorisation vous permet d’activer de manière conditionnelle l’évaluation des permissions pour ses politiques. Cela vous permet de configurer des politiques de CUG dans un environnement d’évaluation et d’activer uniquement l’évaluation des autorisations effectives une fois répliquées dans l’environnement de production.

L’évaluation des autorisations pour les politiques de CUG et l’interaction avec le modèle d’autorisation par défaut ou tout autre modèle d’autorisation suivent le modèle conçu pour plusieurs mécanismes d’autorisation dans Apache Jackrabbit Oak. En d’autres termes, un ensemble donné d’autorisations est accordé si et uniquement si tous les modèles accordent l’accès. Pour plus d’informations, consultez la [documentation de Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html).

Les caractéristiques suivantes s’appliquent à l’évaluation des autorisations associée au modèle d’autorisation conçu pour gérer et évaluer les politiques CUG :

* Seules les autorisations de lecture pour les nœuds et propriétés normaux sont gérés, mais pas la lecture du contenu de contrôle d’accès.
* Il ne prend pas en charge les autorisations d’écriture ni aucun type d’autorisation requis pour la modification du contenu JCR protégé (contrôle d’accès, informations de type de nœud, contrôle de version, verrouillage ou gestion des utilisateurs et utilisatrices, entre autres). Ces autorisations ne sont pas affectées par une politique de CUG et ne seront pas évaluées par le modèle d’autorisation associé. Ces autorisations sont accordées en fonction des autres modèles configurés dans la configuration de sécurité.

L’effet d’une politique de CUG unique sur l’évaluation des permissions peut être résumé comme suit :

* L’accès en lecture est refusé pour tous, à l’exception des sujets contenant des entités de sécurité exclues ou des entités de sécurité répertoriées dans la stratégie.
* La politique prend effet sur le nœud dont l’accès est contrôlé et qui contient la politique et ses propriétés.
* L’effet est également hérité dans la hiérarchie, c’est-à-dire l’arborescence d’éléments définie par le nœud dont l’accès est contrôlé.
* Toutefois, elle n’affecte pas les frères ni les ancêtres du nœud dont l’accès est contrôlé.
* L’héritage d’un CUG donné s’arrête à un CUG imbriqué.

#### Bonnes pratiques {#best-practices}

Les bonnes pratiques suivantes doivent être prises en compte pour définir un accès en lecture limité via les CUG :

* Déterminez si le CUG dont vous avez besoin est destiné à limiter l’accès en lecture ou s’il correspond à une exigence d’authentification. Dans ce dernier cas, ou si les deux sont nécessaires, consultez la section consacrée aux bonnes pratiques pour plus de détails sur l’exigence d’authentification.
* Créez un modèle de menace pour les données ou le contenu qui doivent être protégés afin d’identifier les limites des menaces et d’avoir une idée claire de la sensibilité des données et des rôles associés à l’accès autorisé.
* Modélisez le contenu du référentiel et les CUG en gardant à l’esprit les aspects généraux liés aux autorisations et les bonnes pratiques :

   * N’oubliez pas que l’autorisation de lecture ne sera accordée que si un CUG donné et l’évaluation des autres modules déployés dans la configuration permettent à un sujet donné de lire un élément donné du référentiel.
   * Évitez de créer des CUG redondants où l’accès en lecture est déjà restreint par d’autres modules d’autorisation.
   * Le besoin excessif de CUG imbriqués peut potentiellement mettre en évidence des problèmes dans la conception du contenu.
   * Un besoin excessif de CUG (par exemple, sur chaque page) peut indiquer la nécessité d’un modèle d’autorisation personnalisé potentiellement mieux adapté aux besoins de sécurité spécifiques de l’application et du contenu en question.

* Limitez les chemins pris en charge pour les politiques de CUG à un petit nombre d’arborescences dans le référentiel afin d’optimiser les performances. Par exemple, autorisez uniquement les CUG sous le nœud /content tel qu’établi par défaut depuis AEM 6.3.
* Les politiques de CUG sont conçues pour autoriser l’accès en lecture à un petit ensemble d’entités de sécurité. La nécessité d’un grand nombre d’entités peut mettre en évidence des problèmes liés à la conception du contenu ou de l’application et devrait être reconsidérée.

### Authentification : définir les exigences d’authentification {#authentication-defining-the-auth-requirement}

Les composants liés à l’authentification de la fonction CUG vous permettent de marquer les arborescences nécessitant une authentification et éventuellement de spécifier une page de connexion dédiée. Conformément à la version précédente, la nouvelle mise en œuvre vous permet de marquer les arborescences nécessitant une authentification dans le référentiel de contenu. Elle active également de manière conditionnelle la synchronisation avec l’événement `Sling org.apache.sling.api.auth.Authenticator` responsable de l’application finale de l’exigence et de la redirection vers une ressource de connexion.

Ces exigences sont enregistrées auprès d’Authenticator au moyen d’un service OSGi qui fournit la propriété d’enregistrement `sling.auth.requirements`. Ces propriétés sont ensuite utilisées pour étendre les exigences d’authentification de façon dynamique. Pour plus d’informations, voir la [documentation Sling](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS).

#### Définir les exigences d’authentification avec un type de mixin dédié {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

Pour des raisons de sécurité, la nouvelle mise en œuvre remplace l’utilisation d’une propriété JCR résiduelle par un type de mixin dédié appelé `granite:AuthenticationRequired`, qui définit une propriété facultative unique de type CHAÎNE pour le chemin de connexion `granite:loginPath`. Seules les modifications du contenu liées à ce type de mixin entraînent la mise à jour des exigences enregistrées auprès d’Apache Sling Authenticator. Les modifications sont suivies lors de la persistance de toute modification provisoire et nécessitent donc un appel `javax.jcr.Session.save()` pour prendre effet.

Il en va de même pour la propriété `granite:loginPath`. Elle n’est respectée que si elle est définie par le type de mixin lié à l’exigence d’authentification. L’ajout d’une propriété résiduelle du même nom au niveau d’un nœud JCR non structuré ne produit pas l’effet souhaité et la propriété est ignorée par le gestionnaire responsable de la mise à jour de l’enregistrement OSGi.

>[!NOTE]
>
>La définition de la propriété de chemin de connexion est facultative et elle est uniquement nécessaire si l’arborescence nécessitant une authentification ne peut se replier sur la page de connexion par défaut ou héritée. Voir l’[Évaluation du chemin de connexion](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path) ci-dessous.

#### Enregistrer l’exigence d’authentification et le chemin de connexion avec Sling Authenticator {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

Puisqu’il est prévu que ce type d’exigence d’authentification soit limité à certains modes d’exécution et à un petit sous-ensemble d’arborescences dans le référentiel de contenu, le suivi du type de mixin de l’exigence et des propriétés de chemin de connexion est conditionnel. De plus, il est lié à une configuration correspondante qui définit les chemins pris en charge (voir Options de configuration ci-dessous). Par conséquent, seules les modifications dans la portée de ces chemins pris en charge déclenchent une mise à jour de l’enregistrement OSGi ; dans les autres cas, le type de mixin et la propriété sont tous deux ignorés.

Par défaut, AEM utilise désormais cette configuration en permettant de placer le mixin en mode d’exécution de création, mais en ne le faisant prendre effet que lors de la réplication vers l’instance de publication. Pour plus d’informations sur la manière dont Sling applique les exigences d’authentification, consultez la documentation [Authentification Sling : framework](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html).

L’ajout du type de mixin `granite:AuthenticationRequired` au sein des chemins pris en charge configurés entraîne la mise à jour de l’enregistrement dans OSGi du gestionnaire responsable avec une nouvelle entrée contenant la propriété `sling.auth.requirements`. Si une exigence d’authentification donnée spécifie la propriété facultative `granite:loginPath`, la valeur est en outre enregistrée auprès d’Authenticator avec un préfixe « - » afin de pouvoir être exclue de l’exigence d’authentification.

#### Évaluation et héritage de l’exigence d’authentification {#evaluation-and-inheritance-of-the-authentication-requirement}

Les exigences d’authentification d’Apache Sling sont héritées dans la hiérarchie de page ou de nœud. Les détails même de l’héritage et l’évaluation des exigences d’authentification telles que l’ordre et la priorité considérés comme des détails d’implémentation et ne seront pas documentés dans cet article.

#### Évaluer un chemin de connexion {#evaluation-of-login-path}

L’évaluation du chemin de connexion et de la redirection vers la ressource correspondante lors de l’authentification est actuellement un détail de mise en œuvre du gestionnaire d’authentification du sélecteur de connexion Adobe Granite (`com.day.cq.auth.impl.LoginSelectorHandler`), qui est un gestionnaire d’authentification Apache Sling configuré avec AEM par défaut.

En appelant `AuthenticationHandler.requestCredentials`, ce gestionnaire tente de déterminer la page de connexion de mise en correspondance vers laquelle la personne est redirigée. Cela inclut les étapes suivantes :

* Faites la distinction entre un mot de passe expiré et la nécessité de vous connecter régulièrement comme raison de la redirection ;
* S’il s’agit d’une connexion régulière, teste si un chemin de connexion peut être obtenu dans l’ordre suivant :

   * À partir du LoginPathProvider mis en œuvre par le nouveau `com.adobe.granite.auth.requirement.impl.RequirementService`
   * À partir de l’ancienne mise en œuvre CUG obsolète
   * À partir des mises en correspondance de page de connexion, telles que définies avec `LoginSelectorHandler`
   * Enfin, le retour vers la page de connexion par défaut, telle qu’elle est définie avec `LoginSelectorHandler`.

* Dès qu’un chemin de connexion valide est obtenu par les appels répertoriés ci-dessus, la requête de la personne est redirigée vers cette page.

Cette documentation traite de l’évaluation du chemin de connexion tel qu’il est exposé par l’interface `LoginPathProvider` interne. L’implémentation livrée depuis AEM 6.3 se comporte comme suit :

* L’enregistrement des chemins de connexion dépend de la distinction entre le mot de passe expiré et la nécessité d’une connexion régulière comme raison de la redirection.
* En cas de connexion régulière, teste si un chemin de connexion peut être obtenu dans l’ordre suivant :

   * À partir du `LoginPathProvider` mis en œuvre par le nouveau `com.adobe.granite.auth.requirement.impl.RequirementService`
   * À partir de l’ancienne mise en œuvre CUG obsolète
   * À partir des mises en correspondance de page de connexion, telles que définies avec `LoginSelectorHandler`
   * Enfin, le retour vers la page de connexion par défaut, telle qu’elle est définie avec `LoginSelectorHandler`.

* Dès qu’un chemin de connexion valide est obtenu par les appels répertoriés ci-dessus, la requête de la personne est redirigée vers cette page.

Le `LoginPathProvider`, tel qu’il est mis en œuvre par la nouvelle prise en charge d’exigence d’authentification dans Granite, expose les chemins de connexion Granite tels que définis par les propriétés `granite:loginPath`, qui à leur tour sont définis par le type de mixin comme décrit ci-dessus. Le mappage du chemin de ressource contenant le chemin de connexion et la valeur de la propriété elle-même est conservé en mémoire et sera évalué pour trouver un chemin de connexion approprié pour les autres nœuds de la hiérarchie.

>[!NOTE]
>
>L’évaluation est effectuée uniquement pour les requêtes liées aux ressources qui se trouvent dans les chemins pris en charge configurés. Pour toute autre requête, les méthodes alternatives de détermination du chemin de connexion seront évaluées.

#### Bonnes pratiques {#best-practices-1}

Les bonnes pratiques suivantes doivent être prises en compte lors de la définition des exigences d’authentification :

* Il est préférable de ne pas imbriquer les exigences d’authentification : le fait de placer un marqueur d’exigence d’authentification unique au début d’une arborescence devrait suffire et être hérité par toute la sous-arborescence définie par le nœud cible. Toute exigence supplémentaire d’authentification dans cette arborescence doit être considérée comme redondante et peut entraîner des problèmes de performances lors de l’évaluation de l’exigence d’authentification dans Apache Sling. Grâce à la séparation des zones CUG liées à l’autorisation et à l’authentification, il est possible de restreindre l’accès en lecture au moyen de CUG ou d’autres types de politiques, tout en appliquant en même temps l’authentification pour l’ensemble de l’arborescence.
* Modélisez le contenu de référentiel, de telle façon que les exigences d’authentification s’appliquent à l’arborescence entière sans avoir à exclure à nouveau de l’exigence les sous-arborescences imbriquées.
* Pour éviter de spécifier et d’enregistrer ensuite des chemins de connexion redondants :

   * Utilisez l’héritage et évitez de définir des chemins de connexion imbriqués.
   * Ne définissez pas le chemin de connexion facultatif sur une valeur qui correspond à la valeur par défaut ou à la valeur héritée.
   * Les développeurs d’applications doivent identifier les mises en correspondance de connexion qui doivent être configurées dans les fonctions de chemin de connexion globales (par défaut et mise en correspondance) associées à `LoginSelectorHandler`.

## Représentation dans le référentiel {#representation-in-the-repository}

### Représentation de la politique CUG dans le référentiel {#cug-policy-representation-in-the-repository}

La documentation Oak couvre la façon dont les nouvelles politiques de CUG sont reflétées dans le contenu du référentiel. Pour plus d’informations, consultez la [documentation Jackrabbit Oak sur la gestion de l’accès avec les CUG](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository).

### Exigences d’authentification dans le référentiel {#authentication-requirement-in-the-repository}

Le besoin d’une exigence d’authentification distincte est reflété dans le contenu du référentiel avec un type de nœud mixin dédié placé au niveau du nœud cible. Le type mixin définit une propriété facultative pour spécifier une page de connexion dédiée pour l’arborescence définie par le nœud cible.

La page associée au chemin de connexion peut être placée à l’intérieur ou à l’extérieur de cette arborescence. Elle sera exclue des exigences d’authentification.

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## Gérer les politiques CUG et les exigences d’authentification {#managing-cug-policies-and-authentication-requirement}

### Gérer les politiques CUG {#managing-cug-policies}

Le nouveau type de politiques de contrôle d’accès destiné à limiter l’accès en lecture pour un CUG est géré à l’aide de l’API de gestion du contrôle d’accès JCR et suit les mécanismes décrits par la [Spécification JCR 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html).

#### Définir une nouvelle politique CUG {#set-a-new-cug-policy}

Code pour appliquer une nouvelle politique de CUG à un nœud qui n’avait pas de CUG. Veuillez noter que `getApplicablePolicies` renvoie uniquement les nouvelles politiques qui n’ont pas encore été définies. En fin de compte, la politique nécessite d’être réécrite et les modifications doivent être conservées.

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

AccessControlPolicyIterator it = acMgr.getApplicablePolicies(path);
while (it.hasNext()) {
        AccessControlPolicy policy = it.nextAccessControlPolicy();
        if (policy instanceof PrincipalSetPolicy) {
           cugPolicy = (PrincipalSetPolicy) policy;
           break;
        }
}

if (cugPolicy == null) {
   log.debug("no applicable policy"); // path not supported or no applicable policy (for example,
                                                   // the policy was set before)
   return;
}

cugPolicy.addPrincipals(toAdd1, toAdd2);
cugPolicy.removePrincipals(toRemove));

acMgr.setPolicy(path, cugPolicy); // as of this step the policy can be edited/removed
session.save();
```

#### Modifier une politique CUG existante {#edit-an-existing-cug-policy}

Les étapes suivantes sont nécessaires pour modifier une politique de CUG existante. La politique modifiée nécessite d’être réécrite, et les modifications doivent être conservées à l’aide de `javax.jcr.Session.save()`.

```java
String path = [...] // needs to be a supported, absolute path

Principal toAdd1 = [...]
Principal toAdd2 = [...]
Principal toRemove = [...]

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
     if (policy instanceof PrincipalSetPolicy) {
        cugPolicy = (PrincipalSetPolicy) policy;
        break;
     }
}

if (cugPolicy == null) {
   log.debug("no policy to edit"); // path not supported or policy not set before
   return;
}

if (cugPolicy.addPrincipals(toAdd1, toAdd2) || cugPolicy.removePrincipals(toRemove)) {
   acMgr.setPolicy(path, cugPolicy);
   session.save();
} else {
     log.debug("cug policy not modified");
}
```

### Récupérer des politiques de CUG efficaces {#retrieve-effective-cug-policies}

La gestion du contrôle d’accès JCR définit une méthode du meilleur effort pour récupérer les politiques qui prennent effet à un chemin donné. Étant donné que l’évaluation des politiques de CUG est conditionnelle et dépend de la configuration correspondante à activer, l’appel de `getEffectivePolicies` est un moyen pratique pour vérifier si une politique de CUG donnée prend effet dans une configuration spécifique.

>[!NOTE]
>
>La différence entre `getEffectivePolicies` et l’exemple de code suivant qui remonte la hiérarchie pour déterminer si un chemin donné fait déjà partie d’un CUG existant.

```java
String path = [...] // needs to be a supported, absolute path

AccessControlManager acMgr = session.getAccessControlManager();
PrincipalSetPolicy cugPolicy = null;

// log an debug message of all CUG policies that take effect at the given path
// there could be zero, one or many (creating nested CUGs is possible)
for (AccessControlPolicy policy : acMgr.getEffectivePolicies(path) {
     if (policy instanceof PrincipalSetPolicy) {
        String policyPath = "-";
        if (policy instanceof JackrabbitAccessControlPolicy) {
           policyPath = ((JackrabbitAccessControlPolicy) policy).getPath();
        }
        log.debug("Found effective CUG for path '{}' at '{}', path, policyPath);
     }
}
```

#### Récupérer les politiques CUG héritées {#retrieve-inherited-cug-policies}

Recherche de tous les CUG imbriqués qui ont été définis à un chemin donné, qu’ils soient ou non effectifs. Pour plus d’informations, consultez la section [Options de configuration](/help/sites-administering/closed-user-groups.md#configuration-options).

```java
String path = [...]

List<AccessControlPolicy> cugPolicies = new ArrayList<AccessControlPolicy>();
while (isSupportedPath(path)) {
     for (AccessControlPolicy policy : acMgr.getPolicies(path)) {
         if (policy instanceof PrincipalSetPolicy) {
            cugPolicies.add(policy);
         }
      }
      path = (PathUtils.denotesRoot(path)) ? null : PathUtils.getAncestorPath(path, 1);
}
```

#### Gérer les politiques CUG par principal {#managing-cug-policies-by-pincipal}

Les extensions définies par `JackrabbitAccessControlManager` qui permettent la modification des politiques de contrôle d’accès par un principal ne sont pas mises en œuvre avec la gestion de contrôle d’accès CUG, comme par définition une politique de CUG affecte toujours tous les principaux : ceux répertoriés avec `PrincipalSetPolicy` se voient attribuer une autorisation d’accès en lecture, alors que tous les autres principaux ne peuvent pas lire le contenu dans l’arborescence définie par le nœud cible.

Les méthodes correspondantes renvoient toujours un tableau de politiques vide mais n’entraîneront pas d’exceptions.

### Gérer les exigences d’authentification {#managing-the-authentication-requirement}

La création, la modification ou la suppression de nouvelles exigences d’authentification s’effectuent en modifiant le type de nœud effectif du nœud cible. La propriété de chemin de connexion facultatif peut ensuite être écrite à l’aide de l’API JCR.

>[!NOTE]
>
>Les modifications apportées à un nœud cible donné mentionné ci-dessus ne sont répercutées sur l’authentificateur Apache Sling que si `RequirementHandler` a été configuré et que la cible figure dans les arborescences définies par les chemins pris en charge (voir la section Options de configuration).
>
>Pour plus d’informations, consultez [Attribution de types de nœuds mixin] (https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3 Assigning Mixin Node Types) et [Ajout de nœuds et définition de propriétés] (https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4 Ajout de nœuds et définition de propriétés).

#### Ajouter une nouvelle exigence d’authentification {#adding-a-new-auth-requirement}

Les étapes de création d’une exigence d’authentification sont détaillées ci-dessous. L’exigence n’est enregistrée auprès de l’authentificateur Apache Sling que si `RequirementHandler` a été configuré pour l’arborescence contenant le nœud cible.

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### Ajouter une nouvelle exigence d’authentification avec un chemin de connexion {#add-a-new-auth-requirement-with-login-path}

Procédure à suivre pour créer une exigence d’authentification incluant un chemin de connexion. Notez que cette exigence et l’exclusion du chemin de connexion ne sont enregistrées auprès d’Apache Sling Authenticator que si `RequirementHandler` a été configuré pour l’arborescence contenant le nœud cible.

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### Modifier un chemin de connexion existant {#modify-an-existing-login-path}

Les étapes à suivre pour modifier un chemin de connexion existant sont détaillées ci-dessous. L’a modification n’est enregistrée auprès d’Apache Sling Authenticator que si `RequirementHandler` a été configuré pour l’arborescence contenant le nœud cible. La valeur précédente de chemin de connexion est supprimée de l’enregistrement. L’exigence d’authentification associée au nœud cible n’est pas affectée par cette modification.

```java
Node targetNode = [...]
String newLoginPath = [...] // STRING property

if (targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", newLoginPath);
   session.save();
} else {
     log.debug("cannot modify login path property; mixin type missing");
}
```

#### Supprimer un chemin de connexion existant {#remove-an-existing-login-path}

Procédure pour supprimer un chemin de connexion existant. L’annulation de l’enregistrement de l’entrée de chemin de connexion auprès de l’authentificateur Apache Sling n’est effective que si `RequirementHandler` a été configuré pour l’arborescence contenant le nœud cible. L’exigence d’authentification associée au nœud cible n’est pas affectée.

```java
Node targetNode = [...]

if (targetNode.hasProperty("granite:loginPath") &&
   targetNode.isNodeType("granite:AuthenticationRequired")) {
   targetNode.setProperty("granite:loginPath", null);
   session.save();
} else {
     log.debug("cannot remove login path property; mixin type missing");
}
```

Vous pouvez également utiliser la méthode ci-dessous pour atteindre le même objectif :

```java
String path = [...] // absolute path to target node

String propertyPath = PathUtils.concat(path, "granite:loginPath");
if (session.propertyExists(propertyPath)) {
    session.getProperty(propertyPath).remove();
    // or: session.removeItem(propertyPath);
    session.save();
}
```

#### Supprimer une exigence d’authentification {#remove-an-auth-requirement}

Procédure pour supprimer une exigence d’authentification existante. L’annulation de l’enregistrement de l’exigence auprès de l’authentificateur Apache Sling n’est effective que si `RequirementHandler` a été configuré pour l’arborescence contenant le nœud cible.

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### Récupération des exigences d’authentification effectives {#retrieve-effective-auth-requirements}

Il n’existe aucune API publique dédiée pour lire toutes les exigences d’authentification effectives enregistrées auprès de l’authentificateur Apache Sling. Toutefois, la liste est exposée dans la console système à l’adresse `https://<serveraddress>:<serverport>/system/console/slingauth` dans la section « **Configuration des exigences d’authentification** ».

L’image suivante illustre les exigences d’authentification d’une instance de publication AEM avec du contenu de démonstration. Le chemin en surbrillance de la page de communauté illustre comment une exigence ajoutée par l’implémentation décrite dans ce document est reflétée dans l’authentificateur Apache Sling.

>[!NOTE]
>
>Dans cet exemple, la propriété de chemin de connexion facultatif n’a pas été définie. Par conséquent, aucune deuxième entrée n’a été enregistrée auprès de l’authentificateur.

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### Récupération du chemin de connexion effectif {#retrieve-the-effective-login-path}

Il n’existe actuellement aucune API publique pour récupérer le chemin de connexion qui prend effet lors d’un accès anonyme à une ressource nécessitant une authentification. Consultez la section Évaluation du chemin de connexion pour plus de détails d’implémentation sur la récupération du chemin de connexion.

Notez cependant qu’outre les chemins de connexion définis avec cette fonctionnalité, il existe d’autres moyens de spécifier la redirection vers la connexion, qui doivent être pris en compte lors de la conception du modèle de contenu et des exigences d’authentification d’une installation AEM donnée.

#### Récupérer l’exigence d’authentification héritée {#retrieve-the-inherited-auth-requirement}

Comme pour le chemin de connexion, il n’existe aucune API publique pour récupérer les exigences d’authentification héritées définies dans le contenu. L’exemple suivant illustre comment répertorier toutes les exigences d’authentification qui ont été définies avec une hiérarchie donnée, qu’elles prennent ou non effet. Pour plus d’informations, consultez [Options de configuration](/help/sites-administering/closed-user-groups.md#configuration-options).

>[!NOTE]
>
>Il est recommandé d’utiliser le mécanisme d’héritage à la fois pour les exigences d’authentification et le chemin de connexion, et d’éviter la création d’exigences d’authentification imbriquées.
>
>Pour plus d’informations, consultez [Évaluation et héritage de l’exigence d’authentification](#evaluation-and-inheritance-of-the-authentication-requirement), [Évaluation du chemin de connexion](#evaluation-of-login-path) et [Bonnes pratiques](#best-practices).

```java
String path = [...]
Node node = session.getNode(path);

Map<String, String> authRequirements = new ArrayList<String, String>();
while (isSupported(node)) {
     if (node.isNodeType("granite:AuthenticationRequired")) {
         String loginPath = (node.hasProperty("granite:loginPath") ?
                                     node.getProperty("granite:loginPath").getString() :
                                     "";
        authRequirements.put(node.getPath(), loginPath);
        node = node.getParent();
     }
}
```

### Combinaison des politiques CUG et de l’exigence d’authentification {#combining-cug-policies-and-the-authentication-requirement}

Le tableau suivant répertorie les combinaisons valides de politiques CUG et les exigences d’authentification d’une instance AEM dont les deux modules sont activés via la configuration.

| **Exigence d’authentification** | **Chemin de connexion** | **Accès en lecture limité** | **Effet attendu** |
|---|---|---|---|
| Oui | Oui | Oui | Un utilisateur donné ne pourra afficher la sous-arborescence marquée par la politique de CUG que si l’évaluation des permissions effective accorde l’accès. Les utilisateurs et les utilisatrices non authentifiés sont redirigés vers la page de connexion spécifiée. |
| Oui | Non | Oui | Un utilisateur donné ne pourra afficher la sous-arborescence marquée par la politique de CUG que si l’évaluation des permissions effective accorde l’accès. Les utilisateurs et les utilisatrices non authentifiés sont redirigés vers la page de connexion par défaut héritée. |
| Oui | Oui | Non | Les utilisateurs et les utilisatrices non authentifiés sont redirigés vers la page de connexion spécifiée. L’autorisation d’affichage de l’arborescence marquée par l’exigence d’authentification dépend des autorisations en vigueur des éléments individuels contenus dans cette sous-arborescence. Aucun CUG dédié limitant l’accès en lecture n’est en place. |
| Oui | Non | Non | Les utilisateurs et les utilisatrices non authentifiés sont redirigés vers la page de connexion par défaut héritée. L’autorisation d’affichage de l’arborescence marquée par l’exigence d’authentification dépend des autorisations en vigueur des éléments individuels contenus dans cette sous-arborescence. Aucun CUG dédié limitant l’accès en lecture n’est en place. |
| Non | Non | Oui | Une personne donnée, qu’elle soit authentifiée ou non, ne pourra afficher la sous-arborescence marquée par la politique de CUG que si l’évaluation des permissions effective accorde l’accès. Les utilisateurs et les utilisatrices non authentifiés sont traités de la même manière et ne sont pas redirigés vers la page de connexion. |

>[!NOTE]
>
>La combinaison Exigence d’authentification = oui et Chemin de connexion = oui ne figure pas ci-dessus, car le chemin de connexion est un attribut facultatif associé à une exigence d’authentification. La spécification d’une propriété JCR avec ce nom, sans ajouter le type de mixin de définition, n’a aucun effet et est ignorée par le gestionnaire correspondant.

## Composants et configuration OSGi {#osgi-components-and-configuration}

Cette section donne une vue d’ensemble des composants OSGi et de chaque option de configuration introduite avec la nouvelle mise en œuvre de CUG.

Consultez également la documentation relative à la mise en correspondance de CUG pour une mise en correspondance complète des options de configuration entre l’ancienne et la nouvelle mise en œuvre.

### Autorisation : installation et configuration {#authorization-setup-and-configuration}

Les nouveaux composants liés à l’autorisation figurent dans le lot **Oak CUG Authorization** (`org.apache.jackrabbit.oak-authorization-cug`), qui fait partie de l’installation par défaut d’AEM. Le lot définit un modèle d’autorisation séparé destiné à être déployé comme un autre moyen de gérer l’accès en lecture.

#### Configuration de l’autorisation de CUG {#setting-up-cug-authorization}

L’installation de l’autorisation de CUG est décrite en détail dans la [documentation Apache appropriée](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability). Par défaut, l’autorisation de CUG est déployée dans tous les modes d’exécution d’AEM. Les instructions étape par étape peuvent également être suivies pour désactiver l’autorisation de CUG dans les installations qui nécessitent une configuration d’autorisation différente.

#### Configuration du filtre de référent {#configuring-the-referrer-filter}

Vous devez également configurer le [filtre de référent Sling](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) avec tous les noms d’hôtes pouvant être utilisés pour accéder à AEM ; par exemple, par l’intermédiaire du réseau CDN, de la répartition de charge et d’autres.

Si le filtre de référent n’est pas configuré, des erreurs, similaires à celles-ci, s’affichent lorsqu’un utilisateur ou une utilisatrice tente de se connecter à un site CUG :

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### Caractéristiques des composants OSGi {#characteristics-of-osgi-components}

Les deux composants OSGi suivants ont été introduits pour définir les exigences d’authentification et spécifier des chemins de connexion dédiés :

* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration`
* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl`

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration**

<table>
 <tbody>
  <tr>
   <td>Libellé</td>
   <td>Configuration de CUG Apache Jackrabbit Oak</td>
  </tr>
  <tr>
   <td>Description</td>
   <td>Configuration de l’autorisation dédiée à la configuration et à l’évaluation des permissions de CUG.</td>
  </tr>
  <tr>
   <td>Propriétés de configuration</td>
   <td>
    <ul>
     <li><code>cugSupportedPaths</code></li>
     <li><code>cugEnabled</code></li>
     <li><code>configurationRanking</code></li>
    </ul> <p>Consultez également la section <a href="#configuration-options">Options de configuration</a> ci-dessous.</p> </td>
  </tr>
  <tr>
   <td>Politique de configuration</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>Références</td>
   <td><code>CugExclude (ReferenceCardinality.OPTIONAL_UNARY)</code></td>
  </tr>
 </tbody>
</table>

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl**

<table>
 <tbody>
  <tr>
   <td>Libellé</td>
   <td>Liste d’exclusion de CUG Apache Jackrabbit Oak</td>
  </tr>
  <tr>
   <td>Description</td>
   <td>Vous permet d’exclure les principaux avec les noms configurés de l’évaluation de CUG.</td>
  </tr>
  <tr>
   <td>Propriétés de configuration</td>
   <td>
    <ul>
     <li><code>principalNames</code></li>
    </ul> <p>Consultez également la section Options de configuration ci-dessous.</p> </td>
  </tr>
  <tr>
   <td>Politique de configuration</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>Références</td>
   <td>S/O</td>
  </tr>
 </tbody>
</table>

#### Options de configuration {#configuration-options}

Les principales options de configuration sont :

* `cugSupportedPaths` : spécifiez les sous-arborescences pouvant contenir des CUG. Aucune valeur n’est définie par défaut.
* `cugEnabled` : option de configuration pour activer l’évaluation des permissions pour les politiques de CUG actuelles.

Les options de configuration disponibles associées au module d’autorisation CUG sont répertoriées et décrites plus en détail dans la [documentation Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration).

#### Exclusion des principaux de l’évaluation CUG {#excluding-principals-from-cug-evaluation}

L’exemption de principaux de l’évaluation de CUG a été adoptée à partir de l’ancienne mise en œuvre. La nouvelle autorisation de CUG couvre cette fonction avec une interface dédiée nommée CugExclude. Apache Jackrabbit Oak 1.4 est fourni avec une mise en œuvre par défaut qui exclut un ensemble fixe de principaux, ainsi qu’une mise en œuvre étendue qui permet de configurer les noms des différents principaux. Ce dernier est configuré dans les instances de publication AEM.

La valeur par défaut depuis AEM 6.3 empêche les principaux suivants d’être affectés par les politiques CUG :

* principaux administratifs (utilisateur administrateur ou utilisatrice administratrice, groupe d’administrateurs ou d’administratrices) ;
* principaux utilisateurs du service
* principal du système interne du référentiel

Pour plus d’informations, consultez le tableau dans la section [Configuration par défaut depuis AEM 6.3](#default-configuration-since-aem) ci-dessous.

L’exclusion du groupe d’administrateurs peut être modifiée ou augmentée dans la console système dans la section de configuration de **Liste d’exclusion de CUG Apache Jackrabbit Oak**.

Sinon, il est possible de fournir et de déployer une mise en œuvre personnalisée de l’interface CugExclude pour ajuster l’ensemble des principaux exclus en cas de besoins spécifiques. Consultez la documentation relative à l’[aspect enfichable des CUG](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) pour plus d’informations et pour obtenir un exemple de mise en œuvre.

### Authentification : installation et configuration {#authentication-setup-and-configuration}

Les nouveaux composants liés à l’authentification figurent dans le lot **Gestionnaire d’authentification Adobe Granite** (`com.adobe.granite.auth.authhandler` version 5.6.48). Ce lot fait partie de l’installation par défaut d’AEM.

Pour installer l’exigence d’authentification de remplacement pour la prise en charge de CUG obsolète, certains composants OSGi doivent être présents et actifs dans une configuration d’AEM donnée. Pour plus de détails, consultez les **Caractéristiques des composants OSGi** ci-dessous.

>[!NOTE]
>
>En raison de l’option de configuration obligatoire avec RequirementHandler, les composants liés à l’authentification sont activés uniquement si la fonction a été activée en spécifiant un ensemble de chemins pris en charge. Avec une installation AEM standard, la fonctionnalité est désactivée en mode d’exécution de création et activée pour /content en mode d’exécution de publication.

**Caractéristiques des composants OSGi**

Les deux composants OSGi suivants ont été introduits pour définir les exigences d’authentification et spécifier des chemins de connexion dédiés :

* `com.adobe.granite.auth.requirement.impl.RequirementService`
* `com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler`

**com.adobe.granite.auth.requirement.impl.RequirementService**

<table>
 <tbody>
  <tr>
   <td>Libellé</td>
   <td>-</td>
  </tr>
  <tr>
   <td>Description</td>
   <td>Service OSGi dédié aux exigences d’authentification qui enregistre un observateur pour les modifications de contenu affectant les exigences d’authentification (via le type mixin <code>granite:AuthenticationRequirement</code>) et les chemins de connexion sont exposés à la variable <code>LoginSelectorHandler</code>. </td>
  </tr>
  <tr>
   <td>Propriétés de configuration</td>
   <td>-</td>
  </tr>
  <tr>
   <td>Politique de configuration</td>
   <td><code>ConfigurationPolicy.OPTIONAL</code></td>
  </tr>
  <tr>
   <td>Références</td>
   <td>
    <ul>
     <li><code>RequirementHandler (ReferenceCardinality.MANDATORY_UNARY)</code></li>
     <li><code>Executor (ReferenceCardinality.MANDATORY_UNARY)</code></li>
    </ul> </td>
  </tr>
 </tbody>
</table>

**com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler**

| Libellé | Gestionnaire d’exigence d’authentification et de chemin de connexion Adobe Granite |
|---|---|
| Description | Mise en œuvre de `RequirementHandler` qui met à jour les exigences d’authentification Apache Sling et l’exclusion correspondante pour les chemins de connexion associés. |
| Propriétés de configuration | `supportedPaths` |
| Politique de configuration | `ConfigurationPolicy.REQUIRE` |
| Références | S/O |

#### Options de configuration {#configuration-options-1}

Les parties liées à l’authentification de la réécriture de CUG ne sont accompagnées que d’une seule option de configuration associée au gestionnaire d’exigence d’authentification et de chemin de connexion Adobe Granite :

**« Gestionnaire d’exigence d’authentification et de chemin de connexion »**

<table>
 <tbody>
  <tr>
   <td>Propriété</td>
   <td>Type</td>
   <td>Valeur par défaut</td>
   <td>Description</td>
  </tr>
  <tr>
   <td><p>Libellé = Chemins pris en charge</p> <p>Nom = ’supportedPaths’</p> </td>
   <td>Set&lt;String&gt;</td>
   <td>-</td>
   <td>Chemins sous lesquels les exigences d’authentification seront respectées par ce gestionnaire. Ne définissez pas cette configuration si vous voulez ajouter le type de mixin <code>granite:AuthenticationRequirement</code> aux nœuds sans les appliquer (par exemple, sur les instances de création). Si elle est absente, la fonction est désactivée. </td>
  </tr>
 </tbody>
</table>

## Configuration par défaut depuis AEM 6.3 {#default-configuration-since-aem}

Les nouvelles installations d’AEM utilisent par défaut les nouvelles mises en œuvre à la fois pour les composants liés à l’autorisation et à l’authentification de la fonction CUG. L’ancienne implémentation « Prise en charge des groupes d’utilisateurs fermés (CUG) par Adobe Granite » a été abandonnée et sera désactivée dans toutes les installations d’AEM. Les nouvelles mises en œuvre seront plutôt activées comme suit :

### Instances de création {#author-instances}

| **« Configuration de CUG Apache Jackrabbit Oak »** | **Explication** |
|---|---|
| Chemins pris en charge `/content` | La gestion du contrôle d’accès pour les politiques de CUG est activée. |
| FALSE activée pour l’évaluation des CUG | L’évaluation des autorisations est désactivée. Les politiques de CUG n’ont aucun effet. |
| Classement \|200 | Consultez la documentation d’Oak. |

>[!NOTE]
>
>Aucune configuration pour la **Liste d’exclusion CUG Apache Jackrabbit Oak** et le **Gestionnaire d’exigence d’authentification et de chemin de connexion Adobe Granite** n’est présente sur les instances de création par défaut.

### Instances de publication {#publish-instances}

| **« Configuration de CUG Apache Jackrabbit Oak »** | **Explication** |
|---|---|
| Chemins pris en charge `/content` | La gestion du contrôle d’accès pour les politiques de CUG est activée sous les chemins configurés. |
| Évaluation des CUG activée TRUE | L’évaluation des autorisations est activée sous les chemins configurés. Les politiques de CUG prennent effet `Session.save()`. |
| Classement \|200 | Consultez la documentation d’Oak. |

| **« Liste d’exclusion de CUG Apache Jackrabbit Oak »** | **Explication** |
|---|---|
| Administrateurs de noms principaux | Exclut le principal des administrateurs de l’évaluation des CUG. |

| **« Gestionnaire d’exigence d’authentification et de chemin de connexion Adobe Granite »** | **Explication** |
|---|---|
| Chemins pris en charge `/content` | Les exigences d’authentification telles que définies dans le référentiel au moyen du type de mixin `granite:AuthenticationRequired` prennent effet sous `/content` sur `Session.save()`. L’authentificateur Sling est mis à jour. L’ajout du type de mixin en dehors des chemins pris en charge est ignoré. |

## Désactivation de l’autorisation du CUG et de l’exigence d’authentification {#disabling-cug-authorization-and-authentication-requirement}

La nouvelle implémentation peut être complètement désactivée dans le cas où une installation donnée n’utilise pas de CUG ou utilise d’autres moyens d’authentification et d’autorisation.

### Désactiver l’autorisation du CUG {#disable-cug-authorization}

Consultez la documentation [Possibilité de branchement CUG](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) pour plus de détails sur la suppression du modèle d’autorisation du CUG de la configuration d’autorisation composite.

### Désactiver l’exigence d’authentification {#disable-the-authentication-requirement}

Pour désactiver la prise en charge de l’exigence d’authentification fournie par le module `granite.auth.authhandler`, il suffit de supprimer la configuration associée au **Gestionnaire d’exigence d’authentification et de chemin de connexion Adobe Granite**.

>[!NOTE]
>
>Notez cependant que la suppression de la configuration ne désenregistre pas le type de mixin, qui était toujours applicable aux nœuds sans prendre effet.

## Interactions avec d’autres modules {#interaction-with-other-modules}

### API Apache Jackrabbit {#apache-jackrabbit-api}

Afin de refléter le nouveau type de politique de contrôle d’accès utilisé par le modèle d’autorisation des CUG, l’API définie par Apache Jackrabbit a été étendue. Ainsi, la version 2.11.0 du module `jackrabbit-api` définit une nouvelle interface appelée `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`, qui s’étend à partir de `javax.jcr.security.AccessControlPolicy`.

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

Le mécanisme d’importation d’Apache Jackrabbit FileVault a été adapté pour traiter les politiques de contrôle d’accès de type `PrincipalSetPolicy`.

### Distribution de contenu Apache Sling {#apache-sling-content-distribution}

Voir ci-dessus la section [Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault).

### Réplication Adobe Granite {#adobe-granite-replication}

Le module de réplication a été légèrement ajusté pour pouvoir répliquer les politiques CUG entre différentes instances AEM :

* `DurboImportConfiguration.isImportAcl()` est interprété littéralement et affecte uniquement les politiques de contrôle d’accès mettant en œuvre `javax.jcr.security.AccessControlList`.

* `DurboImportTransformer` respecte uniquement cette configuration pour les vraies listes de contrôle d’accès.
* D’autres politiques telles que les instances de `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` créées par le modèle d’autorisation des CUG sont toujours répliquées, et l’option de configuration `DurboImportConfiguration.isImportAcl` () est ignorée.

Il existe une limite de réplication des politiques de CUG. Si une politique de CUG donnée est supprimée sans supprimer le type de nœud de mixin `rep:CugMixin,` correspondant, la suppression n’est pas répercutée lors de la réplication. Ce problème a été corrigé en supprimant toujours le mixin lors de la suppression d’une politique. La limitation peut néanmoins apparaître si le type de mixin est ajouté manuellement.

### Gestionnaire d’authentification Adobe Granite {#adobe-granite-authentication-handler}

Le gestionnaire d’authentification **Adobe Granite HTTP Header Authentication Handler** fourni avec le lot `com.adobe.granite.auth.authhandler` contient une référence à l’interface `CugSupport` définie par le même module. Il est utilisé pour calculer le domaine dans certains cas, en se repliant sur le domaine configuré avec le gestionnaire.

Cela a été réglé de façon à rendre la référence à `CugSupport` facultative pour assurer une compatibilité ascendante maximale si une configuration donnée décide de réactiver cette mise en œuvre obsolète. Pour les installations recourant à cette mise en œuvre, le domaine n’est pas extrait à partir de la mise en œuvre CUG, mais s’affiche toujours tel que défini auprès du gestionnaire d’authentification **Adobe Granite HTTP Header Authentication Handler**.

>[!NOTE]
>
>Par défaut, le **Gestionnaire d’authentification d’en-tête HTTP Adobe Granite** n’est configuré que dans le mode d’exécution de publication avec l’option « Désactiver la page de connexion » (`auth.http.nologin`) activée.

### AEM LiveCopy {#aem-livecopy}

La configuration des CUG avec LiveCopy est représentée dans le référentiel par l’ajout d’un nœud et d’une propriété supplémentaires comme suit :

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

Ces deux éléments sont créés sous `cq:Page`. Avec la conception actuelle, le MSM ne gère que les nœuds et les propriétés sous le nœud `cq:PageContent` (`jcr:content`).

Par conséquent, les groupes CUG ne peuvent pas être déployés sur des Live Copies à partir de plans directeurs. Tenez-en compte lors de la configuration de la Live Copy.

## Modifications de la nouvelle mise en œuvre du CUG {#changes-with-the-new-cug-implementation}

Cette section est destinée à présenter les modifications apportées à la fonction CUG et à comparer l’ancienne et la nouvelle mise en œuvre. Il répertorie les modifications affectant la façon dont la prise en charge des CUG est configurée et décrit comment et par qui les CUG sont gérés dans le contenu du référentiel.

### Différences dans l’installation et la configuration des CUG {#differences-in-cug-setup-and-configuration}

Le composant OSGi obsolète **Prise en charge des groupes d’utilisateurs fermés (CUG) Adobe Granite** (`com.day.cq.auth.impl.cug.CugSupportImpl`) a été remplacé par de nouveaux composants de façon à gérer séparément les composants liés à l’autorisation et à l’authentification de la fonctionnalité de CUG précédente.

## Différences dans la gestion des CUG au sein du référentiel de contenu {#differences-in-managing-cugs-in-the-repository-content}

Les sections suivantes décrivent les différences entre l’ancienne et la nouvelle mise en œuvre du point de vue de l’implémentation et de la sécurité. Bien que la nouvelle mise en œuvre vise à fournir les mêmes fonctionnalités, il y a des changements subtils qu’il est important de connaître avec le nouveau CUG.

### Différences quant à l’autorisation {#differences-with-regards-to-authorization}

Les principales différences du point de vue des autorisations sont résumées dans la liste ci-dessous :

**Contenu de contrôle d’accès dédié aux CUG**

Dans l’ancienne mise en œuvre, le modèle d’autorisation par défaut était utilisé pour manipuler les politiques de liste de contrôle d’accès sur l’instance de publication, remplaçant tous les ACE existants par la configuration requise par le CUG. Cela a été déclenché par l’écriture de propriétés JCR résiduelles régulières qui ont été interprétées lors de la publication.

Avec la nouvelle mise en œuvre, l’installation du contrôle d’accès du modèle d’autorisation par défaut n’est pas affectée par tout CUG qui est créé, modifié ou supprimé. À la place, un nouveau type de politique nommé `PrincipalSetPolicy` est appliqué en tant que contenu de contrôle d’accès supplémentaire sur le nœud cible. Cette politique supplémentaire est placée en tant qu’enfant du nœud cible et doit être une sœur du nœud de politique par défaut (s’il existe).

**Modifier les politiques CUG dans la gestion du contrôle d’accès**

Cette transition des propriétés JCR résiduelles vers une politique de contrôle d’accès dédiée a un impact sur les permissions requises pour créer ou modifier le composant d’autorisation de la fonction CUG. Dans la mesure où cette opération est considérée comme une modification du contenu de contrôle d’accès, elle requiert que les privilèges `jcr:readAccessControl` et `jcr:modifyAccessControl` soient écrits dans le référentiel. Par conséquent, seuls les auteurs et autrices de contenu autorisés à modifier le contenu de contrôle d’accès d’une page peuvent installer ou modifier ce contenu. Cela contraste avec l’ancienne mise en œuvre où la possibilité d’écrire des propriétés JCR standard suffisait, entraînant la réaffectation des privilèges.

**Nœud cible défini par la politique**

Les politiques CUG sont créées au niveau du nœud JCR définissant la sous-arborescence dont l’accès en lecture est limitée. Il s’agit probablement d’une page AEM au cas où le CUG devrait affecter l’ensemble de l’arborescence.

Le placement de la politique de CUG uniquement au niveau du nœud jcr:content situé en dessous d’une page donnée limite uniquement l’accès au contenu s.str d’une page donnée, mais n’aura aucun effet sur les pages enfants ou frères. Il peut s’agir d’un cas d’utilisation valide, réalisable avec un éditeur de référentiel qui permet d’appliquer un accès de granularité fine au contenu. Toutefois, cela contraste avec l’ancienne mise en œuvre où le placement d’une propriété cq:cugEnabled sur le nœud jcr:content était remis en correspondance en interne sur le nœud de page. Ce mappage n’est plus effectué.

**Évaluation des autorisations avec les politiques CUG**

Le passage de l’ancienne prise en charge des CUG à un modèle d’autorisation supplémentaire, modifie la façon dont les permissions de lecture en vigueur sont évaluées. Comme indiqué dans la [documentation relative à Jackrabbit](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html), un principal spécifique autorisé à afficher `CUGcontent` n’obtient l’accès en lecture que si l’évaluation des autorisations de tous les modèles configurés dans le référentiel Oak lui accorde l’accès en lecture.

En d’autres termes, pour l’évaluation des permissions en vigueur, à la fois `CUGPolicy` et les entrées de contrôle d’accès par défaut font l’objet d’une prise en compte, et l’accès en lecture sur le contenu CUG est uniquement autorisé s’il est accordé par les deux types de politiques. Dans une installation de publication AEM par défaut où l’accès en lecture à l’arborescence `/content` complète est accordé à tout le monde, l’effet des politiques de CUG est le même que celui de l’ancienne mise en œuvre.

**Évaluation à la demande**

Le modèle d’autorisation du CUG permet d’activer individuellement la gestion du contrôle d’accès et l’évaluation des autorisations :

* La gestion du contrôle d’accès est activée si le module dispose d’un ou plusieurs chemins pris en charge où les CUG peuvent être créés.
* L’évaluation des autorisations n’est activée que si vous avez coché la case de l’option **Évaluation des CUG activée**.

Dans l’évaluation des politiques de CUG de la nouvelle configuration par défaut d’AEM, elle est activée uniquement avec le mode d’exécution de publication. Consultez les informations relatives à la [configuration par défaut depuis AEM 6.3](#default-configuration-since-aem) pour en savoir plus. Cela peut être vérifié en comparant les politiques en vigueur pour un chemin donné vers les politiques stockées dans le contenu. Les politiques en vigueur sont affichées uniquement dans le cas où l’évaluation des permissions est activée pour les CUG.

Comme expliqué plus haut, les politiques de contrôle d’accès de CUG sont désormais toujours stockées dans le contenu, mais l’évaluation des permissions en vigueur découlant de ces politiques ne sera imposée que si l’**évaluation des CUG activée** est sélectionnée dans la console système au niveau de la configuration des CUG Apache Jackrabbit Oak **.** Par défaut, elle est uniquement activée avec le mode d’exécution de publication.

### Différences en matière d’authentification {#differences-with-regards-to-authentication}

Les différences concernant l’authentification sont décrites ci-dessous.

#### Type de mixin dédié pour les exigences d’authentification {#dedicated-mixin-type-for-authentication-requirement}

Dans l’ancienne mise en œuvre, les aspects d’autorisation et d’authentification d’un CUG étaient tous deux déclenchés par une seule propriété JCR (`cq:cugEnabled`). En ce qui concerne l’authentification, il en résultait une liste mise à jour des exigences d’authentification telles que stockées avec la mise en œuvre de l’authentificateur Apache Sling. Avec la nouvelle mise en œuvre, le même résultat est obtenu en marquant le nœud cible avec un type spécial de mixin (`granite:AuthenticationRequired`).

#### Propriété d’exclusion d’un chemin de connexion {#property-for-excluding-login-path}

Le type de mixin définit une propriété unique et facultative appelée `granite:loginPath`, qui correspond essentiellement à la propriété `cq:cugLoginPage`. Contrairement à la mise en œuvre précédente, la propriété de chemin de connexion n’est respectée que si son type de nœud d’instruction est le mixin indiqué. L’ajout d’une propriété portant ce nom sans définir le type de mixin n’aura aucun effet. En outre, ni une nouvelle exigence ni une exclusion pour le chemin de connexion ne seront signalées à l’authentificateur.

#### Privilège pour l’exigence d’authentification {#privilege-for-authentication-requirement}

L’ajout ou la suppression d’un type de mixin requiert l’attribution du privilège `jcr:nodeTypeManagement`. Dans la mise en œuvre précédente, le privilège `jcr:modifyProperties` était utilisé pour modifier la propriété résiduelle.

En ce qui concerne `granite:loginPath`, le même privilège est requis pour ajouter, modifier ou supprimer la propriété.

#### Nœud cible défini par type de mixin {#target-node-defined-by-mixin-type}

Créez des exigences d’authentification au niveau du nœud JCR définissant la sous-arborescence qui doit être soumise à une connexion forcée. Il s’agira probablement d’une page AEM dans la mesure où le CUG devrait affecter l’ensemble de l’arborescence et que l’interface utilisateur de la nouvelle implémentation ajouterait ainsi le type de mixin d’exigence d’authentification sur le nœud de la page.

Le fait de placer la politique de CUG uniquement au niveau du nœud jcr:content situé sous une page donnée limite uniquement l’accès au contenu. Toutefois, cela n’a aucune incidence sur le nœud de page lui-même ni sur les pages enfants.

Il peut s’agir d’un scénario valide et possible avec un éditeur de référentiel qui permet de placer le mixin au niveau de n’importe quel nœud. Cependant, le comportement contraste avec l’ancienne mise en œuvre, où le placement d’une propriété cq:cugEnabled ou cq:cugLoginPage sur le nœud jcr:content était remis en correspondance en interne sur le nœud de page. Ce mappage n’est plus effectué.

#### Chemins pris en charge configurés {#configured-supported-paths}

Le type de mixin `granite:AuthenticationRequired` et la propriété granite:loginPath ne sont respectés que dans la portée définie par le jeu de l’option de configuration **Chemins pris en charge** présent avec le gestionnaire d’exigence d’authentification et de chemin de connexion Adobe **&#x200B;**. Si aucun chemin n’est spécifié, la fonction d’exigence d’authentification est complètement désactivée. Dans ce cas, ni le type de mixin ni la propriété ne prennent effet lorsqu’ils sont ajoutés ou définis sur un nœud JCR donné.

### Mappage de contenu JCR, de services OSGi et de configurations {#mapping-of-jcr-content-osgi-services-and-configurations}

Le document ci-dessous fournit un mappage complet des services OSGi, des configurations et du contenu de référentiel entre l’ancienne et la nouvelle mise en œuvre.

Mise en correspondance de CUG depuis AEM 6.3

[Obtenir le fichier](assets/cug-mapping.pdf)

## Mettre à niveau le CUG {#upgrade-cug}

### Installations existantes utilisant le CUG obsolète {#existing-installations-using-the-deprecated-cug}

L’ancienne mise en œuvre de prise en charge des CUG a été abandonnée et sera supprimée dans les futures versions. Il est recommandé de passer aux nouvelles implémentations lors de la mise à niveau à partir de versions antérieures à AEM 6.3.

Pour les installations AEM mises à niveau, il est important de s’assurer qu’une seule mise en œuvre CUG est activée. La combinaison de la nouvelle et de l’ancienne prise en charge des CUG obsolètes n’est pas testée et est susceptible de provoquer un comportement indésirable :

* Des collisions dans Sling Authenticator en ce qui concerne les exigences d’authentification.
* L’accès en lecture refusé lorsque la configuration de l’ACL associée à l’ancien CUG entre en collision avec une nouvelle politique CUG.

### Migration d’un contenu de CGU existant {#migrating-existing-cug-content}

Adobe fournit un outil pour migrer vers la nouvelle mise en œuvre de CUG. Pour l’utiliser, procédez comme suit :

1. Accédez à `https://<serveraddress>:<serverport>/system/console/cug-migration` pour accéder à l’outil.
1. Saisissez le chemin racine pour lequel vous souhaitez vérifier les CUG et appuyez sur le bouton **Exécution d’essai**. Cela permet de rechercher les CUG pouvant être convertis à l’emplacement sélectionné.
1. Une fois que vous avez consulté les résultats, appuyez sur le bouton **Effectuer la migration** pour migrer vers la nouvelle mise en œuvre.

>[!NOTE]
>
>Si vous rencontrez des difficultés, il est possible de configurer un enregistreur spécifique au niveau **DEBUG** sur `com.day.cq.auth.impl.cug` pour obtenir la sortie de l’outil de migration. Consultez la rubrique [Connexion](/help/sites-deploying/configure-logging.md) pour en savoir plus sur la procédure à suivre.
