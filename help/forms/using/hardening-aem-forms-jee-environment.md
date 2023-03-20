---
title: Sécurisation de votre environnement d’AEM Forms sur JEE
seo-title: Hardening Your AEM Forms on JEE Environment
description: Découvrez divers paramètres de renforcement de la sécurité pour améliorer la sécurité d’AEM Forms sur JEE dans le cadre d’une exécution pour un intranet d’entreprise.
seo-description: Learn a variety of security-hardening settings to enhance the security of AEM Forms on JEE running in a corporate intranet.
uuid: f6c63690-6376-4fe1-9df2-a14fbfd62aff
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 6b380e92-f90d-4875-b7a2-f3958daf2364
role: Admin
exl-id: 6fb260f9-d0f8-431e-8d4e-535b451e4124
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: tm+mt
source-wordcount: '7665'
ht-degree: 44%

---

# Sécurisation de votre environnement d’AEM Forms sur JEE {#hardening-your-aem-forms-on-jee-environment}

Découvrez divers paramètres de renforcement de la sécurité pour améliorer la sécurité d’AEM Forms sur JEE dans le cadre d’une exécution pour un intranet d’entreprise.

Cet article décrit les recommandations et les bonnes pratiques relatives à la sécurisation des serveurs exécutant AEM Forms on JEE. Il ne vise pas à expliquer de manière exhaustive comment renforcer des hôtes pour votre système d’exploitation et vos serveurs d’applications. Au lieu de cela, cet article décrit plusieurs paramètres de renforcement de la sécurité, que vous pouvez implémenter pour améliorer la sécurité d’AEM Forms lorsque celui-ci est exécuté pour un intranet d’entreprise. Toutefois, pour garantir la sécurité des serveurs d’applications AEM Forms on JEE, vous devez également mettre en oeuvre des procédures de surveillance, de détection et de réponse de sécurité.

L’article décrit les techniques de renforcement qui doivent être appliquées lors des étapes suivantes du cycle de vie de l’installation et de la configuration :

* **Préinstallation :** Utilisez ces techniques avant d’installer AEM Forms on JEE.
* **Installation :** utilisez ces techniques pendant le processus d’installation d’AEM Forms sur JEE.
* **Post-installation :** Utilisez ces techniques après l’installation et régulièrement par la suite.

AEM Forms on JEE est hautement personnalisable et peut fonctionner dans de nombreux environnements différents. Certaines des recommandations peuvent ne pas correspondre aux besoins de votre entreprise.

## Préinstallation {#preinstallation}

Avant d’installer AEM Forms sur JEE, vous pouvez appliquer des solutions de sécurité à la couche réseau et au système d’exploitation. Cette section décrit certains problèmes et fournit des recommandations pour réduire les vulnérabilités de la sécurité dans ces domaines.

**Installation et configuration sous UNIX et Linux**

Vous ne devez pas installer ni configurer AEM Forms on JEE à l’aide d’un shell racine. Par défaut, les fichiers sont installés sous le répertoire /opt et l’utilisateur qui effectue l’installation a besoin de toutes les autorisations de fichier sous /opt. Vous pouvez également effectuer une installation dans le répertoire /user d’un utilisateur spécifique, où il dispose déjà de toutes les autorisations de fichier.

**Installation et configuration sous Windows**

Sous Windows, vous devez effectuer l’installation en tant qu’administrateur si vous installez AEM Forms on JEE sur JBoss à l’aide de la procédure clé en main ou si vous installez PDF Generator. En outre, lorsque vous installez PDF Generator sous Windows avec prise en charge des applications natives, vous devez exécuter l’installation en tant qu’utilisateur Windows ayant installé Microsoft Office. Pour plus de détails sur l’installation des privilèges, reportez-vous au document Installer et déployer AEM Forms sur JEE de votre serveur d’applications.

### Sécurité des couches réseau {#network-layer-security}

Les vulnérabilités de la sécurité réseau sont parmi les premières menaces qui pèsent sur un serveur d’applications utilisant Internet ou un intranet. Cette section décrit le processus de renforcement des hôtes sur le réseau contre ces vulnérabilités. Il traite de la segmentation du réseau, du renforcement de la pile TCP/IP (Transmission Control Protocol/Internet Protocol) et de l’utilisation de pare-feu pour la protection des hôtes.

Le tableau suivant décrit les processus courants qui réduisent les vulnérabilités de la sécurité réseau.

<table> 
 <thead> 
  <tr> 
   <th><p>Problème</p> </th> 
   <th><p>Description</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Zones démilitarisées (DMZ)</p> </td> 
   <td><p>Déployez des serveurs de formulaires dans une zone démilitarisée (DMZ). La segmentation doit exister à au moins deux niveaux avec le serveur d’applications utilisé pour exécuter AEM Forms on JEE placé derrière le pare-feu interne. Séparez le réseau externe de la DMZ qui contient les serveurs web, qui doivent à leur tour être séparés du réseau interne. Utilisez des pare-feu pour implémenter les couches de séparation. Classez et contrôlez le trafic qui traverse chaque couche réseau pour vous assurer que seul le minimum absolu des données requises est autorisé.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Adresses IP privées</p> </td> 
   <td><p>Utilisez la technique NAT (Network Address Translation) avec des adresses IP privées RFC 1918, pour les serveurs de l’application AEM Forms. Attribuez des adresses IP privées (10.0.0.0/8, 172.16.0.0/12 et 192.168.0.0/16) pour rendre plus difficile, pour une personne malveillante, le routage du trafic depuis et vers un hôte interne NAT via Internet.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Pare-feux</p> </td> 
   <td><p>Utilisez les critères suivants pour sélectionner une solution de pare-feu :</p> 
    <ul> 
     <li><p>Mise en oeuvre de pare-feu qui prennent en charge les serveurs proxy et/ou <em>inspection avec état</em> plutôt que de simples solutions de filtrage de paquets.</p> </li> 
     <li><p>Utilisez un pare-feu qui prend en charge un paradigme de sécurité de type <em>Refuser tous les services hormis ceux autorisés explicitement</em>.</p> </li> 
     <li><p>Mettez en oeuvre une solution de pare-feu à double hébergement ou à hébergement multiple. Cette architecture offre un niveau de sécurité optimal et permet d’empêcher les utilisateurs non autorisés de contourner le pare-feu.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>Ports de base de données</p> </td> 
   <td><p>N’utilisez pas de ports d’écoute par défaut pour les bases de données (MySQL - 3306, Oracle - 1521, MS SQL - 1433). Pour plus d’informations sur la modification des ports de base de données, consultez la documentation de votre base de données.</p> <p>L’utilisation d’un port de base de données différent affecte la configuration globale d’AEM Forms on JEE. Si vous modifiez les ports par défaut, vous devez apporter les modifications correspondantes dans d’autres zones de configuration, telles que les sources de données d’AEM Forms on JEE.</p> <p>Pour obtenir des informations sur la configuration des sources de données dans AEM Forms sur JEE, voir Installer et déployer AEM Forms sur JEE ou Mettre à niveau vers AEM Forms sur JEE pour votre serveur d’applications, dans le <a href="/help/forms/using/introduction-aem-forms.md" target="_blank">Guide de l’utilisateur AEM Forms</a>.</p> </td> 
  </tr> 
 </tbody> 
</table>

### Sécurité du système d’exploitation {#operating-system-security}

Le tableau suivant décrit certaines approches possibles pour réduire les vulnérabilités de sécurité du système d’exploitation.

<table> 
 <thead> 
  <tr> 
   <th><p>Problème</p></th> 
   <th><p>Description</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Correctifs de sécurité</p></td> 
   <td><p>Le risque augmente qu’un utilisateur non autorisé puisse accéder au serveur d’applications si les correctifs de sécurité et les mises à niveau du fournisseur ne sont pas appliqués en temps voulu. Testez les correctifs de sécurité avant de les appliquer aux serveurs de production.</p><p>Créez également des stratégies et des procédures pour vérifier et installer régulièrement les correctifs.</p></td> 
  </tr> 
  <tr> 
   <td><p>Logiciels de protection anti-virus</p></td> 
   <td><p>Les analyseurs de virus peuvent identifier les fichiers infectés en recherchant une signature ou en observant un comportement inhabituel. Les analyseurs conservent leurs signatures de virus dans un fichier, qui est généralement stocké sur le disque dur local. Comme de nouveaux virus sont souvent découverts, vous devez fréquemment mettre à jour ce fichier pour que le scanner de virus identifie tous les virus actuels.</p></td> 
  </tr> 
  <tr> 
   <td><p>NTP (Network Time Protocol)</p></td> 
   <td><p>Pour les analyses médico-légales, vérifiez que le délai sur les serveurs de formulaires est correct. Utilisez NTP pour synchroniser le temps sur tous les systèmes connectés directement à Internet.</p></td> 
  </tr> 
 </tbody> 
