---
title: Sécurisation de votre environnement d’AEM Forms sur JEE
seo-title: Sécurisation de votre environnement d’AEM Forms sur JEE
description: Découvrez divers paramètres de renforcement de la sécurité afin d’améliorer la sécurité des AEM Forms sur JEE s’exécutant sur un intranet d’entreprise.
seo-description: Découvrez divers paramètres de renforcement de la sécurité afin d’améliorer la sécurité des AEM Forms sur JEE s’exécutant sur un intranet d’entreprise.
uuid: f6c63690-6376-4fe1-9df2-a14fbfd62aff
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 6b380e92-f90d-4875-b7a2-f3958daf2364
translation-type: tm+mt
source-git-commit: f9b11eee4c044a8df4e694aa5f660b5ea375ca3c
workflow-type: tm+mt
source-wordcount: '7665'
ht-degree: 71%

---


# Renforcement de l’Environnement de vos AEM Forms sur JEE {#hardening-your-aem-forms-on-jee-environment}

Découvrez divers paramètres de renforcement de la sécurité afin d’améliorer la sécurité des AEM Forms sur JEE s’exécutant sur un intranet d’entreprise.

L’article fournit des conseils et des pratiques recommandées de sécurisation des serveurs exécutant AEM Forms sur JEE. Il ne vise pas à expliquer de manière exhaustive comment renforcer des hôtes pour votre système d’exploitation et vos serveurs d’applications. Cet article décrit plutôt divers paramètres de renforcement de la sécurité que vous devez implémenter pour améliorer la sécurité de AEM Forms sur JEE qui s’exécute dans un intranet d’entreprise. Toutefois, pour que les serveurs d’applications AEM Forms sur JEE restent sécurisés, vous devez également mettre en œuvre des procédures de surveillance, de détection et de réponse de sécurité.

Cet article décrit des techniques de renforcement à appliquer au cours des étapes suivantes, lors du cycle de vie de l’installation et de la configuration :

* **Préinstallation :** Utilisez ces techniques avant d’installer AEM Forms sur JEE.
* **Installation :** Utilisez ces techniques pendant le processus d’installation de AEM Forms on JEE.
* **Post-installation :** Utilisez ces techniques après l’installation, puis régulièrement par la suite.

AEM Forms sur JEE est hautement personnalisable et compatible avec de nombreux environnements. Il est possible que certains des conseils présentés ici ne soient pas directement applicables à votre entreprise.

## Préinstallation {#preinstallation}

Avant d’installer AEM Forms sur JEE, vous pouvez appliquer des solutions de sécurité à la couche réseau et au système d’exploitation. Cette section décrit certains problèmes et propose des conseils pour réduire les vulnérabilités de la sécurité correspondantes.

**Installation et configuration sous UNIX et Linux**

Évitez d’installer ou de configurer AEM Forms sur JEE en utilisant un shell racine. Par défaut, les fichiers sont installés sous le répertoire /opt et l’utilisateur qui effectue l’installation a besoin de disposer de toutes les autorisations de fichier sous /opt. De même, cet utilisateur peut parfaitement exécuter une installation sous un répertoire /user dans lequel il dispose de toutes les autorisations de fichier.

**Installation et configuration sous Windows**

Sous Windows, il est préférable d’effectuer l’installation en tant qu’administrateur si vous installez AEM Forms sur JEE sur JBoss en utilisant la procédure d’installation clé en main ou si vous installez PDF Generator. Par ailleurs, lorsque vous installez PDF Generator sous Windows avec prise en charge des applications natives, vous devez exécuter l’installation sous la même identité que l’utilisateur Windows ayant installé Microsoft Office. Pour plus d’informations sur les privilèges d’installation, voir le document* Installation et déploiement de AEM Forms sur JEE* correspondant à votre serveur d’applications.

### Sécurité de la couche réseau {#network-layer-security}

Les vulnérabilités de sécurité réseau comptent parmi les premières menaces qui affectent les serveurs d’applications accessibles par Internet ou par un intranet. Cette section décrit le processus de renforcement des hôtes du réseau contre ces vulnérabilités. Elle traite de la segmentation du réseau, du renforcement de la pile TCP/IP (Transmission Control Protocol/Internet Protocol) et de l’utilisation de pare-feu pour protéger les hôtes.

Le tableau suivant décrit des processus classiques qui permettent de réduire les vulnérabilités de la sécurité réseau :

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
   <td><p>Déployez des serveurs de formulaires dans une zone démilitarisée. Une segmentation doit avoir été définie dans au moins deux niveaux avec le serveur d’applications utilisé pour exécuter AEM Forms sur JEE placé derrière le pare-feu interne. Séparez le réseau externe de la zone démilitarisée qui contient les serveurs Web, lesquels doivent par ailleurs être séparés du réseau interne. Utilisez des pare-feu pour implémenter les couches de séparation. Classez et contrôlez le trafic passant par chaque couche réseau pour vous assurer que le minimum absolu de données requises est autorisé.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Adresses IP privées</p> </td> 
   <td><p>Utilisez la traduction d’adresses réseau (NAT) avec les adresses IP privées RFC 1918 sur le serveur d’applications AEM Forms. Attribuez des adresses IP privées (10.0.0.0/8, 172.16.0.0/12 et 192.168.0.0/16) pour rendre plus difficile pour un attaquant d'acheminer le trafic vers et depuis un hôte interne de NAT par Internet.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Pare-feu</p> </td> 
   <td><p>Utilisez les critères suivants pour choisir une solution de pare-feu :</p> 
    <ul> 
     <li><p>Implémentez des pare-feu qui prennent en charge les serveurs proxy et/ou la <em>vérification avec état</em> plutôt que de simples solutions de filtrage des paquets.</p> </li> 
     <li><p>Use a firewall that supports a <em>deny all services except those explicitly permitted</em> security paradigms.</p> </li> 
     <li><p>Implémentez une solution de pare-feu à double hébergement ou à hébergement multiple. Cette architecture propose le meilleur niveau de sécurité et contribue à empêcher les utilisateurs non autorisés de contourner le pare-feu.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>Ports de base de données</p> </td> 
   <td><p>N’utilisez pas les ports d’écoute par défaut pour les bases de données (MySQL - 3306, Oracle - 1521, MS SQL - 1433). Pour plus de détails sur la redéfinition des ports de base de données, reportez-vous à la documentation de votre base de données.</p> <p>L’utilisation d’un port de base de données différent affecte la configuration globale d’AEM Forms sur JEE. Si vous redéfinissez les ports par défaut, vous devez modifier en conséquence la configuration et, notamment, les sources de données d’AEM Forms sur JEE.</p> <p>For information about configuring data sources in AEM Forms on JEE, see Install and Upgrade AEM Forms on JEE or Upgrading to AEM Forms on JEE for your application server at <a href="/help/forms/using/introduction-aem-forms.md" target="_blank">AEM Forms user guide</a>.</p> </td> 
  </tr> 
 </tbody> 
</table>

### Sécurité du système d’exploitation {#operating-system-security}

Le tableau suivant décrit plusieurs approches utilisables pour réduire au minimum les vulnérabilités de sécurité du système d’exploitation :

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
   <td><p>Le risque de voir un utilisateur non autorisé accéder au serveur d’applications sera d’autant plus important que les correctifs de sécurité et les mises à niveau du revendeur n’auront pas été appliqués en temps utile. Testez les correctifs de sécurité avant de les appliquer sur les serveurs de production.</p><p>De même, créez des règles et des procédures pour contrôler et installer régulièrement les correctifs.</p></td> 
  </tr> 
  <tr> 
   <td><p>Logiciels de protection antivirus</p></td> 
   <td><p>Les programmes antivirus identifient les fichiers infectés en recherchant des signatures ou en repérant les comportements inhabituels. Ces programmes conservent la signature des virus dans un fichier, qui est généralement stocké sur le disque dur local. De nouveaux virus étant découverts régulièrement, mettez fréquemment à jour ce fichier pour permettre au programme antivirus d’identifier tous les virus actuels.</p></td> 
  </tr> 
  <tr> 
   <td><p>NTP (Network Time Protocol)</p></td> 
   <td><p>Pour les analyses légales, veillez à ce que l’heure des serveurs de fomulaires soit toujours exacte. Utilisez le protocole NTP pour synchroniser l’heure sur tous les systèmes connectés directement à Internet.</p></td> 
  </tr> 
 </tbody> 
