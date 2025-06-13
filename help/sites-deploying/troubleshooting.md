---
title: Dépanner les problèmes d’installation avec AEM
description: Cet article aborde certains des problèmes d’installation que vous pouvez rencontrer avec AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 55576729-be9c-412e-92ac-4be90650c6fa
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 8f638eb384bdca59fb6f4f8990643e64f34622ce
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 100%

---

# Dépanner les problèmes d’installation avec AEM{#troubleshooting}

Cette section comprend des informations détaillées sur les journaux disponibles pour vous aider à résoudre les problèmes, ainsi que des informations sur certains des problèmes que vous pouvez rencontrer avec AEM.

## Dépanner les problèmes de performances sur l’instance de création {#troubleshoot-author-performance}

Il n’est pas toujours facile de connaître la cause d’une baisse des performances sur l’instance de création. Dans un premier temps, il est nécessaire de déterminer à quel niveau de la pile technologique les performances diminuent.

L’arborescence décisionnelle suivante fournit les indications nécessaires pour trouver le goulet d’étranglement.

![chlimage_1-75](assets/chlimage_1-75.png)

## Optimisation de base {#basic-optimization}

![chlimage_1-76](assets/chlimage_1-76.png)

## Configurer les fichiers journaux et les journaux d’audit {#configuring-log-files-and-audit-logs}

AEM enregistre les journaux détaillés que vous pouvez configurer pour résoudre les problèmes d’installation. Pour plus d’informations, consultez la section [Utilisation des enregistrements d’audit et des fichiers journaux](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files).

## Utilisation de l’option d’informations détaillées (Verbose) {#using-the-verbose-option}

Lorsque vous démarrez la gestion de contenu web AEM, vous pouvez ajouter l’option -v (verbose) à la ligne de commande, comme suit : java -jar cq-wcm-quickstart-&lt;version>.jar -v.

L’option détaillée permet d’afficher une partie du journal de démarrage rapide sur la console, à des fins de dépannage.

## Problèmes d’installation courants {#common-installation-issues}

La section suivante décrit certains des problèmes d’installation et leurs solutions.

### Lorsque vous double-cliquez sur le fichier jar de démarrage rapide, rien ne se produit ou le fichier s’ouvre dans un autre programme (par exemple, le gestionnaire d’archives). {#double-clicking-the-quickstart-jar-does-not-have-any-effect-or-opens-the-jar-file-with-another-program-for-example-archive-manager}

Ce problème indique généralement qu’il existe un problème lié à la configuration de l’environnement de poste de travail de votre système d’exploitation pour l’ouverture des fichiers dotés de l’extension .jar. Il peut également indiquer que Java™ n’est pas installé ou que vous utilisez une version de Java™ non prise en charge.

Comme les fichiers jar utilisent le format ZIP très courant, certains programmes d’archivage de fichiers peuvent être configurés pour ouvrir les fichiers jar en tant que fichiers d’archive par défaut.

Pour résoudre le problème, procédez comme suit :

* Vérifiez que vous avez installé Java™ version 1.6 ou ultérieure.
* Ouvrez un menu contextuel (généralement avec le bouton droit de la souris) dans le démarrage rapide de la gestion de contenu web d’AEM, puis sélectionnez « Ouvrir avec… ».
* Vérifiez si Java™ ou Sun Java™ est répertorié et essayez d’exécuter la gestion de contenu web d’AEM avec ce logiciel. Si plusieurs versions de Java™ sont installées, sélectionnez celle prise en charge.

  Si cette étape porte ses fruits et que votre système d’exploitation permet de définir le programme sélectionné pour exécuter les fichiers .jar par défaut, sélectionnez-le. Double-cliquez à présent sur le fichier jar de démarrage rapide pour vérifier si le problème est résolu.

* Parfois, la réinstallation de la version Java™ prise en charge permet de restaurer l’association correcte.
* Vous pouvez toujours exécuter CRX à l’aide de la ligne de commande ou des scripts start/stop, comme décrit précédemment dans ce document.

### Mon application qui s’exécute sur CRX génère des erreurs de mémoire insuffisante. {#my-application-running-on-crx-throws-out-of-memory-errors}

>[!NOTE]
>
>Consultez aussi la section [Analyser les problèmes de mémoire](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html?lang=fr).


L’empreinte mémoire de CRX est faible. Si l’application s’exécutant dans CRX a besoin de plus de mémoire ou lance des opérations gourmandes en mémoire (par exemple, des transactions volumineuses), l’instance JVM où CRX s’exécute doit être démarrée avec les paramètres de mémoire appropriés.

Utilisez les options de commande Java™ pour définir les paramètres de mémoire de JVM (par exemple, java -Xmx512m -jar crx&amp;ast;.jar pour définir la taille des segments de mémoire sur 512 Mo).

Définissez le paramètre d’allocation de mémoire lors du démarrage de la gestion de contenu web d’AEM à partir de la ligne de commande. Les scripts start/stop de la gestion de contenu web d’AEM ou les scripts personnalisés pour gérer la gestion de contenu web d’AEM peuvent également être modifiés pour définir les paramètres de mémoire requis.

Si vous avez déjà défini les segments de mémoire sur 512 Mo, vous souhaiterez peut-être continuer à analyser l’erreur de mémoire en créant une image mémoire des segments de mémoire :

Pour créer automatiquement un vidage de segments de mémoire lorsque la mémoire est insuffisante, utilisez la commande suivante :

java -Xmx256m -XX:+HeapDumpOnOutOfMemoryError -jar &amp;ast;.jar

Cette méthode génère un fichier d’image mémoire des segments de mémoire (**java_...hprof**) chaque fois que le processus manque de mémoire. Le processus peut continuer à s’exécuter une fois l’image mémoire des segments de mémoire générée.

