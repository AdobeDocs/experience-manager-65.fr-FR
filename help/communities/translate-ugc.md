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
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054

---


# Traduction de contenu généré par l’utilisateur {#translating-user-generated-content}

La fonction de traduction pour les communautés AEM étend le concept de [traduction du contenu](../../help/sites-administering/translation.md) de la page au contenu généré par l’utilisateur (UGC) publié sur les sites de la communauté à l’aide des composants [SCF (](scf.md)social component framework).

La traduction de l&#39;UGC permet aux du site et aux membres de faire l&#39;expérience d&#39;une communauté mondiale en supprimant les barrières linguistiques.

Prenons l’exemple suivant :

* Un membre de France publie une recette en français sur le forum communautaire d&#39;un site web multinational de cuisine.
* Un autre membre du Japon utilise la fonction de traduction pour déclencher la traduction de la recette du français vers le japonais.
* Après avoir lu la recette en japonais, le membre du Japon a publié un commentaire en japonais.
* Le membre de France utilise la fonction de traduction pour traduire le commentaire japonais en français.
* Communication mondiale.

## Présentation {#overview}

Cette section de la documentation décrit spécifiquement le fonctionnement du service de traduction avec l’UGC tout en comprenant comment connecter AEM à un [de](../../help/sites-administering/translation.md#connectingtoatranslationserviceprovider) traduction et intégrer ce service dans un site Web en configurant une structure [d’intégration de](../../help/sites-administering/tc-tic.md)traduction.

Lorsqu’un de traduction est associé au site, chaque copie de langue du site conserve ses propres fils de contenu généré par l’UGC, publiés par l’intermédiaire de composants SCF tels que les commentaires.

Lorsqu’une structure d’intégration de traduction est configurée en plus du de traduction, il est possible pour chaque copie de langue du site de partager un seul thread de l’UGC, fournissant ainsi une communication globale entre les copies de langue. Au lieu d’un thread de discussion séparé par langue, le magasin [partagé](#global-translation-of-ugc) global configuré permet à l’ensemble du thread d’être visible quelle que soit la copie de langue affichée. En outre, plusieurs configurations d’intégration de traduction peuvent être configurées en spécifiant différentes boutiques partagées globales pour un regroupement logique de participants globaux, par exemple par régions.

## Service de traduction par défaut {#the-default-translation-service}

Les communautés AEM sont livrées avec une licence [d’](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license) évaluation pour un service [de traduction](../../help/sites-administering/tc-msconf.md) par défaut activé pour plusieurs langues.

Lors de la [création d’un site](sites-console.md)communautaire, le service de traduction par défaut est activé lorsque `Allow Machine Translation` l’option est cochée à partir du sous-panneau [TRADUCTION](sites-console.md#translation) .

>[!CAUTION]
>
>Le service de traduction par défaut est réservé à la démonstration.
>
>Pour un système de production, un service de traduction sous licence est requis. Si la licence n’est pas attribuée, le service de traduction par défaut doit être [désactivé](../../help/sites-administering/tc-msconf.md#microsoft-translator-trial-license-geometrixx-outdoors).


## Traduction globale de l&#39;UGC {#global-translation-of-ugc}

Lorsqu’un site Web comporte plusieurs copies [de](../../help/sites-administering/tc-prep.md)langue, le service de traduction par défaut ne reconnaît pas que l’UGC entré sur un site peut être lié à l’UGC entré sur un autre, comme lorsque l’UGC est essentiellement généré par le même composant (la copie de langue de la page contenant le composant).

C&#39;est semblable à des groupes de personnes qui discutent d&#39;un sujet qui ignorent que des commentaires sont faits dans des groupes autres que les leurs, comparativement à tous les membres d&#39;un grand groupe qui participent à une conversation.

Si vous souhaitez &quot;une conversation de groupe&quot;, il est possible d’activer la traduction globale sur un site Web avec plusieurs copies de langue, de sorte que l’ensemble du fil de discussion soit visible, quelle que soit la langue de la copie consultée.

Par exemple, si un forum a été créé sur le site de base, que des copies de langue ont été créées et que la traduction globale a été activée, un sujet publié sur le forum dans une copie de langue apparaîtra dans toutes les copies de langue. Il en serait de même pour toutes les réponses, quelle que soit la langue à partir de laquelle la réponse a été saisie. Le résultat serait que la rubrique et l’ensemble de son fil de réponses seraient visibles quelle que soit la langue à partir de laquelle la copie de la rubrique est consultée.

>[!CAUTION]
>
>Les UGC qui existaient avant la traduction globale ne sont plus visibles.
>
>Bien que l’UGC soit toujours dans le magasin [](working-with-srp.md)commun, il se trouve sous l’emplacement de l’UGC spécifique à la langue, tandis que le nouveau contenu, ajouté après la configuration de la traduction globale, est en cours de récupération à partir de l’emplacement de stockage partagé global.
>
>Il n’existe aucun outil de migration pour déplacer ou fusionner du contenu spécifique à une langue dans la boutique partagée globale.


### Configuration de l’intégration de traduction {#translation-integration-configuration}

Pour créer une nouvelle intégration de traduction, qui intègre un connecteur du service de traduction au site Web de l’instance d’auteur :

* Connexion en tant qu’administrateur
* Dans le menu [principal](http://localhost:4502/)
* Sélectionnez **[!UICONTROL Outils]**.
* Sélectionner les **[!UICONTROL opérations]**
* Sélectionner **[!UICONTROL Cloud]**
* Sélectionner les services **[!UICONTROL Cloud]**
* Faire défiler vers le bas jusqu’à l’intégration **[!UICONTROL de traduction]**

   ![chlimage_1-65](assets/chlimage_1-65.png)

* Sélectionner **[!UICONTROL Afficher les configurations]**

   ![chlimage_1-66](assets/chlimage_1-66.png)

* Sélectionnez `[+]` l’icône en regard de Configurations **** disponibles pour créer une nouvelle configuration.

#### Boîte de dialogue Créer une configuration {#create-configuration-dialog}

![chlimage_1-67](assets/chlimage_1-67.png)

* **[!UICONTROL Configuration du parent]**

   (Obligatoire) Conservez généralement la valeur par défaut. La valeur par défaut est `/etc/cloudservices/translation`.

* **[!UICONTROL Titre]**

   (Obligatoire) Entrez le titre d’affichage de votre choix. Pas de valeur par défaut.

* **[!UICONTROL Nom]**

   (Facultatif) Entrez un nom pour la configuration. La valeur par défaut est un nom de noeud basé sur le titre.

* Sélectionnez **[!UICONTROL Créer]**

#### Boîte de dialogue Configuration de la traduction {#translation-config-dialog}

![chlimage_1-68](assets/chlimage_1-68.png)

Pour obtenir des instructions détaillées, consultez [Création d’une configuration d’intégration de traduction.](../../help/sites-administering/tc-tic.md#creating-a-translation-integration-configuration)

* **[!UICONTROL Onglet Sites]** : peut laisser comme valeurs par défaut.

* **[!UICONTROL Onglet Communautés]** :
   * **[!UICONTROL Fournisseur]** de traduction Sélectionnez le fournisseur de traduction dans le  déroulant. La valeur par défaut est `microsoft`, le service d’évaluation.

   * **[!UICONTROL de contenu]** Sélectionnez un qui décrit le contenu en cours de traduction. La valeur par défaut est `General.`

   * **[!UICONTROL Choisir une langue...]**
(Facultatif) En sélectionnant un paramètre régional pour le stockage de l’UGC, les publications de toutes les copies de langue s’affichent dans une seule conversation globale. Par convention, choisissez la langue de [base](sites-console.md#translation) du site Web. Le choix `No Common Store` désactivera la traduction globale. Par défaut, la traduction globale est désactivée.

* **[!UICONTROL Onglet Ressources]** : peut laisser comme valeurs par défaut.
* **[!UICONTROL Cliquez sur OK]**

#### Activation {#activation}

Le nouveau service cloud d’intégration de traduction devra être activé sur le  de publication . Lorsqu’il est associé à un site Web, si ce n’est pas encore activé, le flux de travail   vous invite à publier cette configuration de service cloud lorsque la page à laquelle il est associé est publiée.

## Gestion des paramètres de traduction {#managing-translation-settings}

>[!NOTE]
>
>**Langue préférée**
>
>Pour déterminer si la publication est dans une langue différente de la langue préférée, la langue préférée du du site doit être établie.
>
>La langue préférée est la préférence de langue définie dans le  d’un utilisateur, lorsque le du site est connecté et a spécifié une préférence de langue.
>
>Lorsque le du site est anonyme ou n’a pas spécifié de préférence de langue dans son, la langue préférée est la langue de base du modèle de page.


### Préférences utilisateur {#user-preference}

#### Profil utilisateur {#user-profile}

Tous les sites des communautés fournissent un d’utilisateurs que les membres connectés peuvent modifier pour s’identifier à la communauté et définir leurs préférences.

L’un de ces paramètres consiste à afficher ou non toujours le contenu de la communauté dans sa langue préférée. Par défaut, ce paramètre n’est pas défini et sera défini par défaut sur le paramètre système. L’utilisateur peut définir le paramètre Activé ou Désactivé, remplaçant ainsi le paramètre système.

Lorsque les pages sont automatiquement traduites dans la langue préférée de l’utilisateur, l’interface utilisateur permettant d’afficher le texte d’origine et d’améliorer la traduction est toujours disponible.

![chlimage_1-69](assets/chlimage_1-69.png)

### Paramètres du site de la communauté {#community-site-setting}

Lorsqu’un site de la communauté est créé, l’option de traduction peut être activée et configurée. Le paramètre de traduction est en vigueur pour le contenu que les anonymes du site peuvent, mais il est remplacé par le paramètre  de l’utilisateur.