</table>

For additional security information for your operating system, see [“Operating system security information”](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information).

## Installation {#installation}

Cette section décrit des techniques que vous pouvez utiliser pendant le processus d’installation d’AEM Forms pour réduire les vulnérabilités de sécurité. Dans certains cas, ces techniques utilisent des options qui font partie du processus d’installation. Le tableau suivant décrit ces techniques :

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
   <td><p>Utilisez le moins de privilèges nécessaires pour installer le logiciel. Connectez-vous à l’ordinateur via un compte qui n’appartient pas au groupe Administrateurs. Sous Windows, vous pouvez utiliser la commande Exécuter pour exécuter le programme d’installation d’AEM Forms sur JEE en tant qu’utilisateur non administrateur. Sous UNIX et Linux, utilisez une commande comme <code>sudo</code> pour installer le logiciel.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Source du logiciel</p> </td> 
   <td><p>Ne téléchargez et n’exécutez pas AEM Forms sur JEE depuis des sources non approuvées.</p> <p>Des programmes malveillants peuvent contenir des codes conçus pour violer la sécurité de multiples façons, par exemple par vol, par modification et suppression de données, ou par déni de service. Installez AEM Forms sur JEE à partir du DVD Adobe ou depuis une source approuvée uniquement.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Partitions de disques</p> </td> 
   <td><p>Placez AEM Forms sur JEE sur une partition de disque dédiée. La segmentation de disque est un processus qui permet de conserver des données spécifiques sur des disques physiques séparés de votre serveur, pour une sécurité accrue. Le fait d’organiser les données ainsi permet de réduire le risque d’attaques par traversée d’annuaires. Prévoyez de créer une partition distincte de la partition système, dans laquelle vous pouvez installer le répertoire de contenu AEM Forms sur JEE. (sous Windows, la partition système contient le répertoire system32, ou partition racine).</p> </td> 
  </tr> 
  <tr> 
   <td><p>Composants</p> </td> 
   <td><p>Evaluez les services existants et désactivez ou désinstallez tout service inutile. N’installez pas de composants ou de services dont vous n’avez pas besoin.</p> <p>L’installation par défaut d’un serveur d’applications peut inclure des services dont vous n’avez aucune utilité. Par conséquent, désactivez tous les services inutiles avant de procéder au déploiement, pour réduire ainsi au minimum les possibilités de points d’entrée d’une attaque. Par exemple, sur JBoss, vous pouvez placer en commentaire les services inutiles dans le fichier descripteur META-INF/jboss-service.xml.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Fichier de stratégie interdomaines</p> </td> 
   <td><p>La présence d’un fichier <code>crossdomain.xml</code> sur le serveur peut immédiatement affaiblir ce serveur. Il est recommandé de rendre la liste des domaines aussi restrictive que possible. Ne placez pas en production le fichier <code>crossdomain.xml</code> utilisé pendant la phase de développement lors de l’utilisation des guides <em>(obsolète)</em>. Dans le cas d’un guide qui utilise les services Web, si le service figure sur le même serveur ayant servi le guide, aucun fichier <code>crossdomain.xml</code> n’est nécessaire. En revanche, si le service figure sur un autre serveur ou si des grappes sont impliquées, la présence d’un fichier <code>crossdomain.xml</code> est nécessaire. Refer to <a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a>, for more information on the crossdomain.xml file.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Paramètres de sécurité du système d’exploitation</p> </td> 
   <td><p>If you need to use 192-bit or 256-bit XML encryption on Solaris platforms, ensure that you install <code>pkcs11_softtoken_extra.so</code> instead of <code>pkcs11_softtoken.so</code>.</p> </td> 
  </tr> 
 </tbody> 
</table>

## Etapes de post-installation {#post-installation-steps}

Une fois AEM Forms sur JEE installé avec succès, il est important que vous assuriez une maintenance régulière de l’environnement pour en optimiser la sécurité.

La section suivante décrit en détail les différentes tâches recommandées pour sécuriser le serveur de formulaires déployé.

### Sécurité d’AEM Forms {#aem-forms-security}

Les paramètres recommandés suivants s’appliquent au serveur AEM Forms sur JEE hors de l’application Web administrative. Pour réduire les risques de sécurité du serveur, appliquez ces paramètres immédiatement après avoir installé AEM Forms sur JEE.

**Correctifs de sécurité**

Le risque de voir un utilisateur non autorisé accéder au serveur d’applications sera d’autant plus important que les correctifs de sécurité et les mises à niveau du revendeur n’auront pas été appliqués en temps utile. Testez les correctifs de sécurité avant de les appliquer aux serveurs de production pour vous assurer de la compatibilité et de la disponibilité des applications De même, créez des règles et des procédures pour contrôler et installer régulièrement les correctifs. Les mises à jour d’AEM Forms sur JEE se trouvent sur le site de téléchargement des produits Enterprise.

**Comptes de service (JBoss clé en main sur Windows uniquement)**

AEM Forms sur JEE installe un service par défaut en utilisant le compte système local. Le compte utilisateur système local intégré présente un haut niveau d’accessibilité ; il fait partie du groupe Administrateurs. Si une identité de processus de travail est exécutée en tant que compte utilisateur système local, ce processus de travail dispose d’un accès complet à l’ensemble du système.

Pour exécuter le serveur d’applications sur lequel est déployé AEM Forms sur JEE, appliquez les instructions suivantes en utilisant un compte non administratif spécifique :

1. Dans Microsoft Management Console (MMC), créez un utilisateur local pour que le service de serveur de formulaires se connecte en tant que cet utilisateur local :

   * Sélectionnez **L’utilisateur ne peut pas changer de mot de passe**.
   * Vérifiez que le groupe **Utilisateurs** figure dans l’onglet **Membre de**.

   >[!NOTE]
   >
   >vous ne pouvez pas modifier ce paramètre pour PDF Generator.

1. Sélectionnez **Démarrer** > **Paramètres** > **Outils d’administration** > **Services**.
1. Cliquez deux fois sur l’application JBoss pour AEM Forms sur JEE et arrêtez le service.
1. Sur l’onglet **Ouvrir une session**, sélectionnez **Ce compte**, recherchez le compte utilisateur que vous avez créé, puis entrez le mot de passe pour ce compte.
1. Dans MMC, ouvrez **Paramètres de sécurité locaux** et sélectionnez **Stratégies locales** > **Attribution de droits utilisateur**.
1. Attribuez les droits suivants au compte utilisateur sous lequel le serveur de formulaires est exécuté :

   * Interdire l’ouverture de session par les services Terminal
   * Interdire l’ouverture d’une session locale
   * Ouvrir une session en tant que service (ce droit doit être déjà défini)

