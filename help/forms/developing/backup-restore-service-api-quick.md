---
title: Démarrage rapide de l’API du service de sauvegarde et de restauration
seo-title: Backup and Restore Service APIQuick Starts
description: Démarrage rapide de l’API du service de sauvegarde et de restauration
uuid: c3992be2-ceb4-480d-9c8f-71eb0ea66dde
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 813162be-dbf5-4dc1-80ff-e37dbc25ef60
role: Developer
exl-id: ae17fd3a-0ba4-4a00-907b-811e500b0e14
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 100%

---

# Démarrage rapide de l’API du service de sauvegarde et de restauration {#backup-and-restore-service-apiquick-starts}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Le démarrage rapide de l’API Java (SOAP) est disponible pour l’API du service de sauvegarde et de restauration.

[Démarrage rapide : passer en mode de sauvegarde à l’aide de l’API Java (SOAP)](backup-restore-service-api-quick.md#quick-start-soap-mode-entering-backup-mode-using-the-java-api)

[Démarrage rapide : quitter le mode de sauvegarde à l’aide de l’API Java (SOAP)](backup-restore-service-api-quick.md#quick-start-soap-mode-leaving-backup-mode-using-the-java-api)

Les opérations AEM Forms peuvent être effectuées à l’aide de l’API fortement typée d’AEM Forms et le mode de connexion doit être défini sur SOAP.

>[!NOTE]
>
>Les tutoriels de démarrage rapide situés dans Programmer avec AEM Forms sont basés sur le système d’exploitation Forms. Toutefois, si vous utilisez un autre système dʼexploitation, tel quʼUNIX, remplacez les emplacements spécifiques à Windows par des emplacements pris en charge par le système dʼexploitation utilisé. De même, si vous utilisez un autre serveur d’applications J2EE, veillez à spécifier des propriétés de connexion valides. Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## Démarrage rapide (mode SOAP) : passer en mode de sauvegarde à l’aide de l’API Java {#quick-start-soap-mode-entering-backup-mode-using-the-java-api}

L’exemple de code Java suivant passe en mode de sauvegarde avec un libellé unique pendant deux heures. Une fois le délai de sauvegarde expiré ou si le mode de sauvegarde est explicitement quitté, le serveur Forms revient à la purge des fichiers du stockage global de documents. (Voir [Activer le mode de sauvegarde sur le serveur Forms](/help/forms/developing/preparing-aem-forms-backup.md#entering-backup-mode-on-the-forms-server).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-backup-restore-client-sdk.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.Properties;
 
 import com.adobe.idp.backup.dsc.client.BackupServiceClient;
 import com.adobe.idp.backup.dsc.service.BackupModeEntryResult;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class BackupRestoreEnter
 {
     public static void main(String[] args)
     {
         try
         {
             // Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,"administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create a BackupService client object
             BackupServiceClient backup = new BackupServiceClient(myFactory);
 
             // Specify a generic label, 120 minutes to perform the backup,
             // and not to provide continous backup mode coverage (used for snapshot backups)
             String backUpLabel = new String("Snapshot2008July01");
             int minsInBackupMode = 120;
             boolean continousCoverage = false;
 
 
             // Enter backup mode on the forms server server
             BackupModeEntryResult backupResult = backup.enterBackupMode(backUpLabel,minsInBackupMode, continousCoverage);
 
             // Get information from entering backup mode ontheforms server server.
             if (backupResult != null)
             {
                 System.out.println("Start time is: " + backupResult.getStartTime());
                 System.out.println("Backup Current ID is: " + backupResult.getId());
                 System.out.println("Backup Previous ID is: " + backupResult.getPreviousReservationId());
                 System.out.println("Backup Label is: " + backupResult.getLabel());
                 System.out.println("Backup Time to complete is: " + backupResult.getReservationTimeout());
             }
             else
             {
                 System.out.println("Could not enter backup mode.");
             }
 
         }
         catch (Exception e)
         {
             e.printStackTrace();
         }
         return;
     }
 }
 
```

## Démarrage rapide (mode SOAP) : quitter le mode de sauvegarde à l’aide de l’API Java {#quick-start-soap-mode-leaving-backup-mode-using-the-java-api}

L’exemple de code Java suivant amène de façon explicite le serveur Forms à quitter le mode de sauvegarde et à revenir à la purge des fichiers du stockage global de documents. (Voir [Quitter le mode de sauvegarde sur le serveur Forms](/help/forms/developing/preparing-aem-forms-backup.md#leaving-backup-mode-on-the-forms-server).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-backup-restore-client-sdk.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.Properties;
 
 import com.adobe.idp.backup.dsc.client.BackupServiceClient;
 import com.adobe.idp.backup.dsc.service.BackupModeResult;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class BackupRestoreLeave
 {
 
     public static void main(String[] args)
     {
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'server':`port`");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,"administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create a BackupService object
             BackupServiceClient backup = new BackupServiceClient(myFactory);
 
             // Leave backup mode on the forms server
             BackupModeResult leaveBackupResult = backup.leaveBackupMode();
 
             //Get result information from leaving backup mode
             if (leaveBackupResult != null)
             {
                 System.out.println("Backup Mode ID is : " + leaveBackupResult.getId());
             }
             else
             {
                 System.out.println("Forms server is not in backup mode.");
             }
 
         }
         catch (Exception e)
         {
             e.printStackTrace();
         }
         return;
     }
 }
 
```
