---
title: Correctifs pour AEM Forms
description: Fournit des informations sur la manière de télécharger et d’installer un correctif pour AEM Forms.
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '1987'
ht-degree: 91%

---

# Correctifs Adobe Experience Manager Forms{#aem-form-hotfix}

Cet article répertorie les correctifs critiques mis en œuvre pour résoudre les problèmes connus, améliorer la stabilité du système et optimiser les performances globales d’AEM Forms.

>[!NOTE]
>
> Les correctifs sont conçus pour être cumulatifs, c’est-à-dire qu’ils englobent tous les correctifs précédents. Ainsi, lorsque vous appliquez le dernier correctif à une version, il résout non seulement le problème le plus récent, mais incorpore également tous les correctifs et améliorations antérieurs.

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
      <strong>14 octobre 2025</strong><br>
      <em>Application :</em> échec d’ImgToPdf avec AEM Forms SP23 Jboss<br>
    </td>
    <td>
    <ul> Pour toute résolution, contactez l’assistance technique d’Adobe Experience Manager Forms <a href="https://business.adobe.com/in/support/main.html"></a>
    </ul>
    </td>
    <td>
    <ul>
    <li> <b>(FORMS-22029) :</b> améliore la fiabilité de la conversion PDF en résolvant un problème où PDF Generator (PDFG) ne parvient pas à convertir les fichiers image en PDF après la mise à niveau vers SP23, ce qui entraîne des erreurs de post-traitement inattendues.
      <ul>
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
    <li> <b>(FORMS-21378) :</b> amélioration de la fiabilité de l’envoi des formulaires en résolvant un problème où les envois échouent lorsque la validation côté serveur (SSV) est activée et que les informations de Meta calculées sont vides.

<li> <b>(FORMS-21721) :</b> amélioration d’un problème en raison duquel les conversions PS vers PDF et HTML vers PDF (WebKit) échouent après le déploiement du correctif (publié le 5 <b> août 2025</b>) pour 6.5.23.0. 
    </li>
    </ul>
    </td>    
  </tr>
    </ul>
    </td>
  <tr>
    <td>
      <strong>5 août 2025</strong><br>
<em>S’applique à :</em> AEM 6.5 Forms Pack de services 23<br>
<em>Instructions de configuration :</em>
<a href="/help/forms/using/mitigating-xxe-and-configuration-vulnerabilities-for-experience-manager-forms-jee.md#option-1-for-users-on-version-65230-install-latest-hotfix">
Réduire les vulnérabilités XXE, de configuration et d’exécution de code à distance (CVE-2025-49533) pour AEM Forms sur JEE
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
      <strong>5 août 2025</strong><br>
      <em>S’applique à :</em> AEM 6.5 Forms Packs de services 18 - 22<br>
      <em>Instructions de configuration :</em>
      <a href="/help/forms/using/mitigating-xxe-and-configuration-vulnerabilities-for-experience-manager-forms-jee.md#option-2-for-users-on-65180---65220-manual-hotfix-installation">
        Installation manuelle du correctif pour les packs de services 18-22
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
        <li><strong>FORMS-20360 :</strong> après la mise à niveau vers le pack de services 6.5.23.0 d’AEM Forms, le service de conversion ImageToPDF échoue avec l’erreur suivante : <br>
        <code>17:15:44,468 ERROR [com.adobe.pdfg.GeneratePDFImpl] (default task-49) ALC-PDG-001-000-ALC-PDG-011-028-Error occurred while converting the input image file to PDF. com/adobe/internal/pdftoolkit/core/encryption/EncryptionImp</code><br>
        Pour résoudre ce problème, vous pouvez télécharger et installer le correctif.</li>
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
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-jboss.tar.gz">Correctif pour le pack de services AEM 6.5.21.0 sur Linux pour le serveur JBoss JEE </a> </li>
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
     <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Correctif pour AEM Service Pack 6.5.21.0 ou AEM Forms Service Pack 6.5.22.0 sur le serveur JBoss JEE </a> </li>
      <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Correctif pour AEM Service Pack 6.5.21.0 ou AEM Forms Service Pack 6.5.22.0 on Weblogic JEE server </a> </li>
       <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Correctif pour AEM Service Pack 6.5.21.0 ou AEM Forms Service Pack 6.5.22.0 sur le serveur Webshpere JEE </a> </li>
        <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Correctif pour AEM Service Pack 6.5.21.0 ou AEM Forms Service Pack 6.5.22.0 sur le serveur OSGi </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li> Après la mise à niveau vers AEM Forms Service Pack 6.5.21.0 ou AEM Forms Service Pack 6.5.22.0, le service PaperCapture ne parvient pas à effectuer des opérations OCR (reconnaissance optique de caractères) sur les fichiers PDF. Pour obtenir des instructions sur l’installation, reportez-vous à l’article dépannage <a href="/help/forms/using/papercapture-service-resolution.md"></a>.(CQDOC-21680) </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>21 juin 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/fr/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Fccm-ccr-content-10.0.206.zip">Correctif pour le pack de services AEM 6.5.21.0 </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Les brouillons de lettres contenant des données XML sont bloqués à l’état de chargement lors de la prévisualisation. Pour les instructions de téléchargement et d’installation du correctif, reportez-vous à la section <a href="#install-hotfix">Télécharger et installer le correctif pour le problème de brouillon de lettre</a>.(FORMS-14521)</li>
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
     <li>Les configurations qui utilisent le service cloud hérité pour Adobe Analytics avec une authentification basée sur les informations d’identification de l’utilisateur ou de l’utilisatrice ne fonctionnent pas correctement, ce qui entraîne l’échec de l’exécution des règles d’analyse. (FORMS-15428)
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
  <tbody>
</table>

## Télécharger et installer un correctif OSGi {#download-install-hotfix}

Effectuez les étapes suivantes pour télécharger et installer le correctif :

1. Téléchargez le [correctif](#hotfix-for-adaptive-forms) à partir du lien Distribution logicielle.
1. Procédez à l’extraction du fichier d’archive Hotfix pour obtenir un package Experience Manager (.zip) et des fichiers de lot (.jar).
1. Chargez et installez le package (.zip) via le [gestionnaire de modules](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager#accessing).
1. Ouvrez les lots Configuration Manager `https://server:host/system/console/bundles`, chargez et installez le lot (.jar). Le correctif est installé.

## Installer un correctif JEE {#download-install-jee-patch}

Pour obtenir des instructions sur l’installation d’un correctif JEE, consultez la [documentation du programme d’installation du correctif JEE d’AEM Forms](/help/release-notes/jee-patch-installer-65.md).


## Télécharger et installer le correctif pour le problème de brouillon de lettre {#install-hotfix}

Pour résoudre le problème, procédez comme suit :

1. Téléchargez le [correctif](#hotfix-for-adaptive-forms) à partir du portail de distribution logicielle.
2. Chargez et installez le package (.zip) via le [gestionnaire de modules CRX](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager#accessing).
