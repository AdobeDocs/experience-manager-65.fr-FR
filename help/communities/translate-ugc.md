---
title: Traduction de contenu généré par l’utilisateur
seo-title: Traduction de contenu généré par l’utilisateur
description: Fonctionnement de la fonction de traduction
seo-description: Fonctionnement de la fonction de traduction
uuid: 7ee3242c-2aca-4787-a60d-b807161401ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: bfaf80c5-448b-47fb-9f22-57ee0eb169b2
translation-type: tm+mt
source-git-commit: b29945dc73e85504cd42102eafb9e2bf6198c9cc
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 2%

---


# Traduction de contenu généré par l’utilisateur {#translating-user-generated-content}

La fonction de traduction d’AEM Communities étend le concept de [traduction du contenu de la page](../../help/sites-administering/translation.md) au contenu généré par l’utilisateur (UGC) publié sur les sites de la communauté à l’aide des composants [du cadre de composants sociaux (SCF)](scf.md).

La traduction de l&#39;UGC permet aux visiteurs du site et aux membres de faire l&#39;expérience d&#39;une communauté mondiale en supprimant les barrières linguistiques.

Par exemple, supposons :

* Un membre de France publie une recette en français sur le forum communautaire d&#39;un site web multinational de cuisine.
* Un autre membre du Japon utilise la fonction de traduction pour déclencher la traduction de la recette du français vers le japonais.
* Après avoir lu la recette en japonais, le membre du Japon a publié un commentaire en japonais.
* Le député français utilise la fonction de traduction pour traduire le commentaire japonais en français.
* Communication mondiale.

## Présentation {#overview}

Cette section de la documentation traite spécifiquement de la façon dont le service de traduction fonctionne avec UGC tout en supposant une compréhension de la façon de connecter AEM à un [prestataire de traduction](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider) et d&#39;intégrer ce service dans un site Web en configurant un [cadre d&#39;intégration de traduction](../../help/sites-administering/tc-tic.md).

Lorsqu&#39;un prestataire de traduction est associé au site, chaque copie de langue du site conserve ses propres fils de contenu UGC publiés par le biais de composants SCF tels que les commentaires.

Lorsqu’une structure d’intégration de traduction est configurée en plus du prestataire de traduction, il est possible pour chaque copie de langue du site de partager un seul thread de l’UGC, fournissant ainsi une communication globale entre les copies de langue. Au lieu d&#39;un thread de discussion séparé par langue, le [magasin partagé global](#global-translation-of-ugc) configuré permet à l&#39;ensemble du thread d&#39;être visible, quelle que soit la copie de langue affichée. En outre, plusieurs configurations d’intégration de traduction peuvent être configurées en spécifiant différents magasins partagés globaux pour un regroupement logique de participants globaux, par exemple par régions.

## Service de traduction par défaut {#the-default-translation-service}

AEM Communities inclut une [licence d’évaluation](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license) pour un [service de traduction par défaut](../../help/sites-administering/tc-msconf.md) activé pour plusieurs langues.

