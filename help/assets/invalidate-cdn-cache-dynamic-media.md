---
title: Invalidation du cache du réseau de diffusion de contenu par le biais de Dynamic Media
description: L’invalidation du contenu en cache du réseau de diffusion de contenu (CDN) vous permet de mettre à jour rapidement les ressources diffusées par Dynamic Media, au lieu d’attendre l’expiration du cache.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
feature: CDN Cache
exl-id: 23d3c274-0736-49f7-8d44-a56a55cfd06d
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '1372'
ht-degree: 100%

---


# Invalidation du cache de réseau CDN par le biais de Dynamic Media {#invalidating-cdn-cache-for-dm-assets}

Les ressources Dynamic Media sont mises en cache par le réseau de diffusion de contenu (CDN) pour une diffusion rapide à vos clients. Cependant, lorsque vous apportez des mises à jour à ces ressources, vous souhaiterez peut-être que ces modifications prennent effet immédiatement sur votre site web. La purge ou l’invalidation du cache du réseau CDN vous permet de mettre rapidement à jour les ressources distribuées par Dynamic Media. Au lieu d’attendre que le cache arrive à expiration à l’aide d’une valeur TTL (durée de vie, dix heures par défaut), vous pouvez envoyer une requête depuis l’interface utilisateur de Dynamic Media pour que le cache arrive à expiration en quelques minutes.



>[!IMPORTANT]
>
>Les étapes suivantes s’appliquent uniquement à Dynamic Media en mode Scene7 dans le pack de services 6 d’Adobe Experience Manager 6.5 (Experience Manager 6.5.6) ou version ultérieure. Cette fonctionnalité nécessite l’utilisation du réseau CDN prêt à l’emploi fourni avec Adobe Experience Manager - Dynamic Media. Aucun autre réseau CDN personnalisé n’est pris en charge avec cette fonctionnalité.<br>Si vous utilisez Dynamic Media dans le pack de services 5 d’Experience Manager 6.5 (Experience Manager 6.5.5) ou version antérieure, suivez les étapes décrites dans la section [Invalidation du cache CDN via Dynamic Media Classic](/help/assets/invalidate-cdn-cache-dm-classic.md).

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Caching overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**Pour invalider le contenu mis en cache du réseau de diffusion de contenu pour les ressources Dynamic Media :**

*Partie 1 de 2 : création d’un modèle d’invalidation du réseau CDN*