</table>

Pour plus d’informations de sécurité pour votre système d’exploitation, consultez [« Informations sur la sécurité des systèmes d’exploitation »](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr).

## Installation {#installation}

Cette section décrit les techniques que vous pouvez utiliser pendant le processus d&#39;installation d&#39;AEM Forms pour réduire les vulnérabilités de sécurité. Dans certains cas, ces techniques utilisent des options qui font partie du processus d’installation. Le tableau suivant décrit ces techniques.

<table> 
 <thead> 
  <tr> 
   <th><p>Problème</p> </th> 
   <th><p>Description</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Autorisations</p> </td> 
   <td><p>Utilisez le minimum de droits requis pour installer le logiciel. Connectez-vous à votre ordinateur à l’aide d’un compte qui ne figure pas dans le groupe Administrateurs . Sous Windows, vous pouvez utiliser la commande Exécuter pour exécuter le programme d’installation d’AEM Forms sur JEE en tant qu’utilisateur non administrateur. Sous UNIX et Linux, utilisez une commande comme <code>sudo</code> pour installer le logiciel.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Source logicielle</p> </td> 
   <td><p>Ne téléchargez ni n’exécutez AEM Forms on JEE à partir de sources non approuvées.</p> <p>Les programmes malveillants peuvent contenir du code qui enfreint la sécurité de plusieurs manières, y compris le vol, la modification et la suppression de données, et le déni de service. Installez AEM Forms on JEE à partir du DVD de l’Adobe ou uniquement à partir d’une source de confiance.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Partitions de disque</p> </td> 
   <td><p>Placez AEM Forms on JEE sur une partition de disque dédiée. La segmentation du disque est un processus qui conserve des données spécifiques sur votre serveur sur des disques physiques distincts pour une sécurité accrue. L’organisation des données de cette manière réduit le risque d’attaques par traversée de répertoires. Prévoyez de créer une partition distincte de la partition système, dans laquelle vous pouvez installer le répertoire de contenu AEM Forms sur JEE. (Sous Windows, la partition système contient le répertoire system32, ou partition de démarrage.)</p> </td> 
  </tr> 
  <tr> 
   <td><p>Composants</p> </td> 
   <td><p>Evaluez les services existants et désactivez ou désinstallez les services qui ne sont pas requis. N’installez pas de composants et de services inutiles.</p> <p>L’installation par défaut d’un serveur d’applications peut inclure des services qui ne sont pas nécessaires à votre utilisation. Vous devez désactiver tous les services inutiles avant le déploiement afin de minimiser les points d’entrée pour une attaque. Par exemple, sur JBoss, vous pouvez mettre en commentaire les services inutiles dans le fichier de descripteur META-INF/jboss-service.xml.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Fichier de stratégie inter-domaines</p> </td> 
   <td><p>La présence d’un fichier <code>crossdomain.xml</code> sur le serveur peut immédiatement affaiblir ce serveur. Il est recommandé de rendre la liste des domaines aussi restrictive que possible. Ne placez pas en production le fichier <code>crossdomain.xml</code> utilisé pendant la phase de développement lors de l’utilisation des guides <em>(obsolète)</em>. Dans le cas d’un guide qui utilise les services Web, si le service figure sur le même serveur ayant servi le guide, aucun fichier <code>crossdomain.xml</code> n’est nécessaire. En revanche, si le service figure sur un autre serveur ou si des grappes sont impliquées, la présence d’un fichier <code>crossdomain.xml</code> est nécessaire. Voir <a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a>, pour plus d’informations sur le fichier crossdomain.xml.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Paramètres de sécurité du système d’exploitation</p> </td> 
   <td><p>Si vous devez utiliser un chiffrement XML 192 bits ou 256 bits sur les plateformes Solaris, assurez-vous d’installer <code>pkcs11_softtoken_extra.so</code> au lieu de <code>pkcs11_softtoken.so</code>.</p> </td> 
  </tr> 
 </tbody> 
</table>

## Etapes de post-installation {#post-installation-steps}

Une fois AEM Forms on JEE installé avec succès, il est important de maintenir régulièrement l’environnement du point de vue de la sécurité.

La section suivante décrit en détail les différentes tâches recommandées pour sécuriser le serveur de formulaires déployé.

### Sécurité AEM Forms {#aem-forms-security}

Les paramètres recommandés suivants s’appliquent au serveur AEM Forms sur JEE hors de l’application Web administrative. Pour réduire les risques de sécurité sur le serveur, appliquez ces paramètres immédiatement après l’installation d’AEM Forms on JEE.

**Correctifs de sécurité**

Le risque augmente qu’un utilisateur non autorisé puisse accéder au serveur d’applications si les correctifs de sécurité et les mises à niveau du fournisseur ne sont pas appliqués en temps voulu. Testez les correctifs de sécurité avant de les appliquer aux serveurs de production afin de garantir la compatibilité et la disponibilité des applications. Créez également des stratégies et des procédures pour vérifier et installer régulièrement les correctifs. Les mises à jour d’AEM Forms on JEE se trouvent sur le site de téléchargement des produits Enterprise.

**Comptes de service (JBoss clé en main sous Windows uniquement)**

AEM Forms on JEE installe un service par défaut à l’aide du compte système local. Le compte utilisateur système local intégré présente un haut niveau d’accessibilité ; il fait partie du groupe Administrateurs . Si une identité de processus de travail s’exécute en tant que compte utilisateur système local, ce processus de travail dispose d’un accès complet à l’ensemble du système.

Pour exécuter le serveur d’applications sur lequel AEM Forms on JEE est déployé à l’aide d’un compte non administratif spécifique, suivez les instructions suivantes :

1. Dans la console de gestion Microsoft (MMC), créez un utilisateur local pour que le service de serveur de formulaires se connecte en tant que :

   * Sélectionner **L’utilisateur ne peut pas changer de mot de passe**.
   * Vérifiez que le groupe **Utilisateurs** figure dans l’onglet **Membre de**.

   >[!NOTE]
   >
   >Vous ne pouvez pas modifier ce paramètre pour PDF Generator.

1. Sélectionner **Début** > **Paramètres** > **Outils d’administration** > **Services**.
1. Double-cliquez sur JBoss pour AEM Forms on JEE et arrêtez le service.
1. Sur le **Connexion** onglet, sélectionnez **Ce compte**, recherchez le compte utilisateur que vous avez créé et saisissez le mot de passe du compte.
1. Dans le MMC, ouvrez **Paramètres de sécurité locale** et sélectionnez **Stratégies locales** > **Attribution des droits utilisateur**.
1. Attribuez les droits suivants au compte utilisateur sous lequel le serveur Forms est exécuté :

   * Refuser de se connecter via les services Terminal
   * Refuser la connexion locale
   * Ouvrir une session en tant que service (ce droit doit être déjà défini)

