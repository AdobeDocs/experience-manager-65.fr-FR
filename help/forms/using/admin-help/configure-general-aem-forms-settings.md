---
title: Paramètres généraux d’AEM Forms
description: Découvrez comment configurer les paramètres de la page Configurations de base dans la console d’administration afin d’améliorer les performances du système.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
exl-id: e1519477-b5a8-4947-8597-26b945a3b819
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1762'
ht-degree: 100%

---

# Paramètres généraux d’AEM Forms {#general-aem-forms-settings}

La page Configurations de base dans la console d’administration fournit des paramètres qui peuvent améliorer les performances du système. Une fois que vous avez configuré ou mis à jour ces paramètres, redémarrez votre serveur d’applications.

>[!NOTE]
>
> Il est recommandé d’utiliser la commande « Ctrl + C » pour redémarrer le SDK. Le redémarrage du SDK AEM à l’aide de méthodes alternatives, par exemple l’arrêt des processus Java, peut entraîner des incohérences dans l’environnement de développement AEM.

Pour plus d’informations sur l’activation du mode de sauvegarde sécurisé, voir [Activation et désactivation du mode de sauvegarde sécurisé](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode).


>[!NOTE]
>
>Les fichiers du répertoire temporaire et les documents de longue durée du répertoire racine de stockage global de documents peuvent contenir des informations utilisateur sensibles, telles que des informations qui nécessitent des informations d’identification spéciales lors de l’accès à l’aide des API ou des interfaces utilisateur. Par conséquent, il est important que ce répertoire soit correctement sécurisé à l’aide des méthodes disponibles pour le système d’exploitation. Il est recommandé que seul le compte du système d’exploitation utilisé pour exécuter le serveur d’applications dispose d’un accès en lecture et écriture à ce répertoire.


