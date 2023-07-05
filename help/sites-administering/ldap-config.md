---
title: Configurer LDAP avec AEM 6
description: Découvrez comment configurer LDAP avec AEM.
uuid: 0007def4-86f0-401d-aa37-c8d49d5acea1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 5faf6ee5-9242-48f4-87a8-ada887a3be1e
exl-id: 2ebca4fb-20f7-499c-96a0-4018eaeddc1a
source-git-commit: 768576e300b655962adc3e1db20fc5ec06a5ba6c
workflow-type: ht
source-wordcount: '1625'
ht-degree: 100%

---

# Configurer LDAP avec AEM 6 {#configuring-ldap-with-aem}

LDAP (**L** ightweight **D** irectory **A** ccess **P** rotocol) est un protocole utilisé pour accéder aux services d’annuaire centralisé. Cela permet de faciliter la gestion des comptes d’utilisateurs et d’utilisatrices, car plusieurs applications peuvent accéder à ces comptes. L’un de ces serveurs LDAP est Active Directory. LDAP est souvent utilisé pour appliquer l’authentification unique, qui permet à un utilisateur d’accéder à plusieurs applications après s’être connecté une seule fois.

Les comptes utilisateur peuvent être synchronisés entre le serveur LDAP et le référentiel, les détails du compte LDAP étant enregistrés dans le référentiel. Cette fonctionnalité permet d’affecter les comptes aux groupes de référentiel pour attribuer les autorisations et les privilèges requis.

Le référentiel utilise l’authentification LDAP pour authentifier ces utilisateurs, avec les informations d’identification transmises au serveur LDAP pour la validation, ce qui est requis avant d’autoriser l’accès au référentiel. Pour améliorer les performances, les informations d’identification validées peuvent être mises en cache par le référentiel, avec un délai d’expiration pour s’assurer que la revalidation se produit après une période appropriée.

Lorsqu’un compte est supprimé du serveur LDAP, la validation n’est plus accordée et l’accès au référentiel est donc refusé. Les détails des comptes LDAP enregistrés dans le référentiel peuvent également être purgés.

L’utilisation de tels comptes est transparente pour vos utilisateurs et utilisatrices. En effet, ils ne perçoivent aucune différence entre les comptes d’utilisateurs et d’utilisatrices et de groupe créés à partir de LDAP, et les comptes créés uniquement dans le référentiel.

Dans AEM 6, la prise en charge de LDAP s’accompagne d’une nouvelle implémentation qui nécessite un type de configuration différent de celui des versions précédentes.

Toutes les configurations LDAP sont désormais disponibles en tant que configurations OSGi. Elles peuvent être configurées via la console de gestion web à l’adresse suivante :
`https://serveraddress:4502/system/console/configMgr`

Pour que LDAP fonctionne avec AEM, vous devez créer trois configurations d’OSGi :

1. Un fournisseur d’identités LDAP
1. Un gestionnaire de synchronisation
1. Un module de connexion externe

>[!NOTE]
>
>Regardez la vidéo [Module de connexion externe Oak - Authentification avec LDAP, et au-delà](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-oak-external-login-module-authenticating-with-ldap-and-beyond.html?lang=fr) pour découvrir en détail les modules de connexion externes.
>
>Pour lire un exemple de configuration d’Experience Manager avec Apache DS, consultez la section [Configuration d’Adobe Experience Manager 6.5 pour l’utilisation d’Apache Directory Service](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/configuring-adobe-experience-manager-6-to-use-apache-directory/m-p/183805) (en anglais).

## Configuration du fournisseur d’identités LDAP {#configuring-the-ldap-identity-provider}

Le fournisseur d’identités LDAP est utilisé pour définir la manière dont les utilisateurs sont extraits du serveur LDAP.

Il figure dans la console de gestion sous le nom **Fournisseur d’identités LDAP Oak Apache Jackrabbit**.

Les options de configuration suivantes sont disponibles pour le fournisseur d’identités LDAP :