1. Donnez au nouveau compte utilisateur les autorisations de modification sur les répertoires suivants :
   * **Répertoire de stockage global de documents** : l’emplacement du répertoire de stockage global de documents est configuré manuellement pendant le processus d’installation d’AEM Forms. Si le paramètre d’emplacement du stockage global de documents n’est pas défini pendant l’installation, l’emplacement par défaut utilisé est un sous-répertoire de l’emplacement d’installation du serveur d’applications : `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **Répertoire CRX-Repository** : l’emplacement par défaut est `[AEM-Forms-installation-location]\crx-repository`
   * **Répertoires temporaires AEM Forms** :
      * (Windows) Chemin TMP ou TEMP tel que défini dans les variables d’environnement
      * (AIX, Linux ou Solaris) Répertoire racine de l’utilisateur connecté Sur les systèmes UNIX, un utilisateur non root peut utiliser le répertoire suivant comme répertoire temporaire :
      * (Linux) /var/tmp ou /usr/tmp
      * (AIX) /tmp ou /usr/tmp
      * (Solaris) /var/tmp ou /usr/tmp
1. Donnez au nouveau compte utilisateur les autorisations d’écriture pour les répertoires suivants :
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   >L’emplacement de l’installation par défaut de JBoss Application Server :
   >
   >* Windows : C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   >* Linux : /opt/jboss/


1. Démarrez le serveur d’applications.

**Désactivation de la servlet d’amorçage de Configuration Manager**

Configuration Manager a utilisé une servlet déployée sur votre serveur d’applications pour amorcer la base de données AEM Forms sur JEE. Configuration Manager accédant à ce servlet avant la fin de la configuration, son accès n’a pas été sécurisé pour les utilisateurs autorisés et il doit être désactivé une fois que vous avez correctement utilisé Configuration Manager pour configurer AEM Forms on JEE.

1. Décompressez le fichier adobe-livecycle-[appserver].ear.
1. Ouvrez le fichier META-INF/application.xml .
1. Recherchez la section adobe-bootstrapper.war :

   ```java
   <!-- bootstrapper start --> 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   <!-- bootstrapper end-->
   ```

1. Arrêtez le serveur AEM Forms.
1. Mettez en commentaire adobe-bootstrapper.war et le répertoire adobe-lcm-bootstrapper-redirectory. les modules de guerre comme suit :

   ```java
   <!-- bootstrapper start --> 
   <!-- 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   --> 
   <!-- bootstrapper end-->
   ```

1. Enregistrez et fermez le fichier META-INF/application.xml .
1. Compressez le fichier EAR et redéployez-le sur le serveur d’applications.
1. Démarrez le serveur AEM Forms.
1. Entrez l’URL suivante dans un navigateur pour tester la modification et garantir que l’adresse ne fonctionne plus.

   https://&lt;localhost>:&lt;port>/adobe-bootstrapper/bootstrap

**Verrouillage de l’accès distant au Trust Store**

Configuration Manager vous permet de charger des informations d’identification des extensions Acrobat Reader DC dans le trust store d’AEM Forms on JEE. Cela signifie que l’accès à Trust Store Credential Service sur les protocoles distants (SOAP et EJB) a été activé par défaut. Cet accès n’est plus nécessaire après avoir téléchargé les informations d’identification des droits en utilisant Configuration Manager, ou si vous décidez d’utiliser la console d’administration ultérieurement pour gérer les informations d’identification.

Vous pouvez désactiver l’accès distant à tous les services Trust Store en suivant les étapes de la section . [Désactivation de l’accès distant non essentiel aux services](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr).

**Désactiver tous les accès anonymes non indispensables**

Certains services de serveur de formulaires comportent des opérations qui peuvent être appelées par un appelant anonyme. Si l’accès anonyme à ces services n’est pas requis, désactivez-le en suivant les étapes de la section [Désactivation des accès anonymes non indispensables à des services](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr).

#### Modification du mot de passe administrateur par défaut {#change-the-default-administrator-password}

Lors de l’installation d’AEM Forms on JEE, un seul compte utilisateur par défaut est configuré pour l’utilisateur Super administrateur/Administrateur avec un mot de passe par défaut : *password*. Modifiez immédiatement ce mot de passe à l’aide de Configuration Manager.

1. Saisissez l’URL suivante dans un navigateur Web :

   ```java
   https://[host name]:[port]/adminui
   ```

   Le numéro de port par défaut est l’un des suivants :

   **JBoss :** 8080

   **WebLogic Server :** 7001

   **WebSphere :** 9080.

1. Dans le champ **Nom d’utilisateur**, saisissez `administrator` et dans le champ **Mot de passe**, saisissez `password`.
1. Cliquez sur **Paramètres** > **User Management** > **Utilisateurs et groupes**.
1. Saisissez `administrator` dans le champ **Rechercher**, puis cliquez sur **Rechercher**.
1. Cliquez sur **Super administrateur** dans la liste des utilisateurs.
1. Cliquez sur **Modifier le mot de passe** sur la page Modifier l’utilisateur .
1. Indiquez le nouveau mot de passe et cliquez sur **Enregistrer**.

En outre, il est recommandé de modifier le mot de passe par défaut de l’administrateur CRX en procédant comme suit :

1. Connectez-vous à `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` à l’aide du nom d’utilisateur/mot de passe par défaut.
1. Saisissez Administrator dans le champ de recherche, puis cliquez sur **Aller**.
1. Sélectionnez **Administrateur** dans les résultats de la recherche, puis cliquez sur l’icône **Modifier** située dans le coin inférieur droit de l’interface utilisateur.
1. Indiquez le nouveau mot de passe dans le champ **Nouveau mot de passe** et l’ancien mot de passe dans le champ **Votre mot de passe**.
1. Cliquez sur l’icône Enregistrer située dans le coin inférieur droit de l’interface utilisateur.

#### Désactiver la génération WSDL {#disable-wsdl-generation}

La génération WSDL (Web Service Definition Language) ne doit être activée que pour les environnements de développement dans lesquels la génération WSDL est utilisée par les développeurs pour créer leurs applications clientes. Vous pouvez choisir de désactiver la génération WSDL dans un environnement de production afin d’éviter d’exposer les détails internes d’un service.

1. Saisissez l’URL suivante dans un navigateur Web :

   ```java
   https://[host name]:[port]/adminui
   ```

1. Cliquez sur **Paramètres > Paramètres de Core System > Configurations**.
1. Désactivez la case à cocher **Activer WSDL**, puis cliquez sur **OK**.

### Sécurité du serveur d’applications {#application-server-security}

Le tableau suivant décrit certaines techniques de sécurisation de votre serveur d’applications une fois l’application AEM Forms on JEE installée.

<table> 
 <thead> 
  <tr> 
   <th><p>Problème</p> </th> 
   <th><p>Description</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Console d’administration du serveur d’applications</p> </td> 
   <td><p>Après avoir installé, configuré et déployé AEM Forms on JEE sur votre serveur d’applications, désactivez l’accès aux consoles d’administration du serveur d’applications. Pour plus d’informations, voir la documentation de votre serveur d’applications .</p> </td> 
  </tr> 
  <tr> 
   <td><p>Paramètres des cookies du serveur d’applications</p> </td> 
   <td><p>Les cookies d’application sont contrôlés par le serveur d’applications. Lors du déploiement de l’application, l’administrateur du serveur d’applications peut spécifier les préférences des cookies à l’échelle du serveur ou selon l’application. Par défaut, les paramètres du serveur sont prioritaires.</p> <p>Tous les cookies de session générés par votre serveur d’applications devraient inclure l’attribut <code>HttpOnly</code>. Par exemple, si vous utilisez JBoss Application Server, vous pouvez redéfinir l’élément SessionCookie sur <code>httpOnly="true"</code> dans le fichier <code>WEB-INF/web.xml</code>.</p> <p>Vous pouvez limiter l’envoi des cookies en utilisant le protocole HTTPS seulement. Par conséquent, ils ne sont pas envoyés non chiffrés sur HTTP. Les administrateurs de serveur d’applications doivent activer les cookies sécurisés pour le serveur de manière globale. Par exemple, si vous utilisez JBoss Application Server, vous pouvez redéfinir l’élément connecteur sur <code>secure=true</code> dans le fichier <code>server.xml</code>.</p> <p>Pour plus d’informations sur les paramètres des cookies, consultez la documentation de votre serveur d’applications.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Navigation dans les répertoires</p> </td> 
   <td><p>Lorsqu’une personne demande une page qui n’existe pas ou le nom d’un directeur (la chaîne de demande se termine par une barre oblique (/)), le serveur d’applications ne doit pas renvoyer le contenu de ce répertoire. Pour éviter cela, vous pouvez désactiver la navigation dans les répertoires sur votre serveur d’applications. Vous devez effectuer cette opération pour l’application Administration Console et pour les autres applications s’exécutant sur votre serveur.</p> <p>Pour JBoss, définissez la valeur du paramètre d’initialisation des listes de la propriété <code>DefaultServlet</code> sur <code>false</code> dans le fichier web.xml, comme illustré dans l’exemple ci-dessous :</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;default&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;listes&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>Pour WebSphere, définissez la propriété <code>directoryBrowsingEnabled</code> du fichier ibm-web-ext.xmi sur <code>false</code>.</p> <p>Pour WebLogic, définissez les propriétés index-directories du fichier weblogic.xml sur <code>false</code>, comme illustré dans l’exemple suivant :</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### Sécurité des bases de données {#database-security}

Lorsque vous sécurisez votre base de données, vous devez implémenter les mesures décrites par le fournisseur de votre base de données. Attribuez à l’utilisateur de la base de données le nombre minimum d’autorisations requises sur cette base de données pour permettre l’utilisation avec AEM Forms sur JEE. Par exemple, n’utilisez pas de compte avec des privilèges d’administrateur de base de données.

Sur Oracle, le compte de base de données que vous utilisez nécessite uniquement les privilèges CONNECT, RESOURCE et CREATE VIEW. Pour connaître les mêmes exigences sur d’autres bases de données, voir [Préparation à l’installation d’AEM Forms on JEE (serveur unique)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64_fr).

#### Configuration de la sécurité intégrée pour SQL Server sous Windows pour JBoss {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. Modifiez [JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml} pour ajouter `integratedSecurity=true` à l’URL de connexion, comme indiqué dans l’exemple suivant :

   ```java
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. Ajoutez le fichier sqljdbc_auth.dll au chemin d’accès du système Windows sur l’ordinateur exécutant le serveur d’applications. Le fichier sqljdbc_auth.dll se trouve avec les fichiers d’installation du pilote Microsoft SQL JDBC 6.2.1.0.
1. Modifiez la propriété du service Windows JBoss (JBoss pour AEM Forms on JEE) pour Ouvrir une session en tant que depuis le système local vers un compte de connexion qui dispose d’une base de données AEM Forms et d’un ensemble minimum de privilèges. Si vous exécutez JBoss à partir de la ligne de commande et non en tant que service Windows, il n’est pas nécessaire d’effectuer cette étape.
1. Faites passer la sécurité de SQL Server du mode **Mixte** au mode **Authentification Windows**.

