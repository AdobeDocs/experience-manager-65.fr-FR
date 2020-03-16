---
title: Problèmes connus
description: Notes de mise à jour spécifiques aux problèmes connus dans Adobe Experience Manager 6.3
uuid: 8fbdb167-833a-4179-aad1-0a26a4e5b3a7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: d11fc727-f23a-4cde-9fa6-97e2c81b4ad0
docset: aem65
translation-type: tm+mt
source-git-commit: 0ae42d9f81df89a7e1c08fac5cce5240f14e8c60

---


# Problèmes connus {#known-issues}

Cette page contient la liste des problèmes connus dans la version Adobe Experience Manager 6.5 qui a été publiée en avril 2019.

[Contactez l’assistance](https://helpx.adobe.com/support/experience-manager.html) si vous avez besoin d’informations supplémentaires sur les problèmes connus.

## Plate-forme {#platform}

Un problème est signalé en raison duquel CRX-Quickstart et son contenu sont supprimés.

Pour chacune de ces actions, veillez à ce que la propriété &quot;*htmllibmanager.fileSystemOutputCacheLocation*&quot; ne soit jamais une chaîne vide :

1. Appel à &quot;*/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true*&quot;.
2. Mise à niveau vers AEM 6.5.
3. Exécution de la &quot;migration différée de contenu&quot; sur AEM 6.5.

Un article de la base de [connaissances](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) est disponible avec des détails supplémentaires et la solution à ce problème.

## Assets {#assets}

* **Rechercher :** La recherche ne renvoie aucune valeur si la chaîne de recherche contient des espaces de début ([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **Schéma de métadonnées des dossiers** : après l’ajout d’un bouton de choix, les champs ID et Valeur ne sont pas restitués comme prévu et la fonctionnalité de suppression ne fonctionne pas. (CQ-4261144)
* Lors de l’attribution d’un nouveau nom à une ressource, il n’est pas possible d’utiliser un espace dans le nom. (CQ-4266403)

## Forms {#forms}

* Lorsque AEM Forms est installé sous un système d’exploitation Linux, la signature numérique avec le module de sécurité matérielle ne fonctionne pas. (CQ-4266721)
* (AEM Forms on WebSphere only) The **Forms Workflow **> **Task Search** option does not return any result if you search for an **Administrator** with **Username** as the search criteria. (CQ-4266457)

* AEM Forms ne parvient pas à convertir les fichiers .tif et .tiff avec la compression JPEG en documents PDF. (CQ-4265972)
* Les options **Analyseur de ressources AEM Forms** et **Migration de la correspondance vers la communication interactive** ne fonctionnent pas sur la page **Migration d’AEM Forms**. (CQ-4266572)

* (JBoss 7 uniquement) Lorsque vous effectuez une mise à niveau d’une version précédente vers AEM Forms 6.5 et que la version précédente contenait des processus (.lca) qui créaient et utilisaient une copie du processus d’envoi par défaut ou de rendu par défaut, les formulaires HTML5 utilisant de tels processus (.lca) ne parviennent pas à exécuter les actions requises. (CQ-4243928)
* Dans une version adaptative, lorsqu’un service de modèle de données de formulaire est appelé à partir de l’éditeur de règle pour mettre à jour de manière dynamique les valeurs du composant de choix d’image, les valeurs du composant de choix d’image ne sont pas mises à jour. (CQ-4254754)
* AEM Forms Designer installer requires the 32-bit version of [Visual C++ redistributable runtime package 2012](https://support.microsoft.com/en-in/help/2977003/the-latest-supported-visual-c-downloads) and [Visual C++ redistributable runtime packages 2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package). Assurez-vous que les packages d’exécution redistribuables susmentionnés sont installés avant de démarrer l’installation. (CQ-4265668)

* Lorsqu’un formulaire adaptatif est configuré pour mettre à jour de manière dynamique les valeurs d’un composant et que l’instance de publication hébergeant le formulaire est accessible via le dispatcher, la fonctionnalité permettant de mettre à jour de manière dynamique les valeurs d’un champ cesse de fonctionner. Pour résoudre le problème, ouvrez CRXDE sur l’instance de publication, accédez à /libs/fd/af/runtime/clientlibs/guideChartReduce et créez la propriété répertoriée ci-dessous. 

   * Nom : allowProxy
   * Type : booléen
   * Valeur : vraie
   * Protégé : faux
   * Obligatoire : faux
   * Multiple : faux
   * Créé automatiquement : faux 

La propriété permet aux bibliothèques clientes du dossier d’exécution d’accéder aux mandataires. (CQ-4268679)

