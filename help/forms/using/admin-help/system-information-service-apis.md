---
title: API du service d’informations système
description: Ce document contient des informations détaillées sur les API fournies par le service d’information sur le système.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 4da96c8f-8bd0-4cad-9087-18e324f084e7
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 100%

---

# API du service d’information système {#system-information-service-apis}

Le service d’informations système fournit un ensemble d’API REST pour récupérer des informations. Le tableau suivant fournit des informations détaillées sur les API :

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
   <td><p>https://'[server]:[port]'/rest/services/SystemInfo.properties'</p></td>
   <td><p>Cette API est un wrapper pour l’API Java <a href="https://docs.oracle.com/javase/6/docs/api/java/lang/System.html#getProperties()">system.getProperties</a>. Elle récupère la configuration de l’environnement de travail actuel. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.envVar</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.envVar</p></td>
   <td><p>Récupère toutes les variables d’environnement du système d’exploitation hôte. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.logs</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.logs</p></td>
   <td><p>Télécharge un fichier zip contenant les journaux du serveur d’applications. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.config</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.config</p></td>
   <td><p>Récupère tout le contenu du fichier config.xml. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.services</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.services</p></td>
   <td><p>Récupère le statut et les paramètres de configuration des services d’AEM Forms.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.vitalDetails</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.vitalDetails</p></td>
   <td><p>Récupère le temps de disponibilité du serveur, les arguments JVM, la mémoire système, la taille du tas, le nom du système d’exploitation, le nombre de threads actifs et le nombre de threads. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.coreSettings</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.coreSettings</p></td>
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
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.database</p></td>
   <td><p>Récupère des informations détaillées sur la base de données.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.licenseInfo</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.licenseInfo</p></td>
   <td><p>Récupère les informations de version et de licence des composants AEM Forms installés. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfNo.serverConfig</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.serverConfig</p></td>
   <td><p>Télécharge les fichiers de configuration du serveur d’applications hôte. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>Récupère le nombre et la trace de pile des threads actifs. Accepte les paramètres suivants :</p>
    <ul>
     <li><p>iterations= [n] : spécifie le nombre d’itérations. Remplacez n par un nombre. </p></li>
     <li><p>Delay= [n] : spécifie le nombre de millisecondes à attendre avant de commencer la prochaine itération. </p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.info</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.info</p></td>
   <td><p>Cette API est un wrapper pour toutes les API de service d’informations système. En interne, il exécute toutes les API d’informations système et télécharge les informations au format ZIP. </p><p><i><strong>Remarque</strong> : l’API SystemInfo.info n’indique ni le nombre ni la trace de la pile des threads actifs. </i></p></td>
  </tr>
 </tbody>
</table>
