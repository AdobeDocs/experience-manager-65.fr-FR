---
title: Problèmes connus
description: Notes de mise à jour spécifiques aux problèmes connus dans Adobe Experience Manager 6.5
uuid: 8fbdb167-833a-4179-aad1-0a26a4e5b3a7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: d11fc727-f23a-4cde-9fa6-97e2c81b4ad0
docset: aem65
translation-type: tm+mt
source-git-commit: 0a55ed44cb7fe3320b2196df38fe8492ee03912d
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 58%

---


# Problèmes connus {#known-issues}

Cette page contient la liste des problèmes connus dans la version Adobe Experience Manager 6.5 qui a été publiée en avril 2019.

[Contactez l’assistance](https://helpx.adobe.com/fr/support/experience-manager.html) si vous avez besoin d’informations supplémentaires sur les problèmes connus.

## Plate-forme {#platform}

* Un problème est signalé lorsque CRX-Quickstart et son contenu sont supprimés.

   Pour chacune de ces actions, veillez à ce que la propriété &quot;*htmllibmanager.fileSystemOutputCacheLocation*&quot; ne soit jamais une chaîne vide :

   1. Appel à &quot;*/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true*&quot;.
   2. Mise à niveau vers AEM 6.5.
   3. Exécution de la &quot;migration de contenu différée&quot; sur AEM 6.5.

   Un article de la Base [de](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) connaissances est disponible avec des détails supplémentaires et la solution à ce problème.

* Si vous utilisez JDK 11 avec l’instance AEM 6.5, certaines pages peuvent s’afficher comme vides après le déploiement de certains packs. Le message d’erreur suivant s’affiche dans le fichier journal :

   ```
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

Pour résoudre cette erreur :

1. Désactivez l’instance AEM. Accédez à `<aem_server_path_on_server>crx-quickstart\conf` et ouvrez le `sling.properties` fichier. Adobe recommande de sauvegarder ce fichier.

2. Recherchez `org.osgi.framework.bootdelegation=`. Ajoutez `jdk.internal.reflect,jdk.internal.reflect.*` les propriétés pour afficher le résultat comme suit :

   ```
   org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
   ```

3. Enregistrez le fichier et redémarrez l’instance AEM.

## Ressources {#assets}

* **Rechercher :** La recherche n’entraîne aucune valeur renvoyée si la chaîne de recherche contient des espaces de début ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786)).
* **Schéma de métadonnées des dossiers** : après l’ajout d’un bouton de choix, les champs ID et Valeur ne sont pas restitués comme prévu et la fonctionnalité de suppression ne fonctionne pas. (CQ-4261144)
* Lors de l’attribution d’un nouveau nom à une ressource, il n’est pas possible d’utiliser un espace dans le nom. (CQ-4266403)

## Formulaires {#forms}

* Lorsque AEM Forms est installé sous un système d’exploitation Linux, la signature numérique avec le module de sécurité matérielle ne fonctionne pas. (CQ-4266721)
* (AEM Forms sur WebSphere uniquement) L’option **Forms Workflow**> **Recherche de tâche** ne renvoie aucun résultat si vous recherchez un **Administrateur** avec un **Nom d’utilisateur** comme critère de recherche. (CQ-4266457)

* AEM Forms ne parvient pas à convertir les fichiers .tif et .tiff avec la compression JPEG en documents PDF. (CQ-4265972)
* Les options **Analyseur de ressources AEM Forms** et **Migration de la correspondance vers la communication interactive** ne fonctionnent pas sur la page **Migration d’AEM Forms**. (CQ-4266572)

* (JBoss 7 uniquement) Lorsque vous effectuez une mise à niveau d’une version précédente vers AEM Forms 6.5 et que la version précédente contenait des processus (.lca) qui ont créé et utilisé une copie du processus d’envoi ou de rendu par défaut, les formulaires HTML5 utilisant ces processus (.lca) ne parviennent pas à exécuter les actions requises. (CQ-4243928)
* Dans une version adaptative, lorsqu’un service de modèle de données de formulaire est appelé à partir de l’éditeur de règle pour mettre à jour de manière dynamique les valeurs du composant de choix d’image, les valeurs du composant de choix d’image ne sont pas mises à jour. (CQ-4254754)
* AEM Forms Designer installer requires the 32-bit version of [Visual C++ redistributable runtime package 2012](https://support.microsoft.com/en-in/help/2977003/the-latest-supported-visual-c-downloads) and [Visual C++ redistributable runtime packages 2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Assurez-vous que les packages d’exécution redistribuables susmentionnés sont installés avant de démarrer l’installation. (CQ-4265668)

* PDF Generator ne prend pas en charge l’authentification par carte à puce.  Lorsqu’un administrateur active la stratégie de groupe `Interactive Logon: Require Smart card` sur un serveur Windows, tous les utilisateurs existants de PDF Generator sont invalidés.

* Lorsqu’un formulaire adaptatif est configuré pour mettre à jour de manière dynamique les valeurs d’un composant et que l’instance de publication hébergeant le formulaire est accessible via le dispatcher, la fonctionnalité permettant de mettre à jour de manière dynamique les valeurs d’un champ cesse de fonctionner. Pour résoudre le problème, ouvrez CRXDE sur l’instance de publication, accédez à /libs/fd/af/runtime/clientlibs/guideChartReduce et créez la propriété répertoriée ci-dessous. 

   * Nom : allowProxy
   * Type : booléen
   * Valeur : vraie
   * Protégé : faux
   * Obligatoire : faux
   * Multiple : faux
   * Créé automatiquement : faux 

   La propriété permet aux bibliothèques clientes du dossier d’exécution d’accéder aux mandataires. (CQ-4268679)

* 
   * Lorsque le AEM Forms est démarré, l’ `SAX Security Manager could not be setup` avertissement s’affiche.