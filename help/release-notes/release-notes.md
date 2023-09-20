---
title: Notes de mise à jour de la version 6.5 d’ [!DNL Adobe Experience Manager]
description: Consultez les informations sur la mise à jour, y compris les nouveautés, la procédure d’installation et une liste complète des modifications pour  [!DNL Adobe Experience Manager]  6.5.
mini-toc-levels: 4
source-git-commit: a15b9dae5cc4405122ee95e036a83fdfbf34f9bd
workflow-type: tm+mt
source-wordcount: '4490'
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
| Version | 6.5.18.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Type | Mise à jour du pack de services |
| Date | jeudi 24 août 2023 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## Éléments compris dans [!DNL Experience Manager] 6.5.18.0 {#what-is-included-in-aem-6518}

[!DNL Experience Manager] 6.5.18.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les clients, des correctifs de bogues, ainsi que des améliorations des performances, de la stabilité et de la sécurité, publiées depuis la version initiale de 6.5 en avril 2019. [Installez ce pack de services](#install) dans [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Voici quelques-unes des principales fonctionnalités et améliorations de cette version :

**Fonctions clés**

* Assets, Dynamic Media - [Prise en charge du suivi multititre et multiaudio pour les vidéos dans Dynamic Media](/help/assets/video.md#about-msma): vous pouvez désormais facilement ajouter plusieurs sous-titres et plusieurs pistes audio à une vidéo principale. Cette fonctionnalité signifie que vos vidéos sont accessibles à l’échelle mondiale. Vous pouvez personnaliser une seule vidéo principale publiée pour une audience globale dans plusieurs langues et respecter les directives d’accessibilité pour différentes régions géographiques. Les auteurs peuvent également gérer les sous-titres et les pistes audio à partir d’un seul onglet de l’interface utilisateur.

* Ressources : à partir des résultats de recherche, vous pouvez désormais accéder à l’emplacement du dossier contenant une ressource, ce qui vous permet d’effectuer diverses tâches de gestion des ressources. (ASSETS-23182)

**Principales améliorations**

* Le sélecteur Sélecteur de sites dans les fragments de contenu a amélioré les performances. (SITES-14092)

* Activation de l’utilisateur Éditeur de page/Composant d’image Sites pour référencer des ressources à partir du Cloud Service Ressources distant. (SITES-13448, SITES-13433)

* Pour trouver rapidement un projet en mode Liste où votre système peut contenir de nombreux projets, Adobe prend désormais en charge le tri côté serveur. Les noeuds de projet sont triés sur le serveur principal en fonction de la colonne sélectionnée par l’utilisateur avant d’être rendus dans l’interface utilisateur. (NPR-41027)

* AEM 6.5.18.0 prend en charge MongoDB 5.0 vers 6.0.

**Fonctionnalité obsolète**

* ActiveMQ dans AEM est obsolète. ActiveMQ a été utilisé pour la communication entre deux instances de publication AEM. Adobe recommande que les clients utilisent désormais un équilibreur de charge.

**Formulaires**

* **[Amélioration de la gestion des erreurs avec les gestionnaires d’erreurs personnalisés dans l’éditeur de règles](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html):** Vous pouvez désormais appeler une fonction personnalisée (à l’aide de la bibliothèque cliente) en réponse à une erreur renvoyée par un service externe et fournir une réponse personnalisée aux utilisateurs finaux. Vous pouvez également effectuer des actions spécifiques pour les erreurs renvoyées par un service. Par exemple, vous pouvez appeler un workflow personnalisé dans le serveur principal pour des codes d’erreur spécifiques ou informer le client que le service est hors service.

* **[Étape de processus Adobe Sign améliorée](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html#sign-document-step):** L’étape Processus Adobe Sign dans AEM Workflows est disponible avec les améliorations suivantes.

   * **Amélioration de la sécurité avec l’authentification par ID de gouvernement pour Adobe Sign :** Adobe Acrobat Sign Government ID-Based Authentication offre une couche supplémentaire de vérification en permettant aux utilisateurs d&#39;authentifier leur identité à l&#39;aide de cartes d&#39;identité délivrées par le gouvernement (permis de conduire, carte d&#39;identité nationale, passeport). Grâce à l’utilisation de documents d’identification approuvés, le processus de signature est plus confiant, ce qui le rend idéal pour les scénarios qui nécessitent une sécurité renforcée, une conformité accrue et une validation utilisateur plus poussée.

   * **Amélioration de la transparence avec le journal d’audit pour les documents Adobe Sign :** Utilisez la fonction Journal d’audit pour obtenir des informations détaillées sur le cycle de vie de vos documents Adobe Sign. Grâce au journal d’audit, vous pouvez désormais conserver un enregistrement complet de toutes les actions et interactions liées à vos documents. Cela inclut des détails tels que qui a consulté, modifié ou signé le document, ainsi que des horodatages pour chaque événement. Cette amélioration est essentielle pour maintenir la conformité, résoudre les litiges et assurer l’intégrité de vos accords numériques.


   * **Les rôles des destinataires du contrat ont été étendus au-delà du seul signataire :** Adobe Acrobat Sign a la possibilité d’étendre les rôles des destinataires du contrat au-delà du simple signataire afin de mieux répondre aux exigences de leur workflow. Lorsque cette option est activée, le rôle de chaque destinataire d’un contrat peut être configuré individuellement, le signataire étant la valeur par défaut.


* **[Programme d’installation complet d’AEM Forms on JEE](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms.html)**: le Service Pack apporte un programme d’installation complet pour AEM Forms on JEE qui prend en charge plusieurs nouvelles combinaisons de logiciels, notamment :
   * Microsoft® Windows Server 2022
   * Microsoft® Active Directory 2022
   * Oracle de WebLogic 14C sous Windows Server 2022
   * Red Hat® JBoss® 7.4.10
   * MongoDB 4.4
   * Connecteur JDBC MySQL 8

Si vous effectuez une nouvelle installation ou envisagez d’utiliser le dernier logiciel de votre environnement Forms on JEE AEM 6.5, Adobe recommande d’utiliser AEM programme d’installation complet d’Forms on JEE 6.5.18.0. Pour consulter la liste complète des logiciels nouvellement ajoutés et obsolètes, reportez-vous à la documentation d’AEM Forms on JEE ou d’AEM Forms on OSGi.

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## Correction de problèmes dans le Service Pack 18 {#fixed-issues}

### [!DNL Sites]{#sites-6518}

* Utilisation de l’éditeur en bloc pour mettre à jour les propriétés de plusieurs pages en téléchargeant la variable `tsv` Exportez, apportez des modifications hors ligne, puis chargez le `tsv` revenons à Experience Manager. Même si les pages ont été mises à jour, la propriété JCR `cq:lastModified` n’a pas été mis à jour et dans la chronologie. (SITES-14072)
* La référence de lien n’est pas mise à jour dans un fragment d’expérience lors de la création d’une Live Copy ou du déploiement d’un fragment d’expérience. (SITES-14759)
* Une action de synchronisation de workflow a été ajoutée à la configuration de déploiement standard du Experience Manager d’usine, la &quot;page de déploiement et les sous-pages&quot;, à partir de la page parente, et la tâche asynchrone échoue avec l’exception NullPointer . La page de l’emplacement source (en-us) n’existe pas dans le parent, mais existe à l’emplacement cible (Live Copy) (en). (SITES-12207)
* Vous avez une page &quot;en&quot; qui contient `jcr:description` et a envoyé la page pour traduction. La variable `jcr:description` est traduit et la propriété est présente sous launch. Toutefois, lorsque le lancement est promu, `jcr:description` n’est pas mis à jour dans la page. (SITES-13146)
* Le contenu localisé sur Live Copy est perdu après le déploiement du plan directeur. (SITES-12602)

#### Interface utilisateur d’administration{#sites-adminui-6518}

* Si l’autorisation de suppression d’un utilisateur est supprimée par le biais de la console d’administration des utilisateurs, l’utilisateur ne voit plus le bouton &quot;Propriétés&quot; dans la console sites.html (lors de la sélection de la page). Cependant, cette option est présente si l’utilisateur ouvre l’éditeur de page. (SITES-14341)
* Lorsqu’un dossier comporte de nombreuses pages, chacune comportant de nombreuses versions, lors de l’utilisation de la fonction de comparaison de versions, la charge sur l’instance devient élevée. Lorsque plusieurs utilisateurs utilisent la fonction en même temps, l’instance peut diminuer. (SITES-13026)

#### [!DNL Content Fragments]{#sites-contentfragments-6518}

* Un problème a été découvert lors de la gestion des exceptions dans la variable `RemoteAssetClientImpl`. Lorsqu’une exception IOException ou RuntimeException se produit lors de l’interrogation des métadonnées, le thread actuel tente de fermer et de recréer le httpClient partagé, ce qui peut entraîner une cascade d’autres erreurs dans les threads. (SITES-14092)
* Lorsque les auteurs remplissent le champ de l’éditeur de texte enrichi dans un fragment de contenu et insèrent une image dans un lien, lorsque le fragment de contenu est interrogé via l’API GraphQL, le message d’erreur s’affiche. `Exception while fetching data (/genericContentByPath) : null` est renvoyée. Cette erreur ne se produisait que si un lien contenait une image. La suppression de l’image du lien a fait disparaître le message d’erreur. (SITES-13988)
* La mise en oeuvre de GraphQL de Experience Manager 6.5 n’était pas comparable à celle du maître et plusieurs correctifs importants manquaient. (SITES-13096)
* Un en-tête HTTP obligatoire est nécessaire lors de l’accès au point de terminaison du service de métadonnées. (SITES-13068)

#### Composants principaux{#sites-core-components-6518}

* Le sélecteur de ressources ne récupère pas une liste de ressources mise à jour lorsqu’elle est fermée et rouverte. Si de nouvelles ressources sont chargées dans le référentiel, elles ne s’affichent pas dans le sélecteur de ressources tant que la page contenant le sélecteur de ressources n’est pas actualisée. (SITES-14828)
* L’interface utilisateur du sélecteur de ressources, intégrée à l’éditeur de sites (CS), ne répond pas lorsque la fenêtre est réduite. (SITES-14127)
* La configuration Adobe IMS (système Identity Management) pour l’intégration du sélecteur de ressources acceptait des valeurs incorrectes. (SITES-13962)
* Lorsqu’il est intégré au composant Image de sites , le sélecteur de ressources ne doit pas autoriser la sélection de ressources autres que des images. (SITES-13879)
* Une fois la connexion établie, l’utilisateur est redirigé vers l’éditeur de page. L’utilisateur doit rouvrir le sélecteur de ressources pour sélectionner Ressources distantes. (SITES-13851)
* Le sélecteur de ressources distant redirige toujours vers l’environnement intermédiaire Adobe IMS (système Identity Management). (SITES-13448, SITES-13433)

<!-- #### [!DNL Experience Fragments]{#sites-experiencefragments-6518}

* A -->

#### Éditeur de page{#sites-pageeditor-6518}

* Lorsque l’auteur ouvre les propriétés de page, la boîte de dialogue affiche une vue incorrecte. En d’autres termes, une barre de défilement horizontale supplémentaire et des marges supplémentaires sont visibles. (SITES-14502)
* Des styles ajoutés dans Experience Manager 6.5, Service Pack 17, pour l’ancre et la balise de corps provoquaient des problèmes CSS. Les balises d’ancrage ne s’affichaient pas soulignées dans l’auteur. (SITES-14261)

### [!DNL Assets]{#assets-6518}

* Le lecteur d’écran n’annonce pas l’état de développement ou de réduction de la variable [!UICONTROL Commencer recadrage] lors de la modification d’une ressource. (NPR-40593)
* Experience Manager affiche des messages d’erreur et d’avertissement lors du téléchargement d’une ressource sur l’instance AEM 6.5.17.0. (ASSETS-26232)
* Lorsque vous associez une ressource d’un dossier avec un accès complet à une ressource d’un dossier avec un accès en lecture seule, Experience Manager affiche un message d’erreur, tout en créant une relation partielle entre les deux ressources. (ASSETS-25832)
* Les ressources connectées ne fonctionnent pas entre une instance AMS et une instance de Cloud Service. (ASSETS-24930)
* Lors de la modification du Forms de schéma de métadonnées, les valeurs de [!UICONTROL Heure d’activation] et [!UICONTROL Heure de désactivation] ne sont pas enregistrés correctement. (ASSETS-24871)
* Lors de la génération du rapport Balises intelligentes pour les balises formées, les balises ayant un faible degré de confiance ne sont pas répertoriées. (ASSETS-24109)
* Experience Manager affiche un écran vide lors de la modification et de l’annotation d’une image en mode Colonne. (ASSETS-24108)
* Les lecteurs d’écran n’indiquent pas l’objectif du champ Ajouter un utilisateur lors de la création d’une collection. (ASSETS-21736)
* La variable **Collections** Le libellé n’est pas localisé sur la page des propriétés Collections. (ASSETS-21102)
* Lorsque vous ajoutez une règle ou modifiez une règle existante à l’aide du formulaire Schéma de métadonnées par défaut, les langues de la liste déroulante ne sont pas localisées. (ASSETS-21026)
* Experience Manager affiche un message d’erreur non localisé lors de l’ajout d’un chemin JSON dans le schéma de métadonnées. (ASSETS-21025)
* L’option de chronologie dans le volet de navigation de gauche n’affiche pas le rapport de contraste approprié. (ASSETS-17348)
* Les éléments du calendrier n’utilisent pas les attributs ARIA requis. (ASSETS-17282)
* Le texte de navigation de gauche n’affiche pas le rapport de contraste approprié. (ASSETS-17268)
* L’image Lightbox n’est pas masquée pour les utilisateurs de lecteurs d’écran. (ASSETS-17263, ASSETS-17242)
* L’état d’une interface utilisateur active ne fournit pas de rapport de contraste approprié concernant l’arrière-plan. (ASSETS-17260)
* Lors de l’annotation d’une ressource, le lecteur d’écran ne reconnaît pas le paramètre [!UICONTROL Enregistrer en tant que version] ou [!UICONTROL Démarrer le workflow] lors de leur navigation à l’aide des touches fléchées du clavier. (ASSETS-17253)
* Certains rôles ARIA ne contiennent pas les rôles enfants appropriés sur la page d’accueil Assets. (ASSETS-17248)
* Lorsque vous accédez aux options d’édition d’une ressource de type image à l’aide du clavier, la variable [!UICONTROL Lancer une Map] n’est pas reconnue et la sélection au clavier se fait sur le bouton Annuler . (ASSETS-17238)

#### [!DNL Dynamic Media]{#assets-dm-6518}

* Lorsque le téléchargement de la vidéo échoue, la vidéo n’est pas visible. Il affiche un écran vierge, tandis que la barre de défilement de la vidéo s’affiche en cours de progression. (ASSETS-21909)
* Le focus ne passe pas à plusieurs contrôles présents sous la vidéo lorsque vous naviguez à l’aide de la touche de tabulation du clavier. En tant que tels, ils ne sont pas accessibles. Navigation au clavier améliorée pour les vidéos interactives. (ASSETS-25749)
* Correction des paramètres prédéfinis de visionneuse désactivés qui s’affichaient dans le composant Dynamic Media. (ASSETS-22922)
* Suppression de &quot;Image Serving&quot; de l’onglet Sécurité des paramètres généraux . (ASSETS-24618)
* Correction de l’échec du chargement des ressources vers Dynamic Media et StringIndexOutOfBoundsException. (ASSETS-25787)
* Ajout d’un astérisque visuel pour le champ de modification &quot;largeur&quot; obligatoire dans l’onglet &quot;De base&quot;. (ASSETS-25741)
* Correction du téléchargement du rendu Dynamic Media du filigrane. (ASSETS-26173)
* Rétablissement de la limite de 127 caractères pour les noms de ressources non vidéo. (ASSETS-26074)

### [!DNL Forms]{#forms-6518}

<!-- Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.18.0 Forms add-on packages release is scheduled for Thursday, August 31, 2023. A list of Forms fixes and enhancements would be added to this section post the release. -->

* **Services de document**
   * Lorsqu’un utilisateur utilise un service transformPDF, celui-ci échoue avec une exception : `java.lang.ClassNotFoundException: default task-158Class name com.adobe.internal.afml.AFMLExceptionInvalidParameter from package com.adobe.internal.afml` (FORMS-9957)
   * Si le serveur est arrêté pendant la génération de documents PDF, des erreurs de traitement de tâche de démarrage après serveur sont générées. L’argument -Dcom.adobe.livecycle.dsc.deferServiceStart=true doit être ajouté au démarrage du serveur. (FORMS-9836)
   * Si un utilisateur tente de fusionner des PDF à l’aide de la méthode AssemblerService.Invoke , l’assembleur ne parvient pas à effectuer la tâche. (FORMS-9550)
   * Lorsque vous effectuez une mise à niveau vers AEM Service Pack 6.5.15.0 sur les environnements OSGI et JEE, le service Assembler utilisant un modèle spécifique cesse de fonctionner. (FORMS-9355, FORMS-9445, FORMS-9408)
   * Le nettoyage de la mémoire Java™ ne parvient pas à effacer le tas de l’ancienne génération sur un serveur AEM Forms OSGi, car le délai d’expiration global pour XMLFormService n’est pas configuré sur une valeur correcte. (FORMS-9384, FORMS-9035)
   * Lors du rendu de l’aperçu du PDF d’un formulaire adaptatif, les vidages de pile Java™ indésirables apparaissent dans les journaux d’erreurs. (FORMS-8865)
   * Lorsqu’un utilisateur consulte l’état du document pour les documents de la section des détails du document, il ne s’affiche pas correctement. (FORMS-8946, FORMS-10424)
   * Lorsqu’un utilisateur effectue une mise à niveau vers AEM Forms et utilise le service sendToPrinter, l’utilisation du tas ne cesse d’augmenter. (FORMS-10148)
   * Sur le serveur EAP JBoss® 7.4, la fonctionnalité de courrier électronique échoue avec `java.io.IOException`. (FORMS-10138)
   * Lorsqu’un utilisateur utilise le service transformPDF, il échoue avec une erreur : `java.lang.ClassNotFoundException: default task-158Class name com.adobe.internal.afml.AFMLExceptionInvalidParameter from package com.adobe.internal.afml`(FORMS-9957)
   * Après la mise à niveau vers AEM Service Pack 6.5.14.0, le problème survient dans le service Assembler lors de l’utilisation d’un modèle spécifique. (FORMS-9445, FORMS-9408)
  <!-- *  When a user configures the watched folder endpoint for PDF Generator, it fails to pick documents on JDK 11. (FORMS-10152) -->
* **Formulaires adaptatifs**
   * Lorsqu’un utilisateur tente d’appeler une fonction personnalisée sans modifier un champ, par exemple en définissant la valeur d’un autre champ, elle échoue. (FORMS-9921)
   * Lors de l’utilisation de la fonction d’erreur personnalisée pour l’éditeur de règles dans un formulaire adaptatif, les erreurs suivantes se produisent :
      * Lorsqu’un utilisateur tente d’utiliser @param{boolean} avec une fonction , l’éditeur de règles n’autorise pas la transmission de valeurs booléennes à une fonction.
      * Lorsqu’un utilisateur tente d’utiliser @param{string} avec une fonction , l’éditeur de règles ne transmet pas les valeurs facultatives et affiche un avertissement indiquant qu’il existe des règles incomplètes. (FORMS-9816, FORMS-9815)
   * Le groupe d’utilisateurs de formulaires ne parvient pas à appeler l’éditeur de règles deux fois dans un formulaire adaptatif. (FORMS-9051)
   * Dans un éditeur visuel, lorsqu’un utilisateur sélectionne un objet de formulaire, l’objet d’instance de champ entier est transmis à la fonction personnalisée au lieu de la seule valeur du champ. (FORMS-10015)
   * Lorsqu’un utilisateur crée un formulaire adaptatif basé sur des composants principaux et ajoute un composant de saisie de texte, `Is Empty` et `Is Not Empty` ne fonctionnent pas dans l’éditeur de règles. (FORMS-10098)
   * Si un champ est marqué comme non valide dans un formulaire adaptatif basé sur un composant principal, il déclenche un événement de modification sur le champ. (FORMS-10087)
   * Lorsqu’un utilisateur tente de créer un formulaire adaptatif à l’aide d’un schéma JSON complexe, il échoue. L’erreur se produit comme suit :
     `GET /content/forms/af/katezeroone/testaf1.html HTTP/1.1] com.adobe.aemds.guide.service.impl.JsonObjectCreatorImpl Could not emit JSON with context java.lang.ArrayIndexOutOfBoundsException:0`. (FORMS-9639)
   * Dans un formulaire adaptatif, lorsqu’un utilisateur désactive la case à cocher &quot;J’accepte les conditions générales&quot;, elle est de nouveau activée lorsque l’utilisateur fait défiler la page vers le bas. (FORMS-9458)
   * Lorsqu’un utilisateur ouvre un formulaire adaptatif sur un périphérique Android™ à l’aide de Google Chrome/Firefox et saisit le nombre maximal de caractères autorisés dans une zone de texte, la valeur de la zone de texte ne s’efface pas. (FORMS-9354)
   * Lorsque le libellé de la case à cocher comprend des caractères spéciaux tels que &#39;,&#39;, &#39;/&#39; ou &#39;.&#39;, le fait de cliquer sur le texte/le libellé ne coche pas la case correspondante. (FORMS-9313)
   * Lorsqu’un utilisateur tente de valider le composant Termes et conditions, il ne valide pas si le composant n’est pas ciblé alors que l’autre composant est validé. (FORMS-8725, FORMS-8913)
   * Si un formulaire adaptatif est rechargé après la mise à niveau vers AEM Service Pack 6.5.16.0, la récupération des pièces jointes échoue. (FORMS-8906)
   * Dans un formulaire adaptatif basé sur un formulaire XDP, si un composant de case à cocher comprend un titre de texte auquel une valeur numérique est affectée, le titre de texte est tronqué et ne correspond pas à la valeur affectée. (FORMS-8743)
   * Si un utilisateur tente d’implémenter un chargement différé sur un fragment incorporé dans un formulaire adaptatif pour l’environnement de création, les règles/logiques définies pour le fragment ne sont pas reflétées dans le formulaire. (FORMS-8554, FORMS-9182)
   * Lorsque vous essayez d’ouvrir une boîte de dialogue Coral dans AEM Service Pack 6.5.16.0, elle génère la variable `error.log: cannot render resource` exception. (FORMS-8942)
   * Lorsqu’un utilisateur tente de traduire une case à cocher avec une seule option dans un formulaire adaptatif, elle échoue. (FORMS-10181)
   * La publication de tous les modèles de document d’enregistrement (DoR) échoue. Seuls les modèles de document d’enregistrement basés sur des paramètres régionaux anglais et les modèles de document d’enregistrement Forms associés sont publiés. (FORMS-10535)

* **Accessibilité**
   * Lors de l’utilisation du composant Signature tactile dans un formulaire adaptatif, les erreurs suivantes se produisent :
      * Après le composant Scribble Signature, lorsqu’il existe d’autres composants, appuyer sur la touche de tabulation ne passe pas dans la boîte de dialogue de signature. Au lieu de cela, il passe au composant suivant. Ce n’est qu’après avoir parcouru tous les composants qu’il se déplace enfin vers la boîte de dialogue de signature.
      * Lorsqu’un utilisateur se connecte à la boîte de dialogue de signature à l’aide d’une touche ou d’un clavier, appuyer sur la touche Entrée ne ferme pas la boîte de dialogue.
      * La boîte de dialogue de confirmation de signature vide est inaccessible à l’aide du clavier.
      * Le lecteur d’écran ne parvient pas à lire les informations saisies dans une boîte de dialogue.
      * Il n’est pas possible d’effacer la signature sans l’aide d’une souris.  (FORMS-9317)
   * Lorsqu’un utilisateur envoie un formulaire adaptatif, le lecteur d’écran ne lit pas les messages d’erreur pour les champs obligatoires. (FORMS-9316)
   * Lorsqu’un lecteur d’écran lit un formulaire de HTML, le problème survient lors de la lecture du texte avec crénage (espacement). (FORMS-9258)
   * Dans un formulaire adaptatif, les références/notes de bas de page liées au texte ne sont pas appelées à l’aide du lecteur d’écran. (FORMS-8920)
   * Les balises d’accessibilité ne sont pas correctement reconnues dans le dernier Designer. (FORMS-10139)
* **Communications interactives**
   * Dans Correspondence Management, la localisation ne fonctionne pas. (FORMS-8926)
   * Le brouillon de lettre ne s’ouvre pas lorsque le service publishAll est utilisé. (FORMS-8589)
   * Après Experience Manager, le Service Pack 16 est installé sur les serveurs, toutes les lettres de communication interactive commencent à s’afficher si elles tentent de modifier ces lettres. S’ils fournissent un exemple de payload pour prévisualiser, afficher ou modifier la page des propriétés, ils fonctionnent. Toutefois, ils ne peuvent pas modifier les lettres. (FORMS-9067)


<!-- ### [!DNL Commerce]{#commerce-6518}

* A -->

### Foundation{#foundation-6518}

#### Distribution de contenu{#foundation-content-distribution-6518}

* La file d’attente de suppression des ressources ne doit pas être bloquée et aucune erreur ne doit se produire dans le fichier journal. (NPR-40570)

<!-- #### Integrations{#integrations-6518}

* A -->

<!-- #### Oak{#oak-6518}

* A -->

#### Plateforme{#foundation-platform-6518}

* Après l’installation d’un Experience Manager Vanilla, Service Pack 17, des erreurs s’affichent dans la variable `stderr.log`. Les installations Vanilla ne doivent pas générer d’erreurs. (CQ-4353637)
* Bouton Créer dans l’écran Balisage ne respectant pas la liste de contrôle d’accès (ACL). (NPR-40973)
* Impossible de créer, ou d’accéder, ou les deux, au noeud de cache de ContextHub sur Experience Manager. (NPR-40515)

#### Réplication{#foundation-replication-6518}

* La purge de réplication supprime tous les descendants du chemin d’accès demandé. (NPR-40569)

#### Sling{#foundation-sling-6518}

* Lorsqu’un rapport Partage de liens est généré, la colonne Lien ne contient pas les valeurs correctes. (NPR-40798)
* Avec AEM 6.5.15.0, toutes les URL de redirection vers un microsite, tous les alias sling et le mappage sling sont rompus après un redémarrage AEM. (NPR-40420)

#### Projets de traduction{#foundation-translation-6518}

* Traduction `rules.xml` triés de manière incorrecte lorsque des règles sont ajoutées à partir de l’interface utilisateur de configuration de traduction. (NPR-40431)
* Prise en charge des liens avec des paramètres de requête lors de la traduction. (NPR-40339)
* L’interface utilisateur du dictionnaire ne se charge pas pour le client après la mise à jour de la racine de contexte supplémentaire. (NPR-40650)
* Erreur lors de la création de copies de langue lorsque l’une des ressources est un fragment de contenu qui contient un champ multiple avec des types ReferenceFragment ou ContentFragment. (NPR-40892)

#### Interface utilisateur{#foundation-ui-6518}

* Comme décrit dans la section [Documentation du navigateur de configuration](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html?lang=en#using-configuration-browser), _Le nom devient le nom du noeud dans le référentiel._. Toutefois, dans l’explorateur de configurations, le titre de configuration est utilisé pour le chemin d’accès dans CRXDE Lite et le nom de la configuration est ignoré. (NPR-40607)

<!-- #### WCM{#wcm-6518}

* A -->

#### Workflow{#foundation-workflow-6518}

* La restauration d’une version de ressource conserve l’état de la ressource en mode de traitement. (NPR-41029)
* Problème de tri dans l’interface utilisateur Assets and Projects. Certains ont superposé les colonnes personnalisées sur l’interface utilisateur Assets and Projects en fonction des besoins de l’entreprise. Ils ont mis en oeuvre un tri à l’aide de la propriété d’usine `sortable=true`. Cependant, elles constatent des incohérences dans le tri lorsqu’il y a de nombreuses entrées dans l’interface utilisateur Projets ou Assets. (NPR-41027)
* Les journaux sont remplis `NullPointerException` dans le `EMailNotificationService`, et les emails, que les workflows doivent envoyer, ne sont pas envoyés. (NPR-40898)
<!-- REMOVED BY ENGINEERING FROM TOTAL RELEASE CANDIDATE LIST  * The timeline is not providing references to the selected content. (NPR-40806) -->

## Installer [!DNL Experience Manager] 6.5.18.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.18.0 nécessite [!DNL Experience Manager] 6.5. Consultez la [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour des instructions détaillées. <!-- UPDATE FOR EACH NEW RELEASE -->
* Le téléchargement du Pack de services est disponible dans la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip) d’Adobe.
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez [!DNL Experience Manager] 6.5.18.0 sur l’une des instances de création à l’aide du gestionnaire de modules.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe ne recommande pas de supprimer ou de désinstaller le package [!DNL Experience Manager] 6.5.18.0. Par conséquent, avant d’installer le module, vous devez créer une sauvegarde du `crx-repository` au cas où vous auriez besoin de le restaurer. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Installation du pack de services sur [!DNL Experience Manager] 6.5{#install-service-pack}

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.

1. Avant l’installation, prenez un instantané ou exécutez une sauvegarde récente de votre instance [!DNL Experience Manager].

1. Téléchargez le pack de services à partir de la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.18.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Ouvrez le gestionnaire de modules et cliquez sur **[!UICONTROL Charger le module]** pour charger le module. Pour en savoir plus, consultez la section [Gestionnaire de modules](/help/sites-administering/package-manager.md).

1. Sélectionnez le module, puis sélectionnez **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du pack de services, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Consultez la section [Entrepôt de données S3 Amazon](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface utilisateur du gestionnaire de packages se ferme parfois pendant l’installation du pack de services. Adobe recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les logs spécifiques liés à la désinstallation du lot de mise à jour avant de vous assurer que l’installation est réussie. En règle générale, ce problème se produit dans la variable [!DNL Safari] mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Vous pouvez utiliser deux méthodes différentes pour installer automatiquement [!DNL Experience Manager] 6.5.18.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.
* Utilisez l’[API HTTP à partir du gestionnaire de packages](/help/sites-administering/package-manager.md#package-share). Utilisez `cmd=install&recursive=true` afin que les packages imbriqués soient installés.

>[!NOTE]
>
>Experience Manager 6.5.18.0 ne prend pas en charge l’installation en Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validation de l’installation**

Pour connaître les plateformes certifiées pour travailler avec cette version, reportez-vous à la section des [exigences techniques](/help/sites-deploying/technical-requirements.md).

1. La page d’informations sur les produits (`/system/console/productinfo`) affiche la chaîne de version mise à jour `Adobe Experience Manager (6.5.18.0)` sous [!UICONTROL Produits installés]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Tous les lots OSGi sont au statut **[!UICONTROL ACTIF]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (utilisez la console web : `/system/console/bundles`).

1. L’offre groupée OSGi `org.apache.jackrabbit.oak-core` est de la version 1.22.16 ou ultérieure (utiliser la console web : `/system/console/bundles`). <!-- NPR-41010 for 6.5.18.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Installer le Pack de services pour [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Pour obtenir des instructions sur l’installation du Pack de services sur Experience Manager Forms, voir les [instructions d’installation du Pack de services Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### Installer le package d’index GraphQL pour les fragments de contenu d’Experience Manager{#install-aem-graphql-index-add-on-package}

La clientèle qui utilise GraphQL doit installer le [fragment de contenu d’Experience Manager avec le package d’index GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Vous pouvez ainsi ajouter la définition d’index requise selon les fonctionnalités que vous utilisez réellement.

L’échec de l’installation de ce package peut entraîner des requêtes GraphQL lentes ou en échec.

>[!NOTE]
>
>N’installez ce package qu’une seule fois par instance ; il n’est pas nécessaire de le réinstaller avec chaque Pack de services.

### UberJar{#uber-jar}

UberJar pour [!DNL Experience Manager] 6.5.18.0 est disponible dans le [référentiel central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.18/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

Pour utiliser UberJar dans un projet Maven, consultez la section [Utilisation d’UberJar](/help/sites-developing/ht-projects-maven.md) et incluez la dépendance suivante dans le POM de votre projet : <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.18</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar et les autres artefacts associés sont disponibles sur le référentiel central Maven au lieu du référentiel Maven public Adobe (`repo.adobe.com`). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Il n’existe donc pas de `classifier` avec `apis` comme valeur pour la balise `dependency`.

## Fonctionnalités obsolètes et supprimées{#removed-deprecated-features}

Voir [Fonctionnalités obsolètes et supprimées](/help/release-notes/deprecated-removed-features.md/).

## Problèmes connus{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* En rapport avec Oak à partir du Service Pack 13 et versions ultérieures, le journal d’erreur suivant a commencé à s’afficher, ce qui affecte le cache de persistance :

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  Ou

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  Pour résoudre cette exception, procédez comme suit :

   1. Supprimez les deux dossiers suivants de `crx-quickstart/repository/`.

      * `cache`
      * `diff-cache`

   1. Installez le Pack de services ou redémarrez Experience Manager as a Cloud Service.
Les nouveaux dossiers `cache` et `diff-cache` sont automatiquement créés et vous ne voyez plus d’exception liée à `mvstore` dans `error.log`.

* Mettez à jour vos requêtes GraphQL qui peuvent avoir utilisé un nom d’API personnalisé pour votre modèle de contenu afin d’utiliser plutôt le nom par défaut du modèle de contenu.

* Une requête GraphQL peut utiliser l’index `damAssetLucene` plutôt que l’index `fragments`. Il peut en résulter l’échec des requêtes GraphQL ou l’exécution de celles-ci peut prendre beaucoup de temps.

  Pour résoudre le problème, `damAssetLucene` doit être configuré pour inclure les deux propriétés suivantes :

   * `contentFragment`
   * `model`

  Une fois la définition d’index modifiée, une réindexation est nécessaire (`reindex` = `true`).

  Après ces étapes, les requêtes GraphQL doivent être plus rapides.

* Lorsque vous tentez de déplacer, de supprimer ou de publier des fragments de contenu, des sites ou des pages, un problème se produit lorsque les références aux fragments de contenu sont récupérées, car la requête en arrière-plan échoue. En d’autres termes, la fonctionnalité ne fonctionne pas.
Pour garantir le bon fonctionnement de cette opération, vous devez ajouter les propriétés suivantes au nœud de définition d’index `/oak:index/damAssetLucene` (aucune réindexation n’est requise) :

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Si vous mettez à niveau votre instance [!DNL Experience Manager] de 6.5.0 à 6.5.4, jusqu’au dernier Service Pack sur Java™ 11, les exceptions `RRD4JReporter` s’affichent dans le fichier `error.log`. Pour arrêter les exceptions, redémarrez votre instance d’[!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Les utilisateurs peuvent renommer un dossier dans une hiérarchie dans [!DNL Assets] et publier un dossier imbriqué dans [!DNL Brand Portal]. Toutefois, le titre du dossier n’est pas mis à jour dans [!DNL Brand Portal] jusqu’à ce que le dossier racine soit republié.

* Les erreurs et messages d&#39;avertissement suivants peuvent s&#39;afficher lors de l&#39;installation : [!DNL Experience Manager] 6.5.x.x :
   * « Lorsque l’intégration d’Adobe Target est configurée dans [!DNL Experience Manager] à l’aide de l’API Target Standard (authentification IMS), l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. » Au lieu du type « Fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
   * `com.adobe.granite.maintenance.impl.TaskScheduler` : aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégat telles que SUM, MAX et MIN sont utilisées (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La zone réactive d’une image interactive Dynamic Media n’est pas visible lors de la prévisualisation de la ressource via la visionneuse de bannières Shoppable.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : temporisation en attente de modification d’enregistrement pour terminer la désinscription.

* À partir de la version 6.5.15 d’AEM, le moteur JavaScript Rhino fourni par l’offre groupée ```org.apache.servicemix.bundles.rhino``` a un nouveau comportement d’hébergement. Scripts qui utilisent le mode strict (```use strict;```) doivent déclarer correctement leurs variables, sinon elles ne sont pas exécutées, mais génèrent une erreur d’exécution.

### Problèmes connus pour AEM Forms

#### Plateformes prises en charge

* Les versions de JDK supérieures à 1.8.0_281 ne sont pas prises en charge pour le serveur WebLogic JEE. (FORMS-8498, CQDOC-20383)
* [!DNL Microsoft®® Windows Server 2019] ne prend pas en charge [!DNL MySQL 5.7] et [!DNL JBoss®® EAP 7.1], [!DNL Microsoft®® Windows Server 2019] ne prend donc pas en charge les installations clé en main pour [!DNL Experience Manager Forms 6.5.10.0]. (CQDOC-18312)
* JDK 11.0.20 n’est pas pris en charge pour installer le programme d’installation d’AEM Forms on JEE. Seuls les JDK 11.0.19 ou les versions antérieures sont pris en charge pour installer le programme d’installation d’AEM Forms on JEE. (FORMS-10659)

#### Installation

* Sur la plateforme JBoss® 7.1.4, lorsque l’utilisateur ou l’utilisatrice installe le Pack de services Experience Manager 6.5.16.0, le déploiement de `adobe-livecycle-jboss.ear` échoue. (CQ-4351522, CQDOC-20159)
* Après l’installation du programme d’installation complet d’AEM Service Pack 6.5.18.0, le déploiement des fichiers EAR échoue sur JEE en utilisant JBoss® clé en main (CQDOC-20803).
Pour résoudre le problème, recherchez la variable `<AEM_Forms_Installation_dir>\jboss\bin\standalone.bat` fichier et mise à jour `Adobe_Adobe_JAVA_HOME` to `Adobe_JAVA_HOME` pour toutes les occurrences avant d’exécuter configuration manager.

#### Formulaires adaptatifs

* Lorsqu’un formulaire adaptatif est publié, toutes ses dépendances, y compris les stratégies, sont republiées, même si aucune modification ne leur a été apportée. (FORMS-10454)
* Lorsqu’un utilisateur choisit de configurer un champ pour la première fois dans un formulaire adaptatif, l’option permettant d’enregistrer une configuration ne s’affiche pas dans l’explorateur de propriétés. La sélection d’un autre champ du formulaire adaptatif dans le même éditeur résout le problème.
* Lorsqu’une URL de redirection est définie dans le conteneur de guide d’un formulaire adaptatif, la signature en ligne cesse de fonctionner. (FORMS-10493)
* La publication de tous les modèles de document d’enregistrement (DoR) échoue. Seuls les modèles de document d’enregistrement basés sur des paramètres régionaux anglais et les modèles de document d’enregistrement Forms associés sont publiés. (FORMS-10535)

#### Communications interactives

* Après la mise à niveau vers AEM Service Pack 18, il n’est pas possible de modifier les lettres de communication interactive. (FORMS-10578) Pour résoudre le problème, procédez comme suit :

   1. Télécharger [Correctif-FORMS-10578](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) à partir du lien SD.
   1. Extrayez le fichier d’archive Hotfix pour obtenir un package de Experience Manager (.zip) et des fichiers de bundle (.jar).
   1. Téléchargez et installez le package (.zip) via le gestionnaire de modules.
   1. Ouverture des lots Configuration Manager `https://server:host/system/console/bundles`, téléchargez et installez le lot (.jar).

## Bundles OSGi et modules de contenu inclus{#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les bundles OSGi et les modules de contenu inclus dans [!DNL Experience Manager] 6.5.18.0 : <!-- UPDATE FOR EACH NEW RELEASE -->

* [Liste des bundles OSGi inclus dans Experience Manager 6.5.18.0](/help/release-notes/assets/65180_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Liste des modules de contenu inclus dans Experience Manager 6.5.18.0](/help/release-notes/assets/65180_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites web à accès limité{#restricted-sites}

Ces sites Web sont disponibles uniquement pour les clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* [Contacter l’assistance clientèle Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=fr).

>[!MORELIKETHIS]
>
>* Page des produits [[!DNL Experience Manager] ](https://business.adobe.com/fr/products/experience-manager/adobe-experience-manager.html)
>* Documentation [[!DNL Experience Manager]  6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=fr)
>* [Abonnement aux mises à jour prioritaires de produits d’Adobe](https://www.adobe.com/subscription/priority-product-update.html)
