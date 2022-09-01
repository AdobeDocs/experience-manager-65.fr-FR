---
title: 'Étapes supplémentaires pour obtenir un courrier électronique avec une pièce jointe '
description: 'Étapes supplémentaires pour obtenir un courrier électronique avec une pièce jointe   '
source-git-commit: 9ee8e79777b89fbf4d6e5b5fd1dbb1ef3bc9ad5d
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Impossible d’obtenir un courrier électronique avec des pièces jointes pour les plateformes AEM Forms on JEE{#unable-to-get-email-with-attachments}

Le problème s’applique à la version suivante :
* Experience Manager 6.5 Forms

## Problème {#issue}

L’utilisateur ne peut pas effectuer d’opérations telles que Envoyer un PDF par courrier électronique ou Inclure des pièces jointes avec la configuration Envoi.

## Solution {#solution}

1. Télécharger jar en tant que [java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar) et décompressez le fichier jar téléchargé pour obtenir le fichier manifest.

1. Utiliser le fichier manifeste de `java.mail-1.0.jar` récupéré à l’étape 1 pour créer un fichier JAR personnalisé, comme `java.mail-1.5.jar`.

1. Ouvrez le fichier de manifeste et remplacez toutes les occurrences de `1.5.0` avec `1.5.6` et `Bundle-Version: 1.0` avec `Bundle-Version:1.5`

1. Créez un nouveau fichier jar personnalisé (`java.mail-1.5.jar`) à l’aide de la commande suivante dans `C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin` comme suit :
   `jar -cfm java.mail-1.5.jar manifest.mf`

   Dans la commande ci-dessus, *manifest.mf* est le nom du fichier manifeste et *java.mail-1.5.jar* est le nom du fichier qui sera créé après l’exécution de la commande ci-dessus.

1. Télécharger [javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1).

1. Accédez à `http://<server name>:<port>/lc/system/console/bundles`et supprimez le lot portant le nom `JavaMail API (com.sun.mail.javax.mail) version 1.6.2`.

1. Installer `java.mail-1.5.jar` obtenu à l’étape 3.  Cette étape redémarre les propriétés sling du déploiement JEE. Attendez les lots installés à l’adresse `http://<server name>:<port>/lc/system/console/bundles` Pour afficher le statut comme **Principal**.

   >Remarque : Si l’état est toujours **InActive**, redémarrez   **JBoss** de la **Console des services**.


1. Installer `javax.mail-1.5.6.redhat-1.jar`téléchargé à l’aide de l’étape 5.

1. Arrêter **JBoss** de la **Console des services** et ajoutez les propriétés suivantes à **Sling.properties** fichier :
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. Redémarrer **JBoss**.