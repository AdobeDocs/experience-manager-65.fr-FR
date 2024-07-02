---
title: Renforcer et sécuriser AEM Forms dans un environnement OSGi
description: Découvrez les recommandations et les bonnes pratiques relatives à la sécurisation d’AEM Forms sur un serveur OSGi.
topic-tags: Security
role: Admin,User
exl-id: 5da3cc59-4243-4098-b1e0-438304fcd0c5
solution: Experience Manager, Experience Manager Forms
feature: Document Security,Adaptive Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '1434'
ht-degree: 100%

---

# Renforcer et sécuriser AEM Forms dans un environnement OSGi {#hardening-and-securing-aem-forms-on-osgi-environment}

Découvrez les recommandations et les bonnes pratiques relatives à la sécurisation d’AEM Forms sur un serveur OSGi.

La sécurisation ’’un environnement serveur est d’une importance primordiale pour une entreprise. Cet article fournit des conseils et des pratiques recommandées de sécurisation des serveurs exécutant AEM Forms. Il ne vise pas à expliquer de manière exhaustive comment renforcer des hôtes pour votre système d’exploitation. Cet article décrit plutôt les différents paramètres de renforcement de la sécurité que vous devez implémenter pour améliorer la sécurité de votre application déployée. Toutefois, pour garantir la sécurité des serveurs d’applications, vous devez également mettre en œuvre des procédures de surveillance, de détection et de réponse de sécurité, en plus des recommandations fournies dans cet article. Le document contient également les bonnes pratiques et les directives relatives à la sécurisation des informations d’identification personnelles (PII).

Cet article est destiné aux consultants, aux spécialistes de la sécurité, aux architectes de systèmes et aux professionnels de l’informatique chargés de planifier le développement et le déploiement d’application ou d’infrastructure d’AEM Forms. Ces rôles comprennent les rôles communs suivants :

* Les ingénieures et ingénieurs informatiques et d’exploitation qui doivent déployer des applications web et des serveurs sécurisés dans leurs propres organisations ou dans celles de leur clientèle.
* Les architectes et les planificateurs, qui sont chargés de planifier les efforts architecturaux des clients dans leur entreprise.
* Les spécialistes de la sécurité informatique qui œuvrent à la sécurité des plateformes de leur organisation.
* Les consultantes et consultants d’Adobe et leurs partenaires qui ont besoin de ressources détaillées pour la clientèle et les partenaires.

L’image suivante affiche les composants et les protocoles utilisés dans un déploiement AEM Forms classique, y compris la topologie de pare-feu appropriée :

![typical-architecture](assets/typical-architecture.png)

AEM Forms est hautement personnalisable et compatible avec de nombreux environnements. Certaines des recommandations peuvent ne pas s’appliquer à votre organisation.

## Couche de transport sécurisée {#secure-transport-layer}

Les vulnérabilités de sécurité des couches de transport comptent parmi les premières menaces qui affectent les serveurs d’applications accessibles par Internet ou par un intranet. Cette section décrit le processus de renforcement des hôtes du réseau contre ces vulnérabilités. Elle traite de la segmentation du réseau, du renforcement de la pile TCP/IP (Transmission Control Protocol/Internet Protocol) et de l’utilisation de pare-feux pour protéger les hôtes.

### Limiter les points dʼentrée ouverts  {#limit-open-endpoints}

Une entreprise peut configurer un pare-feu externe pour limiter l’accès entre un utilisateur final et une batterie de publication AEM Forms. L’entreprise peut également avoir un pare-feu interne pour limiter l’accès entre une batterie de publication et d’autres dans des éléments d’entreprise (par exemple, instance de création, instance de traitement, bases de données). Autorisez les pare-feu pour autoriser l’accès à un nombre limité d’URL AEM Forms pour les utilisateurs finaux et au sein des éléments d’entreprise :

#### Configurer le pare-feu externe  {#configure-external-firewall}

Vous pouvez configurer un pare-feu externe pour permettre à certaines URL AEM Forms d’accéder à Internet. L’accès à ces URL est nécessaire pour remplir ou envoyer un formulaire adaptatif, HTML5, une lettre Correspondence Management ou pour se connecter à un serveur AEM Forms :

<table> 
 <tbody>
  <tr>
   <td>Composant</td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>Formulaires adaptatifs</td> 
   <td>
    <ul> 
     <li>/content/dam/formsanddocuments/AF_PATH/jcr:content</li> 
     <li>/etc/clientlibs/fd/</li> 
     <li>/content/forms/af/AF_PATH</li> 
     <li>/libs/granite/csrf/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>Formulaires HTML5</td> 
   <td>
    <ul> 
     <li>/content/forms/formsets/profiles/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>Gestion des correspondances </td> 
   <td>
    <ul> 
     <li>/aem/forms/createcorrespondence* </li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>Portail Formulaires </td> 
   <td>
    <ul> 
     <li>/content/forms/portal/</li> 
     <li>/libs/cq/ui/widgets*</li> 
     <li>/libs/cq/security/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td> Application AEM Forms</td> 
   <td>
    <ul> 
     <li>/j_security_check*</li> 
     <li>/soap/services/AuthenticationManagerService</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