1. Dans la console d’administration, sélectionnez **[!UICONTROL Paramètres > Paramètres du système principal > Configurations]**.
1. Sur la page Configurations principales, modifiez les options selon vos besoins, puis sélectionnez **[!UICONTROL OK]**. Pour plus d’informations sur les options, voir [Options des configurations de base](configure-general-aem-forms-settings.md#core-configurations-options).


## Options des configurations de base {#core-configurations-options}

**Emplacement du répertoire temporaire** Le chemin d’accès au répertoire dans lequel AEM Forms créera les fichiers temporaires de produit. Si la valeur de ce paramètre est vide, l’emplacement est défini par défaut sur le répertoire temporaire système. Assurez-vous que le répertoire temporaire est un dossier modifiable.

>[!NOTE]
>
>Assurez-vous que le répertoire temporaire se trouve sur le système de fichiers local. AEM Forms ne prend pas en charge de répertoire temporaire à un emplacement distant.

**Répertoire racine de stockage global de documents** Le répertoire racine de stockage global de documents est utilisé aux fins suivantes :

* Stockez des documents de longue durée. Les documents de longue durée n’ont pas de délai d’expiration et persistent jusqu’à leur suppression (par exemple, les fichiers PDF utilisés dans un processus de workflow). Ils participent pleinement au statut global du système. Si une partie ou la totalité de ces documents est perdue ou corrompue, le serveur Forms peut devenir instable. Par conséquent, il est important que ce répertoire soit stocké sur un périphérique RAID.
* Stockez les documents temporaires nécessaires pendant le traitement.

>[!NOTE]
>
>Vous pouvez également activer le stockage de documents dans la base de données d’AEM Forms. Toutefois, les performances du système sont meilleures lorsque vous utilisez le répertoire de stockage global de documents.

* Transfert de documents entre les nœuds d’un cluster. Si vous exécutez AEM Forms dans un environnement organisé en clusters, ce répertoire doit être accessible à partir de tous les nœuds du cluster.
* Réception de paramètres entrants à partir d’appels d’API distantes.

Si vous ne spécifiez pas de répertoire racine de stockage global de documents, le répertoire est défini par défaut sur un répertoire de serveur d’applications :

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

>[!NOTE]
>
>La modification de la valeur du paramètre de répertoire racine de stockage global de documents doit faire l’objet d’une mûre réflexion. Le répertoire de stockage global de documents est utilisé pour stocker les fichiers de longue durée utilisés dans un processus, ainsi que les composants critiques du produit AEM Forms. Le changement de l’emplacement du répertoire de stockage global de documents représente une modification majeure du système. Une configuration incorrecte de l’emplacement du répertoire de stockage global de documents rend AEM Forms inopérant et peut nécessiter une réinstallation complète de l’application. Si vous spécifiez un nouvel emplacement pour le répertoire de stockage global de documents, le serveur d’applications doit être arrêté et les données migrées avant le redémarrage du serveur. L’administrateur ou l’administratrice système doit déplacer tous les fichiers de l’ancien emplacement vers le nouveau, tout en conservant la structure de répertoires interne.

>[!NOTE]
>
>n’indiquez pas le même répertoire pour le répertoire temporaire et le répertoire de stockage global de documents..

Pour plus d’informations sur le répertoire de stockage global de documents, consultez [Préparation à l’installation d’AEM Forms sur un seul serveur](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63_fr).

**Emplacement du répertoire des polices du serveur Adobe** *ndash; Saisissez le chemin d’accès au répertoire qui contient les polices du serveur Adobe. Ces polices sont installées avec AEM forms. L’emplacement par défaut de ces polices est le répertoire [racine aem-forms]/fonts. Si ce répertoire n’est pas accessible, vous pouvez copier les polices dans un autre répertoire et utiliser ce paramètre pour spécifier son nouvel emplacement.

**Emplacement du répertoire des polices du client** *ndash; Saisissez le chemin d’accès à un répertoire contenant les polices supplémentaires que vous souhaitez utiliser.

***Remarque ** : les polices sont sélectionnées à partir du cache des polices du système Windows et un redémarrage du système est requis pour mettre à jour le cache. Après avoir spécifié le répertoire des polices du client, assurez-vous de redémarrer le système sur lequel AEM forms est installé.*

**Emplacement du répertoire des polices système** *ndash; Saisissez le chemin d’accès au répertoire des polices fourni par votre système d’exploitation. Vous pouvez ajouter plusieurs répertoires en les séparant par des points-virgules **;**.

**Emplacement du fichier de configuration des services de données** *ndash; Indique l’emplacement du fichier services-config.xml. Par défaut, ce fichier est incorporé dans le fichier adobe-core-appserver.ear et n’est pas accessible aux utilisateurs et utilisatrices. Une copie du fichier services-config.xml par défaut se trouve dans [racine aem-forms]\sdk\misc\DataServices\Server-Configuration. Si vous avez modifié ce fichier et que vous l’avez déplacé, saisissez le nouvel emplacement dans ce champ.

Le fichier de configuration des services de données permet de personnaliser les paramètres de ces derniers, tels que le type d’authentification et la sortie de débogage.

Ce paramètre est vide par défaut.

**Taille maximale du document en ligne par défaut (en octets)** *ndash; Le nombre maximal d’octets conservés en mémoire lors de la transmission de documents entre divers composants d’AEM Forms. Utilisez ce paramètre pour optimiser les performances. Les documents d’une taille inférieure à cette valeur sont stockés en mémoire et conservés dans la base de données. Les documents qui dépassent cette valeur sont stockés sur le disque dur.

Ce paramètre est obligatoire. La valeur par défaut est 65 536 octets.

**Délai par défaut avant suppression du document (en secondes)** *ndash; Durée maximale, en secondes, pendant laquelle un document transmis entre divers composants d’AEM Forms est considéré comme actif. Lorsque ce délai est écoulé, les fichiers utilisés pour stocker ce document peuvent être supprimés. Utilisez ce paramètre pour gérer l’espace disque disponible.

Ce paramètre est obligatoire. La valeur par défaut est de 600 secondes.

**Intervalle de balayage du document (en secondes)** *ndash; La durée, en secondes, entre les tentatives de suppression des fichiers obsolètes et qui étaient utilisés pour transmettre les données du document entre les services.

Ce paramètre est obligatoire. La valeur par défaut est de 30 secondes.

**Activer le FIPS** *ndash; Sélectionnez cette option pour activer le mode FIPS. Le FIPS (Federal Information Processing Standard) 140-2 est un standard de chiffrement défini par le gouvernement des États-Unis. En mode FIPS, AEM Forms limite la protection des données aux algorithmes approuvés FIPS 140-2 en utilisant le module de chiffrement RSA BSAFE Crypto-C 2.1.

Le mode FIPS ne prend pas en charge les algorithmes de chiffrement utilisés dans les versions Adobe Acrobat® antérieures à la version 7.0. Si le mode FIPS est activé et que vous utilisez le service Encryption pour chiffrer le PDF à l’aide d’un mot de passe avec un niveau de compatibilité défini sur Acrobat 5, vous obtenez une erreur de chiffrement.

En général, lorsque le mode FIPS est activé, le service Assembler n’applique le chiffrement du mot de passe à aucun document. En cas de tentative, une exception FIPSModeException est générée pour indiquer que « Le chiffrement du mot de passe n’est pas autorisé en mode FIPS ». En outre, l’élément PDFsFromBookmarks DDX (Document Description XML) n’est pas pris en charge en mode FIPS lorsque le document de base est chiffré par mot de passe.

>[!NOTE]
>
>Le logiciel AEM Forms ne valide pas le code pour assurer la compatibilité FIPS. Il fournit un mode de fonctionnement FIPS permettant d’utiliser les algorithmes certifiés FIPS pour les services de chiffrement des bibliothèques certifiées FIPS (RSA).

**Activer le WSDL** *ndash; Sélectionnez cette option pour activer la génération du Web Service Definition Language (WSDL) pour tous les services qui font partie d’AEM Forms.

Activez cette option dans les environnements de développement, dans lesquels l’équipe de développement fait appel à une génération WSDL pour créer ses applications clientes. Vous pouvez choisir de désactiver la génération WSDL dans un environnement de production pour éviter d’exposer les détails internes d’un service.

**Activer le stockage de documents dans la base de données** *ndash; Sélectionnez cette option pour stocker les documents de longue durée dans la base de données d’AEM Forms. L’activation de cette option ne supprime pas la nécessité d’utiliser un répertoire de stockage global de documents. Cependant, la sélection de cette option simplifie les sauvegardes d’AEM Forms. Pour effectuer une sauvegarde lorsque vous utilisez uniquement le répertoire de stockage global de documents, vous devez définir le système AEM Forms en mode de sauvegarde, puis effectuer les sauvegardes de la base de données et du répertoire de stockage global de documents. Si vous sélectionnez l’option de base de données, il est nécessaire, pour effectuer une sauvegarde, d’effectuer la sauvegarde de la base de données pour une nouvelle installation ou d’effectuer la sauvegarde de la base de données et la sauvegarde individuelle du répertoire de stockage global de documents pour une mise à niveau. Par rapport à une configuration impliquant uniquement un répertoire de stockage global de documents, une gestion plus approfondie de la base de données peut être requise pour purger les travaux et les données (voir Options de sauvegarde dans le cas de l’utilisation de la base de données pour le stockage de documents).

**Activer la statistique d’appel de DSC** *ndash; Lorsque cette option est sélectionnée, AEM Forms effectue le suivi des statistiques d’appels, telles que le nombre d’appels, la durée de ces derniers et le nombre d’erreurs dans les appels. Ces informations sont stockées dans un fichier bean JMX afin que vous puissiez utiliser l’outil JConsole Java™ ou un logiciel tiers pour consulter les statistiques. Si vous ne souhaitez pas consulter ces statistiques, désélectionnez cette option afin d’améliorer les performances d’AEM Forms.

**Activer RDS** *ndash; La sélection de cette option active le servlet RDS (Remote Development Services) dans AEM Forms. Lorsque cette option est activée, les outils côté client peuvent interagir avec les services de données dans le but de déployer ou d’annuler le déploiement de modèles afin de créer des destinations et des points d’entrée, ou de déterminer quel modèle a été déployé dans quel point d’entrée. Par défaut, cette option n’est pas sélectionnée.

**Autoriser les requêtes RDS non sécurisées** *ndash; Lorsque cette option est sélectionnée, les requêtes RDS n’ont pas besoin d’utiliser https. Par défaut, cette option n’est pas sélectionnée et toutes les communications avec Data Services doivent avoir recours à des requêtes https.

**Autoriser le chargement de documents non sécurisés à partir d’applications Flex :** *ndash; Le servlet de chargement de fichiers utilisé pour charger des documents depuis des applications Adobe Flex® vers AEM Forms nécessite que les personnes soient authentifiées et autorisées avant de pouvoir charger des documents. La personne doit disposer d’un rôle Utilisateur ou utilisatrice de l’application de chargement de documents ou d’un autre rôle incluant l’autorisation de chargement de documents. Cela empêche des personnes non autorisées de charger des documents vers le serveur AEM Forms. Sélectionnez cette option si vous souhaitez désactiver cette fonctionnalité de sécurité dans un environnement de développement ou dans une rétrocompatibilité avec des versions antérieures d’AEM Forms. Par défaut, cette option n’est pas sélectionnée. Pour plus d’informations, consultez la section « Appeler AEM Forms à l’aide d’AEM Forms Remoting » dans Programmation avec AEM Forms.

**Autoriser le chargement de documents non sécurisés à partir d’applications Java SDK :** les chargements HTTP de DocumentManager doivent être sécurisés. Par défaut, les chargements HTTP nécessitent l’authentification et l’autorisation des utilisateurs et des utilisatrices pour charger les documents. L’utilisateur ou l’utilisatrice doit se voir attribuer le rôle Utilisateur des services ou un autre rôle contenant l’autorisation Service Invoke. Cela permet d’empêcher les personnes non autorisées de charger des documents vers le serveur Forms. Sélectionnez cette option si vous souhaitez désactiver cette fonctionnalité de sécurité dans un environnement de développement, pour une rétrocompatibilité avec les versions précédentes d’AEM Forms ou en fonction de la configuration de votre pare-feu. Par défaut, cette option n’est pas sélectionnée. Pour plus d’informations, consultez la section « Appeler AEM Forms à l’aide de l’API Java » dans Programmation avec AEM Forms.
