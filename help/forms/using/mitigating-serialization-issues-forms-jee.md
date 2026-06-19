---
title: Réduire les problèmes de sérialisation dans AEM Forms JEE | Adobe Experience Manager
description: Découvrez comment atténuer les problèmes de désérialisation Java dans AEM Forms JEE s’exécutant sur JDK 8.
solution: Experience Manager, Experience Manager Forms
feature: Security
version: Experience Manager 6.5
type: Documentation
role: Admin
source-git-commit: ec3941675081255879065c3be9d5af77474b2072
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 1%

---


# Réduire les problèmes de sérialisation dans AEM Forms JEE {#mitigating-serialization-issues-in-aem-forms-jee}

AEM Forms JEE comprend un pare-feu de désérialisation qui ajoute une vérification en amont avant toute tentative de désérialisation d’un objet. Ce contrôle teste un nom de classe par rapport à une liste autorisée de type pare-feu, une ou les deux, et rejette les classes connues pour être exploitables par le biais d’attaques de désérialisation Java™. L’agent sous-jacent est la distribution modifiée par Adobe du projet open source [NotSoSerial](https://github.com/kantega/notsoserial), sous licence [Apache 2](https://www.apache.org/licenses/LICENSE-2.0).

Sur les installations exécutant **JDK 11 ou version ultérieure**, cette protection est activée par le filtrage de sérialisation natif de la plateforme et ne nécessite aucune étape manuelle. Sur les installations exécutant **JDK 8**, le filtrage de sérialisation natif n’est pas efficace. L’agent doit donc être attaché explicitement à la JVM au démarrage. Cet article décrit comment procéder.

>[!NOTE]
>
>Si le contrôle de l’intégrité du filtre de désérialisation indique déjà comme actif sur votre serveur (voir [Vérification de l’activation de l’agent](#verifying-the-agents-activation)), votre serveur d’applications est déjà protégé et vous pouvez ignorer les étapes restantes dans ce document.

## Avant de commencer {#before-you-begin}

Vérifiez la version Java™ avec laquelle votre serveur d’applications s’exécute :

```shell
java -version
```

Si la version signalée est `1.8.x` (JDK 8), les étapes de cet article s’appliquent. S’il s’agit d’une version 11 ou ultérieure, aucune action manuelle n’est requise. Vérifiez la protection à l’aide du contrôle d’intégrité décrit dans la section [Vérification de l’activation de l’agent](#verifying-the-agents-activation).

Dans les étapes qui suivent, `<jee-installation-directory>` fait référence à la racine de votre installation AEM Forms JEE.

## Application de l’agent {#applying-the-agent}

>[!IMPORTANT]
>
>Ces étapes nécessitent un redémarrage du serveur d’applications. Appliquez-les à chaque instance affectée.

1. **Valider l’état actuel.** Accédez au contrôle de l’intégrité du filtre de désérialisation :

   ```text
   https://<server>:<port>/system/console/healthcheck?tags=deserialization
   ```

   Si la vérification indique comme active, l’instance est déjà protégée et aucune autre action n’est nécessaire. En cas d’échec, procédez comme suit.

1. **Vérifiez si le fichier JAR de l’agent est déjà présent.** Recherchez des `notsoserial.jar` à l’emplacement suivant :

   ```text
   <jee-installation-directory>/crx-quickstart/opt/notsoserial/
   ```

1. **Ajoutez le fichier JAR s’il est manquant.** Téléchargez le [`notsoserial.jar`](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/notsoserial.jar) et copiez-le dans le dossier ci-dessus sur chaque instance :

   ```text
   <jee-installation-directory>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >Remplacez cette étape par l’emplacement de téléchargement Adobe officiel pour la distribution Forms JEE de l’agent avant la publication.

1. **Mettez à jour les paramètres de démarrage de la JVM** de votre serveur d’applications pour joindre l’agent. Ajoutez l’option suivante à la ligne d’exécution Java™ :

   ```shell
   -javaagent:<jee-installation-directory>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   L’emplacement exact de la ligne d’exécution Java™ dépend de votre serveur d’applications (par exemple, JBoss, WebLogic ou WebSphere®). Ajoutez l’option aux options JVM utilisées pour démarrer le serveur d’applications AEM Forms JEE.

1. **Redémarrez le serveur JEE** de sorte que l’agent soit chargé au démarrage de la JVM.

1. **Revalider.** Accédez à nouveau au contrôle de l’intégrité :

   ```text
   https://<server>:<port>/system/console/healthcheck?tags=deserialization
   ```

   Le contrôle de l’intégrité doit maintenant être déclaré comme sain.

## Vérification de l’activation de l’agent {#verifying-the-agents-activation}

Vous pouvez vérifier à tout moment la configuration de l’agent de désérialisation en accédant à l’URL suivante :

```text
https://<server>:<port>/system/console/healthcheck?tags=deserialization
```

Une liste des contrôles de l’intégrité associés à l’agent s’affiche. Si les vérifications réussissent, l’agent est correctement activé. S’ils échouent sur une instance JDK 8, l’agent n’a pas été chargé et vous devez le joindre manuellement en suivant les étapes décrites à la section [Application de l’agent](#applying-the-agent).

## Configurer l’agent {#configuring-the-agent}

Les étapes ci-dessous s’appliquent si la version Java™ de votre serveur d’applications est exécutée avec JDK 8. Vous pouvez configurer l’agent après l’avoir joint et chargé en suivant les étapes décrites dans la section [Appliquer l’agent](#applying-the-agent).

La configuration par défaut convient à la plupart des installations. Il comprend une liste bloquée de classes connues exploitables à distance et une batterie de packages où la désérialisation de données approuvées est sécurisée. La place sur la liste bloquée est appliquée avant toute entrée placée sur la liste autorisée.

La configuration du pare-feu est dynamique et peut être modifiée à tout moment :

1. Accédez à la console web à l’adresse `https://<server>:<port>/system/console/configMgr`.

1. Recherchez et cliquez sur **Configuration du pare-feu de désérialisation**.

Cette configuration contient les options de journalisation de la liste autorisée, de la place sur la liste bloquée et des diagnostics :

* **Liste autorisée** - classes ou préfixes de package autorisés pour la désérialisation. Si vous désérialisez vos propres classes, ajoutez les classes ou les packages appropriés ici.
* **Liste bloquée** - classes qui ne sont jamais autorisées pour la désérialisation. L’ensemble initial est limité à des classes considérées comme vulnérables aux attaques d’exécution à distance.
* **Journalisation des diagnostics** - options de journalisation lorsque la désérialisation a lieu. La valeur par défaut **class-name-only** indique les classes désérialisées. L’option **full-stack** consigne une pile Java™ pour la première tentative de désérialisation, ce qui s’avère utile pour localiser et supprimer les désérialisations non approuvées dans votre utilisation. Ces options sont consignées uniquement lors de la première utilisation.

## Autres considérations {#other-considerations}

* L’agent est destiné à atténuer les classes vulnérables actuellement connues. Si votre projet désérialise des données non approuvées, il peut toujours être exposé à des attaques de déni de service, de mémoire insuffisante ou à des attaques de désérialisation futures inconnues.
* Si vous exécutez sur un environnement d’exécution JRE (Java™ Runtime Environment) plutôt que sur un JDK (Java™ Development Kit), les outils requis pour le chargement dynamique de l’agent ne sont pas disponibles et l’agent doit être joint manuellement au démarrage, comme décrit dans la section [Application de l’agent](#applying-the-agent).
* Si vous exécutez sur une JVM ®, consultez la documentation sur la prise en charge de l’API Attach Java™.
