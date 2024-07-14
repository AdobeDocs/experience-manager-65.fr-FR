---
title: Considérations générales sur la sécurité pour AEM Forms sur JEE
description: Découvrez comment préparer le renforcement de votre environnement AEM Forms sur JEE.
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
docset: aem65
role: Admin,User
exl-id: 3f150dd5-f486-4f16-9de9-035cde53b034
solution: Experience Manager, Experience Manager Forms
feature: Document Security,Adaptive Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 100%

---

# Considérations générales sur la sécurité pour AEM Forms sur JEE{#general-security-considerations-for-aem-forms-on-jee}

Cet article présente des informations préliminaires qui vous aideront à préparer le renforcement de votre environnement AEM Forms. Il comprend les informations préalables concernant la sécurité d’AEM Forms sur JEE, le système d’exploitation, le serveur d’applications et la base de données. Passez en revue ces informations avant de continuer à verrouiller votre environnement.

## Informations de sécurité spécifiques au fournisseur {#vendor-specific-security-information}

Cette section présente les informations relatives à la sécurité sur les systèmes d’exploitation, les serveurs d’applications et les bases de données intégrés à votre solution AEM Forms sur JEE.

Suivez les liens de cette section pour trouver des informations de sécurité spécifiques à un fournisseur pour votre système d’exploitation, votre base de données et votre serveur d’applications.

### Informations sur la sécurité du système d’exploitation {#operating-system-security-information}

Lorsque vous sécurisez votre système d’exploitation, veillez à implémenter soigneusement les mesures indiquées par le revendeur de votre système d’exploitation, parmi lesquelles :

* Définir et contrôler les utilisateurs et utilisatrices, les rôles et les privilèges
* Surveiller les journaux et les journaux d’audit
* Supprimer les services et applications inutiles
* Sauvegarder des fichiers

Pour plus de détails sur la sécurité des systèmes d’exploitation pris en charge par AEM Forms sur JEE, consultez les ressources du tableau suivant :

<table>
 <thead>
  <tr>
   <th><p>Système d’exploitation</p> </th>
   <th><p>Ressources en matière de sécurité</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM® AIX® 7.2</p> </td>
   <td><p><a href="https://www.ibm.com/support/knowledgecenter/ssw_aix_72/com.ibm.aix.security/security-kickoff.htm" target="_blank">Avantages de la sécurité IBM® AIX®</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® Windows Server® 2016 </p> </td>
   <td><p><a href="https://cloudblogs.microsoft.com/windowsserver/2017/08/22/now-available-windows-server-2016-security-guide/">Guide de sécurité Windows Server 2016</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Linux® AP ou ES</p> </td>
   <td><p><a href="https://access.redhat.com/documentation/fr-fr/red_hat_enterprise_linux/7/pdf/security_guide/red_hat_enterprise_linux-7-security_guide-fr-fr.pdf" target="_blank">Guide de sécurité de Red Hat® Enterprise Linux®</a></p> </td>
  </tr>
  <tr>
   <td><p>Sun Solaris™ 11</p> </td>
   <td><p><a href="https://docs.oracle.com/cd/E53394_01/html/E54807/index.html" target="_blank">Recommandations relatives à la sécurité et au renforcement</a></p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 Update 3</td>
   <td><a href="https://docs.oracle.com/fr/operating-systems/oracle-linux/7/security/" target="_blank">Guide de sécurité pour la version 7</a><br /> </td>
  </tr>
  <tr>
   <td>CentOS 7<sup> </sup></td>
   <td><a href="https://wiki.centos.org/HowTos/OS_Protection" target="_blank">Documentation sur la protection</a></td>
  </tr>
 </tbody>
</table>

### Informations sur la sécurité des serveurs d’applications {#application-server-security-information}

Lorsque vous sécurisez votre serveur d’applications, veiller à implémenter soigneusement les mesures indiquées par le revendeur de votre serveur, parmi lesquelles :

