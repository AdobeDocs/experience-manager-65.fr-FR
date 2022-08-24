---
title: Considérations générales sur la sécurité pour AEM Forms sur JEE
seo-title: General Security Considerations for AEM Forms on JEE
description: Découvrez comment préparer le renforcement de votre environnement AEM Forms sur JEE.
seo-description: Learn how to prepare for hardening your AEM Forms on JEE environment.
uuid: 4d098731-fc8f-41d7-98b5-5c2e31211614
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 64bc6018-2828-4634-9275-48f1d411452b
docset: aem65
role: Admin
exl-id: 3f150dd5-f486-4f16-9de9-035cde53b034
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 100%

---

# Considérations générales sur la sécurité pour AEM Forms sur JEE{#general-security-considerations-for-aem-forms-on-jee}

Cet article fournit des informations d’introduction qui vous aideront à préparer le renforcement de votre environnement AEM Forms. Elle inclut des informations prérequises sur la sécurité d’AEM Forms sur JEE, des systèmes d’exploitation, des serveurs d’applications et des bases de données. Passez en revue ces informations avant de continuer à verrouiller votre environnement.

## Informations de sécurité spécifiques aux revendeurs {#vendor-specific-security-information}

Cette section contient des informations sur la sécurité des systèmes d’exploitation, des serveurs d’applications et des bases de données intégrés à votre solution AEM Forms sur JEE.

Utilisez les liens proposés dans cette section pour accéder à des informations de sécurité spécifiques au revendeur de votre système d’exploitation, de votre base de données et de votre serveur d’applications.

### Informations sur la sécurité des systèmes d’exploitation {#operating-system-security-information}

Lorsque vous sécurisez votre système d’exploitation, veillez à implémenter soigneusement les mesures indiquées par le revendeur de votre système d’exploitation, parmi lesquelles :

* définir et contrôler les utilisateurs, les rôles et les droits ;
* surveiller les journaux et les journaux d’audit ;
* supprimer les services et les applications inutiles ;
* sauvegarder les fichiers.

Pour plus de détails sur la sécurité des systèmes d’exploitation pris en charge par AEM Forms sur JEE, consultez les ressources du tableau suivant :

<table>
 <thead>
  <tr>
   <th><p>Système d’exploitation</p> </th>
   <th><p>Ressource de sécurité</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM® AIX® 7.2</p> </td>
   <td><p><a href="https://www.ibm.com/support/knowledgecenter/ssw_aix_72/com.ibm.aix.security/security-kickoff.htm" target="_blank">Avantages de la sécurité IBM AIX</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft Windows Server® 2016 </p> </td>
   <td><p><a href="https://cloudblogs.microsoft.com/windowsserver/2017/08/22/now-available-windows-server-2016-security-guide/">Guide de sécurité Windows Server 2016</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Linux® AP ou ES</p> </td>
   <td><p><a href="https://access.redhat.com/documentation/fr-fr/red_hat_enterprise_linux/7/pdf/security_guide/red_hat_enterprise_linux-7-security_guide-fr-fr.pdf" target="_blank">Guide de sécurité Linux pour Red Hat Enterprise</a></p> </td>
  </tr>
  <tr>
   <td><p>Sun Solaris 11</p> </td>
   <td><p><a href="https://docs.oracle.com/cd/E53394_01/html/E54807/index.html" target="_blank">Recommandations relatives à la sécurité et au renforcement</a></p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 Update 3</td>
   <td><a href="https://docs.oracle.com/cd/E52668_01/E54670/E54670.pdf" target="_blank">Guide de sécurité pour la version 7</a><br /> </td>
  </tr>
  <tr>
   <td>CentOS 7<sup> </sup></td>
   <td><a href="https://wiki.centos.org/HowTos/OS_Protection" target="_blank">Documentation sur la protection</a></td>
  </tr>
 </tbody>
</table>

### Informations sur la sécurité des serveurs d’applications {#application-server-security-information}

Lorsque vous sécurisez votre serveur d’applications, veiller à implémenter soigneusement les mesures indiquées par le revendeur de votre serveur, parmi lesquelles :

