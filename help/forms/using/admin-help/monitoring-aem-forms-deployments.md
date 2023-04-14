---
title: Surveiller les déploiements d’AEM Forms
seo-title: Monitoring AEM forms deployments
description: Vous pouvez surveiller les déploiements d’AEM forms au niveau du système et au niveau interne. Pour en savoir plus sur la surveillance des déploiements d’AEM forms, consultez ce document.
seo-description: You can monitor AEM forms deployments from both a system level and an internal level. Learn more about monitoring AEM forms deployments from this document.
uuid: 032b7a93-3069-4ad5-a8c6-4c160f290669
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b3e7bca0-5aaf-4f28-bddb-fd7e8ed72ee8
exl-id: 931e8095-5c7c-4c1f-b95b-75ac2827d4f3
source-git-commit: c47b4dcfd2fbdcb0b98ad815f5b04d8f593e4f64
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 30%

---

# Surveiller les déploiements d’AEM Forms {#monitoring-aem-forms-deployments}

Vous pouvez surveiller les déploiements d’AEM forms au niveau du système et au niveau interne. Vous pouvez utiliser des outils de gestion spécialisés tels que HP OpenView, IBM® Tivoli et CA UniCenter, ainsi qu’un moniteur JMX tiers appelé *JConsole* pour surveiller spécifiquement l’activité Java™. L’implémentation d’une stratégie de surveillance améliore la disponibilité, la fiabilité et les performances des déploiements d’AEM forms.

<!-- For more information about monitoring AEM forms deployments, see [A technical guide for monitoring AEM forms deployments](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf). This URL is 404. No suitable replacement URL was found after a search. Do not make this link live if it is dead! -->

## Surveillance à l’aide des MBeans {#monitoring-using-mbeans}

AEM Forms fournit deux MBeans enregistrés qui fournissent des informations de navigation et de statistiques. Ces parties sont les seuls MBeans pris en charge pour l’intégration et l’inspection :

* **ServiceStatistic :** ce MBean fournit des informations sur le nom du service et sur sa version.
* **OperationStatistic :** Ce MBean fournit les statistiques de chaque service de serveur AEM Forms. Ce MBean permet aux administrateurs d’obtenir des informations sur un service particulier, comme l’heure d’appel et le nombre d’erreurs.

### Interfaces publiques de ServiceStatisticMbean {#servicestatisticmbean-public-interfaces}

Vous pouvez accéder à ces interfaces publiques du MBean ServiceStatistic à des fins de test :

```java
 public String getServiceId();
 public int getMajorVersion();
 public int getMinorVersion();
```

### Interfaces publiques de OperationStatisticMbean {#operationstatisticmbean-public-interfaces}

Vous pouvez accéder à ces interfaces publiques du MBean OperationStatistic à des fins de test :

```java
 // InvocationCount: The number of times the method is invoked.
 public long getInvocationCount();
 // InvocationStartTime: The time at which the method started to execute.
 public long getInvocationStartTime();
 // InvocationEndTime: The time at which the method finished execution.
 public long getInvocationEndTime();
 // InvocationTime: The time taken for the execution of the method.
 public long getInvocationTime();
 // LastSamplingDateTime: Convert InvocationStartTime to a formatted string
 public String getLastSamplingDateTime();
 // MaxInvocationTime: The maximum time taken for the execution of the method.
 public long getMaxInvocationTime();
 // MinInvocationTime: The minimum time taken for the execution of the method.
 public long getMinInvocationTime();
 // AverageInvocationTime: the averege execution time taken for the execution of the method.
 public double getAverageInvocationTime();
 // ExceptionCount: The number of times the method has thrown an Exception.
 public long getExceptionCount();
 // ExceptionMessage: The message of the last exception occurred.
 public String getExeptionMessage();
 public void setExceptionMessage(String errorMessage);
```

### Arborescence de MBean et statistiques des opérations {#mbean-tree-operation-statistics}

À l’aide d’une console JMX (JConsole), les statistiques du MBean OperationStatistic sont disponibles. Ces statistiques sont des attributs de MBean et peuvent être naviguées sous l’arborescence suivante :

**Arborescence MBean**

**Nom de domaine Adobe :** dépend du serveur d’applications. Si celui-ci ne définit pas le domaine, la valeur par défaut sera adobe.com.

**ServiceType :** AdobeService est le nom utilisé pour répertorier tous les services.

**AdobeServiceName :** nom ou identifiant du service.

**Version :** version du service.

**Statistiques des opérations**

**Durée d’appel :** durée de l’exécution de la méthode. Cette invocation n’inclut pas le moment où la requête est sérialisée, transférée du client au serveur et désérialisée.

**Nombre d’appels :** nombre de fois où le service a été appelé.

**Durée moyenne d’appel :** durée moyenne de tous les appels qui ont été exécutés depuis le démarrage du serveur.

**Durée maximale d’appel :** durée de l’appel le plus long qui a été exécuté depuis le démarrage du serveur.

**Durée minimale d’appel :** durée de l’appel le plus court qui a été exécuté depuis le démarrage du serveur.

**Nombre d’exceptions :** nombre d’échecs d’appel.

**Message d’erreur :** message d’erreur de la dernière exception survenue.

**Heure du dernier échantillonnage :** date du dernier appel.

**Unité de temps :** la valeur par défaut est la milliseconde.

Pour activer la surveillance JMX, les serveurs d’applications ont généralement besoin d’une configuration. Consultez la documentation de votre serveur d’applications pour plus d’informations.

### Exemples de configuration de l’accès JMX ouvert {#examples-of-how-to-set-up-open-jmx-access}

**JBoss® 4.0.3/4.2.0 - configuration du démarrage de la JVM**

Pour afficher les MBeans à partir de JConsole, configurez les paramètres de démarrage de la JVM du serveur d’applications JBoss. Assurez-vous que JBoss est démarré à partir du fichier run.bat/sh.

1. Modifiez le fichier run.bat situé sous InstallJBoss/bin.
1. Recherchez la ligne JAVA_OPTS et ajoutez les éléments suivants :

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

**WebLogic 9.2 /10 - configuration du démarrage de la JVM**

1. Modifiez le fichier startWebLogic.bat se trouvant sous `[WebLogic home]/user_projects/domains/Adobe_Live_Cycle/bin`.
1. Recherchez la ligne JAVA_OPTS et ajoutez les éléments suivants :

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

1. Redémarrez WebLogic.

>[!NOTE]
>
>Pour WebLogic, vous pouvez accéder au MBean à distance ou IIOP.

**Accès à distance au MBean**

1. Lancez JConsole pour une nouvelle connexion et cliquez sur l’onglet distant.
1. Saisissez le nom d’hôte et le port (9088, le numéro que vous indiquez lors des options de démarrage de la JVM).

**WebSphere® 6.1 - configuration du démarrage de la JVM**

1. Sur le Admin Console (Serveur d’applications > server1 > Process Definition > JVM), ajoutez la ligne suivante dans le champ pour Generic JVM Argument :

   ```shell
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. Ajoutez ou annulez la mise en commentaire des trois lignes suivantes dans le fichier /opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.properties (ou &lt;your websphere=&quot;&quot; jre=&quot;&quot;>/ lib/management/management.properties) :

   ```shell
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect
    com.sun.management.jmxremote.authenticate=false
    com.sun.management.jmxremote.ssl=false
   ```

1. Redémarrez WebSphere.