#### Configuration de la sécurité intégrée dans SQL Server sur Windows pour WebLogic {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. Démarrez la console d’administration WebLogic Server en saisissant l’URL suivante dans la barre d’adresse d’un navigateur web :

   ```java
   https://[host name]:7001/console
   ```

1. Sous Change Center, cliquez sur **Lock &amp; Edit**.
1. Sous Domain Structure, cliquez sur *[base_domain]* > **Services** > **JDBC** > **Data Sources** et, dans le volet de droite, cliquez sur **IDP_DS**.
1. Dans l’écran suivant, dans l’onglet **Configuration**, cliquez sur l’onglet **Connection Pool** et, dans la zone **Properties**, saisissez `integratedSecurity=true`.
1. Sous Domain Structure, cliquez sur **[base_domain]** > **Services** > **JDBC** > **Data Sources** et, dans le volet de droite, cliquez sur **RM_DS**.
1. Dans l’écran suivant, dans l’onglet **Configuration**, cliquez sur l’onglet **Connection Pool** et, dans la zone **Properties**, saisissez `integratedSecurity=true`.
1. Ajoutez le fichier sqljdbc_auth.dll au chemin d’accès du système Windows sur l’ordinateur exécutant le serveur d’applications. Le fichier sqljdbc_auth.dll se trouve avec les fichiers d’installation du pilote Microsoft SQL JDBC 6.2.1.0.
1. Faites passer la sécurité de SQL Server du mode **Mixte** au mode **Authentification Windows**.

#### Configuration de la sécurité intégrée pour SQL Server sous Windows pour WebSphere {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

Sur WebSphere, vous pouvez configurer la sécurité intégrée uniquement lorsque vous utilisez un pilote JDBC SQL Server externe et non le pilote JDBC SQL Server incorporé avec WebSphere.

1. Connectez-vous à la console d’administration WebSphere.
1. Dans l’arborescence de navigation, cliquez sur **Resources** > **JDBC** > **Data Sources**, puis, dans le volet de droite, cliquez sur **IDP_DS**.
1. Dans le volet de droite, sous Additional Properties, cliquez sur **Custom Properties**, puis sur **New**.
1. Dans la case **Nom**, saisissez `integratedSecurity` et, dans la case **Valeur**, saisissez `true`.
1. Dans l’arborescence de navigation, cliquez sur **Resources** > **JDBC** > **Data Sources**, puis, dans le volet de droite, cliquez sur **RM_DS**.
1. Dans le volet de droite, sous Additional Properties, cliquez sur **Custom Properties**, puis sur **New**.
1. Dans la case **Nom**, saisissez `integratedSecurity` et, dans la case **Valeur**, saisissez `true`.
1. Sur l’ordinateur sur lequel WebSphere est installé, ajoutez le fichier sqljdbc_auth.dll au chemin du système Windows (C:\Windows). Le fichier sqljdbc_auth.dll est situé au même emplacement que le programme d’installation du pilote Microsoft SQL JDBC 1.2 (le chemin par défaut est *[InstallDir]*/sqljdbc_1.2/enu/auth/x86).
1. Sélectionner **Début** > **Panneau de Contrôle** > **Services**, cliquez avec le bouton droit de la souris sur le service Windows pour WebSphere (IBM WebSphere Application Server). &lt;version> - &lt;node>) et sélectionnez **Propriétés**.
1. Dans la boîte de dialogue Propriétés, cliquez sur le bouton **Connexion** .
1. Sélectionner **Ce compte** et fournissez les informations requises pour définir le compte de connexion que vous souhaitez utiliser.
1. Définir la sécurité sur SQL Server à partir de **Mixte** en mode **Authentification Windows uniquement**.

### Protection de l&#39;accès aux contenus sensibles dans la base {#protecting-access-to-sensitive-content-in-the-database}

Le schéma de la base de données AEM Forms contient des informations sensibles sur la configuration du système et les processus métier et doit être masqué derrière le pare-feu. La base de données doit être considérée comme faisant partie de la même limite de confiance que le serveur Forms. Pour éviter toute divulgation d’informations et tout vol de données d’entreprise, la base de données doit être configurée par l’administrateur de base de données (DBA) afin de n’autoriser l’accès que par les administrateurs autorisés.

Par mesure de précaution supplémentaire, vous devez envisager d’utiliser des outils spécifiques au fournisseur de la base de données pour chiffrer les colonnes dans les tableaux contenant les données suivantes :

* Clés de document Rights Management
* Clé de cryptage PIN HSM Trust Store
* hachages du mot de passe de l’utilisateur local ;

Pour plus d’informations des outils spécifiques à des revendeurs, voir [« Informations sur la sécurité des bases de données »](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr).

### Sécurité LDAP {#ldap-security}

Un répertoire LDAP (Lightweight Directory Access Protocol) est généralement utilisé par AEM Forms on JEE comme source d’informations sur les utilisateurs et les groupes d’entreprise, et comme moyen d’authentifier un mot de passe. Assurez-vous que votre annuaire LDAP est configuré pour utiliser le protocole SSL (Secure Socket Layer) et qu’AEM Forms on JEE est configuré pour accéder à votre annuaire LDAP à l’aide de son port SSL.

#### Déni de service LDAP {#ldap-denial-of-service}

Une attaque courante utilisant LDAP implique qu’un attaquant omette délibérément de s’authentifier plusieurs fois. Cela oblige le serveur d’annuaire LDAP à interdire à un utilisateur tous les services dépendant de LDAP.

Vous pouvez définir le nombre de tentatives d’échec et le délai de verrouillage consécutif mis en oeuvre par AEM Forms lorsqu’un utilisateur ne parvient pas à s’authentifier auprès d’AEM Forms à plusieurs reprises. Dans la console d’administration, choisissez des valeurs faibles. Lors de la sélection du nombre d’échecs d’authentification, il est important de comprendre qu’une fois toutes les tentatives effectuées, AEM Forms verrouille l’utilisateur avant que le serveur d’annuaire LDAP ne le fasse.

#### Définir le verrouillage automatique des comptes {#set-automatic-account-locking}

1. Connectez-vous à Administration Console.
1. Cliquez sur **Paramètres** > **Gestion des utilisateurs** > **Gestion des domaines**.
1. Sous Paramètres de verrouillage de compte automatique, définissez **Échecs d’authentification consécutifs max.** à un nombre faible, par exemple 3.
1. Cliquez sur **Enregistrer**.

### Audit et journalisation {#auditing-and-logging}

L’utilisation correcte et sécurisée des capacités de contrôle et de journalisation de l’application peut vous aider à assurer le suivi et la détection rapides de la sécurité et d’autres événements irréguliers. L’utilisation efficace de l’audit et de la journalisation dans une application inclut des éléments tels que le suivi des connexions réussies et échouées, ainsi que des événements d’application clés tels que la création ou la suppression d’enregistrements clés.

Vous pouvez utiliser le contrôle pour détecter de nombreux types d’attaques, notamment :

* Blocage du mot de passe de force
* Les attaques par déni de service
* Injection d’entrées hostiles et des classes associées d’attaques de script

Ce tableau décrit les techniques de contrôle et de journalisation que vous pouvez utiliser pour réduire les vulnérabilités de votre serveur.

