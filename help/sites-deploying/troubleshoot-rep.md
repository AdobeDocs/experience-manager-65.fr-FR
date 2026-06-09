---
title: Résolution des problèmes liés à la réplication
description: Cet article fournit des informations sur la manière de résoudre les problèmes de réplication.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
docset: aem65
feature: Configuring
exl-id: cfa822c8-f9a9-4122-9eac-0293d525f6b5
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 809e9f22a5e8c937a24f2d038a17febdaebe8b5e
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 64%

---

# Résolution des problèmes liés à la réplication{#troubleshooting-replication}

Cette page fournit des informations sur la manière de résoudre les problèmes de réplication.

## Problème {#problem}

La réplication (réplication non inverse) échoue pour une raison quelconque.

## Résolution {#resolution}

Il existe plusieurs raisons pour lesquelles la réplication échoue. Cet article explique l’approche que vous pouvez adopter lors de l’analyse de ces problèmes.

**Les réplications sont-elles déclenchées en cliquant sur le bouton d’activation ? Dans le cas CONTRAIRE, procédez comme suit :**

1. Accédez à `/crx/explorer` et connectez-vous en tant que `admin`.
1. Ouvrez l’explorateur de contenu.
1. Vérifiez si un nœud `/bin/replicate` ou `/bin/replicate.json` existe. Si le nœud existe, supprimez-le et enregistrez.

**Les réplications sont-elles mises en file d’attente dans les files d’attente de l’agent de réplication ?**

Vérifiez ceci en accédant à `/etc/replication/agents.author.html`, puis cliquez sur les agents de réplication pour vérifier.

**Si une ou plusieurs files d’attente sont bloquées :**

1. Le statut de la file d’attente est-t-il **blocked** ? Le cas échéant, l’instance de publication n’est-elle pas en cours d’éxécution ou a-t-elle cessé de répondre ? Vérifiez l’instance de publication pour déterminer ce qui ne va pas. En d’autres termes, consultez les journaux et vérifiez s’il existe une erreur OutOfMemory ou un autre problème. S’il s’agit uniquement d’un problème de lenteur, prenez des images mémoire de threads et analysez-les.
1. Le statut de la file d’attente est-t-il **Queue is active - # pending** ? La tâche de réplication peut être bloquée dans une lecture de socket en attente de réponse de l’instance de publication ou du Dispatcher. Cela peut signifier que l’instance de publication ou de Dispatcher est en charge élevée ou bloquée dans un verrou. Dans ce cas, prenez les images mémoire de threads des instances de création et de publication.

   * Ouvrez les images mémoire de threads de l’instance de création dans un analyseur d’image mémoire de threads, vérifiez s’il indique que la tâche d’événement Sling de l’agent de réplication est bloquée dans un socketRead.
   * Ouvrez les images mémoire des threads de la publication dans un analyseur d’image mémoire des threads et analysez les raisons possibles pour lesquelles l’instance de publication ne répond pas. Vous devriez voir un thread dont le nom contient une `/bin/receive` POST. Il s’agit du thread recevant la réplication de l’auteur.

**Si toutes les files d’attente de l’agent sont bloquées**

1. Il est possible qu’un certain élément du contenu ne puisse pas être sérialisé sous /var/replication/data à cause de la corruption du référentiel ou d’un autre problème. Vérifiez les journaux /error.log pour détecter une erreur correspondante. Pour supprimer un élément de réplication défectueux, procédez comme suit :

   1. Accédez à `https://<host>:<port>/crx/de` le et connectez-vous en tant qu’utilisateur administrateur.
   1. Cliquez sur « Outils » dans le menu supérieur.
   1. Cliquez sur le bouton de loupe.
   1. Sélectionnez « XPath » comme type.
   1. Dans la zone « Requête », saisissez cette requête `/jcr:root/var/eventing/jobs//element(*,slingevent:Job) order by @slingevent:created`
   1. Cliquez sur « Rechercher ».
   1. Dans les résultats, les éléments principaux sont les dernières tâches d’événement Sling. Cliquez sur chacune d’elles et recherchez les réplications bloquées qui correspondent à ce qui apparaît en haut de la file d’attente.

1. Il se peut qu’il y ait un problème avec les files d’attente de tâche de framework d’événement Sling. Essayez de redémarrer le lot `org.apache.sling.event` dans `/system/console`.
1. Il se peut que le traitement des tâches soit désactivé. Vous pouvez vérifier cela sous la console Felix dans l’onglet Sling Eventing. Vérifiez s’il s’affiche « Apache Sling Eventing (JOB PROCESSING IS DISABLED!) ».

   * Si c’est le cas, cochez le gestionnaire d’événements de tâche Apache Sling sous l’onglet Configuration dans la console Felix. La case « Traitement des tâches activé » peut être décochée. Si cette option est cochée et que le message « Le traitement des tâches est désactivé » s’affiche toujours, vérifiez s’il existe sous `/apps/system/config` un recouvrement qui désactive le traitement des tâches. Essayez de créer un nœud `osgi:config` pour les `jobmanager.enabled` avec une valeur booléenne de `true` et vérifiez à nouveau si l’activation a démarré et s’il n’y a plus de tâches en file d’attente.

