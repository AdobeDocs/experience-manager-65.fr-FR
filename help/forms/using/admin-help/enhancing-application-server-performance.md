---
title: Amélioration des performances du serveur d’applications
seo-title: Amélioration des performances du serveur d’applications
description: Ce document décrit les paramètres facultatifs que vous pouvez configurer pour améliorer les performances du serveur d’applications AEM forms.
seo-description: Ce document décrit les paramètres facultatifs que vous pouvez configurer pour améliorer les performances du serveur d’applications AEM forms.
uuid: 88d2f96a-3b59-410d-8160-20581d27acad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fad65765-d56d-4a9f-82d5-bcceb1758953
translation-type: tm+mt
source-git-commit: a26bc4e4ea10370dd2fc3403500004b9e378c418
workflow-type: tm+mt
source-wordcount: '1886'
ht-degree: 95%

---


# Amélioration des performances du serveur d’applications{#enhancing-application-server-performance}

Cette section décrit les paramètres facultatifs que vous pouvez configurer pour améliorer les performances du serveur d’applications AEM forms.

## Configuration des sources de données du serveur d’applications {#configuring-application-server-data-sources}

AEM forms utilise le référentiel AEM forms comme source de données. Le référentiel AEM forms stocke les actifs de l’application et, lors de l’exécution, les services peuvent récupérer ces derniers dans le cadre d’un processus métier automatisé.

L’accès à la source de données peut être ralenti selon le nombre de modules AEM forms exécutés et le nombre d’utilisateurs qui accèdent simultanément à l’application. Il peut être optimisé grâce à l’utilisation d’un pool de connexions. *Le regroupement de connexions en un pool* est une technique qui permet d’éviter de créer d’autres connexions de base de données, chaque fois qu’un objet d’application ou de serveur a besoin d’accéder à la base de données. Ce pool est généralement utilisé dans des applications Web ou d’entreprise, et géré par un serveur d’applications, mais sans être limité à ce dernier.

Il est important de correctement configurer les paramètres du pool de connexions de sorte à ne jamais être à court de connexions, ce qui pourrait entraîner une détérioration des performances de l’application.

Pour configurer correctement les paramètres du pool de connexions, l’administrateur du serveur d’applications doit contrôler l’utilisation du pool pendant les heures de pointe. Ce contrôle garantit que le nombre de connexions disponibles est suffisant pour les applications et les utilisateurs, quelle que soit l’heure. En majorité, les serveurs d’applications incluent des outils de surveillance.

Utilisez WebLogic Server Administration Console pour contrôler les statistiques de chaque instance de source de données JDBC dans votre domaine Reportez-vous à votre documentation WebLogic pour plus d’informations.

Lorsque l’administrateur du serveur d’applications détermine les paramètres corrects du pool de connexions, il doit communiquer ces informations à l’administrateur de la base de données. Cette information lui est nécessaire car le nombre de connexions à la base de données doit être égal au nombre de connexions définies dans le pool pour la source de données. Ensuite, suivez la procédure ci-dessous pour configurer les paramètres du pool de connexions de votre serveur d’applications et de votre type de source de données.

### Configuration des paramètres du pool de connexions sur WebLogic pour Oracle et MySQL  {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. Sous Domain Structure, cliquez sur Services > JDBC > Data sources et, dans le volet de droite, cliquez sur IDP_DS.
1. Dans l’écran suivant, cliquez sur Configuration > Connection Pool (onglet), puis saisissez une valeur dans les champs suivants :

   * Initial Capacity
   * Maximum Capacity
   * Capacity Increment
   * Statement Cache Size

1. Cliquez sur Enregistrer, puis sur Activer les changements.
1. Redémarrez le serveur géré WebLogic.

### Configuration des paramètres du pool de connexions sur WebLogic pour SQLServer  {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. Sous Change Center, cliquez sur Lock &amp; Edit.
1. Sous Domain Structure, cliquez sur Services > JDBC > Data sources, puis dans le volet de droite, cliquez sur EDC_DS.
1. Dans l’écran suivant, cliquez sur Configuration > Connection Pool (onglet), puis saisissez une valeur dans les champs suivants :

   * Capacité initiale
   * Capacité maximale
   * Augmentation de capacité
   * Statement Cache Size

