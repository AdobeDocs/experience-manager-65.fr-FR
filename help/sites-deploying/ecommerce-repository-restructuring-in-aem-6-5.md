---
title: Restructuration des référentiels e-Commerce dans AEM 6.5
seo-title: Restructuration des référentiels e-Commerce dans AEM 6.5
description: Découvrez comment apporter les modifications nécessaires pour migrer vers la nouvelle structure de référentiel dans AEM 6.5 pour e-Commerce.
seo-description: Découvrez comment apporter les modifications nécessaires pour migrer vers la nouvelle structure de référentiel dans AEM 6.5 pour e-Commerce.
uuid: 1fff1a4b-c8d0-4016-92fb-e2ea26e3a302
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 28c92e7d-2106-4333-afa6-c5528a00d7b4
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 77%

---


# Restructuration des référentiels e-Commerce dans AEM 6.5{#e-commerce-repository-restructuring-in-aem}

Comme décrit sur la page parent [Restructuration du référentiel dans AEM 6.5](/help/sites-deploying/repository-restructuring.md), les clients qui effectuent la mise à niveau vers AEM 6.5 doivent utiliser cette page pour évaluer l&#39;effort de travail associé aux modifications du référentiel qui affectent la solution de commerce électronique de l&#39;AEM. Certaines modifications nécessitent un effort de travail pendant le processus de mise à niveau AEM 6.5, tandis que d’autres peuvent être différées jusqu’à une mise à niveau ultérieure.

## Avec la mise à niveau vers la version 6.5 {#with-upgrade}

### Données sur les produits, commandes, collections, classifications, méthodes d’expédition et modes de paiement {#product-order-collections-classifications-shipping-methods-and-payment-methods-data}

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
   <td><p>Vous pouvez utiliser une tâche de <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">migration différée</a> pour migrer les données e-Commerce.</p> <p>La procédure effectue les étapes suivantes :</p>
    <ul>
     <li>ajuste les références à l’ancien emplacement pour pointer vers le nouvel emplacement</li>
     <li>transfère le contenu de l’ancien emplacement vers le nouvel emplacement</li>
     <li>supprime l’ancien emplacement pour éventuellement activer l’utilisation du nouvel emplacement dans l’ensemble du système</li>
    </ul> <p>Les emplacements couverts par la tâche sont les suivants :</p>
    <ul>
     <li>/etc/commerce/products</li>
     <li>/etc/commerce/collections<br /> </li>
     <li>/etc/commerce/orders<br /> </li>
     <li>/etc/commerce/payment-methods<br /> </li>
     <li>/etc/commerce/shipping-methods<br /> </li>
    </ul> <p>Pour les catalogues plus volumineux, il est recommandé d’exécuter la tâche de migration de commerce individuellement en transmettant la propriété système Java suivante à AEM :</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>Après la migration, AEM doit être redémarré.</p> </td>
  </tr>
  <tr>
   <td><strong>Remarques</strong></td>
   <td>N/A<br /> </td>
  </tr>
 </tbody>
</table>

