---
title: Amélioration des performances du serveur d’applications
description: Ce document décrit les paramètres facultatifs que vous pouvez configurer pour améliorer les performances de votre serveur d’applications AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6e2f3d4c-2ead-45b3-98e7-32cacc7e2985
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '1870'
ht-degree: 100%

---

# Amélioration des performances du serveur d’applications{#enhancing-application-server-performance}

Ce contenu décrit les paramètres facultatifs que vous pouvez configurer pour améliorer les performances de votre serveur d’applications AEM Forms.

## Configurer les sources de données du serveur d’applications {#configuring-application-server-data-sources}

AEM Forms utilise le référentiel AEM Forms comme source de données. Le référentiel d’AEM Forms stocke les ressources d’application et, au moment de l’exécution, les services peuvent récupérer les ressources du référentiel dans le cadre d’un processus métier automatisé.

L’accès à la source de données peut être important, selon le nombre de modules d’AEM Forms en cours d’exécution et le nombre d’utilisateurs et utilisatrices accédant simultanément à l’application. L’accès aux sources de données peut être optimisé à l’aide de la mise en pool de connexions. La *mise en pool de connexions* est une technique qui permet d’éviter de créer de nouvelles connexions de base de données chaque fois qu’une application ou un objet de serveur requiert un accès à la base de données. La mise en pool de connexions est généralement utilisée dans les applications web et d’entreprise. Elle est généralement gérée par un serveur d’applications, mais sans s’y limiter.

Il est important de configurer correctement les paramètres du pool de connexions afin de ne jamais manquer de connexions, ce qui peut entraîner une détérioration des performances de l’application.

Pour configurer correctement les paramètres du pool de connexions, il est important que l’administrateur ou l’administratrice du serveur d’applications surveille le pool de connexions aux heures de pointe de la journée. La surveillance permet de s’assurer qu’un nombre suffisant de connexions sont disponibles en permanence pour les applications et les utilisateurs et utilisatrices. La plupart des serveurs d’applications incluent des outils de surveillance.

Vous pouvez surveiller différentes statistiques pour chaque instance de source de données JDBC dans votre domaine à l’aide de de la console d’administration du serveur WebLogic. Consultez votre documentation WebLogic pour plus de détails.

Lorsque l’administrateur ou l’administratrice du serveur d’applications détermine les paramètres corrects du pool de connexions, il ou elle doit communiquer ces informations à l’administrateur ou à l’administratrice de base de données. L’administrateur ou l’administratrice de base de données a besoin de ces informations, car le nombre de connexions à la base de données est égal au nombre de connexions dans le pool de connexions pour la source de données. Suivez ensuite les étapes ci-dessous pour configurer les paramètres du pool de connexions pour votre serveur d’applications et le type de source de données.

### Configurer les paramètres du pool de connexions pour WebLogic pour Oracle et MySQL {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. Sous Structure du domaine, cliquez sur Services > JDBC > Sources de données et, dans le volet de droite, cliquez sur IDP_DS.
1. Dans l’écran suivant, cliquez sur l’onglet Configuration > Pool de connexions, et saisissez une valeur dans les zones suivantes :

   * Capacité initiale
   * Capacité maximale
   * Augmentation de capacité
   * Taille du cache d’instruction

1. Cliquez sur Enregistrer, puis sur Activer les modifications.
1. Redémarrez le serveur géré WebLogic.

### Configurer les paramètres du pool de connexions pour WebLogic pour SQLServer {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. Sous Centre des modifications, cliquez sur Verrouiller et modifier.
1. Sous Structure du domaine, cliquez sur Services > JDBC > Sources de données et, dans le volet de droite, cliquez sur EDC_DS.
1. Dans l’écran suivant, cliquez sur l’onglet Configuration > Pool de connexions, et saisissez une valeur dans les zones suivantes :

   * Capacité initiale
   * Capacité maximale
   * Augmentation de capacité
   * Taille du cache d’instruction

1. Cliquez sur Enregistrer, puis sur Activer les modifications.
1. Redémarrez le serveur géré WebLogic.

### Configurer les paramètres du pool de connexions pour WebSphere pour DB2 {#configure-connection-pool-settings-for-websphere-for-db2}

