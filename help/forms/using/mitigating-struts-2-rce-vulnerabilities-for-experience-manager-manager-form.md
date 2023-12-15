---
title: Réduction des vulnérabilités de Struts 2 RCE pour Experience Manager Forms
description: Réduction des vulnérabilités de Struts 2 RCE pour Experience Manager Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
source-git-commit: e35f7a683928b7de7ab0b02e6aa3401eeccacd95
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 1%

---


# Réduction des vulnérabilités de Struts 2 RCE pour Experience Manager Forms {#mitigatin-struts2-rce-vulnerabilities-for-aem-forms}

## Problème

Des vulnérabilités de sécurité critiques ont été signalées pour Struts 2 RCE, un framework d’applications web populaire et open source pour le développement d’applications web Java EE. Les vulnérabilités suivantes ont été analysées :

| Vulnérabilité | Qu&#39;est-ce qui est impacté ? | Qu&#39;est-ce qui n&#39;a pas d&#39;impact ? |
|---|---|---|
| [CVE-2023-50164](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2023-50164) | Experience Manager 6.5 Forms on JEE (toutes les versions de 6.5 GA à 6.5.19.0) | <ul><li> Experience Manager Forms Workbench (toutes versions)</li> <li> Experience Manager Forms sur OSGi (toutes les versions) </li> <li> Experience Manager Forms as a Cloud Service </li> <ul> |

## Résolution

Le tableau suivant répertorie la résolution pour toutes les versions affectées :

| Version | Version actuelle | Action de l’utilisateur |
|---|---|---|
| Experience Manager 6.5 Forms on JEE | 6.5.19.0 | [Installation du dernier Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=fr) |
| Experience Manager 6.5 Forms on JEE | 6.5.13.0 - 6.5.18.0 | Utilisez l’une des méthodes suivantes : <ul><li>  <a href="https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=fr"> Installation du dernier Service Pack </a> </li> <li> <a href ="#use-manual-mitigation-steps"> Utilisation des étapes de limitation manuelles </a> |
| Experience Manager 6.5 Forms on JEE | 6.5 - 6.5.12.0 | [Installation du dernier Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=fr)  </br> </br> **REMARQUE :** AEM Forms prend actuellement en charge les versions 6.5.13.0 à 6.5.19.0. Si vous utilisez une ancienne version, nous vous recommandons de mettre à niveau vers la version 6.5.13.0 ou une version ultérieure. Pour obtenir des instructions sur l’installation d’AEM version 6.5.13.0 ou ultérieure, voir les notes de mise à jour. |

### Utilisation des étapes de limitation manuelles {#use-manual-mitigation-steps}

Vous pouvez utiliser les étapes de limitation manuelle pour résoudre le problème sur AEM 6.5 Form Server exécutant le Service Pack 13 vers AEM 6.5 Form Server exécutant le Service Pack 18 (6.5.13.0 - 6.5.18.0) :

1. Arrêtez toutes les instances de serveur et tous les localisateurs.
1. Téléchargez la [struts-core 2.5.33 jar](https://repo1.maven.org/maven2/org/apache/struts/struts2-core/2.5.33/struts2-core-2.5.33.jar).
1. Téléchargez l’outil de correction manuelle d’AEM Forms on JEE depuis [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/patch_utility/archive-patcher-1.0.0.zip).
1. Décompressez l’archive manuelle de l’outil de correction. Il extrait les fichiers suivants :
   * archive-patcher-1.0.0.jar
   * patch-archive.bat
   * patch-archive.sh
1. Ouvrez la fenêtre du terminal et accédez au dossier contenant les fichiers extraits.
1. Utilisez l’outil de correction manuelle pour rechercher, répertorier et remplacer tous les fichiers JAR de struts2. Pour rechercher et remplacer le fichier jar struts2-core-2.5.30 et struts2-core.jar :


>[!BEGINTABS]

>[!TAB Windows]

1. Exécutez la commande suivante pour répertorier tous les fichiers jar struts2. Avant d’exécuter la commande, remplacez le chemin d’accès de la commande ci-dessus par celui de votre serveur de formulaires AEM :

       &quot;javascript
       
       patch-archive.bat -root=C:\Adobe\Adobe_Experience_Manager_Forms\...\export -pattern=.*struts2-core-2.5.30.jar$
       
       &quot;
   
1. Exécutez les commandes suivantes dans l’ordre indiqué pour le remplacement récursif statique. Avant d’exécuter la commande Remplacez le chemin d’accès de la commande ci-dessus par le chemin d’accès de votre serveur de formulaires AEM et par le chemin d’accès `struts2-core-2.5.33.jar` fichier .


       &quot;javascript
       
       patch-archive.bat -root=C:\Adobe\Adobe_Experience_Manager_Forms\...\export -pattern=.*struts2-core-2.5.30.jar$ -action=replace C:\temp\struts2-core-2.5.33.jar
       
       
       patch-archive.bat -root=C:\Users\labuser\Desktop\check -pattern=.*struts2-core.jar$ -action=replace C:\Users\labuser\Desktop\struts2-core.jar -action=replace C:\Users\labuser\Desktop\struts2-core.jar
       
       
       &quot;
   
1. Démarrez votre serveur AEM Forms.


>[!TAB Linux]

1. Exécutez la commande suivante pour répertorier tous les fichiers jar struts2. Avant d’exécuter la commande, remplacez le chemin d’accès de la commande ci-dessus par celui de votre serveur de formulaires AEM :

       &quot;javascript
       
       patch-archive.sh -root=\Users\labuser\Adobe\Adobe_Experience_Manager_Forms\...\export -pattern=.*struts2-core-2.5.30.jar$
       
       &quot;
   
1. Exécutez les commandes suivantes dans l’ordre indiqué pour le remplacement récursif statique. Avant d’exécuter la commande Remplacez le chemin d’accès de la commande ci-dessus par le chemin d’accès de votre serveur de formulaires AEM et par le chemin d’accès `struts2-core-2.5.33.jar` fichier .

       &quot;javascript
       
       patch-archive.sh -root=\Users\labuser\Adobe\Adobe_Experience_Manager_Forms\...\export -pattern=.*struts2-core-2.5.30.jar$ -action=replace \temp\struts2-core-2.5.33.jar
       
       
       patch-archive.sh -root=\Users\labuser\Desktop\check -pattern=.*struts2-core.jar$ -action=replace \Users\labuser\Desktop\struts2-core.jar -action=replace \Users\labuser\Desktop\struts2-core.jar
       
       &quot;
   
1. Démarrez votre serveur AEM Forms.

>[!ENDTABS]




<!-- 
### Manual patching tool 


>[!BEGINTABS]

>[!TAB Windows]

    ```
    
    patch-archive.bat [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.

>[!TAB macOS]

    ```
    
    patch-archive.sh [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.  

>[!TAB Linux]

    ```
    
    patch-archive.sh [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.  



>[!ENDTABS]









-->