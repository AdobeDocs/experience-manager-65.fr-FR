---
title: Correctifs pour AEM Forms
description: Fournit des informations sur la manière de télécharger et d’installer un correctif pour AEM Forms.
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
source-git-commit: 11e155ed72caf8f75bd2d8c8293723f24fe82945
workflow-type: tm+mt
source-wordcount: '4751'
ht-degree: 69%
---
# Correctifs Adobe Experience Manager Forms{#aem-form-hotfix}

Cet article répertorie les correctifs critiques mis en œuvre pour résoudre les problèmes connus, améliorer la stabilité du système et optimiser les performances globales d’AEM Forms.

>[!NOTE]
>
> Les correctifs sont conçus pour être cumulatifs, c’est-à-dire qu’ils englobent tous les correctifs précédents. Ainsi, lorsque vous appliquez le dernier correctif à une version, il résout non seulement le problème le plus récent, mais incorpore également tous les correctifs et améliorations antérieurs.
>
> Comme le correctif est cumulatif, son application lors de l’utilisation d’un pack de services précédent met à jour votre déploiement avec tous les correctifs publiés jusqu’au pack de services sur lequel le correctif est créé, et pas seulement les problèmes répertoriés pour ce correctif.

## Correctifs pour AEM Forms {#hotfix-for-aem-forms}

