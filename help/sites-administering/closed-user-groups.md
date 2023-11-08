---
title: Groupes d’utilisateurs fermés dans AEM
description: Découvrez les groupes d’utilisateurs fermés et les avantages qu’ils apportent à l’évolutivité et à la sécurité dans AEM.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 39e35a07-140f-4853-8f0d-8275bce27a65
feature: Security
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '6816'
ht-degree: 55%

---

# Groupes d’utilisateurs fermés dans AEM{#closed-user-groups-in-aem}

## Présentation {#introduction}

Depuis AEM 6.3, une nouvelle mise en oeuvre de groupe d’utilisateurs fermé est disponible pour résoudre les problèmes de performances, d’évolutivité et de sécurité liés à la mise en oeuvre existante.

>[!NOTE]
>
>Par souci de simplicité, l’abréviation CUG est utilisée dans toute cette documentation.

Cette nouvelle mise en œuvre a pour objectif de couvrir les fonctionnalités existantes en fonction des besoins, tout en résolvant les problèmes d’adressage et les limites de conception des versions antérieures. Le résultat est une nouvelle conception de CUG avec les caractéristiques suivantes :

* Séparation claire des éléments d’authentification et d’autorisation, qui peuvent être utilisés individuellement ou en combinaison ;
* modèle d’autorisation dédié pour refléter l’accès en lecture restreint aux arborescences de CUG configurées sans interférer avec d’autres exigences de configuration et d’autorisation de contrôle d’accès ;
* Séparation entre la configuration de contrôle de l’accès en lecture restreint, qui est nécessaire généralement sur les instances de création, et l’évaluation des permissions qui n’est généralement souhaitée que sur l’instance de publication
* Modification d’un accès en lecture restreint sans transmission de privilèges ;
* Extension de type de noeud dédiée pour marquer l’exigence d’authentification ;
* Chemin de connexion facultatif associé à l’exigence d’authentification.

### Nouvelle mise en oeuvre d’un groupe d’utilisateurs personnalisé {#the-new-custom-user-group-implementation}

Un groupe d’utilisateurs fermé tel qu’il est connu dans le contexte d’AEM comprend les étapes suivantes :

* Restreindre l’accès en lecture sur l’arborescence qui doit être protégée et uniquement autoriser la lecture pour les principaux qui sont soit répertoriés avec une instance de données CUG spécifique, soit exclus de l’évaluation des CUG. Cela s’appelle la variable **authorization** élément .
* Renforcez l’authentification sur une arborescence donnée et spécifiez éventuellement une page de connexion dédiée pour cette arborescence qui est ensuite exclue. Cela s’appelle la variable **authentication** élément .

La nouvelle mise en œuvre a été conçue pour distinguer les éléments d’authentification des éléments d’autorisation. Depuis AEM 6.3, il est possible de restreindre l’accès en lecture sans ajouter explicitement une exigence d’authentification. Par exemple, si une instance donnée nécessite une authentification complète ou si une arborescence donnée réside déjà dans une sous-arborescence qui nécessite déjà une authentification.

Aussi, une arborescence donnée peut être marquée par une exigence d’authentification sans modifier la configuration de permission effective. Les combinaisons et les résultats sont répertoriés dans la section [Combinaison des stratégies de CUG et de l’exigence d’authentification](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement) .

## du commerce électronique {#overview}

### Autorisation : limitation de l’accès en lecture {#authorization-restricting-read-access}

La fonctionnalité clé d’un CUG est de restreindre l’accès en lecture sur une arborescence donnée dans le référentiel de contenu pour tous à l’exception des principaux sélectionnés. Au lieu de manipuler à la volée le contenu du contrôle d’accès par défaut, la nouvelle mise en oeuvre adopte une approche différente en définissant un type dédié de stratégie de contrôle d’accès qui représente un CUG.

#### Stratégie de contrôle d’accès pour les CUG {#access-control-policy-for-cug}

Ce nouveau type de stratégie présente les caractéristiques suivantes :

* Politique de contrôle d’accès de org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy (définie par l’API Apache Jackrabbit)
* PrincipalSetPolicy accorde des privilèges à un ensemble modifiable d’entités de sécurité
* Les privilèges accordés et le domaine de la politique constituent des détails de la mise en œuvre.

La mise en œuvre de PrincipalSetPolicy utilisée pour représenter les CUG définit en outre les points suivants :

* les stratégies de CUG accordent uniquement l’accès en lecture aux éléments JCR standard (par exemple, le contenu du contrôle d’accès est exclu) ;
* La portée est définie par le noeud contrôlé par l’accès qui contient la stratégie de CUG ;
* Les stratégies de CUG peuvent être imbriquées, un CUG imbriqué démarre un nouveau CUG sans hériter de l’ensemble principal du CUG &quot;parent&quot; ;
* Si l’évaluation est activée, l’effet de la stratégie est hérité à l’ensemble de la sous-arborescence jusqu’au prochain groupe d’utilisateurs fermé imbriqué.

Ces politiques de CUG sont déployées sur les instances AEM par l’intermédiaire d’un module d’autorisation distinct appelé oak-authorization-cug. Ce module est fourni avec ses propres fonctions d’évaluation des permissions et de gestion du contrôle d’accès. En d’autres termes, la configuration par défaut d’AEM est livrée avec une configuration de référentiel de contenu Oak qui combine plusieurs mécanismes d’autorisation. Pour plus d’informations, consultez [cette page sur la documentation Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html).

Dans cette configuration composite, un nouveau CUG ne remplace pas le contenu de contrôle d’accès existant associé au nœud cible. Au contraire, il est conçu pour être un supplément qui peut également être supprimé ultérieurement sans affecter le contrôle d’accès d’origine (qui dans AEM serait par défaut une liste de contrôle d’accès).

