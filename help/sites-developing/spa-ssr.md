---
title: Rendu SPA et côté serveur
seo-title: Rendu SPA et côté serveur
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
workflow-type: tm+mt
source-wordcount: '1692'
ht-degree: 2%

---


# Rendu SPA et côté serveur{#spa-and-server-side-rendering}

>[!NOTE]
>
>L’éditeur SPA est la solution recommandée pour les projets qui nécessitent un rendu côté client SPA structure (par exemple, Réagir ou Angulaire).

>[!NOTE]
>
>aem version 6.5.1.0 ou ultérieure est requise pour utiliser les fonctions de rendu SPA côté serveur, comme décrit dans ce document.

## Présentation {#overview}

Les applications d’une seule page (SPA) peuvent offre à l’utilisateur une expérience riche et dynamique qui réagit et se comporte de manière familière, souvent tout comme une application native. [Pour ce faire, le client doit charger le contenu à l’avance, puis gérer l’](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) interaction des utilisateurs de manière intensive, ce qui réduit le volume de communication nécessaire entre le client et le serveur, ce qui rend l’application plus réactive.

Toutefois, cela peut entraîner des temps de chargement initiaux plus longs, en particulier si le SPA est volumineux et riche en contenu. Pour optimiser les temps de chargement, une partie du contenu peut être rendue côté serveur. L’utilisation du rendu côté serveur (SSR) peut accélérer le chargement initial de la page, puis transmettre le rendu au client.

## Quand utiliser SSR {#when-to-use-ssr}

SSR n&#39;est pas requis pour tous les projets. Bien que l&#39;Adobe AEM pleinement soutenir JS SSR pour SPA, il ne recommande pas de le mettre en oeuvre systématiquement pour chaque projet.

Lorsque vous décidez de mettre en oeuvre des SSR, vous devez d&#39;abord estimer la complexité, les efforts et les coûts supplémentaires associés à l&#39;ajout de SSR de façon réaliste pour le projet, y compris la maintenance à long terme. Une architecture SSR ne devrait être choisie que lorsque la valeur ajoutée dépasse clairement les coûts estimés.

Le SSR fournit habituellement une certaine valeur lorsqu&#39;il y a un &quot;oui&quot; clair à l&#39;une ou l&#39;autre des questions suivantes :

* **Optimisation du référencement :** La fonction SSR est-elle toujours nécessaire pour que votre site soit correctement indexé par les moteurs de recherche qui génèrent du trafic ? Gardez à l’esprit que les principaux moteurs de recherche évaluent désormais JS.
* **Vitesse de la page :** La SSR améliore-t-elle la vitesse de manière mesurable dans les environnements réels et ajoute-t-elle à l&#39;expérience globale de l&#39;utilisateur ?

Ce n&#39;est que lorsqu&#39;au moins l&#39;une de ces deux questions reçoit une réponse &quot;oui&quot; clair pour votre projet que l&#39;Adobe recommande la mise en oeuvre de la SSR. Les sections suivantes décrivent comment utiliser Adobe I/O Runtime.

## Adobe I/O Runtime {#adobe-i-o-runtime}

Si [vous êtes certain que votre projet nécessite l&#39;implémentation de SSR](/help/sites-developing/spa-ssr.md#when-to-use-ssr), la solution recommandée par l&#39;Adobe est d&#39;utiliser Adobe I/O Runtime.

Pour plus d’informations sur Adobe I/O Runtime, voir

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html) - pour un aperçu du service
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) - pour obtenir une documentation détaillée sur la plateforme

Les sections suivantes décrivent comment Adobe I/O Runtime peut être utilisé pour implémenter la technologie SSR pour votre SPA dans deux modèles différents :

