---
title: '[!DNL Experience Manager] Notes de mise à jour du Service Pack 6.5'
description: Notes de mise à jour spécifiques à  [!DNL Adobe Experience Manager] Service Pack 8 6.5
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: 024f03c04a980c544ac59e736caeaa24f7565582
workflow-type: tm+mt
source-wordcount: '3409'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager] Notes de mise à jour du Service Pack 6.5  {#aem-service-pack-release-notes}

## Informations sur la version {#release-information}

| Produits | [!DNL Adobe Experience Manager] 6,5 |
| -------- | ---------------------------- |
| Version | 6.5.8.0 |
| Type | Version du Service Pack |
| Date | 11 mars 2021 |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip) |

<!-- TBD: Update the SD link when SP8 is available. Same link is duplicated below in install -->

## Éléments inclus dans [!DNL Adobe Experience Manager] 6.5.8.0 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] La version 6.5.8.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les clients, ainsi que des améliorations en termes de performances, de stabilité et de sécurité, publiées depuis la version 6.5 d’avril 2019. Le Service Pack est installé sur [!DNL Adobe Experience Manager] 6.5.

Les fonctionnalités et améliorations clés introduites dans [!DNL Adobe Experience Manager] 6.5.8.0 sont les suivantes :

<!-- TBD:
* Using the Connected Assets functionality, it is now possible to connect up to 3 [!DNL Sites] instances with 1 [!DNL Assets] instances. The configuration user interface now allows the administrators to provide the details of these [!DNL Sites] instances. -->

* Lors de l’utilisation de la fonction [Ressources connectées](/help/assets/use-assets-across-connected-assets-instances.md), vous pouvez désormais afficher la liste de toutes les pages [!DNL Sites] qui utilisent la ressource. Ces références à une ressource sont disponibles dans la page [!UICONTROL Propriétés] d’une ressource. Cela permet aux administrateurs, aux spécialistes du marketing et aux bibliothécaires d’avoir une vue complète de l’utilisation des ressources, ce qui permet un meilleur suivi, une meilleure gestion et une meilleure cohérence de la marque.

