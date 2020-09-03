---
title: Invalidation du cache CDN par le biais de Contenu multimédia dynamique
description: L’annulation de la validité du contenu CDN en cache vous permet de mettre à jour rapidement les ressources diffusées par Dynamic Media, au lieu d’attendre l’expiration du cache.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: 34227ea285c48ce46488ee2256fee6c6dfeae162
workflow-type: tm+mt
source-wordcount: '1385'
ht-degree: 3%

---


# Invalidation du cache CDN par le biais de Contenu multimédia dynamique {#invalidating-cdn-cache-for-dm-assets}

Les ressources Contenu multimédia dynamique sont mises en cache par le réseau CDN (Content Diffusion Network) pour une diffusion rapide à vos clients. Cependant, lorsque vous apportez des mises à jour à ces ressources, vous souhaiterez peut-être que ces modifications prennent effet immédiatement sur votre site Web. La purge ou l’invalidation du cache CDN vous permet de mettre rapidement à jour les fichiers distribués par Contenu multimédia dynamique. Au lieu d’attendre que le cache arrive à expiration à l’aide d’une valeur TTL (durée de vie) (10 heures par défaut), vous pouvez envoyer une demande depuis l’interface utilisateur Contenu multimédia dynamique pour que le cache arrive à expiration en quelques minutes.

>[!IMPORTANT]
>
>Les étapes suivantes s’appliquent uniquement au mode Contenu multimédia dynamique - Scene7 dans AEM 6.5, Service Pack 6 (AEM 6.5.6) ou version ultérieure. Cette fonction d’invalidation du réseau de diffusion de contenu requiert également que vous utilisiez le réseau de diffusion de contenu prêt à l’emploi fourni avec AEM Contenu multimédia dynamique ; aucun autre CDN personnalisé n’est pris en charge.<br>Si vous utilisez Contenu multimédia dynamique dans AEM 6.5, Service Pack 5 (AEM 6.5.5) ou une version antérieure, suivez les étapes décrites dans la section [Invalidation du cache CDN par le biais de Contenu multimédia dynamique Classic.](/help/assets/invalidate-cdn-cache-dm-classic.md)

>Les étapes suivantes s’appliquent uniquement à Contenu multimédia dynamique dans AEM 6.5, Service Pack 5 (AEM 6.5.5) ou version antérieure.<br>Si vous utilisez Contenu multimédia dynamique dans AEM 6.5, Service Pack 6 (AEM 6.5.6) ou une version ultérieure, suivez les étapes décrites dans la section [Invalidation du cache CDN au moyen de Contenu multimédia dynamique.](/help/assets/invalidate-cdn-cache-dynamic-media.md)

