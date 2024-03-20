---
title: Restructuration des référentiels e-Commerce dans AEM 6.5
description: Découvrez comment apporter les modifications nécessaires pour migrer vers la nouvelle structure de référentiel dans AEM 6.5 pour e-Commerce.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: 78b7c497-c474-4308-bfab-8f424b5f7268
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 100%

---

# Restructuration des référentiels e-Commerce dans AEM 6.5{#e-commerce-repository-restructuring-in-aem}

Comme indiqué dans la page parent [Restructuration des référentiels dans AEM 6.5](/help/sites-deploying/repository-restructuring.md), les clients effectuant une mise à niveau vers AEM 6.5 doivent utiliser cette page pour évaluer le travail associé aux modifications des référentiels ayant un impact sur la solution de e-Commerce d’AEM. Certaines modifications demandent du travail lors du processus de mise à niveau vers AEM 6.5, tandis que d’autres peuvent être différées jusqu’à une mise à niveau vers une version future.

## Avec la mise à niveau vers la version 6.5 {#with-upgrade}

### Données sur les produits, les commandes, les collections, les classifications, les méthodes d’expédition et les modes de paiement {#product-order-collections-classifications-shipping-methods-and-payment-methods-data}

<table>
 <tbody>
  <tr>
   <td><strong>Emplacement précédent</strong></td>
   <td><p><code>/etc/commerce/products</code></p> <p><code>/etc/commerce/orders</code></p> <p><code>/etc/commerce/collections</code></p> <p><code>/etc/commerce/classifications</code></p> <p><code>/etc/commerce/shipping-methods</code></p> <p><code>/etc/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>Nouveaux emplacements</strong></td>
   <td><p><code>/var/commerce/products</code></p> <p><code>/var/commerce/orders</code></p> <p><code>/var/commerce/collections</code></p> <p><code>/var/commerce/classifications</code></p> <p><code>/var/commerce/shipping-methods</code></p> <p><code>/var/commerce/payment-methods</code></p> </td>
  </tr>
  <tr>
   <td><strong>Conseil de restructuration</strong></td>
   <td><p>Vous pouvez utiliser une tâche <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">Migration différée</a> pour migrer des données E-commerce.</p> <p>Elle effectue les étapes suivantes :</p>
    <ul>
     <li>Elle ajuste les références à l’ancien emplacement pour qu’elles pointent vers le nouvel emplacement.</li>
     <li>Elle déplace le contenu de l’ancien emplacement vers le nouvel emplacement.</li>
     <li>Elle supprime l’ancien emplacement pour activer éventuellement l’utilisation du nouvel emplacement dans l’ensemble du système.</li>
    </ul> <p>Les emplacements couverts par la tâche sont les suivants :</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>Pour les catalogues plus volumineux, Adobe vous recommande d’exécuter la tâche de migration de commerce individuellement en transmettant la propriété système Java™ suivante à AEM :</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>Après la migration, redémarrez AEM.</p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>
