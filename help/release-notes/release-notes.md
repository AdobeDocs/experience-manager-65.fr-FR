---
title: Notes de mise à jour d’ [!DNL Adobe Experience Manager] 6,5
description: '"[!DNL Adobe Experience Manager] 6.5 Notes décrivant les informations de mise à jour, les nouveautés, la procédure d’installation et les listes de modifications détaillées."'
mini-toc-levels: 3
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: e51cf7a5b7d14bc4aed053496c7fe6685dd2b0b8
workflow-type: tm+mt
source-wordcount: '3653'
ht-degree: 7%

---

# [!DNL Adobe Experience Manager] 6.5 Dernières notes de mise à jour du Service Pack {#aem-service-pack-release-notes}

## Informations sur la version {#release-information}

| Produit | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.13.0 |
| Type | Version du Service Pack |
| Date  | 26 mai 2022 |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.13.0.zip) |

## Éléments compris dans [!DNL Experience Manager] 6.5.13.0 {#what-is-included-in-aem}

[!DNL Experience Manager] 6.5.13.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les clients, ainsi que des améliorations en termes de performances, de stabilité et de sécurité, publiées depuis la version initiale de 6.5 en avril 2019. [Installer ce Service Pack](#install) on [!DNL Experience Manager] 6.5.

Les fonctionnalités et améliorations clés introduites dans [!DNL Adobe Experience Manager] 6.5.13.0 sont :

* Utiliser CAPTCHA invisible dans un formulaire adaptatif : Vous pouvez désormais utiliser un CAPTCHA invisible pour montrer le défi CAPTCHA uniquement en cas d&#39;activité suspecte. Si aucune activité suspecte n&#39;est trouvée, le défi CAPTCHA ne s&#39;affiche pas. Il permet d’évaluer le remplissage du formulaire par un humain sans exiger de case à cocher, de réduire les efforts de personnalisation et d’améliorer l’expérience de l’utilisateur final. (NPR-38500)

* Ajout de la prise en charge de la récupération des en-têtes de réponse dans le post-processeur du modèle de données de formulaire pour les points de terminaison REST. (NPR-38275)

* Désormais, lors de la génération d’un fichier de traduction de formulaire adaptatif, la même séquence de textes que le fichier XLIFF généré est identique à la séquence de composants dans le formulaire adaptatif correspondant. (NPR-37700)

* Lorsque vous localisez un formulaire adaptatif et apportez même une petite modification au texte de la langue de base, la traduction complète est manquante pour toutes les autres langues. Le problème est corrigé dans [!DNL Experience Manager] 6.5.13.0. (NPR-37189)

* Améliorations de l’accessibilité pour Forms :

   * Ajout de la prise en charge pour les lecteurs d’écran de reconnaître l’en-tête et le corps d’un tableau comme des entités continues et connectées. Cela permet aux lecteurs d’écran de naviguer correctement dans les tableaux. (NPR-37139)
   * Ajout de la prise en charge des lecteurs d’écran pour arrêter la navigation dans l’espace de travail de HTML jusqu’à l’ouverture d’une boîte de dialogue. (NPR-37134)

   <!-- 

    * Added ability to specify Screen Reader Text for Hyperlinks in Forms Designer.(NPR-36221)
  
  -->

Les correctifs de bogues, fonctionnalités clés et améliorations suivants ont été introduits dans [!DNL Experience Manager] 6.5.13.0 :

<!-- The following issues are fixed in [!DNL Experience Manager] 6.5.13.0: -->

## [!DNL Assets] {#assets-6513}

* Lors de la tentative de modification d’un champ déroulant en lecture seule, la valeur de la liste déroulante est réinitialisée à vide. (NPR-38389)
* L’utilisateur ne peut pas ingérer de ressource vidéo (.mp4) s’il n’y a pas de contenu audio dans le fichier vidéo. Le workflow Ressources de mise à jour de gestion des actifs numériques échoue et affiche un message d’erreur. (NPR-38116)
* Lorsque vous utilisez l’assistant de déplacement de ressources pour déplacer un dossier contenant des ressources, le workflow échoue et reflète un message d’erreur. (NPR-38061)
* Échec du workflow de transcodage FFmpeg pour le profil vidéo FLV. (CQ-4343249)
* Après la mise à jour vers [!DNL Experience Manager] 6.5 SP10, l’éditeur de métadonnées de ressource ne fonctionne pas correctement. (CQ-4341359)
* Lors de l’ouverture d’une collection dynamique enregistrée avec le filtre de recherche appliqué comme Publier, le filtre de recherche passe automatiquement à Publication annulée. (CQ-4341191)
* Lors du changement de langue dans **[!UICONTROL Préférences utilisateur]**, le libellé **[!UICONTROL Trier par]**, le bouton déroulant et d’autres options de tri sur la page d’accueil des ressources ne sont pas répercutés dans la langue sélectionnée. (CQ-4339306)
* Lors de l’ajout d’une règle à un champ déroulant dans **[!UICONTROL Schéma de métadonnées]**, la variable **[!UICONTROL Dépendant de]** ne reflète pas le libellé du champ de la liste déroulante. (ASSETS-9442)
* La liste déroulante Métadonnées des ressources est désactivée et ne conserve pas les valeurs. (ASSETS-8918)
* Lors de l’affichage de la ressource à l’aide de **[!UICONTROL Plus de détails]** dans **[!UICONTROL Colonne]** affichage, des annotations incorrectes s’affichent. (ASSETS-8851)
* Lors de la création d’une ressource en double avec une version différente, les rendus ne sont pas générés. (ASSETS-8607)

* Un utilisateur non administrateur peut publier une ressource déjà extraite par un autre utilisateur. (NPR-38128)
* La visionneuse Dimensionnel n’est pas fonctionnelle sur Chrome 97. (CQ-4340456)
* Le bouton de téléchargement de ressources n’affiche pas le menu complet sur la page Détails de la ressource. (CQ-4336703)
* Lors de l’utilisation du partage de lien, certaines chaînes de la fenêtre de partage de lien ne sont pas localisées. (CQ-4330540)
* Lors de l’ajout d’éléments dans Gérer la publication, la chaîne qui reflète le nombre d’éléments sélectionnés n’est pas localisée. (CQ-4330491)

### [!DNL Dynamic Media] {#dynamic-media-6513}

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Zero day exploit with the Java™ Spring Core Framework (CVE-2022-22963) impacting Experience Manager 6.5.12. (ASSETS-9031) -->
* Aperçu sécurisé basé sur les jetons pour les ressources Dynamic Media sur les auteurs AEM. (ASSETS-4995)
* Lors de la création d’un paramètre d’image prédéfini pour Dynamic Media dans [!DNL Experience Manager], le nombre maximal autorisé est limité à 2 000 x 2 000 pixels dans l’interface utilisateur. Lorsque la valeur est augmentée à 2 001 pixels pour la largeur ou la hauteur, la variable **[!UICONTROL Enregistrer]** est désactivé. (ASSETS-5691)
* L’utilisateur peut empêcher le téléchargement de certains formats de fichier vers Dynamic Media. (ASSETS-5693)
* Accessibilité : les utilisateurs ayant un problème visuel et qui dépendent des lecteurs d’écran sont affectés si l’attribut Alt n’est pas implémenté sur une image dans l’interface utilisateur des paramètres d’image prédéfinis. (ASSETS-9817)
* Accessibilité : les lecteurs d’écran sont impactés lorsque les lecteurs d’écran narrent une image sans libellé pour les images présentes dans le &quot;segment de la chronologie&quot; et dans l’onglet &quot;Actions&quot;, lorsqu’ils y accèdent en mode Flèche vers le bas. (ASSETS-5651)
* Accessibilité : les lecteurs d’écran sont impactés, car les lecteurs d’écran (NVDA/JAWS) ne narrent pas le nom descriptif (Envoyer un courrier électronique) pour le bouton &quot;Envoyer un courrier électronique&quot; dans la boîte de dialogue &quot;Lien de courrier électronique&quot; du lecteur vidéo, lors de la navigation en mode (Parcourir/Curseur). (ASSETS-5641)
* Accessibilité : la sélection du clavier ne passe pas au bouton &quot;Rétablir&quot; qui s’affiche après avoir appelé le bouton &quot;Annuler&quot; sur la page de l’éditeur de visionneuse d’images, lors de la navigation à l’aide de la touche TAB du clavier. (ASSETS-5582)
* Accessibilité : les utilisateurs qui dépendent des lecteurs d’écran sont affectés, car l’attribut Alt n’est pas fourni pour une image de visionneuse d’images qui se trouve sous l’en-tête Propriétés . (ASSETS-5576)
* Accessibilité : les lecteurs d’écran ne narrent pas le rôle d’en-tête pour `Cannot save this set` texte dans la variable `Cannot save this set` alerte, lors de la navigation à l’aide de la touche de raccourci de titre `H`et touche Flèche vers le bas. (ASSETS-5569)
* Accessibilité : les utilisateurs qui dépendent des lecteurs d’écran sont affectés pour naviguer dans les formulaires. Ils ont des difficultés à comprendre les informations sur les commandes de formulaire si la variable NVDA ne décrit pas les informations d’étiquette des commandes de rotation &quot;Largeur et hauteur&quot;. Ces commandes sont présentes sous l’en-tête Recadrage d’image réactive lors de la navigation dans le mode de formulaire NVDA &quot;F&quot;. (ASSETS-5393)
* Après l’ajout d’un composant Dynamic Media sur un site et la publication de la page, la ressource Dynamic Media nouvellement ajoutée n’est pas visible sur la page publiée, ni elle n’est visible dans la page Aperçu. Ce problème survenait pour les types de ressources image et vidéo. (ASSETS-9467)

## Commerce  {#commerce-6513}

* &quot;everyone&quot; a jcr:write sur `/content/usergenerated/etc/commerce/smartlists`. (NPR-35230)
* Le tri local des produits de commerce ne fonctionne plus. (CQ-4343750)
* Impossible de publier rapidement un produit à partir de la page des résultats de recherche après avoir modifié les propriétés. (CQ-4343318)

## CRX  {#crx-6513}

* Impossible de télécharger un package s’il possède le caractère spécial `+` dans le nom du module. (NPR-38102)

## [!DNL Forms] {#forms-65130}

<!-- * When you use the prefill service to fill an adaptive form that contains a fragment and the fragment contains a Text box that supports rich text, the form fails to submit, and the following error occurs:

  `[AF] [AEM-AF-901-004]: Encountered an internal error while submitting the form.` (NPR-38542) -->

* Les composants Bouton radio, Case à cocher et Téléchargement de fichier ne sont pas correctement traduits de l’allemand vers l’anglais. (NPR-38527)
* Encodage du code à barres PDF417 produit par [!DNL Experience Manager] Forms n’est pas valide pour un groupe de boutons radio. (NPR-38525)
* L’erreur suivante se produit lors de l’envoi d’un formulaire adaptatif.
   `WARN [10.172.114.236 [1650871578492] POST /lc/content/forms/af/public/DHS-3754-ENG/jcr:content/guideContainer.af.internalsubmit.jsp HTTP/1.1] com.adobe.aemds.guide.internal.impl.utils.SubmitDataCollector TemplateKey not found in merge json:cq:responsive` (NPR-38520)
* L’option Exclure les champs masqués du document d’enregistrement ne fonctionne pas. (NPR-38512)
* Après l’ajout du composant Conteneur Forms à une page Sites, les utilisateurs ne peuvent pas accéder à une autre page Sites et la page Sites se bloque parfois. Le problème apparaît par intermittence. (NPR-38506)
* Les utilisateurs voient le texte se chevaucher dans le Forms adaptatif après application [!DNL Experience Manager] 6.5 Service Pack 11. (NPR-38376, CQ-4342472)
* Les utilisateurs rencontrent une exception lors du déplacement des panneaux de formulaires adaptatifs vers une nouvelle mise en page réactive. (NPR-38369)
* La prise en charge d’ECMASCRIPT 6 (ES6) n’est pas activée pour la bibliothèque cliente ` /libs/fd/expeditor/clientlibs/view`. (NPR-38358)
* Lorsque vous utilisez une [!DNL Experience Manager] Pour envoyer un email en hébreu, le message reçu à la fin de l’utilisateur contient des points d’interrogation (??) au lieu du texte en hébreu (NPR-38296).
* Les utilisateurs sont déconnectés de manière aléatoire de [!DNL Experience Manager] Les instances de publication et un formulaire adaptatif ne peuvent pas être envoyés. Le problème apparaît sur [!DNL Experience Manager] instances qui utilisent Dispatcher. (NPR-38285)
* Lorsque vous utilisez l’option getFormDataString dans la règle d’un Adobe Launch pour capturer les données de formulaire adaptatif, l’option ne renvoie pas de données de Forms adaptatif. (NPR-38283)
* [!DNL Experience Manager] 6.5 L’API java.acl.Group obsolète de Forms et les messages d’erreur suivants apparaissent dans le fichier error.log :
   ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details` (NPR-38282)
* Les Forms créées en allemand ne parviennent pas à traduire en anglais ou dans toute autre langue. (NPR-38280)
* Lorsque vous utilisez une version localisée d’un formulaire adaptatif, le document d’enregistrement correspondant n’est pas localisé. (NPR-38235)
* Lorsque vous utilisez l’étape Envoyer un courrier électronique pour envoyer une pièce jointe avec un courrier électronique, la pièce jointe ne conserve pas le nom spécifié dans l’étape Processus. (NPR-38216)
* Lorsqu’une nouvelle version de la lettre est publiée, les utilisateurs ne peuvent pas ouvrir les brouillons de lettres pour les versions précédentes des lettres. (NPR-38215, CQ-4342515)
* Lors de l’appel d’une méthode de service de point d’entrée SOAP du service AEM Forms JEE sur un clic de bouton configuré en tant que règle de formulaire adaptatif, le service SOAP échoue avec l’exception suivante :
   `ERROR* [0:0:0:0:0:0:0:1 [1624362360493] POST /content/forms/af/testsoapwsdl/jcr:content/guideContainer.af.dermis HTTP/1.1] com.adobe.aemds.guide.addon expeditor.servlet.ExpEditorServiceManager Error while making web service related call java.lang.Exception: createSOAPParam: JSONException`
* Lors de l’utilisation de com.adobe.fd.pdfutility.services.PDFUtilityService#convertPDFtoXDP pour convertir un PDF au format XDP, un fichier XDP non valide est renvoyé. (NPR-38140, CQ-4342099)
* Lorsque plusieurs utilisateurs utilisent Correspondence Management pour générer des lettres différentes, lors de l’aperçu, une lettre incorrecte s’affiche pour certains utilisateurs. (NPR-38134)
* Le composant AEM Forms incorporé dans la page SITES utilise l’attribut width qui a une valeur en % et n’est pas valide conformément à la validation du HTML W3C. Les utilisateurs rencontrent une erreur d’analyse incorrecte lors de la validation du HTML. (NPR-38124)
* Les éléments de bouton radio et de case à cocher correspondant à la plupart des thèmes prêts à l’emploi dans les formulaires adaptatifs ne font pas partie de l’ordre de tabulation (NPR-38108)
* Lorsqu’un utilisateur ajoute des balises de HTML à la section de commentaire lors de l’exécution d’un workflow, les balises de HTML sont rendues. (NPR-37591)
* Lors de l’importation et de la publication d’une lettre contenant un nouveau fichier XDP, les lettres ne parviennent pas à être prévisualisées sur l’instance de publication. Toutefois, si les lettres sont importées et publiées une seconde fois à l’aide du même fichier de CMP, les lettres sont prévisualisées avec succès. (CQ-4343599)
* Le rendu d’un formulaire avec le jeu de propriétés de processus de données Préparer échoue dans HTML Workspace. (CQ-4343294)
<!--
For static PDF forms that are created with Forms 6.5 Designer, PDF accessibility fails with error `Tab order entry in page with annotations not set to "S"`. (CQ-4343117) 
 -->
* Impossible de convertir une image en PDF à l’aide du service PDFG avec OCR, après avoir appliqué le correctif AEMForms-6.5.0-0038 (log4jv2.16). (CQ-4342450)

<!-- 
* Incorrect value is displayed for barcode SSCC-18. Forms servers omit the value on the right part of the barcode. (CQ-4342400)
-->
* Impossible d’importer un fichier Microsoft® Word dans Forms Designer. L’utilisateur rencontre une erreur `Word (version XP or onwards) could not be found on the machine`. (CQ-4342146)

<!-- 
* In Forms 6.5 Designer, when you open a form created with Forms 6.1 Designer and edit a textbox, paragraph spacing exceeds the specified space. All previous settings to the space are removed and manual reformatting of the text box is required. (CQ-4341899) 
-->
* L’utilisateur ne peut pas définir d’heure personnalisée dans le planificateur de purge de tâche. (CQ-4339192)
* L’utilisateur ne peut pas mettre à jour une configuration sous l’interface utilisateur de gestion des points de fin et rencontrer une erreur ` Uncaught ReferenceError: updateEndpoint_required is not defined`. (CQ-4331523)
* Pour les balises non valides, la gestion correcte du message d’erreur ne fonctionne pas comme prévu. (NPR-38106 et CQ-4337173)

>[!NOTE]
>
>* [!DNL Experience Manager Forms] publie les packages de modules complémentaires une semaine après la date de publication prévue du Service Pack [!DNL Experience Manager].


## Granite {#granite-6513}

* L’omni-recherche renvoie le résultat pour les utilisateurs ne disposant pas de droits de lecture. (NPR-38373)
* Activer ES6 pour `/libs/granite/configurations/clientlibs/confbrowser`. (NPR-38300)

## Intégrations {#integrations-6513}

* Fuite des sessions de résolveur de ressources sur le service Test and Target à partir d’UserInfoServlet obsolète. (NPR-38112)

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * AEM‑OP‑13 ‑ HTTP Parameter Pollution in `com.day.cq.searchpromote.impl.servlet`. (NPR-38033) -->
<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Analytics 2.0 IMS support added to Experience Manager 6.5. (NPR-37914) -->

## Oak - Indexation et requêtes {#oak-6513}

* La version Oak de la version 6.5.13.0 est désormais mise à jour vers la version 1.22.11. (NPR-38084) -->

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Create a CFP based on latest 6.5.12 and update Oak-related bundle versions. (NPR-38144) -->

## Plateforme {#platform-6513}

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * RTC : Universal XSS through cq-rewriter HtmlParser. (NPR-38064) -->
* Mise à niveau de la dépendance de `org.apache.httpcomponents.httpclient` in [!DNL Experience Manager] 6.5. (NPR-37999)
* Chargement élevé de l’auteur en raison des suggestions de champs de chemin d’accès. (CQ-4341826)
* L’utilisateur doit actualiser la page lorsqu’il passe du mode Carte au mode Calendrier. (CQ-4340368)
* Les balises sont perdues en raison de restrictions d’autorisation. (CQ-4339543)
* Plusieurs problèmes signalés avec Recherche et filtrage dans la sélection de chemins ne fonctionnent pas. (CQ-4339402)
* Arrêtez d’utiliser DTM sur la version 6.5 - basculez sur Launch pour l’instrumentation Omega et ajoutez la prise en charge de Gainsight. (CQ-4337809)
* Restreindre la fonction de recherche du composant pathfield en fonction de la propriété de filtre pathfield définie. (CQ-4309556)
* [!DNL Experience Manager] Platform 6.5 : Correctifs d’attribution de noms aux paramètres régionaux chinois. (CQ-4308978)
* Basculez vers Launch pour l’instrumentation Omega. (NPR-38377)
* [!DNL Experience Manager] Platform 6.5 : Correctifs de noms de paramètres régionaux chinois. (CQ-4308978)

## Réplication {#replication-6513}

* Publication du noeud utilisateur Échec de l’auteur dans l’éditeur. (NPR-38005)

## [!DNL Sites] {#sites-6513}

### Admin {#sites-admin-6513}

* Correction d’une régression introduite avec SP 12 qui était susceptible d’entraîner un problème lors du déplacement de pages. (SITES-5298)

### Interface utilisateur classique {#sites-classicui-6513}

* Éditeur de texte enrichi : L’image mise à jour n’est pas visible lorsqu’une nouvelle image est glissée sur une image existante. (NPR-38141)

<!-- version 2 of description above * Updated Image is not visible When a new image is dragged on top of an existing image the updated image is not visible in RTE - Classic UI. (NPR-38141) -->

### Fragments de contenu {#sites-contentfragments-6513}

* Prise en charge de la création de modèles de fragment de contenu dans les sous-configurations. (NPR-38054)

<!-- version 2 of description above * The Configuration Manager now allows you to set the Content Fragment Model config on a sub-config folder. (NPR-38054) -->
* Améliorez les performances lors de l’utilisation de la validation &quot;Champ unique&quot; dans le modèle de fragment de contenu. (NPR-38142)

<!-- version 2 of description above * The unique field validation query is now fixed. (NPR-38142) -->
* Amélioration du temps de réponse lors de l’ouverture de l’éditeur de modèle de fragment de contenu. Les clients qui ont de nombreux fragments dans Assets peuvent avoir rencontré des erreurs lors de l’ouverture. (SITES-6284)

<!-- version 2 of description above * If the customer is trying to access the editor of the content fragment models, they get a query error because of too many fragments on the dam. (SITES-6284) -->
* Correction d’une régression introduite lors de la mise à jour de la version 6.5.11 vers la version 6.5.12 qui était susceptible d’entraîner des erreurs dans l’éditeur de modèle de fragment de contenu. (SITES-5088 et SITES-4967)

<!-- version 2 of description above * Paths were getting deleted when AEM 6.5.12.0 was installed on existing 6.5.11.0 instance. (SITES-5088)
* Apple 6.5.10 system crashing when using CF model editor, due to erroneous feature toggle check. (SITES-4967) -->
* Améliorez la localisation de l’interface utilisateur de l’éditeur de modèle de fragment de contenu. (NPR-38126)

<!-- version 2 of description above * Some strings in the Content Fragment Model editor are not localized. (NPR-38126) -->
* Correction d’un problème en raison duquel la fermeture de l’éditeur de fragments de contenu pouvait entraîner une erreur lorsque le serveur de création était utilisé avec Dispatcher. (NPR-38205)

<!-- version 2 of description above * Update of Content Fragment references is returning an invalid JSON response via Dispatcher. (NPR-38205) -->
* Correction d’un problème en raison duquel l’enregistrement d’un modèle n’était pas possible lorsque la validation était utilisée sur un champ d’éditeur de texte enrichi. (NPR-38210)

<!--version 2 of description above * Content Fragment Model Rich Text Validation Prevents Blocks Saving a Content Fragment Model. (NPR-38210) -->
* Problème de fragment de contenu en raison duquel la propriété booléenne n’affichait pas le texte du champ dans &quot;titre&quot;, mais affichait plutôt &quot;Nom de la propriété&quot;. (NPR-38244)
* Erreur lors de l’exécution de la requête persistante avec la variable de requête via Postman. (NPR-38251, NPR-38057)
<!--version 2 of description above * An unexpected error message is coming in Postman, when executing the graphQL persisted query having query variables. (NPR-38251) -->
* Composant de fragment de contenu : Correction d’une régression dans l’option &quot;Gérer les en-têtes comme des paragraphes&quot; qui était de 6.5 SP7. (NPR-38055)

<!--version 2 of description above * After applying SP11 to the Publish instance of AEM 6.5.6, the display result of the Content Fragment set in the published page changes. (NPR-38055) -->
* Correction d’une régression introduite dans la version 6.5.11 qui était susceptible d’entraîner des erreurs de recherche de ressources. (SITES-4784)

<!--version 2 of description above * Adapt external index package to use selection Policy (fragment versus asset index). (SITES-4784) -->
* Utilisation **[!UICONTROL Modifier]** dans les résultats de la recherche, un événement `Not Found` erreur. (NPR-37810)

<!--version 2 of description above * When editing Content Fragment from the Assets Search Rail results page, it throws 'Not Found' error. (NPR-37810) -->

### ContentHub {#sites-contenthub-6513}

* Les modèles d’IU ContextHub ne sont pas correctement rendus sans actualisation de la page dure. (NPR-38212)

### Éditeur de messagerie électronique {#sites-emaileditor-6513}

* Activation de la prise en charge de la prochaine version des composants principaux de messagerie électronique [https://github.com/adobe/aem-core-email-components](https://github.com/adobe/aem-core-email-components). (NPR-38445 et NPR-38204)

<!-- version 2 of description above * Allow new email templated under campaign and ambit. (NPR-38445) * The "Approve for Adobe Campaign" workflow was only running for pages which are of type or extending the resource types: "mcm/neolane/components/newsletter", "mcm/campaign/components/newsletter" and "mcm/campaign/components/campaign_newsletterpage". (NPR-38204) -->

### Présentation {#sites-experiencefragments-6513}

* Lorsque vous utilisez l’action Accéder à la page dans Références d’un fragment d’expérience, elle ouvre la mauvaise page. (NPR-38062)
* Les propriétés de mise en page provenant du modèle XF ne sont pas observées dans le côté d’une page. (NPR-38214)
* Amélioration des performances du calcul de référence XF. (NPR-38269)

<!-- version 2 of description above * Job queue configuration is incorrect - The OSGi configuration for the reference updater job queue has not been ported back to 6.5. This issue leads to jobs being run in the main queue, which has a higher priority and allows more jobs to run in parallel. This flow can lead to CPU exhaustion. (NPR-38269) -->

### Éditeur de page {#sites-pageeditor-6513}

* Améliorez l’annulation pour les composants qui n’ont pas de fonctionnalité intégréeEditing ou dropTarget dans `cq:editConfig`. (NPR-38361)

<!-- version 2 of the description above * When out of the box components that don't have inlineEditing or dropTarget feature in the _cq_editConfig file (navigation, breadcrumb, embed) are deleted > undeleted (by way of Undo), all configurations are lost and empty placeholder reappears. Component must be reconfigured from scratch. (NPR-38361) -->
* La liste déroulante Système de style a peut-être été positionnée en haut de la page au lieu de dans le contexte du composant, pour les composants qui utilisent `cq:editConfig` &quot;afteredit: REFRESH_PAGE&quot;. Ce problème est maintenant résolu. (NPR-38384)

<!-- version 2 of description above* When selecting a style option on a component, the Styles box shifts to the upper left corner of the screen, rather than staying put below the style icon. Happens for components that have  cq:editConfig “afteredit: REFRESH_PAGE”. (NPR-38384) -->
* Le composant Texte n’est pas aligné lorsqu’il est ajouté aux conteneurs de mise en page imbriqués. (NPR-38193)
* Un onglet de style vide s’affichait lorsqu’il n’y avait aucune configuration de système de style pour un composant ; l’onglet est maintenant masqué lorsqu’aucune configuration n’est présente. (NPR-38218)
<!-- version 2 of description above * Style tab is blank on components without styles/policies. (NPR-38218) -->
* La propriété `useLegacyResponsiveBehaviour` fonctionne uniquement lors de l’authentification. (NPR-37996)
* La mise à niveau de jquery-ui vers la dernière version entraînait la rupture de l’éditeur. (SITES-5647)

### Sécurité {#sites-security-6513}

* L’interface utilisateur de gestion des groupes d’utilisateurs ne parvenait parfois pas à supprimer les utilisateurs, en particulier dans les groupes comportant plus de 20 utilisateurs. (NPR-38041)

<!--version 2 of description above * Cannot remove users from user groups. (NPR-38041) -->

### SEO {#sites-seo-6513}

* Le générateur de plans de site et la balise canonique prennent en charge les URL sans .html. (CIF-2647)
* Ajoutez la prise en charge de la suppression des langues alternatives à l’aide de la configuration noindex . (CIF-2496)
* Ajoutez la prise en charge pour fournir une URL personnalisée afin de remplacer l’URL canonique par défaut pour les pages comportant un contenu quasi identique. (CIF-2747)

### Éditeur SPA et SDK {#sites-spa-sdk-6513}

* À compter de la version 6.5.13, vous ne devez plus créer le noeud de composant de conteneur dans JCR avant d’apporter des modifications par le biais de l’éditeur SPA. A `virtual container` est créé avant de l’enregistrer au moyen du SDK. (SITES-5762)

<!-- version 2 of description above * Virtual container support - Adding a child component to a virtual container that is not yet present in the database implies the creation of a node to represent the container in content structure. (SITES-5762) -->

### Éditeur de modèles {#sites-templateeditor-6513}

* Correction de la régression selon laquelle la publication d’un modèle modifié ne publiait pas toutes les dépendances. (NPR-38274)

<!-- version 2 of description above * Template changes do not get published until you publish a page that uses that template. (NPR-38274) -->
* TemplatedResource valueMap doit permettre des lectures profondes selon l’API ValueMap. (NPR-38439)

## Sling {#sling-6513}

<!-- OBSOLETE BASED ON CQDOC-19400 * Memory leak in `DiscoveryLiteDescriptor`. (NPR-38288) -->
* Mettre à jour `sling-javax.activation` lot avec le correctif de SLING-8777. (NPR-38077)

<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * Security issues reported under `org.apache.sling.scripting.jst`. (NPR-38067) -->

## Projets de traduction {#translation-6513}

* Plusieurs lancements sont créés pour les pages/xf référencées. (NPR-38263)
* Modification du comportement de l’ajout de pages aux projets de traduction depuis le Service Pack 10. Le projet de traduction ne contient pas de page nouvellement créée. [ex : test-page-femmes-2] dans la liste, lorsqu’il est sélectionné parent de la page nouvellement créée. [ne pas directement créer la page]. (NPR-38256)
* Ajouter `cq:isTranslationLaunch` dans Lancements créés par le projet de traduction. (NPR-38224)
* Launch est créé pour une page dont le fichier XF est référencé et qui contient une ressource. (NPR-38199)
* [!DNL Experience Manager] la mise à jour de la mémoire de traduction ne fonctionne pas. (NPR-38196)
* Activer ES6 pour `/libs/cq/gui/components/projects/admin/translation/job/addcontent/clientlibs.js`. (NPR-38306)
* Dernier package 18n pour les traductions pour [!DNL Experience Manager] 6.5. (CQ-4339505)

## Interface utilisateur {#ui-6513}

* Mettre à jour vers `favicon.ico` utilisé en Experience Manager. (CQ-4315324)
* Lorsque vous êtes sur la page de démarrage > dans la section Outils , cliquez sur le bouton [!DNL Experience Manager] , l’icône [!DNL Experience Manager] L’écran de navigation doit s’afficher. (NPR-38417)
* Activer ES6 pour `/libs/granite/ui/references/clientlibs/coral/references`. (NPR-38303)
* Activer ES6 pour `/libs/granite/datavisualization/clientlibs/d3-3.x`. (NPR-38302)
<!-- VULNERABILITY ISSUE - REMOVED AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * AEM‑OP‑09 ‑ Persistent cross‑site scripting selecting paths in templates. (NPR-38301) -->
* Le sélecteur de date dans l’interface utilisateur tactile s’affiche en coréen. (NPR-38079)
* Boîte de dialogue de création avec plusieurs champs, lors de la réorganisation des champs en perdant la valeur de sélection du bouton radio. (NPR-38063)

## WCM {#wcm-6513}

* [!DNL Experience Manager] MCM (Campaign) 6.5 : Correctifs d’attribution de noms aux paramètres régionaux chinois. (CQ-4308973)
* ResourceResolver non fermé dans com.day.cq.wcm.workflow.impl.WcmWorkflowServiceImpl.autoSubmitPageAfterModification (NPR-38286)

## Installer [!DNL Experience Manager] 6.5.13.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback -->

* [!DNL Experience Manager] 6.5.13.0 nécessite [!DNL Experience Manager] 6.5. Voir [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour obtenir des instructions détaillées.
* Le téléchargement du Service Pack est disponible sur Adobe [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Sur un déploiement avec MongoDB et plusieurs instances, installez [!DNL Experience Manager] 6.5.13.0 sur l’une des instances d’auteur à l’aide du gestionnaire de modules.

>[!NOTE]
>
>Adobe ne recommande pas de supprimer ou de désinstaller le [!DNL Experience Manager] Package 6.5.13.0.

### Installez le Service Pack sur [!DNL Experience Manager] 6,5 {#install-service-pack}

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.

1. Avant l’installation, prenez un instantané ou une nouvelle sauvegarde de votre [!DNL Experience Manager] instance.

1. Téléchargez le Service Pack à partir de [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.13.0.zip).

1. Ouvrez Package Manager et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package. Pour en savoir plus, voir [Gestionnaire de modules](/help/sites-administering/package-manager.md).

1. Sélectionnez le module et cliquez sur **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du Service Pack, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Voir [Entrepôt de données Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface utilisateur de Package Manager se ferme parfois pendant l’installation du Service Pack. Adobe recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les logs spécifiques liés à la désinstallation du lot de mise à jour avant de vous assurer que les installations sont réussies. En règle générale, ce problème se produit dans [!DNL Safari] mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Vous pouvez utiliser deux méthodes différentes pour installer automatiquement [!DNL Experience Manager] 6.5.13.0.

* Placez le module dans `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.
* Utilisez la variable [API HTTP à partir de Package Manager](/help/sites-administering/package-manager.md#package-share). Utilisation `cmd=install&recursive=true` afin que les modules imbriqués soient installés.

>[!NOTE]
>
>[!DNL Experience Manager] 6.5.13.0 ne prend pas en charge l’installation du Bootstrap.

**Validation de l’installation**

Pour connaître les plates-formes certifiées pour travailler avec cette version, reportez-vous à la section [exigences techniques](/help/sites-deploying/technical-requirements.md).

1. la page d’informations sur les produits (`/system/console/productinfo`) affiche la chaîne de version mise à jour. `Adobe Experience Manager (6.5.13.0)` under [!UICONTROL Produits installés].

1. Tous les lots OSGi sont : **[!UICONTROL PRINCIPAL]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (Utiliser la console web : `/system/console/bundles`).

1. Le lot OSGi `org.apache.jackrabbit.oak-core` est version 1.22.3 ou ultérieure (Utiliser la console web : `/system/console/bundles`).


### Installer [!DNL Experience Manager] Package de module complémentaire Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Ignorer si vous n’utilisez pas [!DNL Experience Manager] Forms. Correctifs de [!DNL Experience Manager] Forms est livré par le biais d’un module complémentaire distinct une semaine après la planification de la [!DNL Experience Manager] Version du Service Pack.

1. Assurez-vous que vous avez installé le [!DNL Experience Manager] Service Pack.
1. Téléchargez le module complémentaire Forms correspondant répertorié dans les [versions AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) pour votre système d’exploitation.
1. Installez le module complémentaire Forms comme décrit dans [Installation des packages de modules complémentaires AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).
1. Si vous utilisez des lettres dans Experience Manager 6.5 Forms, installez la variable [dernier package de compatibilité AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates).

### Installer [!DNL Experience Manager] Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Passez cette étape si vous n’utilisez pas AEM Forms sous JEE. Correctifs de [!DNL Experience Manager] Forms on JEE est fourni via un programme d’installation distinct.

Pour plus d’informations sur l’installation du programme d’installation cumulatif pour [!DNL Experience Manager] Configuration de Forms on JEE et post-déploiement, voir la section [notes de mise à jour](jee-patch-installer-65.md).

>[!NOTE]
>
>Après l’installation du programme d’installation cumulatif pour [!DNL Experience Manager] Forms on JEE, installez le dernier module complémentaire Forms, supprimez le module complémentaire Forms du `crx-repository\install` et redémarrez le serveur.

### UberJar {#uber-jar}

UberJar pour [!DNL Experience Manager] 6.5.13.0 est disponible dans la [Référentiel Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.13/)(https://).

Pour utiliser UberJar dans un projet Maven, voir [utilisation d’UberJar](/help/sites-developing/ht-projects-maven.md) et incluez la dépendance suivante dans le POM de votre projet :

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.13</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar et les autres artefacts associés sont disponibles sur le référentiel central Maven au lieu du référentiel Maven public Maven Adobe (`repo.adobe.com`). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Il n&#39;y a donc pas de `classifier`, avec `apis` comme valeur, pour la propriété `dependency` balise .

## Fonctionnalités obsolètes {#removed-deprecated-features}

Vous trouverez ci-dessous une liste des fonctionnalités signalées comme obsolètes par [!DNL Experience Manager] 6.5.7.0. Les fonctionnalités sont initialement marquées comme obsolètes et supprimées ultérieurement dans une version ultérieure. Une autre option est fournie.

Vérifiez si vous utilisez une fonctionnalité ou une fonctionnalité dans un déploiement. En outre, envisagez de modifier la mise en oeuvre afin d’utiliser une autre option.

| Zone | Fonctionnalité | Remplacement |
|---|---|---|
| Intégrations | Le **[!UICONTROL Accord préalable des services cloud AEM]** est obsolète, car la variable [!DNL Experience Manager] et [!DNL Adobe Target] l’intégration est mise à jour dans [!DNL Experience Manager] 6.5. L’intégration prend en charge l’API Adobe Target Standard. L’API utilise l’authentification au moyen d’Adobe IMS et [!DNL Adobe I/O]. Il prend en charge le rôle croissant d’Adobe Launch pour l’instrumenter. [!DNL Experience Manager] pour les analyses et la personnalisation, l’assistant de souscription n’a aucune utilité sur le plan fonctionnel. | Configuration des connexions système, de l’authentification Adobe IMS et [!DNL Adobe I/O] intégrations via les [!DNL Experience Manager] services cloud. |
| Connecteurs | Adobe JCR Connector for Microsoft® SharePoint 2010 et Microsoft® SharePoint 2013 est obsolète pour [!DNL Experience Manager] 6.5. | S/O |

## Problèmes connus {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THE LIST.
 -->

<!-- VULNERABILITY ISSUE - REMOVED MAY 23, 2022 AND ADDED TO https://wiki.corp.adobe.com/display/DXContent/Security+and+Vulnerability+issues+for+SP+and+CFP+releases * If you are using Content Fragments and GraphQL, Adobe recommends that you install the following packages on top of 6.5.12.0:

  * [AEM 6.5.12 Sites HotFix-NPR-38144](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Faem-service-pkg-6.5.12.0-NPR-38144-B0002.zip) (this hot fix replaces SP12, but can be installed on top of SP12) -->

* [AEM du fragment de contenu avec le package d’index GraphQL 1.0.3](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.3.zip)

* As [!DNL Microsoft® Windows Server 2019] ne prend pas en charge [!DNL MySQL 5.7] et [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] ne prend pas en charge les installations clé en main pour [!DNL AEM Forms 6.5.10.0].

* Si vous effectuez une mise à niveau de votre [!DNL Experience Manager] de la version 6.5 à la version 6.5.10.0, vous pouvez afficher `RRD4JReporter` exceptions dans la variable `error.log` fichier . Pour résoudre le problème, redémarrez l’instance.

* Si vous installez [!DNL Experience Manager] 6.5 Service Pack 10 ou un Service Pack précédent sur [!DNL Experience Manager] 6.5, la copie d’exécution du modèle de workflow personnalisé de vos ressources (créé dans `/var/workflow/models/dam`) est supprimé.
Pour récupérer votre copie d’exécution, Adobe recommande de synchroniser la copie d’heure de conception du modèle de workflow personnalisé avec sa copie d’exécution à l’aide de l’API HTTP :
   `<designModelPath>/jcr:content.generate.json`.

* Les utilisateurs peuvent renommer un dossier dans une hiérarchie de [!DNL Assets] et publier un dossier imbriqué dans [!DNL Brand Portal]. Toutefois, le titre du dossier n’est pas mis à jour dans [!DNL Brand Portal] jusqu’à ce que le dossier racine soit republié.

* Lorsqu’un utilisateur choisit de configurer un champ pour la première fois dans un formulaire adaptatif, l’option permettant d’enregistrer une configuration ne s’affiche pas dans l’explorateur de propriétés. Sélectionner pour configurer un autre champ du formulaire adaptatif dans le même éditeur résout le problème.

* Les erreurs et messages d’avertissement suivants peuvent s’afficher lors de l’installation : [!DNL Experience Manager] 6.5.x.x :
   * &quot;Lorsque l’intégration Adobe Target est configurée dans [!DNL Experience Manager] l’utilisation de l’API Target Standard (authentification IMS), puis l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. Au lieu du type « Fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégat telles que SUM, MAX et MIN sont utilisées (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La zone réactive d’une image interactive Dynamic Media n’est pas visible lors de la prévisualisation de la ressource via la visionneuse de bannières Shoppable.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Délai d’attente avant que la modification du reg ne soit terminée sans enregistrement.

* Lorsque vous tentez de déplacer/supprimer/publier des fragments de contenu ou des sites/pages, un problème se produit lorsque les références aux fragments de contenu sont récupérées, car la requête en arrière-plan échoue ; c’est-à-dire que la fonctionnalité ne fonctionne pas.
Pour garantir le bon fonctionnement, vous devez ajouter les propriétés suivantes au noeud de définition d’index. `/oak:index/damAssetLucene` (aucune réindexation n’est requise) :

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## Lots OSGi et packages de contenu inclus {#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les lots OSGi et les packages de contenu inclus dans [!DNL Experience Manager] 6.5.13.0 :

* [Liste des lots OSGi inclus dans Experience Manager 6.5.13.0](/help/release-notes/assets/65130_bundles.txt)

* [Liste des packages de contenu inclus dans Experience Manager 6.5.13.0](/help/release-notes/assets/65130_packages.txt)

## Sites web à accès limité {#restricted-sites}

Ces sites web ne sont disponibles que pour les clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* [Contacter le service clientèle d’Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] page produit](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentation 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=fr)
>* [Abonnement aux mises à jour de produits prioritaires d’Adobe](https://www.adobe.com/subscription/priority-product-update.html)