1. Attribuez au nouveau compte d’utilisateur les autorisations de modification sur les répertoires suivants :
   * **Répertoire** d’Enregistrement de Document global (GDS) : L’emplacement du répertoire de stockage global de documents est configuré manuellement pendant le processus d’installation AEM Forms. If the location setting remains empty during installation, the location defaults to a directory under the application server installation at `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **Répertoire** CRX-Repository : L’emplacement par défaut est `[AEM-Forms-installation-location]\crx-repository`
   * **Répertoires** temporaires AEM Forms :
      * (Windows) Chemin TMP ou TEMP tel que défini dans les variables d’environnement
      * (AIX, Linux, ou Solaris) Répertoire racine de l’utilisateur connecté
Sur les systèmes de type UNIX, un utilisateur non connecté comme utilisateur root peut utiliser le répertoire suivant comme répertoire temporaire :
      * (Linux) /var/tmp ou /usr/tmp
      * (AIX) /tmp ou /usr/tmp
      * (Solaris) /var/tmp ou /usr/tmp
1. Attribuez au nouveau compte d’utilisateur des autorisations d’écriture sur les répertoires suivants :
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   > Emplacement d’installation par défaut de JBoss Application Server :
   > * Windows : C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux : /opt/jboss/

1. Démarrez le serveur d’applications.

**Désactivation de la servlet d’amorçage de Configuration Manager**

Configuration Manager a utilisé une servlet déployée sur votre serveur d’applications pour amorcer la base de données AEM Forms sur JEE. Configuration Manager accédant à cette servlet avant la fin de la configuration, son accès n’a pas été sécurisé pour les utilisateurs autorisés et il convient de le désactiver après avoir utilisé Configuration Manager pour configurer AEM Forms sur JEE.

1. Unzip the adobe-livecycle-[appserver].ear file.
1. Ouvrez le fichier META-INF/application.xml.
1. Recherchez la section adobe-bootstrapper.war :

   ```as3
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
1. Placez en commentaire les modules adobe-bootstrapper.war et adobe-lcm-bootstrapper-redirectory. war, comme suit :

   ```as3
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
1. Entrez l’URL ci-dessous dans un navigateur pour tester la modification et vous assurer qu’elle ne fonctionne plus.

   https://&lt;hôte_local>:&lt;port>/adobe-bootstrapper/bootstrap

**Verrouillage de l’accès distant à Trust Store**

Configuration Manager vous permet de télécharger des informations d’identification Acrobat Reader DC extensions dans le Trust Store AEM Forms sur JEE. Ceci signifie que l’accès au service d’informations d’identification Trust Store sur les protocoles distants (SOAP et EJB) a été activé par défaut. Cet accès n’est plus nécessaire après avoir téléchargé les informations d’identification des droits à l’aide de Configuration Manager ou si vous décidez d’utiliser Administration Console ultérieurement pour gérer les informations d’identification.

Vous pouvez désactiver l’accès distant à tous les services Trust Store en procédant comme indiqué dans la section [Désactivation des accès distants non indispensables à des services](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services).

**Désactivation de tous les accès anonymes non indispensables**

Certains services du serveur de formulaires comportent des opérations qu’un appelant anonyme peut appeler. Si l’accès anonyme à ces services n’est pas obligatoire, désactivez-le en suivant les étapes de [Désactivation des accès anonymes non indispensables à des services](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services).

#### Modification du mot de passe par défaut du compte administrateur {#change-the-default-administrator-password}

Lorsqu’AEM Forms sur JEE est installé, un compte utilisateur par défaut unique est configuré pour l’utilisateur Super administrateur/Administrateur à ID de connexion avec un mot de passe par défaut, *password*. Modifiez immédiatement ce mot de passe à l’aide de Configuration Manager.

1. Saisissez l’URL suivante dans un navigateur Web :

   ```as3
   https://[host name]:[port]/adminui
   ```

   Le numéro de port par défaut est l’un des numéros suivants :

   **JBoss :** 8080

   **WebLogic Server :** 7001

   **WebSphere :** 9080.

1. Dans le champ **Nom d’utilisateur**, saisissez `administrator` et dans le champ **Mot de passe**, saisissez `password`.
1. Cliquez sur **Paramètres** >**User Management** > **Utilisateurs et groupes**.
1. Saisissez `administrator` dans le champ **Rechercher**, puis cliquez sur **Rechercher**.
1. Cliquez sur **Super Administrateur** dans la liste des utilisateurs.
1. Cliquez sur **Changer de mot de passe** dans la page Modifier l’utilisateur.
1. Indiquez le nouveau mot de passe et cliquez sur **Enregistrer**.

En outre, il est recommandé de modifier le mot de passe par défaut de l’administrateur CRX en procédant comme suit :

1. Connectez-vous à `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` l’aide du nom d’utilisateur/mot de passe par défaut.
1. Saisissez Administrator dans le champ de recherche, puis cliquez sur **Aller**.
1. Select **Administrator** from the search result and click the **Edit** icon at the lower right of the user interface.
1. Indiquez le nouveau mot de passe dans le champ **Nouveau mot de passe** et l’ancien mot de passe dans le champ **Votre mot de passe**.
1. Cliquez sur l’icône Enregistrer dans l’angle inférieur droit de l’interface utilisateur.

#### Désactivation de la génération WSDL {#disable-wsdl-generation}

La génération Web Service Definition Language (WSDL) doit être activée uniquement pour les environnements de développement dans lesquels les développeurs font appel à la génération WSDL pour créer leurs applications clientes. Vous pouvez choisir de désactiver la génération WSDL dans un environnement de production pour éviter d’exposer les détails internes d’un service.

1. Saisissez l’URL suivante dans un navigateur Web :

   ```as3
   https://[host name]:[port]/adminui
   ```

1. Cliquez sur **Paramètres > Paramètres de Core System > Configurations de base**.
1. Deselect **Enable WSDL** and click **OK**.

### Sécurité du serveur d’applications {#application-server-security}

Le tableau suivant décrit certaines techniques qui permettent de sécuriser votre serveur d’applications une fois l’application AEM Forms sur JEE installée.

<table> 
 <thead> 
  <tr> 
   <th><p>Problème</p> </th> 
   <th><p>Description</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Consoles d’administration de serveur d’applications</p> </td> 
   <td><p>Après avoir installé, configuré et déployé AEM Forms sur JEE sur votre serveur d’applications, désactivez l’accès aux consoles d’administration de serveur d’applications. Pour plus de détails, reportez-vous à la documentation de votre serveur d’applications.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Paramétrage des cookies pour le serveur d’applications</p> </td> 
   <td><p>Les cookies des applications sont contrôlés par le serveur d’applications. Lorsqu’il déploie l’application, l’administrateur du serveur d’applications peut spécifier des préférences concernant les cookies, soit à l’échelle du serveur, soit pour des applications spécifiques. Par défaut, les paramètres définis à l’échelle du serveur sont prioritaires.</p> <p>Tous les cookies de session générés par votre serveur d’applications devraient inclure l’attribut <code>HttpOnly</code>. For example, when using the JBoss Application Server, you can modify the SessionCookie element to <code>httpOnly="true"</code> in the <code>WEB-INF/web.xml</code> file.</p> <p>Vous pouvez limiter l’envoi de cookies au moyen de HTTPS uniquement. En conséquence, les cookies ne sont pas envoyés non codés sur HTTP. Il est conseillé aux administrateurs de serveurs d’applications d’autoriser les cookies sûrs à l’échelle du serveur. Par exemple, si vous utilisez JBoss Application Server, vous pouvez redéfinir l’élément connecteur sur <code>secure=true</code> dans le fichier <code>server.xml</code>.</p> <p>Reportez-vous à la documentation de votre serveur d’applications pour plus d’informations sur les paramètres des cookies.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Exploration des répertoires</p> </td> 
   <td><p>Lorsqu’un utilisateur demande une page qui n’existe pas ou le nom d’un directeur (la chaîne de demande se termine par une barre oblique (/)), le serveur d’applications ne devrait pas renvoyer le contenu de ce répertoire. Pour éviter cela, vous pouvez désactiver la capacité d’exploration des répertoires sur votre serveur d’applications. Vous devriez effectuer cette action pour l’application Administration Console, et pour les autres applications exécutées sur votre serveur.</p> <p>Pour JBoss, définissez la valeur du paramètre d’initialisation des listes de la propriété <code>DefaultServlet</code> sur <code>false</code> dans le fichier web.xml, comme illustré dans l’exemple ci-dessous :</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;default&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;listings&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>Pour WebSphere, définissez la propriété <code>directoryBrowsingEnabled</code> du fichier ibm-web-ext.xmi sur <code>false</code>.</p> <p>Pour WebLogic, définissez les propriétés index-directories du fichier weblogic.xml sur <code>false</code>, comme illustré dans l’exemple suivant :</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### Sécurité de la base de données {#database-security}

Lorsque vous sécurisez votre base de données, implémentez les mesures indiquées par le revendeur de votre base de données. Attribuez à l’utilisateur de la base de données le nombre minimum d’autorisations requises sur cette base de données pour permettre l’utilisation avec AEM Forms sur JEE. Par exemple, n’utilisez pas de compte avec des autorisations d’administrateur de base de données.

Sur Oracle, le compte de base de données que vous utilisez nécessite uniquement les droits CONNECT, RESOURCE et CREATE VIEW. Pour connaître les exigences des autres bases de données, voir [Préparation à l’installation d’AEM Forms sur JEE (serveur unique)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64).

#### Configuration de la sécurité intégrée dans SQL Server sur Windows pour JBoss {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. Modifiez [JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml} pour ajouter `integratedSecurity=true` à l’URL de connexion, comme indiqué dans cet exemple :

   ```as3
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. Ajoutez le fichier sqljdbc_auth.dll au chemin d’accès du système Windows sur l’ordinateur exécutant le serveur d’applications. Le fichier sqljdbc_auth.dll se trouve avec les fichiers d’installation du pilote Microsoft SQL JDBC 6.2.1.0.
1. Modifiez la propriété du service Windows JBoss (JBoss pour AEM Forms sur JEE) pour Ouvrir une session en tant que dans le Système local pour un compte utilisateur disposant d’une base de données AEM Forms et d’un ensemble minimum de droits. Si vous exécutez JBoss à partir de la ligne de commande plutôt que comme un service Windows, ignorez cette étape.
1. Faites passer la sécurité de SQL Server du mode **Mixte** au mode **Authentification Windows**.