See also [Caching overview in Dynamic Media](https://helpx.adobe.com/fr/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Pour invalider le contenu mis en cache sur le réseau de diffusion de contenu pour les ressources de médias dynamiques :**

*Partie 1 de 2 : Création d’un modèle d’invalidation CDN*

1. Dans AEM version 6.5.6 ou ultérieure, appuyez sur **[!UICONTROL Outils > Actifs > Invalidation CDN.]**

   ![Fonction de validation CDN](/help/assets/assets-dm/cdn-invalidation-path.png)

1. Sur la page du modèle **[!UICONTROL d’invalidation]** CDN, effectuez l’une des options suivantes en fonction de votre scénario :

   | Scénario | Option |
   | --- | --- |
   | J’ai déjà créé un modèle d’invalidation CDN dans le passé à l’aide de Contenu multimédia dynamique classique. | Le champ de texte **[!UICONTROL Créer un modèle]** est prérenseigné avec vos données de modèle. Dans ce cas, vous pouvez modifier le modèle ou passer à l’étape suivante. |
   | Je dois créer un modèle. Que puis-je entrer ? | Dans le champ de texte **[!UICONTROL Créer un modèle]** , saisissez une URL d’image (y compris les paramètres prédéfinis ou les modificateurs d’image) référençant `<ID>`l’image au lieu d’un ID d’image spécifique comme dans l’exemple suivant :<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Si le modèle contient uniquement `<ID>`, Contenu multimédia dynamique remplit `https://<publishserver_name>/is/image/<company_name>/<ID>` l’emplacement où `<publishserver_name>` est le nom de votre serveur de publication défini dans Paramètres généraux de Contenu multimédia dynamique classique ; le nom `<company_name>` est celui de la racine de votre société associée à cette instance AEM et `<ID>` est le nom des ressources sélectionnées par le biais du sélecteur de ressources à invalider.<br>Toute publication de paramètres prédéfinis/modificateurs `<ID>` est copiée en l’état dans la définition d’URL.<br>Seules les images (c&#39;est-à-dire `/is/image`) peuvent être formées automatiquement en fonction du modèle.<br>Par exemple, `/is/content/`l’ajout de fichiers tels que des vidéos ou des fichiers PDF à l’aide du sélecteur de ressources ne génère pas automatiquement d’URL. Au lieu de cela, vous devez spécifier de tels actifs soit dans le modèle d’invalidation CDN, soit vous pouvez ajouter manuellement l’URL à ces actifs dans la *partie 2 de la 2 : Définition des options* d’invalidation CDN.<br>**Exemples :**<br> Dans ce premier exemple, le modèle d’invalidation contient `<ID>` avec l’URL de ressource `/is/content`. Par exemple, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Le Contenu multimédia dynamique forme l’URL en fonction de ce paramètre, en `<ID>` étant les ressources sélectionnées par le biais du sélecteur de ressources que vous souhaitez invalider.<br>Dans ce deuxième exemple, le modèle d’invalidation contient l’URL complète de la ressource utilisée dans vos propriétés Web avec `/is/content` (sans dépendre du sélecteur de ressources). Par exemple, `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` où backpack correspond à l’ID de fichier.<br>Les formats de fichier pris en charge dans Contenu multimédia dynamique peuvent être invalidés. Les types de fichiers *non* pris en charge pour l’invalidation CDN sont Postscript, Encapsulated Postscript, Adobe Illustrator, Adobe InDesign, Microsoft Powerpoint, Microsoft Excel, Microsoft Word et Rich Text Format.<br>Lorsque vous créez le modèle, mais que vous prêtez une attention particulière à la syntaxe et aux fautes de frappe ; Contenu multimédia dynamique n’effectue aucune validation de modèle.<br>Notez que vous devez spécifier des URL pour les images de rognage intelligent dans ce modèle d’invalidation CDN ou dans le champ de texte URL **[!UICONTROL d’]** Ajoute de la *partie 2 : Définition des options d’invalidation CDN.*<br>**Important :**Chaque entrée d’un modèle d’invalidation CDN doit se trouver sur sa propre ligne.<br>*L&#39;exemple de modèle suivant est fourni à titre d&#39;illustration uniquement.* |

   ![Modèle d’invalidation CDN - Créer](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. Dans le coin supérieur droit de la page de modèle **[!UICONTROL d’invalidation du]** CDN, appuyez sur **[!UICONTROL Enregistrer]**, puis sur **[!UICONTROL OK.]**<br>   *Partie 2 de 2 : Définition des options d’invalidation CDN*
   <br>

1. Dans AEM en tant que Cloud Service, appuyez sur **[!UICONTROL Outils > Actifs > Invalidation CDN.]**

   ![Fonction de validation CDN](/help/assets/assets-dm/cdn-invalidation-path.png)

1. Sur la page Invalidation **** CDN - Détails **[!UICONTROL de l’]** Ajoute, sélectionnez les ressources pour l’invalidation CDN.

   ![Invalidation CDN - Détails de l&#39;Ajoute](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Si vous décidez de ne pas cocher les options **[!UICONTROL Invalider les paramètres d’image prédéfinis associés au fichier dans le CDN]** *et* Invalider en fonction du modèle **** , l’URL de base des fichiers sélectionnés est alors formée pour invalidation. Cette option est réservée aux images.


   | Option | Description |
   | --- | --- |
   | **[!UICONTROL Invalider les paramètres d’image prédéfinis associés à la ressource dans le réseau de diffusion de contenu]** | (Facultatif) Lorsque vous cochez cette option, les fichiers sélectionnés et toutes les URL de paramètres d’image prédéfinis associées sont automatiquement formés en vue de l’invalidation du cache.<br>Les fichiers et leurs URL prédéfinies associées sont automatiquement créés pour invalidation. Cette option fonctionne uniquement pour les fichiers d’image. |
   | **[!UICONTROL Invalidation basée sur un modèle]** | (Facultatif) Cochez cette option pour n’utiliser que le modèle défini pour la formation d’URL. |
   | **[!UICONTROL Ajouter des ressources]** | Utilisez le sélecteur de ressources pour sélectionner les fichiers que vous souhaitez invalider. Vous pouvez sélectionner des fichiers publiés ou non publiés.<br>La mise en cache sur le CDN repose sur des URL et non sur des ressources. Par conséquent, il est nécessaire que vous connaissiez les URL complètes qui se trouvent sur votre site Web. Après avoir déterminé ces URL, vous pouvez les ajouter au modèle. Vous pouvez ensuite sélectionner et ajouter ces ressources et invalider les URL en une seule étape. <br>Utilisez cette option conjointement avec les paramètres d’image prédéfinis associés au fichier **[!UICONTROL Invalider dans le CDN]** ou **[!UICONTROL Invalidation en fonction du modèle]**, ou les deux. |
   | **[!UICONTROL Ajouter une URL]** | Ajoutez ou collez manuellement des chemins d’URL complets aux fichiers Contenu multimédia dynamique dont vous souhaitez invalider le cache CDN. Utilisez cette option si vous n’avez pas créé de modèle d’invalidation CDN dans la ***partie 1 de 2 : Création d’un modèle*** d’invalidation CDN et n’avoir que quelques ressources à invalider.<br>**Important :** Chaque URL que vous ajoutez doit se trouver sur sa propre ligne.<br>Vous pouvez invalider jusqu’à 1 000 URL à la fois. Si le nombre d’URL dans le champ de texte URL **[!UICONTROL d’]** Ajoute est supérieur à 1 000, vous ne pouvez pas appuyer sur **[!UICONTROL Suivant]**. Dans ce cas, vous devez appuyer sur **[!UICONTROL X]** à droite d’une ressource sélectionnée ou sur une URL ajoutée manuellement pour la supprimer de la liste d’invalidation.<br>Notez que vous devez spécifier des URL pour les images de rognage intelligent dans le modèle d’invalidation CDN ou dans ce champ de texte URL **** Ajoute. |

1. Near the upper-right corner of the page, tap **[!UICONTROL Next.]**
1. Sur la page Invalidation **** CDN - **[!UICONTROL Confirmer]** , dans la zone de liste des **[!UICONTROL URL]** , une ou plusieurs URL sont générées à partir du modèle d’invalidation CDN que vous avez créé précédemment et des ressources que vous venez d’ajouter.

   Par exemple, à l’aide de l’exemple Modèle d’invalidation CDN qui s’affichait dans les étapes précédentes, supposons que vous ayez ajouté une ressource unique nommée `spinset`. Lorsque vous appuyez sur **[!UICONTROL Outils > Ressources > Invalidation]** CDN, les cinq URL suivantes sont générées dans l’interface utilisateur Invalidation **[!UICONTROL CDN - Confirmer]** :

   ![Invalidation CDN - Confirmer](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Si nécessaire, appuyez sur **X** à droite d’une URL pour la supprimer du processus d’invalidation.

1. Près du coin supérieur droit de la page, appuyez sur **[!UICONTROL Envoyer]** pour lancer le processus d’invalidation du réseau de diffusion de contenu.

## Résolution des erreurs d’invalidation CDN

Dans tous les cas, soit le lot entier est traité pour invalidation, soit le lot entier a échoué.

| Erreur | Explication |
| --- | --- |
| *Échec de la récupération des URL pour les ressources sélectionnées.* | Se produit si l&#39;un des scénarios suivants est satisfait :<br>- Une configuration Contenu multimédia dynamique est introuvable.<br>- Il existe une exception lors de la récupération d’un utilisateur de service par l’intermédiaire duquel la configuration Contenu multimédia dynamique est lue.<br>- Le serveur de publication ou la racine de société utilisée pour former les URL est absent de la configuration Contenu multimédia dynamique. |
| *Certaines URL ne sont pas correctement définies. Veuillez corriger et soumettre à nouveau.* | Se produit si l&#39;API d&#39;invalidation du cache CDN d&#39;IPS renvoie une erreur indiquant que l&#39;URL fait référence à une autre société ou si l&#39;URL n&#39;est pas valide conformément à la validation effectuée par l&#39;API cdnCacheInvalidation d&#39;IPS. |
| *Échec de l&#39;invalidation du cache CDN.* | Se produit si la demande d’invalidation du cache CDN échoue pour une autre raison. |
| *Aucune URL entrée n&#39;a été invalidée.* | Se produit si aucune URL n’est présente dans la page Invalidation **** CDN - **[!UICONTROL Confirmer]** et que vous appuyez sur **[!UICONTROL Envoyer.]** |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
