---
title: Problèmes connus
description: Notes de mise à jour spécifiques aux problèmes connus dans Adobe Experience Manager 6.5
exl-id: 736037cf-af8c-4ce2-969e-c100a939a038
source-git-commit: e0f024c2e1dc9fc7908382d406844575b4b38363
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 50%

---

# Problèmes connus {#known-issues}

Cette page contient la liste des problèmes connus dans la version Adobe Experience Manager 6.5 qui a été publiée en avril 2019.

[Contactez l’assistance](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=fr) si vous avez besoin d’informations supplémentaires sur les problèmes connus.

## Plate-forme {#platform}

* Un problème est signalé lorsque le démarrage rapide CRX et son contenu sont supprimés.

   Sur chacune de ces actions, assurez-vous que la propriété `htmllibmanager.fileSystemOutputCacheLocation` n’est pas une chaîne vide :

   1. L’appel de la fonction `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`.
   2. Mise à niveau vers AEM 6.5.
   3. Exécution de la &quot;migration différée du contenu&quot; sur AEM 6.5.

   A [Base de connaissances](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) Cet article est disponible avec d’autres détails et la solution à ce problème.

* Si vous utilisez JDK 11 avec l’instance AEM 6.5, certaines pages peuvent s’afficher comme vides après le déploiement de certains modules. Le message d’erreur suivant s’affiche dans le fichier journal :

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

Pour résoudre cette erreur :

1. Désactivez l’instance AEM. Accédez à `<aem_server_path_on_server>crx-quickstart\conf` et ouvrez le `sling.properties` fichier . Adobe recommande de sauvegarder ce fichier.

1. Recherchez `org.osgi.framework.bootdelegation=`. Ajouter `jdk.internal.reflect,jdk.internal.reflect.*` pour afficher le résultat.

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. Enregistrez le fichier et redémarrez l’instance AEM.

## Ressources {#assets}

* **Rechercher :** La recherche ne renvoie aucun résultat si la chaîne de recherche contient des espaces au début ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Schéma de métadonnées des dossiers** : après l’ajout d’un bouton de choix, les champs ID et Valeur ne sont pas restitués comme prévu et la fonctionnalité de suppression ne fonctionne pas. (CQ-4261144)
* Lors de l’attribution d’un nouveau nom à une ressource, il n’est pas possible d’utiliser un espace dans le nom. (CQ-4266403)

## Formulaires {#forms}

* Lorsque AEM Forms est installé sur un système d’exploitation Linux, la signature numérique avec le module de sécurité matérielle ne fonctionne pas. (CQ-4266721)
* (AEM Forms sur WebSphere uniquement) L’option **Forms Workflow**> **Recherche de tâche** ne renvoie aucun résultat si vous recherchez un **Administrateur** avec un **Nom d’utilisateur** comme critère de recherche. (CQ-4266457)

* AEM Forms ne parvient pas à convertir les fichiers TIF et de TIFF avec compression de JPEG en documents PDF. (CQ-4265972)
* Les options **Analyseur de ressources AEM Forms** et **Migration de la correspondance vers la communication interactive** ne fonctionnent pas sur la page **Migration d’AEM Forms**. (CQ-4266572)

* (JBoss 7 uniquement) Lorsque vous effectuez une mise à niveau d’une version précédente vers AEM 6.5 Forms et que la version précédente comporte des processus (.lca) qui ont créé et utilisé une copie du processus d’envoi ou de rendu par défaut, HTML5 Forms utilisant ces processus (.lca) ne parvient pas à effectuer les actions requises. (CQ-4243928)
* Dans une version adaptative, lorsqu’un service de modèle de données de formulaire est appelé à partir de l’éditeur de règle pour mettre à jour de manière dynamique les valeurs du composant de choix d’image, les valeurs du composant de choix d’image ne sont pas mises à jour. (CQ-4254754)
* Le programme d’installation d’AEM Forms Designer nécessite la version 32 bits de [Package d’exécution redistribuable Visual C++ 2012](https://support.microsoft.com/en-in/help/2977003/the-latest-supported-visual-c-downloads) et [Packages d’exécution redistribuables Visual C++ 2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Assurez-vous que les packages d’exécution redistribuables susmentionnés sont installés avant de démarrer l’installation. (CQ-4265668)

* PDF Generator ne prend pas en charge l’authentification par carte intelligente.  Lorsqu’un administrateur active la stratégie de groupe `Interactive Logon: Require Smart card` sur un serveur Windows, tous les utilisateurs de PDF Generator existants sont invalidés.

* Lorsqu’un formulaire adaptatif est configuré pour mettre à jour de manière dynamique les valeurs d’un composant et que l’instance de publication hébergeant le formulaire est accessible via le dispatcher, la fonctionnalité permettant de mettre à jour de manière dynamique les valeurs d’un champ cesse de fonctionner. Pour résoudre le problème, sur l’instance de publication, ouvrez CRXDE, accédez à `/libs/fd/af/runtime/clientlibs/guideChartReducer`et créez la propriété répertoriée ci-dessous.

   * Nom : allowProxy
   * Type : booléen
   * Valeur : vraie
   * Protégé : faux
   * Obligatoire : faux
   * Multiple : faux
   * Créé automatiquement : False

   La propriété permet aux bibliothèques clientes du dossier d’exécution d’accéder aux mandataires. (CQ-4268679)

* Au démarrage d’AEM Forms, la variable `SAX Security Manager could not be setup` s’affiche.
* Lorsque vous ouvrez un PDF protégé par AEM Forms Document Security sur un iOS Apple ou un iPadOS exécutant Adobe Acrobat Reader version 20.10.00.
* Lorsque vous envoyez un formulaire contenant un champ de chargement HTML standard d’un appareil iOS d’Apple, le contenu du fichier n’est parfois pas envoyé et un fichier de 0 octet est reçu à l’autre bout. Apple iOS 15.1 fournit un correctif pour le problème.