<table>
 <tbody>
  <tr>
   <td><strong>Nom du fournisseur LDAP</strong></td>
   <td>Nom de la configuration de ce fournisseur LDAP.</td>
  </tr>
  <tr>
   <td><strong>Nom d’hôte du serveur LDAP</strong><br /> </td>
   <td>Nom d’hôte du serveur LDAP</td>
  </tr>
  <tr>
   <td><strong>Port du serveur LDAP</strong></td>
   <td>Port du serveur LDAP</td>
  </tr>
  <tr>
   <td><strong>Utiliser SSL</strong></td>
   <td>Indique si une connexion SSL (LDAP) doit être utilisée.</td>
  </tr>
  <tr>
   <td><strong>Utiliser TLS</strong></td>
   <td>Indique si TLS doit être démarré sur les connexions.</td>
  </tr>
  <tr>
   <td><strong>Désactivation de la vérification de certificat</strong></td>
   <td>Indique si la validation du certificat du serveur doit être désactivée.</td>
  </tr>
  <tr>
   <td><strong>DN de liaison</strong></td>
   <td>DN de l’utilisateur pour l’authentification. Si ce champ n’est pas renseigné, la liaison est anonyme.</td>
  </tr>
  <tr>
   <td><strong>Lier le mot de passe</strong></td>
   <td>Mot de passe de l’utilisateur pour l’authentification</td>
  </tr>
  <tr>
   <td><strong>Délai de recherche</strong></td>
   <td>Durée jusqu’à ce que la recherche expire</td>
  </tr>
  <tr>
   <td><strong>max actif sur le pool d’administration</strong></td>
   <td>Nombre maximale d’actifs sur le pool de connexions d’administration.</td>
  </tr>
  <tr>
   <td><strong>Max actif sur le pool d’utilisateurs</strong></td>
   <td>Nombre maximal d’actifs sur le pool de connexions utilisateur.</td>
  </tr>
  <tr>
   <td><strong>DN de base de l’utilisateur</strong></td>
   <td>DN des recherches d’utilisateurs</td>
  </tr>
  <tr>
   <td><strong>Classes d’objet utilisateur</strong></td>
   <td>La liste des classes d’objets qu’une entrée d’utilisateur ou d’utilisatrice doit contenir.</td>
  </tr>
  <tr>
   <td><strong>Attribut d’identifiant utilisateur</strong></td>
   <td>Nom de l’attribut qui contient l’identifiant de l’utilisateur.</td>
  </tr>
  <tr>
   <td><strong>Filtre supplémentaire utilisateur</strong></td>
   <td>Filtre LDAP supplémentaire à utiliser lors de la recherche d’utilisateurs. Le filtre final est formaté comme suit : '(&amp;(&lt;idAttr&gt;=&lt;userId&gt;)(objectclass=&lt;objectclass&gt;)&lt;extraFilter&gt;)' (user.extraFilter)</td>
  </tr>
  <tr>
   <td><strong>Chemins de noms utilisateur</strong></td>
   <td>Contrôle si le DN doit être utilisé pour calculer une partie du chemin intermédiaire.</td>
  </tr>
  <tr>
   <td><strong>DN de base du groupe</strong></td>
   <td>DN de base pour les recherches de groupe.</td>
  </tr>
  <tr>
   <td><strong>Classes d’objet de groupe</strong></td>
   <td>La liste des classes d’objets qu’une entrée de groupe doit contenir.</td>
  </tr>
  <tr>
   <td><strong>Attribut de nom de groupe</strong></td>
   <td>Nom de l’attribut qui contient le nom du groupe.</td>
  </tr>
  <tr>
   <td><strong>Filtre supplémentaire de groupe</strong></td>
   <td>Filtre LDAP supplémentaire à utiliser lors de la recherche de groupes. Le filtre final est formaté comme suit : '(&amp;(&lt;nameAttr&gt;=&lt;groupName&gt;)(objectclass=&lt;objectclass&gt;)&lt;extraFilter&gt;)'</td>
  </tr>
  <tr>
   <td><strong>Chemins d’accès DN du groupe</strong></td>
   <td>Contrôle si le DN doit être utilisé pour calculer une partie du chemin intermédiaire.</td>
  </tr>
  <tr>
   <td><strong>Attribut du membre du groupe</strong></td>
   <td>Attribut de groupe contenant un ou plusieurs membres d’un groupe.</td>
  </tr>
 </tbody>
</table>

## Configurer le gestionnaire de synchronisation {#configuring-the-synchronization-handler}

Le gestionnaire de synchronisation définit la manière dont les utilisateurs et utilisatrices et les groupes du fournisseur d’identité sont synchronisés avec le référentiel.

Il se trouve sous le nom **Gestionnaire de synchronisation par défaut Apache Jackrabbit Oak** dans la console de gestion.

Les options de configuration suivantes sont disponibles pour le gestionnaire de synchronisation :

