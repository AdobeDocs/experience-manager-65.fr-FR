---
title: Sécurisation de votre environnement d’AEM Forms sur JEE
description: Découvrez divers paramètres de renforcement de la sécurité pour améliorer la sécurité d’AEM Forms sur JEE dans le cadre d’une exécution pour un intranet d’entreprise.
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
role: Admin
exl-id: 6fb260f9-d0f8-431e-8d4e-535b451e4124
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '7608'
ht-degree: 100%

---

# Sécurisation de votre environnement d’AEM Forms sur JEE {#hardening-your-aem-forms-on-jee-environment}

Découvrez divers paramètres de renforcement de la sécurité pour améliorer la sécurité d’AEM Forms sur JEE dans le cadre d’une exécution pour un intranet d’entreprise.

Cet article fournit des recommandations et des bonnes pratiques de sécurisation des serveurs exécutant AEM Forms sur JEE. Il ne vise pas à expliquer de manière exhaustive comment renforcer des hôtes pour votre système d’exploitation et vos serveurs d’applications. Au lieu de cela, cet article décrit plusieurs paramètres de renforcement de la sécurité, que vous pouvez implémenter pour améliorer la sécurité d’AEM Forms lorsque celui-ci est exécuté pour un intranet d’entreprise. Toutefois, pour que les serveurs d’applications AEM Forms sur JEE restent sécurisés, vous devez également implémenter des procédures de surveillance, de détection et de réponse de sécurité.

Cet article décrit des techniques de renforcement à appliquer au cours des étapes suivantes, lors du cycle de vie de l’installation et de la configuration :

* **Préinstallation :** utilisez ces techniques avant d’installer AEM Forms sur JEE.
* **Installation :** utilisez ces techniques pendant le processus d’installation d’AEM Forms sur JEE.
* **Post-installation :** utilisez ces techniques après l’installation, puis de manière régulière.

AEM Forms sur JEE est hautement personnalisable et compatible avec de nombreux environnements. Certaines des recommandations peuvent ne pas correspondre aux besoins de votre organisation.

## Préinstallation {#preinstallation}

Avant d’installer AEM Forms sur JEE, vous pouvez appliquer des solutions de sécurité à la couche réseau et au système d’exploitation. Cette section décrit certains problèmes et fournit des recommandations pour réduire les vulnérabilités de la sécurité dans ces domaines.

**Installation et configuration sous UNIX et Linux**

Vous ne devez pas installer ni configurer AEM Forms sur JEE à l’aide d’un shell racine. Par défaut, les fichiers sont installés sous le répertoire /opt et l’utilisateur ou l’utilisatrice qui effectue l’installation a besoin de disposer de toutes les autorisations de fichier sous /opt. De même, une personne peut parfaitement exécuter une installation sous un répertoire /user dans lequel elle dispose de toutes les autorisations de fichier.

**Installation et configuration sous Windows**

Sous Windows, vous devez effectuer l’installation en tant qu’administrateur ou administratrice si vous installez AEM Forms sur JEE sur JBoss à l’aide de la procédure clé en main ou si vous installez PDF Generator. Par ailleurs, lorsque vous installez PDF Generator sous Windows avec prise en charge des applications natives, vous devez exécuter l’installation sous la même identité que l’utilisateur ou utilisatrice Windows ayant installé Microsoft Office. Pour plus de détails sur l’installation des privilèges, reportez-vous au document Installer et déployer AEM Forms sur JEE de votre serveur d’applications.

### Sécurité de la couche réseau {#network-layer-security}

Les vulnérabilités de sécurité réseau comptent parmi les premières menaces qui affectent les serveurs d’applications accessibles par Internet ou par un intranet. Cette section décrit le processus de renforcement des hôtes du réseau contre ces vulnérabilités. Elle traite de la segmentation du réseau, du renforcement de la pile TCP/IP (Transmission Control Protocol/Internet Protocol) et de l’utilisation de pare-feux pour protéger les hôtes.

Le tableau suivant décrit des processus classiques qui permettent de réduire les vulnérabilités de la sécurité réseau.

<table> 
 <thead> 
  <tr> 
   <th><p>Problème</p> </th> 
   <th><p>Description</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Zones démilitarisées</p> </td> 
   <td><p>Déployez des serveurs de formulaires dans une zone démilitarisée. Une segmentation doit avoir été définie dans au moins deux niveaux avec le serveur d’applications utilisé pour exécuter AEM Forms sur JEE placé derrière le pare-feu interne. Séparez le réseau externe de la zone démilitarisée qui contient les serveurs web, lesquels doivent par ailleurs être séparés du réseau interne. Utilisez des pare-feux pour implémenter les couches de séparation. Classez et contrôlez le trafic passant par chaque couche réseau pour vous assurer que le minimum absolu de données requises est autorisé.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Adresses IP privées</p> </td> 
   <td><p>Utilisez la technique NAT (Network Address Translation) avec des adresses IP privées RFC 1918, pour les serveurs de l’application AEM Forms. Attribuez des adresses IP privées (10.0.0.0/8, 172.16.0.0/12 et 192.168.0.0/16) pour rendre plus difficile, pour une personne malveillante, le routage du trafic depuis et vers un hôte interne NAT via Internet.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Pare-feux</p> </td> 
   <td><p>Utilisez les critères suivants pour sélectionner une solution de pare-feu :</p> 
    <ul> 
     <li><p>Implémentez des pare-feux qui prennent en charge les serveurs proxy et/ou la <em>vérification avec état</em> plutôt que de simples solutions de filtrage des paquets.</p> </li> 
     <li><p>Utilisez un pare-feu qui prend en charge un paradigme de sécurité de type <em>Refuser tous les services hormis ceux autorisés explicitement</em>.</p> </li> 
     <li><p>Implémentez une solution de pare-feu à double hébergement ou à hébergement multiple. Cette architecture offre un niveau de sécurité optimal et permet d’empêcher les personnes non autorisées de contourner le pare-feu.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>Ports de base de données</p> </td> 
   <td><p>N’utilisez pas de ports d’écoute par défaut pour les bases de données (MySQL - 3306, Oracle - 1521, MS SQL - 1433). Pour plus d’informations sur la modification des ports de base de données, consultez la documentation de votre base de données.</p> <p>L’utilisation d’un port de base de données différent affecte la configuration globale d’AEM Forms sur JEE. Si vous modifiez les ports par défaut, vous devez modifier en conséquence la configuration et, notamment, les sources de données d’AEM Forms sur JEE.</p> <p>Pour obtenir des informations sur la configuration des sources de données dans AEM Forms sur JEE, voir Installer et déployer AEM Forms sur JEE ou Mettre à niveau vers AEM Forms sur JEE pour votre serveur d’applications, dans le <a href="/help/forms/using/introduction-aem-forms.md" target="_blank">Guide de l’utilisateur AEM Forms</a>.</p> </td> 
  </tr> 
 </tbody> 
</table>

### Sécurité du système d’exploitation {#operating-system-security}

Le tableau suivant décrit plusieurs approches utilisables pour minimiser les vulnérabilités de sécurité du système d’exploitation.

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
   <td><p>Le risque qu’une personne non autorisée accède au serveur d’application est accru si les correctifs et les mises à jour de sécurité du fournisseur ne sont pas appliqués en temps voulu. Testez les correctifs de sécurité avant de les appliquer aux serveurs de production.</p><p>De même, créez des politiques et des procédures pour contrôler et installer régulièrement les correctifs.</p></td> 
  </tr> 
  <tr> 
   <td><p>Logiciels de protection antivirus</p></td> 
   <td><p>Les antivirus peuvent identifier les fichiers infectés en recherchant une signature ou en observant un comportement inhabituel. Ces antivirus conservent la signature des virus dans un fichier, qui est généralement stocké sur le disque dur local. De nouveaux virus étant découverts régulièrement, mettez fréquemment à jour ce fichier pour permettre à l’antivirus d’identifier tous les virus actuels.</p></td> 
  </tr> 
  <tr> 
   <td><p>NTP (Network Time Protocol)</p></td> 
   <td><p>Pour les analyses légales, veillez à ce que l’heure des serveurs de fomulaires soit toujours exacte. Utilisez le protocole NTP pour synchroniser l’heure sur tous les systèmes connectés directement à Internet.</p></td> 
  </tr> 
 </tbody> 
