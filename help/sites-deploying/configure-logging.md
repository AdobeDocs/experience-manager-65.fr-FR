---
title: Journalisation
seo-title: Logging
description: Découvrez comment configurer des paramètres globaux pour le service de journalisation central, des paramètres spécifiques pour les services individuels ou comment demander la journalisation des données.
seo-description: Learn how to configure global parameters for the central logging service, specific settings for the individual services or how to request data logging.
uuid: 8c9e3628-2f2c-445d-9706-5c7725b85fe2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5aa69b10-2cd0-4d34-8104-8c3b88405926
feature: Configuring
exl-id: b32001a1-0078-43f6-89d6-781d6d2e9c94
source-git-commit: 941e5d7574d31622f50e50e717c21cd2eba2e602
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 54%

---

# Journalisation{#logging}

AEM vous offre la possibilité de configurer :

* paramètres globaux pour le service de journalisation central
* journalisation des données de requête ; configuration de journalisation spécialisée pour les informations de requête
* les paramètres spécifiques des services individuels ; par exemple, un fichier journal individuel et le format des messages du journal.

Il s’agit toutes de [configurations OSGi](/help/sites-deploying/configuring-osgi.md).

>[!NOTE]
>
>La journalisation dans AEM est basée sur les principes de Sling. Pour plus d’informations, consultez [Journalisation Sling](https://sling.apache.org/site/logging.html).

## Journalisation globale {#global-logging}

[Configuration de la journalisation Apache Sling](/help/sites-deploying/osgi-configuration-settings.md) est utilisé pour configurer l’enregistreur racine. Cela définit les paramètres globaux pour la connexion à AEM :

* niveau de journalisation
* l’emplacement du fichier journal central ;
* le nombre de versions à conserver
* la rotation de version (soit une taille maximale, soit un intervalle de temps)
* le format à utiliser lors de l’écriture des messages du journal

>[!NOTE]
>
>Cet [article de la base de connaissances](https://helpx.adobe.com/fr/experience-manager/kb/HowToRotateRequestAndAccessLog.html) explique comment appliquer une rotation aux fichiers request.log et access.log.

## Enregistreurs et rédacteurs pour les services individuels {#loggers-and-writers-for-individual-services}

Outre les paramètres de journalisation globaux, AEM permet de configurer des paramètres spécifiques pour un service individuel :

* le niveau de journalisation spécifique
* emplacement du fichier journal individuel
* le nombre de versions à conserver
* la rotation de version (soit une taille maximale, soit un intervalle de temps) 
* le format à utiliser lors de l’écriture des messages du journal
* l’enregistreur (le service OSGi fournissant les messages de journal)

Vous pouvez ainsi canaliser les messages de journal pour un seul service dans un fichier distinct. Cela peut être particulièrement utile pendant le développement ou les tests, par exemple, si vous avez besoin d’un niveau de journalisation accru pour un service spécifique.

AEM utilise les éléments suivants pour écrire des messages de journal dans le fichier :

1. Un **Service OSGi** (journal) écrit un message de journal.
1. A **Journalisation** prend ce message et le formate selon vos spécifications.
1. A **Enregistreur de journalisation** écrit tous ces messages dans le fichier physique que vous avez défini.

Ces éléments sont liés par les paramètres suivants pour les éléments appropriés :

* **Enregistreur (enregistreur de journalisation)**

  Définissez le ou les services qui génèrent les messages.

* **Fichier journal (enregistreur de journalisation)**

  Définissez le fichier physique pour stocker les messages du journal.

  Ceci est utilisé pour lier un enregistreur de journalisation à un rédacteur de journalisation. La valeur doit être identique au même paramètre de la configuration du rédacteur de journalisation pour que la connexion s’effectue.

* **Fichier journal (rédacteur de journalisation)**

  Définissez le fichier physique dans lequel les messages du journal seront écrits.

  La valeur doit être identique au même paramètre de la configuration du rédacteur de journalisation, sinon la correspondance ne s’effectue pas. S’il n’existe aucune correspondance, un rédacteur implicite est créé avec la configuration par défaut (rotation quotidienne du journal).

### Enregistreurs et rédacteurs standard {#standard-loggers-and-writers}

Certains enregistreurs et rédacteurs sont inclus dans une installation d’AEM standard.

Le premier est un cas particulier car il contrôle à la fois les fichiers `request.log` et `access.log` :

* L’enregistreur :

   * Enregistreur de données de demandes personnalisables Apache Sling

     (org.apache.sling.engine.impl.log.RequestLoggerService)

   * Écrit les messages relatifs au contenu des demandes dans `request.log`.

* Est lié à :

   * Enregistreur de demandes Apache Sling

     (org.apache.sling.engine.impl.log.RequestLogger)

   * Écrit les messages dans `request.log` ou `access.log`.

Ils peuvent être personnalisés si nécessaire, bien que la configuration standard soit adaptée à la plupart des installations.

Les autres paires suivent la configuration standard :

* L’enregistreur :

   * Apache Sling Logging Logger Configuration

     (org.apache.sling.commons.log.LogManager.factory.config)

   * Écrit des messages `Information` sur `logs/error.log`.

* Est lié au rédacteur :

   * Apache Sling Logging Writer Configuration

     (org.apache.sling.commons.log.LogManager.factory.writer)

* L’enregistreur :

   * Apache Sling Logging Logger Configuration (org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * Écrit des messages `Warning` sur `../logs/error.log` pour le service `org.apache.pdfbox`.

* N’est pas lié à un rédacteur spécifique, et crée et utilise donc un rédacteur implicite avec une configuration par défaut (rotation quotidienne du journal).

### Création de vos propres enregistreurs et rédacteurs {#creating-your-own-loggers-and-writers}

Vous pouvez définir votre propre paire enregistreur/rédacteur :

1. Création d’une instance de la configuration d’usine [Configuration de l’enregistreur de journalisation Apache Sling](/help/sites-deploying/osgi-configuration-settings.md).

   1. Spécifiez le fichier journal.
   1. Définissez l’enregistreur.
   1. Configurez les autres paramètres selon les besoins.

1. Création d’une instance de la configuration d’usine [Configuration de l’auteur de journalisation Apache Sling](/help/sites-deploying/osgi-configuration-settings.md).

   1. Spécifiez le fichier journal. Celui-ci doit correspondre à celui spécifié pour l’enregistreur.
   1. Configurez les autres paramètres selon les besoins.

>[!NOTE]
>
>Dans certains cas, vous pouvez créer une [fichier journal personnalisé](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).