#### Configuration de la sécurité intégrée dans SQL Server sur Windows pour WebLogic {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. Début de WebLogic Server Administration Console en saisissant l’URL suivante dans la ligne d’adresse d’un navigateur Web :

   ```as3
   https://[host name]:7001/console
   ```

1. Sous Change Center, cliquez sur **Lock &amp; Edit**.
1. Under Domain Structure, click *[base_domain]* > **Services** > **JDBC** > **Data Sources** and, in the right pane, click **IDP_DS**.
1. Dans l’écran suivant, dans l’onglet **Configuration**, cliquez sur l’onglet **Connection Pool** et, dans la zone **Properties**, saisissez `integratedSecurity=true`.
1. Under Domain Structure, click **[base_domain]** > **Services** > **JDBC** > **Data Sources** and, in the right pane, click **RM_DS**.
1. Dans l’écran suivant, dans l’onglet **Configuration**, cliquez sur l’onglet **Connection Pool** et, dans la zone **Properties**, saisissez `integratedSecurity=true`.
1. Ajoutez le fichier sqljdbc_auth.dll au chemin d’accès du système Windows sur l’ordinateur exécutant le serveur d’applications. Le fichier sqljdbc_auth.dll se trouve avec les fichiers d’installation du pilote Microsoft SQL JDBC 6.2.1.0.
1. Faites passer la sécurité de SQL Server du mode **Mixte** au mode **Authentification Windows**.

#### Configuration de la sécurité intégrée dans SQL Server sur Windows pour WebSphere {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

Sur WebSphere, vous pouvez configurer la sécurité intégrée uniquement lorsque vous utilisez un pilote JDBC SQL Server externe et non le pilote JDBC SQL Server incorporé avec WebSphere.

1. Connectez-vous à WebSphere Administrative Console.
1. Dans l’arborescence de navigation, cliquez sur **Resources** > **JDBC** > **Data Sources**, puis, dans le volet de droite, cliquez sur **IDP_DS**.
1. Dans le volet de droite, sous Additional Properties, cliquez sur **Custom Properties**, puis sur **New**.
1. In the **Name** box, type `integratedSecurity` and, in the **Value** box, type `true`.
1. Dans l’arborescence de navigation, cliquez sur **Resources** > **JDBC** > **Data Sources**, puis, dans le volet de droite, cliquez sur **RM_DS**.
1. Dans le volet de droite, sous Additional Properties, cliquez sur **Custom Properties**, puis sur **New**.
1. In the **Name** box, type `integratedSecurity` and, in the **Value** box, type `true`.
1. Sur l’ordinateur sur lequel WebSphere est installé, ajoutez le fichier sqljdbc_auth.dll au chemin du système Windows (C:\Windows). The sqljdbc_auth.dll file is in the same location as the Microsoft SQL JDBC 1.2 driver installation (default is *[InstallDir]*/sqljdbc_1.2/enu/auth/x86).
1. Sélectionnez **Démarrer** > **Panneau de configuration** > **Services**, cliquez avec le bouton droit de la souris sur le service Windows pour WebSphere (IBM WebSphere Application Server &lt;version> - &lt;nœud>), puis sélectionnez **Propriétés**.
1. Dans la boîte de dialogue Propriétés, cliquez sur l’onglet **Ouvrir une session**.
1. Sélectionnez **Ce compte** et indiquez les informations requises pour définir le compte de connexion à utiliser.
1. Faites passer la sécurité de SQL Server du mode **Mixte** au mode **Authentification Windows**.

### Protection de l’accès aux contenus sensibles dans la base de données {#protecting-access-to-sensitive-content-in-the-database}

Le schéma de la base de données AEM Forms contient des informations sensibles relatives à la configuration du système et aux processus de l’entreprise et doit être protégé par un pare-feu. La base de données doit être considérée comme faisant partie de la même zone de confiance que le serveur de formulaires. Pour éviter tout risque de divulgation d’informations et de vol de données d’entreprise, la base de données doit être configurée par l’administrateur de base de données (DBA) pour donner l’accès aux administrateurs autorisés uniquement.

Pour une sécurité accrue, prévoyez d’utiliser des outils spécifiques au revendeur de votre base de données pour chiffrer les colonnes des tableaux contenant les données suivantes :

* clés de document Rights Management ;
* clé de chiffrement de PIN HSM Trust Store ;
* hachages des mots de passe des utilisateurs locaux.

For information about vendor-specific tools, see [“Database security information”](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information).

### Sécurité LDAP {#ldap-security}

En règle générale, un répertoire LDAP (Lightweight Directory Access Protocol) est utilisé par AEM Forms sur JEE comme une source d’informations relatives aux utilisateurs et aux groupes de l’entreprise et comme un moyen d’authentifier les mots de passe. Assurez-vous que votre répertoire LDAP est configuré pour utiliser le protocole SSL (Secure Socket Layer) et qu’AEM Forms sur JEE est configuré pour accéder à votre répertoire LDAP en utilisant son port SSL.

#### Déni de service LDAP {#ldap-denial-of-service}

Une attaque courante utilisant LDAP consiste, pour un attaquant, à omettre délibérément de s’authentifier à plusieurs reprises. Ceci oblige le serveur d’annuaires LDAP à interdire à un utilisateur l’accès à tous les services dépendant de LDAP.

