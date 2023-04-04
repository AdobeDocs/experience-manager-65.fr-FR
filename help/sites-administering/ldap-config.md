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
workflow-type: tm+mt
source-wordcount: '1625'
ht-degree: 45%

---

# Configurer LDAP avec AEM 6 {#configuring-ldap-with-aem}

LDAP (**L** ightweight **D** irectory **A** ccess **P** rotocol) est un protocole utilisé pour accéder aux services d’annuaire centralisé. Cela permet de réduire les efforts requis pour gérer les comptes d’utilisateurs, car ils sont accessibles par plusieurs applications. L’un de ces serveurs LDAP est Active Directory. LDAP est souvent utilisé pour appliquer l’authentification unique, qui permet à un utilisateur d’accéder à plusieurs applications après s’être connecté une seule fois.

Les comptes utilisateur peuvent être synchronisés entre le serveur LDAP et le référentiel, les détails du compte LDAP étant enregistrés dans le référentiel. Cette fonctionnalité permet d’affecter les comptes aux groupes de référentiel pour l’allocation des autorisations et des privilèges requis.

Le référentiel utilise l’authentification LDAP pour authentifier ces utilisateurs, avec les informations d’identification transmises au serveur LDAP pour la validation, ce qui est requis avant d’autoriser l’accès au référentiel. Pour améliorer les performances, les informations d’identification validées peuvent être mises en cache par le référentiel, avec un délai d’expiration pour s’assurer que la revalidation se produit après une période appropriée.

Lorsqu’un compte est supprimé du serveur LDAP, la validation n’est plus accordée et l’accès au référentiel est refusé. Les détails des comptes LDAP enregistrés dans le référentiel peuvent également être purgés.

L’utilisation de tels comptes est transparente pour vos utilisateurs. En d’autres termes, ils ne voient aucune différence entre les comptes utilisateur et de groupe créés à partir de LDAP, et les comptes créés uniquement dans le référentiel.

Dans AEM 6, la prise en charge LDAP s’accompagne d’une nouvelle mise en oeuvre qui nécessite un type de configuration différent de celui des versions précédentes.

Toutes les configurations LDAP sont désormais disponibles en tant que configurations OSGi. Elles peuvent être configurées via la console de gestion web à l’adresse suivante :
`https://serveraddress:4502/system/console/configMgr`

Pour que LDAP fonctionne avec AEM, vous devez créer trois configurations OSGi :

1. Un fournisseur d’identités LDAP
1. Gestionnaire de synchronisation.
1. Module de connexion externe.

>[!NOTE]
>
>Regardez la vidéo [Module de connexion externe Oak - Authentification avec LDAP, et au-delà](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-oak-external-login-module-authenticating-with-ldap-and-beyond.html?lang=en) pour découvrir en détail les modules de connexion externes.
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
   <td>DN de l’utilisateur pour l’authentification. Si ce champ est vide, une liaison anonyme est exécutée.</td>
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
   <td>La liste des classes d’objets qu’une entrée utilisateur doit contenir.</td>
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
   <td>Attribut Groupe contenant un ou plusieurs membres d’un groupe.</td>
  </tr>
 </tbody>
</table>

## Configuration Du Gestionnaire De Synchronisation {#configuring-the-synchronization-handler}

Le gestionnaire de synchronisation définit la manière dont les utilisateurs et les groupes du fournisseur d’identité sont synchronisés avec le référentiel.

Il se trouve sous le noeud **Gestionnaire de synchronisation par défaut Apache Jackrabbit Oak** nom dans la console de gestion.

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
   <td>Liste des groupes auxquels un utilisateur synchronisé est automatiquement ajouté.</td>
  </tr>
  <tr>
   <td><strong>Mappage des propriétés de l’utilisateur</strong></td>
   <td>Définition du mapping de liste des propriétés locales à partir de propriétés externes.</td>
  </tr>
  <tr>
   <td><strong>Préfixe du chemin d’accès de l’utilisateur</strong></td>
   <td>Préfixe de chemin d’accès utilisé lors de la création d’utilisateurs.</td>
  </tr>
  <tr>
   <td><strong>Expiration de l’appartenance de l’utilisateur</strong></td>
   <td>Heure à partir de laquelle l’appartenance expire.<br /> </td>
  </tr>
  <tr>
   <td><strong>Niveau d’imbrication de l’appartenance de l’utilisateur</strong></td>
   <td>Renvoie la profondeur maximale de l’imbrication de groupes lorsque les relations d’appartenance sont synchronisées. Une valeur égale à 0 désactive la recherche de l’appartenance à un groupe. Une valeur égale à 1 ajoute uniquement les groupes directs d’un utilisateur. Cette valeur n’a aucun effet lors de la synchronisation de groupes individuels uniquement lors de la synchronisation d’une ancêtre d’appartenance d’utilisateur.</td>
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
   <td>Définition du mapping de liste des propriétés locales à partir de propriétés externes.</td>
  </tr>
  <tr>
   <td><strong>Préfixe du chemin d’accès du groupe</strong></td>
   <td>Préfixe de chemin d’accès utilisé lors de la création de groupes.</td>
  </tr>
 </tbody>
</table>

## Module de connexion externe {#the-external-login-module}

Le module de connexion externe se trouve sous le **Module de connexion externe Apache Jackrabbit Oak** sous la console de gestion.

>[!NOTE]
>
>Le module de connexion externe Apache Jackrabbit Oak met en oeuvre les spécifications Java™ Authentication and Authorization Service (JAAS). Voir [Guide de référence de sécurité Java™ Oracle officiel](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) pour plus d’informations.

Sa tâche consiste à définir le fournisseur d’identité et le gestionnaire de synchronisation à utiliser, liant efficacement les deux modules.