1. Dans l’arborescence de navigation, cliquez sur Resources > JDBC > Fournisseurs JDBC. Dans le volet de droite, cliquez sur la source de données que vous avez créée, DB2 Universal JDBC Driver Provider ou LiveCycle - db2 - IDP_DS.
1. Sous Propriétés supplémentaires, cliquez sur Sources de données, puis sélectionnez IDP_DS.
1. Dans l’écran suivant, sous Propriétés supplémentaires, cliquez sur Propriétés du pool de connexions, puis saisissez une valeur dans les zones Connexions maximales et Connexions minimales.
1. Cliquez sur OK ou Appliquer, puis cliquez sur Enregistrer directement dans la configuration principale.

### Configurer les paramètres du pool de connexions pour WebSphere pour Oracle {#configure-connection-pool-settings-for-websphere-for-oracle}

1. Dans l’arborescence de navigation, cliquez sur Resources > JDBC > Fournisseurs JDBC. Dans le volet de droite, cliquez sur la source de données Oracle JDBC Driver que vous avez créée.
1. Sous Propriétés supplémentaires, cliquez sur Sources de données, puis sélectionnez IDP_DS.
1. Dans l’écran suivant, sous Propriétés supplémentaires, cliquez sur Propriétés du pool de connexions, puis saisissez une valeur dans les zones Connexions maximales et Connexions minimales.
1. Cliquez sur OK ou Appliquer, puis cliquez sur Enregistrer directement dans la configuration principale.

### Configurer les paramètres du pool de connexions pour WebSphere pour SqlServer {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. Dans l’arborescence de navigation, cliquez sur Ressources > JDBC > Fournisseurs JDBC, puis, dans le volet de droite, cliquez sur la source de données du pilote JDBC défini par l’utilisateur ou utilisatrice que vous avez créée.
1. Sous Propriétés supplémentaires, cliquez sur Sources de données, puis sélectionnez IDP_DS.
1. Dans l’écran suivant, sous Propriétés supplémentaires, cliquez sur Propriétés du pool de connexions puis saisissez une valeur dans les zones Connexions maximales et Connexions minimales :
1. Cliquez sur OK ou Appliquer, puis cliquez sur Enregistrer directement dans la configuration principale.

## Optimisation des documents intégrés et impact sur la mémoire JVM {#optimizing-inline-documents-and-impact-on-jvm-memory}

Si vous traitez généralement des documents d’une taille relativement réduite, vous pouvez améliorer les performances associées à la vitesse de transfert des documents et à l’espace de stockage. Pour ce faire, implémentez les configurations de produit d’AEM Forms suivantes :

* Augmentation de la taille maximale de la ligne d’entrée (document par défaut) d’AEM forms afin qu’elle soit supérieure à la taille de la plupart des documents.
* Pour traiter des fichiers plus volumineux, spécifiez les répertoires de stockage situés sur un système de disque à grande vitesse ou un disque RAM.

La taille maximale de la ligne d’entrée et les répertoires de stockage (répertoire des fichiers temporaires et répertoire de stockage global d’AEM forms) sont configurés dans Administration Console.

### Taille du document et taille maximale de la ligne d’entrée {#document-size-and-maximum-inline-size}

Lorsqu’un document envoyé pour traitement par AEM Forms est inférieur ou égal à la taille maximale de la ligne d’entrée du document par défaut, le document est stocké en ligne dans le serveur et il est sérialisé en tant qu’objet Adobe Document. Le stockage de documents en ligne peut améliorer considérablement les performances. Cependant, si vous utilisez Forms Workflow, le contenu peut également être stocké dans la base de données à des fins de suivi. Par conséquent, l’augmentation de la taille maximale de la ligne d’entrée peut affecter la taille de la base de données.

Un document dont la taille est supérieure à la taille maximale de la ligne d’entrée est stocké sur le système de fichiers local. L’objet Adobe Document transféré vers et depuis le serveur n’est qu’un pointeur vers ce fichier.

