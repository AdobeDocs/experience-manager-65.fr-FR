---
title: Architecture de HTML5 forms
seo-title: Architecture of HTML5 forms
description: HTML5 forms est déployé sous la forme d’un package au sein de l’instance d’AEM intégrée et expose la fonctionnalité comme point de terminaison REST sur HTTP/S à l’aide de l’architecture Apache Sling RESTful.
seo-description: HTML5 forms is deployed as a package within the embedded AEM instance and exposes the functionality as REST end point over HTTP/S using RESTful Apache Sling architecture.
uuid: 7f515cea-1447-4fc7-82ba-17f2e3f9f80c
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a644978e-5736-4771-918a-dfefe350a4a1
docset: aem65
feature: Mobile Forms
exl-id: ed8349a1-f761-483f-9186-bf435899df7d
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 38%

---

# Architecture de HTML5 forms{#architecture-of-html-forms}

## Architecture {#architecture}

La fonctionnalité de formulaire HTML5 est déployée sous la forme d’un package au sein de l’instance AEM intégrée et est exposée sous la forme d’un point de terminaison REST sur HTTP/S à l’aide de l’[Architecture Apache Sling](https://sling.apache.org/) RESTful.

![02-aem-forms-architecture_large](assets/02-aem-forms-architecture_large.jpg)

### Utilisation de la structure Sling {#using-sling-framework}

[Apache Sling](https://sling.apache.org/) est centré sur la ressource. Elle utilise une URL de requête pour résoudre la ressource en premier. Chaque ressource comporte une **sling:resourceType** (ou **sling:resourceSuperType**). En fonction de cette propriété, de la méthode de requête et des propriétés de l’URL de requête, un script sling est ensuite sélectionné pour gérer la requête. Ce script sling peut être un JSP ou un servlet. Pour les formulaires HTML5, les nœuds de **Profil** agissent en tant que ressources sling et le **Rendu de profil** a le rôle du script sling qui gère la demande pour générer un formulaire pour périphériques mobiles avec un profil particulier. Un **Rendu de profil** est un JSP qui lit les paramètres depuis une requête et appelle le service Forms OSGi.

Pour plus d’informations sur les points de terminaison REST et les paramètres de demande, reportez-vous à [Générer un modèle de formulaire](/help/forms/using/rendering-form-template.md). 

Lorsqu’un utilisateur effectue une requête à partir d’un appareil client tel qu’un navigateur iOS ou Android™, Sling résout d’abord le noeud de profil en fonction de l’URL de requête. À partir de ce noeud de profil, il lit : **sling:resourceSuperType** et **sling:resourceType** pour déterminer tous les scripts disponibles pouvant gérer cette requête de rendu de formulaire. Il utilise ensuite les sélecteurs de requête Sling avec la méthode de requête pour identifier le script le mieux adapté au traitement de cette requête. Une fois que la requête atteint un JSP de rendu de profil, le JSP appelle le service Forms OSGi.

Pour plus d’informations sur la résolution du script sling, voir [AEM Aide-mémoire Sling](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr) ou [Décomposition de l’URL Apache Sling](https://sling.apache.org/documentation/the-sling-engine/url-decomposition.html).

#### Flux d’appel de traitement de formulaire standard {#typical-form-processing-call-flow}

Les formulaires HTML5 mettent en cache tous les objets intermédiaires requis pour traiter (rendu ou envoi) un formulaire à la première requête. Il ne met pas en cache les objets qui dépendent des données, car ces objets risquent de changer.

Mobile Form conserve deux niveaux différents de cache, le cache de prérendu et le cache de rendu. Le cache de prérendu contient tous les fragments et images d’un modèle résolu et le cache de rendu contient le contenu rendu tel que HTML.

![Processus HTML5 forms](assets/cacheworkflow.png)

Processus HTML5 forms

HTML5 forms ne met pas en cache les modèles avec des références d’images ou de fragments manquantes. Si HTML5 forms a besoin de plus de temps que d’habitude, alors vérifiez les journaux du serveur pour voir les références et avertissements manquants. Assurez-vous également que l’objet n’a pas encore atteint la taille maximale.

Le service Forms OSGi traite une requête en deux étapes :

* **Génération de mises en page et d’état de formulaire initial** : le service de rendu Forms OSGi appelle le composant Forms Cache pour déterminer si le formulaire a déjà été mis en cache et s’il n’a pas été invalidé. Si le formulaire est mis en cache et valide, il sert la sortie HTML du cache. Si le formulaire est invalidé, le service de rendu Forms OSGi génère la mise en page initiale du formulaire et l’état du formulaire au format XML. Ce fichier XML est transformé en mise en page de HTML et en état de formulaire JSON initial par le service Forms OSGi, puis mis en cache pour les demandes suivantes.
* **Formulaires préremplis** : pendant le rendu, si un utilisateur demande des formulaires avec des données préremplies, le service de rendu Forms OSGi appelle le conteneur de services de formulaires et génère un nouvel état de formulaire avec des données fusionnées. Cependant, comme la mise en page est déjà générée à l’étape ci-dessus, cet appel est plus rapide que le premier. Cet appel effectue uniquement la fusion de données et exécute les scripts sur les données.

S’il existe des mises à jour dans un formulaire ou tout autre actif utilisé à l’intérieur d’un formulaire, le composant de mise en cache du formulaire les détecte et le cache de ce formulaire en particulier est invalidé. Une fois le traitement terminé par le service Forms OSGi, le jsp du rendu de profil ajoute des références de bibliothèque JavaScript et des styles à ce formulaire et renvoie la réponse au client. Un serveur web type [Apache](https://httpd.apache.org/) peut être utilisé ici avec la compression par HTML activée. Un serveur web réduirait considérablement le temps de réponse, le trafic réseau et la durée nécessaire au trafic des données entre le serveur et le client.

Lorsqu’un utilisateur envoie le formulaire, le navigateur envoie l’état du formulaire au format JSON au [proxy de service d’envoi](../../forms/using/service-proxy.md), puis le proxy de service d’envoi génère un fichier XML avec les données provenant des fichiers JSON et envoie le fichier XML au point de terminaison d’envoi.

## Composants {#components}

Vous avez besoin du module complémentaire AEM Forms pour activer les formulaires HTML5. Pour plus d’informations sur l’installation du module complémentaire AEM Forms, voir [Installation et configuration d’AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

### Composants OSGi (adobe-lc-forms-core.jar) {#osgi-components-adobe-lc-forms-core-jar}

**Adobe XFA Forms Renderer (com.adobe.livecycle.adobe-lc-forms-core)** est le nom d’affichage du lot OSGi Forms HTML5 depuis la vue du lot de la console d’administration Felix (https://[host]:[port]/system/console/bundles).

Ce composant contient des composants OSGi pour le rendu, la gestion du cache et les paramètres de configuration.

#### Service Forms OSGi {#forms-osgi-service}

Ce service OSGi contient la logique permettant de générer un XDP en tant que HTML et gère l’envoi d’un formulaire pour générer des données XML. Ce service utilise le conteneur de services Forms. Le conteneur de services de formulaires appelle en interne le composant natif `XMLFormService.exe` qui effectue le traitement.

Si une requête de génération est reçue, ce composant appelle le conteneur de services de formulaires pour générer des informations de mise en page et d’état qui sont ensuite traitées afin de générer des états DOM de formulaires HTML et JSON.

Ce composant est également responsable de la génération de données XML à partir de l’état du formulaire envoyé JSON.

#### Composant du cache {#cache-component}

HTML5 forms utilise la mise en cache pour optimiser le débit et le temps de réponse. Vous pouvez configurer le niveau du service de cache pour affiner le compromis entre les performances et l’utilisation de l’espace.

<table>
 <tbody>
  <tr>
   <th>Stratégie de cache</th>
   <th>Description</th>
  </tr>
  <tr>
   <td>Aucune</td>
   <td>Ne pas mettre en cache les artefacts<br /> </td>
  </tr>
  <tr>
   <td>Conservatrice</td>
   <td>Seuls les artefacts intermédiaires générés avant le rendu du formulaire, tels que le modèle contenant des fragments et des images en ligne, sont mis en cache.</td>
  </tr>
  <tr>
   <td>Agressive</td>
   <td>Contenu du HTML rendu en cache<br /> Mettez en cache tous les artefacts mis en cache au niveau Conservateur.<br /> <strong>Remarque</strong>: Cette stratégie offre de meilleures performances, mais consomme plus de mémoire pour le stockage des artefacts mis en cache.</td>
  </tr>
 </tbody>
</table>

Les formulaires HTML5 effectuent la mise en cache en mémoire à l’aide de la stratégie LRU. Si la stratégie de cache est définie sur Aucun, le cache ne sera pas créé et les données de cache existantes, le cas échéant, seront effacées. Outre la stratégie de mise en cache, vous pouvez configurer la taille totale du cache en mémoire, ce qui peut aider à limiter la taille maximale du cache. S’il dépasse cette limite, il utilisera le mode LRU pour libérer les ressources du cache.

>[!NOTE]
>
>Le cache en mémoire n’est pas partagé entre les noeuds de la grappe.

#### Service de configuration {#configuration-service}

Le service de configuration permet d’affiner les paramètres de configuration et les paramètres de cache pour les formulaires HTML5.

Pour mettre à jour ces paramètres, accédez à la console d’administration CQ Felix (disponible à l’adresse https://&lt;&#39;[server]:[port]&#39;/system/console/configMgr), puis recherchez et sélectionnez Configuration Mobile Forms.

Vous pouvez configurer la taille du cache ou la désactiver à l’aide du service de configuration. Vous pouvez également activer le débogage à l’aide du paramètre Options de débogage . Vous trouverez plus d’informations sur le débogage des formulaires dans [Débogage des formulaires HTML5](/help/forms/using/debug.md).

### Composants d’exécution (adobe-lc-forms-runtime-pkg.zip) {#runtime-components-adobe-lc-forms-runtime-pkg-zip}

Le module d’exécution contient les bibliothèques côté client utilisées pour effectuer le rendu des formulaires de HTML.

**Composants importants disponibles dans le cadre du package Runtime :**

#### Moteur de script {#scripting-engine}

L’implémentation d’Adobe XFA prend en charge deux types de langage de script pour activer l’exécution de la logique définie par l’utilisateur dans les formulaires : JavaScript et FormCalc.

Le moteur de script de HTML Forms est écrit en JavaScript pour prendre en charge l’API de script XFA dans ces deux langages.

Au moment du rendu, le script FormCalc est traduit (et mis en cache) en JavaScript sur le serveur de manière transparente pour l’utilisateur ou le concepteur.

Ce moteur de script utilise certaines fonctionnalités d’ECMAScript5 comme Object.defineProperty. Le moteur et/ou la bibliothèque sont délivrés en tant que bibliothèques client CQ avec pour nom de catégorie **xfaforms.profile**.  L’**API FormBridge** est également fournie pour permettre aux portails ou applications externes d’interagir avec le formulaire. Avec FormBridge, une application externe peut masquer certains éléments, obtenir ou définir leurs valeurs ou modifier leurs attributs par programmation.

Pour plus d’informations, voir [Form Bridge](/help/forms/using/form-bridge-apis.md) article.

#### Moteur de mise en page {#layout-engine}

La mise en page et l’aspect visuel des formulaires HTML5 reposent sur les fonctionnalités SVG 1.1, jQuery, BackBone et CSS3. L’aspect initial d’un formulaire est généré et mis en cache sur le serveur. Le réglage de cette disposition initiale et toute modification incrémentielle supplémentaire de la disposition du formulaire sont gérés sur le client. Pour ce faire, le package d’exécution contient un moteur de mise en page écrit dans Javascript et basé sur jQuery/Backbone. Ce moteur gère tous les comportements dynamiques, tels que l’ajout/la suppression d’instances répétables, la mise en page évolutive d’objet. Ce moteur de mise en page effectue le rendu d’un formulaire page par page. L’utilisateur ne voit qu’une page au début, et la barre de défilement horizontale ne prend qu’une page en compte. Cependant, lorsqu’un utilisateur fait défiler l’écran vers le bas, la page suivante commence le rendu. Ce rendu page par page réduit le temps nécessaire au rendu de la première page dans un navigateur et améliore les performances perçues du formulaire. Ce moteur/cette bibliothèque fait partie de la bibliothèque cliente CQ avec le nom de catégorie. **xfaforms.profile**.

Le moteur de mise en page contient également un ensemble de widgets utilisés pour capturer la valeur des champs de formulaire d’un utilisateur. Ces widgets sont modélisés comme suit : [Widgets de l’interface utilisateur jQuery](https://api.jqueryui.com/jQuery.widget/) qui implémentent certains contrats supplémentaires pour travailler en toute transparence avec le moteur de mise en page.

Pour plus d’informations sur les widgets et les contrats correspondants, voir [Widgets personnalisés pour les formulaires HTML5](/help/forms/using/introduction-widgets.md).

#### Style {#styling}

Le style associé aux éléments HTML est ajouté soit en ligne, soit en fonction du bloc CSS intégré.  Certains styles courants et indépendants sur les formulaires font partie de la bibliothèque client CQ avec pour nom de catégorie xfaforms.profile.

Outre les propriétés de style par défaut, chaque élément de formulaire contient également certaines classes CSS en fonction du type d’élément, du nom et d’autres propriétés. À l’aide de ces classes, vous pouvez redéfinir le style des éléments en spécifiant leur propre CSS.

Pour plus d’informations sur le style et les classes par défaut, voir [Présentation des styles](/help/forms/using/css-styles.md).

#### Script côté serveur et services web {#server-side-script-and-web-services}

Tous les scripts marqués pour exécution sur le serveur ou pour appeler un service Web (quel que soit l’endroit où il est marqué pour exécution) s’exécutent toujours sur le serveur.

Le moteur de script client :

1. Effectue un appel synchrone au serveur transmettant l’état actuel du formulaire sous la forme de JSON
1. Exécute le script ou le service Web sur le serveur.
1. Génère un nouvel état JSON
1. Fusionne le nouvel état JSON sur le client lorsque la réponse est renvoyée.

#### Lots de ressources de localisation {#localization-resource-bundles}

Les formulaires HTML5 prennent en charge l’italien (it), l’espagnols (es), le portugais du Brésil (pt_BR), le chinois simplifié (zh_CN), le chinois traditionnel (zh_TW, prise en charge limitée uniquement), le coréen (ko_KR), l’anglais (en_US), le français (fr_FR), l’allemand (de_DE) et le japonais (ja). En fonction du jeu de paramètres régionaux reçus dans l’en-tête de requête, le lot de ressources correspondant est envoyé au client. Ce lot de ressources est ajouté au profil JSP sous la forme d’une bibliothèque cliente CQ sous le nom de catégorie **xfaforms.I18N**. Vous pouvez remplacer la logique du profil consistant à prendre les packages avec paramètres régionaux.

### Composants Sling (adobe-lc-forms-content-pkg.zip) {#sling-components-adobe-lc-forms-content-pkg-zip}

Le package Sling contient du contenu relatif aux profils et au rendu de profil.

#### Profils {#profiles}

Les profils sont les noeuds de ressource dans sling qui représentent un formulaire ou une famille de Forms. Au niveau CQ, ces profils sont des noeuds JCR. Les noeuds se trouvent sous la propriété **/content** dans le référentiel JCR et peut se trouver dans n’importe quel sous-dossier sous **/content** dossier.

#### Rendus de profil {#profile-renderers}

Le noeud Profile possède une propriété . **sling:resourceSuperType** avec valeur **xfaforms/profile**. Cette propriété envoie en interne des demandes de transfert au script sling pour les nœuds de profil qui figurent dans le dossier **/libs/xfaforms/profile**. Ces scripts sont des pages JSP, qui sont des conteneurs permettant de rassembler les formulaires de HTML et les artefacts JS/CSS requis. Les pages contiennent des références à :

* **xfaforms.I18N.&lt;locale>**: Cette bibliothèque contient des données localisées.
* **xfaforms.profile**: Cette bibliothèque contient l’implémentation du moteur de script XFA et de mise en page.

Ces bibliothèques sont modélisées sous la forme de bibliothèques clientes CQ qui tirent parti des fonctionnalités de concaténation, minification et compression automatiques des bibliothèques JavaScript de la structure CQ.
Pour plus d’informations sur les bibliothèques clientes CQ, voir [Documentation sur les bibliothèques clientes CQ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr).

Comme décrit ci-dessus, le rendu de profil JSP appelle le service de formulaires grâce à une inclusion sling. Ce JSP définit également diverses options de débogage en fonction de la configuration de l’administrateur ou des paramètres de requête.

HTML5 forms permet aux développeurs de créer un profil et un rendu du profil pour personnaliser l’aspect des formulaires. Par exemple, les formulaires HTML permettent aux développeurs d’intégrer des formulaires dans un panneau ou une section &lt;div> d’un portail HTML existant.
Pour plus d’informations sur la création de profils personnalisés, reportez-vous à [Création d’un profil personnalisé](/help/forms/using/custom-profile.md).