<table>
 <tbody>
  <tr>
   <td><strong>Nom du gestionnaire de synchronisation</strong></td>
   <td>Nom de la configuration de synchronisation.</td>
  </tr>
  <tr>
   <td><strong>Délai d’expiration de l’utilisateur</strong></td>
   <td>Durée jusqu’à ce qu’un utilisateur synchronisé expire.</td>
  </tr>
  <tr>
   <td><strong>Abonnement automatique des utilisateurs</strong></td>
   <td>Liste des groupes auxquels une personne synchronisée est automatiquement ajoutée.</td>
  </tr>
  <tr>
   <td><strong>Mappage des propriétés de l’utilisateur ou de l’utilisatrice</strong></td>
   <td>Définition du mappage de liste des propriétés locales à partir de propriétés externes.</td>
  </tr>
  <tr>
   <td><strong>Préfixe du chemin d’accès de l’utilisateur ou de l’utilisatrice</strong></td>
   <td>Préfixe de chemin d’accès utilisé lors de la création d’utilisateurs et d’utilisatrices.</td>
  </tr>
  <tr>
   <td><strong>Expiration de l’appartenance de l’utilisateur</strong></td>
   <td>Heure à partir de laquelle l’appartenance expire.<br /> </td>
  </tr>
  <tr>
   <td><strong>Niveau d’imbrication de l’appartenance de l’utilisateur</strong></td>
   <td>Renvoie la profondeur maximale de l’imbrication de groupes lorsque les relations d’appartenance sont synchronisées. Une valeur égale à 0 désactive la recherche de l’appartenance à un groupe. Une valeur égale à 1 ajoute uniquement les groupes directs d’un utilisateur. Cette valeur n’a aucun effet sur la synchronisation de groupes individuels, mais uniquement sur la synchronisation d’une ascendance d’abonnement d’utilisateurs et d’utilisatrices.</td>
  </tr>
  <tr>
   <td><strong>Délai d’expiration du groupe</strong></td>
   <td>Durée jusqu’à l’expiration d’un groupe synchronisé.</td>
  </tr>
  <tr>
   <td><strong>Appartenance automatique au groupe</strong></td>
   <td>Liste des groupes auxquels un groupe synchronisé est automatiquement ajouté.</td>
  </tr>
  <tr>
   <td><strong>Mappage des propriétés du groupe</strong></td>
   <td>Définition du mappage de liste des propriétés locales à partir de propriétés externes.</td>
  </tr>
  <tr>
   <td><strong>Préfixe du chemin d’accès du groupe</strong></td>
   <td>Le préfixe du chemin d’accès utilisé lors de la création des groupes.</td>
  </tr>
 </tbody>
</table>

## Le module de connexion externe {#the-external-login-module}

Le module de connexion externe se trouve sous le **Module de connexion externe Apache Jackrabbit Oak** de la console de gestion.

>[!NOTE]
>
>Le module de connexion externe Apache Jackrabbit Oak implémente les spécifications JAAS (Java™ Authentication and Authorization Service). Consultez le [Guide de référence de la sécurité d’Oracle Java officiel](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) pour plus d’informations.

Sa tâche consiste à définir le fournisseur d’identité et le gestionnaire de synchronisation à utiliser afin de lier les deux modules.

Les options de configuration suivantes sont disponibles :

| **Classement JAAS** | Spécification du classement (c’est-à-dire de l’ordre de tri) de cette entrée de module de connexion. Les entrées sont triées dans l’ordre descendant (les configurations ayant une valeur de rang supérieure apparaissent en premier). |
|---|---|
| **Indicateur de contrôle JAAS** | Propriété indiquant si le module de connexion est Obligatoire, Requis, Suffisant ou Facultatif. Pour plus d’informations sur la signification de ces indicateurs, consultez la documentation de la configuration JAAS. |
| **Domaine JAAS** | Nom du domaine (ou nom de l’application) sur lequel LoginModule est enregistré. Si aucun nom de domaine n’est indiqué, le module de connexion est enregistré dans un domaine par défaut tel que configuré dans la configuration JAAS Felix. |
| **Nom du fournisseur d’identité** | Nom du fournisseur d’identité. |
| **Nom du gestionnaire de synchronisation** | Nom du gestionnaire de synchronisation. |

>[!NOTE]
>Si vous envisagez plusieurs configurations LDAP avec votre instance d’AEM, vous devez créer des fournisseurs d’identité et des gestionnaires de synchronisation distincts pour chaque configuration.

## Configurer LDAP sur SSL {#configure-ldap-over-ssl}