Contrairement à la mise en œuvre précédente, les nouvelles politiques de CUG sont systématiquement reconnues et traitées comme contenu de contrôle d’accès. Cela signifie qu’elles sont créées et modifiées à l’aide de l’API de gestion du contrôle d’accès JCR. Pour plus d’informations, consultez [Gestion des politiques de CUG](#managing-cug-policies).

#### Évaluation des autorisations des stratégies de CUG {#permission-evaluation-of-cug-policies}

Outre une gestion dédiée du contrôle d’accès pour les CUG, le nouveau modèle d’autorisation vous permet d’activer de manière conditionnelle l’évaluation des permissions pour ses stratégies. Cela vous permet de configurer des stratégies de CUG dans un environnement d’évaluation et de n’activer l’évaluation des autorisations efficaces qu’une fois répliquées dans l’environnement de production.

L’évaluation des permissions pour les politiques de CUG et l’interaction avec le modèle d’autorisation par défaut ou tout modèle supplémentaire suit le modèle destiné aux mécanismes d’autorisation multiples dans Apache Jackrabbit Oak : un jeu de permissions donné est accordé si et uniquement si tous les modèles accordent l’accès. Consultez [cette page](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html) pour plus de détails.

Les caractéristiques suivantes s’appliquent à l’évaluation des autorisations associées au modèle d’autorisation conçu pour gérer et évaluer les stratégies de CUG :

* Il ne gère que les autorisations de lecture pour les noeuds et propriétés standard, mais pas le contenu de contrôle d’accès.
* Il ne prend pas en charge les autorisations d’écriture ni aucun type d’autorisation requis pour la modification du contenu JCR protégé (contrôle d’accès, informations de type de noeud, contrôle de version, verrouillage ou gestion utilisateur, entre autres). Ces autorisations ne sont pas affectées par une stratégie de CUG et ne seront pas évaluées par le modèle d’autorisation associé. Ces permissions sont accordées en fonction des autres modèles configurés dans la configuration de sécurité.

L’effet d’une politique de CUG unique sur l’évaluation des permissions peut être résumé comme suit :

* L’accès en lecture est refusé pour tous, à l’exception des sujets contenant des entités de sécurité exclues ou des entités de sécurité répertoriées dans la stratégie.
* La stratégie prend effet sur le noeud contrôlé par l’accès qui contient la stratégie et ses propriétés.
* L’effet est en outre hérité vers le bas de la hiérarchie, c’est-à-dire l’arborescence d’éléments définie par le noeud contrôlé par l’accès ;
* Toutefois, elle n’affecte ni les frères ni les ancêtres du noeud contrôlé par l’accès.
* L’héritage d’un CUG donné s’arrête à un CUG imbriqué.

#### Bonnes pratiques {#best-practices}

Les bonnes pratiques suivantes doivent être prises en compte pour définir un accès en lecture restreint par le biais de CUG :

* Déterminez si le CUG dont vous avez besoin est destiné à limiter l’accès en lecture ou s’il correspond à une exigence d’authentification. Si ce dernier, ou s’il y a un besoin des deux, consultez la section sur les bonnes pratiques pour plus de détails sur l’exigence d’authentification.
* Créez un modèle de menace pour les données ou le contenu qui doivent être protégés afin d’identifier les limites de la menace et d’obtenir une vue d’ensemble claire de la sensibilité des données et des rôles associés à l’accès autorisé.
* Modérez le contenu du référentiel et les CUG en gardant à l’esprit les aspects généraux liés aux autorisations et les bonnes pratiques :

   * N’oubliez pas que l’autorisation de lecture ne sera accordée que si un CUG donné et l’évaluation des autres modules déployés dans l’aide à la configuration permettent à un sujet donné de lire un élément de référentiel donné.
   * Évitez de créer des CUG redondants dans lesquels l’accès en lecture est déjà limité par d’autres modules d’autorisation.
   * Un besoin excessif de CUG imbriqués peut mettre en évidence des problèmes dans la conception de contenu.
   * Un besoin très excessif de CUG (par exemple, sur chaque page) peut indiquer la nécessité d’un modèle d’autorisation personnalisé potentiellement mieux adapté aux besoins de sécurité spécifiques de l’application et du contenu en question.

* Limitez les chemins pris en charge pour les politiques de CUG à un petit nombre d’arborescences dans le référentiel afin d’optimiser les performances. Par exemple, autorisez uniquement les CUG sous le noeud /content , tel qu’il est fourni comme valeur par défaut depuis AEM 6.3.
* Les politiques de CUG sont conçues pour autoriser l’accès en lecture à un petit ensemble d’entités de sécurité. La nécessité d’un grand nombre d’entités de sécurité peut mettre en évidence des problèmes dans la conception du contenu ou de l’application et doit être reconsidérée.

### Authentification : définition de l’exigence d’authentification {#authentication-defining-the-auth-requirement}

Les parties liées à l’authentification de la fonction CUG vous permettent de marquer les arborescences qui nécessitent une authentification et éventuellement de spécifier une page de connexion dédiée. Conformément à la version précédente, la nouvelle mise en oeuvre vous permet de marquer les arborescences qui nécessitent une authentification dans le référentiel de contenu et d’activer de manière conditionnelle la synchronisation avec l’ `Sling org.apache.sling.api.auth.Authenticator`responsable de l’application finale de l’exigence et de la redirection vers une ressource de connexion.

Ces exigences sont enregistrées auprès de l’authentificateur au moyen d’un service OSGi qui fournit la propriété d’enregistrement `sling.auth.requirements`. Ces propriétés sont ensuite utilisées pour étendre les exigences d’authentification de façon dynamique. Pour plus d’informations, consultez la [Documentation Sling](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS).

#### Définition de l’exigence d’authentification avec un type de mixin dédié {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

Pour des raisons de sécurité, la nouvelle mise en œuvre remplace l’utilisation d’une propriété JCR résiduelle par un type de mixin dédié appelé `granite:AuthenticationRequired`, qui définit une propriété facultative unique de type CHAÎNE pour le chemin de connexion `granite:loginPath`. Seules les modifications du contenu liées à ce type de mixin entraînent la mise à jour des exigences enregistrées auprès de l’authentificateur Apache Sling. Les modifications sont suivies lors de la persistance de toute modification provisoire et nécessitent donc un appel `javax.jcr.Session.save()` pour prendre effet.

Il en va de même pour la propriété `granite:loginPath`. Elle n’est respectée que si elle est définie par le type de mixin lié à l’exigence d’authentification. L’ajout d’une propriété résiduelle du même nom au niveau d’un nœud JCR non structuré ne produit pas l’effet souhaité, et la propriété est ignorée par le gestionnaire responsable de la mise à jour de l’enregistrement OSGi.

>[!NOTE]
>
>La définition de la propriété de chemin de connexion est facultative et elle est uniquement nécessaire si l’arborescence nécessitant une authentification ne peut se replier sur la page de connexion par défaut ou héritée. Voir [Évaluation du chemin de connexion](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path) ci-dessous

#### Enregistrement de l’exigence d’authentification et du chemin de connexion avec l’authentificateur Sling {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

Puisqu’il est prévu que ce type d’exigence d’authentification soit limité à certains modes d’exécution et à un petit sous-ensemble d’arborescences dans le référentiel de contenu, le suivi du type de mixin de l’exigence et des propriétés de chemin de connexion est conditionnel et associé à une configuration correspondante qui définit les chemins pris en charge (voir la section Options de configuration ci-dessous). Par conséquent, seules les modifications dans la portée de ces chemins pris en charge déclenchent une mise à jour de l’enregistrement OSGi ; dans les autres cas, le type de mixin et la propriété sont tous deux ignorés.

Par défaut, AEM utilise désormais cette configuration en permettant de placer le mixin en mode d’exécution de création, mais en ne le faisant prendre effet que lors de la réplication vers l’instance de publication. Consultez [cette page](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html) pour plus d’informations sur la façon dont Sling impose l’exigence d’authentification.

Ajouter le `granite:AuthenticationRequired` le type de mixin dans les chemins pris en charge configurés entraîne la mise à jour de l’enregistrement OSGi du gestionnaire responsable, contenant une nouvelle entrée supplémentaire avec la propriété `sling.auth.requirements` . Si une exigence d’authentification donnée spécifie l’option `granite:loginPath` , la valeur est également enregistrée auprès de l’authentificateur avec un préfixe &quot;-&quot; à exclure de l’exigence d’authentification.

#### Évaluation et héritage de l’exigence d’authentification {#evaluation-and-inheritance-of-the-authentication-requirement}

Il est attendu que les exigences d’authentification d’Apache Sling soient héritées dans la hiérarchie de page ou de nœud. Les détails de l’héritage et l’évaluation des exigences d’authentification, tels que l’ordre et la priorité, sont considérés comme un détail de mise en oeuvre et ne seront pas documentés dans cet article.

#### Évaluation du chemin de connexion {#evaluation-of-login-path}

L’évaluation du chemin de connexion et de la redirection vers la ressource correspondante lors de l’authentification est actuellement un détail de mise en œuvre du gestionnaire d’authentification du sélecteur de connexion Adobe Granite (`com.day.cq.auth.impl.LoginSelectorHandler`), qui est un gestionnaire d’authentification Apache Sling configuré avec AEM par défaut.

En appelant `AuthenticationHandler.requestCredentials`, ce gestionnaire tente de déterminer la page de connexion de mise en correspondance vers laquelle l’utilisateur est redirigé. Les étapes sont les suivantes :

* faire la distinction entre le mot de passe expiré et la nécessité d’une connexion régulière comme motif de redirection ;
* Lors d’une connexion normale, vérifie si un chemin de connexion peut être obtenu dans l’ordre suivant :

   * À partir du LoginPathProvider mis en œuvre par le nouveau `com.adobe.granite.auth.requirement.impl.RequirementService`
   * À partir de l’ancienne mise en œuvre CUG obsolète
   * À partir des mises en correspondance de page de connexion, telles que définies avec `LoginSelectorHandler`
   * et enfin, revenez à la page de connexion par défaut, telle que définie avec la variable `LoginSelectorHandler`.

* Dès qu’un chemin de connexion valide est obtenu par les appels répertoriés ci-dessus, la requête de l’utilisateur est redirigée vers cette page.

Cette documentation traite de l’évaluation du chemin de connexion tel qu’il est exposé par l’interface `LoginPathProvider` interne. L’implémentation fournie depuis AEM 6.3 se comporte comme suit :

* L’enregistrement des chemins de connexion dépend de la distinction entre le mot de passe expiré et la nécessité d’une connexion régulière comme raison de la redirection.
* Lors d’une connexion normale, vérifie si un chemin de connexion peut être obtenu dans l’ordre suivant :

   * À partir du `LoginPathProvider` mis en œuvre par le nouveau `com.adobe.granite.auth.requirement.impl.RequirementService`
   * À partir de l’ancienne mise en œuvre CUG obsolète
   * À partir des mises en correspondance de page de connexion, telles que définies avec `LoginSelectorHandler`
   * et enfin retournez à la page de connexion par défaut telle que définie avec la variable `LoginSelectorHandler`.

* Dès qu’un chemin de connexion valide est obtenu par les appels répertoriés ci-dessus, la requête de l’utilisateur est redirigée vers cette page.

Le `LoginPathProvider`, tel qu’il est mis en œuvre par la nouvelle prise en charge d’exigence d’authentification dans Granite, expose les chemins de connexion Granite tels que définis par les propriétés `granite:loginPath`, qui à leur tour sont définis par le type de mixin comme décrit ci-dessus. Le mappage du chemin de ressource contenant le chemin de connexion et la valeur de propriété elle-même est conservé en mémoire et sera évalué afin de trouver un chemin de connexion approprié pour les autres noeuds de la hiérarchie.

>[!NOTE]
>
>L’évaluation est effectuée uniquement pour les requêtes liées aux ressources qui se trouvent dans les chemins pris en charge configurés. Pour toute autre requête, les autres méthodes permettant de déterminer le chemin de connexion seront évaluées.

#### Bonnes pratiques {#best-practices-1}

Les bonnes pratiques suivantes doivent être prises en compte lors de la définition des exigences d’authentification :

* Il est préférable de ne pas imbriquer les exigences d’authentification : le fait de placer un marqueur d’exigence d’authentification unique au début d’une arborescence devrait suffire et est hérité par toute la sous-arborescence définie par le nœud cible. Tout exigence supplémentaire d’authentification dans cette arborescence doit être considérée comme redondante et peut entraîner des problèmes de performances lors de l’évaluation de l’exigence d’authentification dans Apache Sling. Avec la séparation des zones CUG liées aux autorisations et à l’authentification, il est possible de restreindre l’accès en lecture au moyen de CUG ou d’autres types de stratégies tout en appliquant l’authentification pour l’ensemble de l’arborescence.
* Le contenu du référentiel de modèle de sorte que les exigences d’authentification s’appliquent à l’ensemble de l’arborescence sans avoir à exclure à nouveau les sous-arborescences imbriquées de l’exigence.
* Pour éviter de spécifier et d’enregistrer ensuite des chemins de connexion redondants :

   * Utilisez l’héritage et évitez de définir des chemins de connexion imbriqués.
   * Ne définissez pas le chemin de connexion facultatif sur une valeur qui correspond à la valeur par défaut ou à la valeur héritée.
   * Les développeurs d’applications doivent identifier les mises en correspondance de connexion qui doivent être configurées dans les fonctions de chemin de connexion globales (par défaut et mise en correspondance) associées à `LoginSelectorHandler`.

## Représentation dans le référentiel {#representation-in-the-repository}

### Représentation de la stratégie de CUG dans le référentiel {#cug-policy-representation-in-the-repository}

La documentation Oak couvre la façon dont les nouvelles politiques de CUG sont reflétées dans le contenu du référentiel. Pour plus d’informations, consultez [cette page](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository).

### Exigence d’authentification dans le référentiel {#authentication-requirement-in-the-repository}

Le besoin d’une exigence d’authentification distincte est reflété dans le contenu du référentiel avec un type de nœud mixin dédié placé au niveau du nœud cible. Le type de mixin définit une propriété facultative afin de spécifier une page de connexion dédiée pour l’arborescence définie par le noeud cible.

La page associée au chemin de connexion peut être placée à l’intérieur ou à l’extérieur de cette arborescence. Il sera exclu de l’exigence d’authentification.

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## Gestion des stratégies de CUG et des exigences d’authentification {#managing-cug-policies-and-authentication-requirement}

### Gestion des stratégies de CUG {#managing-cug-policies}

Le nouveau type de politiques de contrôle d’accès destiné à limiter l’accès en lecture pour un CUG est géré à l’aide de l’API de gestion du contrôle d’accès JCR et suit les mécanismes décrits par la [Spécification JCR 2.0](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html).

#### Définition d’une nouvelle stratégie de CUG {#set-a-new-cug-policy}

Code pour appliquer une nouvelle politique de CUG à un nœud qui n’avait pas de CUG. Notez que `getApplicablePolicies` renvoie uniquement les nouvelles stratégies qui n’ont pas été définies auparavant. À la fin, la stratégie doit être réécrite et les modifications doivent être conservées.

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

#### Modification d’une stratégie de CUG existante {#edit-an-existing-cug-policy}

Les étapes suivantes sont nécessaires pour modifier une politique de CUG existante. La stratégie modifiée doit être réécrite et les modifications doivent être conservées à l’aide de `javax.jcr.Session.save()`.

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

### Récupération des stratégies de CUG efficaces {#retrieve-effective-cug-policies}

La gestion du contrôle d’accès JCR définit une méthode du meilleur effort pour récupérer les politiques qui prennent effet à un chemin donné. L’évaluation des stratégies de CUG étant conditionnelle et dépendant de la configuration correspondante à activer, l’appel de la méthode `getEffectivePolicies` est un moyen pratique de vérifier si une stratégie de CUG donnée prend effet dans une installation donnée.

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

#### Récupération des stratégies de CUG héritées {#retrieve-inherited-cug-policies}

Recherche de tous les CUG imbriqués qui ont été définis à un chemin donné, qu’ils soient ou non effectifs. Pour plus d’informations, voir [Options de configuration](/help/sites-administering/closed-user-groups.md#configuration-options) .

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

#### Gestion des stratégies de CUG par principal {#managing-cug-policies-by-pincipal}

Les extensions définies par `JackrabbitAccessControlManager` qui permettent la modification des politiques de contrôle d’accès par une entité de sécurité ne sont pas mises en œuvre avec la gestion de contrôle d’accès CUG, comme par définition une politique de CUG affecte toujours toutes les entités de sécurité : celles répertoriées avec `PrincipalSetPolicy` se voient attribuer une autorisation d’accès en lecture, alors que toutes les autres entités de sécurité ne peuvent pas lire le contenu dans l’arborescence définie par le nœud cible.

Les méthodes correspondantes renvoient toujours un tableau de stratégie vide, mais ne renvoient pas d’exceptions.

### Gestion de l’exigence d’authentification {#managing-the-authentication-requirement}

La création, la modification ou la suppression d’une nouvelle exigence d’authentification est réalisée en modifiant le type de noeud effectif du noeud cible. La propriété de chemin de connexion facultatif peut ensuite être écrite à l’aide de l’API JCR.

>[!NOTE]
>
>Les modifications apportées à un nœud cible donné mentionné ci-dessus ne sont répercutées sur l’authentificateur Apache Sling que si `RequirementHandler` a été configuré et que la cible figure dans les arborescences définies par les chemins pris en charge (voir la section Options de configuration).
>
>Pour plus d’informations, consultez [Attribution de types de nœuds mixin] (https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3 Assigning Mixin Node Types) et [Ajout de nœuds et définition de propriétés] (https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4 Ajout de nœuds et définition de propriétés).

#### Ajout d’une nouvelle exigence d’authentification {#adding-a-new-auth-requirement}

Les étapes de création d’une exigence d’authentification sont présentées ci-dessous. L’exigence n’est enregistrée auprès de l’authentificateur Apache Sling que si la variable `RequirementHandler` a été configuré pour l’arborescence contenant le noeud cible.

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### Ajout d’une nouvelle exigence d’authentification avec le chemin de connexion {#add-a-new-auth-requirement-with-login-path}

Procédure de création d’une exigence d’authentification comprenant un chemin de connexion. Notez que cette exigence et l’exclusion du chemin de connexion ne sont enregistrées auprès de l’authentificateur Apache Sling que si `RequirementHandler` a été configuré pour l’arborescence contenant le nœud cible.

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### Modification d’un chemin de connexion existant {#modify-an-existing-login-path}

Les étapes à suivre pour modifier un chemin de connexion existant sont détaillées ci-dessous. La modification n’est enregistrée auprès de l’authentificateur Apache Sling que si `RequirementHandler` a été configuré pour l’arborescence contenant le nœud cible. La valeur précédente de chemin de connexion est supprimée de l’enregistrement. L’exigence d’authentification associée au noeud cible n’est pas affectée par cette modification.

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

#### Suppression d’un chemin de connexion existant {#remove-an-existing-login-path}

Procédure pour supprimer un chemin de connexion existant. L’annulation de l’enregistrement de l’entrée de chemin de connexion auprès de l’authentificateur Apache Sling n’est effective que si `RequirementHandler` a été configuré pour l’arborescence contenant le nœud cible. L’exigence d’authentification associée au noeud cible n’est pas affectée.

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

Vous pouvez également utiliser la méthode ci-dessous pour atteindre le même objectif :

```java
String path = [...] // absolute path to target node

String propertyPath = PathUtils.concat(path, "granite:loginPath");
if (session.propertyExists(propertyPath)) {
    session.getProperty(propertyPath).remove();
    // or: session.removeItem(propertyPath);
    session.save();
}
```

#### Suppression d’une exigence d’authentification {#remove-an-auth-requirement}

Procédure pour supprimer une exigence d’authentification existante. L’annulation de l’enregistrement de l’exigence auprès de l’authentificateur Apache Sling n’est effective que si `RequirementHandler` a été configuré pour l’arborescence contenant le nœud cible.

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### Récupération des exigences d’authentification effectives {#retrieve-effective-auth-requirements}

Il n’existe aucune API publique dédiée pour lire toutes les exigences d’authentification effectives enregistrées auprès de l’authentificateur Apache Sling. Toutefois, la liste est exposée dans la console système à l’adresse `https://<serveraddress>:<serverport>/system/console/slingauth` dans la section « **Configuration des exigences d’authentification** ».

L’image suivante illustre les exigences d’authentification d’une instance de publication AEM avec du contenu de démonstration. Le chemin mis en surbrillance de la page de la communauté illustre la façon dont une exigence ajoutée par l’implémentation décrite dans ce document est reflétée dans l’authentificateur Apache Sling.

>[!NOTE]
>
>Dans cet exemple, la propriété de chemin de connexion facultatif n’a pas été définie. Par conséquent, aucune deuxième entrée n’a été enregistrée auprès de l’authentificateur.

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### Récupération du chemin de connexion effectif {#retrieve-the-effective-login-path}

Il n’existe actuellement aucune API publique pour récupérer le chemin de connexion qui prend effet lors d’un accès anonyme à une ressource nécessitant une authentification. Voir la section Évaluation du chemin de connexion pour plus d’informations sur la mise en oeuvre de la récupération du chemin de connexion.

Notez toutefois qu’en plus des chemins de connexion définis avec cette fonctionnalité, il existe d’autres façons de spécifier la redirection vers la connexion, qui doivent être prises en compte lors de la conception du modèle de contenu et des exigences d’authentification d’une installation AEM donnée.

#### Récupération de l’exigence d’authentification héritée {#retrieve-the-inherited-auth-requirement}

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

### Combinaison des stratégies de CUG et de l’exigence d’authentification {#combining-cug-policies-and-the-authentication-requirement}

Le tableau suivant répertorie les combinaisons valides de stratégies de CUG et les exigences d’authentification dans une instance d’AEM dont les deux modules sont activés via la configuration.

| **Exigence d’authentification** | **Chemin de connexion** | **Accès en lecture limité** | **Effet attendu** |
|---|---|---|---|
| Oui | Oui | Oui | Un utilisateur donné ne pourra afficher la sous-arborescence marquée par la politique de CUG que si l’évaluation des permissions effective accorde l’accès. Les utilisateurs non authentifiés sont redirigés vers la page de connexion spécifiée. |
| Oui | Non | Oui | Un utilisateur donné ne pourra afficher la sous-arborescence marquée par la politique de CUG que si l’évaluation des permissions effective accorde l’accès. Les utilisateurs non authentifiés sont redirigés vers la page de connexion par défaut héritée. |
| Oui | Oui | Non | Les utilisateurs non authentifiés sont redirigés vers la page de connexion spécifiée. L’autorisation d’affichage de l’arborescence marquée par l’exigence d’authentification dépend des autorisations en vigueur des éléments individuels contenus dans cette sous-arborescence. Aucun CUG dédié restreignant l’accès en lecture en place. |
| Oui | Non | Non | Les utilisateurs non authentifiés sont redirigés vers la page de connexion par défaut héritée. L’autorisation d’affichage de l’arborescence marquée par l’exigence d’authentification dépend des autorisations en vigueur des éléments individuels contenus dans cette sous-arborescence. Aucun CUG dédié restreignant l’accès en lecture en place. |
| Non | Non | Oui | Un utilisateur donné, qu’il soit authentifié ou non, ne pourra afficher la sous-arborescence marquée par la politique de CUG que si l’évaluation des permissions effective accorde l’accès. Un utilisateur non authentifié sera traité de manière égale et ne sera pas redirigé vers la connexion. |

>[!NOTE]
>
>La combinaison Exigence d’authentification = oui et Chemin de connexion = oui ne figure pas ci-dessus, car le chemin de connexion est un attribut facultatif associé à une exigence d’authentification. La spécification d’une propriété JCR avec ce nom, sans ajouter le type de mixin de définition n’a aucun effet et est ignorée par le gestionnaire correspondant.

## Composants et configuration OSGi {#osgi-components-and-configuration}

Cette section présente un aperçu des composants OSGi et des différentes options de configuration introduites avec la nouvelle mise en oeuvre de CUG.

Consultez également la documentation sur le mappage des CUG pour obtenir un mappage complet des options de configuration entre l’ancienne et la nouvelle mise en oeuvre.

### Autorisation : installation et configuration {#authorization-setup-and-configuration}

Les nouvelles parties relatives aux autorisations sont présentées dans la section **Autorisation des groupes d’utilisateurs fermés Oak** bundle ( `org.apache.jackrabbit.oak-authorization-cug`), qui fait partie de l’installation AEM par défaut. Le lot définit un modèle d’autorisation séparé destiné à être déployé comme un moyen supplémentaire de gérer l’accès en lecture.

#### Configuration de l’autorisation des groupes d’utilisateurs fermés {#setting-up-cug-authorization}

L’installation de l’autorisation de CUG est décrite en détail dans la [documentation Apache appropriée](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability). Par défaut, l’autorisation de CUG est déployée dans tous les modes d’exécution d’AEM. Les instructions étape par étape peuvent également être utilisées pour désactiver l’autorisation de CUG dans les installations qui nécessitent une configuration d’autorisation différente.

#### Configuration du filtre de référent {#configuring-the-referrer-filter}

Vous devez également configurer le [filtre de référent Sling](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) avec tous les noms d’hôtes pouvant être utilisés pour accéder à AEM ; par exemple, par l’intermédiaire du réseau de diffusion de contenu, de l’équilibreur de charge et de n’importe quel autre.

Si le filtre de référent n’est pas configuré, des erreurs, semblables à ce qui suit, s’affichent lorsqu’un utilisateur tente de se connecter à un site de CUG :

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### Caractéristiques des composants OSGi {#characteristics-of-osgi-components}

Les deux composants OSGi suivants ont été introduits pour définir les exigences d’authentification et spécifier des chemins de connexion dédiés :

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
   <td>Permet d’exclure de l’évaluation des CUG les entités dont les noms sont configurés.</td>
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

Les options de configuration disponibles associées au module d’autorisation des CUG sont répertoriées et décrites plus en détail à la section [Documentation Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration).

#### Exclusion des entités de sécurité de l’évaluation des CUG {#excluding-principals-from-cug-evaluation}

L’exemption de principaux de l’évaluation de CUG a été adoptée à partir de l’ancienne mise en œuvre. La nouvelle autorisation de CUG couvre cette fonction avec une interface dédiée nommée CugExclude. Apache Jackrabbit Oak 1.4 est fourni avec une implémentation par défaut qui exclut un ensemble fixe d’entités de sécurité et une implémentation étendue qui permet de configurer des noms de principal individuels. Ce dernier est configuré dans AEM instances de publication.

La valeur par défaut depuis AEM 6.3 empêche les entités de sécurité suivantes d’être affectées par les stratégies de CUG :

* entités d’administration (utilisateur administrateur, groupe administrateurs)
* Entités de sécurité des utilisateurs du service
* principal système interne du référentiel

Pour plus d’informations, reportez-vous au tableau de la section [Configuration par défaut depuis AEM 6.3](#default-configuration-since-aem) ci-dessous.

L’exclusion du groupe d’administrateurs peut être modifiée ou augmentée dans la console système dans la section de configuration de **Liste d’exclusion de CUG Apache Jackrabbit Oak**.

Vous pouvez également fournir et déployer une implémentation personnalisée de l’interface CugExclude afin d’ajuster l’ensemble des entités exclues en cas de besoins spécifiques. Consultez la documentation relative à l’[aspect enfichable des CUG](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) pour plus d’informations et pour obtenir un exemple de mise en œuvre.

### Authentification : installation et configuration {#authentication-setup-and-configuration}

Les nouveaux composants liés à l’authentification sont contenus dans la variable **Gestionnaire d’authentification Adobe Granite** bundle ( `com.adobe.granite.auth.authhandler` version 5.6.48). Ce lot fait partie de l’installation AEM par défaut.

Pour configurer le remplacement des exigences d’authentification pour la prise en charge des CUG obsolètes, certains composants OSGi doivent être présents et actifs dans une installation AEM donnée. Pour plus d’informations, voir **Caractéristiques des composants OSGi** ci-dessous

>[!NOTE]
>
>En raison de l’option de configuration obligatoire avec RequirementHandler, les parties liées à l’authentification ne sont actives que si la fonctionnalité a été activée en spécifiant un ensemble de chemins pris en charge. Avec une installation d’AEM standard, la fonction est désactivée en mode d’exécution de création et activée pour /content en mode d’exécution de publication.

**Caractéristiques des composants OSGi**

Les deux composants OSGi suivants ont été introduits pour définir les exigences d’authentification et spécifier des chemins de connexion dédiés :

* `com.adobe.granite.auth.requirement.impl.RequirementService`
* `com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler`

**com.adobe.granite.auth.requirements.impl.RequirementService**

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

Les parties liées à l’authentification de la réécriture des CUG ne sont fournies qu’avec une seule option de configuration associée au gestionnaire d’exigence d’authentification et de chemin de connexion Granite Adobe :

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

## Configuration par défaut depuis AEM 6.3 {#default-configuration-since-aem}

Les nouvelles installations d’AEM utiliseront par défaut les nouvelles mises en oeuvre à la fois pour les parties concernant l’autorisation et l’authentification de la fonction CUG. L’ancienne implémentation « Prise en charge des groupes d’utilisateurs fermés (CUG) par Adobe Granite » a été abandonnée et sera désactivée dans toutes les installations d’AEM. Les nouvelles implémentations seront activées à la place comme suit :

### Instances d’auteur {#author-instances}

| **« Configuration de CUG Apache Jackrabbit Oak »** | **Explication** |
|---|---|
| Chemins pris en charge `/content` | La gestion du contrôle d’accès pour les politiques de CUG est activée. |
| FALSE activée pour l’évaluation des CUG | L’évaluation des autorisations est désactivée. Les politiques de CUG n’ont aucun effet. |
| Classement | 200 | Consultez la documentation d’Oak. |

>[!NOTE]
>
>Aucune configuration pour **Liste d’exclusion de CUG Apache Jackrabbit Oak** et **Gestionnaire d’exigence d’authentification et de chemin de connexion Adobe Granite** est présente sur les instances de création par défaut.

### Instances de publication {#publish-instances}

| **« Configuration de CUG Apache Jackrabbit Oak »** | **Explication** |
|---|---|
| Chemins pris en charge `/content` | La gestion du contrôle d’accès pour les politiques de CUG est activée sous les chemins configurés. |
| Évaluation des CUG activée TRUE | L’évaluation des autorisations est activée sous les chemins configurés. Les politiques de CUG prennent effet `Session.save()`. |
| Classement | 200 | Consultez la documentation d’Oak. |

| **« Liste d’exclusion de CUG Apache Jackrabbit Oak »** | **Explication** |
|---|---|
| Administrateurs de noms principaux | Exclut le principal des administrateurs de l’évaluation des CUG. |

| **« Gestionnaire d’exigence d’authentification et de chemin de connexion Adobe Granite »** | **Explication** |
|---|---|
| Chemins pris en charge `/content` | Exigences d’authentification telles que définies dans le référentiel au moyen du type de mixin `granite:AuthenticationRequired` prend effet ci-dessous `/content` sous `Session.save()`. L’authentificateur Sling est mis à jour. L’ajout du type de mixin en dehors des chemins pris en charge est ignoré. |

## Désactivation de l’autorisation de CUG et de l’exigence d’authentification {#disabling-cug-authorization-and-authentication-requirement}

La nouvelle implémentation peut être complètement désactivée si une installation donnée n’utilise pas de CUG ou utilise des moyens différents pour l’authentification et l’autorisation.

### Désactiver l’autorisation de CUG {#disable-cug-authorization}

Consultez la [Plug-ins CUG](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) documentation pour plus d’informations sur la façon de supprimer le modèle d’autorisation de CUG de la configuration d’autorisation composite.

### Désactivation de l’exigence d’authentification {#disable-the-authentication-requirement}

Pour désactiver la prise en charge de l’exigence d’authentification fournie par le `granite.auth.authhandler` module , il suffit de supprimer la configuration associée à **Gestionnaire d’exigence d’authentification et de chemin de connexion Adobe Granite**.

>[!NOTE]
>
>Notez toutefois que la suppression de la configuration n’annule pas l’enregistrement du type de mixin, qui était toujours applicable aux noeuds sans effet.

## Interaction avec d’autres modules {#interaction-with-other-modules}

### API Apache Jackrabbit {#apache-jackrabbit-api}

Pour refléter le nouveau type de stratégie de contrôle d’accès utilisé par le modèle d’autorisation des CUG, l’API définie par Apache Jackrabbit a été étendue. Ainsi, la version 2.11.0 du module `jackrabbit-api` définit une nouvelle interface appelée `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`, qui s’étend à partir de `javax.jcr.security.AccessControlPolicy`.

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

Le mécanisme d’importation d’Apache Jackrabbit FileVault a été adapté pour traiter les politiques de contrôle d’accès de type `PrincipalSetPolicy`.

### Distribution de contenu Apache Sling {#apache-sling-content-distribution}

Voir ci-dessus [Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault) .

### Réplication Granite des Adobes {#adobe-granite-replication}

Le module de réplication a été légèrement ajusté pour pouvoir répliquer les stratégies de CUG entre différentes instances AEM :

* `DurboImportConfiguration.isImportAcl()` est interprété littéralement et affecte uniquement les politiques de contrôle d’accès mettant en œuvre `javax.jcr.security.AccessControlList`.

* `DurboImportTransformer` respecte uniquement cette configuration pour les vraies listes de contrôle d’accès.
* D’autres politiques telles que les instances de `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` créées par le modèle d’autorisation des CUG sont toujours répliquées, et l’option de configuration `DurboImportConfiguration.isImportAcl` () est ignorée.

Il existe une limite de réplication des politiques de CUG. Si une politique de CUG donnée est supprimée sans supprimer le type de nœud de mixin `rep:CugMixin,` correspondant, la suppression n’est pas répercutée lors de la réplication. Ce problème a été corrigé en supprimant toujours le mixin lors de la suppression d’une politique. La limitation peut néanmoins s’afficher si le type de mixin est ajouté manuellement.

### Gestionnaire d’authentification Adobe Granite {#adobe-granite-authentication-handler}

Le gestionnaire d’authentification **Adobe Granite HTTP Header Authentication Handler** fourni avec le lot `com.adobe.granite.auth.authhandler` contient une référence à l’interface `CugSupport` définie par le même module. Il est utilisé pour calculer le domaine dans certains cas, en se repliant sur le domaine configuré avec le gestionnaire.

Ceci a été adapté afin d’effectuer la référence à `CugSupport` facultatif afin d’assurer une compatibilité ascendante maximale si une configuration donnée décide de réactiver la mise en oeuvre obsolète. Pour les installations recourant à cette mise en œuvre, le domaine n’est pas extrait à partir de la mise en œuvre CUG, mais s’affiche toujours tel que défini auprès du gestionnaire d’authentification **Adobe Granite HTTP Header Authentication Handler**.

>[!NOTE]
>
>Par défaut, le **Gestionnaire d’authentification d’en-tête HTTP Adobe Granite** n’est configuré que dans le mode d’exécution de publication avec l’option « Désactiver la page de connexion » (`auth.http.nologin`) activée.

### AEM LiveCopy {#aem-livecopy}

La configuration des CUG en accord avec LiveCopy est représentée dans le référentiel par l’ajout d’un nœud et d’une propriété supplémentaires comme suit :

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

Ces deux éléments sont créés sous `cq:Page`. Avec la conception actuelle, le MSM ne gère que les nœuds et les propriétés sous le nœud `cq:PageContent` (`jcr:content`).

Par conséquent, les groupes CUG ne peuvent pas être déployés sur des Live Copies à partir de plans directeurs. Planifiez la configuration de la Live Copy.

## Modifications avec la nouvelle mise en oeuvre du groupe d’utilisateurs fermé {#changes-with-the-new-cug-implementation}

Cette section a pour but de fournir un aperçu des modifications apportées à la fonction CUG et une comparaison entre l’ancienne et la nouvelle mise en oeuvre. Il répertorie les modifications affectant la configuration de la prise en charge des CUG et décrit comment et par qui les CUG sont gérés dans le contenu du référentiel.

### Différences dans l’installation et la configuration des CUG {#differences-in-cug-setup-and-configuration}

Composant OSGi obsolète **Prise en charge du groupe d’utilisateurs fermé Adobe Granite** ( `com.day.cq.auth.impl.cug.CugSupportImpl`) a été remplacé par de nouveaux composants afin de pouvoir gérer séparément les parties liées à l’autorisation et à l’authentification de l’ancienne fonctionnalité de CUG.

## Différences dans la gestion des CUG au sein du référentiel de contenu {#differences-in-managing-cugs-in-the-repository-content}

Les sections suivantes décrivent les différences entre l’ancienne et la nouvelle mise en œuvre du point de vue de l’implémentation et de la sécurité. Bien que la nouvelle mise en oeuvre vise à fournir les mêmes fonctionnalités, des modifications subtiles sont importantes à connaître lors de l’utilisation du nouveau CUG.

### Différences En Ce Qui Concerne L’Autorisation {#differences-with-regards-to-authorization}

Les principales différences du point de vue des autorisations sont résumées dans la liste ci-dessous :

**Contenu du contrôle d’accès dédié pour les groupes d’utilisateurs fermés**

Dans l’ancienne mise en œuvre, le modèle d’autorisation par défaut était utilisé pour manipuler les politiques de liste de contrôle d’accès sur l’instance de publication, remplaçant tous les ACE existants par la configuration requise par le CUG. Cela a été déclenché en écrivant des propriétés JCR résiduelles régulières qui ont été interprétées lors de la publication.

Avec la nouvelle mise en oeuvre, la configuration du contrôle d’accès du modèle d’autorisation par défaut n’est pas affectée par les CUG créés, modifiés ou supprimés. À la place, un nouveau type de politique nommé `PrincipalSetPolicy` est appliqué en tant que contenu de contrôle d’accès supplémentaire sur le nœud cible. Cette politique supplémentaire est placée en tant qu’enfant du nœud cible et doit être une sœur du nœud de politique par défaut (s’il existe).

**Modification des stratégies de CUG dans la gestion du contrôle d’accès**

Cette transition des propriétés JCR résiduelles vers une politique de contrôle d’accès dédiée a un impact sur les permissions requises pour créer ou modifier le composant d’autorisation de la fonction CUG. Puisqu’il s’agit d’une modification du contenu de contrôle d’accès, il nécessite `jcr:readAccessControl` et `jcr:modifyAccessControl` droits à écrire dans le référentiel. Par conséquent, seuls les auteurs de contenu autorisés à modifier le contenu du contrôle d’accès d’une page peuvent configurer ou modifier ce contenu. Cela contraste avec l’ancienne mise en œuvre où la possibilité d’écrire des propriétés JCR standard suffisait, entraînant la réaffectation des privilèges.

**Noeud cible défini par la stratégie**

Il est attendu que les politiques de CUG sont créées au niveau du nœud JCR définissant la sous-arborescence dont l’accès en lecture est à restreindre. Il est probable qu’il s’agisse d’une page AEM au cas où le CUG affecterait l’ensemble de l’arborescence.

Notez que le fait de placer la politique de CUG uniquement au nœud jcr:content situé sous une page donnée limite l’accès au contenu s.str d’une page donnée, mais n’aura aucun effet sur les pages enfants ou frères. Il peut s’agir d’un cas d’utilisation valide. Il est possible d’y parvenir avec un éditeur de référentiel qui permet d’appliquer un contenu d’accès affiné. Cependant, elle contraste avec l’ancienne mise en oeuvre où le placement d’une propriété cq:cugEnabled sur le noeud jcr:content a été mappé en interne au noeud de page. Ce mappage n’est plus effectué.

**Évaluation des autorisations avec des stratégies de CUG**

Le passage de l’ancienne prise en charge des CUG à un modèle d’autorisation supplémentaire, modifie la façon dont les permissions de lecture en vigueur sont évaluées. Comme indiqué dans la [documentation relative à Jackrabbit](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html), un principal spécifique autorisé à afficher `CUGcontent` n’obtient l’accès en lecture que si l’évaluation des autorisations de tous les modèles configurés dans le référentiel Oak lui accorde l’accès en lecture.

En d’autres termes, pour l’évaluation des permissions en vigueur, à la fois `CUGPolicy` et les entrées de contrôle d’accès par défaut sont pris en compte, et l’accès en lecture sur le contenu CUG est uniquement autorisé s’il est accordé par les deux types de politiques. Dans une installation de publication AEM par défaut où l’accès en lecture à l’arborescence `/content` complète est accordé à tout le monde, l’effet des politiques de CUG est le même que celui de l’ancienne mise en œuvre.

**Évaluation à la demande**

Le modèle d’autorisation des CUG permet d’activer individuellement la gestion du contrôle d’accès et l’évaluation des autorisations :

* la gestion du contrôle d’accès est activée si le module comporte un ou plusieurs chemins pris en charge où des CUG peuvent être créés.
* l’évaluation des autorisations n’est activée que si l’option **Évaluation des CUG activée** est également cochée.

Dans l’évaluation des politiques de CUG de la nouvelle configuration par défaut d’AEM, elle est activée uniquement avec le mode d’exécution de publication. Consultez les informations relatives à la [configuration par défaut depuis AEM 6.3](#default-configuration-since-aem) pour en savoir plus. Cela peut être vérifié en comparant les politiques en vigueur pour un chemin donné vers les politiques stockées dans le contenu. Les politiques en vigueur sont affichées uniquement dans le cas où l’évaluation des permissions est activée pour les CUG.

Comme expliqué plus haut, les politiques de contrôle d’accès de CUG sont désormais toujours stockées dans le contenu, mais l’évaluation des permissions en vigueur découlant de ces politiques ne sera imposée que si l’**évaluation des CUG activée** est sélectionnée dans la console système au niveau de la configuration des CUG Apache Jackrabbit Oak **.** Par défaut, elle est uniquement activée avec le mode d’exécution de publication.

### Différences En Matière D’Authentification {#differences-with-regards-to-authentication}

Les différences concernant l’authentification sont décrites ci-dessous.

#### Type de mixin dédié pour l’exigence d’authentification {#dedicated-mixin-type-for-authentication-requirement}

Dans l’ancienne mise en œuvre, les aspects d’autorisation et d’authentification d’un CUG étaient tous deux déclenchés par une seule propriété JCR (`cq:cugEnabled`). En ce qui concerne l’authentification, il en résultait une liste mise à jour des exigences d’authentification telles que stockées avec la mise en œuvre de l’authentificateur Apache Sling. Avec la nouvelle mise en œuvre, le même résultat est obtenu en marquant le nœud cible avec un type spécial de mixin (`granite:AuthenticationRequired`).

#### Propriété d’exclusion d’un chemin de connexion {#property-for-excluding-login-path}

Le type de mixin définit une propriété unique et facultative appelée `granite:loginPath`, qui correspond essentiellement à la propriété `cq:cugLoginPage`. Contrairement à la mise en œuvre précédente, la propriété de chemin de connexion n’est respectée que si son type de nœud d’instruction est le mixin indiqué. L’ajout d’une propriété portant ce nom sans définir le type de mixin n’aura aucun effet et ni une nouvelle exigence ni une exclusion pour le chemin de connexion ne seront signalées à l’authentificateur.

#### Privilège Pour L’Exigence D’Authentification {#privilege-for-authentication-requirement}

L’ajout ou la suppression d’un type de mixin requiert l’attribution du privilège `jcr:nodeTypeManagement`. Dans la mise en œuvre précédente, le privilège `jcr:modifyProperties` était utilisé pour modifier la propriété résiduelle.

En ce qui concerne `granite:loginPath` est concerné le même privilège est requis pour ajouter, modifier ou supprimer la propriété.

#### Noeud cible défini par le type de mixin {#target-node-defined-by-mixin-type}

Il est attendu que les exigences d’authentification sont créées au niveau du nœud JCR définissant la sous-arborescence pour laquelle la connexion doit être forcée. Il est probable qu’il s’agisse d’une page AEM au cas où le CUG devrait affecter l’ensemble de l’arborescence et que l’interface utilisateur de la nouvelle mise en oeuvre ajoutera par conséquent le type de mixin auth-required sur le noeud de page.

Le fait de placer la stratégie de CUG uniquement au niveau du noeud jcr:content situé sous une page donnée limite uniquement l’accès au contenu, mais n’aura aucune incidence sur le noeud de page lui-même ni sur les pages enfants.

Il peut s’agir d’un scénario valide et possible avec un éditeur de référentiel qui permet de placer le mixin au niveau de n’importe quel nœud. Toutefois, le comportement contraste avec l’ancienne mise en œuvre où le placement d’une propriété cq:cugEnabled ou cq:cugLoginPage sur le nœud jcr:content était remis en correspondance en interne sur le nœud de page. Ce mappage n’est plus effectué.

#### Chemins pris en charge configurés {#configured-supported-paths}

Le type de mixin `granite:AuthenticationRequired` et la propriété granite:loginPath sont respectés uniquement dans la portée définie par le jeu de l’option de configuration **Chemins pris en charge** présent avec le **Gestionnaire d’exigence d’authentification et de chemin de connexion Adobe Granite**. Si aucun chemin n’est spécifié, la fonction d’exigence d’authentification est complètement désactivée. Dans ce cas, ni le type de mixin ni la propriété ne prennent effet lorsqu’ils sont ajoutés ou définis sur un nœud JCR donné.

### Mappage du contenu JCR, des services OSGi et des configurations {#mapping-of-jcr-content-osgi-services-and-configurations}

Le document ci-dessous fournit un mappage complet des services OSGi, des configurations et du contenu du référentiel entre l’ancienne et la nouvelle mise en oeuvre.

Mise en correspondance de CUG depuis AEM 6.3

[Obtenir le fichier](assets/cug-mapping.pdf)

## Mettre à niveau le CUG {#upgrade-cug}

### Installations existantes utilisant un groupe d’utilisateurs fermé obsolète {#existing-installations-using-the-deprecated-cug}

L’ancienne mise en œuvre de prise en charge des CUG a été abandonnée et sera supprimée dans les futures versions. Il est recommandé de passer aux nouvelles implémentations lors de la mise à niveau à partir de versions antérieures à AEM 6.3.

Pour les installations AEM mises à niveau, il est important de s’assurer qu’une seule mise en œuvre CUG est activée. La combinaison de la nouvelle prise en charge des CUG et de l’ancienne prise en charge des CUG obsolètes n’est pas testée et risque de provoquer un comportement indésirable :

* collisions dans l’authentificateur Sling en ce qui concerne les exigences d’authentification
* refusé l’accès en lecture lorsque la configuration ACL associée à l’ancien CUG entre en conflit avec une nouvelle stratégie de CUG.

### Migration d’un contenu de CGU existant {#migrating-existing-cug-content}

Adobe fournit un outil pour la migration vers la nouvelle mise en oeuvre de CUG. Pour l’utiliser, procédez comme suit :

1. Accédez à `https://<serveraddress>:<serverport>/system/console/cug-migration` pour accéder à l’outil.
1. Saisissez le chemin racine pour lequel vous souhaitez vérifier les CUG, puis appuyez sur la touche **Exécution à sec** bouton . Cela permet de rechercher les CUG pouvant être convertis à l’emplacement sélectionné.
1. Une fois que vous avez consulté les résultats, appuyez sur le bouton **Effectuer la migration** pour migrer vers la nouvelle mise en œuvre.

>[!NOTE]
>
>Si vous rencontrez des difficultés, il est possible de configurer un enregistreur spécifique au niveau **DEBUG** sur `com.day.cq.auth.impl.cug` pour obtenir la sortie de l’outil de migration. Consultez la rubrique [Connexion](/help/sites-deploying/configure-logging.md) pour en savoir plus sur la procédure à suivre.