1. Il se peut également que la configuration DefaultJobManager se trouve dans un état incohérent. Cela peut se produire lorsqu’une personne modifie manuellement la configuration « Gestionnaire d’événements de tâche Apache Sling » via la console OSGi (par exemple, en désactivant et réactivant la propriété « Traitement de tâche activé » et en enregistrant la configuration).

   * À ce stade, la configuration DefaultJobManager stockée dans `crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config` entre dans un état incohérent. Et même si la propriété de gestionnaire d’événements de tâche Apache Sling indique que le traitement de tâche activé est coché, lorsque l’on accède à l’onglet Sling Eventing, le message - JOB PROCESSING IS DISABLED s’affiche et la réplication ne fonctionne pas.
   * Pour résoudre ce problème, accédez à la page de configuration de la console OSGi et supprimez la configuration de gestionnaire d’événements de tâche Apache Sling. Redémarrez ensuite le nœud maître du cluster afin de rétablir un état cohérent de la configuration. Cela devrait résoudre le problème et permettre à la réplication de recommencer à fonctionner.

**Créer un replication.log**

Il est parfois utile de définir toutes les journaux de réplication à ajouter dans un fichier journal distinct au niveau DEBUG. Pour ce faire :

1. Accédez à `https://<host>:<port>/system/console/configMgr` et connectez-vous en tant qu’utilisateur administrateur.
1. Identifiez la fabrique Enregistreur de connexion Sling Apache et créez une instance en cliquant sur le bouton **+** à droite de la configuration de la fabrique. Cela crée un nouvel enregistreur de journal.
1. Définissez la configuration comme suit :

   * Niveau de journal : `DEBUG`
   * Chemin d&#39;accès du fichier journal : `logs/replication.log`
   * Catégories : `com.day.cq.replication`

1. Si vous pensez que le problème est lié aux tâches/événements Sling de quelque manière que ce soit, vous pouvez également ajouter ce package Java ; sous `categories:org.apache.sling.event`.

## Suspension de la file d’attente de l’agent de réplication  {#pausing-replication-agent-queue}

Parfois, il peut être judicieux de suspendre la file d’attente de réplication afin de réduire la charge sur le système de création, sans la désactiver. Actuellement, cela n’est possible qu’en configurant temporairement un port non valide. À partir de la version 5.4, un bouton pause a été défini dans la file d’attente de l’agent de réplication, avec certaines restrictions :

1. L’état n’est pas conservé. En d’autres termes, si vous redémarrez un serveur ou qu’un lot de réplication est recyclé, il revient à l’état en cours d’exécution.
1. La pause est inactive pendant une période plus courte (1 heure après l’absence d’activités avec réplication par d’autres threads). En effet, Sling comporte une fonctionnalité qui évite les threads inactifs. Vérifiez si un thread de file d’attente de tâches est inutilisé depuis longtemps. Si tel est le cas, il lance des cycles de nettoyage. En raison du cycle de nettoyage, il arrête le thread et, par conséquent, le paramètre en pause est perdu. Comme les tâches sont conservées, il lance un nouveau thread pour traiter la file d’attente, qui ne contient pas les détails de la configuration en pause. Pour cette raison, la file d’attente passe en état d’exécution.

## Les autorisations de page ne sont pas répliquées lors de l’activation de l’utilisateur ou l’utilisatrice. {#page-permissions-are-not-replicated-on-user-activation}

Les autorisations de page ne sont pas répliquées car elles sont stockées sous les nœuds auxquels l’accès est accordé, pas avec l’utilisateur.

En règle générale, les autorisations de page ne doivent pas être répliquées de l’instance de création vers l’instance de publication et ne le sont pas par défaut. En effet, les droits d’accès doivent être différents dans ces deux environnements. Par conséquent, Adobe recommande de configurer les listes de contrôle d’accès sur l’instance de publication, indépendamment de l’instance de création.

## File d’attente de réplication bloquée lors de la réplication des informations d’espace de noms, de l’instance de création vers l’instance de publication {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

Dans certains cas, la file d’attente de réplication est bloquée lors de la tentative de réplication des informations sur les espaces de noms, de l’instance de création vers l’instance de publication. Ce problème se produit car l’utilisateur de la réplication ne dispose pas du privilège `jcr:namespaceManagement`. Pour éviter ce problème, vérifiez les points suivants :

* L’utilisateur de la réplication (tel que configuré sous l’onglet [Transfert](/help/sites-deploying/replication.md#replication-agents-configuration-parameters) > Utilisateur) existe également sur l’instance de publication.
* L’utilisateur dispose des privilèges de lecture et d’écriture sur le chemin où le contenu est installé.
* L’utilisateur possède le privilège `jcr:namespaceManagement` au niveau du référentiel. Vous pouvez accorder le privilège comme suit :

1. Connectez-vous à CRX/DE (`https://<host>:<port>/crx/de/index.jsp`) en tant qu’administrateur ou administratrice.
1. Cliquez sur l’onglet **Contrôle d’accès**.
1. Sélectionnez **Référentiel**.
1. Cliquez sur **Ajouter une entrée** (icône plus).
1. Entrez le nom de l’utilisateur ou de l’utilisatrice.
1. Sélectionnez `jcr:namespaceManagement` dans la liste des privilèges.
1. Cliquez sur **OK**.
