---
title: '[!DNL Experience Manager] Notes de mise à jour de Service Pack 6.5'
description: Notes de mise à jour spécifiques à  [!DNL Adobe Experience Manager] Service Pack 6.5 8
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: dfaa25ea72e50b60b8a40883ffb0241c131cc846
workflow-type: tm+mt
source-wordcount: '3352'
ht-degree: 5%

---


# [!DNL Adobe Experience Manager] Notes de mise à jour de Service Pack 6.5  {#aem-service-pack-release-notes}

## Informations sur la version {#release-information}

| Produits | [!DNL Adobe Experience Manager] 6,5 |
| -------- | ---------------------------- |
| Version | 6.5.8.0 |
| Type | Version du Service Pack |
| Date | 11 mars 2021 |
| URL de téléchargement | [Distribution de logiciels](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip) |

<!-- TBD: Update the SD link when SP8 is available. Same link is duplicated below in install -->

## Éléments inclus dans [!DNL Adobe Experience Manager] 6.5.8.0 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] La version 6.5.8.0 comprend de nouvelles fonctionnalités, des améliorations clés demandées par les clients, ainsi que des améliorations des performances, de la stabilité et de la sécurité, publiées depuis la version 6.5 d’avril 2019. Le Service Pack est installé sur [!DNL Adobe Experience Manager] 6.5.

Les principales fonctionnalités et améliorations introduites dans [!DNL Adobe Experience Manager] 6.5.8.0 sont les suivantes :

<!-- TBD:
* Using the Connected Assets functionality, it is now possible to connect up to 3 [!DNL Sites] instances with 1 [!DNL Assets] instances. The configuration user interface now allows the administrators to provide the details of these [!DNL Sites] instances. -->

* Lorsque vous utilisez la fonctionnalité [Ressources connectées](/help/assets/use-assets-across-connected-assets-instances.md), vous pouvez désormais vue une liste de toutes les [!DNL Sites] pages qui utilisent la ressource. Ces références à une ressource sont disponibles dans la page [!UICONTROL Propriétés] d&#39;une ressource. Cela permet aux administrateurs, aux marketeurs et aux bibliothécaires d’avoir une vue complète de l’utilisation des ressources, ce qui permet un meilleur suivi, une meilleure gestion et une meilleure cohérence de la marque.

