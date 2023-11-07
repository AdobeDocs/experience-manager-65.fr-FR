---
title: Paramètres généraux d’AEM Forms
seo-title: General AEM Forms settings
description: Découvrez comment configurer les paramètres de la page Configurations de base dans Administration Console afin d’améliorer les performances du système.
seo-description: Learn to configure the Core Configurations page settings in administration console that can help improve system performance.
uuid: 940680fd-b7ab-4376-aa5b-e139223522ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: bd648c38-731b-420e-973d-a4728b69868e
exl-id: e1519477-b5a8-4947-8597-26b945a3b819
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1707'
ht-degree: 31%

---

# Paramètres généraux d’AEM Forms {#general-aem-forms-settings}

La page Configurations de base d’Administration Console fournit des paramètres qui peuvent améliorer les performances du système. Après avoir configuré ou mis à jour ces paramètres, redémarrez votre serveur d’applications.

Pour plus d’informations sur l’activation du mode de sauvegarde sécurisé, voir [Activation et désactivation du mode de sauvegarde sécurisé](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode).


>[!NOTE]
>
>Les fichiers du répertoire temporaire et les documents de longue durée du répertoire racine de stockage global de documents peuvent contenir des informations utilisateur sensibles, telles que des informations qui nécessitent des informations d’identification spéciales lors de l’accès à l’aide des API ou des interfaces utilisateur. Par conséquent, il est important que ce répertoire soit correctement sécurisé à l’aide des méthodes disponibles pour le système d’exploitation. Il est recommandé que seul le compte du système d’exploitation utilisé pour exécuter le serveur d’applications dispose d’un accès en lecture et écriture à ce répertoire.