Vous pouvez définir le nombre de tentatives d’authentification maximum autorisé et la durée du verrouillage appliqué par AEM Forms lorsqu’un utilisateur échoue de manière répétée à s’authentifier auprès dAEM Forms. Dans Administration Console, choisissez des valeurs faibles. Lors de la sélection du nombre d’échecs d’authentification maximum autorisé, il est important de comprendre que si toutes les tentatives échouent, AEM Forms verrouille l’utilisateur avant que le serveur d’annuaire LDAP ne le fasse.

#### Paramètres de verrouillage de compte automatique {#set-automatic-account-locking}

1. Connectez-vous à Administration Console.
1. Cliquez sur **Paramètres** > **User Management** > **Gestion des domaines**.
1. Sous Paramètres de verrouillage de compte automatique, définissez **Echecs d’authentification consécutifs max.** sur un nombre peu élevé, 3 par exemple.
1. Cliquez sur **Enregistrer**.

### Contrôle et consignation {#auditing-and-logging}

L’utilisation appropriée et sécurisée des capacités de contrôle et de consignation des applications peut contribuer au suivi et à la détection rapides des événements liés à la sécurité et autres anomalies. L’utilisation efficace des capacités de contrôle et de consignation dans une application inclut des points comme le suivi des connexions réussies et échouées, de même que les événements clés de l’application comme la création ou la suppression d’enregistrements clés.

Vous pouvez utiliser les capacités de contrôle pour détecter de nombreux types d’attaques, parmi lesquels :

* les attaques de mot de passe en force ;
* les attaques par déni de service ;
* les attaques par injection de saisie hostile et les classes associées d’attaques de script.

Ce tableau décrit les techniques de contrôle et de consignation que vous pouvez utiliser pour limiter les vulnérabilités du serveur.

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
   <td><p>Définissez des liste de contrôle d’accès (ACL) de fichier journal AEM Forms sur JEE appropriées.</p> <p>Définir des informations d’identification appropriées contribue à empêcher les attaquants de supprimer les fichiers.</p> <p>Les autorisations de sécurité sur le répertoire des fichiers journaux doivent être de type « contrôle complet » pour les Administrateurs et les groupes SYSTEM. Seules les autorisations de lecture et d’écriture doivent être attribuées au compte utilisateur AEM Forms.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Fichiers journaux redondants</p> </td> 
   <td><p>Si les ressources le permettent, envoyez en temps réel des journaux à un autre serveur inaccessible pour l’attaquant (en lecture seule) en utilisant Syslog, Tivoli, Microsoft Operations Manager (MOM) Server ou tout autre mécanisme équivalent.</p> <p>En protégeant les journaux de cette manière, vous réduisez le risque de falsification. Par ailleurs, le fait de stocker les journaux dans un référentiel central facilite les processus de corrélation et de surveillance (par exemple, si plusieurs serveurs de formulaires sont en cours d’utilisation et qu’une attaque par recherche de mot de passe a lieu sur plusieurs ordinateurs, un mot de passe étant demandé à chaque ordinateur).</p> </td> 
  </tr> 
 </tbody> 
</table>

### Autoriser un utilisateur ne disposant pas de droits d’administrateur à exécuter PDF Generator

Vous pouvez permettre à un utilisateur non administrateur d’utiliser PDF Generator. Normalement, seuls les utilisateurs disposant de droits d’administrateur peuvent utiliser PDF Generator. Effectuez les étapes suivantes pour permettre à un utilisateur non administrateur d’exécuter PDF Generator :

1. Création d’un nom de variable d’environnement PDFG_NON_ADMIN_ENABLED.

1. Définissez la valeur de la variable à TRUE.

1. Redémarrez l’instance AEM Forms.

## Configuration d’AEM Forms sur JEE pour un accès au-delà de l’entreprise {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

Une fois AEM Forms sur JEE installé avec succès, il est important que vous assuriez une maintenance régulière de la sécurité de votre environnement. Cette section décrit les tâches recommandées pour assurer la maintenance de la sécurité du serveur de production AEM Forms sur JEE.

### Configuration d’un proxy inverse pour l’accès Web {#setting-up-a-reverse-proxy-for-web-access}

Un *proxy inverse* peut être utilisé pour garantir qu’un jeu d’URL d’applications AEM Forms sur JEE est disponible à la fois pour des utilisateurs externes et internes. Cette configuration est plus sûre que si vous autorisiez des utilisateurs à se connecter directement au serveur d’applications sur lequel est exécuté AEM Forms sur JEE. Le proxy inverse exécute toutes les requêtes HTTP pour le serveur d’applications qui exécute AEM Forms sur JEE. Les utilisateurs disposent d’un accès réseau limité au seul proxy inverse et ne peuvent se connecter qu’aux URL prises en charge par le proxy inverse.

**URL racine des AEM Forms sur JEE à utiliser avec un serveur proxy inverse**

Les URL suivantes sont les URL racine de chaque application Web AEM Forms sur JEE. Configurez votre proxy inverse pour qu’il n’expose que les URL de fonctionnalités d’applications Web dont vous souhaitez autoriser l’accès aux utilisateurs finaux.