<table> 
 <thead> 
  <tr> 
   <th><p>Problème</p> </th> 
   <th><p>Description</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Fichier journal ACL</p> </td> 
   <td><p>Définissez les listes de contrôle d’accès (ACL) des fichiers journaux d’AEM Forms on JEE appropriées.</p> <p>La définition des informations d’identification appropriées permet d’empêcher les attaquants de supprimer les fichiers.</p> <p>Les autorisations de sécurité du répertoire du fichier journal doivent être de type Contrôle complet pour les administrateurs et les groupes SYSTEM. Le compte utilisateur AEM Forms ne doit disposer que d’autorisations de lecture et d’écriture.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Redondance des fichiers journaux</p> </td> 
   <td><p>Si les ressources le permettent, envoyez des journaux à un autre serveur en temps réel qui n’est pas accessible par l’attaquant (en écriture uniquement) à l’aide de Syslog, Tivoli, du serveur Microsoft Operations Manager (MOM) ou d’un autre mécanisme.</p> <p>La protection des journaux de cette manière permet d’empêcher la falsification. En outre, le stockage des journaux dans un référentiel central facilite la corrélation et la surveillance (par exemple, si plusieurs serveurs de formulaires sont en cours d’utilisation et qu’une attaque par devinette de mot de passe se produit sur plusieurs ordinateurs où chaque ordinateur est interrogé pour obtenir un mot de passe).</p> </td> 
  </tr> 
 </tbody> 
</table>

### Autorisation d’un utilisateur non administrateur à exécuter PDF Generator

Vous pouvez permettre à un utilisateur non administrateur d’utiliser PDF Generator. Normalement, seuls les utilisateurs disposant de privilèges d’administrateur peuvent utiliser PDF Generator. Effectuez les étapes suivantes pour permettre à un utilisateur non administrateur d’exécuter PDF Generator :

1. Création d’un nom de variable d’environnement PDFG_NON_ADMIN_ENABLED.

1. Définissez la valeur de la variable à TRUE.

1. Redémarrez l’instance AEM Forms.

## Configuration d’AEM Forms on JEE pour un accès au-delà de l’entreprise {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

Une fois AEM Forms sur JEE installé avec succès, il est important que vous assuriez une maintenance régulière de la sécurité de votre environnement. Cette section décrit les tâches recommandées pour maintenir la sécurité de votre serveur de production AEM Forms on JEE.

### Configuration d’un proxy inverse pour l’accès web {#setting-up-a-reverse-proxy-for-web-access}

A *proxy inverse* peut être utilisé pour s’assurer qu’un ensemble d’URL pour les applications Web d’AEM Forms on JEE est disponible pour les utilisateurs externes et internes. Cette configuration est plus sûre que si vous autorisiez des utilisateurs à se connecter directement au serveur d’applications sur lequel est exécuté AEM Forms sur JEE. Le proxy inverse exécute toutes les requêtes HTTP pour le serveur d’applications qui exécute AEM Forms sur JEE. Les utilisateurs disposent uniquement d’un accès réseau au proxy inverse et peuvent uniquement tenter des connexions URL prises en charge par le proxy inverse.

**URL racine AEM Forms on JEE pour une utilisation avec un serveur proxy inverse** 

Les URL racine d’application suivantes pour chaque application Web d’AEM Forms on JEE. Configurez votre proxy inverse uniquement pour exposer les URL de fonctionnalités d’application web que vous souhaitez fournir aux utilisateurs finaux.

Certaines URL sont indiquées comme des applications web destinées aux utilisateurs finaux. Évitez d’exposer d’autres URL de Configuration Manager pour l’accès à des utilisateurs externes par le biais du proxy inverse.

