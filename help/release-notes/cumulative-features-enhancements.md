---
title: Principales fonctionnalités et améliorations cumulées dans la version 6.5 d’Adobe Experience Manager.
description: Liste cumulée des fonctionnalités et améliorations clés apportées à Adobe Experience Manager 6.5 à partir des huit versions précédentes du pack de services.
content-type: reference
docset: aem65
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 01fe5b53-2244-445f-a4d0-bd58ea38b611
solution: Experience Manager
source-git-commit: 03c070f7bba1d66ce2a5309d2ab79567dbef3264
workflow-type: tm+mt
source-wordcount: '3539'
ht-degree: 71%

---

# Principales fonctionnalités et améliorations cumulées

Liste cumulative des fonctionnalités et améliorations clés de Adobe Experience Manager 6.5 pour les versions précédentes du Service Pack.

Voir également les [Notes de mise à jour du dernier pack de services d’Adobe Experience Manager 6.5](/help/release-notes/release-notes.md)


## AEM 6.5 Service Pack 23 - 22 mai 2025

### Formulaires {#forms-sp23}

* [Hyperliens accessibles avec style de texte mixte dans les PDF statiques](https://helpx.adobe.com/content/dam/help/fr/experience-manager/6-5/forms/pdf/using-designer.pdf) : les hyperliens contenant des styles de texte mixte dans les PDF statiques sont désormais balisés en tant qu’élément accessible unique. Cette amélioration simplifie l’arborescence des balises, améliore la navigation dans le lecteur d’écran et permet une meilleure conformité en matière d’accessibilité.

* [Mise à jour de la matrice des plateformes prises en charge](/help/forms/using/aem-forms-jee-supported-platforms.md)

  La dernière version introduit des mises à jour de la matrice des plateformes prises en charge, assurant ainsi la compatibilité avec les technologies plus récentes.

   * IBM®Content Manager Client 8.7

   * MongoDB Enterprise 7.0

   * MySQL 8.4

   * Microsoft® SQL Server 2022

   * Pilote Microsoft® SQL Server JDBC 12.8

   * Red Hat® Enterprise Linux® 9 (noyau 4.x, 64 bits)

* [Composant de pièce jointe renforcé](https://experienceleague.adobe.com/fr/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment) : par mesure de sécurité, le composant empêche désormais l’envoi de fichiers avec des extensions modifiées qui tentent de contourner les vérifications des types de fichier autorisés. Ces fichiers sont bloqués lors de la soumission afin de garantir que seuls des types de fichiers valides sont acceptés.

## AEM 6.5 Service Pack 22 - 21 novembre 2024

### Sites {#sites}

[L’éditeur universel](/help/sites-developing/universal-editor/introduction.md) est désormais disponible sur AEM 6.5 pour les cas d’utilisation découplés avec l’application d’un pack de fonctionnalités.

### [!DNL Assets]

L’onglet IPTC prend désormais en charge les champs de texte [!UICONTROL Texte de remplacement] et [!UICONTROL Description étendue]. (Assets-34918)

### Formulaires {#forms-sp22}

#### Nouvelles fonctionnalités GA d’AEM Forms {#ga-aem-forms-sp22}

* Ajout de la prise en charge de l’incorporation des polices dans les [API Batch de communications interactives](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/interactive-communications/create-interactive-communication#output-format-print-channel) : les communications interactives prennent désormais en charge l’incorporation des polices Adobe Ming et Adobe Myungjo dans les PDF générés via l’API Batch. Cette amélioration garantit un rendu de texte précis dans les documents générés, même lors de l’utilisation de sous-ensembles de polices, offrant ainsi une meilleure prise en charge du contenu multilingue dans les sorties PDF.

* [API Table des matières pour l’accessibilité du PDF](/help/forms/using/aem-document-services-programmatically.md#auto-tag-pdf-documents-auto-tag-api) : AEM Forms sur OSGi prend désormais en charge la nouvelle API de balisage de table des matières, améliorant ainsi les normes d’accessibilité aux PDF. Cela rend les PDF plus accessibles pour les utilisateurs et utilisatrices utilisant des technologies d’assistance.

* [Résolution XDP de fragment](/help/forms/using/assembler-service.md#resolve-references-on-crx-repository-resolve-references-on-crx-repository) : AEM Forms sur OSGi résout désormais les fichiers XDP de fragment référencés dans les fichiers XDP maîtres et stockés dans le référentiel CRX d’AEM.

* [Améliorations de la conformité PDF/A](/help/forms/developing/pdf-a-documents.md#converting-documents-to-pdfa-documents-converting-documents-to-pdf-a-documents) : les utilisateurs et utilisatrices peuvent désormais convertir des documents PDF au format PDF/A (1a, 2a, 3a) à des fins d’archivage tout en assurant l’accessibilité et en vérifiant la conformité avec ces normes.

* **Prise en charge du dimensionnement automatique des polices pour les documents PDF statiques** : AEM Forms Designer,OutputService, et FormsService prennent désormais en charge le dimensionnement automatique des polices dans les fichiers PDF statiques. Si l’utilisateur ou l’utilisatrice définit la taille de police sur 0 pour les champs de texte, numériques, de mot de passe ou de date et heure, elle s’ajuste automatiquement dans ces champs sans modifier la taille globale du champ. Pour utiliser la fonctionnalité, les utilisateurs et utilisatrices transmettent un indicateur dans le fichier xci personnalisé : `<behaviorOverride>patch-LC-3921991:1</behaviorOverride>`.

#### Nouvelles fonctionnalités bêta d’AEM Forms {#beta-aem-forms-sp22}

La fonctionnalité bêta d’AEM Forms vous offre une opportunité unique d’accéder de manière exclusive à des innovations de pointe et de contribuer à façonner leur développement. Vous souhaitez activer une fonctionnalité bêta pour vos environnements ? Envoyez un e-mail depuis votre adresse officielle à aem-forms-ea@adobe.com avec la liste des fonctionnalités qui vous intéressent.

* [hCaptcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md) et [services Captcha Cloudflare Turnstile](/help/forms/using/integrate-adaptive-forms-turnstile.md) : AEM Forms prend en charge les services Captcha suivants :
   * Captcha protège les formulaires contre les robots, les spams et les abus automatisés en affichant un widget de case à cocher. Ainsi, seules les vraies personnes peuvent poursuivre, ce qui renforce la sécurité pour les transactions en ligne.
   * Cloudflare Turnstile offre une mesure de sécurité visant à protéger les formulaires contre les robots automatisés, les attaques malveillantes, les spams et le trafic automatisé indésirable. Il affiche une case à cocher lors de l’envoi de formulaires, ce qui permet de vérifier que l’action est effectuée par de vraies personnes, avant l’envoi effectif.

* Contrôle de version de formulaire adaptatif :
   * [Créer plusieurs versions d’un formulaire adaptatif](/help/forms/using/add-versioning-reviews-comments.md) : vous pouvez désormais gérer facilement les variations de formulaires existants. Cela simplifie la gestion de versions et facilite la comparaison pour l’optimisation des formulaires, le tout au sein d’un seul workflow simplifié.
   * [Comparer des formulaires adaptatifs](/help/forms/using/compare-forms-core-components.md) : vous pouvez désormais comparer facilement deux formulaires pour identifier les différences. Cela facilite la collaboration en permettant aux personnes membres de l’équipe de comparer les révisions et de discuter efficacement des modifications.

## AEM 6.5 Service Pack 21 - 6 juin 2024

### [!DNL Assets]

#### Améliorations

L’onglet IPTC prend désormais en charge les champs de texte [!UICONTROL Texte de remplacement] et [!UICONTROL Description étendue]. (Assets-34918)

#### Accessibilité

* Si l’état de traitement d’une ressource est Échec ou Échec des métadonnées , l’interface utilisateur des légendes et des pistes audio fonctionne désormais correctement. (Assets-37281)
* Lorsque vous enregistrez des métadonnées de ressources et que vous essayez de les modifier, le nom de la langue s’affiche désormais. (Assets-37281)

### [!DNL Forms]

Voici quelques-unes des fonctionnalités et améliorations clés de cette version :

* **Prise en charge des informations d’identification Oauth** : nouvelles informations d’identification plus faciles à utiliser pour l’authentification de serveur à serveur, remplaçant les informations d’identification de compte de service (JWT) existant. (NPR-41994)
* [Améliorations de l’éditeur de règles dans AEM Forms](/help/forms/using/rule-editor-core-components.md) :
   * Prise en charge de l’implémentation de conditions imbriquées avec la fonctionnalité `When-then-else`.
   * Validez ou réinitialisez les panneaux et les formulaires, y compris les champs.
   * Prise en charge des fonctionnalités JavaScript modernes telles que les fonctions let et arrow (prise en charge d’ES10) dans les fonctions personnalisées.
* [API AutoTag pour l’accessibilité du PDF](/help/forms/using/aem-document-services-programmatically.md#doc-utility-services-doc-utility-services) : AEM Forms sur OSGi prend désormais en charge la nouvelle API AutoTag afin d’améliorer le PDF pour les normes d’accessibilité en ajoutant des balises, des paragraphes et des listes. Cela rend les PDF plus accessibles pour les utilisateurs et utilisatrices dotés de technologie d’assistance.
* **Prise en charge de PNG 16 bits** : le service ImageToPdf du PDF Generator prend désormais en charge la conversion des PNG avec une profondeur de la couleur de 16 bits.
* **Appliquer des artefacts à des blocs de texte individuels dans des fichiers XDP** : Forms Designer permet désormais aux utilisateurs et utilisatrices de configurer des paramètres sur des blocs de texte individuels dans des fichiers XDP. Cette fonctionnalité vous permet de contrôler les éléments traités comme des artefacts dans les PDF résultants. Ces éléments, tels que les en-têtes et les pieds de page, sont rendus accessibles aux technologies d’assistance. Les principales fonctionnalités incluent le marquage des blocs de texte en tant qu’artefacts et l’incorporation de ces paramètres dans les métadonnées XDP. Le service Forms Output applique ces paramètres lors de la génération du PDF, en assurant un balisage PDF/UA approprié.
* **AEM Forms Designer est certifié par la norme `GB18030:2022`** : grâce à la certification `GB18030:2022`, Forms Designer prend désormais en charge les jeux de caractères Unicode chinois permettant de saisir des caractères chinois dans tous les champs et boîtes de dialogue modifiables.
* [Prise en charge de l’itinéraire WebToPDF dans le serveur JEE](/help/forms/using/admin-help/configure-service-settings.md#generate-pdf-service-settings-generate-pdf-service-settings) l’utilisation du service PDF Generator prend désormais en charge l’itinéraire WebToPDF pour la conversion de fichiers HTML en documents PDF sur JEE. Cette prise en charge s’ajoute aux itinéraires Webkit et WebCapture (Windows uniquement) existants. Notons que l’itinéraire WebToPDF est déjà disponible sur OSGi et étendu à JEE. À présent, sur les plateformes JEE et OSGi, le service PDF Generator prend en charge les itinéraires suivants sur différents systèmes d’exploitation :
   * **Windows** : Webkit, WebCapture, WebToPDF
   * **Linux®** : Webkit, WebToPDF


## AEM 6.5 Service Pack 20 - 22 février 2024

### [!DNL Assets]

* Dynamic Media prend désormais en charge le format d’image HEIC sans perte pour les systèmes iOS et iPadOS d’Apple. Consultez également la section [fmt](https://experienceleague.adobe.com/fr/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt) dans l’API de diffusion et de rendu d’images Dynamic Media.
* Le gestionnaire de sites multiples (MSM) prend désormais en charge les structures de fragments d’expérience, y compris les dossiers et les sous-dossiers, pour un déploiement en masse efficace des fragments d’expérience sur des Live Copies.

### [!DNL Forms]

* **Rapports de transaction dans AEM Forms on JEE** : la fonctionnalité de rapport de transaction a été introduite pour AEM Forms on JEE. Il permet l’enregistrement complet des transactions de document, telles que les conversions, les rendus et les envois. Cet apport améliore l’efficacité et facilite la conservation des données. Cette fonction est désactivée par défaut. Vous pouvez l’activer à partir de l’interface utilisateur d’administration.
* **Sécurité renforcée avec prise en charge d’ECDSA** : AEM Forms offre désormais une prise en charge robuste de l’algorithme de signature numérique (ECDSA) avec courbes elliptiques pour les piles JEE et OSGi. Il est désormais possible de signer, certifier et vérifier des documents PDF avec une sécurité renforcée. Les algorithmes avec courbes EC pris en charge incluent les éléments suivants :
   * Courbe elliptique ECDSA P256 avec algorithme de condensé SHA256
   * Courbe elliptique ECDSA P384 avec algorithme de condensé SHA384
   * Courbe elliptique ECDSA P512 avec algorithme de condensé SHA512
* **Compatibilité transparente avec Windows 11 pour Forms Designer** : AEM Forms Designer prend désormais en charge Windows 11, ce qui facilite l’installation et le fonctionnement. Il est possible d’effectuer une mise à niveau en toute confiance vers Windows 11 sans avoir à réinstaller Forms Designer ni se soucier des problèmes de compatibilité, pour un workflow ininterrompu.
* **Amélioration de l’accessibilité avec le rôle « légende » personnalisé dans AEM Forms Designer** : AEM Forms Designer inclut désormais un rôle d’accessibilité personnalisé appelé « légende », qui permet de créer des fichiers XDP avec des éléments de sous-titrage personnalisés. Cette fonctionnalité améliore l’accessibilité en permettant d’intégrer des sous-titres personnalisés dans les conceptions de document afin d’améliorer l’inclusion et l’expérience utilisateur.

## AEM 6.5 Service Pack 19 - 7 décembre 2023

* Activation de la personne Éditeur de page/Composant d’image Sites pour référencer des ressources à partir du service cloud Assets à distance. (SITES-13448, SITES-13433)
* AEM prend désormais en charge le tri côté serveur pour une navigation plus rapide dans les projets en mode Liste. Les nœuds de projet sont triés en fonction de la colonne sélectionnée par l’utilisateur ou l’utilisatrice avant d’apparaître dans l’interface.

### [!DNL Forms]

* **Nouveaux composants principaux de formulaires adaptatifs** : des onglets verticaux, des conditions générales et une case à cocher sont ajoutés pour améliorer l’évolutivité des formulaires.
   * **[Composant de case à cocher](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox)** : les formulaires adaptatifs basés sur les composants principaux peuvent désormais inclure un composant de case à cocher. Il permet aux utilisateurs et utilisatrices de faire des choix binaires, en sélectionnant ou en désélectionnant une option particulière. Il s’affiche généralement sous la forme d’une petite case sur laquelle vous pouvez cliquer ou appuyer pour basculer entre deux états : cochée et décochée. La case à cocher est un élément de formulaire courant, utilisé pour présenter un choix oui/non ou vrai/faux.

   * **[Composant des termes et conditions](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions)** : le Forms adaptatif basé sur les composants principaux inclut désormais un composant des termes et conditions. Les auteurs de formulaires ajoutent cette section pour afficher aux utilisateurs les termes, conditions ou accords juridiques du service, du produit ou de la plateforme. Ce composant est conçu pour informer les utilisateurs et utilisatrices des règles, des réglementations et des obligations qu’ils acceptent en envoyant le formulaire.

     ![Composants Onglets verticaux, Conditions générales et Case à cocher](/help/forms/using/assets/forms-components.png)

   * **[Composant Onglets verticaux](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)** : les formulaires adaptatifs basés sur les composants principaux peuvent désormais organiser le contenu des formulaires en une liste verticale d’onglets, ce qui assure une disposition structurée et navigable. Les onglets verticaux d’un formulaire améliorent l’expérience utilisateur en simplifiant la navigation et en organisant le contenu. Elles s’avèrent particulièrement utiles lorsque le formulaire contient plusieurs sections ou des informations complexes.

* **[Version 64 bits d’AEM Forms Designer](/help/forms/using/installing-configuring-designer.md)** : la version 64 bits d’AEM Forms Designer offre des performances, une évolutivité et une gestion de la mémoire améliorées pour optimiser votre expérience de création de formulaires. Grâce à l’architecture 64 bits, vous pouvez aborder facilement des projets plus volumineux et plus complexes, assurant ainsi des workflows de conception transparents et une efficacité optimisée. Améliorez encore vos capacités de conception de formulaire et accueillez l’avenir d’AEM Forms Designer avec cette version de pointe.

* **[Connexion d’un formulaire adaptatif à une liste Microsoft® SharePoint](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)** : AEM Forms assure une intégration prête à l’emploi pour envoyer les données de formulaire directement à la liste SharePoint, ce qui vous permet d’utiliser les fonctionnalités des listes SharePoint. Vous pouvez configurer une liste Microsoft® SharePoint comme source de données pour un modèle de données de formulaire et utiliser l’action Envoyer à l’aide du modèle de données de formulaire pour connecter un formulaire adaptatif à la liste SharePoint.

* **[Prise en charge de la configuration des propriétés de document d’enregistrement pour les fragments de formulaire adaptatif](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)** : vous pouvez désormais facilement personnaliser vos fragments de formulaire adaptatif et ses champs dans l’éditeur de formulaire adaptatif.

* **XMLFM 64 bits** : l’itération 64 bits de XMLFM améliore les performances, l’évolutivité et la gestion de la mémoire. Il s’agit du premier service natif 64 bits déployé côté serveur. En exploitant sa capacité intrinsèque à accéder à des ressources de mémoire plus importantes par rapport à son équivalent 32 bits, XMLFM 64 bits permet une gestion transparente des charges de travail de rendu plus lourdes. Ce jalon représente non seulement un bond en avant en termes de performances, mais il introduit également des améliorations clés du framework de service natif dans le serveur AEM Forms. Cette mise à jour permet à AEM Forms Server de prendre en charge n’importe quel service natif 64 bits de manière transparente.

## AEM 6.5, Pack de services 18—24 août, 2023

* Assets, Dynamic Media - [Prise en charge de plusieurs légendes et pistes audio pour les vidéos dans Dynamic Media](/help/assets/video.md#about-msma) - Vous pouvez désormais facilement ajouter plusieurs sous-titres et plusieurs pistes audio à une vidéo principale. Cette fonctionnalité signifie que vos vidéos sont accessibles à une audience mondiale. Vous pouvez personnaliser une seule vidéo principale publiée pour une audience mondiale dans plusieurs langues et respecter les directives d’accessibilité pour différentes régions géographiques. Les auteurs et autrices peuvent également gérer les sous-titres et les pistes audio à partir d’un seul onglet de l’interface utilisateur.
* Ressources - À partir des résultats de recherche, vous pouvez désormais accéder à l’emplacement du dossier contenant une ressource, ce qui vous permet d’effectuer diverses tâches de gestion des ressources numériques.
* Les performances du sélecteur Polaris de sites dans les fragments de contenu ont été améliorées.
* La personne utilisant l’éditeur de pages/le composant d’images des sites peut référencer des actifs à partir du service cloud d’Assets distant.
* Pour rechercher rapidement un projet dans la vue Liste, où vous pouvez avoir de nombreux projets dans votre système, Adobe prend désormais en charge le tri côté serveur. Les nœuds de projet sont triés sur le serveur principal en fonction de la colonne sélectionnée par l’utilisateur ou l’utilisatrice avant d’effectuer leur rendu dans l’interface utilisateur.
* AEM 6.5.18.0 prend en charge MongoDB, de la version 5.0 à la version 6.0.

### [!DNL Forms]

* **[Amélioration de la gestion des erreurs avec les gestionnaires d’erreurs personnalisés dans l’éditeur de règles](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms)** – Vous pouvez désormais appeler une fonction personnalisée (à l’aide de la bibliothèque cliente) en réponse à une erreur renvoyée par un service externe. Vous pouvez également fournir une réponse personnalisée aux utilisateurs finaux et utilisatrices finales. Vous pouvez également effectuer des actions spécifiques pour les erreurs renvoyées par un service. Par exemple, vous pouvez appeler un workflow personnalisé dans le serveur principal pour des codes d’erreur spécifiques ou informer le client ou la cliente que le service ne fonctionne pas.

* **[Amélioration de l’étape de workflow Adobe Sign](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/workflows/aem-forms-workflow-step-reference#sign-document-step)** – L’étape de workflow Adobe Sign dans les workflows AEM est disponible avec les améliorations suivantes.

   * **Sécurité renforcée avec authentification par ID gouvernement pour Adobe Sign** - L’authentification par ID gouvernement Adobe Acrobat Sign offre une couche supplémentaire de vérification. Elle permet aux utilisateurs et utilisatrices d’authentifier leur identité à l’aide d’une pièce d’identité officielle (permis de conduire, carte d’identité nationale, passeport). En utilisant des documents d’identification approuvés, cette amélioration ajoute un niveau de confiance supplémentaire au processus de signature, ce qui en fait une solution idéale pour les scénarios qui nécessitent une sécurité, une conformité et une validation des utilisateurs et utilisatrices renforcées.

   * **Transparence améliorée à l’aide du journal d’audit pour les documents Adobe Sign** - Utilisez la fonctionnalité du journal d’audit pour obtenir des informations détaillées sur le cycle de vie de vos documents Adobe Sign. Grâce au journal d&#39;audit, vous pouvez désormais conserver un enregistrement complet de toutes les actions et interactions liées à vos documents. Ces actions et interactions incluent les personnes qui ont consulté, modifié ou signé le document, ainsi que les horodatages de chaque événement. Cette amélioration est essentielle pour maintenir la conformité, résoudre les litiges et assurer l’intégrité de vos accords numériques.


   * **Développement des rôles des destinataires du contrat au-delà du simple signataire** - Adobe Acrobat Sign vous permet d’étendre les rôles des destinataires du contrat au-delà du simple signataire afin de mieux répondre aux exigences de leur workflow. Lorsque cette option est activée, le rôle de chaque destinataire d’un contrat peut être configuré individuellement, la personne signataire étant la valeur par défaut.


* **[Programme d’installation complet d’AEM Forms on JEE](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms)** – Le pack de services apporte un programme d’installation complet pour AEM Forms on JEE qui prend en charge plusieurs nouvelles combinaisons de logiciels, notamment :
   * Microsoft® Windows Server 2022
   * Microsoft® Active Directory 2022
   * Oracle WebLogic 14C sous Windows Server 2022
   * Red Hat® JBoss® 7.4.10
   * MongoDB 6.0 <!-- it was previously MongoDB 4.4 -->
   * Connecteur 8 JDBC MySQL

Si vous installez ou envisagez d’utiliser les derniers logiciels pour votre environnement AEM Forms 6.5 on JEE, Adobe recommande d’utiliser le programme d’installation complet d’AEM 6.5.18.0 Forms on JEE. Pour consulter la liste complète des logiciels nouvellement ajoutés et obsolètes, reportez-vous à la documentation d’AEM Forms on JEE ou d’AEM Forms on OSGi.

## AEM 6.5, Pack de services 17—25 mai 2023

* **Améliorations de l’expérience de recherche** : vous pouvez désormais effectuer rapidement les opérations suivantes sur les ressources qui s’affichent dans les résultats de recherche :
   * Créer un workflow
   * Créer une version
   * Associer ou dissocier des ressources

  Vous n’avez pas besoin d’accéder à l’emplacement de la ressource et d’afficher ses propriétés pour effectuer ces opérations.

* **Dynamic Media _Snapshot_**vous permet de prévisualiser les modificateurs d’image et les optimisations de l’imagerie dynamique, comme la sortie WebP ou AVIF, la compression basée sur la bande passante et la mise à l’échelle du rapport pixel d’appareil, à l’aide d’images de test ou d’URL Dynamic Media. Vous pouvez ensuite comparer immédiatement l’impact de chaque paramètre sur la qualité et la taille du fichier.
Voir [Instantané Dynamic Media](https://experienceleague.adobe.com/fr/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot).
* **Diffusion en continu DASH avec Dynamic Media** - Nouveau protocole (DASH - Diffusion en continu adaptative dynamique sur HTTP) lancé pour la diffusion en continu adaptative dans la diffusion vidéo Dynamic Media (avec CMAF activé). Disponible maintenant dans toutes les régions.
* **Intégration de Experience Manager Sites et des fragments de contenu à Assets Dynamic Media nouvelle génération** - Les utilisateurs peuvent désormais utiliser leurs ressources hébergées dans le cloud dans Experience Manager Sites 6.5. Ils peuvent créer et diffuser ces ressources sur des instances on-premise ou Managed Services.

### [!DNL Forms]

* **[Forms adaptative dans l’éditeur de page d’AEM](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)** - Vous pouvez désormais utiliser l’éditeur de page d’AEM pour créer et ajouter rapidement plusieurs formulaires à vos pages de sites. Cette fonctionnalité permet aux auteurs et autrices de contenu de créer des expériences fluides de capture de données dans les pages Sites à l’aide de la puissance des composants de formulaires adaptatifs, notamment le comportement dynamique, les validations, l’intégration de données, la génération d’un document d’enregistrement et l’automatisation de la gestion commerciale. Vous pouvez effectuer les actions suivantes :
   * Créez un formulaire adaptatif en faisant glisser et en déposant les composants de formulaire dans le composant Conteneur de Forms adaptatif de l’éditeur AEM Sites ou des fragments d’expérience.
   * Utilisez l’assistant de Forms adaptative dans l’éditeur AEM Sites afin de créer des formulaires indépendants de toute page Sites. Vous pouvez ainsi réutiliser ces formulaires sur plusieurs pages.
   * Ajouter plusieurs formulaires à une page Sites, en rationalisant l’expérience client et en offrant une plus grande flexibilité.
* **[Prise en charge de reCAPTCHA Enterprise dans Experience Manager Forms](/help/forms/using/captcha-adaptive-forms.md)** - Ajout de la prise en charge de reCAPTCHA Enterprise dans Experience Manager Forms. Cette fonctionnalité offre une protection améliorée contre les activités frauduleuses et le spam, en plus de la prise en charge actuelle de Google reCAPTCHA v2.
* **[Ajout de la prise en charge de Adobe Acrobat Sign for Government avec Experience Manager Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md)** - AEM Forms s’intègre désormais à Adobe Acrobat Sign for Government (compatible avec FedRAMP). Cette intégration offre un niveau avancé de conformité et de sécurité pour les signatures électroniques avec les envois de formulaires adaptatifs pour les comptes associés au gouvernement (ministères et organismes gouvernementaux). Les intégrations à Adobe Acrobat Sign for Government permettent aux partenaires d’Adobe et aux clients gouvernementaux d’utiliser les signatures électroniques dans Adaptive Forms pour certains des secteurs d’activité les plus critiques et les plus sensibles. Cette couche supplémentaire de sécurité garantit que toutes les signatures électroniques sont entièrement conformes à la norme FedRAMP Moderate, offrant ainsi la tranquillité d’esprit aux clientes et clients gouvernementaux d’Adobe.
* **Activer l’intégration de Salesforce à Experience Manager Forms pour l’échange de données** - Configurez l’intégration entre Experience Manager Forms et l’application Salesforce à l’aide du flux d’informations d’identification du client OAuth 2.0. Cette fonctionnalité permet une authentification et une autorisation sécurisées et directes de l’application et offre une communication transparente sans intervention de l’utilisateur ou utilisatrice.
* **Optimisation et fonctionnalité améliorée du moteur de workflow** : augmentez les performances des moteurs de workflow en réduisant le nombre d’instances de workflow. En complément des valeurs de statut `COMPLETED` et `RUNNING`, le workflow prend également en charge trois nouvelles valeurs de statut : `ABORTED`, `SUSPENDED` et `FAILED`.

## AEM 6.5, Pack de services 16—23 février 2023

Nouveau protocole DASH (Dynamic Adaptive Streaming over HTTP) pour le streaming à débit adaptatif dans les diffusions vidéo Dynamic Media (avec CMAF, le [format d’application de média commun], activé).

* Le streaming adaptatif (DASH/HLS) garantit une meilleure expérience de visionnage des vidéos aux utilisateurs et utilisatrices finaux.
* Largement adopté dans le secteur, DASH est le protocole standard international pour la diffusion en continu à débit adaptatif de vidéos.
* Disponible maintenant en Asie-Pacifique et en Amérique du Nord ; bientôt en Europe, au Moyen-Orient et en Afrique.

### [!DNL Forms]

* Les [formulaires adaptatifs découplés](https://experienceleague.adobe.com/en/docs/experience-manager-headless-adaptive-forms/using/overview) permettent aux développeurs et développeuses de créer, publier et gérer des formulaires interactifs accessibles et interactifs via des API, plutôt que par le biais d’une interface utilisateur graphique classique.

* Les [composants principaux des formulaires adaptatifs](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction#features) sont un ensemble de 24 composants open source compatibles avec BEM qui sont conçus sur la base des composants principaux de la gestion de contenu web d’Adobe Experience Manager. Ces composants sont en open source et permettent aux développeurs et aux développeuses de personnaliser et d’étendre facilement ces composants pour répondre aux besoins spécifiques de leur entreprise. Toute personne disposant de compétences pour personnaliser les [composants principaux de gestion de contenu web](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/get-started/authoring) peut facilement personnaliser et mettre en forme ces composants.

* Le service Reader Extensions sur OSGi fournit désormais des options distinctes permettant d’importer et d’exporter des droits d’utilisation sur un PDF afin d’importer ou d’exporter des données dans Adobe Acrobat Reader.

## AEM 6.5, Pack de services 15—24 novembre 2022

### [!DNL Forms]

* AEM Forms Designer est désormais disponible en [espagnol](https://experienceleague.adobe.com/fr/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases).
* Vous pouvez désormais utiliser [OAuth2 pour l’authentification avec les protocoles de serveur de messagerie Microsoft® Office 365 (SMTP et IMAP)](/help/forms/using/oauth2-support-for-mail-service.md).
* Vous pouvez définir la propriété [Revalider sur le serveur](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#enabling-server-side-validation-br) sur true pour identifier les champs masqués à exclure d’un document d’enregistrement côté serveur.
* AEM Forms Designer nécessite une version 32 bits de Visual C++ 2019 Redistributable (x86).

## AEM 6.5, Pack de services 14—25 août 2022

Correctifs de bogues uniquement.

## AEM 6.5, Pack de services 13—26 mai 2022

* Utilisation d’un CAPTCHA invisible dans un formulaire adaptatif : vous pouvez désormais utiliser un CAPTCHA invisible pour afficher le test de vérification CAPTCHA uniquement en cas d’activité suspecte. Si aucune activité suspecte n’est détectée, le CAPTCHA ne s’affiche pas. Il permet d’évaluer le remplissage du formulaire par un humain sans exiger de case à cocher, de réduire les efforts de personnalisation et d’améliorer l’expérience de l’utilisateur final.

* Ajout de la prise en charge de la récupération des en-têtes de réponse dans le post-processeur du modèle de données de formulaire pour les points d’entrée REST.

* Désormais, lors de la génération d’un fichier de traduction de formulaire adaptatif, la même séquence de textes dans le fichier XLIFF généré est identique à la séquence de composants dans le formulaire adaptatif correspondant.

* Lorsque vous localisez un formulaire adaptatif et apportez même une petite modification au texte de la langue de base, la traduction complète est manquante pour toutes les autres langues. Le problème est corrigé dans [!DNL Experience Manager] 6.5.13.0.

* Améliorations de l’accessibilité pour Forms :

   * Ajout de la prise en charge pour que les lecteurs d’écran reconnaissent l’en-tête et le corps d’un tableau en tant qu’entités continues et connectées. Cela permet aux lecteurs d’écran de naviguer correctement entre les tableaux. (NPR-37139)
   * Ajout de la prise en charge des lecteurs d’écran pour arrêter la navigation dans l’espace de travail HTML jusqu’à l’ouverture d’une boîte de dialogue.

## AEM 6.5, Pack de services 12—24 février 2022

* Après la configuration d’une connexion entre les déploiements de gestion des DAM et Sites à distance, les ressources de gestion des DAM à distance sont disponibles pour le déploiement sur Sites. Vous pouvez désormais effectuer les opérations suivantes : mettre à jour, supprimer, renommer et déplacer des opérations sur les ressources ou dossiers de gestion des DAM à distance. Les mises à jour, avec un certain retard, sont disponibles automatiquement sur le déploiement Sites.
* Les déploiements push d’une source de Live Copy vers plusieurs Live Copies sont désormais possibles par défaut, sans nécessiter de configuration de plan directeur.
* Le statut des opérations asynchrones en cours s’affiche désormais dans l’interface utilisateur afin d’empêcher les utilisateurs de déclencher accidentellement plusieurs opérations asynchrones sur le même chemin.
* La prise en charge de l’authentification IMS est fournie pour les API Analytics 2.0.
* Prise en charge de l’API pour le fragment d’expérience de type offre JSON.
* La demande d’offre est désormais fournie pour l’option Supprimer l’offre (API de fragment d’expérience) dans IMS.
* Le référentiel intégré (Apache Jackrabbit Oak) reste à la version 1.22.9.
