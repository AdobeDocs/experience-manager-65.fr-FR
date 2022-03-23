---
title: Notes de mise à jour d’ [!DNL Adobe Experience Manager] 6,5
description: '"[!DNL Adobe Experience Manager] 6.5 Notes décrivant les informations de mise à jour, les nouveautés, la procédure d’installation et les listes de modifications détaillées."'
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: b654785af72bbe124f7296ae0f8ecb94e7815234
workflow-type: tm+mt
source-wordcount: '3329'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager] 6.5 Dernières notes de mise à jour du Service Pack {#aem-service-pack-release-notes}

## Informations sur la version {#release-information}

| Produits | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.12.0 |
| Type | Version du Service Pack |
| Date  | 24 février 2022 |
| URL de téléchargement | [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.12.0.zip) |

## Éléments compris dans [!DNL Adobe Experience Manager] 6.5.12.0 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] La version 6.5.12.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les clients, ainsi que des améliorations en termes de performances, de stabilité et de sécurité, publiées depuis la version 6.5 d’avril 2019. Le Service Pack est installé sur [!DNL Adobe Experience Manager] 6.5.

Les fonctionnalités et améliorations clés introduites dans [!DNL Adobe Experience Manager] 6.5.12.0 sont :

* Après la configuration d’une connexion entre les déploiements DAM distant et Sites, les ressources sur DAM distant sont disponibles sur le déploiement Sites. Vous pouvez désormais effectuer des opérations de mise à jour, de suppression, de changement de nom et de déplacement sur des ressources ou des dossiers DAM distants. Les mises à jour, avec un certain délai, sont disponibles automatiquement sur le déploiement Sites (NPR-37816).

* Les déploiements push d’une source de Live Copy vers plusieurs Live Copies sont désormais possibles par défaut, sans nécessiter de configuration de plan directeur (CQ-4259951).
* L’état des opérations asynchrones en cours s’affiche désormais dans l’interface utilisateur afin d’empêcher les utilisateurs de déclencher accidentellement plusieurs opérations asynchrones sur le même chemin (NPR-37611).
* La prise en charge de l’authentification IMS est fournie pour les API Analytics 2.0 (CQ-4285474, NPR-37803, NPR-37701, NPR-37702, NPR-37703).
* Prise en charge de l’API pour le fragment d’expérience de type d’offre JSON (NPR-37796).
* La demande d’offre est désormais fournie pour l’offre de suppression (API de fragment d’expérience) dans IMS (NPR-37668).
* Le référentiel intégré (Apache Jackrabbit Oak) reste à 1.22.9.

Voici la liste des correctifs fournis dans [!DNL Experience Manager] Version 6.5.12.0.

### [!DNL Sites] {#sites-65120}

Les problèmes suivants ont été corrigés dans [!DNL Sites]:

* La mise en page des propriétés du fragment de contenu est rompue, car les onglets De base et Avancé ne comportent aucune marge vers la gauche (SITES-4484).
* L’option de fermeture de la bannière sur les fragments de contenu, référencés sur différentes pages de site, ne fonctionne pas. Cette bannière informe les utilisateurs que le fragment de contenu est référencé sur une ou plusieurs pages (SITES-4173).
* Les cases à cocher ne sont pas alignées dans la boîte de dialogue Rétablir l’héritage (SITES-3514).
* La page de modèle sur les sites we-retail et wknd est endommagée, car l’option de chargement et de structure des composants n’est pas disponible, car le servlet pageinfo.json est bloqué sur LaunchManagerImpl.getLaunchStream (SITES-3489).
* La publication du noeud utilisateur de l’environnement de création vers l’environnement de publication ne fonctionne pas (NPR-38005).
* La tentative de création d’un fragment d’expérience à l’aide d’un modèle modifié n’affiche pas les modifications apportées aux propriétés initiales de la page (NPR-37962).
* L’opération de déplacement de page sur Experience Manager est lente (NPR-37961).
* La traduction des fragments d’expérience ne met pas à jour les références aux chemins de copie de langue (NPR-37953).
* Les utilisateurs ne disposant pas d’autorisations de réplication ne peuvent pas supprimer ni déplacer des pages, même si les pages ne sont pas activées (NPR-37936).
* Des erreurs aléatoires org.apache.felix.metatype sont observées sur le serveur (NPR-37935).
* Les références dans l’interface utilisateur tactile d’administration de Sites n’affichent pas correctement les liens entrants (NPR-37934).
* Le chemin de lancement pour ajouter de nouvelles pages ou ressources n’est pas disponible lors de la sélection de pages dans une tâche de traduction (NPR-37912).
* Les pages de référence d’un composant de liste ajoutées dans des fragments d’expérience ne sont pas mises à jour vers la page de destination lors de la promotion du lancement (NPR-37886).
* L’environnement de création présente des problèmes d’interface utilisateur, tels que le titre de la page Mode d’édition, qui n’est pas centré et le sélecteur de composants autorisés dans l’éditeur de stratégies : La case à cocher du groupe occupe toute la largeur du conteneur. Le libellé est donc rendu dans la ligne suivante (NPR-37878).
* [Plateforme] Le numéro de version de xmlns:metatype dans le fichier metatype.xml de commons-httpclient est &quot;http://www.osgi.org/xmlns/metatype/v1.0.0&quot; au lieu de &quot;http://www.osgi.org/xmlns/metatype/v1.2.0&quot; (NPR-37865).
* Des erreurs sont observées et les pages ne se déplacent pas lors d’une tentative sur une page (NPR-37864).
* [Éditeur de texte enrichi] L’image n’est pas rendue dans l’interface utilisateur classique lors de l’ajout de l’image en tant qu’élément de liste dans l’éditeur de texte enrichi (NPR-37835).
* Les auteurs peuvent appliquer des balises situées en dehors du chemin racine configuré lors de l’utilisation du champ de balise dans une boîte de dialogue (NPR-37834).
* Multifield ne s’affiche pas correctement dans le conteneur de mises en page et renvoie une erreur (NPR-37811).
* Tenter de redimensionner la mise en page du composant dans l’éditeur de page ne fonctionne pas dans la mise en page pour périphériques mobiles (NPR-37805).
* La traduction des fragments d’expérience ne met pas à jour les références cycliques aux chemins de copie de langue (NPR-37745).
* L’utilisation d’un champ de texte enrichi verrouillable cq-msm dans les propriétés de page ne désactive pas le champ lors du déploiement de la page et peut être modifié par les auteurs (NPR-37714).
* Lors de l’activation d’un fragment d’expérience, l’éditeur envoie de nombreuses demandes d’activation à Dispatcher (NPR-37707).
* Lors d’une modification de topologie, la tâche Sling pour le traitement des ressources est réinitialisée, ce qui entraîne l’ignorance des tâches en cours au moment du changement de topologie (NPR-37706).
* Les guillemets, les croix et les tirets ne sont pas exportés au format CSV lorsque les utilisateurs de sites d’exportation MacOS et d’URL de ressources (NPR-37698).
* Le conteneur de mises en page dans SPA modèle de page ne peut pas enregistrer les classes CSS personnalisées définies dans la stratégie de modèle lors de l’exécution des pages de SPA de réaction (NPR-37697).
* L’image d’arrière-plan n’est pas visible lorsque l’utilisateur sélectionne le ciblage sur un fragment d’expérience dont l’arrière-plan se trouve dans le conteneur (NPR-37662).
* La tâche de traduction sur un fragment d’expérience ne traduit pas tous les composants de ce fragment d’expérience (NPR-37660).
* La traduction des fragments d’expérience et de la page contenant le fragment d’expérience ne met pas à jour le chemin de lancement dans le lien du fragment d’expérience (NPR-37659).
* Le widget Téléchargement de fichier n’affiche pas le nom du fichier, lorsqu’un fichier est chargé et que la boîte de dialogue est enregistrée (NPR-37634).
* L’activation (publication) planifiée de la ressource ne se déclenche pas à l’heure planifiée si le dossier contenant cette ressource est déplacé (NPR-37621).
* [Plateforme] Le tableau de bord du vérificateur de lien externe ne parvient pas à générer des résultats [!DNL Adobe Experience Manager] WCM (NPR-37614).
* L’éditeur de fragment de contenu ne fonctionne pas correctement lorsque des majuscules sont utilisées dans les noms de balise lors de l’édition de balises dans l’éditeur (NPR-37601).
* L’éditeur d’interface utilisateur classique n’affiche pas de marque comme dans la vue de comparaison de l’interface utilisateur tactile (NPR-37588).
* Une erreur 500 intermittente est consignée lors de l’ajout d’un fragment d’expérience aux tâches de traduction (NPR-37587).
* Les auteurs peuvent sélectionner et utiliser la date du sélecteur de date même sur le sélecteur de date désactivé (NPR-37583).
* [Foundation] Les auteurs ne peuvent pas saisir certaines valeurs décimales dans le type de ressource de champ numérique dans une structure de boîte de dialogue de composant pour l’interface utilisateur tactile (NPR-37059).
* Les chemins d’accès dans le dossier libs sont supprimés lors de l’installation des Service Packs précédents (NPR-36815).
* [Commerce] La désactivation d’un dossier racine ne modifie pas l’état de désactivation des produits enfants dans [!DNL Experience Manager Commerce] console; de plus, le nombre de dossiers enfants d’un dossier racine au moment de la désactivation s’affiche incorrectement dans l’interface utilisateur (CQ-4338261).
* [Processus de localisation] Le contenu de la personnalisation des colonnes et de la personnalisation de la marque n’est pas localisé dans la boîte de dialogue Admin Control (en sélectionnant l’icône sous l’icône de profil dans [!DNL Adobe Experience Manager] boîte de réception (CQ-4334864).
* [Communautés] Il n’est pas possible de cliquer sur le contenu du tableau pour les membres du groupe (CQ-4334404).
* [Oak] Le processus de synchronisation Secondaire à froid ne fonctionne pas et génère une erreur de journalisation (CQ-4333868).
* [Interface utilisateur de Platform Foundation] [!DNL Experience Manager] La page de démarrage s’affiche à nouveau lorsque l’utilisateur sélectionne la variable [!DNL Adobe Experience Manager] icône déjà en cours sur la page de démarrage (CQ-4317409).
* Pour qu’un utilisateur (sans autorisation de réplication) supprime ou déplace des pages (même si les pages ne sont pas activées), la variable `Page Subtree Activation Check` Sous Configuration `Page Manager Factory` doit être activé (NPR-37936).

### [!DNL Assets] {#assets-65120}

<!--
The following accessibility enhancements are available in [!DNL Assets]:

* enhancement 1
-->

Les problèmes suivants ont été corrigés dans [!DNL Assets]:

* Lors de l’ajout d’une ressource ou d’un dossier (contenant `single quote` dans le nom) dans Ressources connectées, le chemin de référence échoue et produit une exception (NPR-37712).
* Lors de l’ajout d’un filigrane à une ressource, le filigrane est toujours affiché en noir, quelle que soit la couleur définie par l’utilisateur (NPR-37720).
* Lors de l’utilisation de ressources connectées, un utilisateur non administrateur peut rechercher une ressource même si les utilisateurs non-administrateurs sont limités à l’accès au référentiel DAM (NPR-37644).
* Lors de la mise à jour des métadonnées de ressources à l’aide d’une modification en masse, les modifications appliquées aux champs déroulants ne sont pas enregistrées et réinitialisées aux valeurs par défaut (NPR-37345).
* La suppression d’un dossier en trop longtemps a un impact sur les performances globales (NPR-37107).
* Lors de l’application de règles dans un schéma de métadonnées, l’utilisateur ne peut pas afficher la valeur complète de la liste déroulante `Field Value` et `Field Choices` si la valeur est supérieure à la zone de texte (CQ-4338074).
* Après la mise à niveau vers la version 6.5.10.0, la page des propriétés de la ressource reflète un message de rendu de HTML inutile (CQ-4336994).
* Tri des ressources dans `List View` ne fonctionne pas efficacement (CQ-4335298).
* Lors du partage de ressources à l’aide du lien de partage, les ressources sont téléchargées dans des dossiers distincts (CQ-4335000).
* Lors de la vérification de la variable [!DNL Experience Manager] `Inbox` , les `Share` et `Out of office` les onglets reflètent le contenu non traduit (CQ-4334858).

* Les correctifs suivants sont liés aux métadonnées en cascade dans les propriétés des ressources.
   * Une liste déroulante obligatoire reflète plusieurs messages d’erreur pour chaque sélection dans le champ à plusieurs valeurs (NPR-37859).
   * Seule la dernière sélection du champ parent est enregistrée pour le champ non modifiable dépendant (NPR-37858).
   * La liste déroulante dépendante (champ à plusieurs valeurs) reflète par intermittence la valeur par défaut pour la liste déroulante parent sélectionnée (NPR-37791).

### [!DNL Dynamic Media] {#dynamic-media-65120}

Les problèmes suivants ont été corrigés dans [!DNL Dynamic Media]:

* Les ressources d’un dossier contenant `renditions` dans le nom du dossier ne sont pas synchronisés dans `Dynamic Media` (CQ-4338428).
* Lors de la création d’un paramètre d’image prédéfini dans `tiff` format, le paramètre prédéfini est créé, mais le format devient `jpeg` (CQ-4335985).
* Lors de la modification de la variable `Progressive JPEG Scan` dans l’éditeur de paramètres d’image prédéfinis, la valeur de la liste déroulante est toujours réinitialisée sur `auto`(CQ-4335971).
* Les métadonnées vidéo ne sont pas visibles pour la variable `mxf` vidéos sur la page des propriétés de la ressource (CQ-4335499).
* Lors du retraitement des ressources vidéo, l’AVS (visionneuse de vidéos adaptative) et les rendus vidéo sont dépubliés à partir du serveur de publication (CQ-4335461).
* Les miniatures du PDF générées sont différentes de la première page du PDF réel. Certaines parties de l’image sont manquantes dans la miniature (CQ-4315554).
* L’invalidation du réseau de diffusion de contenu échoue avec une mauvaise réponse d’URL si la variable `companyName` et `companyRoot` sont différents (CQ-4339896).

### Workflows {#workflows-65120}

* Le défilement ne fonctionne pas comme prévu si vous appliquez un filtre sur les éléments de boîte de réception (CQ-4333594).

### [!DNL Forms] {#forms-65120}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] publie les packages de modules complémentaires une semaine après la date de publication prévue du Service Pack [!DNL Experience Manager].


**Formulaires adaptatifs**

* Lorsqu’un composant de texte d’un formulaire adaptatif contient un tableau, coller du contenu dans le composant entraîne l’effacement du tableau dans l’éditeur (NPR-38078).

* Un formulaire affiche une barre d’outils uniquement lorsque vous ouvrez un formulaire enregistré (NPR-38060).

* L’opération d’annulation ne fonctionne pas correctement pour l’éditeur de règles (NPR-37973).

* `getAemFormContainer` renvoie un pointeur null après l’installation d’AEM Forms 6.5.10.0 (NPR-37881).

* Accessibilité : le lecteur d’écran annonce la description longue d’une zone de texte dès que la sélection de l’onglet se déplace vers le champ au lieu de l’annoncer uniquement lorsque vous cliquez sur le champ (NPR-37855).

* Lorsque vous activez la propriété Autoriser le texte enrichi pour une zone de texte, la longueur maximale autorisée des caractères pose problème (NPR-37825).

* Problèmes CSS lorsque vous copiez un composant dans un formulaire adaptatif (NPR-37812).

* Lors de la génération de la traduction de formulaires adaptatifs, le fichier XLIFF généré ne contient pas la même séquence de textes que dans le formulaire adaptatif. Dans certains cas, il est nécessaire de voir le contexte des textes. Cela n’est pas possible si la séquence dans XLIFF est alphabétique. (NPR-37435).

* Lorsqu’un formulaire adaptatif est traduit, les balises de HTML font partie de la traduction. Si un utilisateur commet une erreur et que les balises ne sont pas valides, le texte entier n’est pas affiché dans le document d’enregistrement. (NPR-37499)

* Lorsqu’un formulaire adaptatif est créé et finalisé dans la langue de base, la traduction est effectuée par une équipe externe et importée. S’il existe même une légère modification du texte, comme un ajout ou un point manquant (.) est effectué dans la langue de base, la traduction complète est manquante pour toutes les autres langues. (NPR-37189)

**Modèle de données de formulaire**

* Problème lors de l’enregistrement des pièces jointes de formulaire adaptatif connectées à un modèle de données de formulaire dans la base de données (CQ-4338561).

**Communication interactive**

* L’onglet Référence ne répertorie aucune référence dans une communication interactive (NPR-37995).

**Services de document**

* Assembler n’incorpore pas les polices, comme prévu (NPR-38056).

* Impossible de convertir le PDF au format PDFA à l’aide de Workbench (NPR-37879).

* Problèmes avec les documents d’entreprise lors de l’utilisation du service PDF Generator après la mise à niveau d’AEM Forms 6.5.7.0 vers AEM 6.5.10.0 Forms (NPR-37758).

**Document Security**

* Le chiffrement du PDF ne fonctionne pas après la mise à niveau vers la version 1.8.0_281 de java (NPR-37716).

**Foundation JEE**

* Le service de générateur de PDF multithreads se bloque après un temps aléatoire pour AEM 6.5.7.0 Forms (NPR-38053).

* Dans AEM Workbench version 6.5.0.20210518.1.338459, lorsque vous utilisez un point de départ de courrier électronique et que vous modifiez le nom d’utilisateur et le mot de passe, les configurations ne sont pas enregistrées (NPR-37967, CQ-4336081).

* L’enregistrement des journaux entraîne une utilisation élevée du processeur qui nécessite un redémarrage du serveur (NPR-37868).

* `Gemfire.log` n’est pas créé dans la variable `temp\adobejb_server1\Caching` après l’installation d’AEM Forms-6.5.0-0038 (CQ-4340237).

* L’erreur suivante s’affiche après l’exécution de la fonction `ConfigurationManager.sh` Commande (CQ-4338323) :

   ```TXT
     [root@localhost bin]# ./ConfigurationManager.sh 
     bash: ./ConfigurationManagerCLI.sh: /bin/sh^M: bad interpreter: No such file or directory
   ```

* AEM 6.5 Forms sous RHEL8 ne prend pas en charge JBOSS EAP 7.3 et MySQL8 (CQ-4331770).

**Processus**

* Problèmes lors du stockage de caractères spéciaux UTF-8 dans le cadre d’un workflow sur AEM instance de publication Forms 6.5.10.0 (NPR-37673).

* Problème lors de la création d’une variable de type ArrayList et de sous-type JSON (NPR-37600).

* Problèmes avec le navigateur de notation XPath/point avec l’étape Définir la variable dans le workflow dans AEM 6.5.9.0 Forms et AEM 6.5.10.0 Forms (CQ-4336582).

Pour plus d’informations sur les mises à jour de sécurité, voir [[!DNL Experience Manager] page bulletins de sécurité](https://helpx.adobe.com/security/products/experience-manager.html).

## Installation de la version 6.5.12.0 {#install}

**Configuration des exigences et informations supplémentaires**

* Experience Manager 6.5.12.0 nécessite Experience Manager 6.5. Voir [documentation de mise à niveau](/help/sites-deploying/upgrade.md) pour obtenir des instructions détaillées.
* Le téléchargement du Service Pack est disponible sur Adobe [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Sur un déploiement avec MongoDB et plusieurs instances, installez Experience Manager 6.5.12.0 sur l’une des instances d’auteur à l’aide du gestionnaire de modules.

>[!NOTE]
>
>Adobe ne recommande pas de supprimer ou de désinstaller le [!DNL Adobe Experience Manager] Package 6.5.12.0.

### Installation du Service Pack {#install-service-pack}

Pour installer le Service Pack sur un [!DNL Adobe Experience Manager] 6.5, procédez comme suit :

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.

1. Avant l’installation, prenez un instantané ou une nouvelle sauvegarde de votre [!DNL Experience Manager] instance.

1. Téléchargez le Service Pack à partir de [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.12.0.zip).

1. Ouvrez Package Manager et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package. Pour en savoir plus, voir [Gestionnaire de modules](/help/sites-administering/package-manager.md).

1. Sélectionnez le package et cliquez sur **[!UICONTROL Installer]**.

1. Pour mettre à jour le connecteur S3, arrêtez l’instance après l’installation du Service Pack, remplacez le connecteur existant par un nouveau fichier binaire fourni dans le dossier d’installation, puis redémarrez l’instance. Voir [Entrepôt de données Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>La boîte de dialogue de l’interface utilisateur de Package Manager se ferme parfois pendant l’installation du Service Pack. Adobe recommande d’attendre que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les logs spécifiques liés à la désinstallation du lot de mise à jour avant de vous assurer que les installations sont réussies. En règle générale, ce problème se produit dans [!DNL Safari] mais peut se produire par intermittence sur n’importe quel navigateur.

**Installation automatique**

Il existe deux manières d’installer automatiquement [!DNL Experience Manager] 6.5.12.0 sur une instance de travail :

A. Placez le package dans `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.

B. Utilisez la variable [API HTTP à partir de Package Manager](/help/sites-administering/package-manager.md#package-share). Utilisation `cmd=install&recursive=true` afin que les modules imbriqués soient installés.

>[!NOTE]
>
>Adobe Experience Manager 6.5.12.0 ne prend pas en charge l’installation de Bootstrap.

**Validation de l’installation**

1. la page d’informations sur les produits (`/system/console/productinfo`) affiche la chaîne de version mise à jour. `Adobe Experience Manager (6.5.12.0)` under [!UICONTROL Produits installés].

1. Tous les lots OSGi sont : **[!UICONTROL PRINCIPAL]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (Utiliser la console web : `/system/console/bundles`).

1. Le lot OSGi `org.apache.jackrabbit.oak-core` est version 1.22.3 ou ultérieure (Utiliser la console web : `/system/console/bundles`).

Pour connaître les plates-formes certifiées pour travailler avec cette version, voir [exigences techniques](/help/sites-deploying/technical-requirements.md).

### Installation du module complémentaire Adobe Experience Manager Forms {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Ignorez si vous n’utilisez pas Experience Manager Forms. Les correctifs dans Experience Manager Forms sont fournis par le biais d’un module complémentaire distinct une semaine après la planification de la [!DNL Experience Manager] Version du Service Pack.

1. Vérifiez que vous avez installé le Service Pack Adobe Experience Manager.
1. Téléchargez le module complémentaire Forms correspondant répertorié dans les [versions AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) pour votre système d’exploitation.
1. Installez le module complémentaire Forms comme décrit dans [Installation des packages de modules complémentaires AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Installation d’Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Passez cette étape si vous n’utilisez pas AEM Forms sous JEE. Les correctifs d’Adobe Experience Manager Forms on JEE sont fournis via un programme d’installation distinct.

Pour plus d’informations sur l’installation du programme d’installation cumulatif pour Experience Manager Forms on JEE et la configuration après le déploiement, voir la section [notes de mise à jour](jee-patch-installer-65.md).

>[!NOTE]
>
>Après avoir installé le programme d’installation cumulatif de Experience Manager Forms on JEE, installez le dernier module complémentaire Forms, supprimez le module complémentaire Forms du `crx-repository\install` et redémarrez le serveur.

### UberJar {#uber-jar}

UberJar pour Experience Manager 6.5.12.0 est disponible dans la section [Référentiel Maven Central](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.12/).

Pour utiliser UberJar dans un projet Maven, voir [utilisation d’UberJar](/help/sites-developing/ht-projects-maven.md) et incluez la dépendance suivante dans le POM de votre projet :

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.12</version>
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
| Intégrations | Le **[!UICONTROL Accord préalable des services cloud AEM]** est obsolète, car la variable [!DNL Experience Manager] et [!DNL Adobe Target] L’intégration est mise à jour dans Experience Manager 6.5. L’intégration prend en charge l’API Adobe Target Standard. L’API utilise l’authentification via Adobe IMS et [!DNL Adobe I/O] et prend en charge le rôle croissant d’Adobe Launch pour l’instrumenter [!DNL Experience Manager] pour les analyses et la personnalisation, l’assistant de souscription n’a aucune utilité sur le plan fonctionnel. | Configuration des connexions système, de l’authentification Adobe IMS et [!DNL Adobe I/O] intégrations via les [!DNL Experience Manager] services cloud. |
| Connecteurs | Adobe JCR Connector for Microsoft® SharePoint 2010 et Microsoft® SharePoint 2013 est obsolète pour Experience Manager 6.5. | N/A |

## Problèmes connus {#known-issues}

* Si vous utilisez des fragments de contenu et GraphQL, il est recommandé d’installer les packages suivants sur la version 6.5.12.0 :

   * [AEM 6.5.12 Sites HotFix-NPR-38144](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Faem-service-pkg-6.5.12.0-NPR-38144-B0002.zip) (il remplace SP12 mais peut être installé sur SP12)

   * [AEM du fragment de contenu avec le package d’index GraphQL 1.0.3](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.3.zip)

* As [!DNL Microsoft Windows Server 2019] ne prend pas en charge [!DNL MySQL 5.7] et [!DNL JBoss EAP 7.1], [!DNL Microsoft Windows Server 2019] ne prend pas en charge les installations clé en main pour [!DNL AEM Forms 6.5.10.0].

* Si vous effectuez une mise à niveau de votre [!DNL Experience Manager] de la version 6.5 à la version 6.5.10.0, vous pouvez afficher `RRD4JReporter` exceptions dans la variable `error.log` fichier . Pour résoudre le problème, redémarrez l’instance.

* Si vous installez [!DNL Experience Manager] 6.5 Service Pack 10 ou un Service Pack précédent sur [!DNL Experience Manager] 6.5, la copie d’exécution du modèle de workflow personnalisé de vos ressources (créé dans `/var/workflow/models/dam`) est supprimé.
Pour récupérer votre copie d’exécution, Adobe recommande de synchroniser la copie d’heure de conception du modèle de workflow personnalisé avec sa copie d’exécution à l’aide de l’API HTTP :
   `<designModelPath>/jcr:content.generate.json`.

* Les utilisateurs peuvent renommer un dossier dans une hiérarchie de [!DNL Assets] et publier un dossier imbriqué dans [!DNL Brand Portal]. Toutefois, le titre du dossier n’est pas mis à jour dans [!DNL Brand Portal] jusqu’à ce que le dossier racine soit republié.

* Lorsqu’un utilisateur choisit de configurer un champ pour la première fois dans un formulaire adaptatif, l’option permettant d’enregistrer une configuration ne s’affiche pas dans l’explorateur de propriétés. Sélectionner pour configurer un autre champ du formulaire adaptatif dans le même éditeur résout le problème.

* Les erreurs et messages d’avertissement suivants peuvent s’afficher lors de l’installation de Experience Manager 6.5.x.x :
   * &quot;Lorsque l’intégration d’Adobe Target est configurée dans Experience Manager à l’aide de l’API Target Standard (authentification IMS), l’exportation de fragments d’expérience vers Target entraîne la création de types d’offres incorrects. Au lieu du type « Fragment d’expérience » / source « Adobe Experience Manager », Target crée plusieurs offres avec le type « HTML » / source « Adobe Target Classic ».
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

Les documents texte suivants répertorient les lots OSGi et les packages de contenu inclus dans [!DNL Experience Manager] 6.5.12.0 :

* [Liste des lots OSGi inclus dans Experience Manager 6.5.12.0](assets/65120_bundles.txt)

* [Liste des packages de contenu inclus dans Experience Manager 6.5.12.0](assets/65120_packages.txt)

## Sites web à accès limité {#restricted-sites}

Ces sites web ne sont disponibles que pour les clients. Si vous êtes client et avez besoin d’un accès, contactez votre responsable de compte Adobe.

* [Téléchargement du produit à l’adresse licensing.adobe.com](https://licensing.adobe.com/)
* Voir [Comment contacter le service clientèle d’Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] page produit](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentation 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=fr)
>* [Abonnement aux mises à jour de produits prioritaires d’Adobe](https://www.adobe.com/subscription/priority-product-update.html)