#### Configurer le pare-feu interne  {#configure-internal-firewall}

Vous pouvez configurer le pare-feu interne pour permettre à certains composants AEM Forms (par exemple, l’instance de création, l’instance de traitement, les bases de données) de communiquer avec la batterie de publication et d’autres composants internes mentionnés dans le diagramme de topologie :

<table> 
 <tbody>
  <tr>
   <td>Hôte<br /> </td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>Batterie de publication (nœuds de publication)</td> 
   <td>/bin/receive</td> 
  </tr>
  <tr>
   <td>Serveur de traitement</td> 
   <td>/content/forms/fp/*</td> 
  </tr>
  <tr>
   <td>Serveur du module complémentaire Forms Workflow (serveur AEM Forms on JEE)</td> 
   <td>/soap/sdk</td> 
  </tr>
 </tbody>
</table>

#### Configurer les autorisations de référentiel et les listes de contrôle d’accès (ACL) {#setup-repository-permissions-and-access-control-lists-acls}

Par défaut, les ressources disponibles sur les nœuds de publication sont accessibles à tous. L’accès en lecture seule est activé pour toutes les ressources. Il est nécessaire pour autoriser l’accès anonyme. Si vous envisagez de restreindre l’affichage des formulaires et de n’envoyer l’accès qu’aux utilisateurs et utilisatrices authentifiés, utilisez un groupe commun pour autoriser uniquement les utilisateurs et utilisatrices authentifiés à disposer d’un accès en lecture seule aux ressources disponibles sur les nœuds de publication. Les emplacements/répertoires suivants contiennent des ressources de formulaire qui nécessitent un renforcement (accès en lecture seule pour les utilisateurs et utilisatrices authentifiés) :

* /content/&amp;ast;
* /etc.clientlibs/fd/&amp;ast;
* /libs/fd/&amp;ast;

## Gérer de manière sécurisée des données de formulaire  {#securely-handle-forms-data}

AEM Forms stocke les données dans des emplacements prédéfinis et des dossiers temporaires. Vous devez sécuriser les données pour empêcher une utilisation non autorisée.

### Configurer le nettoyage périodique du dossier temporaire {#setup-periodic-cleanup-of-temporary-folder}

Lorsque vous configurez des formulaires pour des pièces jointes, des composants de vérification ou d’aperçu, les données correspondantes sont stockées sur les nœuds de publication sous /tmp/fd/. Les données sont régulièrement purgées. Vous pouvez modifier la tâche de purge de données par défaut afin de la rendre plus agressive. Pour modifier la tâche planifiée de purge des données, ouvrez la console web AEM, ouvrez la tâche de nettoyage de stockage temporaire AEM Forms et modifiez l’expression Cron.

Dans les scénarios mentionnés ci-dessus, les données sont enregistrées uniquement pour les utilisateurs et utilisatrices authentifiés. De plus, les données sont protégées par des listes de contrôle d’accès (ACL). La modification de la purge des données est donc une étape supplémentaire pour sécuriser les informations.

### Données sécurisées enregistrées par l’action d’envoi du portail Formulaires {#secure-data-saved-by-forms-portal-submit-action}

Par défaut, l’action d’envoi du portail Formulaires des formulaires adaptatifs enregistre les données dans le référentiel local du nœud de publication. Les données sont enregistrées dans /content/forms/fp. **Il n’est pas recommandé de stocker des données sur l’instance de publication.**

Vous pouvez configurer le service de stockage pour qu’il envoie les données par le réseau vers le cluster de traitement sans rien enregistrer localement sur le nœud de publication. Le cluster de traitement se trouve dans une zone sécurisée derrière le pare-feu privé et les données restent protégées.

Utilisez les informations d’identification du serveur de traitement pour le service de paramètres AEM DS afin de publier les données du nœud de publication sur le serveur de traitement. Utilisez les informations d’identification d’une personne non administratrice restreinte disposant d’un accès en lecture-écriture au référentiel du serveur de traitement. Pour plus d’informations, voir [Configuration des services de stockage pour les brouillons et les envois](/help/forms/using/configuring-draft-submission-storage.md).

### Données sécurisées gérées par le modèle de données de formulaire (FDM) {#secure-data-handled-by-form-data-model-fdm}

Utilisez des comptes d’utilisateur disposant des privilèges requis minimum pour configurer des sources de données pour le modèle de données de formulaire (FDM). L’utilisation d’un compte d’administration peut fournir un accès ouvert aux métadonnées et aux entités de schéma à des utilisateurs et utilisatrices non autorisés.\
L’intégration de données fournit également des méthodes pour autoriser les demandes de service FDM. Vous pouvez insérer des mécanismes d’autorisation avant et après exécution pour valider une requête. Les requêtes de service sont générées lors du préremplissage d’un formulaire, de l’envoi d’un formulaire et de l’appel de services par le biais d’une règle.

**Autorisation de pré-traitement :** vous pouvez utiliser l’autorisation de prétraitement pour valider l’authenticité d’une requête avant de l’exécuter. Vous pouvez utiliser des entrées, des détails de service et de requête pour autoriser ou arrêter l’exécution de la requête. Vous pouvez renvoyer une exception d’intégration de données OPERATION_ACCESS_DENIED si l’exécution est arrêtée. Vous pouvez également modifier la requête cliente avant de l’envoyer pour exécution. Par exemple, en modifiant la saisie et en ajoutant des informations supplémentaires.

**Autorisation de post-traitement :** vous pouvez utiliser l’autorisation de post-traitement pour valider et contrôler les résultats avant de renvoyer les résultats à l’auteur de la requête. Vous pouvez également filtrer, supprimer et insérer des données dans les résultats.

### Limiter l’accès des utilisateurs et des utilisatrices {#limit-user-access}

Un ensemble différent de rôles d’utilisateurs et d’utilisatrices est requis pour les instances de création, de publication et de traitement. N’exécutez aucune instance avec des informations d’identification d’administrateur.

**Sur une instance de publication :**

* Seuls les utilisateurs et utilisatrices du groupe forms-users peuvent prévisualiser, créer des brouillons et envoyer des formulaires.
* Seuls les utilisateurs et utilisatrices du groupe cm-user-agent peuvent prévisualiser les lettres Correspondence Management.
* Désactivez tous les accès anonymes non indispensables.

**Sur une instance de création :**

* Il existe un ensemble différent de groupes prédéfinis avec des privilèges spécifiques pour chaque rôle. Attribuer des utilisateurs au groupe.

   * Un utilisateur ou une utilisatrice du groupe forms-user :

      * peut créer, remplir, publier et envoyer un formulaire ;
      * ne peut pas créer de formulaire adaptatif basé sur XDP ;
      * n’a pas l’autorisation d’écrire des scripts pour les formulaires adaptatifs ;
      * ne peut pas importer de XDP ou tout package contenant du XDP.

   * Un utilisateur ou une utilisatrice du groupe forms-power-user crée, remplit, publie et envoie tous les types de formulaires, écrit des scripts pour les formulaires adaptatifs, importe des modules contenant du XDP.
   * Un utilisateur ou une utilisatrice de template-authors et template-power-user peut prévisualiser et créer un modèle.
   * Un utilisateur ou une utilisatrice de fdm-authors peut créer et modifier un modèle de données de formulaire.
   * Un utilisateur ou une utilisatrice du groupe cm-user-agent peut créer, prévisualiser et publier des lettres Correspondence Management.
   * Un utilisateur ou une utilisatrice du groupe workflow-editors peut créer une application de boîte de réception et un modèle de workflow.

**Sur l’instance de traitement de création :**

* Pour les cas d’utilisation d’enregistrement et d’envoi à distance, créez un utilisateur ou une utilisatrice avec des autorisations de lecture, de création et de modification sur le chemin content/form/fp du référentiel crx-repository. 
* Ajoutez un utilisateur ou une utilisatrice au groupe workflow-user pour permettre à un utilisateur ou une utilisatrice d’utiliser les applications de boîte de réception AEM.

## Éléments intranet sécurisés d’un environnement AEM Forms {#secure-intranet-elements-of-an-aem-forms-environment}

En général, les clusters de traitement et le module complémentaire Forms Workflow (AEM Forms on JEE) s’exécutent derrière un pare-feu. Donc, ils sont considérés comme sûrs. Vous pouvez toujours effectuer quelques étapes pour renforcer ces environnements :

### Cluster de traitement sécurisé {#secure-processing-cluster}

Un cluster de traitement s’exécute en mode création, mais ne l’utilise pas pour les activités de développement. N’autorisez pas un utilisateur normal à être inclus dans les groupes contenu-auteurs et formulaire-utilisateurs d’une grappe de traitement.

### Bonnes pratiques d’utilisation AEM pour sécuriser un environnement AEM Forms {#use-aem-best-practices-to-secure-an-aem-forms-environment}

Ce document fournit des instructions spécifiques à l’environnement AEM Forms. Veillez à ce que votre installation AEM sous-jacente soit sécurisée lors du déploiement. Pour obtenir des instructions détaillées, voir la documentation [Liste de contrôle de la sécurité](/help/sites-administering/security-checklist.md) d’AEM. 