Lorsque le contenu du document est intégré (c’est-à-dire inférieur à la taille maximale de la ligne d’entrée), il est stocké dans la base de données dans le cadre de la payload de sérialisation du document. Par conséquent, l’augmentation de la taille maximale de la ligne d’entrée peut affecter la taille de la base de données.

**Modification de la taille maximale de la ligne d’entrée**

1. Dans la console d’administration, cliquez sur Paramètres > Paramètres du système principal > Configurations.
1. Saisissez une valeur dans la zone Taille maximale par défaut de la ligne d’entrée du document, puis cliquez sur OK.

   >[!NOTE]
   >
   >La valeur de la propriété de la taille maximale de la ligne d’entrée du document doit être identique pour l’environnement AEM Forms sur JEE et pour le bundle AEM Forms sur OSGi, inclus dans l’environnement AEM Forms sur JEE. Cette procédure a mis à jour la valeur pour l’environnement AEM Forms on JEE uniquement et non pour le lot AEM Forms sur OSGi, y compris l’environnement AEM Forms on JEE.

1. Redémarrez le serveur d’applications avec la propriété système suivante :

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >La propriété système mentionnée ci-dessus remplace la valeur de la propriété Taille maximale de la ligne d’entrée du document définie pour l’environnement AEM Forms on JEE et pour le lot AEM Forms sur OSGi, y compris l’environnement AEM Forms on JEE.

>[!NOTE]
>
>La taille maximale par défaut de la ligne d’entrée est de 65 536 octets.

### Taille maximale du tas JVM {#jvm-maximum-heap-size}

Une augmentation de la taille maximale de la ligne d’entrée nécessite plus de mémoire pour le stockage des documents sérialisés. Une augmentation de la taille maximale du tas JVM est donc généralement nécessaire.

Un système lourdement chargé qui traite de nombreux documents peut rapidement saturer la mémoire du tas JVM. Pour éviter de saturer la mémoire (OutOfMemoryError), vous devez augmenter la taille maximale du tas JVM d’un volume correspondant à la taille des documents de la ligne d’entrée multipliée par le nombre de documents généralement exécutés à un moment donné.

Augmentation de la taille maximale du tas JVM = (taille des documents de la ligne d’entrée) x (nombre moyen de documents traités).

**Calcul de la taille maximale du tas JVM**

Dans cet exemple, la taille maximale actuelle du tas JVM est de 512 Mo et la taille maximale de la ligne d’entrée, de 64 Ko. Vous devez configurer le serveur pour le scénario suivant : 10 tâches sont exécutées simultanément et chacune compte 9 fichiers d’entrée et un fichier de résultats (soit un total de 10 fichiers par tâche et 100 fichiers traités simultanément). La taille de chaque fichier ne dépasse pas 512 Ko.

Pour stocker tous les fichiers dans la ligne d’entrée, la taille maximale de cette dernière doit être de 512 Ko au minimum.

L’augmentation requise de la taille maximale du tas JVM est calculée à l’aide de l’équation suivante :

(512 Ko) x (100) = 51 200 Ko ou 50 Mo.

La taille maximale du tas JVM doit être augmentée de 50 Mo pour un total de 562 Mo.

**Fragmentation du tas**

Si vous réglez la taille des documents de ligne d’entrée sur de grandes valeurs, vous augmentez le risque d’apparition d’erreurs OutOfMemoryError sur les systèmes sujets à la fragmentation du tas. Pour stocker un document de ligne d’entrée, il faut que la mémoire du tas JVM dispose d’un espace contigu suffisant. Certains systèmes d’exploitation, JVM et algorithmes de récupération de l’espace mémoire sont sujets à la fragmentation du tas. La fragmentation réduit la quantité d’espace de tas contigu et peut générer un message de mémoire saturée (OutOfMemoryError) même si l’espace disponible total est suffisant.

Par exemple, les opérations précédentes sur le serveur d’applications ont laissé le tas JVM dans un état fragmenté, et le récupérateur d’espace ne peut pas suffisamment compresser le tas pour récupérer de grands blocs d’espace libre. Une erreur OutOfMemoryError peut se produire même si vous augmentez la taille maximale du tas JVM en fonction de la ligne d’entrée.

