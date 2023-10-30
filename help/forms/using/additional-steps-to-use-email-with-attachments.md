---
title: Étapes supplémentaires pour obtenir un e-mail avec une pièce jointe
description: Corrigez l’erreur lorsque vous ne parvenez pas à récupérer les courriers électroniques contenant des pièces jointes pour les plateformes AEM Forms on JEE.
exl-id: 0d0713fb-d95a-4a95-91ef-9cdaea30e343
source-git-commit: 20b0d0db54dc30285c056a10032f02ba45f8baca
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 68%

---

# Impossible d’obtenir un e-mail avec des pièces jointes pour les plateformes AEM Forms sur JEE{#unable-to-get-email-with-attachments}

Le problème s’applique à la version suivante :
* Formulaires avec Experience Manager 6.5

## Problème {#issue}

L’utilisateur ou l’utilisatrice ne peut pas effectuer d’opérations telles qu’Envoyer un PDF par e-mail ou Inclure des pièces jointes avec la configuration Envoi.

## Solution {#solution}

1. Téléchargez le fichier JAR en tant que [java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar) et décompressez le fichier JAR téléchargé pour obtenir le fichier manifeste.

1. Utiliser le fichier manifeste de `java.mail-1.0.jar` récupéré à l’étape 1 pour créer un fichier JAR personnalisé, comme indiqué par `java.mail-1.5.jar`.

1. Ouvrez le fichier manifeste et remplacez toutes les occurrences de `1.5.0` par `1.5.6` et `Bundle-Version: 1.0` par `Bundle-Version:1.5`.

1. Création d’un fichier jar personnalisé (`java.mail-1.5.jar`) à l’aide de la commande suivante dans `C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin` comme suit :
   `jar -cfm java.mail-1.5.jar manifest.mf`

   Dans la commande ci-dessus, *manifest.mf* est le nom du fichier manifeste et *java.mail-1.5.jar* est le nom du fichier qui sera créé après l’exécution de la commande ci-dessus.

1. Téléchargez [javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1).

1. Accédez à `http://<server name>:<port>/lc/system/console/bundles` et supprimez le lot portant le nom `JavaMail API (com.sun.mail.javax.mail) version 1.6.2`.

1. Installez `java.mail-1.5.jar` obtenu à l’étape 3. Cette étape redémarre les propriétés sling du déploiement JEE. Attendez que les lots installés sur `http://<server name>:<port>/lc/system/console/bundles` affichent le statut **Actif**.

   >Remarque : Si l’état est toujours **InActive**, redémarrez   **JBoss ®** de la **Console des services**.


1. Installez le fichier `javax.mail-1.5.6.redhat-1.jar` téléchargé à l’étape 5.

1. Arrêter **JBoss ®** de la **Console des services** et ajoutez les propriétés suivantes à **Sling.properties** fichier :
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. Redémarrez **JBoss®**.
