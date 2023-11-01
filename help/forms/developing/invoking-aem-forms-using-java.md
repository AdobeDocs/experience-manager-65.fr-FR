---
title: Appel d’AEM Forms à l’aide de l’API Java
description: Utilisez l’API Java AEM Forms relative au protocole de transport RMI pour l’appel à distance, le transport VM pour l’appel local, une requête SOAP pour l’appel à distance, une authentification différente, par exemple le nom d’utilisateur et le mot de passe, ainsi que des demandes d’appel synchrones et asynchrones.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
exl-id: 036c35c1-1be7-4825-bbb6-ea025e49c6f6
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '5396'
ht-degree: 48%

---

# Appel d’AEM Forms en utilisant l’API Java {#invoking-aem-forms-using-the-javaapi}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

AEM Forms peut être appelé à l’aide de l’API Java AEM Forms. Lors de l’utilisation de l’API Java AEM Forms, vous pouvez utiliser l’API d’appel ou les bibliothèques clientes Java. Les bibliothèques clientes Java sont disponibles pour les services tels que le service Rights Management. Ces API fortement typées vous permettent de développer des applications Java qui appellent AEM Forms.

Les API d’appel sont des classes situées dans le package `com.adobe.idp.dsc`. À l’aide de ces classes, vous pouvez envoyer une demande d’appel directement à un service et gérer une réponse d’appel renvoyée. Utilisez l’API d’appel pour appeler des processus de courte ou de longue durée créés à l’aide de Workbench.

Pour appeler un service par programmation, il est recommandé d’utiliser une bibliothèque cliente Java correspondant au service plutôt qu’à l’API d’appel. Par exemple, pour appeler le service Encryption, utilisez la bibliothèque cliente du service Encryption. Pour effectuer une opération du service Encryption, appelez une méthode appartenant à l’objet client du service Encryption. Vous pouvez chiffrer un document de PDF avec un mot de passe en appelant la méthode `EncryptionServiceClient` de `encryptPDFUsingPassword` .

L’API Java prend en charge les fonctionnalités suivantes :

