---
title: Résolution des problèmes liés à la réplication
seo-title: Résolution des problèmes liés à la réplication
description: Cet article fournit des informations sur la manière de résoudre les problèmes de réplication.
seo-description: Cet article fournit des informations sur la manière de résoudre les problèmes de réplication.
uuid: 1662bf60-b000-4eb2-8834-c6da607128fe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 0d055be7-7189-4587-8c7c-2ce34e22a6ad
docset: aem65
translation-type: tm+mt
source-git-commit: 38ef8fc8d80009c8ca79aca9e45cf10bd70e1f1e
workflow-type: tm+mt
source-wordcount: '1255'
ht-degree: 81%

---


# Résolution des problèmes liés à la réplication{#troubleshooting-replication}

Cette page fournit des informations sur la manière de résoudre les problèmes de réplication.

## Problème {#problem}

La réplication (réplication non inversée) échoue pour quelque raison que ce soit.

## Résolution {#resolution}

Il existe diverses facteurs pouvant mener à l’échec d’une réplication. Cet article explique l’approche que l’on peut prendre en analysant de ces problèmes.

**Les réplications sont-elles déclenchées en cliquant sur le bouton d’activation ? Si la réponse est NON, procédez comme suit :**

1. Accédez à /crx/explorer et connectez-vous en tant qu’administrateur.
1. Ouvrez « Content Explorer » (l’explorateur de contenu).
1. Vérifiez si un nœud /bin/replicate ou /bin/replicate.json existe. Si le noeud existe, supprimez-le puis enregistrez les modifications.

**Les réplications sont-elles alignées dans les files d’attente des agents de réplication ?**

Vérifiez ce point en accédant à /etc/replication/agents.author.html, puis en cliquant sur les agents de réplication à vérifier.

**Si une ou plusieurs files d’attente sont bloquées :**

1. La file d’attente affiche-t-elle l’état **bloqué** ? Le cas échéant, l’instance de publication n’est-elle pas en cours d’éxécution ou a-t-elle cessé totalement de répondre ? Vérifiez l’instance de publication pour détecter le problème (c’est-à-dire vérifiez les journaux pour voir s’il existe une erreur OutOfMemory ou un autre problème). S’il s’agit d’une lenteur générale, prenez des thread dumps et analysez-les.
1. L&#39;état de la file d&#39;attente indique-t-il **La file d&#39;attente est principale - # en attente** ? La tâche de réplication peut être simplement bloquée dans une fiche, en attente d’une instance de publication ou du dispatcher pour répondre. Il se peut également que l’instance de publication ou le dispatcher subisse un chargement élevé ou qu’il soit coincé dans un verrouillage. Prenez les thread dumps de l’auteur et de la publication dans ce cas.

   * Ouvrez les thread dumps de l’auteur dans un programme d’analyse de thread dump, vérifiez s’il indique que la tâche sling eventing de l’agent de réplication est boquée dans un socketRead.
   * Ouvrez les thread dumps de la publication dans un programme d’analyse de thread dump, analysez ce qui peut causer le manque de réaction de l’instance de publication. Vous devriez voir un thread avec le POST /bin/receive dans son nom, c&#39;est-à-dire le thread recevant la réplication de l&#39;auteur.

**Si toutes les files d’attente de l’agent sont bloquées**

1. Il est possible qu’un certain élément de contenu ne puisse pas être sérialisé sous /var/Replication/data en raison d’une corruption du référentiel ou d’un autre problème. Recherchez une erreur connexe dans le fichier logs/error.log. Pour supprimer un élément de réplication défectueux, procédez comme suit :

   1. Accédez à https://&lt;hôte>:&lt;port>/crx/de et connectez-vous en tant qu’utilisateur administrateur.
   1. Cliquez sur « Outils » dans le menu supérieur.
   1. Cliquez sur le bouton représentant une loupe.
   1. Sélectionnez « XPath » comme type.
   1. Dans la zone &quot;Requête&quot;, saisissez l’ordre de requête /jcr:root/var/eventing/jobs//element(*,slingevent:Job) par @slingevent:created.
   1. Cliquez sur « Search » (Rechercher).
   1. Les résultats affichés dans la partie supérieure de la page correspondent aux dernières tâches sling eventing. Cliquez sur chacune d’entre elles et recherchez les réplications bloquées qui correspondent aux résultats visibles dans la partie supérieure de la file d’attente.

1. Il peut exister un problème avec les files d’attente des tâches de structure de sling eventing. Essayez de redémarrer le lot org.apache.sling.event dans la console du système.
1. Le traitement des tâches peut être complètement désactivé. Vous pouvez vérifier cela dans Console Felix, sur l’onglet Sling Eventing. Vérifiez si « Apache Sling Eventing (JOB PROCESSING IS DISABLED!) » s’affiche.

   * Si c’est le cas, vérifiez le gestionnaire Apache Sling Job Event sous l’onglet de configuration de la Console Felix. Il se peut que la case « Job processing Enabled » (Traitement des tâches activé) ne soit pas été cochée. Si la case est cochée et que le message « job processing is disabled » s’affiche toujours, vérifiez s’il y a une incrustation sous /apps/system/config qui désactive le traitement de tâche. Essayez de créer un nœud osgi:config pour jobmanager.enabled avec une valeur booléenne de true. Revérifiez ensuite si l’activation est déclenchée et s’il n’y a plus de tâches dans la file d’attente.

