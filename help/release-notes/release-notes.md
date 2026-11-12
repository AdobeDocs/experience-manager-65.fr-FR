---
title: Notes de mise à jour de [!DNL Adobe Experience Manager] 6.5
description: Consultez les informations sur la mise à jour, y compris les nouveautés, la procédure d’installation et une liste complète des modifications pour [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
contentOwner: Rick Brough
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: ed762d86-a04b-452b-a08f-86359bb8ff27
    internal-label: Configuration and operations
subfeature_v2:
  - id: c21ccc2b-e0c8-4853-bf41-f12259ed93f8
    internal-label: Release information
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 56b13809475a59f188750b86503e316e69171fe1
workflow-type: tm+mt
source-wordcount: '7273'
ht-degree: 15%
---
# Notes de mise à jour du dernier pack de services [!DNL Adobe Experience Manager] 6.5 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!--
DO NOT DELETE THIS HIDDEN NOTE!      DO NOT DELETE THIS HIDDEN NOTE!
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, May 29, 2025. In addition, a list of Forms fixes and enhancements is added to this section.
-->

## Résumé de la version {#release-information}

| Produit | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.26.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Type | Mise à jour du pack de services |
| Date | 12 Novembre 2026 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |


<!-- REWRITE AI GENERATED SUMMARY OF NOTES BELOW FOR EACH NEW SERVICE PACK RELEASE -->

Experience Manager 6.5.26.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les clients et les clientes, ainsi que des correctifs de bugs. Elle comprend également des améliorations en matière d’accessibilité, de localisation, de performances, de stabilité et de sécurité, reposant sur la version 6.5 Foundation disponible depuis avril 2019.

Les principaux points forts du pack de services 26 sont les suivants :

* Sécurité. Deux correctifs critiques permettent de corriger une vulnérabilité d’injection de modèle côté serveur dans l’éditeur de métadonnées et des violations de script entre sites (XSS) dans les servlets de l’interface utilisateur Coral.
* Conformité C2PA. Assets détecte désormais les informations d’identification C2PA et signe les rendus générés par le workflow Ressource de mise à jour . La signature s’exécute localement dans chaque instance et l’infrastructure de signature dédiée ou appartenant au client n’est pas prise en charge.
* Accessibilité. Plus de 25 correctifs permettent à l’éditeur de page et à la console Sites de répondre aux exigences de contraste WCAG, de clavier et de lecteur d’écran.
* Localisation. Des dizaines de correctifs traduisent les chaînes et corrigent les problèmes de mise en page sur Sites, Assets, Security et Operations.
* Fiabilité. Correction des conflits de verrouillage GraphQL sur les instances de publication, les déploiements MSM, les actions de la barre d’outils de l’éditeur de texte enrichi et l’activation de pages dans l’interface utilisateur classique.
* Analytics. L’intégration de Launch utilise l’API Adobe Analytics 2.0 avant la fin de vie d’Analytics 1.4 le 31 août 2026.


<!-- UPDATE FOR EACH NEW RELEASE -->

## Correction de problèmes, d’améliorations et d’améliorations apportées au pack de services 26 d’ {#fixed-issues}

<!-- 6.5.25.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE? -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->


### [!DNL Sites]{#sites-6526}

#### Accessibilité {#sites-accessibility-6526}

* Les auteurs peuvent ajouter, déplacer et supprimer des composants à l’aide du clavier uniquement. L’interaction glisser-déposer nécessitait un pointeur, elle a donc échoué avec le critère Clavier WCAG 2.1.1 . L’éditeur fournit désormais les composants Insérer pop-up, Couper et coller et Supprimer comme équivalents au clavier. (SITES-25359)

* Les auteurs peuvent désormais voir le bouton Format actif (« T ») dans le menu intégré du composant Texte . Une fois que les créateurs et créatrices ont appliqué une mise en forme gras ou italique, l’icône du bouton est restée sombre sur un arrière-plan gris foncé et n’a pas atteint le rapport de contraste minimum de 4,5:1 AA WCAG 2.1. Le CSS mis à jour allège l’icône, ce qui restaure le contraste fourni par les packs de services précédents. (SITES-51864)

* L’onglet Assets de l’éditeur de page affiche désormais une chaîne traduite dans le menu déroulant Sélectionner les composants une fois que vous avez choisi Paragraphes dans le menu déroulant Images . Auparavant, la chaîne « OTHER » s’affichait en anglais, car elle manquait aux ressources de localisation. Le dictionnaire mis à jour fournit la traduction dans tous les paramètres régionaux. (SITES-24525)




* L’iframe ContextHub dans l’éditeur de page dispose désormais d’un attribut de titre descriptif. Auparavant, l’élément `contexthub-ui-iframe` n’avait pas de titre. Par conséquent, les utilisateurs d’un lecteur d’écran ne l’ont pas identifié lorsque le focus s’est déplacé vers celui-ci. Le titre apparaît désormais sur chaque page et affichage de l’éditeur, y compris la zone de travail, le rail latéral et l’aperçu de la disposition. (SITES-24650)
* Le bouton Filtres du rail de filtres de la console Sites n’ajoute pas de libellés visibles au-dessus des champs Recherches enregistrées et Sélectionner le répertoire de recherche . Un audit a révélé que les libellés s’affichaient lorsque le focus quittait le bouton, lorsqu’une touche était enfoncée ou lorsque l’utilisateur cliquait sur le bouton. Les tests n’ont pas permis de reproduire le comportement, aucune modification n’a donc été nécessaire. (SITES-24706)
* Les liens dans la console Sites de navigation de l’application se démarquent désormais plus clairement. Le texte du lien répondait au rapport de contraste de 4,5:1, mais l’épaisseur réduite de la police et la petite taille rendaient les liens difficiles à voir. Un poids de police plus élevé et une taille plus grande facilitent la lecture du texte pour les utilisateurs ayant une déficience visuelle. (SITES-24723)
* Les lecteurs d’écran n’annoncent plus « vide » avant le contenu de l’info-bulle dans la boîte de dialogue modale Préférences utilisateur. Auparavant, l’icône d’informations utilisait `role="tooltip"` avec une référence `aria-labelledby`. NVDA lisait donc d’abord un libellé vide. L’icône utilise désormais `role="button"` et un `aria-label` d’« informations », et la modification s’applique aux composants de formulaire Coral qui partagent le modèle. (SITES-24732)
* Le bouton Supprimer de la boîte de dialogue modale Supprimer répond désormais à l’exigence de contraste de 4.5:1 du WCAG 1.4.3. Auparavant, le texte blanc sur arrière-plan rouge donnait un rapport de 3,9:1 une fois que les auteurs avaient sélectionné un élément et cliqué sur Supprimer dans la barre d’outils Action. La couleur plus foncée du bouton rend le libellé lisible par les auteurs ayant une déficience visuelle. (SITES-24772)
* L’en-tête Références du rail Références de la console Sites utilise désormais un élément d’en-tête au lieu d’un `div`. Auparavant, les lecteurs d’écran ne pouvaient pas annoncer le texte comme en-tête, de sorte que les utilisateurs ne pouvaient pas naviguer par en-têtes. L’en-tête s’affiche également en haut de la vue des références initiale. (SITES-24967)
* L’indicateur de focus des boutons d’accordéon dans le rail de filtre de la console Sites répond désormais à l’exigence de contraste de la version 3:1 de WCAG 1.4.11. Auparavant, l’indicateur bleu affichait un rapport de 2,3:1 en arrière-plan, ce qui rendait difficile la recherche du bouton d’accordéon Balises pour les utilisateurs d’un clavier. La couleur mise à jour donne aux utilisateurs du clavier une indication de mise au point claire. (SITES-24986)
* L’indicateur de focus des boutons radio dans le rail de filtrage de la console Sites répond désormais à l’exigence de contraste de la version 3:1 de WCAG 1.4.11. Auparavant, l&#39;indicateur bleu clair affichait un rapport de 1,7:1 sur le fond. Les utilisateurs du clavier peuvent désormais suivre leur position dans l’accordéon Date de modification . (SITES-24987)
* Le bouton Sélectionner en regard des champs Chemin d’accès et Balises dans le rail latéral de l’éditeur de page n’utilise plus d’icône de case à cocher. Auparavant, l’icône suggérait un bouton (bascule), mais l’activation du bouton a ouvert une boîte de dialogue modale contenant l’annuaire d’arborescences. Le bouton Sélectionner communique désormais correctement sa fonction, de même que les modèles Image et Teaser . (SITES-25210)
* Les lecteurs d’écran ignorent désormais les miniatures des ressources dans le rail latéral de l’éditeur de page. Auparavant, chaque image comportait un texte secondaire qui dupliquait le nom de la ressource visible. Les utilisateurs entendaient donc le même texte deux fois. Un attribut `alt` vide marque l’image comme décorative et conserve le nom dans le titre de la carte. (SITES-25213)
* Les lecteurs d’écran reconnaissent la liste Composants du rail latéral sous la forme d’une liste. Un audit a signalé les éléments comme n’étant pas liés, mais les tests ont confirmé que le balisage utilise un élément de liste et des éléments de liste. Aucun changement de code n’était nécessaire. (SITES-25214)
* Les icônes d’informations des composants dans le rail latéral de l’éditeur de page sont plus grandes et plus faciles à voir. Auparavant, les icônes utilisaient la taille très réduite d’environ 12 px, que les utilisateurs ayant une déficience visuelle avaient du mal à voir. Les icônes utilisent désormais la taille moyenne.(SITES-25217)
* L’indicateur de focus sur le bouton Échantillon dans la boîte de dialogue modale d’annotation se distingue désormais du bouton. Auparavant, l’indicateur correspondait à la couleur d’échantillon. Il était donc difficile pour les utilisateurs d’un clavier de voir quel bouton avait le focus. Un décalage donne à l&#39;indicateur un contraste suffisant par rapport à l&#39;arrière-plan et le rend clairement visible. (SITES-25253)
* Le champ Date de la fenêtre modale Timewarp ne contient plus `aria-haspopup="dialog"`. Auparavant, les lecteurs d’écran annonçaient que le champ ouvrait une boîte de dialogue, même si ce n’est pas le cas. La suppression de l’attribut donne aux utilisateurs de lecteurs d’écran des informations précises. (SITES-25263)
* Les libellés de texte de la barre d’outils Démographie, tels que « Recommandé », répondent désormais à l’exigence de contraste de WCAG 1.4.3 de 4,5:1. Auparavant, le texte gris sur un arrière-plan gris foncé donnait un rapport de 2,8:1 en mode Aperçu. Le texte plus foncé ou plus clair, selon l’arrière-plan, rend chaque étiquette lisible. (SITES-25307)
* L’indicateur de focus sur les boutons Commerce, Persona et Appareil de la barre d’outils Démographie répond désormais à l’exigence de contraste de la version 3:1 du WCAG 1.4.11. Auparavant, l’indicateur affichait un rapport de 1,9:1 par rapport à l’arrière-plan de la barre d’outils. Utilisez le clavier pour suivre leur position. (SITES-25308)
* Le texte que les auteurs saisissent dans les champs de texte de la barre d’outils Démographie répond désormais à l’exigence de contraste de WCAG 1.4.3 de 4.5:1. Auparavant, le texte blanc sur arrière-plan gris produisait un rapport de 2,9:1 dans les champs, tels que le champ `displayName` de la liste déroulante Profil en mode Aperçu. Les couleurs mises à jour rendent les valeurs saisies lisibles pour les auteurs ayant une déficience visuelle. (SITES-25318)
* Les lecteurs d’écran lisent désormais l’info-bulle de description lorsque le focus atteint les cases à cocher dans les boîtes de dialogue Teaser, Image et Carrousel. Auparavant, le texte n’était pas associé par programmation à la case à cocher, de sorte que les utilisateurs ne pouvaient pas entendre l’instruction. Un attribut `aria-describedby` lie désormais chaque case à cocher à sa description. (SITES-25364)
* Les lecteurs d’écran indiquent désormais quel bouton Formats de paragraphe est actif dans l’éditeur de texte enrichi. Auparavant, la sélection d’une option dans la liste ne donnait aucune indication sur le choix actuel pour la technologie d’assistance. Le bouton actif contient désormais `aria-current="true"`, et l’option Cible de l’hyperlien actif contient `aria-selected="true"`. (SITES-25367)
* Les boutons Trier dans l’en-tête du tableau de la vue Liste de la console Sites répondent désormais à l’exigence de contraste de la version 3:1 du WCAG 1.4.11. Auparavant, les icônes gris clair affichaient un rapport de 1,5:1 sur l’arrière-plan de l’en-tête. La couleur plus foncée de l’icône rend les boutons visibles par les créateurs et créatrices ayant une déficience visuelle. (SITES-25372)
* L’onglet Assets du rail latéral de l’éditeur de page ne se recharge plus lorsque le focus se déplace vers le champ Filtre . Auparavant, le fait de tabuler dans le champ vide déclenchait un rechargement et les lecteurs d’écran annonçaient un message de chargement à chaque fois. L’onglet se recharge uniquement après avoir modifié la valeur du filtre et appuyé sur Entrée. (SITES-25377)
* L’icône d’échantillon sélectionnée dans la boîte de dialogue modale d’annotation répond désormais à l’exigence de contraste de 3:1 de WCAG 1.4.11. Auparavant, la coche blanche affichait un rapport aussi faible que 1,58:1 par rapport aux échantillons jaunes, orange et verts. L’icône mise à jour fournit aux auteurs ayant une déficience visuelle un indicateur clair. (SITES-25523)
* La liste Composants du panneau latéral de l’éditeur de page n’utilise plus le focus du clavier. Utiliser un clavier pour sélectionner et déplacer des composants avec les commandes de la fenêtre de contenu ; la liste du panneau latéral a donc répété la fonction. Une note sous le filtre de composant indique aux utilisateurs du clavier où trouver les commandes. (SITES-40752)


#### Interface d’utilisation d’administration{#sites-adminui-6526}


#### Interface utilisateur classique{#sites-classicui-6526}

* Les auteurs peuvent de nouveau activer des pages dans la console Sites de l’interface utilisateur classique (`siteadmin.html`). Auparavant, le bouton Activer la page affichait indéfiniment une double flèche « Chargement » et ne déclenchait jamais de réplication, car un script de suivi ayant échoué arrêtait le gestionnaire de clics. Le gestionnaire de clics s’exécute maintenant sans erreur et termine l’activation. (SITES-52165)
* Le code de langue indonésien s’affiche désormais sous la forme d’un ID dans les propriétés de copie de la langue. Auparavant, le rail Références affichait l’ancien code IN pour les pages sous la racine de langue indonésienne. La mise à jour du lot cq-wcm-core corrige la valeur afin que le code corresponde à la norme ISO. (SITES-4491)

<!--
#### Component Console{#sites-component-console-6526}



#### [!DNL Content Fragments]{#sites-contentfragments-6526}



#### [!DNL Content Fragments] - Admin{#sites-admin-6526}
-->


#### [!DNL Content Fragments] - Éditeur De Fragments{#sites-fragments-editor-6526}

* Le bouton Modifier le fragment de contenu s’affiche immédiatement pour chaque référence à plusieurs champs dans l’éditeur de fragment de contenu. Auparavant, le bouton restait masqué jusqu’à ce que les auteurs enregistrent le fragment parent, et il n’agissait pas après l’ouverture de l’explorateur de chemins d’accès. L’éditeur crée désormais la liste d’actions lors du premier rendu, de sorte que les auteurs ouvrent les fragments référencés sans étapes supplémentaires. (SITES-43733)

* Les caractères chinois, japonais et coréens ne s’affichent plus en italique dans l’espace réservé de la boîte de dialogue Créer un fragment de contenu . Auparavant, le style italique appliqué aux caractères CJK sous **Assets** > **Fichiers** rendait le texte difficile à lire. Les styles mis à jour ignorent l’italique pour les langues CJC. (SITES-43548)
* L’éditeur de fragment de contenu valide correctement les champs après la mise à jour de l’interface utilisateur Granite. Une récente modification de l’interface utilisateur Granite a provoqué une régression. Les bibliothèques clientes de l’éditeur ne correspondaient donc plus au nouveau comportement de validation. Les bibliothèques et tests adaptés résolvent l’incohérence. (SITES-46650)


#### [!DNL Content Fragments] - API GraphQL {#sites-graphql-api-6526}

* Les requêtes GraphQL sur les fragments de contenu reconnaissent désormais les références RemoteRef à Dynamic Media avec OpenAPI Assets. Auparavant, les requêtes échouaient avec une « erreur de validation de requête persistante » et ne renvoyaient aucune donnée de ressource lorsqu’AEM 6.5 Sites utilisait AEM as a Cloud Service Assets. Les réponses incluent désormais l’ID de référentiel et l’ID de ressource, afin que les clients puissent créer des URL de diffusion. (SITES-48507)

* Les instances de publication restent réactives lors d’un trafic GraphQL important. Verrouiller la contention dans `GraphQLServiceImpl` threads de traitement des demandes retardés au niveau des méthodes de schéma, ce qui a ralenti les demandes et a nécessité des redémarrages. Une synchronisation améliorée résout la contrainte de performance et maintient la disponibilité des sites et des applications mobiles. (SITES-48699)

* Le message sur la page Points d’entrée GraphQL reste localisé après le rechargement de la page. Auparavant, le message « Aucun point d’entrée n’a été trouvé » s’affichait dans votre langue lorsque vous créiez et supprimiez des points d’entrée, mais il est revenu à l’anglais après un rechargement. La page charge désormais la chaîne traduite à chaque visite. (SITES-43586)


<!--
#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6526}
-->


#### [!DNL Content Fragments] - Modèles et éditeur de modèles{#sites-models-model-editor-6526}

* Les miniatures des modèles de fragment de contenu s’affichent dans **Outils** > **Général** > **Modèles de fragment de contenu** lorsque le nom de la configuration contient des caractères localisés, tels que « español テスト ». Auparavant, la miniature chargée n’apparaissait pas, car les caractères provoquaient une erreur dans le chemin d’accès. La gestion mise à jour code correctement le nom. (SITES-39242)

* La chaîne Libellé du champ dans la zone de travail de l’éditeur de modèles de fragments de contenu s’affiche désormais dans la langue de l’utilisateur. Auparavant, le libellé restait en anglais lorsque les auteurs faisaient glisser un composant sur la zone de travail et il n’était traduit qu’après l’enregistrement et la réouverture du modèle. Le libellé est désormais traduit immédiatement, conformément au panneau Propriétés . (SITES-45383)


<!--
#### [!DNL Content Fragments] - REST API{#sites-restapi-6526}

#### ContextHub{#sites-contexthub-6526}
-->


#### Back-end principal{#sites-core-backend-6526}

* L’activation des pages planifiée via l’heure d’activation s’exécute désormais uniquement lorsque cela est nécessaire. `OnOffTriggerProcessor` a trop souvent déclenché la réplication et l’invalidation du cache, ce qui a forcé les auteurs à republier le contenu manuellement. Le correctif rétroporté élimine le traitement inutile et restaure une publication planifiée fiable. (SITES-48483)

* Le chargement de fichiers fonctionne pour les ressources distantes à partir de la gestion des ressources nouvelle génération dans un champ multiple. Auparavant, le chargement échouait lorsque les auteurs choisissaient une ressource distante pour un champ dans un multichamp. La mise à jour des composants principaux restaure le flux de chargement, de sorte que le champ accepte la ressource. (SITES-44266)


#### Composants principaux{#sites-core-components-6526}

* Le sélecteur de ressources à distance sépare l’image de chaque élément multichamp. Auparavant, la sélection d’une image dans un élément à champs multiples l’appliquait à tous les autres éléments, et la référence de ressource distante n’était pas enregistrée. Chaque élément contient désormais sa propre sélection et la référence persiste après l’enregistrement de la boîte de dialogue. (SITES-42376)

* Cette version comprend des correctifs rétroportés pour Commerce, les composants principaux, les composants de base (hérités), les lancements et les Live Copies MSM. Ces correctifs traitent des vulnérabilités de sécurité, des violations de script entre sites (XSS), du comportement de chargement de fichiers et du comportement de Live Copy. Les rétroports permettent à AEM 6.5 et au LTS AEM 6.5 d’être conformes aux correctifs fournis précédemment dans AEM as a Cloud Service. (SITES-43738)


<!--
#### Campaign integration{#sites-campaign-integration-6526}

#### ContentHub {#sites-contenthub-6526}

#### Crosswalk {#sites-crosswalk-6526}

#### Experience Fragments{#sites-experiencefragments-6526}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-6526}
-->


#### Headless - Admin {#sites-headless-admin-6526}

Amélioration : l’aperçu dans l’Administration découplée transmet désormais le chemin de variation sélectionné au composant d’aperçu. Cette modification garantit que les aperçus de fragments de contenu avec plusieurs variations chargent le contenu de la variation correcte. Le tableau `draftFragmentIds` inclut le paramètre de variation. (SITES-42714)


#### Lancements{#sites-launches-6526}

* Les entrées de chronologie des lancements promus s’affichent désormais dans la langue de l’utilisateur. Auparavant, les chaînes « Version créée de » et « avant la promotion du lancement » restaient en anglais après la promotion d’un lancement par les auteurs et l’ouverture de la chronologie du site dans Sites. Les ressources mises à jour fournissent les traductions dans tous les paramètres régionaux. (SITES-13389)
* L’espace réservé Sélectionner le chemin d’accès de Source Launch dans le panneau de filtrage Lancements s’affiche en entier. Auparavant, le texte était coupé dans des interfaces localisées, telles que le français, l’italien et le portugais, car il ne correspondait pas au champ. La mise en page mise à jour affiche l’espace réservé complet. (SITES-42792)
* La colonne Date d’activation dans Outils > Sites > Lancements n’affiche plus AM ou PM dans les langues allemande, française, espagnole, italienne, portugaise brésilienne et chinoise traditionnelle. Auparavant, la colonne utilisait un format de 12 heures qui ne correspondait pas à ces paramètres régionaux. La colonne affiche désormais le format 24 heures. (SITES-43178)


<!--
#### Link Checker{#sites-link-checker-6526}
-->


#### Localisation{#sites-localization-6526}

* Les chaînes des pages Rapports d’intégrité sous **Outils** > **Opérations** s’affichent désormais dans la langue de l’utilisateur. Auparavant, les messages pour le chemin de recherche des ressources, la maintenance, la file d’attente de réplication, les erreurs de journal, les lots actifs et les performances des requêtes étaient toujours en anglais. Les ressources i18n mises à jour fournissent les traductions, et un fichier de secours garde les chaînes disponibles. (NPR-44279)

* Le message d’erreur « Les paramètres du chemin JSON sont ignorés lorsque l’option « Ajouter manuellement » est cochée » s’affiche désormais dans la langue de l’utilisateur dans la console **Outils** > **Assets** > **Schémas de métadonnées**. Auparavant, le message restait en anglais après l’ajout par les auteurs d’un élément de liste déroulante, ils sélectionnaient Ajouter via le chemin JSON et passaient à Ajouter manuellement. Les ressources mises à jour fournissent les traductions. (ASSETS-31575)
* La chaîne « promue » dans les balises **Assets** > **Gérer** s’affiche désormais dans la langue de l’utilisateur. Auparavant, la chaîne était conservée en anglais lorsque vous passiez la souris sur une balise active après avoir sélectionné Convertir. Les ressources mises à jour fournissent la traduction dans tous les paramètres régionaux. (ASSETS-36070)
* Le libellé du bouton Ajouter ne chevauche plus le bouton dans **Propriétés du dossier** > **Contribution des ressources**. Auparavant, le texte était en conflit avec le bouton dans les interfaces allemande, italienne et portugaise brésilienne après la création d’un dossier avec le paramètre « Contribution des ressources ». Les styles mis à jour donnent suffisamment de place aux libellés traduits plus longs. (ASSETS-36746)
* Les titres des colonnes dans la vue Liste d’Assets s’affichent désormais horizontalement dans l’interface japonaise. Auparavant, les titres s’affichaient verticalement dans la vue Liste sous **Assets** > **Fichiers**, et dans la vue Carte de l’éditeur de fragment de contenu. Le package `cq-dam-content` mis à jour corrige l’orientation du texte.(ASSETS-43105)
* Le statut de la publication « Planifiée pour plus tard » dans la vue Colonnes d’Assets s’affiche désormais dans la langue de l’utilisateur. Auparavant, la chaîne restait en anglais après la sélection d’une ressource par les auteurs, la sélection de **Gérer la publication**, la sélection de l’option **Plus tard**, l’ajout d’une date et la publication. Le package `cq-dam-content` mis à jour fournit les traductions dans tous les paramètres régionaux. (ASSETS-43307)
* Les chaînes de l’onglet **Configuration des balises intelligentes** s’affichent désormais en entier pour le français et le portugais brésilien. Auparavant, le texte était coupé après avoir cliqué sur **Créer** sous **Outils** > **Services cloud** > **Balise intelligente**. Pour lire le texte sans info-bulle, utilisez la mise à jour CSS qui offre suffisamment d’espace. (ASSETS-68045)
* La chaîne « Prédicat de propriété de valeur à chemins multiples » dans le rail de recherche d’administration d’Assets s’affiche désormais dans la langue de l’utilisateur. Auparavant, la chaîne restait en anglais lorsque les administrateurs modifiaient le formulaire de recherche sous **Outils** > **Général** > **Rechercher** formulaires et faisaient glisser le prédicat sur le formulaire. Le package `cq-dam-content` mis à jour fournit les traductions.(CQ-4336103)
* Les libellés Aria de la vue Projets s’affichent désormais dans la langue de l’utilisateur. Auparavant, le bouton Actions de chaque mosaïque de projet n’avait aucun nom accessible et l’action Configurer la mosaïque utilisait un libellé anglais codé en dur tandis que les libellés frères étaient localisés. Le script de mosaïque mis à jour fournit un libellé localisé pour les deux actions. (CQ-4352359)
* Les collections dynamiques dont le nom contient des caractères chinois, japonais ou coréens s’enregistrent désormais correctement. Auparavant, l’enregistrement d’une collection à partir de **Assets** > **Fichiers** > **Filtre** échouait avec « Échec de l’enregistrement de la recherche - Requête non valide, la collection en double n’est pas autorisée » lorsque le nom contenait des caractères CJK. La vérification en double compare désormais les titres des collections plutôt que les noms de nœud, de sorte que les collections avec différents titres CJC ne soient plus en conflit. (GRANITE-62592)
* La liste déroulante Pays/zone géographique dans **Sécurité** > **Utilisateurs** > **Créer** trie désormais les noms par ordre alphabétique dans la langue de l’utilisateur. Auparavant, la liste triait les noms dans l’ordre anglais, tandis qu’elle affichait des noms localisés. Les pays apparaissaient donc dans le désordre dans des paramètres régionaux tels que le japonais. Le lot `com.adobe.granite.security.content` mis à jour trie avec des règles tenant compte des paramètres régionaux. (GRANITE-67789)
* La clause d’exclusion de responsabilité de la tâche de maintenance du journal d’audit dans **Outils** > **Opérations** > **Maintenance** s’affiche désormais dans la langue de l’utilisateur. Auparavant, l’avertissement relatif à la purge du journal d’audit et aux exigences de conformité restait en anglais lorsque les utilisateurs cliquaient sur l’icône de clause de non-responsabilité dans la fenêtre Maintenance hebdomadaire . Les ressources mises à jour fournissent la traduction dans tous les paramètres régionaux. (NPR-44189)
* Les noms des autorisations dans **Sécurité** > **Autorisations** > **Vue d’audit** s’affichent désormais dans la langue de l’utilisateur. Auparavant, les noms apparaissaient en anglais parce que les traductions manquaient. Le lot `com.adobe.granite.platform.i18n` mis à jour les fournit. (NPR-44477)
* La boîte de dialogue Vérifier l’intégrité dans **Sécurité** > **Configurations d’Adobe IMS** s’affiche désormais dans la langue de l’utilisateur. Auparavant, la boîte de dialogue affichait des chaînes de caractères anglaises dans les interfaces localisées, car les traductions étaient manquantes. Le lot `com.adobe.granite.platform.i18n` mis à jour les fournit. (NPR-44479)
* Les chaînes de l’outil Diagnostics de synchronisation des utilisateurs sous **Outils** > **Opérations** > **Diagnostic** s’affichent désormais dans la langue de l’utilisateur. Auparavant, l’outil affichait du texte en anglais dans des interfaces localisées. Le lot `com.adobe.granite.platform.i18n` mis à jour fournit les traductions. (NPR-44481)
* Les flux de configuration affichent désormais des messages d’erreur conviviaux dans la langue de l’utilisateur. Auparavant, les échecs des pages de configuration AEM généraient du texte technique ou non traduit. Le lot `com.adobe.granite.ui.content` mis à jour gère les erreurs et fournit des messages localisés. (NPR-44840)
* Le message d’erreur qui s’affiche lorsque vous modifiez les propriétés d’un groupe supprimé dans **Sécurité** > **Groupes** s’affiche désormais dans la langue de l’utilisateur. Auparavant, le message restait en anglais pour les interfaces localisées. Le lot `com.adobe.granite.security.content` mis à jour fournit les traductions. (NPR-44841)
* Message d’erreur « Un problème est survenu lors de l’enregistrement des modifications dans le groupe ! » s’affiche désormais dans la langue de l’utilisateur dans la console **Sécurité** > **Groupes** > **Modifier le groupe**. Auparavant, le message restait en anglais pour les interfaces localisées. Le lot `com.adobe.granite.security.content` mis à jour fournit les traductions. (NPR-44842)
* Les caractères chinois, japonais et coréens ne s’affichent plus en italique dans le message d’erreur de l’icône de boîte de réception. Auparavant, le style italique déformait les caractères et rendait le texte plus difficile à lire. Le lot `com.adobe.granite.ui.coralui3` mis à jour supprime le style de ces langues. (NPR-44843)
* Les nombres dans **Opérations** > **Surveillance** suivent désormais le format des paramètres régionaux de l’utilisateur. Auparavant, la page affichait les nombres dans un format fixe, quelle que soit la langue de l’interface. Le lot `com.adobe.granite.monitoring.dashboard` mis à jour applique les séparateurs et le format corrects. (NPR-44844)
* L’onglet Expliquer la requête affiche désormais l’outil Query Builder Debugger. lien dans la langue de l’utilisateur. Auparavant, le texte du lien était manquant dans les interfaces localisées, car la chaîne n’était pas externalisée. Le lot `com.adobe.granite.monitoring.dashboard` mis à jour le restaure. (NPR-44845)
* Le texte de la boîte de dialogue de l’outil de débogage Query Builder s’affiche désormais dans la langue de l’utilisateur dans l’onglet Expliquer la requête . Auparavant, plusieurs chaînes restaient en anglais car elles n&#39;étaient pas externalisées. Le lot `cq-platform-content` mis à jour fournit les traductions. (NPR-44846)
* Le texte de la page Résultat de la vérification de cohérence s’affiche désormais dans la langue de l’utilisateur. Auparavant, plusieurs chaînes apparaissaient en anglais car elles n&#39;étaient pas externalisées. Le lot `com.adobe.granite.operations.ui.core` mis à jour fournit les traductions. (NPR-44847)
* Le graphique de surveillance affiche désormais les libellés des mois et des semaines dans la langue de l’utilisateur. Auparavant, les libellés étaient codés en dur en anglais. Le graphique a donc ignoré les paramètres régionaux de l’interface. Le lot `com.adobe.granite.monitoring.dashboard` mis à jour externalise les chaînes et les traductions s’affichent désormais. (NPR-44848)
* La liste déroulante Pays/Région dans **Sécurité** > **Utilisateurs** > **Créer** trie désormais correctement les entrées. Auparavant, les noms de pays localisés s’affichaient dans le mauvais ordre pour certaines langues. Le lot `com.adobe.granite.security.content` mis à jour applique un tri tenant compte des paramètres régionaux. (NPR-44942)
* Les info-bulles de la boîte de dialogue du composant Bouton s’affichent désormais dans la langue de l’utilisateur. Auparavant, le texte des informations pour les champs texte du bouton, lien, icône, HTML ID et `aria-label` restait en anglais même si les chaînes existaient dans le service de localisation. Le dictionnaire mis à jour fournit les traductions dans tous les paramètres régionaux pris en charge. (SITES-7579)
* Les info-bulles de la section Propriétés du composant Liste de fragments de contenu s’affichent désormais dans la langue de l’utilisateur. Auparavant, le texte des informations pour les champs Modèle de fragment de contenu, Balises, Nombre maximal d’éléments, Chemin d’accès parent, Ordre de tri et Trier par restait en anglais. Le dictionnaire mis à jour fournit des traductions pour tous les paramètres régionaux pris en charge. (SITES-14969)
* Les liens d’aide des composants principaux dans l’éditeur de modèles mènent désormais à des pages de documentation localisées. Auparavant, si vous sélectionniez Aide dans la boîte de dialogue de configuration des composants, la page Anglais s’ouvrait, quelle que soit la langue de l’interface. Les URL mises à jour acheminent désormais les utilisateurs vers la page en fonction de leurs paramètres régionaux. (SITES-15058)
* Les info-bulles de la boîte de dialogue Fragment de contenu s’affichent désormais dans la langue de l’utilisateur. Auparavant, le texte de l’info-bulle pour les modes Un seul élément de texte et Plusieurs éléments , ainsi que pour le chemin d’accès au fragment de contenu restait en anglais. Un dictionnaire mis à jour fournit des traductions pour tous les paramètres régionaux. (SITES-17333)
* Les messages d’erreur dans l’éditeur de stratégie des composants de l’éditeur de modèles s’affichent désormais dans la langue de l’utilisateur. Auparavant, les messages « Resource {} is not modifiable » et « Impossible de créer le nœud à » restaient en anglais lorsque les auteurs modifiaient une politique de composant ou en créaient une. Les ressources mises à jour fournissent des traductions pour tous les paramètres régionaux pris en charge. (SITES-17475)
* L’onglet Assets de l’éditeur de page affiche désormais une chaîne traduite dans le menu déroulant Sélectionner les composants une fois que vous avez choisi Paragraphes dans le menu déroulant Images . Auparavant, la chaîne « OTHER » s’affichait en anglais, car elle manquait aux ressources de localisation. Le dictionnaire mis à jour fournit la traduction dans tous les paramètres régionaux. (SITES-21481)
* Les info-bulles de la boîte de dialogue du composant Configuration de l’éditeur de page n’affichent plus de saut de ligne supplémentaire. Auparavant, les infobulles des composants, tels que la visionneuse PDF et la barre de progression, s’affichaient maladroitement dans plusieurs paramètres régionaux. Les infobulles s’encapsulent désormais correctement et la coupure de mots fonctionne comme prévu. (SITES-38567)
* L’info-bulle « Pour quitter l’éditeur de texte, appuyez sur la touche Échap » s’affiche désormais dans la langue de l’utilisateur dans la boîte de dialogue de configuration du composant de texte. Auparavant, la chaîne s’affichait en anglais car les ressources de localisation manquaient de chaîne. L’info-bulle se traduit désormais dans tous les paramètres régionaux. (SITES-43186)
* Le libellé STRUCTURE dans l’éditeur de modèles s’affiche désormais dans la langue de l’utilisateur. Auparavant, le libellé restait en anglais lorsque les auteurs ouvraient un modèle de formulaire adaptatif, car la chaîne était manquante dans les ressources de localisation. Le libellé est désormais traduit dans tous les paramètres régionaux. (SITES-43599)


#### MSM - Copies dynamiques{#sites-msm-live-copies-6526}

* La boîte de dialogue Déploiement MSM charge à nouveau la liste Live Copy après une mise à niveau. Auparavant, un `NullPointerException` dans `AsyncOperationServlet.doGet` arrêtait la boîte de dialogue sur une double flèche, de sorte que les auteurs ne pouvaient pas sélectionner les paramètres régionaux cibles ni démarrer le déploiement. Un lot `com.adobe.granite.jobs.async` mis à jour gère les données de tâche manquantes et termine la requête. (SITES-43116)
* Le déploiement à partir de la barre d’outils modifiable sur une page de plan directeur fonctionne à nouveau. Échec de l’action de la barre d’outils avec « Impossible de lire les propriétés de l’objet non défini (lecture de « doRollout ») », car la bibliothèque cliente `MSM.Rollout` ne s’est pas chargée. La page mise à jour charge désormais la bibliothèque, de sorte que la tâche de déploiement démarre et que les modifications atteignent les Live Copies. (SITES-46052)

* La désactivation par lots d’une page de plan directeur et de ses pages enfants n’envoie plus d’événements de déploiement en double. Lorsque vous avez désactivé un parent et ses enfants dans une seule requête, le système de réplication a émis cinq événements au lieu de trois, et chaque page enfant a été déployée deux fois. La déduplication dans le gestionnaire de déploiement envoie désormais un déploiement par page, de sorte que les Live Copies ne reçoivent aucun package redondant. (SITES-44988)


#### Éditeur de page{#sites-pageeditor-6526}

* Le style sélectionné reste en surbrillance dans la boîte de dialogue de sélection des styles de l’éditeur de page après avoir fait défiler la liste. Auparavant, un style était mis en surbrillance lorsque vous le choisissiez, mais il disparaissait lorsque vous cliquiez sur la barre de défilement. Cette régression a commencé après SP22 et la boîte de dialogue conserve désormais l’état sélectionné visible. (SITES-30874)

* Les auteurs peuvent modifier les pages en mode Mise en page lorsque les composants parents et enfants définissent différents points d’arrêt réactifs. La fonction getResponsiveCssClasses a précédemment échoué avec une erreur TypeError sur les composants qui ont omis la largeur cq:responsive/téléphone. La fonction revient désormais aux valeurs disponibles et poursuit le rendu. (SITES-46681)
* Les proportions de recadrage personnalisé se chargent désormais en mode de modification en ligne hybride pour les composants avec plusieurs cibles de dépôt d’images. Auparavant, l’éditeur d’image initialisait un ipeConfig générique pour toutes les cibles de dépôt. Il n’affichait donc que les proportions par défaut et ignorait les proportions de chaque cible. L’éditeur lit désormais la configuration de la cible de dépôt sélectionnée et le recadrage s’applique en mode plein écran et en mode intégré. (SITES-45771)
* Appuyez sur la touche Retour arrière dans l’éditeur de texte enrichi pour n’ajouter pas de styles intégrés supplémentaires au texte. Un client a signalé que la suppression d’un saut de ligne après le texte en gras a ajouté style=« font-size: 0.8125rem; background-color: transparent; » à la balise en gras. Le test sur le dernier pack de services n’a pas pu reproduire le comportement, aucune modification n’était donc nécessaire. (SITES-15883)


<!--
#### Replication{#sites-replication-6526}
-->


#### Éditeur de texte enrichi{#sites-rte-6526}

* Les boutons de la barre d’outils de l’éditeur de texte enrichi fonctionnent en mode Réactif et en mode Mise en page. Auparavant, les boutons étaient mis en surbrillance lorsque l’utilisateur cliquait dessus, mais la sélection restait inchangée et aucune boîte de dialogue n’était ouverte. Le script d’éditeur mis à jour applique la mise en forme , correspondant au comportement en mode d’édition . (SITES-44233)
* Les auteurs peuvent ajouter des symboles de devise et de marque aux composants de texte sans les perdre. Le plug-in Caractères spéciaux insérait les symboles, mais ils s’affichaient en tant que vides dans l’éditeur et dans la sortie publiée. La gestion corrigée rend chaque symbole tel qu’il a été saisi. (SITES-46532)
* L’icône Plein écran de la barre d’outils de l’éditeur de texte enrichi développe à nouveau l’éditeur. Auparavant, cliquer sur l’icône dans le composant Texte principal n’avait aucun effet et l’éditeur restait à sa taille en ligne. Les auteurs disposent désormais d’un espace de travail ciblé pour le contenu de forme longue pour la modification en ligne et dans les boîtes de dialogue. (SITES-46396)


#### Interface utilisateur d’administration du site{#sites-admin-ui-6526}

Le rétablissement d’une version antérieure d’une ressource actualise désormais sa miniature. Une modification du codage d’URL dans la bibliothèque cliente Chronologie a provoqué une incohérence des chemins d’accès. La recherche de la carte a donc échoué et la miniature est restée obsolète. La correspondance entre les chemins codés et bruts restaure l’actualisation. (SITES-46590)

<!--
#### Universal editor {#sites-universal-editor-6526}
-->

#### Extensions de workflow {#sites-workflow-extensions-6526}

Afficher la payload ouvre désormais l’éditeur de package de l’interface utilisateur tactile pour les workflows qui Gérer les démarrages de publication pour plusieurs pages. Auparavant, l’action ouvrait l’éditeur de package d’interface utilisateur classique obsolète, même si les créateurs et créatrices démarraient le workflow dans l’interface utilisateur tactile. Les auteurs inspectent désormais la payload sans quitter l’interface utilisateur tactile. (SITES-40928)


### [!DNL Assets] {#assets-6526}

* Amélioration : AEM Assets 6.5 comprend la prise en charge de la conformité C2PA (Coalition for Content Provenance and Authenticity) pour le contenu d’IA génératif. Le workflow Mettre à jour la ressource détecte les informations d’identification C2PA, extrait les métadonnées et signe les rendus que le workflow régénère. La signature s’exécute localement dans chaque instance d’AEM, de sorte que les clients n’ont pas besoin d’infrastructure de signature dédiée. (ASSETS-75868)

* Amélioration de la documentation : la nouvelle documentation publique explique comment personnaliser le pipeline de traitement des ressources tout en respectant la conformité C2PA. La documentation explique comment positionner l’étape Détecter les informations d’identification C2PA avant les étapes de rendu et comment la signature s’exécute localement dans chaque instance AEM. La documentation indique également les restrictions relatives aux infrastructures de signature dédiées ou détenues par le client. (ASSETS-76100)
* Le menu déroulant Aide de l’en-tête shell reste ouvert lorsque vous passez la souris sur ses liens dans les environnements AEM 6.5 SP26. Auparavant, la liste déroulante se fermait lorsque le pointeur accédait à la liste, de sorte que les auteurs ne pouvaient pas cliquer sur les liens Documentation, Communauté ou Assistance. Le lot `com.adobe.granite.ui.content` mis à jour reporte la vérification de la sélection, de sorte que le menu se ferme uniquement lorsque la sélection est vraiment arrêtée. (ASSETS-65676)

<!--
#### [!DNL Dynamic Media]{#assets-dm-6526}
-->

### [!DNL Forms]{#forms-6526}

* Nouvelle fonctionnalité : prise en charge des balises d’accessibilité sur les listes en texte enrichi. Auparavant, les balises de liste s’affichaient dans l’arborescence des balises d’accessibilité uniquement lorsque le modèle suivait une structure spécifique. La demande s’est close en tant que doublon d’un ticket associé qui offre la fonctionnalité. (LC-3923202)


<!--
#### Forms JEE {#forms-jee-6526}

#### Forms Designer {#forms-designer-6526}
-->


### Foundation {#foundation-6526}

* La chaîne « Pays/Région » dans la boîte de dialogue de l’utilisateur **Sécurité** > **Utilisateurs** > **Créer** s’affiche désormais dans la langue de l’utilisateur. Auparavant, le libellé était conservé en anglais pour les interfaces localisées. Le lot `com.adobe.granite.security.content` mis à jour fournit les traductions. (NPR-43882)
* Le menu déroulant Aide de l’en-tête shell reste ouvert lorsque vous passez la souris sur ses liens dans les environnements AEM 6.5 SP26. Auparavant, la liste déroulante se fermait lorsque le pointeur accédait à la liste, de sorte que les auteurs ne pouvaient pas cliquer sur les liens Documentation, Communauté ou Assistance. Le lot `com.adobe.granite.ui.content` mis à jour reporte la vérification de la sélection, de sorte que le menu se ferme uniquement lorsque la sélection est vraiment arrêtée. (NPR-44686)
* Amélioration : la requête `HtmlLibraryManagerImpl` inclut désormais une balise de type nœud afin que la requête utilise toujours l’index attendu. Le service consigne également une ERREUR lorsqu’il ne trouve aucune bibliothèque cliente, ce qui avertit les administrateurs du problème. La mise à jour déplace la version du bundle `com.adobe.granite.clientlibs` dans le pack de services. (NPR-44698)


<!--
#### Apache Felix {#foundation-apachefelix-6526}
-->


#### Authentification {#foundation-authentication-6526}

Enregistrer et fermer dans l’éditeur utilisateur revient désormais aux résultats de la recherche en cours. Auparavant, lorsque les auteurs recherchaient un second utilisateur dans Omnisearch, modifiaient les propriétés et cliquaient sur Enregistrer et fermer, la page ouvrait les propriétés du premier utilisateur à la place. Le script UserProperties.js mis à jour restaure la navigation attendue. (NPR-44774)

<!--
#### Campaign{#foundation-campaign-6526}

#### Cloud Services{#foundation-cloudservices-6526}

#### Communities {#foundation-communities-6526}

#### Content distribution{#foundation-content-distribution-6526}

#### Adobe CRX {#foundation-crx-6526}
-->


#### Granite{#foundation-granite-6526}

* L’espace réservé « Modèle de fragment de contenu » dans le filtre Omnisearch d’Assets s’affiche désormais en entier. Auparavant, le texte était coupé après avoir accédé à Assets, cliqué sur l’icône Filtres ou Rechercher et développé le champ Modèle de fragment de contenu . La mise à jour du style donne suffisamment d’espace à l’espace réservé. (GRANITE-54387)
* Le menu déroulant Aide de l’en-tête shell reste ouvert lorsque vous déplacez le pointeur sur ses liens. Auparavant, la liste déroulante se fermait dès que le pointeur accédait à la liste des liens Documentation, Communauté et assistance, ce qui rendait les liens inaccessibles avec une souris. Le gestionnaire de sélection reporte désormais sa vérification à l’image d’animation suivante, de sorte que le survol ne compte plus comme sélection à la sortie du menu. (GRANITE-70978)

<!--
#### Jetty{#foundation-jetty-6526}
-->

#### Intégrations de Launch{#foundation-launch-integrations-6526}

Amélioration : l’intégration d’Adobe Analytics à Adobe Experience Manager Launch utilise l’API Analytics 2.0. L’API Analytics 1.4 arrive en fin de vie le 31 août 2026. La migration continue de fonctionner après cette date. (CQ-4365074, CQ-4365080)

<!--
#### Localization{#foundation-localization-6526}

#### Oak {#foundation-oak-6526}
-->

#### Plateforme{#foundation-platform-6526}

* Le lien Aide situé dans le pied de page de la page de connexion d’AEM ouvre désormais une page de travail. Auparavant, le lien pointait vers une URL marketing.adobe.com qui n’existe plus. La configuration du pied de page utilise désormais l’URL [Documentation Adobe Experience Manager](https://experienceleague.adobe.com/fr/docs/experience-manager). (NPR-44388)
* Amélioration : une demande de client a demandé l’API Microsoft Graph comme alternative à SMTP lorsqu’AEM envoie un e-mail. Le ticket a été résolu en tant que doublon, car un autre ticket implémente déjà le flux de l’API Graph. SMTP avec OAuth 2.0 reste disponible pour les clients qui doivent abandonner l’authentification de base SMTP. (GRANITE-57478)

* Les chaînes de la boîte de dialogue Autorisations effectives s’alignent désormais correctement dans le navigateur **Outils** > **Général** > **Configuration**. Auparavant, une chaîne s’affichait hors ligne après que vous ayez sélectionné un dossier, cliqué sur Propriétés, puis sur Autorisations effectives. Les règles de mise en page mises à jour restaurent l’alignement. (CQ-4359166)


#### Projets {#foundation-projects-6526}

La chaîne « Sélectionner le répertoire racine » dans la boîte de dialogue Sélectionner le dictionnaire i18n s’affiche désormais dans son intégralité. Auparavant, le texte était coupé dans plusieurs interfaces localisées après la création d’un projet de traduction et l’ajout d’un dictionnaire i18n. Le package `cq-projects-translation-content` mis à jour donne suffisamment d’espace à la chaîne. (CQ-4355405)

<!--
#### Security{#foundation-security-6526}

#### Sling{#foundation-sling-6526}

#### SPA editor {#foundation-spa-editor-6526}
-->


#### Traduction{#foundation-translation-6526}

Les options de style du composant Liste s’affichent désormais dans la langue de l’utilisateur. Auparavant, les chaînes telles que Bloc et Grille étaient conservées en anglais dans le menu Styles après l’ajout du composant Liste à un fragment d’expérience. Les ressources mises à jour fournissent les traductions, y compris les interfaces Coréen, Chinois simplifié et Chinois traditionnel. (CQ-4349666)

<!--
#### User interface{#foundation-ui-6526}

#### WCM{#foundation-wcm-6526}
-->

#### Workflow{#foundation-workflow-6526}

Amélioration : l’éditeur de page de l’interface utilisateur tactile effectue désormais le rendu de l’arborescence de contenu et prend en charge la modification des composants Définition de ressource sur les pages du package de workflow. Auparavant, les pages sous `/etc/workflow/packages/` créées par **Gérer la publication** > **Publier ultérieurement** n’affichaient aucune arborescence de contenu dans le panneau de gauche et les auteurs ne pouvaient pas modifier les composants Définition de ressource. Les approbateurs inspectent désormais les pages et les ressources dans une payload de workflow dans l’interface utilisateur tactile, conformément au comportement de l’interface utilisateur classique. (GRANITE-65620)

## Installer [!DNL Experience Manager] 6.5.26.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.26.0 nécessite [!DNL Experience Manager] 6.5. Consultez la [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour obtenir des instructions détaillées. <!-- UPDATE FOR EACH NEW RELEASE -->
* Le téléchargement du pack de services est disponible dans la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip) d’Adobe.
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez [!DNL Experience Manager] 6.5.26.0 sur l’une des instances de création à l’aide du gestionnaire de modules.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe recommande de ne pas supprimer ni désinstaller le package [!DNL Experience Manager] 6.5.26.0. Pour effectuer une restauration si nécessaire, créez une sauvegarde du `crx-repository` avant d’installer le module. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- FORMS For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->

### Installer le pack de services dans [!DNL Experience Manager] 6.5{#install-service-pack}

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.

1. Avant l’installation, prenez un instantané ou exécutez une sauvegarde récente de votre instance [!DNL Experience Manager].

1. Téléchargez le pack de services à partir de la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.26.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Ouvrez le gestionnaire de modules et cliquez sur **[!UICONTROL Charger le module]** pour charger le module. Pour plus d&#39;informations, consultez [Gestionnaire de packages](/help/sites-administering/package-manager.md).

1. Sélectionnez le module, puis sélectionnez **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du pack de services, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Consultez la section [Entrepôt de données S3 Amazon](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface utilisateur du gestionnaire de packages se ferme parfois pendant l’installation du pack de services. Adobe vous conseille d’attendre que les journaux d’erreurs cessent de changer avant d’accéder au déploiement. Attendez les journaux spécifiques liés à la désinstallation du lot de mise à jour avant de confirmer que l’installation est réussie. Ce problème se produit dans le navigateur [!DNL Safari], mais peut parfois se produire dans n’importe quel navigateur.

**Installation automatique**

Vous pouvez utiliser deux méthodes différentes pour installer automatiquement [!DNL Experience Manager] 6.5.26.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.
* Utilisez l’[API HTTP à partir du gestionnaire de modules](/help/sites-administering/package-manager.md#package-share). Utilisez `cmd=install&recursive=true` afin que les packages imbriqués soient installés.

>[!NOTE]
>
>Experience Manager 6.5.26.0 ne prend pas en charge l’installation Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validation de l’installation**

Pour les plateformes certifiées pour travailler avec cette version, consultez les [exigences techniques](/help/sites-deploying/technical-requirements.md).

1. La page d’informations sur les produits (`/system/console/productinfo`) affiche le numéro de version mis à jour `Adobe Experience Manager (6.5.26.0)` sous [!UICONTROL Produits installés]. <!-- UPDATE FOR EACH NEW RELEASE -->.

1. Tous les bundles OSGi sont au statut **[!UICONTROL ACTIF]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (utilisez la console web : `/system/console/bundles`).

1. Le bundle OSGi `org.apache.jackrabbit.oak-core` est de la version 1.22.20 ou ultérieure (utilisez la console web : `/system/console/bundles`). <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### Installer le pack de services pour [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

Pour obtenir des instructions sur l’installation du pack de services pour Experience Manager Forms, consultez les [instructions d’installation du pack de services Experience Manager Forms](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>La fonctionnalité de formulaires adaptatifs, disponible dans [AEM 6.5 QuickStart](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/implementing/deploying/deploying/deploy), est conçue à des fins d’exploration et d’évaluation uniquement. Pour une utilisation à des fins de production, il est essentiel d’obtenir une licence valide pour AEM Forms, car la fonctionnalité de formulaires adaptatifs nécessite une licence appropriée.

### Installer le package d’index GraphQL pour les fragments de contenu d’Experience Manager{#install-aem-graphql-index-add-on-package}

La clientèle qui utilise GraphQL doit installer le [fragment de contenu d’Experience Manager avec le package d’index GraphQL 1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

Vous pouvez ainsi ajouter la définition d’index requise en fonction des fonctionnalités utilisées.

L’échec de l’installation de ce package entraîne des requêtes GraphQL lentes ou en échec.

>[!NOTE]
>
>N’installez ce package qu’une seule fois par instance ; il n’est pas nécessaire de le réinstaller avec chaque Pack de services.

### UberJar{#uber-jar}

UberJar pour [!DNL Experience Manager] 6.5.26.0 est disponible dans le [référentiel central Maven](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.26/). <!-- CHECK FOR UPDATE EACH NEW RELEASE FROM MADHULIKA SINGH -->

Pour utiliser UberJar dans un projet Maven, consultez la section [Utilisation d’UberJar](/help/sites-developing/ht-projects-maven.md) et incluez la dépendance suivante dans le POM de votre projet : <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.26</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar et les autres artefacts associés sont disponibles sur le référentiel central Maven au lieu du référentiel Maven public Adobe (`repo.adobe.com`). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Il n’existe donc pas de `classifier` avec `apis` comme valeur pour la balise `dependency`.



## Fonctionnalités obsolètes et supprimées{#removed-deprecated-features}

Consultez [Fonctionnalités obsolètes et supprimées](/help/release-notes/deprecated-removed-features.md) pour obtenir une liste détaillée de toutes les fonctionnalités obsolètes ou supprimées pour AEM 6.5.

### Prise en charge des fragments de contenu dans l’API REST AEM Assets {#cf-support-assets-rest-api}

AEM 6.5 LTS SP2 fournit des API OpenAPI modernes pour la gestion des fragments de contenu et des modèles, de sorte que les anciens points d’entrée de la prise en charge des fragments de contenu dans l’API REST AEM Assets sont désormais obsolètes.

Adobe prévoit de conserver ces anciens points d’entrée disponibles jusqu’à une annonce de fin de vie. Adobe ne prévoit pas d’autres améliorations pour les points d’entrée obsolètes.

### Éditeur de SPA {#spa-editor}

[L’éditeur de SPA](/help/sites-developing/spa-overview.md) a été abandonné pour les nouveaux projets commençant par la version 6.5.25 d’AEM 6.5. L’éditeur de SPA reste pris en charge pour les projets existants, mais ne doit pas être utilisé pour de nouveaux projets.

Les éditeurs privilégiés pour la gestion du contenu découplé dans AEM sont désormais les suivants :

* [Éditeur universel](/help/sites-developing/universal-editor/introduction.md) pour la modification visuelle.
* [Éditeur de fragments de contenu](/help/sites-developing/universal-editor/introduction.md) pour la modification basée sur les formulaires.

## Problèmes connus{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST. -->

* **En rapport avec Oak**
À partir du pack de services 13 et versions ultérieures, le journal d’erreurs suivant a commencé à s’afficher, ce qui affecte le cache de persistance :

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

  1. Supprimez les deux dossiers suivants de `crx-quickstart/repository/`

     * `cache`
     * `diff-cache`

  1. Installez le Pack de services ou redémarrez Experience Manager as a Cloud Service.
     De nouveaux dossiers pour `cache` et `diff-cache` sont automatiquement créés et vous ne rencontrez plus d’exception liée à `mvstore` dans `error.log`.

* Mettez à jour vos requêtes GraphQL qui utilisaient un nom d’API personnalisé pour votre modèle de contenu afin d’utiliser le nom par défaut du modèle de contenu à la place.

* Une requête GraphQL utilise l’index `damAssetLucene` au lieu de l’index `fragments`. Cette action entraîne l’échec des requêtes GraphQL ou leur exécution prend beaucoup de temps.

  Pour résoudre le problème, `damAssetLucene` doit être configuré pour inclure les deux propriétés suivantes sous `/indexRules/dam:Asset/properties` :

  * `contentFragment`
    * `jcr:primaryType="nt:unstructured"`
    * `name="jcr:content/contentFragment"`
    * `propertyIndex="{Boolean}true"`
    * `type="Boolean"`
  * `model`
    * `jcr:primaryType="nt:unstructured"`
    * `name="jcr:content/data/cq:model"`
    * `ordered="{Boolean}true"`
    * `propertyIndex="{Boolean}true"`
    * `type="String"`

  Une fois la définition d’index modifiée, une réindexation est nécessaire (`reindex` = `true`).

  Après ces étapes, les requêtes GraphQL s’exécutent à une vitesse améliorée.

* Lorsque vous tentez de déplacer, de supprimer ou de publier des fragments de contenu, des sites ou des pages, un problème se produit lorsque les références aux fragments de contenu sont récupérées. La requête en arrière-plan échoue ; la fonctionnalité ne fonctionne pas.
Pour garantir le bon fonctionnement de cette opération, vous devez ajouter les propriétés suivantes au nœud de définition d’index `/oak:index/damAssetLucene` (aucune réindexation n’est requise) :

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* Si vous mettez à niveau votre instance [!DNL Experience Manager] de la version 6.5.0 - 6.5.4 au pack de services le plus récent sur Java™ 11, des exceptions `RRD4JReporter` s’affichent dans le fichier `error.log`. Pour arrêter les exceptions, redémarrez votre instance d’[!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Les utilisateurs peuvent renommer un dossier dans [!DNL Assets] et publier un dossier imbriqué dans [!DNL Brand Portal]. Toutefois, le titre du dossier n’est pas mis à jour dans [!DNL Brand Portal] jusqu’à ce que le dossier racine soit republié.

* Les erreurs et messages d&#39;avertissement suivants s&#39;affichent lors de l&#39;installation de [!DNL Experience Manager] 6.5.x.x :
  * « Lorsque l’intégration d’Adobe Target est configurée dans [!DNL Experience Manager] à l’aide de l’API Target Standard (authentification IMS), l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. » Au lieu du type « fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
  * `com.adobe.granite.maintenance.impl.TaskScheduler` : aucune fenêtre de maintenance n’a été trouvée sur `granite/operations/maintenance`.
  * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégat telles que SUM, MAX et MIN sont utilisées (CQ-4274424).
  * `com.adobe.granite.maintenance.impl.TaskScheduler` : aucune fenêtre de maintenance n’a été trouvée sur `granite/operations/maintenance`.
  * La zone réactive d’une image interactive de Dynamic Media n’est pas visible lors de la prévisualisation du fichier via la visionneuse de bannières avec achat.
  * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : temporisation en attente de modification d’enregistrement pour terminer la désinscription.

* À partir de la version 6.5.15 d’AEM, le moteur JavaScript Rhino fourni par le bundle `org.apache.servicemix.bundles.rhino` a un nouveau comportement d’hébergement. Les scripts qui utilisent le mode strict (`use strict;`) doivent déclarer leurs variables correctes. Dans le cas contraire, elles ne sont pas exécutées et finissent par générer une erreur d’exécution.

* L&#39;installation du contenu standard associé au balisage par le biais d&#39;un package de mise à jour officiel réinitialise la propriété de langues du nœud `/content/cq:tags` sur la valeur par défaut. Cette action est vraie pour les packs de services, les packs de services de sécurité, les packs de fonctionnalités étendues, les packs de fonctionnalités cumulatives, les correctifs, etc. Par conséquent, il est nécessaire de l’ajouter aux propriétés avant l’installation.

### Problèmes connus pour AEM Sites {#known-issues-aem-sites-6526}

* **Problème connu avec un correctif disponible pour AEM Foundation**

  Après la mise à niveau d’un pack de services précédent vers Experience Manager 6.5.26.0, l’ordre de version des lots CRXDE Lite peut empêcher Experience Manager de sélectionner le lot prévu. Pour corriger l’ordre des versions, installez le pack de services 26, puis téléchargez et installez le correctif [`CRXDE Lite hotfix GRANITE-76725`](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq660%2Fhotfixes%2Fgranite-76725%2Fcq-6.5.26-hotfix-GRANITE-76725-1.0.zip) à partir de la distribution logicielle. Le correctif est une mise à jour de version uniquement. Il ne contient aucun code ni modification fonctionnelle. (GRANITE-76725)

* Fragments de contenu : la prévisualisation échoue en raison de la protection DoS pour une arborescence de fragments volumineuse. Voir l’[article de la base de connaissances sur les options de configuration par défaut de l’exécuteur de requêtes GraphQL](https://experienceleague.adobe.com/fr/docs/experience-cloud-kcs/kbarticles/ka-23945) (SITES-17934).

### Problèmes connus d’AEM Forms {#known-issues-aem-forms-6526}

* Lorsqu’un formulaire contenant un champ **Pièce jointe** qui utilise `bindref` est envoyé à un workflow AEM avec une étape **Affecter une tâche**, les pièces jointes ne s’affichent pas. Par conséquent, ils n’apparaissent pas lorsque la tâche est ouverte à partir de la boîte de réception. Les fichiers sont correctement enregistrés dans le référentiel, mais l’interface utilisateur de l’étape Affecter une tâche ne parvient pas à afficher les pièces jointes. (FORMS-23722)

* Lorsqu’un PDF signé numériquement est joint à une tâche dans AEM Forms JEE Workspace, le chargement reste bloqué en statut de chargement ou échoue avec une erreur « Fichier non valide ». Par conséquent, des pièces jointes PDF signées plus volumineuses ne peuvent pas être ajoutées à la tâche. Ce problème est corrigé dans une version ultérieure. Pour obtenir un correctif concernant cette version, contactez l’assistance Adobe. (FORMS-28517)

#### Problèmes connus liés aux correctifs disponibles {#aem-forms-issues-with-hotfixes}

Un correctif logiciel peut être téléchargé et installé pour les problèmes suivants. Pour résoudre ces problèmes, vous pouvez [télécharger et installer le correctif](/help/release-notes/aem-forms-hotfix.md) :

* Après l’installation du pack de services 21 d’AEM Forms JEE (6.5.21.0), si vous trouvez des entrées en double de Geode jars `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)` sous le dossier `<AEM_Forms_Installation>/lib/caching/lib`, procédez comme suit pour résoudre le problème (FORMS-14926) :

  1. Arrêtez les localisateurs s’ils sont en cours d’exécution.
  1. Arrêtez le serveur AEM.
  1. Accédez à `<AEM_Forms_Installation>/lib/caching/lib`.
  1. Supprimez tous les fichiers de correctifs Geode, à l’exception de `geode-*-1.15.1.2.jar`. Confirmez que seuls les fichiers JAR Geode avec `version 1.15.1.2` sont présents.
  1. Ouvrez l’invite de commande en mode d’administration.
  1. Installez le correctif Geode à l’aide du fichier `geode-*-1.15.1.2.jar`.

## Lots OSGi et modules de contenu inclus{#osgi-bundles-and-content-packages-included}

Les fichiers zip suivants contiennent les documents texte qui répertorient les lots OSGi et les packages de contenu inclus dans cette version du pack de services [!DNL Experience Manager] 6.5 :

* [Liste des lots OSGi inclus dans Experience Manager 6.5.26.0](/help/release-notes/assets/65260-bundles.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->
* [Liste des packages de contenu inclus dans Experience Manager 6.5.26.0](/help/release-notes/assets/65260-packages.zip)
<!-- UPDATE FOR EACH NEW RELEASE -->

## Sites web à accès limité{#restricted-sites}

Ces sites web sont disponibles uniquement pour les clients et clientes. Si vous êtes client et avez besoin d’un accès, contactez votre gestionnaire de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* [Contacter l’assistance clientèle Adobe](https://experienceleague.adobe.com/fr/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience#).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] page produit](https://business.adobe.com/fr/products/experience-manager/adobe-experience-manager.html)
>* Documentation [[!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/fr/docs/experience-manager-65)
>* [S’abonner aux mises à jour de produits prioritaires d’Adobe](https://www.adobe.com/fr/subscription/priority-product-update.html)