* Lors de la suppression d’une ressource référencée dans une page web, [!DNL Experience Manager] [affiche un avertissement](/help/assets/use-assets-across-connected-assets-instances.md#asset-usage-references). Vous pouvez forcer la suppression d’une ressource référencée ou vérifier et modifier les références affichées dans la page [!DNL Properties] de la ressource. Cliquer sur les références ouvre les pages [!DNL Sites] locales et distantes.

* Tri des pages Live Copy disponibles pour déploiement à l’aide des propriétés [!UICONTROL Nom], [!UICONTROL Date de dernière modification,] et [!UICONTROL Date du dernier déploiement].

* Le référentiel intégré (Apache Jackrabbit Oak) a été mis à niveau vers la  1.22.6. <!-- TBD: Mention the version -->

Pour obtenir la liste complète des fonctionnalités et améliorations introduites dans [!DNL Experience Manager] 6.5.8.0, voir [les nouveautés de [!DNL Adobe Experience Manager] 6.5 Service Pack 8](new-features-latest-service-pack.md).

Voici la liste des correctifs fournis dans la version [!DNL Experience Manager] 6.5.8.0.

### [!DNL Sites] {#sites-6580}

* Lorsqu’une page est déplacée vers le plan directeur, la destination des liens n’est pas mise à jour (NPR-35724).
* Le lecteur basé sur Tizen ne parvient pas à s’authentifier sur certains navigateurs. Le problème se produit avec les navigateurs qui ne prennent pas en charge l’attribut samesite=none (NPR-35589).
* Un conteneur réactif déverrouillé n’affiche pas les composants autorisés (NPR-35565).
* Lorsque vous créez une Live Copy d’une nouvelle page ajoutée, le gabarit de langue crée deux copies pour chaque domaine (NPR-35545).
* Un blocage dans le registre des composants SCR lorsque de nombreux threads sont bloqués en raison du minuteur `org.apache.felix.scr.impl.ComponentRegistry`. Par conséquent, [!DNL Experience Manager] cesse de répondre pour une durée indéterminée (GRANITE-33125,FELIX-6252).
* Lorsque vous recherchez une ressource spécifique dans le rail latéral, le résultat contient des ressources non recherchées (NPR-35524).
* Lorsque vous activez SSL pour une instance de Experience Manager, le chemin d’accès au contexte est supprimé (NPR-35477).
* Lorsque vous créez une liste, ajoutez du texte comme premier élément, ajoutez un tableau comme second élément, puis ajoutez une liste à l’intérieur du tableau, la liste parent se déforme (NPR-35465).
* Lorsque vous utilisez différents modules externes sur des éléments de liste consécutifs, une balise <br> supplémentaire est ajoutée aux éléments de liste (NPR-35464).
* Lorsqu’une liste est placée entre deux paragraphes, vous ne pouvez pas ajouter de tableau à la liste (NPR-35356).
* Lorsque vous démarrez une mise à niveau de l’instance d’AEM d’AEM 6.3 vers la version 6.5, l’instance de mise à niveau prend plus de temps à démarrer (NPR-35323).
* Lorsque vous répliquez une ressource AEM qui inclut un crochet (). dans le nom, la réplication échoue (GRANITE-27004, NPR-35315).
* Lorsque vous ajoutez des en-têtes à un éditeur de texte enrichi, le bouton de paragraphe est désactivé (NPR-35256).
* Lorsque vous ajoutez un élément à une liste existante, il supprime la liste réductible ou basculable suivante (NPR-35206).
* Lorsque l’option Page de déploiement est sélectionnée, une boîte de dialogue contenant toutes les Live Copies disponibles s’affiche et le déploiement automatique a lieu. Les Live Copies des pages sont déployées dans toutes les zones géographiques sans action de l’utilisateur (NPR-35138).
* Lorsque vous utilisez l’option d’inclusion des enfants, l’option Gérer la publication ne répertorie pas toutes les pages. Seuls 22 pages sont répertoriées (NPR-35086).
* Lorsqu’une stratégie est modifiée, le composant de texte ne conserve pas les modifications de stratégie (NPR-35070).
* Lors de la mise en retrait de certains éléments dans une liste numérotée, tous les éléments conservent le même numéro bien que la numérotation doit commencer à 1 pour les éléments avec le même retrait (CQ-4313011).
* Lorsque la minification est activée, vous ne pouvez pas modifier de page ou de composant. Les problèmes ont commencé après l’installation AEM Service Pack 7 6.5 (CQ-4311133).
* Les filtres de recherche et de ressources omni renvoient des résultats non pertinents ou non (CQ-4312322, NPR-35793).
* Lorsque plusieurs pages accèdent simultanément à une bibliothèque cliente, le gestionnaire de bibliothèques HTML ne parvient pas à charger la bibliothèque cliente. Cela entraîne un rendu incorrect des pages (NPR-35538).
* Le chemin d’accès au contexte est supprimé automatiquement lorsque vous configurez un protocole SSL dans [!DNL Experience Manager] (NPR-35294).
* Le gestionnaire de modules ne déconnecte pas les utilisateurs après avoir cliqué sur l’option Déconnexion (NPR-35160).

### [!DNL Assets] {#assets-6580}

[!DNL Adobe Experience Manager] La version 6.5.8.0  [!DNL Assets] corrige les problèmes suivants et apporte les améliorations suivantes.

* Lors de la restauration d’une version précédente d’une ressource, l’événement DamEvent.Type RESTORED n’est pas déclenché dans la console OSGi (NPR-35789).
* `IndexWriter.merge` provoque  `OutOfMemoryError` une erreur, car la fonctionnalité de balisage intelligent crée des  `/oak:index/lucene` index et des  `/oak:index/ntBaseLucene` index volumineux (NPR-35651).
* Un message d’erreur s’affiche lorsque vous essayez d’enregistrer un dossier de type [!UICONTROL Contribution des ressources] dont le nom contient des caractères à plusieurs octets (NPR-35605).
* Lorsque des champs de sous-type de métadonnées en cascade sont utilisés, une erreur &quot;Veuillez remplir ce champ&quot; incorrecte se produit (NPR-35643).
* Lorsqu’une ressource existante est glissée-déposée sur l’interface utilisateur [!DNL Assets] et qu’une nouvelle version est créée, les modifications apportées aux métadonnées ne sont pas persistantes (NPR-34940).
* Lors de la création de règles dans l’éditeur de schéma de métadonnées pour un menu en cascade, l’option [!UICONTROL Dépendre de] répète le même nom (NPR-35596).
* La recherche par analogie ne fonctionne pas après la modification de [!UICONTROL Rail de recherche d’administrateurs de ressources] (NPR-35588).
* Dans un dossier, si vous ouvrez la recherche de ressources dans le rail de gauche en cliquant sur [!UICONTROL Filtrer], le filtre dans [!UICONTROL État] > [!UICONTROL Passage en caisse] > [!UICONTROL Extraits] ne fonctionne pas (NPR-35530).
* Si vous tentez de supprimer toutes les balises intelligentes d’une ressource et d’enregistrer les modifications, les balises ne sont pas supprimées. Toutefois, l’interface utilisateur indique que les modifications sont enregistrées (NPR-35519).
* Les utilisateurs ne peuvent pas réorganiser ni trier les ressources en mode Liste dans un dossier organisable (NPR-35516).
* Si vous modifiez le schéma de métadonnées par défaut, le champ de balises de la page [!UICONTROL Propriétés] de la ressource se transforme en champ de texte. La modification permet aux utilisateurs inconscients d’ajouter des balises à la demande et les balises sont stockées sous la forme d’une chaîne dans le référentiel (NPR-35478).
* Lors du téléchargement d’une ressource, si vous indiquez un nom ne disposant pas d’adresse électronique valide, l’option de téléchargement est indisponible. Toutefois, si une autre option de la boîte de dialogue de téléchargement est sélectionnée, le bouton est activé, mais aucun email n’est envoyé (NPR-35365).
* Les utilisateurs ne peuvent pas archiver des ressources après les avoir modifiées dans [!DNL Adobe InDesign] et reçoivent une erreur au sujet de l’absence d’autorisations (NPR-35341).
* La bibliothèque JavaScript Handlebars est mise à niveau vers la version 4.7.6 (NPR-35333).
* L’interface de l’éditeur de métadonnées cesse de fonctionner comme prévu lorsque vous commencez à modifier et à désélectionner des éléments de métadonnées en masse jusqu’à ce qu’un seul élément reste sélectionné (NPR-35144).
* La navigation globale n’ouvre pas la console correcte lorsque l’utilisateur clique dans la page `assets.html` (CQ-4312311).
* [!DNL Assets] n’affiche pas le rendu RVB pour une ressource dont le rendu est RVB (CQ-4310190).
* L’option [!UICONTROL Relate] du menu ne s’affiche pas correctement dans la page [!UICONTROL Propriétés] (CQ-4310188).
* Si le filtre filetype pour les documents est utilisé pour rechercher des ressources et créer une collection dynamique, le filtre n’est pas appliqué lors de l’accès à la collection. À la place, tous les types de ressources sont affichés dans la recherche (NPR-35759).
* Vous ne pouvez pas faire glisser et ajouter des ressources dans un Lightbox à partir de l’interface utilisateur [!DNL Assets] (NPR-35901).
* Lorsqu’une nouvelle version d’une ressource existante est créée après la résolution du conflit de dénomination, les métadonnées de la ressource d’origine sont écrasées (CQ-4313594).
* Lorsque vous filtrez la recherche de ressources à l’aide d’un filtre ou d’un prédicat de recherche, ouvrez une ressource pour l’afficher ou la modifier, puis revenez à la page des résultats de la recherche, le filtre ne fonctionne pas. Toutes les ressources recherchées sont répertoriées sans filtre (NPR-35913).

#### [!DNL Dynamic Media] {#dynamic-media-6580}

* L’option URL du paramètre d’image prédéfini RESS est activée sur la page des détails de la ressource. Désormais, les options URL et RESS sont disponibles sur la page des détails de la ressource lorsque le paramètre d’image prédéfini RESS est sélectionné dans la section des rendus dynamiques. (CQ-4311241)
* Composant de média interactif : la vidéo interactive ne fonctionne pas si l’utilisateur possède [!DNL Experience Manager] avec la configuration de publication sélective (CQ-4311054).
* Si vous déplacez des ressources dans des dossiers, la synchronisation entre [!DNL Experience Manager] et [!DNL Dynamic Media–Scene7] via l’API est très lente (CQ-4310001).
* Lors de l’utilisation de l’omni-recherche, la taille des journaux augmente considérablement (CQ-4309153).
* Lorsque la synchronisation sélective est activée et qu’une ressource est copiée (et non déplacée) dans un dossier de synchronisation, elle ne se synchronise pas comme prévu (CQ-4307122).
* Pour les ressources chargées qui sont automatiquement publiées dans DM, l’état ne s’affiche pas Publié sur AEM. En outre, la colonne État de publication de Dynamic Media n’affiche pas l’état de publication correct (CQ-4306415).
* Si une ressource est publiée sur [!DNL Experience Manager] et est définie pour la publication sur [!DNL Dynamic Media] lors de l’activation, la valeur de métadonnées `scene7FileStatus` ne se met pas à jour comme prévu (CQ-4308269).
* Lors de la modification du profil vidéo, [!DNL Experience Manager] n’affiche pas les valeurs de hauteur et de débit binaire définies pour le paramètre vidéo prédéfini. Les champs apparaissent vides (CQ-4311828).

### [!DNL Commerce] {#commerce-6580}

* Impossible de créer une balise personnalisée pour tous les produits dans Commerce (CQ-4310682).

* La mise à jour de la référence des ressources du produit entraîne l’état d’attente des threads de réplication jusqu’à ce que le thread ProductAssetListener termine ses validations dans le JCR (NPR-35269).

### Plate-forme {#platform-6580}

* Lorsque vous utilisez un composant Vue de l’onglet Coral sans onglets, puis que vous déclenchez un validateur Foundation, l’erreur suivante se produit (NPR-35636) :

   ```TXT
    Uncaught TypeError: Cannot set property 'invalid' of undefined
     at enable (foundation.js:10703)
     at foundation.js:10710
   ```

* La réplication de transfert SCD échoue pour les événements de suppression pour les noeuds qui incluent une virgule dans le nom (NPR-35191).

* Après la mise à niveau vers AEM 6.5.7, les builds commencent à échouer. En effet, une ancienne version ou aucun jackson-core n’est incorporé dans l’uber-jar (GRANITE-33006).

### Interface utilisateur {#ui-6580}

* Lorsque vous passez du mode Carte au mode Liste pour les documents d’un dossier dans la console Ressources, le tri ne fonctionne pas correctement (NPR-35842).

* Lorsque vous insérez un hyperlien dans un composant de texte, la fonction de recherche n’affiche pas les résultats appropriés (NPR-35849).

* Lorsqu’une valeur n’est pas fournie à un champ masqué marqué obligatoire, cela vous empêche d’enregistrer un composant (NPR-35219).

### Intégrations {#integrations-6580}

* Lorsque vous utilisez des valeurs différentes pour l’ID de tenant IMS et le code client Target, [!DNL Experience Manager] ne parvient pas à s’intégrer à [!DNL Adobe Target] (NPR-35342).

### Projets de traduction {#translation-6580}

* Problèmes lors de l’export ou de l’import d’une tâche de traduction dans [!DNL Experience Manager] (NPR-35259).

### Campagne {#campaign-6580}

* Lorsque vous créez une page de campagne à l’aide d’un modèle d’usine dans l’interface utilisateur tactile et que vous ouvrez l’onglet Courrier électronique dans la boîte de dialogue Propriétés de la page, la variable de personnalisation pour l’objet et les champs de corps reste désactivée (CQ-4312388).

### [!DNL Communities] {#communities-6580}

* Lors de l’ajout d’une structure de page à un groupe de communautés, le titre [!UICONTROL Groupe] du chemin de navigation est remplacé par le titre du premier [!UICONTROL Page] (NPR-35803).
* Contrairement aux modérateurs, un membre standard de la communauté ne peut accéder à aucune publication préliminaire ni la modifier (NPR-35339).
* Contrôle d’accès rompu et déni de service avec `DSRPReindexServlet`, ce qui réduit le site des communautés jusqu’à ce que l’indexation soit terminée (NPR-35591).
* La suppression de [!UICONTROL Tous les utilisateurs] du champ [!UICONTROL Administrateurs] ne les supprime pas du serveur principal (NPR-35592, NPR-35611).
* Le composant [!UICONTROL Composer le message] ne renvoie aucun résultat lorsque le texte saisi est une correspondance partielle (NPR-35666).

* Vous pouvez constater un certain impact sur les performances et une certaine lenteur lorsque vous essayez d’ajouter des balises à un nouveau blog en sélectionnant **[!UICONTROL Ajouter des balises]**. Pour améliorer les performances, installez le correctif [cqTagLucene-0.0.1.zip](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cqTagLucene-0.0.1.zip).

### [!DNL Brand Portal] {#brandportal-6580}

* L’ajout d’un membre à un dossier de type [!UICONTROL Contribution des ressources] affiche la légende [!UICONTROL Ajouter un utilisateur ou un groupe] dans l’interface utilisateur, bien que seuls les utilisateurs principaux de Brand Portal soient pris en charge et non les groupes (NPR-35332).

### [!DNL Forms] {#forms-6580}

>[!NOTE]
>
>[!DNL Experience Manager Forms] publie les packages de modules complémentaires une semaine après la date de publication prévue du Service Pack [!DNL Experience Manager].

**Formulaires adaptatifs**

* Lorsque vous insérez un tableau avec une ligne répétable dans un panneau répétable contenant plusieurs instances dans un formulaire adaptatif, le tableau est toujours ajouté à la première instance du panneau (NPR-35635).

* Lorsque la mise au point de l’onglet atteint à nouveau le composant CAPTCHA après sa vérification réussie dans un formulaire adaptatif, [!DNL Experience Manager Forms] affiche le message d’erreur `Provide Captcha phrase to proceed` (NPR-35539).

**Communication interactive**

* Lorsque vous envoyez un formulaire traduit, les messages d&#39;envoi s&#39;affichent en anglais et ne sont pas traduits dans la langue appropriée (NPR-35808).

* Lorsque vous incluez une condition de masquage dans le fichier XDP ou les fragments de document joints, le chargement de la communication interactive échoue (NPR-35745).

**Correspondence Management**

* Lorsque vous modifiez une lettre, le chargement des modules contenant des conditions prend plus de temps (NPR-35325).

* Lorsque vous sélectionnez, dans le volet de navigation de gauche, une ressource qui n’est pas incluse dans une lettre, puis la ressource suivante, la mise en surbrillance bleue n’est pas supprimée de la ressource précédemment sélectionnée (NPR-35851).

* Lorsque vous modifiez des champs de texte dans une lettre, [!DNL Experience Manager Forms] affiche le message d’erreur `Text Edit Failed` (CQ-4313770).

**Processus**

* Lorsque vous essayez d’ouvrir un formulaire adaptatif sur une application mobile [!DNL Experience Manager Forms] pour iOS, l’application s’arrête pour répondre (CQ-4314825).

* L’onglet [!UICONTROL Tâches] de l’espace de travail HTML affiche des caractères HTML (NPR-35298).

**XMLFM**

* Lorsque vous générez un document XML à l’aide du service Output, l’erreur `OutputServiceException` se produit pour certains fichiers XML (CQ-4311341, CQ-4313893).

* Lorsque vous appliquez la propriété exposant au premier caractère de la puce, la taille de la puce est réduite (CQ-4306476).

* Les PDF forms générés à l’aide du service Output n’incluent pas de bordures (CQ-4312564).

**Designer**

* Lorsque vous ouvrez un fichier XDP dans [!DNL Experience Manager Forms] Designer, un fichier designer.log est généré dans le même dossier que le fichier XDP (CQ-4309427, CQ-4310865).

**Formulaires HTML5**

* Lorsque vous cochez une case dans un formulaire adaptatif dans un navigateur web [!DNL Safari] pour [!DNL iOS 14.1 or 14.2], les champs supplémentaires ne s’affichent pas (NPR-35652).

**Gestion de Forms**

* Aucun message de confirmation n’indique le téléchargement massif réussi des fichiers XDP vers le référentiel CRX (NPR-35546).

**Document Security**

* Plusieurs problèmes signalés pour l’option [!UICONTROL Modifier la stratégie] sur AdminUI (NPR-35747).

Pour plus d’informations sur les mises à jour de sécurité, voir la [page Bulletins de sécurité des Experience Manager](https://helpx.adobe.com/security/products/experience-manager.html).

## Installation de la version 6.5.8.0 {#install}

**Configuration des exigences et informations supplémentaires**

* Experience Manager 6.5.8.0 nécessite Experience Manager 6.5. Voir [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour obtenir des instructions détaillées.
* Le téléchargement du Service Pack est disponible sur l’Adobe [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Sur un déploiement avec MongoDB et plusieurs instances, installez Experience Manager 6.5.8.0 sur l’une des instances d’auteur à l’aide du gestionnaire de modules.

>[!NOTE]
>
>Adobe ne recommande pas de supprimer ou de désinstaller le package [!DNL Adobe Experience Manager] 6.5.8.0.

### Installer le Service Pack {#install-service-pack}

Pour installer le Service Pack sur une instance [!DNL Adobe Experience Manager] 6.5, procédez comme suit :

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (et c’est le cas lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande également un redémarrage si le temps de disponibilité actuel d’une instance est élevé.

1. Avant l’installation, prenez un instantané ou une nouvelle sauvegarde de votre instance [!DNL Experience Manager].

1. Téléchargez le Service Pack à partir de [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip).

1. Ouvrez Package Manager et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package. Pour en savoir plus, voir [Gestionnaire de modules](/help/sites-administering/package-manager.md).

1. Sélectionnez le package et cliquez sur **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du Service Pack, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Voir [Entrepôt de données Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface utilisateur de Package Manager se ferme parfois pendant l’installation du Service Pack. Adobe recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les logs spécifiques liés à la désinstallation du lot de mise à jour avant de vous assurer que les installations sont réussies. En règle générale, cela se produit sur [!DNL Safari] mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Il existe deux manières d’installer automatiquement Adobe Experience Manager 6.5.8.0 sur une instance de travail :

A. Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.

B. Utilisez l’API [HTTP du gestionnaire de modules](/help/sites-administering/package-manager.md#package-share). Utilisez `cmd=install&recursive=true` pour que les packages imbriqués soient installés.

>[!NOTE]
>
>Adobe Experience Manager 6.5.8.0 ne prend pas en charge l’installation de Bootstrap.

**Validation de l’installation**

1. La page d’informations sur les produits (`/system/console/productinfo`) affiche la chaîne de version mise à jour `Adobe Experience Manager (6.5.8.0)` sous [!UICONTROL Produits installés].

1. Tous les lots OSGi sont **[!UICONTROL PRINCIPAL]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (utiliser la console web : `/system/console/bundles`).

1. Le lot OSGi `org.apache.jackrabbit.oak-core` est version 1.22.3 ou ultérieure (Utiliser la console web : `/system/console/bundles`).

Pour connaître les plates-formes certifiées pour fonctionner avec cette version, voir les [exigences techniques](/help/sites-deploying/technical-requirements.md).

### Installer le module complémentaire Adobe Experience Manager Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Ignorez si vous n’utilisez pas Experience Manager Forms. Les correctifs dans Experience Manager Forms sont fournis par le biais d’un module complémentaire distinct une semaine après la publication du Service Pack [!DNL Experience Manager] planifiée.

1. Vérifiez que vous avez installé le Service Pack Adobe Experience Manager.
1. Téléchargez le module complémentaire Forms correspondant répertorié dans les [versions AEM Forms](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html) pour votre système d’exploitation.
1. Installez le module complémentaire Forms comme décrit dans [Installation des modules complémentaires AEM Forms](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>AEM 6.5.8.0 comprend une nouvelle version du [module de compatibilité AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases). Si vous utilisez une ancienne version du package de compatibilité AEM Forms et que vous mettez à jour vers AEM 6.5.8.0, installez la dernière version du package après l’installation du package du module complémentaire Forms.

### Installation d’Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Passez cette étape si vous n’utilisez pas AEM Forms sous JEE. Les correctifs d’Adobe Experience Manager Forms on JEE sont fournis via un programme d’installation distinct.

Pour plus d’informations sur l’installation du programme d’installation cumulatif pour Experience Manager Forms on JEE et la configuration après le déploiement, consultez les [notes de mise à jour](jee-patch-installer-65.md).

>[!NOTE]
>
>Après avoir installé le programme d’installation cumulatif pour Experience Manager Forms on JEE, installez le dernier module complémentaire Forms, supprimez le module complémentaire Forms du dossier `crx-repository\install` et redémarrez le serveur.

### UberJar {#uber-jar}

UberJar pour Experience Manager 6.5.8.0 est disponible dans le [référentiel central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.8/).

Pour utiliser UberJar dans un projet Maven, voir [Comment utiliser UberJar](/help/sites-developing/ht-projects-maven.md) et inclure la dépendance suivante dans le POM de votre projet :

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
>UberJar et les autres artefacts associés sont disponibles sur le référentiel central Maven au lieu du référentiel Maven public Maven Adobe (`repo.adobe.com`). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Il n’existe donc pas de `classifier`, avec `apis` comme valeur, pour la balise `dependency`.

## Fonctionnalités obsolètes {#removed-deprecated-features}

Vous trouverez ci-dessous une liste des fonctionnalités marquées comme obsolètes avec la version [!DNL Experience Manager] 6.5.7.0. Les fonctionnalités sont marquées comme obsolètes initialement et supprimées ultérieurement dans une version ultérieure. Une autre option est généralement fournie.

Vérifiez si vous utilisez une fonctionnalité ou une fonctionnalité dans un déploiement. En outre, envisagez de modifier la mise en oeuvre afin d’utiliser une autre option.

| Zone | Fonctionnalité | Remplacement |
|---|---|---|
| Intégrations | L’écran **[!UICONTROL Opt-in des services cloud AEM]** est obsolète. L’intégration de Experience Manager et Adobe Target ayant été mise à jour dans Experience Manager 6.5 afin de prendre en charge l’API Adobe Target Standard, qui utilise l’authentification via l’Adobe IMS et I/O, et le rôle croissant d’Adobe Launch pour l’instrumentalisation de pages de Experience Manager pour l’analyse et la personnalisation, l’assistant de souscription est devenu non pertinent du point de vue fonctionnel. | Configurez les connexions système, l’authentification IMS par Adobe et les intégrations [!DNL Adobe I/O] via les services cloud de Experience Manager respectifs. |
| Connecteurs | Adobe JCR Connector for Microsoft SharePoint 2010 et Microsoft SharePoint 2013 est obsolète pour Experience Manager 6.5. | N/A |

## Problèmes connus {#known-issues}

* Si vous mettez à niveau votre instance [!DNL Experience Manager] de la version 6.5 à la version 6.5.8.0, vous pouvez afficher les exceptions `RRD4JReporter` dans le fichier `error.log`. Redémarrez l’instance pour résoudre le problème.

* Si vous installez [!DNL Experience Manager] 6.5 Service Pack 5 ou un Service Pack précédent sur [!DNL Experience Manager] 6.5, la copie d’exécution du modèle de workflow personnalisé de vos ressources (créée dans `/var/workflow/models/dam`) est supprimée.
Pour récupérer votre copie d’exécution, Adobe recommande de synchroniser la copie d’heure de conception du modèle de workflow personnalisé avec sa copie d’exécution à l’aide de l’API HTTP :
   `<designModelPath>/jcr:content.generate.json`.

* Contactez l’assistance clientèle d’Adobe si vous rencontrez des problèmes lors de la modification et de la création de règles en cascade dans [!UICONTROL Éditeur de Forms de schéma de métadonnées de dossier] et [!UICONTROL Éditeur de Forms de schéma de métadonnées] à l’aide de la boîte de dialogue [!UICONTROL Définir la règle]. Les règles déjà créées et enregistrées fonctionnent comme prévu.

* Si un dossier de la hiérarchie est renommé [!DNL Experience Manager Assets] et que le dossier imbriqué contenant une ressource est publié sur [!DNL Brand Portal], le titre du dossier n’est pas mis à jour dans [!DNL Brand Portal] tant que le dossier racine n’a pas été republié.

* Lorsqu’un utilisateur choisit de configurer un champ pour la première fois dans un formulaire adaptatif, l’option permettant d’enregistrer une configuration ne s’affiche pas dans l’explorateur de propriétés. Sélectionner pour configurer un autre champ du formulaire adaptatif dans le même éditeur résout le problème.

* Si l’assistant [!UICONTROL Configuration des ressources connectées] renvoie un message d’erreur 404 après l’installation, réinstallez manuellement les packages `cq-remotedam-client-ui-content` et `cq-remotedam-client-ui-components` à l’aide du gestionnaire de modules.

* Les erreurs et messages d’avertissement suivants peuvent s’afficher lors de l’installation de Experience Manager 6.5.x.x :
   * &quot;Lorsque l’intégration d’Adobe Target est configurée dans Experience Manager à l’aide de l’API Target Standard (authentification IMS), l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. Au lieu du type « Fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La validation côté serveur du formulaire adaptatif échoue lorsque des fonctions d’agrégat telles que SUM, MAX et MIN sont utilisées (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Aucune fenêtre de maintenance n’a été trouvée sur granite/operations/maintenance.
   * La zone réactive d’une image interactive Dynamic Media n’est pas visible lors de la prévisualisation de la ressource via la visionneuse de bannières Shoppable.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Délai d’attente avant que la modification du reg ne soit terminée sans enregistrement.

## Lots OSGi et packages de contenu {#osgi-bundles-and-content-packages-included}

Les documents texte suivants répertorient les lots OSGi et les packages de contenu inclus dans [!DNL Experience Manager] 6.5.8.0 :

* [Liste des lots OSGi inclus dans Experience Manager 6.5.8.0](assets/6580_bundles.txt)

* [Liste des packages de contenu inclus dans Experience Manager 6.5.8.0](assets/6580_packages.txt)

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