1. Dans la console d’administration, cliquez sur **[!UICONTROL Paramètres > Paramètres du système principal > Configurations]**.
1. Sur la page Configurations principales, modifiez les options selon vos besoins, puis cliquez sur **[!UICONTROL OK]**. Pour plus d’informations sur les options, voir [Options des configurations principales](configure-general-aem-forms-settings.md#core-configurations-options).


## Options des configurations principales {#core-configurations-options}

**Emplacement du répertoire temporaire** Le chemin d’accès au répertoire dans lequel AEM Forms créera les fichiers temporaires de produit. Si la valeur de ce paramètre est vide, l’emplacement est défini par défaut sur le répertoire temporaire système. Assurez-vous que le répertoire temporaire est un dossier modifiable.

>[!NOTE]
>
>Assurez-vous que le répertoire temporaire se trouve sur le système de fichiers local. AEM forms ne prend pas en charge un répertoire temporaire à un emplacement distant.

**Répertoire racine de stockage global de documents** Le répertoire racine de stockage global de documents est utilisé aux fins suivantes :

* Stockage de documents de longue durée. Les documents de longue durée n’ont pas de délai d’expiration et persistent jusqu’à ce qu’ils soient supprimés (par exemple, les fichiers de PDF utilisés dans un processus de workflow). Les documents de longue durée constituent une partie essentielle de l’état global du système. Si certains ou tous ces documents sont perdus ou corrompus, le serveur Forms peut devenir instable. Par conséquent, il est important que ce répertoire soit stocké sur un périphérique RAID.
* Stockage des documents temporaires nécessaires pendant le traitement.

>[!NOTE]
>
>Vous pouvez également activer le stockage de documents dans la base de données d’AEM forms. Toutefois, les performances du système sont meilleures lorsque vous utilisez le répertoire de stockage global de documents.

* Transfert de documents entre les noeuds d’une grappe. Si vous exécutez AEM forms dans un environnement organisé en grappes, ce répertoire doit être accessible à partir de tous les noeuds de la grappe.
* Réception des paramètres entrants à partir d’appels API distants.

Si vous ne spécifiez pas de répertoire racine de stockage global de documents, le répertoire est défini par défaut sur un répertoire de serveur d’applications :

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

>[!NOTE]
>
>La modification de la valeur du paramètre de répertoire racine de stockage global de documents doit être effectuée avec une attention particulière. Le répertoire de stockage global de documents est utilisé pour stocker les fichiers de longue durée utilisés dans un processus et les composants de produit d’AEM forms critiques. La modification de l’emplacement du répertoire de stockage global de documents est un changement majeur du système. Une configuration incorrecte de l’emplacement du répertoire de stockage global de documents rend AEM forms inopérant et peut nécessiter une réinstallation complète d’AEM forms. Si vous spécifiez un nouvel emplacement pour le répertoire de stockage global de documents, le serveur d’applications doit être arrêté et les données migrées avant le redémarrage du serveur. L’administrateur système doit déplacer tous les fichiers de l’ancien emplacement vers le nouvel emplacement, tout en conservant la structure de répertoires interne.

>[!NOTE]
>
>n’indiquez pas le même répertoire pour le répertoire temporaire et le répertoire de stockage global de documents..

Pour plus d’informations sur le répertoire de stockage global de documents, consultez [Préparation à l’installation d’AEM Forms sur un seul serveur](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63_fr).

**Emplacement du répertoire des polices du serveur Adobe** Saisissez le chemin d’accès au répertoire qui contient les polices du serveur Adobe. Ces polices sont installées avec AEM forms. L’emplacement par défaut de ces polices est le répertoire [racine aem-forms]/fonts. Si ce répertoire n’est pas accessible, vous pouvez copier les polices dans un autre répertoire et utiliser ce paramètre pour spécifier son nouvel emplacement.

**Emplacement du répertoire des polices du client** Saisissez le chemin d’accès à un répertoire contenant les polices supplémentaires que vous souhaitez utiliser.

***Remarque ** : les polices sont sélectionnées à partir du cache des polices du système Windows et un redémarrage du système est requis pour mettre à jour le cache. Après avoir spécifié le répertoire des polices du client, assurez-vous de redémarrer le système sur lequel AEM forms est installé.*

**Emplacement du répertoire des polices système** Saisissez le chemin d’accès au répertoire des polices fourni par votre système d’exploitation. Vous pouvez ajouter plusieurs répertoires en les séparant par des points-virgules **;**.

**Emplacement du fichier de configuration des services de données** Indique l’emplacement du fichier services-config.xml. Par défaut, ce fichier est incorporé au fichier adobe-core-appserver.ear et n’est pas accessible aux utilisateurs. Une copie du fichier services-config.xml par défaut se trouve dans [racine aem-forms]\sdk\misc\DataServices\Server-Configuration. Si vous avez modifié ce fichier et que vous l’avez déplacé, saisissez le nouvel emplacement dans ce champ.

Le fichier de configuration des services de données permet de personnaliser les paramètres des services de données, tels que le type d’authentification et la sortie de débogage.

Ce paramètre est vide par défaut.

**Taille maximale du document en ligne par défaut (octets)** Le nombre maximal d’octets conservés en mémoire lors de la transmission de documents entre divers composants d’AEM Forms. Utilisez ce paramètre pour optimiser les performances. Les documents plus petits que ce nombre sont stockés en mémoire et conservés dans la base de données. Les documents qui dépassent cette limite sont stockés sur le disque dur.

Ce paramètre est obligatoire. La valeur par défaut est de 6 536 octets.

**Délai par défaut avant suppression du document (secondes)** Durée maximale, en secondes, pendant laquelle un document transmis entre divers composants d’AEM Forms est considéré comme actif. Une fois ce délai écoulé, les fichiers utilisés pour stocker ce document peuvent être supprimés. Utilisez ce paramètre pour contrôler l’utilisation de l’espace disque.

Ce paramètre est obligatoire. La valeur par défaut est de 600 secondes.

**Intervalle de balayage du document (secondes)** La durée, en secondes, entre les tentatives de suppression des fichiers obsolètes et qui étaient utilisés pour transmettre les données du document entre les services.

Ce paramètre est obligatoire. La valeur par défaut est de 30 secondes.

**Activer FIPS** Sélectionnez cette option pour activer le mode FIPS. La norme FIPS (Federal Information Processing Standard) 140-2 est une norme de chiffrement définie par le gouvernement américain. Lors de l’exécution en mode FIPS, AEM forms limite la protection des données aux algorithmes approuvés FIPS 140-2 à l’aide du module de chiffrement RSA BSAFE Crypto-C 2.1.

Le mode FIPS ne prend pas en charge les algorithmes de chiffrement utilisés dans les versions Adobe Acrobat® antérieures à la version 7.0. Si le mode FIPS est activé et que vous utilisez le service Encryption pour chiffrer le PDF à l’aide d’un mot de passe avec un niveau de compatibilité défini sur Acrobat 5, la tentative de chiffrement échoue avec une erreur.

En règle générale, lorsque FIPS est activé, le service Assembler n’applique le chiffrement du mot de passe à aucun document. En cas de tentative, une exception FIPSModeException est générée pour indiquer que &quot;Le chiffrement du mot de passe n’est pas autorisé en mode FIPS&quot;. De plus, l’élément PDFsFromBookmarks DDX (Document Description XML) n’est pas pris en charge en mode FIPS lorsque le document de base est chiffré par mot de passe.

>[!NOTE]
>
>AEM logiciel forms ne valide pas le code pour assurer la compatibilité FIPS. Il fournit un mode de fonctionnement FIPS qui permet d’utiliser les algorithmes approuvés FIPS pour les services de cryptographie des bibliothèques certifiées FIPS (RSA).

**Activer le WSDL** Sélectionnez cette option pour activer la génération du Web Service Definition Language (WSDL) pour tous les services qui font partie d’AEM Forms.

Activez cette option dans les environnements de développement, où les développeurs utilisent la génération WSDL pour créer leurs applications clientes. Vous pouvez choisir de désactiver la génération WSDL dans un environnement de production afin d’éviter d’exposer les détails internes d’un service.

**Activer le stockage de documents dans la base de données** Sélectionnez cette option pour stocker les documents de longue durée dans la base de données d’AEM Forms. L’activation de cette option ne supprime pas la nécessité d’utiliser un répertoire de stockage global de documents. Toutefois, le choix de cette option simplifie AEM sauvegardes de formulaires. Si vous utilisez uniquement le répertoire de stockage global de documents, une sauvegarde consiste à mettre AEM système AEM forms en mode de sauvegarde, puis à effectuer les sauvegardes de la base de données et du répertoire de stockage global de documents. Si vous sélectionnez l’option de base de données, la sauvegarde consiste à effectuer la sauvegarde de la base de données pour une nouvelle installation ou à effectuer la sauvegarde de la base de données et la sauvegarde unique du répertoire de stockage global de documents pour une mise à niveau. Une gestion supplémentaire de votre base de données peut être nécessaire pour purger les tâches et les données par rapport à une configuration du répertoire de stockage global de documents uniquement. (voir Options de sauvegarde dans le cas de l’utilisation de la base de données pour le stockage de documents).

**Activer la statistique d’invocation de DSC** Lorsque cette option est sélectionnée, AEM Forms effectue le suivi des statistiques d’invocation, telles que le nombre d’invocations, la durée de ces dernières et le nombre d’erreurs dans les invocations. Ces informations sont stockées dans un bean JMX afin que vous puissiez utiliser Java™ JConsole ou un logiciel tiers pour consulter les statistiques. Si vous ne souhaitez pas afficher ces statistiques, désélectionnez cette option pour améliorer les performances d’AEM forms.

**Activer RDS** La sélection de cette option active le servlet RDS (Remote Development Services) dans AEM Forms. Lorsque cette option est activée, les outils côté client peuvent interagir avec les services de données pour effectuer des opérations comme déployer ou annuler le déploiement de modèles pour créer des destinations et des points de terminaison, ou pour déterminer les modèles qui ont été déployés dans des points de terminaison. Par défaut, cette option n’est pas sélectionnée.

**Autoriser une requête RDS non sécurisée** Lorsque cette option est sélectionnée, les demandes RDS n’ont pas besoin d’utiliser https. Par défaut, cette option n’est pas sélectionnée et toutes les communications destinées à Data Services ont recours à des demandes en mode https.

**Autoriser le téléchargement de documents non sécurisés à partir d’applications Flex :** Le servlet de téléchargement de fichiers utilisé pour charger des documents à partir des applications Adobe Flex® vers AEM forms exige que les utilisateurs soient authentifiés et autorisés avant de pouvoir télécharger des documents. L’utilisateur doit se voir attribuer le rôle Utilisateur de l’application de téléchargement de document ou un autre rôle incluant l’autorisation de téléchargement de document. Cela permet d’empêcher les utilisateurs non autorisés de télécharger des documents vers le serveur d’AEM forms. Sélectionnez cette option si vous souhaitez désactiver cette fonction de sécurité dans un environnement de développement ou pour une compatibilité descendante avec les versions précédentes d’AEM forms. Par défaut, cette option n’est pas sélectionnée. Pour plus d’informations, consultez la section « Appeler AEM Forms à l’aide d’AEM Forms Remoting » dans Programmation avec AEM Forms.

**Autoriser le téléchargement de documents non sécurisés à partir d’applications Java SDK :** Les téléchargements HTTP DocumentManager doivent être sécurisés. Par défaut, les téléchargements HTTP nécessitent que les utilisateurs soient authentifiés et autorisés avant de pouvoir télécharger des documents. L’utilisateur doit se voir attribuer le rôle Utilisateur des services ou un autre rôle contenant l’autorisation Service Invoke . Cela permet d’empêcher les utilisateurs non autorisés de télécharger des documents vers le serveur Forms. Sélectionnez cette option si vous souhaitez désactiver cette fonctionnalité de sécurité dans un environnement de développement, pour une compatibilité descendante avec les versions précédentes d’AEM forms ou en fonction de la configuration de votre pare-feu. Par défaut, cette option n’est pas sélectionnée. Pour plus d’informations, consultez la section « Appeler AEM Forms à l’aide de l’API Java » dans Programmation avec AEM Forms.