Souvent, trois fichiers d’image mémoire des segments de mémoire, collectés sur une période donnée, sont nécessaires pour analyser le problème :

* Avant qu’un échec ne se produise.
* Lors de l’échec 1
* Lors de l’échec 2
* *Idéalement, il serait également préférable de collecter des informations une fois l’événement résolu.*

Celles-ci peuvent être comparées pour voir les modifications et comment les objets utilisent la mémoire.

>[!NOTE]
>
>Si vous collectez régulièrement de telles informations, ou si vous êtes habitué à lire des images mémoire des segments de mémoire, un seul fichier d’image mémoire des segments de mémoire peut suffire à analyser le problème.

### Après avoir double-cliqué sur AEM Quickstart, l’écran d’accueil d’AEM ne s’affiche pas dans le navigateur. {#the-aem-welcome-screen-does-not-display-in-the-browser-after-double-clicking-aem-quickstart}

Dans certains cas, les écrans de bienvenue de la gestion de contenu web d’AEM ne s’affichent pas automatiquement, même si le référentiel s’exécute correctement. Ce problème peut dépendre de la configuration du système d’exploitation, de la configuration du navigateur ou de facteurs similaires.

Dans ce cas, la fenêtre Quickstart affiche le message suivant : « Démarrage de la gestion de contenu web AEM. En attente du démarrage du serveur... » Si ce message s’affiche pendant une période relativement longue, saisissez manuellement l’URL de gestion de contenu web d’AEM dans la fenêtre du navigateur, à l’aide du port 4502 par défaut, ou du port sur lequel l’instance est en cours d’exécution : http://localhost:4502/.

En outre, les journaux peuvent indiquer la raison pour laquelle le navigateur ne démarre pas.

Parfois, la fenêtre de démarrage rapide de la gestion de contenu web d’AEM comporte le message « La gestion de contenu web d’AEM s’exécutant sur http://localhost:port/ » et le navigateur ne démarre pas automatiquement. Dans ce cas, cliquez sur l’URL dans la fenêtre de démarrage rapide de gestion de contenu web d’AEM (il s’agit d’un lien hypertexte) ou saisissez manuellement l’URL dans le navigateur.

Si tout le reste échoue, consultez les journaux pour savoir ce qui s’est passé.

### Le site web ne se charge pas ou échoue par intermittence avec Java™ 11 {#the-website-does-not-load-or-fails-intermittently-with-java11}

Il existe un problème connu avec AEM 6.5 exécuté sur Java™ 11 : le site web peut ne pas se charger ou son chargement échoue par intermittence.

Si ce problème se produit, procédez comme suit :

1. Ouvrez le fichier `sling.properties` dans le dossier `crx-quickstart/conf/`.
1. Recherchez la ligne suivante :

   `org.osgi.framework.bootdelegation=sun.,com.sun.`

1. Remplacez-la par ce qui suit :

   `org.osgi.framework.bootdelegation=sun.,com.sun.,jdk.internal.reflect,jdk.internal.reflect.*`

1. Redémarrez l’instance.

## Dépanner des installations avec un serveur d’applications {#troubleshooting-installations-with-an-application-server}

### Page introuvable lors de la demande d’une page geometrixx-outdoor {#page-not-found-returned-when-requesting-a-geometrixx-outdoor-page}

**S’applique à WebLogic 10.3.5 et JBoss® 5.1**

Lorsqu’une requête de page geometrixx-outdoors/en renvoie une erreur 404 (Page introuvable), vérifiez que vous avez défini la propriété Sling supplémentaire dans le fichier sling.properties de ces serveurs d’applications.

Pour plus d’informations, reportez-vous à la procédure *Déployer une application web AEM*.

### La taille de l’en-tête de réponse peut être supérieure à 4 Ko. {#response-header-size-can-be-greater-than-kb}

Les erreurs 502 peuvent indiquer que le serveur web ne peut pas gérer la taille de l’en-tête de réponse HTTP d’AEM. AEM peut générer des en-têtes de réponse HTTP qui incluent des cookies d’une taille supérieure à 4 Ko. Assurez-vous que votre conteneur de servlets est configuré de sorte que la taille maximale de l’en-tête de réponse puisse dépasser 4 Ko.

Par exemple, pour Tomcat 7.0, l’attribut maxHttpHeaderSize de [Connecteur HTTP](https://tomcat.apache.org/tomcat-7.0-doc/config/http.html) contrôle les limites de la taille de l’en-tête.

## Désinstaller Adobe Experience Manager {#uninstalling-adobe-experience-manager}

AEM s’installant dans un seul répertoire, un utilitaire de désinstallation n’est pas nécessaire. La désinstallation peut être aussi simple que la suppression de l’intégralité du répertoire d’installation, mais elle dépend en réalité de ce que vous souhaitez réaliser et du stockage persistant que vous utilisez.

Si le stockage persistant est incorporé dans le répertoire d’installation, par exemple dans l’installation par défaut de TarPM, la suppression de dossiers supprime également les données.

>[!NOTE]
>
>Adobe vous recommande de sauvegarder votre référentiel avant de supprimer AEM. Si vous supprimez l’intégralité de la variable &lt;cq-installation-directory>, vous supprimez également le référentiel. Pour conserver les données du référentiel avant de supprimer, déplacez ou copiez le dossier &lt;cq-installation-directory>/crx-quickstart/repository ailleurs avant de supprimer les autres dossiers.

Si votre installation d’AEM utilise un stockage externe, par exemple un serveur de base de données, la suppression du dossier ne supprime pas automatiquement les données, mais supprime la configuration de stockage, ce qui rend difficile la restauration du contenu JCR.
