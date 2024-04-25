---
title: Arborescence de la performance
description: Découvrez les étapes à suivre pour résoudre les problèmes de performances dans AEM.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: f2f968b8-b21c-487d-bc0d-ed60903bc4bf
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 99%

---

# Arborescence de la performance{#performance-tree}

## Portée {#scope}

Le diagramme suivant est destiné à fournir des conseils sur les étapes à suivre pour résoudre les problèmes de performances. Il est divisé en cinq sections afin de faciliter la lecture.

Chaque étape du diagramme est associée à une ressource ou à une recommandation.

## Conditions préalables et hypothèses {#prerequisites-and-assumptions}

L’hypothèse est qu’un problème de performance est observé sur une page donnée (une console d’AEM ou une page web) et peut être reproduit de manière cohérente. Disposer d’un moyen de tester ou de surveiller les performances est une condition préalable à l’ouverture de l’enquête.

L’analyse commence à l’étape 0. L’objectif est de déterminer quelle entité (Dispatcher, hôte externe ou AEM) est responsable du problème de performance, puis de découvrir la zone (serveur ou réseau) qui doit être étudiée.

### Section 1 {#section}

![chlimage_1-103](assets/chlimage_1-103.png)

### Section 2 {#section-1}

![chlimage_1-104](assets/chlimage_1-104.png)

### Section 3 {#section-2}

![chlimage_1-105](assets/chlimage_1-105.png)

### Section 4 {#section-3}

![chlimage_1-106](assets/chlimage_1-106.png)

### Section 5 {#section-4}

![chlimage_1-107](assets/chlimage_1-107.png)

## Liens de référence {#reference-links}

