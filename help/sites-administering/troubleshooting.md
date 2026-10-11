---
title: Utiliser les journaux
description: Découvrez comment résoudre les problèmes d’AEM en utilisant les journaux.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: ab4fc41f-e0e9-4577-aab2-f0b4298f9a59
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 5ef752af-d616-5b23-8312-06964e46b208
    internal-label: Administering
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 100%
---
# Utiliser les journaux{#working-with-logs}

Cette section contient des informations détaillées sur les journaux disponibles pour vous aider à résoudre les problèmes.

>[!NOTE]
>
>Pour plus d’informations sur les journaux, voir :
>
>* [Maintenance du journal d’audit dans AEM](/help/sites-administering/operations-audit-log.md)
>* [Utilisation des enregistrements d’audit et des fichiers journaux](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)

CRX enregistre des journaux détaillés. Une fois que vous avez décompressé et démarré Quickstart, vous pouvez trouver les journaux aux emplacements suivants :

* crx-quickstart/launchpad/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## Activation du niveau de journalisation DÉBOGUER {#activating-the-debug-log-level}

Le niveau de journalisation par défaut est INFO, ce qui signifie que les messages DÉBOGUER ne sont pas consignés.

Pour activer le niveau de journalisation DEBUG, utilisez l’explorateur CRX pour définir

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

la propriété à corriger. Ne laissez pas le journal au niveau de journalisation DEBUG plus longtemps que nécessaire, car cela génère un grand nombre de journaux.

Une ligne dans le fichier de débogage commence généralement par DEBUG, puis fournit le niveau de journalisation, l’action d’installation et le message du journal. Par exemple :

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

Les niveaux de journal sont les suivants :

| 0 | Erreur fatale | L’action a échoué et le programme d’installation ne peut pas continuer. |
|---|---|---|
| 1 | Erreur | L’action a échoué. L’installation se poursuit, mais une partie de CRX n’a pas été installée correctement et ne fonctionnera pas. |
| 2 | Avertissement | L’action a réussi, mais des problèmes sont survenus. CRX peut fonctionner correctement ou non. |
| 3 | Informations | L’action a réussi. |

## Option d’informations détaillées utilisée pour la résolution des incidents {#verbose-option-used-for-troubleshooting}

Lorsque vous démarrez CRX, vous pouvez ajouter l’option -v (verbose) à la ligne de commande :

` java -jar crx-<*version*>-<*edition*>.jar -v`

Utilisez l’option d’informations détaillées pour procéder à la résolution des incidents, car cette option affiche une partie de la sortie du journal quickstart sur la console.
