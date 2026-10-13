---
title: Étapes supplémentaires pour obtenir un e-mail avec des pièces jointes
description: Découvrez comment corriger l’erreur lorsque vous ne parvenez pas à récupérer des e-mails avec des pièces jointes pour les plateformes AEM Forms sur JEE.
exl-id: 0d0713fb-d95a-4a95-91ef-9cdaea30e343
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 100%
---
# Impossible d’obtenir un e-mail avec des pièces jointes pour les plateformes AEM Forms sur JEE{#unable-to-get-email-with-attachments}

Le problème s’applique à la version suivante :

* Formulaires avec Experience Manager 6.5

## Problème {#issue}

L’utilisateur ou l’utilisatrice ne peut pas effectuer d’opérations telles qu’Envoyer un PDF par e-mail ou Inclure des pièces jointes avec la configuration Envoi.

## Solution {#solution}

1. Téléchargez le fichier JAR en tant que [java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar) et décompressez le fichier JAR téléchargé pour obtenir le fichier manifeste.

1. Utilisez le fichier manifeste de `java.mail-1.0.jar` récupéré à l’étape 1 pour créer un fichier JAR personnalisé, comme `java.mail-1.5.jar`.

1. Ouvrez le fichier manifeste et remplacez toutes les occurrences de `1.5.0` par `1.5.6` et `Bundle-Version: 1.0` par `Bundle-Version:1.5`.

1. Créez un fichier JAR personnalisé (`java.mail-1.5.jar`) à l’aide de la commande suivante dans le dossier `C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin` comme suit :
   `jar -cfm java.mail-1.5.jar manifest.mf`

   Dans la commande ci-dessus, *manifest.mf* est le nom du fichier manifeste et *java.mail-1.5.jar* est le nom du fichier qui sera créé après l’exécution de la commande ci-dessus.

1. Téléchargez [javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1).

1. Accédez à `http://<server name>:<port>/lc/system/console/bundles` et supprimez le bundle portant le nom `JavaMail API (com.sun.mail.javax.mail) version 1.6.2`.

1. Installez `java.mail-1.5.jar` obtenu à l’étape 3. Cette étape redémarre les propriétés sling du déploiement JEE. Attendez que les bundles installés sur `http://<server name>:<port>/lc/system/console/bundles` affichent le statut **Actif**.

   >Si le statut est toujours **inactif**, redémarrez **JBoss®** à partir de la **console de services**.


1. Installez le fichier `javax.mail-1.5.6.redhat-1.jar` téléchargé à l’étape 5.

1. Arrêtez **JBoss®** à partir de la **console de services** et ajoutez les propriétés suivantes au fichier **Sling.properties** :
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. Redémarrez **JBoss®**.

>[!NOTE]
>
> Il est recommandé d’utiliser la commande « Ctrl+C » pour redémarrer le SDK. Le redémarrage du SDK AEM à l’aide de méthodes alternatives, par exemple l’arrêt des processus Java, peut entraîner des incohérences dans l’environnement de développement AEM.
