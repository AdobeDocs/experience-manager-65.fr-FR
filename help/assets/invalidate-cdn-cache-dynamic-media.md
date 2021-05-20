---
title: Invalidation du cache du réseau CDN par le biais de Dynamic Media
description: L’invalidation du contenu de réseau de diffusion de continu (CDN) en cache vous permet de mettre à jour rapidement les ressources diffusées par Dynamic Media, au lieu d’attendre l’expiration du cache.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
role: Business Practitioner, Administrator
exl-id: 23d3c274-0736-49f7-8d44-a56a55cfd06d
feature: Cache CDN
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '1366'
ht-degree: 55%

---

# Invalidation du cache du réseau CDN par le biais de Dynamic Media {#invalidating-cdn-cache-for-dm-assets}

Les ressources Dynamic Media sont mises en cache par le réseau de diffusion de contenu (CDN) pour une diffusion rapide à vos clients. Cependant, lorsque vous apportez des mises à jour à ces ressources, vous souhaitez que ces modifications prennent effet immédiatement sur votre site web. La purge ou l’invalidation du cache du réseau CDN vous permet de mettre rapidement à jour les ressources distribuées par Dynamic Media. Au lieu d’attendre que le cache arrive à expiration à l’aide d’une valeur TTL (durée de vie) (la valeur par défaut est de dix heures), vous pouvez envoyer une requête depuis Dynamic Media pour que le cache arrive à expiration en quelques minutes.

>[!NOTE]
>
>Cette fonctionnalité nécessite l’utilisation du réseau de diffusion de contenu prêt à l’emploi fourni avec Adobe Experience Manager Dynamic Media. Aucun autre réseau de diffusion de contenu personnalisé n’est pris en charge avec cette fonctionnalité.

>[!IMPORTANT]
>
>Les étapes suivantes s’appliquent uniquement au mode Dynamic Media - Scene7 dans Adobe Experience Manager 6.5, Service Pack 6 (Experience Manager 6.5.6) ou version ultérieure. Cette fonction d’invalidation du réseau de diffusion de contenu nécessite également l’utilisation du réseau de diffusion de contenu prêt à l’emploi fourni avec Dynamic Media Experience Manager ; tout autre réseau de diffusion de contenu personnalisé n’est pas pris en charge.<br>Si vous utilisez Dynamic Media dans Experience Manager 6.5, Service Pack 5 (Experience Manager 6.5.5) ou une version antérieure, suivez les étapes décrites dans  [Invalidation du cache CDN au moyen de Dynamic Media Classic.](/help/assets/invalidate-cdn-cache-dm-classic.md)