* utiliser un nom d’utilisateur administrateur difficilement identifiable ;
* désactiver les services inutiles ;
* sécuriser le gestionnaire de console ;
* autoriser les cookies sûrs ;
* fermer les ports inutiles ;
* restreindre les clients par adresses ou domaines IP ;
* utiliser Java™ Security Manager pour limiter les droits par programme.

Pour plus de détails sur la sécurité des serveurs d’applications pris en charge par AEM Forms sur JEE, reportez-vous aux ressources indiquées dans le tableau ci-dessous.

<table>
 <thead>
  <tr>
   <th><p>Serveur d’applications</p> </th>
   <th><p>Ressource de sécurité</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Oracle WebLogic®</p> </td>
   <td><p>Recherchez « Understanding WebLogic Security » sur <a href="https://download.oracle.com/docs/">https://download.oracle.com/docs/</a>.</p> </td>
  </tr>
  <tr>
   <td><p>IBM WebSphere®</p> </td>
   <td><p><a href="https://www.ibm.com/developerworks/websphere/zones/was/security/" target="_blank">Sécurisation des applications dans leur environnement</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® JBoss®</p> </td>
   <td><p><a href="https://docs.jboss.org/author/display/AS7/Security+subsystem+configuration">Configuration du sous-système de sécurité</a></p> </td>
  </tr>
 </tbody>
</table>

### Informations sur la sécurité des bases de données {#database-security-information}

Lorsque vous sécurisez votre base de données, veillez à implémenter soigneusement les mesures indiquées par le revendeur de votre base de données, parmi lesquelles :

* restreindre les opérations avec des listes de contrôle d’accès (ACL) ;
* utiliser des ports non standard ;
* masquer la base de données derrière un pare-feu ;
* chiffrer les données sensibles avant de les écrire dans la base de données (consultez la documentation du fabricant de la base de données).

Pour plus de détails sur la sécurité des bases de données prises en charge par AEM Forms sur JEE, reportez-vous aux ressources indiquées dans le tableau ci-dessous.

<table>
 <thead>
  <tr>
   <th><p>Base de données</p> </th>
   <th><p>Ressource de sécurité</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM DB2® 11.1</p> </td>
   <td><p><a href="https://www.ibm.com/fr-fr/analytics/db2">Bibliothèque de la famille de produits DB2</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016</p> </td>
   <td>Recherchez « SQL Server 2016 : sécurité » sur le Web.</td>
  </tr>
  <tr>
   <td><p>MySQL 5</p> </td>
   <td><p><a href="https://dev.mysql.com/doc/refman/5.0/en/security.html">MySQL 5.0 General Security Issues</a></p> <p><a href="https://dev.mysql.com/doc/refman/5.1/en/security.html">MySQL 5.1 General Security Issues</a></p> </td>
  </tr>
  <tr>
   <td><p>Oracle® 12c</p> </td>
   <td><p>Reportez-vous au chapitre Security dans <a href="https://docs.oracle.com/database/121/TDPSG/GUID-6E2F4E53-5D87-4FCD-9C9C-6792217D7014.htm#TDPSG94426" target="_blank">Oracle 12g Documentation</a></p> </td>
  </tr>
 </tbody>
</table>

Ce tableau décrit les ports par défaut devant être ouverts pendant le processus de configuration d’AEM Forms sur JEE. Si vous vous connectez via https, reparamétrez les informations de port et les adresses IP en conséquence. Pour plus de détails sur la configuration des ports, reportez-vous au document *Installation et déploiement d’AEM Forms sur JEE* de votre serveur d’applications.

<table>
 <thead>
  <tr>
   <th><p>Produit ou service</p> </th>
   <th><p>le numéro de port ;</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>JBoss </p> </td>
   <td><p>8080</p> </td>
  </tr>
  <tr>
   <td><p>WebLo gic</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>Serveur géré WebLogic</p> </td>
   <td><p>Défini par l’administrateur lors de la configuration</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebSphere</p> </td>
   <td><p>9060 ; si la sécurité globale est activée, la valeur de port SSL par défaut est 9043.</p> <p>9080</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>Serveur BAM</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>méthode d’objet</p> </td>
   <td><p>8880</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>MySQL</p> </td>
   <td><p>3306</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>Oracle</p> </td>
   <td><p>1521</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>DB2</p> </td>
   <td><p>50 000</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SQL Server</p> </td>
   <td><p>1433</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>LDAP</p> </td>
   <td><p>port sur lequel le serveur LDAP fonctionne. Il s’agit généralement du port 389. Toutefois, si vous sélectionnez l’option SSL, le port par défaut est habituellement le port 636. Vérifiez auprès de votre administrateur LDAP le numéro de port à utiliser.</p> </td>
  </tr>
 </tbody>
