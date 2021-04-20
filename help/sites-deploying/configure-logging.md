---
title: Journalisation
seo-title: Journalisation
description: Découvrez comment configurer des paramètres globaux pour le service de journalisation centrale, des paramètres spécifiques pour les services individuels ou apprenez à demander la journalisation des données.
seo-description: Découvrez comment configurer des paramètres globaux pour le service de journalisation centrale, des paramètres spécifiques pour les services individuels ou apprenez à demander la journalisation des données.
uuid: 8c9e3628-2f2c-445d-9706-5c7725b85fe2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5aa69b10-2cd0-4d34-8104-8c3b88405926
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 93%

---


# Journalisation{#logging}

AEM vous offre la possibilité de configurer :

* les paramètres généraux du service de journalisation central ;
* la journalisation des données de requête (une configuration de journalisation spécialisée pour les informations de requête) :
* les paramètres spécifiques des services individuels; par exemple, un fichier journal individuel et un format pour les messages du journal

Il s’agit toutes de [configurations OSGi](/help/sites-deploying/configuring-osgi.md).

>[!NOTE]
>
>La journalisation dans AEM est basée sur les principes de Sling. Pour plus d’informations, voir [Journalisation Sling](https://sling.apache.org/site/logging.html).

## Journalisation globale {#global-logging}

La [configuration de la journalisation d’Apache Sling](/help/sites-deploying/osgi-configuration-settings.md) sert à configurer l’enregistreur racine. Cela définit les paramètres globaux pour la journalisation dans AEM :

* le niveau de journalisation
* l’emplacement du fichier journal central
* le nombre de versions à conserver
* la rotation de version (soit une taille maximale, soit un intervalle de temps)
* le format à utiliser lors de l’écriture des messages du journal

>[!NOTE]
>
>Cet [article de la base de connaissances ](https://helpx.adobe.com/experience-manager/kb/HowToRotateRequestAndAccessLog.html)explique comment appliquer une rotation aux fichiers request.log et access.log.

## Enregistreurs et rédacteurs pour les services individuels {#loggers-and-writers-for-individual-services}

En plus des paramètres de journalisation globale, AEM permet de configurer des paramètres spécifiques pour un service individuel :

* le niveau de journalisation spécifique
* l’emplacement du fichier journal individuel
* le nombre de versions à conserver
* la rotation de version (soit une taille maximale, soit un intervalle de temps) 
* le format à utiliser lors de l’écriture des messages du journal
* l’enregistreur (le service OSGi fournissant les messages de journal)

Cela vous permet de canaliser les messages de journal pour un seul service dans un fichier distinct. Cela peut être particulièrement utile pendant le développement ou les tests, par exemple, si vous avez besoin d’un niveau de journalisation accru pour un service spécifique.

AEM utilise ce qui suit pour écrire des messages de journal dans un fichier :

1. Un **service OSGi**(enregistreur) écrit un message de journal.
1. Un **enregistreur de journalisation** met en forme ce message selon vos spécifications.
1. Un **rédacteur de journalisation** rédige tous ces messages dans le fichier physique que vous avez défini.

Ces éléments sont liés par les paramètres suivants pour les éléments appropriés :

* **Enregistreur (enregistreur de journalisation)**

   Définissez le ou les services qui génèrent les messages.

* **Fichier journal (Journalisation)**

   Définissez le fichier physique pour stocker les messages du journal.

   Ceci est utilisé pour lier un enregistreur de journalisation à un rédacteur de journalisation. La valeur doit être identique au même paramètre de la configuration du rédacteur de journalisation pour que la connexion s’effectue.

* **Fichier journal (enregistreur de journalisation)**

   Définissez le fichier physique dans lequel les messages du journal seront écrits.

   La valeur doit être identique au même paramètre de la configuration du rédacteur de journalisation, sinon la correspondance ne s’effectue pas. En l’absence de correspondance, un rédacteur implicite est créé avec la configuration par défaut (rotation quotidienne du journal).

### Enregistreurs et rédacteurs standard {#standard-loggers-and-writers}

Certains enregistreurs et rédacteurs sont inclus dans l’installation AEM standard.

Le premier est un cas particulier car il contrôle à la fois les fichiers `request.log`et `access.log` :

* L’enregistreur :

   * Enregistreur de données de demandes personnalisables Apache Sling

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * Écrit les messages relatifs au contenu des demandes dans `request.log`.

* Est lié à :

   * Enregistreur de demandes Apache Sling

      (org.apache.sling.engine.impl.log.RequestLogger)

   * Écrit les messages dans `request.log` ou `access.log`.

Ceux-ci peuvent être personnalisés si nécessaire, bien que la configuration standard convienne à la plupart des installations.

Les autres paires suivent la configuration standard :

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

Vous pouvez définir votre propre paire Enregistrer/Rédacteur :

1. Créez une nouvelle instance de la configuration d’usine [Apache Sling Logging Logger Configuration](/help/sites-deploying/osgi-configuration-settings.md).

   1. Définissez le fichier journal.
   1. Définissez l’enregistreur.
   1. Configurez les autres paramètres en fonction de vos besoins.

1. Créez une nouvelle instance de la configuration d’usine [Apache Sling Logging Writer Configuration](/help/sites-deploying/osgi-configuration-settings.md).

   1. Spécifiez le fichier journal (il doit correspondre à celui spécifié pour l’enregistreur).
   1. Configurez les autres paramètres en fonction de vos besoins.

>[!NOTE]
>
>Dans certaines circonstances, vous pouvez créer un [fichier journal personnalisé](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).