Pour configurer AEM 6 afin qu’il puisse s’authentifier à l’aide du protocole LDAP sur SSL, suivez la procédure ci-dessous :

1. Vérifiez les cases à cocher **Utiliser SSL** ou **Utiliser TLS** lors de la configuration du [Fournisseur d’identité LDAP](#configuring-the-ldap-identity-provider).
1. Configurez le gestionnaire de synchronisation et le module de connexion externe en fonction de votre configuration.
1. Installez les certificats SSL sur votre machine virtuelle Java™, si nécessaire. Vous pouvez effectuer l’installation à l’aide de l’outil keytool :

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. Testez la connexion au serveur LDAP.

### Créer des certificats SSL {#creating-ssl-certificates}

Les certificats auto-signés peuvent être utilisés lors de la configuration d’AEM pour s’authentifier à l’aide de LDAP sur SSL. Vous trouverez ci-dessous un exemple de procédure de travail pour générer des certificats à utiliser avec AEM.

1. Assurez-vous qu’une bibliothèque SSL est installée et fonctionnelle. Cette procédure prend OpenSSL comme exemple.

1. Créez un fichier de configuration OpenSSL personnalisée (cnf). Vous pouvez effectuer cette configuration en copiant le fichier de configuration **openssl.cnf** par défaut et en le personnalisant. Sur les systèmes UNIX®, ce fichier se trouve dans `/usr/lib/ssl/openssl.cnf`.

1. Créez la clé racine CA en exécutant la commande ci-dessous sur un terminal :

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. Créez ensuite un certificat auto-signé :

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. Pour vérifier que tout est en ordre, examinez le certificat nouvellement généré :

   `openssl x509 -noout -text -in root-ca.crt`

1. Assurez-vous que tous les dossiers spécifiés dans le fichier de configuration de certificat (.cnf) existent. Si ce n’est pas le cas, créez-les.
1. Créez une graine aléatoire en exécutant, par exemple :

   `openssl rand -out private/.rand 8192`

1. Déplacez les fichiers .pem créés vers les emplacements définis dans le fichier .cnf.

1. Enfin, ajoutez le certificat au KeyStore Java™.

## Activer la journalisation du débogage {#enabling-debug-logging}

La journalisation du débogage peut être activée pour le fournisseur d’identité LDAP et le module de connexion externe afin de résoudre les problèmes de connexion.

Pour activer la journalisation du débogage, procédez comme suit :

1. Accédez à la console de gestion web.
1. Recherchez « Configuration du journal de journalisation Apache Sling » et créez deux journaux avec les options suivantes :

* Niveau de journal : débogage
* Fichier journal logs/ldap.log
* Motif de message : {0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Journal : org.apache.jackrabbit.oak.security.authentication.ldap

* Niveau de journal : débogage
* Fichier journal : logs/external.log
* Motif de message : {0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Journal : org.apache.jackrabbit.oak.spi.security.authentication.external

## Une remarque sur l’appartenance à un groupe {#a-word-on-group-affiliation}

Les utilisateurs synchronisés via LDAP peuvent faire partie de différents groupes dans AEM. Ces groupes peuvent être des groupes LDAP externes ajoutés à AEM dans le cadre du processus de synchronisation. Cependant, il peut également s’agir de groupes qui sont ajoutés séparément et qui ne font pas partie du schéma d’appartenance de groupe LDAP d’origine.

En règle générale, ces groupes sont ajoutés par l’administration locale d’AEM ou par tout autre fournisseur d’identité.

Si une personne est supprimée d’un groupe sur le serveur LDAP, cette suppression apparaît dans AEM lors de la synchronisation. Cependant, toutes les autres appartenances de groupe de la personne qui n’ont pas été ajoutées par LDAP restent en place.

AEM détecte et gère la purge des utilisateurs et utilisatrices des groupes externes à l’aide de la propriété `rep:externalId`. Cette propriété est automatiquement ajoutée aux utilisateurs et utilisatrices ou aux groupes synchronisés par le gestionnaire de synchronisation et contient des informations sur le fournisseur d’identités d’origine.

Voir la documentation Apache Oak sur la [synchronisation des utilisateurs et utilisatrice et des groupes](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html).

## Problèmes connus {#known-issues}

Si vous envisagez d’utiliser LDAP via SSL, assurez-vous que les certificats que vous utilisez sont créés sans l’option de commentaire Netscape. Si cette option est activée, l’authentification échoue avec une erreur SSL Handshake.