<table>
  <tbody>
  <tr>
    <td><strong>Date</strong></td>
    <td><strong>Lien de téléchargement des correctifs (lien de distribution logicielle AEM)</strong></td>
    <td><strong>Problèmes résolus</strong></td>
  </tr>
  <tr>
    <td>
      <strong>18 septembre 2026</strong><br>
      <em>S’applique à : </em> AEM 6.5.25.0 les déploiements Forms JEE (JBoss, WebLogic, WebSphere).<br>
    </td>
    <td>
    <p><strong>Pour installer ce correctif, procédez comme suit :</strong></p>
    <p><strong>Étape 1 : installation du correctif</strong></p>
    <ul>
    <strong>JBoss:</strong>
    <li>Windows : <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-25-0-hotfix/jboss/adobe-aem-forms-jee-hotfix-6.5.25.0-win-jboss.zip">correctif pour AEM Service Pack 6.5.25.0 sur Windows pour le serveur JBoss JEE</a></li>
    <li>Linux : <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-25-0-hotfix/jboss/adobe-aem-forms-jee-hotfix-6.5.25.0-linux-jboss.tar.gz">correctif pour AEM Service Pack 6.5.25.0 sur Linux pour le serveur JBoss JEE</a></li>
    <strong>WebLogic:</strong>
    <li>Windows : <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-25-0-hotfix/weblogic/adobe-aem-forms-jee-hotfix-6.5.25.0-win-weblogic.zip">correctif pour AEM Service Pack 6.5.25.0 sur Windows pour le serveur Weblogic JEE</a></li>
    <li>Linux : <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-25-0-hotfix/weblogic/adobe-aem-forms-jee-hotfix-6.5.25.0-linux-weblogic.tar.gz">correctif pour AEM Service Pack 6.5.25.0 sur Linux pour le serveur Weblogic JEE</a></li>
    <strong>WebSphere:</strong>
    <li>Windows : <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-25-0-hotfix/websphere/adobe-aem-forms-jee-hotfix2-6.5.25.0-win-websphere.zip">correctif pour AEM Service Pack 6.5.25.0 sur Windows pour le serveur WebSphere JEE</a></li>
    <li>Linux : <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-25-0-hotfix/websphere/adobe-aem-forms-jee-hotfix-6.5.25.0-linux-websphere.tar.gz">correctif pour AEM Service Pack 6.5.25.0 sous Linux pour le serveur WebSphere JEE</a></li>
    </ul>
    <p>Suivez les instructions d’installation standard du correctif JEE d’<a href="/help/release-notes/jee-patch-installer-65.md"></a>.</p>
    <p><strong>Étape 2 : installer le lot de correctifs de vulnérabilité</strong></p>
    <ul>
    <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-25-0-hotfix/SP25Bundles_VULN-36670.zip">Lot de correctifs de vulnérabilité pour AEM 6.5.25.0</a></li>
    </ul>
    <ol>
    <li>Ouvrez la console OSGi sur <code>http://&lt;host&gt;:&lt;port&gt;/lc/system/console/bundles</code>.</li>
    <li>Cliquez sur <strong> Installer/Mettre à jour </strong>.</li>
    <li>Cochez les cases <strong>Démarrer le bundle</strong> et <strong>Actualiser les packages</strong>.</li>
    <li>Cliquez sur <strong>Choisir un fichier</strong>, puis chargez le lot téléchargé.</li>
    <li>Patientez jusqu’à ce que le journal se dépose et que le lot s’affiche comme <strong>Actif</strong>.</li>
    </ol>
    <p><strong>Étape 3 : mettre à jour le programme d’installation d’AEM Forms Workbench</strong></p>
    <p>Vous devez mettre à jour vers le dernier programme d’installation d’AEM Forms Workbench (6.5.25.0). Pour plus d’informations, voir <a href="https://experienceleague.adobe.com/fr/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases">Versions d’</a>.</p>
    <p><strong>Étape 4 : mettre à jour les fichiers de bibliothèque cliente (développeurs)</strong></p>
    <p>Ce correctif comprend une mise à jour majeure de la <code>adobe-livecycle-client.jar</code> de bibliothèque cliente SDK (voir <a href="/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files">Inclure des fichiers de bibliothèque Java AEM Forms</a>). Si votre projet utilise ce fichier JAR, mettez à jour <code>adobe-livecycle-client.jar</code> dans le chemin d’accès aux classes de votre projet après avoir installé le correctif. La dernière version est disponible à l’adresse <code>&lt;AEM_Forms_Installation_dir&gt;\sdk\client-libs\common\adobe-livecycle-client.jar</code>.</p>
    <p>Le correctif est cumulatif. Vous pouvez donc l’appliquer au pack de services 25 (6.5.25.0) ou à un pack de services antérieur sans installer le pack de services 25 au préalable.</p>
    </td>
    <td>
    <ul>
    <li><b>FORMS-26802</b> Après le renforcement de l’authentification SOAP SDK, LCM Configuration Manager, Workbench et Designer ne parviennent pas à se connecter au serveur avec le <code>ALC-LCM-200-001</code> d’erreur (le point d’entrée <code>/soap/sdk</code> rejette une requête non authentifiée). Ce correctif restaure la connectivité tout en maintenant l’authentification appliquée sur le point d’entrée.</li>
    <li><b>FORMS-26679</b> Dans AEM Forms Document Security, les cookies d’authentification sont ignorés après une redirection de Microsoft Entra ID (MFA), provoquant une erreur « Les cookies peuvent ne pas être activés » lors de l’ouverture de documents protégés par une politique. Ce correctif conserve les cookies de session sur la redirection intersite.</li>
    <li><b>FORMS-26617</b> Sur WebLogic, la configuration de la base de données via Configuration Manager échoue avec « Aucun pilote approprié trouvé » lors de l’utilisation du pilote Microsoft SQL Server JDBC 12.10.0. Ce correctif restaure la configuration réussie de la source de données.</li>
    <li>Les PDF <b>FORMS-27869</b> s’ouvrent lentement après l’installation de la dernière version d’AEM Forms 6.5. Ce correctif améliore les performances d’ouverture des documents.</li>
    </ul>
    </td>
  </tr>
  <tr>
    <td>
      <strong>8 juin 2026</strong><br>
      <em>S’applique à : </em> AEM 6.5.25.0 les déploiements Forms JEE.<br>
    </td>
    <td>
    <ul>
    <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-service-pkg-6.5.25-NPR-44100-B0002.zip">Correctif pour AEM Service Pack 6.5.25.0 (NPR-44100)</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li><b>NPR-44100</b> Après l’installation du pack de services 25.0 d’AEM 6.5 sur des déploiements WAR/JEE, le lot <code>com.adobe.cq.screens.sessions</code> reste à l’état Installé et ne devient jamais Actif.</li>
    </ul>
    </td>
  </tr>
  <tr>
    <td>
      <strong>6 janvier 2026</strong><br>
      <em>S’applique à : </em> AEM 6.5.24.0 les déploiements Forms JEE (JBoss, WebLogic, WebSphere).<br>
    </td>
    <td>
    <ul>
    <strong>Jboss:</strong>
    <li>Windows : <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-115/jboss/adobe-aem-forms-jee-service-pack-6.5.24.0-win-jboss.zip">correctif pour AEM Service Pack 6.5.24.0 sur Windows pour le serveur JBoss JEE</a></li>
    <li>Linux : <a href="https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-115/jboss/adobe-aem-forms-jee-service-pack-6.5.24.0-linux-jboss.gz">correctif pour AEM Service Pack 6.5.24.0 sur Linux pour le serveur JBoss JEE</a></li>
    <strong>Weblogic:</strong>
    <li>Windows : <a href="https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-115/weblogic/adobe-aem-forms-jee-service-pack-6.5.24.0-win-weblogic.zip">correctif pour AEM Service Pack 6.5.24.0 sur Windows pour le serveur Weblogic JEE</a></li>
    <li>Linux : <a href="https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-115/weblogic/adobe-aem-forms-jee-service-pack-6.5.24.0-linux-weblogic.gz">correctif pour AEM Service Pack 6.5.24.0 sur Linux pour le serveur Weblogic JEE</a></li>
    <strong>Websphere:</strong>
    <li>Windows : <a href="https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-115/websphere/adobe-aem-forms-jee-service-pack-6.5.24.0-windows-websphere.zip">correctif pour AEM Service Pack 6.5.24.0 sur Windows pour le serveur WebSphere JEE</a></li>
    <li>Linux : <a href="https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-115/websphere/adobe-aem-forms-jee-service-pack-6.5.24.0-linux-websphere.gz">correctif pour AEM Service Pack 6.5.24.0 sous Linux pour le serveur WebSphere JEE</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li><b>FORMS-23491</b> atténue la vulnérabilité CVE-2025-64775 (vulnérabilité de déni de service Apache Struts dans le traitement multipartie des requêtes) en mettant à niveau Struts vers une version qui résout le problème.</li>
    </ul>
    </td>
  </tr>
  <tr>
    <td>
      <strong>14 octobre 2025</strong><br>
      <em>Application :</em> échec d’ImgToPdf avec AEM Forms SP23 Jboss<br>
    </td>
    <td>
    <ul> Pour toute résolution, contactez l’assistance technique d’Adobe Experience Manager Forms <a href="https://business.adobe.com/in/support/main.html"></a>
    </ul>
    </td>
    <td>
    <ul>
    <li> <b>(FORMS-22029) :</b> améliore la fiabilité de la conversion PDF en résolvant un problème où PDF Generator (PDFG) ne parvient pas à convertir les fichiers image en PDF après la mise à niveau vers SP23, ce qui entraîne des erreurs de post-traitement inattendues.</li>
    </ul>
    </td>
  </tr>
  <tr>
    <td>
      <strong>23 septembre 2025</strong><br>
    </td>
    <td>
    <ul>
    <strong>Jboss:</strong>
    <li>Windows - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/jboss/adobe-aem-forms-jee-hotfix3-6.5.23.0-win-jboss.zip">Correctif pour le pack de services AEM 6.5.23.0 sur Windows pour le serveur JBoss JEE</a></li>
    <li>Linux - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/jboss/adobe-aem-forms-jee-hotfix3-6.5.23.0-linux-jboss.tar.gz">Correctif pour le pack de services AEM 6.5.23.0 sur Linux pour le serveur JBoss JEE</a></li>
    <strong>Weblogic:</strong>
    <li>Windows - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/weblogic/adobe-aem-forms-jee-hotfix3-6.5.23.0-win-weblogic.zip">Correctif pour le pack de services AEM 6.5.23.0 sur Windows pour le serveur WebLogic JEE</a></li>
    <li>Linux - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/weblogic/adobe-aem-forms-jee-hotfix3-6.5.23.0-linux-weblogic.tar.gz">Correctif pour le pack de services AEM 6.5.23.0 sur Linux pour le serveur WebLogic JEE</a></li>
    <strong>Websphere:</strong>
    <li>Windows : <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/websphere/adobe-aem-forms-jee-hotfix3-6.5.23.0-win-websphere.zip">correctif pour AEM Service Pack 6.5.23.0 sur Windows pour le serveur WebSphere JEE</a></li>
    <li>Linux : <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-23-0-hotfix-3/websphere/adobe-aem-forms-jee-hotfix3-6.5.23.0-linux-websphere.tar.gz">correctif pour AEM Service Pack 6.5.23.0 sous Linux pour le serveur WebSphere JEE</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <strong>Ce correctif corrige les problèmes suivants :</strong> 
   <li> <b>(FORMS-21721) :</b> amélioration d’un problème en raison duquel les conversions PS vers PDF et HTML vers PDF (WebKit) échouent après le déploiement du correctif (publié le 5 <b> août 2025</b>) pour 6.5.23.0. 
    </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>
      <strong>5 août 2025</strong><br>
      <em>S’applique à :</em> AEM 6.5 Forms Service Pack 23<br>
      <em>Instructions de configuration :</em>
      <a href="/help/forms/using/mitigating-xxe-and-configuration-vulnerabilities-for-experience-manager-forms-jee.md#option-1-for-users-on-version-65230-install-latest-hotfix">
        Réduire les vulnérabilités XXE, de configuration et d’exécution de code à distance (CVE-2025-49533) pour AEM Forms sur JEE
      </a>
    </td>
    <td>
    <ul>
    <li><strong>Jboss :</strong></li>
    <li>Windows - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.23.0-win-jboss.zip">Correctif pour le pack de services AEM 6.5.23.0 sur Windows pour le serveur JBoss JEE</a></li>
    <li>Linux - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.23.0-linux-jboss.tar.gz">Correctif pour le pack de services AEM 6.5.23.0 sur Linux pour le serveur JBoss JEE</a></li>
    <li><strong>Weblogic :</strong></li>
    <li>Windows - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.23.0-win-weblogic.zip">Correctif pour le pack de services AEM 6.5.23.0 sur Windows pour le serveur WebLogic JEE</a></li>
    <li>Linux - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.23.0-linux-weblogic.tar.gz">Correctif pour le pack de services AEM 6.5.23.0 sur Linux pour le serveur WebLogic JEE</a></li>
    <li><strong>Websphere :</strong></li>
    <li>Windows : <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.23.0-win-websphere.zip">correctif pour AEM Service Pack 6.5.23.0 sur Windows pour le serveur WebSphere JEE</a></li>
    <li>Linux : <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.23.0-linux-websphere.zip">correctif pour AEM Service Pack 6.5.23.0 sous Linux pour le serveur WebSphere JEE</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li>Amélioration de la sécurité en remédiant à une vulnérabilité d’exécution de code à distance (RCE) dans Adobe Experience Manager (AEM) Forms. Le problème était lié au mode de développement Struts dans l’interface d’utilisation (UI) d’administration, qui permettait une évaluation arbitraire du langage de navigation objet-graphique (OGNL) via la fonctionnalité de débogage. Ce correctif garantit que le mode de développement Struts est désactivé et que des filtres de sécurité appropriés sont appliqués pour empêcher tout accès non autorisé.</li>
    <li>Amélioration de la protection contre les vulnérabilités d’entité externe (XXE) XML (Extensible Markup Language) dans le module EDC (Electronic Document Component) d’Adobe Experience Manager (AEM) Forms. Ces vulnérabilités étaient dues à une gestion incorrecte des documents XML sans protection XXE, ce qui pouvait entraîner des lectures de fichiers locaux. Le correctif comprend :
      <ul>
        <li>La vérification que DocumentBuilderFactory utilisé dans la classe SecurityCheckHandler est configuré pour empêcher les attaques XXE.</li>
        <li>La mise à jour du service web EDC pour gérer les documents XML en toute sécurité, empêchant ainsi tout accès non autorisé aux fichiers locaux.</li>
      </ul>
    </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>
      <strong>5 août 2025</strong><br>
      <em>S’applique à :</em> AEM 6.5 Forms Service Pack 18 - 22<br>
      <em>Instructions de configuration :</em>
      <a href="/help/forms/using/mitigating-xxe-and-configuration-vulnerabilities-for-experience-manager-forms-jee.md#option-2-for-users-on-65180---65220-manual-hotfix-installation">
        Installation manuelle du correctif pour les packs de services 18-22
      </a>
    </td>
    <td>
    <ul>
    <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-xxe-configuration-hotfix.zip">Correctif pour AEM 6.5 Forms Pack de services 18 - AEM 6.5 Forms Pack de services 22 </a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li>Amélioration de la sécurité en remédiant à une vulnérabilité d’exécution de code à distance (RCE) dans Adobe Experience Manager (AEM) Forms. Le problème était lié au mode de développement Struts dans l’interface d’utilisation (UI) d’administration, qui permettait une évaluation arbitraire du langage de navigation objet-graphique (OGNL) via la fonctionnalité de débogage. Ce correctif garantit que le mode de développement Struts est désactivé et que des filtres de sécurité appropriés sont appliqués pour empêcher tout accès non autorisé.</li>
    <li>Amélioration de la protection contre les vulnérabilités d’entité externe (XXE) XML (Extensible Markup Language) dans le module Document Security d’Adobe Experience Manager (AEM) Forms. Ces vulnérabilités étaient dues à une gestion incorrecte des documents XML sans protection XXE, ce qui pouvait entraîner des lectures de fichiers locaux. Le correctif comprend :
      <ul>
        <li>La vérification que DocumentBuilderFactory utilisé dans la classe SecurityCheckHandler est configuré pour empêcher les attaques XXE.</li>
        <li>Mise à jour du service web Document Security pour gérer les documents XML en toute sécurité, empêchant ainsi tout accès non autorisé aux fichiers locaux.</li>
      </ul>
    </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>10 juillet 2025</td>
    <td>
    <ul>
    <li><strong>Jboss :</strong></li>
    <li>Windows - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/jboss/adobe-aem-forms-jee-hotfix-6.5.23.0-win-jboss.zip">Correctif pour le pack de services AEM 6.5.23.0 sur Windows pour le serveur JBoss JEE</a></li>
    <li>Linux - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/jboss/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-jboss.tar.gz">Correctif pour le pack de services AEM 6.5.23.0 sur Linux pour le serveur JBoss JEE</a></li>
    <li><strong>Weblogic :</strong></li>
    <li>Windows - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/weblogic/adobe-aem-forms-jee-hotfix-6.5.23.0-win-weblogic.zip">Correctif pour le pack de services AEM 6.5.23.0 sur Windows pour le serveur WebLogic JEE</a></li>
    <li>Linux - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/weblogic/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-weblogic.tar.gz">Correctif pour le pack de services AEM 6.5.23.0 sur Linux pour le serveur WebLogic JEE</a></li>
    <li><strong>Websphere :</strong></li>
    <li>Windows : <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/websphere/adobe-aem-forms-jee-hotfix-6.5.23.0-win-websphere.zip">Correctif pour le pack de services AEM 6.5.23.0 sur Windows pour le serveur Webshpere JEE</a></li>
    <li>Linux : <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/websphere/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-websphere.tar.gz">Correctif pour le pack de services AEM 6.5.23.0 sur Linux pour le serveur Websphere JEE</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li><strong>Ce correctif corrige les problèmes suivants :</strong>
      <ul>
        <li><strong>FORMS-20533 :</strong> AEM Forms comprend désormais une mise à niveau de Struts, de la version 2.5.33 vers la version 6.x, pour le composant de formulaire. Cela permet d’obtenir les modifications apportées à Struts et précédemment manquées qui n’étaient pas incluses dans SP23. La prise en charge a été ajoutée via un correctif que vous pouvez télécharger et installer. La dernière version de Struts est alors prise en charge.</li>
        <li><strong>FORMS-20532 :</strong> AEM Forms comprend désormais une mise à niveau de la version Struts, de 2.5.33 vers 6.x, pour le composant de sortie. Cela permet d’obtenir les modifications apportées à Struts et précédemment manquées qui n’étaient pas incluses dans SP23. La prise en charge a été ajoutée via un correctif que vous pouvez télécharger et installer. La dernière version de Struts est alors prise en charge.</li>
        <li><strong>FORMS-20203 :</strong> lorsqu’un utilisateur ou une utilisatrice met à niveau Struts du pack de services AEM 2.5.x vers le pack de services AEM Forms 6.x, l’interface d’utilisation des politiques n’affiche pas toutes les configurations, telles que l’option d’ajout d’un filigrane. Pour résoudre ce problème, vous pouvez télécharger et installer le correctif.</li>
        <li><strong>FORMS-20360 :</strong> après la mise à niveau vers le pack de services AEM Forms 6.5.23.0, le service de conversion ImageToPDF échoue avec l’erreur :<br>
        <code>17:15:44,468 ERROR [com.adobe.pdfg.GeneratePDFImpl] (default task-49) ALC-PDG-001-000-ALC-PDG-011-028-Error occurred while converting the input image file to PDF. com/adobe/internal/pdftoolkit/core/encryption/EncryptionImp</code><br>
        Vous pouvez télécharger et installer le correctif pour résoudre ce problème.</li>
      </ul>
    </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>26 mars 2025 </br> </br> Pour installer ce correctif, suivez les instructions <a href="/help/forms/using/mitigating-spring-framework-vulnerabilities-for-aem-forms-on-jee.md"> Atténuation des vulnérabilités du framework Spring pour AEM Forms on JEE</a>.</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/jboss/adobe-aem-forms-jee-hotfix-6.5.22.0-win-jboss.tar.gz">Correctif pour le pack de services AEM 6.5.22.0 sur Windows pour le serveur JBoss JEE </a> </li>
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/fr/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/jboss/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-jboss.tar.gz">Correctif pour le pack de services AEM 6.5.22.0 sur Linux pour le serveur JBoss JEE </a> </li>
       <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/fr/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/weblogic/adobe-aem-forms-jee-hotfix-6.5.22.0-win-weblogic.tar.gz">Correctif pour le pack de services AEM 6.5.22.0 sur Windows pour le serveur WebLogic JEE</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/fr/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/weblogic/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-weblogic.tar.gz">Correctif pour le pack de services AEM 6.5.22.0 sur Linux pour le serveur WebLogic JEE</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/fr/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/websphere/adobe-aem-forms-jee-hotfix-6.5.22.0-win-websphere.tar.gz">Correctif pour le pack de services AEM 6.5.22.0 sur Windows pour le serveur Webshpere JEE </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/fr/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/websphere/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-websphere.tar.gz">Correctif pour le pack de services AEM 6.5.22.0 sur Linux pour le serveur Websphere JEE </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Atténuation des vulnérabilités du framework Spring pour AEM Forms on JEE</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>10 juillet 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-jboss.zip.zip">Correctif pour le pack de services AEM 6.5.21.0 sur Windows pour le serveur JBoss JEE </a> </li>
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-jboss.tar.gz">Correctif pour AEM Service Pack 6.5.21.0 sur Linux pour JBoss JEE server </a> </li>
       <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-websphere.zip.zip">Correctif pour le pack de services AEM 6.5.21.0 sur Windows pour le serveur Webshpere JEE </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-websphere.tar.gz">Correctif pour le pack de services AEM 6.5.21.0 sur Linux pour le serveur WebSphere JEE </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-weblogic.zip.zip">Correctif pour le pack de services AEM 6.5.21.0 sur Windows pour le serveur WebLogic JEE </a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-weblogic.tar.gz">Correctif pour le pack de services AEM 6.5.21.0 sur Linux pour le serveur WebLogic JEE </a> </li>
     </ul>
     </td>
    <td>
    <ul><li>Lorsqu’une personne effectue une mise à jour vers le pack de services AEM Forms 20 (6.5.20.0) sur le serveur JEE et génère des PDF à l’aide des services Output, le rendu des PDF pose des problèmes d’accessibilité. (LC-3922112)</li><li>Les PDF balisés générés à l’aide du service Output sur AEM Forms JEE affichent un « avertissement de structure inappropriée ». (LC-3922038)</li><li>Lorsqu’un formulaire est envoyé sur AEM Forms JEE, les instances d’un élément XML répétitif sont supprimées des données. (LC-3922017)</li><li>Lorsqu’une personne utilisant un environnement Linux effectue le rendu d’un formulaire adaptatif (sur JEE) en HTML, le rendu ne s’affiche pas correctement. (LC-3921957)</li><li>Lorsqu’une personne convertit un fichier XTG au format PostScript à l’aide du service Output sur AEM Forms JEE, l’opération échoue avec l’erreur : AEM_OUT_001_003 : exception inattendue : Échec PAExecute : XFA_RENDER_FAILURE. (LC-3921720)</li><li>Après la mise à niveau vers le pack de services AEM Forms 18 (6.5.18.0) sur le serveur JEE, lorsqu’une personne envoie un formulaire, elle ne parvient pas à générer des fichiers HTML5 ou PDF Forms et XMLFM se bloque. (LC-3921718)
    </ul>
    </td>    
  </tr>
  <tr>
    <td>21 juin 2024</td>
     <td>
     <ul>
     <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&reserved=0">Correctif pour AEM Service Pack 6.5.21.0 ou AEM Forms Service Pack 6.5.22.0 sur le serveur JBoss JEE </a> </li>
      <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&reserved=0">Correctif pour AEM Service Pack 6.5.21.0 ou AEM Forms Service Pack 6.5.22.0 on Weblogic JEE server </a> </li>
       <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&reserved=0">Correctif pour AEM Service Pack 6.5.21.0 ou AEM Forms Service Pack 6.5.22.0 sur le serveur Webshpere JEE </a> </li>
        <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&reserved=0">Correctif pour AEM Service Pack 6.5.21.0 ou AEM Forms Service Pack 6.5.22.0 sur le serveur OSGi </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li> Après la mise à niveau vers AEM Forms Service Pack 6.5.21.0 ou AEM Forms Service Pack 6.5.22.0, le service PaperCapture ne parvient pas à effectuer des opérations OCR (reconnaissance optique de caractères) sur les fichiers PDF. Pour obtenir des instructions d’installation, reportez-vous à l’article <a href="/help/forms/using/papercapture-service-resolution.md"> dépannage </a> (CQDOC-21680). </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>vendredi 16 mai 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1192-010.zip">Correctif pour le pack de services 6.5.20.0 d’AEM pour Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1192-010.zip">Correctif pour le pack de services 6.5.20.0 d’AEM pour Linux</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1192-010.zip">Correctif pour le pack de services 6.5.20.0 d’AEM pour Apple macOS</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Dans un formulaire adaptatif basé sur un XDP avec des scripts intégrés sur des cases à cocher, les scripts ne sont pas exécutés pour les éléments après ces cases à cocher. Un correctif est disponible pour ce problème. (FORMS-14244) </li>
     <li> Les lignes du widget du sélecteur de date sont tronquées lors du parcours de plusieurs mois dans le widget de pop-up pour les champs suivant le modèle de modification/d’affichage. Un correctif est disponible pour ce problème. (FORMS-13620) </li>
     <li>Les envois de formulaire échouent lors de la tentative d’utilisation du service DOR (Document d’enregistrement) dans le serveur principal. Le message d’erreur rencontré est : « L’action Envoyer n’a pas pu se terminer, car la ressource de formulaire n’a pas été correctement affectée. » (FORMS-13798) </li>
     <li>Lorsqu’un formulaire adaptatif est envoyé d’une instance de publication Adobe Experience Manager vers un workflow Adobe Experience Manager, le workflow ne parvient pas à enregistrer les pièces jointes.  (FORMS-14209) </li>
     <li> Lors de l’installation du pack de services 20 d’AEM Forms 6.5 (package de modules complémentaires d’AEM Forms pour SP20), l’interface d’utilisation (IU) d’AEM Sites présente une dégradation significative des performances.  (FORMS-13791) </li>
     <li>Le service de préremplissage échoue avec une exception de pointeur nulle dans les communications interactives. (CQDOC-21355)</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>29 janvier 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fforms-foundation-qs-content-4.0.170-FORMS-12692-B0001.zip">Correctif pour le pack de services 6.5.19.0 d’AEM pour le serveur Windows on JEE</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Dans AEM Forms sur le serveur JEE, le rendu des formulaires HTML5 qui utilisent le chemin d’accès au contexte échoue. (FORMS-12485, FORMS-12691).</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>29 janvier 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-win-pkg-6.0.1016-004.zip">Correctif pour le pack de services 6.5.18.0 d’AEM pour Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-linux-pkg-6.0.1016-004.zip">Correctif pour le pack de services 6.5.18.0 d’AEM pour Linux</a></li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-osx-pkg-6.0.1016-004.zip">Correctif pour le pack de services 6.5.18.0 d’AEM pour Apple macOS</a></li> 
     </ul>
     </td>
    <td>
    <ul>
    <li> Le rendu du composant Signature tactile prêt à l’emploi échoue pour un aperçu dans un formulaire adaptatif. (FORMS-12073).</li>
    </ul>
    </td>    
   </tr>
   <tr>
    <td>mardi 20 novembre 2023</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">Correctif pour le pack de services 6.5.18.0 d’AEM pour Linux</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/fr/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">Correctif pour le pack de services 6.5.18.0 d’AEM pour Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">Correctif pour le pack de services 6.5.18.0 d’AEM pour Apple macOS</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Lorsqu’une URL de redirection est définie dans le conteneur de guide d’un formulaire adaptatif, la signature intégrée cesse de fonctionner. (FORMS-10493)</li>
    <li>Les modèles de document d’enregistrement (DoR) ne se publient pas pour les formulaires adaptatifs localisés. (FORMS-10535)</li>
    <li>La communication interactive avec les images intégrées volumineuses ne s’ouvre pas en mode d’édition. (FORMS-10578)</li>
    </ul>
    </td>    
  </tr>
  </tbody>
