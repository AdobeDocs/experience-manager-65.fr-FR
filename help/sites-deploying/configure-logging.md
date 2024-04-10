---
title: Journalisation
description: Découvrez comment configurer des paramètres globaux pour le service de journalisation centrale, des paramètres spécifiques pour les services individuels ou comment demander la journalisation des données.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: b32001a1-0078-43f6-89d6-781d6d2e9c94
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 100%

---

# Journalisation{#logging}

AEM vous offre la possibilité de configurer :

* les paramètres globaux pour le service de journalisation centrale
* la journalisation des données de requête ; une configuration de journalisation spécialisée pour les informations de requête
* des paramètres spécifiques pour les services individuels ; par exemple, un fichier journal individuel et le format des messages du journal.

Il s’agit toutes de [configurations OSGi](/help/sites-deploying/configuring-osgi.md).

>[!NOTE]
>
>La journalisation dans AEM est basée sur les principes de Sling. Pour plus d’informations, consultez [Journalisation Sling](https://sling.apache.org/site/logging.html).

## Journalisation globale {#global-logging}

La [configuration de la journalisation Apache Sling](/help/sites-deploying/osgi-configuration-settings.md) est utilisée pour configurer l’enregistreur racine. Cela définit les paramètres globaux pour la journalisation dans AEM :

* le niveau de journalisation spécifique
* l’emplacement du fichier journal central
* le nombre de versions à conserver
* la rotation de version (soit une taille maximale, soit un intervalle de temps)
* le format à utiliser lors de l’écriture des messages du journal

>[!NOTE]
>
>Cet [article de la base de connaissances](https://helpx.adobe.com/fr/experience-manager/kb/HowToRotateRequestAndAccessLog.html) explique comment appliquer une rotation aux fichiers request.log et access.log.

## Enregistreurs et rédacteurs pour les services individuels {#loggers-and-writers-for-individual-services}

En plus des paramètres de journalisation globale, AEM vous permet de configurer des paramètres spécifiques pour un service individuel :

* le niveau de journalisation spécifique
* l’emplacement du fichier journal individuel
* le nombre de versions à conserver
* la rotation de version (soit une taille maximale, soit un intervalle de temps) 
* le format à utiliser lors de l’écriture des messages du journal
* l’enregistreur (le service OSGi fournissant les messages de journal)

Cela vous permet de canaliser les messages de journal pour un seul service dans un fichier distinct. Cela peut être particulièrement utile pendant le développement ou les tests, par exemple, si vous avez besoin d’un niveau de journalisation accru pour un service spécifique.

AEM utilise les éléments suivants pour écrire des messages de journal dans un fichier :

1. Un **service OSGi** (enregistreur) écrit un message de journal.
1. Un **enregistreur de journalisation** prend ce message et le formate selon vos spécifications.
1. Un **rédacteur de journalisation** écrit tous ces messages dans le fichier physique que vous avez défini.

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

Certains enregistreurs et rédacteurs sont inclus dans une installation standard d’AEM.

Le premier est un cas particulier car il contrôle à la fois les fichiers `request.log` et `access.log` :

* L’enregistreur :

   * Enregistreur de données de demandes personnalisables Apache Sling

     (org.apache.sling.engine.impl.log.RequestLoggerService)

   * Écrit les messages relatifs au contenu des demandes dans `request.log`.

* Est lié à :

   * Enregistreur de demandes Apache Sling

     (org.apache.sling.engine.impl.log.RequestLogger)

   * Écrit les messages dans `request.log` ou `access.log`.

Ceux-ci peuvent être personnalisés si nécessaire, bien que la configuration standard convienne à la plupart des installations.

Les autres paires adoptent la configuration standard :

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

Vous pouvez définir votre propre paire enregistreur/rédacteur :

1. Créez une instance de la configuration d’usine [Configuration de l’enregistreur de journalisation Apache Sling](/help/sites-deploying/osgi-configuration-settings.md).

   1. Spécifiez le fichier journal.
   1. Définissez l’enregistreur.
   1. Configurez les autres paramètres en fonction de vos besoins.

1. Créez une instance de la configuration d’usine [Configuration du rédacteur de journalisation Apache Sling](/help/sites-deploying/osgi-configuration-settings.md).

   1. Spécifiez le fichier journal. Celui-ci doit correspondre à celui spécifié pour l’enregistreur.
   1. Configurez les autres paramètres en fonction de vos besoins.

>[!NOTE]
>
>Dans certains cas, vous voudrez peut-être créer un [fichier journal personnalisé](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).