<table>
 <tbody>
  <tr>
   <td><strong>Étape</strong></td>
   <td><strong>Titre</strong></td>
   <td><strong>Ressources</strong></td>
  </tr>
  <tr>
   <td><strong>Étape 0</strong></td>
   <td>Analyser le flux de requêtes</td>
   <td><p>Vous pouvez utiliser l’analyse des requêtes HTTP standard dans le navigateur pour analyser le flux de requêtes. Pour plus d’informations sur la manière d’effectuer cette analyse sur Chrome, veuillez consulter :<br /> </p> <p><a href="https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading">https://developer.chrome.com/docs/devtools/</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Étape 2</strong></td>
   <td>Les requêtes proviennent-elles d’hôtes externes ?</td>
   <td>Vous pouvez utiliser l’analyse des requêtes HTTP standard dans le navigateur pour analyser le flux de requêtes. Consultez les liens ci-dessus pour savoir comment effectuer cette analyse sur Chrome.<br /> </td>
  </tr>
  <tr>
   <td><strong>Étape 3</strong></td>
   <td>Les requêtes peuvent-elles être mises en cache ?</td>
   <td>Pour plus d’informations sur les requêtes pouvant être mises en cache et pour obtenir des conseils généraux sur l’optimisation des performances du Dispatcher, veuillez consulter <a href="/help/sites-deploying/configuring-performance.md#optimizing-performance-when-using-the-dispatcher">Optimisation des performances du Dispatcher</a>.</td>
  </tr>
  <tr>
   <td><strong>Étape 4</strong></td>
   <td>Les demandes proviennent-elles du Dispatcher ?</td>
   <td><p>Pour vérifier si les requêtes sont correctement mises en cache, veuillez consulter la <a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#debugging">documentation sur le débogage du Dispatcher</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Étape 5</strong></td>
   <td>Le Dispatcher essaie-t-il d’authentifier chaque demande via AEM ?</td>
   <td>Vérifiez si le Dispatcher envoie les requêtes <code>HEAD</code> à AEM pour authentification avant de diffuser la ressource mise en cache. Recherchez les requêtes <code>HEAD</code> dans le <code>access.log</code> d’AEM. Pour plus d’informations, consultez la section <a href="/help/sites-deploying/configure-logging.md">Journalisation</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Étape 6</strong></td>
   <td>L’emplacement géographique du Dispatcher est-il éloigné des utilisateurs et utilisatrices ?</td>
   <td>Rapprochez le Dispatcher des utilisateurs et utilisatrices.</td>
  </tr>
  <tr>
   <td><strong>Étape 7</strong></td>
   <td>La couche réseau du Dispatcher est-elle normale ?</td>
   <td><br /> Examinez la couche réseau pour détecter les problèmes de saturation et de latence.<p> </p> </td>
  </tr>
  <tr>
   <td><strong>Étape 8</strong></td>
   <td>La lenteur est-elle reproductible avec une instance locale ?</td>
   <td><br /> <p>Utiliser <a href="/help/sites-developing/tough-day.md">Tough Day</a> pour répliquer des conditions « réelles » à partir des instances de production. Si ce scénario n’est pas réaliste pour l’espace de votre développement, veillez à tester l’instance de production (ou une instance d’évaluation identique) dans un contexte réseau différent.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Étape 9</strong></td>
   <td>L’emplacement géographique du serveur est-il éloigné des utilisateurs et utilisatrices ?</td>
   <td>Rapprochez le serveur des utilisateurs et utilisatrices.</td>
  </tr>
  <tr>
   <td><strong>Étapes 10 et 29</strong></td>
   <td>Examiner la couche réseau</td>
   <td><p>Examinez la couche réseau pour détecter les problèmes de saturation et de latence.</p> <p>Pour le niveau de création, il est recommandé que la latence ne dépasse pas 100 millisecondes.</p> <p>Pour plus d’informations sur les conseils d’optimisation des performances, reportez-vous <a href="https://helpx.adobe.com/customer-care-office-hours/aem/6x-performance-tuning-best-practices.html">à cette page</a>.</p> </td>
  </tr>
  <tr>
   <td><strong>Étape 11</strong></td>
   <td>Rapprochez le serveur ou ajoutez-en un par région</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Étape 12</strong></td>
   <td>Résoudre les problèmes liés au serveur AEM</td>
   <td>Pour plus d’informations, consultez les sous-étapes suivantes du diagramme.</td>
  </tr>
  <tr>
   <td><strong>Étape 13</strong></td>
   <td>Vérifier les exigences matérielles</td>
   <td>Consultez la documentation sur les <a href="/help/managing/hardware-sizing-guidelines.md">Instructions de dimensionnement du matériel</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Étape 14</strong></td>
   <td>Vérification des causes fréquentes des problèmes de performances</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Étape 15</strong></td>
   <td>Identification des demandes lentes</td>
   <td><p>Vous pouvez identifier les requêtes lentes en analysant le <code>request.log</code> ou à l’aide de <code>rlog.jar</code>.</p> <p>Pour plus d’informations sur l’utilisation de rlog.jar, consultez cette page.</p> <p>Voir <a href="/help/sites-deploying/monitoring-and-maintaining.md#using-rlog-jar-to-find-requests-with-long-duration-times">Recherche de requêtes avec de longues durées à l’aide de rlog.jar</a>.<br /> </p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Étape 16</strong></td>
   <td>Serveur de profil</td>
   <td><p>Pour plus d’informations sur les outils de création de profils utilisateur que vous pouvez utiliser avec AEM, consultez <a href="/help/sites-deploying/monitoring-and-maintaining.md#tools-for-monitoring-and-analyzing-performance">Outils de surveillance et d’analyse des performances</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Étape 17</strong></td>
   <td>Recherche de méthodes lentes dans le profilage</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Étape 18</strong></td>
   <td>Scénarios courants de création de profils utilisateur</td>
   <td>Voir <a href="/help/sites-deploying/monitoring-and-maintaining.md#analyzing-specific-scenarios">Analyse de scénarios spécifiques</a> dans la section Optimisation des performances.<br /> </td>
  </tr>
  <tr>
   <td><strong>Étape 19</strong></td>
   <td>Processeur à 100 %</td>
   <td><a href="/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance">https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr</a></td>
  </tr>
  <tr>
   <td><strong>Étape 20</strong></td>
   <td>Mémoire insuffisante</td>
   <td><br />
    <ol>
     <li><a href="/help/sites-deploying/monitoring-and-maintaining.md#out-of-memory">Mémoire insuffisante</a></li>
     <li><a href="/help/sites-deploying/troubleshooting.md">Mon application renvoie des erreurs de mémoire insuffisante</a></li>
     <li><a href="https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html?lang=fr">Analysez les problèmes de mémoire.</a><br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Étape 21</strong></td>
   <td>E/S de disque</td>
   <td><p>Voir la section <a href="/help/sites-deploying/monitoring-and-maintaining.md#disk-i-o">E/S de disque</a> dans la documentation Surveillance et maintenance.</p> </td>
  </tr>
  <tr>
   <td><strong>Étapes 22 et 22.1</strong></td>
   <td>Ratio de cache</td>
   <td>Voir <a href="/help/sites-deploying/configuring-performance.md#calculating-the-dispatcher-cache-ratio">Calcul du ratio de cache de Dispatcher</a>.<br /> <br /> </td>
  </tr>
  <tr>
   <td><strong>Étape 23</strong></td>
   <td>Requêtes lentes</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">Bonnes pratiques relatives aux requêtes et à l’indexation</a></td>
  </tr>
  <tr>
   <td><strong>Étape 24</strong></td>
   <td>Réglage du référentiel</td>
   <td>
    <ul>
     <li><a href="https://helpx.adobe.com/customer-care-office-hours/aem/6x-performance-tuning-best-practices.html">Conseils de réglage de la performance</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#configuring-for-performance">Configuration des performances</a></li>
     <li><a href="https://www.slideshare.net/jukka/repository-performance-tuning">Réglage de la performance du référentiel</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Étape 25</strong></td>
   <td>Workflows en cours d’exécution</td>
   <td>
    <ul>
     <li><a href="/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing">Traitement de workflows simultanés</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#configure-the-queue-for-a-specific-workflow">Configuration de la file d’attente pour un workflow spécifique</a></li>
     <li><a href="/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances">Purge régulière des instances de workflow</a></li>
     <li><a href="/help/sites-developing/workflows.md#transient-workflows">Workflows transitoires</a><br /> </li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Étape 26</strong></td>
   <td>Infrastructure MSM</td>
   <td><p><a href="/help/sites-administering/msm-best-practices.md">Bonnes pratiques relatives au gestionnaire de sites multiples</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Étape 27</strong></td>
   <td>Réglage d’Assets</td>
   <td>
    <ol>
     <li><a href="/help/sites-deploying/configuring-performance.md#cq-dam-asset-synchronization-service">Service de synchronisation d’Assets</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#multiple-dam-instances">Instances multiples de gestion des ressources numériques</a></li>
     <li>Article présentant des conseils sur l’optimisation des performances disponible <a href="https://helpx.adobe.com/customer-care-office-hours/aem/6x-performance-tuning-best-practices.html">ici</a>.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Étape 28</strong></td>
   <td>Sessions non fermées</td>
   <td><p> </p> <p><a href="/help/sites-administering/troubleshoot.md#checking-for-unclosed-jcr-sessions">Contrôle des sessions JCR non fermées</a></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Étape 30</strong></td>
   <td>Rapprochement du Dispatcher (ajout d’un Dispatcher par « région » ?)</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Étape 31</strong></td>
   <td>Utilisation d’un réseau CDN devant le Dispatcher</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">Utilisation du Dispatcher avec un CDN</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Étape 32</strong></td>
   <td>Pour décharger le serveur AEM, utilisez la gestion de session au niveau du Dispatcher.</td>
   <td><p><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement">Activation de sessions sécurisées</a></p> </td>
  </tr>
  <tr>
   <td><strong>Étape 33</strong></td>
   <td>Activation de la mise en cache potentielle des demandes</td>
   <td>
    <ol>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=fr">Configuration générale du Dispatcher</a></li>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache">Configuration du cache du Dispatcher</a></li>
    </ol> <p>Comment améliorer le ratio de cache ; faire en sorte que les requêtes puissent être mises en cache (bonnes pratiques du Dispatcher)</p> <p>Tenez également compte des paramètres ci-dessous pour optimiser vos configurations de mise en cache.<br /> </p>
    <ol>
     <li>Définissez une règle de non-mise en cache pour une requête HTTP qui n’est pas GET.</li>
     <li>Configurez les chaînes de requête pour qu’elles ne puissent pas être mises en cache.</li>
     <li>Ne mettez pas en cache les URL avec des extensions manquantes.</li>
     <li>En-têtes d’authentification du cache (possibles depuis la version 4.1.10 du Dispatcher)</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Étape 34</strong></td>
   <td>Mettre à niveau la version du Dispatcher</td>
   <td><p>Vous pouvez télécharger la dernière version du Dispatcher à cet emplacement :</p> <p><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html?lang=fr">Suivez le lien.</a></p> </td>
  </tr>
  <tr>
   <td><strong>Étape 35</strong></td>
   <td>Configuration du Dispatcher</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=fr">Configuration du Dispatcher</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Étape 36</strong></td>
   <td>Vérification de l’invalidation du cache</td>
   <td><br />
    <ul>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment">Invalidation du cache pour le niveau de création</a></li>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=fr#invalidating-dispatcher-cache-from-a-publishing-instance">Invalidation du cache pour le niveau de publication.</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Étapes 37 et 38</strong></td>
   <td>Chargement différé</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html">Suivez la session Gem sur la performance web d’AEM.</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Étape 39</strong></td>
   <td>Utilisation de la pré-connexion pour réduire la surcharge de connexion</td>
   <td>Reportez-vous à la session Gem ci-dessus. Vous pouvez également accéder à d’autres documents sur la pré-connexion sur W3c : <a href="https://html.spec.whatwg.org/#linkTypes">https://html.spec.whatwg.org/#linkTypes</a></td>
  </tr>
  <tr>
   <td><strong>Étapes 40 et 41</strong><br /> </td>
   <td>Latence et temps de réponse des hôtes externes</td>
   <td>Examinez la latence et le temps de réponse des hôtes externes.</td>
  </tr>
  <tr>
   <td><strong>Étapes 45<br /> et 47</strong><br /> </td>
   <td>Utilisation du HTTP/2</td>
   <td>Voir la session Gem des étapes 37, 38 et 39. En outre, consultez <a href="https://help-forums.adobe.com/content/adobeforums/en/experience-manager-forum/adobe-experience-manager.topic.html/forum__kdzc-does_anyoneknowwhe.html">cet article</a> de forum sur la prise en charge du HTTP/2<br />. </td>
  </tr>
  <tr>
   <td><strong>Étape 49</strong></td>
   <td>Réduction de la taille d’une payload</td>
   <td><a href="/help/sites-deploying/osgi-configuration-settings.md">Activez Gzip</a> et <a href="https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html">réduisez la taille de l’image</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Étapes 42 et 43</strong></td>
   <td>Keep-Alive</td>
   <td><p>L’en-tête <code>Keep-Alive</code> est-il présent dans les différentes requêtes de réutilisation des connexions ? Dans le cas contraire, cela signifie que chaque requête mène à établir une nouvelle connexion, entraînant ainsi une surcharge inopportune. (Analyse des requêtes HTTP standard dans le navigateur)</p> <p>Vous pouvez accéder à l’<a href="/help/sites-administering/proxy-jar.md">Outil Serveur proxy</a> pour vérifier les connexions Keep-alive.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Étape 44</strong></td>
   <td>Combien de requêtes sont-elles effectuées ?</td>
   <td>Exécutez l’analyse des requêtes HTTP standard dans le navigateur.</td>
  </tr>
  <tr>
   <td><strong>Étape 46</strong></td>
   <td>Réduction du nombre de requêtes</td>
   <td>
    <ol>
     <li>Concaténation de ressources (images, sprites CSS, JSON)<br /> </li>
     <li>Incorporation de bibliothèques clientes
      <ol>
       <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders">Création de dossiers dans la bibliothèque cliente</a> : consultez la section Utilisation d’incorporations pour réduire les demandes.</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Étape 48</strong></td>
   <td>Quelle est la taille de la payload ?</td>
   <td>Analyse des requêtes HTTP standard dans le navigateur</td>
  </tr>
  <tr>
   <td><strong>Étapes 50 et 51</strong></td>
   <td>Blocage du code JS</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html">https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html</a></td>
  </tr>
 </tbody>
</table>
