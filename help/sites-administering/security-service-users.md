---
title: Utilisateurs du service dans Adobe Experience Manager
description: Découvrez les utilisateurs du service dans Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: ccd8577b-3bbf-40ba-9696-474545f07b84
feature: Security
source-git-commit: f317783f3320e3987c7468aa0b2471e525b0387a
workflow-type: tm+mt
source-wordcount: '1797'
ht-degree: 46%

---


# Utilisateurs du service dans Adobe Experience Manager (AEM) {#service-users-in-aem}

## Présentation {#overview}

La principale façon d’obtenir un résolveur de session d’administration ou de ressource dans AEM consistait à utiliser les méthodes `SlingRepository.loginAdministrative()` et `ResourceResolverFactory.getAdministrativeResourceResolver()` fournies par Sling.

Toutefois, aucune de ces méthodes n’a été conçue selon le [principe de moindre privilège](https://fr.wikipedia.org/wiki/Principe_de_moindre_privil%C3%A8ge). En conséquence, il est trop facile d’ignorer au cours du développement la planification d’une structure et de niveaux de contrôle d’accès (ACL) appropriés pour leur contenu dès le début. Si une vulnérabilité est présente dans un tel service, elle conduit souvent à des réaffectations de privilèges `admin`, même si le code n’a pas besoin de privilèges d’administration pour fonctionner.

## Comment supprimer les sessions d’administration {#how-to-phase-out-admin-sessions}

### Priorité 0 : la fonctionnalité est-elle principale/nécessaire/abandonnée ? {#priority-is-the-feature-active-needed-derelict}

Il peut y avoir des cas où la session d’administration n’est pas utilisée, ou la fonction est complètement désactivée. Si tel est le cas avec votre mise en œuvre, assurez-vous de supprimer la fonction entièrement ou accompagnez-la d’une [instruction nulle](https://fr.wikipedia.org/wiki/Instruction_nulle).

### Priorité 1 : Utilisation De La Session De Requête {#priority-use-the-request-session}

Lorsque cela est possible, refactorisez votre fonction de sorte que la session de requête authentifiée donnée puisse être utilisée pour écrire ou lire du contenu. Si cela n&#39;est pas possible, il est souvent possible d&#39;y parvenir en appliquant les priorités suivantes.

### Priorité 2 : Restructuration du contenu {#priority-restructure-content}

De nombreux problèmes peuvent être résolus en restructurant le contenu. Gardez ces règles simples à l’esprit lorsque vous effectuez la restructuration :

* **Modifier le contrôle d’accès**

   * Assurez-vous que les utilisateurs ou les groupes qui ont réellement besoin d’un accès ont bien accès à .

* **Affiner la structure de contenu**

   * Déplacez-le vers d’autres emplacements, par exemple lorsque le contrôle d’accès correspond aux sessions de requête disponibles ;
   * modifier la granularité du contenu ;

* **Refactorisation du code afin qu’il corresponde à un service approprié**

   * Redéfinissez la logique métier du code JSP en service. Cela permet une modélisation de contenu différente.

Veillez également à ce que toutes les nouvelles fonctionnalités que vous développez respectent les principes suivants :

* **Les exigences de sécurité doivent déterminer la structure de contenu**

   * La gestion du contrôle d’accès doit être naturelle
   * Le contrôle d’accès doit être appliqué par le référentiel, et non par l’application.

* **Utilisation des types de noeuds**

   * Restreindre l’ensemble des propriétés qui peuvent être définies

* **Respectez les paramètres de confidentialité**

   * S’il existe des profils privés, par exemple, ne pas exposer l’image de profil, l’email ou le nom complet figurant sur le profil privé. `/profile` noeud .

## Contrôle d’accès strict {#strict-access-control}

Si vous appliquez le contrôle d’accès lors de la restructuration du contenu ou lorsque vous le faites pour un nouvel utilisateur, vous devez appliquer les listes ACL les plus strictes possibles. Utilisez tous les moyens de contrôle d’accès possibles :

* Par exemple, plutôt que d’appliquer `jcr:read` sur `/apps`, appliquez-le uniquement sur `/apps/*/components/*/analytics`.

* Utilisez des [restrictions](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html).

* Application de listes de contrôle d’accès pour les types de noeuds
* Limiter les autorisations

   * Par exemple, si vous avez besoin de l’autorisation d’écriture uniquement pour les propriétés, ne donnez pas l’autorisation `jcr:write`, utilisez plutôt `jcr:modifyProperties`.

## Utilisateurs de services et mises en correspondance {#service-users-and-mappings}

Si ce qui précède échoue, Sling 7 propose un service de mappage des utilisateurs de service, qui permet de configurer un mappage de lot à utilisateur et deux méthodes d’API correspondantes :

* [`SlingRepository.loginService()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)
* [`ResourceResolverFactory.getServiceResourceResolver()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)

Les méthodes renvoient un résolveur de session/ressource avec les privilèges d’un utilisateur configuré uniquement. Ces méthodes présentent les caractéristiques suivantes :

* Elles permettent de mettre en correspondance les services avec les utilisateurs.
* Ils permettent de définir des utilisateurs de sous-services.
* Le point central de configuration est le suivant : `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`.
* `service-id` = `service-name` [&quot;:&quot; subservice-name]

* `service-id` est mis en correspondance avec un résolveur de ressource et/ou un ID d’utilisateur de référentiel JCR pour l’authentification.
* `service-name` est le nom symbolique du lot qui fournit le service.

## Autres Recommendations {#other-recommendations}

### Remplacement de la session d’administration par un utilisateur de service {#replacing-the-admin-session-with-a-service-user}

Un utilisateur de service est un utilisateur JCR sans mot de passe défini et avec un jeu minimal d’autorisations nécessaires pour effectuer une tâche spécifique. Si aucun mot de passe n’est défini, il ne sera pas possible de se connecter avec un utilisateur du service.

Une façon de rendre une session administrative obsolète consiste à la remplacer par des sessions d’utilisateurs de services. Il peut également être remplacé par plusieurs utilisateurs de sous-service si nécessaire.

Pour remplacer la session d’administrateur par un utilisateur de service, procédez comme suit :

1. Identifiez les autorisations nécessaires à votre service, en gardant à l’esprit le principe de la moindre autorisation.
1. Vérifiez s’il existe déjà un utilisateur disponible ayant exactement la configuration de permissions dont vous avez besoin. Créez un utilisateur de service système si aucun utilisateur existant ne correspond à vos besoins. RTC est nécessaire pour créer un utilisateur de service. Parfois, il est logique de créer plusieurs utilisateurs de sous-services (par exemple, un pour l’écriture et un autre pour la lecture) pour compartimenter encore plus l’accès.
1. Configurez et testez des listes ACE pour votre utilisateur.
1. Ajoutez une mise en correspondance `service-user` pour votre service et pour les `user/sub-users`

1. Rendez la fonction Sling d’utilisateur de service disponible pour votre lot : mettez à jour vers la version la plus récente de `org.apache.sling.api`.

1. Remplacez `admin-session` dans votre code par les API `loginService` ou `getServiceResourceResolver`.

## Création d’un utilisateur de service {#creating-a-new-service-user}

Après avoir vérifié qu’aucun utilisateur de la liste des utilisateurs du service AEM ne s’applique à votre cas d’utilisation et que les problèmes RTC correspondants ont été approuvés, vous pouvez poursuivre et ajouter le nouvel utilisateur au contenu par défaut.

Il est recommandé de créer un utilisateur de service pour utiliser l’explorateur de référentiel à l’adresse *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*.

L’objectif est d’obtenir un `jcr:uuid` qui est obligatoire pour créer l’utilisateur via une installation de module de contenu.

Vous pouvez créer des utilisateurs de services de la façon suivante :

1. En vous rendant dans l’explorateur de référentiel sur *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*.
1. Connectez-vous en tant qu’administrateur en appuyant sur la touche **Connexion** dans le coin supérieur gauche de l’écran.
1. Ensuite, créez et nommez votre utilisateur système. Pour créer l’utilisateur en tant qu’utilisateur système, définissez le chemin intermédiaire comme `system` et ajoutez des sous-dossiers facultatifs en fonction de vos besoins :

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. Vérifiez que le nœud d’utilisateur système se présente comme suit :

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >Aucun type de mixin n’est associé aux utilisateurs du service. Cela signifie qu’il n’y a aucune politique de contrôle d’accès pour les utilisateurs système.

En ajoutant le fichier content.xml correspondant au contenu du lot, assurez-vous que vous avez défini le `rep:authorizableId` et que le type principal est `rep:SystemUser`. Il doit ressembler à ceci :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## Ajout d’une modification de configuration à la configuration ServiceUserMapper {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

Pour ajouter un mappage de votre service aux utilisateurs système correspondants, créez une configuration de fabrique pour la variable [`ServiceUserMapper`](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html) service. Pour conserver ce module, une telle configuration peut être fournie à l’aide de la variable [Mécanisme de modification Sling](https://issues.apache.org/jira/browse/SLING-3578). La méthode recommandée pour installer de telles configurations avec votre lot consiste à utiliser [Chargement initial du contenu Sling](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html):

1. Créez un sous-dossier SLING-INF/content sous le dossier src/main/resources de votre lot.
1. Dans ce dossier, créez un fichier nommé org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.modified-&lt;some unique=&quot;&quot; name=&quot;&quot; for=&quot;&quot; your=&quot;&quot; factory=&quot;&quot; configuration=&quot;&quot;>.xml avec le contenu de votre configuration d’usine (y compris tous les mappages utilisateur de sous-service). Exemple :

1. Créez un sous-dossier `SLING-INF/content` sous le dossier `src/main/resources` de votre lot.
1. Dans ce dossier, créez un fichier `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` avec le contenu de votre configuration d’usine, y compris tous les mappages utilisateur de sous-service.

   À titre d’illustration, prenez le fichier appelé `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`:

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

1. Référencez le contenu initial Sling dans la configuration de `maven-bundle-plugin` dans le fichier `pom.xml` du lot. Exemple :

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. Installez votre lot et assurez-vous que la configuration d’usine est installée. Vous pouvez le faire en procédant comme suit :

   * Accédez à la console web à l’adresse *https://serverhost:serveraddress/system/console/configMgr*.
   * Recherchez **Amendement du service de mappage des utilisateurs de service Apache Sling**.
   * Cliquez sur le lien pour vérifier si la configuration appropriée est en place.

## Traitement des sessions partagées dans les services {#dealing-with-shared-sessions-in-services}

Les appels à `loginAdministrative()` apparaissent souvent avec les sessions partagées. Ces sessions sont acquises lors de l’activation du service et ne sont déconnectées qu’après l’arrêt du service. Bien qu’il s’agisse d’une pratique courante, cela débouche sur deux problèmes :

* **Sécurité** : ces sessions d’administrateur sont utilisées pour mettre en cache et renvoyer les ressources ou d’autres objets qui sont liés à la session partagée. Plus loin dans la pile d’appels, ces objets peuvent être adaptés aux sessions ou aux résolveurs de ressources avec des privilèges élevés. Il n’est souvent pas clair pour l’appelant qu’il s’agit d’une session d’administration avec laquelle ils opèrent.
* **Performances :** Dans Oak, les sessions partagées peuvent entraîner des problèmes de performances et il n’est pas recommandé de les utiliser.

La solution la plus évidente au risque de sécurité est de remplacer simplement l’appel `loginAdministrative()` par un appel `loginService()` à un utilisateur disposant d’autorisations limitées. Toutefois, cette opération n’aura aucune incidence sur une éventuelle dégradation des performances. Vous pouvez limiter ces éventuelles dégradations en incluant toutes les informations requises dans un objet qui n’est plus associé à la session. Ensuite, créez (ou détruisez) la session à la demande.

L’approche recommandée consiste à refactoriser l’API du service afin que l’appelant puisse contrôler la création/destruction de la session.

## Sessions d’administration dans les JSP {#administrative-sessions-in-jsps}

Les JSP ne peuvent pas utiliser `loginService()` car il n’y a aucun service associé. Toutefois, les sessions administratives dans les JSP indiquent généralement une violation du paradigme MVC.

Ce problème peut être résolu de deux façons :

1. Restructurer le contenu de manière à pouvoir le manipuler avec la session utilisateur ;
1. Extraire la logique vers un service qui fournit une API qui peut ensuite être utilisée par le JSP.

La première méthode est préférable.

## Événements de traitement, préprocesseurs de réplication et tâches {#processing-events-replication-preprocessors-and-jobs}

Lors du traitement d’événements ou de tâches, et parfois de workflows, la session correspondante qui a déclenché l’événement est perdue. Il en résulte que les gestionnaires d’événements et les processeurs de tâches utilisent souvent des sessions administratives pour effectuer leurs tâches. Il existe différentes approches concevables pour résoudre ce problème, chacune présentant ses avantages et ses inconvénients :

1. Transmettez l’`user-id` dans le payload de l’événement et utilisez l’emprunt d’identité.

   **Avantages :** facilité d’utilisation.

   **Inconvénients :** continue d’utiliser `loginAdministrative()`. Elle réauthentifie une requête qui a déjà été authentifiée.

1. Créez ou réutilisez un utilisateur de service ayant accès aux données.

   **Avantages :** cohérent par rapport à la conception actuelle. Nécessite peu de modifications.

   **Inconvénients :** Nécessite que les utilisateurs puissants du service soient flexibles, ce qui peut facilement conduire à des réaffectations de privilèges. Évite le modèle de sécurité.

1. Transmettez une sérialisation du `Subject` dans le payload d’événement et créez un `ResourceResolver` basé sur cet objet. Un exemple serait d’utiliser le JAAS `doAsPrivileged` dans le `ResourceResolverFactory`.

   **Avantages :** mise en œuvre propre du point de vue de la sécurité. Il évite la réauthentification et fonctionne avec les privilèges d’origine. Le code pertinent pour la sécurité est transparent pour le consommateur de l’événement.

   **Inconvénients :** nécessité de refactoriser. Le fait que le code approprié pour la sécurité soit transparent pour le consommateur de l’événement peut également entraîner des problèmes.

La troisième méthode consiste à privilégier la technique de traitement.

## Processus de workflow {#workflow-processes}

Dans les implémentations de processus de workflow, la session utilisateur correspondante qui a déclenché le workflow est perdue. Cela entraîne des processus de workflow qui utilisent souvent des sessions administratives pour effectuer leur travail.

Pour résoudre ces problèmes, il est recommandé d’utiliser les mêmes méthodes que celles mentionnées dans la section [Événements de traitement, préprocesseurs de réplication et tâches](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs) à utiliser.

## Traitateurs de POST Sling et pages supprimées {#sling-post-processors-and-deleted-pages}

Plusieurs sessions administratives sont utilisées dans les mises en œuvre de processeur POST Sling. En règle générale, les sessions administratives sont utilisées pour accéder aux nœuds qui sont en attente de suppression dans le POST en cours de traitement. Par conséquent, ils ne sont plus disponibles via la session de requête. Un noeud en attente de suppression peut être accessible pour révéler des métadonnées qui ne devraient pas être accessibles dans le cas contraire.