Voir aussi [Présentation de la mise en cache dans Dynamic Media](https://helpx.adobe.com/fr/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Pour invalider le contenu mis en cache du réseau de diffusion de contenu pour les ressources Dynamic Media :**

*Partie 1 de 2 : création d’un modèle d’invalidation du réseau CDN*

1. Dans Experience Manager 6.5.6 ou version ultérieure, appuyez sur **[!UICONTROL Outils > Ressources > Invalidation du réseau de diffusion de contenu.]**

   ![Fonction de validation du réseau CDN](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. Sur la page **[!UICONTROL Modèle d’invalidation du réseau de diffusion de contenu]**, effectuez l’une des opérations suivantes en fonction de votre scénario :

   | Scénario | Option |
   | --- | --- |
   | J’ai déjà créé un modèle d’invalidation du réseau CDN dans le passé à l’aide de Dynamic Media Classic. | Le champ de texte **[!UICONTROL Créer un modèle]** est prérenseigné avec vos données de modèle. Dans ce cas, vous pouvez modifier le modèle ou passer à l’étape suivante. |
   | Je dois créer un modèle. Que dois-je entrer ? | Dans le champ de texte **[!UICONTROL Créer un modèle]** , saisissez une URL d’image (y compris des paramètres d’image prédéfinis ou des modificateurs) référençant `<ID>`, au lieu d’un ID d’image spécifique comme dans l’exemple suivant :<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Si le modèle contient uniquement `<ID>`, Dynamic Media renseigne `https://<publishserver_name>/is/image/<company_name>/<ID>` où `<publishserver_name>` est le nom de votre serveur de publication défini dans les paramètres généraux dans Dynamic Media Classic . `<company_name>` est le nom de la racine de votre société associée à cette instance de Experience Manager et `<ID>` est les ressources sélectionnées par le biais du sélecteur de ressources à invalider.<br>Tout paramètre prédéfini/modificateur placé après `<ID>` est copié en l’état dans la définition d’URL.<br>Seules les images (c’est-à-dire  `/is/image` ) peuvent être formées automatiquement en fonction du modèle.<br>Pour `/is/content/`, l’ajout de ressources telles que des vidéos ou des fichiers PDF à l’aide du sélecteur de ressources ne génère pas automatiquement d’URL. Au lieu de cela, vous devez spécifier ces ressources dans le modèle d’invalidation du réseau CDN ou vous pouvez ajouter manuellement l’URL à ces ressources dans *Partie 2 de 2 : définition des options d’invalidation du réseau CDN*.<br>**Exemples :**<br> Dans ce premier exemple, le modèle d’invalidation contient `<ID>` avec l’URL de ressource `/is/content`. Par exemple, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Media forme l’URL en fonction de ce chemin d’accès, `<ID>` correspondant aux ressources sélectionnées par le biais du sélecteur de ressources que vous souhaitez invalider.<br>Dans ce deuxième exemple, le modèle d’invalidation contient l’URL complète de la ressource utilisée dans vos propriétés web avec `/is/content` (indépendamment du sélecteur de ressources). Par exemple, `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` où backpack correspond à l’ID de ressource.<br>Les formats de ressources pris en charge dans Dynamic Media peuvent être invalidés. Les types de fichiers de ressources *non* pris en charge pour l’invalidation du réseau CDN sont les suivants : PostScript®, Encapsulated PostScript®, Adobe Illustrator, Adobe InDesign, Microsoft PowerPoint, Microsoft Excel, Microsoft Word et Rich Text Format.<br>Lorsque vous créez le modèle, faites très attention à la syntaxe et aux fautes de frappe ; Dynamic Media n’effectue aucune validation de modèle.<br>Spécifiez les URL pour les recadrages intelligents d’image dans ce modèle d’invalidation du réseau de diffusion de contenu ou dans le champ  **[!UICONTROL Ajouter une]** URL de texte dans  *Partie 2 : Définition des options d’invalidation du réseau CDN.*<br>**Important :** Chaque entrée d’un modèle d’invalidation du réseau CDN doit se trouver sur sa propre ligne.<br>*L’exemple de modèle suivant est fourni à titre d’illustration uniquement.* |

   ![Modèle d’invalidation du réseau CDN – Créer](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. Dans le coin supérieur droit de la page **[!UICONTROL Modèle d’invalidation du réseau de diffusion de contenu]**, appuyez sur **[!UICONTROL Enregistrer]**, puis sur **[!UICONTROL OK.]**<br>

   *Partie 2 de 2 : définition des options d’invalidation du réseau CDN*
   <br>

1. Dans Experience Manager en tant que Cloud Service, appuyez sur **[!UICONTROL Outils > Ressources > Invalidation du réseau de diffusion de contenu.]**

   ![Fonction de validation du réseau CDN](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. Sur la page **[!UICONTROL Invalidation du réseau de diffusion de contenu - Ajouter des détails]** , sélectionnez les ressources pour l’invalidation du réseau de diffusion de contenu.

   ![Invalidation du réseau de diffusion de contenu – Ajouter des détails](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Si vous décidez de ne pas cocher les options **[!UICONTROL Invalider les paramètres d’image prédéfinis associés à la ressource dans le réseau de diffusion de contenu]** *et* **[!UICONTROL Invalider en fonction d’un modèle]**, l’URL de base des ressources sélectionnées est alors formée pour invalidation. Cette option est réservée aux images.


   | Option | Description |
   | --- | --- |
   | **[!UICONTROL Invalider les paramètres d’image prédéfinis associés à la ressource dans le réseau de diffusion de contenu]** | (Facultatif) Lorsque vous cochez cette option, les ressources sélectionnées et toutes les URL de paramètres d’image prédéfinis associées sont automatiquement formées en vue de l’invalidation du cache.<br>Les ressources et leurs URL prédéfinies associées sont automatiquement formées en vue de l’invalidation. Cette option fonctionne uniquement pour les ressources d’image. |
   | **[!UICONTROL Invalidation en fonction d’un modèle]** | (Facultatif) Cochez cette option afin de n’utiliser que le modèle défini pour la formation d’URL. |
   | **[!UICONTROL Ajouter des ressources]** | Utilisez le sélecteur de ressources pour sélectionner les ressources que vous souhaitez invalider. Vous pouvez sélectionner des ressources publiées ou non publiées.<br>La mise en cache sur le réseau CDN repose sur des URL et non sur des ressources. Il est donc nécessaire de connaître les URL complètes qui se trouvent sur votre site web. Après avoir déterminé ces URL, vous pouvez les ajouter au modèle. Vous pouvez ensuite sélectionner et ajouter ces ressources et invalider les URL en une seule étape. <br>Utilisez cette option avec  **[!UICONTROL Invalider les paramètres d’image prédéfinis associés à la ressource dans le réseau de diffusion de contenu]** ou  **[!UICONTROL Invalidation en fonction du modèle]**, ou les deux. |
   | **[!UICONTROL Ajouter une URL]** | Ajoutez ou collez manuellement des chemins d’URL complets aux ressources Dynamic Media dont vous souhaitez invalider le cache de réseau CDN. Utilisez cette option si vous n’avez pas créé de modèle d’invalidation du réseau CDN dans ***Partie 1 de 2 : création d’un modèle d’invalidation du réseau CDN*** et n’avez que quelques ressources à invalider.<br>**Important :** Chaque URL que vous ajoutez doit se trouver sur sa propre ligne.<br>Vous pouvez invalider jusqu’à 1 000 URL à la fois. Si le nombre d’URL indiqué dans le champ de texte URL **[!UICONTROL Ajouter une URL]** est supérieur à 1 000, vous ne pouvez pas appuyer sur **[!UICONTROL Suivant]**. Dans ce cas, vous devez appuyer sur **[!UICONTROL X]** à droite d’une ressource sélectionnée ou sur une URL ajoutée manuellement pour la supprimer de la liste d’invalidation.<br>Spécifiez les URL pour les recadrages intelligents d’image dans le modèle d’invalidation du réseau CDN ou dans ce champ  **[!UICONTROL Ajouter]** une URL. |

1. Dans le coin supérieur droit de la page, appuyez sur **[!UICONTROL Suivant]**.
1. Sur la page **[!UICONTROL Invalidation du réseau de diffusion de contenu - Confirmer]**, dans la zone de liste **[!UICONTROL URL]**, vous pouvez voir une liste d’une ou de plusieurs URL générées à partir du modèle d’invalidation du réseau de diffusion de contenu que vous avez créé précédemment et des ressources que vous venez d’ajouter.

   Par exemple, en suivant l’exemple de modèle d’invalidation du réseau CDN utilisé dans les étapes précédentes, supposons que vous ayez ajouté une ressource unique nommée `spinset`. Lorsque vous appuyez sur **[!UICONTROL Outils > Ressources > Invalidation du réseau de diffusion de contenu]**, les cinq URL suivantes sont générées dans l’interface utilisateur **[!UICONTROL Invalidation du réseau de diffusion de contenu - Confirmer]** :

   ![Invalidation du réseau de diffusion de contenu – Confirmer](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Si nécessaire, appuyez sur **X** à droite d’une URL pour supprimer cette URL du processus d’invalidation.

1. Dans le coin supérieur droit de la page, appuyez sur **[!UICONTROL Envoyer]** pour lancer le processus d’invalidation du réseau CDN.

## Résolution des erreurs d’invalidation du réseau CDN

Dans tous les cas, soit le lot entier est traité pour invalidation, soit le lot entier a échoué.

| Erreur | Explication |
| --- | --- |
| *Échec de la récupération des URL des ressources sélectionnées.* | Se produit si l’un des scénarios suivants est satisfait :<br>- Une configuration Dynamic Media est introuvable.<br>- Il existe une exception lors de la récupération d’un utilisateur de service par l’intermédiaire duquel la configuration Dynamic Media est lue.<br>- Le serveur de publication ou la racine d’entreprise utilisée pour former les URL est absent de la configuration Dynamic Media. |
| *Certaines URL ne sont pas correctement définies. Corriger et renvoyer.* | Se produit si l’API d’invalidation du cache du réseau de diffusion de contenu IPS renvoie une erreur indiquant que l’URL fait référence à une autre société. Ou, si l’URL n’est pas valide conformément à la validation effectuée par l’API `cdnCacheInvalidation` IPS. |
| *Échec de l’invalidation du cache de réseau CDN.* | Se produit si la requête d’invalidation du cache de réseau CDN échoue pour une autre raison. |
| *Aucune URL entrée à invalider.* | Se produit si aucune URL n’est présente dans la page **[!UICONTROL Invalidation du réseau de diffusion de contenu - Confirmer]** et que vous appuyez sur **[!UICONTROL Envoyer.]** |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