Les options de configuration suivantes sont disponibles :

| **Classement JAAS** | Spécification du classement (ordre de tri) de cette entrée de module de connexion. Les entrées sont triées dans un ordre décroissant (c’est-à-dire que les configurations avec classement de valeurs supérieures sont les premières). |
|---|---|
| **Indicateur de contrôle JAAS** | Propriété spécifiant si un module de connexion est REQUIS, REQUIS, SUFFISANT ou FACULTATIF. Pour plus d’informations sur la signification de ces indicateurs, consultez la documentation sur la configuration JAAS . |
| **Domaine JAAS** | Nom du domaine (ou nom de l’application) sur lequel le module de connexion est enregistré. Si aucun nom de domaine n’est fourni, LoginModule est enregistré avec un domaine par défaut tel que configuré dans la configuration Felix JAAS. |
| **Nom du fournisseur d’identité** | Nom du fournisseur d’identité. |
| **Nom du gestionnaire de synchronisation** | Nom du gestionnaire de synchronisation. |

>[!NOTE]
Si vous prévoyez plusieurs configurations LDAP avec votre instance AEM, des fournisseurs d’identité et des gestionnaires de synchronisation distincts doivent être créés pour chaque configuration.

## Configuration de LDAP sur SSL {#configure-ldap-over-ssl}

AEM 6 peut être configuré pour s’authentifier auprès de LDAP via SSL en suivant la procédure ci-dessous :

1. Vérifiez les **Utiliser SSL** ou **Utiliser TLS** des cases à cocher lors de la configuration de la variable [Fournisseur d’identités LDAP](#configuring-the-ldap-identity-provider).
1. Configurez le gestionnaire de synchronisation et le module de connexion externe en fonction de votre configuration.
1. Installez les certificats SSL dans votre machine virtuelle Java™, si nécessaire. Cette installation peut être effectuée à l’aide de l’outil keytool :

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. Testez la connexion au serveur LDAP.

### Création de certificats SSL {#creating-ssl-certificates}

Les certificats auto-signés peuvent être utilisés lors de la configuration d’AEM pour s’authentifier auprès de LDAP via SSL. Vous trouverez ci-dessous un exemple de procédure de travail pour générer des certificats à utiliser avec AEM.

1. Assurez-vous qu’une bibliothèque SSL est installée et fonctionne. Cette procédure utilise OpenSSL comme exemple.

1. Créez un fichier de configuration OpenSSL personnalisée (cnf). Cette configuration peut être effectuée en copiant le fichier de configuration par défaut **openssl.cnf ** et en le personnalisant. Sur les systèmes UNIX®, il se trouve à l’adresse `/usr/lib/ssl/openssl.cnf`

1. Créez la clé racine CA en exécutant la commande ci-dessous sur un terminal :

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. Créez ensuite un certificat autosigné :

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. Pour vérifier que tout est dans l’ordre, examinez le certificat nouvellement généré :

   `openssl x509 -noout -text -in root-ca.crt`

1. Assurez-vous que tous les dossiers spécifiés dans le fichier de configuration de certificat (.cnf) existent. Si ce n’est pas le cas, créez-les.
1. Créez une source aléatoire en exécutant, par exemple :

   `openssl rand -out private/.rand 8192`

1. Déplacez les fichiers .pem créés vers les emplacements définis dans le fichier .cnf.

1. Enfin, ajoutez le certificat au KeyStore Java™.

## Activation de la journalisation du débogage {#enabling-debug-logging}

La journalisation de débogage peut être activée pour le fournisseur d’identité LDAP et le module de connexion externe afin de résoudre les problèmes de connexion.

Pour activer la journalisation de débogage, procédez comme suit :

1. Accédez à la console de gestion Web.
1. Recherchez &quot;Configuration de l’enregistreur de journalisation Apache Sling&quot; et créez deux enregistreurs avec les options suivantes :

* Niveau de journal : Déboguer
* Fichier journal logs/ldap.log
* Motif de message : {0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Enregistreur : org.apache.jackrabbit.oak.security.authentication.ldap

* Niveau de journal : Déboguer
* Fichier journal : logs/external.log
* Motif de message : {0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Journal : org.apache.jackrabbit.oak.spi.security.authentication.external

## Un mot sur l’appartenance à un groupe {#a-word-on-group-affiliation}

Les utilisateurs synchronisés via LDAP peuvent faire partie de différents groupes dans AEM. Ces groupes peuvent être des groupes LDAP externes qui sont ajoutés à AEM dans le cadre du processus de synchronisation. Cependant, il peut également s’agir de groupes qui sont ajoutés séparément et qui ne font pas partie du schéma d’affiliation de groupe LDAP d’origine.

En règle générale, ces groupes sont ajoutés par un administrateur AEM local ou par tout autre fournisseur d’identité.

Si un utilisateur est supprimé d’un groupe sur le serveur LDAP, la modification est répercutée du côté AEM lors de la synchronisation. Cependant, toutes les autres affiliations de groupe de l’utilisateur qui n’ont pas été ajoutées par LDAP restent en place.

AEM détecte et gère la purge des utilisateurs à partir de groupes externes à l’aide de la fonction `rep:externalId` . Cette propriété est automatiquement ajoutée aux utilisateurs ou aux groupes synchronisés par le gestionnaire de synchronisation et contient des informations sur le fournisseur d’identités d’origine.

Voir la documentation Apache Oak sur [Synchronisation des utilisateurs et des groupes](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html).

## Problèmes connus {#known-issues}

Si vous envisagez d’utiliser LDAP sur SSL, assurez-vous que les certificats que vous utilisez sont créés sans l’option de commentaire Netscape. Si cette option est activée, l’authentification échoue avec une erreur de négociation SSL.