* [Flux de communication AEM](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Flux de communication piloté par Adobe I/O Runtime](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe recommande une instance Adobe I/O Runtime distincte pour chaque environnement AEM (auteur, publication, étape, etc.).

## Configuration du rendu distant {#remote-renderer-configuration}

aem doit savoir où le contenu rendu à distance peut être récupéré. [quel que soit le modèle que vous choisissez d&#39;implémenter pour SSR,](#adobe-i-o-runtime) vous devez spécifier pour AEM comment accéder à ce service de rendu à distance.

Pour ce faire, utilisez le service **RemoteContentRenderer - Configuration Factory OSGi**. Recherchez la chaîne &quot;RemoteContentRenderer&quot; dans la console de configuration de la console Web à l&#39;adresse `http://<host>:<port>/system/console/configMgr`.

![Configuration du moteur de rendu](assets/rendererconfig.png)

Les champs suivants sont disponibles pour la configuration :

* **Modèle**  de chemin de contenu - expression régulière afin de correspondre à une partie du contenu, si nécessaire
* **URL**  de point de terminaison distant - URL du point de terminaison responsable de la génération du contenu
   * Utilisez le protocole HTTPS sécurisé si ce n&#39;est pas sur le réseau local.
* **En-têtes**  de demande supplémentaires - En-têtes supplémentaires à ajouter à la demande envoyée au point de terminaison distant
   * Modèle: `key=value`
* **Délai d’expiration**  de la demande - Délai d’expiration de la demande d’hôte distant en millisecondes

>[!NOTE]
>
>Que vous choisissiez d&#39;implémenter le [flux de communication AEM dirigé](#aem-driven-communication-flow) ou le [flux dirigé par Adobe I/O Runtime,](#adobe-i-o-runtime-driven-communication-flow), vous devez définir une configuration de rendu de contenu distant.
>
>Cette configuration doit également être définie si vous choisissez [d&#39;utiliser un serveur Node.js personnalisé.](#using-node-js)

>[!NOTE]
>
>Cette configuration exploite le [Remote Content Renderer,](#remote-content-renderer) qui dispose d&#39;options d&#39;extension et de personnalisation supplémentaires.

## Flux de communication dirigé par l&#39;AEM {#aem-driven-communication-flow}

Lors de l’utilisation de la technologie SSR, le processus d’interaction de composant [](/help/sites-developing/spa-overview.md#workflow) de SPA dans AEM inclut une phase au cours de laquelle le contenu initial de l’application est généré sur Adobe I/O Runtime.

1. Le navigateur demande le contenu de la SSR à AEM.

1. aem publie le modèle à Adobe I/O Runtime.

1. Adobe I/O Runtime renvoie le contenu généré.

1. aem diffuse le code HTML renvoyé par Adobe I/O Runtime via le modèle HTML du composant de page d’arrière-plan.

![rendu côté serveur-cms-drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Flux de communication piloté par Adobe I/O Runtime {#adobe-i-o-runtime-driven-communication-flow}

La section précédente décrit l’implémentation standard et recommandée du rendu côté serveur en ce qui concerne les SPA dans AEM, où l’AEM effectue l’amorçage et la diffusion du contenu.

Une autre solution consiste à mettre en oeuvre la SSR de sorte que Adobe I/O Runtime soit responsable de l&#39;amorçage, inversant ainsi le flux de communication.

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
     <li>aem gère les bibliothèques d’injection si nécessaire.</li>
     <li>Les ressources ne doivent être maintenues que sur AEM<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Peut-être pas familier au développeur SPA<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>via Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>Plus familier aux développeurs SPA<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Les ressources de bibliothèque cliente requises par l'application, telles que CSS et JavaScript, devront être rendues disponibles par le développeur AEM via la propriété <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code> <br />. </li>
     <li>Les ressources doivent être synchronisées entre AEM et Adobe I/O Runtime<br /> </li>
     <li>Pour activer la création du SPA, un serveur proxy pour Adobe I/O Runtime peut être nécessaire.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Planification de la RSS {#planning-for-ssr}

En règle générale, seule une partie d’une application doit être rendue côté serveur. L’exemple courant est le contenu qui s’affichera au-dessus du pli lors du chargement initial de la page est rendu côté serveur. Cela permet de gagner du temps en fournissant au client du contenu déjà rendu. Lorsque l’utilisateur interagit avec le SPA, le contenu supplémentaire est rendu par le client.

Lorsque vous envisagez d’implémenter le rendu côté serveur pour votre SPA, vous devez vérifier quelles parties de l’application seront nécessaires.

## Développement d&#39;un SPA à l&#39;aide de SSR {#developing-an-spa-using-ssr}

SPA composants peuvent être rendus par le client (dans le navigateur) ou côté serveur. Lorsqu’il est rendu côté serveur, les propriétés du navigateur telles que la taille de la fenêtre et l’emplacement ne sont pas présentes. Par conséquent, SPA composants doivent être isomorphiques, sans présumer de l&#39;endroit où ils seront rendus.

Pour utiliser la technologie SSR, vous devez déployer votre code dans AEM et sur Adobe I/O Runtime, qui est responsable du rendu côté serveur. La plupart du code sera identique, mais les tâches spécifiques au serveur seront différentes.

## SSR pour SPA en AEM {#ssr-for-spas-in-aem}

La fonction SSR pour SPA dans AEM nécessite Adobe I/O Runtime, qui est appelée pour le rendu du côté serveur de contenu d’application. Dans le fichier HTL de l’application, une ressource sur Adobe I/O Runtime est appelée pour générer le contenu.

Tout comme AEM prend en charge les structures de SPA Angular et React prêtes à l’emploi, le rendu côté serveur est également pris en charge pour les applications Angular et React. Pour plus d&#39;informations, consultez la documentation du mécanisme national de prévention pour les deux cadres.

* Réagir : [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* Angular : [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

Pour un exemple simpliste, reportez-vous à l&#39;[application de Journal We.Retail](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal). Il rend l’intégralité du côté serveur d’applications. Bien qu&#39;il ne s&#39;agisse pas d&#39;un exemple concret, il illustre bien ce qui est nécessaire pour mettre en oeuvre la RSS.

>[!CAUTION]
>
>L&#39;application de Journal [We.Retail](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) n&#39;est utilisée qu&#39;à des fins de démonstration et utilise donc Node.js comme exemple simple au lieu du Adobe I/O Runtime recommandé. Cet exemple ne doit être utilisé pour aucun travail de projet.

>[!NOTE]
>
>Tout projet AEM doit exploiter l’[archétype de projet AEM](https://docs.adobe.com/content/help/fr-FR/experience-manager-core-components/using/developing/archetype/overview.html), qui prend en charge les projets SPA à l’aide de React ou d’Angular et utilise le SDK SPA.

## Utilisation de Node.js {#using-node-js}

Adobe I/O Runtime est la solution recommandée pour la mise en oeuvre de la technologie SSR pour SPA en AEM.

Pour les instances d’AEM prédéfinie, il est également possible d’implémenter une SSR à l’aide d’une instance personnalisée de Node.js de la même manière que décrit ci-dessus. Bien que cet aspect soit pris en charge par l’Adobe, il n’est pas recommandé.

>[!NOTE]
>
>Node.js n’est pas pris en charge pour les instances d’AEM hébergées par Adobe.

>[!NOTE]
>
>Si SSR doit être implémenté via Node.js, l’Adobe recommande une instance distincte de Node.js pour chaque environnement AEM (auteur, publication, étape, etc.).

## Rendu de contenu distant {#remote-content-renderer}

La [configuration du rendu de contenu à distance](#remote-content-renderer-configuration) requise pour utiliser SSR avec votre SPA dans AEM permet d&#39;accéder à un service de rendu plus généralisé qui peut être étendu et personnalisé pour répondre à vos besoins.

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` est un service OSGi permettant de récupérer le contenu rendu sur un serveur distant, tel qu’Adobe I/O. Le contenu envoyé au serveur distant est basé sur le paramètre de requête transmis.

`RemoteContentRenderingService` peut être injecté par inversion de dépendance dans un modèle Sling personnalisé ou une servlet lorsque des manipulations de contenu supplémentaires sont requises.

Ce service est utilisé en interne par le [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

`RemoteContentRendererRequestHandlerServlet` peut être utilisé pour définir par programmation la configuration de la requête. `DefaultRemoteContentRendererRequestHandlerImpl`, l’implémentation du gestionnaire de requêtes par défaut fournie vous permet de créer plusieurs configurations OSGi afin de mapper un emplacement dans la structure de contenu à un point de terminaison distant.

Pour ajouter un gestionnaire de requêtes personnalisées, implémentez l&#39;interface `RemoteContentRendererRequestHandler`. Veillez à définir la propriété de composant `Constants.SERVICE_RANKING` sur un entier supérieur à 100, qui correspond au classement de `DefaultRemoteContentRendererRequestHandlerImpl`.

```
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### Configurez la configuration OSGi du gestionnaire par défaut {#configure-default-handler}

La configuration du gestionnaire par défaut doit être configurée comme décrit dans la section [Remote Content Renderer Configuration](#remote-content-renderer-configuration).

### Utilisation du rendu de contenu distant {#usage}

Pour qu’une servlet récupère et renvoie du contenu qui peut être injecté dans la page :

1. Assurez-vous que votre serveur distant est accessible.
1. Ajoutez l’un des fragments de code suivants sur le modèle HTML d’un composant AEM.
1. Vous pouvez éventuellement créer ou modifier les configurations OSGi.
1. Parcourir le contenu de votre site

En général, le modèle HTML d’un composant de page est le principal destinataire d’une telle fonctionnalité.

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### Conditions requises {#requirements}

Les servlets tirent parti de Sling Model Exporter pour sérialiser les données du composant. Par défaut, les cartes `com.adobe.cq.export.json.ContainerExporter` et `com.adobe.cq.export.json.ComponentExporter` sont prises en charge en tant que cartes de modèle Sling. Si nécessaire, vous pouvez ajouter des classes que la requête doit être adaptée pour utiliser `RemoteContentRendererServlet` et mettre en oeuvre `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. Les classes supplémentaires doivent étendre le `ComponentExporter`.
