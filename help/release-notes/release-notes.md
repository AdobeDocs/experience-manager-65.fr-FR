---
title: Notes de mise à jour de la version 6.5 d’ [!DNL Adobe Experience Manager]
description: Consultez les informations sur la mise à jour, y compris les nouveautés, la procédure d’installation et une liste complète des modifications pour  [!DNL Adobe Experience Manager]  6.5.
mini-toc-levels: 3
exl-id: fed4e110-9415-4740-aba1-75da522039a9
source-git-commit: 1077aeabacb1dbb489dbc7222c45da0a35b8cf16
workflow-type: tm+mt
source-wordcount: '3777'
ht-degree: 28%

---

# Notes de mise à jour du dernier pack de services [!DNL Adobe Experience Manager] 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=7yhrWb&nav=MTVfe0U0RjdDQUM3LTZCQ0EtNDk1Qy04Mjc1LTM2MUJEMzE1OEVGN30 -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, June 1, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## Informations sur la version {#release-information}

| Produit | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.17.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Type | Mise à jour du pack de services |
| Date | jeudi 25 mai 2023 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Éléments compris dans [!DNL Experience Manager] 6.5.17.0 {#what-is-included-in-aem-6517}

[!DNL Experience Manager] 6.5.17.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les clients, des correctifs de bogues, ainsi que des améliorations des performances, de la stabilité et de la sécurité, publiées depuis la version initiale de 6.5 en avril 2019. [Installez ce pack de services](#install) dans [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Certaines des fonctionnalités et améliorations clés de cette version sont les suivantes :

* **Améliorations de l’expérience de recherche** - Vous pouvez désormais effectuer rapidement les opérations suivantes sur les ressources qui s’affichent dans les résultats de recherche :
   * Créer un workflow
   * Création d’une version
   * Lier ou dissocier des ressources

  Vous n’avez pas besoin d’accéder à l’emplacement de la ressource et d’afficher ses propriétés pour effectuer ces opérations.
* **Dynamic Media _Instantané_**- Testez des images de test ou des URL Dynamic Media pour voir la sortie de différents modificateurs d’image et les optimisations de l’imagerie dynamique pour la taille de fichier (avec diffusion WebP et AVIF), la bande passante réseau et le rapport pixel du périphérique. Voir [Instantané Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html).
* **Diffusion DASH en continu avec Dynamic Media** - Nouvelle prise en charge du protocole (DASH - Dynamic Adaptive Streaming over HTTP) pour la diffusion en continu adaptative dans les diffusions vidéo Dynamic Media (avec CMAF activé). Disponible maintenant pour toutes les régions, [activé au moyen d’un ticket d’assistance](/help/assets/video.md#enable-dash-on-your-account-enable-dash).
* **Intégration de Experience Manager Sites et de fragments de contenu à Assets Next-Generation Dynamic Media** - Les utilisateurs d’Experience Manager Assets as a Cloud Service Next-Generation Dynamic Media peuvent désormais utiliser ces ressources hébergées dans le cloud pour la création et la diffusion avec des instances on-premise ou Managed Services de Experience Manager Sites 6.5.

**AEM Forms**

* **[Forms adaptatif dans AEM éditeur de page](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)**: Vous pouvez désormais utiliser AEM éditeur de page pour créer et ajouter rapidement plusieurs formulaires aux pages de vos sites. Cette fonctionnalité permet aux auteurs de contenu de créer des expériences de capture de données transparentes dans les pages Sites à l’aide de la puissance des composants de formulaires adaptatifs, notamment le comportement dynamique, les validations, l’intégration de données, la génération d’un document d’enregistrement et l’automatisation des processus d’entreprise. Vous pouvez :
   * Créez un formulaire adaptatif en faisant glisser les composants de formulaire vers le composant de conteneur de Forms adaptatif dans l’éditeur AEM Sites ou les fragments d’expérience.
   * Utilisez l’assistant de Forms adaptatif dans l’éditeur AEM Sites pour créer des formulaires indépendants de n’importe quelle page Sites, ce qui vous permet de réutiliser ces formulaires sur plusieurs pages.
   * Ajoutez plusieurs formulaires à une page Sites, en rationalisant l’expérience utilisateur et en offrant une plus grande flexibilité.
* **[Prise en charge de reCAPTCHA Enterprise dans Experience Manager Forms](/help/forms/using/captcha-adaptive-forms.md)**: Ajout de la prise en charge de reCAPTCHA Enterprise dans Experience Manager Forms, offrant une meilleure protection contre les activités frauduleuses et les spams, en plus de la prise en charge existante de Google reCAPTCHA v2.
* **[Prise en charge de Adobe Acrobat Sign pour les administrations avec Experience Manager Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md)**: AEM Forms s’intègre désormais à Adobe Acrobat Sign for Government (compatible avec FedRAMP). Cette intégration offre un niveau avancé de conformité et de sécurité pour les signatures électroniques avec les envois de formulaires adaptatifs pour les comptes associés au gouvernement (ministères et organismes gouvernementaux). L’intégration à Adobe Acrobat Sign for Government permet aux partenaires d’Adobe et aux clients gouvernementaux d’utiliser des signatures électroniques dans Adaptive Forms pour certains secteurs d’activité les plus critiques et les plus sensibles. Cette couche supplémentaire de sécurité garantit que toutes les signatures électroniques sont entièrement conformes à la conformité FedRAMP Modérate, offrant ainsi une certaine tranquillité d’esprit aux clients gouvernementaux de l’Adobe.
* **[Activation de l’intégration de Salesforce avec Experience Manager Forms pour l’échange de données](/help/forms/using/oauth2-client-credentials-flow-for-server-to-server-integration.md)**: Configurez l’intégration entre Experience Manager Forms et l’application Salesforce à l’aide du flux d’informations d’identification du client OAuth 2.0. Cette fonctionnalité permet une authentification et une autorisation sécurisées et directes de l’application et permet une communication transparente sans intervention de l’utilisateur.
* **Optimisation et fonctionnalité améliorée du moteur de workflow**: Augmentez les performances des moteurs de workflow en réduisant le nombre d’instances de workflow. En complément de `COMPLETED` et `RUNNING` valeurs d’état, le workflow prend également en charge trois nouvelles valeurs d’état : `ABORTED`, `SUSPENDED`, et `FAILED`.


<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets]{#assets-6517}

* Lorsque vous publiez plus de 40 PDF simultanément, [!DNL Experience Manager] arrête de répondre et devient indisponible pendant un certain temps. (ASSETS-21789)
* Si vous êtes connecté en tant qu’utilisateur test, vous ne pouvez pas voir les ressources liées à une ressource spécifique lorsque vous cliquez sur les propriétés d’une ressource. (ASSETS-21648)
* Lors de la modification de ressources à l’aide de `Desktop Actions`, si vous essayez d’archiver plus de cinq ressources à la fois, `Limit Reached` s’affiche et les ressources sélectionnées sont extraites. (ASSETS-21121)
* Impossible de trier les ressources par nom dans une collection. (ASSETS-20924)
* Impossible de définir des dimensions sur les ressources d’un type de format d’image. (ASSETS-20835)
* Le texte de l’info-bulle et son arrière-plan dans le champ Rechercher/ajouter une adresse électronique n’affichent pas le rapport de contraste approprié lors du partage d’un lien. (ASSETS-17347)
* Lorsque vous développez `Notifications`, le texte ne s’affiche pas correctement en raison de l’espacement des paragraphes. (ASSETS-17345)
* Lorsque vous copiez une ressource dans la collection, `Public Collection` ne s’affiche pas correctement. (ASSETS-17343)
* Les éléments utilisent des attributs ARIA sans rôle. (ASSETS-17325, ASSETS-17323)
* Le lien n’est pas descriptif lorsque vous développez `Notifications`. (ASSETS-17283)
* Lorsque vous naviguez et développez l’événement [!DNL Smart Crop] , le contenu apparaît comme une liste, mais il n’est pas marqué comme une liste non ordonnée. Par conséquent, le lecteur d’écran ne reconnaît pas la liste non ordonnée et la lit comme du texte brut. (ASSETS-17247)
* Le `Sort By` n’est pas associé à la liste déroulante correspondante. Par conséquent, le lecteur d’écran ne reconnaît pas les options de liste déroulante. (ASSETS-17239)
* Impossible d’avancer ou de reculer à l’aide de l’onglet du clavier ou des touches fléchées lorsque vous essayez d’ajouter un utilisateur à l’aide de la fonction `Add user` liste déroulante. (ASSETS-17233)
* Le lecteur d’écran ne transmet pas correctement les informations de l’étape Workflows (ASSETS-17285).
* Lorsque vous accédez à `Saved Searches` liste modifiable, les noms et les rôles ne sont associés à aucun libellé. (ASSETS-17329)
* Lorsque vous naviguez `Collection` et passez la souris sur le texte. *Membres*, le texte n’apparaît pas comme marqué. Par conséquent, le lecteur d’écran ne reconnaît pas le texte du titre et le lit comme du texte brut. (ASSETS-17245)
* Impossible d’accéder à `View Settings` à l’aide de la touche de défilement du clavier vers le bas ou vers le haut. (ASSETS-17257)
* Impossible de déclencher un workflow pour plusieurs ressources sélectionnées qui se trouvent à l’aide de filtres de recherche. (ASSETS-7689)
* Lorsque vous sélectionnez une ressource (ou plusieurs ressources) dans les résultats de recherche, l’option Mettre en relation ou Ne plus mettre en relation n’est pas visible. Mais cette option est disponible, sinon. (ASSETS-7679)
* Le panneau Filtres de recherche ne s’ouvre qu’une seule fois après la connexion et ne s’ouvre pas si vous quittez la page de recherche et réexécutez la recherche. (ASSETS-7671)
* La liste déroulante des emails n’affiche pas le rapport de contraste approprié lors du partage d’un lien. (ASSETS-17349)

<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST 
* When you select any file in a Collection and click `Download`, and then navigate to the email checkbox and expand it, regular text and email link is not recognizable due to background color. (ASSETS-17349) 
* When you navigate to `Smart Crop` option, the screen reader does not announce the expand or collapse state of the button. (ASSETS-17335)-->

## [!DNL Assets] - [!DNL Dynamic Media]{#dm-6517}

* La connexion à Dynamic Media est interrompue lorsqu’une configuration de cloud Dynamic Media existe déjà. (ASSETS-23057)
* Les performances accrues lors de la navigation dans des dossiers contenant de nombreuses vidéos Dynamic Media et résolus ne parviennent pas à charger le problème en mode Carte de dossiers. (ASSETS-23016)
* Les jetons d’aperçu sont supprimés de `error.log` qui peut être utilisé pour demander du contenu sécurisé auprès des serveurs de test sécurisés. (ASSETS-22685)
* Le rendu des miniatures de PDF ajoute une ombre. Mise à niveau de la bibliothèque Gibson version 4.0.1680232194 pour résoudre le problème de rendu des miniatures de PDF. (ASSETS-22585)
* Le mode hybride de Dynamic Media est désormais compatible avec la version 8.0.1 de l’agent New Relic (ASSETS-22578).
* Les listes de contrôle d’accès de Experience Manager (Access Control List) sont désormais respectées lors de la prévisualisation de fichiers Dynamic Media sur Experience Manager. (ASSETS-21628)
* Les lecteurs d’écran ne naviguent pas vers un élément masqué lorsque l’utilisateur tente de naviguer à l’aide de la touche Flèche vers le bas ou de la touche de tabulation. (ASSETS-5617)
* Interface utilisateur du profil d’image limitée pour les recadrages intelligents portant le même nom, la même dimension ou les deux. (ASSETS-16997)
* La largeur et la hauteur par défaut sont désormais définies sur 50 pixels pour les recadrages intelligents sur l’interface utilisateur du profil d’image. (ASSETS-16997)

## [!DNL Commerce]{#commerce-6517}

* Les balises déplacées sont nettoyées mais sont toujours référencées par les produits sous `/var`. (CQ-4351337)

## [!DNL Forms]{#forms-6517}

* Après la mise à jour vers AEM Service Pack 6.5.15.0, les formulaires HTML5 ne fonctionnent pas ou ne se chargent pas correctement dans le navigateur Edge avec le mode de compatibilité IE. (FORMS-8526, FORMS-8523)
* Lorsqu’un utilisateur applique AEM Service Pack 6.5.16.0, l’éditeur de règles ne s’ouvre pas. (FORMS-8290)
* Lorsque la validation du nombre maximal de chiffres est appliquée à un composant de zone numérique, elle échoue. (FORMS-7938)
* Lors de la création d’instructions de communication interactives, le composant de graphique dans le PDF n’est pas généré correctement. (FORMS-7827, FORMS-8297)
* Le nettoyage de la mémoire Java™ ne peut pas effacer l’ancien tas de génération sur un serveur OSGi Experience Manager Forms. (FORMS-8207)
* Lorsqu’un utilisateur effectue une mise à niveau vers le Service Pack Experience Manager 6.5.16.0, les propriétés de métadonnées CRX sont manquantes après envoi. (FORMS-8205)
* Lorsqu’un utilisateur désactive le composant Sélecteur de date dans un formulaire adaptatif, il est toujours modifiable. (FORMS-7804)
* Dans Experience Manager 6.5.16.0 Forms Service Pack, lorsqu’un utilisateur tente de modifier les coordinateurs de jeux de stratégies, le gestionnaire de l’éditeur de document reste toujours décoché. (FORMS-7775, FORMS-8599)
* Lorsqu’un utilisateur effectue une mise à niveau vers le Service Pack Experience Manager 6.5.16.0, la méthode &quot;GuideNode.externalize&quot;, qui gère les chaînes qui doivent être traduites, cesse de fonctionner. (FORMS-7709)
* Dans le `Assign task` , lorsqu’un utilisateur sélectionne l’option &quot;Envoyer un courrier électronique de notification&quot; et appelle le workflow, le texte ne s’affiche pas correctement dans l’email reçu. Les points d’interrogation sont reçus à la place du texte de l’e-mail reçu. (FORMS-7675)
* Le document d’enregistrement est partiellement localisé. (FORMS-7674, FORMS-7573)
* Un utilisateur ne peut pas modifier les jeux de stratégies, même s’il lui a attribué des autorisations spécifiques. (FORMS-7665)
* Lorsqu’un utilisateur dans la variable `forms-users` tente de créer un formulaire, l’instance Experience Manager Forms se bloque. (FORMS-7629)
* Lorsque l’utilisateur clique sur les boutons Réinitialiser, Enregistrer ou Envoyer d’un formulaire adaptatif, aucun message ne s’affiche à l’écran. (FORMS-7524)
* Pour améliorer les performances de la conversion PDFG sur un Service Pack Experience Manager 6.5.16.0, l’intervalle de sommeil est rendu configurable. (FORMS-6752)
* L’option de basculement reste la même, mais la visibilité du champ change même lorsqu’un utilisateur fait légèrement glisser le curseur. (FORMS-6728)
* Lorsque l’utilisateur effectue la mise à niveau vers le Service Pack Experience Manager 6.5.15.0, la redirection cesse de fonctionner lorsqu’un formulaire adaptatif est rendu dans Internet Explorer. (FORMS-6725)
* L’outil PAC 2021 pour tous les objets d’arrière-plan d’un formulaire de PDF créé par un concepteur de Experience Manager renvoie une erreur en tant que `Path object not tagged`. (FORMS-6707)
* Lorsqu’un utilisateur applique un filtre dans la boîte de réception, un événement `NullPointerException` erreur. (FORMS-6706)
* Lorsqu’un utilisateur importe un fichier de modèle (.tds) avec des fragments référencés, un Experience Manager Designer se bloque. (FORMS-6702)
* Si l’utilisateur crée un PDF statique à l’aide du service Output dans Experience Manager Forms Designer 6.5, une erreur se produit comme suit : `OCCD (optional content configuration dictionary) contains AS key`. (FORMS-6691)
* Lorsque l’utilisateur crée un workflow simple et ajoute une variable simple, une `set variable mapping` s’affiche. (FORMS-5819)
* Lorsqu’un utilisateur tente de générer un PDF à l’aide du service Output, même s’il est marqué comme `PDF/A-1a`, un contrôle de conformité à l’aide de la variable`Preflight` échoue. (LC-3920837)
* Après l’installation d’un Service Pack Experience Manager 6.5.16.0, un Concepteur de Experience Manager ne s’ouvre pas. (LC-3921000)
* Lorsqu’un utilisateur ajoute une case à cocher et un bouton radio, la structure d’une arborescence de balises n’est pas générée conformément aux normes du PDF. (LC-3920838)
* Si un utilisateur génère un PDF statique à l’aide de l’incorporation et du sous-paramétrage des polices via le service de sortie, le PDF obtenu contient uniquement les polices incorporées. (LC-3920963)
* Le texte en hébreu s’affiche incorrectement au format RTL. (LC-3919632)
* Lorsqu’un utilisateur effectue la mise à niveau vers le Service Pack Experience Manager 6.5.16.0 sur un serveur JBoss® clé en main, le service Signature ne parvient pas à appeler. L’erreur rencontrée est la suivante : `java.lang.ClassCastException: com.adobe.xfa.TextNode cannot be cast to com.adobe.xfa.Element`. (FORMS-7833)
* Après la mise à niveau vers le Service Pack Experience Manager 6.5.14.0, les processus de Workbench pour déplacer un noeud CRX d’un emplacement à un autre ne fonctionnent pas. L’erreur se produit comme suit : `ALC-CRX-30000-000: com.adobe.ep.crx.client.exceptions.CRCException: ALC-CRX-030-000-[Internal Server Error]`. (FORMS-7713)
* Lorsqu’un utilisateur effectue la mise à jour vers le Service Pack Experience Manager 6.5.16.0, la variable `Usage Rights` ne s’applique pas. (FORMS-7892)
* Lorsqu’un utilisateur tente de générer un document de PDF, la validation PDF/A-1b échoue. (FORMS-7615)
* Lorsqu’un utilisateur clique sur la variable `Configure` pour l’option `Form Container` , le navigateur ne répond plus. (FORMS-7605)
* Lorsqu’un utilisateur effectue la mise à jour vers Experience Manager Forms 6.5.16.0 Service Pack et tente de modifier la variable `LicenseType` to `Production`, les modifications ne sont pas reflétées. (FORMS-7594)
* Lorsqu’un utilisateur tente d’appeler un processus LCA avec un PDF qui comprend la variable `Chinese Full Width Characters`, un problème se produit avec la variable `ValidateForm` processus. (FORMS-7464)
* Dans Experience Manager Forms Designer, XMLFM génère une sortie ZPL avec des formats de papier différents, tels que Lettre, A4 et A5, pour les modèles basés sur XDP. (FORMS-7898)

## Intégrations{#integrations-6517}

* Lors de la conversion d’une configuration IMS Adobe Target en informations d’identification d’utilisateur dans les configurations cloud héritées, la variable `connectedWhen` ne change pas. Ce problème fait passer tous les appels comme si la configuration était toujours basée sur IMS. (CQ-4352810)
* Ajouter `modifyProperties` autorisation d’accès `fd-cloudservice` utilisateur système pour la configuration Adobe Sign. (FORMS-6164)
* Avec Experience Manager intégré à Adobe Target, lorsque vous créez une activité de test AB, elle ne synchronise pas les audiences qui lui sont associées, avec Target. (NPR-40085)

## Oak{#oak-6517}

Depuis le Service Pack 13 et les versions ultérieures, le journal d’erreur suivant a commencé à s’afficher, ce qui affecte le cache de persistance :

```shell
org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
    at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
    at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
    at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
    at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
    at org.h2.mvstore.db.Store.<init>(Store.java:129)
```

OU

```shell
org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
```

Pour résoudre cette exception, procédez comme suit :

1. Supprimez les deux dossiers suivants de `crx-quickstart/repository/`

   * `cache`
   * `diff-cache`

1. Installez le Service Pack ou redémarrez Experience Manager as a Cloud Service.
Nouveaux dossiers de `cache` et `diff-cache` sont automatiquement créés et vous ne voyez plus d’exception liée à `mvstore` dans le `error.log`.

## Plateforme{#platform-6517}

* Dans l’interface utilisateur de Experience Manager Tag Management (/aem/tags/), les espaces de noms et les balises s’affichent dans l’ordre dans lequel ils ont été créés. Cependant, lorsqu’il existe de nombreux espaces de noms et balises, la possibilité de les afficher et de les gérer est difficile. Ce problème est dû au fait qu’ils ne peuvent pas être triés d’une autre manière. (NPR-39620)
* La mise à jour de la version de fermeture de Google est nécessaire, car Minification js ne fonctionne pas pour certaines bibliothèques clientes. (NPR-40043)

## [!DNL Sites]{#sites-6517}

* Baisse des performances dans LinkCheckerTransformer. (SITES-11661)
* Les copies de langue d’une page n’étaient pas mises à jour comme prévu. (SITES-11191)
* Ouverture d’un appel de pages hors campagne `targeteditor.html` inutilement. Supprimez le `targeteditor` appelez lorsque cela n’est pas nécessaire. (SITES-12469)
* Les Live Copies ne peuvent pas être créées pour les pages avec des annotations. (SITES-12154)
* Le déploiement des pages ne fonctionne pas sur Experience Manager 6.5.16. (SITES-12008)
* Mémoire insuffisante; activité de nettoyage de la mémoire élevée en raison de `NotificationManagerImpl`. `NotificationManager` mise à niveau du lot vers Experience Manager 6.5. (SITES-11440)
* Correction des tests WCM IT qui bloquaient le service pack 17. (SITES-13089)
* La récupération des références Sites échoue sur le servlet. (SITES-10901)

### [!DNL Sites] - Interface utilisateur d’administration{#sites-adminui-6517}

* La fenêtre d’aperçu du sélecteur d’images miniatures ne peut pas être fermée. (SITES-10459)

### [!DNL Sites] - [!DNL Content Fragments]{#sites-contentfragments-6517}

* Configuration pour la connexion à l’objet de service Polaris (URL, informations d’identification, rappel, etc.). (SITES-12149)
* Utilisation de `SemanticDataType.REFERENCE` doit prendre en charge &quot;Remote-Asset-IDs&quot;. (SITES-12127)
* Intégrez le sélecteur de ressources Polaris à l’éditeur de fragment de contenu. (SITES-12125)
* Un en-tête http obligatoire était nécessaire pour accéder au point d’entrée du service de métadonnées. (SITES-13068)
* La mise en oeuvre GraphQL de la version 6.5 n’était pas conforme avec Cloud Service (Principal); les problèmes identifiés ont été corrigés. (SITES-13096)
* La pagination/le tri GraphQL et le filtrage hybride doivent être disponibles sur Experience Manager 6.5/AMS. (SITES-9154)

### [!DNL Sites] - Composants principaux{#sites-core-components-6517}

* La propriété `cq-msm-lockable` a une valeur de redirection incorrecte dans le composant de page Foundation. (SITES-10904)
* Le sélecteur de ressources distant redirige toujours vers l’environnement intermédiaire IMS. (SITES-13433)

### [!DNL Sites] - [!DNL Experience Fragments]{#sites-experiencefragments-6517}

* Lorsque vous sélectionnez une configuration Externalizer dans un fragment d’expérience lors de l’exportation vers Adobe Target, une URL externalisée incorrecte est envoyée. (SITES-12402)
* Supprimer les termes non inclusifs ; appliquez les directives relatives aux termes inclusifs. (SITES-11244)

### [!DNL Sites] - Éditeur de page{#sites-pageeditor-6517}

* Aucune miniature n’est affichée pour un ensemble de carrousel dans le rail latéral de l’outil de recherche de contenu du Experience Manager. (SITES-8593)

## Sling{#sling-6517}

* Sling `ResourceMerger` consomme une grande quantité de processeur lorsqu’il est fourni avec un chemin fictif, ce qui entraîne un déni de service. (NPR-40338)

## Projets de traduction{#translation-6517}

<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST * The `translationrules.xml` is sorted poorly when adding a rule to a property by way of the translation configuration user interface. (NPR-40431) -->
* La copie de langue n’est pas créée lorsque l’utilisateur ne configure pas de champs non obligatoires. (NPR-40036)

## Interface utilisateur{#ui-6517}

* Le bouton Annuler dans les propriétés de page est inactif ; vous devriez accéder à l’interface utilisateur Administration de sites . (NPR-40501)

<!-- ## WCM{#wcm-6517}

* TEXT -->

## Workflow{#workflow-6517}

* Modifications de la console Processus. (NPR-40502)
* `SegmentNotfound errors` dans les journaux d’une instance d’auteur de production, provoquée par le résolveur de ressources non fermé dans la classe . `com.day.cq.workflow.impl.email.EMailNotificationServic`. (NPR-40187)
* Une fermeture non fermée `ResourceResolver` l’exception est consignée. (ASSETS-22495)
* L’auteur Experience Manager se bloque lorsque PSD/PDF est énorme `DocumentAncestors` les attributs de métadonnées sont chargés. (ASSETS-22966)
* Fuite de session dans la classe `InboxSharingCache` avec `user-reader-service`. (CQ-4352513)
* La liste des utilisateurs et des groupes incomplète s’affiche lorsque l’étape &quot;Programme de sélection des participants de l’initiateur de workflow&quot; répertorie les utilisateurs et les groupes pour l’étape Participant. Ce problème se produisait lorsqu’un groupe était également membre d’un autre groupe. (NPR-40055)
* Purge améliorée des workflows. (NPR-40459)

## Installer [!DNL Experience Manager] 6.5.17.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.17.0 nécessite [!DNL Experience Manager] 6.5. Consultez la [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour des instructions détaillées. <!-- UPDATE FOR EACH NEW RELEASE -->
* Le téléchargement du Service Pack est disponible dans la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip) d’Adobe.
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez [!DNL Experience Manager] 6.5.17.0 sur l’une des instances de création à l’aide du gestionnaire de modules.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe ne recommande pas de supprimer ou de désinstaller le module [!DNL Experience Manager] 6.5.17.0. Par conséquent, avant d’installer le module, vous devez créer une sauvegarde de la variable `crx-repository` au cas où vous devriez le restaurer. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installation du pack de services sur [!DNL Experience Manager] 6.5{#install-service-pack}

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.

1. Avant l’installation, prenez un instantané ou exécutez une sauvegarde récente de votre instance [!DNL Experience Manager].

1. Téléchargez le pack de services à partir de la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.17.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Ouvrez le gestionnaire de modules et cliquez sur **[!UICONTROL Charger le module]** pour charger le module. Pour en savoir plus, consultez la section [Gestionnaire de modules](/help/sites-administering/package-manager.md).

1. Sélectionnez le module, puis sélectionnez **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du pack de services, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Consultez la section [Entrepôt de données S3 Amazon](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface utilisateur du gestionnaire de packages se ferme parfois pendant l’installation du pack de services. Adobe recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les logs spécifiques liés à la désinstallation de la mise à jour complète avant de vous assurer que les installations sont réussies. En règle générale, ce problème se produit dans [!DNL Safari] mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Vous pouvez utiliser deux méthodes différentes pour installer automatiquement [!DNL Experience Manager] 6.5.17.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.
* Utilisez l’[API HTTP à partir du gestionnaire de packages](/help/sites-administering/package-manager.md#package-share). Utilisez `cmd=install&recursive=true` afin que les packages imbriqués soient installés.

>[!NOTE]
>
>Experience Manager 6.5.17.0 ne prend pas en charge l’installation en Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validation de l’installation**

Pour connaître les plateformes certifiées pour travailler avec cette version, reportez-vous à la section des [exigences techniques](/help/sites-deploying/technical-requirements.md).

1. La page d’informations sur les produits (`/system/console/productinfo`) affiche la chaîne de version mise à jour `Adobe Experience Manager (6.5.17.0)` sous [!UICONTROL Produits installés]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Tous les lots OSGi sont au statut **[!UICONTROL ACTIF]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (utilisez la console web : `/system/console/bundles`).

1. Le bundle OSGi `org.apache.jackrabbit.oak-core` est de la version 1.22.15 ou ultérieure (utiliser la console Web : `/system/console/bundles`). <!-- NPR-40398 for 6.5.17.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installer le Service Pack sur [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Pour obtenir des instructions sur l’installation du Service Pack sur Experience Manager Forms, voir [Instructions d’installation du Service Pack Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### Installation du package d’index GraphQL pour les fragments de contenu Experience Manager{#install-aem-graphql-index-add-on-package}

Les clients qui utilisent GraphQL doivent installer la variable [Fragment de contenu Experience Manager avec package d’index GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Cela vous permet d’ajouter la définition d’index requise en fonction des fonctionnalités qu’ils utilisent réellement.

L’échec de l’installation de ce package peut entraîner des requêtes GraphQL lentes ou en échec.

>[!NOTE]
>
>N’installez ce package qu’une seule fois par instance ; il n’est pas nécessaire de le réinstaller avec chaque Service Pack.

### UberJar{#uber-jar}

UberJar pour [!DNL Experience Manager] 6.5.17.0 est disponible dans le [référentiel central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.17/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Pour utiliser UberJar dans un projet Maven, consultez la section [Utilisation d’UberJar](/help/sites-developing/ht-projects-maven.md) et incluez la dépendance suivante dans le POM de votre projet : <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.17</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar et les autres artefacts associés sont disponibles sur le référentiel central Maven au lieu du référentiel Maven public Adobe (`repo.adobe.com`). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Il n’existe donc pas de `classifier` avec `apis` comme valeur pour la balise `dependency`.

## Fonctionnalités obsolètes{#removed-deprecated-features}

Vous trouverez ci-dessous une liste des fonctionnalités signalées comme obsolètes par [!DNL Experience Manager] 6.5.7.0. Ces fonctionnalités sont initialement marquées comme obsolètes et supprimées ultérieurement dans une version future. Une option alternative est fournie.

Vérifiez si vous utilisez une de ces fonctionnalités dans un déploiement. Envisagez également de changer de mise en œuvre et d’utiliser une autre option.

| Domaine | Fonctionnalité | Remplacement |
|---|---|---|
| Intégrations | L’écran **[!UICONTROL Accord préalable des Experience Manager Cloud Services]** est obsolète, car la variable [!DNL Experience Manager] et [!DNL Adobe Target] l’intégration est mise à jour dans [!DNL Experience Manager] 6.5. L’intégration prend en charge l’API Adobe Target Standard. L’API utilise l’authentification au moyen d’Adobe IMS et d’[!DNL Adobe I/O Runtime]. Elle prend en charge le rôle croissant d’Adobe Launch pour utiliser les pages [!DNL Experience Manager] à des fins d’analyse et de personnalisation, l’assistant d’accord préalable n’a donc aucune utilité sur le plan fonctionnel. | Configurez des connexions système, l’authentification Adobe IMS et les intégrations d’[!DNL Adobe I/O Runtime] à l’aide des services cloud [!DNL Experience Manager] correspondants. |
| Connecteurs | Adobe JCR Connector for Microsoft® SharePoint 2010 et Microsoft® SharePoint 2013 est obsolète dans [!DNL Experience Manager] 6.5. | S/O |

## Problèmes connus{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* Mettez à jour vos requêtes GraphQL qui peuvent avoir utilisé un nom d’API personnalisé pour votre modèle de contenu afin d’utiliser plutôt le nom par défaut du modèle de contenu.

* Une requête GraphQL peut utiliser la variable `damAssetLucene` plutôt que l’index `fragments` index. Cette action peut entraîner l’échec des requêtes GraphQL ou un long délai d’exécution.

  Pour résoudre le problème, `damAssetLucene` doit être configuré pour inclure les deux propriétés suivantes :

   * `contentFragment`
   * `model`

  Une fois la définition d’index modifiée, une réindexation est requise (`reindex` = `true`).

  Après ces étapes, les requêtes GraphQL doivent être plus rapides.

* [!DNL Microsoft® Windows Server 2019] ne prend pas en charge [!DNL MySQL 5.7] et [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] ne prend donc pas en charge les installations clé en main pour [!DNL Experience Manager Forms 6.5.10.0].

* Si vous mettez à niveau votre instance [!DNL Experience Manager] de 6.5.0 à 6.5.4, jusqu’au dernier Service Pack sur Java™ 11, les exceptions `RRD4JReporter` s’affichent dans le fichier `error.log`. Pour arrêter les exceptions, redémarrez votre instance d’[!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Les utilisateurs peuvent renommer un dossier dans une hiérarchie dans [!DNL Assets] et publier un dossier imbriqué dans [!DNL Brand Portal]. Toutefois, le titre du dossier n’est pas mis à jour dans [!DNL Brand Portal] jusqu’à ce que le dossier racine soit republié.

* Lorsqu’un utilisateur choisit de configurer un champ pour la première fois dans un formulaire adaptatif, l’option permettant d’enregistrer une configuration ne s’affiche pas dans l’explorateur de propriétés. Sélectionner un autre champ du formulaire adaptatif à configurer dans le même éditeur pour résoudre le problème.

* Les erreurs et messages d’avertissement suivants peuvent s’afficher lors de l’installation d’[!DNL Experience Manager] 6.5.x.x :
   * « Lorsque l’intégration d’Adobe Target est configurée dans [!DNL Experience Manager] à l’aide de l’API Target Standard (authentification IMS), l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. » Au lieu du type « Fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégat telles que SUM, MAX et MIN sont utilisées (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La zone réactive d’une image interactive de Dynamic Media n’est pas visible lors de la prévisualisation du fichier via la visionneuse de bannières modifiables.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : temporisation en attente de modification d’enregistrement pour terminer la désinscription.

* Lorsque vous tentez de déplacer, supprimer ou publier des fragments de contenu, des sites ou des pages, un problème se produit lorsque les références aux fragments de contenu sont récupérées, car la requête en arrière-plan échoue. En d’autres termes, la fonctionnalité ne fonctionne pas.
Pour garantir le bon fonctionnement de cette opération, vous devez ajouter les propriétés suivantes au nœud de définition d’index `/oak:index/damAssetLucene` (aucune réindexation n’est requise) :

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Sur la plateforme JBoss® 7.1.4, lorsque l’utilisateur installe Experience Manager 6.5.16.0 ou un Service Pack ultérieur, `adobe-livecycle-jboss.ear` échec du déploiement.
* Les versions de JDK supérieures à 1.8.0_281 ne sont pas prises en charge pour le serveur WebLogic JEE.
* À partir de la version 6.5.15 d’AEM, le moteur JavaScript Rhino fourni par la variable ```org.apache.servicemix.bundles.rhino``` Le lot a un nouveau comportement d’hébergement. Scripts qui utilisent le mode strict (```use strict;```) doivent déclarer correctement leurs variables, sinon elles ne seront pas exécutées, mais génèrent une erreur d’exécution.

## Bundles OSGi et modules de contenu inclus{#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les bundles OSGi et les modules de contenu inclus dans [!DNL Experience Manager] 6.5.17.0 : <!-- UPDATE FOR EACH NEW RELEASE -->

* [Liste des bundles OSGi inclus dans Experience Manager 6.5.17.0](/help/release-notes/assets/65170_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Liste des modules de contenu inclus dans Experience Manager 6.5.17.0](/help/release-notes/assets/65170_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites web à accès limité{#restricted-sites}

Ces sites Web sont disponibles uniquement pour les clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* [Contacter l’assistance clientèle Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=fr).

>[!MORELIKETHIS]
>
>* Page des produits [[!DNL Experience Manager] ](https://business.adobe.com/fr/products/experience-manager/adobe-experience-manager.html)
>* Documentation [[!DNL Experience Manager]  6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=fr)
>* [Abonnement aux mises à jour prioritaires de produits d’Adobe](https://www.adobe.com/subscription/priority-product-update.html)
