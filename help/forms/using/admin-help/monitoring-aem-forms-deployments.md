---
title: Surveiller les déploiements d’AEM Forms
seo-title: Monitoring AEM forms deployments
description: Vous pouvez surveiller les déploiements d’AEM Forms, tant au niveau du système qu’au niveau interne. Ce document vous permet d’en savoir plus sur la surveillance des déploiements d’AEM Forms.
seo-description: You can monitor AEM forms deployments from both a system level and an internal level. Learn more about monitoring AEM forms deployments from this document.
uuid: 032b7a93-3069-4ad5-a8c6-4c160f290669
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b3e7bca0-5aaf-4f28-bddb-fd7e8ed72ee8
exl-id: 931e8095-5c7c-4c1f-b95b-75ac2827d4f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '605'
ht-degree: 100%

---

# Surveiller les déploiements d’AEM Forms {#monitoring-aem-forms-deployments}

Vous pouvez surveiller les déploiements d’AEM Forms, tant au niveau du système qu’au niveau interne. Utilisez pour cela des outils de gestion spécialisés tels que HP OpenView, IBM Tivoli et CA UniCenter, ainsi qu’un moniteur JMX tiers appelé *JConsole* et tout particulièrement dédié au contrôle de l’activité Java. L’implémentation d’une stratégie de surveillance améliore la disponibilité, la fiabilité et les performances des déploiements d’AEM Forms.

Pour plus d’informations sur la surveillance des déploiements d’AEM Forms, voir le[ Guide technique pour la surveillance des déploiements d’AEM Forms](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf).

## Contrôle via les MBeans {#monitoring-using-mbeans}

AEM forms propose deux MBeans qui fournissent des informations de navigation et des statistiques. Il s’agit des seuls MBeans pris en charge au niveau de l’intégration et de l’inspection :

* **ServiceStatistic :** ce MBean fournit des informations sur le nom du service et sur sa version.
* **OperationStatistic :** ce MBean fournit les statistiques de chaque service du serveur Forms. C’est là que les administrateurs peuvent obtenir des informations sur un service donné, par exemple l’heure d’appel, le nombre d’erreurs, etc.

### Interfaces publiques de ServiceStatisticMbean {#servicestatisticmbean-public-interfaces}

Vous pouvez accéder à ces interfaces publiques du MBean ServiceStatistic à des fins de test :

```java
 public String getServiceId();
 public int getMajorVersion();
 public int getMinorVersion();
```

### Interfaces publiques de OperationStatisticMbean {#operationstatisticmbean-public-interfaces}

Vous pouvez accéder à ces interfaces publiques du MBean OperationStatistic à des fins de test :

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

### Arborescence des MBeans et statistiques sur les opérations {#mbean-tree-operation-statistics}

Vous pouvez accéder aux statistiques du MBean OperationStatistic depuis une console JMX (JConsole). Ces statistiques sont des attributs de MBean et vous pouvez les parcourir dans l’arborescence suivante :

**Arborescence de MBean**

**Nom de domaine Adobe :** dépend du serveur d’applications. Si celui-ci ne définit pas le domaine, la valeur par défaut sera adobe.com.

**ServiceType :** AdobeService est le nom utilisé pour répertorier tous les services.

**AdobeServiceName :** nom ou identifiant du service.

**Version :** version du service.

**Statistiques des opérations**

**Durée d’appel :** durée de l’exécution de la méthode. Cette valeur ne comprend pas le temps de sérialisation de la demande, de transfert du client vers le serveur et de désérialisation.

**Nombre d’appels :** nombre de fois où le service a été appelé.

**Durée moyenne d’appel :** durée moyenne de tous les appels qui ont été exécutés depuis le démarrage du serveur.

**Durée maximale d’appel :** durée de l’appel le plus long qui a été exécuté depuis le démarrage du serveur.

**Durée minimale d’appel :** durée de l’appel le plus court qui a été exécuté depuis le démarrage du serveur.

**Nombre d’exceptions :** nombre d’échecs d’appel.

**Message d’erreur :** message d’erreur de la dernière exception survenue.

**Heure du dernier échantillonnage :** date du dernier appel.

**Unité de temps :** la valeur par défaut est la milliseconde.

Pour activer le contrôle JMX, les serveurs d’applications ont généralement besoin d’être configurés. Veuillez consulter la documentation de votre serveur d’applications pour obtenir des informations détaillées.

### Exemples de configuration d’un accès JMX ouvert {#examples-of-how-to-set-up-open-jmx-access}

**JBoss 4.0.3/4.2.0 - configuration du démarrage de la JVM**

Pour afficher les MBeans depuis JConsole, vous devez configurer les paramètres de démarrage de la JVM du serveur d’applications JBoss. Assurez-vous que JBoss est démarré depuis le fichier run.bat/sh.

1. Modifiez le fichier run.bat situé sous InstallJBoss/bin.
1. Recherchez la ligne JAVA_OPTS et ajoutez le code suivant :

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

**WebLogic 9.2 /10 - configuration du démarrage de la JVM**

1. Modifiez le fichier startWebLogic.bat se trouvant sous `[WebLogic home]/user_projects/domains/Adobe_Live_Cycle/bin`.
1. Recherchez la ligne JAVA_OPTS et ajoutez le code suivant :

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

1. Redémarrez WebLogic.

>[!NOTE]
>
>pour WebLogic, vous pouvez accéder au MBean à distance ou via IIOP.

**Accès à distance au MBean**

1. Lancez JConsole pour établir une nouvelle connexion et cliquez sur l’onglet Remote.
1. Entrez le nom d’hôte et le port (9088, le nombre spécifié dans les options de démarrage de la JVM).

**WebSphere 6.1 - configuration du démarrage de la JVM**

1. Dans la console d’administration (Serveur d’applications > server1 > Process Definition > JVM), ajoutez la ligne suivante dans le champ correspondant à Generic JVM Argument :

   ```shell
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. Ajoutez les trois lignes suivantes (ou annulez leur mise en commentaires) dans le fichier /opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.properties (ou &lt;Votre JRE WebSphere>/lib/management/management.properties) :

   ```shell
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect
    com.sun.management.jmxremote.authenticate=false
    com.sun.management.jmxremote.ssl=false
   ```

1. Redémarrez WebSphere.