</table>

Pour plus d’informations de sécurité pour votre système d’exploitation, consultez [« Informations sur la sécurité des systèmes d’exploitation »](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr).

## Installation {#installation}

Cette section décrit des techniques que vous pouvez utiliser pendant le processus d’installation d’AEM Forms pour réduire les failles de sécurité. Dans certains cas, ces techniques utilisent des options qui font partie du processus d’installation. Le tableau suivant décrit ces techniques.

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
   <td><p>Utilisez le minimum de droits requis pour installer le logiciel. Connectez-vous à votre ordinateur via un compte qui n’appartient pas au groupe d’administration. Sous Windows, vous pouvez utiliser la commande Exécuter pour exécuter le programme d’installation d’AEM Forms sur JEE en tant qu’utilisateur non administrateur. Sous UNIX et Linux, utilisez une commande comme <code>sudo</code> pour installer le logiciel.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Source du logiciel</p> </td> 
   <td><p>Ne téléchargez pas et n’exécutez pas AEM Forms sur JEE à partir de sources non approuvées.</p> <p>Les programmes malveillants peuvent contenir un code permettant de compromettre la sécurité de plusieurs manières, notamment par le vol, la modification et la suppression de données, ainsi que par le déni de service. Installez AEM Forms sur JEE à partir du DVD d’Adobe ou à partir d’une source approuvée uniquement.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Partitions de disque</p> </td> 
   <td><p>Placez AEM Forms sur JEE sur une partition de disque dédiée. La segmentation de disque est un processus qui permet de conserver des données spécifiques sur des disques physiques séparés de votre serveur, pour une sécurité accrue. Le fait d’organiser les données ainsi permet de réduire le risque d’attaques par traversée de répertoire. Prévoyez de créer une partition distincte de la partition système, dans laquelle vous pouvez installer le répertoire de contenu AEM Forms sur JEE. (Sous Windows, la partition système contient le répertoire system32, ou partition de démarrage.)</p> </td> 
  </tr> 
  <tr> 
   <td><p>Composants</p> </td> 
   <td><p>Évaluez les services existants et désactivez ou désinstallez ceux qui ne sont pas nécessaires. N’installez pas de composants et de services inutiles.</p> <p>L’installation par défaut d’un serveur d’applications peut inclure des services dont vous n’avez aucune utilité. Vous devez désactiver tous les services inutiles avant le déploiement afin de minimiser les points d’entrée d’une attaque. Par exemple, sur JBoss, vous pouvez placer en commentaire les services inutiles dans le fichier descripteur META-INF/jboss-service.xml.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Fichier de politique interdomaine</p> </td> 
   <td><p>La présence d’un fichier <code>crossdomain.xml</code> sur le serveur peut immédiatement affaiblir ce serveur. Il est recommandé de rendre la liste des domaines aussi restrictive que possible. Ne placez pas en production le fichier <code>crossdomain.xml</code> utilisé pendant la phase de développement lors de l’utilisation des guides <em>(obsolète)</em>. Dans le cas d’un guide qui utilise les services Web, si le service figure sur le même serveur ayant servi le guide, aucun fichier <code>crossdomain.xml</code> n’est nécessaire. En revanche, si le service figure sur un autre serveur ou si des grappes sont impliquées, la présence d’un fichier <code>crossdomain.xml</code> est nécessaire. Voir <a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a>, pour plus d’informations sur le fichier crossdomain.xml.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Paramètres de sécurité du système d’exploitation</p> </td> 
   <td><p>Si vous devez utiliser un chiffrement XML 192 bits ou 256 bits sur les plateformes Solaris, assurez-vous d’installer <code>pkcs11_softtoken_extra.so</code> au lieu de <code>pkcs11_softtoken.so</code>.</p> </td> 
  </tr> 
 </tbody> 
</table>

## Étapes de post-installation {#post-installation-steps}

Une fois AEM Forms sur JEE installé avec succès, il est important que vous assuriez une maintenance régulière de l’environnement pour en optimiser la sécurité.

La section suivante décrit en détail les différentes tâches recommandées pour sécuriser le serveur Forms Server déployé.

### Sécurité d’AEM Forms {#aem-forms-security}

Les paramètres recommandés suivants s’appliquent au serveur AEM Forms sur JEE hors de l’application Web administrative. Pour réduire les risques de sécurité du serveur, appliquez ces paramètres immédiatement après avoir installé AEM Forms sur JEE.

**Correctifs de sécurité**

Le risque de voir une personne non autorisée accéder au serveur d’applications s’accroît si les correctifs de sécurité et les mises à niveau du revendeur ne sont pas appliqués en temps utile. Testez les correctifs de sécurité avant de les appliquer aux serveurs de production pour vous assurer de la compatibilité et de la disponibilité des applications. De même, créez des politiques et des procédures pour contrôler et installer régulièrement les correctifs. Les mises à jour d’AEM Forms sur JEE se trouvent sur le site de téléchargement des produits Enterprise.

**Comptes de service (JBoss clé en main sous Windows uniquement)**

AEM Forms sur JEE installe un service par défaut en utilisant le compte système local. Le compte d’utilisateur système local intégré présente un haut niveau d’accessibilité ; il fait partie du groupe d’administration. Si une identité de processus de travail est exécutée en tant que compte d’utilisateur système local, ce processus de travail dispose d’un accès complet à l’ensemble du système.

Pour exécuter le serveur d’applications sur lequel est déployé AEM Forms sur JEE, appliquez les instructions suivantes en utilisant un compte non administratif spécifique :

1. Dans Microsoft Management Console (MMC), créez un utilisateur local ou une utilisatrice locale que le service Forms Server peut utiliser pour se connecter :

   * Sélectionnez **L’utilisateur ne peut pas changer de mot de passe**.
   * Vérifiez que le groupe **Utilisateurs** figure dans l’onglet **Membre de**.

   >[!NOTE]
   >
   >Vous ne pouvez pas modifier ce paramètre pour PDF Generator.

1. Sélectionnez **Démarrer** > **Paramètres** > **Outils d’administration** > **Services**.
1. Double-cliquez sur l’application JBoss pour AEM Forms sur JEE et arrêtez le service.
1. Sur l’onglet **Connexion**, sélectionnez **Ce compte**, recherchez le compte d’utilisateur que vous avez créé et saisissez le mot de passe du compte.
1. Dans MMC, ouvrez **Paramètres de sécurité locaux** et sélectionnez **Politiques locales** > **Attribution des droits utilisateur**.
1. Attribuez les droits suivants au compte d’utilisateur avec lequel le serveur Forms Server est exécuté :

   * Interdire l’ouverture de session par les services Terminal
   * Interdire l’ouverture d’une session locale
   * Ouvrir une session en tant que service (ce droit doit être déjà défini)

