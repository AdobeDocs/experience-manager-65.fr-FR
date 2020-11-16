---
title: Groupes d’utilisateurs fermés dans AEM
seo-title: Groupes d’utilisateurs fermés dans AEM
description: Découvrez les groupes d’utilisateurs fermés dans AEM.
seo-description: Découvrez les groupes d’utilisateurs fermés dans AEM.
uuid: 83396163-86ce-406b-b797-2457ed975ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: a2bd7045-970f-4245-ad5d-a272a654df0a
docset: aem65
translation-type: tm+mt
source-git-commit: 2142df4f7579e052e18879b437fc43911010b475
workflow-type: tm+mt
source-wordcount: '6890'
ht-degree: 61%

---


# Groupes d’utilisateurs fermés dans AEM{#closed-user-groups-in-aem}

## Présentation {#introduction}

Depuis AEM 6.3, une nouvelle mise en œuvre de groupe d’utilisateurs fermé a été mise en place dans le but de résoudre les problèmes de performances, d’évolutivité et de sécurité rencontrés dans la mise en œuvre existante.

>[!NOTE]
>
>Par souci de simplicité, l’abréviation CUG (Closer User Group) sera utilisée dans cette documentation pour se référer aux groupes d’utilisateurs fermés.

L’objectif de la nouvelle mise en oeuvre est de couvrir les fonctionnalités existantes lorsque cela est nécessaire tout en traitant les problèmes et les limitations de conception des versions antérieures. Le résultat est une nouvelle conception de CUG avec les caractéristiques suivantes :

* Séparation claire des éléments d’authentification et d’autorisation, qui peuvent être utilisés séparément ou conjointement
* Modèle d’autorisation dédié afin de refléter l’accès en lecture restreint aux arborescences de CUG configurées sans interférer avec d’autres exigences de permission et de configuration de contrôle d’accès
* Séparation entre la configuration par contrôle d&#39;accès de l’accès en lecture restreint, qui est généralement nécessaire sur les instances de création, et l’évaluation des autorisations qui n’est généralement souhaitée que lors de la publication ;
* Modification de l’accès en lecture restreint sans réaffectation de privilège
* Extension de type de nœud dédiée pour marquer l’exigence d’authentification
* Chemin de connexion facultatif associé à l’exigence d’authentification

### La nouvelle mise en œuvre personnalisée de groupe d’utilisateurs {#the-new-custom-user-group-implementation}

Dans le contexte d’AEM, un CUG comprend les étapes suivantes :

* Restreindre l’accès en lecture sur l’arborescence qui doit être protégée et uniquement autoriser la lecture pour les entités de sécurité qui sont soit répertoriées avec une instance de données CUG spécifique, soit exclues de l’évaluation des CUG. On parle d’élément d’**autorisation**.
* Renforcez l’authentification sur une arborescence donnée et spécifiez éventuellement une page de connexion dédiée pour cette arborescence qui est ensuite exclue. On parle d’élément d’**authentification**.

La nouvelle mise en œuvre a été conçue pour distinguer les éléments d’authentification des éléments d’autorisation. Depuis AEM 6.3, il est possible de restreindre l’accès en lecture sans ajouter explicitement une exigence d’authentification. Par exemple, si une instance donnée requiert une authentification ou si une arborescence donnée se trouve déjà dans une sous-arborescence nécessitant une authentification.

De même, une arborescence donnée peut être marquée avec une exigence d&#39;authentification sans modifier la configuration des autorisations effectives. Les combinaisons et les résultats sont répertoriés dans la section [Combinaison des stratégies de combinaison de CUG et de l’exigence d’authentification](/help/sites-administering/closed-user-groups.md#combining-cug-policies-and-the-authentication-requirement).

## Présentation {#overview}

### Autorisation : restriction de l’accès en lecture {#authorization-restricting-read-access}

La fonctionnalité clé d’un CUG est de restreindre l’accès en lecture sur une arborescence donnée dans le référentiel de contenu pour tous à l’exception des entités de sécurité sélectionnées. Au lieu de manipuler à la volée le contenu du contrôle d’accès par défaut, la nouvelle mise en œuvre adopte une approche différente en définissant un type dédié de stratégie de contrôle d’accès qui représente un CUG.

#### Stratégie de contrôle d’accès pour CUG {#access-control-policy-for-cug}

Ce nouveau type de stratégie présente les caractéristiques suivantes :

* stratégie de contrôle d&#39;accès de type org.apache.jackrabbit.api.security.authorized.PrincipalSetPolicy (définie par l&#39;API Apache Jackrabbit);
* PrincipalSetPolicy accorde des privilèges à un ensemble modifiable de entités ;
* Les privilèges accordés et le domaine de la stratégie constituent des détails de la mise en œuvre.

L&#39;implémentation de PrincipalSetPolicy utilisée pour représenter les CUG en outre définit que :

* Les stratégies de CUG accordent l’accès en lecture aux éléments JCR standard (par exemple, le contenu de contrôle d’accès est exclu).
* La portée est définie par le nœud dont l’accès est contrôlé et qui contient la stratégie de CUG.
* Les stratégies de CUG peuvent être imbriquées : un CUG imbriqué commence un nouveau CUG sans hériter de l’ensemble principal du CUG « parent ».
* L’effet de la stratégie, si l’évaluation est activée, est hérité par la sous-arborescence entière jusqu’au prochain CUG imbriqué.

Ces stratégies CUG sont déployées sur une instance AEM par le biais d’un module d’autorisation distinct appelé oak-autorisation-cug. Ce module est fourni avec ses propres fonctions d’évaluation des permissions et de gestion du contrôle d’accès. En d’autres termes, la configuration par défaut d’AEM est livrée avec une configuration de référentiel de contenu Oak qui combine plusieurs mécanismes d’autorisation. For more info, see [this page on the Apache Oak Documentation](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html).

Dans cette configuration composite, un nouveau CUG ne remplace pas le contenu de contrôle d&#39;accès existant attaché au noeud de cible, mais il est conçu pour être un supplément qui peut également être supprimé ultérieurement sans affecter le contrôle d&#39;accès d&#39;origine, qui par défaut dans AEM serait une liste de contrôle d&#39;accès.