* Lors de la suppression d’un élément référencé dans une page Web, [!DNL Experience Manager] [affiche un avertissement](/help/assets/use-assets-across-connected-assets-instances.md#asset-usage-references). Vous pouvez forcer la suppression d’une ressource référencée ou vérifier et modifier les références affichées dans la page [!DNL Properties] de la ressource. Cliquez sur les références pour ouvrir les pages locales et distantes [!DNL Sites].

* Tri des pages Live Copy disponibles pour le déploiement à l’aide des propriétés [!UICONTROL Name], [!UICONTROL Date de la dernière modification,] et [!UICONTROL Date de la dernière exécution].

* Le référentiel intégré (Apache Jackrabbit Oak) a été mis à niveau vers la  1.22.6. <!-- TBD: Mention the version -->

Pour une liste complète des fonctionnalités et améliorations introduites dans [!DNL Experience Manager] 6.5.8.0, voir [ce qui est nouveau dans  [!DNL Adobe Experience Manager] 6.5 Service Pack 8](new-features-latest-service-pack.md).

Voici la liste des correctifs fournis dans la version [!DNL Experience Manager] 6.5.8.0.

### [!DNL Sites] {#sites-6580}

* Lorsqu&#39;une page est déplacée vers le plan directeur, la destination des liens n&#39;est pas mise à jour (NPR-35724).
* Le lecteur basé sur les balises ne parvient pas à s’authentifier sur certains navigateurs. Le problème se produit avec les navigateurs qui ne prennent pas en charge l’attribut samesite=none (NPR-35589).
* Un conteneur réactif déverrouillé n&#39;affiche pas les composants autorisés (NPR-35565).
* Lorsque vous créez une copie dynamique d’une nouvelle page ajoutée, le gabarit de langue crée deux copies pour chaque domaine (NPR-35545).
* Déblocage dans le registre des composants SCR lorsque de nombreux threads sont bloqués en raison du minuteur `org.apache.felix.scr.impl.ComponentRegistry`. Par conséquent, [!DNL Experience Manager] cesse de répondre pour une durée indéterminée (GRANITE-33125, FELIX-6252).
* Lorsque vous recherchez un élément spécifique dans le rail latéral, le résultat contient des éléments non recherchés (NPR-35524).
* Lorsque vous activez SSL pour une instance de Experience Manager, le chemin de contexte est supprimé (NPR-35477).
* Lorsque vous créez une liste, ajoutez du texte en tant que premier élément, ajoutez un tableau en tant que second élément et ajoutez une liste dans le tableau, la liste parent se déforme (NPR-35465).
* Lorsque vous utilisez des modules externes différents sur des éléments de liste consécutifs, une balise <br> supplémentaire est ajoutée aux éléments de liste (NPR-35464).
* Lorsqu&#39;une liste est placée entre deux paragraphes, vous ne pouvez pas ajouter de tableau à la liste (NPR-35356).
* Lorsque vous début une mise à niveau d&#39;une instance AEM de AEM 6.3 à l&#39; 6.5, l&#39;instance de mise à niveau prend plus de temps pour être début (NPR-35323).
* Lorsque vous dupliquez un élément AEM qui inclut un crochet (). dans le nom, la réplication échoue (GRANITE-27004, NPR-35315).
* Lorsque vous ajoutez des en-têtes à un éditeur de texte enrichi, le bouton de paragraphe est désactivé (NPR-35256).
* Lorsque vous ajoutez un élément à une liste existante, il supprime la liste réductible ou de basculement suivante (NPR-35206).
* Lorsque l’option de page Déploiement est sélectionnée, une boîte de dialogue contenant toutes les copies dynamiques disponibles s’affiche et le déploiement automatique s’effectue. Les copies en direct des pages sont déployées dans tous les pays sans l’intervention de l’utilisateur (NPR-35138).
* Lorsque vous utilisez l’option Inclure les enfants, l’option Gérer la publication ne liste pas toutes les pages. Seuls 22 pages sont répertoriées (NPR-35086).
* Lorsqu&#39;une stratégie est modifiée, le composant de texte ne conserve pas les modifications de stratégie (NPR-35070).
* Lors de la mise en retrait de certains éléments dans une liste numérotée, tous les éléments conservent le même numéro bien que la numérotation doive début de 1 pour les éléments avec le même retrait (CQ-4313011).
* Lorsque la minification est activée, vous ne pouvez pas modifier de page ou de composant. Les problèmes ont commencé après l’installation de AEM 6.5 Service Pack 7 (CQ-4311133).
* Les filtres de recherche et de ressources Omni renvoient des résultats non pertinents ou sans résultat (CQ-4312322, NPR-35793).
* Lorsque plusieurs pages accèdent simultanément à une bibliothèque cliente, le gestionnaire de bibliothèques HTML ne parvient pas à charger la bibliothèque cliente. Cela entraîne un mauvais rendu des pages (NPR-35538).
* Le chemin de contexte est automatiquement supprimé lorsque vous configurez un protocole SSL dans [!DNL Experience Manager] (NPR-35294).
* Package Manager ne déconnecte pas les utilisateurs après avoir cliqué sur l’option Déconnexion (NPR-35160).

### [!DNL Assets] {#assets-6580}

[!DNL Adobe Experience Manager] La version 6.5.8.0  [!DNL Assets] corrige les problèmes suivants et apporte les améliorations suivantes.

* Lors de la restauration d’une version précédente d’une ressource, le événement DamEvent.Type RESTORED n’est pas déclenché dans la console OSGi (NPR-35789).
* `IndexWriter.merge` provoque  `OutOfMemoryError` des erreurs, car la fonctionnalité de balisage intelligent crée de grands  `/oak:index/lucene` index et des  `/oak:index/ntBaseLucene` index (NPR-35651).
* Un message d’erreur s’affiche lorsque vous tentez d’enregistrer un dossier de type [!UICONTROL Asset Contribution] avec des caractères multioctets dans le nom (NPR-35605).
* Lorsque des champs de sous-type de métadonnées en cascade sont utilisés, une erreur &quot;Veuillez remplir ce champ&quot; incorrecte se produit (NPR-35643).
* Lorsqu’un fichier existant est glissé vers l’interface utilisateur [!DNL Assets] et qu’une nouvelle version est créée, les modifications apportées aux métadonnées ne sont pas persistantes (NPR-34940).
* Lors de la création de règles dans l’éditeur de schémas de métadonnées pour un menu en cascade, l’option [!UICONTROL Dépendante de] répète le même nom (NPR-35596).
* La recherche par analogie ne fonctionne pas après la modification du [!UICONTROL rail de recherche de l’administrateur des ressources] (NPR-35588).
* Dans un dossier, si vous ouvrez la recherche de ressources dans le rail de gauche en cliquant sur [!UICONTROL Filtre], le filtre [!UICONTROL État] > [!UICONTROL Passage en caisse] > [!UICONTROL Passé en caisse] ne fonctionne pas (NPR-35530).
* Si vous tentez de supprimer toutes les balises actives d’un fichier et d’enregistrer les modifications, les balises ne sont pas supprimées. Cependant, l&#39;interface utilisateur indique que les modifications sont enregistrées (NPR-35519).
* Les utilisateurs ne peuvent pas réorganiser ou trier les fichiers dans liste vue dans un dossier pouvant être commandé (NPR-35516).
* Si vous modifiez le schéma de métadonnées par défaut, le champ de balises de la page [!UICONTROL Propriétés] du fichier se transforme en champ de texte. Cette modification permet aux utilisateurs inconscients d’ajouter des balises à la demande et les balises sont stockées sous la forme d’une chaîne dans le référentiel (NPR-35478).
* Lors du téléchargement d’un fichier, si vous indiquez un nom sans adresse électronique valide, l’option de téléchargement n’est pas disponible. Cependant, si une autre option de la boîte de dialogue de téléchargement est sélectionnée, le bouton est activé, mais aucun message électronique n’est envoyé (NPR-35365).
* Les utilisateurs ne peuvent pas archiver les ressources après avoir modifié celles de [!DNL Adobe InDesign] et reçoivent une erreur au sujet du manque d&#39;autorisations (NPR-35341).
* La bibliothèque JavaScript Handlebars est mise à niveau vers la version 4.7.6 (NPR-35333).
* L’interface de l’éditeur de métadonnées cesse de fonctionner comme prévu lorsque vous effectuez un début à partir des éléments de modification et de désélection de métadonnées en masse jusqu’à ce qu’un seul élément reste sélectionné (NPR-35144).
* La navigation globale n’ouvre pas la console correcte lorsque vous cliquez à partir de la page `assets.html` (CQ-4312311).
* [!DNL Assets] n’affiche pas le rendu RVB pour une ressource dont le rendu est RVB (CQ-4310190).
* L&#39;option [!UICONTROL Relate] du menu ne s&#39;affiche pas correctement dans la page [!UICONTROL Propriétés] (CQ-4310188).
* Si le filtre de type de fichier pour les documents est utilisé pour rechercher des ressources et créer une collection dynamique, le filtre n’est pas appliqué lors de l’accès à la collection. Tous les types de ressources sont affichés dans la recherche (NPR-35759).
* Vous ne pouvez pas faire glisser et ajouter des ressources dans un Lightbox à partir de l&#39;interface utilisateur [!DNL Assets] (NPR-35901).
* Lorsqu’une nouvelle version d’une ressource existante est créée après la résolution du conflit d’affectation de nom, les métadonnées de la ressource d’origine sont remplacées (CQ-4313594).
* Lorsque vous filtrez la recherche de ressources à l’aide d’un filtre de recherche ou d’un prédicat, ouvrez un fichier pour le vue ou le modifier, puis revenez à la page des résultats de la recherche, le filtre ne fonctionne pas. Toutes les ressources recherchées sont répertoriées sans filtre (NPR-35913).

#### [!DNL Dynamic Media] {#dynamic-media-6580}

* L’option URL pour le paramètre d’image prédéfini RESS est activée sur la page des détails du fichier. Désormais, les options URL et RESS sont disponibles sur la page des détails de la ressource lorsque le paramètre d’image prédéfini RESS est sélectionné dans la section Rendus dynamiques. (CQ-4311241)
* Composant multimédia interactif : la vidéo interactive ne fonctionne pas si l’utilisateur dispose de [!DNL Experience Manager] avec une configuration de publication sélective (CQ-4311054).
* Si vous déplacez des fichiers entre des dossiers, la synchronisation entre [!DNL Experience Manager] et [!DNL Dynamic Media–Scene7] via l’API est très lente (CQ-4310001).
* Lors de l’utilisation d’Omnisearch, la taille des journaux augmente considérablement (CQ-4309153).
* Lorsque la synchronisation sélective est activée et qu’une ressource est copiée (non déplacée) dans un dossier de synchronisation, elle n’est pas synchronisée comme prévu (CQ-4307122).
* Pour les fichiers téléchargés qui sont automatiquement publiés vers DM, l’état n’est pas Publié sur AEM. En outre, la colonne d’état Publication de Dynamic Media n’affiche pas l’état de publication correct (CQ-4306415).
* Si un fichier est publié le [!DNL Experience Manager] et défini pour une publication sur [!DNL Dynamic Media] à l’activation, la valeur de métadonnées `scene7FileStatus` n’est pas mise à jour comme prévu (CQ-4308269).
* Lors de la modification du profil vidéo, [!DNL Experience Manager] n’affiche pas les valeurs de hauteur et de débit définies pour le paramètre vidéo prédéfini. Les champs s’affichent en blanc (CQ-4311828).

### [!DNL Commerce] {#commerce-6580}

* Impossible de créer une balise personnalisée pour tous les produits dans Commerce (CQ-4310682).

* La mise à jour de la référence des ressources du produit entraîne l&#39;état d&#39;attente des threads de réplication jusqu&#39;à ce que le thread ProductAssetListener termine ses engagements au JCR (NPR-35269).

### Plate-forme {#platform-6580}

* Lorsque vous utilisez un composant de Vue d’onglets Coral sans onglets, puis que vous déclenchez un validateur Foundation, l’erreur suivante se produit (NPR-35636) :

   ```TXT
    Uncaught TypeError: Cannot set property 'invalid' of undefined
     at enable (foundation.js:10703)
     at foundation.js:10710
   ```

* La réplication de transfert SCD échoue pour les événements de suppression pour les noeuds qui incluent une virgule dans le nom (NPR-35191).

* Après la mise à niveau vers AEM 6.5.7, le début de génération échoue. La raison en est qu&#39;une ancienne version ou qu&#39;aucun noyau de jackson n&#39;est intégré dans l&#39;uber-jar (GRANITE-33006).

### Interface utilisateur {#ui-6580}

* Lorsque vous passez de la vue Carte à la vue Liste pour les documents d’un dossier dans la console Ressources, le tri ne fonctionne pas correctement (NPR-35842).

* Lorsque vous liez du texte dans un composant de texte, la fonction de recherche n&#39;affiche pas les résultats appropriés (NPR-35849).

* Lorsqu’une valeur n’est pas fournie à un champ masqué marqué obligatoire, elle vous empêche d’enregistrer un composant (NPR-35219).

### Intégrations {#integrations-6580}

* Lorsque vous utilisez des valeurs différentes pour l’ID de client IMS et le code client de Cible, [!DNL Experience Manager] ne parvient pas à s’intégrer à [!DNL Adobe Target] (NPR-35342).

### Projets de traduction {#translation-6580}

* Problèmes lors de l&#39;exportation ou de l&#39;importation d&#39;une tâche de traduction dans [!DNL Experience Manager] (NPR-35259).

### Campagne {#campaign-6580}

* Lorsque vous créez une page de campagne à l’aide d’un modèle prêt à l’emploi dans l’interface utilisateur tactile et que vous ouvrez l’onglet Courriel dans la boîte de dialogue Propriétés de la page, la variable de personnalisation des champs d’objet et de contenu reste désactivée (CQ-4312388).

### [!DNL Communities] {#communities-6580}

* Lors de l’ajout d’une structure de page à un groupe de communauté, le titre [!UICONTROL Groupe] dans le chemin de navigation est remplacé par le titre de la première [!UICONTROL page] (NPR-35803).
* Contrairement aux modérateurs, un membre standard de la communauté n&#39;est pas en mesure d&#39;accéder à un brouillon de publication et de le modifier (NPR-35339).
* Contrôle d&#39;accès rompu et déni de service avec DSRPReindexServlet, ce qui réduit le site des communautés jusqu&#39;à ce que l&#39;indexation soit terminée (NPR-35591).
* La suppression de [!UICONTROL Tous les utilisateurs] du champ [!UICONTROL Administrateurs] ne les supprime pas du serveur principal (NPR-35592, NPR-35611).
* Le composant [!UICONTROL Composer le message] ne renvoie aucun résultat lorsque le texte saisi correspond partiellement (NPR-35666).

### [!DNL Brand Portal] {#brandportal-6580}

* L’Ajoute d’un membre à un dossier de type [!UICONTROL Contribution des ressources] affiche la légende [!UICONTROL Ajouter l’utilisateur ou le groupe] dans l’interface utilisateur, bien que seuls les utilisateurs principaux du portail de marque soient pris en charge et non les groupes (NPR-35332).

### [!DNL Forms] {#forms-6580}

>[!NOTE]
>
>[!DNL Experience Manager Forms] publie les packages de modules complémentaires une semaine après la date de publication prévue du Service Pack [!DNL Experience Manager].

**Formulaires adaptatifs**

* Lorsque vous insérez un tableau avec une rangée répétable dans un panneau répétable contenant plusieurs instances dans un formulaire adaptatif, le tableau est toujours ajouté à la première instance du panneau (NPR-35635).

* Lorsque la mise au point de l&#39;onglet atteint à nouveau le composant CAPTCHA après avoir vérifié correctement sa présence dans un formulaire adaptatif, [!DNL Experience Manager Forms] affiche le message d&#39;erreur `Provide Captcha phrase to proceed` (NPR-35539).

**Communication interactive**

* Lorsque vous envoyez un formulaire traduit, les messages d’envoi s’affichent en anglais et ne sont pas traduits dans la langue appropriée (NPR-35808).

* Lorsque vous incluez une condition de masquage dans les fragments XDP ou de document joints, le chargement de la communication interactive échoue (NPR-35745).

**Correspondence Management**

* Lorsque vous modifiez une lettre, le chargement des modules avec des conditions prend plus de temps (NPR-35325).

* Lorsque vous sélectionnez un fichier dans le volet de navigation de gauche qui n&#39;est pas inclus dans une lettre, puis que vous sélectionnez le fichier suivant, la mise en surbrillance bleue n&#39;est pas supprimée de l&#39;actif précédemment sélectionné (NPR-35851).

* Lorsque vous modifiez des champs de texte dans une lettre, [!DNL Experience Manager Forms] affiche le message d’erreur `Text Edit Failed` (CQ-4313770).

**Processus**

* Lorsque vous essayez d’ouvrir un formulaire adaptatif sur une application mobile [!DNL Experience Manager Forms] pour iOS, l’application s’arrête pour répondre (CQ-4314825).

* L’onglet [!UICONTROL Tâches] de l’espace de travail HTML affiche des caractères HTML (NPR-35298).

**XMLFM**

* Lorsque vous générez un document XML à l’aide du service Output, l’erreur `OutputServiceException` se produit pour certains fichiers XML (CQ-4311341, CQ-4313893).

* Lorsque vous appliquez la propriété exposant au premier caractère de la puce, la taille de la puce devient plus petite (CQ-4306476).

* Les PDF forms générés à l’aide du service Output n’incluent pas de bordures (CQ-4312564).

**Designer**

* Lorsque vous ouvrez un fichier XDP dans [!DNL Experience Manager Forms] Designer, un fichier designer.log est généré dans le même dossier que le fichier XDP (CQ-4309427, CQ-4310865).

**Formulaires HTML5**

* Lorsque vous cochez une case dans un formulaire adaptatif dans le navigateur Web [!DNL Safari] pour [!DNL iOS 14.1 or 14.2], d’autres champs ne s’affichent pas (NPR-35652).

**Gestion des Forms**

* Aucun message de confirmation n’indique la réussite du transfert en masse des fichiers XDP vers le référentiel CRX (NPR-35546).

**Document Security**

* Plusieurs problèmes ont été signalés pour l&#39;option [!UICONTROL Modifier la stratégie] sur AdminUI (NPR-35747).

Pour plus d’informations sur les mises à jour de sécurité, voir [Experience Manager security bulletins page](https://helpx.adobe.com/security/products/experience-manager.html).

## Installer 6.5.8.0 {#install}

**Configuration requise et informations supplémentaires**

* Experience Manager 6.5.8.0 requiert Experience Manager 6.5. Voir [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour obtenir des instructions détaillées.
* Le téléchargement du Service Pack est disponible sur l&#39;Adobe [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Lors d’un déploiement avec MongoDB et plusieurs instances, installez Experience Manager 6.5.8.0 sur l’une des instances d’auteur à l’aide de Package Manager.

>[!NOTE]
>
>Adobe ne recommande pas de supprimer ou de désinstaller le package [!DNL Adobe Experience Manager] 6.5.8.0.

### Installer le Service Pack {#install-service-pack}

Pour installer le Service Pack sur une instance [!DNL Adobe Experience Manager] 6.5, procédez comme suit :

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (ce qui est le cas lorsque l’instance a été mise à jour à partir d’une version antérieure). L’Adobe recommande également un redémarrage si le temps de fonctionnement actuel d’une instance est élevé.

1. Avant l&#39;installation, effectuez un instantané ou une nouvelle sauvegarde de votre instance [!DNL Experience Manager].

1. Téléchargez le Service Pack à partir de [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip).

1. Ouvrez Package Manager et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package. Pour en savoir plus, voir [Package Manager](/help/sites-administering/package-manager.md).

1. Sélectionnez le package et cliquez sur **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du Service Pack, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Voir [Banque de données Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface utilisateur de Package Manager se ferme parfois lors de l’installation du Service Pack. Adobe vous recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les journaux spécifiques liés à la désinstallation du lot de mise à jour avant de vous assurer que l&#39;installation est réussie. En règle générale, cela se produit sur [!DNL Safari] mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Il existe deux manières d’installer automatiquement Adobe Experience Manager 6.5.8.0 sur une instance de travail :

R. Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.

B. Utilisez l’API [HTTP de Package Manager](/help/sites-administering/package-manager.md#package-share). Utilisez `cmd=install&recursive=true` pour installer les packages imbriqués.

>[!NOTE]
>
>Adobe Experience Manager 6.5.8.0 ne prend pas en charge l’installation des Bootstrap.

**Validation de l’installation**

1. La page d&#39;informations sur le produit (`/system/console/productinfo`) affiche la chaîne de version mise à jour `Adobe Experience Manager (6.5.8.0)` sous [!UICONTROL Produits installés].

1. Tous les lots OSGi sont soit **[!UICONTROL PRINCIPAL]** soit **[!UICONTROL FRAGMENT]** dans la console OSGi (Utiliser la console Web : `/system/console/bundles`).

1. Le lot OSGi `org.apache.jackrabbit.oak-core` est de la version 1.22.3 ou ultérieure (Utilisez la console Web : `/system/console/bundles`).

Pour connaître les plates-formes certifiées pour fonctionner avec cette version, voir les [exigences techniques](/help/sites-deploying/technical-requirements.md).

### Installer le module complémentaire Adobe Experience Manager Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Ignorez si vous n’utilisez pas le Forms Experience Manager. Les correctifs dans le Forms Experience Manager sont diffusés par le biais d’un module complémentaire distinct une semaine après la publication du Service Pack [!DNL Experience Manager] planifiée.

1. Assurez-vous d’avoir installé le Service Pack de Adobe Experience Manager.
1. Téléchargez le module complémentaire Forms correspondant répertorié dans les [versions AEM Forms](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html) pour votre système d’exploitation.
1. Installez le module complémentaire Forms comme décrit dans [Installation des modules complémentaires AEM Forms](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>AEM 6.5.8.0 inclut une nouvelle version du [package de compatibilité AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases). Si vous utilisez une ancienne version du package de compatibilité AEM Forms et que vous mettez à jour vers AEM 6.5.8.0, installez la dernière version du package après l&#39;installation du package Forms-Ajoute-On.

### Installer Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Passez cette étape si vous n’utilisez pas AEM Forms sous JEE. Les correctifs d’Adobe Experience Manager Forms on JEE sont diffusés par le biais d’un programme d’installation distinct.

Pour plus d’informations sur l’installation cumulative du programme d’installation pour Experience Manager Forms on JEE et sur la configuration après le déploiement, voir les [notes de mise à jour](jee-patch-installer-65.md).

>[!NOTE]
>
>Après avoir installé le programme d’installation cumulatif pour Experience Manager Forms on JEE, installez le dernier module complémentaire Forms, supprimez le module complémentaire Forms du dossier `crx-repository\install`, puis redémarrez le serveur.

### UberJar {#uber-jar}

UberJar pour Experience Manager 6.5.8.0 est disponible dans le [référentiel Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.8/).

Pour utiliser UberJar dans un projet Maven, voir [comment utiliser UberJar](/help/sites-developing/ht-projects-maven.md) et inclure la dépendance suivante dans le POM de votre projet :

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.8</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar et les autres artefacts associés sont disponibles dans le référentiel Maven Central au lieu du référentiel Adobe Public Maven (`repo.adobe.com`). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Il n’existe donc pas de valeur `classifier`, avec `apis`, pour la balise `dependency`.

## Fonctionnalités obsolètes {#removed-deprecated-features}

Vous trouverez ci-dessous une liste de fonctionnalités marquées comme obsolètes avec [!DNL Experience Manager] 6.5.7.0. Les fonctionnalités sont marquées comme obsolètes initialement et ultérieurement supprimées dans une prochaine version. Une autre option est généralement fournie.

Vérifiez si vous utilisez une fonction ou une fonctionnalité dans un déploiement. Par ailleurs, prévoyez de modifier la mise en oeuvre pour utiliser une autre option.

| Zone | Fonctionnalité | Remplacement |
|---|---|---|
| Intégrations | L’écran **[!UICONTROL souscription aux services Cloud AEM]** est obsolète. L&#39;intégration de l&#39;Experience Manager et de Adobe Target ayant été mise à jour dans Experience Manager 6.5 pour prendre en charge l&#39;API Adobe Target Standard, qui utilise l&#39;authentification via l&#39;Adobe IMS et E/S, et le rôle croissant du lancement d&#39;Adobe pour l&#39;instrumentalisation des pages de Experience Manager pour l&#39;analyse et la personnalisation, l&#39;assistant d&#39;inclusion est devenu non pertinent du point de vue fonctionnel. | Configurez les connexions système, l&#39;authentification IMS Adobe et les intégrations [!DNL Adobe I/O] via les services de cloud Experience Manager respectifs. |
| Connecteurs | L’Adobe JCR Connector for Microsoft SharePoint 2010 et Microsoft SharePoint 2013 est obsolète pour Experience Manager 6.5. | N/A |

## Problèmes connus {#known-issues}

* Si vous effectuez une mise à niveau de votre instance [!DNL Experience Manager] de la version 6.5 à la version 6.5.8.0, vous pouvez vue `RRD4JReporter` exceptions dans le fichier `error.log`. Redémarrez l’instance pour résoudre le problème.

* Si vous installez [!DNL Experience Manager] 6.5 Service Pack 5 ou un Service Pack précédent sur [!DNL Experience Manager] 6.5, la copie d&#39;exécution du modèle de flux de travaux personnalisé de vos ressources (créée dans `/var/workflow/models/dam`) est supprimée.
Pour récupérer votre copie d’exécution, l’Adobe recommande de synchroniser la copie au moment de la conception du modèle de flux de travail personnalisé avec sa copie au moment de l’exécution à l’aide de l’API HTTP :
   `<designModelPath>/jcr:content.generate.json`.

* Contactez le service à la clientèle d’Adobe si vous rencontrez des problèmes lors de la modification et de la création de règles en cascade dans [!UICONTROL éditeur Forms de Schéma de métadonnées de dossiers] et [!UICONTROL éditeur de Schéma de métadonnées] à l’aide de la boîte de dialogue [!UICONTROL Définir la règle]. Les règles déjà créées et enregistrées fonctionnent comme prévu.

* Si un dossier de la hiérarchie est renommé [!DNL Experience Manager Assets] et que le dossier imbriqué contenant une ressource est publié dans [!DNL Brand Portal], le titre du dossier n’est pas mis à jour dans [!DNL Brand Portal] tant que le dossier racine n’a pas été publié à nouveau.

* Lorsqu’un utilisateur sélectionne pour la première fois un champ dans un formulaire adaptatif, l’option permettant d’enregistrer une configuration ne s’affiche pas dans le navigateur de propriétés. La sélection pour configurer un autre champ du formulaire adaptatif dans le même éditeur résout le problème.

* Si [!UICONTROL l&#39;Assistant Configuration des ressources connectées] renvoie un message d&#39;erreur 404 après l&#39;installation, réinstallez manuellement les packages `cq-remotedam-client-ui-content` et `cq-remotedam-client-ui-components` à l&#39;aide de Package Manager.

* Les erreurs et les messages d&#39;avertissement suivants peuvent s&#39;afficher lors de l&#39;installation du Experience Manager 6.5.x.x :
   * &quot;Lorsque l’intégration Adobe Target est configurée dans le Experience Manager à l’aide de l’API Target Standard (authentification IMS), l’exportation de fragments d’expérience vers la Cible entraîne la création de types d’offres incorrects. Au lieu du type « Fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégat telles que SUM, MAX et MIN sont utilisées. CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La zone réactive d’une image interactive Dynamic Media n’est pas visible lors de la prévisualisation du fichier via la visionneuse de bannières modifiables.

## bundles OSGi et packages de contenu inclus {#osgi-bundles-and-content-packages-included}

Les documents de texte suivants liste les lots OSGi et les packages de contenu inclus dans [!DNL Experience Manager] 6.5.8.0 :

* [Liste des lots OSGi inclus dans le Experience Manager 6.5.8.0](assets/6580_bundles.txt)

* [Liste des packages de contenu inclus dans le Experience Manager 6.5.8.0](assets/6580_packages.txt)

## Sites Web restreints {#restricted-sites}

Ces sites Web ne sont accessibles qu&#39;aux clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* Voir [comment contacter le service à la clientèle d’Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] Notes de mise à jour 6.5](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] page de produits](https://www.adobe.com/fr/marketing/experience-manager.html)
>* [[!DNL Experience Manager] 6.5 Documentation](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=fr)
>* [Abonnement aux mises à jour de produits prioritaires d’Adobe](https://www.adobe.com/subscription/priority-product-update.html)