1. Cliquez sur Enregistrer, puis sur Activer les changements.
1. Redémarrez le serveur géré WebLogic.

### Configuration des paramètres du pool de connexions sur WebLogic pour DB2  {#configure-connection-pool-settings-for-websphere-for-db2}

1. Dans l’arborescence de navigation, cliquez sur Resources > JDBC > JDBC Providers. Dans le volet de droite, cliquez sur la source de données que vous venez de créer, DB2 Universal JDBC Driver Provider ou LiveCycle - db2 - IDP_DS.
1. Sous Additional Properties, cliquez sur Data sources, puis sélectionnez IDP_DS.
1. Dans l’écran suivant, sous Additional Properties, cliquez sur Connection Pool Properties, puis saisissez une valeur dans les champs Maximum Connections et Minimum Connections.
1. Cliquez sur OK ou sur Apply, puis sur Save Directly To Master Configuration.

### Configuration des paramètres du pool de connexions sur WebLogic pour Oracle  {#configure-connection-pool-settings-for-websphere-for-oracle}

1. Dans l’arborescence de navigation, cliquez sur Resources > JDBC > JDBC Providers. Dans le volet de droite, cliquez sur la source de données Oracle JDBC Driver que vous venez de créer.
1. Sous Additional Properties, cliquez sur Data sources, puis sélectionnez IDP_DS.
1. Dans l’écran suivant, sous Additional Properties, cliquez sur Connection Pool Properties, puis saisissez une valeur dans les champs Maximum Connections et Minimum Connections.
1. Cliquez sur OK ou sur Apply, puis sur Save Directly To Master Configuration.

### Configuration des paramètres du pool de connexions sur WebLogic pour SQLServer  {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. Dans l’arborescence de navigation, cliquez sur Resources > JDBC > JDBC Providers, puis dans le volet de droite, cliquez sur la source de données User-Defined JDBC Driver que vous avez créée.
1. Sous Additional Properties, cliquez sur Data sources, puis sélectionnez IDP_DS.
1. Dans l’écran suivant, sous Additional Properties, cliquez sur Connection Pool Properties, puis saisissez une valeur dans les champs Maximum Connections et Minimum Connections.
1. Cliquez sur OK ou sur Apply, puis sur Save Directly To Master Configuration.

## Optimisation de documents en ligne d’entrée et impacts sur la mémoire JVM  {#optimizing-inline-documents-and-impact-on-jvm-memory}

Si vous traitez régulièrement des documents de petite taille, vous pouvez améliorer les performances associées à la vitesse de transfert des documents et à l’espace de stockage. Pour ce faire, implémentez les configurations de produit AEM forms suivantes :

* Augmentation de la taille maximale de la ligne d’entrée (document par défaut) d&#39;AEM forms afin qu’elle soit supérieure à la taille de la plupart des documents.
* Pour le traitement de fichiers plus volumineux, spécification de répertoires de stockage situés sur un système de disque à grande vitesse ou un disque RAM.

