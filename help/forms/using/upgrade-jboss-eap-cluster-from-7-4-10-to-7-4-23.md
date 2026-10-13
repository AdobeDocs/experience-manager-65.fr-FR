---
title: Mise à niveau du cluster JBoss EAP de la version 7.4.10 vers la version 7.4.23 pour AEM Forms on JEE
description: Étapes supplémentaires pour mettre à niveau un cluster EAP JBoss de la version 7.4.10 vers la version 7.4.23 pour AEM Forms on JEE.
SEO Description: Additional cluster upgrade steps for JBoss EAP 7.4.10 to 7.4.23 on AEM Forms on JEE.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
exl-id: 2c9e7f41-a8d6-4b03-8e5c-1a4f6d9e0b72
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms Upgrade,AEM Forms on JEE
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: d49d6117-dd89-469c-a774-cc96b7eee433
    internal-label: Administration
subfeature_v2:
  - id: b9cdd520-e7a7-4af9-a95f-296f28882b69
    internal-label: AEM Forms upgrade
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 1%
---
# Mise à niveau du cluster JBoss EAP de la version 7.4.10 vers la version 7.4.23 pour AEM Forms on JEE {#upgrade-jboss-eap-cluster-from-7-4-10-to-7-4-23}

## Vue d’ensemble {#overview}

Lorsque vous mettez à niveau un cluster JBoss EAP de la version 7.4.10 vers la version 7.4.23 pour AEM Forms on JEE, une configuration supplémentaire est requise au-delà des étapes de mise à niveau autonomes. Les paramètres spécifiques au cluster, tels que les localisateurs de cache, l’authentification maître-esclave, les liaisons hôte et la configuration du contrôleur de domaine, doivent être mis à jour lors de la nouvelle installation de JBoss.

## Application {#applies-to}

Cet article s’applique aux éléments suivants :

* AEM Forms on JEE s’exécutant sur JBoss EAP 7.4.10 dans un environnement de cluster
* Configurations JBoss EAP Principal-esclave sous Windows et Linux

## Conditions préalables {#prerequisites}

Effectuez toutes les étapes de la [Mise à niveau de JBoss EAP de la version 7.4.10 vers la version 7.4.23 pour AEM Forms sur JEE](/help/forms/using/upgrade-jboss-eap-from-7-4-10-to-7-4-23.md), y compris la copie de l’URL de connexion, du nom d’utilisateur et du mot de passe de l’installation existante vers les nouveaux fichiers de configuration.

## Étapes {#steps}

Effectuez les étapes supplémentaires suivantes spécifiques au cluster :

### Mettre à jour domain.conf.bat {#update-domain-conf-bat}

1. Dans votre `domain.conf.bat`, ajoutez les informations de localisation de votre configuration existante au nouveau fichier :

   ```text
   set "JAVA_OPTS=%JAVA_OPTS% -Doak.documentMK.maxServerTimeDiffMillis=-1"
   set "JAVA_OPTS=%JAVA_OPTS% -Dadobe.cache.cluster-locators=<ip-address-master>[22345],<ip-address-slave>[22345]"
   set "JAVA_OPTS=%JAVA_OPTS% -DentityExpansionLimit=10000"
   ```

### Configurer l’authentification maître-esclave {#configure-master-slave-authentication}

1. Créez un nouvel utilisateur pour l’authentification maître-esclave sur le nœud maître.
1. Sur les nœuds esclaves, mettez à jour le mot de passe utilisateur dans `host.xml` :

   ```xml
   <server-identities>
       <secret value="Y2hhbmdlaXQ="/>
   </server-identities>
   ```

### Mise à jour des adresses IP dans host.xml {#update-ip-addresses-in-host-xml}

1. Mettez à jour les adresses IP pour les nœuds maîtres et esclaves dans `host.xml` :

   ```xml
   <interfaces>
       <interface name="management">
           <inet-address value="${jboss.bind.address.management:<ip-address>}"/>
       </interface>
       <interface name="public">
           <inet-address value="${jboss.bind.address:<ip-address>}"/>
       </interface>
   </interfaces>
   ```

### Supprimer les déploiements de la configuration de domaine {#remove-deployments-from-domain-configuration}

1. Assurez-vous qu’il n’existe aucune section `<deployments>` dans le nouveau fichier `domain_<db>.xml`.
1. Ne copiez pas le bloc suivant à partir de la configuration existante :

   ```xml
   <deployments>
       <deployment name="adobe-forms-ivs-jboss.ear" runtime-name="adobe-forms-ivs-jboss.ear"/>
       <deployment name="adobe-livecycle-cq-author.ear" runtime-name="adobe-livecycle-cq-author.ear"/>
       <deployment name="adobe-livecycle-jboss.ear" runtime-name="adobe-livecycle-jboss.ear"/>
       <deployment name="adobe-livecycle-native-jboss-x86_win32.ear" runtime-name="adobe-livecycle-native-jboss-x86_win32.ear"/>
       <deployment name="adobe-livecycle-native-jboss-x86_win64.ear" runtime-name="adobe-livecycle-native-jboss-x86_win64.ear"/>
       <deployment name="adobe-output-ivs-jboss.ear" runtime-name="adobe-output-ivs-jboss.ear"/>
       <deployment name="adobe-workspace-client.ear" runtime-name="adobe-workspace-client.ear"/>
   </deployments>
   ```

### Mise à jour de la classe de pilote dans la configuration de domaine {#update-driver-class-in-domain-configuration}

1. Mettez à jour la section de classe de pilote dans `domain_<db>.xml` en fonction de votre moteur de base de données :

   **MSSQL:**

   ```xml
   <xa-datasource-class>com.microsoft.sqlserver.jdbc.SQLServerXADataSource</xa-datasource-class>
   ```

   **Oracle:**

   ```xml
   <xa-datasource-class>oracle.jdbc.xa.client.OracleXADataSource</xa-datasource-class>
   ```

### Mettre à jour le contrôleur de domaine sur les nœuds esclaves {#update-domain-controller-on-slave-nodes}

1. Mettez à jour le bloc de contrôleur de domaine sur le nœud esclave en `host.xml` avec l&#39;adresse IP principale, le port `9999`, le nom d&#39;utilisateur `slave1` et le domaine `ManagementRealm` :

   ```xml
   <remote host="<ip-address>" port="9999" username="slave1" realm="ManagementRealm"/>
   ```

### Mettre à jour jboss-cli.xml {#update-jboss-cli-xml}

1. Mettez à jour l’entrée `<host>` dans `jboss-cli.xml` sur les nœuds maître et esclave.
