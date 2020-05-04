---
title: SPA et rendu côté serveur
seo-title: SPA et rendu côté serveur
description: 'null'
seo-description: 'null'
uuid: 27e26e3f-65d4-4069-b570-58b8b9e2a1ae
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 844e5c96-2a18-4869-b4c8-2fb9efe0332a
docset: aem65
translation-type: tm+mt
source-git-commit: 590dc4464182d4baf8293e7bb0774ce92971c0af

---


# SPA et rendu côté serveur{#spa-and-server-side-rendering}

>[!NOTE]
>
>L’éditeur d’applications monopages est la solution recommandée pour les projets qui nécessitent un rendu côté client basé sur la structure d’applications monopages (par exemple, Réagir ou Angular).

>[!NOTE]
>
>AEM 6.5.1.0 ou version ultérieure est requis pour utiliser les fonctions de rendu côté serveur SPA comme décrit dans ce document.

## Présentation {#overview}

Les applications d’une seule page (SPA) peuvent offre à l’utilisateur une expérience riche et dynamique qui réagit et se comporte de manière familière, souvent comme une application native. [Pour ce faire, le client doit charger le contenu à l’avance, puis gérer l’interaction](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) utilisateur de manière intensive, ce qui réduit le volume de communication nécessaire entre le client et le serveur, ce qui rend l’application plus réactive.

Toutefois, cela peut entraîner des temps de chargement initiaux plus longs, en particulier si le SPA est volumineux et riche en contenu. Pour optimiser les temps de chargement, une partie du contenu peut être rendue côté serveur. L’utilisation du rendu côté serveur (SSR) peut accélérer le chargement initial de la page, puis transmettre le rendu au client.

## Quand utiliser SSR {#when-to-use-ssr}

SSR n&#39;est pas requis pour tous les projets. Bien qu’AEM prenne entièrement en charge JS SSR pour les applications monopages, Adobe ne recommande pas de les implémenter systématiquement pour chaque projet.

Lorsque vous décidez de mettre en oeuvre des SSR, vous devez d&#39;abord estimer la complexité, les efforts et les coûts supplémentaires associés à l&#39;ajout de SSR de façon réaliste pour le projet, y compris la maintenance à long terme. Une architecture SSR ne devrait être choisie que lorsque la valeur ajoutée dépasse clairement les coûts estimés.

Le SSR fournit habituellement une certaine valeur lorsqu&#39;il y a un &quot;oui&quot; clair à l&#39;une ou l&#39;autre des questions suivantes :

* **SEO :** Est-il toujours nécessaire d&#39;utiliser la SSR pour que votre site soit correctement indexé par les moteurs de recherche qui génèrent du trafic ? Gardez à l’esprit que les principaux moteurs de recherche évaluent désormais JS.
* **Vitesse de la page :** Est-ce que la SSR améliore la vitesse de façon mesurable dans les environnements réels et ajoute à l&#39;expérience globale de l&#39;utilisateur ?

Adobe recommande la mise en oeuvre de la solution SSR uniquement lorsque l’une de ces deux questions a reçu une réponse &quot;oui&quot; claire pour votre projet. Les sections suivantes décrivent comment effectuer cette opération à l’aide d’Adobe E/S Runtime.

## Adobe I/O Runtime {#adobe-i-o-runtime}

Si vous [pensez que votre projet nécessite la mise en oeuvre de SSR](/help/sites-developing/spa-ssr.md#when-to-use-ssr), la solution recommandée par Adobe est d’utiliser l’exécution d’E/S d’Adobe.

Pour plus d’informations sur Adobe E/S Runtime, voir

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html) - pour une présentation du service
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) - pour obtenir une documentation détaillée sur la plateforme

Les sections suivantes décrivent comment Adobe I/O Runtime peut être utilisé pour implémenter la technologie SSR pour votre application d’une seule page dans deux modèles différents :