La taille maximale de la ligne d’entrée et les répertoires de stockage (répertoire des fichiers temporaires et répertoire de stockage global d&#39;AEM forms) sont configurés dans Administration Console.

### Taille du document et taille maximale de la ligne d’entrée  {#document-size-and-maximum-inline-size}

Lorsque la taille d’un document à traiter avec AEM forms est inférieure ou égale à la taille maximale de la ligne d’entrée du document par défaut, le document est stocké sur le serveur de la ligne d’entrée et sérialisé sous la forme d’un objet Adobe Document. Le stockage de documents de ligne d’entrée peut considérablement accroître les performances. Toutefois, si vous utilisez le processus des formulaires, le contenu peut également être stocké dans la base de données à des fins de suivi. Par conséquent, une augmentation de la taille maximale de la ligne d’entrée peut affecter la taille de la base de données.

Un document dont la taille est supérieure à la taille maximale de la ligne d’entrée est stocké dans le système de fichiers local. L’objet Adobe Document transféré au serveur ou par ce dernier n’est qu’un pointeur permettant de localiser ce fichier.

Lorsque le contenu du document est en ligne d’entrée (c’est-à-dire qu’il est inférieur à la taille maximale de la ligne d’entrée), il est enregistré dans la base de données (dans le cadre de la charge utile de sérialisation du document). Par conséquent, une augmentation de la taille maximale de la ligne d’entrée peut affecter la taille de la base de données.

**Modification de la taille maximale de la ligne d’entrée**

1. Dans Administration Console, cliquez sur Paramètres > Paramètres de Core System > Configurations.
1. Saisissez une valeur dans le champ Taille maximale par défaut de la ligne d’entrée du document, puis cliquez sur OK.

   >[!NOTE]
   >
   >La valeur de la propriété Taille maximale en ligne d’entrée du Document doit être identique pour l’environnement AEM Forms on JEE et AEM Forms sur l’environnement JEE inclus dans le lot OSGi. Cette étape a mis à jour la valeur uniquement pour l’environnement AEM Forms sur JEE et non pour le lot AEM Forms sur OSGi, y compris l’environnement AEM Forms sur JEE.

1. Redémarrez le serveur d’applications à l’aide de la propriété système suivante :

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >La propriété système mentionnée ci-dessus remplace la valeur de la propriété Taille maximale de la ligne d’entrée du document définie pour l’environnement AEM Forms sur JEE et pour le lot AEM Forms sur OSGi, y compris l’environnement AEM Forms sur JEE.

>[!NOTE]
>
>La taille maximale par défaut de la ligne d’entrée équivaut à 65 536 octets.

### Taille de tas maximale de la JVM  {#jvm-maximum-heap-size}

L’augmentation de la taille maximale de la ligne d’entrée nécessite plus de mémoire pour le stockage des documents sérialisés. Une augmentation de la taille maximale du tas de la JVM est donc généralement nécessaire.

Un système lourdement chargé et traitant un grand nombre de documents peut rapidement saturer la mémoire du tas JVM. Pour éviter de saturer la mémoire (OutOfMemoryError), vous devez augmenter la taille maximale du tas de la JVM d’un volume correspondant à la taille des documents de la ligne d’entrée multipliée par le nombre de documents généralement exécutés à un moment donné.

Taille maximale du tas de la JVM = (taille des documents de ligne d’entrée) x (nombre moyen de documents traités)

**Calcul de la taille maximale du tas de la JVM**

Dans cet exemple, la taille maximale actuelle du tas de la JVM est de 512 Mo et la taille maximale de la ligne d’entrée, de 64 Ko. Vous devez configurer le serveur pour le scénario suivant : 10 tâches sont exécutées simultanément et chacune compte 9 fichiers d’entrée et un fichier de résultats (soit un total de 10 fichiers par tâche et 100 fichiers traités simultanément). La taille de chaque fichier ne dépasse pas 512 Ko.

Pour stocker tous les fichiers dans la ligne d’entrée, la taille maximale de cette dernière doit être de 512 Ko au minimum.

Utilisez l’équation suivante pour calculer l’augmentation requise de la taille maximale du tas de la JVM :

(512 Ko) x (100) = 51 200 Ko ou 50 Mo

Vous devez augmenter la taille maximale du tas JVM de 50 Mo pour un total de 562 Mo.

**Fragmentation du tas**

Si vous réglez la taille des documents de ligne d’entrée sur de grandes valeurs, vous augmentez le risque d’apparition d’erreurs OutOfMemoryError sur les systèmes sujets à la fragmentation du tas. Pour stocker un document de ligne d’entrée, il faut que la mémoire du tas JVM dispose d’un espace contigu suffisant. Certains systèmes d’exploitation, JVM et algorithmes collecteurs sont sujets à la fragmentation du tas. La fragmentation réduit la quantité d’espace de tas contigu et peut générer un message de mémoire saturée (OutOfMemoryError) même si l’espace disponible total est suffisant.

Par exemple, les précédentes opérations sur le serveur d’applications ont laissé le tas JVM dans un état fragmenté et le collecteur est incapable de compresser suffisamment le tas pour récupérer de grands blocs d’espace libre. Une erreur OutOfMemoryError peut se produire même si vous augmentez la taille maximale du tas JVM en fonction de la ligne d’entrée.

Pour éviter une fragmentation du tas, la taille du document de ligne d’entrée ne doit pas dépasser la taille totale du tas de plus de 0,1 %. Par exemple, une taille maximale du tas JVM de 512 Mo peut prendre en charge une taille maximale de ligne d’entrée de 512 Mo x 0,001 = 0,512 Mo, soit 512 Ko.

## Amélioration du fonctionnement du serveur d’applications WebSphere  {#websphere-application-server-enhancements}

Cette section décrit les paramètres spécifiques à l’environnement du serveur d’applications WebSphere.

### Augmentation de la quantité maximale de mémoire affectée à la JVM  {#increasing-the-maximum-memory-allocated-to-the-jvm}

Si vous exécutez Configuration Manager ou si vous essayez de générer le code de déploiement EJB (Enterprise JavaBeans) à l’aide de l’utilitaire de ligne de commande *ejbdeploy* et qu’une erreur OutOfMemory survient, augmentez la quantité maximale de mémoire allouée à la JVM.

1. Modifiez le script ejbdeploy dans le répertoire *[racine du serveur d’applications]*/deploytool/itp/ :

   * (Windows) `ejbdeploy.bat`
   * (Linux et UNIX) `ejbdeploy.sh`

1. Recherchez le paramètre `-Xmx256M` et remplacez-le par une valeur supérieure, telle que `-Xmx1024M`.
1. Enregistrez le fichier .
1. Exécutez la commande `ejbdeploy` ou effectuez de nouveau le déploiement à l’aide de Configuration Manager.

## Amélioration des performances de Windows Server 2003 avec le protocole LDAP {#improving-windows-server-2003-performance-with-ldap}

Cette section décrit les paramètres propres à un environnement exécutant le système d’exploitation Windows Server 2003.

L’utilisation du pool de connexions sur la connexion de recherche peut réduire le nombre de ports requis de 50 %. Ceci est dû au fait que cette connexion utilise toujours les mêmes informations d’identification pour un domaine donné, et le contexte et les objets liés sont fermés de manière explicite.

### Configuration de Windows Server pour le pool de connexion  {#configure-your-windows-server-for-connection-pooling}

1. Cliquez sur Démarrer > Exécuter pour lancer l’éditeur de registre, puis dans le champ Ouvrir, tapez `regedit` et cliquez sur OK.
1. Accéder à la clé de Registre `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
1. Dans le volet droit de l’éditeur de registre, recherchez le nom de valeur TcpTimedWaitDelay. Si ce nom n’apparaît pas, sélectionnez Edition > Nouveau > Valeur DWORD dans la barre de menus pour l’ajouter.
1. Dans la zone Nom, saisissez `TcpTimedWaitDelay`

   >[!NOTE]
   >
   >Si vous ne voyez pas de curseur clignotant et `New Value #` dans la zone, cliquez avec le bouton droit dans le panneau de droite, sélectionnez Renommer et, dans la zone Nom, tapez `TcpTimedWaitDelay`*.*

1. Répétez l’étape 4 pour les noms de valeur MaxUserPort, MaxHashTableSize et MaxFreeTcbs.
1. Cliquez deux fois dans le volet de droite pour définir la valeur TcpTimedWaitDelay. Sous Base, sélectionnez Décimale puis entrez `30` dans le champ Valeur.
1. Cliquez deux fois dans le volet de droite pour définir la valeur MaxUserPort. Sous Base, sélectionnez Décimale puis entrez `65534` dans le champ Valeur.
1. Cliquez deux fois dans le volet de droite pour définir la valeur MaxHashTableSize. Sous Base, sélectionnez Décimale puis entrez `65536` dans le champ Valeur.
1. Cliquez deux fois dans le volet de droite pour définir la valeur MaxFreeTcbs. Sous Base, sélectionnez Décimale puis entrez `16000` dans le champ Valeur.

>[!NOTE]
>
>Vous risquez de rencontrer de sérieux problèmes si vous modifiez le registre, au moyen de l’éditeur de registre ou d’une autre méthode, de façon incorrecte. Vous pourriez être obligé de réinstaller votre système d’exploitation. Modifiez le registre à vos propres risques.

