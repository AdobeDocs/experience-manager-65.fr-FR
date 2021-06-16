---
title: '[!DNL Experience Manager] Notes de mise à jour du Service Pack 6.5'
description: Notes de mise à jour spécifiques à [!DNL Adobe Experience Manager] Service Pack 9 6.5
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: 0ed031e8be43633caf6d9916542b6650e3dfd327
workflow-type: tm+mt
source-wordcount: '3857'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] Notes de mise à jour du Service Pack 6.5  {#aem-service-pack-release-notes}

## Informations sur la version {#release-information}

| Produits | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.9.0 |
| Type | Version du Service Pack |
| Date | 27 mai 2021 |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.9-1.0.zip) |

## Éléments inclus dans [!DNL Adobe Experience Manager] 6.5.9.0 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] La version 6.5.9.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les clients, ainsi que des améliorations en termes de performances, de stabilité et de sécurité, publiées depuis la version 6.5 d’avril 2019. Le Service Pack est installé sur [!DNL Adobe Experience Manager] 6.5.

Les fonctionnalités et améliorations clés introduites dans [!DNL Adobe Experience Manager] 6.5.9.0 sont les suivantes :

* [!DNL Experience Manager Sites] Le composant Dynamic Media Foundation permet désormais d’activer ou de désactiver l’optimisation pour les appareils à résolution plus élevée lors de l’utilisation d’un paramètre d’image prédéfini réactif ou d’un recadrage intelligent.

* Pour améliorer les performances, la condition hidden=false est déplacée de la requête JCR vers l’évaluateur QueryBuilder. Pour vérifier qu’un prédicat masqué fonctionne après la modification, Experience Manager vérifie que tout dossier masqué n’est pas affiché dans l’interface.

* Possibilité de restaurer les pages et l’arborescence supprimées sur une page [!DNL Experience Manager Sites].

* Prise en charge d’un nouvel utilisateur pour actualiser le jeton d’accès à l’aide d’un jeton d’actualisation pour le service de configuration des emails.

