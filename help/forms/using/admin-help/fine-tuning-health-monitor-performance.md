---
title: Réglage précis des performances d’Health Monitor
seo-title: Réglage précis des performances de Health Monitor
description: Découvrez comment optimiser les performances de Health Monitor
seo-description: Découvrez comment optimiser les performances de Health Monitor
uuid: 770b10cb-065f-41b5-9594-a291e4311151
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b8f8bddc-0d38-4d5e-b33f-978f04bc16c6
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 88%

---


# Réglage précis des performances de Health Monitor{#fine-tuning-health-monitor-performance}

La collecte des statistiques système qui remplissent Health Monitor a une incidence sur les performances de votre environnement AEM forms. Vous pouvez contrôler cette incidence en définissant les options Java répertoriées ci-dessous dans votre serveur d’applications.

<table>
 <thead>
  <tr>
   <th><p>Propriété</p></th>
   <th><p>Objectif</p></th>
   <th><p>Valeur par défaut</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe.healthmonitor.enabled</p></td>
   <td><p>Active ou désactive le thread Health Monitor.</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.statistics-enabled</p></td>
   <td><p>Active ou désactive la mise en cache Gemfire.</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.healthmonitor.refresh-interval</p></td>
   <td><p>Intervalle en millisecondes après lequel le thread Health Monitor recueille les statistiques.</p></td>
   <td><p>10 minutes (600 000 millisecondes)</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.multicast-port</p></td>
   <td><p>Port multidiffusion utilisé pour communiquer avec d’autres membres du système distribué. S’il est défini sur zéro, la multidiffusion est désactivée pour la détection et la distribution de membres. </p><p>Sélectionnez des adresses et ports multidiffusion différents pour des systèmes distribués distincts. N’utilisez pas uniquement des adresses distinctes.</p></td>
   <td><p>Pas de valeur par défaut. Les valeurs valides sont comprises entre 0 et 65535.</p></td>
  </tr>
  <tr>
   <td><p>statistic-sample-rate</p></td>
   <td><p>Taux en millisecondes auquel les statistiques sont échantillonnées. Les statistiques du système d’exploitation ne sont mises à jour que lors de la collecte d’un échantillon.</p></td>
   <td><p>600000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td>
   <td><p>Cette propriété active ou désactive la collecte de statistiques de Work Manager, telles que le nombre de tâches.</p></td>
   <td><p>true</p></td>
  </tr>
 </tbody>
</table>

## Ajout d’options Java à JBoss {#add-java-options-to-jboss}

1. Arrêtez le serveur d’applications JBoss.
1. Open the *[appserver root]*/bin/run.bat (Windows) or run.sh (Linux or UNIX) in an editor and add any of the Java options as required.
1. Redémarrez le serveur.

## Ajout d’options Java à WebLogic {#add-java-options-to-weblogic}

1. Start the WebLogic administration console by typing https://[host name]:&#39;port&#39;/console in the URL line of a web browser.
1. Saisissez le nom d’utilisateur et le mot de passe créés pour le domaine WebLogic Server, puis cliquez sur Log. Sous Change Center, cliquez sur Lock &amp; Edit.
1. Sous Domain Structure, cliquez sur Environment > Servers et, dans le volet de droite, cliquez sur le nom du serveur géré.
1. Dans l’écran suivant, cliquez sur les onglets Configuration > Server Start.
1. Dans la zone Arguments, ajoutez les arguments souhaités à la fin du contenu actuel. For example, adding - `Dadobe.healthmonitor.enabled=false` disables Health Monitor.
1. Cliquez sur Enregistrer, puis sur Activer les changements.
1. Redémarrez le serveur géré WebLogic.

## Ajout d’options Java à WebSphere {#add-java-options-to-websphere}

1. Dans l’arborescence de navigation de la console d’administration WebSphere, effectuez la procédure suivante pour le serveur d’applications :

   (WebSphere 6.x) Cliquez sur Servers > Application servers

   (WebSphere 7.x) Cliquez sur Servers > Server Types > WebSphere application servers

1. Dans le volet de droite, cliquez sur le nom du serveur.
1. Sous Infrastructure du serveur, cliquez sur Processus Java et formulaires > Définition du process.
1. Sous Additional Properties, cliquez sur Java Virtual Machine.
1. Dans la zone Generic JVM arguments, saisissez les arguments souhaités.
1. Cliquez sur OK ou sur Apply, puis sur Save directly to master configuration.

