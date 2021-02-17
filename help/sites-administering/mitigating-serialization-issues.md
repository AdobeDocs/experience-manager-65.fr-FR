---
title: Réduction des problèmes de sérialisation dans AEM
seo-title: Réduction des problèmes de sérialisation dans AEM
description: Apprenez à réduire les problèmes de sérialisation dans AEM.
seo-description: Apprenez à réduire les problèmes de sérialisation dans AEM.
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
translation-type: tm+mt
source-git-commit: 3cbbad3ce9d93a353f48fc3206df989a8bf1991a
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 66%

---


# Réduction des problèmes de sérialisation dans AEM{#mitigating-serialization-issues-in-aem}

## Présentation {#overview}

 L’équipe d’AEM chez Adobe travaille en étroite collaboration avec le projet [NotSoSerial](https://github.com/kantega/notsoserial) open source pour limiter les vulnérabilités décrites dans **CVE-2015-7501**. NotSoSerial est accordé sous [licence Apache 2](https://www.apache.org/licenses/LICENSE-2.0) et comprend du code ASM accordé sous sa propre [licence de type BSD](https://asm.ow2.org/license.html).

Le fichier JAR d’agent inclus dans ce module est la distribution de NotSoSerial modifiée par Adobe.

  NotSoSerial est une solution de niveau Java à un problème de niveau Java, et il n’est pas spécifique à AEM. Il ajoute un contrôle en amont à une tentative de désérialisation d’un objet. Cette vérification testera un nom de classe par rapport à une liste autorisée et/ou une liste bloquée de type pare-feu. En raison du nombre limité de classes dans la liste bloquée par défaut, il est peu probable que cela ait un impact sur vos systèmes ou votre code.

Par défaut, l&#39;agent effectue une vérification de liste bloquée des classes vulnérables connues actuelles. Cette liste bloquée est destinée à vous protéger de la liste actuelle d&#39;exploits qui utilisent ce type de vulnérabilité.

La liste bloquée et la liste autorisée peuvent être configurées en suivant les instructions de la section [Configuration de l&#39;agent](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) de cet article.

L’agent est conçu pour vous aider à limiter les dernières classes vulnérables connues. Si votre projet désérialise des données non approuvées, il peut être vulnérable aux attaques par déni de service, aux attaques de mémoire insuffisante et aux futures attaques inconnues de désérialisation.

Adobe prend officiellement en charge Java 6, 7 et 8, toutefois, il semble que NotSoSerial prend également en charge Java 5.

## Installation de l’agent {#installing-the-agent}

>[!NOTE]
>
>Si vous avez déjà installé le correctif de sérialisation pour AEM 6.1, supprimez les commandes de démarrage de l’agent de la ligne d’exécution Java.

1. Installez le lot **com.adobe.cq.cq-serialization-tester**.

1. Accédez à la console Web du lot à l&#39;adresse `https://server:port/system/console/bundles`
1. Recherchez le lot de sérialisation et démarrez-le. Cela devrait charger automatiquement et dynamiquement l’agent NotSoSerial.

## Installation de l’agent sur les serveurs d’applications {#installing-the-agent-on-application-servers}

L’agent NotSoSerial n’est pas inclus dans la distribution standard des AEM pour les serveurs d’applications. Cependant, vous pouvez l’extraire du fichier de distribution JAR d’AEM et l’utiliser avec la configuration de votre serveur d’applications :

1. Tout d’abord, téléchargez le fichier QuickStart AEM et extrayez-le :

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. Accédez à l’emplacement de l’AEM décompressé de démarrage rapide et copiez le dossier `crx-quickstart/opt/notsoserial/` dans le dossier `crx-quickstart` de l’installation AEM du serveur d’applications.

1. Remplacez la propriété de `/opt` par l’utilisateur exécutant le serveur :

   ```shell
   chown -R opt <user running the server>
   ```

1. Configurez l’agent et vérifiez qu’il a été correctement activé, comme indiqué dans les sections suivantes de cet article.

## Configuration de l’agent  {#configuring-the-agent}

La configuration par défaut est appropriée pour la plupart des installations. Cela inclut une liste bloquée de classes vulnérables connues d&#39;exécution à distance et une liste autorisée de paquets où la désérialisation de données fiables devrait être relativement sûre.

   La configuration de pare-feu est dynamique et peut être changée à tout moment en :

1. Accéder à la console Web à `https://server:port/system/console/configMgr`
1. recherchant **Configuration du pare-feu de désérialisation** et en cliquant dessus.

   >[!NOTE]
   >
   >Vous pouvez également atteindre la page de configuration directement en accédant à l’URL :
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


Cette configuration contient la journalisation de la liste autorisée, de la liste bloquée et de la désérialisation.

**Autoriser la liste**

Dans la section permettant la mise en vente, il s’agit de classes ou de préfixes de package qui seront autorisés pour la désérialisation. Il est important de savoir que si vous désérialisez les classes vous-même, vous devrez ajouter les classes ou les paquets à cette liste autorisée.

**Liste des blocs**

Dans la section de liste des blocs, il y a des classes qui ne sont jamais autorisées pour la désérialisation. L’ensemble initial de ces classes est limité à celles qui sont considérées comme vulnérables aux attaques d’exécution à distance. La liste bloquée est appliquée avant toute entrée répertoriée autorisée.

**Journalisation du diagnostic**

Dans la section relative à la journalisation des diagnostics, vous pouvez choisir plusieurs options de connexion lors de la désérialisation. Les désérialisations sont uniquement consignées lors de la première utilisation, elles ne le sont pas pour les utilisations suivantes.

La valeur par défaut **class-name-only** vous notifie les classes qui sont désérialisées.

Vous pouvez également définir l’option **full-stack** qui consigne une pile Java de la première tentative de désérialisation afin de vous informer lorsque votre désérialisation a lieu. Cela peut être utile pour rechercher et supprimer la désérialisation de votre utilisation.

## Vérification de l’activation de l’agent {#verifying-the-agent-s-activation}

Vous pouvez vérifier la configuration de l’agent de désérialisation en accédant à l’URL :

* `https://server:port/system/console/healthcheck?tags=deserialization`

Lorsque vous accédez à l’URL, la liste des contrôles de l’intégrité associés à l’agent s’affiche. Vous pouvez déterminer si l’agent est correctement activé en vérifiant la réussite des contrôles de l’intégrité. S’ils échouent, vous pouvez être amené à charger l’agent manuellement.

Pour plus d’informations sur la résolution des incidents avec l’agent, voir [Gestion des erreurs lors du chargement dynamique de l’agent](#handling-errors-with-dynamic-agent-loading) ci-dessous.

>[!NOTE]
>
>Si vous ajoutez `org.apache.commons.collections.functors` à la liste autorisée, la vérification d&#39;intégrité échoue toujours.

## Gestion des erreurs lors du chargement dynamique de l’agent {#handling-errors-with-dynamic-agent-loading}

Si des erreurs sont exposées dans le journal, ou si les étapes de vérification détectent un problème lors du chargement de l’agent, vous devrez peut-être charger l’agent manuellement. Cela est également recommandé au cas où vous utilisez un JRE (Java Runtime Environment) plutôt qu’un JDK (Java Development Toolkit), dans la mesure où les outils pour le chargement dynamique ne sont pas disponibles.

Pour charger l’agent manuellement, suivez les instructions ci-dessous :

1. Modifiez les paramètres de démarrage de la JVM du fichier JAR de CQ, en ajoutant l’option suivante :

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >Pour cela, utilisez également l’option -nofork de CQ/d’AEM, avec les paramètres appropriés de mémoire JVM, car l’agent ne sera pas activé sur une JVM divisée.

   >[!NOTE]
   >
   >La distribution par Adobe du fichier jar de l&#39;agent NotSoSerial se trouve dans le dossier `crx-quickstart/opt/notsoserial/` de votre installation AEM.

1. Arrêtez et redémarrez la JVM.

1. Vérifiez à nouveau l’activation de l’agent en suivant les étapes décrites ci-dessus dans [Vérification de l’activation de l’agent](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation).

## Autres considérations  {#other-considerations}

Si vous exécutez sur une JVM IBM, voir la documentation sur la prise en charge de l’API Attach Java à cet [emplacement](https://www.ibm.com/support/knowledgecenter/SSSTCZ_2.0.0/com.ibm.rt.doc.20/user/attachapi.html).
