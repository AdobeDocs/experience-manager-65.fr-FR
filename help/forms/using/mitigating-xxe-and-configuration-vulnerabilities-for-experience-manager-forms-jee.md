---
title: Atténuation des vulnérabilités liées aux XXE, à la configuration du mode de développement de Struts et à l’exécution de code à distance pour AEM Forms sur JEE
description: Atténuation des vulnérabilités XXE, de configuration et d’exécution de code à distance pour AEM Forms sur JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 9fade12f-a038-4fd6-8767-1c30966574c5
solution: Experience Manager, Experience Manager Forms
release-date: 2025-08-05T00:00:00Z
source-git-commit: 3f64cfa688ef1f0090b7ce0d821324593cbea693
workflow-type: ht
source-wordcount: '675'
ht-degree: 100%

---

# Atténuation de l’exécution de code à distance (CVE-2025-49533), de la configuration du mode de développement Struts (CVE-2025-54253), des XXE (CVE-2025-54254) et des vulnérabilités pour AEM Forms sur JEE {#mitigating-xxe-configuration-rce-vulnerabilities-aem-forms}

## Référence rapide

| **Niveau d’impact** | **Versions affectées** | **Action recommandée** |
|---|---|---|
| **Critique** | AEM 6.5 Forms sur JEE pack de services 23 (6.5.23.0) | [Installez le dernier correctif](#option-1-for-users-on-version-65230-install-latest-hotfix) |
| **Critique** | AEM 6.5 Forms sur JEE packs de services 18 à 22 (6.5.18.0 - 6.5.22.0) | [Installez manuellement les correctifs](#option-2-for-users-on-65180---65220-manual-hotfix-installation) |
| **Critique** | AEM 6.5 Forms sur JEE Pack de services 17 (6.5.17.0) ou version antérieure | Mettez à niveau vers une version de pack de services prise en charge, puis appliquez les étapes d’atténuation recommandées pour votre nouvelle version |
| **Non affecté** | AEM Forms sur OSGi, Workbench, Cloud Service | Aucune action n’est requise. |

**Vulnérabilités corrigées :**

- Exécution du code à distance (CVE-2025-49533)
- Problèmes de sécurité de la configuration (CVE-2025-54253)
- Traitement d’une entité externe XML (XXE) (CVE-2025-54254)

## Vue d’ensemble

### Éléments affectés

| Vulnérabilité | Impact | Composants affectés |
|---|---|---|
| **CVE-2025-49533** : exécution de code à distance | Exécution de code non authentifié dans GetDocumentServlet | AEM 6.5 Forms sur JEE Pack de services 23 (6.5.23.0) et versions antérieures |
| **CVE-2025-54253** : problèmes de configuration | Mode de développement Struts activé dans l’interface d’administration | AEM 6.5 Forms sur JEE Pack de services 23 (6.5.23.0) et versions antérieures |
| **CVE-2025-54254** : traitement d’une XXE | Le module Document Security autorise un accès non autorisé aux fichiers. | AEM 6.5 Forms sur JEE Pack de services 23 (6.5.23.0) et versions antérieures |


### Éléments non affectés

- Workbench Experience Manager Forms (toutes les versions)
- Experience Manager Forms sur OSGi (toutes les versions)
- Experience Manager Forms as a Cloud Service

## Options de résolution


### Avant de commencer

Avant d’apporter toute modification, effectuez une sauvegarde du fichier EAR ou DSC que vous allez modifier ou mettre à jour :

- Recherchez le fichier EAR ou DSC d’origine dans votre répertoire de déploiement.
- Copiez le fichier vers un emplacement de sauvegarde sécurisé en dehors du répertoire de déploiement.
- Vérifiez que la sauvegarde est terminée et accessible avant de procéder aux mises à jour.

Cette précaution vous permet d’effectuer une restauration à l’état d’origine en cas de problème lors du processus de mise à jour.

### Option 1 : (pour les utilisateurs et les utilisatrices de la version 6.5.23.0) installez le correctif le plus récent

1. [Téléchargez le correctif pour 6.5.23.0](/help/release-notes/aem-forms-hotfix.md).
1. Suivez les [instructions d’installation standard du correctif](/help/release-notes/jee-patch-installer-65.md).
1. Si vous utilisez Document Security (anciennement Rights Management) sur IBM WebSphere ou Oracle WebLogic, définissez la propriété système Java suivante (argument JVM) avant de démarrer le serveur AEM Forms :

   ```
   -Dcom.adobe.forms.jee.services.allowDoctypeDeclaration=true
   ```

1. Redémarrez le serveur d’applications.

### Option 2 : (pour les utilisateurs et les utilisatrices de la version 6.5.18.0 - 6.5.22.0) Installation manuelle du correctif

+++Installation manuelle du correctif pour 6.5.18.0 via 6.5.22.0

**Étape 1 : téléchargez et extrayez le package du correctif**

- Téléchargez le [correctif pour 6.5.18.0 - 6.5.22.](/help/release-notes/aem-forms-hotfix.md) à partir du portail de distribution de logiciels Adobe.
- Extrayez-le localement

**Étape 2 : accédez au dossier de version approprié**

- En fonction de la version du pack de services installée sur votre environnement, accédez au dossier correspondant.

  Par exemple, pour le pack de services 20, le dossier est :

  ```
  <extracted-hotfix>/SP20/
  ```

**Étape 3 : recherchez le répertoire de déploiement**

- Sur votre serveur AEM Forms sur JEE, accédez à :

  ```
  [AEM installation directory]/deploy
  ```

  Exemple : `adobe/adobe-experience-manager-forms/deploy`



**Étape 4 : mettez à jour et remplacez les fichiers EAR**

>[!BEGINTABS]

>[!TAB JBoss]

1. Ouvrez `adobe-core-jboss.ear` et remplacez `adminui.war` par

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adminui.war
   ```

   Par exemple, `adobe-xxe-configuration-hotfix/SP20/jboss/adminui.war`.

1. Dans `adobe-core-jboss.ear`, accédez au dossier `lib/` et remplacez `adobe-uisupport.jar` par :

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   Par exemple, `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`.

1. Enregistrez le EAR. Vérifiez que les modifications sont correctement enregistrées.


1. Remplacez `adobe-edcserver-jboss.ear` par

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adobe-edcserver-jboss.ear
   ```

   Par exemple, `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-edcserver-jboss.ear`.

1. Remplacez `adobe-forms-jboss.ear` par

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adobe-forms-jboss.ear
   ```

   Par exemple, `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-forms-jboss.ear`.



>[!TAB WebLogic]

1. Ouvrez `adobe-core-weblogic.ear` et remplacez `adminui.war` par

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adminui.war
   ```

   Par exemple, `adobe-xxe-configuration-hotfix/SP20/weblogic/adminui.war`.

1. Dans `adobe-core-weblogic.ear`, remplacez `adobe-uisupport.jar` par :

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   Par exemple, `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`.

1. Enregistrez le EAR. Vérifiez que les modifications sont correctement enregistrées.


1. Remplacez `adobe-edcserver-weblogic.ear` par

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adobe-edcserver-weblogic.ear
   ```

   Par exemple, `adobe-xxe-configuration-hotfix/SP20/weblogic/adobe-edcserver-weblogic.ear`.

1. Remplacez `adobe-forms-weblogic.ear` par

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adobe-forms-weblogic.ear
   ```

   Par exemple, `adobe-xxe-configuration-hotfix/SP20/weblogic/adobe-forms-weblogic.ear`.

>[!TAB WebSphere]

1. Ouvrez `adobe-core-websphere.ear` et remplacez `adminui.war` par

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adminui.war
   ```

   Par exemple, `adobe-xxe-configuration-hotfix/SP20/websphere/adminui.war`.

1. Dans `adobe-core-websphere.ear`, remplacez `adobe-uisupport.jar` par :

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   Par exemple, `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`.

1. Enregistrez le EAR. Vérifiez que les modifications sont correctement enregistrées.


1. Remplacez `adobe-edcserver-websphere.ear` par

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adobe-edcserver-websphere.ear
   ```

   Par exemple, `adobe-xxe-configuration-hotfix/SP20/websphere/adobe-edcserver-websphere.ear`.

1. Remplacez `adobe-forms-websphere.ear` par

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adobe-forms-websphere.ear
   ```

   Par exemple, `adobe-xxe-configuration-hotfix/SP20/websphere/adobe-forms-websphere.ear`.

>[!ENDTABS]



**Étape 5 : mettez à jour le fichier `adobe-rightsmanagement-<appserver>-dsc.jar`avec**

```
adobe-xxe-configuration-hotfix/SP[version]/<appserver>/adobe-rightsmanagement-<appserver>-dsc.jar
```

Par exemple, `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-rightsmanagement-jboss-dsc.jar`.

**Étape 6 : configuration supplémentaire pour Document Security sur WebSphere et WebLogic** :

Si vous utilisez Document Security (anciennement Rights Management), définissez la propriété système Java suivante (argument JVM) avant de démarrer le serveur AEM Forms :

```
-Dcom.adobe.forms.jee.services.allowDoctypeDeclaration=true
```


**Étape 7 : réexécutez le gestionnaire de configuration**

- Lancez le gestionnaire de configuration pour redéployer le fichier EAR mis à jour et appliquer le correctif.

+++

### Option 3 : (pour les utilisateurs et les utilisatrices de la version 6.5.17.0 et versions antérieures) chemin de mise à niveau

1. [Mettez à niveau vers une version de pack de services prise en charge.](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)
1. Suivez les options 1 ou 2 ci-dessus en fonction de votre nouvelle version.

## Références

- [CWE-611 : restriction incorrecte de la référence d’entité externe XML](https://cwe.mitre.org/data/definitions/611.html)
- [CWE-16 : configuration](https://cwe.mitre.org/data/definitions/16.html)
- [Aide-mémoire OWASP sur la prévention des XXE](https://owasp.org/www-community/vulnerabilities/XML_External_Entity_XXE_Processing)
- [Bonnes pratiques de sécurité pour Adobe Experience Manager Forms](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=fr)