<table> 
 <thead> 
  <tr> 
   <th><p>URL racine</p> </th> 
   <th><p>Objectif et/ou application web associée</p> </th> 
   <th><p>Interface web</p> </th> 
   <th><p>Accès des utilisateurs finaux</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>/ReaderExtensions/*</p> </td> 
   <td><p>Application Web d’utilisateur final d’Acrobat Reader DC extensions pour appliquer des droits d’utilisation à des documents PDF.</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Oui</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/*</p> </td> 
   <td><p>Application web pour utilisateur final Rights Management</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Oui</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edcws/*</p> </td> 
   <td><p>URL du service Web du Rights Management</p> </td> 
   <td><p>Non</p> </td> 
   <td><p>Oui</p> </td> 
  </tr> 
  <tr> 
   <td><p>/pdfgui/*</p> </td> 
   <td><p>Application Web d’administration de PDF Generator</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Oui</p> </td> 
  </tr> 
  <tr> 
   <td><p>/un espace de travail/*</p> </td> 
   <td><p>Application Web d’utilisateur final Workspace</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Oui</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace-server/*</p> </td> 
   <td><p>Servlets et services de données Workspace requis par l’application cliente Workspace</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Oui</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adobe-bootstrapper/*</p> </td> 
   <td><p>Servlet d’amorçage du référentiel AEM Forms on JEE</p> </td> 
   <td><p>Non</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/*</p> </td> 
   <td><p>Page d’informations pour les services Web de serveur de formulaires</p> </td> 
   <td><p>Non</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/services/*</p> </td> 
   <td><p>URL de service Web de tous les services de serveur de formulaires</p> </td> 
   <td><p>Non</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/admin/*</p> </td> 
   <td><p>Application Web d’administration Rights Management</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adminui/*</p> </td> 
   <td><p>Page d’accueil de la console d’administration</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/TruststoreComponent/</p> <p>secure/*</p> </td> 
   <td><p>Pages d’administration de Trust Store Management</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormsIVS/*</p> </td> 
   <td><p>Application Forms IVS pour tester et déboguer le rendu du formulaire</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputIVS/*</p> </td> 
   <td><p>Application Output IVS pour tester et déboguer le service de sortie</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rmws/*</p> </td> 
   <td><p>URL REST pour le Rights Management</p> </td> 
   <td><p>Non</p> </td> 
   <td><p>Oui</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputAdmin/*</p> </td> 
   <td><p>Pages d’administration de sortie</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/*</p> </td> 
   <td><p>Fichiers de l’application web Forms</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/GetImage</p> <p>Servlet</p> </td> 
   <td><p>Utilisé pour récupérer du code JavaScript pendant la transformation de HTML</p> </td> 
   <td><p>Non</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServerAdmin/*</p> </td> 
   <td><p>Pages d’administration Forms</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/repository/*</p> </td> 
   <td><p>URL d’accès WebDAV (débogage)</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/AACComponent/*</p> </td> 
   <td><p>Interface utilisateur des applications et services</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/WorkspaceAdmin/*</p> </td> 
   <td><p>Pages d’administration de Workspace</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rest/*</p> </td> 
   <td><p>Pages de support REST</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CoreSystemConfig/*</p> </td> 
   <td><p>Page des paramètres de configuration de base d’AEM Forms on JEE</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/</p> </td> 
   <td><p>Authentification User Management</p> </td> 
   <td><p>Non</p> </td> 
   <td><p>Oui</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/*</p> </td> 
   <td><p>Interface d’administration de User Management</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/DocumentManager/*</p> </td> 
   <td><p>Téléchargement des documents à traiter lors de l’accès aux points de fin distants, aux points de fin SOAP WSDL et au SDK Java via le transport SOAP ou le transport EJB avec activation des documents HTTP.</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Oui</p> </td> 
  </tr> 
 </tbody> 
</table>

## Protection contre les attaques multisites par usurpation de requête {#protecting-from-cross-site-request-forgery-attacks}

Un Cross-site request forgery (CSRF) exploite la confiance d’un site web envers l’utilisateur dans le but de transmettre des instructions non autorisées à son insu. Le principe de l’attaque consiste à inclure un lien ou un script dans une page web ou une URL dans un courrier électronique afin d’accéder à un autre site sur lequel l’utilisateur a déjà été authentifié.

Par exemple, vous pouvez être connecté à la console d’administration tout en explorant un autre site web. L’une des pages Web peut inclure une balise d’image HTML avec un attribut `src` visant un script côté serveur sur le site Web de la victime. En exploitant le mécanisme d’authentification de session basé sur les cookies, le site Web attaquant peut envoyer des requêtes malveillantes au script côté serveur ciblé en les faisant passer pour les requêtes de l’utilisateur autorisé. Pour obtenir d’autres exemples, voir [https://owasp.org/www-community/attacks/csrf#Examples](https://owasp.org/www-community/attacks/csrf#Examples).

Les caractéristiques suivantes sont communes aux CSRF :

* impliquent des sites qui reposent sur l’identité d’un utilisateur ;
* Exploitez la confiance du site dans cette identité.
* trompez le navigateur de l’utilisateur pour envoyer des requêtes HTTP à un site cible.
* impliquent des requêtes HTTP ayant des effets secondaires.

AEM Forms on JEE utilise la fonctionnalité de filtrage des référents pour bloquer les attaques CSRF. Les termes suivants sont utilisés dans cette section pour décrire ce dispositif de filtrage des référents :

* **Référent autorisé :** un référent est l’adresse de la page source qui envoie une requête au serveur. Pour les pages ou les formulaires JSP, ce référent est généralement la page précédente dans l’historique de navigation. Les référents pour les images sont généralement les pages sur lesquelles les images sont affichées. Vous pouvez identifier les référents autorisés à accéder à votre serveur en les ajoutant à la liste de référents autorisés.
* **Exceptions aux référents autorisés :** si vous souhaitez restreindre l’accès pour un référent particulier dans votre liste de référents autorisés. Pour mettre en place cette restriction, vous pouvez ajouter des chemins d’accès individuels de ce référent vers la liste des exceptions aux référents autorisés. Les requêtes provenant des chemins d’accès de la liste des exceptions aux référents autorisés ne peuvent appeler aucune ressource du serveur de formulaires. Vous pouvez définir des exceptions aux référents autorisés pour une application spécifique et également utiliser une liste globale des exceptions s’appliquant à toutes les applications.
* **URI autorisés :** il s’agit d’une liste des ressources générées sans vérification de l’en-tête référent. Par exemple, les ressources telles que les pages d’aide, qui n’entraînent pas de changements d’état sur le serveur, peuvent être ajoutées à cette liste. Les ressources figurant dans la liste des URI autorisés ne sont jamais bloquées par le filtrage des référents, quel que soit le référent.
* **Référent de valeur NULL (null referer) :** une requête serveur qui n’est pas associée ou ne provient pas d’une page web parente est considérée comme une requête de référent de valeur NULL. Par exemple, lorsque vous ouvrez une nouvelle fenêtre de navigateur, saisissez une adresse puis appuyez sur la touche Entrée, le référent envoyé au serveur est nul. Une application de bureau (.NET ou SWING) envoyant une requête HTTP à un serveur web envoie également un référent de valeur NULL au serveur.

### Filtrage des référents {#referer-filtering}

Le processus de filtrage des référents peut être décrit comme suit :

1. Le serveur Forms vérifie la méthode HTTP utilisée pour l’appel :

   1. S’il s’agit d’une méthode POST, le serveur Forms vérifie l’en-tête référent.
   1. S’il s’agit d’une méthode GET, le serveur de formulaires ignore la vérification du référent, à moins que la variable *CSRF_CHECK_GETS* ne soit définie sur true. Dans ce cas, il vérifie l’en-tête du référent. La variable *CSRF_CHECK_GETS* est spécifiée dans le fichier *web.xml* pour votre application.

1. Le serveur Forms vérifie si l’URI requis existe en liste autorisée :

   1. Si l’URI est autorisé, le serveur transmet la requête.
   1. Si l’URI requis n’est pas autorisé, le serveur récupère le référent de la requête.

1. S’il existe un référent pour la requête, le serveur vérifie s’il s’agit d’un référent autorisé. Si le référent est autorisé, le serveur vérifie qu’il ne fait pas partie des exceptions aux référents autorisés :

   1. S’il s’agit d’une exception, la requête est bloquée.
   1. S’il ne s’agit pas d’une exception, la requête est transmise.

1. S’il n’existe aucun référent pour la requête, le serveur vérifie que les référents de valeur NULL sont autorisés :

   1. Si les référents de valeur NULL sont autorisés, la requête est transmise.
   1. Si ce n’est pas le cas, le serveur vérifie que l’URI requis fait partie des exceptions aux référents de valeur NULL et traite la requête en fonction.

### Gérer le filtrage des référents {#managing-referer-filtering}

AEM Forms on JEE effectue un filtrage des référents afin de spécifier les référents qui sont autorisés à accéder aux ressources du serveur. Par défaut, le filtrage des référents ne filtre pas les requêtes qui utilisent une méthode HTTP sécurisée, par exemple GET, sauf si *CSRF_CHECK_GETS* est défini sur true. Si le numéro de port pour un référent autorisé est défini sur 0, AEM Forms on JEE autorisera toutes les requêtes des référents provenant de cet hôte quel que soit le numéro de port. Si aucun numéro de port n’est spécifié, seules les requêtes provenant du port par défaut 80 (HTTP) ou du port 443 (HTTPS) sont autorisées. Le filtrage des référents est désactivé si toutes les entrées de la liste de référents autorisés sont supprimées.

Lorsque vous installez Document Services pour la première fois, la liste de référents autorisés est mise à jour avec l’adresse du serveur sur lequel Document Services est installé. Les entrées pour le serveur comprennent le nom du serveur, l’adresse IPv4, l’adresse IPv6 si le protocole IPv6 est activé, l’adresse de bouclage et une entrée localhost. Les noms ajoutés à la liste de référents autorisés sont renvoyés par le système d’exploitation hôte. Par exemple, un serveur dont l’adresse IP est 10.40.54.187 contiendra les entrées suivantes : `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`. Pour chaque nom non qualifié renvoyé par le système d’exploitation hôte (les noms sans adresse IPv4, IPv6 ou sans nom de domaine qualifié) la liste autorisée n’est pas mise à jour. Modifiez la liste de référents autorisés en fonction de votre environnement de travail. Ne déployez pas le serveur de formulaires dans l’environnement de production avec la liste de référents autorisés par défaut. Après avoir modifié l’un des référents autorisés, l’une des exceptions aux référents ou l’un des URI, assurez-vous de redémarrer le serveur pour que les modifications prennent effet.

**Gérer la liste de référents autorisés**

Vous pouvez gérer la liste de référents autorisés à partir de l’interface User Management de la console d’administration. L’interface User Management offre des fonctionnalités pour créer, éditer ou supprimer la liste. Pour plus d’informations sur l’utilisation de la liste de référents autorisés, reportez-vous à la section [Prévenir les attaques CSRF](/help/forms/using/admin-help/preventing-csrf-attacks.md) du guide *Aide à l’administration*.

**Gérer les exceptions aux référents autorisés et des listes des URI autorisés**

AEM Forms on JEE fournit des API pour gérer la liste des exceptions aux référents autorisés et la liste des URI autorisés. Vous pouvez utiliser ces API pour récupérer, créer, modifier ou supprimer la liste. Voici une liste des API disponibles :

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

Pour plus d’informations sur les API, reportez-vous à la référence API d’AEM Forms on JEE.

Utilisez la liste ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** pour les exceptions aux référents autorisés au niveau global, c’est-à-dire pour définir les exceptions qui s’appliquent à toutes les applications. Cette liste contient uniquement des URI ayant soit un chemin absolu (par exemple `/index.html`), soit un chemin relatif (par exemple `/sample/`). Vous pouvez également ajouter une expression régulière à la fin d’un URI relatif, par ex. `/sample/(.)*`.

L’ID de liste ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** est définie comme une constante dans la classe `UMConstants` de l’espace de noms `com.adobe.idp.um.api`, figurant dans `adobe-usermanager-client.jar`. Vous pouvez utiliser les API AEM Forms pour créer, modifier ou éditer cette liste. Par exemple, pour créer la liste globale des exceptions aux référents autorisés, utilisez :

```java
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

Utilisez la liste ***CSRF_ALLOWED_REFERER_EXCEPTIONS*** pour les exceptions spécifiques à une application.

**Désactiver le filtrage des référents**

Dans le cas où le filtrage des référents bloque complètement l’accès au serveur de formulaires et que vous ne pouvez pas modifier la liste des référents autorisés, vous pouvez mettre à jour le script de démarrage du serveur et désactiver le filtrage des référents.

Incluez l’argument JAVA `-Dlc.um.csrffilter.disabled=true` dans le script de démarrage et redémarrez le serveur. Assurez-vous de supprimer l’argument JAVA après avoir correctement reconfiguré la liste de référents autorisés.

**Filtrer les référents pour les fichiers WAR personnalisés**

Vous avez peut-être créé des fichiers WAR personnalisés afin de travailler avec AEM Forms sur JEE pour répondre aux besoins de l’activité. Pour activer le filtrage des référents pour vos fichiers WAR personnalisés, vous devez inclure ***adobe-usermanager-client.jar*** dans le chemin de classe pour les fichiers WAR et inclure une entrée de filtre dans le fichier « web.xml » avec les paramètres suivants :

**CSRF_CHECK_GETS** contrôle la vérification du référent pour les requêtes GET. Si ce paramètre n’est pas défini, la valeur par défaut est définie sur false. Incluez ce paramètre uniquement si vous souhaitez filtrer vos requêtes de GET.

**CSRF_ALLOWED_REFERER_EXCEPTIONS** est l’identifiant de la liste des exceptions aux référents autorisés. Le filtrage des référents empêche les requêtes de référents de la liste identifiés par l’identifiant de la liste d’appeler toute ressource du serveur de formulaires.

**CSRF_ALLOWED_URIS_LIST_NAME** est l’ID de la liste des URI autorisés. Le filtrage des référents ne bloque pas les requêtes concernant les ressources de la liste identifiées par l’ID de liste, quelle que soit la valeur de l’en-tête référent dans la requête.

**CSRF_ALLOW_NULL_REFERER** contrôle le comportement du filtrage des référents lorsque le référent est null ou non présent. Si ce paramètre n’est pas défini, la valeur par défaut est définie sur false. Incluez ce paramètre uniquement si vous souhaitez autoriser les référents ayant pour valeur NULL. L’autorisation des référents ayant pour valeur NULL peut permettre certains types d’attaques CSRF (Cross Site Request Forgery).

**CSRF_NULL_REFERER_EXCEPTIONS** est une liste des URI pour lesquels une vérification référent n’est pas exécutée lorsque la valeur du référent est null. Ce paramètre est activé uniquement lorsque *CSRF_ALLOW_NULL_REFERER* est définie sur false. Séparez plusieurs URI dans la liste par une virgule.

Voici un exemple de l’entrée de filtre dans la variable *web.xml* pour un ***EXEMPLE*** Fichier WAR :

```java
<filter> 
       <filter-name> filter-name </filter-name> 
       <filter-class> com.adobe.idp.um.auth.filter.RemoteCSRFFilter </filter-class> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_ALLOW_NULL_REFERER </param-name> 
      <param-value> false </param-value> 
     </init-param> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_CHECK_GETS </param-name> 
      <param-value> true </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
       <param-name> CSRF_NULL_REFERER_EXCEPTIONS </param-name> 
       <param-value> /SAMPLE/login, /SAMPLE/logout  </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_REFERER_EXCEPTIONS </param-name> 
      <param-value> SAMPLE_ALLOWED_REF_EXP_ID </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_URIS_LIST_NAME </param-name> 
      <param-value> SAMPLE_ALLOWED_URI_LIST_ID     </param-value> 
     </init-param> 
</filter> 
    ........ 
    <filter-mapping> 
      <filter-name> filter-name </filter-name> 
      <url-pattern>/*</url-pattern> 
    </filter-mapping>
```

**Résolution des incidents**

Si des requêtes serveur légitimes sont bloquées par le filtre CSRF, essayez l’une des méthodes suivantes :

* Si la requête rejetée a un en-tête référent, il peut être intéressant de l’ajouter à liste des référents autorisés. Ajoutez uniquement les référents auxquels vous faites confiance.
* Si la requête rejetée ne dispose pas d’un en-tête référent, modifiez votre application client pour inclure un en-tête référent.
* Si le client peut travailler dans un navigateur, essayez ce modèle de déploiement.
* En dernier recours, vous pouvez ajouter la ressource à la liste des URI autorisés. Ce paramètre n’est pas recommandé.

## Configuration réseau sécurisée {#secure-network-configuration}

Cette section décrit les protocoles et les ports requis par AEM Forms on JEE et fournit des recommandations pour le déploiement d’AEM Forms on JEE dans une configuration réseau sécurisée.

### Protocoles réseau utilisés par AEM Forms on JEE {#network-protocols-used-by-aem-forms-on-jee}

Lorsque vous configurez une architecture réseau sécurisée comme décrit dans la section précédente, les protocoles réseau suivants sont requis pour l’interaction entre AEM Forms on JEE et d’autres systèmes du réseau de votre entreprise.

<table> 
 <thead> 
  <tr> 
   <th><p>Protocole</p> </th> 
   <th><p>Utilisez</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>HTTP</p> </td> 
   <td> 
    <ul> 
     <li><p>Le navigateur affiche Configuration Manager et les applications Web destinées aux utilisateurs finaux.</p> </li> 
     <li><p>Toutes les connexions SOAP</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP</p> </td> 
   <td> 
    <ul> 
     <li><p>des applications clientes de services Web, telles que des applications .NET ;</p> </li> 
     <li><p>Adobe Reader® utilise SOAP pour les services Web du serveur AEM Forms on JEE</p> </li> 
     <li><p>Les applications Adobe Flash® utilisent SOAP pour les services Web de serveur de formulaires</p> </li> 
     <li><p>Appels SDK AEM Forms on JEE en mode SOAP</p> </li> 
     <li><p>Environnement de conception de Workbench</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>Appels SDK AEM Forms on JEE en mode Enterprise JavaBeans (EJB)</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP / POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>Entrée par courrier électronique dans un service (point de fin de courrier électronique)</p> </li> 
     <li><p>Notifications de tâches utilisateur par e-mail</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>UNC File IO</p> </td> 
   <td><p>Surveillance d’AEM Forms on JEE des dossiers de contrôle pour l’entrée dans un service (point de fin du dossier de contrôle)</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Synchronisations des informations sur les utilisateurs et les groupes de l’organisation dans un annuaire</p> </li> 
     <li><p>Authentification LDAP pour les utilisateurs interactifs</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>Appels de requête et de procédure à une base de données externe lors de l’exécution d’un processus à l’aide du service JDBC</p> </li> 
     <li><p>Référentiel AEM Forms on JEE d’accès interne</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>Permet la navigation à distance du référentiel de conception d’AEM Forms on JEE (formulaires, fragments, etc.) par n’importe quel client WebDAV.</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>Adobe des applications Flash, où les services du serveur AEM Forms on JEE sont configurés avec un point de fin Remoting.</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>AEM Forms on JEE expose les MBeans pour la surveillance à l’aide de JMX</p> </td> 
  </tr> 
 </tbody> 
</table>

### Ports pour les serveurs d’applications {#ports-for-application-servers}

Cette section décrit les ports par défaut (et les plages de configuration alternatives) pour chaque type de serveur d’applications pris en charge. Ces ports doivent être activés ou désactivés sur le pare-feu interne, selon la fonctionnalité réseau que vous souhaitez autoriser aux clients qui se connectent au serveur d’applications exécutant AEM Forms on JEE.

>[!NOTE]
>
>Par défaut, le serveur expose plusieurs MBeans JMX sous l’espace de noms adobe.com . Seules les informations utiles à la surveillance de l’intégrité du serveur sont exposées. Toutefois, pour empêcher la divulgation d’informations, vous devez empêcher les appelants d’un réseau non approuvé de rechercher des MBeans JMX et d’accéder aux mesures d’intégrité.

**Ports JBoss**

<table> 
 <thead> 
  <tr> 
   <th><p>Objectif</p> </th> 
   <th><p>Port</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Accès aux applications web</p> </td> 
   <td><p>[JBOSS_Root]/standalone/configuration/lc_[base_données].xml</p> <p>Port HTTP/1.1 Connector 8080</p> <p>Port AJP 1.3 Connector 8009</p> <p>Port SSL/TLS Connector 8443</p> </td> 
  </tr> 
  <tr> 
   <td><p>Prise en charge de CORBA</p> </td> 
   <td><p>[racine JBoss]/server/all/conf/jacorb.properties</p> <p>OAPort 3528</p> <p>OASSLPort 3529</p> </td> 
  </tr> 
 </tbody> 
</table>

**Ports WebLogic**

<table> 
 <thead> 
  <tr> 
   <th><p>Objectif</p> </th> 
   <th><p>Port</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Accès aux applications web</p> </td> 
   <td> 
    <ul> 
     <li><p>Port d’écoute d’Admin Server : La valeur par défaut est 7001</p> </li> 
     <li><p>Port d’écoute SSL d’Admin Server : La valeur par défaut est 7002</p> </li> 
     <li><p>Port configuré pour le serveur géré, par exemple 8001</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>Ports d’administration WebLogic non requis pour l’accès à AEM Forms on JEE</p> </td> 
   <td> 
    <ul> 
     <li><p>Port d’écoute de Managed Server : Configurable de 1 à 65534</p> </li> 
     <li><p>Port d’écoute SSL du serveur géré : Configurable de 1 à 65534</p> </li> 
     <li><p>Port d’écoute de Node Manager : La valeur par défaut est 5556</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**Ports WebSphere **

Pour plus d’informations sur les ports WebSphere requis par AEM Forms sur JEE, consultez Configuration des numéros de ports dans l’interface utilisateur de WebSphere Application Server.

### Configuration de SSL {#configuring-ssl}

En vous référant à l’architecture physique décrite dans la section [Architecture physique d’AEM Forms sur JEE](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture), configurez SSL pour toutes les connexions que vous prévoyez d’utiliser. Spécifiquement, toutes les connexions SOAP doivent être établies via SSL pour empêcher que les informations d’identification des utilisateurs soient exposées sur un réseau.

Pour obtenir des instructions sur la manière de configurer SSL sur JBoss, WebLogic et WebSphere, consultez « Configuration de SSL » dans l’[aide d’administration](https://www.adobe.com/go/learn_aemforms_admin_64_fr).

Pour plus d’informations sur l’importation de certificats dans JVM (Java Virtual Machine) configuré pour un serveur AEM Forms, consultez la section Authentification mutuelle dans l’[Aide d’AEM Forms Workbench](https://www.adobe.com/go/learn_aemforms_workbench_65_fr).

### Configuration de la redirection SSL {#configuring-ssl-redirect}

Une fois que vous avez configuré votre serveur d’applications pour prendre en charge le protocole SSL, vous devez vous assurer que tout le trafic HTTP vers les applications et services est appliqué pour utiliser le port SSL.

Pour configurer la redirection SSL pour WebSphere ou WebLogic, consultez la documentation de votre serveur d’applications.

1. Ouvrez une invite de commande, accédez au répertoire /JBOSS_HOME/standalone/configuration, puis exécutez la commande suivante :

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. Ouvrez le fichier JBOSS_HOME/standalone/configuration/standalone.xml pour le modifier.

   Après l’élément &lt;subsystem xmlns=&quot;urn:jboss:domaine:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;>, ajoutez les détails suivants :

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot;/>

1. Ajoutez le code suivant dans l’élément HTTPS connector :

   ```xml
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   Enregistrez le fichier autonome .xml, puis fermez-le.

## Recommandations de sécurité spécifiques à Windows {#windows-specific-security-recommendations}

Cette section contient des recommandations de sécurité spécifiques à Windows dans le cadre de l’exécution d’AEM Forms sur JEE.

### Comptes JBoss Service {#jboss-service-accounts}

L’installation clé en main d’AEM Forms sur JEE installe un compte de service par défaut en utilisant le compte système local. Le compte utilisateur système local intégré présente un haut niveau d’accessibilité ; il fait partie du groupe Administrateurs . Si une identité de processus de travail s’exécute en tant que compte utilisateur système local, ce processus de travail dispose d’un accès complet à l’ensemble du système.

#### Exécution du serveur d’applications à l’aide d’un compte non administratif {#run-the-application-server-using-a-non-administrative-account}

1. Dans la console de gestion Microsoft (MMC), créez un utilisateur local pour que le service de serveur de formulaires se connecte en tant que :

   * Sélectionner **L’utilisateur ne peut pas changer de mot de passe**.
   * Vérifiez que le groupe Utilisateurs figure dans l’onglet **Membre de**.

1. Sélectionner **Paramètres** > **Outils d’administration** > **Services**.
1. Double-cliquez sur le service du serveur d’applications et arrêtez le service.
1. Sur le **Connexion** onglet, sélectionnez **Ce compte**, recherchez le compte utilisateur que vous avez créé et saisissez le mot de passe du compte.
1. Dans la fenêtre Paramètres de sécurité locaux, sous Attribution des droits utilisateur, attribuez les droits suivants au compte utilisateur sous lequel est exécuté le serveur de formulaires :

   * Refuser de se connecter via les services Terminal
   * Interdire l’ouverture d’une session locale
   * Ouvrir une session en tant que service (ce droit doit être déjà défini)

1. Donnez au nouveau compte utilisateur les autorisations de modification sur les répertoires suivants :
   * **Répertoire de stockage global de documents** : l’emplacement du répertoire de stockage global de documents est configuré manuellement pendant le processus d’installation d’AEM Forms. Si le paramètre d’emplacement du stockage global de documents n’est pas défini pendant l’installation, l’emplacement par défaut utilisé est un sous-répertoire de l’emplacement d’installation du serveur d’applications : `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **Répertoire CRX-Repository** : l’emplacement par défaut est `[AEM-Forms-installation-location]\crx-repository`
   * **Répertoires temporaires AEM Forms** :
      * (Windows) Chemin TMP ou TEMP tel que défini dans les variables d’environnement
      * (AIX, Linux ou Solaris) Répertoire racine de l’utilisateur connecté Sur les systèmes UNIX, un utilisateur non root peut utiliser le répertoire suivant comme répertoire temporaire :
      * (Linux) /var/tmp ou /usr/tmp
      * (AIX) /tmp ou /usr/tmp
      * (Solaris) /var/tmp ou /usr/tmp
1. Donnez au nouveau compte utilisateur les autorisations d’écriture pour les répertoires suivants :
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   >L’emplacement de l’installation par défaut de JBoss Application Server :
   >
   >* Windows : C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   >* Linux : /opt/jboss/.


1. Démarrez le service du serveur d’applications.

### Sécurité du système de fichiers {#file-system-security}

AEM Forms on JEE utilise le système de fichiers comme suit :

* Stocke les fichiers temporaires utilisés lors du traitement des entrées et sorties de document
* Stocke les fichiers dans la banque d’archives globale utilisés pour prendre en charge les composants de solution installés.
* Les dossiers de contrôle stockent les fichiers déposés qui sont utilisés comme entrée d’un service à partir d’un emplacement de dossier du système de fichiers.

Lorsque vous utilisez des dossiers de contrôle comme moyen d’envoyer et de recevoir des documents avec un service de serveur de formulaires, prenez des précautions supplémentaires en matière de sécurité du système de fichiers. Lorsqu’un utilisateur dépose du contenu dans le dossier de contrôle, ce contenu est exposé via le dossier de contrôle. Dans ce cas, le service n’authentifie pas l’utilisateur final réel. Au lieu de cela, il s’appuie sur la sécurité de niveau ACL et Partage pour être défini au niveau du dossier afin de déterminer qui peut effectivement appeler le service.

## Recommandations de sécurité spécifiques à JBoss {#jboss-specific-security-recommendations}

La présente section propose des recommandations relatives à la configuration du serveur d’applications qui sont spécifiques à JBoss 7.0.6. lorsque celui-ci est utilisé pour exécuter AEM Forms sur JEE.

### Désactivation de la console de gestion JBoss et de la console JMX {#disable-jboss-management-console-and-jmx-console}

L’accès à la console de gestion JBoss et à la console JMX est déjà configuré (la surveillance JMX est désactivée) lorsque vous installez AEM Forms on JEE sur JBoss à l’aide de la méthode d’installation clé en main. Si vous utilisez votre propre serveur d’applications JBoss, assurez-vous que l’accès à la console de gestion JBoss et à la console de surveillance JMX est sécurisé. L’accès à la console de surveillance JMX est défini dans le fichier de configuration JBoss appelé jmx-invoker-service.xml.

### Désactivation de la navigation dans les répertoires {#disable-directory-browsing}

Une fois connecté à Administration Console, il est possible de parcourir la liste des répertoires de la console en modifiant l’URL. Par exemple, si vous modifiez l’URL pour l’une de ces adresses, une liste de répertoires s’affiche :

```java
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## Recommandations de sécurité spécifiques à WebLogic {#weblogic-specific-security-recommendations}

Cette section présente des recommandations relatives à la configuration du serveur d’applications et spécifiques à WebLogic 9.1 lors de l’exécution d’AEM Forms on JEE.

### Désactivation de la navigation dans les répertoires {#disable_directory_browsing-1}

Définissez les propriétés index-directories du fichier weblogic.xml sur `false`, comme illustré dans l’exemple suivant :

```xml
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### Activation du port SSL de WebLogic {#enable-weblogic-ssl-port}

Par défaut, WebLogic n’active pas le port d’écoute SSL par défaut, 7002. Activez ce port dans WebLogic Server Administration Console avant de configurer SSL.

## Recommandations de sécurité spécifiques à WebSphere {#websphere-specific-security-recommendations}

Cette section contient des recommandations relatives à la configuration du serveur d’applications et destinées à sécuriser WebSphere lors de l’exécution d’AEM Forms on JEE.

### Désactivation de la navigation dans les répertoires {#disable_directory_browsing-2}

Définissez la propriété `directoryBrowsingEnabled` du fichier ibm-web-ext.xml sur `false`.

### Activation de la sécurité administrative de WebSphere {#enable-websphere-administrative-security}

1. Connectez-vous à la console d’administration WebSphere.
1. Dans l’arborescence de navigation, accédez à **Sécurité** > **Sécurité globale**
1. Sélectionner **Activation de la sécurité administrative**.
1. Désélectionner les deux **Activation de la sécurité des applications** et **Utiliser la sécurité Java 2**.
1. Cliquez sur **OK** ou **Appliquer**.
1. Dans le **Messages** , cliquez sur **Enregistrer directement dans la configuration principale**.