* [Flux de communication piloté par AEM](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Flux de communication Adobe E/S piloté par l’exécution](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe recommande une instance d’exécution des E/S Adobe distincte pour chaque environnement AEM (auteur, publication, étape, etc.).

## Configuration du rendu à distance {#remote-renderer-configuration}

AEM doit savoir où le contenu rendu à distance peut être récupéré. Quel que soit [le modèle que vous choisissiez d’implémenter pour SSR,](#adobe-i-o-runtime) vous devrez indiquer à AEM comment accéder à ce service de rendu à distance.

Ceci est effectué via le service **OSGi** RemoteContentRenderer - Configuration Factory. Recherchez la chaîne &quot;RemoteContentRenderer&quot; dans la console de configuration de la console Web à `http://<host>:<port>/system/console/configMgr`.

![Configuration du moteur de rendu](assets/rendererconfig.png)

Les champs suivants sont disponibles pour la configuration :

* **Modèle** de chemin de contenu - expression régulière afin de correspondre à une partie du contenu, si nécessaire
* **URL** du point de terminaison distant - URL du point de terminaison responsable de la génération du contenu
   * Utilisez le protocole HTTPS sécurisé si ce n&#39;est pas sur le réseau local.
* **En-têtes** de demande supplémentaires - En-têtes supplémentaires à ajouter à la demande envoyée au point de terminaison distant
   * Modèle: `key=value`
* **Délai d’expiration** de la demande - Délai d’expiration de la demande d’hôte distant en millisecondes

>[!NOTE]
>
>Que vous choisissiez d’implémenter le flux [de communication](#aem-driven-communication-flow) AEM ou le flux d’exécution d’E/S [Adobe,](#adobe-i-o-runtime-driven-communication-flow) vous devez définir une configuration de rendu de contenu distant.
>
>Cette configuration doit également être définie si vous choisissez d’ [utiliser un serveur Node.js personnalisé.](#using-node-js)

>[!NOTE]
>
>Cette configuration exploite le [Remote Content Renderer,](#remote-content-renderer) qui offre des options d’extension et de personnalisation supplémentaires.

## Flux de communication piloté par AEM {#aem-driven-communication-flow}

Lors de l’utilisation de la technologie SSR, le processus [d’interaction des](/help/sites-developing/spa-overview.md#workflow) composants des applications monopages dans AEM inclut une phase au cours de laquelle le contenu initial de l’application est généré sur l’exécution des E/S d’Adobe.

1. Le navigateur demande le contenu SSR à AEM.

1. AEM publie le modèle sur Adobe E/S Runtime.

1. L’exécution d’E/S d’Adobe renvoie le contenu généré.

1. AEM diffuse le code HTML renvoyé par Adobe I/O Runtime via le modèle HTL du composant de page d’arrière-plan.

![rendu côté serveur-cms-drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Flux de communication Adobe E/S piloté par l’exécution {#adobe-i-o-runtime-driven-communication-flow}

La section précédente décrit l’implémentation standard et recommandée du rendu côté serveur en ce qui concerne les applications monopages dans AEM, où AEM effectue l’amorçage et la diffusion de contenu.

Une autre solution consiste à mettre en oeuvre la technologie SSR de sorte qu’Adobe E/S Runtime soit responsable de l’amorçage et que le flux de communication soit inversé.

Les deux modèles sont valides et pris en charge par AEM. Toutefois, il faut tenir compte des avantages et des inconvénients de chacun avant de mettre en oeuvre un modèle particulier.

<table>
 <tbody>
  <tr>
   <th><strong>Démarrage</strong></th>
   <th><strong>Avantages</strong></th>
   <th><strong>Inconvénients</strong></th>
  </tr>
  <tr>
   <th><strong>via AEM</strong><br /> </th>
   <td>
    <ul>
     <li>AEM gère les bibliothèques d’injection si nécessaire</li>
     <li>Les ressources doivent uniquement être conservées sur AEM.<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Peut-être pas familier avec les développeurs d’applications monopages<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>via Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>Plus familier aux développeurs d’applications monopages<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Les ressources de bibliothèque cliente requises par l’application, telles que CSS et JavaScript, devront être rendues disponibles par le développeur AEM via la <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code> propriété<br /> </li>
     <li>Les ressources doivent être synchronisées entre AEM et Adobe E/S Runtime<br /> </li>
     <li>Pour activer la création de l’application d’une seule page, un serveur proxy pour l’exécution des E/S d’Adobe peut s’avérer nécessaire.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Planification de la SSR {#planning-for-ssr}

En règle générale, seule une partie d’une application doit être rendue côté serveur. L’exemple courant est le contenu qui s’affichera au-dessus du pli lors du chargement initial de la page est rendu côté serveur. Cela permet de gagner du temps en fournissant au client du contenu déjà rendu. Lorsque l’utilisateur interagit avec l’application d’une seule page, le contenu supplémentaire est rendu par le client.

Lorsque vous envisagez d’implémenter le rendu côté serveur pour votre application monopage, vous devez vérifier quelles parties de l’application seront nécessaires.

## Développement d’une application d’une seule page à l’aide d’une SSR {#developing-an-spa-using-ssr}

Les composants SPA peuvent être rendus par le client (dans le navigateur) ou côté serveur. Lorsqu’il est rendu côté serveur, les propriétés du navigateur telles que la taille de la fenêtre et l’emplacement ne sont pas présentes. Par conséquent, les composants de l&#39;APS doivent être isomorphiques, sans présumer de l&#39;endroit où ils seront rendus.

Pour utiliser la technologie SSR, vous devez déployer votre code dans AEM ainsi que sur Adobe I/O Runtime, qui est responsable du rendu côté serveur. La plupart du code sera identique, mais les tâches spécifiques au serveur seront différentes.

## SSR pour les applications monopages dans AEM {#ssr-for-spas-in-aem}

La SSR pour les applications monopages dans AEM nécessite l’exécution des E/S d’Adobe, qui est appelée pour le rendu côté serveur de contenu d’application. Dans le fichier HTL de l’application, une ressource sur l’exécution des E/S d’Adobe est appelée pour générer le contenu.

Tout comme AEM prend en charge les infrastructures d’application d’une seule page, le rendu côté serveur est également pris en charge pour les applications Angular et React. Pour plus d&#39;informations, consultez la documentation du mécanisme national de prévention pour les deux cadres.

* Réagir : [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* Angular : [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

Pour un exemple simpliste, reportez-vous à l&#39;application [Journal](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)We.Retail. Il rend l’intégralité du côté serveur d’applications. Bien qu&#39;il ne s&#39;agisse pas d&#39;un exemple concret, il illustre bien ce qui est nécessaire pour mettre en oeuvre la RSS.

>[!CAUTION]
>
>L’application [de Journal](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) We.Retail est utilisée à des fins de démonstration uniquement et utilise donc Node.js comme exemple simple au lieu de l’exécution d’E/S Adobe recommandée. Cet exemple ne doit être utilisé pour aucun travail de projet.

>[!NOTE]
>
>Tout projet AEM doit tirer parti de l’archétype [du projet](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)AEM, qui prend en charge les projets d’application d’une seule page à l’aide de React ou d’Angular et exploite le SDK de l’application d’une seule page.

## Utilisation de Node.js {#using-node-js}

Adobe I/O Runtime est la solution recommandée pour l’implémentation de SSR pour les applications monopages dans AEM.

Pour les instances AEM sur mesure, il est également possible d’implémenter une SSR à l’aide d’une instance Node.js personnalisée de la même manière que décrit ci-dessus. Bien qu’elle soit prise en charge par Adobe, elle n’est pas recommandée.

>[!NOTE]
>
>Node.js n’est pas pris en charge pour les instances AEM hébergées par Adobe.

>[!NOTE]
>
>Si SSR doit être implémenté via Node.js, Adobe recommande une instance distincte de Node.js pour chaque environnement AEM (auteur, publication, étape, etc.).

## Rendu de contenu distant {#remote-content-renderer}

La configuration [de Rendu de contenu](#remote-content-renderer-configuration) distant requise pour utiliser SSR avec votre application d’une seule page dans AEM permet d’exploiter un service de rendu plus généralisé qui peut être étendu et personnalisé pour répondre à vos besoins.

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` est un service OSGi permettant de récupérer le contenu rendu sur un serveur distant, par exemple à partir des E/S Adobe. Le contenu envoyé au serveur distant est basé sur le paramètre de requête transmis.

`RemoteContentRenderingService` peut être injecté par inversion de dépendance dans un modèle Sling personnalisé ou une servlet lorsque des manipulations de contenu supplémentaires sont requises.

Ce service est utilisé en interne par la servlet [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

Il `RemoteContentRendererRequestHandlerServlet` peut être utilisé pour définir par programmation la configuration de la requête. `DefaultRemoteContentRendererRequestHandlerImpl`, l’implémentation du gestionnaire de requêtes par défaut fournie vous permet de créer plusieurs configurations OSGi afin de mapper un emplacement dans la structure de contenu à un point de terminaison distant.

Pour ajouter un gestionnaire de requêtes personnalisé, implémentez l’ `RemoteContentRendererRequestHandler` interface. Veillez à définir la propriété `Constants.SERVICE_RANKING` du composant sur un nombre entier supérieur à 100, qui correspond au classement du `DefaultRemoteContentRendererRequestHandlerImpl`.

```
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### Configuration d’OSGi du gestionnaire par défaut {#configure-default-handler}

La configuration du gestionnaire par défaut doit être configurée comme décrit dans la section Configuration [du rendu de contenu](#remote-content-renderer-configuration)distant.

### Utilisation du rendu de contenu distant {#usage}

Pour qu’une servlet récupère et renvoie du contenu qui peut être injecté dans la page :

1. Assurez-vous que votre serveur distant est accessible.
1. Ajouter l’un des fragments de code suivants au modèle HTML d’un composant AEM.
1. Vous pouvez éventuellement créer ou modifier les configurations OSGi.
1. Parcourir le contenu de votre site

En général, le modèle HTML d’un composant de page est le principal destinataire d’une telle fonctionnalité.

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### Conditions requises {#requirements}

Les servlets tirent parti de Sling Model Exporter pour sérialiser les données du composant. Par défaut, les cartes `com.adobe.cq.export.json.ContainerExporter` et `com.adobe.cq.export.json.ComponentExporter` sont prises en charge en tant que cartes de modèle Sling. Si nécessaire, vous pouvez ajouter des classes que la requête doit être adaptée pour utiliser la `RemoteContentRendererServlet` et mettre en oeuvre la `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. Les classes supplémentaires doivent étendre le `ComponentExporter`.