* Utiliser un nom d’utilisateur administrateur ou d’utilisatrice administratrice difficilement identifiable
* Désactiver les services inutiles
* Sécuriser le gestionnaire de console
* Activer les cookies sécurisés
* Fermer les ports inutiles
* Limiter les clients par adresses ou domaines IP
* Utiliser le gestionnaire de sécurité Java™ pour limiter les privilèges par programmation

Pour obtenir des informations sur la sécurité des serveurs d’application pris en charge par AEM Forms sur JEE, consultez les ressources de ce tableau.

<table>
 <thead>
  <tr>
   <th><p>Serveur d’applications</p> </th>
   <th><p>Ressources en matière de sécurité</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Oracle WebLogic®</p> </td>
   <td><p>Recherchez « Understanding WebLogic Security » sur <a href="https://docs.oracle.com/">https://docs.oracle.com/</a> (en anglais).</p> </td>
  </tr>
  <tr>
   <td><p>IBM® WebSphere®</p> </td>
   <td><p><a href="https://www.ibm.com/developerworks/websphere/zones/was/security/" target="_blank">Sécurisation des applications dans leur environnement</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® JBoss®</p> </td>
   <td><p><a href="https://docs.jboss.org/author/display/AS7/Security%20subsystem%20configuration.html">Configuration du sous-système de sécurité</a></p> </td>
  </tr>
 </tbody>
</table>

### Informations sur la sécurité des bases de données {#database-security-information}

Lorsque vous sécurisez votre base de données, veillez à implémenter soigneusement les mesures indiquées par le revendeur de votre base de données, parmi lesquelles :

* Restreindre des opérations avec des listes de contrôle d’accès (ACL)
* Utiliser des ports non standard
* Masquer la base de données derrière un pare-feu
* Chiffrer des données sensibles avant leur écriture dans la base de données (voir la documentation du fournisseur de la base de données)

Pour obtenir des informations sur la sécurité des bases de données prises en charge par AEM Forms sur JEE, consultez les ressources de ce tableau.

<table>
 <thead>
  <tr>
   <th><p>Base de données</p> </th>
   <th><p>Ressources en matière de sécurité</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM® DB2® 11.1</p> </td>
   <td><p><a href="https://www-01.ibm.com/software/data/db2/library/">Bibliothèque de la famille de produits DB2®</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® SQL Server 2016</p> </td>
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

Ce tableau décrit les ports par défaut devant être ouverts pendant le processus de configuration d’AEM Forms sur JEE. Si vous vous connectez via https, ajustez les informations de port et les adresses IP en conséquence. Pour plus d’informations sur la configuration des ports, consultez le document *Installation et déploiement d’AEM Forms sur JEE* pour votre serveur d’application.

<table>
 <thead>
  <tr>
   <th><p>Produit ou service</p> </th>
   <th><p>Numéro de port</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>JBoss®</p> </td>
   <td><p>8080</p> </td>
  </tr>
  <tr>
   <td><p>WebLo gic</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>Serveur géré par WebLogic</p> </td>
   <td><p>Défini par l’administration lors de la configuration</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebSphere®</p> </td>
   <td><p>9060, si la fonction Global Security est activée, la valeur de port SSL par défaut est 9043.</p> <p>9080</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>Serveur BAM</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SOAP</p> </td>
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
   <td>&gt;<p>DB2®</p> </td>
   <td><p>50 000</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SQL Server</p> </td>
   <td><p>1433</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>LDAP</p> </td>
   <td><p>Port sur lequel le serveur LDAP est en cours d’exécution. Le port par défaut est généralement 389. Cependant, si vous sélectionnez l’option SSL, le port par défaut est généralement 636. Vérifiez auprès de votre administrateur LDAP le numéro de port à utiliser.</p> </td>
  </tr>
 </tbody>
</table>

