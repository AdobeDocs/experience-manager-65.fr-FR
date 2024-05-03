---
title: Optimiser les performances de Health Monitor
description: Découvrez comment optimiser les performances de Health Monitor. Contrôlez les statistiques système qui affectent les performances de l’environnement de formulaires à l’aide de l’option de paramétrage JAVA.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 41042e08-5e14-4809-89b7-16d98a72d1b4
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 100%

---

# Optimiser les performances de Health Monitor{#fine-tuning-health-monitor-performance}

La collecte des statistiques système qui renseignent Health Monitor a un impact sur les performances de votre environnement AEM Forms. Vous pouvez contrôler cet impact en définissant les options Java répertoriées ci-dessous dans votre serveur d’applications.

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
   <td><p>Activer ou désactiver le thread Health Monitor</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.statistics-enabled</p></td>
   <td><p>Activer ou désactiver la mise en cache de Gemfire</p></td>
   <td><p>true</p></td>
  </tr>
  <tr>
   <td><p>adobe.healthmonitor.refresh-interval</p></td>
   <td><p>Intervalle en millisecondes après lequel le thread Health Monitor collecte les statistiques</p></td>
   <td><p>10 minutes (600 000 millisecondes)</p></td>
  </tr>
  <tr>
   <td><p>adobe.cache.multicast-port</p></td>
   <td><p>Port multidiffusion utilisé pour communiquer avec d’autres membres du système distribué. S’il est défini sur zéro, la multidiffusion est désactivée pour la découverte et la distribution de membres. </p><p>Remarque : sélectionnez plusieurs adresses et ports de multidiffusion pour différents systèmes distribués. N’utilisez pas uniquement des adresses différentes.</p></td>
   <td><p>Pas de valeur par défaut. Les valeurs valides sont comprises entre 0 et 65 535.</p></td>
  </tr>
  <tr>
   <td><p>statistic-sample-rate</p></td>
   <td><p>Taux en millisecondes auquel les statistiques sont échantillonnées. Les statistiques du système d’exploitation ne sont mises à jour que lorsqu’un échantillon est prélevé.</p></td>
   <td><p>600 000</p></td>
  </tr>
  <tr>
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td>
   <td><p>Cette propriété active ou désactive la collecte de statistiques Work Manager, telles que le nombre de traitements ou d’éléments de travail.</p></td>
   <td><p>true</p></td>
  </tr>
 </tbody>
</table>

## Ajouter des options Java à JBoss {#add-java-options-to-jboss}

1. Arrêtez le serveur d’applications JBoss.
1. Ouvrez la *[racine du serveur d’applications]*/bin/run.bat (Windows) ou run.sh (Linux ou UNIX) dans un éditeur et ajoutez toutes les options Java requises.
1. Redémarrez le serveur.

## Ajouter des options Java à WebLogic {#add-java-options-to-weblogic}

1. Ouvrez la console d’administration WebLogic en saisissant https://[nom hôte]:&#39;port&#39;/console dans la ligne d’URL d’un navigateur web.
1. Tapez le nom d’utilisateur et le mot de passe que vous avez créés pour le domaine du serveur WebLogic, sélectionnez Se connecter sous Centre des modifications, puis Verrouiller et modifier.
1. Sous Structure du domaine, cliquez sur Environment > Serveurs et, dans le volet de droite, cliquez sur le nom du serveur géré.
1. Dans l’écran suivant, cliquez sur les onglets Configuration > Server Start.
1. Dans la zone Arguments, ajoutez les arguments dont vous avez besoin à la fin du contenu actuel. Par exemple, ajouter ‑ `Dadobe.healthmonitor.enabled=false` permet de désactiver Health Monitor.
1. Cliquez sur Save, puis sur Activate Changes.
1. Redémarrez le serveur géré WebLogic.

## Ajouter des options Java à WebSphere {#add-java-options-to-websphere}

1. Dans l’arborescence de navigation de la console d’administration WebSphere, procédez comme suit pour votre serveur d’applications :

   (WebSphere 6.x) Cliquez sur Serveurs > Serveurs d’applications

   (WebSphere 7.x) Cliquez sur Serveurs > Types de serveurs > Serveurs d’applications WebSphere.

1. Dans le volet de droite, cliquez sur le nom du serveur.
1. Sous Infrastructure du serveur, cliquez sur Java et Forms Workflow > Définition du processus.
1. Sous Propriétés supplémentaires, cliquez sur Machine virtuelle Java (JVM).
1. Dans la zone Arguments JVM génériques, saisissez les arguments dont vous avez besoin.
1. Cliquez sur OK ou Appliquer, puis sur Enregistrer directement dans la configuration principale.
