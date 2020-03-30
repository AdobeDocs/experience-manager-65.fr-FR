---
title: Paramètres généraux d’AEM Forms
seo-title: Paramètres généraux d’AEM Forms
description: Apprenez à configurer les paramètres de la page Configurations de base dans la console d’administration qui peuvent améliorer les performances système.
seo-description: Apprenez à configurer les paramètres de la page Configurations de base dans la console d’administration qui peuvent améliorer les performances système.
uuid: 940680fd-b7ab-4376-aa5b-e139223522ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: bd648c38-731b-420e-973d-a4728b69868e
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Paramètres généraux d’AEM Forms {#general-aem-forms-settings}

La page Configurations de base d’Administration Console permet de configurer les paramètres qui peuvent améliorer les performances du système. Après avoir configuré ou mis à jour ces paramètres, redémarrez votre serveur d’applications.

Pour plus d’informations sur l’activation du mode de sauvegarde sécurisé, voir [Activation et désactivation du mode de sauvegarde sécurisé ](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode).


>[!NOTE]
>
>les fichiers du répertoire temporaire et les documents de longue durée du répertoire racine de stockage global de documents peuvent contenir des informations utilisateur sensibles nécessitant des informations d’identification spéciales lorsqu’elles sont consultées via les API ou des interfaces utilisateur. Il est donc important que ce répertoire soit sécurisé à l’aide de l’une des méthodes utilisables par le système d’exploitation. Il est préférable que seul le compte système d’exploitation utilisé pour exécuter le serveur d’applications dispose d’un accès en lecture et en écriture sur ce répertoire.


1. In administration console, click **[!UICONTROL Settings > Core System Settings > Configurations]**.
1. On the Core Configurations page, change the options as required and click **[!UICONTROL OK]**. Pour plus d’informations sur les options, voir [Options Configurations de base](configure-general-aem-forms-settings.md#core-configurations-options).


## Options Configurations de base {#core-configurations-options}

**Emplacement du répertoire** temporaire Chemin du répertoire dans lequel AEM forms crée des fichiers temporaires de produit. Si la valeur de ce paramètre est vide, l’emplacement par défaut est le répertoire temporaire système. Assurez-vous que le répertoire temporaire est un dossier modifiable.

***Remarque ** : assurez-vous que le répertoire temporaire se trouve sur le système de fichiers local. AEM forms ne prend pas en charge un répertoire temporaire à un emplacement distant.*

**Répertoire** racine de l’   globale Le répertoire racine du de(GDS) global est utilisé aux fins suivantes :

* Stockage de documents de longue durée. Les documents de longue durée ne sont assortis d’aucune date d’expiration et sont conservés jusqu’à leur suppression (fichiers PDF utilisés dans un processus de flux de production, par exemple). Les documents de longue durée représentent une partie stratégique de l’état du système global. Si certains d’entre eux sont perdus ou corrompus, le serveur Forms peut devenir instable. De ce fait, il est important de stocker ce répertoire sur un périphérique RAID.
* Stockage de documents temporaires nécessaires au cours du traitement.

   ***Remarque ** : vous pouvez également activer le stockage de documents dans la base de données AEM Forms. Cependant, les performances du système sont meilleures lorsque vous utilisez le répertoire de stockage global de documents.*

* Transfert de documents entre les nœuds d’un groupe de serveurs. Si vous exécutez AEM forms dans un environnement en grappe, ce répertoire doit être accessible à partir de tous les nœuds de la grappe.
* Réception de paramètres entrants à partir d’appels d’API distantes.

Si vous ne spécifiez pas un répertoire racine de stockage global de documents, le système valide un répertoire du serveur d’applications :

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

***Remarque ** : toute modification de la valeur du paramètre de répertoire racine de stockage global de documents doit faire l’objet d’un soin particulier. Ce répertoire stocke les fichiers de longue durée utilisés dans un processus, ainsi que les composants critiques du produit AEM forms. Le changement de l’emplacement du répertoire de stockage global de documents représente une modification majeure du système. Une mauvaise configuration de cet emplacement rend AEM forms inopérant et peut nécessiter une réinstallation complète de ce dernier. Si vous spécifiez un nouvel emplacement pour le répertoire de stockage global de documents, le serveur d’applications doit être arrêté et les données migrées avant le redémarrage du serveur. L’administrateur système doit déplacer tous les fichiers de l’ancien emplacement vers le nouvel emplacement en conservant l’arborescence interne.*

***Remarque ** : n’indiquez pas le même répertoire pour le répertoire temporaire et le répertoire de stockage global de documents.*

Pour plus d’informations sur le répertoire de stockage global de documents, consultez [Préparation à l’installation d’AEM Forms sur un seul serveur](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

**Emplacement du répertoire** des polices Adobe Server Tapez le chemin d’accès au répertoire contenant les polices du serveur Adobe. Ces polices sont installées avec AEM forms. The default location for these fonts is the [aem-forms root]/fonts directory. Si ce répertoire n’est pas accessible, vous pouvez copier les polices dans un autre répertoire et utiliser ce paramètre pour spécifier son nouvel emplacement.

**Emplacement du répertoire** des polices du client Entrez le chemin d’accès à un répertoire contenant des polices supplémentaires que vous souhaitez utiliser.

***Remarque ** : les polices sont sélectionnées à partir du cache des polices du système Windows et un redémarrage du système est requis pour mettre à jour le cache. Après avoir spécifié le répertoire des polices du client, assurez-vous de redémarrer le système sur lequel AEM forms est installé.*

**Emplacement du répertoire** des polices système Entrez le chemin d’accès au répertoire des polices fourni par votre système d’exploitation. Vous pouvez ajouter plusieurs répertoires en les séparant par des points-virgules **;**.

**Emplacement du fichier** de configuration de Data Services Indique l’emplacement du fichier services-config.xml. Par défaut, ce fichier est incorporé dans le fichier adobe-core-appserver.ear et n’est pas accessible aux utilisateurs. A copy of the default services-config.xml file is located in [aem-forms root]\sdk\misc\DataServices\Server-Configuration. Si vous avez modifié ce fichier puis déplacé ce fichier, saisissez son nouvel emplacement dans ce champ.

Le fichier de configuration des services de données permet de personnaliser les paramètres des services de données, comme le type d’authentification et les résultats du débogage.

Ce paramètre est vide par défaut.

**Taille maximale par défaut de la ligne d’entrée (octets)** du Nombre maximal d’octets conservés en mémoire lors de la transmission de entre différents composants d’AEM forms. Utilisez ce paramètre afin d’améliorer les performances du système. Les documents d’une taille inférieure à cette valeur sont stockés en mémoire et conservés dans la base de données. Les documents qui dépassent cette valeur sont stockés sur le disque dur.

ce paramètre est obligatoire. La valeur par défaut est 65 536 octets.

**Délai d’expiration de  par défaut (secondes)** Durée maximale (en secondes) pendant laquelle un transmis entre différents composants d’AEM forms est considéré comme actif. Lorsque ce délai est écoulé, les fichiers utilisés pour stocker ce document peuvent être supprimés. Utilisez ce paramètre pour gérer l’espace disque disponible.

ce paramètre est obligatoire. La valeur par défaut est de 600 secondes.

**Intervalle de balayage  (secondes)** Durée, en secondes, entre les tentatives de suppression de fichiers devenus inutiles et utilisés pour transmettre des données de entre les services.

ce paramètre est obligatoire. La valeur par défaut est de 30 secondes.

**Activer FIPS** Sélectionnez cette option pour activer le mode FIPS. Le FIPS (Federal Information Processing Standard) 140-2 est un standard de chiffrement défini par le gouvernement américain. En mode FIPS, AEM forms limite la protection des données aux algorithmes approuvés FIPS 140-2 utilisant le module de chiffrement RSA BSAFE Crypto-C 2.1.

Le mode FIPS ne prend pas en charge les algorithmes de chiffrement utilisés dans les versions d’Adobe Acrobat® antérieures à la version 7.0. Si le mode FIPS est activé et que vous utilisez le service Encryption pour chiffrer le PDF à l’aide d’un mot de passe avec un niveau de compatibilité défini sur Acrobat 5, vous obtenez une erreur de chiffrement.

En général, lorsque le mode FIPS est activé, le service Assembler n’applique le chiffrement du mot de passe à aucun document. En cas de tentative, une exception FIPSModeException est générée pour indiquer que « Le chiffrement du mot de passe n’est pas autorisé en mode FIPS ». En outre, l’élément PDFsFromBookmarks DDX (Document Description XML) n’est pas pris en charge en mode FIPS lorsque le document de base est chiffré par mot de passe.

***Remarque ** : le logiciel AEM Forms ne valide pas le code pour assurer la compatibilité FIPS. Il fournit un mode de fonctionnement FIPS permettant d’utiliser les algorithmes certifiés FIPS pour les services de cryptographie des bibliothèques certifiées FIPS (RSA).*

**Activer WSDL** Sélectionnez cette option pour activer la génération WSDL (Web Service Definition Language) pour tous les services faisant partie d’AEM forms.

Activez cette option dans les environnements de développement, dans lesquels les développeurs font appel à une génération WSDL pour créer leurs applications clientes. Vous pouvez choisir de désactiver la génération WSDL dans un environnement de production pour éviter d’exposer les détails internes d’un service.

**Activez    dans la base de données** Sélectionnez cette option pour stocker les données de longue durée dans la base de données AEM forms. L’activation de cette option ne supprime pas la nécessité d’utiliser un répertoire de stockage global de documents. Cependant, la sélection de cette option simplifie les sauvegardes d’AEM forms. Pour effectuer une sauvegarde lorsque vous utilisez uniquement le répertoire de stockage global de documents, vous devez définir le système AEM forms en mode de sauvegarde, puis effectuer les sauvegardes de la base de données et du répertoire de stockage global de documents. Si vous sélectionnez l’option de base de données, il est nécessaire, pour effectuer une sauvegarde, d’effectuer la sauvegarde de la base de données avant une nouvelle installation ou de terminer cette sauvegarde et d’effectuer la sauvegarde individuelle du répertoire de stockage global de documents avant une mise à niveau. Par rapport à une configuration impliquant uniquement un répertoire de stockage global de documents, une gestion plus approfondie de la base de données peut être requise pour purger les travaux et les données (voir Options de sauvegarde dans le cas de l’utilisation de la base de données pour le stockage de documents).

**Activer la statistique** d’appel DSC Lorsque cette option est sélectionnée, AEM forms effectue le suivi des statistiques d’appel, telles que le nombre d’appels, le temps nécessaire pour appeler et le nombre d’erreurs dans les appels. Ces informations sont stockées dans un fichier bean JMX afin que vous puissiez utiliser l’outil JConsole Java™ ou un logiciel tiers pour consulter les statistiques. Si vous ne souhaitez pas consulter ces statistiques, désélectionnez cette option afin d’améliorer les performances d’AEM forms.

**Activer RDS** La sélection de cette option active la servlet RDS (Remote Development Services) dans AEM forms. Lorsque cette option est activée, les outils côté client peuvent interagir avec Data Services dans le but de déployer ou d’annuler le déploiement de modèles afin de créer des destinations et des points de fin, ou de déterminer quel modèle a été déployé dans quel point de fin. Par défaut, cette option n’est pas sélectionnée.

**Autoriser une requête** RDS non sécurisée Lorsque cette option est sélectionnée, les requêtes RDS n’ont pas besoin d’utiliser https. Par défaut, cette option n’est pas sélectionnée et toutes les communications destinées à Data Services ont recours à des demandes en mode https.

**Autoriser le téléchargement de  non sécurisés à partir d’applications Flex :** La servlet de téléchargement de fichiers utilisée pour télécharger des  depuis les applications Adobe Flex® vers AEM forms exige que les utilisateurs soient authentifiés et autorisés avant de pouvoir télécharger des  de. L’utilisateur doit disposer d’un rôle Utilisateur de l’application de téléchargement de documents ou d’un autre rôle incluant l’autorisation de téléchargement de documents. Ce dispositif empêche des utilisateurs non autorisés de télécharger des documents vers AEM forms. Sélectionnez cette option si vous souhaitez désactiver cette sécurité, dans le cadre d’un environnement de développement ou d’une compatibilité ascendante avec des versions antérieures d’AEM forms. Par défaut, cette option n’est pas sélectionnée. Pour plus d’informations, consultez la section « Appel d’AEM Forms à l’aide d’AEM Forms Remoting » dans Programmation avec AEM Forms.

**Autoriser le téléchargement de  non sécurisés à partir d’applications Java SDK :** Les téléchargements HTTP DocumentManager doivent être sécurisés. Par défaut, les téléchargements HTTP nécessitent que les utilisateurs soient authentifiés et autorisés avant de pouvoir télécharger les documents. L’utilisateur doit disposer d’un rôle Utilisateur des services ou d’un autre rôle incluant l’autorisation d’appel de services. Ce dispositif empêche des utilisateurs non autorisés de télécharger des documents vers le serveur Forms. Sélectionnez cette option si vous souhaitez désactiver cette sécurité, dans le cadre d’un environnement de développement, d’une compatibilité ascendante avec des versions antérieures d’AEM forms ou en fonction de la configuration de votre pare-feu. Par défaut, cette option n’est pas sélectionnée. Pour plus d’informations, consultez la section « Appel d’AEM Forms à l’aide de l’API Java » dans Programmation avec AEM Forms.