1. Il se peut également que la configuration DefaultJobManager ait cessé de fonctionner normalement. Cela peut avoir lieu lorsqu’une personne modifie manuellement la configuration du gestionnaire Apache Sling Job Event via la console OSGi (par exemple, en désactivant et en réactivant la propriété « Job Processing Enabled », puis en enregistrant la configuration).

   * À ce stade, la configuration de DefaultJobManager stockée sur crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config cesse de fonctionner normalement. Même si la case « Job Processing Enabled » de la propriété « Apache Sling Job Event Handler » est cochée, lorsque l’on accède à l’onglet Sling Eventing, le message suivant s’affiche : « JOB PROCESSING IS DISABLED » (Le traitement des tâches est désactivé) et la réplication ne fonctionne pas.
   * Pour résoudre ce problème, vous devez accéder à la page Configuration de la console OSGi et supprimer la configuration &quot;Apache Sling Job Événement Handler&quot;. Relancez ensuite le noeud maître du cluster pour que la configuration revienne à un état stable. Cela devrait résoudre le problème et faire fonctionner de nouveau la réplication.

**Création de replication.log**

Il est parfois très utile de programmer toute la journalisation de la réplication de sorte qu’elle soit ajouté à un fichier journal séparé au niveau de DEBUG. Pour ce faire :

1. Accédez à https://host:port/system/console/configMgr et connectez-vous en tant qu’administrateur.
1. Recherchez l&#39;usine Apache Sling Logging Logger et créez une instance en cliquant sur le bouton **+** à droite de la configuration de l&#39;usine. Cela entraîne la création d’un enregistreur de connexions.
1. Définissez la configuration comme suit :

   * Niveau de journal : DEBUG
   * Chemin du fichier journal : logs/replication.log
   * Catégories : com.day.cq.replication

1. Si vous soupçonnez que le problème est lié de quelque manière que ce soit à sling eventing/jobs, vous pouvez également ajouter ce module Java sous categories:org.apache.sling.event.

## Mise en pause de la file d’attentre des agents de réplication  {#pausing-replication-agent-queue}

Parfois, il vaut mieux mettre la file d’attente de réplication en pause pour réduire le chargement sur le système de création, sans le désactiver. Actuellement, cela est uniquement possible par le biais d’une configuration temporaire d’un port non valide. À partir de la version 5.4, vous pourrez voir un bouton pause dans la file d’attente des agents de réplication, mais avec certaines limites.

1. L’état n’est pas stable, c’est-à-dire que si vous redémarrez un serveur si un lot est réutilisé, il repasse en mode d’exécution.
1. La pause reste inactive durant une période plus courte (sans travail 1ִ heure après qu’aucune activité avec la réplication par d’autres threads ne soit enregistrée) et pas une minute de plus. Il existe en effet une fonction dans sling qui permet d’éviter les threads inactifs. Vérifiez si un thread de file d’attente des tâches a été inutilisé pour une période plus longue. Le cas échéant, cela déclenche les cycles de nettoyage. En raison du cycle de nettoyage, le thread est arrêté, et le paramètre mis sur pause est perdu. Étant donné que les tâches sont conservées, un nouveau thread est lancé pour traiter la file d’attente qui ne contient pas de détails sur la configuration mise en pause. En conséquence, la file d’attente passe en mode d’exécution.

## Les autorisations de page ne sont pas répliquées lors de l’activation des utilisateurs  {#page-permissions-are-not-replicated-on-user-activation}

Les autorisations de page ne sont pas répliquées, car elles sont stockées sous les nœuds auxquels l’accès est accordé, pas avec l’utilisateur.

En général, des autorisations de page ne doivent pas être répliquées depuis l’instance d’auteur vers l’instance de publication, et ne sont pas définies par défaut. Cela est dû au fait que les droits d’accès doivent être différents dans ces deux environnements. Par conséquent, il est recommandé de configurer les listes de contrôle d’accès de la publication séparément de l’auteur.

## La file d’attente de réplication est bloquée lors de la réplication des informations sur les espaces de noms depuis l’auteur vers la publication.  {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

Dans certains cas, la file d’attente de réplication est bloquée lors de la tentative de réplication des informations sur les espaces de noms depuis l’instance d’auteur vers l’instance de publication. Cela se produit car l&#39;utilisateur de réplication n&#39;a pas le privilège `jcr:namespaceManagement`. Pour éviter ce problème, vérifiez les points suivants :

* L’utilisateur de réplication (tel que configuré sous l’onglet [Transport&lt;a1/&quot;Utilisateur) existe également sur l’instance de publication.](/help/sites-deploying/replication.md#replication-agents-configuration-parameters)
* L’utilisateur dispose des privilèges de lecture et d’écriture sur le chemin où le contenu est installé.
* L&#39;utilisateur dispose du privilège `jcr:namespaceManagement` au niveau du référentiel. Vous pouvez accorder le privilège comme suit :

1. Connectez-vous à CRX/DE ( `https://localhost:4502/crx/de/index.jsp`) en tant qu’administrateur.
1. Cliquez sur l’onglet **Contrôle d’accès**.
1. Sélectionnez **Référentiel**.
1. Cliquez sur **Ajouter une entrée** (icône Plus).
1. Entrez le nom de l’utilisateur.
1. Sélectionnez `jcr:namespaceManagement` dans la liste de privilèges.
1. Cliquez sur OK.

