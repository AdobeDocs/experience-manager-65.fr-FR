---
title: Utilisation des journaux
seo-title: Working with Logs
description: Découvrez comment résoudre les problèmes d’AEM à l’aide des journaux.
seo-description: Learn how to troubleshoot AEM by working with logs.
uuid: af8b7f50-c8d4-4760-9f00-3feb0b79ee4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: da92d751-6f14-4512-9d77-7ecf098bd58e
docset: aem65
exl-id: ab4fc41f-e0e9-4577-aab2-f0b4298f9a59
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 92%

---

# Utilisation des journaux{#working-with-logs}

Cette section contient des informations détaillées sur les journaux disponibles pour vous aider à résoudre les problèmes.

CRX enregistre des journaux détaillés. Après avoir décompressé et démarré Quickstart, vous pouvez retrouver les journaux dans les emplacements suivants :

* crx-quickstart/launchpad/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## Activation du niveau de journalisation DEBUG {#activating-the-debug-log-level}

Le niveau de journalisation par défaut est INFO, ce qui signifie que les messages DEBUG ne sont pas consignés.

Pour activer le niveau de journalisation DEBUG, utilisez l’explorateur CRX afin de définir

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

la propriété à corriger. Ne laissez pas le journal au niveau de débogage DEBUG plus longtemps que nécessaire, car cela génère un grand nombre de journaux.

Une ligne dans le fichier de débogage commence généralement par DEBUG, puis fournit le niveau de journalisation, l’action d’installation et le message du journal. Par exemple :

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

Les niveaux de journalisation sont les suivants :

| 0 | Erreur fatale | L’action a échoué et le programme d’installation ne peut pas continuer. |
|---|---|---|
| 1 | Erreur | L’action a échoué. L’installation se poursuit, mais une partie de CRX n’a pas été installée correctement et ne fonctionnera pas. |
| 2 | Avertissement | L’action a réussi, mais a rencontré des problèmes. CRX risque de ne pas fonctionner correctement. |
| 3 | Informations | L’action a réussi. |

## Option d’informations détaillées utilisée pour la résolution des incidents {#verbose-option-used-for-troubleshooting}

Lorsque vous démarrez CRX, vous pouvez ajouter l’option -v (verbose) à la ligne de commande, comme dans :

` java -jar crx-<*version*>-<*edition*>.jar -v`

Utilisez l’option d’informations détaillées pour procéder à la résolution des incidents, car cette option affiche une partie de la sortie du journal quickstart sur la console.
