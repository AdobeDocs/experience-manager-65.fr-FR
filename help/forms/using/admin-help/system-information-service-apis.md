---
title: API du service d’informations système
seo-title: API du service d’informations système
description: Ce  fournit des informations détaillées sur les API fournies par le de système.
seo-description: Ce  fournit des informations détaillées sur les API fournies par le de système.
uuid: 7f624216-56e6-4d49-b9a1-3c9af045dabe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 79fccce2-d090-4b50-9c58-3f2a00e651b2
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# API du service d’informations système {#system-information-service-apis}

Le service d’informations système fournit un ensemble d’API REST pour récupérer les informations. Le tableau suivant fournit des informations détaillées sur les API :

<table>
 <thead>
  <tr>
   <th><p>Nom</p></th>
   <th><p>URL</p></th>
   <th><p>Description</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>SystemInfo.properties</p></td>
   <td><p>https://'[serveur]:[port]'/rest/services/SystemInfo.properties`</p></td>
   <td><p>Cette API est un wrapper pour l’API Java <a href="https://docs.oracle.com/javase/6/docs/api/java/lang/System.html#getProperties()">system.getProperties</a>. Elle récupère la configuration de l’environnement de travail actif. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.envVar</p></td>
   <td><p>https://'[serveur]:[port]'/rest/services/ SystemInfo.envVar</p></td>
   <td><p>Récupère toutes les variables d’environnement du système d’exploitation hôte. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.logs</p></td>
   <td><p>https://'[serveur]:[port]'/rest/services/ SystemInfo.logs</p></td>
   <td><p>Télécharge un fichier ZIP contenant les journaux du serveur d’applications. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.config</p></td>
   <td><p>https://'[serveur]:[port]'/rest/services/ SystemInfo.config</p></td>
   <td><p>Récupère tout le contenu du fichier config.xml. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.services</p></td>
   <td><p>https://'[serveur]:[port]'/rest/services/ SystemInfo.services</p></td>
   <td><p>Récupère l’état et les paramètres de configuration des services AEM Forms.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.vitalDetails</p></td>
   <td><p>https://'[serveur]:[port]'/rest/services/ SystemInfo.vitalDetails</p></td>
   <td><p>Récupère la durée de fonctionnement du serveur, l’argument JVM, la mémoire du système, la taille de tas, le nom du système d’exploitation, le nombre de threads actifs et le nombre de threads. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.coreSettings</p></td>
   <td><p>https://'[serveur]:[port]'/rest/services/ SystemInfo.coreSettings</p></td>
   <td><p>Récupère les valeurs des propriétés suivantes :</p>
    <ul>
     <li><p>AdobeTempDir</p></li>
     <li><p>AdobeServerFontDir</p></li>
     <li><p>CustomerFontDir</p></li>
     <li><p>GlobalDocumentStorageRootDir</p></li>
     <li><p>DefaultDocumentMaxInlineSize</p></li>
     <li><p>DefaultDocumentDisposalTimeout</p></li>
     <li><p>EnableDocumentDBStorage</p></li>
     <li><p>GlobalDocumentStorageUseNetworkShare</p></li>
     <li><p>EnableFIPS</p></li>
     <li><p>EnableWSDL</p></li>
     <li><p>DataServicesConfigFile </p></li>
     <li><p>EnableRDS</p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.database</p></td>
   <td><p>https://'[serveur]:[port]'/rest/services/ SystemInfo.database</p></td>
   <td><p>Récupère des informations détaillées sur la base de données.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.licenseInfo</p></td>
   <td><p>https://'[serveur]:[port]'/rest/services/ SystemInfo.licenseInfo</p></td>
   <td><p>Récupère les informations de version et de licence des composants d’AEM Forms installés. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfNo.serverConfig</p></td>
   <td><p>https://'[serveur]:[port]'/rest/services/ SystemInfo.serverConfig</p></td>
   <td><p>Télécharge les fichiers de configuration du serveur d’applications hôte. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>https://'[serveur]:[port]'/rest/services/ SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>Récupère le nombre et la trace de la pile des threads actifs. Accepte les paramètres suivants :</p>
    <ul>
     <li><p>iterations= [n] : spécifie le nombre d’itérations, où n est un nombre. </p></li>
     <li><p>Delay= [n] : indique le nombre de millisecondes avant le début de la prochaine itération. </p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.info</p></td>
   <td><p>https://'[serveur]:[port]'/rest/services/ SystemInfo.info</p></td>
   <td><p>Cette API est un wrapper de toutes les API du service d’informations système. En interne, elle exécute toutes les API d’informations système et télécharge les informations au format .zip. </p><p><i><strong>Remarque</strong> : l’API SystemInfo.info n’indique ni le nombre ni la trace de la pile des threads actifs. </i></p></td>
  </tr>
 </tbody>
</table>