1. Dans Experience Manager 6.5.6 ou une version ultérieure, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Invalidation du réseau CDN]**.

   ![Fonction de validation du réseau CDN](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. Sur la page **[!UICONTROL Modèle d’invalidation du réseau de diffusion de contenu]**, effectuez l’une des opérations suivantes en fonction de votre scénario :

   | Scénario | Option |
   | --- | --- |
   | J’ai déjà créé un modèle d’invalidation du réseau CDN dans le passé à l’aide de Dynamic Media Classic. | Le champ de texte **[!UICONTROL Créer un modèle]** est prérenseigné avec vos données de modèle. Dans ce cas, vous pouvez modifier le modèle ou passer à l’étape suivante. |
   | Je dois créer un modèle. Que dois-je entrer ? | Dans le champ de texte **[!UICONTROL Créer un modèle]**, saisissez une URL d’image (y compris les paramètres d’image prédéfinis ou les modificateurs) référençant `<ID>`, au lieu d’un ID d’image spécifique comme dans l’exemple suivant : <br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Si le modèle contient uniquement `<ID>`, Dynamic Media renseigne `https://<publishserver_name>/is/image/<company_name>/<ID>` avec `<publishserver_name>` comme nom de serveur de publication défini dans les paramètres généraux dans Dynamic Media Classic. `<company_name>` est le nom de la racine de votre société associée à cette instance d’Experience Manager et `<ID>` correspond aux ressources sélectionnées par le biais du sélecteur de ressources à invalider.<br>Tout paramètre prédéfini/modificateur placé après `<ID>` est copié tel quel dans la définition d’URL.<br>Seules les images (c’est-à-dire `/is/image`) peuvent être formées automatiquement en fonction du modèle.<br>Pour `/is/content/`, l’ajout de ressources telles que des vidéos ou des fichiers PDF à l’aide du sélecteur de ressources ne génère pas automatiquement d’URL. Au lieu de cela, vous devez spécifier ces ressources dans le modèle d’invalidation du réseau CDN ou vous pouvez ajouter manuellement l’URL à ces ressources dans *Partie 2 de 2 : définition des options d’invalidation du réseau CDN*.<br>**Exemples :**<br> Dans ce premier exemple, le modèle d’invalidation contient `<ID>` avec l’URL de ressource `/is/content`. Par exemple, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Media forme l’URL en fonction de ce chemin d’accès, `<ID>` correspondant aux ressources sélectionnées par le biais du sélecteur de ressources que vous souhaitez invalider.<br>Dans ce deuxième exemple, le modèle d’invalidation contient l’URL complète de la ressource utilisée dans vos propriétés web avec `/is/content` (indépendamment du sélecteur de ressources). Par exemple, `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` où backpack correspond à l’ID de ressource.<br>Les formats de ressources pris en charge dans Dynamic Media peuvent être invalidés. Les types de fichiers de ressources *non* pris en charge pour l’invalidation du réseau CDN comprennent les types PostScript®, Encapsulated PostScript®, Adobe Illustrator, Adobe InDesign, Microsoft® PowerPoint, Microsoft® Excel, Microsoft® Word et Rich Text Format.<br><br>• Lorsque vous créez le modèle, faites très attention à la syntaxe et aux fautes de frappe ; Dynamic Media n’effectue aucune validation de modèle.<br>• Le modèle d’invalidation du réseau CDN peut enregistrer du texte jusqu’à 2 500 caractères.<br>• Spécifiez des URL pour les recadrages intelligents d’images dans ce modèle d’invalidation du CDN ou dans le champ de texte **[!UICONTROL Ajouter une URL]** dans *Partie 2 : définition des options d’invalidation CDN.*<br>• Chaque entrée d’un modèle d’invalidation du réseau CDN doit se trouver sur sa propre ligne.<br>• L’exemple de modèle d’invalidation du réseau CDN suivant est fourni à des fins de démonstration uniquement. |

   ![Modèle d’invalidation du réseau CDN – Créer](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >Le modèle d’invalidation du réseau CDN peut enregistrer du texte jusqu’à 2 500 caractères.

1. Dans le coin supérieur droit de la page **[!UICONTROL Modèle d’invalidation du réseau CDN]**, sélectionnez **[!UICONTROL Enregistrer]**, puis **[!UICONTROL OK]**.<br>
   *Partie 2 de 2 : définition des options d’invalidation du réseau CDN*
   <br>

1. Dans Experience Manager as a Cloud Service, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Invalidation du réseau de diffusion de contenu]**.

   ![Fonction de validation du réseau CDN](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. Sur la page **[!UICONTROL Invalidation du réseau de diffusion de contenu - Ajouter des détails]**, sélectionnez les ressources pour l’invalidation du réseau CDN.

   ![Invalidation du réseau de diffusion de contenu – Ajouter des détails](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Si vous décidez de ne pas cocher les options **[!UICONTROL Invalider les paramètres d’image prédéfinis associés à la ressource dans le réseau de diffusion de contenu]** *et* **[!UICONTROL Invalider en fonction d’un modèle]**, l’URL de base des ressources sélectionnées est alors formée pour invalidation. Utilisez cette option réservée aux images.


   | Option | Description |
   | --- | --- |
   | **[!UICONTROL Invalider les paramètres d’image prédéfinis associés à la ressource dans le réseau de diffusion de contenu]** | (Facultatif) Lorsque vous cochez cette option, les ressources sélectionnées et toutes les URL de paramètres d’image prédéfinis associées sont automatiquement formées en vue de l’invalidation du cache.<br>Les ressources et leurs URL prédéfinies associées sont automatiquement formées en vue de l’invalidation. Cette option fonctionne uniquement pour les ressources d’image. |
   | **[!UICONTROL Invalidation en fonction d’un modèle]** | (Facultatif) Cochez cette option afin de n’utiliser que le modèle défini pour la formation d’URL. |
   | **[!UICONTROL Ajouter des ressources]** | Utilisez le sélecteur de ressources pour sélectionner les ressources que vous souhaitez invalider. Vous pouvez sélectionner des ressources publiées ou dépubliées.<br>La mise en cache sur le réseau CDN repose sur des URL et non sur des ressources. Il est donc nécessaire de connaître les URL complètes qui se trouvent sur votre site web. Après avoir déterminé ces URL, vous pouvez les ajouter au modèle. Vous pouvez ensuite sélectionner et ajouter ces ressources et invalider les URL en une seule étape. <br>Utilisez cette option avec les options **[!UICONTROL Invalider les paramètres d’image prédéfinis associés à la ressource dans le réseau de diffusion de contenu]** ou **[!UICONTROL Invalidation en fonction d’un modèle]**, ou les deux. |
   | **[!UICONTROL Ajouter une URL]** | Ajoutez ou collez manuellement des chemins d’URL complets aux ressources Dynamic Media dont vous souhaitez invalider le cache de réseau CDN. Utilisez cette option si vous n’avez pas créé de modèle d’invalidation du réseau CDN dans ***Partie 1 de 2 : création d’un modèle d’invalidation du réseau CDN*** et n’avez que quelques ressources à invalider.<br>**Important :** Chaque URL que vous ajoutez doit se trouver sur sa propre ligne.<br>Vous pouvez invalider jusqu’à 1 000 URL à la fois. Si le nombre d’URL indiqué dans le champ de texte URL **[!UICONTROL Ajouter une URL]** est supérieur à 1 000, vous ne pouvez pas sélectionner **[!UICONTROL Suivant]**. Dans ce cas, vous devez sélectionner **[!UICONTROL X]** à droite d’une ressource sélectionnée ou sur une URL ajoutée manuellement pour la supprimer de la liste d’invalidation.<br>Spécifiez des URL pour les recadrages intelligents d’images dans le modèle d’invalidation du CDN ou dans ce champ de texte **[!UICONTROL Ajouter une URL]**. |

1. Dans le coin supérieur droit de la page, sélectionnez **[!UICONTROL Suivant]**.
1. Sur la page **[!UICONTROL Invalidation du réseau de diffusion de contenu - Confirmer]**, dans la zone de liste **[!UICONTROL URL]**, apparaît une liste d’une ou plusieurs URL générées à partir du modèle d’invalidation du réseau CDN que vous avez créé précédemment et les ressources que vous venez d’ajouter.

   Par exemple, en suivant le cas de modèle d’invalidation du réseau CDN utilisé dans les étapes précédentes, supposons que vous ayez ajouté une ressource unique nommée `spinset`. Lorsque vous accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Invalidation du réseau CDN]**, les cinq URL suivantes sont générées dans l’interface utilisateur **[!UICONTROL Invalidation du réseau CDN – Confirmer]** :

   ![Invalidation du réseau de diffusion de contenu – Confirmer](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Si nécessaire, sélectionnez **X** à droite d’une URL pour supprimer cette URL du processus d’invalidation.

1. Dans le coin supérieur droit de la page, sélectionnez **[!UICONTROL Envoyer]** pour lancer le processus d’invalidation du réseau CDN.

## Résolution des erreurs d’invalidation du réseau CDN

Dans tous les cas, soit le lot entier est traité pour invalidation, soit le lot entier a échoué.

| Erreur | Explication |
| --- | --- |
| *Échec de la récupération des URL pour les ressources sélectionnées.* | Se produit dans l’un des scénarios suivants :<br>- Une configuration Dynamic Media est introuvable.<br>- Il existe une exception lors de la récupération d’un utilisateur de service par l’intermédiaire duquel la configuration Dynamic Media est lue.<br>- Le serveur de publication ou le dossier racine d’entreprise utilisé pour former les URL est absent de la configuration Dynamic Media. |
| *Certaines URL ne sont pas correctement définies. Correction et renvoi.* | Se produit si l’API d’invalidation du cache du réseau de diffusion de contenu IPS renvoie une erreur indiquant que l’URL fait référence à une autre société. Ou, si l’URL n’est pas valide conformément à la validation effectuée par l’API `cdnCacheInvalidation` IPS. |
| *Échec de l’invalidation du cache de réseau CDN.* | Se produit si la requête d’invalidation du cache de réseau CDN échoue pour une autre raison. |
| *Aucune URL entrée pour être invalidée.* | Se produit si aucune URL n’est présente sur la page **[!UICONTROL Invalidation du réseau CDN - Confirmer]** et que vous sélectionnez **[!UICONTROL Envoyer]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