### Configurer JBoss® pour utiliser un port HTTP qui n’est pas un port par défaut {#configuring-jboss-to-use-a-non-default-http-port}

Le serveur d’applications JBoss® utilise le port HTTP par défaut 8080. JBoss® dispose également des ports préconfigurés 8180, 8280 et 8380, qui sont commentés dans le fichier jboss-service.xml. Si votre ordinateur comporte déjà une application utilisant ce port, modifiez le port utilisé par AEM Forms sur JEE en procédant comme suit :

1. Ouvrez le fichier suivant pour le modifier :

   Installation sur un serveur unique : [racine JBoss®]/standalone/configuration/standalone.xml

   Installations de cluster : [racine JBoss]/domain/configuration/domain.xml

1. Modifiez la valeur de lʼattribut **port** dans la balise **&lt;socket-binding>** vers un numéro de port personnalisé. Dans lʼexemple suivant, le port 8090 est utilisé :

   &lt;socket-binding name=&quot;http&quot; port=&quot;8090&quot;/>

1. Enregistrez et fermez le fichier.
1. Redémarrez le serveur d’applications JBoss®.

>[!NOTE]
>
> Il est recommandé d’utiliser la commande « Ctrl + C » pour redémarrer le SDK. Le redémarrage du SDK AEM à l’aide de méthodes alternatives, par exemple l’arrêt des processus Java, peut entraîner des incohérences dans l’environnement de développement AEM.

## Considérations relatives à la sécurité d’AEM Forms sur JEE {#aem-forms-on-jee-security-considerations}

Cette section décrit certains problèmes de sécurité spécifiques à AEM Forms sur JEE que vous devez connaître.

### Informations d’identification de messagerie non chiffrées dans la base de données {#email-credentials-not-encrypted-in-database}

Les informations d’identification de messagerie stockées par les applications ne sont pas chiffrées avant d’être stockées dans la base de données d’AEM Forms sur JEE. Lorsque vous configurez un point d’entrée du service pour utiliser l’e-mail, les mots de passe utilisés dans le cadre de cette configuration de point d’entrée ne sont pas chiffrés lorsqu’ils sont stockés dans la base de données.

### Contenu sensible pour Rights Management dans la base de données {#sensitive-content-for-rights-management-in-the-database}

AEM Forms sur JEE utilise sa base de données pour stocker des informations clés sur des documents sensibles et d’autres données cryptographiques utilisées pour les documents de politique. Le fait de sécuriser la base de données contre les intrusions contribue à la protection de ces informations sensibles.

### Mot de passe en texte clair {#password-in-clear-text-format-in-adobe-ds-xml}

Le serveur d’applications utilisé pour exécuter AEM Forms sur JEE nécessite sa propre configuration pour accéder à votre base de données via une source de données configurée sur le serveur d’applications. Veillez à ce que votre serveur d’applications n’expose pas le mot de passe de votre base de données en texte lisible dans le fichier de configuration de sa source de données.

Le fichier lc_[database].xml ne doit pas contenir de mot de passe en texte clair. Consultez le revendeur de votre serveur d’applications pour savoir comment chiffrer ces mots de passe pour votre serveur d’applications.

>[!NOTE]
>
>Le programme d’installation clé en main de JBoss® pour AEM Forms sur JEE chiffre le mot de passe de la base de données.

Le serveur d’applications IBM® WebSphere® et le serveur Oracle WebLogic peuvent chiffrer les mots de passe de la source de données par défaut. Cependant, vous devez vérifier dans la documentation de votre serveur d’applications que c’est bien le cas.

### Protéger la clé privée stockée dans Trust Store {#protecting-the-private-key-stored-in-trust-store}

Les clés privées ou les informations d’identification importées dans Trust Store sont stockées dans la base de données d’AEM Forms sur JEE. Pour sécuriser la base de données et restreindre l’accès aux administrateurs et administratrices désignés uniquement, prenez les précautions adéquates.