Contrairement à la mise en œuvre précédente, les nouvelles stratégies de CUG sont systématiquement reconnues et traitées comme contenu de contrôle d’accès. Cela signifie qu’elles sont créées et modifiées à l’aide de l’API de gestion du contrôle d’accès JCR. For more info, see the [Managing CUG Policies](#managing-cug-policies) section.

#### Évaluation des permissions des stratégies de CUG {#permission-evaluation-of-cug-policies}

Outre la gestion de contrôle d’accès dédiée pour les CUG, le nouveau modèle d’autorisation permet d’activer de manière conditionnelle l’évaluation des permissions pour ses stratégies. Cette opération permet de configurer des stratégies de CUG dans un environnement d’évaluation, et permet uniquement l’évaluation des permissions après réplication sur l’environnement de production.

L’évaluation des permissions pour les stratégies de CUG et l’interaction avec le modèle d’autorisation par défaut ou tout modèle supplémentaire suit le modèle destiné aux mécanismes d’autorisation multiples dans Apache Jackrabbit Oak : un jeu de permissions donné est accordé si et uniquement si tous les modèles accordent l’accès. See [this page](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html) for more details.

Les caractéristiques suivantes s’appliquent à l’évaluation des permissions associée au modèle d’autorisation conçu pour gérer et évaluer les stratégies de CUG :

* Elle gère uniquement les permissions de lecture pour les nœuds et les propriétés standard, mais sans lire le contenu du contrôle d’accès.
* Il ne gère pas les autorisations d’écriture ni aucun type d’autorisation requis pour modifier le contenu JCR protégé (contrôle d&#39;accès, informations de type de noeud, gestion de version, verrouillage ou gestion d’utilisateur, entre autres); Ces autorisations ne sont pas affectées par une stratégie CUG et ne seront pas évaluées par le modèle d’autorisation associé. Ces permissions sont accordées en fonction des autres modèles configurés dans la configuration de sécurité.

L&#39;effet d&#39;une seule politique du CUG sur l&#39;évaluation des autorisations peut être résumé comme suit :

* L’accès en lecture est refusé pour tous, à l’exception des personnes contenant des entités de sécurité exclues ou des entités de sécurité répertoriées dans la stratégie.
* La stratégie prend effet sur le noeud contrôlé d&#39;accès qui détient la stratégie et ses propriétés ;
* L&#39;effet est en outre hérité vers le bas de la hiérarchie, c&#39;est-à-dire l&#39;arborescence d&#39;éléments définie par le noeud contrôlé d&#39;accès ;
* Toutefois, elle n&#39;affecte ni les frères ni les ancêtres du noeud contrôlé d&#39;accès ;
* L’héritage d’un CUG donné s’arrête au niveau d’un CUG imbriqué.

#### Bonnes pratiques {#best-practices}

Les meilleures pratiques suivantes doivent être prises en compte pour définir l’accès en lecture restreint par l’intermédiaire de CUG :

* Déterminez si le CUG dont vous avez besoin est destiné à limiter l’accès en lecture ou s’il correspond à une exigence d’authentification. Dans le cas de la seconde ou s&#39;il y a un besoin des deux, consultez la section sur les meilleures pratiques pour plus de détails sur l&#39;exigence d&#39;authentification
* Créez un modèle de menace portant sur les données ou le contenu qui doivent être protégés afin d’identifier les limites des menaces et d’obtenir une vision claire de la sensibilité des données et des rôles associés à l’accès autorisé.
* Modélisez le contenu de référentiel et les CUG en gardant à l’esprit les aspects relatifs à l’autorisation de base et les meilleures pratiques :

   * N’oubliez pas que la permission de lecture est uniquement accordée si un CUG donné et l’évaluation des autres modules déployés dans la configuration permettent à une personne spécifique de lire un élément de référentiel donné.
   * Évitez de créer des CUG redondants où l’accès en lecture est déjà restreint par d’autres modules d’autorisation.
   * Un besoin excessif de CUG imbriqués peut mettre en évidence des problèmes de conception du contenu.
   * Un besoin très excessif de CUG (par exemple, sur chaque page) peut indiquer la nécessité d’un modèle d’autorisation personnalisé potentiellement mieux adapté aux besoins de sécurité de l’application et du contenu en question.

* Limitez les chemins pris en charge pour les stratégies de CUG à un petit nombre d’arborescences dans le référentiel afin d’optimiser les performances. Par exemple, n’autorisez que les CUG situés sous le noeud /content comme valeur par défaut depuis AEM 6.3.
* Les stratégies de CUG sont conçues pour autoriser l’accès en lecture à un petit ensemble d’entités de sécurité. La nécessité d’un nombre très important d’entités de sécurité peut mettre en évidence des problèmes dans la conception du contenu ou de l’application et devrait être reconsidérée.

### Authentification : définition de l’exigence d’authentification {#authentication-defining-the-auth-requirement}

Les composants liés à l’authentification de la fonction CUG permettent de marquer les arborescences nécessitant une authentification et éventuellement de spécifier une page de connexion dédiée. In accordance to the previous version, the new implementation allows to mark trees that require authentication in the content repository and conditionally enable synchronization with the `Sling org.apache.sling.api.auth.Authenticator`responsible for ultimately enforcing the requirement and redirecting to a login resource.

Ces exigences sont enregistrées auprès de l’authentificateur au moyen d’un service OSGi qui fournit la propriété d’enregistrement `sling.auth.requirements`. Ces propriétés sont ensuite utilisées pour étendre les exigences d’authentification de façon dynamique. Pour plus de détails, consulter la [documentation de Sling](https://sling.apache.org/apidocs/sling7/org/apache/sling/auth/core/AuthConstants.html#AUTH_REQUIREMENTS).

#### Définition de l’exigence d’authentification avec un type de mixin dédié {#defining-the-authentication-requirement-with-a-dedicated-mixin-type}

For security reasons the new implementation replaces the usage of a residual JCR property by a dedicated mixin type called `granite:AuthenticationRequired`, which defines a single optional property of type STRING for the login path `granite:loginPath`. Seules les modifications du contenu liées à ce type de mixin entraînent la mise à jour des exigences enregistrées auprès de l’authentificateur Apache Sling. The modifications are tracked upon persisting any transient modifications and thus require a `javax.jcr.Session.save()` call to become effective.

The same applies for the `granite:loginPath` property. Elle ne sera respectée que si elle est définie par le type de mixin lié aux exigences d&#39;auth. Ajouter une propriété résiduelle portant ce nom même sur un noeud JCR non structuré n’affichera pas l’effet souhaité et la propriété sera ignorée par le gestionnaire responsable de la mise à jour de l’enregistrement OSGi.

>[!NOTE]
>
>La définition de la propriété de chemin de connexion est facultative et elle est uniquement nécessaire si l’arborescence nécessitant une authentification ne peut se replier sur la page de connexion par défaut ou héritée. Voir [Évaluation du chemin de connexion](/help/sites-administering/closed-user-groups.md#evaluation-of-login-path) ci-dessous.

#### Enregistrement de l’exigence d’authentification et du chemin de connexion avec l’authentificateur Sling {#registering-the-authentication-requirement-and-login-path-with-the-sling-authenticator}

Étant donné que ce type d’exigence d’authentification doit être limité à certains modes d’exécution et à un petit sous-ensemble d’arbres dans le référentiel de contenu, le suivi du type de mixin d’exigence et des propriétés de chemin d’accès de connexion est conditionnel et lié à une configuration correspondante qui définit les chemins pris en charge (voir Options de configuration ci-dessous). Par conséquent, seules les modifications dans la portée de ces chemins pris en charge déclenchent une mise à jour de l’enregistrement OSGi ; dans les autres cas, le type de mixin et la propriété sont tous deux ignorés.

La configuration AEM par défaut utilise désormais cette configuration en permettant de définir le mixin en mode d’exécution Auteur, mais n’a d’effet que lors de la réplication sur l’instance de publication. See [this page](https://sling.apache.org/documentation/the-sling-engine/authentication/authenticationframework.html) for details how Sling enforces the authentication requirement.

Adding the `granite:AuthenticationRequired` mixin type within the configured supported paths will cause the OSGi registration of the responsible handler to be updated containing an new, additional entry with the `sling.auth.requirements` property. If a given authentication requirement specifies the optional `granite:loginPath` property, the value is additionally registered with the Authenticator with a &#39;-&#39; prefix in order to be excluded from authentication requirement.

#### Evaluation and Inheritance of the Authentication Requirement {#evaluation-and-inheritance-of-the-authentication-requirement}

Il est attendu que les exigences d’authentification d’Apache Sling soient héritées dans la hiérarchie de page ou de nœud. Les détails de l’héritage et l’évaluation des exigences d’authentification, comme l’ordre et la priorité, sont considérés comme un détail de mise en œuvre et ne seront pas décrits dans cet article.

#### Évaluation du chemin de connexion {#evaluation-of-login-path}

The evaluation of the login path and redirect to the corresponding resource upon authentication is currently an implementation detail of the Adobe Granite Login Selector Authentication Handler ( `com.day.cq.auth.impl.LoginSelectorHandler`), which is an Apache Sling AuthenticationHandler configured with AEM by default.

Upon calling `AuthenticationHandler.requestCredentials` this handler makes an attempt to determine the mapping login page to which the user will be redirected. Cela inclut les étapes suivantes :

* Différencier entre l’expiration d’un mot de passe et le besoin d’une connexion standard comme motif de redirection.
* En cas de connexion standard, tester si un chemin de connexion peut être obtenu dans l’ordre suivant :

   * from the LoginPathProvider as implemented by the new `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * à partir de l’ancienne mise en œuvre CUG obsolète ;
   * from the Login Page Mappings, as defined with the `LoginSelectorHandler`,
   * and finally, fallback to the Default Login Page, as defined with the `LoginSelectorHandler`.

* Dès qu’un chemin de connexion valide est obtenu par les appels répertoriés ci-dessus, la requête de l’utilisateur est redirigée vers cette page.

The target of this documentation is the evaluation of the login path as exposed by the internal `LoginPathProvider` interface. La mise en œuvre fournie depuis AEM 6.3 se comporte comme suit :

* L’enregistrement des chemins de connexion dépend de la distinction entre l’expiration d’un mot de passe expiré et le besoin d’une connexion standard comme motif de la redirection.
* En cas de connexion standard, tester si un chemin de connexion peut être obtenu dans l’ordre suivant :

   * from the `LoginPathProvider` as implemented by the new `com.adobe.granite.auth.requirement.impl.RequirementService`,
   * à partir de l’ancienne mise en œuvre CUG obsolète ;
   * from the Login Page Mappings as defined with the `LoginSelectorHandler`,
   * and finally fallback to the Default Login Page as defined with the `LoginSelectorHandler`.

* Dès qu’un chemin de connexion valide est obtenu par les appels répertoriés ci-dessus, la requête de l’utilisateur est redirigée vers cette page.

The `LoginPathProvider` as implemented by the new auth-requirement support in Granite exposes login paths as defined by the `granite:loginPath` properties, which in turn are defined by the mixin type as described above. La mise en correspondance du chemin de ressource contenant le chemin de connexion et la valeur de la propriété elle-même est conservée en mémoire et est évaluée afin de trouver un chemin de connexion approprié pour d’autres nœuds dans la hiérarchie.

>[!NOTE]
>
>L’évaluation est effectuée uniquement pour les requêtes liées aux ressources qui se trouvent dans les chemins pris en charge configurés. Pour toute autre requête, les autres façons de déterminer le chemin de connexion seront évaluées.

#### Bonnes pratiques {#best-practices-1}

Les meilleures pratiques suivantes doivent être prises en compte lors de la définition des exigences d’authentification :

* Il est préférable de ne pas imbriquer les exigences d’authentification : le fait de placer un marqueur d’exigence d’authentification unique au début d’une arborescence devrait suffire et est hérité par toute la sous-arborescence définie par le nœud cible. Tout exigence supplémentaire d’authentification dans cette arborescence doit être considérée comme redondante et peut entraîner des problèmes de performances lors de l’évaluation de l’exigence d’authentification dans Apache Sling. Grâce à la séparation des domaines de CUG liés à l’autorisation et à l’authentification, il est possible de restreindre l’accès en lecture au moyen d’un CUG ou d’autres types de stratégies, tout en appliquant l’authentification pour l’arborescence entière.
* Le contenu du référentiel de modèles de sorte que les exigences d&#39;authentification s&#39;appliquent à l&#39;arborescence entière sans qu&#39;il soit nécessaire d&#39;exclure à nouveau les sous-arborescences imbriquées de cette exigence.
* Pour éviter de spécifier et d’enregistrer ensuite des chemins de connexion redondants :

   * dépendent de l&#39;héritage et évitent de définir des chemins de connexion imbriqués,
   * Ne définissez pas le chemin de connexion facultatif sur une valeur qui correspond à la valeur par défaut ou à la valeur héritée.
   * Les développeurs d’applications doivent identifier les mises en correspondance de connexion qui doivent être configurées dans les fonctions de chemin de connexion globales (par défaut et mise en correspondance) associées à `LoginSelectorHandler`.

## Représentation dans le référentiel {#representation-in-the-repository}

### Représentation d’une stratégie de CUG dans le référentiel {#cug-policy-representation-in-the-repository}

La documentation de Oak explique comment les nouvelles stratégies CUG sont reflétées dans le contenu du référentiel. Pour plus d’informations, consulter [cette page](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#Representation_in_the_Repository).

### Exigence d’authentification dans le référentiel {#authentication-requirement-in-the-repository}

La nécessité d’une authentification distincte est reflétée dans le contenu du référentiel avec un type de noeud de mixin dédié placé au noeud de cible. Le type de mixin définit une propriété facultative de façon à spécifier une page de connexion dédiée pour l’arborescence définie par le nœud cible.

La page associée au chemin de connexion peut être placée à l’intérieur ou à l’extérieur de cette arborescence. Elle est exclue de l’exigence d’authentification.

```java
[granite:AuthenticationRequired]
      mixin
      - granite:loginPath (STRING)
```

## Gestion des stratégies de CUG et de l’exigence d’authentification {#managing-cug-policies-and-authentication-requirement}

### Gestion des stratégies de CUG {#managing-cug-policies}

The new type of access control policies to restrict read access for a CUG is managed using the JCR access control management API and follows the mechanisms described with the [JCR 2.0 specification](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html).

#### Définition d’une nouvelle stratégie de CUG {#set-a-new-cug-policy}

Code pour appliquer une nouvelle stratégie de CUG à un nœud qui n’avait pas de CUG. Please note that `getApplicablePolicies` will only return new policies that have not been set before. À la fin, la stratégie a besoin d’être mise à jour, et les modifications doivent persister.

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
   log.debug("no applicable policy"); // path not supported or no applicable policy (e.g.
                                                   // the policy was set before)
   return;
}

cugPolicy.addPrincipals(toAdd1, toAdd2);
cugPolicy.removePrincipals(toRemove));

acMgr.setPolicy(path, cugPolicy); // as of this step the policy can be edited/removed
session.save();
```

#### Modification d’une stratégie de CUG existante {#edit-an-existing-cug-policy}

Les étapes suivantes sont nécessaires pour modifier une stratégie de CUG existante. Please note that the modified policy needs to written back and changes needs to be persisted using `javax.jcr.Session.save()`.

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

### Récupération des stratégies de CUG effectives {#retrieve-effective-cug-policies}

La gestion du contrôle d’accès JCR définit une méthode du meilleur effort pour récupérer les stratégies qui prennent effet à un chemin donné. Due to the fact that evaluation of CUG policies is conditional and depends on the corresponding configuration to be enabled, calling `getEffectivePolicies` is a convenient way to verify if a given CUG policy is taking effect in a given installation.

>[!NOTE]
>
>Please note the difference between `getEffectivePolicies` and the subsequent code example that walks up the hierarchy to find if a given path is already part of an existing CUG.

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

Recherche de tous les CUG imbriqués qui ont été définis à un chemin donné, qu’ils soient ou non effectifs. Pour plus d’informations, voir la section [Options de configuration](/help/sites-administering/closed-user-groups.md#configuration-options).

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

#### Gestion des stratégies de CUG par une entité de sécurité {#managing-cug-policies-by-pincipal}

The extensions defined by `JackrabbitAccessControlManager` that allow to edit access control policies by principal are not implemented with CUG access control management, as by definition a CUG policy always affects all principals: those listed with the `PrincipalSetPolicy` are being granted read access while all other principals will be prevented to read content in the tree defined by the target node.

Les méthodes correspondantes renvoient toujours un tableau de stratégie vide, mais sans renvoyer d’exceptions.

### Gestion de l’exigence d’authentification {#managing-the-authentication-requirement}

La création, la modification ou la suppression d’une nouvelle exigence d’authentification s’effectue en modifiant le type de noeud effectif du noeud de cible. La propriété de chemin de connexion facultatif peut ensuite être écrite à l’aide de l’API JCR.

>[!NOTE]
>
>The modifications to a given target node mentioned above will only be reflected on the Apache Sling Authenticator if the `RequirementHandler` has been configured and the target is contained in the trees defined by the supported paths (see section Configuration Options).
>
>Pour plus d’informations, voir [Affectation de types]de noeuds mixtes (https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.10.3éation de types de noeuds mixtes) et [Ajoute de noeuds et définition de propriétés](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.4éation de noeuds et définition de propriétés).

#### Ajout d’une nouvelle exigence d’authentification {#adding-a-new-auth-requirement}

Les étapes de création d’une exigence d’authentification sont détaillées ci-dessous. Note that the requirement will only be registered with the Apache Sling Authenticator if the `RequirementHandler` has been configured for the tree containing the target node.

```java
Node targetNode = [...]

targetNode.addMixin("granite:AuthenticationRequired");
session.save();
```

#### Ajout d’une nouvelle exigence d’authentification avec un chemin de connexion {#add-a-new-auth-requirement-with-login-path}

Procédure à suivre pour créer une exigence d’authentification incluant un chemin de connexion. Note, that the requirement and the exclusion for the login path will only be registered with the Apache Sling Authenticator if the `RequirementHandler` has been configured for the tree containing the target node.

```java
Node targetNode = [...]
String loginPath = [...] // STRING property

Node targetNode = session.getNode(path);
targetNode.addMixin("granite:AuthenticationRequired");

targetNode.setProperty("granite:loginPath", loginPath);
session.save();
```

#### Modification d’un chemin de connexion existant {#modify-an-existing-login-path}

Les étapes à suivre pour modifier un chemin de connexion existant sont détaillées ci-dessous. The modification will only be registered with the Apache Sling Authenticator if the `RequirementHandler` has been configured for the tree containing the target node. La valeur précédente de chemin de connexion est supprimée de l’enregistrement. L’exigence d’authentification associée au nœud cible n’est pas affectée par cette modification.

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

#### Suppression d’une exigence d’authentification {#remove-an-auth-requirement}

Procédure pour supprimer une exigence d’authentification existante. The requirement will only be unregistered from the Apache Sling Authenticator if the `RequirementHandler` has been configured for the tree containing the target node.

```java
Node targetNode = [...]
targetNode.removeMixin("granite:AuthenticationRequired");

session.save();
```

#### Récupération des exigences d’authentification effectives {#retrieve-effective-auth-requirements}

Il n&#39;existe pas d&#39;API publique dédiée pour lire toutes les exigences d&#39;authentification efficaces telles qu&#39;elles sont enregistrées avec l&#39;Authentificateur Apache Sling. Cependant, la liste est exposée dans la console système `https://<serveraddress>:<serverport>/system/console/slingauth` sous la section &quot;Configuration **** requise pour l’authentification&quot;.

L’image suivante illustre les exigences d’authentification d’une instance de publication AEM avec du contenu de démonstration. Le chemin en surbrillance de la page de la communauté illustre comment une exigence ajoutée par la mise en œuvre décrite dans ce document est reflétée dans l’authentificateur Apache Sling.

>[!NOTE]
>
>Dans cet exemple, la propriété de chemin de connexion facultatif n’a pas été définie. Par conséquent, aucune deuxième entrée n’a été enregistrée auprès de l’authentificateur.

![chlimage_1-24](assets/chlimage_1-24.jpeg)

#### Récupération du chemin de connexion effectif {#retrieve-the-effective-login-path}

Il n&#39;existe actuellement aucune API publique pour récupérer le chemin de connexion qui prendra effet lors de l&#39;accès anonyme à une ressource nécessitant une authentification. Consultez la section Évaluation du chemin de connexion pour de plus amples informations sur la manière dont le chemin de connexion est récupéré.

Notez toutefois, qu’à part les chemins de connexion définis avec cette fonction, il existe d’autres façons de spécifier la redirection vers la connexion, qui devraient être prises en compte lors de la conception du modèle de contenu et des exigences d’authentification d’une installation d’AEM donnée.

#### Récupération de l’exigence d’authentification héritée {#retrieve-the-inherited-auth-requirement}

Comme pour le chemin de connexion, il n’existe aucune API publique pour récupérer les exigences d’authentification héritées définies dans le contenu. L’exemple suivant illustre comment liste à toutes les exigences d’authentification définies avec une hiérarchie donnée, qu’elles prennent ou non effet. Pour plus d’informations, voir [Options de configuration](/help/sites-administering/closed-user-groups.md#configuration-options).

>[!NOTE]
>
>Il est recommandé de s’appuyer sur le mécanisme d’héritage pour les besoins d’authentification et le chemin d’accès de connexion et d’éviter la création de conditions d’authentification imbriquées.
>
>For more information see [Evaluation and Inheritance of Authentication Requirement](#evaluation-and-inheritance-of-the-authentication-requirement), [Evaluation of Login Path](#evaluation-of-login-path) and [Best Practices](#best-practices).

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

### Combinaison de stratégies de CUG et d’exigence d’authentification {#combining-cug-policies-and-the-authentication-requirement}

Le tableau suivant répertorie les combinaisons valides des stratégies de CUG et de l’exigence d’authentification dans une instance AEM dont les deux modules sont activés par configuration.

| **Authentification requise** | **Chemin de connexion** | **Accès en lecture restreint** | **Effet attendu** |
|---|---|---|---|
| Oui | Oui | Oui | Un utilisateur donné ne pourra vue la sous-arborescence marquée par la stratégie CUG que si l&#39;évaluation des autorisations effectives lui permet d&#39;accéder. Un utilisateur non authentifié sera redirigé vers la page de connexion spécifiée. |
| Oui | Non | Oui | Un utilisateur donné ne pourra vue la sous-arborescence marquée par la stratégie CUG que si l&#39;évaluation des autorisations effectives lui permet d&#39;accéder. Les utilisateurs non authentifiés sont redirigés vers la page de connexion par défaut héritée. |
| Oui | Oui | Non | Un utilisateur non authentifié sera redirigé vers la page de connexion spécifiée. L’autorisation d’affichage de l’arborescence marquée par l’exigence d’authentification dépend des autorisations en vigueur des éléments individuels contenus dans cette sous-arborescence. Aucun CUG dédié limitant l’accès en lecture en place. |
| Oui | Non | Non | Les utilisateurs non authentifiés sont redirigés vers la page de connexion par défaut héritée. L’autorisation d’affichage de l’arborescence marquée par l’exigence d’authentification dépend des autorisations en vigueur des éléments individuels contenus dans cette sous-arborescence. Aucun CUG dédié limitant l’accès en lecture en place. |
| Non | Non | Oui | Un utilisateur authentifié ou non authentifié donné ne pourra vue la sous-arborescence marquée par la stratégie CUG que si l&#39;évaluation des autorisations effectives lui permet d&#39;accéder. Les utilisateurs non authentifiés sont traités de la même manière et ne sont pas redirigés vers la page de connexion. |

>[!NOTE]
>
>La combinaison Exigence d’authentification = oui et Chemin de connexion = oui ne figure pas ci-dessus, car le chemin de connexion est un attribut facultatif associé à une exigence d’authentification. La spécification d’une propriété JCR portant ce nom sans ajouter le type de mixin de définition n’aura aucun effet et sera ignorée par le gestionnaire correspondant.

## Composants OSGi et configuration {#osgi-components-and-configuration}

Cette section fournit un aperçu des composants OSGi et des différentes options de configuration introduits avec la nouvelle mise en œuvre CUG.

Consultez également la documentation relative au mappage CUG pour obtenir un mappage complet des options de configuration entre l’ancienne et la nouvelle implémentation.

### Autorisation : installation et configuration {#authorization-setup-and-configuration}

Les nouveaux composants liés à l’autorisation figurent dans le lot **Oak CUG Authorization** (`org.apache.jackrabbit.oak-authorization-cug`), qui fait partie de l’installation par défaut d’AEM. Le lot définit un modèle séparé d’autorisation destiné à être déployé comme une façon supplémentaire de gérer l’accès en lecture.

#### Installation de l’autorisation de CUG {#setting-up-cug-authorization}

Setting up CUG authorization is described in detail in the [relevant Apache Documentation](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability). Par défaut, l’autorisation de CUG est déployée dans tous les modes d’exécution d’AEM. Les instructions détaillées peuvent également être utilisées pour désactiver l’autorisation de CUG dans ces installations qui requièrent une installation d’autorisation différente.

#### Configuration du filtre de référent {#configuring-the-referrer-filter}

You also need to configure the [Sling Referrer Filter](/help/sites-administering/security-checklist.md#the-sling-referrer-filter) with all hostnames that may be used to access AEM; for example, via CDN, Load Balancer, and any others.

Si le filtre de référent n’est pas configuré, alors des erreurs, comme celles qui suivent, apparaissent lorsqu’un utilisateur tente de se connecter à un site CUG :

```shell
31.01.2017 13:49:42.321 *INFO* [qtp1263731568-346] org.apache.sling.security.impl.ReferrerFilter Rejected referrer header for POST request to /libs/granite/core/content/login.html/j_security_check : https://hostname/libs/granite/core/content/login.html?resource=%2Fcontent%2Fgeometrixx%2Fen%2Ftest-site%2Ftest-page.html&$$login$$=%24%24login%24%24&j_reason=unknown&j_reason_code=unknown
```

#### Caractéristiques des composants OSGi {#characteristics-of-osgi-components}

Les deux composants OSGi suivants ont été ajoutés pour définir les exigences d’authentification et spécifier les chemins de connexion dédiés :

* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration`
* `org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl`

**org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration**

<table>
 <tbody>
  <tr>
   <td>Libellé</td>
   <td>Configuration d'Apache Jackrabbit Oak CUG</td>
  </tr>
  <tr>
   <td>Description</td>
   <td>Configuration de l'autorisation dédiée à la configuration et à l'évaluation des autorisations CUG.</td>
  </tr>
  <tr>
   <td>Propriétés de configuration</td>
   <td>
    <ul>
     <li><code>cugSupportedPaths</code></li>
     <li><code>cugEnabled</code></li>
     <li><code>configurationRanking</code></li>
    </ul> <p>Voir aussi Options <a href="#configuration-options">de</a> configuration ci-dessous.</p> </td>
  </tr>
  <tr>
   <td>Stratégie de configuration</td>
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
   <td>Liste d'exclusion Apache Jackrabbit Oak CUG</td>
  </tr>
  <tr>
   <td>Description</td>
   <td>Permet d'exclure du contrôle CUG les entités dont le ou les noms sont configurés.</td>
  </tr>
  <tr>
   <td>Propriétés de configuration</td>
   <td>
    <ul>
     <li><code>principalNames</code></li>
    </ul> <p>Voir aussi la section Options de configuration ci-dessous.</p> </td>
  </tr>
  <tr>
   <td>Stratégie de configuration</td>
   <td><code>ConfigurationPolicy.REQUIRE</code></td>
  </tr>
  <tr>
   <td>Références</td>
   <td>N/A</td>
  </tr>
 </tbody>
</table>

#### Options de configuration {#configuration-options}

Les options de configuration clés sont les suivantes :

* `cugSupportedPaths` : spécifiez les sous-arborescences pouvant contenir des CUG. Aucune valeur n’est définie par défaut.
* `cugEnabled` : option de configuration pour activer l’évaluation des permissions pour les stratégies de CUG actuelles.

Les options de configuration disponibles liées au module d’autorisation de CUG sont répertoriées et décrites avec davantage de détails dans la [documentation Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#configuration).

#### Exclusion d’entités de sécurité de l’évaluation de CUG {#excluding-principals-from-cug-evaluation}

L’exemption d’entités de sécurité de l’évaluation de CUG a été adoptée à partir de l’ancienne mise en œuvre. La nouvelle autorisation de CUG couvre ce problème avec une interface dédiée nommée CugExclude. Apache Jackrabbit Oak 1.4 est livré avec une mise en œuvre par défaut qui exclut un ensemble fixe d’entités de sécurité, ainsi qu’une mise en œuvre étendue qui permet de configurer les noms des différentes entités de sécurité. Ce dernier est configuré dans les instances de publication d’AEM.

Depuis la version 6.3, par défaut, AEM empêche les entités de sécurité suivantes d’être affectées par les stratégies de CUG :

* Entités de sécurité administratives (utilisateur administrateur et groupe d’administrateurs)
* Entités de sécurité d’utilisateurs de services
* Entité de sécurité de système interne de référentiel

Pour plus d’informations, voir le tableau de la section [Configuration par défaut depuis AEM 6.3](#default-configuration-since-aem) ci-dessous.

The exclusion of the &#39;administrators&#39; group can be altered or expanded in the system console in the configuration section of **Apache Jackrabbit Oak CUG Exclude List**.

Vous pouvez également fournir et déployer une implémentation personnalisée de l’interface CugExclude pour ajuster l’ensemble des entités exclues en cas de besoins spéciaux. See the documentation on [CUG pluggability](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) for details and an example implementation.

### Authentification : installation et configuration {#authentication-setup-and-configuration}

Les nouveaux composants liés à l’authentification figurent dans le lot **Gestionnaire d’authentification Adobe Granite** (`com.adobe.granite.auth.authhandler` version 5.6.48). Ce lot fait partie de l’installation par défaut d’AEM.

Pour installer l’exigence d’authentification de remplacement pour la prise en charge de CUG obsolète, certains composants OSGi doivent être présents et actifs dans une configuration d’AEM donnée. Pour plus d’informations, voir **Caractéristiques des composants OSGi** ci-dessous.

>[!NOTE]
>
>En raison de l’option de configuration obligatoire avec RequirementHandler, les composants liés à l’authentification sont activés uniquement si la fonction a été activée en spécifiant un ensemble de chemins pris en charge. Avec une installation AEM standard, cette fonction est désactivée en mode d’exécution de création et activée pour /content en mode d’exécution de publication.

**Caractéristiques des composants OSGi**

Les deux composants OSGi suivants ont été ajoutés pour définir les exigences d’authentification et spécifier les chemins de connexion dédiés :

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
   <td>Service OSGi dédié pour les exigences d'authentification qui enregistre un observateur pour les modifications de contenu affectant les exigences d'authentification (par le type de <code>granite:AuthenticationRequirement</code> mixin) et les chemins de connexion avec sont exposés au <code>LoginSelectorHandler</code>. </td>
  </tr>
  <tr>
   <td>Propriétés de configuration</td>
   <td>-</td>
  </tr>
  <tr>
   <td>Stratégie de configuration</td>
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

| Libellé | Exigences en matière d&#39;authentification Granite Adobe et gestionnaire de chemins d&#39;accès de connexion |
|---|---|
| Description | `RequirementHandler` implémentation qui met à jour les exigences d’authentification Apache Sling et l’exclusion correspondante pour les chemins d’accès associés. |
| Propriétés de configuration | `supportedPaths` |
| Stratégie de configuration | `ConfigurationPolicy.REQUIRE` |
| Références | N/A |

#### Options de configuration {#configuration-options-1}

Les composants de relecture de CUG liés à l’authentification ne proposent qu’une option de configuration associée au gestionnaire d’exigence d’authentification et de chemin de connexion Adobe Granite :

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
   <td><p>Libellé = Chemins pris en charge</p> <p>Name = 'supportedPaths'</p> </td>
   <td>Set&lt;String&gt;</td>
   <td>-</td>
   <td>Chemins sous lesquels les exigences d'authentification seront respectées par ce gestionnaire. Leave this configuration unset if you want to add the <code>granite:AuthenticationRequirement</code> mixin type to nodes without having them enforced (for example, on author instances). Si elle est absente, la fonction est désactivée. </td>
  </tr>
 </tbody>
</table>

## Configuration par défaut depuis AEM 6.3 {#default-configuration-since-aem}

Les nouvelles installations d’AEM utilisent par défaut les nouvelles mises en œuvre à la fois pour les composants liés à l’autorisation et à l’authentification de la fonction CUG. L’ancienne mise en œuvre « Prise en charge des groupes d’utilisateurs fermés (CUG) par Adobe Granite » a été abandonnée et sera désactivée par défaut dans toutes les installations d’AEM. Les nouvelles mises en œuvre sont activées comme suit :

### Instances de création {#author-instances}

| **&quot;Apache Jackrabbit Oak CUG Configuration&quot;** | **Explication** |
|---|---|
| Chemins pris en charge `/content` | La gestion des contrôles d&#39;accès pour les stratégies CUG est activée. |
| Évaluation du CUG activée pour FALSE | L&#39;évaluation des autorisations est désactivée. Les stratégies de CUG n’ont aucun effet. |
| Classement | 200 | Voir la documentation sur les chênes. |

>[!NOTE]
>
>Aucune configuration pour la **liste d’exclusion de CUG Apache Jackrabbit Oak** et le **gestionnaire d’exigence d’authentification et de chemin de connexion Adobe Granite** n’est présente sur les instances de création par défaut.

### Instances de publication {#publish-instances}

| **&quot;Apache Jackrabbit Oak CUG Configuration&quot;** | **Explication** |
|---|---|
| Chemins pris en charge `/content` | La gestion des contrôles d&#39;accès pour les stratégies CUG est activée sous les chemins configurés. |
| Évaluation CUG activée TRUE | L’évaluation des autorisations est activée sous les chemins configurés. Les politiques du CUG entrent en vigueur `Session.save()`. |
| Classement | 200 | Voir la documentation sur les chênes. |

| **&quot;Apache Jackrabbit Oak CUG Exclusion Liste&quot;** | **Explication** |
|---|---|
| Administrateurs des noms principaux | Exclut le principal administrateur de l’évaluation CUG. |

| **&quot;Adobe Granite Authentication Requirements and Login Path Handler&quot; (Configuration requise pour l&#39;authentification Granite et gestionnaire de chemins d&#39;accès de connexion)** | **Explication** |
|---|---|
| Chemins pris en charge  `/content` | Les exigences d&#39;authentification définies dans le référentiel au moyen du type de `granite:AuthenticationRequired` mixin prennent effet ci-dessous `/content` sur `Session.save()`. L’authentificateur Sling est mis à jour. L’ajout du type de mixin en dehors des chemins pris en charge est ignoré. |

## Désactivation de l’exigence d’authentification et de l’autorisation des CUG {#disabling-cug-authorization-and-authentication-requirement}

La nouvelle mise en œuvre peut être désactivée entièrement au cas où une installation donnée n’utilise pas de CUG ou utilise des moyens différents pour l’authentification et l’autorisation.

### Désactivation de l’autorisation des CUG {#disable-cug-authorization}

Consultez la documentation sur l’[aspect enfichable des CUG](https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html#pluggability) pour plus d’informations sur la procédure de suppression du modèle d’autorisation des CUG de la configuration d’autorisation composite.

### Désactivation de l’exigence d’authentification {#disable-the-authentication-requirement}

Pour désactiver la prise en charge de l’exigence d’authentification fournie par le module `granite.auth.authhandler`, il suffit de supprimer la configuration associée au **Gestionnaire d’exigence d’authentification et de chemin de connexion Adobe Granite**.

>[!NOTE]
>
>Notez toutefois que la suppression de la configuration n’annule pas l’enregistrement du type de mixin, qui peut toujours s’appliquer aux nœuds sans prendre effet.

## Interaction avec d’autres modules {#interaction-with-other-modules}

### API Apache Jackrabbit {#apache-jackrabbit-api}

Afin de refléter le nouveau type de stratégie de contrôle d’accès utilisé par le modèle d’autorisation des CUG, l’API définie par Apache Jackrabbit a été étendue. Since version 2.11.0 of the `jackrabbit-api` module defines a new interface called `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy`, which extends from `javax.jcr.security.AccessControlPolicy`.

### Apache Jackrabbit FileVault {#apache-jackrabbit-filevault}

The import mechanism of Apache Jackrabbit FileVault has been adjusted to deal with access control policies of type `PrincipalSetPolicy`.

### Distribution de contenu Apache Sling {#apache-sling-content-distribution}

Voir la section [Apache Jackrabbit FileVault](/help/sites-administering/closed-user-groups.md#apache-jackrabbit-filevault) ci-dessus.

### Réplication Adobe Granite {#adobe-granite-replication}

Le module de réplication a été légèrement ajusté afin de pouvoir répliquer les stratégies de CUG entre différentes instances d’AEM :

* `DurboImportConfiguration.isImportAcl()` est interprété au sens littéral et n&#39;affectera que la mise en oeuvre des politiques de contrôle d&#39;accès `javax.jcr.security.AccessControlList`

* `DurboImportTransformer` respectera uniquement cette configuration pour les listes ACL réelles
* D’autres stratégies telles que les instances de `org.apache.jackrabbit.api.security.authorization.PrincipalSetPolicy` créées par le modèle d’autorisation des CUG sont toujours répliquées, et l’option de configuration `DurboImportConfiguration.isImportAcl` () est ignorée.

Il existe une limite de réplication des stratégies de CUG. If a given CUG policy gets removed without removing the corresponding mixin node type `rep:CugMixin,` the removal will not be reflected upon replication. Ce problème a été corrigé en supprimant toujours le mixin lors de la suppression d’une stratégie. La limitation peut toutefois apparaître si le type de mixin est ajouté manuellement.

### Gestionnaire d’authentification Adobe Granite {#adobe-granite-authentication-handler}

Le gestionnaire d’authentification **Adobe Granite HTTP Header Authentication Handler** fourni avec le lot `com.adobe.granite.auth.authhandler` contient une référence à l’interface `CugSupport` définie par le même module. Il est utilisé pour calculer le domaine dans certains cas, en se repliant sur le domaine configuré avec le gestionnaire.

Cela a été réglé de façon à rendre la référence à `CugSupport` facultative pour assurer une compatibilité ascendante maximale si une configuration donnée décide de réactiver cette mise en œuvre obsolète. Installations using the implementation will no longer get the realm extracted from the CUG implementation but will always display the realm as defined with **Adobe Granite HTTP Header Authentication Handler**.

>[!NOTE]
>
>Par défaut, **Adobe Granite HTTP Header Authentication Handler** n’est configuré que dans le mode d’exécution de publication avec l’option Désactiver la page de connexion (`auth.http.nologin`) activée.

### AEM LiveCopy {#aem-livecopy}

La configuration de CUG en association avec LiveCopy est représentée dans le référentiel par l’ajout d’un noeud supplémentaire et d’une propriété supplémentaire, comme suit :

* `/content/we-retail/us/en/blueprint/rep:cugPolicy`
* `/content/we-retail/us/en/LiveCopy@granite:loginPath`

Both of these elements are created under the `cq:Page`. With the current design, MSM only handles nodes and properties that are under the `cq:PageContent` (`jcr:content`) node.

Par conséquent, les groupes CUG ne peuvent pas être récupérés d’un plan directeur vers une Live Copy. Veuillez prendre en compte ce paramètre lors de la configuration d’une Live Copy.

## Modifications avec la nouvelle mise en œuvre CUG {#changes-with-the-new-cug-implementation}

Cette section est destinée à présenter les modifications apportées à la fonction CUG et à comparer l’ancienne et la nouvelle mise en œuvre. Elle répertorie les modifications affectant la façon dont la prise en charge des CUG est configurée, et décrit comment et par qui les CUG sont gérés dans le référentiel de contenu.

### Differences in CUG Setup and Configuration {#differences-in-cug-setup-and-configuration}

Le composant OSGi obsolète **Prise en charge des groupes d’utilisateurs fermés (CUG) Adobe Granite** (`com.day.cq.auth.impl.cug.CugSupportImpl`) a été remplacé par de nouveaux composants de façon à gérer séparément les composants liés à l’autorisation et à l’authentification de la fonctionnalité de CUG précédente.

## Differences in Managing CUGs in the Repository Content {#differences-in-managing-cugs-in-the-repository-content}

Les sections suivantes décrivent les différences entre l’ancienne et la nouvelle mise en œuvre du point de vue de l’implémentation et de la sécurité. Bien que la nouvelle mise en œuvre vise à proposer des fonctionnalités équivalentes, il existe de légères modifications importantes à connaître lorsque vous utilisez les nouveaux CUG.

### Differences With Regards To Authorization {#differences-with-regards-to-authorization}

Les principales différences du point de vue de l&#39;autorisation sont résumées dans la liste ci-dessous :

**Contenu de contrôle d’accès dédié pour les CUG**

Dans l’ancienne mise en œuvre, le modèle d’autorisation par défaut était utilisé pour manipuler les stratégies de contrôle d’accès sur l’instance de publication, remplaçant tous les ACE existants par la configuration requise par le CUG. Cela était déclenché en écrivant des propriétés JCR résiduelles standard qui étaient interprétées sur l’instance de publication.

Avec la nouvelle mise en oeuvre, la configuration de contrôle d&#39;accès du modèle d&#39;autorisation par défaut n&#39;est affectée par aucun CUG créé, modifié ou supprimé. Instead a new type of policy called `PrincipalSetPolicy` is applied as additional access control content to the target node. Cette stratégie supplémentaire est placée en tant qu’enfant du nœud cible et doit être une sœur du nœud de stratégie par défaut (s’il existe).

**Modification des stratégies de CUG dans la gestion du contrôle d’accès**

Cette transition des propriétés JCR résiduelles vers une stratégie de contrôle d’accès dédiée a un impact sur les permissions requises pour créer ou modifier le composant d’autorisation de la fonction CUG. Since this is considered a modification to access control content, it requires `jcr:readAccessControl` and `jcr:modifyAccessControl` privileges in order to be written to the repository. Par conséquent, seuls les auteurs de contenu autorisés à modifier le contenu de contrôle d’accès d’une page peuvent installer ou modifier ce contenu. Cela contraste avec l’ancienne mise en œuvre où la possibilité d’écrire des·propriétés JCR standard suffisait, entraînant la réaffectation des privilèges.

**Nœud cible défini par stratégie**

Il est attendu que les stratégies de CUG sont créées au niveau du nœud JCR définissant la sous-arborescence dont l’accès en lecture est à restreindre. Il est vraisemblable qu’il s’agisse d’une page AEM dans le cas où le CUG devrait affecter l’arborescence entière.

Notez que le fait de placer la stratégie CUG uniquement sur le noeud jcr:content situé en dessous d’une page donnée ne fera que restreindre l’accès au contenu s.str d’une page donnée, mais n’aura aucun effet sur les pages frères ou soeurs ou enfants. Il peut s’agir d’un cas d’utilisation valide, réalisable avec un éditeur de référentiel qui permet d’appliquer un accès de granularité fine au contenu. Cependant, il compare l’ancienne mise en oeuvre dans laquelle le placement d’une propriété cq:cugEnabled sur le noeud jcr:content était remappé en interne au noeud de page. Cette mise en correspondance n’est plus réalisée.

**Évaluation des permissions avec des stratégies de CUG**

Le passage de l’ancienne prise en charge des CUG à un modèle d’autorisation supplémentaire, modifie la façon dont les permissions de lecture en vigueur sont évaluées. As described in the [Jackrabbit documentation](https://jackrabbit.apache.org/oak/docs/security/authorization/composite.html), a given principal allowed to view the `CUGcontent` will only be granted read access if the permission evaluation of all models configured in the Oak repository grant read access.

En d’autres termes, pour l’évaluation des permissions en vigueur, à la fois `CUGPolicy` et les entrées de contrôle d’accès par défaut sont pris en compte, et l’accès en lecture sur le contenu CUG est uniquement autorisé s’il est accordé par les deux types de stratégies. In a default AEM publish installation where read access to the complete `/content` tree is granted for everyone, the effect of the CUG policies will be the same as with the old implementation.

**Évaluation à la demande**

Le modèle d’autorisation des CUG permet d’activer individuellement la gestion du contrôle d’accès et l’évaluation des permissions :

* La gestion du contrôle d’accès est activée si le module dispose d’un ou de plusieurs chemins où des CUG peuvent être créés.
* L’évaluation des permissions est activée uniquement si l’option **Évaluation des CUG activée** est cochée.

Dans l’évaluation des stratégies de CUG de la nouvelle configuration par défaut d’AEM, elle est activée uniquement avec le mode d’exécution de publication. Consultez les informations relatives à la [configuration par défaut depuis AEM 6.3](#default-configuration-since-aem) pour en savoir plus. Ceci peut être vérifié en comparant les stratégies efficaces pour un chemin d’accès donné aux stratégies stockées dans le contenu. Les stratégies en vigueur sont affichées uniquement dans le cas où l’évaluation des permissions est activée pour les CUG.

As explained above the CUG access control policies are now always stored in the content but evaluation of the effective permissions that result from those policies will only be enforced if **CUG Evaluation Enabled** is turned on in the system console at Apache Jackrabbit Oak **CUG Configuration.** Par défaut, elle est uniquement activée avec le mode d’exécution de publication.

### Différences quant à l’authentification {#differences-with-regards-to-authentication}

Les différences en qui concerne l’authentification sont décrites ci-dessous.

#### Type de mixin pour l’exigence d’authentification {#dedicated-mixin-type-for-authentication-requirement}

Dans l’ancienne mise en œuvre, les aspects d’autorisation et d’authentification d’un CUG étaient tous deux déclenchés par une seule propriété JCR (`cq:cugEnabled`). En ce qui concerne l’authentification, il en résultait une liste mise à jour des exigences d’authentification telles que stockées avec la mise en œuvre de l’authentificateur Apache Sling. Avec la nouvelle mise en œuvre, le même résultat est obtenu en marquant le nœud cible avec un type spécial de mixin ( `granite:AuthenticationRequired`).

#### Propriété d’exclusion d’un chemin de connexion {#property-for-excluding-login-path}

The mixin type defines a single, optional property called `granite:loginPath`, which basically corresponds to the `cq:cugLoginPage` property. Contrairement à la mise en œuvre précédente, la propriété de chemin de connexion n’est respectée que si son type de nœud d’instruction est le mixin indiqué. L’ajout d’une propriété portant ce nom sans définir le type de mixin n’a aucun effet, et ni une nouvelle exigence ni une exclusion du chemin de connexion ne seront signalées à l’authentificateur.

#### Privilège pour l’exigence d’authentification {#privilege-for-authentication-requirement}

L’ajout ou la suppression d’un type de mixin requiert l’attribution du privilège `jcr:nodeTypeManagement`. In the previous implementation, the `jcr:modifyProperties` privilege is used to edit the residual property.

En ce qui concerne `granite:loginPath`, le même privilège est requis pour ajouter, modifier ou supprimer la propriété.

#### Nœud cible défini par le type de mixin {#target-node-defined-by-mixin-type}

Il est attendu que les exigences d’authentification sont créées au niveau du nœud JCR définissant la sous-arborescence pour laquelle la connexion doit être forcée. Il est vraisemblable qu’il s’agisse d’une page AEM dans le cas où le CUG devrait affecter l’arborescence entière, et l’IU de la nouvelle mise en œuvre ajoute par conséquent le type de mixin auth-requirement au nœud de la page.

Le fait de placer la stratégie CUG uniquement au noeud jcr:content situé en dessous d’une page donnée ne fera que restreindre l’accès au contenu, mais n’aura aucune incidence sur le noeud de page lui-même ni sur les pages enfants.

Il peut s’agir d’un scénario valide et possible avec un éditeur de référentiel qui permet de placer le mixin au niveau de n’importe quel nœud. Cependant, le comportement contraste avec l’ancienne mise en oeuvre, où le placement d’une propriété cq:cugEnabled ou cq:cugLoginPage sur le noeud jcr:content a été effectué en interne, en fin de compte, sur le noeud de page. Cette mise en correspondance n’est plus réalisée.

#### Chemins pris en charge configurés {#configured-supported-paths}

Both the `granite:AuthenticationRequired` mixin type and the granite:loginPath property will only be respected within the scope defined by the set of **Supported Paths** configuration option present with the **Adobe Granite Authentication Requirement and Login Path Handler**. Si aucun chemin n’est spécifié, la fonction d’exigence d’authentification est complètement désactivée. Dans ce cas, le type de mixin ou la propriété prend effet lors de l’ajout ou de la définition d’un noeud JCR donné.

### Mise en correspondance de contenu JCR, de services OSGi et de configurations {#mapping-of-jcr-content-osgi-services-and-configurations}

Le document ci-dessous fournit un mappage complet des services OSGi, des configurations et du contenu du référentiel entre l&#39;ancienne et la nouvelle implémentation.

Mise en correspondance de CUG depuis AEM 6.3

[Obtenir le fichier](assets/cug-mapping.pdf)

## Mettre à niveau la fonction CUG {#upgrade-cug}

### Installations existantes utilisant la fonction CUG obsolète {#existing-installations-using-the-deprecated-cug}

L’ancienne mise en œuvre de prise en charge des CUG a été abandonnée et sera supprimée dans les futures versions. Il est recommandé de passer aux nouvelles mises en œuvre lors de la mise à niveau à partir de versions antérieures à AEM 6.3.

Pour les installations AEM mises à niveau, il est important de s’assurer qu’une seule mise en œuvre CUG est activée. La combinaison de la nouvelle mise en œuvre et de l’ancienne prise en charge de CUG obsolète n’a pas été testée et risque de provoquer un comportement indésirable :

* Des collisions dans l’authentificateur Sling en ce qui concerne les exigences d’authentification
* Des refus d’accès en lecture lorsque la configuration de liste de contrôle d’accès associée à l’ancien CUG entre en conflit avec une nouvelle stratégie de CUG.

### Migration d’un contenu de CGU existant {#migrating-existing-cug-content}

Adobe fournit un outil pour migrer vers la nouvelle mise en œuvre CUG. Pour l’utiliser, suivez les étapes ci-dessous :

1. Accédez `https://<serveraddress>:<serverport>/system/console/cug-migration` à pour accéder à l&#39;outil.
1. Saisissez le chemin racine pour lequel vous souhaitez vérifier les CUG et appuyez sur le bouton **Exécution d’essai**. Cette opération analyse les CUG pouvant être convertis à l&#39;emplacement sélectionné.
1. Une fois que vous avez consulté les résultats, appuyez sur le bouton **Effectuer la migration** pour migrer vers la nouvelle mise en œuvre.

>[!NOTE]
>
>If you run into issues, it is possible to set up a specific logger at **DEBUG** level on `com.day.cq.auth.impl.cug` to get the output of the migration tool. Consultez la rubrique [Connexion](/help/sites-deploying/configure-logging.md) pour en savoir plus sur la procédure à suivre.