* [Prise en charge du mécanisme SMTP XOAUTH2](/help/sites-administering/notification.md#setting-up-oauth)  pour le service de configuration des emails.

* Prise en charge des versions 4.2 et 4.4 de [!DNL MongoDB].

* Les occurrences de noms liés à Hong Kong, Macao et Taïwan sont mises à jour en fonction des nouvelles conventions de dénomination pour les régions et les paramètres régionaux chinois.

* Améliorations de l’accessibilité dans [!DNL Experience Manager] [Assets](#assets-accessibility-6590) et [Dynamic Media](#accessibility-dm-6590).

* l’imagerie dynamique RGPD (rapport de pixels d’appareil) et l’optimisation de la bande passante du réseau vous permettent de diffuser des images de meilleure qualité de manière efficace ; sur les périphériques à haute résolution qui s’affichent et qui disposent d’une bande passante réseau limitée. Pour plus d’informations, voir [FAQ sur l’imagerie dynamique](/help/assets/imaging-faq.md).

   >[!NOTE]
   >
   >La date de publication des améliorations de l’imagerie dynamique ci-dessus est la suivante :
   >
   >* Amérique du Nord, le 24 mai 2021, dans l&#39;Alliance du Nord,
      >
      >
   * Europe, Moyen-Orient et Afrique, 25 juin 2021,
      >
      >
   * Asie-Pacifique 19 juillet 2021.


* Prise en charge du format d’image AVIF nouvelle génération dans la diffusion Dynamic Media (modificateur d’URL fmt). Pour plus d’informations, voir [service d’images et rendu api fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html).

   >[!NOTE]
   >
   >La date de publication de la prise en charge d’AVIF est la suivante :
   >
   >* Amérique du Nord, 10 mai 2021,
      >
      >
   * Europe, Moyen-Orient et Afrique 24 mai 2021,
      >
      >
   * Asie-Pacifique 24 juin 2021.


* Possibilité d’envoyer un email de notification à un groupe à l’aide de l’étape de workflow [!UICONTROL Assign Task].

* Possibilité de récupérer un brouillon de communication interactive après modification de la communication interactive source.

* Définissez le nom de domaine personnalisé pour le chargement, le rendu et la validation du service reCAPTCHA dans [!DNL Experience Manager Forms].

* Améliorations des données d’entrée pour l’étape de workflow [!UICONTROL Invoke Form Data Model Service].

* Possibilité d’utiliser plusieurs gabarits dans un modèle de document d’enregistrement dans [!DNL Experience Manager Forms].

* Sauts de page de prise en charge dans le document d’enregistrement de [!DNL Experience Manager Forms].

* Le référentiel intégré (Apache Jackrabbit Oak) a été mis à niveau vers la  1.22.7.

Pour obtenir la liste complète des fonctionnalités et améliorations introduites dans [!DNL Experience Manager] 6.5.9.0, voir [les nouveautés de [!DNL Adobe Experience Manager] 6.5 Service Pack 9](new-features-latest-service-pack.md).

>[!NOTE]
>
>À partir du Service Pack 9, les clients [!DNL Experience Manager] peuvent développer et exploiter leurs applications [!DNL Experience Manager] avec des distributions des [!DNL Azul Zulu] versions d’OpenJDK, conformes aux normes de Java SE.
>La prise en charge des JDK [!DNL Azul Zulu] est également fournie par Adobe aux clients [!DNL Experience Manager].
>Vous pouvez télécharger les versions appropriées des JDK [!DNL Azul Zulu] à partir de [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
>Les droits d’utilisation de la technologie Java d’Oracle, tels qu’ils sont distribués par Adobe, expireront d’ici la fin décembre 2022. [!DNL Experience Manager] Nous vous recommandons de planifier et de mettre en oeuvre l’utilisation des  [!DNL Azul Zulu] JDK au plus tard à cette date. Pour plus d’informations sur l’utilisation de la technologie [!DNL Oracle Java] et de la technologie [!DNL Azul Zulu], consultez la [FAQ](https://experienceleague.adobe.com/docs/experience-manager-65/assets/adobe-azul-openjdk-license-agreement.pdf?lang=en) associée.

Voici la liste des correctifs fournis dans la version [!DNL Experience Manager] 6.5.9.0.

### [!DNL Sites] {#sites-6590}

* Les pages publiées avec la propriété Exigence d’authentification activée ne redirigent pas vers la page de connexion et renvoient le message d’erreur 404 (NPR-36354).

* Lors de la création d’un lien hypertexte, l’option permettant de rechercher un lien ne fonctionne pas dans le composant Texte (NPR-35849).

* Une requête transversale est déclenchée lors de l’utilisation de l’API `com.day.cq.wcm.commons.ReferenceSearch`. Cela a un impact sur les performances du serveur [!DNL Experience Manager] (NPR-36407).

* Le conteneur de mises en page imbriqué à l’intérieur d’un autre conteneur de mises en page redimensionné affiche un nombre incorrect de colonnes pour ses composants enfants, de sorte que ces composants ne sont pas alignés sur la grille (NPR-36359).

* Le vérificateur de liens externes affiche les liens externes valides comme des liens non valides (NPR-36289).

* Après avoir affiché les références pendant un certain temps, le panneau Références commence à afficher un message d’erreur (NPR-36167).

* Lors du déplacement d’un composant, le système de paragraphes (parsys) créé automatiquement n’a pas le noeud `sling:resourceType` (NPR-36165).

* Lors de la synchronisation d’une Live Copy (lors de l’utilisation des configurations de déploiement [!UICONTROL Activer sur l’activation du plan directeur] et [!UICONTROL Désactiver sur l’activation du plan directeur]) si un composant est supprimé dans le gabarit de Live Copy, la synchronisation échoue et un `NullPointerException` est consigné (NPR-36127).

* Lorsqu’un utilisateur saisit du texte ad hoc pour une balise (balise qui n’existe pas sur le système) et appuie sur Entrée, la balise apparaît sous le champ, mais lorsque le fragment de contenu est enregistré et ouvert à nouveau, la balise ad hoc disparaît (NPR-36132).

* La boîte de réception n’a pas d’option pour afficher l’état des opérations asynchrones (NPR-36104).

* Un composant en double est créé après la restauration de l’héritage (NPR-36000).

* Lors de l’utilisation de la balise `RemoteContentRenderingService`, la requête à la balise `RemoteContentRendererRequestHandler.getRequest` inclut toujours la page racine de la balise `ComponentExporter`, mais n’inclut pas la page demandée si elle n’est pas incluse dans le modèle racine en fonction de la profondeur de traversée et des options de filtrage définies. La requête doit toujours inclure la page demandée afin que le SPA dispose de suffisamment d’informations pour effectuer le rendu d’une réponse (NPR-35961).

* Les éléments onTime/offTime ne s’activent pas/ne se désactivent pas sur le paramètre onTime/offTime attendu (NPR-35936).

* Lorsque vous publiez une page contenant un fragment d’expérience dépourvu de propriété `cq:lastModified`, une `NullPointerException` se produit (NPR-35914).

* Lorsque vous essayez de redimensionner un composant dans un conteneur, il n’est pas possible de redimensionner le composant à sa taille d’origine. Lorsque la taille du conteneur de composants est réduite, il n’est pas possible de redéfinir la taille sur l’original (NPR-35809).

* Dans la boîte de dialogue de déploiement, déclenchée dans l’éditeur ou à partir de l’aperçu de la Live Copy, les icônes d’état pour les pages détachées, suspendues ou non créées sont incorrectes (NPR-35691).

* Les propriétés de déploiement sur page de Multi Site Manager du gabarit ignorent la case à cocher des pages de déploiement et des sous-pages (NPR-35634).

* La fonctionnalité Restaurer l’arborescence, disponible dans l’IU classique, est absente de l’IU tactile (CQ-4315352, CQ-4309415).

* Problèmes lors de la restauration de l’héritage et du déploiement d’une page [!DNL Experience Manager Sites] (NPR-36033).

### [!DNL Assets] {#assets-6590}

[!DNL Adobe Experience Manager] La version 6.5.9.0  [!DNL Assets] corrige les problèmes suivants.

* Les balises créées à partir d’un élément de sélection de balise dans un formulaire [!UICONTROL Schéma de métadonnées de dossier] ne sont pas enregistrées (NPR-36119).

* Lorsqu’une petite ellipse est utilisée pour annoter des ressources, elle chevauche le nombre d’annotations dans la version imprimée (NPR-36114).

* En mode Colonne, dans certains cas, [!DNL Experience Manager] n’invite pas à un conflit de ressources en double lorsqu’une ressource en double est chargée (NPR-36048).

* La boîte de dialogue Partager le lien ne se ferme pas en cliquant sur le bouton Fermer si elle est ouverte et qu’aucune modification n’est apportée (NPR-36030).

* Lorsque plusieurs ressources sont sélectionnées pour mettre à jour les propriétés, une erreur se produit parfois ou les propriétés d’une ressource désélectionnée sont mises à jour (NPR-36002).

* Lors du chargement d’une ressource, des espaces sont ajoutés au début ou à la fin des noms de fichier de ressource, les caractères restants étant identiques au nom d’une ressource existante dans le référentiel, la ressource existante est remplacée sans erreur de journalisation (NPR-36001).

* Lorsque la vidéo est lue dans la page des détails de la ressource, les options de lecture et de pause ne fonctionnent pas (NPR-35999).

* Lors de l’annulation de la publication de ressources en bloc, Brand Portal génère une erreur suggérant que l’URI de demande est trop long (NPR-35954).

* Lorsqu’une ressource contenant du texte d’annotation long est imprimée, le texte d’annotation est rogné, même si de l’espace est disponible (NPR-35948).

* L’option permettant de passer à la page suivante est désactivée lors de la sélection de la page dans la vue Modèles sélectionnée sur la page Créer un catalogue (CQ-4315462).

* Lorsque le workflow de mise à jour de la ressource vidéo est démarré, la page s’actualise à plusieurs reprises (CQ-4313375).

* Les dossiers de la gestion des actifs numériques ne peuvent pas être supprimés ni déplacés et une exception est consignée (NPR-35942).

#### Améliorations dans Assets {#assets-enhancements}

* Introduction de l’option [!UICONTROL Aucune] dans la vue Carte, Colonnes et insights pour trier les ressources dans l’ordre dans lequel elles sont stockées dans le noeud JCR (NPR-36356).

* Une option est ajoutée pour ajouter l’ID d’email en minuscules dans la réponse de l’API depuis Adobe Experience Manager (CQ-4317704).

#### Améliorations de l’accessibilité dans Assets {#assets-accessibility-6590}

[!DNL Adobe Experience Manager] La version 6.5.9.0  [!DNL Assets] apporte les améliorations d’accessibilité suivantes.

Le contraste (avec l’arrière-plan) du texte et des icônes ci-dessous est amélioré, de sorte que les utilisateurs ayant une vision et une perception limitées des couleurs puissent comprendre :

* titre de la ressource sur la page [!UICONTROL Propriétés] (NPR-35967).
* icônes d’évaluation par étoiles dans les sections [!UICONTROL Évaluation] à différents endroits (NPR-36009).
* texte sur la vue de la ressource et de la carte de dossier (NPR-35966).
* texte d’espace réservé sur la vue [!UICONTROL Chronologie] (NPR-35965).
* noms de ressources dans les résultats de recherche de ressources (NPR-35964).
* texte d’espace réservé dans la boîte de dialogue [!UICONTROL Partage de lien] (NPR-35963).
* [!UICONTROL Métadonnées],  [!UICONTROL état] et   autre texte dans la   liste dans la boîte de dialogue  [!UICONTROL Afficher les ] paramètres (NPR-35910).
*  Emplacement et  [!UICONTROL type dans les textes d’] espace réservé de recherche dans la recherche globale (NPR-35909).
* développez et réduisez les icônes sous l’[!UICONTROL arborescence de contenu] (NPR-35908).
* texte [!UICONTROL Ressources] sur la page où sont affichés les dossiers de ressources (NPR-35905).
* texte dans [!UICONTROL Métadonnées de ressource], [!UICONTROL Statistiques d’utilisation] dans l’option [!UICONTROL Aperçu] de la page des détails de la ressource (NPR-35904).
* texte des raccourcis clavier pour les options [!UICONTROL properties] et [!UICONTROL edit] dans la page des détails de la ressource (NPR-35904).

### [!DNL Dynamic Media] {#dynamic-media-6590}

Adobe Experience Manager 6.5.9.0 Assets résout les problèmes suivants dans [!DNL Dynamic Media] :

* Les paramètres de visionneuse prédéfinis et CSS personnalisés ne sont pas répliqués vers [!DNL Dynamic Media] lorsque [!DNL Dynamic Media] est activé de manière sélective et désactivé par [default](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/config-dm.html?lang=en#troubleshoot-dm-config) (NPR-36232).

* Lors de la tentative de prévisualisation de rendus vidéo sur la page des détails de la ressource, le chargement des vidéos est lent (CQ-4320122).

* La page du navigateur ne répond plus et ralentit le chargement de plus de 200 ressources avec l’option Dupliquer le détecteur de ressources activée (CQ-4319633).

* Lorsqu’une ressource d’image panoramique est ajoutée au composant de média panoramique sur une page, une erreur de référence non interceptée est consignée (CQ-4317666).

* Lorsque la visionneuse de médias interactifs est implémentée avec le fragment d’expérience, le fragment d’expérience n’est pas ouvert à partir de l’éditeur et une erreur est consignée (CQ-4317655).

* L’option Publier sur Dynamic Media n’est pas disponible dans Publication rapide dans la vue de l’éditeur de métadonnées (CQ-4317199).

* Les auteurs de site disposant d’autorisations en lecture seule peuvent utiliser la fonctionnalité de recadrage intelligent sur les ressources et modifier les rendus recadrés intelligents. Toutefois, les utilisateurs disposant d’autorisations de lecture seule ne doivent pas être en mesure de modifier les propriétés des ressources dans l’instance de développement Sites (CQ-4316450).

* Les annotations vidéo ne fonctionnent pas pour les chemins d’accès aux dossiers [!DNL where Dynamic] La configuration du média n’est pas activée, même si l’instance [!DNL Experience Manager] est configurée en mode [!DNL Dynamic Media] (CQ-4314950).

* Lorsque le titre des ressources comporte deux octets, plusieurs octets, ASCII élevé, cyrillique, deux paires de substitution, hébreu, arabe et GB18030, puis lors de la publication sur Dynamic Media, le titre de la ressource comporte un point d’interrogation (?) (CQ-4311872).

#### Améliorations de l’accessibilité dans Dynamic Media {#accessibility-dm-6590}

[!DNL Adobe Experience Manager] La version 6.5.9.0  [!DNL Assets] apporte les améliorations d’accessibilité suivantes à  [!DNL Dynamic Media].

* Lorsque vous ouvrez la boîte de dialogue pour ajouter des ressources à l’aide des touches du clavier dans l’éditeur de visionneuse d’images :
   * les lecteurs d’écran indiquent que la boîte de dialogue est ouverte.
   * la sélection au clavier se déplace vers la boîte de dialogue à l’ouverture.
   * lorsque la boîte de dialogue est fermée (CQ-4312134), la sélection du clavier revient à l’option Ajouter une ressource.

* Vous pouvez désormais ajouter et modifier des zones réactives sur des ressources à l’aide des touches du clavier dans l’éditeur de zones réactives (CQ-4305965).

* Vous pouvez désormais placer un lien hypertexte sur une zone réactive à l’aide des touches du clavier. Le lecteur d’écran sélectionné se déplace désormais vers le champ pour modifier le chemin de l’URL et l’option Ouvrir la boîte de dialogue de sélection (CQ-4290735).

* Le contraste (avec l’arrière-plan) du texte et des contrôles sur la page de l’éditeur de visionneuse d’images est amélioré, de sorte que les utilisateurs ayant une vision et une perception limitées des couleurs puissent comprendre (CQ-4290733).

* Vous pouvez désormais accéder aux options de partage de ressources dans l’éditeur de paramètres prédéfinis de la visionneuse et réduire l’option de partage développée à l’aide des touches du clavier (CQ-4290724).

* Vous pouvez désormais parcourir et afficher des info-bulles sur les icônes d’information et d’alerte dans les onglets De base et Avancé de la page Modifier le codage vidéo à l’aide des touches du clavier (CQ-4290722).

* Les lecteurs d’écran indiquent maintenant les instructions pour divers champs dans les onglets Apparence et Comportement de l’éditeur de paramètres prédéfinis de la visionneuse (CQ-4290721).

* Lors de la navigation dans la page Modifier le paramètre d’image prédéfini en mode Formulaire, le lecteur d’écran indique l’objectif et le nom des différents champs et contrôles (CQ-4290717).

* Lors de la navigation dans la page des détails des ressources, les lecteurs d’écran décrivent désormais l’objectif de diverses options dans les visionneuses (CQ-4290716).

* Le contraste (avec l’arrière-plan) du texte d’espace réservé L’option Tous les rendus de la page Rendus des détails de la ressource est améliorée, de sorte que les utilisateurs ayant une vision et une perception limitées de la couleur puissent comprendre (CQ-4290713).

* L’astérisque visuel pour désigner le champ obligatoire est désormais fourni dans le champ Titre de la ressource dans l’éditeur de visionneuse d’images, et les lecteurs d’écran annoncent les informations requises pour le champ (CQ-4290712).

* Les lecteurs d’écran peuvent désormais accéder à diverses options interactives et les décrire dans la page des détails de la ressource (CQ-4290708) des visionneuses.

### Plate-forme {#platform-6590}

* Lorsque vous générez une miniature pour un plan directeur et déployez les modifications sur la Live Copy, l’héritage de certains champs ne fonctionne pas (CQ-4319517).

* Lorsque vous créez un dossier, sélectionnez la propriété Orderable, puis ajoutez plus de 20 ressources au dossier. La sélection de toutes les ressources du dossier affiche un nombre incorrect (CQ-4316243).

* Lorsque vous actualisez une page, le tri des dossiers ou des ressources n’affiche pas les résultats appropriés (CQ-4316200).

* La bibliothèque JavaScript Handlebars est mise à niveau vers la version 4.7.7 (NPR-36375).

* Les lots personnalisés ne sont pas mis à jour lors de l’installation d’un nouveau module de code à l’aide de Package Manager (NPR-35949).

* Un lot `resourceresolver` Sling entraîne l’échec de la requête `Sling:alias` (NPR-35335).

* Le chemin d’accès au contexte est supprimé lors de la configuration de SSL en Experience Manager (NPR-35294).

* L’exception `SegmentNotFound` est renvoyée après une session longue (NPR-36405).

### Intégrations {#integrations-6590}

* Impossible d’enregistrer les propriétés de page avec l’héritage activé pour les fragments d’expérience Cloud Services (NPR-36107).

* La pagination et le chargement différé de l’interface utilisateur IMS n’affichent pas les résultats appropriés (NPR-36046).

* Lorsque vous créez une configuration A4T Target et que vous sélectionnez la source de création de rapports [!DNL Adobe Analytics], aucune suite de rapports compatible Adobe Target n’est disponible dans la liste déroulante (NPR-36006).

### Projets {#projects-6590}

* Impossible d’enregistrer les propriétés d’un projet, car le chemin JCR vers le projet n’est pas résolu en raison d’une barre oblique (`/`) supplémentaire ajoutée au chemin du projet (NPR-36191).

### Screens {#screens-6590}

* [!DNL Experience Manager Screens] les lecteurs ne peuvent pas s’authentifier si un gestionnaire d’authentification personnalisé à deux facteurs est utilisé (NPR-35854).

### Commerce {#commerce-6590}

* L’assistant [!UICONTROL Catalogue commercial] ne parvient pas à charger plus de 40 éléments dans le mode Colonnes (CQ-4318379).

### Projets de traduction {#translation-6590}

* Les options de mise à jour ou de remplacement ne s’affichent pas lors de la retraduction d’une page `es` en `es_es` (NPR-36170).

* Lorsque l’option d’approbation automatique est sélectionnée pour un projet avec traduction humaine, l’état de la tâche s’affiche sous la forme `Unknown` (NPR-35981).

* Lorsque vous traduisez une page, le chemin de référence de [!DNL Experience Fragments] ne se met pas à jour vers le chemin de référence de destination [!DNL Experience Fragment] (NPR-35911).

* Lorsque vous apportez des modifications aux pages parents et enfants et que vous envoyez la page parente pour traduction, les pages enfants sont également mal traduites (NPR-35896).

* Lorsqu’il existe plusieurs projets de traduction simultanés pour une page sélectionnée, l’option [!UICONTROL Aller aux projets] ne renvoie pas au dernier projet de traduction (NPR-35454).

* Lorsque vous publiez des ressources dans [!DNL Dynamic Media], [!DNL Experience Manager] affiche un message incorrect pour les balises non publiées (CQ-4315914, CQ-4315913).

* Lorsque vous ouvrez une tâche supprimée, [!DNL Experience Manager] affiche un message incorrect (CQ-4315910).

### Workflow {#workflow-6590}

* Lorsque vous cliquez sur Terminer, Déléguer ou Ouvrir des actions pour les éléments disponibles dans la boîte de réception, il n’existe aucune indice visuel pour que ces actions soient terminées (NPR-36317).

### [!DNL Communities] {#communities-6590}

* Dans le filtrage des messages indésirables, le système consomme 100 % de l’espace de tas Java, ce qui rend le serveur de Experience Manager inréactif (NPR-36316, NPR-36493).
* Dans les forums, les données des sessions JCR provenant de `SearchCommentSocialComponentListProvider` sont divulguées (NPR-36235).
* L’ouverture d’un message de boîte de réception spécifique reflète tous les messages présentant une pagination incorrecte et d’autres problèmes (NPR-35917).

### [!DNL Brand Portal] {#brandportal-6590}

* L’indicateur de la fonctionnalité d’approvisionnement des ressources est activé automatiquement lors de la configuration de [!DNL Experience Manager Assets] avec [!DNL Brand Portal] (NPR-36010).

### [!DNL Forms] {#forms-6590}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] publie les packages de modules complémentaires une semaine après la date de publication prévue du Service Pack [!DNL Experience Manager].
>* Vous pouvez désormais développer et exploiter des applications avec des [!DNL Azul Zulu] versions de [!DNL OpenJDK] pour [!DNL Experience Manager Forms] sur des déploiements OSGi.


**Formulaires adaptatifs**

* Problèmes d’initialisation de langue dans [!DNL Experience Manager Forms] 6.5.7.0 lors de la génération de plusieurs dictionnaires de traduction (NPR-36439).
* Lorsque vous ajoutez une pièce jointe au fragment de formulaire adaptatif et envoyez le formulaire, [!DNL Experience Manager Forms] affiche le message d’erreur suivant (NPR-36195) :

   ```TXT
    POST /content/forms/af/attachmentissue/jcr:content/guideContainer.af.submit.jsp HTTP/1.1] com.adobe.aemds.guide.servlet.GuideSubmitServlet [AF] Invalid file name or mime type for file resulted in submission failure
   ```

* Lorsque vous utilisez la traduction humaine pour mettre à jour un dictionnaire, puis prévisualiser un formulaire adaptatif, les modifications ne s’affichent pas (NPR-36035).

**Communications interactives**

* Lorsque vous chargez une image à l’aide du canal d’impression des communications interactives et la modifiez, elle n’est plus visible (NPR-36518).

* Lors de la modification d’une ressource de texte et du remplissage d’un espace réservé, tous les éléments interactifs sont supprimés du volet de navigation (NPR-35991).

**Processus**

* Lorsque vous appelez le point de terminaison REST d’un service [!DNL Experience Manager Forms] sur JBoss, [!DNL Experience Manager] affiche le message d’erreur suivant (NPR-36305) :

   ```TXT
   Invalid input. The maximum length of 2000 characters was exceeded.
   ```

**BackendIntegration**

* Impossible d’enregistrer un modèle de données de formulaire lors de la liaison de l’argument de service de lecture à une valeur littérale contenant un tiret (NPR-36366).

**Document Security**

* Lorsque vous définissez la certification et HSM pour GlobalSign, [!DNL Experience Manager Forms] affiche les messages d’erreur `Unsuported Algorithm` et `Invalid TSA Certificate` lors de l’ajout d’un horodatage à LTV (NPR-36026, NPR-36025).

**Services de document**

* Mises à jour de la bibliothèque [!DNL Gibson] pour l’intégration à [!DNL Experience Manager Forms] (NPR-36211).

**Foundation JEE**

* Lorsque vous sélectionnez Gestion des points de fin dans l’interface utilisateur d’administration, [!DNL Experience Manager Forms] affiche le message d’erreur `endpoint registry failure` (CQ-4320249).

Pour plus d’informations sur les mises à jour de sécurité, voir [[!DNL Experience Manager] page des bulletins de sécurité](https://helpx.adobe.com/security/products/experience-manager.html).

## Installation de la version 6.5.9.0 {#install}

**Configuration des exigences et informations supplémentaires**

* Experience Manager 6.5.9.0 nécessite Experience Manager 6.5. Voir la [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour obtenir des instructions détaillées.
* Le téléchargement du Service Pack est disponible sur l’Adobe [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Sur un déploiement avec MongoDB et plusieurs instances, installez Experience Manager 6.5.9.0 sur l’une des instances d’auteur à l’aide du gestionnaire de modules.

>[!NOTE]
>
>Adobe ne recommande pas de supprimer ou de désinstaller le package [!DNL Adobe Experience Manager] 6.5.9.0.

### Installer le Service Pack {#install-service-pack}

Pour installer le Service Pack sur une instance [!DNL Adobe Experience Manager] 6.5, procédez comme suit :

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (et c’est le cas lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande également un redémarrage si le temps de disponibilité actuel d’une instance est élevé.

1. Avant l’installation, prenez un instantané ou une nouvelle sauvegarde de votre instance [!DNL Experience Manager].

1. Téléchargez le Service Pack à partir de [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.9-1.0.zip).

1. Ouvrez Package Manager et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package. Pour en savoir plus, voir [Gestionnaire de modules](/help/sites-administering/package-manager.md).

1. Sélectionnez le package et cliquez sur **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du Service Pack, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Voir [Entrepôt de données Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface utilisateur de Package Manager se ferme parfois pendant l’installation du Service Pack. Adobe recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les logs spécifiques liés à la désinstallation du lot de mise à jour avant de vous assurer que les installations sont réussies. En règle générale, cela se produit sur [!DNL Safari] mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Il existe deux manières d’installer automatiquement [!DNL Experience Manager] 6.5.9.0 sur une instance de travail :

A. Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.

B. Utilisez l’API [HTTP du gestionnaire de modules](/help/sites-administering/package-manager.md#package-share). Utilisez `cmd=install&recursive=true` pour que les packages imbriqués soient installés.

>[!NOTE]
>
>Adobe Experience Manager 6.5.9.0 ne prend pas en charge l’installation de Bootstrap.

**Validation de l’installation**

1. La page d’informations sur les produits (`/system/console/productinfo`) affiche la chaîne de version mise à jour `Adobe Experience Manager (6.5.9.0)` sous [!UICONTROL Produits installés].

1. Tous les lots OSGi sont **[!UICONTROL PRINCIPAL]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (utiliser la console web : `/system/console/bundles`).

1. Le lot OSGi `org.apache.jackrabbit.oak-core` est version 1.22.3 ou ultérieure (Utiliser la console web : `/system/console/bundles`).

Pour connaître les plates-formes certifiées pour fonctionner avec cette version, voir les [exigences techniques](/help/sites-deploying/technical-requirements.md).

### Installer le module complémentaire Adobe Experience Manager Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Ignorez si vous n’utilisez pas Experience Manager Forms. Les correctifs dans Experience Manager Forms sont fournis par le biais d’un module complémentaire distinct une semaine après la publication du Service Pack [!DNL Experience Manager] planifiée.

1. Vérifiez que vous avez installé le Service Pack Adobe Experience Manager.
1. Téléchargez le module complémentaire Forms correspondant répertorié dans les [versions AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#forms-updates) pour votre système d’exploitation.
1. Installez le module complémentaire Forms comme décrit dans [Installation des modules complémentaires AEM Forms](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>AEM 6.5.9.0 comprend une nouvelle version du [package de compatibilité AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases). Si vous utilisez une ancienne version du package de compatibilité AEM Forms et que vous mettez à jour vers AEM 6.5.9.0, installez la dernière version du package après l’installation du package du module complémentaire Forms.

### Installation d’Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Passez cette étape si vous n’utilisez pas AEM Forms sous JEE. Les correctifs d’Adobe Experience Manager Forms on JEE sont fournis via un programme d’installation distinct.

Pour plus d’informations sur l’installation du programme d’installation cumulatif pour Experience Manager Forms on JEE et la configuration après le déploiement, consultez les [notes de mise à jour](jee-patch-installer-65.md).

>[!NOTE]
>
>Après avoir installé le programme d’installation cumulatif pour Experience Manager Forms on JEE, installez le dernier module complémentaire Forms, supprimez le module complémentaire Forms du dossier `crx-repository\install` et redémarrez le serveur.

### UberJar {#uber-jar}

UberJar pour Experience Manager 6.5.9.0 est disponible dans le [référentiel central Maven](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.9/).

Pour utiliser UberJar dans un projet Maven, voir [Comment utiliser UberJar](/help/sites-developing/ht-projects-maven.md) et inclure la dépendance suivante dans le POM de votre projet :

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.9</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar et les autres artefacts associés sont disponibles sur le référentiel central Maven au lieu du référentiel Maven public Maven Adobe (`repo.adobe.com`). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Il n’existe donc pas de `classifier`, avec `apis` comme valeur, pour la balise `dependency`.

## Fonctionnalités obsolètes {#removed-deprecated-features}

Vous trouverez ci-dessous une liste des fonctionnalités marquées comme obsolètes avec la version [!DNL Experience Manager] 6.5.7.0. Les fonctionnalités sont marquées comme obsolètes initialement et supprimées ultérieurement dans une version ultérieure. Une autre option est généralement fournie.

Vérifiez si vous utilisez une fonctionnalité ou une fonctionnalité dans un déploiement. En outre, envisagez de modifier la mise en oeuvre afin d’utiliser une autre option.

| Zone | Fonctionnalité | Remplacement |
|---|---|---|
| Intégrations | L’écran **[!UICONTROL Opt-in des services cloud AEM]** est obsolète. L’intégration de Experience Manager et Adobe Target ayant été mise à jour dans Experience Manager 6.5 afin de prendre en charge l’API Adobe Target Standard, qui utilise l’authentification via l’Adobe IMS et [!DNL Adobe I/O], et le rôle croissant d’Adobe Launch pour l’instrumentalisation de pages de Experience Manager pour l’analyse et la personnalisation, l’assistant de souscription est devenu non pertinent du point de vue fonctionnel. | Configurez les connexions système, l’authentification IMS par Adobe et les intégrations [!DNL Adobe I/O] via les services cloud [!DNL Experience Manager] respectifs. |
| Connecteurs | Adobe JCR Connector for Microsoft SharePoint 2010 et Microsoft SharePoint 2013 est obsolète pour Experience Manager 6.5. | N/A |

## Problèmes connus {#known-issues}

* Si vous mettez à niveau votre instance [!DNL Experience Manager] de la version 6.5 vers la version 6.5.9.0, vous pouvez afficher les exceptions `RRD4JReporter` dans le fichier `error.log`. Redémarrez l’instance pour résoudre le problème.

* Si vous installez [!DNL Experience Manager] 6.5 Service Pack 5 ou un Service Pack précédent sur [!DNL Experience Manager] 6.5, la copie d’exécution du modèle de workflow personnalisé de vos ressources (créée dans `/var/workflow/models/dam`) est supprimée.
Pour récupérer votre copie d’exécution, Adobe recommande de synchroniser la copie d’heure de conception du modèle de workflow personnalisé avec sa copie d’exécution à l’aide de l’API HTTP :
   `<designModelPath>/jcr:content.generate.json`.

* Si un dossier de la hiérarchie est renommé [!DNL Assets] et qu’un dossier imbriqué contenant une ressource est publié sur [!DNL Brand Portal], le titre du dossier n’est pas mis à jour dans [!DNL Brand Portal] tant que le dossier racine n’a pas été republié.

* Lorsqu’un utilisateur choisit de configurer un champ pour la première fois dans un formulaire adaptatif, l’option permettant d’enregistrer une configuration ne s’affiche pas dans l’explorateur de propriétés. Sélectionner pour configurer un autre champ du formulaire adaptatif dans le même éditeur résout le problème.

* Les erreurs et messages d’avertissement suivants peuvent s’afficher lors de l’installation de Experience Manager 6.5.x.x :
   * &quot;Lorsque l’intégration d’Adobe Target est configurée dans Experience Manager à l’aide de l’API Target Standard (authentification IMS), l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. Au lieu du type « Fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégat telles que SUM, MAX et MIN sont utilisées (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La zone réactive d’une image interactive Dynamic Media n’est pas visible lors de la prévisualisation de la ressource via la visionneuse de bannières Shoppable.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Délai d’attente avant que la modification du reg ne soit terminée sans enregistrement.

## Lots OSGi et packages de contenu {#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les lots OSGi et les packages de contenu inclus dans [!DNL Experience Manager] 6.5.9.0 :

* [Liste des lots OSGi inclus dans Experience Manager 6.5.9.0](assets/6590_bundles.txt)

* [Liste des packages de contenu inclus dans Experience Manager 6.5.9.0](assets/6590_packages.txt)

## Sites Web restreints {#restricted-sites}

Ces sites web ne sont disponibles que pour les clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* Voir [Comment contacter l’assistance clientèle d’Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] Notes de mise à jour de la version 6.5](/help/release-notes/release-notes.md)
* [[!DNL Experience Manager] page produit](https://www.adobe.com/fr/marketing/experience-manager.html)
* [[!DNL Experience Manager] Documentation 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=fr)
* [Abonnement aux mises à jour de produits prioritaires d’Adobe](https://www.adobe.com/subscription/priority-product-update.html)