* Protocole de transport RMI pour un appel à distance
* Transport VM pour un appel local
* SOAP pour un appel à distance
* Authentification différente, telle que le nom d’utilisateur et le mot de passe
* Demandes d’appel synchrones et asynchrones

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](#including-aem-forms-java-library-files)

[Appel de processus pour des intervenants humains de longue durée](invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Appel d’AEM Forms utilisant des services Web](/help/forms/developing/invoking-aem-forms-using-web.md)

[Réglage des propriétés de la connexion](#setting-connection-properties)

[Transmission de données vers les services AEM Forms à l’aide de l’API Java](#passing-data-to-aem-forms-services-using-the-java-api)

[Appel d’un service à l’aide d’une bibliothèque client Java](#invoking-a-service-using-a-java-client-library)

[Appel d’un processus de courte durée en utilisant l’API d’appel](#invoking-a-short-lived-process-using-the-invocation-api)

[Création d’une application Web Java qui appelle un processus pour des intervenants humains de longue durée](/help/forms/developing/invoking-human-centric-long-lived.md)

## Inclusion des fichiers de bibliothèque Java d’AEM Forms {#including-aem-forms-java-library-files}

Pour appeler par programmation un service AEM Forms à l’aide de l’API Java, incluez les fichiers de bibliothèque requis (fichiers JAR) dans le chemin d’accès aux classes de votre projet Java. Les fichiers JAR que vous incluez dans le chemin d’accès aux classes de votre application cliente dépendent de plusieurs facteurs :

* Service AEM Forms à appeler. Une application cliente peut appeler un ou plusieurs services.
* Mode dans lequel vous souhaitez appeler un service AEM Forms. Vous pouvez utiliser le mode EJB ou SOAP. (Voir [Réglage des propriétés de la connexion](invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>(Clé en main uniquement) Démarrez le serveur AEM Forms à l’aide de la commande `standalone.bat -b <Server IP> -c lc_turnkey.xml` pour spécifier une adresse IP de serveur pour EJB.

* Serveur d’applications J2EE sur lequel AEM Forms est déployé.

### Fichiers JAR spécifiques au service {#service-specific-jar-files}

Le tableau suivant répertorie les fichiers JAR requis pour appeler les services AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>File</p></th>
   <th><p>Description</p></th>
   <th><p>Emplacement</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe-livecycle-client.jar</p></td>
   <td><p>Doit toujours être inclus dans le chemin de classe d’une application cliente Java.</p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>Doit toujours être inclus dans le chemin de classe d’une application cliente Java.</p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>Doit toujours être inclus dans le chemin de classe d’une application cliente Java.</p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk//client-libs/&lt;app server=""&gt;</p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>Requis pour appeler le service Application Manager.</p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>Requis pour appeler le service Assembler. </p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>Requis pour appeler l’API du service de sauvegarde et de restauration.</p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>Requis pour appeler le service Barcoded Forms. </p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>Requis pour appeler le service Convert PDF. </p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>Requis pour appeler le service Distiller.</p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>Requis pour appeler le service DocConverter.</p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>Requis pour appeler le service Document Management.</p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>Requis pour appeler le service Encryption.</p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>Requis pour appeler le service Forms.</p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>Requis pour appeler le service Form Data Integration.</p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>Requis pour appeler le service Generate PDF.</p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>Requis pour appeler le service Generate 3D PDF.</p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>Requis pour appeler le service Job Manager. </p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>Requis pour appeler le service Output.</p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>Requis pour appeler le service PDF Utilities ou XMP Utilities.</p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>Requis pour appeler le service d’extensions Acrobat Reader DC.</p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>Requis pour appeler le service Repository.</p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/thirdparty</p></td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>adobe-rightsmanagement-client.jar</p></li>
     <li><p>namespace.jar</p></li>
     <li><p>jaxb-api.jar</p></li>
     <li><p>jaxb-impl.jar</p></li>
     <li><p>jaxb-libs.jar</p></li>
     <li><p>jaxb-xjc.jar</p></li>
     <li><p>relaxngDatatype.jar</p></li>
     <li><p>xsdlib.jar</p></li>
    </ul></td>
   <td><p>Requis pour appeler le service de Rights Management.</p><p>Si AEM Forms est déployé sur JBoss, incluez tous ces fichiers. </p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p><p>Répertoire lib spécifique à JBoss</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>Requis pour appeler le service Signature.</p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>Requis pour appeler le service Task Manager. </p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>Requis pour appeler le service Trust Store. </p></td>
   <td><p>&lt;<i>répertoire d’installation</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
 </tbody>
</table>

### Mode de connexion et fichiers JAR de l’application J2EE {#connection-mode-and-j2ee-application-jar-files}

Le tableau suivant répertorie les fichiers JAR qui dépendent du mode de connexion et du serveur d’applications J2EE sur lequel AEM Forms est déployé.

<table>
 <thead>
  <tr>
   <th><p>File</p> </th>
   <th><p>Description</p> </th>
   <th><p>Emplacement</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td>
    <ul>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
    </ul>
    <ul>
     <li>xercesImpl.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> <p> </p> </td>
   <td><p>si AEM Forms est appelé en mode SOAP, incluez ces fichiers JAR.</p> </td>
   <td><p>&lt;<em>répertoire d’installation</em>&gt;/sdk/client-libs/thirdparty</p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>Si AEM Forms est déployé sur le serveur d’applications JBoss, incluez ce fichier JAR.</p> <p>Les classes requises ne seront pas trouvées par le chargeur de classes si jboss-client.jar et les fichiers JAR référencés ne sont pas co-localisés.</p> </td>
   <td><p>Répertoire de bibliothèque cliente JBoss</p> <p>Si vous déployez votre application cliente sur le même serveur d’applications J2EE, vous n’avez pas besoin d’inclure ce fichier.</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>si AEM Forms est déployé sur BEA WebLogic Server®, incluez ce fichier JAR.</p> </td>
   <td><p>Répertoire lib spécifique à WebLogic</p> <p>Si vous déployez votre application cliente sur le même serveur d’applications J2EE, vous n’avez pas besoin d’inclure ce fichier.</p> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>com.ibm.ws.admin.client_6.1.0.jar</p> </li>
     <li><p>com.ibm.ws.webservices.thinclient_6.1.0.jar</p> </li>
    </ul> </td>
   <td>
    <ul>
     <li><p>si AEM Forms est déployé sur WebSphere Application Server, incluez ces fichiers JAR.</p> </li>
     <li><p>(com.ibm.ws.webservices.thinclient_6.1.0.jar est requis pour l’appel de service Web).</p> </li>
    </ul> </td>
   <td><p>Répertoire lib spécifique à WebSphere (<em>[WAS_HOME]</em>/runtimes)</p> <p>Si vous déployez votre application cliente sur le même serveur d’applications J2EE, vous n’avez pas à inclure ces fichiers.</p> </td>
  </tr>
 </tbody>
</table>

### Appel de scénarios {#invoking-scenarios}

Le tableau suivant indique les scénarios d’appel et répertorie les fichiers JAR requis pour appeler correctement AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>Services</p> </th>
   <th><p>Mode d’appel</p> </th>
   <th><p>Serveur d’applications J2EE</p> </th>
   <th><p>Fichiers JAR requis</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td><p>Service Forms</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss </p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar</li>
    </ul>
    <ul>
     <li>adobe-forms-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Service Forms</p> <p>Service d’extensions Acrobat Reader DC</p> <p>Service Signature</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss </p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul>
    <ul>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Service Forms</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLo gic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Service Forms</p> <p>Service d’extensions Acrobat Reader DC</p> <p>Service Signature</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLo gic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr> xmp-uti
 </tbody>
</table>

### Mise à niveau des fichiers JAR {#upgrading-jar-files}

Si vous effectuez une mise à niveau de LiveCycle vers AEM Forms, il est recommandé d’inclure les fichiers JAR AEM Forms dans le chemin de classe de votre projet Java. Par exemple, si vous utilisez des services tels que le service Rights Management, vous rencontrerez un problème de compatibilité si vous n’incluez pas les fichiers JAR AEM Forms dans le chemin de classe.

En supposant que vous effectuez une mise à niveau vers AEM Forms. Pour utiliser une application Java qui appelle le service de Rights Management, incluez les versions AEM Forms des fichiers JAR suivants :

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**Voir également**

[Appel d’AEM Forms en utilisant l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Réglage des propriétés de la connexion](invoking-aem-forms-using-java.md#setting-connection-properties)

[Transmission de données vers les services AEM Forms à l’aide de l’API Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Appel d’un service à l’aide d’une bibliothèque client Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Définir les propriétés de connexion {#setting-connection-properties}

Vous définissez les propriétés de connexion pour appeler AEM Forms lors de l’utilisation de l’API Java. Lors de la définition des propriétés de connexion, indiquez si vous souhaitez appeler des services à distance ou localement, ainsi que le mode de connexion et les valeurs d’authentification. Les valeurs d’authentification sont requises si la sécurité du service est activée. Toutefois, si la sécurité du service est désactivée, il n’est pas nécessaire de spécifier des valeurs d’authentification.

Le mode de connexion peut être SOAP ou EJB. Le mode EJB utilise le protocole RMI/IIOP et les performances du mode EJB sont meilleures que celles du mode SOAP. Le mode SOAP permet d’éliminer une dépendance du serveur d’applications J2EE ou lorsqu’un pare-feu se trouve entre AEM Forms et l’application cliente. Le mode SOAP utilise le protocole https comme transport sous-jacent et peut communiquer au-delà des limites du pare-feu. Si aucune dépendance de serveur d’applications J2EE ni aucun pare-feu ne pose problème, il est recommandé d’utiliser le mode EJB.

Pour appeler un service AEM Forms avec succès, définissez les propriétés de connexion suivantes :

* **DSC_DEFAULT_EJB_ENDPOINT :** Si vous utilisez le mode de connexion EJB, cette valeur représente l’URL du serveur d’applications J2EE sur lequel AEM Forms est déployé. Pour appeler AEM Forms à distance, spécifiez le nom du serveur d’applications J2EE sur lequel AEM Forms est déployé. Si votre application client est située sur le même serveur d’applications J2EE, vous pouvez spécifier `localhost`. Selon le serveur d’application J2EE sur lequel AEM Forms est déployé, spécifiez l’une des valeurs suivantes :

   * JBoss : `https://<ServerName>:8080 (default port)`
   * WebSphere: `iiop://<ServerName>:2809 (default port)`
   * WebLo gic: `t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**: si vous utilisez le mode de connexion SOAP, cette valeur représente le point de terminaison vers lequel une demande d’appel est envoyée. Pour appeler AEM Forms à distance, spécifiez le nom du serveur d’applications J2EE sur lequel AEM Forms est déployé. Si votre application client est située sur le même serveur d’applications J2EE, vous pouvez spécifier `localhost` (par exemple : `http://localhost:8080`.)

   * La valeur du port `8080` est applicable si l’application J2EE est JBoss. Si le serveur d’applications J2EE est IBM® WebSphere®, utilisez le port `9080`. Si le serveur d’applications J2EE est WebLogic, utilisez le port `7001`. (Ces valeurs sont des valeurs de port par défaut. Si vous modifiez la valeur de port, utilisez le numéro de port approprié.)

* **DSC_TRANSPORT_PROTOCOL** : si vous utilisez le mode de connexion EJB, spécifiez `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` pour cette valeur. Si vous utilisez le mode de connexion SOAP, spécifiez `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`.
* **DSC_SERVER_TYPE** : spécifiez le serveur d’applications J2EE sur lequel AEM Forms est déployé. Les valeurs valides sont `JBoss`, `WebSphere` et `WebLogic`.

   * Si vous définissez cette propriété de connexion sur `WebSphere`, la valeur `java.naming.factory.initial` est définie sur `com.ibm.ws.naming.util.WsnInitCtxFactory`.
   * Si vous définissez cette propriété de connexion sur `WebLogic`, la valeur `java.naming.factory.initial` est définie sur `weblogic.jndi.WLInitialContextFactory`.
   * De la même façon, si vous définissez cette propriété de connexion sur `JBoss`, la valeur `java.naming.factory.initial` est définie sur `org.jnp.interfaces.NamingContextFactory`.
   * Vous pouvez définir la propriété `java.naming.factory.initial` sur une valeur répondant à vos exigences si vous ne souhaitez pas utiliser les valeurs par défaut.

  >[!NOTE]
  >
  >Au lieu d’utiliser une chaîne pour définir la propriété de connexion `DSC_SERVER_TYPE`, vous pouvez utiliser un élément statique de la classe `ServiceClientFactoryProperties`. Les valeurs suivantes peuvent être utilisées : `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`, `ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE` ou `ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`.

* **DSC_CREDENTIAL_USERNAME :** Indique le nom d’utilisateur AEM forms. Pour qu’un utilisateur puisse appeler un service AEM Forms avec succès, il a besoin du rôle Utilisateur des services . Un utilisateur peut également disposer d’un autre rôle incluant l’autorisation Service Invoke. Dans le cas contraire, une exception est générée lorsqu’il tente d’appeler un service. Si la sécurité du service est désactivée, il n’est pas nécessaire de spécifier cette propriété de connexion.
* **DSC_CREDENTIAL_PASSWORD :** Indique la valeur de mot de passe correspondante. Si la sécurité du service est désactivée, il n’est pas nécessaire de spécifier cette propriété de connexion.
* **DSC_REQUEST_TIMEOUT :** la limite du délai d’attente de requête par défaut pour la demande SOAP est 1 200 000 millisecondes (20 minutes). Parfois, une requête peut nécessiter plus de temps pour terminer l’opération. Par exemple, une requête SOAP qui récupère un grand ensemble d’enregistrements peut nécessiter une limite de délai d’expiration plus longue. Vous pouvez utiliser le `ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT` pour augmenter la limite de délai d’appel de demande pour les requêtes SOAP.

  **Remarque** : seuls les appels basés sur SOAP prennent en charge la propriété DSC_REQUEST_TIMEOUT.

Pour définir les propriétés de connexion, effectuez les tâches suivantes :

1. Créez un objet `java.util.Properties` en utilisant son constructeur.
1. Pour définir la variable `DSC_DEFAULT_EJB_ENDPOINT` propriété de connexion, appelez la propriété `java.util.Properties` de `setProperty` et transmettez les valeurs suivantes :

   * Valeur d’énumération `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT`
   * Une valeur string qui spécifie l’URL du serveur d’applications J2EE hébergeant AEM Forms

   >[!NOTE]
   >
   >Si vous utilisez le mode de connexion SOAP, spécifiez la valeur d’énumération `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` au lieu de la valeur d’énumération `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT`.

1. Pour définir la variable `DSC_TRANSPORT_PROTOCOL` propriété de connexion, appelez la propriété `java.util.Properties` de `setProperty` et transmettez les valeurs suivantes :

   * Valeur d’énumération `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL`
   * Valeur d’énumération `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL`

   >[!NOTE]
   >
   >Si vous utilisez le mode de connexion SOAP, spécifiez la valeur d’énumération `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL` au lieu de la valeur d’énumération `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL`.

1. Pour définir la variable `DSC_SERVER_TYPE` propriété de connexion, appelez la propriété `java.util.Properties` de `setProperty` et transmettez les valeurs suivantes :

   * Valeur d’énumération `ServiceClientFactoryProperties.DSC_SERVER_TYPE`
   * Valeur string qui spécifie le serveur d’application J2EE hébergeant AEM Forms (par exemple, si AEM Forms est déployé sur JBoss, spécifiez`JBoss`).

      1. Pour définir la variable `DSC_CREDENTIAL_USERNAME` propriété de connexion, appelez la propriété `java.util.Properties` de `setProperty` et transmettez les valeurs suivantes :

   * Valeur d’énumération `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME`
   * Valeur string qui spécifie le nom d’utilisateur requis pour appeler AEM Forms

      1. Pour définir la variable `DSC_CREDENTIAL_PASSWORD` propriété de connexion, appelez la propriété `java.util.Properties` de `setProperty` et transmettez les valeurs suivantes :

   * Valeur d’énumération `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD`
   * Valeur string qui spécifie la valeur du mot de passe correspondant

**Régler le mode de connexion EJB pour JBoss**

L’exemple de code Java suivant définit les propriétés de connexion pour appeler AEM Forms déployé sur JBoss et utilisant le mode de connexion EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "https://<hostname>:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"https://<hostname>:8080");
```

**Définition du mode de connexion EJB pour WebLogic**

L’exemple de code Java suivant définit les propriétés de connexion pour appeler AEM Forms déployé sur WebLogic et utilisant le mode de connexion EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Définition du mode de connexion EJB pour WebSphere**

L’exemple de code Java suivant définit les propriétés de connexion pour appeler AEM Forms déployé sur WebSphere et à l’aide du mode de connexion EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Définition du mode de connexion SOAP**

L’exemple de code Java suivant définit les propriétés de connexion en mode SOAP pour appeler AEM Forms déployé sur JBoss.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

>[!NOTE]
>
>Si vous sélectionnez le mode de connexion SOAP, veillez à inclure des fichiers JAR supplémentaires dans le chemin de classe de votre application cliente.

**Définition des propriétés de connexion lorsque la sécurité des services est désactivée**

L’exemple de code Java suivant définit les propriétés de connexion requises pour appeler AEM Forms déployé sur le serveur d’applications JBoss et lorsque la sécurité du service est désactivée.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>Tous les didacticiels Java Quick Starts associés à la programmation avec AEM Forms affichent les paramètres de connexion EJB et SOAP.

**Définition du mode de connexion SOAP avec limite de délai d’expiration de requête personnalisée**

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT, "1800000"); // Request timeout limit 30 Minutes
```

**Utilisation d’un objet Context pour appeler AEM Forms**

Vous pouvez utiliser un objet `com.adobe.idp.Context` pour appeler un service AEM Forms avec un utilisateur authentifié (l’objet du `com.adobe.idp.Context` représente un utilisateur authentifié). Lors de l’utilisation d’un objet `com.adobe.idp.Context`, vous n’avez pas besoin de définir les propriétés `DSC_CREDENTIAL_USERNAME` ou `DSC_CREDENTIAL_PASSWORD`. Vous pouvez obtenir un `com.adobe.idp.Context` lors de l’authentification d’utilisateurs à l’aide de l’objet `AuthenticationManagerServiceClient` de `authenticate` .

La méthode `authenticate` renvoie un objet `AuthResult` contenant les résultats de l’authentification. Vous pouvez créer un objet `com.adobe.idp.Context` en appelant son constructeur. Appelez ensuite le `com.adobe.idp.Context` de `initPrincipal` et transmettez la méthode `AuthResult` , comme illustré dans le code suivant :

```java
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

Au lieu de définir la variable `DSC_CREDENTIAL_USERNAME` ou `DSC_CREDENTIAL_PASSWORD` vous pouvez appeler les propriétés `ServiceClientFactory` de `setContext` et transmettez la méthode `com.adobe.idp.Context` . Lorsque vous utilisez un utilisateur d’AEM forms pour appeler un service, assurez-vous qu’il dispose du rôle nommé `Services User` qui est requis pour appeler un service AEM Forms.

L’exemple de code suivant montre comment utiliser un objet `com.adobe.idp.Context` dans les paramètres de connexion qui sont utilisés pour créer un objet `EncryptionServiceClient`.

```java
 //Authenticate a user and use the Context object within connection settings
 // Authenticate the user
 String username = "wblue";
 String password = "password";
 AuthResult authResult = authClient.authenticate(username, password.getBytes());
 
 //Set a Content object that represents the authenticated user
 //Use the Context object to invoke the Encryption service
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
 
 //Set connection settings
 Properties connectionProps = new Properties();
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://<server>:1099");
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"jnp://<server>:1099");

 
 //Create a ServiceClientFactory object
 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 myFactory.setContext(myCtx);
 
 //Create an EncryptionServiceClient object
 EncryptionServiceClient encryptClient  = new EncryptionServiceClient(myFactory);
```

>[!NOTE]
>
>Pour plus d’informations sur l’authentification d’un utilisateur, voir [Authentification des utilisateurs](/help/forms/developing/users.md#authenticating-users).

### Appel de scénarios {#invoking_scenarios-1}

Les scénarios d’appel suivants sont abordés dans cette section :

* Une application cliente s’exécutant sur sa propre machine virtuelle Java (JVM) appelle une instance AEM Forms autonome.
* Une application cliente s’exécutant dans sa propre JVM appelle des instances AEM Forms en grappe.

### Application cliente appelant une instance AEM Forms autonome {#client-application-invoking-a-stand-alone-aem-forms-instance}

Le diagramme suivant présente une application cliente s’exécutant dans sa propre JVM et appelant une instance AEM Forms autonome.

Dans ce scénario, une application cliente s’exécute dans sa propre JVM et appelle les services AEM Forms.

>[!NOTE]
>
>Il s’agit du scénario d’appel sur lequel reposent tous les didacticiels de mise en route.

### Application cliente appelant des instances AEM Forms en grappe {#client-application-invoking-clustered-aem-forms-instances}

Le diagramme suivant montre une application client s’exécutant dans sa propre JVM et invoquant des instances d’AEM Forms situées dans un cluster.

Ce scénario est similaire à une application client appelant une instance AEM Forms autonome. Cependant, l’URL du fournisseur est différente. Si une application cliente souhaite se connecter à un serveur d’applications J2EE spécifique, l’application doit modifier l’URL pour référencer le serveur d’applications J2EE spécifique.

Il n’est pas recommandé de référencer un serveur d’applications J2EE spécifique, car la connexion entre l’application cliente et AEM Forms est arrêtée si le serveur d’applications s’arrête. Il est recommandé que l’URL du fournisseur fasse référence à un gestionnaire JNDI de niveau cellule, au lieu d’un serveur d’applications J2EE spécifique.

Les applications clientes qui utilisent le mode de connexion SOAP peuvent utiliser le port d’équilibreur de charge HTTP pour la grappe. Les applications clientes qui utilisent le mode de connexion EJB peuvent se connecter au port EJB d’un serveur d’applications J2EE spécifique. Cette action gère l’équilibrage de charge entre les noeuds de la grappe.

**WebSphere **

L’exemple suivant illustre le contenu d’un fichier jndi.properties utilisé pour se connecter à AEM Forms déployé sur WebSphere.

```ini
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**WebLo gic**

L’exemple suivant illustre le contenu d’un fichier jndi.properties utilisé pour se connecter à AEM Forms déployé sur WebLogic.

```ini
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**JBoss **

L’exemple suivant illustre le contenu d’un fichier jndi.properties utilisé pour se connecter à AEM Forms déployé sur JBoss.

```ini
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>Consultez votre administrateur pour déterminer le nom et le numéro de port du serveur d’applications J2EE.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Transmission de données vers les services AEM Forms à l’aide de l’API Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Appel d’un service à l’aide d’une bibliothèque client Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Transmettre des données vers les services AEM Forms à l’aide de l’API Java {#passing-data-to-aem-forms-services-using-the-java-api}

En règle générale, les opérations du service AEM Forms utilisent ou produisent des documents de PDF. Lorsque vous appelez un service, il est parfois nécessaire de lui transmettre un document de PDF (ou d’autres types de document tels que des données XML). De même, il est parfois nécessaire de gérer un document PDF renvoyé par le service. La classe Java qui vous permet de transmettre des données depuis et vers les services AEM Forms est `com.adobe.idp.Document`.

Les services AEM Forms n’acceptent aucun autre type de données qu’un document PDF, comme un objet `java.io.InputStream` ou un tableau d’octets. Un objet `com.adobe.idp.Document` peut également être utilisé pour transmettre d’autres types de données aux services, comme des données XML.

Un objet `com.adobe.idp.Document` est un type sérialisable Java, donc il peut être passé sur un appel RMI. Le côté récepteur peut être colocalisé (même hôte, même chargeur de classe), local (même hôte, chargeur de classe différent) ou distant (hôte différent). La transmission du contenu du document est optimisée pour chaque cas. Par exemple, si l’expéditeur et le destinataire se trouvent sur le même hôte, le contenu est transmis sur un système de fichiers local. (Dans certains cas, les documents peuvent être transmis en mémoire.)

En fonction de la taille de l’objet de `com.adobe.idp.Document`, les données sont transmises au sein de l’objet `com.adobe.idp.Document` ou stockées sur le système de fichiers du serveur. Toutes les ressources de stockage temporaires occupées par l’objet du `com.adobe.idp.Document` sont automatiquement supprimées lors de l’élimination de `com.adobe.idp.Document`. (Voir [Élimination d’objets de document](invoking-aem-forms-using-java.md#disposing-document-objects))

Parfois, il est nécessaire de connaître le type de contenu d’un objet `com.adobe.idp.Document` avant de pouvoir le transmettre à un service. Par exemple, si une opération nécessite un type de contenu spécifique, comme `application/pdf`, il est recommandé de déterminer le type de contenu. (Voir [Détermination du type de contenu d’un document](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document).)

L’objet `com.adobe.idp.Document` tente de déterminer le type de contenu en utilisant les données fournies. Si le type de contenu ne peut pas être extrait des données fournies (par exemple, lorsque les données ont été fournies sous forme de tableau d’octets), définissez le type de contenu. Pour définir le type de contenu, appelez la méthode `com.adobe.idp.Document` de `setContentType` . (Voir [Détermination du type de contenu d’un document](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document))

Si les fichiers de documentation et ressources résident sur le même système de fichiers, cela crée un objet `com.adobe.idp.Document` plus rapide. Si les fichiers de documentation et ressources résident sur des systèmes de fichiers distants, une opération de copie doit avoir lieu, ce qui affecte les performances.

Une application peut contenir à la fois les types de données `com.adobe.idp.Document` et `org.w3c.dom.Document`. Cependant, assurez-vous que vous êtes complètement admissible pour le type de données `org.w3c.dom.Document`. Pour plus d’informations sur la conversion d’un objet `org.w3c.dom.Document` à un objet `com.adobe.idp.Document`, voir le [didacticiel de mise en route (mode EJB) : Préremplissage des formulaires avec les mises en page souples à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api).

>[!NOTE]
>
>Pour éviter une fuite de mémoire dans WebLogic en utilisant l’objet `com.adobe.idp.Document`, lisez les informations de documents en blocs de 2 048 octets maximum. Par exemple, le code suivant lit les informations du document en blocs de 2 048 octets :

```java
        // Set up the chunk size to prevent a potential memory leak
        int buffSize = 2048;
 
        // Determine the total number of bytes to read
        int docLength = (int) inDoc.length();
        byte [] byteDoc = new byte[docLength];
 
        // Set up the reading position
        int pos = 0;
 
        // Loop through the document information, 2048 bytes at a time
        while (docLength > 0) {
      // Read the next chunk of information
            int toRead = Math.min(buffSize, docLength);
            int bytesRead = inDoc.read(pos, byteDoc, pos, toRead);
 
            // Handle the exception in case data retrieval failed
            if (bytesRead == -1) {
 
                inDoc.doneReading();
                inDoc.dispose();
                throw new RuntimeException("Data retrieval failed!");
 
            }
 
             // Update the reading position and number of bytes remaining
             pos += bytesRead;
             docLength -= bytesRead;
 
        }
 
        // The document information has been successfully read
        inDoc.doneReading();
        inDoc.dispose();
```

**Voir également**

[Appel d’AEM Forms en utilisant l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Réglage des propriétés de la connexion](invoking-aem-forms-using-java.md#setting-connection-properties)

### Création de documents {#creating-documents}

Créez un objet `com.adobe.idp.Document` avant d’appeler une opération de service ayant besoin d’un document PDF (ou d’autres types de documents) comme une valeur d’entrée. La classe `com.adobe.idp.Document` fournit des constructeurs qui vous permettent de créer un document à partir des types de contenu suivants :

* Tableau d’octets
* Un objet `com.adobe.idp.Document` existant.
* Un objet `java.io.File`.
* Un objet `java.io.InputStream`.
* Un objet `java.net.URL`.

#### Création d’un document basé sur un tableau d’octets {#creating-a-document-based-on-a-byte-array}

L’exemple de code suivant crée un objet `com.adobe.idp.Document` basé sur un tableau d’octets.

**Création d’un objet Document basé sur un tableau d’octets**

```java
 Document myPDFDocument = new Document(myByteArray);
```

#### Création d’un document basé sur un autre document {#creating-a-document-based-on-another-document}

L’exemple de code suivant crée un objet `com.adobe.idp.Document` basé sur un autre objet `com.adobe.idp.Document`.

**Création d’un objet Document basé sur un autre document**

```java
 //Create a Document object based on a byte array
 InputStream is = new FileInputStream("C:\\Map.pdf");
 int len = is.available();
 byte [] myByteArray = new byte[len];
 int i = 0;
 while (i < len) {
       i += is.read(myByteArray, i, len);
 }
 Document myPDFDocument = new Document(myByteArray);
 
 //Create another Document object
 Document anotherDocument = new Document(myPDFDocument);
```

#### Création d’un document à partir d’un fichier {#creating-a-document-based-on-a-file}

L’exemple de code suivant crée un objet `com.adobe.idp.Document` basé sur un fichier PDF nommé *map.pdf*. Ce fichier se trouve dans la racine du disque dur C. Ce constructeur tente de définir le type de contenu MIME de l’objet `com.adobe.idp.Document` en utilisant l’extension de nom de fichier.

Le constructeur `com.adobe.idp.Document` qui accepte l’objet `java.io.File` accepte également un paramètre Boolean. En définissant ce paramètre sur `true`, l’objet `com.adobe.idp.Document` supprime le fichier. Cette action signifie que vous n’avez pas besoin de supprimer le fichier après l’avoir passé au constructeur `com.adobe.idp.Document`.

Définir ce paramètre sur `false` signifie que vous conservez la propriété de ce fichier. Définir ce paramètre sur `true` est plus efficace. La raison est que l’objet `com.adobe.idp.Document` peut déplacer le fichier directement sur la zone gérée locale au lieu de le copier (ce qui est plus lent).

**Création d’un objet Document basé sur un fichier PDF**

```java
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### Création d’un document à partir d’un objet InputStream {#creating-a-document-based-on-an-inputstream-object}

L’exemple de code Java suivant crée un objet `com.adobe.idp.Document` basé sur un objet `java.io.InputStream`.

**Création d’un document à partir d’un objet InputStream**

```java
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### Création d’un document à partir d’un contenu accessible à partir d’une URL {#creating-a-document-based-on-content-accessible-from-an-url}

L’exemple de code Java suivant crée un objet `com.adobe.idp.Document` basé sur un fichier PDF nommé *map.pdf*. Ce fichier se trouve dans une application Web nommée `WebApp` qui s’exécute sur `localhost`. Ce constructeur tente de définir la variable `com.adobe.idp.Document` type de contenu MIME de l’objet à l’aide du type de contenu renvoyé avec le protocole URL.

L’URL fournie à l’objet `com.adobe.idp.Document` est toujours lue du côté où l’objet `com.adobe.idp.Document` original est créé, comme indiqué dans cet exemple :

```java
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

Le fichier c:/temp/input.pdf doit se trouver sur l’ordinateur client (et non sur l’ordinateur serveur). L’ordinateur client est l’emplacement de lecture de l’URL et de création de l’objet `com.adobe.idp.Document`.

**Création d’un document à partir d’un contenu accessible à partir d’une URL**

```java
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**Voir également**

[Appel d’AEM Forms en utilisant l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Réglage des propriétés de la connexion](invoking-aem-forms-using-java.md#setting-connection-properties)

### Traitement des documents retournés {#handling-returned-documents}

Les opérations de service retournant un document PDF (ou d’autres types de données telles que les données XML) comme valeur de sortie retournent l’objet `com.adobe.idp.Document`. Après avoir reçu un objet `com.adobe.idp.Document`, vous pouvez le convertir aux formats suivants :

* Un objet `java.io.File`.
* Un objet `java.io.InputStream`.
* Tableau d’octets

La ligne suivante de code convertit un objet `com.adobe.idp.Document` à un objet `java.io.InputStream`. Supposons que `myPDFDocument` représente un objet `com.adobe.idp.Document` :

```java
     java.io.InputStream resultStream = myDocument.getInputStream();
```

De même, vous pouvez copier le contenu d’un fichier `com.adobe.idp.Document` dans un fichier local en effectuant les tâches suivantes :

1. Créez un objet `java.io.File`.
1. Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` et transmettez l’objet `java.io.File`. 

L’exemple de code suivant copie le contenu d’un objet `com.adobe.idp.Document` dans un fichier nommé *AnotherMap.pdf*.

**Copie du contenu d’un objet document dans un fichier**

```java
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**Voir également**

[Appel d’AEM Forms en utilisant l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Réglage des propriétés de la connexion](invoking-aem-forms-using-java.md#setting-connection-properties)

### Détermination du type de contenu d’un document {#determining-the-content-type-of-a-document}

Déterminer le type MIME d’un `com.adobe.idp.Document` en appelant la méthode `com.adobe.idp.Document` de `getContentType` . Cette méthode renvoie une valeur string qui spécifie le type de contenu de l’objet `com.adobe.idp.Document`. Le tableau suivant décrit les différents types de contenu renvoyés par AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>Type MIME</p></th>
   <th><p>Description</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>application/pdf</code></p></td>
   <td><p>Document PDF</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xdp+xml</code></p></td>
   <td><p>XML Data Packaging (XDP), utilisé pour les formulaires XML Forms Architecture (XFA) exportés</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>Signets, pièces jointes ou autres documents XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>Format de données de formulaires (FDF), utilisé pour les formulaires Acrobat exportés</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xfdf</code></p></td>
   <td><p>Format de données de formulaires XML (XFDF), utilisé pour les formulaires Acrobat exportés</p></td>
  </tr>
  <tr>
   <td><p><code>application/rdf+xml</code></p></td>
   <td><p>Format de données enrichi et XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/octet-stream</code></p></td>
   <td><p>Format de données générique</p></td>
  </tr>
  <tr>
   <td><p><code>NULL</code></p></td>
   <td><p>Type MIME non spécifié</p></td>
  </tr>
 </tbody>
</table>

L’exemple de code suivant détermine le type de contenu d’un objet `com.adobe.idp.Document`.

**Détermination du type de contenu d’un objet Document**

```java
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**Voir également**

[Appel d’AEM Forms en utilisant l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Réglage des propriétés de la connexion](invoking-aem-forms-using-java.md#setting-connection-properties)

### Élimination d’objets de document {#disposing-document-objects}

Lorsque vous n’avez plus besoin d’un objet `Document`, il est recommandé de l’éliminer en appelant la méthode `dispose`. Chaque `Document` consomme un descripteur de fichier et jusqu’à 75 Mo d’espace RAM sur la plateforme hôte de votre application. Si un objet `Document` n’est pas éliminé, le processus de collecte de Java Garage le supprime. Toutefois, si vous l’éliminez avant en utilisant la méthode `dispose`, vous pouvez libérer la mémoire occupée par l’objet `Document`.

**Voir également**

[Appel d’AEM Forms en utilisant l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Appel d’un service à l’aide d’une bibliothèque client Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Appeler un service à l’aide d’une bibliothèque client Java {#invoking-a-service-using-a-java-client-library}

Les opérations du service AEM Forms peuvent être invoquées à l’aide de l’API fortement typée d’un service, connue sous le nom de bibliothèque client Java. A *Bibliothèque cliente Java* est un ensemble de classes concrètes qui permettent d’accéder aux services déployés dans le conteneur de services. Vous instanciez un objet Java qui représente le service à appeler au lieu de créer l’objet `InvocationRequest` en utilisant l’API d’appel. L’API d’appel est utilisée pour appeler des processus, tels que des processus de longue durée, créés dans Workbench. (Voir [Appel de processus pour des intervenants humains de longue durée](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

Pour effectuer une opération de service, appelez une méthode appartenant à l’objet Java. Une bibliothèque cliente Java contient des méthodes qui mappent généralement un à un avec les opérations de service. Lors de l’utilisation d’une bibliothèque cliente Java, définissez les propriétés de connexion requises. (Voir [Réglage des propriétés de la connexion](invoking-aem-forms-using-java.md#setting-connection-properties).)

Après avoir défini les propriétés de connexion, créez un objet `ServiceClientFactory` utilisé pour instancier un objet Java qui vous permet d’appeler un service. Chaque service qui a une bibliothèque client Java a un objet client correspondant. Par exemple, pour appeler le service Repository, créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. L’objet `ServiceClientFactory` est responsable de la gestion des paramètres de connexion nécessaires pour appeler les services AEM Forms.

Bien que l’obtention d’un objet `ServiceClientFactory` soit généralement rapide, des frais généraux sont à prévoir lorsque l’usine est utilisée pour la première fois. Cet objet est optimisé pour la réutilisation et, par conséquent, le cas échéant, utilisez le même objet `ServiceClientFactory` lorsque vous créez des objets client Java multiples. En d’autres termes, ne créez pas d’objet `ServiceClientFactory` distinct pour chaque objet de bibliothèque client que vous créez.

Un paramètre User Manager contrôle la durée de vie de l’assertion SAML qui se trouve dans l’objet `com.adobe.idp.Context` affectant l’objet `ServiceClientFactory`. Ce paramètre contrôle toutes les durées de vie du contexte d’authentification dans AEM Forms, y compris tous les appels effectués à l’aide de l’API Java. Par défaut, un objet `ServiceCleintFactory` peut être utilisé pendant une période de deux heures.

>[!NOTE]
>
>Pour expliquer comment appeler un service à l’aide de l’API Java, le `writeResource` est appelée. Cette opération place une nouvelle ressource dans le référentiel.

Vous pouvez appeler le service Repository à l’aide d’une bibliothèque cliente Java et en procédant comme suit :

1. Incluez les fichiers JAR du client, tels que adobe-repository-client.jar, dans le chemin de classe de votre projet Java. Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).
1. Définissez les propriétés de connexion requises pour appeler un service.
1. Créez un `ServiceClientFactory` en appelant la méthode `ServiceClientFactory` statique de l’objet `createInstance` et transmission de la méthode `java.util.Properties` contenant des propriétés de connexion.
1. Créez un objet `ResourceRepositoryClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. Utilisez l’objet `ResourceRepositoryClient` pour appeler les opérations du service Repository.
1. Créez un objet `RepositoryInfomodelFactoryBean` en utilisant son constructeur et transmettez-le comme `null`. Cet objet vous permet de créer un objet `Resource` qui représente le contenu ajouté au référentiel.
1. Créez un `Resource` en appelant la méthode `RepositoryInfomodelFactoryBean` de `newImage` et transmission des valeurs suivantes :

   * Une valeur ID unique en spécifiant `new Id()`.
   * Une valeur UUID unique en spécifiant `new Lid()`.
   * Nom de la ressource. Vous pouvez spécifier le nom de fichier du fichier XDP.

   Convertissez la valeur de retour en `Resource`.

1. Créez un `ResourceContent` en appelant la méthode `RepositoryInfomodelFactoryBean` de `newImage` et attribuer la valeur renvoyée à `ResourceContent`. Cet objet représente le contenu ajouté au référentiel.
1. Créez un objet `com.adobe.idp.Document` en transmettant un objet `java.io.FileInputStream` qui stocke le fichier XDP à ajouter au référentiel. (Voir [Création d’un document basé sur un objet InputStream](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object).)
1. Ajoutez le contenu de la `com.adobe.idp.Document` vers l’objet `ResourceContent` en appelant la méthode `ResourceContent` de `setDataDocument` . Transmettez l’objet `com.adobe.idp.Document`.
1. Définissez le type MIME du fichier XDP à ajouter au référentiel en appelant le `ResourceContent` de `setMimeType` méthode et transmission `application/vnd.adobe.xdp+xml`.
1. Ajoutez le contenu de la `ResourceContent` vers l’objet `Resource` en appelant la méthode `Resource` object’s `setContent` et transmission de la méthode `ResourceContent` .
1. Ajoutez une description de la ressource en appelant la fonction `Resource` object’s `setDescription` et transmettre une valeur string qui représente une description de la ressource.
1. Ajoutez la conception de formulaire au référentiel en appelant la méthode `ResourceRepositoryClient` de `writeResource` et transmission des valeurs suivantes :

   * Valeur string qui spécifie le nouveau chemin vers la collecte de ressources contenant la nouvelle ressource
   * L’objet `Resource` qui a été créé

**Voir également**

[Didacticiel de mise en route (mode EJB) : écriture d’une ressource en utilisant l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Appel d’AEM Forms en utilisant l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## Appeler un processus de courte durée en utilisant l’API d’appel {#invoking-a-short-lived-process-using-the-invocation-api}

Vous pouvez appeler un processus de courte durée à l’aide de l’API d’appel Java. Lorsque vous appelez un processus de courte durée à l’aide de l’API d’appel, vous transmettez les valeurs de paramètre requises à l’aide d’un objet `java.util.HashMap`. Pour chaque paramètre à transmettre à un service, appelez la méthode `java.util.HashMap` de `put` et spécifiez la paire nom-valeur requise par le service pour effectuer l’opération spécifiée. Indiquez le nom exact des paramètres appartenant au processus de courte durée.

>[!NOTE]
>
>Pour plus d’informations sur l’appel d’un processus de longue durée, voir [Appel de processus pour des intervenants humains de longue durée](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

La discussion ici porte sur l’utilisation de l’API d’appel pour appeler le processus de courte durée AEM Forms suivant, nommé `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Ce processus n’est pas basé sur un processus AEM Forms existant. Pour suivre l’exemple de code, créez un processus désigné par `MyApplication/EncryptDocument` à l’aide de Workbench. (Voir [Utilisation de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63_fr).)

Lorsque ce processus est appelé, il effectue les actions suivantes :

1. Obtient le document de PDF non sécurisé transmis au processus. Cette action est basée sur l’opération `SetValue`. Le paramètre d’entrée pour ce processus est une variable de processus `document` désignée par `inDoc`.
1. Chiffrement du document PDF avec un mot de passe. Cette action est basée sur l’opération `PasswordEncryptPDF`. Le document PDF chiffré avec un mot de passe est retourné dans une variable de processus nommée `outDoc`.

### Appelez le processus de courte durée MyApplication/EncryptDocument à l’aide de l’API d’appel Java {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

Appelez le processus de courte durée `MyApplication/EncryptDocument` à l’aide de l’API d’appel Java :

1. Incluez les fichiers JAR client, tels que adobe-livecycle-client.jar, dans le chemin de classe de votre projet Java. (Voir [Inclusion des fichiers de bibliothèque Java AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)
1. Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](invoking-aem-forms-using-java.md#setting-connection-properties).)
1. Créez un objet `ServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. Un objet `ServiceClient` vous permet d’appeler une opération de service. Il gère des tâches telles que la localisation, la répartition et le routage des demandes d’appel.
1. Créez un objet `java.util.HashMap` en utilisant son constructeur.
1. Appeler la variable `java.util.HashMap` de `put` pour chaque paramètre d’entrée à transmettre au processus de longue durée. Vu que le processus de courte durée `MyApplication/EncryptDocument` nécessite un paramètre d’entrée de type `Document`, il suffit d’appeler la méthode `put` une fois, comme le montre l’exemple suivant.

   ```java
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. Créez un `InvocationRequest` en appelant la méthode `ServiceClientFactory` de `createInvocationRequest` et transmission des valeurs suivantes :

   * Valeur string qui spécifie le nom du processus de longue durée à appeler. Pour appeler le processus `MyApplication/EncryptDocument`, spécifiez `MyApplication/EncryptDocument`.
   * Une valeur string qui représente le nom de l’opération de processus. En général, le nom d’une opération de processus de courte durée est `invoke`.
   * L’objet `java.util.HashMap` qui contient les valeurs de paramètre requises par l’opération de service.
   * Une valeur Boolean définie sur `true` qui crée une demande synchrone (cette valeur est applicable pour appeler un processus de courte durée).

1. Envoyez la demande d’appel au service en appelant la fonction `ServiceClient` de `invoke` et transmission de la méthode `InvocationRequest` . La méthode `invoke` renvoie un objet `InvocationReponse`.

   >[!NOTE]
   >
   >Un processus de longue durée peut être appelé en transmettant la valeur `false` en tant que quatrième paramètre de la méthode `createInvocationRequest`. La transmission de la valeur `false`*crée une requête asynchrone.*

1. Récupérez la valeur renvoyée par le processus en appelant la variable `InvocationReponse` de `getOutputParameter` et transmettre une valeur string qui spécifie le nom du paramètre de sortie. Dans cette situation, spécifiez `outDoc` (`outDoc` est le nom du paramètre de sortie pour le processus `MyApplication/EncryptDocument`). Convertissez la valeur de retour en `Document`, comme le montre l’exemple suivant.

   ```java
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .pdf.
1. Appeler la variable `com.adobe.idp.Document` de `copyToFile` pour copier le contenu de la méthode `com.adobe.idp.Document` vers le fichier . Assurez-vous d’utiliser l’objet `com.adobe.idp.Document` qui a été retourné par la méthode `getOutputParameter`.

**Voir également**

[Didacticiel de mise en route : appel d’un processus de courte durée en utilisant l’API d’appel](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[Appel de processus pour des intervenants humains de longue durée](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