1. Donnez au nouveau compte d’utilisateur les autorisations de modification sur les répertoires suivants :
   * **Répertoire de stockage global de documents** : l’emplacement du répertoire de stockage global de documents est configuré manuellement pendant le processus d’installation d’AEM Forms. Si le paramètre d’emplacement du stockage global de documents n’est pas défini pendant l’installation, l’emplacement par défaut utilisé est un sous-répertoire de l’emplacement d’installation du serveur d’applications : `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **Répertoire CRX-Repository** : l’emplacement par défaut est `[AEM-Forms-installation-location]\crx-repository`
   * **Répertoires temporaires AEM Forms** :
      * (Windows) Chemin TMP ou TEMP tel que défini dans les variables d’environnement
      * (AIX, Linux ou Solaris) Répertoire racine de la personne connectée
Sur les systèmes de type UNIX, une personne non connectée en tant qu’utilisateur root peut utiliser le répertoire suivant comme répertoire temporaire :
      * (Linux) /var/tmp ou /usr/tmp
      * (AIX) /tmp ou /usr/tmp
      * (Solaris) /var/tmp ou /usr/tmp
1. Donnez au nouveau compte d’utilisateur les autorisations d’écriture pour les répertoires suivants :
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

**Désactivation du servlet d’amorçage de Configuration Manager**

Configuration Manager a utilisé une servlet déployée sur votre serveur d’applications pour amorcer la base de données AEM Forms sur JEE. Étant donné que Configuration Manager accède à ce servlet avant la fin de la configuration, son accès n’a pas été sécurisé pour les personnes autorisées et il doit être désactivé après avoir correctement utilisé Configuration Manager pour configurer AEM Forms sur JEE.

1. Décompressez le fichier adobe-livecycle-[appserver].ear.
1. Ouvrez le fichier META-INF/application.xml.
1. Recherchez la section adobe-bootstrapper.war :

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
1. Placez en commentaire les modules adobe-bootstrapper.war et adobe-lcm-bootstrapper-redirectory.  war, comme suit :

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

1. Enregistrez et fermez le fichier META-INF/application.xml.
1. Compressez le fichier EAR et redéployez-le sur le serveur d’applications.
1. Démarrez le serveur AEM Forms.
1. Entrez l’URL suivante dans un navigateur pour tester la modification et garantir que l’adresse ne fonctionne plus.

   https://&lt;localhost>:&lt;port>/adobe-bootstrapper/bootstrap

**Verrouillage de l’accès distant au Trust Store**

Configuration Manager vous permet de télécharger des informations d’identification d’extensions Acrobat Reader DC dans le Trust Store d’AEM Forms sur JEE. Cela signifie que l’accès au service d’informations d’identification du Trust Store sur les protocoles distants (SOAP et EJB) a été activé par défaut. Cet accès n’est plus nécessaire après avoir téléchargé les informations d’identification des droits en utilisant Configuration Manager, ou si vous décidez d’utiliser la console d’administration ultérieurement pour gérer les informations d’identification.

Vous pouvez désactiver l’accès distant à tous les services de Trust Store en suivant les étapes de la section [Désactivation des accès distants facultatifs à des services](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr).

**Désactivation de tous les accès anonymes non indispensables**

Certains services Server Forms comportent des opérations qu’une personne anonyme peut appeler. Si l’accès anonyme à ces services n’est pas obligatoire, désactivez-le en suivant les étapes de [Désactivation des accès anonymes non indispensables à des services](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr).

#### Modifier le mot de passe d’administration par défaut {#change-the-default-administrator-password}

Lors de l’installation d’AEM Forms sur JEE, un compte d’utilisateur par défaut unique est configuré pour Super-administrateur/Administrateur à ID de connexion avec un mot de passe par défaut, *password*. Modifiez immédiatement ce mot de passe à l’aide de Configuration Manager.

1. Saisissez l’URL suivante dans un navigateur web :

   ```java
   https://[host name]:[port]/adminui
   ```

   Le numéro de port par défaut est l’un des numéros suivants :

   **JBoss :** 8080

   **WebLogic Server :** 7001

   **WebSphere :** 9080.

1. Dans le champ **Nom d’utilisateur**, saisissez `administrator` et dans le champ **Mot de passe**, saisissez `password`.
1. Cliquez sur **Paramètres** > **User Management** > **Utilisateurs et groupes**.
1. Saisissez `administrator` dans le champ **Rechercher**, puis cliquez sur **Rechercher**.
1. Cliquez sur **Super-administrateur** dans la liste des utilisateurs et utilisatrices.
1. Cliquez sur **Modifier le mot de passe** sur la page Modifier l’utilisateur.
1. Indiquez le nouveau mot de passe et cliquez sur **Enregistrer**.

En outre, il est recommandé de modifier le mot de passe par défaut de l’administrateur CRX en procédant comme suit :

1. Connectez-vous à `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` à l’aide du nom d’utilisateur/mot de passe par défaut.
1. Saisissez Administrator dans le champ de recherche, puis cliquez sur **Aller**.
1. Sélectionnez **Administrateur** dans les résultats de la recherche, puis cliquez sur l’icône **Modifier** située dans le coin inférieur droit de l’interface utilisateur.
1. Indiquez le nouveau mot de passe dans le champ **Nouveau mot de passe** et l’ancien mot de passe dans le champ **Votre mot de passe**.
1. Cliquez sur l’icône Enregistrer située dans le coin inférieur droit de l’interface utilisateur.

#### Désactiver la génération WSDL {#disable-wsdl-generation}

La génération WSDL (Web Service Definition Language) ne doit être activée que pour les environnements de développement dans lesquels les développeurs et développeuses utilisent la génération WSDL pour créer leurs applications clientes. Vous pouvez choisir de désactiver la génération WSDL dans un environnement de production pour éviter d’exposer les détails internes d’un service.

1. Saisissez l’URL suivante dans un navigateur web :

   ```java
   https://[host name]:[port]/adminui
   ```

1. Cliquez sur **Paramètres > Paramètres de Core System > Configurations**.
1. Désélectionnez **Activer WSDL**, puis sélectionnez **OK**.

### Sécurité du serveur d’applications {#application-server-security}

Le tableau suivant décrit certaines techniques qui permettent de sécuriser votre serveur d’applications une fois l’application AEM Forms sur JEE installée.

<table> 
 <thead> 
  <tr> 
   <th><p>Problème</p> </th> 
   <th><p>Description</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Console d’administration de serveur d’applications</p> </td> 
   <td><p>Après avoir installé, configuré et déployé AEM Forms sur JEE sur votre serveur d’applications, désactivez l’accès aux consoles d’administration du serveur d’applications. Pour plus de détails, reportez-vous à la documentation de votre serveur d’applications.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Paramétres des cookies pour le serveur d’applications</p> </td> 
   <td><p>Les cookies des applications sont contrôlés par le serveur d’applications. Lorsqu’elle déploie l’application, la personne chargée de l’administration du serveur d’applications peut spécifier des préférences concernant les cookies, soit à l’échelle du serveur, soit pour des applications spécifiques. Par défaut, les paramètres du serveur sont prioritaires.</p> <p>Tous les cookies de session générés par votre serveur d’applications devraient inclure l’attribut <code>HttpOnly</code>. Par exemple, si vous utilisez JBoss Application Server, vous pouvez redéfinir l’élément SessionCookie sur <code>httpOnly="true"</code> dans le fichier <code>WEB-INF/web.xml</code>.</p> <p>Vous pouvez limiter l’envoi de cookies au moyen de HTTPS uniquement. En conséquence, ils ne sont pas envoyés non codés via HTTP. Il est conseillé aux administrateurs et administratrices de serveurs d’applications d’autoriser les cookies sûrs à l’échelle du serveur. Par exemple, si vous utilisez JBoss Application Server, vous pouvez redéfinir l’élément connecteur sur <code>secure=true</code> dans le fichier <code>server.xml</code>.</p> <p>Reportez-vous à la documentation de votre serveur d’applications pour plus d’informations sur les paramètres des cookies.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Navigation des répertoires</p> </td> 
   <td><p>Lorsqu’une personne demande une page qui n’existe pas ou le nom d’un directeur (la chaîne de requête se termine par une barre oblique (/)), le serveur d’applications ne devrait pas renvoyer le contenu de ce répertoire. Pour éviter cela, vous pouvez désactiver la navigation dans les répertoires sur votre serveur d’applications. Vous devez effectuer cette opération pour l’application de console d’administratrion et pour les autres applications s’exécutant sur votre serveur.</p> <p>Pour JBoss, définissez la valeur du paramètre d’initialisation des listes de la propriété <code>DefaultServlet</code> sur <code>false</code> dans le fichier web.xml, comme illustré dans l’exemple ci-dessous :</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;par défaut&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;listes&lt;/param-name&gt;</p> <p>&lt;param-value&gt;faux&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>Pour WebSphere, définissez la propriété <code>directoryBrowsingEnabled</code> du fichier ibm-web-ext.xmi sur <code>false</code>.</p> <p>Pour WebLogic, définissez les propriétés index-directories du fichier weblogic.xml sur <code>false</code>, comme illustré dans l’exemple suivant :</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### Sécurité de la base de données {#database-security}

Lorsque vous sécurisez votre base de données, implémentez les mesures indiquées par le fournisseur de votre base de données. Attribuez à l’utilisateur de la base de données le nombre minimum d’autorisations requises sur cette base de données pour permettre l’utilisation avec AEM Forms sur JEE. Par exemple, n’utilisez pas de compte avec des privilèges d’administration de base de données.

Sur Oracle, le compte de base de données que vous utilisez nécessite uniquement les privilèges CONNECT, RESOURCE et CREATE VIEW. Pour connaître les exigences des autres bases de données, voir [Préparation à l’installation d’AEM Forms on JEE (serveur unique)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64_fr).

#### Configuration de la sécurité intégrée dans SQL Server sur Windows pour JBoss {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. Modifiez [JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml} pour ajouter `integratedSecurity=true` à l’URL de connexion, comme indiqué dans l’exemple suivant :

   ```java
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. Ajoutez le fichier sqljdbc_auth.dll au chemin d’accès du système Windows sur l’ordinateur exécutant le serveur d’applications. Le fichier sqljdbc_auth.dll se trouve avec les fichiers d’installation du pilote Microsoft SQL JDBC 6.2.1.0.
1. Modifiez la propriété du service Windows JBoss (JBoss pour AEM Forms on JEE) pour Ouvrir une session en tant que dans le Système local pour un compte utilisateur disposant d’une base de données AEM Forms et d’un ensemble minimum de droits. Si vous exécutez JBoss à partir de la ligne de commande plutôt que comme un service Windows, ignorez cette étape.
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

