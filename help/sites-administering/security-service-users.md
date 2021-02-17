---
title: Utilisateurs de services dans AEM
seo-title: Utilisateurs de services dans AEM
description: Apprenez-en plus sur les utilisateurs de services dans AEM.
seo-description: Apprenez-en plus sur les utilisateurs de services dans AEM.
uuid: 4efab5fb-ba11-4922-bd68-43ccde4eb355
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 9cfe5f11-8a0e-4a27-9681-a8d50835c864
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '1788'
ht-degree: 77%

---


# Utilisateurs de services dans AEM{#service-users-in-aem}

## Présentation {#overview}

Le principal moyen d&#39;obtenir une session administrative ou un résolveur de ressources en AEM était d&#39;utiliser les méthodes `SlingRepository.loginAdministrative()` et `ResourceResolverFactory.getAdministrativeResourceResolver()` fournies par Sling.

Toutefois, aucune de ces méthodes n’a été conçue selon le [principe de moindre autorisation](https://en.wikipedia.org/wiki/Principle_of_least_privilege). En conséquence, elles permettent facilement à un développeur de ne pas planifier de structure et de niveaux de contrôle d’accès (ACL) appropriés pour leur contenu dès le début. Si une vulnérabilité est présente dans un tel service, elle conduit souvent à des réaffectations de privilèges à l’utilisateur `admin`, même si le code n’a pas besoin de privilèges d’administrateur pour fonctionner.

## Élimination des sessions d’administrateur {#how-to-phase-out-admin-sessions}

### Priorité 0 : La fonction est-elle principale/nécessaire/abandonnée ? {#priority-is-the-feature-active-needed-derelict}

Il peut y avoir des cas où la session administrateur n’est pas utilisée, ou la fonction est complètement désactivée. Si tel est le cas avec votre mise en œuvre, assurez-vous de supprimer la fonction entièrement ou accompagnez-la d’une [instruction nulle](https://fr.wikipedia.org/wiki/Instruction_nulle).

### Priorité 1 : utilisez la session de requête {#priority-use-the-request-session}

Lorsque cela est possible, refactorisez votre fonction de sorte que la session de requête authentifiée donnée puisse être utilisée pour écrire ou lire du contenu. Si ce n’est pas possible, elle peut fréquemment être obtenue en appliquant les priorités comme ci-dessous.

### Priorité 2 : restructurez le contenu {#priority-restructure-content}

De nombreux problèmes peuvent être résolus en restructurant le contenu. Gardez ces règles simples à l’esprit lors de la restructuration :

* **Modification du contrôle d’accès**

   * Assurez-vous que les utilisateurs ou les groupes qui ont réellement besoin d’accès ont accès.

* **Amélioration de la structure de contenu**

   * Déplacez-le vers d’autres emplacements, par exemple là où le contrôle d’accès correspond aux sessions de requête disponibles.
   * Modifiez la granularité du contenu.

* **Refactorisation du code afin qu’il corresponde à un service approprié**

   * Redéfinissez la logique métier du code JSP en service. Cela permet une modélisation de contenu différente.

En outre, assurez-vous que toutes les nouvelles fonctions que vous développez sont conformes aux principes suivants :

* **Les exigences de sécurité doivent déterminer la structure du contenu.**

   * La gestion du contrôle d’accès doit sembler naturelle.
   * Le contrôle d’accès doit être imposé par le référentiel, et non par l’application.

* **Tirez parti des types de nœuds.**

   * Limitez le jeu de propriétés qui peut être défini.

* **Respectez les paramètres de confidentialité.**

   * Dans le cas des profils privés, un exemple consisterait à ne pas exposer l&#39;image du profil, le courriel ou le nom complet figurant sur le noeud privé `/profile`.

## Contrôle d’accès strict {#strict-access-control}

Que vous appliquiez un contrôle d&#39;accès lors de la restructuration du contenu ou lorsque vous le faisiez pour un nouvel utilisateur de service, vous devez appliquer les ACL les plus strictes possible. Utilisez tous les moyens de contrôle d’accès possibles :

* Par exemple, au lieu d&#39;appliquer `jcr:read` sur `/apps`, appliquez-le uniquement à `/apps/*/components/*/analytics`

* Utiliser les [restrictions](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html)

* Application de listes ACL aux types de nœuds
* Limitation des autorisations

   * par exemple, lorsqu&#39;il suffit d&#39;écrire des propriétés, ne donnez pas l&#39;autorisation `jcr:write`; utilisez plutôt `jcr:modifyProperties`

## Utilisateurs de services et mises en correspondance {#service-users-and-mappings}

Si ce qui précède échoue, Sling 7 offre un service de mappage utilisateur de service, qui permet de configurer un mappage de groupe à utilisateur et deux méthodes d’API correspondantes : ` [SlingRepository.loginService()](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)` et ` [ResourceResolverFactory.getServiceResourceResolver()](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)` qui renvoient un résolveur de session/ressource avec les privilèges d&#39;un utilisateur configuré uniquement. Ces méthodes présentent les caractéristiques suivantes¬:

* Elles permettent de mettre en correspondance les services avec les utilisateurs.
* Elles permettent de définir des utilisateurs de sous-services.
* Le point central de configuration est le suivant : `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` =  `service-name` [ &quot;:&quot; sous-service-name  ] 

* `service-id` est mis en correspondance avec un résolveur de ressource et/ou un ID d’utilisateur de référentiel JCR pour l’authentification.
* `service-name` est le nom symbolique du lot qui fournit le service.

## Autres recommandations {#other-recommendations}

### Remplacement de l’admin-session par un service-user {#replacing-the-admin-session-with-a-service-user}

Un utilisateur de service est un utilisateur JCR sans mot de passe défini et avec un jeu minimal d’autorisations nécessaires pour effectuer une tâche spécifique. L’absence de mot de passe défini signifie qu’il n’est pas possible de se connecter avec un utilisateur de service.

Une façon de rendre une session administrative obsolète consiste à la remplacer par des sessions d’utilisateurs de services. Elle pourrait également être remplacée par plusieurs utilisateurs de sous-services si nécessaire.

Pour remplacer la session administrative par un utilisateur de services, vous devez effectuer les étapes suivantes :

1. Identifiez les autorisations nécessaires pour votre service, en gardant à l’esprit le principe de moindre autorisation.
1. Vérifiez s’il existe déjà un utilisateur disponible ayant exactement la configuration de permissions dont vous avez besoin. Créez un utilisateur de service système si aucun utilisateur existant ne correspond à vos besoins. RTC est nécessaire pour créer un utilisateur de service. Dans certains cas, il est préférable de créer plusieurs utilisateurs de sous-services (par exemple, un pour écrire et l’autre pour lire) afin de compartimenter encore davantage l’accès.
1. Configurez et testez les ACE pour votre utilisateur.
1. Ajouter un mappage `service-user` pour votre service et pour `user/sub-users`

1. Rendez la fonction Sling d’utilisateur de service disponible pour votre lot : mettez à jour vers la version la plus récente de `org.apache.sling.api`.

1. Remplacez `admin-session` dans votre code par les API `loginService` ou `getServiceResourceResolver`.

## Création d’un utilisateur de service {#creating-a-new-service-user}

Après avoir vérifié qu’aucun utilisateur dans la liste des utilisateurs de services AEM ne s’applique à votre cas d’utilisation, et que les problèmes RTC correspondants ont été approuvés, vous pouvez procéder à l’ajout de l’utilisateur au contenu par défaut.

L’approche recommandée consiste à créer un utilisateur de service pour utiliser l’explorateur de référentiel à l’adresse *https://&lt;serveur>:&lt;port>/crx/explorer/index.jsp*.

Le but est d’obtenir une propriété `jcr:uuid` valide qui est obligatoire pour créer l’utilisateur par l’intermédiaire d’une installation de module de contenu.

Vous pouvez créer des utilisateurs de services de la façon suivante :

1. Accédez à l’explorateur de référentiel à l’adresse *https://&lt;serveur>:&lt;port>/crx/explorer/index.jsp*.
1. Ouvrez une session en tant qu’administrateur en appuyant sur le lien **Connexion** dans le coin supérieur gauche de l’écran.
1. Ensuite, créez et nommez votre utilisateur système. Pour créer l’utilisateur en tant qu’utilisateur système, définissez le chemin intermédiaire comme `system` et ajoutez des sous-dossiers facultatifs en fonction de vos besoins :

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. Vérifiez que le nœud d’utilisateur système se présente comme suit :

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >Notez qu’il n’y a aucun type de mixin associé aux utilisateurs de services. Cela signifie qu’il n’y a aucune stratégie de contrôle d’accès pour les utilisateurs système.

En ajoutant le fichier content.xml correspondant au contenu du lot, assurez-vous que vous avez défini le `rep:authorizableId` et que le type principal est `rep:SystemUser`. Il doit ressembler à ceci :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## Ajout d’un amendement de configuration à la configuration ServiceUserMapper  {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

Pour ajouter une mise en correspondance de votre service avec les utilisateurs système correspondants, vous devez créer une configuration de fabrique pour le service ` [ServiceUserMapper](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html)`. Pour conserver la modularité, de telles fonctionnalités peuvent être fournies·par le [mécanisme d’amendement de Sling](https://issues.apache.org/jira/browse/SLING-3578). La méthode recommandée pour installer ces configurations avec votre lot consiste à utiliser le [chargement du contenu initial de Sling](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html) :

1. Créez un sous-dossier SLING-INF/content sous le dossier src/main/resources de votre lot
1. Dans ce dossier, créez un fichier nommé org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.changed-&lt;un nom unique pour votre configuration d’usine>.xml avec le contenu de votre configuration d’usine (y compris tous les mappages d’utilisateurs de sous-services). Exemple :

1. Créez un dossier `SLING-INF/content` sous le dossier `src/main/resources` de votre lot ;
1. Dans ce dossier, créez un fichier `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` contenant le contenu de votre configuration d’usine, y compris tous les mappages d’utilisateurs de sous-services.

   À des fins d’illustration, prenez le fichier nommé `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml` :

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <node>
       <primaryNodeType>sling:OsgiConfig</primaryNodeType>
       <property>
           <name>user.default</name>
           <value></value>
       </property>
       <property>
           <name>user.mapping</name>
           <values>
               <value>com.adobe.granite.auth.saml=authentication-service</value>
           </values>
       </property>
   </node>
   ```

1. Référencez le contenu initial Sling dans la configuration de `maven-bundle-plugin` dans la `pom.xml` de votre lot. Exemple :

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. Installez le lot et assurez-vous que la configuration de fabrique a été installée. Vous pouvez le faire en procédant comme suit :

   * Accédez à la console Web à l&#39;adresse *https://serverhost:serveraddress/system/console/configMgr*.
   * Recherchez **Apache Sling Service User Mapper Service Amendment**.
   * Cliquez sur le lien pour vérifier si la configuration appropriée est en place.

## Traitement des sessions partagées dans les services {#dealing-with-shared-sessions-in-services}

Les appels à `loginAdministrative()` s’affichent souvent avec des sessions partagées. Ces sessions sont acquises lors de l’activation du service et ne sont déconnectées qu’après l’arrêt du service. Bien que cette pratique soit courante, elle soulève deux problèmes :

* **Sécurité** : ces sessions d’administrateur sont utilisées pour mettre en cache et renvoyer les ressources ou d’autres objets qui sont liés à la session partagée. Plus loin dans la pile d’appels, ces objets peuvent être adaptés aux sessions ou aux résolveurs de ressources avec des autorisations élevées, or il n’est souvent pas évident pour l’appelant que la session utilisée est une session d’administrateur.
* **Performances** : dans Oak, les sessions partagées peuvent entraîner des problèmes de performances, et il n’est pas recommandé de les utiliser à l’heure actuelle.

La solution la plus évidente pour le risque de sécurité est de simplement remplacer l&#39;appel `loginAdministrative()` par un appel `loginService()` à un utilisateur disposant de privilèges restreints. Toutefois, cette opération n’aura aucune incidence sur une éventuelle dégradation des performances. Vous pouvez limiter ces éventuelles dégradations en incluant toutes les informations requises dans un objet qui n’est plus associé à la session. Ensuite, créez (ou détruisez) la session à la demande.

L’approche recommandée consiste à refactoriser l’API du service pour donner à l’appelant le contrôle de la création/destruction de la session.

## Sessions administratives dans les JSP  {#administrative-sessions-in-jsps}

Les JSP ne peuvent pas utiliser `loginService()`, car aucun service associé n’existe. Cependant, les sessions administratives dans les JSP sont généralement le signe d&#39;une violation du paradigme du MVC.

Cela peut être corrigé de deux façons :

1. En restructurant le contenu d’une manière qui permet de les manipuler avec la session utilisateur
1. En extrayant la logique vers un service qui fournit une API qui peut alors être utilisée par le JSP

La première méthode est préférable.

## Traitement des événements, des préprocesseurs de réplication et des tâches {#processing-events-replication-preprocessors-and-jobs}

Lors du traitement d’événements, de tâches, et dans certains cas, de workflows, la session correspondante qui a déclenché l’événement est généralement perdue. Il en résulte que les gestionnaires d’événements et les processeurs de tâches utilisent souvent des sessions administratives pour effectuer leurs tâches. Différentes approches sont envisageables pour résoudre ce problème, chacune ayant ses avantages et ses inconvénients :

1. Transmettez le `user-id` dans la charge utile de l’événement et utilisez l’emprunt d’identité.

   **Avantages :** facilité d’utilisation.

   **Inconvénients : utilisation** continue  `loginAdministrative()`. Il réauthentifie une requête qui a déjà été authentifiée.

1. Créez ou réutilisez un utilisateur de service ayant accès aux données.

   **Avantages :** cohérent par rapport à la conception actuelle. Nécessite un minimum de modifications.

   **Inconvénients :** Les utilisateurs de services très puissants doivent être flexibles, ce qui peut facilement conduire à des réaffectations de privilèges. Évite le modèle de sécurité.

1. Transmettez une sérialisation de `Subject` dans la charge utile du événement et créez une `ResourceResolver` en fonction de ce sujet. Un exemple serait d’utiliser le JAAS `doAsPrivileged` dans le `ResourceResolverFactory`.

   **Avantages :** mise en œuvre propre du point de vue de la sécurité. Cela évite la réauthentification et utilise les privilèges d’origine. Le code relevant de la sécurité est transparent pour le consommateur de l’événement.

   **Inconvénients :** Besoin de refaçonner. Le fait que le code relevant de la sécurité soit transparent pour le consommateur de l’événement peut également entraîner des problèmes.

La troisième approche est actuellement la technique de traitement préférée.

## Processus de workflow {#workflow-processes}

Dans les mises en œuvre de processus de workflow, la session utilisateur correspondante ayant déclenché le workflow est généralement perdue. En conséquence, les processus de workflow utilisent souvent des sessions administratives pour effectuer leurs tâches.

Pour résoudre ces problèmes, il est recommandé que les mêmes approches mentionnées dans les [Traitement des événements, des préprocesseurs de réplication et des tâches](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs) soient utilisées.

## Processeurs POST Sling et pages supprimées  {#sling-post-processors-and-deleted-pages}

Plusieurs sessions administratives sont utilisées dans les mises en œuvre de processeur POST Sling. En règle générale, les sessions administratives sont utilisées pour accéder aux nœuds qui sont en attente de suppression dans le POST en cours de traitement. Par conséquent, ils ne sont plus disponibles via la session de requête. Les nœuds en attente de suppression sont accessibles pour révéler les métadonnées qui ne devraient pas être accessibles dans le cas contraire.