</table>

### Configuration de JBoss pour utiliser un port HTTP qui n’est pas un port par défaut {#configuring-jboss-to-use-a-non-default-http-port}

Le serveur d’applications JBoss utilise 8080 en tant que port HTTP par défaut. JBoss possède également des ports 8180, 8280 et 8380 préconfigurés ; ils sont mis en commentaires dans le fichier jboss-service.xml. Si vous possédez sur votre ordinateur une application qui utilise déjà ce port, vous devez modifier celui qui est utilisé par AEM Forms sur JEE comme suit :

1. Ouvrez le fichier suivant pour le modifier :

   Installation sur un serveur : [racine JBoss]/standalone/configuration/standalone.xml

   Installations de cluster : [racine JBoss]/domain/configuration/domain.xml

1. Modifiez la valeur de lʼattribut **port** dans la balise **&lt;socket-binding>** vers un numéro de port personnalisé. Dans lʼexemple suivant, le port 8090 est utilisé :

   &lt;socket-binding name=&quot;http&quot; port=&quot;8090&quot;/>

1. Enregistrez et fermez le fichier.
1. Redémarrez le serveur d’applications JBoss.

## Considérations sur la sécurité d’AEM Forms sur JEE {#aem-forms-on-jee-security-considerations}

Cette section décrit certains problèmes de sécurité d’AEM Forms sur JEE que vous devez connaître.

### Informations d’identification de courrier électronique non chiffrées dans la base de données {#email-credentials-not-encrypted-in-database}

Les informations d’identification stockées par les applications ne sont pas chiffrées avant d’être enregistrées dans la base de données d’AEM Forms sur JEE. Lorsque vous configurez un point de fin de service pour utiliser le courrier électronique, les informations de mot de passe utilisées pour configurer ce point de fin ne sont pas chiffrées lorsqu’elles sont enregistrées dans la base de données.

### Contenu sensible pour Rights Management dans la base de données {#sensitive-content-for-rights-management-in-the-database}

AEM Forms sur JEE utilise sa base de données pour stocker des informations clés sur des documents sensibles et d’autres données cryptographiques utilisées pour les documents de stratégie. Le fait de sécuriser la base de données contre les intrusions contribue à la protection de ces informations sensibles.

### Mot de passe en texte clair {#password-in-clear-text-format-in-adobe-ds-xml}

Le serveur d’applications utilisé pour exécuter AEM Forms sur JEE nécessite sa propre configuration pour accéder à votre base de données via une source de données configurée sur le serveur d’applications. Veillez à ce que votre serveur d’applications n’expose pas le mot de passe de votre base de données en texte lisible dans le fichier de configuration de sa source de données.

Le fichier lc_[database].xml ne doit pas contenir de mot de passe en texte clair. Consultez le revendeur de votre serveur d’applications pour savoir comment chiffrer ces mots de passe pour votre serveur d’applications.

>[!NOTE]
>
>Le programme d’installation de la clé en main de Jboss d’AEM Forms sur JEE chiffre le mot de passe de la base de données.

Il est possible que le serveur d’applications IBM WebSphere et qu’Oracle WebLogic Server chiffrent les mots de passe des sources de données par défaut. Vérifiez ce point dans la documentation de votre serveur d’applications.

### Protection de la clé privée stockée dans Trust Store {#protecting-the-private-key-stored-in-trust-store}

Les clés privées ou les informations d’identification importées dans Trust Store sont stockées dans la base de données d’AEM Forms sur JEE. Prenez des mesures de sécurité appropriées pour sécuriser la base de données et limiter l’accès aux seuls administrateurs indiqués.
