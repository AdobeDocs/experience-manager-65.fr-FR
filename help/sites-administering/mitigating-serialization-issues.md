---
title: Réduire les problèmes de sérialisation dans AEM
seo-title: Mitigating serialization issues in AEM
description: Découvrez comment atténuer les problèmes de sérialisation dans AEM.
seo-description: Learn how to mitigate serialization issues in AEM.
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
exl-id: 01e9ab67-15e2-4bc4-9b8f-0c84bcd56862
source-git-commit: 614c4c88f3f09feb5a400ade9f45f634ac4fbcd5
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 25%

---

# Réduire les problèmes de sérialisation dans AEM{#mitigating-serialization-issues-in-aem}

## Présentation {#overview}

L&#39;équipe AEM d&#39;Adobe a travaillé en étroite collaboration avec le projet open source. [NotSoSerial](https://github.com/kantega/notsoserial) pour vous aider à atténuer les vulnérabilités décrites dans la section **CVE-2015-7501**. NotSoSerial est accordé sous [licence Apache 2](https://www.apache.org/licenses/LICENSE-2.0) et comprend du code ASM accordé sous sa propre [licence de type BSD](https://asm.ow2.io/).

Le fichier JAR d’agent inclus dans ce package est la distribution de NotSoSerial modifiée par Adobe.

NotSoSerial est une solution de niveau Java™ à un problème de niveau Java™ et n’est pas spécifique à AEM. Il ajoute un contrôle en amont à une tentative de désérialisation d’un objet. Ce contrôle teste un nom de classe par rapport à une liste autorisée de type pare-feu, ou à une liste bloquée, ou les deux. En raison du nombre limité de classes dans la liste bloquée par défaut, ce test ne risque pas d’avoir un impact sur vos systèmes ou votre code.

Par défaut, l’agent effectue une vérification de liste bloquée par rapport aux classes vulnérables connues actuelles. Cette liste bloquée est destinée à vous protéger de la liste actuelle des exploits qui utilisent ce type de vulnérabilité.

La liste bloquée et la liste autorisée peuvent être configurées en suivant les instructions de la section [Configuration de l’agent](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) de cet article.

L’agent est conçu pour vous aider à limiter les dernières classes vulnérables connues. Si votre projet désérialise des données non approuvées, il peut toujours être vulnérable aux attaques par déni de service, aux attaques par saturation de mémoire et aux futures attaques inconnues de désérialisation.

Adobe prend officiellement en charge Java™ 6, 7 et 8. Cependant, l’Adobe a compris que NotSoSerial prend également en charge Java™ 5.

## Installation de l’agent {#installing-the-agent}

>[!NOTE]
>
>Si vous avez précédemment installé le correctif de sérialisation pour AEM 6.1, supprimez les commandes de démarrage de l’agent de votre ligne d’exécution Java™.

1. Installez le lot **com.adobe.cq.cq-serialization-tester**.

1. Accédez à la console Lots web à l’adresse `https://server:port/system/console/bundles`.
1. Recherchez le lot de sérialisation et démarrez-le. Cela charge automatiquement de manière dynamique l’agent NotSoSerial.

## Installation de l’agent sur les serveurs d’applications {#installing-the-agent-on-application-servers}

L’agent NotSoSerial n’est pas inclus dans la distribution standard d’AEM pour les serveurs d’applications. Cependant, vous pouvez l’extraire de la distribution jar d’AEM et l’utiliser avec la configuration de votre serveur d’applications :

1. Tout d’abord, téléchargez AEM fichier quickstart et extrayez-le :

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. Accédez à l’emplacement du QuickStart AEM que vous venez de décompresser et copiez le dossier `crx-quickstart/opt/notsoserial/` dans le dossier `crx-quickstart` de l’installation du serveur d’applications AEM.

1. Modifiez le propriétaire de `/opt` sur l’utilisateur exécutant le serveur :

   ```shell
   chown -R opt <user running the server>
   ```

1. Configurez et vérifiez que l’agent a été correctement activé, comme indiqué dans les sections suivantes de cet article.

## Configuration de l’agent {#configuring-the-agent}

La configuration par défaut est appropriée pour la plupart des installations. Cette configuration inclut une liste bloquée de classes vulnérables connues d’exécution distante et une liste autorisée de packages où la désérialisation de données approuvées est sécurisée.