</table>

## Télécharger et installer un correctif OSGi {#download-install-hotfix}

Effectuez les étapes suivantes pour télécharger et installer le correctif :

1. Téléchargez le [correctif](#hotfix-for-adaptive-forms) à partir du lien Distribution logicielle.
1. Procédez à l’extraction du fichier d’archive Hotfix pour obtenir un package Experience Manager (.zip) et des fichiers de bundle (.jar).
1. Chargez et installez le package (.zip) via le [gestionnaire de modules](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager#accessing).
1. Ouvrez les bundles Configuration Manager `https://server:host/system/console/bundles`, chargez et installez le bundle (.jar). Le correctif est installé.

## Installer un correctif JEE {#download-install-jee-patch}

Pour obtenir des instructions sur l’installation d’un correctif JEE, consultez la [documentation du programme d’installation du correctif JEE d’AEM Forms](/help/release-notes/jee-patch-installer-65.md).

<!--
Retained for retrieval: hotfix entries hidden because issues are fixed in AEM Forms 6.5.25.0 or earlier.
Issues: FORMS-14521, FORMS-15428, FORMS-21378, FORMS-23789, FORMS-23802, FORMS-23875, GRANITE-63681

  <tr>
    <td>
      <strong>Feb 18, 2026</strong><br>
      <em>Applies to:</em> AEM Forms on JEE Service Pack 6.5.24.0<br>
    </td>
    <td>
    <ul>
    <strong>Jboss:</strong>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-patch/jboss/adobe-aem-forms-jee-hotfix-6.5.24.0-win-jboss.zip">Hotfix for AEM Service Pack 6.5.24.0 on Windows for JBoss JEE server</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-patch/jboss/adobe-aem-forms-jee-hotfix-6.5.24.0-linux-jboss.zip">Hotfix for AEM Service Pack 6.5.24.0 on Linux for JBoss JEE server</a></li>
    <strong>Weblogic:</strong>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-patch/weblogic/adobe-aem-forms-jee-hotfix-6.5.24.0-win-weblogic.zip">Hotfix for AEM Service Pack 6.5.24.0 on Windows for Weblogic JEE server</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-patch/weblogic/adobe-aem-forms-jee-hotfix-6.5.24.0-linux-weblogic.tar.gz">Hotfix for AEM Service Pack 6.5.24.0 on Linux for Weblogic JEE server</a></li>
    <strong>Websphere:</strong>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-patch/websphere/adobe-aem-forms-jee-hotfix-6.5.24.0-win-websphere.zip">Hotfix for AEM Service Pack 6.5.24.0 on Windows for Websphere JEE server</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-patch/websphere/adobe-aem-forms-jee-hotfix-6.5.24.0-linux-websphere.zip">Hotfix for AEM Service Pack 6.5.24.0 on Linux for Websphere JEE server</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li><b>FORMS-23789</b> Addresses Log4j-related issues in AEM Forms on JEE SP24 that caused disruptions in logging and monitoring for enterprise customers.</li>
    </ul>
    </td>
  </tr>
  <tr>
    <td>
      <strong>Feb 17, 2026</strong><br>
      <em>Applies to:</em> AEM Forms SP24<br>
    </td>
    <td>
    <ul> <a href = "https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-GRANITE-64751-SP24-1.0.zip"> AEM 6.5 Forms Hotfix</a>
    </ul>
    </td>
    <td>
    <ul>
    <li><b>GRANITE-63681</b> Form Data Model connectors may fail to authenticate because the required keywords and regex pattern are not allowed by default.</li>
    </ul>
    </td>
  </tr>
  <tr>
    <td>
      <strong>Feb 17, 2026</strong><br>
      <em>Applies to:</em> AEM Forms SP24<br>
    </td>
    <td>
    <ul>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-on-add-on/adobe-aemfd-win-pkg-6.0.1454.zip">Hotfix for AEM Forms AddOn 6.0.1454 on Windows</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-on-add-on/adobe-aemfd-linux-pkg-6.0.1454.zip">Hotfix for AEM Forms AddOn 6.0.1454 on Linux</a></li>
    <li>OSX: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-on-add-on/adobe-aemfd-osx-pkg-6.0.1454.zip">Hotfix for AEM Forms AddOn 6.0.1454 on macOS</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li><b>FORMS-23802</b> Custom functions do not work in preview or publish when the Adaptive Form is embedded in a Sites page and the aem-forms-core-component version is less than 1.1.76. This hotfix restores backward compatibility with older aem-forms-core-component versions.</li>
    </ul>
    </td>
  </tr>
  <tr>
    <td>
      <strong>Feb 10, 2026</strong><br>
      <em>Applies to:</em>  AEM Forms SP24<br>
    </td>
    <td>
    <ul> <a href = "https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bb-expressionmanager-pkg-10.0.48.zip"> AEM 6.5 Forms AddOn Hotfix</a>
    </ul>
    </td>
    <td>
    <ul>
    <li><b>FORMS-23875</b> In Form Data Model search, an HTML tag is displayed in the UI even when a relevant entity is not present.</li>
    </ul>
    </td>
  </tr>

  Sept 23, 2025 — FORMS-21378 list item:
  <li> <b>(FORMS-21378):</b> Improved form submission reliability by addressing an issue where submissions fail when Server-Side Validation (SSV) is enabled and computed Meta Info is empty.</li>

  June 21, 2024 — FORMS-14521 row:
  <tr>
    <td>June 21, 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Fccm-ccr-content-10.0.206.zip">Hotfix for AEM Service Pack 6.5.21.0 </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Draft letters with XML data are getting stuck in the loading state during preview. (FORMS-14521)</li>
    </ul>
    </td>
  </tr>

  May 16, 2024 — FORMS-15428 list item:
  <li>Configurations using the legacy cloud service for Adobe Analytics with user credential-based authentication, fail to function correctly, causing the failure of analytics rules to execute. (FORMS-15428)</li>

  ## Download and install hotfix for draft letter issue {#install-hotfix}
  To resolve FORMS-14521, perform the following steps:
  1. Download the hotfix from the Software Distribution portal.
  2. Upload and install the package (.zip) using the CRX Package Manager.
-->
