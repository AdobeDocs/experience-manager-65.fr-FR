---
title: Configuration de LDAP avec AEM 6
seo-title: Configuration de LDAP avec AEM 6
description: Découvrez comment configurer LDAP avec AEM.
seo-description: Découvrez comment configurer LDAP avec AEM.
uuid: 0007def4-86f0-401d-aa37-c8d49d5acea1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 5faf6ee5-9242-48f4-87a8-ada887a3be1e
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 67%

---


# Configuration de LDAP avec AEM 6 {#configuring-ldap-with-aem}

LDAP (**L** ightweight **D** irectory **A** ccess **P** rotocol) est un protocole utilisé pour accéder aux services d’annuaire centralisé. Cela permet de réduire l’effort de gestion des comptes utilisateur, car plusieurs applications peuvent accéder à ces comptes. L’un de ces serveurs LDAP est Active Directory. LDAP est souvent utilisé pour appliquer l’authentification unique, qui permet à un utilisateur d’accéder à plusieurs applications après s’être connecté une seule fois.

Les comptes utilisateur peuvent être synchronisés entre le serveur LDAP et le référentiel, les détails du compte LDAP étant enregistrés dans le référentiel. Cela permet d’affecter les comptes aux groupes de référentiel pour attribuer les autorisations et les privilèges requis.

Le référentiel utilise l’authentification LDAP pour authentifier ces utilisateurs, avec les informations d’identification transmises au serveur LDAP pour la validation, ce qui est requis avant d’autoriser l’accès au référentiel. Pour améliorer les performances, les informations d’identification validées peuvent être mises en cache par le référentiel, avec un délai d’expiration pour s’assurer que la revalidation se produit après une période appropriée.

Lorsqu’un compte est supprimé du serveur LDAP, la validation n’est plus effectuée et l’accès au référentiel est donc refusé. Les informations sur les comptes LDAP enregistrés dans le référentiel peuvent également être purgées.

L’utilisation de tels comptes est transparente pour vos utilisateurs, lesquels ne voient aucune différence entre les comptes d’utilisateur et de groupe créés à partir de LDAP et ceux créés uniquement dans le référentiel.

Dans AEM 6, la prise en charge de LDAP est fournie avec une nouvelle implémentation qui requiert un type de configuration différent de celui des versions précédentes.

Toutes les configurations LDAP sont désormais disponibles en tant que configurations OSGi. They can be configured via the Web Management console at:
`https://serveraddress:4502/system/console/configMgr`

Pour que LDAP fonctionne avec AEM, vous devez créer trois configurations OSGi :

1. Un fournisseur d’identités LDAP
1. Un gestionnaire de synchronisation
1. Un module de connexion externe