Pour éviter une fragmentation du tas, la taille du document de ligne d’entrée ne doit pas dépasser la taille totale du tas de plus de 0,1 %. Par exemple, une taille maximale de tas JVM de 512 Mo peut prendre en charge une taille maximale de ligne d’entrée de 512 Mo x 0,001 = 0,512 Mo, soit 512 Ko.

## Amélioration du fonctionnement du serveur d’applications WebSphere {#websphere-application-server-enhancements}

Cette section décrit les paramètres spécifiques à l’environnement du serveur d’applications WebSphere.

### Augmentation de la quantité maximale de mémoire affectée à la JVM {#increasing-the-maximum-memory-allocated-to-the-jvm}

Si vous exécutez Configuration Manager ou si vous essayez de générer le code de déploiement EJB (Enterprise JavaBeans) à l’aide de l’utilitaire de ligne de commande *ejbdeploy* et qu’une erreur OutOfMemory survient, augmentez la quantité maximale de mémoire allouée à la JVM.

1. Modifiez le script ejbdeploy dans le répertoire *[racine du serveur d’applications]*/deploytool/itp/ :

   * (Windows) `ejbdeploy.bat`
   * (Linux et UNIX) `ejbdeploy.sh`

1. Recherchez le paramètre `-Xmx256M` et affectez-lui une valeur supérieure, comme `-Xmx1024M`.
1. Enregistrez le fichier.
1. Exécutez la commande `ejbdeploy` ou effectuez de nouveau le déploiement à l’aide de Configuration Manager.

## Amélioration des performances de Windows Server 2003 avec le protocole LDAP {#improving-windows-server-2003-performance-with-ldap}

Cette section décrit les paramètres propres à un environnement exécutant le système d’exploitation Windows Server 2003.

L’utilisation du pool de connexions sur la connexion de recherche peut réduire le nombre de ports requis de 50 %. Ceci est dû au fait que cette connexion utilise toujours les mêmes informations d’identification pour un domaine donné, et le contexte et les objets liés sont fermés de manière explicite.

### Configuration de Windows Server pour le pool de connexions {#configure-your-windows-server-for-connection-pooling}

1. Cliquez sur Démarrer > Exécuter pour lancer l’éditeur de registre, puis dans le champ Ouvrir, tapez `regedit` et cliquez sur OK.
1. Accédez à la clé de registre `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`.
1. Dans le volet droit de l’éditeur de registre, recherchez le nom de valeur TcpTimedWaitDelay. Si ce nom n’apparaît pas, sélectionnez  Édition > Nouveau > Valeur DWORD dans la barre de menus pour l’ajouter.
1. Dans la zone Nom, saisissez `TcpTimedWaitDelay`

   >[!NOTE]
   >
   >Si vous ne voyez pas un curseur clignotant et `New Value #` dans le champ, effectuez un clic droit dans le panneau de droite, sélectionnez Renommer, puis dans le champ Nom, saisissez `TcpTimedWaitDelay`*.*

1. Répétez l’étape 4 pour les noms de valeur MaxUserPort, MaxHashTableSize et MaxFreeTcbs.
1. Double-cliquez dans le volet de droite pour définir la valeur TcpTimedWaitDelay. Sous Base, sélectionnez Décimale puis entrez `30` dans le champ Valeur.
1. Cliquez deux fois dans le volet de droite pour définir la valeur MaxUserPort. Sous Base, sélectionnez Décimale puis entrez `65534` dans le champ Valeur.
1. Cliquez deux fois dans le volet de droite pour définir la valeur MaxHashTableSize. Sous Base, sélectionnez Décimale puis entrez `65536` dans le champ Valeur.
1. Cliquez deux fois dans le volet de droite pour définir la valeur MaxFreeTcbs. Sous Base, sélectionnez Décimale puis entrez `16000` dans le champ Valeur.

>[!NOTE]
>
>Vous risquez de rencontrer de sérieux problèmes si vous modifiez le registre, au moyen de l’éditeur de registre ou d’une autre méthode, de façon incorrecte. Ces problèmes peuvent nécessiter la réinstallation de votre système d’exploitation. Modifiez le registre à vos propres risques.