#### Configuration de la sécurité intégrée dans SQL Server sur Windows pour WebSphere {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

Sur WebSphere, vous pouvez configurer la sécurité intégrée uniquement lorsque vous utilisez un pilote JDBC SQL Server externe et non le pilote JDBC SQL Server intégré à WebSphere.

1. Connectez-vous à la console d’administration WebSphere.
1. Dans l’arborescence de navigation, cliquez sur **Resources** > **JDBC** > **Data Sources**, puis, dans le volet de droite, cliquez sur **IDP_DS**.
1. Dans le volet de droite, sous Additional Properties, cliquez sur **Custom Properties**, puis sur **New**.
1. Dans la case **Nom**, saisissez `integratedSecurity` et, dans la case **Valeur**, saisissez `true`.
1. Dans l’arborescence de navigation, cliquez sur **Resources** > **JDBC** > **Data Sources**, puis, dans le volet de droite, cliquez sur **RM_DS**.
1. Dans le volet de droite, sous Additional Properties, cliquez sur **Custom Properties**, puis sur **New**.
1. Dans la case **Nom**, saisissez `integratedSecurity` et, dans la case **Valeur**, saisissez `true`.
1. Sur l’ordinateur sur lequel WebSphere est installé, ajoutez le fichier sqljdbc_auth.dll au chemin du système Windows (C:\Windows). Le fichier sqljdbc_auth.dll est situé au même emplacement que le programme d’installation du pilote Microsoft SQL JDBC 1.2 (le chemin par défaut est *[InstallDir]*/sqljdbc_1.2/enu/auth/x86).
1. Sélectionnez **Démarrer** > **Panneau de configuration** > **Services**, cliquez avec le bouton droit de la souris sur le service Windows pour WebSphere (IBM WebSphere Application Server &lt;version> - &lt;node>), puis sélectionnez **Propriétés**.
1. Dans la boîte de dialogue Propriétés, cliquez sur l’onglet **Connexion**.
1. Sélectionnez **Ce compte** et indiquez les informations requises pour définir le compte de connexion à utiliser.
1. Faites passer la sécurité de SQL Server du mode **Mixte** au mode **Authentification Windows uniquement**.

### Protection de l’accès aux contenus sensibles dans la base de données {#protecting-access-to-sensitive-content-in-the-database}

Le schéma de la base de données AEM Forms contient des informations sensibles relatives à la configuration du système et aux processus métier et doit être protégé par un pare-feu. La base de données doit être considérée comme faisant partie de la même zone de confiance que Forms Server. Pour éviter tout risque de divulgation d’informations et de vol de données d’entreprise, la base de données doit être configurée par l’administrateur ou l’administratrice de base de données (DBA) pour donner l’accès aux administrateurs et administratrices autorisés uniquement.

Pour une sécurité accrue, prévoyez d’utiliser des outils spécifiques au revendeur de votre base de données pour chiffrer les colonnes des tableaux contenant les données suivantes :

* clés de document Rights Management ;
* clé de chiffrement de PIN HSM Trust Store ;
* hachages des mots de passe des utilisateurs locaux.

Pour plus d’informations des outils spécifiques à des revendeurs, voir [« Informations sur la sécurité des bases de données »](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr).

### Sécurité LDAP {#ldap-security}

En règle générale, un annuaire LDAP (Lightweight Directory Access Protocol) est utilisé par AEM Forms on JEE comme une source d’informations relatives aux utilisateurs, aux utilisatrices et aux groupes de l’entreprise et comme un moyen d’authentifier les mots de passe. Assurez-vous que votre annuaire LDAP est configuré pour utiliser le protocole SSL (Secure Socket Layer) et qu’AEM Forms on JEE est configuré pour accéder à votre annuaire LDAP en utilisant son port SSL.

#### Déni de service LDAP {#ldap-denial-of-service}

Une attaque courante utilisant LDAP consiste, pour une personne malveillante, à omettre délibérément de s’authentifier à plusieurs reprises. Ceci oblige le serveur d’annuaires LDAP à interdire à un utilisateur ou une utilisatrice l’accès à tous les services dépendant de LDAP.

Vous pouvez définir le nombre de tentatives d’authentification maximum autorisé et la durée du verrouillage appliqué par AEM Forms lorsqu’un utilisateur ou une utilisatrice échoue de manière répétée à s’authentifier auprès dAEM Forms. Dans la console d’administration, choisissez des valeurs faibles. Lors de la sélection du nombre d’échecs d’authentification maximum autorisé, il est important de comprendre que si toutes les tentatives échouent, AEM Forms verrouille l’utilisateur ou l’utilisatrice avant que le serveur d’annuaire LDAP ne le fasse.

#### Définir le verrouillage de compte automatique {#set-automatic-account-locking}

1. Connectez-vous à Administration Console.
1. Cliquez sur **Paramètres** > **User Management** > **Gestion des domaines**.
1. Sous Paramètres de verrouillage de compte automatique, définissez **Échecs d’authentification consécutifs max.** sur un nombre peu élevé, 3 par exemple.
1. Cliquez sur **Enregistrer**.

### Contrôle et journalisation {#auditing-and-logging}