>[!NOTE]
>
>Regardez [Module de connexion externe Oak - Authentification avec LDAP et au-delà](https://docs.adobe.com/content/ddc/en/gems/oak-s-external-login-module---authenticating-with-ldap-and-beyon.html#) pour découvrir en détail les modules de connexion externes.
>
>Pour lire un exemple de configuration d’Experience Manager avec Apache DS, voir [Configuration d’Adobe Experience Manager 6.5 pour l’utilisation d’Apache Directory Service](https://helpx.adobe.com/experience-manager/using/configuring-aem64-apache-directory-service.html) (en anglais).

## Configuration du fournisseur d’identités LDAP {#configuring-the-ldap-identity-provider}

Le fournisseur d’identités LDAP est utilisé pour définir la manière dont les utilisateurs sont extraits du serveur LDAP.

Il figure dans la console de gestion sous le nom **Fournisseur d’identités LDAP Oak Apache Jackrabbit**.

Les options de configuration suivantes sont disponibles pour le fournisseur d’identités LDAP :

<table>
 <tbody>
  <tr>
   <td><strong>Nom du fournisseur LDAP</strong></td>
   <td>Nom de cette configuration du fournisseur LDAP.</td>
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
   <td><strong>Désactiver la vérification de certificat</strong></td>
   <td>Indique si la validation du certificat du serveur doit être désactivée.</td>
  </tr>
  <tr>
   <td><strong>DN de liaison</strong></td>
   <td>ND de l’utilisateur pour l’authentification. Si ce champ n’est pas renseigné, la liaison est anonyme.</td>
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
   <td><strong>Principal max du pool d’administrateurs</strong></td>
   <td>Taille principale maximale du pool de connexions d’administration.</td>
  </tr>
  <tr>
   <td><strong>Principal maximal du pool d’utilisateurs</strong></td>
   <td>Taille principale maximale du pool de connexions utilisateur.</td>
  </tr>
  <tr>
   <td><strong>ND de base utilisateur</strong></td>
   <td>Le nom unique pour les recherches d’utilisateurs</td>
  </tr>
  <tr>
   <td><strong>Classes d’objets utilisateur</strong></td>
   <td>Liste des classes d'objets qu'une entrée utilisateur doit contenir.</td>
  </tr>
  <tr>
   <td><strong>Attribut d’ID utilisateur</strong></td>
   <td>Nom de l’attribut contenant l’ID utilisateur.</td>
  </tr>
  <tr>
   <td><strong>Filtre supplémentaire utilisateur</strong></td>
   <td>Filtre LDAP supplémentaire à utiliser lors de la recherche d’utilisateurs. Le filtre final est formaté comme suit : '(&amp;(&lt;idAttr&gt;=&lt;userId&gt;)(objectclass=&lt;objectclass&gt;)&lt;extraFilter&gt;)' (user.extraFilter)'</td>
  </tr>
  <tr>
   <td><strong>Chemins DN utilisateur</strong></td>
   <td>Contrôle si le DN doit être utilisé pour calculer une partie du chemin intermédiaire.</td>
  </tr>
  <tr>
   <td><strong>ND de base du groupe</strong></td>
   <td>ND de base pour les recherches de groupe.</td>
  </tr>
  <tr>
   <td><strong>Classes d’objets de groupe</strong></td>
   <td>Liste des classes d'objets qu'une entrée de groupe doit contenir.</td>
  </tr>
  <tr>
   <td><strong>Attribut de nom de groupe</strong></td>
   <td>Nom de l’attribut qui contient le nom du groupe.</td>
  </tr>
  <tr>
   <td><strong>Filtre supplémentaire de groupe</strong></td>
   <td>Filtre LDAP supplémentaire à utiliser lors de la recherche de groupes. Le filtre final est formaté comme suit : '(&amp;(&lt;nameAttr&gt;=&lt;groupName&gt;)(objectclass=&lt;objectclass&gt;)&lt;extraFilter&gt;)'</td>
  </tr>
  <tr>
   <td><strong>Chemins DN du groupe</strong></td>
   <td>Contrôle si le DN doit être utilisé pour calculer une partie du chemin intermédiaire.</td>
  </tr>
  <tr>
   <td><strong>Attribut de membre du groupe</strong></td>
   <td>Attribut de groupe contenant le ou les membres d'un groupe.</td>
  </tr>
 </tbody>
</table>

## Configuration du gestionnaire de synchronisation {#configuring-the-synchronization-handler}

Le gestionnaire de synchronisation définit comment les utilisateurs et les groupes du fournisseur d’identités sont synchronisés avec le référentiel.

Il se trouve sous le nom **Gestionnaire de synchronisation par défaut Apache Jackrabbit Oak** dans la console de gestion.

Les options de configuration suivantes sont disponibles pour le gestionnaire de synchronisation :

<table>
 <tbody>
  <tr>
   <td><strong>Nom du gestionnaire de synchronisation</strong></td>
   <td>Nom de la configuration de synchronisation.</td>
  </tr>
  <tr>
   <td><strong>Heure d’expiration de l’utilisateur</strong></td>
   <td>Durée jusqu’à ce qu’un utilisateur synchronisé expire.</td>
  </tr>
  <tr>
   <td><strong>Abonnement automatique des utilisateurs</strong></td>
   <td>Liste des groupes auxquels un utilisateur synchronisé est ajouté automatiquement.</td>
  </tr>
  <tr>
   <td><strong>Mappage des propriétés utilisateur</strong></td>
   <td>Définition de mappage des listes des propriétés locales par rapport aux propriétés externes.</td>
  </tr>
  <tr>
   <td><strong>Préfixe de chemin d’accès utilisateur</strong></td>
   <td>Préfixe de chemin utilisé lors de la création de nouveaux utilisateurs.</td>
  </tr>
  <tr>
   <td><strong>Expiration de l’abonnement utilisateur</strong></td>
   <td>Heure après laquelle l’adhésion expire.<br /> </td>
  </tr>
  <tr>
   <td><strong>Profondeur d'imbrication de l'appartenance des utilisateurs</strong></td>
   <td>Renvoie la profondeur maximale de l’imbrication de groupes lors de la synchronisation des relations d’appartenance. Une valeur égale à 0 désactive la recherche de l’appartenance à un groupe. Une valeur égale à 1 ajoute uniquement les groupes directs d’un utilisateur. Cette valeur est sans effet lorsque des groupes individuels uniquement sont synchronisés dans le cadre de la synchronisation d’un ancêtre d’appartenance d’utilisateur.</td>
  </tr>
  <tr>
   <td><strong>Heure d'expiration du groupe</strong></td>
   <td>Durée jusqu’à l’expiration d’un groupe synchronisé.</td>
  </tr>
  <tr>
   <td><strong>Appartenance automatique au groupe</strong></td>
   <td>Liste des groupes auxquels un groupe synchronisé est ajouté automatiquement.</td>
  </tr>
  <tr>
   <td><strong>Mappage des propriétés du groupe</strong></td>
   <td>Définition de mappage des listes des propriétés locales par rapport aux propriétés externes.</td>
  </tr>
  <tr>
   <td><strong>Préfixe de chemin de groupe</strong></td>
   <td>Préfixe de chemin utilisé lors de la création de groupes.</td>
  </tr>
 </tbody>
</table>

## Module de connexion externe {#the-external-login-module}

Le module de connexion externe est placé sous **Module de connexion externe Apache Jackrabbit Oak**, dans la console de gestion.

>[!NOTE]
>
>Le module de connexion externe Apache Jackrabbit Oak met en œuvre les spécifications JAAS (Java Authentication and Authorization Service). Voir le [Guide de référence de la sécurité Oracle Java officiel](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) pour plus d’informations.

Son objectif est de définir quel fournisseur d’identités et quel gestionnaire de synchronisation utiliser, reliant ainsi les deux modules.

Les options de configuration suivantes sont disponibles :

| **Classement JAAS** | Spécification du classement (ordre de tri) de cette entrée de module de connexion. Les entrées sont triées dans l’ordre décroissant (les configurations ayant une valeur de rang supérieure apparaissent en premier). |
|---|---|
| **Indicateur de contrôle JAAS** | Propriété spécifiant si un LoginModule est OBLIGATOIRE, REQUIS, SUFFISANT ou FACULTATIF.Reportez-vous à la documentation de configuration JAAS pour plus de détails sur la signification de ces indicateurs. |
| **JAAS Realm** | Nom de domaine (ou nom de l&#39;application) pour lequel le LoginModule est enregistré. Si aucun nom de domaine n’est indiqué, le module de connexion est enregistré avec un domaine par défaut tel que configuré dans la configuration Felix JAAS. |
| **Nom du fournisseur d’identité** | Nom du fournisseur d&#39;identité. |
| **Nom du gestionnaire de synchronisation** | Nom du gestionnaire de synchronisation. |

>[!NOTE]
>
>Si vous envisagez plusieurs configurations LDAP avec votre instance AEM, vous devez créer des fournisseurs d’identité et des gestionnaires de synchronisation distincts pour chaque configuration.

## Configuration de LDAP via SSL {#configure-ldap-over-ssl}

Vous pouvez configurer AEM 6 pour vous authentifier auprès de LDAP via SSL en suivant la procédure ci-dessous :

1. Cochez la case **Utiliser SSL** ou **Utiliser TLS** lorsque vous configurez le [Fournisseur d’identités LDAP](#configuring-the-ldap-identity-provider).
1. Configurez le gestionnaire de synchronisation et le module de connexion externe en fonction de votre configuration.
1. Installez les certificats SSL sur votre machine virtuelle Java si nécessaire. Pour ce faire, vous pouvez utiliser l’outil keytool :

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. Testez la connexion au serveur LDAP.

### Création de certificats SSL {#creating-ssl-certificates}

Les certificats auto-signés peuvent être utilisés lors de la configuration d’AEM pour s’authentifier auprès d’AEM via SSL. Voici un exemple de méthode de travail utilisée pour générer des certificats à utiliser avec AEM.

1. Assurez-vous qu’une bibliothèque SSL est installée et fonctionne. Cette procédure utilise OpenSSL comme exemple.

1. Créez un fichier de configuration OpenSSL personnalisée (cnf). Pour ce faire, copiez le fichier de configuration **openssl.cnf **et personnalisez-le. On UNIX systems, it is usually located at `/usr/lib/ssl/openssl.cnf`

1. Créez la clé racine CA en exécutant la commande ci-dessous sur un terminal :

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. Créez ensuite un certificat auto-signé :

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. Examinez le certificat nouvellement généré pour vous assurer que tout est en règle :

   `openssl x509 -noout -text -in root-ca.crt`

1. Assurez-vous que tous les dossiers spécifiés dans le fichier de configuration de certificat (.cnf) existent. Si ce n’est pas le cas, créez-les.
1. Créez une source aléatoire, en exécutant, par exemple :

   `openssl rand -out private/.rand 8192`

1. Déplacez les fichiers .pem créés vers les emplacements définis dans le fichier .cnf.

1. Enfin, ajoutez le certificat au KeyStore Java.

## Activation de la journalisation du débogage {#enabling-debug-logging}

Vous pouvez activer la journalisation du débogage pour le fournisseur d’identités LDAP et le module de connexion externe afin de résoudre les problèmes de connexion.

Pour activer la journalisation du débogage, procédez comme suit :

1. Accédez à la console de gestion Web.
1. Recherchez « Apache Sling Logging Logger Configuration » et créez deux journaux avec les options suivantes :

* Niveau de consignation : Débogage
* Fichier journal logs/ldap.log
* Modèle de message : {0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Journal : org.apache.jackrabbit.oak.security.authentication.ldap

* Niveau de consignation : Débogage
* Fichier journal : logs/external.log
* Modèle de message : {0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Journal : org.apache.jackrabbit.oak.spi.security.authentication.external

## À propos de l’affiliation de groupe {#a-word-on-group-affiliation}

Les utilisateurs synchronisés via LDAP peuvent faire partie de différents groupes dans AEM. Ces groupes peuvent être des groupes LDAP externes qui seront ajoutés à AEM dans le cadre du processus de synchronisation, mais il peut également s’agir de groupes ajoutés séparément et ne faisant pas partie du schéma d’affiliation de groupe LDAP d’origine.

Dans la plupart des cas, il peut s’agir de groupes ajoutés par un administrateur AEM local ou par n’importe quel autre fournisseur d’identités.

Si un utilisateur est supprimé d’un groupe sur le serveur LDAP, cette suppression est également reflétée au niveau d’AEM lors de la synchronisation. Néanmoins, toutes les autres affiliations de groupe de l’utilisateur qui n’ont pas été ajoutées par LDAP restent en place.

AEM détecte et gère la purge des utilisateurs des groupes externes à l’aide de la propriété `rep:externalId`. Cette propriété est automatiquement ajoutée aux utilisateurs ou aux groupes synchronisés par le gestionnaire de synchronisation et contient des informations sur le fournisseur d’identités d’origine.

Pour plus d’informations, voir la documentation d’Apache Oak relative à la [Synchronisation des utilisateurs et des groupes](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html).

## Problèmes connus {#known-issues}

Si vous envisagez d’utiliser LDAP via SSL, assurez-vous que les certificats que vous utilisez sont créés sans l’option de commentaire Netscape. Si cette option est activée, l’authentification échoue avec une erreur de négociation SSL.