La configuration de pare-feu est dynamique et peut être changée à tout moment en :

1. accédant à la console web à l’adresse `https://server:port/system/console/configMgr` ;
1. Recherche et clic **Configuration du pare-feu de désérialisation.**

   >[!NOTE]
   Vous pouvez également accéder directement à la page de configuration en accédant à l’URL :
   * `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


Cette configuration contient la liste autorisée, la liste bloquée et la journalisation de désérialisation.

**Liste autorisée**

Dans la section des listes autorisées, ces listes sont des classes ou des préfixes de package autorisés pour la désérialisation. Si vous désérialisez des classes, ajoutez les classes ou les packages à cette liste autorisée.

**Liste bloquée**

Dans la section de liste bloquée se trouvent des classes qui ne sont jamais autorisées pour la désérialisation. L’ensemble initial de ces classes est limité à celles qui sont considérées comme vulnérables aux attaques d’exécution à distance. La liste bloquée est appliquée avant toute entrée de liste autorisée.

**Journalisation des diagnostics**

Dans la section relative à la journalisation des diagnostics, vous pouvez choisir plusieurs options de journalisation lorsque la désérialisation a lieu. Ces options sont uniquement consignées lors de la première utilisation et ne sont pas reenregistrées lors d’utilisations ultérieures.

La valeur par défaut de **class-name-only** vous informe des classes qui sont désérialisées.

Vous pouvez également définir la variable **full-stack** qui consigne une pile Java™ de la première tentative de désérialisation afin de vous informer de l’endroit où votre désérialisation a lieu. Cette option est utile pour rechercher et supprimer la désérialisation de votre utilisation.

## Vérification de l’activation de l’agent {#verifying-the-agent-s-activation}

Vous pouvez vérifier la configuration de l’agent de désérialisation en accédant à l’URL à l’adresse :

* `https://server:port/system/console/healthcheck?tags=deserialization`

Une fois que vous avez accédé à l’URL, une liste de contrôles de l’intégrité associés à l’agent s’affiche. Vous pouvez déterminer si l’agent est correctement activé en vérifiant la réussite des contrôles de l’intégrité. S’ils échouent, vous devez charger l’agent manuellement.

Pour plus d’informations sur la résolution des problèmes avec l’agent, voir [Gestion Des Erreurs Avec Le Chargement Dynamique De L’Agent](#handling-errors-with-dynamic-agent-loading) ci-dessous.

>[!NOTE]
Si vous ajoutez `org.apache.commons.collections.functors` à la liste autorisée, le contrôle de l’intégrité échoue toujours.

## Gestion des erreurs avec le chargement de l’agent dynamique {#handling-errors-with-dynamic-agent-loading}

Si des erreurs sont exposées dans le journal ou si les étapes de vérification détectent un problème lors du chargement de l’agent, chargez l’agent manuellement. Ce workflow est également recommandé si vous utilisez un environnement d’exécution JRE (Java™ Runtime Environment) au lieu d’un JDK (Java™ Development Toolkit), car les outils de chargement dynamique ne sont pas disponibles.

Pour charger l’agent manuellement, procédez comme suit :

1. Modifiez les paramètres de démarrage de la JVM du jar CQ, en ajoutant l’option suivante :

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   Requiert que vous utilisiez également l’option -nofork CQ/AEM, ainsi que les paramètres de mémoire JVM appropriés, car l’agent n’est pas activé sur une JVM dupliquée.

   >[!NOTE]
   La distribution Adobe du fichier JAR de l’agent NotSoSerial réside dans le dossier `crx-quickstart/opt/notsoserial/` pour votre installation AEM.

1. Arrêtez et redémarrez la JVM.

1. Vérifiez à nouveau l’activation de l’agent en suivant les étapes décrites ci-dessus dans la section [Vérification de l’activation de l’agent](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation).

## Autres considérations {#other-considerations}

Si vous exécutez une JVM IBM®, consultez la documentation sur la prise en charge de l’API Joindre Java™ à l’adresse [cet emplacement](https://www.ibm.com/docs/en/sdk-java-technology/8?topic=documentation-java-attach-api).