Lorsque [créez un site communautaire](sites-console.md), le service de traduction par défaut est activé lorsque `Allow Machine Translation` est coché à partir du sous-panneau [TRANSLATION](sites-console.md#translation).

>[!CAUTION]
>
>Le service de traduction par défaut est réservé à la démonstration.
>
>Pour un système de production, un service de traduction sous licence est requis. Si aucune licence n’est accordée, le service de traduction par défaut doit être [désactivé](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors).

## Traduction globale de l&#39;UGC {#global-translation-of-ugc}

Lorsqu&#39;un site Web comporte plusieurs [copies de langue](../../help/sites-administering/tc-prep.md), le service de traduction par défaut ne reconnaît pas que l&#39;UGC saisi sur un site peut être lié à l&#39;UGC saisi sur un autre, comme lorsque l&#39;UGC est essentiellement généré par le même composant (la copie de langue de la page contenant le composant).

Elle est semblable à celle des groupes de personnes qui discutent d&#39;un sujet qui n&#39;est pas au courant des commentaires faits dans des groupes autres que le leur, par rapport à tous les membres d&#39;un grand groupe participant à une conversation.

Si vous souhaitez &quot;une conversation de groupe&quot;, il est possible d’activer la traduction globale sur un site Web avec plusieurs copies de langue, de sorte que l’ensemble du thread soit visible, quelle que soit la copie de langue consultée.

Par exemple, si un forum a été établi sur le site de base, que des copies de langue ont été créées et que la traduction globale a été activée, un sujet affiché sur le forum fait dans une copie de langue apparaîtra dans toutes les copies de langue. Il en va de même pour toute réponse, quelle que soit la langue à partir de laquelle la réponse a été saisie. Il en résulterait que la rubrique et l’ensemble de ses réponses seraient visibles, quelle que soit la langue à partir de laquelle la copie de la rubrique est consultée.

>[!CAUTION]
>
>Tout UGC existant avant la traduction globale n&#39;est plus visible.
>
>Bien que l’UGC se trouve toujours dans le [magasin commun](working-with-srp.md), il se trouve sous l’emplacement de l’UGC spécifique à la langue, tandis que le nouveau contenu, ajouté après la configuration de la traduction globale, est récupéré à partir de l’emplacement de stockage partagé global.
>
>Il n’existe aucun outil de migration pour déplacer ou fusionner du contenu spécifique à une langue dans la boutique partagée globale.

### Configuration de l’intégration de traduction {#translation-integration-configuration}

Pour créer une nouvelle intégration de traduction, qui intègre un connecteur de service de traduction au site Web de l’instance d’auteur :

* Se connecter en tant qu’administrateur
* Dans le menu principal [](http://localhost:4502/)
* Sélectionnez **[!UICONTROL Outils]**.
* Sélectionner **[!UICONTROL Opérations]**
* Sélectionner **[!UICONTROL Cloud]**
* Sélectionner **[!UICONTROL Cloud Services]**
* Faites défiler jusqu’à **[!UICONTROL Intégration de traduction]**

   ![traduction-intégration](assets/translation-integration.png)

* Sélectionnez **[!UICONTROL Afficher les configurations]**

   ![show-configuration](assets/translation-integration1.png)

* Sélectionnez l&#39;icône `[+]` en regard de **[!UICONTROL Configurations disponibles]** pour créer une nouvelle configuration.

#### Boîte de dialogue Créer une configuration {#create-configuration-dialog}

![create-configuration](assets/translation-integration2.png)

* **[!UICONTROL Configuration du parent]**

   (Obligatoire) Conservez généralement la valeur par défaut. La valeur par défaut est `/etc/cloudservices/translation`.

* **[!UICONTROL Titre]**

   (Obligatoire) Saisissez le titre d’affichage de votre choix. Pas de valeur par défaut.

* **[!UICONTROL Name]** (Nom)

   (Facultatif) Entrez un nom pour la configuration. Par défaut, il s’agit d’un nom de noeud basé sur le titre.

* Sélectionnez **[!UICONTROL Créer]**

#### Boîte de dialogue Configuration de la traduction {#translation-config-dialog}

![configuration-dialog](assets/translation-integration3.png)

Pour obtenir des instructions détaillées, consultez [Création d’une configuration d’intégration de traduction](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration).

* **[!UICONTROL Onglet]** Sites : peut laisser comme valeur par défaut.

* **[!UICONTROL Onglet]** Communautés :
   * **[!UICONTROL Fournisseur]**
de traductionSélectionnez le fournisseur de traduction dans la liste déroulante. La valeur par défaut est 
`microsoft`, le service d’évaluation.

   * **[!UICONTROL Catégorie de contenuSélectionnez une catégorie qui décrit le contenu en cours de traduction.]**
La valeur par défaut est 
`General.`

   * **[!UICONTROL Choisir un paramètre régional...]**
(Facultatif) En sélectionnant un paramètre régional pour le stockage de l’UGC, les publications de toutes les copies de langue apparaîtront dans une seule conversation globale. Par convention, choisissez le paramètre régional pour la [langue de base](sites-console.md#translation) du site Web. Le choix de `No Common Store` désactivera la traduction globale. Par défaut, la traduction globale est désactivée.

* **** Assetstab : peut laisser comme valeur par défaut.
* **[!UICONTROL Cliquez sur OK]**

#### Activation {#activation}

Le nouveau service cloud d’intégration de traduction doit être activé sur l’environnement de publication. Lorsqu’il est associé à un site Web, si ce n’est pas encore fait, le processus d’activation vous invite à publier cette configuration de service cloud lorsque la page à laquelle il est associé est publiée.

## Gestion des paramètres de traduction {#managing-translation-settings}

>[!NOTE]
>
>**Langue préférée**
>
>Pour déterminer si la publication est dans une langue différente de la langue préférée, la langue préférée du visiteur du site doit être définie.
>
>La langue préférée est la préférence de langue définie dans le profil d’un utilisateur, lorsque le visiteur du site est connecté et a spécifié une préférence de langue.
>
>Lorsque le visiteur du site est anonyme ou n’a pas indiqué de préférence de langue dans son profil, la langue préférée est la langue de base du modèle de page.

### Préférences utilisateur {#user-preference}

#### Profil utilisateur {#user-profile}

Tous les sites des communautés fournissent un profil utilisateur que les membres connectés peuvent modifier pour s&#39;identifier à la communauté et définir leurs préférences.

L’un de ces paramètres consiste à déterminer s’il faut toujours afficher le contenu de la communauté dans sa langue préférée. Par défaut, le paramètre n’est pas défini et sera défini par défaut sur le paramètre système. L’utilisateur peut remplacer le paramètre système par Activé ou Désactivé.

Lorsque les pages sont automatiquement traduites dans la langue préférée de l’utilisateur, l’interface utilisateur permettant d’afficher le texte d’origine et d’améliorer la traduction est toujours disponible.

![profil utilisateur](assets/translation-integration4.png)

### Paramètre du site communautaire {#community-site-setting}

Lorsqu’un site communautaire est créé, l’option de traduction peut être activée et configurée. Le paramètre de traduction est en vigueur pour le contenu que les visiteurs anonymes du site peuvent vue, mais il est remplacé par le paramètre de profil de l’utilisateur.