L’utilisation appropriée et sécurisée des capacités de contrôle et de journalisation des applications peut contribuer au suivi et à la détection rapides des événements liés à la sécurité et autres anomalies. L’utilisation efficace des options d&#39;audit et de journalisation dans une application implique notamment le suivi des connexions ayant réussi et échoué, ainsi que des événements clés de l’application comme la création ou la suppression d’enregistrements clés.

Vous pouvez utiliser les capacités de contrôle pour détecter de nombreux types d’attaques, parmi lesquels :

* les attaques de mot de passe par force brute ;
* les attaques par déni de service ;
* les attaques par injection de données hostiles et les classes associées d’attaques par script.

Ce tableau décrit les techniques de contrôle et de journalisation que vous pouvez utiliser pour limiter les vulnérabilités du serveur.

<table> 
 <thead> 
  <tr> 
   <th><p>Problème</p> </th> 
   <th><p>Description</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Listes de contrôle d’accès de fichier journal</p> </td> 
   <td><p>Définissez les liste de contrôle d’accès (ACL) de fichier journal AEM Forms on JEE appropriées.</p> <p>Définir des informations d’identification appropriées contribue à empêcher les personnes malveillantes de supprimer les fichiers.</p> <p>Les autorisations de sécurité sur le répertoire des fichiers journaux doivent être de type « contrôle complet » pour les administrateurs, administratrices et les groupes SYSTEM. Seules les autorisations de lecture et d’écriture doivent être attribuées au compte d’utilisateur AEM Forms.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Fichiers journaux redondants</p> </td> 
   <td><p>Si les ressources le permettent, envoyez en temps réel des journaux à un autre serveur inaccessible pour la personne malveillante (en lecture seule) en utilisant Syslog, Tivoli, Microsoft Operations Manager (MOM) Server ou tout autre mécanisme équivalent.</p> <p>En protégeant les journaux de cette manière, vous réduisez le risque de falsification. Par ailleurs, le fait de stocker les journaux dans un référentiel central facilite les processus de corrélation et de surveillance (par exemple, si plusieurs serveurs de formulaires sont en cours d’utilisation et qu’une attaque par recherche de mot de passe a lieu sur plusieurs ordinateurs, un mot de passe étant demandé à chaque ordinateur).</p> </td> 
  </tr> 
 </tbody> 
</table>

### Autoriser un utilisateur ou une utilisatrice ne disposant pas de droits d’administrateur à exécuter PDF Generator

Vous pouvez permettre à un utilisateur non administrateur ou une utilisatrice non administratrice d’utiliser PDF Generator. Normalement, seuls les utilisateurs et utilisatrices disposant de droits d’administrateur peuvent utiliser PDF Generator. Effectuez les étapes suivantes pour permettre à un utilisateur non administrateur d’exécuter PDF Generator :

1. Création d’un nom de variable d’environnement PDFG_NON_ADMIN_ENABLED.

1. Définissez la valeur de la variable à TRUE.

1. Redémarrez l’instance AEM Forms.

>[!NOTE]
>
> Il est recommandé d’utiliser la commande « Ctrl + C » pour redémarrer le SDK. Le redémarrage du SDK AEM à l’aide de méthodes alternatives, par exemple l’arrêt des processus Java, peut entraîner des incohérences dans l’environnement de développement AEM.

## Configuration d’AEM Forms on JEE pour un accès au-delà de l’entreprise {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

Une fois AEM Forms sur JEE installé avec succès, il est important que vous assuriez une maintenance régulière de la sécurité de votre environnement. Cette section décrit les tâches recommandées pour assurer la maintenance de la sécurité du serveur de production AEM Forms on JEE.

### Configuration d’un proxy inverse pour l’accès Web {#setting-up-a-reverse-proxy-for-web-access}

Un *proxy inverse* peut être utilisé pour garantir qu’un jeu d’URL pour des applications AEM Forms on JEE est disponible à la fois pour des utilisateurs et utilisatrices externes et internes. Cette configuration est plus sûre que si vous autorisiez des utilisateurs à se connecter directement au serveur d’applications sur lequel est exécuté AEM Forms sur JEE. Le proxy inverse exécute toutes les requêtes HTTP pour le serveur d’applications qui exécute AEM Forms sur JEE. Les utilisateurs et utilisatrices disposent d’un accès réseau limité au seul proxy inverse et ne peuvent se connecter qu’aux URL prises en charge par le proxy inverse.

**URL racine AEM Forms on JEE pour une utilisation avec un serveur proxy inverse** 

Les URL suivantes sont les URL racine de chaque application Web AEM Forms on JEE. Configurez votre proxy inverse pour qu’il n’expose que les URL de fonctionnalités d’applications Web dont vous souhaitez autoriser l’accès aux utilisateurs finaux et utilisatrices finales.

Certaines URL sont présentées comme des applications Web accessibles par les utilisateurs finaux et utilisatrices finales. Évitez d’exposer d’autres URL Configuration Manager pour l’accès à des utilisateurs et utilisatrices externes via le proxy inverse.