Certaines URL sont présentées comme des applications Web accessibles par les utilisateurs finaux. Evitez d’exposer d’autres URL Configuration Manager pour l’accès à des utilisateurs externes via le proxy inverse.

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
   <td><p>Application Web d’utilisateur final d'Acrobat Reader DC extensions pour appliquer des droits d’utilisation à des documents PDF.</p> </td> 
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
   <td><p>Servlet d’amorçage du référentiel AEM Forms sur JEE</p> </td> 
   <td><p>Non</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/*</p> </td> 
   <td><p>Page d’informations pour les services Web du serveur de formulaires.</p> </td> 
   <td><p>Non</p> </td> 
   <td><p>Non</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/services/*</p> </td> 
   <td><p>URL de service Web de tous les services de serveur de formulaires.</p> </td> 
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
   <td><p>page d'accueil Administration Console</p> </td> 
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
   <td><p>Fichiers de l’application Web de Forms</p> </td> 
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
   <td><p>Page des paramètres de configuration de base d’AEM Forms sur JEE</p> </td> 
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
   <td><p>Téléchargement des documents à traiter lors de l’accès à des points de fin Remoting et SOAP WSDL et au JDK Java à l’aide du transport SOAP ou EJB avec activation des documents HTTP.</p> </td> 
   <td><p>Oui</p> </td> 
   <td><p>Oui</p> </td> 
  </tr> 
 </tbody> 
</table>

## Protection contre les attaques multisites par usurpation de requête {#protecting-from-cross-site-request-forgery-attacks}

Une attaque multisite par usurpation de requête (CSRF) exploite la confiance qu&#39;un site Web a pour l&#39;utilisateur, afin de transmettre des commandes non autorisées et involontaires par l&#39;utilisateur. L&#39;attaque est configurée en incluant un lien ou un script dans une page Web, ou une URL dans un message électronique, pour accéder à un autre site sur lequel l&#39;utilisateur a déjà été authentifié.

Par exemple, vous pouvez être connecté à Administration Console tout en parcourant un autre site Web. L’une des pages Web peut inclure une balise d’image HTML avec un attribut `src` visant un script côté serveur sur le site Web de la victime. En exploitant le mécanisme d’authentification de session basé sur les cookies, le site Web attaquant peut envoyer des requêtes malveillantes au script côté serveur ciblé en les faisant passer pour les requêtes de l’utilisateur autorisé. Pour plus d’exemples, voir [https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples).

Les caractéristiques suivantes sont communes aux cas de CSRF :

* impliquent des sites qui reposent sur une identité de l’utilisateur ;
* exploitent la confiance du site dans cette identité ;
* trompent le navigateur de l’utilisateur pour le faire envoyer des requêtes HTTP à un site cible ;
* impliquent des requêtes HTTP ayant des effets secondaires.

AEM Forms on JEE utilise la fonction Filtre de Parrain pour bloquer les attaques CSRF. Les termes suivants sont utilisés dans cette section pour décrire le mécanisme de filtrage des Parrains :

* **Parrain autorisé :** Un Parrain est l’adresse de la page source qui envoie une requête au serveur. Pour les pages ou les formulaires JSP, les Parrains sont généralement la page précédente dans l’historique de navigation. Les Parrains des images sont généralement les pages sur lesquelles les images sont affichées. Vous pouvez identifier le Parrain autorisé à accéder aux ressources de votre serveur en les ajoutant à la liste de Parrain autorisée.
* **Exceptions de Parrain autorisées :** Vous pouvez restreindre la portée de l&#39;accès pour un Parrain particulier dans votre liste de Parrain autorisée. Pour appliquer cette restriction, vous pouvez ajouter des chemins d&#39;accès individuels de ce Parrain à la liste des exceptions aux Parrains autorisés. Les requêtes provenant de chemins d’accès dans la liste des exceptions aux Parrains autorisés ne peuvent pas appeler de ressource sur le serveur Forms. Vous pouvez définir des exceptions aux Parrains autorisés pour une application spécifique et utiliser également une liste globale d’exceptions qui s’appliquent à toutes les applications.
* **URI autorisés :** Il s&#39;agit d&#39;une liste de ressources à fournir sans vérification de l&#39;en-tête du Parrain. Par exemple, les ressources telles que les pages d’aide, qui n’entraînent pas de changements d’état sur le serveur, peuvent être ajoutées à cette liste. Les ressources de la liste URIs autorisée ne sont jamais bloquées par le filtre de Parrain, quel que soit le Parrain.
* **Parrain nul :** Une requête de serveur qui n’est pas associée ou ne provient pas d’une page Web parente est considérée comme une requête d’un Parrain Null. Par exemple, lorsque vous ouvrez une nouvelle fenêtre de navigateur, tapez une adresse et appuyez sur Entrée, le Parrain envoyé au serveur est nul. Une application de bureau (.NET ou SWING) qui émet une requête HTTP à un serveur Web, envoie également un Parrain Null au serveur.

### Filtrage des Parrains {#referer-filtering}

Le processus de filtrage des Parrains peut être décrit comme suit :

1. Le serveur Forms vérifie la méthode HTTP utilisée pour l’appel :

   1. S’il s’agit d’un POST, le serveur Forms vérifie l’en-tête du Parrain.
   1. If it is GET, the forms server bypasses the Referrer check, unless *CSRF_CHECK_GETS* is set to true, in which case it performs the Referrer header check. La variable *CSRF_CHECK_GETS* est spécifiée dans le fichier *web.xml* pour votre application.

1. Le serveur Forms vérifie si l’URI requis existe dans la liste autorisée :

   1. Si l’URI est placé sur l&#39;liste autorisée, le serveur accepte la demande.
   1. Si l’URI requis n’est pas placé sur l&#39;liste autorisée, le serveur récupère le Parrain de la requête.

1. S’il existe un Parrain dans la requête, le serveur vérifie s’il s’agit d’un Parrain autorisé. S’il est autorisé, le serveur recherche une exception de Parrain :

   1. S’il s’agit d’une exception, la requête est bloquée.
   1. S’il ne fait pas partie des exceptions, la requête est transmise.

1. S’il n’y a aucun Parrain dans la requête, le serveur vérifie si un Parrain Null est autorisé :

   1. Si un Parrain Null est autorisé, la requête est transmise.
   1. Si un Parrain Null n’est pas autorisé, le serveur vérifie si l’URI requis est une exception pour le Parrain Null et traite la demande en conséquence.

### Gestion du filtrage des Parrains {#managing-referer-filtering}

AEM Forms on JEE fournit un filtre de Parrain pour spécifier les Parrains autorisés à accéder aux ressources de votre serveur. By default, the Referrer filter does not filter requests that use a safe HTTP method, e.g. GET, unless *CSRF_CHECK_GETS* is set to true. Si le numéro de port d’une entrée de Parrain autorisée est défini sur 0, AEM Forms on JEE autorise toutes les requêtes avec Parrain de cet hôte, quel que soit le numéro de port. Si aucun numéro de port n’est spécifié, seules les requêtes provenant du port par défaut 80 (HTTP) ou du port 443 (HTTPS) sont autorisées. Le filtrage de Parrain est désactivé si toutes les entrées de la liste de Parrain autorisée sont supprimées.

Lors de la première installation de Document Services, la liste de Parrain autorisée est mise à jour avec l’adresse du serveur sur lequel Document Services est installé. Les entrées pour le serveur comprennent le nom du serveur, l’adresse IPv4, l’adresse IPv6 si le protocole IPv6 est activé, l’adresse de bouclage et une entrée localhost. Les noms ajoutés à la liste de Parrain autorisée sont renvoyés par le système d’exploitation hôte. Par exemple, un serveur dont l’adresse IP est 10.40.54.187 comprend les entrées suivantes : `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`. Pour tout nom non qualifié renvoyé par le système d’exploitation hôte (noms sans adresse IPv4, adresse IPv6 ou nom de domaine qualifié), la liste autorisée n’est pas mise à jour. Modifiez la liste de Parrain autorisée en fonction de votre environnement d’entreprise. Ne déployez pas le serveur Forms dans l’environnement de production avec la liste de Parrain autorisée par défaut. Après avoir modifié l’un des Parrains, Parrains Exceptions ou URI autorisés, veillez à redémarrer le serveur pour que les modifications prennent effet.

**Gestion des listes de Parrain autorisées**

Vous pouvez gérer la liste de Parrain autorisée à partir de l&#39;interface User Management d&#39;Administration Console. L’interface User Management offre des fonctionnalités pour créer, éditer ou supprimer la liste. Refer to the * [Preventing CSRF attacks](/help/forms/using/admin-help/preventing-csrf-attacks.md)* section of the *administration help* for more information on working with the Allowed Referrer list.

**Gestion des exceptions aux Parrains autorisés et des listes URI autorisées**

AEM Forms on JEE fournit des API pour gérer la liste d’exception Parrain autorisé et la liste URI autorisée. Vous pouvez utiliser ces API pour récupérer, créer, éditer ou supprimer la liste. Voici la liste des API disponibles :

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

Pour plus d’informations sur les API, voir le Guide de référence de l’API de AEM Forms on JEE*.

Use the ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** list for Allowed Referrer Exceptions at the global level i.e. to define exceptions that are applicable to all applications. This list contains only URIs with either an absolute path (e.g. `/index.html`) or a relative path (e.g. `/sample/`). Vous pouvez également ajouter une expression régulière à la fin d’un URI relatif, par ex. `/sample/(.)*`.

L’ID de liste ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** est définie comme une constante dans la classe `UMConstants` de l’espace de noms `com.adobe.idp.um.api`, figurant dans `adobe-usermanager-client.jar`. Vous pouvez utiliser les API AEM Forms pour créer, modifier ou éditer cette liste. Par exemple, pour créer la liste globale des exceptions aux Parrains autorisés, utilisez :

```as3
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

Utilisez la liste ***CSRF_ALLOWED_REFERER_EXCEPTIONS*** pour les exceptions spécifiques à une application.

**Désactivation du filtre de Parrain**

Dans le événement où le filtre de Parrain bloque complètement l’accès au serveur Forms et que vous ne pouvez pas modifier la liste de Parrain autorisée, vous pouvez mettre à jour le script de démarrage du serveur et désactiver le filtrage de Parrain.

Include the `-Dlc.um.csrffilter.disabled=true` JAVA argument in the startup script and restart the server. Assurez-vous de supprimer l’argument JAVA après avoir correctement reconfiguré la liste de Parrain autorisée.

**Filtrage des Parrains pour les fichiers WAR personnalisés**

Vous avez peut-être créé des fichiers WAR personnalisés afin de travailler avec AEM Forms sur JEE pour répondre aux besoins de l’activité. To enable Referrer Filtering for your custom WAR files, include ***adobe-usermanager-client.jar*** in the class path for the WAR and include a filter entry in the* web.xml* file with the following parameters:

**CSRF_CHECK_GETS** contrôle la vérification du Parrain sur les requêtes GET. Si ce paramètre n’est pas défini, la valeur par défaut est définie sur false. Incluez ce paramètre uniquement si vous souhaitez filtrer vos requêtes GET.

**CSRF_ALLOWED_REFERER_EXCEPTIONS** est l’identifiant de la liste d’exceptions aux Parrains autorisés. Le filtre de Parrain empêche les requêtes provenant de Parrains de la liste identifiés par l’ID de liste d’appeler toute ressource sur le serveur Forms.

**CSRF_ALLOWED_URIS_LIST_NAME** est l’ID de la liste des URI autorisés. Le filtre de Parrain ne bloque aucune requête pour les ressources de la liste identifiées par l’identifiant de liste, quelle que soit la valeur de l’en-tête de Parrain dans la requête.

**CSRF_ALLOW_NULL_REFERER** contrôle le comportement du filtre de Parrain lorsque le Parrain est nul ou non présent. Si ce paramètre n’est pas défini, la valeur par défaut est définie sur false. N&#39;incluez ce paramètre que si vous souhaitez autoriser les Parrains nuls. L’autorisation de parrains nuls peut autoriser certains types d’attaques multisites par usurpation de requête.

**CSRF_NULL_REFERER_EXCEPTIONS** est une liste des URI pour lesquels une vérification de Parrain n’est pas effectuée lorsque le Parrain est nul. Ce paramètre est activé uniquement lorsque la variable *CSRF_ALLOW_NULL_REFERER* est définie sur false. Séparez les URI de la liste à l’aide de virgules.

Voici un exemple de l’entrée de filtre dans le fichier *web.xml* pour un ***exemple*** de dossier WAR :

```as3
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

* Si la demande rejetée comporte un en-tête de Parrain, pensez à l’ajouter à la liste de Parrain autorisée. Ajoutez uniquement le Parrain en lequel vous avez confiance.
* Si la demande rejetée ne comporte pas d’en-tête de Parrain, modifiez votre application cliente pour y inclure un en-tête de Parrain.
* Si le client peut travailler dans un navigateur, essayez ce modèle de déploiement.
* En dernier recours, vous pouvez ajouter la ressource à la liste des URI autorisés. Ceci n’est pas un paramètre recommandé.

## Configuration réseau sécurisée {#secure-network-configuration}

Cette section décrit les protocoles et les ports requis par AEM Forms sur JEE et fournit des recommandations pour déployer AEM Forms sur JEE dans une configuration réseau sécurisée.

### Protocoles réseau utilisés par AEM Forms sur JEE {#network-protocols-used-by-aem-forms-on-jee}

Lorsque vous configurez une architecture réseau sécurisée comme décrit dans la section précédente, les protocoles réseau suivants sont requis pour l’interaction entre AEM Forms sur JEE et d’autres systèmes dans le réseau de votre entreprise.

<table> 
 <thead> 
  <tr> 
   <th><p>Protocole</p> </th> 
   <th><p>Utilisation</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>HTTP</p> </td> 
   <td> 
    <ul> 
     <li><p>Le navigateur affiche Configuration Manager et des applications Web d’utilisateur final.</p> </li> 
     <li><p>Toutes les connexions SOAP</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Applications clientes de services Web telles que les applications .NET</p> </li> 
     <li><p>Adobe Reader® utilise les services Web de serveur SOAP pour AEM Forms sur JEE.</p> </li> 
     <li><p>Les applications Adobe Flash® utilisent SOAP pour les services Web de serveur de formulaires</p> </li> 
     <li><p>Appels SDK AEM Forms sur JEE en mode SOAP</p> </li> 
     <li><p>Environnement de création de Workbench</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>Appels SDK AEM Forms sur JEE en mode Enterprise JavaBeans (EJB)</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP / POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>Entrée par courrier électronique dans un service (point de fin de courrier électronique)</p> </li> 
     <li><p>Notifications des tâches utilisateur par courrier électronique</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>UNC File IO</p> </td> 
   <td><p>Surveillance d’AEM Forms sur JEE des dossiers de contrôle pour l’entrée dans un service (point de fin de dossier de contrôle)</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Synchronisations des informations relatives aux utilisateurs et aux groupes de l’entreprise dans un annuaire</p> </li> 
     <li><p>Authentification LDAP pour les utilisateurs interactifs</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>Appels de requête et de procédure à une base de données externe lors de l’exécution d’un processus utilisant le service JDBC</p> </li> 
     <li><p>Référentiel AEM Forms sur JEE d’accès interne</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>Permet la navigation à distance dans le référentiel de conception AEM Forms sur JEE (formulaires, fragments, etc.) par tout client WebDAV.</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>Applications Adobe Flash, dans lesquelles les services de serveur AEM Forms sur JEE sont configurés avec un point de fin Remoting.</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>AEM Forms sur JEE expose les MBeans pour le contrôle avec JMX.</p> </td> 
  </tr> 
 </tbody> 
</table>

### Ports de serveur d’applications {#ports-for-application-servers}

Cette section décrit les ports par défaut (et les plages de configurations alternatives) pour chaque type de serveur d’applications pris en charge. Ces ports doivent être activés ou désactivés sur le pare-feu interne, selon la fonctionnalité réseau que vous souhaitez autoriser aux clients qui se connectent au serveur d’applications qui exécute AEM Forms sur JEE.

>[!NOTE]
>
>par défaut, le serveur expose plusieurs MBeans JMX sous l’espace de nom adobe.com. Seules les informations utiles à la surveillance de la santé du serveur sont exposées. Toutefois, pour éviter toute divulgation d’informations, interdisez aux appelants dans un réseau non approuvé de rechercher les MBean JMX et d’accéder aux mesures de santé.

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
   <td><p>[racine_JBOSS]/standalone/configuration/lc_[base de données].xml</p> <p>Port HTTP/1.1 Connector 8080</p> <p>Port AJP 1.3 Connector 8009</p> <p>Port SSL/TLS Connector 8443</p> </td> 
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
     <li><p>Port d’écoute d’Admin Server : 7001 par défaut</p> </li> 
     <li><p>Port d’écoute SSL d’Admin Server : 7002 par défaut</p> </li> 
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

Pour plus d’informations sur les ports WebSphere requis par AEM Forms on JEE, voir Paramètres de numéro de port dans l’interface utilisateur de WebSphere Application Server.

### Configuration de SSL {#configuring-ssl}

Referring to the physical architecture that is described in the section [AEM Forms on JEE physical architecture](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture), you should configure SSL for all of the connections that you plan to use. Spécifiquement, toutes les connexions SOAP doivent être établies via SSL pour empêcher que les informations d’identification des utilisateurs soient exposées sur un réseau.

Pour obtenir des instructions sur la manière de configurer SSL sur JBoss, WebLogic et WebSphere, voir Configuration de SSL, dans l’[aide à l’administration](https://www.adobe.com/go/learn_aemforms_admin_64).

### Configuration de la redirection SSL {#configuring-ssl-redirect}

Après avoir configuré votre serveur d’applications pour qu’il prenne en charge SSL, vous devez vous assurer que l’ensemble du trafic HTTP vers les applications et les services utilise le port SSL.

Pour configurer la redirection SSL pour WebSphere et WebLogic, reportez-vous à la documentation de votre serveur d’applications.

1. Ouvrez l’invite de commande, accédez au répertoire /JBOSS_HOME/standalone/configuration, puis exécutez la commande suivante :

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. Ouvrez le fichier JBOSS_HOME/standalone/configuration/standalone.xml pour le modifier.

   Après l’élément &lt;sous-système xmlns=&quot;urn:jboss:domain:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;>, ajoutez les détails suivants :

   &lt;nom du connecteur=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot;/>

1. Ajoutez le code suivant dans l’élément connecteur https :

   ```
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   Enregistrez et fermez le fichier standalone.xml.

## Recommandations de sécurité spécifiques à Windows {#windows-specific-security-recommendations}

Cette section contient des recommandations de sécurité spécifiques à Windows dans le cadre de l&#39;exécution d&#39;AEM Forms sur JEE.

### Comptes de service JBoss {#jboss-service-accounts}

L’installation clé en main d’AEM Forms sur JEE installe un compte de service par défaut en utilisant le compte système local. Le compte utilisateur système local intégré présente un haut niveau d’accessibilité ; il fait partie du groupe Administrateurs. Si une identité de processus de travail est exécutée en tant que compte utilisateur système local, ce processus de travail dispose d’un accès complet à l’ensemble du système.

#### Exécution du serveur d’applications à l’aide d’un compte non administratif spécifique {#run-the-application-server-using-a-non-administrative-account}

1. Dans Microsoft Management Console (MMC), créez un utilisateur local pour que le service de serveur de formulaires se connecte en tant que cet utilisateur local :

   * Sélectionnez **L’utilisateur ne peut pas changer de mot de passe**.
   * Vérifiez que le groupe Utilisateurs figure dans l’onglet **Membre de**.

1. Sélectionnez **Paramètres** > **Outils d’administration** > **Services**.
1. Cliquez deux fois sur le service de serveur d’applications et arrêtez ce service.
1. Sur l’onglet **Ouvrir une session**, sélectionnez **Ce compte**, recherchez le compte utilisateur que vous avez créé, puis entrez le mot de passe pour ce compte.
1. Dans la fenêtre Paramètres de sécurité locaux, sous Attribution des droits utilisateur, attribuez les droits suivants au compte utilisateur sous lequel est exécuté le serveur de formulaires :

   * Interdire l’ouverture de session par les services Terminal
   * Refuser de se connecter sur locallyxx
   * Ouvrir une session en tant que service (ce droit doit être déjà défini)

1. Attribuez au nouveau compte d’utilisateur les autorisations de modification sur les répertoires suivants :
   * **Répertoire** d’Enregistrement de Document global (GDS) : L’emplacement du répertoire de stockage global de documents est configuré manuellement pendant le processus d’installation AEM Forms. If the location setting remains empty during installation, the location defaults to a directory under the application server installation at `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **Répertoire** CRX-Repository : L’emplacement par défaut est `[AEM-Forms-installation-location]\crx-repository`
   * **Répertoires** temporaires AEM Forms :
      * (Windows) Chemin TMP ou TEMP tel que défini dans les variables d’environnement
      * (AIX, Linux, ou Solaris) Répertoire racine de l’utilisateur connecté
Sur les systèmes de type UNIX, un utilisateur non connecté comme utilisateur root peut utiliser le répertoire suivant comme répertoire temporaire :
      * (Linux) /var/tmp ou /usr/tmp
      * (AIX) /tmp ou /usr/tmp
      * (Solaris) /var/tmp ou /usr/tmp
1. Attribuez au nouveau compte d’utilisateur des autorisations d’écriture sur les répertoires suivants :
   * [JBoss-directory]\standalone\deployment
   * [JBoss-directory]\standalone\
   * [JBoss-directory]\bin\

   >[!NOTE]
   >
   > Emplacement d’installation par défaut de JBoss Application Server :
   > * Windows : C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux : /opt/jboss/.


1. Démarrez le service de serveur d’applications.

### Sécurité du système de fichiers {#file-system-security}

AEM Forms sur JEE utilise le système de fichiers comme suit :

* stocke les fichiers temporaires utilisés lors du traitement des entrées et sorties de documents ;
* stocke dans une banque d’archives globale les fichiers utilisés pour prendre en charge les composants de la solution qui sont installés ;
* les dossiers de contrôle stockent les fichiers utilisés en entrée dans un service à partir d’un emplacement de dossier du système de fichiers.

Lorsque vous utilisez des dossiers de contrôle comme moyen d’envoyer et de recevoir des documents avec un service de serveur de formulaires, soyez très prudent quant à la sécurité du système de fichiers. Lorsqu’un utilisateur dépose des contenus dans le dossier de contrôle, ces contenus sont exposés via le dossier de contrôle. Dès lors, le service n’authentifie pas l’utilisateur final réel. Au lieu de cela, il considère que la sécurité par liste de contrôle d’accès et par niveau de dossier a été définie au niveau des dossiers pour déterminer qui peut effectivement appeler le service.

## Recommandations de sécurité spécifiques à JBoss {#jboss-specific-security-recommendations}

Cette section présente des recommandations relatives à la configuration du serveur d’applications et spécifiques à JBoss 7.0.6 lorsqu’il est utilisé pour exécuter AEM Forms on JEE.

### Désactivation de la console de gestion JBoss et de la console JMX {#disable-jboss-management-console-and-jmx-console}

L’accès à la console de gestion JBoss et à la console JMX est déjà configuré (la surveillance JMX est désactivée) lorsque vous installez AEM Forms sur JEE sur Jboss en appliquant la méthode d’installation clé en main. Si vous utilisez votre propre serveur d’applications JBoss, assurez-vous que l’accès à la console de gestion JBoss et à la console de surveillance JMX est sécurisé. L’accès à la console de surveillance JMX est défini dans le fichier de configuration de JBoss appelé jmx-invoker-service.xml.

### Désactivation de l’exploration des répertoires {#disable-directory-browsing}

Après vous être connecté à Administration Console, vous pouvez parcourir la liste des répertoires de la console en modifiant l’URL. Par exemple, si vous modifiez l’URL pour l’une de ces adresses, une liste de répertoires s’affiche :

```as3
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## Recommandations de sécurité spécifiques à WebLogic {#weblogic-specific-security-recommendations}

Cette section présente des recommandations relatives à la configuration du serveur d’applications et spécifiques à WebLogic9.1 lorsque celui-ci est utilisé pour exécuter AEM Forms sur JEE.

### Désactivation de l’exploration des répertoires {#disable_directory_browsing-1}

Définissez les propriétés index-directories du fichier weblogic.xml sur `false`, comme illustré dans l’exemple suivant :

```as3
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### Activation du port SSL de WebLogic {#enable-weblogic-ssl-port}

Par défaut, WebLogic n’active pas le port d’écoute SSL par défaut, 7002. Activez ce port dans le serveur WebLogic Server Administration Console avant de configurer SSL.

## Recommandations de sécurité spécifiques à WebSphere {#websphere-specific-security-recommendations}

Cette section présente des recommandations relatives à la configuration du serveur d’applications pour sécuriser Websphere exécutant AEM Forms sur JEE.

### Désactivation de l’exploration des répertoires {#disable_directory_browsing-2}

Set the `directoryBrowsingEnabled` property in the ibm-web-ext.xml file to `false`.

### Activation de la sécurité administrative de WebSphere {#enable-websphere-administrative-security}

1. Connectez-vous à WebSphere Administrative Console.
1. Dans l’arborescence de navigation, accédez à **Sécurité** > Sécurité **globale**
1. Sélectionnez **Enable administrative security**.
1. Désélectionnez **Enable application security** et **Use Java 2 security**.
1. Cliquez sur **OK** ou sur **Apply**.
1. Dans la zone **Messages**, cliquez sur **Save directly to master configuration**.