<table> 
 <thead> 
  <tr> 
   <th><p>URL racine</p> </th> 
   <th><p>Objectif et/ou application Web associée</p> </th> 
   <th><p>Interface Web</p> </th> 
   <th><p>Accès utilisateurs finaux</p> </th> 
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
   <td><p>Application Web d’utilisateur final Rights Management.</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Oui</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edcws/*</p> </td> 
   <td><p>URL du service Web de Rights Management.</p> </td> 
   <td><p>Non</p> </td> 
   <td><p>Oui</p> </td> 
  </tr> 
  <tr> 
   <td><p>/pdfgui/*</p> </td> 
   <td><p>Application Web d’administration de PDF Generator.</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Oui</p> </td> 
  </tr> 
  <tr> 
   <td><p>/un espace de travail/*</p> </td> 
   <td><p>Application Web d’utilisateur final Workspace.</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Oui</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace-server/*</p> </td> 
   <td><p>Servlets et services de données Workspace requis par l’application cliente Workspace.</p> </td> 
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
   <td><p>Page d’informations pour les services web Forms Server.</p> </td> 
   <td><p>Non</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/services/*</p> </td> 
   <td><p>URL de service web pour tous les services Forms Server.</p> </td> 
   <td><p>Non</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/admin/*</p> </td> 
   <td><p>Application Web d’administration Rights Management.</p> </td> 
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
   <td><p>/TruststoreComponent/</p> <p>secured/*</p> </td> 
   <td><p>Pages d’administration de Trust Store Management</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormsIVS/*</p> </td> 
   <td><p>Application Forms IVS pour tester et déboguer le rendu de formulaire.</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputIVS/*</p> </td> 
   <td><p>Application Output IVS pour tester et déboguer le service de sortie</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rmws/*</p> </td> 
   <td><p>URL REST pour Rights Management</p> </td> 
   <td><p>Non</p> </td> 
   <td><p>Oui</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputAdmin/*</p> </td> 
   <td><p>Pages d’administration de Output</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/*</p> </td> 
   <td><p>Fichiers de l’application Web Forms</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/GetImage</p> <p>Servlet</p> </td> 
   <td><p>Utilisée pour extraire du code JavaScript lors de transformations HTML</p> </td> 
   <td><p>Non</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServerAdmin/*</p> </td> 
   <td><p>Pages d’administration de Forms</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/repository/*</p> </td> 
   <td><p>URL d’accès à WebDAV (débogage)</p> </td> 
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
   <td><p>Pages de support de Rest</p> </td> 
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
   <td><p>Téléchargement des documents à traiter lors de l’accès à des points d’entrée Remoting et SOAP WSDL et au SDK Java à l’aide du transport SOAP ou EJB avec activation des documents HTTP.</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Oui</p> </td> 
  </tr> 
 </tbody> 
</table>

## Protection contre les attaques Cross-Site Request Forgery (CSRF) {#protecting-from-cross-site-request-forgery-attacks}

Un Cross-site request forgery (CSRF) exploite la confiance d’un site web envers l’utilisateur dans le but de transmettre des instructions non autorisées à son insu. Le principe de l’attaque consiste à inclure un lien ou un script dans une page web ou une URL dans un courrier électronique afin d’accéder à un autre site sur lequel l’utilisateur a déjà été authentifié.

Par exemple, vous pouvez être connecté à la console d’administration tout en explorant un autre site web. L’une des pages Web peut inclure une balise d’image HTML avec un attribut `src` visant un script côté serveur sur le site Web de la victime. En utilisant le mécanisme d’authentification de session basé sur les cookies que fournissent les navigateurs web, le site web attaquant peut envoyer des requêtes malveillantes au script côté serveur ciblé en les faisant passer pour les requêtes de l’utilisateur ou de l&#39;utilisatrice légitime. Pour obtenir d’autres exemples, voir [https://owasp.org/www-community/attacks/csrf#Examples](https://owasp.org/www-community/attacks/csrf#Examples).

Les caractéristiques suivantes sont communes aux cas de CSRF :

* impliquent des sites qui reposent sur une identité de l’utilisateur ;
* exploitent la confiance du site dans cette identité ;
* trompent le navigateur de l’utilisateur ou de l’utilisatrice pour lui faire envoyer des requêtes HTTP à un site cible ;
* impliquent des requêtes HTTP ayant des effets secondaires.

AEM Forms on JEE utilise la fonctionnalité de filtrage des référents pour bloquer les attaques CSRF. Les termes suivants sont utilisés dans cette section pour décrire ce dispositif de filtrage des référents :

* **Référent autorisé :** un référent est l’adresse de la page source qui envoie une requête au serveur. Pour les pages ou les formulaires JSP, ce référent est généralement la page précédente dans l’historique de navigation. Les référents pour les images sont généralement les pages sur lesquelles les images sont affichées. Vous pouvez identifier les référents autorisés à accéder à votre serveur en les ajoutant à la liste de référents autorisés.
* **Exceptions aux référents autorisés :** si vous souhaitez restreindre l’accès pour un référent particulier dans votre liste de référents autorisés. Pour mettre en place cette restriction, vous pouvez ajouter des chemins d’accès individuels de ce référent vers la liste des exceptions aux référents autorisés. Les requêtes provenant de chemins d’accès de la liste des exceptions aux référents autorisés ne peuvent appeler aucune ressource du serveur Forms Server. Vous pouvez définir des exceptions aux référents autorisés pour une application spécifique et également utiliser une liste globale des exceptions s’appliquant à toutes les applications.
* **URI autorisés :** il s’agit d’une liste des ressources générées sans vérification de l’en-tête référent. Par exemple, les ressources telles que les pages d’aide, qui n’entraînent pas de changements d’état sur le serveur, peuvent être ajoutées à cette liste. Les ressources figurant dans la liste des URI autorisés ne sont jamais bloquées par le filtrage des référents, quel que soit le référent.
* **Référent de valeur NULL (null referer) :** une requête serveur qui n’est pas associée ou ne provient pas d’une page web parente est considérée comme une requête de référent de valeur NULL. Par exemple, lorsque vous ouvrez une nouvelle fenêtre de navigateur, saisissez une adresse puis appuyez sur la touche Entrée, le référent envoyé au serveur est nul. Une application de bureau (.NET ou SWING) envoyant une requête HTTP à un serveur web envoie également un référent de valeur NULL au serveur.

### Filtrage des référents {#referer-filtering}

Le processus de filtrage des référents peut être décrit comme suit :

1. Le serveur Forms Server vérifie la méthode HTTP utilisée pour l’appel :

   1. S’il s’agit d’une méthode POST, le serveur Forms Server vérifie l’en-tête du référent.
   1. S’il s’agit d’une méthode GET, le serveur Forms Server ignore la vérification du référent, à moins que la variable *CSRF_CHECK_GETS* ne soit définie sur True. Dans ce cas, il vérifie l’en-tête du référent. La variable *CSRF_CHECK_GETS* est spécifiée dans le fichier *web.xml* pour votre application.

1. Le serveur Forms Server vérifie si l’URI requis existe dans la liste autorisée :

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

Lorsque vous installez Document Services pour la première fois, la liste de référents autorisés est mise à jour avec l’adresse du serveur sur lequel Document Services est installé. Les entrées pour le serveur comprennent le nom du serveur, l’adresse IPv4, l’adresse IPv6 si le protocole IPv6 est activé, l’adresse de bouclage et une entrée localhost. Les noms ajoutés à la liste de référents autorisés sont renvoyés par le système d’exploitation hôte. Par exemple, un serveur dont l’adresse IP est 10.40.54.187 contiendra les entrées suivantes : `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`. Pour chaque nom non qualifié renvoyé par le système d’exploitation hôte (les noms sans adresse IPv4, IPv6 ou sans nom de domaine qualifié) la liste autorisée n’est pas mise à jour. Modifiez la liste de référents autorisés en fonction de votre environnement de travail. Ne déployez pas le serveur Forms Server dans l’environnement de production avec la liste de référents autorisés par défaut. Après avoir modifié l’un des référents autorisés, l’une des exceptions aux référents ou l’un des URI, assurez-vous de redémarrer le serveur pour que les modifications prennent effet.

**Gérer la liste de référents autorisés**

Vous pouvez gérer la liste de référents autorisés à partir de l’interface User Management de la console d’administration. L’interface User Management offre des fonctionnalités pour créer, éditer ou supprimer la liste. Pour plus d’informations sur l’utilisation de la liste de référents autorisés, reportez-vous à la section [Prévenir les attaques CSRF](/help/forms/using/admin-help/preventing-csrf-attacks.md) du guide *Aide à l’administration*.

**Gérer les exceptions aux référents autorisés et des listes des URI autorisés**

AEM Forms on JEE fournit des API pour gérer la liste des exceptions aux référents autorisés et la liste des URI autorisés. Vous pouvez utiliser ces API pour récupérer, créer, modifier ou supprimer la liste. Voici la liste des API disponibles :

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

Pour plus d’informations sur les API, reportez-vous à la référence API d’AEM Forms on JEE.

Utilisez la liste ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** pour les exceptions aux référents autorisés au niveau global, c’est-à-dire pour définir les exceptions qui s’appliquent à toutes les applications. Cette liste contient uniquement des URI ayant soit un chemin absolu (par exemple `/index.html`), soit un chemin relatif (par exemple `/sample/`). Vous pouvez également ajouter une expression régulière à la fin d’un URI relatif, par ex, `/sample/(.)*`.

L’ID de liste ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** est définie comme une constante dans la classe `UMConstants` de l’espace de noms `com.adobe.idp.um.api`, figurant dans `adobe-usermanager-client.jar`. Vous pouvez utiliser les API AEM Forms pour créer, modifier ou éditer cette liste. Par exemple, pour créer la liste globale des exceptions aux référents autorisés, utilisez :

```java
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

Utilisez la liste ***CSRF_ALLOWED_REFERER_EXCEPTIONS*** pour les exceptions spécifiques à une application.

**Désactiver le filtrage des référents**

Dans le cas où le filtrage des référents bloque complètement l’accès au serveur Forms Server et que vous ne pouvez pas modifier la liste des référents autorisés, vous pouvez mettre à jour le script de démarrage du serveur et désactiver le filtrage des référents.

Incluez l’argument JAVA `-Dlc.um.csrffilter.disabled=true` dans le script de démarrage et redémarrez le serveur. Assurez-vous de supprimer l’argument JAVA après avoir correctement reconfiguré la liste de référents autorisés.

**Filtrer les référents pour les fichiers WAR personnalisés**

Vous avez peut-être créé des fichiers WAR personnalisés afin de travailler avec AEM Forms on JEE pour répondre aux besoins de votre entreprise. Pour activer le filtrage des référents pour vos fichiers WAR personnalisés, vous devez inclure ***adobe-usermanager-client.jar*** dans le chemin de classe pour les fichiers WAR et inclure une entrée de filtre dans le fichier « web.xml » avec les paramètres suivants :

**CSRF_CHECK_GETS** contrôle la vérification du référent pour les requêtes GET. Si ce paramètre n’est pas défini, la valeur par défaut est définie sur false. Incluez ce paramètre uniquement si vous souhaitez filtrer vos requêtes GET.

**CSRF_ALLOWED_REFERER_EXCEPTIONS** est l’identifiant de la liste des exceptions aux référents autorisés. Le filtrage des référents empêche les requêtes provenant de référents de la liste identifiée par l’identifiant de la liste d’appeler toute ressource du serveur Forms Server.

**CSRF_ALLOWED_URIS_LIST_NAME** est l’ID de la liste des URI autorisés. Le filtrage des référents ne bloque pas les requêtes concernant les ressources de la liste identifiées par l’ID de liste, quelle que soit la valeur de l’en-tête référent dans la requête.

**CSRF_ALLOW_NULL_REFERER** contrôle le comportement du filtrage des référents lorsque le référent est null ou non présent. Si ce paramètre n’est pas défini, la valeur par défaut est définie sur false. Incluez ce paramètre uniquement si vous souhaitez autoriser les référents ayant pour valeur NULL. L’autorisation des référents ayant pour valeur NULL peut permettre certains types d’attaques CSRF (Cross Site Request Forgery).

**CSRF_NULL_REFERER_EXCEPTIONS** est une liste des URI pour lesquels une vérification référent n’est pas exécutée lorsque la valeur du référent est null. Ce paramètre est activé uniquement lorsque la variable *CSRF_ALLOW_NULL_REFERER* est définie sur false. Séparez plusieurs URI dans la liste par une virgule.

Voici un exemple de l’entrée de filtre dans le fichier *web.xml* pour un ***EXEMPLE*** de fichier WAR :

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

Si des requêtes serveur légitimes sont bloquées par le filtre CSRF, essayez l’une des méthodes suivantes :

* Si la requête rejetée a un en-tête référent, il peut être intéressant de l’ajouter à liste des référents autorisés. Ajoutez uniquement les référents auxquels vous faites confiance.
* Si la requête rejetée ne dispose pas d’un en-tête référent, modifiez votre application client pour inclure un en-tête référent.
* Si le client ou la cliente peut travailler dans un navigateur, essayez ce modèle de déploiement.
* En dernier recours, vous pouvez ajouter la ressource à la liste des URI autorisés. Ce paramètre n’est pas recommandé.

## Configuration réseau sécurisée {#secure-network-configuration}

Cette section décrit les protocoles et les ports requis par AEM Forms on JEE et fournit des recommandations pour déployer AEM Forms on JEE dans une configuration réseau sécurisée.

### Protocoles réseau utilisés par AEM Forms on JEE {#network-protocols-used-by-aem-forms-on-jee}

Lorsque vous configurez une architecture réseau sécurisée comme décrit dans la section précédente, les protocoles réseau suivants sont requis pour l’interaction entre AEM Forms on JEE et d’autres systèmes dans le réseau de votre entreprise.

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
     <li><p>Le navigateur affiche Configuration Manager et des applications web d’utilisateur ou utilisatrice final(e).</p> </li> 
     <li><p>Toutes les connexions SOAP.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Applications clientes de services web telles que les applications .NET.</p> </li> 
     <li><p>Adobe Reader® utilise SOAP pour les services web du serveur AEM Forms on JEE.</p> </li> 
     <li><p>Les applications Adobe Flash® utilisent SOAP pour les services web Forms Server.</p> </li> 
     <li><p>Appels SDK AEM Forms on JEE en mode SOAP.</p> </li> 
     <li><p>Environnement de conception de Workbench.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>Appels SDK AEM Forms on JEE en mode Enterprise JavaBeans (EJB)</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP/POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>Entrée par e-mail dans un service (point d’entrée d’e-mail)</p> </li> 
     <li><p>Notifications de tâches utilisateur par e-mail</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>UNC File IO</p> </td> 
   <td><p>Surveillance AEM Forms on JEE des dossiers de contrôle pour l’entrée dans un service (point d’entrée de dossier de contrôle)</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Synchronisations des informations sur les utilisateurs, utilisatrices, et les groupes de l’organisation dans un répertoire</p> </li> 
     <li><p>Authentification LDAP pour les utilisateurs interactifs et utilisatrices interactives</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>Appels de requête et de procédure à une base de données externe lors de l’exécution d’un processus utilisant le service JDBC</p> </li> 
     <li><p>Référentiel AEM Forms on JEE d’accès interne</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>Permet la navigation à distance dans le référentiel de conception AEM Forms on JEE (formulaires, fragments, etc.) par tout client ou toute cliente WebDAV.</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>Applications Adobe Flash, dans lesquelles les services de serveur AEM Forms sur JEE sont configurés avec un point d’entrée Remoting.</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>AEM Forms sur JEE expose les MBeans pour le contrôle avec JMX.</p> </td> 
  </tr> 
 </tbody> 
</table>

### Ports de serveur d’applications {#ports-for-application-servers}

Cette section décrit les ports par défaut (et les plages de configurations alternatives) pour chaque type de serveur d’applications pris en charge. Ces ports doivent être activés ou désactivés sur le pare-feu interne, selon la fonctionnalité réseau que vous souhaitez autoriser aux clients et clientes qui se connectent au serveur d’applications qui exécute AEM Forms sur JEE.

>[!NOTE]
>
>Par défaut, le serveur expose plusieurs MBeans JMX sous l’espace de noms adobe.com. Seules les informations utiles à la surveillance de la santé du serveur sont exposées. Toutefois, pour éviter toute divulgation d’informations, interdisez aux appelants et appelantes dans un réseau non approuvé de rechercher les MBean JMX et d’accéder aux mesures de santé.

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
   <td><p>Accès aux applications Web</p> </td> 
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
   <td><p>Accès aux applications Web</p> </td> 
   <td> 
    <ul> 
     <li><p>Port d’écoute par défaut d’Admin Server : 7001</p> </li> 
     <li><p>Port d’écoute SSL par défaut d’Admin Server : 7002</p> </li> 
     <li><p>Port configuré pour Managed Server, par exemple 8001</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>Ports d’administration WebLogic non requis pour l’accès à AEM Forms sur JEE</p> </td> 
   <td> 
    <ul> 
     <li><p>Port d’écoute de Managed Server : configurable de 1 à 65534</p> </li> 
     <li><p>Port d’écoute SSL de Managed Server : configurable de 1 à 65534</p> </li> 
     <li><p>Port d’écoute de Node Manager : 5556 par défaut</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**Ports WebSphere **

Pour plus d’informations sur les ports WebSphere requis par AEM Forms sur JEE, consultez Configuration des numéros de ports dans l’interface utilisateur de WebSphere Application Server.

### Configuration de SSL {#configuring-ssl}

En vous référant à l’architecture physique décrite dans la section [Architecture physique d’AEM Forms on JEE](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture), configurez SSL pour toutes les connexions que vous prévoyez d’utiliser. Spécifiquement, toutes les connexions SOAP doivent être établies via SSL pour empêcher que les informations d’identification des utilisateurs et des utilisatrices soient exposées sur un réseau.

Pour obtenir des instructions sur la manière de configurer SSL sur JBoss, WebLogic et WebSphere, consultez « Configuration de SSL » dans l’[aide d’administration](https://www.adobe.com/go/learn_aemforms_admin_64_fr).

Pour plus d’informations sur l’importation de certificats dans JVM (Java Virtual Machine) configuré pour un serveur AEM Forms, consultez la section Authentification mutuelle dans l’[Aide d’AEM Forms Workbench](https://www.adobe.com/go/learn_aemforms_workbench_65_fr).

### Configuration de la redirection SSL {#configuring-ssl-redirect}

Après avoir configuré votre serveur d’applications pour qu’il prenne en charge SSL, vous devez vous assurer que l’ensemble du trafic HTTP vers les applications et les services utilise le port SSL.

Pour configurer la redirection SSL pour WebSphere et WebLogic, reportez-vous à la documentation de votre serveur d’applications.

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

### Comptes de service JBoss {#jboss-service-accounts}

L’installation clé en main d’AEM Forms sur JEE installe un compte de service par défaut en utilisant le compte système local. Le compte d’utilisateur système local intégré présente un haut niveau d’accessibilité ; il fait partie du groupe Administrateurs. Si une identité de processus de travail est exécutée en tant que compte d’utilisateur système local, ce processus de travail dispose d’un accès complet à l’ensemble du système.

#### Exécution du serveur d’applications à l’aide d’un compte non administratif spécifique {#run-the-application-server-using-a-non-administrative-account}

1. Dans Microsoft Management Console (MMC), créez un utilisateur local ou une utilisatrice locale que le service Forms Server peut utiliser pour se connecter :

   * Sélectionnez **L’utilisateur ne peut pas changer de mot de passe**.
   * Vérifiez que le groupe Utilisateurs figure dans l’onglet **Membre de**.

1. Sélectionnez **Paramètres** > **Outils d’administration** > **Services**.
1. Cliquez deux fois sur le service de serveur d’applications et arrêtez ce service.
1. Sur l’onglet **Connexion**, sélectionnez **Ce compte**, recherchez le compte d’utilisateur que vous avez créé et saisissez le mot de passe du compte.
1. Dans la fenêtre Paramètres de sécurité locaux, dans Attribution des droits utilisateur, attribuez les droits suivants au compte d’utilisateur avec lequel est exécuté le serveur Forms Server :

   * Interdire l’ouverture de session par les services Terminal
   * Interdire l’ouverture d’une session locale
   * Ouvrir une session en tant que service (ce droit doit être déjà défini)

1. Donnez au nouveau compte d’utilisateur les autorisations de modification sur les répertoires suivants :
   * **Répertoire de stockage global de documents** : l’emplacement du répertoire de stockage global de documents est configuré manuellement pendant le processus d’installation d’AEM Forms. Si le paramètre d’emplacement du stockage global de documents n’est pas défini pendant l’installation, l’emplacement par défaut utilisé est un sous-répertoire de l’emplacement d’installation du serveur d’applications : `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **Répertoire CRX-Repository** : l’emplacement par défaut est `[AEM-Forms-installation-location]\crx-repository`
   * **Répertoires temporaires AEM Forms** :
      * (Windows) Chemin TMP ou TEMP tel que défini dans les variables d’environnement
      * (AIX, Linux ou Solaris) Répertoire racine de la personne connectée
Sur les systèmes de type UNIX, une personne non connectée en tant qu’utilisateur root peut utiliser le répertoire suivant comme répertoire temporaire :
      * (Linux) /var/tmp ou /usr/tmp
      * (AIX) /tmp ou /usr/tmp
      * (Solaris) /var/tmp ou /usr/tmp
1. Donnez au nouveau compte d’utilisateur les autorisations d’écriture pour les répertoires suivants :
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   >L’emplacement de l’installation par défaut de JBoss Application Server :
   >
   >* Windows : C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   >* Linux : /opt/jboss/.

1. Démarrez le service de serveur d’applications.

### Sécurité du système de fichiers {#file-system-security}

AEM Forms sur JEE utilise le système de fichiers comme suit :

* stocke les fichiers temporaires utilisés lors du traitement des entrées et sorties de documents ;
* stocke dans une banque d’archivage globale les fichiers utilisés pour prendre en charge les composants de la solution qui sont installés ;
* les dossiers de contrôle stockent les fichiers utilisés en entrée dans un service à partir d’un emplacement de dossier du système de fichiers.

Lorsque vous utilisez des dossiers de contrôle comme moyen d’envoi et de réception de documents avec un service Forms Server, soyez très prudent quant à la sécurité du système de fichiers. Lorsqu’un utilisateur ou une utilisatrice dépose des contenus dans le dossier de contrôle, ces contenus sont exposés via le dossier de contrôle. Dès lors, le service n’authentifie pas l’utilisateur final réel ou l’utilisatrice finale réelle. Au lieu de cela, il considère que la sécurité par liste de contrôle d’accès et par niveau de dossier a été définie au niveau des dossiers pour déterminer qui peut effectivement appeler le service.

## Recommandations de sécurité spécifiques à JBoss {#jboss-specific-security-recommendations}

La présente section propose des recommandations relatives à la configuration du serveur d’applications qui sont spécifiques à JBoss 7.0.6. lorsque celui-ci est utilisé pour exécuter AEM Forms sur JEE.

### Désactiver la console de gestion JBoss et la console JMX {#disable-jboss-management-console-and-jmx-console}

L’accès à la console de gestion JBoss et à la console JMX est déjà configuré (la surveillance JMX est désactivée) lorsque vous installez AEM Forms sur JEE sur Jboss en appliquant la méthode d’installation clé en main. Si vous utilisez votre propre serveur d’applications JBoss, assurez-vous que l’accès à la console de gestion JBoss et à la console de surveillance JMX est sécurisé. L’accès à la console de surveillance JMX est défini dans le fichier de configuration de JBoss appelé jmx-invoker-service.xml.

### Désactiver l’exploration des répertoires {#disable-directory-browsing}

Après vous être identifié dans la console d’administration, il vous est possible de parcourir la liste des répertoires de la console en modifiant l’URL. Par exemple, si vous modifiez l’URL pour l’une de ces adresses, une liste de répertoires s’affiche :

```java
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## Recommandations de sécurité spécifiques à WebLogic {#weblogic-specific-security-recommendations}

Cette section présente des recommandations relatives à la configuration du serveur d’applications et spécifiques à WebLogic 9.1 lorsque celui-ci est utilisé pour exécuter AEM Forms sur JEE.

### Désactiver l’exploration des répertoires {#disable_directory_browsing-1}

Définissez les propriétés index-directories du fichier weblogic.xml sur `false`, comme illustré dans l’exemple suivant :

```xml
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### Activer le port SSL de WebLogic {#enable-weblogic-ssl-port}

Par défaut, WebLogic n’active pas le port d’écoute SSL par défaut, 7002. Activez ce port dans la console d’administration du serveur WebLogic avant de configurer SSL.

## Recommandations de sécurité spécifiques à WebSphere {#websphere-specific-security-recommendations}

Cette section contient des recommandations relatives à la configuration du serveur d’applications et destinées à sécuriser WebSphere lors de l’exécution d’AEM Forms on JEE.

### Désactiver l’exploration des répertoires {#disable_directory_browsing-2}

Définissez la propriété `directoryBrowsingEnabled` du fichier ibm-web-ext.xml sur `false`.

### Activer la sécurité administrative de WebSphere {#enable-websphere-administrative-security}

1. Connectez-vous à la console d’administration WebSphere.
1. Dans l’arborescence de navigation, accédez à **Sécurité** > **Sécurité globale**
1. Sélectionnez **Activation de la sécurité administrative**.
1. Désélectionnez les options **Activation de la sécurité des applications** et **Utilisation de la sécurité Java 2**.
1. Cliquez sur **OK** ou sur **Appliquer**.
1. Dans la zone des **Messages**, cliquez sur **Enregistrer directement dans la configuration principale**.
